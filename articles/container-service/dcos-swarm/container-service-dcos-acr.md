---
title: "與 Azure DC/OS 叢集 aaaUsing ACR |Microsoft 文件"
description: "在 Azure Container Service 中搭配使用 Azure Container Registry 與 DC/OS 叢集"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, Containers, Micro-services, Mesos, Azure, FileShare, cifs, 容器, 微服務"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>您的應用程式使用與 DC/OS 叢集 toodeploy ACR

在本文中，我們探討如何與 DC/OS 叢集 toouse Azure 容器登錄中。 使用 ACR 可讓您 tooprivately 存放區和管理容器映像。 本教學課程涵蓋 hello 下列工作：

> [!div class="checklist"]
> * 部署 Azure Container Registry (如有需要)
> * 在 DC/OS 叢集上設定 ACR 驗證
> * 上傳映像 toohello Azure 容器登錄中
> * 從 hello Azure 容器登錄中執行的容器映像

您必須在本教學課程步驟的叢集 toocomplete hello ACS DC/OS。 如有需要，[此指令碼範例](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)可為您建立一個叢集。

本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>部署 Azure Container Registry

如有需要建立 Azure 容器登錄以 hello [az acr 建立](/cli/azure/acr#create)命令。 

hello 下列範例會建立登錄中的以隨機產生的名稱。 hello 登錄也會搭配使用 hello 系統管理員帳戶設定`--admin-enabled`引數。

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

一旦建立 hello 登錄之後，hello Azure CLI 輸出類似 toohello 下列資料。 記下 hello`name`和`loginServer`，會在稍後步驟中使用這些。

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

取得使用 hello hello 容器登錄認證[az acr 認證顯示](/cli/azure/acr/credential)命令。 替代 hello`--name`以 hello 一個 hello 最後一個步驟中所述。 記下一組密碼，稍後的步驟中會用到此密碼。

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

如需有關 Azure 容器登錄中的詳細資訊，請參閱[簡介 tooprivate Docker 容器登錄](../../container-registry/container-registry-intro.md)。 

## <a name="manage-acr-authentication"></a>管理 ACR 驗證

hello 傳統方式 toopush 和提取映像從私人登錄 toofirst 向 hello 登錄。 toodo 因此，您會使用 hello`docker login`命令需要 tooaccess hello 私人登錄任何用戶端上。 DC/OS 叢集可以包含許多節點，其中需要 toobe 驗證以 hello ACR，因為它是很有幫助 tooautomate 透過此程序的每個節點。 

### <a name="create-shared-storage"></a>建立共用儲存體

此程序使用的 Azure 檔案共用，已掛接 hello 叢集中的每個節點上。 如果尚未設定共用儲存體，請參閱[在 DC/OS 叢集內設定檔案共用](container-service-dcos-fileshare.md)。

### <a name="configure-acr-authentication"></a>設定 ACR 驗證

首先，取得 hello hello 主要 DC/OS，並將它儲存在變數中的 FQDN。

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

建立 SSH 連線與 hello 主要 （或 hello 第一個主要） 的 DC/作業系統為基礎的叢集。 如果建立 hello 叢集時使用非預設值，請更新 hello 使用者名稱。

```azurecli-interactive
ssh azureuser@$FQDN
```

執行下列命令 toologin toohello Azure 容器登錄中的 hello。 取代 hello `--username` hello 名稱 hello 容器登錄中，hello`--password`與其中一個 hello 提供密碼。 取代 hello 最後一個引數*mycontainerregistry.azurecr.io*中的 hello 容器登錄中的 hello 範例與 hello loginServer 名稱。 

此命令會儲存在本機下 hello hello 驗證值`~/.docker`路徑。

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

建立壓縮的檔案，其中包含 hello 容器登錄驗證值。

```azurecli-interactive
tar czf docker.tar.gz .docker
```

複製這個檔案 toohello 叢集共用存放裝置。 此步驟會 hello 檔案 hello DC/OS 叢集的所有節點上使用。

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>上傳映像 tooACR

現在從開發電腦或任何其他系統已安裝 docker，請建立映像，並將它上傳 toohello Azure 容器登錄中。

從 hello Ubuntu 映像建立容器。

```azurecli-interactive
docker run ubunut --name base-image
```

現在擷取到新的映像的 hello 容器。 hello 映像名稱必須 tooinclude hello`loginServer`名稱格式的 hello 容器 registrywith `loginServer/imageName`。

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

登入 hello Azure 容器登錄中。 取代 hello hello loginServer 名稱、 hello-具有 hello 名稱 hello 容器登錄中和 hello-密碼與其中一個 hello 提供密碼的使用者名稱。

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

最後上, 傳 hello 映像 toohello ACR 登錄。 這個範例會上傳名為 dcos-demo 的映像。

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>從 ACR 執行映像

toouse hello ACR 登錄中，從映像建立的檔案名稱*acrDemo.json*並複製 hello 遵循到其中的文字。 Hello 映像名稱取代 hello 容器登錄 loginServer 名稱和映像名稱，例如`loginServer/imageName`。 記下 hello`uris`屬性。 這個屬性會保留 hello hello 容器登錄驗證檔案位置，在此情況下是裝載在 hello DC/OS 叢集中的每個節點的 hello Azure 檔案共用。

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

部署以 hello DC/MICROSOFT-WINDOWS-NETFX3-OC-PACKAGE CLI hello 應用程式。

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已設定 DC/OS toouse Azure 容器登錄中包括 hello 下列工作：

> [!div class="checklist"]
> * 部署 Azure Container Registry (如有需要)
> * 在 DC/OS 叢集上設定 ACR 驗證
> * 上傳映像 toohello Azure 容器登錄中
> * 從 hello Azure 容器登錄中執行的容器映像
