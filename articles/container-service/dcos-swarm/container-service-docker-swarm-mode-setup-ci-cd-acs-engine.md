---
title: "aaaCI/CD 與 Azure 容器服務引擎廣域模式 |Microsoft 文件"
description: "Docker Swarm 模式、 Azure 容器登錄中，而且 Visual Studio Team Services toodeliver 持續多容器.NET Core 應用程式搭配使用 Azure 容器服務引擎"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, 容器, 微服務, Swarm, Azure, Visual Studio Team Services, DevOps, ACS 引擎"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="20e8e-104">完整的 CI/CD 管線 toodeploy 多容器上的應用程式與 ACS 引擎使用 Visual Studio Team Services 的 Docker Swarm 模式 Azure 容器服務</span><span class="sxs-lookup"><span data-stu-id="20e8e-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="20e8e-105">*這篇文章根據[完整的 CI CD 管線 toodeploy 多容器上的應用程式與使用 Visual Studio Team Services 的 Docker Swarm Azure 容器服務](container-service-docker-swarm-setup-ci-cd.md)文件*</span><span class="sxs-lookup"><span data-stu-id="20e8e-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="20e8e-106">Screen 鍵，其中一個 hello 最大的挑戰時開發 hello 雲端的現代應用程式可以 toodeliver 這些應用程式持續。</span><span class="sxs-lookup"><span data-stu-id="20e8e-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="20e8e-107">在本文中，您會學習如何 tooimplement 完整連續整合和部署 (CI/CD) 管線使用：</span><span class="sxs-lookup"><span data-stu-id="20e8e-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="20e8e-108">使用 Docker Swarm 模式的 Azure Container Service 引擎</span><span class="sxs-lookup"><span data-stu-id="20e8e-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="20e8e-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="20e8e-109">Azure Container Registry</span></span>
* <span data-ttu-id="20e8e-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="20e8e-110">Visual Studio Team Services</span></span>

