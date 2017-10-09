---
title: "Azure 容器服務與 Azure 容器登錄中的草稿 aaaUse |Microsoft 文件"
description: "ACS Kubernetes 叢集和 Azure 容器登錄中 toocreate 第一個應用程式在 Azure 中建立與草稿。"
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
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="2ee20-104">使用 Azure 容器服務和 Azure 容器登錄 toobuild 草稿和部署應用程式 tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="2ee20-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="2ee20-105">[草稿](https://aka.ms/draft)是一種新的開放原始碼工具，可讓您輕鬆 toodevelop 容器基礎的應用程式和部署它們 tooKubernetes 叢集而不需要了解太多 Docker 和 Kubernetes-，或甚至進行安裝。</span><span class="sxs-lookup"><span data-stu-id="2ee20-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="2ee20-106">使用草稿等工具可讓您和小組焦點建置 Kubernetes hello 應用程式、 未支付盡注意 tooinfrastructure。</span><span class="sxs-lookup"><span data-stu-id="2ee20-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="2ee20-107">您可以使用 Draft 搭配任何 Docker 映像登錄與任何 Kubernetes 叢集，包括本機。</span><span class="sxs-lookup"><span data-stu-id="2ee20-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="2ee20-108">本教學課程會示範如何使用 Kubernetes、 ACR 及 Azure DNS toocreate toouse ACS 即時 CI/CD 開發人員管線使用草稿。</span><span class="sxs-lookup"><span data-stu-id="2ee20-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="2ee20-109">建立 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="2ee20-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="2ee20-110">您可以輕鬆地[建立新的 Azure 容器登錄](../../container-registry/container-registry-get-started-azure-cli.md)，但 hello 步驟，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ee20-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="2ee20-111">在 ACS 中建立 Azure 資源群組 toomanage ACR 登錄和 hello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="2ee20-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="2ee20-112">使用 [az acr create](/cli/azure/acr#create) 來建立 ACR 映像登錄</span><span class="sxs-lookup"><span data-stu-id="2ee20-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="2ee20-113">使用 Kubernetes 建立 Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="2ee20-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="2ee20-114">您現在已經準備好 toouse [az acs 建立](/cli/azure/acs#create)toocreate ACS 叢集 Kubernetes 用作 hello`--orchestrator-type`值。</span><span class="sxs-lookup"><span data-stu-id="2ee20-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="2ee20-115">由於 Kubernetes 不 hello 預設 orchestrator 類型，因此請務必使用 hello`--orchestrator-type kubernetes`切換。</span><span class="sxs-lookup"><span data-stu-id="2ee20-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="2ee20-116">成功時的 hello 輸出看起來類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="2ee20-116">hello output when successful looks similar toohello following.</span></span>

