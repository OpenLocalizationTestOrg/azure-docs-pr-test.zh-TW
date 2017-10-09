---
title: "aaaCI/CD 群集與 Azure 容器服務 |Microsoft 文件"
description: "Docker Swarm、 Azure 容器登錄中，而且 Visual Studio Team Services toodeliver 持續多容器.NET Core 應用程式搭配使用 Azure 容器服務"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, Containers, Micro-services, Swarm, Azure, Visual Studio Team Services, DevOps, 容器, 微型服務"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="38fa3-104">完整的 CI/CD 管線 toodeploy 多容器上的應用程式與使用 Visual Studio Team Services 的 Docker Swarm Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="38fa3-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="38fa3-105">其中一個 hello 最大的挑戰時開發 hello 雲端的現代應用程式可以 toodeliver 這些應用程式持續。</span><span class="sxs-lookup"><span data-stu-id="38fa3-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="38fa3-106">在本文中，您會了解 tooimplement 完整連續整合和部署 (CI/CD) 管線 Docker Swarm、 與 Azure 容器登錄中，Visual Studio Team Services 中使用 Azure 容器服務的建置，以及發行管理。</span><span class="sxs-lookup"><span data-stu-id="38fa3-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="38fa3-107">本文是以一個使用 ASP.NET Core 開發的簡單應用程式 (可在 [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs) 上取得) 為依據。</span><span class="sxs-lookup"><span data-stu-id="38fa3-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="38fa3-108">hello 應用程式由四個不同的服務所組成： 三個 web 應用程式開發介面和一個 web 前端：</span><span class="sxs-lookup"><span data-stu-id="38fa3-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop 範例應用程式](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="38fa3-110">hello 目標是 toodeliver 持續在 Docker Swarm 叢集中，使用 Visual Studio Team Services 的這個應用程式。</span><span class="sxs-lookup"><span data-stu-id="38fa3-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="38fa3-111">hello 下列圖這個連續的傳送管線的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="38fa3-111">hello following figure details this continuous delivery pipeline:</span></span>

![MyShop 範例應用程式](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="38fa3-113">以下是 hello 步驟的簡短說明：</span><span class="sxs-lookup"><span data-stu-id="38fa3-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="38fa3-114">程式碼變更都會認可的 toohello 原始程式碼儲存機制 （此處 GitHub）</span><span class="sxs-lookup"><span data-stu-id="38fa3-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="38fa3-115">GitHub 觸發 Visual Studio Team Services 中的組建</span><span class="sxs-lookup"><span data-stu-id="38fa3-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="38fa3-116">Visual Studio Team Services 取得 hello 的 hello 來源的最新版本，並建置撰寫 hello 應用程式的所有 hello 映像</span><span class="sxs-lookup"><span data-stu-id="38fa3-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="38fa3-117">Visual Studio Team Services 推播通知使用 hello Azure 容器登錄服務所建立的每個映像 tooa Docker 登錄</span><span class="sxs-lookup"><span data-stu-id="38fa3-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="38fa3-118">Visual Studio Team Services 觸發新版本</span><span class="sxs-lookup"><span data-stu-id="38fa3-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="38fa3-119">hello 版本執行 hello Azure 容器服務叢集主機節點上使用 SSH 一些命令</span><span class="sxs-lookup"><span data-stu-id="38fa3-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="38fa3-120">Hello 叢集提取 hello 最新版本的 hello 映像上的 docker 群集</span><span class="sxs-lookup"><span data-stu-id="38fa3-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="38fa3-121">使用 Docker Compose 部署 hello 新版 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="38fa3-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="38fa3-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="38fa3-122">Prerequisites</span></span>

<span data-ttu-id="38fa3-123">開始之前本教學課程，您需要 toocomplete hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="38fa3-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="38fa3-124">在 Azure 容器服務中建立 Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="38fa3-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="38fa3-125">連接與 Azure 容器服務中的 hello 群集叢集</span><span class="sxs-lookup"><span data-stu-id="38fa3-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="38fa3-126">建立 Azure 容器登錄</span><span class="sxs-lookup"><span data-stu-id="38fa3-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="38fa3-127">建立 Visual Studio Team Services 帳戶以及 Team 專案 (英文)</span><span class="sxs-lookup"><span data-stu-id="38fa3-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="38fa3-128">分岔 hello GitHub 儲存機制 tooyour GitHub 帳戶</span><span class="sxs-lookup"><span data-stu-id="38fa3-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="38fa3-129">您也需要已經安裝 Docker 的 Ubuntu (14.04 or 16.04) 機器。</span><span class="sxs-lookup"><span data-stu-id="38fa3-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="38fa3-130">使用這部電腦是由 Visual Studio Team Services 在 hello 期間建立及發佈程序。</span><span class="sxs-lookup"><span data-stu-id="38fa3-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="38fa3-131">其中一種方式 toocreate 這台電腦是 toouse hello 映像可在 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/)。</span><span class="sxs-lookup"><span data-stu-id="38fa3-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="38fa3-132">步驟 1：設定 Visual Studio Team Services 帳戶</span><span class="sxs-lookup"><span data-stu-id="38fa3-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="38fa3-133">在本節中，您會設定您的 Visual Studio Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="38fa3-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="38fa3-134">設定 Visual Studio Team Services Linux 組件代理程式</span><span class="sxs-lookup"><span data-stu-id="38fa3-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="38fa3-135">toocreate Docker 映像並推送建置到 Visual Studio Team Services 從 Azure 容器登錄這些映像，您會需要 tooregister Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="38fa3-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="38fa3-136">安裝選項如下：</span><span class="sxs-lookup"><span data-stu-id="38fa3-136">You have these installation options:</span></span>

* [<span data-ttu-id="38fa3-137">在 Linux 上部署代理程式 (英文)</span><span class="sxs-lookup"><span data-stu-id="38fa3-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="38fa3-138">使用 Docker toorun hello VSTS 代理程式</span><span class="sxs-lookup"><span data-stu-id="38fa3-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="38fa3-139">安裝 hello Docker 整合 VSTS 擴充功能</span><span class="sxs-lookup"><span data-stu-id="38fa3-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="38fa3-140">Microsoft 提供 VSTS 延伸 toowork 使用 Docker 在組建中的，並釋放處理程序。</span><span class="sxs-lookup"><span data-stu-id="38fa3-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="38fa3-141">這個延伸可用於 hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker)。</span><span class="sxs-lookup"><span data-stu-id="38fa3-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="38fa3-142">按一下**安裝**tooadd 此延伸模組 tooyour VSTS 帳戶：</span><span class="sxs-lookup"><span data-stu-id="38fa3-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![安裝 hello Docker 整合](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="38fa3-144">系統會要求您使用您的認證 tooconnect tooyour VSTS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="38fa3-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="38fa3-145">將 Visual Studio Team Services 與 GitHub 連線</span><span class="sxs-lookup"><span data-stu-id="38fa3-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="38fa3-146">設定您的 VSTS 專案與 GitHub 帳戶之間的連線。</span><span class="sxs-lookup"><span data-stu-id="38fa3-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="38fa3-147">在 Visual Studio Team Services 專案中，按一下 hello**設定**hello 工具列上，然後選取圖示**服務**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - 外部連線](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="38fa3-149">Hello 左側，按一下 **新的服務端點** > **GitHub**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="38fa3-151">按一下與您的 GitHub 帳戶 tooauthorize VSTS toowork**授權**遵循 hello hello 開啟的視窗中的程序。</span><span class="sxs-lookup"><span data-stu-id="38fa3-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - 授權 GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="38fa3-153">連接 Azure 容器登錄中 VSTS tooyour 和 Azure 容器服務的叢集</span><span class="sxs-lookup"><span data-stu-id="38fa3-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="38fa3-154">hello hello CI/CD 管線之前的最後一個步驟是 tooconfigure 外部連接 tooyour 容器登錄中和在 Azure 中您 Docker Swarm 的叢集。</span><span class="sxs-lookup"><span data-stu-id="38fa3-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="38fa3-155">在 hello**服務**設定您的 Visual Studio Team Services 專案，加入服務端點的型別**Docker 登錄**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="38fa3-156">在 hello 快顯視窗開啟，輸入 hello URL 和 Azure 容器登錄 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="38fa3-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Docker 登錄](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="38fa3-158">Hello Docker Swarm 叢集中，將端點的型別加入**SSH**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="38fa3-159">然後輸入 hello SSH 連接資訊的群集叢集。</span><span class="sxs-lookup"><span data-stu-id="38fa3-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="38fa3-161">所有的 hello 組態是立即完成。</span><span class="sxs-lookup"><span data-stu-id="38fa3-161">All hello configuration is done now.</span></span> <span data-ttu-id="38fa3-162">在 hello 下一個步驟中，您可以建立組建和部署 hello 應用程式 toohello Docker Swarm 叢集 hello CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="38fa3-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="38fa3-163">步驟 2： 建立 hello 組建定義</span><span class="sxs-lookup"><span data-stu-id="38fa3-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="38fa3-164">在此步驟中，您需要設定組建 definitionfor VSTS 專案並 hello 組建工作流程定義您的容器映像</span><span class="sxs-lookup"><span data-stu-id="38fa3-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="38fa3-165">初始定義設定</span><span class="sxs-lookup"><span data-stu-id="38fa3-165">Initial definition setup</span></span>

1. <span data-ttu-id="38fa3-166">toocreate 組建定義中，連接 Visual Studio Team Services 專案，然後按一下的 tooyour**建置和發行**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="38fa3-167">在 hello**組建定義**區段中，按一下**+ 新增**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="38fa3-168">選取 hello**空**範本。</span><span class="sxs-lookup"><span data-stu-id="38fa3-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services - 新增組建定義](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="38fa3-170">設定新組建的 hello 與 GitHub 儲存機制來源，核取**連續整合**，和您用來註冊您的 Linux 代理程式選取 hello 代理程式佇列。</span><span class="sxs-lookup"><span data-stu-id="38fa3-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="38fa3-171">按一下**建立**toocreate hello 組建定義。</span><span class="sxs-lookup"><span data-stu-id="38fa3-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services - 建立組建定義](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="38fa3-173">在 hello**組建定義**頁面上，第一次開啟 hello**儲存機制**索引標籤，設定 hello 組建 toouse hello 分岔 hello MyShop 專案在 hello 必要條件中所建立。</span><span class="sxs-lookup"><span data-stu-id="38fa3-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="38fa3-174">請確定您選取*acs 文件*為 hello**預設分支**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services - 組建存放庫組態](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="38fa3-176">在 hello**觸發程序**索引標籤上，設定 hello 組建 toobe 每次認可之後觸發。</span><span class="sxs-lookup"><span data-stu-id="38fa3-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="38fa3-177">選取 [持續整合] 和 [批次變更]。</span><span class="sxs-lookup"><span data-stu-id="38fa3-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - 組建觸發組態](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="38fa3-179">定義 hello 組建工作流程</span><span class="sxs-lookup"><span data-stu-id="38fa3-179">Define hello build workflow</span></span>
<span data-ttu-id="38fa3-180">hello 接下來的步驟定義 hello 組建工作流程。</span><span class="sxs-lookup"><span data-stu-id="38fa3-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="38fa3-181">有五個容器映像 toobuild hello *MyShop*應用程式。</span><span class="sxs-lookup"><span data-stu-id="38fa3-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="38fa3-182">每個映像的建立使用 Dockerfile 位於 hello 專案資料夾中的 hello:</span><span class="sxs-lookup"><span data-stu-id="38fa3-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="38fa3-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="38fa3-183">ProductsApi</span></span>
* <span data-ttu-id="38fa3-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="38fa3-184">Proxy</span></span>
* <span data-ttu-id="38fa3-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="38fa3-185">RatingsApi</span></span>
* <span data-ttu-id="38fa3-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="38fa3-186">RecommandationsApi</span></span>
* <span data-ttu-id="38fa3-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="38fa3-187">ShopFront</span></span>

<span data-ttu-id="38fa3-188">您需要每個映像 tooadd 兩個 Docker 步驟、 一個 toobuild hello 影像和 hello Azure 容器登錄中的一個 toopush hello 映像。</span><span class="sxs-lookup"><span data-stu-id="38fa3-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="38fa3-189">按一下 tooadd hello 組建工作流程中的步驟**+ 加入建置步驟**選取**Docker**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - 新增建置步驟](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="38fa3-191">每個映像，設定一個步驟，來使用 hello`docker build`命令。</span><span class="sxs-lookup"><span data-stu-id="38fa3-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker 建置](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="38fa3-193">Hello 建置作業中，選取您的 Azure 容器登錄 hello**建置的映像**動作和 hello 定義每個映像的 Dockerfile。</span><span class="sxs-lookup"><span data-stu-id="38fa3-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="38fa3-194">設定 hello**建置內容**hello Dockerfile 為根目錄，並定義 hello**映像名稱**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="38fa3-195">如下所示 hello 前面螢幕，hello 映像名稱開頭 hello Azure 容器登錄的 URI。</span><span class="sxs-lookup"><span data-stu-id="38fa3-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="38fa3-196">（您也可以使用組建變數 tooparameterize hello 標記 hello 映像，例如在此範例中的 hello 組建識別項）。</span><span class="sxs-lookup"><span data-stu-id="38fa3-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="38fa3-197">每個映像，設定 第二個步驟使用 hello`docker push`命令。</span><span class="sxs-lookup"><span data-stu-id="38fa3-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker 推送](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="38fa3-199">Hello 推入作業中，選取您的 Azure 容器登錄 hello**推入映像**動作，然後輸入 hello**映像名稱**hello 上一個步驟中內建。</span><span class="sxs-lookup"><span data-stu-id="38fa3-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="38fa3-200">之後您設定 hello 組建和 push hello 五個映像的每個步驟，加入兩個步驟，在 hello 組建工作流程。</span><span class="sxs-lookup"><span data-stu-id="38fa3-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="38fa3-201">a.</span><span class="sxs-lookup"><span data-stu-id="38fa3-201">a.</span></span> <span data-ttu-id="38fa3-202">使用 bash 指令碼 tooreplace hello 的命令列工作*BuildNumber* hello 目前 hello docker compose.yml 檔案中的項目建立的識別碼。請參閱下列詳細資料螢幕的 hello。</span><span class="sxs-lookup"><span data-stu-id="38fa3-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services - 更新 Compose 檔案](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="38fa3-204">b.</span><span class="sxs-lookup"><span data-stu-id="38fa3-204">b.</span></span> <span data-ttu-id="38fa3-205">卸除 hello 工作更新組建成品撰寫檔案，所以用於 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="38fa3-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="38fa3-206">請參閱下列詳細資料螢幕的 hello。</span><span class="sxs-lookup"><span data-stu-id="38fa3-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - 發佈 Compose 檔案](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="38fa3-208">按一下 [儲存] 並命名您的組建定義。</span><span class="sxs-lookup"><span data-stu-id="38fa3-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="38fa3-209">步驟 3： 建立 hello 發行定義</span><span class="sxs-lookup"><span data-stu-id="38fa3-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="38fa3-210">Visual Studio Team Services 可讓您太[的環境中管理發行](https://www.visualstudio.com/team-services/release-management/)。</span><span class="sxs-lookup"><span data-stu-id="38fa3-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="38fa3-211">您可以啟用連續部署 toomake 確定您的應用程式部署在不同環境 （例如開發、 測試、 生產階段前及生產），以平滑的方式。</span><span class="sxs-lookup"><span data-stu-id="38fa3-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="38fa3-212">您可以建立代表 Azure Container Service Docker Swarm 叢集的新環境。</span><span class="sxs-lookup"><span data-stu-id="38fa3-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services 的版本 tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="38fa3-214">初始發行設定</span><span class="sxs-lookup"><span data-stu-id="38fa3-214">Initial release setup</span></span>

1. <span data-ttu-id="38fa3-215">toocreate 發行定義中，按一下**版本** > **+ 版本**</span><span class="sxs-lookup"><span data-stu-id="38fa3-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="38fa3-216">tooconfigure hello 成品來源，按一下**成品** > **連結成品來源**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="38fa3-217">在這裡，連結此新發行定義 toohello 組建在 hello 上一個步驟中所定義。</span><span class="sxs-lookup"><span data-stu-id="38fa3-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="38fa3-218">如此一來，hello docker compose.yml 檔案可在 hello 發行程序。</span><span class="sxs-lookup"><span data-stu-id="38fa3-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - 發行構件](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="38fa3-220">tooconfigure hello 釋放觸發程序，按一下 **觸發程序**選取**連續部署**。</span><span class="sxs-lookup"><span data-stu-id="38fa3-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="38fa3-221">Hello hello 組觸發程序相同的成品來源。</span><span class="sxs-lookup"><span data-stu-id="38fa3-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="38fa3-222">此設定可確保新的版本會在 hello 建置成功完成時立即啟動。</span><span class="sxs-lookup"><span data-stu-id="38fa3-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services - 發行觸發程序](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="38fa3-224">定義 hello 發行工作流程</span><span class="sxs-lookup"><span data-stu-id="38fa3-224">Define hello release workflow</span></span>

<span data-ttu-id="38fa3-225">hello 發行工作流程是由您加入的兩個工作所組成。</span><span class="sxs-lookup"><span data-stu-id="38fa3-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="38fa3-226">設定工作 toosecurely 複製 hello 撰寫檔案 tooa*部署*hello Docker Swarm 主要節點上，使用您先前設定的 hello SSH 連線的資料夾。</span><span class="sxs-lookup"><span data-stu-id="38fa3-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="38fa3-227">請參閱下列詳細資料螢幕的 hello。</span><span class="sxs-lookup"><span data-stu-id="38fa3-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - 發行 SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="38fa3-229">設定第二個工作 tooexecute bash 指令 toorun`docker`和`docker-compose`hello 主要節點上的命令。</span><span class="sxs-lookup"><span data-stu-id="38fa3-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="38fa3-230">請參閱下列詳細資料螢幕的 hello。</span><span class="sxs-lookup"><span data-stu-id="38fa3-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - 發行 Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="38fa3-232">hello hello 主要使用 hello Docker CLI 和 hello Docker Compose CLI toodo hello 下列工作上執行的命令：</span><span class="sxs-lookup"><span data-stu-id="38fa3-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="38fa3-233">登入 toohello Azure 容器登錄中 (它會使用三個 hello 中所定義的組建 variab'les**變數** 索引標籤)</span><span class="sxs-lookup"><span data-stu-id="38fa3-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="38fa3-234">定義 hello **DOCKER_HOST**變數 toowork 與 hello 群集端點 (: 2375年)</span><span class="sxs-lookup"><span data-stu-id="38fa3-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="38fa3-235">瀏覽 toohello*部署*hello 前面安全複製工作所建立，並包含 hello docker compose.yml 檔案的資料夾</span><span class="sxs-lookup"><span data-stu-id="38fa3-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="38fa3-236">執行`docker-compose`提取 hello 新映像的命令停止 hello 服務、 移除 hello 服務，以及建立 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="38fa3-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="38fa3-237">Hello 前面螢幕上所示，將保留 hello**失敗 STDERR 上**未核取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="38fa3-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="38fa3-238">這是重要設定，因為`docker-compose`會列印數診斷訊息，例如容器會停止中或正在刪除，hello 標準錯誤輸出上。</span><span class="sxs-lookup"><span data-stu-id="38fa3-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="38fa3-239">如果您檢查 hello 核取方塊時，Visual Studio Team Services 報告錯誤時發生 hello 版本中，即使一切順利。</span><span class="sxs-lookup"><span data-stu-id="38fa3-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="38fa3-240">儲存這個新的發行定義。</span><span class="sxs-lookup"><span data-stu-id="38fa3-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="38fa3-241">此部署包含一些停機時間，因為我們會停止 hello 舊服務並執行新的 hello。</span><span class="sxs-lookup"><span data-stu-id="38fa3-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="38fa3-242">它是可能 tooavoid 這執行藍綠色部署。</span><span class="sxs-lookup"><span data-stu-id="38fa3-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="38fa3-243">步驟 4.</span><span class="sxs-lookup"><span data-stu-id="38fa3-243">Step 4.</span></span> <span data-ttu-id="38fa3-244">測試 hello CI/CD 管線</span><span class="sxs-lookup"><span data-stu-id="38fa3-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="38fa3-245">既然您以 hello 組態完成之後，它是這個新的時間 tootest CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="38fa3-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="38fa3-246">hello tooupdate hello 來源的程式碼和 commit hello 是最簡單方式 tootest 變更為您的 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="38fa3-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="38fa3-247">幾秒後就是您推送 hello 程式碼中，您會看到新的組建，在 Visual Studio Team Services 中執行。</span><span class="sxs-lookup"><span data-stu-id="38fa3-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="38fa3-248">順利完成後，新的版本會將觸發，因此將會部署 hello hello hello Azure 容器服務的叢集上的應用程式的新版本。</span><span class="sxs-lookup"><span data-stu-id="38fa3-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38fa3-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38fa3-249">Next Steps</span></span>

* <span data-ttu-id="38fa3-250">如需使用 Visual Studio Team Services 的 CI/CD 的詳細資訊，請參閱 hello [VSTS 建置概觀](https://www.visualstudio.com/docs/build/overview)。</span><span class="sxs-lookup"><span data-stu-id="38fa3-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