<span data-ttu-id="20e8e-111">本文是以一個使用 ASP.NET Core 開發的簡單應用程式 (可在 [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux) 上取得) 為依據。</span><span class="sxs-lookup"><span data-stu-id="20e8e-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="20e8e-112">hello 應用程式由四個不同的服務所組成： 三個 web 應用程式開發介面和一個 web 前端：</span><span class="sxs-lookup"><span data-stu-id="20e8e-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop 範例應用程式](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="20e8e-114">hello 目標是 toodeliver 持續在 Docker Swarm 模式叢集中，使用 Visual Studio Team Services 的這個應用程式。</span><span class="sxs-lookup"><span data-stu-id="20e8e-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="20e8e-115">hello 下列圖這個連續的傳送管線的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="20e8e-115">hello following figure details this continuous delivery pipeline:</span></span>

![MyShop 範例應用程式](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="20e8e-117">以下是 hello 步驟的簡短說明：</span><span class="sxs-lookup"><span data-stu-id="20e8e-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="20e8e-118">程式碼變更都會認可的 toohello 原始程式碼儲存機制 （此處 GitHub）</span><span class="sxs-lookup"><span data-stu-id="20e8e-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="20e8e-119">GitHub 觸發 Visual Studio Team Services 中的組建</span><span class="sxs-lookup"><span data-stu-id="20e8e-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="20e8e-120">Visual Studio Team Services 取得 hello 的 hello 來源的最新版本，並建置撰寫 hello 應用程式的所有 hello 映像</span><span class="sxs-lookup"><span data-stu-id="20e8e-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="20e8e-121">Visual Studio Team Services 推播通知使用 hello Azure 容器登錄服務所建立的每個映像 tooa Docker 登錄</span><span class="sxs-lookup"><span data-stu-id="20e8e-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="20e8e-122">Visual Studio Team Services 觸發新版本</span><span class="sxs-lookup"><span data-stu-id="20e8e-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="20e8e-123">hello 版本執行 hello Azure 容器服務叢集主機節點上使用 SSH 一些命令</span><span class="sxs-lookup"><span data-stu-id="20e8e-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="20e8e-124">Hello 叢集上的 docker Swarm 模式會提取 hello hello 映像的最新版本</span><span class="sxs-lookup"><span data-stu-id="20e8e-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="20e8e-125">hello hello 應用程式被部署新版使用 Docker 堆疊</span><span class="sxs-lookup"><span data-stu-id="20e8e-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="20e8e-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="20e8e-126">Prerequisites</span></span>

<span data-ttu-id="20e8e-127">開始之前本教學課程，您需要 toocomplete hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="20e8e-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="20e8e-128">使用 ACS 引擎在 Azure Container Service 中建立 Swarm 模式叢集</span><span class="sxs-lookup"><span data-stu-id="20e8e-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="20e8e-129">連接與 Azure 容器服務中的 hello 群集叢集</span><span class="sxs-lookup"><span data-stu-id="20e8e-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="20e8e-130">建立 Azure 容器登錄</span><span class="sxs-lookup"><span data-stu-id="20e8e-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="20e8e-131">建立 Visual Studio Team Services 帳戶以及 Team 專案 (英文)</span><span class="sxs-lookup"><span data-stu-id="20e8e-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="20e8e-132">分岔 hello GitHub 儲存機制 tooyour GitHub 帳戶</span><span class="sxs-lookup"><span data-stu-id="20e8e-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="20e8e-133">在 Azure 容器服務中的 hello Docker Swarm orchestrator 會使用舊版獨立群集。</span><span class="sxs-lookup"><span data-stu-id="20e8e-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="20e8e-134">目前，hello 整合[群集模式](https://docs.docker.com/engine/swarm/)（Docker 1.12 （含） 以上） 不是在 Azure 容器服務中的支援的 orchestrator。</span><span class="sxs-lookup"><span data-stu-id="20e8e-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="20e8e-135">基於這個理由，我們使用[ACS 引擎](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md)，社群貢獻[快速入門範本](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/)，或在 hello Docker 方案[Azure Marketplace](https://azuremarketplace.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="20e8e-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="20e8e-136">步驟 1：設定 Visual Studio Team Services 帳戶</span><span class="sxs-lookup"><span data-stu-id="20e8e-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="20e8e-137">在本節中，您會設定您的 Visual Studio Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="20e8e-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="20e8e-138">tooconfigure VSTS 服務端點，在 Visual Studio Team Services 專案中，按一下 hello**設定**hello 工具列上，然後選取圖示**服務**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![開啟服務端點](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="20e8e-140">連接 Visual Studio Team Services 與 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="20e8e-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="20e8e-141">設定 VSTS 專案與 Azure 帳戶之間的連線。</span><span class="sxs-lookup"><span data-stu-id="20e8e-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="20e8e-142">Hello 左側，按一下 **新的服務端點** > **Azure Resource Manager**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="20e8e-143">tooauthorize VSTS toowork 與 Azure 帳戶，選取您**訂用帳戶**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services - 授權 Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="20e8e-145">將 Visual Studio Team Services 與 GitHub 連線</span><span class="sxs-lookup"><span data-stu-id="20e8e-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="20e8e-146">設定您的 VSTS 專案與 GitHub 帳戶之間的連線。</span><span class="sxs-lookup"><span data-stu-id="20e8e-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="20e8e-147">Hello 左側，按一下 **新的服務端點** > **GitHub**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="20e8e-148">按一下與您的 GitHub 帳戶 tooauthorize VSTS toowork**授權**遵循 hello hello 開啟的視窗中的程序。</span><span class="sxs-lookup"><span data-stu-id="20e8e-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - 授權 GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="20e8e-150">VSTS tooyour Azure 容器服務叢集連線</span><span class="sxs-lookup"><span data-stu-id="20e8e-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="20e8e-151">hello hello CI/CD 管線之前的最後一個步驟是 tooconfigure 外部連接 tooyour Docker Swarm Azure 中的叢集。</span><span class="sxs-lookup"><span data-stu-id="20e8e-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="20e8e-152">Hello Docker Swarm 叢集中，將端點的型別加入**SSH**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="20e8e-153">然後輸入 hello SSH 連接資訊的群集叢集 （主要節點）。</span><span class="sxs-lookup"><span data-stu-id="20e8e-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="20e8e-155">所有的 hello 組態是立即完成。</span><span class="sxs-lookup"><span data-stu-id="20e8e-155">All hello configuration is done now.</span></span> <span data-ttu-id="20e8e-156">在 hello 下一個步驟中，您可以建立組建和部署 hello 應用程式 toohello Docker Swarm 叢集 hello CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="20e8e-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="20e8e-157">步驟 2： 建立 hello 組建定義</span><span class="sxs-lookup"><span data-stu-id="20e8e-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="20e8e-158">在此步驟中，設定 VSTS 專案的組建定義和定義 hello 組建工作流程的容器映像</span><span class="sxs-lookup"><span data-stu-id="20e8e-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="20e8e-159">初始定義設定</span><span class="sxs-lookup"><span data-stu-id="20e8e-159">Initial definition setup</span></span>

1. <span data-ttu-id="20e8e-160">toocreate 組建定義中，連接 Visual Studio Team Services 專案，然後按一下的 tooyour**建置和發行**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="20e8e-161">在 hello**組建定義**區段中，按一下**+ 新增**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services - 新增組建定義](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="20e8e-163">選取 hello**清空處理序**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-163">Select hello **Empty process**.</span></span>

    ![Visual Studio Team Services - 新增空白的組建定義](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="20e8e-165">然後，按一下 hello**變數**索引標籤，然後建立兩個新的變數： **RegistryURL**和**AgentURL**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="20e8e-166">貼上您登錄與叢集代理程式的 DNS hello 值。</span><span class="sxs-lookup"><span data-stu-id="20e8e-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - 組建變數設定](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="20e8e-168">在 [hello**組建定義**頁面上，開啟 hello**觸發程序**索引標籤，然後設定與您建立在 hello prerequisites] 中的 hello MyShop 專案 hello 分岔 hello 組建 toouse 連續整合。</span><span class="sxs-lookup"><span data-stu-id="20e8e-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="20e8e-169">接著，選取 [批次變更]。</span><span class="sxs-lookup"><span data-stu-id="20e8e-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="20e8e-170">請確定您選取*docker linux*為 hello**分支規格**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services - 組建存放庫組態](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="20e8e-172">最後，按一下 hello**選項**索引標籤，設定 hello 預設代理程式佇列太**裝載的 Linux 預覽**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services - 主機代理程式設定](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="20e8e-174">定義 hello 組建工作流程</span><span class="sxs-lookup"><span data-stu-id="20e8e-174">Define hello build workflow</span></span>
<span data-ttu-id="20e8e-175">hello 接下來的步驟定義 hello 組建工作流程。</span><span class="sxs-lookup"><span data-stu-id="20e8e-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="20e8e-176">首先，您需要 tooconfigure hello 來源 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="20e8e-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="20e8e-177">toodo 它，選取**GitHub**和您**儲存機制**和**分支**(docker linux)。</span><span class="sxs-lookup"><span data-stu-id="20e8e-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services - 設定程式碼來源](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="20e8e-179">有五個容器映像 toobuild hello *MyShop*應用程式。</span><span class="sxs-lookup"><span data-stu-id="20e8e-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="20e8e-180">每個映像的建立使用 Dockerfile 位於 hello 專案資料夾中的 hello:</span><span class="sxs-lookup"><span data-stu-id="20e8e-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="20e8e-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="20e8e-181">ProductsApi</span></span>
* <span data-ttu-id="20e8e-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="20e8e-182">Proxy</span></span>
* <span data-ttu-id="20e8e-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="20e8e-183">RatingsApi</span></span>
* <span data-ttu-id="20e8e-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="20e8e-184">RecommandationsApi</span></span>
* <span data-ttu-id="20e8e-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="20e8e-185">ShopFront</span></span>

<span data-ttu-id="20e8e-186">您需要每個映像的兩個 Docker 步驟、 一個 toobuild hello 影像和 hello Azure 容器登錄中的一個 toopush hello 映像。</span><span class="sxs-lookup"><span data-stu-id="20e8e-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="20e8e-187">按一下 tooadd hello 組建工作流程中的步驟**+ 加入建置步驟**選取**Docker**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - 新增建置步驟](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="20e8e-189">每個映像，設定一個步驟，來使用 hello`docker build`命令。</span><span class="sxs-lookup"><span data-stu-id="20e8e-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker 建置](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="20e8e-191">Hello 建置作業中，選取您的 Azure 容器登錄 hello**建置的映像**動作和 hello 定義每個映像的 Dockerfile。</span><span class="sxs-lookup"><span data-stu-id="20e8e-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="20e8e-192">設定 hello**工作目錄**hello Dockerfile 根目錄中，定義 hello**映像名稱**，然後選取**包含最新的標籤**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="20e8e-193">hello 映像名稱具有 toobe 格式如下： ```$(RegistryURL)/[NAME]:$(Build.BuildId)```。</span><span class="sxs-lookup"><span data-stu-id="20e8e-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="20e8e-194">取代**[NAME]** hello 映像名稱：</span><span class="sxs-lookup"><span data-stu-id="20e8e-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="20e8e-195">每個映像，設定 第二個步驟使用 hello`docker push`命令。</span><span class="sxs-lookup"><span data-stu-id="20e8e-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker 推送](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="20e8e-197">Hello 推入作業中，選取您的 Azure 容器登錄 hello**推入映像**動作中，輸入 hello**映像名稱**hello 上一個步驟並選取內建**包含最新的標籤**.</span><span class="sxs-lookup"><span data-stu-id="20e8e-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="20e8e-198">之後您設定 hello 組建和 push hello 五個映像的每個步驟，加入三個步驟詳細 hello 組建工作流程。</span><span class="sxs-lookup"><span data-stu-id="20e8e-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services - 新增命令列工作](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="20e8e-200">使用 bash 指令碼 tooreplace hello 的命令列工作*RegistryURL* hello RegistryURL 變數 hello docker compose.yml 檔案中的項目。</span><span class="sxs-lookup"><span data-stu-id="20e8e-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - 使用登錄 URL 更新 Compose 檔案](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="20e8e-202">使用 bash 指令碼 tooreplace hello 的命令列工作*AgentURL* hello AgentURL 變數 hello docker compose.yml 檔案中的項目。</span><span class="sxs-lookup"><span data-stu-id="20e8e-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="20e8e-203">卸除 hello 工作更新組建成品撰寫檔案，所以用於 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="20e8e-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="20e8e-204">請參閱下列詳細資料螢幕的 hello。</span><span class="sxs-lookup"><span data-stu-id="20e8e-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services - 發佈構件](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - 發佈 Compose 檔案](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="20e8e-207">按一下**儲存，並佇列**tootest 組建定義。</span><span class="sxs-lookup"><span data-stu-id="20e8e-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services - 儲存並排入佇列](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - 新增佇列](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="20e8e-210">如果 hello**建置**是否正確，您有 toosee 這個畫面：</span><span class="sxs-lookup"><span data-stu-id="20e8e-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services - 建置成功](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="20e8e-212">步驟 3： 建立 hello 發行定義</span><span class="sxs-lookup"><span data-stu-id="20e8e-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="20e8e-213">Visual Studio Team Services 可讓您太[的環境中管理發行](https://www.visualstudio.com/team-services/release-management/)。</span><span class="sxs-lookup"><span data-stu-id="20e8e-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="20e8e-214">您可以啟用連續部署 toomake 確定您的應用程式部署在不同環境 （例如開發、 測試、 生產階段前及生產），以平滑的方式。</span><span class="sxs-lookup"><span data-stu-id="20e8e-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="20e8e-215">您可以建立代表 Azure Container Service Docker Swarm 模式叢集的環境。</span><span class="sxs-lookup"><span data-stu-id="20e8e-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services 的版本 tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="20e8e-217">初始發行設定</span><span class="sxs-lookup"><span data-stu-id="20e8e-217">Initial release setup</span></span>

1. <span data-ttu-id="20e8e-218">toocreate 發行定義中，按一下**版本** > **+ 版本**</span><span class="sxs-lookup"><span data-stu-id="20e8e-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="20e8e-219">tooconfigure hello 成品來源，按一下**成品** > **連結成品來源**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="20e8e-220">在這裡，連結此新發行定義 toohello 組建在 hello 上一個步驟中所定義。</span><span class="sxs-lookup"><span data-stu-id="20e8e-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="20e8e-221">在這之後，hello docker compose.yml 檔案位於 hello 發行程序。</span><span class="sxs-lookup"><span data-stu-id="20e8e-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - 發行構件](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="20e8e-223">tooconfigure hello 釋放觸發程序，按一下 **觸發程序**選取**連續部署**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="20e8e-224">Hello hello 組觸發程序相同的成品來源。</span><span class="sxs-lookup"><span data-stu-id="20e8e-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="20e8e-225">此設定可確保 hello 組建已成功完成時，會啟動新的版本。</span><span class="sxs-lookup"><span data-stu-id="20e8e-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services - 發行觸發程序](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="20e8e-227">tooconfigure hello 發行變數，按一下**變數**選取**+ 變數**toocreate 三個新的變數與 hello hello 登錄資訊： **docker.username**，**docker.password**，和**docker.registry**。</span><span class="sxs-lookup"><span data-stu-id="20e8e-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="20e8e-228">貼上您登錄與叢集代理程式的 DNS hello 值。</span><span class="sxs-lookup"><span data-stu-id="20e8e-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - 組建存放庫組態](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="20e8e-230">顯示 hello 上一個畫面中，按一下 hello**鎖定**docker.password 中的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="20e8e-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="20e8e-231">這項設定是很重要的 toorestrict hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="20e8e-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="20e8e-232">定義 hello 發行工作流程</span><span class="sxs-lookup"><span data-stu-id="20e8e-232">Define hello release workflow</span></span>

<span data-ttu-id="20e8e-233">hello 發行工作流程是由您加入的兩個工作所組成。</span><span class="sxs-lookup"><span data-stu-id="20e8e-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="20e8e-234">設定工作 toosecurely 複製 hello 撰寫檔案 tooa*部署*hello Docker Swarm 主要節點上，使用您先前設定的 hello SSH 連線的資料夾。</span><span class="sxs-lookup"><span data-stu-id="20e8e-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="20e8e-235">請參閱下列詳細資料螢幕的 hello。</span><span class="sxs-lookup"><span data-stu-id="20e8e-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="20e8e-236">來源資料夾：```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="20e8e-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - 發行 SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="20e8e-238">設定第二個工作 tooexecute bash 指令 toorun`docker`和`docker stack deploy`hello 主要節點上的命令。</span><span class="sxs-lookup"><span data-stu-id="20e8e-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="20e8e-239">請參閱下列詳細資料螢幕的 hello。</span><span class="sxs-lookup"><span data-stu-id="20e8e-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - 發行 Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="20e8e-241">hello hello 主機上執行的命令會使用 hello Docker CLI 和 hello Docker Compose CLI toodo hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="20e8e-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="20e8e-242">登入 toohello Azure 容器登錄中 (它會使用三個 hello 中所定義的組建變數**變數** 索引標籤)</span><span class="sxs-lookup"><span data-stu-id="20e8e-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="20e8e-243">定義 hello **DOCKER_HOST**變數 toowork 與 hello 群集端點 (: 2375年)</span><span class="sxs-lookup"><span data-stu-id="20e8e-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="20e8e-244">瀏覽 toohello*部署*hello 前面安全複製工作所建立，並包含 hello docker compose.yml 檔案的資料夾</span><span class="sxs-lookup"><span data-stu-id="20e8e-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="20e8e-245">執行`docker stack deploy`提取 hello 新映像，並建立 hello 容器的命令。</span><span class="sxs-lookup"><span data-stu-id="20e8e-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="20e8e-246">如下所示 hello 上一個畫面，讓 hello**失敗 STDERR 上**未核取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="20e8e-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="20e8e-247">此設定可讓我們 toocomplete hello 發行程序，因為太`docker-compose`會列印數診斷訊息，例如容器會停止中或正在刪除，hello 標準錯誤輸出上。</span><span class="sxs-lookup"><span data-stu-id="20e8e-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="20e8e-248">如果您檢查 hello 核取方塊時，Visual Studio Team Services 報告錯誤時發生 hello 版本中，即使一切順利。</span><span class="sxs-lookup"><span data-stu-id="20e8e-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="20e8e-249">儲存這個新的發行定義。</span><span class="sxs-lookup"><span data-stu-id="20e8e-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="20e8e-250">步驟 4： 測試 hello CI/CD 管線</span><span class="sxs-lookup"><span data-stu-id="20e8e-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="20e8e-251">既然您以 hello 組態完成之後，它是這個新的時間 tootest CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="20e8e-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="20e8e-252">hello tooupdate hello 來源的程式碼和 commit hello 是最簡單方式 tootest 變更為您的 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="20e8e-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="20e8e-253">幾秒後就是您推送 hello 程式碼中，您會看到新的組建，在 Visual Studio Team Services 中執行。</span><span class="sxs-lookup"><span data-stu-id="20e8e-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="20e8e-254">順利完成後，會觸發新的版本，並部署 hello hello hello Azure 容器服務的叢集上的應用程式的新版本。</span><span class="sxs-lookup"><span data-stu-id="20e8e-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20e8e-255">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20e8e-255">Next steps</span></span>

* <span data-ttu-id="20e8e-256">如需使用 Visual Studio Team Services 的 CI/CD 的詳細資訊，請參閱 hello [VSTS 建置概觀](https://www.visualstudio.com/docs/build/overview)。</span><span class="sxs-lookup"><span data-stu-id="20e8e-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="20e8e-257">如需 ACS 引擎的詳細資訊，請參閱 hello [ACS 引擎 GitHub 儲存機制](https://github.com/Azure/acs-engine)。</span><span class="sxs-lookup"><span data-stu-id="20e8e-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="20e8e-258">如需有關 Docker Swarm 模式的詳細資訊，請參閱 hello [Docker Swarm 模式概觀](https://docs.docker.com/engine/swarm/)。</span><span class="sxs-lookup"><span data-stu-id="20e8e-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
