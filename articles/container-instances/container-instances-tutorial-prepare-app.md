---
title: "Azure Container Instances 教學課程 - 準備您的應用程式 | Azure Docs"
description: "準備應用程式以便部署至 Azure Container Instances"
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
ms.openlocfilehash: 167297e10eed11833623ff797e676ad43c65f9ad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-container-for-deployment-to-azure-container-instances"></a><span data-ttu-id="39339-103">建立容器以部署至 Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="39339-103">Create container for deployment to Azure Container Instances</span></span>

<span data-ttu-id="39339-104">Azure Container Instances 能夠將 Docker 容器部署至 Azure 基礎結構，而不需要佈建任何虛擬機器，或採用較高層級的任何服務。</span><span class="sxs-lookup"><span data-stu-id="39339-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="39339-105">在本教學課程中，您將以 Node.js 建置簡單的 Web 應用程式，然後封裝在可使用 Azure Container Instances 來執行的容器中。</span><span class="sxs-lookup"><span data-stu-id="39339-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="39339-106">我們將討論：</span><span class="sxs-lookup"><span data-stu-id="39339-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39339-107">從 GitHub 複製應用程式來源</span><span class="sxs-lookup"><span data-stu-id="39339-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="39339-108">從應用程式來源建立容器映像</span><span class="sxs-lookup"><span data-stu-id="39339-108">Creating container images from application source</span></span>
> * <span data-ttu-id="39339-109">在本機 Docker 環境中測試映像</span><span class="sxs-lookup"><span data-stu-id="39339-109">Testing the images in a local Docker environment</span></span>

<span data-ttu-id="39339-110">在後續教學課程中，您會將映像上傳至 Azure Container Registry，然後部署至 Azure Container Instances。</span><span class="sxs-lookup"><span data-stu-id="39339-110">In subsequent tutorials, you will upload your image to an Azure Container Registry, and then deploy them to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="39339-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="39339-111">Before you begin</span></span>

<span data-ttu-id="39339-112">本教學課程假設使用者對核心 Docker 概念有基本認識，例如容器、容器映像和基本 Docker 命令。</span><span class="sxs-lookup"><span data-stu-id="39339-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="39339-113">如有需要，請參閱[開始使用 Docker]( https://docs.docker.com/get-started/)以取得容器基本概念入門。</span><span class="sxs-lookup"><span data-stu-id="39339-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="39339-114">若要完成本教學課程，您需要 Docker 開發環境。</span><span class="sxs-lookup"><span data-stu-id="39339-114">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="39339-115">Docker 提供可輕鬆在 [Mac](https://docs.docker.com/docker-for-mac/)、[Windows](https://docs.docker.com/docker-for-windows/) 或 [Linux](https://docs.docker.com/engine/installation/#supported-platforms) 系統上設定 Docker 的套件。</span><span class="sxs-lookup"><span data-stu-id="39339-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="39339-116">取得應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="39339-116">Get application code</span></span>

<span data-ttu-id="39339-117">本教學課程中的範例包含一個以 [Node.js](http://nodejs.org) 建置的簡單 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="39339-117">The sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="39339-118">應用程式提供一個 HTML 靜態網頁，外觀如下所示：</span><span class="sxs-lookup"><span data-stu-id="39339-118">The app serves a static HTML page and looks like this:</span></span>

![在瀏覽器中顯示的教學課程應用程式][aci-tutorial-app]

<span data-ttu-id="39339-120">使用 git 來下載範例：</span><span class="sxs-lookup"><span data-stu-id="39339-120">Use git to download the sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-the-container-image"></a><span data-ttu-id="39339-121">建置容器映像</span><span class="sxs-lookup"><span data-stu-id="39339-121">Build the container image</span></span>

<span data-ttu-id="39339-122">範例儲存庫中提供的 Dockerfile 會示範如何建置容器。</span><span class="sxs-lookup"><span data-stu-id="39339-122">The Dockerfile provided in the sample repo shows how the container is built.</span></span> <span data-ttu-id="39339-123">首先會使用以 [Alpine Linux](https://alpinelinux.org/) 為基礎的[官方 Node.js 映像][dockerhub-nodeimage]，這是一個很適合用於容器的小型散發。</span><span class="sxs-lookup"><span data-stu-id="39339-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited to use with containers.</span></span> <span data-ttu-id="39339-124">接著會將應用程式檔案複製到容器、使用節點封裝管理員來安裝相依性，最後就啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="39339-124">It then copies the application files into the container, installs dependencies using the Node Package Manager, and finally starts the application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="39339-125">使用 `docker build` 命令來建立容器映像，並標記成 *aci-tutorial-app*：</span><span class="sxs-lookup"><span data-stu-id="39339-125">Use the `docker build` command to create the container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="39339-126">使用 `docker images` 查看已建置的映像：</span><span class="sxs-lookup"><span data-stu-id="39339-126">Use the `docker images` to see the built image:</span></span>

```bash
docker images
```

<span data-ttu-id="39339-127">輸出：</span><span class="sxs-lookup"><span data-stu-id="39339-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-the-container-locally"></a><span data-ttu-id="39339-128">在本機執行容器</span><span class="sxs-lookup"><span data-stu-id="39339-128">Run the container locally</span></span>

<span data-ttu-id="39339-129">在嘗試將容器部署至 Container Instances 之前，請先在本機執行，以確認可以運作。</span><span class="sxs-lookup"><span data-stu-id="39339-129">Before you try deploying the container to Azure Container Instances, run it locally to confirm that it works.</span></span> <span data-ttu-id="39339-130">`-d` 參數可讓容器在背景中執行，而 `-p` 可讓您將電腦上的任意連接埠對應至容器中的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="39339-130">The `-d` switch lets the container run in the background, while `-p` allows you to map an arbitrary port on your compute to port 80 in the container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="39339-131">開啟瀏覽器來移至 http://localhost:8080/，以確認容器正在執行。</span><span class="sxs-lookup"><span data-stu-id="39339-131">Open the browser to http://localhost:8080 to confirm that the container is running.</span></span>

![在本機瀏覽器中執行應用程式][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="39339-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39339-133">Next steps</span></span>

<span data-ttu-id="39339-134">在本教學課程中，您已建立可部署至 Azure Container Instances 的容器映像。</span><span class="sxs-lookup"><span data-stu-id="39339-134">In this tutorial, you created a container image that can be deployed to Azure Container Instances.</span></span> <span data-ttu-id="39339-135">已完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="39339-135">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39339-136">從 GitHub 複製應用程式來源</span><span class="sxs-lookup"><span data-stu-id="39339-136">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="39339-137">從應用程式來源建立容器映像</span><span class="sxs-lookup"><span data-stu-id="39339-137">Creating container images from application source</span></span>
> * <span data-ttu-id="39339-138">在本機測試容器</span><span class="sxs-lookup"><span data-stu-id="39339-138">Testing the container locally</span></span>

<span data-ttu-id="39339-139">前往下一個教學課程，了解如何在 Azure Container Registry 中儲存容器映像。</span><span class="sxs-lookup"><span data-stu-id="39339-139">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="39339-140">將映像推送至 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="39339-140">Push images to Azure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png