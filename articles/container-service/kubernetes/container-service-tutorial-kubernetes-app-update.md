---
title: "aaaAzure 容器服務教學課程-更新應用程式 |Microsoft 文件"
description: "Azure Container Service 教學課程 - 更新應用程式"
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>在 Kubernetes 中更新應用程式

在 Kubernetes 中部署應用程式之後，您可以藉由指定新的容器映像或映像版本來進行更新。 當您更新應用程式時，會同時更新一部分的 hello 部署預備 hello 更新首度發行。 此暫存的更新可讓 hello 應用程式 tookeep hello 更新期間執行，並提供復原機制，如果部署失敗，就會發生。 

在本教學課程中，更新的七個，hello 範例 Azure 投票應用程式的六個組件。 您完成的工作包括：

> [!div class="checklist"]
> * 更新 hello 前端應用程式程式碼
> * 建立已更新的容器映像
> * 推送 hello 容器映像 tooAzure 容器登錄中
> * 部署的 hello 更新的容器映像

在後續教學課程中，Operations Management Suite 是設定的 toomonitor hello Kubernetes 叢集。

## <a name="before-you-begin"></a>開始之前

在上一個教學課程中，應用程式封裝成容器映像、 hello 映像上傳 tooAzure 容器登錄中，並建立 Kubernetes 叢集。 hello 應用程式然後 hello Kubernetes 叢集上執行。 

如果您沒有完成這些步驟，而且想沿著 toofollow，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。 

## <a name="update-application"></a>更新應用程式

本教學課程 toocomplete hello 步驟，您必須擁有的複製複本 hello Azure 投票應用程式。 如有必要，建立此複製的複本以 hello 下列命令：

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

開啟 hello`config_file.cfg`使用任何程式碼或文字編輯器的檔案。 您可以找到這個 hello 遵循 hello 複製儲存機制的目錄下的檔案。

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

變更 hello 值`VOTE1VALUE`和`VOTE2VALUE`，然後儲存 hello 檔案。

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

使用[docker 撰寫](https://docs.docker.com/compose/)toore-建立 hello 前端映像和執行的 hello 更新應用程式。

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>在本機測試應用程式

瀏覽過`http://localhost:8080`toosee hello 已更新應用程式。

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>標記和推送映像

標記 hello *azure 投票前*hello loginServer hello 容器登錄中的映像。

如果您使用 Azure 容器登錄中，會收到 hello 登入伺服器名稱以 hello [az acr 清單](/cli/azure/acr#list)命令。

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

使用[docker 標記](https://docs.docker.com/engine/reference/commandline/tag/)tootag hello 映像。 以您的 Azure Container Registry 登入伺服器名稱或公用登錄主機名稱取代 `<acrLoginServer>`。

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

使用[docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello 映像 tooyour 登錄。 以您的 Azure Container Registry 登入伺服器名稱或公用登錄主機名稱取代 `<acrLoginServer>`。

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>部署更新應用程式

tooensure 最大執行時間，必須執行 hello 應用程式 pod 的多個執行個體。 確認此組態以 hello [kubectl 取得 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get)命令。

```bash
kubectl get pod
```

輸出：

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

如果您沒有執行 hello azure 投票前映像的多個 pod，調整 hello *azure 投票前*部署。


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

tooupdate hello 應用程式，使用 hello [kubectl 組](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set)命令。 更新`<acrLoginServer>`hello 登入伺服器或主機名稱的容器登錄。

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

toomonitor hello 部署中，使用 hello [kubectl 取得 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get)命令。 Hello 更新應用程式部署，因為您 pod 被終止，並重新建立與 hello 新容器映像。

```azurecli-interactive
kubectl get pod
```

輸出：

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>測試已更新的應用程式

取得 hello 外部 IP 位址的 hello *azure 投票前*服務。

```azurecli-interactive
kubectl get service azure-vote-front
```

瀏覽 toohello IP 位址 toosee hello 更新應用程式。

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以更新應用程式及推出此更新 tooa Kubernetes 叢集。 已完成下列工作的 hello:

> [!div class="checklist"]
> * 更新的 hello 前端應用程式程式碼
> * 建立了已更新的容器映像
> * 推入 hello 容器映像 tooAzure 容器登錄中
> * 更新已部署的 hello 應用程式

前進 toohello 下一個教學課程的 toolearn 有關 toomonitor Kubernetes 與利用 Operations Management Suite。

> [!div class="nextstepaction"]
> [透過 OMS 監視 Kubernetes](./container-service-tutorial-kubernetes-monitor.md)