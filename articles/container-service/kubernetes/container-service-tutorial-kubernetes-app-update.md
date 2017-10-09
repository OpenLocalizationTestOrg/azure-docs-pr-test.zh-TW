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
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="9162c-104">在 Kubernetes 中更新應用程式</span><span class="sxs-lookup"><span data-stu-id="9162c-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="9162c-105">在 Kubernetes 中部署應用程式之後，您可以藉由指定新的容器映像或映像版本來進行更新。</span><span class="sxs-lookup"><span data-stu-id="9162c-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="9162c-106">當您更新應用程式時，會同時更新一部分的 hello 部署預備 hello 更新首度發行。</span><span class="sxs-lookup"><span data-stu-id="9162c-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="9162c-107">此暫存的更新可讓 hello 應用程式 tookeep hello 更新期間執行，並提供復原機制，如果部署失敗，就會發生。</span><span class="sxs-lookup"><span data-stu-id="9162c-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="9162c-108">在本教學課程中，更新的七個，hello 範例 Azure 投票應用程式的六個組件。</span><span class="sxs-lookup"><span data-stu-id="9162c-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="9162c-109">您完成的工作包括：</span><span class="sxs-lookup"><span data-stu-id="9162c-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9162c-110">更新 hello 前端應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="9162c-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="9162c-111">建立已更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="9162c-111">Creating an updated container image</span></span>
> * <span data-ttu-id="9162c-112">推送 hello 容器映像 tooAzure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="9162c-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="9162c-113">部署的 hello 更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="9162c-113">Deploying hello updated container image</span></span>

<span data-ttu-id="9162c-114">在後續教學課程中，Operations Management Suite 是設定的 toomonitor hello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="9162c-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9162c-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="9162c-115">Before you begin</span></span>

<span data-ttu-id="9162c-116">在上一個教學課程中，應用程式封裝成容器映像、 hello 映像上傳 tooAzure 容器登錄中，並建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="9162c-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="9162c-117">hello 應用程式然後 hello Kubernetes 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="9162c-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="9162c-118">如果您沒有完成這些步驟，而且想沿著 toofollow，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9162c-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="9162c-119">更新應用程式</span><span class="sxs-lookup"><span data-stu-id="9162c-119">Update application</span></span>

<span data-ttu-id="9162c-120">本教學課程 toocomplete hello 步驟，您必須擁有的複製複本 hello Azure 投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="9162c-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="9162c-121">如有必要，建立此複製的複本以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="9162c-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="9162c-122">開啟 hello`config_file.cfg`使用任何程式碼或文字編輯器的檔案。</span><span class="sxs-lookup"><span data-stu-id="9162c-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="9162c-123">您可以找到這個 hello 遵循 hello 複製儲存機制的目錄下的檔案。</span><span class="sxs-lookup"><span data-stu-id="9162c-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="9162c-124">變更 hello 值`VOTE1VALUE`和`VOTE2VALUE`，然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="9162c-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="9162c-125">使用[docker 撰寫](https://docs.docker.com/compose/)toore-建立 hello 前端映像和執行的 hello 更新應用程式。</span><span class="sxs-lookup"><span data-stu-id="9162c-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="9162c-126">在本機測試應用程式</span><span class="sxs-lookup"><span data-stu-id="9162c-126">Test application locally</span></span>

<span data-ttu-id="9162c-127">瀏覽過`http://localhost:8080`toosee hello 已更新應用程式。</span><span class="sxs-lookup"><span data-stu-id="9162c-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="9162c-129">標記和推送映像</span><span class="sxs-lookup"><span data-stu-id="9162c-129">Tag and push images</span></span>

<span data-ttu-id="9162c-130">標記 hello *azure 投票前*hello loginServer hello 容器登錄中的映像。</span><span class="sxs-lookup"><span data-stu-id="9162c-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="9162c-131">如果您使用 Azure 容器登錄中，會收到 hello 登入伺服器名稱以 hello [az acr 清單](/cli/azure/acr#list)命令。</span><span class="sxs-lookup"><span data-stu-id="9162c-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="9162c-132">使用[docker 標記](https://docs.docker.com/engine/reference/commandline/tag/)tootag hello 映像。</span><span class="sxs-lookup"><span data-stu-id="9162c-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="9162c-133">以您的 Azure Container Registry 登入伺服器名稱或公用登錄主機名稱取代 `<acrLoginServer>`。</span><span class="sxs-lookup"><span data-stu-id="9162c-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="9162c-134">使用[docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello 映像 tooyour 登錄。</span><span class="sxs-lookup"><span data-stu-id="9162c-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="9162c-135">以您的 Azure Container Registry 登入伺服器名稱或公用登錄主機名稱取代 `<acrLoginServer>`。</span><span class="sxs-lookup"><span data-stu-id="9162c-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="9162c-136">部署更新應用程式</span><span class="sxs-lookup"><span data-stu-id="9162c-136">Deploy update application</span></span>

<span data-ttu-id="9162c-137">tooensure 最大執行時間，必須執行 hello 應用程式 pod 的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="9162c-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="9162c-138">確認此組態以 hello [kubectl 取得 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get)命令。</span><span class="sxs-lookup"><span data-stu-id="9162c-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="9162c-139">輸出：</span><span class="sxs-lookup"><span data-stu-id="9162c-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="9162c-140">如果您沒有執行 hello azure 投票前映像的多個 pod，調整 hello *azure 投票前*部署。</span><span class="sxs-lookup"><span data-stu-id="9162c-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="9162c-141">tooupdate hello 應用程式，使用 hello [kubectl 組](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set)命令。</span><span class="sxs-lookup"><span data-stu-id="9162c-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="9162c-142">更新`<acrLoginServer>`hello 登入伺服器或主機名稱的容器登錄。</span><span class="sxs-lookup"><span data-stu-id="9162c-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="9162c-143">toomonitor hello 部署中，使用 hello [kubectl 取得 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get)命令。</span><span class="sxs-lookup"><span data-stu-id="9162c-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="9162c-144">Hello 更新應用程式部署，因為您 pod 被終止，並重新建立與 hello 新容器映像。</span><span class="sxs-lookup"><span data-stu-id="9162c-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="9162c-145">輸出：</span><span class="sxs-lookup"><span data-stu-id="9162c-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="9162c-146">測試已更新的應用程式</span><span class="sxs-lookup"><span data-stu-id="9162c-146">Test updated application</span></span>

<span data-ttu-id="9162c-147">取得 hello 外部 IP 位址的 hello *azure 投票前*服務。</span><span class="sxs-lookup"><span data-stu-id="9162c-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="9162c-148">瀏覽 toohello IP 位址 toosee hello 更新應用程式。</span><span class="sxs-lookup"><span data-stu-id="9162c-148">Browse toohello IP address toosee hello updated application.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="9162c-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9162c-150">Next steps</span></span>

<span data-ttu-id="9162c-151">在本教學課程中，您可以更新應用程式及推出此更新 tooa Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="9162c-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="9162c-152">已完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="9162c-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9162c-153">更新的 hello 前端應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="9162c-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="9162c-154">建立了已更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="9162c-154">Created an updated container image</span></span>
> * <span data-ttu-id="9162c-155">推入 hello 容器映像 tooAzure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="9162c-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="9162c-156">更新已部署的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="9162c-156">Deployed hello updated application</span></span>

<span data-ttu-id="9162c-157">前進 toohello 下一個教學課程的 toolearn 有關 toomonitor Kubernetes 與利用 Operations Management Suite。</span><span class="sxs-lookup"><span data-stu-id="9162c-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9162c-158">透過 OMS 監視 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="9162c-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)