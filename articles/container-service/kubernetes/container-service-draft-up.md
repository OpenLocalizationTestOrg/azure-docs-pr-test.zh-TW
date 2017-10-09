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
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>使用 Azure 容器服務和 Azure 容器登錄 toobuild 草稿和部署應用程式 tooKubernetes

[草稿](https://aka.ms/draft)是一種新的開放原始碼工具，可讓您輕鬆 toodevelop 容器基礎的應用程式和部署它們 tooKubernetes 叢集而不需要了解太多 Docker 和 Kubernetes-，或甚至進行安裝。 使用草稿等工具可讓您和小組焦點建置 Kubernetes hello 應用程式、 未支付盡注意 tooinfrastructure。

您可以使用 Draft 搭配任何 Docker 映像登錄與任何 Kubernetes 叢集，包括本機。 本教學課程會示範如何使用 Kubernetes、 ACR 及 Azure DNS toocreate toouse ACS 即時 CI/CD 開發人員管線使用草稿。


## <a name="create-an-azure-container-registry"></a>建立 Azure Container Registry
您可以輕鬆地[建立新的 Azure 容器登錄](../../container-registry/container-registry-get-started-azure-cli.md)，但 hello 步驟，如下所示：

1. 在 ACS 中建立 Azure 資源群組 toomanage ACR 登錄和 hello Kubernetes 叢集。
      ```azurecli
      az group create --name draft --location eastus
      ```

2. 使用 [az acr create](/cli/azure/acr#create) 來建立 ACR 映像登錄
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>使用 Kubernetes 建立 Azure Container Service

您現在已經準備好 toouse [az acs 建立](/cli/azure/acs#create)toocreate ACS 叢集 Kubernetes 用作 hello`--orchestrator-type`值。
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> 由於 Kubernetes 不 hello 預設 orchestrator 類型，因此請務必使用 hello`--orchestrator-type kubernetes`切換。

成功時的 hello 輸出看起來類似 toohello 下列。

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

現在，您有一個叢集時，您可以使用匯入 hello 認證 hello [az acs kubernetes 取得認證](/cli/azure/acs/kubernetes#get-credentials)命令。 現在您有本機組態檔，為您的叢集，也就是哪些頭盔和草稿需要 tooget 完成其工作。

## <a name="install-and-configure-draft"></a>安裝及設定草稿
hello 安裝指示草稿位於 hello[草稿儲存機制](https://github.com/Azure/draft/blob/master/docs/install.md)。 它們相對而言較為簡單，但需要一些設定，因為它相依於[頭盔](https://aka.ms/helm)toocreate 和到 hello Kubernetes 叢集中部署頭盔圖表。

1. [下載並安裝 Helm](https://aka.ms/helm#install)。
2. 使用如頭盔 toosearch 並安裝`stable/traefik`，並輸入控制器 tooenable 輸入您的組建要求。
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    現在設定 hello 監看式`ingress`控制器 toocapture hello 外部 IP 值在部署時。 此 IP 位址會是一個 hello[對應 tooyour 部署網域](#wire-up-deployment-domain)hello 下一節。

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    在此情況下，在 hello 部署網域是 hello 外部 IP `13.64.108.240`。 現在您可以對應您的網域 toothat IP。

## <a name="wire-up-deployment-domain"></a>接通部署網域

Draft 會針對其所建立的每個 Helm 圖表，以及您在使用每個應用程式建立一個版本。 每一項取得產生的名稱，以供做為草稿_子網域_hello 根之上_部署網域_您所控制。 (在此範例中，我們使用`squillace.io`為 hello 部署網域。) tooenable 這子網域的行為，您必須建立 A 記錄`'*'`部署網域的 DNS 項目，以便每個產生的子網域是路由的 toohello Kubernetes叢集的輸入控制器。

網域提供者具有自己的方式 tooassign DNS 伺服器。太[委派 DNS 您網域 nameservers tooAzure](../../dns/dns-delegate-domain-azure-dns.md)，採取下列步驟的 hello:

1. 建立您區域的資源群組。
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

2. 建立您網域的 DNS 區域。
使用 hello [az 網路 dns 區域建立](/cli/azure/network/dns/zone#create)tooobtain hello nameservers toodelegate DNS 控制 tooAzure DNS 網域的命令。
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
3. 新增您有 toohello 網域提供者，您部署的網域，可讓您 toouse Azure DNS toorepoint 您的網域，您想要的 hello DNS 伺服器。
4. 建立 A 記錄集項目，針對您部署網域對應 toohello `ingress` hello 上一節的步驟 2 中的 IP。
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
hello 輸出看起來像這樣：
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

5. 您的登錄設定草稿 toouse 並建立它會建立每個頭盔圖表的子網域。 tooconfigure 草稿，您需要：
  - 您的 Azure Container Registry 名稱 (在此範例中為 `draft`)
  - 您的登錄機碼或密碼，從 `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`。
  - 您已設定 toomap toohello Kubernetes ingress 外部 IP 位址的 hello 根部署網域 (在這裡， `squillace.io`)

  呼叫`draft init`和 hello 設定程序會提示您輸入 hello 上述的值。 hello 程序看起來像下列 hello hello 第一次您執行此程式碼。
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

您現在已經準備好 toodeploy 應用程式。


## <a name="build-and-deploy-an-application"></a>建置和部署應用程式

在 hello 草稿儲存機制是[六個簡單的範例應用程式](https://github.com/Azure/draft/tree/master/examples)。 複製 hello 儲存機制，讓我們使用 hello [Python 範例](https://github.com/Azure/draft/tree/master/examples/python)。 將變更 hello 範例/Python 目錄，然後輸入`draft create`toobuild hello 應用程式。 它看起來應該像下列範例中的 hello。
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

hello 輸出包含了 Dockerfile 並頭盔圖表。 toobuild 和部署，您只需要輸入`draft up`。 hello 輸出很大，但類似下列範例中的 hello 開始。
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

與時機與下列範例類似 toohello 成功結束。
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

圖表的名稱為任何內容，您可以現在`curl http://gangly-bronco.squillace.io`tooreceive hello 回覆， `Hello World!`。

## <a name="next-steps"></a>後續步驟

有 ACS Kubernetes 叢集之後，您可以調查使用[Azure 容器登錄中](../../container-registry/container-registry-intro.md)toocreate 這種情況的詳細和不同的部署。 例如，您可以建立 draft._basedomain.toplevel_ 網域 DNS 記錄集，可針對特定 ACS 部署，控制項目移出更深入的子網域。






