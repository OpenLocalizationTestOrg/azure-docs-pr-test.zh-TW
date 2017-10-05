---
title: "使用 Draft 搭配 Azure Container Service 與 Azure Container Registry | Microsoft Docs"
description: "建立 ACS Kubernetes 叢集和 Azure Container Registry，可使用 Draft 在 Azure 中建立第一個應用程式。"
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, Draft, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7e3ea461145571753a1a6d768b52118dcbfb507
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="6b24b-104">使用 Draft 搭配 Azure Container Service 與 Azure Container Registry，可將應用程式建置及部署至 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6b24b-104">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

<span data-ttu-id="6b24b-105">[Draft](https://aka.ms/draft) 是新的開放原始碼工具，可讓您輕鬆地開發以容器作為基礎的應用程式，並將其部署至 Kubernetes 叢集，而無需深入了解 Docker 和 Kubernetes，或甚至進行安裝。</span><span class="sxs-lookup"><span data-stu-id="6b24b-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="6b24b-106">使用諸如 Draft 等工具可讓您和小組專注於使用 Kubernetes 來建置應用程式，無須投入過多注意力在基礎結構。</span><span class="sxs-lookup"><span data-stu-id="6b24b-106">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="6b24b-107">您可以使用 Draft 搭配任何 Docker 映像登錄與任何 Kubernetes 叢集，包括本機。</span><span class="sxs-lookup"><span data-stu-id="6b24b-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="6b24b-108">本教學課程會示範如何使用 ACS 搭配 Kubernetes、ACR 和 Azure DNS，使用 Draft 來建立即時的 CI/CD 開發人員管線。</span><span class="sxs-lookup"><span data-stu-id="6b24b-108">This tutorial shows how to use ACS with Kubernetes, ACR, and Azure DNS to create a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="6b24b-109">建立 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6b24b-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="6b24b-110">您可以輕鬆地[建立新的 Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md)，步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b24b-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="6b24b-111">建立 Azure 資源群組可在 ACS 中管理您的 ACR 登錄和 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="6b24b-111">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="6b24b-112">使用 [az acr create](/cli/azure/acr#create) 來建立 ACR 映像登錄</span><span class="sxs-lookup"><span data-stu-id="6b24b-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="6b24b-113">使用 Kubernetes 建立 Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="6b24b-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="6b24b-114">現在您準備好使用 [az acs create](/cli/azure/acs#create)，利用 Kubernetes 作為 `--orchestrator-type` 值來建立 ACS 叢集。</span><span class="sxs-lookup"><span data-stu-id="6b24b-114">Now you're ready to use [az acs create](/cli/azure/acs#create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="6b24b-115">因為 Kubernetes 不是預設的 Orchestrator 類型，請確定您使用 `--orchestrator-type kubernetes` 參數。</span><span class="sxs-lookup"><span data-stu-id="6b24b-115">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="6b24b-116">成功時的輸出大致如下所示。</span><span class="sxs-lookup"><span data-stu-id="6b24b-116">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

<span data-ttu-id="6b24b-117">現在，您有一個叢集，可以使用 [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) 命令將認證匯入。</span><span class="sxs-lookup"><span data-stu-id="6b24b-117">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="6b24b-118">現在您有叢集的本機組態檔，這是 Helm 和 Draft 完成其工作所需要的項目。</span><span class="sxs-lookup"><span data-stu-id="6b24b-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="6b24b-119">安裝及設定草稿</span><span class="sxs-lookup"><span data-stu-id="6b24b-119">Install and configure draft</span></span>
<span data-ttu-id="6b24b-120">Draft 的安裝指示位於 [Draft 存放庫](https://github.com/Azure/draft/blob/master/docs/install.md)。</span><span class="sxs-lookup"><span data-stu-id="6b24b-120">The installation instructions for Draft are in the [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="6b24b-121">它們相對而言較為簡單，但需要一些設定，因為它取決於 [Helm](https://aka.ms/helm) 來建立 Helm，並加以部署到 Kubernetes 叢集中。</span><span class="sxs-lookup"><span data-stu-id="6b24b-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) to create and deploy a Helm chart into the Kubernetes cluster.</span></span>

1. <span data-ttu-id="6b24b-122">[下載並安裝 Helm](https://aka.ms/helm#install)。</span><span class="sxs-lookup"><span data-stu-id="6b24b-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="6b24b-123">使用 Helm 來搜尋及安裝 `stable/traefik`，並輸入控制器以啟用您組建的輸入要求。</span><span class="sxs-lookup"><span data-stu-id="6b24b-123">Use Helm to search for and install `stable/traefik`, and ingress controller to enable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="6b24b-124">現在，請在 `ingress` 控制站上設定監看，以在部署外部 IP 值時加以擷取。</span><span class="sxs-lookup"><span data-stu-id="6b24b-124">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="6b24b-125">此 IP 位址會是下一節中[對應到您部署網域](#wire-up-deployment-domain)的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6b24b-125">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="6b24b-126">在此案例中，部署網域的外部 IP 是 `13.64.108.240`。</span><span class="sxs-lookup"><span data-stu-id="6b24b-126">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="6b24b-127">現在您可以將網域對應至該 IP。</span><span class="sxs-lookup"><span data-stu-id="6b24b-127">Now you can map your domain to that IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="6b24b-128">接通部署網域</span><span class="sxs-lookup"><span data-stu-id="6b24b-128">Wire up deployment domain</span></span>

<span data-ttu-id="6b24b-129">Draft 會針對其所建立的每個 Helm 圖表，以及您在使用每個應用程式建立一個版本。</span><span class="sxs-lookup"><span data-stu-id="6b24b-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="6b24b-130">每個版本都會取得一個已產生的名稱，以在您所控制的根_部署網域_上作為_子網域_草稿。</span><span class="sxs-lookup"><span data-stu-id="6b24b-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="6b24b-131">(在此範例中，我們使用 `squillace.io` 作為部署網域。)若要啟用此子網域行為，您必須針對部署網域，在 DNS 項目中建立 `'*'` 的 A 記錄，以便每個產生的子網域會路由傳送至 Kubernetes 叢集的輸入控制器。</span><span class="sxs-lookup"><span data-stu-id="6b24b-131">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="6b24b-132">您自己的網域提供者都有其各自的方法可指派 DNS 伺服器；若要[將您的 nameservers 網域委派給 Azure DNS](../../dns/dns-delegate-domain-azure-dns.md)，請採取下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6b24b-132">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="6b24b-133">建立您區域的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6b24b-133">Create a resource group for your zone.</span></span>
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. <span data-ttu-id="6b24b-134">建立您網域的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="6b24b-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="6b24b-135">使用 [az network dns zone create](/cli/azure/network/dns/zone#create) 命令來取得 nameservers，將 DNS 控制項委派給網域的 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="6b24b-135">Use the [az network dns zone create](/cli/azure/network/dns/zone#create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. <span data-ttu-id="6b24b-136">將您所取得的 DNS 伺服器新增至您部署網域的網域提供者，可讓您視需要使用 Azure DNS 重新指向您的網域。</span><span class="sxs-lookup"><span data-stu-id="6b24b-136">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span>
4. <span data-ttu-id="6b24b-137">建立部署網域的 A 記錄集項目，從上一節的步驟 2 中對應至 `ingress` IP。</span><span class="sxs-lookup"><span data-stu-id="6b24b-137">Create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="6b24b-138">輸出看起來會類似於：</span><span class="sxs-lookup"><span data-stu-id="6b24b-138">The output looks something like:</span></span>
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. <span data-ttu-id="6b24b-139">設定 Draft 以使用您的登錄，並針對它所建立的每個 Helm 圖表建立子網域。</span><span class="sxs-lookup"><span data-stu-id="6b24b-139">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="6b24b-140">若要設定 Draft，您需要：</span><span class="sxs-lookup"><span data-stu-id="6b24b-140">To configure Draft, you need:</span></span>
  - <span data-ttu-id="6b24b-141">您的 Azure Container Registry 名稱 (在此範例中為 `draft`)</span><span class="sxs-lookup"><span data-stu-id="6b24b-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="6b24b-142">您的登錄機碼或密碼，從 `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`。</span><span class="sxs-lookup"><span data-stu-id="6b24b-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="6b24b-143">您已設定為對應至 Kubernetes 輸入外部 IP 位址的根部署網域 (這裡為 `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="6b24b-143">the root deployment domain that you have configured to map to the Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="6b24b-144">呼叫 `draft init`，而設定程序會提示您輸入上述的值。</span><span class="sxs-lookup"><span data-stu-id="6b24b-144">Call `draft init` and the configuration process prompts you for the values above.</span></span> <span data-ttu-id="6b24b-145">第一次執行此程序時，它看起來如下所示。</span><span class="sxs-lookup"><span data-stu-id="6b24b-145">The process looks something like the following the first time you run it.</span></span>
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order to install Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="6b24b-146">您現在已準備好要部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b24b-146">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="6b24b-147">建置和部署應用程式</span><span class="sxs-lookup"><span data-stu-id="6b24b-147">Build and deploy an application</span></span>

<span data-ttu-id="6b24b-148">在 Draft 存放庫中，有[六個簡單的範例應用程式](https://github.com/Azure/draft/tree/master/examples)。</span><span class="sxs-lookup"><span data-stu-id="6b24b-148">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="6b24b-149">複製存放庫，讓我們使用 [Python 範例](https://github.com/Azure/draft/tree/master/examples/python)。</span><span class="sxs-lookup"><span data-stu-id="6b24b-149">Clone the repo and let's use the [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="6b24b-150">變更為範例/Python 目錄，並輸入 `draft create` 可建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b24b-150">Change into the examples/Python directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="6b24b-151">它看起來會如下範例所示。</span><span class="sxs-lookup"><span data-stu-id="6b24b-151">It should look like the following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready to sail
```

<span data-ttu-id="6b24b-152">輸出包含 Dockerfile 和 Helm 圖表。</span><span class="sxs-lookup"><span data-stu-id="6b24b-152">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="6b24b-153">若要建置和部署，您只要輸入 `draft up`。</span><span class="sxs-lookup"><span data-stu-id="6b24b-153">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="6b24b-154">輸出會很廣泛，但會如下列範例開始。</span><span class="sxs-lookup"><span data-stu-id="6b24b-154">The output is extensive, but begins like the following example.</span></span>
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

<span data-ttu-id="6b24b-155">且在成功時會以類似下列的範例結束。</span><span class="sxs-lookup"><span data-stu-id="6b24b-155">and when successful ends with something similar to the following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying to Kubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io to access your application

Watching local files for changes...
```

<span data-ttu-id="6b24b-156">無論圖表的名稱為何，您可以現在 `curl http://gangly-bronco.squillace.io` 接收回覆，`Hello World!`。</span><span class="sxs-lookup"><span data-stu-id="6b24b-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` to receive the reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b24b-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b24b-157">Next steps</span></span>

<span data-ttu-id="6b24b-158">您有了 ACS Kubernetes 叢集之後，可以使用 [Azure Container Registry](../../container-registry/container-registry-intro.md) 進行調查，建立更多這種案例與不同的部署。</span><span class="sxs-lookup"><span data-stu-id="6b24b-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="6b24b-159">例如，您可以建立 draft._basedomain.toplevel_ 網域 DNS 記錄集，可針對特定 ACS 部署，控制項目移出更深入的子網域。</span><span class="sxs-lookup"><span data-stu-id="6b24b-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






