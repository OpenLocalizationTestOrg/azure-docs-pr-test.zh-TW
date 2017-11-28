---
title: "Azure Container Service 教學課程 - 更新應用程式 | Microsoft Docs"
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
ms.openlocfilehash: db580da3e2d70892bc37305394df5be609ebb8a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="3115c-104">在 Kubernetes 中更新應用程式</span><span class="sxs-lookup"><span data-stu-id="3115c-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="3115c-105">在 Kubernetes 中部署應用程式之後，您可以藉由指定新的容器映像或映像版本來進行更新。</span><span class="sxs-lookup"><span data-stu-id="3115c-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="3115c-106">當您更新應用程式時，更新會分段推出，所以只有一部分的部署會同時更新。</span><span class="sxs-lookup"><span data-stu-id="3115c-106">When you update an application, the update rollout is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="3115c-107">此分段更新可讓應用程式在更新期間繼續執行，並且在發生部署失敗時提供復原機制。</span><span class="sxs-lookup"><span data-stu-id="3115c-107">This staged update enables the application to keep running during the update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="3115c-108">在本教學課程 (6/7 部分) 中，已更新範例 Azure Vote 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3115c-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="3115c-109">您完成的工作包括：</span><span class="sxs-lookup"><span data-stu-id="3115c-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3115c-110">更新前端應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="3115c-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="3115c-111">建立已更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="3115c-111">Creating an updated container image</span></span>
> * <span data-ttu-id="3115c-112">將容器映像推送至 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3115c-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="3115c-113">部署已更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="3115c-113">Deploying the updated container image</span></span>

<span data-ttu-id="3115c-114">在後續教學課程中，會將 Operations Management Suite 設定為監視 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="3115c-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3115c-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="3115c-115">Before you begin</span></span>

