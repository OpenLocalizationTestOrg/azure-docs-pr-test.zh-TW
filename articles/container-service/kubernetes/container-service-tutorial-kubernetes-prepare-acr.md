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
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="1b367-104">部署和使用 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="1b367-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="1b367-105">Azure Container Registry (ACR) 是以 Azure 為基礎的私人登錄，用於裝載 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="1b367-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="1b367-106">此教學課程中，七個，逐步解說部署容器登錄中 Azure 執行個體，並將容器映像 tooit 推入兩個部分。</span><span class="sxs-lookup"><span data-stu-id="1b367-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="1b367-107">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="1b367-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b367-108">部署 Azure Container Registry (ACR) 執行個體</span><span class="sxs-lookup"><span data-stu-id="1b367-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="1b367-109">標記 ACR 的容器映像</span><span class="sxs-lookup"><span data-stu-id="1b367-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="1b367-110">上傳 hello 映像 tooACR</span><span class="sxs-lookup"><span data-stu-id="1b367-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="1b367-111">在後續教學課程中，此 ACR 執行個體會與 Azure Container Service 的 Kubernetes 叢集整合，以便安全地執行容器映像。</span><span class="sxs-lookup"><span data-stu-id="1b367-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="1b367-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="1b367-112">Before you begin</span></span>

<span data-ttu-id="1b367-113">在 hello[上一個教學課程](./container-service-tutorial-kubernetes-prepare-app.md)，容器映像建立簡單的投票 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b367-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="1b367-114">在本教學課程中，此映像推入 tooan Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="1b367-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="1b367-115">如果您尚未建立 hello Azure 投票應用程式映像，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="1b367-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="1b367-116">或者，hello 步驟這裡所詳述使用任何容器映像的工作。</span><span class="sxs-lookup"><span data-stu-id="1b367-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="1b367-117">本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1b367-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1b367-118">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="1b367-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1b367-119">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="1b367-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="1b367-120">部署 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="1b367-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="1b367-121">部署 Azure Container Registry 時，您必須先有資源群組。</span><span class="sxs-lookup"><span data-stu-id="1b367-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="1b367-122">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="1b367-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="1b367-123">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="1b367-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1b367-124">在此範例中，資源群組命名為*myResourceGroup*會建立在 hello *westeurope*區域。</span><span class="sxs-lookup"><span data-stu-id="1b367-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="1b367-125">建立 Azure 容器登錄以 hello [az acr 建立](/cli/azure/acr#create)命令。</span><span class="sxs-lookup"><span data-stu-id="1b367-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="1b367-126">容器登錄中的 hello 名稱**必須是唯一的**。</span><span class="sxs-lookup"><span data-stu-id="1b367-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="1b367-127">Hello 的其餘本教學課程中，我們使用 「 acrname"做為預留位置您選擇的 hello 容器登錄名稱。</span><span class="sxs-lookup"><span data-stu-id="1b367-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="1b367-128">Container Registry 登入</span><span class="sxs-lookup"><span data-stu-id="1b367-128">Container registry login</span></span>

