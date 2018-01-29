---
title: "Azure 上的 Kubernetes 教學課程 - 更新應用程式"
description: "AKS 教學課程 - 更新應用程式"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 10/24/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 6de5173aedc836f7a2d56370ea8e54ad6e77ab5e
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2017
---
# <a name="update-an-application-in-azure-container-service-aks"></a>更新 Azure Container Service (AKS) 中的應用程式

在 Kubernetes 中部署應用程式之後，您可以藉由指定新的容器映像或映像版本來進行更新。 當您更新應用程式時，更新會分段進行，所以只有一部分的部署會同時更新。 此分段更新方式可讓應用程式在更新期間保持運作， 此外也能當作部署失敗時的復原機制。 

在本教學課程 (6/8 部分) 中，已更新範例 Azure Vote 應用程式。 您完成的工作包括：

> [!div class="checklist"]
> * 更新前端應用程式程式碼
> * 建立已更新的容器映像
> * 將容器映像推送至 Azure Container Registry
> * 部署已更新的容器映像

在後續教學課程中，會將 Operations Management Suite 設定為監視 Kubernetes 叢集。

## <a name="before-you-begin"></a>開始之前

在先前的教學課程中，已將應用程式封裝成容器映像、將這些映像上傳至 Azure Container Registry，並已建立 Kubernetes 叢集。 該應用程式接著便在 Kubernetes 叢集上執行。 

應用程式存放庫也會一併複製，其中包括應用程式原始程式碼，以及本教學課程使用的預先建立 Docker Compose 檔案。 請確認您已建立存放庫的複製品，而且已將目錄變更為複製的目錄。 其中有一個名為 `azure-vote` 的目錄和一個名為 `docker-compose.yaml` 的檔案。

如果您尚未完成這些步驟，而且想要跟著做，返回[教學課程 1 – 建立容器映像][aks-tutorial-prepare-app]。 

## <a name="update-application"></a>更新應用程式

在本教學課程中，我們變更了應用程式，並將更新後的應用程式部署到 Kubernetes 叢集。 

您可以在 `azure-vote` 目錄中找到應用程式原始程式碼。 使用任何程式碼或文字編輯器開啟 `config_file.cfg` 檔案。 在此範例中使用 `vi` 。

```console
vi azure-vote/azure-vote/config_file.cfg
```

變更 `VOTE1VALUE` 和 `VOTE2VALUE` 的值，然後儲存檔案。

```console
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

儲存並關閉檔案。

## <a name="update-container-image"></a>更新容器映像

使用[docker 撰寫][ docker-compose]重新建立前端的映像，並執行更新的應用程式。 `--build` 引數可用來指示 Docker Compose 重新建立應用程式映像。

```console
docker-compose up --build -d
```

## <a name="test-application-locally"></a>在本機測試應用程式

瀏覽至 http://localhost:8080 以查看更新後的應用程式。

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>標記和推送映像

以容器登錄的 loginServer 標記 `azure-vote-front` 映像。 

使用 [az acr list](/cli/azure/acr#list) 命令來取得登入伺服器名稱。

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

使用[docker 標記][ docker-tag]來標記的影像。 以您的 Azure Container Registry 登入伺服器名稱或公用登錄主機名稱取代 `<acrLoginServer>`。 另請注意，映像版本已更新為 `redis-v2`。

```console
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

使用[docker push] [ docker-push]登錄檔上傳映像。 以您的 Azure Container Registry 登入伺服器名稱取代 `<acrLoginServer>`。

```console
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>部署更新應用程式

若要確保最大執行時間，則應用程式 pod 必須有多個執行個體正在執行中。 請確認此組態[kubectl 取得 pod] [ kubectl-get]命令。

```
kubectl get pod
```

輸出：

```
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

如果您沒有執行 azure-vote-front 映像的多個 Pod，請調整 `azure-vote-front` 部署。


```azurecli
kubectl scale --replicas=3 deployment/azure-vote-front
```

若要更新應用程式，請使用[kubectl 組][ kubectl-set]命令。 以容器登錄的登入伺服器或主機名稱來更新 `<acrLoginServer>`。

```azurecli
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

若要監視部署，使用[kubectl 取得 pod] [ kubectl-get]命令。 部署已更新的應用程式後，您的 pod 會終止並以新的容器映像重建。

```azurecli
kubectl get pod
```

輸出：

```
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>測試已更新的應用程式

取得 `azure-vote-front` 服務的外部 IP 位址。

```azurecli
kubectl get service azure-vote-front
```

瀏覽至此 IP 位址以查看已更新的應用程式。

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已更新應用程式並將此更新推出至 Kubernetes 叢集。 已完成下列工作：

> [!div class="checklist"]
> * 更新了前端應用程式程式碼
> * 建立了已更新的容器映像
> * 已將容器映像推送至 Azure Container Registry
> * 部署了已更新的應用程式

請前進到下一個教學課程，了解如何利用 Operations Management Suite 監視 Kubernetes。

> [!div class="nextstepaction"]
> [監視 Kubernetes 記錄分析][aks-tutorial-monitor]

<!-- LINKS - external -->
[docker-compose]: https://docs.docker.com/compose/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubectl-set]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#set

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-monitor]: ./tutorial-kubernetes-monitor.md