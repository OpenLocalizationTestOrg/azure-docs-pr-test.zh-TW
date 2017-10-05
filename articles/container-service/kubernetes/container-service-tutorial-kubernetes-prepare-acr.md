---
title: "Azure Container Service 教學課程 - 準備 ACR | Microsoft Docs"
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
ms.openlocfilehash: 3e1f7617bf2fc52ee4c15598f51a46276f4dc57d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="99a98-104">部署和使用 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="99a98-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="99a98-105">Azure Container Registry (ACR) 是以 Azure 為基礎的私人登錄，用於裝載 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="99a98-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="99a98-106">本教學課程 (2/7 部分) 逐步解說如何部署 Azure Container Registry 執行個體，以及將容器映像推送至該執行個體。</span><span class="sxs-lookup"><span data-stu-id="99a98-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="99a98-107">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="99a98-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="99a98-108">部署 Azure Container Registry (ACR) 執行個體</span><span class="sxs-lookup"><span data-stu-id="99a98-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="99a98-109">標記 ACR 的容器映像</span><span class="sxs-lookup"><span data-stu-id="99a98-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="99a98-110">將映像上傳至 ACR</span><span class="sxs-lookup"><span data-stu-id="99a98-110">Uploading the image to ACR</span></span>

<span data-ttu-id="99a98-111">在後續教學課程中，此 ACR 執行個體會與 Azure Container Service 的 Kubernetes 叢集整合，以便安全地執行容器映像。</span><span class="sxs-lookup"><span data-stu-id="99a98-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="99a98-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="99a98-112">Before you begin</span></span>

