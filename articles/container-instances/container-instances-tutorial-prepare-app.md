---
title: "aaaAzure 容器執行個體的教學課程-準備您的應用程式 |Azure 文件"
description: "準備部署 tooAzure 容器執行個體的應用程式"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="8c9d4-103">建立部署 tooAzure 容器執行個體的容器</span><span class="sxs-lookup"><span data-stu-id="8c9d4-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="8c9d4-104">Azure Container Instances 能夠將 Docker 容器部署至 Azure 基礎結構，而不需要佈建任何虛擬機器，或採用較高層級的任何服務。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="8c9d4-105">在本教學課程中，您將以 Node.js 建置簡單的 Web 應用程式，然後封裝在可使用 Azure Container Instances 來執行的容器中。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="8c9d4-106">我們將討論：</span><span class="sxs-lookup"><span data-stu-id="8c9d4-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8c9d4-107">從 GitHub 複製應用程式來源</span><span class="sxs-lookup"><span data-stu-id="8c9d4-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="8c9d4-108">從應用程式來源建立容器映像</span><span class="sxs-lookup"><span data-stu-id="8c9d4-108">Creating container images from application source</span></span>
> * <span data-ttu-id="8c9d4-109">在本機的 Docker 環境中測試 hello 映像</span><span class="sxs-lookup"><span data-stu-id="8c9d4-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="8c9d4-110">在後續教學課程中，您將上傳您的映像 tooan Azure 容器登錄中，然後再部署它們 tooAzure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8c9d4-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="8c9d4-111">Before you begin</span></span>

<span data-ttu-id="8c9d4-112">本教學課程假設使用者對核心 Docker 概念有基本認識，例如容器、容器映像和基本 Docker 命令。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="8c9d4-113">如有需要，請參閱[開始使用 Docker]( https://docs.docker.com/get-started/)以取得容器基本概念入門。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="8c9d4-114">toocomplete 本教學課程中，您需要 Docker 開發環境。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="8c9d4-115">Docker 提供可輕鬆在 [Mac](https://docs.docker.com/docker-for-mac/)、[Windows](https://docs.docker.com/docker-for-windows/) 或 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 系統上設定 Docker 的套件。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="8c9d4-116">取得應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="8c9d4-116">Get application code</span></span>

<span data-ttu-id="8c9d4-117">在此教學課程中的 hello 範例包含簡單的 web 應用程式內建[Node.js](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="8c9d4-118">hello 應用程式是靜態的 HTML 網頁，並看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="8c9d4-118">hello app serves a static HTML page and looks like this:</span></span>

![在瀏覽器中顯示的教學課程應用程式][aci-tutorial-app]

<span data-ttu-id="8c9d4-120">使用 git toodownload hello 範例：</span><span class="sxs-lookup"><span data-stu-id="8c9d4-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="8c9d4-121">建立 hello 容器映像</span><span class="sxs-lookup"><span data-stu-id="8c9d4-121">Build hello container image</span></span>

<span data-ttu-id="8c9d4-122">hello hello 範例儲存機制中提供的 Dockerfile 顯示 hello 容器的建立方式。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="8c9d4-123">它會從開始[官方 Node.js 映像][ dockerhub-nodeimage]根據[Alpine Linux](https://alpinelinux.org/)，是很適合的 toouse 與容器的小型分佈。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="8c9d4-124">接著將 hello 應用程式檔案複製到 hello 容器，會安裝相依性使用 hello Node 封裝管理員，而且最後會開始 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="8c9d4-125">使用 hello`docker build`命令 toocreate hello 容器映像，標記成*aci 教學課程應用*:</span><span class="sxs-lookup"><span data-stu-id="8c9d4-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="8c9d4-126">使用 hello `docker images` toosee hello 建置映像：</span><span class="sxs-lookup"><span data-stu-id="8c9d4-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="8c9d4-127">輸出：</span><span class="sxs-lookup"><span data-stu-id="8c9d4-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="8c9d4-128">在本機執行 hello 容器</span><span class="sxs-lookup"><span data-stu-id="8c9d4-128">Run hello container locally</span></span>

<span data-ttu-id="8c9d4-129">您嘗試部署 hello 容器 tooAzure 容器執行個體之前，本機執行 tooconfirm 正常運作。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="8c9d4-130">hello`-d`參數讓 hello 容器 hello 背景中執行時`-p`可讓您 toomap 您計算 tooport 80 hello 容器中的任意連接埠。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="8c9d4-131">Hello 容器開啟 hello 瀏覽器 toohttp://localhost:8080 tooconfirm 正在執行。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Hello 瀏覽器中的本機執行 hello 應用程式][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="8c9d4-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c9d4-133">Next steps</span></span>

<span data-ttu-id="8c9d4-134">在此教學課程中，您可以建立容器映像可以部署的 tooAzure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="8c9d4-135">已完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c9d4-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8c9d4-136">從 GitHub 複製 hello 應用程式來源</span><span class="sxs-lookup"><span data-stu-id="8c9d4-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="8c9d4-137">從應用程式來源建立容器映像</span><span class="sxs-lookup"><span data-stu-id="8c9d4-137">Creating container images from application source</span></span>
> * <span data-ttu-id="8c9d4-138">在本機測試 hello 容器</span><span class="sxs-lookup"><span data-stu-id="8c9d4-138">Testing hello container locally</span></span>

<span data-ttu-id="8c9d4-139">前進 toohello 下一個教學課程的 toolearn 有關在 Azure 容器登錄中儲存容器映像。</span><span class="sxs-lookup"><span data-stu-id="8c9d4-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8c9d4-140">推入映像 tooAzure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="8c9d4-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png