<span data-ttu-id="3115c-116">在先前的教學課程中，已將應用程式封裝成容器映像、將這些映像上傳至 Azure Container Registry，並已建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="3115c-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="3115c-117">該應用程式接著便在 Kubernetes 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="3115c-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="3115c-118">如果您尚未完成這些步驟，而想要跟著做，請回到[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="3115c-118">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="3115c-119">更新應用程式</span><span class="sxs-lookup"><span data-stu-id="3115c-119">Update application</span></span>

<span data-ttu-id="3115c-120">若要完成本教學課程中的步驟，您必須複製一份 Azure Vote 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3115c-120">To complete the steps in this tutorial, you must have cloned a copy of the Azure Vote application.</span></span> <span data-ttu-id="3115c-121">如有必要，請使用下列命令建立此複製的複本：</span><span class="sxs-lookup"><span data-stu-id="3115c-121">If necessary, create this cloned copy with the following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="3115c-122">使用任何程式碼或文字編輯器開啟 `config_file.cfg` 檔案。</span><span class="sxs-lookup"><span data-stu-id="3115c-122">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="3115c-123">您可以在所複製存放庫的下列目錄下找到這個檔案。</span><span class="sxs-lookup"><span data-stu-id="3115c-123">You can find this file under the following directory of the cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="3115c-124">變更 `VOTE1VALUE` 和 `VOTE2VALUE` 的值，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="3115c-124">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="3115c-125">使用 [docker-compose](https://docs.docker.com/compose/) 重新建立前端映像，並執行已更新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3115c-125">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="3115c-126">在本機測試應用程式</span><span class="sxs-lookup"><span data-stu-id="3115c-126">Test application locally</span></span>

<span data-ttu-id="3115c-127">瀏覽至 `http://localhost:8080` 以查看已更新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3115c-127">Browse to `http://localhost:8080` to see the updated application.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="3115c-129">標記和推送映像</span><span class="sxs-lookup"><span data-stu-id="3115c-129">Tag and push images</span></span>

<span data-ttu-id="3115c-130">以容器登錄的 loginServer 標記 *azure-vote-front* 映像。</span><span class="sxs-lookup"><span data-stu-id="3115c-130">Tag the *azure-vote-front* image with the loginServer of the container registry.</span></span>

<span data-ttu-id="3115c-131">如果您使用 Azure Container Registry，請使用 [az acr list](/cli/azure/acr#list) 命令取得登入伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="3115c-131">If you're using Azure Container Registry, get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="3115c-132">使用 [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) 來標記映像。</span><span class="sxs-lookup"><span data-stu-id="3115c-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="3115c-133">以您的 Azure Container Registry 登入伺服器名稱或公用登錄主機名稱取代 `<acrLoginServer>`。</span><span class="sxs-lookup"><span data-stu-id="3115c-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="3115c-134">使用 [docker push](https://docs.docker.com/engine/reference/commandline/push/) 將映像上傳至您的登錄。</span><span class="sxs-lookup"><span data-stu-id="3115c-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="3115c-135">以您的 Azure Container Registry 登入伺服器名稱或公用登錄主機名稱取代 `<acrLoginServer>`。</span><span class="sxs-lookup"><span data-stu-id="3115c-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="3115c-136">部署更新應用程式</span><span class="sxs-lookup"><span data-stu-id="3115c-136">Deploy update application</span></span>

<span data-ttu-id="3115c-137">若要確保最大執行時間，則應用程式 pod 必須有多個執行個體正在執行中。</span><span class="sxs-lookup"><span data-stu-id="3115c-137">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="3115c-138">請使用 [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 命令驗證此組態。</span><span class="sxs-lookup"><span data-stu-id="3115c-138">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="3115c-139">輸出：</span><span class="sxs-lookup"><span data-stu-id="3115c-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="3115c-140">如果您沒有執行 azure-vote-front 映像的多個 pod，請調整 *azure-vote-front* 部署。</span><span class="sxs-lookup"><span data-stu-id="3115c-140">If you don't have multiple pods running the azure-vote-front image, scale the *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="3115c-141">若要更新應用程式，請使用 [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) 命令。</span><span class="sxs-lookup"><span data-stu-id="3115c-141">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="3115c-142">以容器登錄的登入伺服器或主機名稱來更新 `<acrLoginServer>`。</span><span class="sxs-lookup"><span data-stu-id="3115c-142">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="3115c-143">若要監視部署，請使用 [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 命令。</span><span class="sxs-lookup"><span data-stu-id="3115c-143">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="3115c-144">部署已更新的應用程式後，您的 pod 會終止並以新的容器映像重建。</span><span class="sxs-lookup"><span data-stu-id="3115c-144">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="3115c-145">輸出：</span><span class="sxs-lookup"><span data-stu-id="3115c-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="3115c-146">測試已更新的應用程式</span><span class="sxs-lookup"><span data-stu-id="3115c-146">Test updated application</span></span>

<span data-ttu-id="3115c-147">取得 *azure-vote-front* 服務的外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3115c-147">Get the external IP address of the *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="3115c-148">瀏覽至此 IP 位址以查看已更新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3115c-148">Browse to the IP address to see the updated application.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="3115c-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3115c-150">Next steps</span></span>

<span data-ttu-id="3115c-151">在本教學課程中，您已更新應用程式並將此更新推出至 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="3115c-151">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="3115c-152">已完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="3115c-152">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3115c-153">更新了前端應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="3115c-153">Updated the front-end application code</span></span>
> * <span data-ttu-id="3115c-154">建立了已更新的容器映像</span><span class="sxs-lookup"><span data-stu-id="3115c-154">Created an updated container image</span></span>
> * <span data-ttu-id="3115c-155">已將容器映像推送至 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3115c-155">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="3115c-156">部署了已更新的應用程式</span><span class="sxs-lookup"><span data-stu-id="3115c-156">Deployed the updated application</span></span>

<span data-ttu-id="3115c-157">請前進到下一個教學課程，了解如何利用 Operations Management Suite 監視 Kubernetes。</span><span class="sxs-lookup"><span data-stu-id="3115c-157">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3115c-158">透過 OMS 監視 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3115c-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)