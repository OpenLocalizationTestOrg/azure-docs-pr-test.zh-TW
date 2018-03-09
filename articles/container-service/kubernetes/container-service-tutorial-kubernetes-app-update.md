---
title: "Azure Container Service 教學課程 - 更新應用程式"
description: "Azure Container Service 教學課程 - 更新應用程式"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5ecaa3a79270e29ac002e91065f7df4f7e8914e7
ms.sourcegitcommit: 694e40a193980dea1e2f945471071f11030d5641
ms.translationtype: MTE
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2018
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="ef814-103">在 Kubernetes 中更新應用程式</span><span class="sxs-lookup"><span data-stu-id="ef814-103">Update an application in Kubernetes</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="ef814-104">在 Kubernetes 中部署應用程式之後，您可以藉由指定新的容器映像或映像版本來進行更新。</span><span class="sxs-lookup"><span data-stu-id="ef814-104">After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="ef814-105">當您更新應用程式時，更新會分段進行，所以只有一部分的部署會同時更新。</span><span class="sxs-lookup"><span data-stu-id="ef814-105">When doing so, the update is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="ef814-106">此分段更新方式可讓應用程式在更新期間保持運作，</span><span class="sxs-lookup"><span data-stu-id="ef814-106">This staged update enables the application to keep running during the update.</span></span> <span data-ttu-id="ef814-107">此外也能當作部署失敗時的復原機制。</span><span class="sxs-lookup"><span data-stu-id="ef814-107">It also provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="ef814-108">在本教學課程 (6/7 部分) 中，已更新範例 Azure Vote 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef814-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="ef814-109">您完成的工作包括：</span><span class="sxs-lookup"><span data-stu-id="ef814-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ef814-110">更新前端應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="ef814-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="ef814-111">建立已更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="ef814-111">Creating an updated container image</span></span>
> * <span data-ttu-id="ef814-112">將容器映像推送至 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ef814-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="ef814-113">部署已更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="ef814-113">Deploying the updated container image</span></span>

<span data-ttu-id="ef814-114">在後續教學課程中，會將 Operations Management Suite 設定為監視 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="ef814-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ef814-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="ef814-115">Before you begin</span></span>

<span data-ttu-id="ef814-116">在先前的教學課程中，已將應用程式封裝成容器映像、將這些映像上傳至 Azure Container Registry，並已建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="ef814-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="ef814-117">該應用程式接著便在 Kubernetes 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="ef814-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="ef814-118">應用程式存放庫也會一併複製，其中包括應用程式原始程式碼，以及本教學課程使用的預先建立 Docker Compose 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef814-118">An application repository was also cloned which includes the application source code, and a pre-created Docker Compose file used in this tutorial.</span></span> <span data-ttu-id="ef814-119">請確認您已建立存放庫的複製品，而且已將目錄變更為複製的目錄。</span><span class="sxs-lookup"><span data-stu-id="ef814-119">Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory.</span></span> <span data-ttu-id="ef814-120">其中有一個名為 `azure-vote` 的目錄和一個名為 `docker-compose.yml` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="ef814-120">Inside is a directory named `azure-vote` and a file named `docker-compose.yml`.</span></span>

