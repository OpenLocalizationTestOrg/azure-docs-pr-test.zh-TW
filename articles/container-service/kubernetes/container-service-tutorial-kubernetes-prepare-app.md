---
title: "aaaAzure 容器服務教學課程-準備應用程式 |Microsoft 文件"
description: "Azure Container Service 教學課程 - 準備應用程式"
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a><span data-ttu-id="75b1c-104">建立容器映像 toobe 搭配 Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="75b1c-104">Create container images toobe used with Azure Container Service</span></span>

<span data-ttu-id="75b1c-105">在本教學課程 (七個章節的第一部分) 中，多容器應用程式已準備好用於 Kubernetes。</span><span class="sxs-lookup"><span data-stu-id="75b1c-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="75b1c-106">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="75b1c-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="75b1c-107">從 GitHub 複製應用程式來源</span><span class="sxs-lookup"><span data-stu-id="75b1c-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="75b1c-108">從 hello 應用程式來源中建立的容器映像</span><span class="sxs-lookup"><span data-stu-id="75b1c-108">Creating a container image from hello application source</span></span>
> * <span data-ttu-id="75b1c-109">在本機的 Docker 環境中測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="75b1c-109">Testing hello application in a local Docker environment</span></span>

<span data-ttu-id="75b1c-110">一旦完成，hello 下列應用程式是在本機開發環境中存取。</span><span class="sxs-lookup"><span data-stu-id="75b1c-110">Once completed, hello following application is accessible in your local development environment.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="75b1c-112">在後續的教學課程，hello 容器映像已上傳的 tooan Azure 容器登錄中，而然後在 Azure 中的執行裝載 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="75b1c-112">In subsequent tutorials, hello container image is uploaded tooan Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="75b1c-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="75b1c-113">Before you begin</span></span>

