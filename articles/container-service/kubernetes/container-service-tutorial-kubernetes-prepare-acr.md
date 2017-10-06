---
title: "aaaAzure 容器服務教學課程-準備 ACR |Microsoft 文件"
description: "Azure Container Service 教學課程 - 準備 ACR"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>部署和使用 Azure Container Registry

Azure Container Registry (ACR) 是以 Azure 為基礎的私人登錄，用於裝載 Docker 容器映像。 此教學課程中，七個，逐步解說部署容器登錄中 Azure 執行個體，並將容器映像 tooit 推入兩個部分。 完成的步驟包括：

> [!div class="checklist"]
> * 部署 Azure Container Registry (ACR) 執行個體
> * 標記 ACR 的容器映像
> * 上傳 hello 映像 tooACR

在後續教學課程中，此 ACR 執行個體會與 Azure Container Service 的 Kubernetes 叢集整合，以便安全地執行容器映像。 

## <a name="before-you-begin"></a>開始之前

在 hello[上一個教學課程](./container-service-tutorial-kubernetes-prepare-app.md)，容器映像建立簡單的投票 Azure 應用程式。 在本教學課程中，此映像推入 tooan Azure 容器登錄中。 如果您尚未建立 hello Azure 投票應用程式映像，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。 或者，hello 步驟這裡所詳述使用任何容器映像的工作。

本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="deploy-azure-container-registry"></a>部署 Azure Container Registry

部署 Azure Container Registry 時，您必須先有資源群組。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 在此範例中，資源群組命名為*myResourceGroup*會建立在 hello *westeurope*區域。

```azurecli
az group create --name myResourceGroup --location westeurope
```

建立 Azure 容器登錄以 hello [az acr 建立](/cli/azure/acr#create)命令。 容器登錄中的 hello 名稱**必須是唯一的**。

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

Hello 的其餘本教學課程中，我們使用 「 acrname"做為預留位置您選擇的 hello 容器登錄名稱。

## <a name="container-registry-login"></a>Container Registry 登入

推送 tooit 映像之前，您必須登入 tooyour ACR 執行個體。 使用 hello [az acr 登入](https://docs.microsoft.com/en-us/cli/azure/acr#login)命令 toocomplete hello 作業。 您必須指定 toohello 容器登錄中建立時的 tooprovide hello 唯一名稱。

```azurecli
az acr login --name <acrName>
```

hello 命令會傳回 「 已成功登入 」 的訊息，一旦完成後。

## <a name="tag-container-images"></a>標記容器映像

每個容器映像必須加上 hello 登錄 hello loginServer 名稱 toobe。 這個標記可用於路由推入容器映像 tooan 映像登錄中時。

一份目前的映像，使用 hello toosee [docker 映像](https://docs.docker.com/engine/reference/commandline/images/)命令。

```bash
docker images
```

輸出：

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

tooget hello loginServer 名稱，執行下列命令的 hello。

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

現在，標記 hello *azure 投票前*hello loginServer hello 容器登錄中的映像。 此外，請加入`:redis-v1`toohello hello 映像名稱結尾。 此標記代表 hello 映像版本。

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

一旦標記，請執行 [docker 映像] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello 作業。

```bash
docker images
```

輸出：

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>推入映像 tooregistry

推播 hello *azure 投票前*映像 toohello 登錄。 

使用下列範例中的 hello，取代從您的環境的 hello loginServer hello ACR loginServer 名稱。

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

這只需要幾分鐘的時間 toocomplete。

## <a name="list-images-in-registry"></a>列出登錄中的映像

tooreturn 已推入 tooyour Azure 容器登錄中，使用者 hello 的映像清單[az acr 儲存機制清單](/cli/azure/acr/repository#list)命令。 更新 hello 命令與 hello ACR 執行個體名稱。

```azurecli
az acr repository list --name <acrName> --output table
```

輸出：

```azurecli
Result
----------------
azure-vote-front
```

Toosee hello 標記用於特定的映像，然後使用 hello [az acr 儲存機制顯示標籤](/cli/azure/acr/repository#show-tags)命令。

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

輸出：

```azurecli
Result
--------
redis-v1
```

在教學課程完成，hello 容器映像已儲存在私用的 Azure 容器登錄中執行個體。 此映像從 ACR tooa Kubernetes 叢集部署在後續的教學課程。

## <a name="next-steps"></a>後續步驟

在本教學課程中，已備妥可用於 ACS Kubernetes 叢集中的 Azure Container Registry。 已完成下列步驟的 hello:

> [!div class="checklist"]
> * 已部署 Azure Container Registry 執行個體
> * 已標記 ACR 的容器映像
> * 上傳的 hello 映像 tooACR

前進 toohello 下一個教學課程的 toolearn 有關部署在 Azure 中的 Kubernetes 叢集。

> [!div class="nextstepaction"]
> [部署 Kubernetes 叢集](./container-service-tutorial-kubernetes-deploy-cluster.md)