<span data-ttu-id="ef814-121">如果您尚未完成這些步驟，而想要跟著做，請回到[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ef814-121">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="ef814-122">更新應用程式</span><span class="sxs-lookup"><span data-stu-id="ef814-122">Update application</span></span>

<span data-ttu-id="ef814-123">在本教學課程中，我們變更了應用程式，並將更新後的應用程式部署到 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="ef814-123">For this tutorial, a change is made to the application, and the updated application deployed to the Kubernetes cluster.</span></span> 

<span data-ttu-id="ef814-124">您可以在 `azure-vote` 目錄中找到應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef814-124">The application source code can be found inside of the `azure-vote` directory.</span></span> <span data-ttu-id="ef814-125">使用任何程式碼或文字編輯器開啟 `config_file.cfg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef814-125">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="ef814-126">在此範例中使用 `vi` 。</span><span class="sxs-lookup"><span data-stu-id="ef814-126">In this example `vi` is used.</span></span>

```bash
vi azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="ef814-127">變更 `VOTE1VALUE` 和 `VOTE2VALUE` 的值，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="ef814-127">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="ef814-128">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="ef814-128">Save and close the file.</span></span>

## <a name="update-container-image"></a><span data-ttu-id="ef814-129">更新容器映像</span><span class="sxs-lookup"><span data-stu-id="ef814-129">Update container image</span></span>

<span data-ttu-id="ef814-130">使用 [docker-compose](https://docs.docker.com/compose/) 重新建立前端映像，並執行已更新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef814-130">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span> <span data-ttu-id="ef814-131">`--build` 引數可用來指示 Docker Compose 重新建立應用程式映像。</span><span class="sxs-lookup"><span data-stu-id="ef814-131">The `--build` argument is used to instruct Docker Compose to re-create the application image.</span></span>

```bash
docker-compose up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="ef814-132">在本機測試應用程式</span><span class="sxs-lookup"><span data-stu-id="ef814-132">Test application locally</span></span>

<span data-ttu-id="ef814-133">瀏覽至 http://localhost:8080 以查看更新後的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef814-133">Browse to http://localhost:8080 to see the updated application.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="ef814-135">標記和推送映像</span><span class="sxs-lookup"><span data-stu-id="ef814-135">Tag and push images</span></span>

<span data-ttu-id="ef814-136">以容器登錄的 loginServer 標記 `azure-vote-front` 映像。</span><span class="sxs-lookup"><span data-stu-id="ef814-136">Tag the `azure-vote-front` image with the loginServer of the container registry.</span></span> 

<span data-ttu-id="ef814-137">使用 [az acr list](/cli/azure/acr#list) 命令來取得登入伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="ef814-137">Get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="ef814-138">使用 [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) 來標記映像。</span><span class="sxs-lookup"><span data-stu-id="ef814-138">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="ef814-139">以您的 Azure Container Registry 登入伺服器名稱或公用登錄主機名稱取代 `<acrLoginServer>`。</span><span class="sxs-lookup"><span data-stu-id="ef814-139">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span> <span data-ttu-id="ef814-140">另請注意，映像版本已更新為 `redis-v2`。</span><span class="sxs-lookup"><span data-stu-id="ef814-140">Also notice that the image version is updated to `redis-v2`.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="ef814-141">使用 [docker push](https://docs.docker.com/engine/reference/commandline/push/) 將映像上傳至您的登錄。</span><span class="sxs-lookup"><span data-stu-id="ef814-141">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="ef814-142">以您的 Azure Container Registry 登入伺服器名稱取代 `<acrLoginServer>`。</span><span class="sxs-lookup"><span data-stu-id="ef814-142">Replace `<acrLoginServer>` with your Azure Container Registry login server name.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="ef814-143">部署更新應用程式</span><span class="sxs-lookup"><span data-stu-id="ef814-143">Deploy update application</span></span>

<span data-ttu-id="ef814-144">若要確保最大執行時間，則應用程式 pod 必須有多個執行個體正在執行中。</span><span class="sxs-lookup"><span data-stu-id="ef814-144">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="ef814-145">請使用 [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 命令驗證此組態。</span><span class="sxs-lookup"><span data-stu-id="ef814-145">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="ef814-146">輸出：</span><span class="sxs-lookup"><span data-stu-id="ef814-146">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="ef814-147">如果您沒有執行 azure-vote-front 映像的多個 Pod，請調整 `azure-vote-front` 部署。</span><span class="sxs-lookup"><span data-stu-id="ef814-147">If you do not have multiple pods running the azure-vote-front image, scale the `azure-vote-front` deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="ef814-148">若要更新應用程式，請使用 [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) 命令。</span><span class="sxs-lookup"><span data-stu-id="ef814-148">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="ef814-149">以容器登錄的登入伺服器或主機名稱來更新 `<acrLoginServer>`。</span><span class="sxs-lookup"><span data-stu-id="ef814-149">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="ef814-150">若要監視部署，請使用 [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 命令。</span><span class="sxs-lookup"><span data-stu-id="ef814-150">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="ef814-151">部署已更新的應用程式後，您的 pod 會終止並以新的容器映像重建。</span><span class="sxs-lookup"><span data-stu-id="ef814-151">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="ef814-152">輸出：</span><span class="sxs-lookup"><span data-stu-id="ef814-152">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="ef814-153">測試已更新的應用程式</span><span class="sxs-lookup"><span data-stu-id="ef814-153">Test updated application</span></span>

<span data-ttu-id="ef814-154">取得 `azure-vote-front` 服務的外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ef814-154">Get the external IP address of the `azure-vote-front` service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="ef814-155">瀏覽至此 IP 位址以查看已更新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef814-155">Browse to the IP address to see the updated application.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="ef814-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef814-157">Next steps</span></span>

<span data-ttu-id="ef814-158">在本教學課程中，您已更新應用程式並將此更新推出至 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="ef814-158">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="ef814-159">已完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="ef814-159">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ef814-160">更新了前端應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="ef814-160">Updated the front-end application code</span></span>
> * <span data-ttu-id="ef814-161">建立了已更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="ef814-161">Created an updated container image</span></span>
> * <span data-ttu-id="ef814-162">已將容器映像推送至 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ef814-162">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="ef814-163">部署了已更新的應用程式</span><span class="sxs-lookup"><span data-stu-id="ef814-163">Deployed the updated application</span></span>

<span data-ttu-id="ef814-164">請前進到下一個教學課程，了解如何利用 Operations Management Suite 監視 Kubernetes。</span><span class="sxs-lookup"><span data-stu-id="ef814-164">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef814-165">透過 OMS 監視 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ef814-165">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)