---
title: "準備 Azure 容器登錄-aaaAzure 容器執行個體教學課程 |Microsoft 文件"
description: "Azure 容器執行個體教學課程 - 準備 Azure Container Registry"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>部署和使用 Azure Container Registry

這是三段式教學課程的第二段。 在 hello[上一個步驟](./container-instances-tutorial-prepare-app.md)，以撰寫簡單的 web 應用程式建立的容器映像[Node.js](http://nodejs.org)。 在本教學課程中，此映像推入 tooan Azure 容器登錄中。 如果您尚未建立 hello 容器映像，傳回太[教學課程 1 – 建立容器映像](./container-instances-tutorial-prepare-app.md)。 

hello Azure 容器登錄中是以 Azure 為基礎的私人登錄中，為 Docker 容器映像。 本教學課程會逐步部署容器登錄中 Azure 執行個體，並將容器映像 tooit 推入。 完成的步驟包括：

> [!div class="checklist"]
> * 部署 Azure Container Registry 執行個體
> * 標記 Azure Container Registry 的容器映像
> * 上傳映像 tooAzure 容器登錄中

在後續的教學課程中，您可以部署 hello 容器從您私用登錄 tooAzure 容器執行個體。

## <a name="before-you-begin"></a>開始之前

本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。

## <a name="deploy-azure-container-registry"></a>部署 Azure Container Registry

部署 Azure Container Registry 時，您必須先有資源群組。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯集合。

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 在此範例中，資源群組命名為*myResourceGroup*會建立在 hello *eastus*區域。

```azurecli
az group create --name myResourceGroup --location eastus
```

建立 Azure 容器登錄以 hello [az acr 建立](/cli/azure/acr#create)命令。 容器登錄中的 hello 名稱**必須是唯一的**。 在下列範例的 hello，我們使用 hello 名稱*mycontainerregistry082*。

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

在本教學課程的 hello 其餘部分，我們使用`<acrname>`作為您所選擇的 hello 容器登錄名稱的預留位置。

## <a name="container-registry-login"></a>Container Registry 登入

推送 tooit 映像之前，您必須登入 tooyour ACR 執行個體。 使用 hello [az acr 登入](https://docs.microsoft.com/en-us/cli/azure/acr#login)命令 toocomplete hello 作業。 您必須指定 toohello 容器登錄中建立時的 tooprovide hello 唯一名稱。

```azurecli
az acr login --name <acrName>
```

hello 命令會傳回 「 已成功登入 」 的訊息，一旦完成後。

## <a name="tag-container-image"></a>標記容器映像

toodeploy 私人登錄中的容器映像，hello 映像必須加上 hello toobe `loginServer` hello 登錄的名稱。

一份目前的映像，使用 hello toosee`docker images`命令。

```bash
docker images
```

輸出：

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

tooget hello loginServer 名稱，執行下列命令的 hello。

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

標記 hello *aci 教學課程應用*hello loginServer hello 容器登錄中的映像。 此外，請加入`:v1`toohello hello 映像名稱結尾。 此標記代表 hello 映像的版本號碼。

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

加上標記，一旦執行`docker images`tooverify hello 作業。

```bash
docker images
```

輸出：

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>推入映像 tooAzure 容器登錄中

推播 hello *aci 教學課程應用*映像 toohello 登錄。

使用下列範例中的 hello，取代從您的環境的 hello loginServer hello 容器登錄 loginServer 名稱。

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>在 Azure Container Registry 中列出映像

tooreturn 已推入 tooyour Azure 容器登錄中，使用者 hello 的映像清單[az acr 儲存機制清單](/cli/azure/acr/repository#list)命令。 更新 hello 容器登錄名稱的 hello 命令。

```azurecli
az acr repository list --name <acrName> --output table
```

輸出：

```azurecli
Result
----------------
aci-tutorial-app
```

Toosee hello 標記用於特定的映像，然後使用 hello [az acr 儲存機制顯示標籤](/cli/azure/acr/repository#show-tags)命令。

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

輸出：

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，Azure 容器登錄中已備妥用於 Azure 容器執行個體，而且 hello 容器映像已推入。 已完成下列步驟的 hello:

> [!div class="checklist"]
> * 部署 Azure Container Registry 執行個體
> * 標記 Azure Container Registry 的容器映像
> * 上傳映像 tooAzure 容器登錄中

前進 toohello 下一個教學課程的 toolearn 有關部署 hello 容器 tooAzure 使用 Azure 容器執行個體。

> [!div class="nextstepaction"]
> [部署容器 tooAzure 容器執行個體](./container-instances-tutorial-deploy-app.md)