```json
waiting for AAD role toopropagate.done
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

<span data-ttu-id="2ee20-117">現在，您有一個叢集時，您可以使用匯入 hello 認證 hello [az acs kubernetes 取得認證](/cli/azure/acs/kubernetes#get-credentials)命令。</span><span class="sxs-lookup"><span data-stu-id="2ee20-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="2ee20-118">現在您有本機組態檔，為您的叢集，也就是哪些頭盔和草稿需要 tooget 完成其工作。</span><span class="sxs-lookup"><span data-stu-id="2ee20-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="2ee20-119">安裝及設定草稿</span><span class="sxs-lookup"><span data-stu-id="2ee20-119">Install and configure draft</span></span>
<span data-ttu-id="2ee20-120">hello 安裝指示草稿位於 hello[草稿儲存機制](https://github.com/Azure/draft/blob/master/docs/install.md)。</span><span class="sxs-lookup"><span data-stu-id="2ee20-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="2ee20-121">它們相對而言較為簡單，但需要一些設定，因為它相依於[頭盔](https://aka.ms/helm)toocreate 和到 hello Kubernetes 叢集中部署頭盔圖表。</span><span class="sxs-lookup"><span data-stu-id="2ee20-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="2ee20-122">[下載並安裝 Helm](https://aka.ms/helm#install)。</span><span class="sxs-lookup"><span data-stu-id="2ee20-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="2ee20-123">使用如頭盔 toosearch 並安裝`stable/traefik`，並輸入控制器 tooenable 輸入您的組建要求。</span><span class="sxs-lookup"><span data-stu-id="2ee20-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="2ee20-124">現在設定 hello 監看式`ingress`控制器 toocapture hello 外部 IP 值在部署時。</span><span class="sxs-lookup"><span data-stu-id="2ee20-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="2ee20-125">此 IP 位址會是一個 hello[對應 tooyour 部署網域](#wire-up-deployment-domain)hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="2ee20-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="2ee20-126">在此情況下，在 hello 部署網域是 hello 外部 IP `13.64.108.240`。</span><span class="sxs-lookup"><span data-stu-id="2ee20-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="2ee20-127">現在您可以對應您的網域 toothat IP。</span><span class="sxs-lookup"><span data-stu-id="2ee20-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="2ee20-128">接通部署網域</span><span class="sxs-lookup"><span data-stu-id="2ee20-128">Wire up deployment domain</span></span>

<span data-ttu-id="2ee20-129">Draft 會針對其所建立的每個 Helm 圖表，以及您在使用每個應用程式建立一個版本。</span><span class="sxs-lookup"><span data-stu-id="2ee20-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="2ee20-130">每一項取得產生的名稱，以供做為草稿_子網域_hello 根之上_部署網域_您所控制。</span><span class="sxs-lookup"><span data-stu-id="2ee20-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="2ee20-131">(在此範例中，我們使用`squillace.io`為 hello 部署網域。) tooenable 這子網域的行為，您必須建立 A 記錄`'*'`部署網域的 DNS 項目，以便每個產生的子網域是路由的 toohello Kubernetes叢集的輸入控制器。</span><span class="sxs-lookup"><span data-stu-id="2ee20-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="2ee20-132">網域提供者具有自己的方式 tooassign DNS 伺服器。太[委派 DNS 您網域 nameservers tooAzure](../../dns/dns-delegate-domain-azure-dns.md)，採取下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ee20-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="2ee20-133">建立您區域的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2ee20-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="2ee20-134">建立您網域的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="2ee20-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="2ee20-135">使用 hello [az 網路 dns 區域建立](/cli/azure/network/dns/zone#create)tooobtain hello nameservers toodelegate DNS 控制 tooAzure DNS 網域的命令。</span><span class="sxs-lookup"><span data-stu-id="2ee20-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
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
3. <span data-ttu-id="2ee20-136">新增您有 toohello 網域提供者，您部署的網域，可讓您 toouse Azure DNS toorepoint 您的網域，您想要的 hello DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2ee20-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="2ee20-137">建立 A 記錄集項目，針對您部署網域對應 toohello `ingress` hello 上一節的步驟 2 中的 IP。</span><span class="sxs-lookup"><span data-stu-id="2ee20-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="2ee20-138">hello 輸出看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="2ee20-138">hello output looks something like:</span></span>
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

5. <span data-ttu-id="2ee20-139">您的登錄設定草稿 toouse 並建立它會建立每個頭盔圖表的子網域。</span><span class="sxs-lookup"><span data-stu-id="2ee20-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="2ee20-140">tooconfigure 草稿，您需要：</span><span class="sxs-lookup"><span data-stu-id="2ee20-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="2ee20-141">您的 Azure Container Registry 名稱 (在此範例中為 `draft`)</span><span class="sxs-lookup"><span data-stu-id="2ee20-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="2ee20-142">您的登錄機碼或密碼，從 `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`。</span><span class="sxs-lookup"><span data-stu-id="2ee20-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="2ee20-143">您已設定 toomap toohello Kubernetes ingress 外部 IP 位址的 hello 根部署網域 (在這裡， `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="2ee20-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="2ee20-144">呼叫`draft init`和 hello 設定程序會提示您輸入 hello 上述的值。</span><span class="sxs-lookup"><span data-stu-id="2ee20-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="2ee20-145">hello 程序看起來像下列 hello hello 第一次您執行此程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ee20-145">hello process looks something like hello following hello first time you run it.</span></span>
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

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="2ee20-146">您現在已經準備好 toodeploy 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ee20-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="2ee20-147">建置和部署應用程式</span><span class="sxs-lookup"><span data-stu-id="2ee20-147">Build and deploy an application</span></span>

<span data-ttu-id="2ee20-148">在 hello 草稿儲存機制是[六個簡單的範例應用程式](https://github.com/Azure/draft/tree/master/examples)。</span><span class="sxs-lookup"><span data-stu-id="2ee20-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="2ee20-149">複製 hello 儲存機制，讓我們使用 hello [Python 範例](https://github.com/Azure/draft/tree/master/examples/python)。</span><span class="sxs-lookup"><span data-stu-id="2ee20-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="2ee20-150">將變更 hello 範例/Python 目錄，然後輸入`draft create`toobuild hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ee20-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="2ee20-151">它看起來應該像下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="2ee20-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="2ee20-152">hello 輸出包含了 Dockerfile 並頭盔圖表。</span><span class="sxs-lookup"><span data-stu-id="2ee20-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="2ee20-153">toobuild 和部署，您只需要輸入`draft up`。</span><span class="sxs-lookup"><span data-stu-id="2ee20-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="2ee20-154">hello 輸出很大，但類似下列範例中的 hello 開始。</span><span class="sxs-lookup"><span data-stu-id="2ee20-154">hello output is extensive, but begins like hello following example.</span></span>
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

<span data-ttu-id="2ee20-155">與時機與下列範例類似 toohello 成功結束。</span><span class="sxs-lookup"><span data-stu-id="2ee20-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="2ee20-156">圖表的名稱為任何內容，您可以現在`curl http://gangly-bronco.squillace.io`tooreceive hello 回覆， `Hello World!`。</span><span class="sxs-lookup"><span data-stu-id="2ee20-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ee20-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ee20-157">Next steps</span></span>

<span data-ttu-id="2ee20-158">有 ACS Kubernetes 叢集之後，您可以調查使用[Azure 容器登錄中](../../container-registry/container-registry-intro.md)toocreate 這種情況的詳細和不同的部署。</span><span class="sxs-lookup"><span data-stu-id="2ee20-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="2ee20-159">例如，您可以建立 draft._basedomain.toplevel_ 網域 DNS 記錄集，可針對特定 ACS 部署，控制項目移出更深入的子網域。</span><span class="sxs-lookup"><span data-stu-id="2ee20-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






