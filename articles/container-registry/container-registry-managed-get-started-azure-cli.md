---
title: "aaaCreate 私用 Docker 容器登錄中的 Azure CLI |Microsoft 文件"
description: "開始建立及管理私人 Docker 容器登錄以 hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>建立受管理的容器登錄中使用 Azure CLI hello

Azure Container Registry 是用於儲存私用 Docker 容器映像的受管理 Docker 容器登錄服務。 本指南詳述建立受管理的 Azure 容器登錄中執行個體使用 hello Azure CLI。

受管理 Azure 容器登錄為預覽版本，並不適用於所有區域。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *westcentralus*位置。

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>建立容器登錄庫

建立使用 hello ACR 執行個體[az acr 建立](/cli/azure/acr#create)命令。

> [!NOTE]
> 當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。

 hello 範例中的 hello 登錄名稱是*myContainerRegistry1*，以取代您自己的唯一名稱。

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

建立 hello 登錄時，hello 輸出會是類似 toohello 下列：

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>登入 tooACR 執行個體

然後再推送和提取容器映像，您必須登入 toohello ACR 執行個體。 因此，使用 toodo 的 hello [az acr 登入](/cli/azure/acr#login)命令。

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

hello 命令會傳回 「 已成功登入 」 的訊息，一旦完成後。

## <a name="use-azure-container-registry"></a>使用 Azure Container Registry

### <a name="list-container-images"></a>列出容器映像

使用 hello `az acr` CLI 命令 tooquery hello 映像儲存機制中的標記。

> [!NOTE]
> 目前，容器登錄中不支援 hello`docker search`命令 tooquery 映像和標記。

### <a name="list-repositories"></a>列出儲存機制

hello 下列範例會列出在登錄中，JSON （JavaScript 物件標記法） 格式的 hello 儲存機制：

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>列出標籤

hello 下列範例會列出在 hello hello 標記**範例/nginx**儲存機制，以 JSON 格式：

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>後續步驟

在這個快速入門中，您已建立受管理的 Azure 容器登錄中執行個體，使用 Azure CLI hello。

> [!div class="nextstepaction"]
> [推入第一個映像使用 Docker CLI hello](container-registry-get-started-docker-cli.md)
