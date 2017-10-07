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
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="56362-104">部署和使用 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="56362-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="56362-105">這是三段式教學課程的第二段。</span><span class="sxs-lookup"><span data-stu-id="56362-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="56362-106">在 hello[上一個步驟](./container-instances-tutorial-prepare-app.md)，以撰寫簡單的 web 應用程式建立的容器映像[Node.js](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="56362-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="56362-107">在本教學課程中，此映像推入 tooan Azure 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="56362-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="56362-108">如果您尚未建立 hello 容器映像，傳回太[教學課程 1 – 建立容器映像](./container-instances-tutorial-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="56362-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="56362-109">hello Azure 容器登錄中是以 Azure 為基礎的私人登錄中，為 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="56362-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="56362-110">本教學課程會逐步部署容器登錄中 Azure 執行個體，並將容器映像 tooit 推入。</span><span class="sxs-lookup"><span data-stu-id="56362-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="56362-111">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="56362-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56362-112">部署 Azure Container Registry 執行個體</span><span class="sxs-lookup"><span data-stu-id="56362-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="56362-113">標記 Azure Container Registry 的容器映像</span><span class="sxs-lookup"><span data-stu-id="56362-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="56362-114">上傳映像 tooAzure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="56362-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="56362-115">在後續的教學課程中，您可以部署 hello 容器從您私用登錄 tooAzure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="56362-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="56362-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="56362-116">Before you begin</span></span>

<span data-ttu-id="56362-117">本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="56362-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="56362-118">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="56362-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="56362-119">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="56362-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="56362-120">部署 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="56362-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="56362-121">部署 Azure Container Registry 時，您必須先有資源群組。</span><span class="sxs-lookup"><span data-stu-id="56362-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="56362-122">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯集合。</span><span class="sxs-lookup"><span data-stu-id="56362-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="56362-123">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="56362-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="56362-124">在此範例中，資源群組命名為*myResourceGroup*會建立在 hello *eastus*區域。</span><span class="sxs-lookup"><span data-stu-id="56362-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="56362-125">建立 Azure 容器登錄以 hello [az acr 建立](/cli/azure/acr#create)命令。</span><span class="sxs-lookup"><span data-stu-id="56362-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="56362-126">容器登錄中的 hello 名稱**必須是唯一的**。</span><span class="sxs-lookup"><span data-stu-id="56362-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="56362-127">在下列範例的 hello，我們使用 hello 名稱*mycontainerregistry082*。</span><span class="sxs-lookup"><span data-stu-id="56362-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="56362-128">在本教學課程的 hello 其餘部分，我們使用`<acrname>`作為您所選擇的 hello 容器登錄名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="56362-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="56362-129">Container Registry 登入</span><span class="sxs-lookup"><span data-stu-id="56362-129">Container registry login</span></span>

<span data-ttu-id="56362-130">推送 tooit 映像之前，您必須登入 tooyour ACR 執行個體。</span><span class="sxs-lookup"><span data-stu-id="56362-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="56362-131">使用 hello [az acr 登入](https://docs.microsoft.com/en-us/cli/azure/acr#login)命令 toocomplete hello 作業。</span><span class="sxs-lookup"><span data-stu-id="56362-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="56362-132">您必須指定 toohello 容器登錄中建立時的 tooprovide hello 唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="56362-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="56362-133">hello 命令會傳回 「 已成功登入 」 的訊息，一旦完成後。</span><span class="sxs-lookup"><span data-stu-id="56362-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="56362-134">標記容器映像</span><span class="sxs-lookup"><span data-stu-id="56362-134">Tag container image</span></span>

<span data-ttu-id="56362-135">toodeploy 私人登錄中的容器映像，hello 映像必須加上 hello toobe `loginServer` hello 登錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="56362-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="56362-136">一份目前的映像，使用 hello toosee`docker images`命令。</span><span class="sxs-lookup"><span data-stu-id="56362-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="56362-137">輸出：</span><span class="sxs-lookup"><span data-stu-id="56362-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="56362-138">tooget hello loginServer 名稱，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="56362-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="56362-139">標記 hello *aci 教學課程應用*hello loginServer hello 容器登錄中的映像。</span><span class="sxs-lookup"><span data-stu-id="56362-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="56362-140">此外，請加入`:v1`toohello hello 映像名稱結尾。</span><span class="sxs-lookup"><span data-stu-id="56362-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="56362-141">此標記代表 hello 映像的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="56362-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="56362-142">加上標記，一旦執行`docker images`tooverify hello 作業。</span><span class="sxs-lookup"><span data-stu-id="56362-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="56362-143">輸出：</span><span class="sxs-lookup"><span data-stu-id="56362-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="56362-144">推入映像 tooAzure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="56362-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="56362-145">推播 hello *aci 教學課程應用*映像 toohello 登錄。</span><span class="sxs-lookup"><span data-stu-id="56362-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="56362-146">使用下列範例中的 hello，取代從您的環境的 hello loginServer hello 容器登錄 loginServer 名稱。</span><span class="sxs-lookup"><span data-stu-id="56362-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="56362-147">在 Azure Container Registry 中列出映像</span><span class="sxs-lookup"><span data-stu-id="56362-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="56362-148">tooreturn 已推入 tooyour Azure 容器登錄中，使用者 hello 的映像清單[az acr 儲存機制清單](/cli/azure/acr/repository#list)命令。</span><span class="sxs-lookup"><span data-stu-id="56362-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="56362-149">更新 hello 容器登錄名稱的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="56362-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="56362-150">輸出：</span><span class="sxs-lookup"><span data-stu-id="56362-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="56362-151">Toosee hello 標記用於特定的映像，然後使用 hello [az acr 儲存機制顯示標籤](/cli/azure/acr/repository#show-tags)命令。</span><span class="sxs-lookup"><span data-stu-id="56362-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="56362-152">輸出：</span><span class="sxs-lookup"><span data-stu-id="56362-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="56362-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56362-153">Next steps</span></span>

<span data-ttu-id="56362-154">在本教學課程中，Azure 容器登錄中已備妥用於 Azure 容器執行個體，而且 hello 容器映像已推入。</span><span class="sxs-lookup"><span data-stu-id="56362-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="56362-155">已完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="56362-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56362-156">部署 Azure Container Registry 執行個體</span><span class="sxs-lookup"><span data-stu-id="56362-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="56362-157">標記 Azure Container Registry 的容器映像</span><span class="sxs-lookup"><span data-stu-id="56362-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="56362-158">上傳映像 tooAzure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="56362-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="56362-159">前進 toohello 下一個教學課程的 toolearn 有關部署 hello 容器 tooAzure 使用 Azure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="56362-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56362-160">部署容器 tooAzure 容器執行個體</span><span class="sxs-lookup"><span data-stu-id="56362-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