<span data-ttu-id="99a98-113">在[上一個教學課程](./container-service-tutorial-kubernetes-prepare-app.md)中，已針對簡單的 Azure Voting 應用程式建立容器映像。</span><span class="sxs-lookup"><span data-stu-id="99a98-113">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="99a98-114">在本教學課程中，此映像會推送至 Azure Container Registry。</span><span class="sxs-lookup"><span data-stu-id="99a98-114">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="99a98-115">如果您尚未建立 Azure Voting 應用程式映像，請回到[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="99a98-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="99a98-116">或者，將這裡詳述的步驟使用於任何容器映像。</span><span class="sxs-lookup"><span data-stu-id="99a98-116">Alternatively, the steps detailed here work with any container image.</span></span>

<span data-ttu-id="99a98-117">本教學課程需要您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="99a98-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="99a98-118">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="99a98-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="99a98-119">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="99a98-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="99a98-120">部署 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="99a98-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="99a98-121">部署 Azure Container Registry 時，您必須先有資源群組。</span><span class="sxs-lookup"><span data-stu-id="99a98-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="99a98-122">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="99a98-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="99a98-123">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="99a98-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="99a98-124">在此範例中，會在 westeurope 區域中建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="99a98-124">In this example, a resource group named *myResourceGroup* is created in the *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="99a98-125">使用 [az acr create](/cli/azure/acr#create) 命令來建立 Azure Container Registry。</span><span class="sxs-lookup"><span data-stu-id="99a98-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="99a98-126">Container Registry 的名稱**必須是唯一的**。</span><span class="sxs-lookup"><span data-stu-id="99a98-126">The name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="99a98-127">在本教學課程的其餘部分，我們使用 "acrname" 作為您選擇之容器登錄名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="99a98-127">Throughout the rest of this tutorial, we use "acrname" as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="99a98-128">Container Registry 登入</span><span class="sxs-lookup"><span data-stu-id="99a98-128">Container registry login</span></span>

<span data-ttu-id="99a98-129">您必須先登入 ACR 執行個體，再將映像推送到它。</span><span class="sxs-lookup"><span data-stu-id="99a98-129">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="99a98-130">使用 [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) 命令來完成此作業。</span><span class="sxs-lookup"><span data-stu-id="99a98-130">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="99a98-131">您必須在建立容器登錄時，為容器登錄提供唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="99a98-131">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="99a98-132">此命令在完成之後會傳回「登入成功」訊息。</span><span class="sxs-lookup"><span data-stu-id="99a98-132">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="99a98-133">標記容器映像</span><span class="sxs-lookup"><span data-stu-id="99a98-133">Tag container images</span></span>

<span data-ttu-id="99a98-134">每個容器映像都必須標記登錄的 loginServer 名稱。</span><span class="sxs-lookup"><span data-stu-id="99a98-134">Each container image needs to be tagged with the loginServer name of the registry.</span></span> <span data-ttu-id="99a98-135">將容器映像推送到映像登錄時，此標籤可用於路由傳送。</span><span class="sxs-lookup"><span data-stu-id="99a98-135">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="99a98-136">若要查看目前的映像清單，請使用 [docker images](https://docs.docker.com/engine/reference/commandline/images/) 命令。</span><span class="sxs-lookup"><span data-stu-id="99a98-136">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="99a98-137">輸出：</span><span class="sxs-lookup"><span data-stu-id="99a98-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="99a98-138">若要取得 loginServer 名稱，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="99a98-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="99a98-139">現在，以容器登錄的 loginServer 標記 azure-vote-front 映像。</span><span class="sxs-lookup"><span data-stu-id="99a98-139">Now, tag the *azure-vote-front* image with the loginServer of the container registry.</span></span> <span data-ttu-id="99a98-140">此外，將 `:redis-v1` 新增至映像名稱的結尾。</span><span class="sxs-lookup"><span data-stu-id="99a98-140">Also, add `:redis-v1` to the end of the image name.</span></span> <span data-ttu-id="99a98-141">此標籤指示映像版本。</span><span class="sxs-lookup"><span data-stu-id="99a98-141">This tag indicates the image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="99a98-142">一旦標記，請執行 [docker images] (https://docs.docker.com/engine/reference/commandline/images/) 來驗證作業。</span><span class="sxs-lookup"><span data-stu-id="99a98-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="99a98-143">輸出：</span><span class="sxs-lookup"><span data-stu-id="99a98-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="99a98-144">將映像推送到登錄</span><span class="sxs-lookup"><span data-stu-id="99a98-144">Push images to registry</span></span>

<span data-ttu-id="99a98-145">將 *azure-vote-front* 映像推送到登錄。</span><span class="sxs-lookup"><span data-stu-id="99a98-145">Push the *azure-vote-front* image to the registry.</span></span> 

<span data-ttu-id="99a98-146">使用下列範例，以您環境中的 loginServer 取代 ACR loginServer 名稱。</span><span class="sxs-lookup"><span data-stu-id="99a98-146">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="99a98-147">這需要幾分鐘的時間完成。</span><span class="sxs-lookup"><span data-stu-id="99a98-147">This takes a couple of minutes to complete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="99a98-148">列出登錄中的映像</span><span class="sxs-lookup"><span data-stu-id="99a98-148">List images in registry</span></span>

<span data-ttu-id="99a98-149">若要傳回已推送至 Azure Container Registry 的映像清單，請使用 [az acr repository list](/cli/azure/acr/repository#list) 命令。</span><span class="sxs-lookup"><span data-stu-id="99a98-149">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="99a98-150">以 ACR 執行個體名稱更新命令。</span><span class="sxs-lookup"><span data-stu-id="99a98-150">Update the command with the ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="99a98-151">輸出：</span><span class="sxs-lookup"><span data-stu-id="99a98-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="99a98-152">而後若要查看特定映像的標籤，請使用 [az acr repository show-tags](/cli/azure/acr/repository#show-tags) 命令。</span><span class="sxs-lookup"><span data-stu-id="99a98-152">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="99a98-153">輸出：</span><span class="sxs-lookup"><span data-stu-id="99a98-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="99a98-154">當教學課程完成時，私人 Azure Container Registry 執行個體中已儲存容器映像。</span><span class="sxs-lookup"><span data-stu-id="99a98-154">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="99a98-155">在後續的教學課程中，此映像會從 ACR 部署到 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="99a98-155">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99a98-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99a98-156">Next steps</span></span>

<span data-ttu-id="99a98-157">在本教學課程中，已備妥可用於 ACS Kubernetes 叢集中的 Azure Container Registry。</span><span class="sxs-lookup"><span data-stu-id="99a98-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="99a98-158">已完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="99a98-158">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="99a98-159">已部署 Azure Container Registry 執行個體</span><span class="sxs-lookup"><span data-stu-id="99a98-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="99a98-160">已標記 ACR 的容器映像</span><span class="sxs-lookup"><span data-stu-id="99a98-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="99a98-161">已將映像上傳至 ACR</span><span class="sxs-lookup"><span data-stu-id="99a98-161">Uploaded the image to ACR</span></span>

<span data-ttu-id="99a98-162">請前進到下一個教學課程，了解如何在 Azure 中部署 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="99a98-162">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99a98-163">部署 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="99a98-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)