---
title: "aaaAzure 容器服務教學課程-部署的應用程式 |Microsoft 文件"
description: "Azure Container Service 教學課程 - 部署應用程式"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>在 Kubernetes 中執行應用程式

在本教學課程 (七個章節的第四部分) 中，已在 Kubernetes 叢集中部署一個應用程式範例。 完成的步驟包括：

> [!div class="checklist"]
> * 下載 Kubernetes 資訊清單檔
> * 在 Kubernetes 中執行應用程式
> * 測試 hello 應用程式

在後續教學課程中，此應用程式會向外延展，更新，而且 Operations Management Suite 設定 toomonitor hello Kubernetes 叢集。

本教學課程假設 Kubernetes 概念的基本了解、 Kubernetes 的詳細資訊請參閱 hello [Kubernetes 文件](https://kubernetes.io/docs/home/)。

## <a name="before-you-begin"></a>開始之前

在上一個教學課程中，應用程式封裝成容器映像、 此映像上傳的 tooAzure 容器登錄中，並已建立 Kubernetes 叢集。 如果您有未完成這些步驟，並希望沿著 toofollow，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。 

本教學課程至少需要一個 Kubernetes 叢集。

## <a name="get-manifest-file"></a>取得資訊清單檔

針對此教學課程，會使用 Kubernetes 資訊清單來部署 [Kubernetes 物件](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)。 Kubernetes 資訊清單為 YAML 或 JSON 格式的檔案，包含 Kubernetes 物件部署和設定指示。

使用 hello Azure 投票應用程式儲存機制中，這已在上一個教學課程中複製此教學課程中的 hello 應用程式資訊清單檔案。 如果您尚未這樣做，請使用下列命令的 hello 複製 hello 儲存機制： 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

hello 遵循 hello 複製儲存機制的目錄中找到 hello 資訊清單檔案。

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>更新資訊清單檔

如果使用 Azure 容器登錄中 toostore hello 容器映像，hello 資訊清單需求 toobe 更新 hello loginServer 的 ACR 名稱。

取得 hello ACR 登入伺服器名稱以 hello [az acr 清單](/cli/azure/acr#list)命令。

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

hello 範例資訊清單已預先建立的儲存機制名稱*microsoft*。 使用任何文字編輯器 中，開啟 hello 檔案和取代 hello *microsoft* hello 登入伺服器名稱為您的 ACR 的執行個體的值。

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>部署應用程式

使用 hello [kubectl 建立](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create)命令 toorun hello 應用程式。 此命令剖析 hello 資訊清單檔案，並建立 hello 定義 Kubernetes 物件。

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

輸出：

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>測試應用程式

A [Kubernetes 服務](https://kubernetes.io/docs/concepts/services-networking/service/)建立 hello 應用程式 toohello 公開網際網路。 此程序需要數分鐘的時間。 

toomonitor 進度，使用 hello [kubectl 取得服務](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681)命令與 hello`--watch`引數。

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

一開始，hello**外部 IP** hello *azure 投票前*服務會顯示為*暫止*。 一旦 hello 外部 IP 位址已從*暫止*tooan *IP 位址*，使用`CTRL-C`toostop hello kubectl 監看式程序。

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

toosee hello 應用程式中，瀏覽 toohello 外部 IP 位址。

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>後續步驟

在本教學課程，hello Azure 投票應用程式已部署的 tooan Azure 容器服務 Kubernetes 叢集。 完成的工作包括：  

> [!div class="checklist"]
> * 下載 Kubernetes 資訊清單檔
> * 執行 Kubernetes hello 應用程式
> * 已測試的 hello 應用程式

前進 toohello 下一個教學課程的 toolearn 調整規模的 Kubernetes 應用程式 」 和 「 hello 基礎 Kubernetes 基礎結構。 

> [!div class="nextstepaction"]
> [調整 Kubernetes 應用程式和基礎結構](./container-service-tutorial-kubernetes-scale.md)