<span data-ttu-id="75b1c-114">本教學課程假設使用者對核心 Docker 概念有基本認識，例如容器、容器映像和基本 Docker 命令。</span><span class="sxs-lookup"><span data-stu-id="75b1c-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="75b1c-115">如有需要，請參閱[開始使用 Docker]( https://docs.docker.com/get-started/)以取得容器基本概念入門。</span><span class="sxs-lookup"><span data-stu-id="75b1c-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="75b1c-116">toocomplete 本教學課程中，您需要 Docker 開發環境。</span><span class="sxs-lookup"><span data-stu-id="75b1c-116">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="75b1c-117">Docker 提供可輕鬆在 [Mac](https://docs.docker.com/docker-for-mac/)、[Windows](https://docs.docker.com/docker-for-windows/) 或 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 系統上設定 Docker 的套件。</span><span class="sxs-lookup"><span data-stu-id="75b1c-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="75b1c-118">取得應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="75b1c-118">Get application code</span></span>

<span data-ttu-id="75b1c-119">在本教學課程中使用的 hello 範例應用程式是基本的投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b1c-119">hello sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="75b1c-120">hello 應用程式是由 web 前端元件及後端 Redis 執行個體所組成。</span><span class="sxs-lookup"><span data-stu-id="75b1c-120">hello application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="75b1c-121">hello web 元件封裝成自訂容器映像。</span><span class="sxs-lookup"><span data-stu-id="75b1c-121">hello web component is packaged into a custom container image.</span></span> <span data-ttu-id="75b1c-122">hello Redis 執行個體使用的未修改的映像從 Docker Hub。</span><span class="sxs-lookup"><span data-stu-id="75b1c-122">hello Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="75b1c-123">使用 git toodownload hello 應用程式 tooyour 開發環境的複本。</span><span class="sxs-lookup"><span data-stu-id="75b1c-123">Use git toodownload a copy of hello application tooyour development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="75b1c-124">內部 hello 複製的目錄 hello 應用程式的原始程式碼，預先建立的 Docker compose 檔和 Kubernetes 資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="75b1c-124">Inside hello cloned directory is hello application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="75b1c-125">這些檔案是使用的 toocreate 資產到 hello 教學課程集。</span><span class="sxs-lookup"><span data-stu-id="75b1c-125">These files are used toocreate assets throughout hello tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="75b1c-126">建立容器映像</span><span class="sxs-lookup"><span data-stu-id="75b1c-126">Create container images</span></span>

<span data-ttu-id="75b1c-127">[Docker 撰寫](https://docs.docker.com/compose/)可以是使用 tooautomate hello 建置現成可用的容器映像和 hello 多容器應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="75b1c-127">[Docker Compose](https://docs.docker.com/compose/) can be used tooautomate hello build out of container images and hello deployment of multi-container applications.</span></span>

<span data-ttu-id="75b1c-128">執行 hello docker compose.yml 檔案 toocreate hello 容器映像，下載 hello Redis 映像，並啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b1c-128">Run hello docker-compose.yml file toocreate hello container image, download hello Redis image, and start hello application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="75b1c-129">完成時，使用 hello [docker 映像](https://docs.docker.com/engine/reference/commandline/images/)命令 toosee hello 建立映像。</span><span class="sxs-lookup"><span data-stu-id="75b1c-129">When completed, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command toosee hello created images.</span></span>

```bash
docker images
```

<span data-ttu-id="75b1c-130">請注意，已下載或建立三個映像。</span><span class="sxs-lookup"><span data-stu-id="75b1c-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="75b1c-131">hello *azure 投票前*映像包含 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b1c-131">hello *azure-vote-front* image contains hello application.</span></span> <span data-ttu-id="75b1c-132">它衍生自 hello *nginx 酒瓶*映像。</span><span class="sxs-lookup"><span data-stu-id="75b1c-132">It was derived from hello *nginx-flask* image.</span></span> <span data-ttu-id="75b1c-133">從 Docker Hub 下載 hello Redis 映像。</span><span class="sxs-lookup"><span data-stu-id="75b1c-133">hello Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="75b1c-134">執行 hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/)命令 toosee hello 執行中的容器。</span><span class="sxs-lookup"><span data-stu-id="75b1c-134">Run hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command toosee hello running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="75b1c-135">輸出：</span><span class="sxs-lookup"><span data-stu-id="75b1c-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="75b1c-136">在本機測試應用程式</span><span class="sxs-lookup"><span data-stu-id="75b1c-136">Test application locally</span></span>

<span data-ttu-id="75b1c-137">瀏覽 toohttp://localhost:8080 toosee hello 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b1c-137">Browse toohttp://localhost:8080 toosee hello running application.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="75b1c-139">清除資源</span><span class="sxs-lookup"><span data-stu-id="75b1c-139">Clean up resources</span></span>

<span data-ttu-id="75b1c-140">既然已經驗證應用程式的功能，就可以停止並移除 hello 執行中的容器。</span><span class="sxs-lookup"><span data-stu-id="75b1c-140">Now that application functionality has been validated, hello running containers can be stopped and removed.</span></span> <span data-ttu-id="75b1c-141">請勿刪除 hello 容器映像。</span><span class="sxs-lookup"><span data-stu-id="75b1c-141">Do not delete hello container images.</span></span> <span data-ttu-id="75b1c-142">hello *azure 投票前*映像處於 hello 下一個教學課程的上傳的 tooan Azure 容器登錄中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="75b1c-142">hello *azure-vote-front* image is uploaded tooan Azure Container Registry instance in hello next tutorial.</span></span>

<span data-ttu-id="75b1c-143">執行下列 toostop hello 執行容器的 hello。</span><span class="sxs-lookup"><span data-stu-id="75b1c-143">Run hello following toostop hello running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="75b1c-144">使用下列命令的 hello 來刪除 hello 停止容器。</span><span class="sxs-lookup"><span data-stu-id="75b1c-144">Delete hello stopped containers with hello following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="75b1c-145">在完成時，您必須包含 hello Azure 投票應用程式的容器映像。</span><span class="sxs-lookup"><span data-stu-id="75b1c-145">At completion, you have a container image that contains hello Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75b1c-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75b1c-146">Next steps</span></span>

<span data-ttu-id="75b1c-147">在本教學課程中，應用程式已通過測試，且容器映像建立 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b1c-147">In this tutorial, an application was tested and container images created for hello application.</span></span> <span data-ttu-id="75b1c-148">已完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="75b1c-148">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75b1c-149">從 GitHub 複製 hello 應用程式來源</span><span class="sxs-lookup"><span data-stu-id="75b1c-149">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="75b1c-150">已從應用程式來源建立容器映像</span><span class="sxs-lookup"><span data-stu-id="75b1c-150">Created a container image from application source</span></span>
> * <span data-ttu-id="75b1c-151">在本機的 Docker 環境中測試的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="75b1c-151">Tested hello application in a local Docker environment</span></span>

<span data-ttu-id="75b1c-152">前進 toohello 下一個教學課程的 toolearn 有關在 Azure 容器登錄中儲存容器映像。</span><span class="sxs-lookup"><span data-stu-id="75b1c-152">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75b1c-153">推入映像 tooAzure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="75b1c-153">Push images tooAzure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