<span data-ttu-id="1b367-129">推送 tooit 映像之前，您必須登入 tooyour ACR 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1b367-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="1b367-130">使用 hello [az acr 登入](https://docs.microsoft.com/en-us/cli/azure/acr#login)命令 toocomplete hello 作業。</span><span class="sxs-lookup"><span data-stu-id="1b367-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="1b367-131">您必須指定 toohello 容器登錄中建立時的 tooprovide hello 唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="1b367-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="1b367-132">hello 命令會傳回 「 已成功登入 」 的訊息，一旦完成後。</span><span class="sxs-lookup"><span data-stu-id="1b367-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="1b367-133">標記容器映像</span><span class="sxs-lookup"><span data-stu-id="1b367-133">Tag container images</span></span>

<span data-ttu-id="1b367-134">每個容器映像必須加上 hello 登錄 hello loginServer 名稱 toobe。</span><span class="sxs-lookup"><span data-stu-id="1b367-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="1b367-135">這個標記可用於路由推入容器映像 tooan 映像登錄中時。</span><span class="sxs-lookup"><span data-stu-id="1b367-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="1b367-136">一份目前的映像，使用 hello toosee [docker 映像](https://docs.docker.com/engine/reference/commandline/images/)命令。</span><span class="sxs-lookup"><span data-stu-id="1b367-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="1b367-137">輸出：</span><span class="sxs-lookup"><span data-stu-id="1b367-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="1b367-138">tooget hello loginServer 名稱，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="1b367-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="1b367-139">現在，標記 hello *azure 投票前*hello loginServer hello 容器登錄中的映像。</span><span class="sxs-lookup"><span data-stu-id="1b367-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="1b367-140">此外，請加入`:redis-v1`toohello hello 映像名稱結尾。</span><span class="sxs-lookup"><span data-stu-id="1b367-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="1b367-141">此標記代表 hello 映像版本。</span><span class="sxs-lookup"><span data-stu-id="1b367-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="1b367-142">一旦標記，請執行 [docker 映像] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello 作業。</span><span class="sxs-lookup"><span data-stu-id="1b367-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="1b367-143">輸出：</span><span class="sxs-lookup"><span data-stu-id="1b367-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="1b367-144">推入映像 tooregistry</span><span class="sxs-lookup"><span data-stu-id="1b367-144">Push images tooregistry</span></span>

<span data-ttu-id="1b367-145">推播 hello *azure 投票前*映像 toohello 登錄。</span><span class="sxs-lookup"><span data-stu-id="1b367-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="1b367-146">使用下列範例中的 hello，取代從您的環境的 hello loginServer hello ACR loginServer 名稱。</span><span class="sxs-lookup"><span data-stu-id="1b367-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="1b367-147">這只需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1b367-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="1b367-148">列出登錄中的映像</span><span class="sxs-lookup"><span data-stu-id="1b367-148">List images in registry</span></span>

<span data-ttu-id="1b367-149">tooreturn 已推入 tooyour Azure 容器登錄中，使用者 hello 的映像清單[az acr 儲存機制清單](/cli/azure/acr/repository#list)命令。</span><span class="sxs-lookup"><span data-stu-id="1b367-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="1b367-150">更新 hello 命令與 hello ACR 執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="1b367-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="1b367-151">輸出：</span><span class="sxs-lookup"><span data-stu-id="1b367-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="1b367-152">Toosee hello 標記用於特定的映像，然後使用 hello [az acr 儲存機制顯示標籤](/cli/azure/acr/repository#show-tags)命令。</span><span class="sxs-lookup"><span data-stu-id="1b367-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="1b367-153">輸出：</span><span class="sxs-lookup"><span data-stu-id="1b367-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="1b367-154">在教學課程完成，hello 容器映像已儲存在私用的 Azure 容器登錄中執行個體。</span><span class="sxs-lookup"><span data-stu-id="1b367-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="1b367-155">此映像從 ACR tooa Kubernetes 叢集部署在後續的教學課程。</span><span class="sxs-lookup"><span data-stu-id="1b367-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b367-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b367-156">Next steps</span></span>

<span data-ttu-id="1b367-157">在本教學課程中，已備妥可用於 ACS Kubernetes 叢集中的 Azure Container Registry。</span><span class="sxs-lookup"><span data-stu-id="1b367-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="1b367-158">已完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b367-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1b367-159">已部署 Azure Container Registry 執行個體</span><span class="sxs-lookup"><span data-stu-id="1b367-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="1b367-160">已標記 ACR 的容器映像</span><span class="sxs-lookup"><span data-stu-id="1b367-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="1b367-161">上傳的 hello 映像 tooACR</span><span class="sxs-lookup"><span data-stu-id="1b367-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="1b367-162">前進 toohello 下一個教學課程的 toolearn 有關部署在 Azure 中的 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="1b367-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b367-163">部署 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="1b367-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)