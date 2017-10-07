---
title: "aaaCI/CD 從 Jenkins tooAzure Team Services 的 Vm |Microsoft 文件"
description: "設定持續整合 (CI) 和使用 Visual Studio Team Services (VSTS) 或 Microsoft Team Foundation Server (TFS) 中的 Release Management 從 Jenkins tooAzure Vm Node.js 應用程式的連續部署 (CD)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="046c4-103">部署您的應用程式 tooLinux Vm 使用 Jenkins 和 Team Services</span><span class="sxs-lookup"><span data-stu-id="046c4-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="046c4-104">持續整合 (CI) 與持續部署 (CD) 是讓您可以建置、發行和部署程式碼的管道。</span><span class="sxs-lookup"><span data-stu-id="046c4-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="046c4-105">Team Services 部署 tooAzure 提供一組完整、 全功能的 CI/CD 自動化工具。</span><span class="sxs-lookup"><span data-stu-id="046c4-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="046c4-106">Jenkins 是廣為使用的第三方 CI/CD 伺服器型工具，也提供 CI/CD 自動化。</span><span class="sxs-lookup"><span data-stu-id="046c4-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="046c4-107">您可以使用這兩個一起 toocustomize 如何傳遞您的雲端應用程式或服務。</span><span class="sxs-lookup"><span data-stu-id="046c4-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="046c4-108">在此教學課程中，您可以使用 Jenkins toobuild **Node.js web 應用程式**，和 Visual Studio Team Services toodeploy 它 tooa[部署群組](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/)包含 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="046c4-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="046c4-109">您將：</span><span class="sxs-lookup"><span data-stu-id="046c4-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="046c4-110">在 Jenkins 中建置應用程式</span><span class="sxs-lookup"><span data-stu-id="046c4-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="046c4-111">設定適用於 Team Services 整合的 Jenkins</span><span class="sxs-lookup"><span data-stu-id="046c4-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="046c4-112">Azure 虛擬機器建立 hello 部署群組</span><span class="sxs-lookup"><span data-stu-id="046c4-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="046c4-113">建立設定 hello Vm，然後部署 hello 應用程式的發行定義</span><span class="sxs-lookup"><span data-stu-id="046c4-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="046c4-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="046c4-114">Before you begin</span></span>

* <span data-ttu-id="046c4-115">您需要存取 tooa Jenkins 帳戶。</span><span class="sxs-lookup"><span data-stu-id="046c4-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="046c4-116">如果您尚未建立 Jenkins 伺服器，請參閱 [Jenkins 文件](https://jenkins.io/doc/)。</span><span class="sxs-lookup"><span data-stu-id="046c4-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="046c4-117">登入 tooyour Team Services 帳戶 (`https://{youraccount}.visualstudio.com`)。</span><span class="sxs-lookup"><span data-stu-id="046c4-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="046c4-118">您可以取得[免費的 Team Services 帳戶](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308)。</span><span class="sxs-lookup"><span data-stu-id="046c4-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="046c4-119">如需詳細資訊，請參閱[tooTeam 服務連接](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services)。</span><span class="sxs-lookup"><span data-stu-id="046c4-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="046c4-120">如果您的 Team Services 帳戶中沒有個人存取權杖 (PAT)，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="046c4-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="046c4-121">Jenkins 需要此資訊 tooaccess Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="046c4-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="046c4-122">讀取[如何適用於 Team Services 和 TFS 建立個人存取權杖](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)toolearn 如何 toogenerate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="046c4-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="046c4-123">取得 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="046c4-123">Get hello sample app</span></span>

<span data-ttu-id="046c4-124">您必須儲存在 Git 儲存機制的應用程式 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="046c4-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="046c4-125">在本教學課程中，我們建議您使用[從 GitHub 中取得的此範例應用程式](https://github.com/azooinmyluggage/fabrikam-node)。</span><span class="sxs-lookup"><span data-stu-id="046c4-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="046c4-126">建立此應用程式的 「 分叉 」，並記在本教學課程的後續步驟中使用的 hello 位置 (URL)。</span><span class="sxs-lookup"><span data-stu-id="046c4-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="046c4-127">請 hello 分岔**公用**toosimplify 稍後連接 tooGitHub。</span><span class="sxs-lookup"><span data-stu-id="046c4-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="046c4-128">如需詳細資訊，請參閱＜[建立存放庫的分支](https://help.github.com/articles/fork-a-repo/)＞和＜[將私密存放庫設為公用](https://help.github.com/articles/making-a-private-repository-public/)＞。</span><span class="sxs-lookup"><span data-stu-id="046c4-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="046c4-129">hello 應用程式使用建立[Yeoman](http://yeoman.io/learning/index.html); 它會使用**Express**， **bower**，和**grunt**; 而且它具有某些**npm**封裝做為相依性。</span><span class="sxs-lookup"><span data-stu-id="046c4-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="046c4-130">hello 範例應用程式包含一組[Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)，會使用的 toodynamically hello 虛擬機器部署在 Azure 上建立。</span><span class="sxs-lookup"><span data-stu-id="046c4-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="046c4-131">這些範本由工作在 hello [Team Services 發行定義](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions)。</span><span class="sxs-lookup"><span data-stu-id="046c4-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="046c4-132">hello 主要範本會建立網路安全性群組、 虛擬機器和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="046c4-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="046c4-133">並指派公用 IP 位址和開啟輸入連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="046c4-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="046c4-134">它也會加入 hello 部署群組太選取 hello 機器 tooreceive hello 部署使用的標記。</span><span class="sxs-lookup"><span data-stu-id="046c4-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="046c4-135">hello 範例也包含可設定 Nginx hello 應用程式會將部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="046c4-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="046c4-136">在每個 hello 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="046c4-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="046c4-137">具體來說，hello 指令碼安裝節點、 Nginx 及 PM2;設定 Nginx 和 PM2;接著，啟動 hello 節點應用程式。</span><span class="sxs-lookup"><span data-stu-id="046c4-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="046c4-138">設定 Jenkins 外掛程式</span><span class="sxs-lookup"><span data-stu-id="046c4-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="046c4-139">首先，您必須設定兩個 Jenkins 外掛程式，用於 **NodeJS**，以及**與 Team Services 整合**。</span><span class="sxs-lookup"><span data-stu-id="046c4-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="046c4-140">開啟您的 Jenkins 帳戶，然後選擇 [管理 Jenkins]。</span><span class="sxs-lookup"><span data-stu-id="046c4-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="046c4-141">在 hello**管理 Jenkins**頁面上，選擇**管理外掛程式**。</span><span class="sxs-lookup"><span data-stu-id="046c4-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="046c4-142">篩選 hello 清單 toolocate hello **NodeJS**外掛程式並將它安裝在不需重新啟動。</span><span class="sxs-lookup"><span data-stu-id="046c4-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![加入 hello NodeJS 外掛程式 tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="046c4-144">篩選 hello 清單 toofind hello **Team Foundation Server**外掛程式並安裝它。</span><span class="sxs-lookup"><span data-stu-id="046c4-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="046c4-145">(此外掛程式適用於 Team Services 和 Team Foundation Server。)不需要重新啟動 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="046c4-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="046c4-146">設定適用於 Node.js 的 Jenkins 組建</span><span class="sxs-lookup"><span data-stu-id="046c4-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="046c4-147">在 Jenkins 中建立新的組建專案並加以設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="046c4-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="046c4-148">在 hello**一般**索引標籤上，輸入您建置專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="046c4-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="046c4-149">在 hello**原始程式碼管理**索引標籤上，選取**Git** ，然後輸入 hello 的 hello 儲存機制與 hello 分支包含應用程式程式碼的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="046c4-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![加入儲存機制 tooyour 組建](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="046c4-151">如果您的儲存機制不是公用的請選擇**新增**並提供認證 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="046c4-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="046c4-152">在 hello**組建觸發程序**索引標籤上，選取**輪詢 SCM** ，然後輸入 hello 排程`H/03 * * * *`toopoll hello Git 儲存機制，變更每隔三分鐘。</span><span class="sxs-lookup"><span data-stu-id="046c4-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="046c4-153">在 hello **Build Environment**索引標籤上，選取**提供節點&amp;npm bin / 資料夾路徑**輸入`NodeJS`hello JS 安裝節點值。</span><span class="sxs-lookup"><span data-stu-id="046c4-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="046c4-154">將 **npmrc 檔案**的設定保留為「使用系統預設值」。</span><span class="sxs-lookup"><span data-stu-id="046c4-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="046c4-155">在 hello**建置**索引標籤上，輸入 hello 命令`npm install`tooensure 會更新所有相依性。</span><span class="sxs-lookup"><span data-stu-id="046c4-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="046c4-156">設定適用於 Team Services 整合的 Jenkins</span><span class="sxs-lookup"><span data-stu-id="046c4-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="046c4-157">在 hello**建置後動作**索引標籤上，針對**檔案 tooarchive**，輸入`**/*`tooinclude 所有檔案。</span><span class="sxs-lookup"><span data-stu-id="046c4-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="046c4-158">如**觸發 TFS/Team Services 中的發行**，輸入您的帳戶 hello 完整的 URL (例如`https://your-account-name.visualstudio.com`)、 hello 專案名稱，hello （稍後建立） 的發行定義、 名稱和 hello 認證 tooconnect tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="046c4-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="046c4-159">您需要使用者名稱及您稍早建立的 PAT hello。</span><span class="sxs-lookup"><span data-stu-id="046c4-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![設定 Jenkins 建置後動作](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="046c4-161">儲存 hello 建置專案。</span><span class="sxs-lookup"><span data-stu-id="046c4-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="046c4-162">建立 Jenkins 服務端點</span><span class="sxs-lookup"><span data-stu-id="046c4-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="046c4-163">服務端點可讓 Team Services tooconnect tooJenkins。</span><span class="sxs-lookup"><span data-stu-id="046c4-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="046c4-164">開啟 hello**服務**頁面在 Team Services 中，開啟 hello**新的服務端點**清單，並選擇**Jenkins**。</span><span class="sxs-lookup"><span data-stu-id="046c4-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![新增 Jenkins 端點](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="046c4-166">輸入您將使用 toorefer toothis 連接的名稱。</span><span class="sxs-lookup"><span data-stu-id="046c4-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="046c4-167">輸入您的 Jenkins 伺服器 hello URL 和刻度 hello**接受不受信任的 SSL 憑證**選項。</span><span class="sxs-lookup"><span data-stu-id="046c4-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="046c4-168">Jenkins 帳戶輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="046c4-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="046c4-169">選擇**驗證連線**toocheck 的 hello 資訊是否正確。</span><span class="sxs-lookup"><span data-stu-id="046c4-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="046c4-170">選擇**確定**toocreate hello 服務端點。</span><span class="sxs-lookup"><span data-stu-id="046c4-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="046c4-171">建立部署群組</span><span class="sxs-lookup"><span data-stu-id="046c4-171">Create a deployment group</span></span>

<span data-ttu-id="046c4-172">您需要[部署群組](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/)太包含 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="046c4-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="046c4-173">開啟 hello**版本**] 索引標籤的 hello**建置&amp;發行**集線器，然後開啟 hello**部署群組**索引標籤，然後選擇 [ **+ 新增**.</span><span class="sxs-lookup"><span data-stu-id="046c4-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="046c4-174">輸入 hello 部署群組，以及選擇性的描述名稱。</span><span class="sxs-lookup"><span data-stu-id="046c4-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="046c4-175">然後選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="046c4-175">Then choose **Create**.</span></span>

<span data-ttu-id="046c4-176">hello Azure 資源群組部署工作建立，並執行使用 hello Azure Resource Manager 範本時，登錄 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="046c4-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="046c4-177">您不需要 toocreate 並自行註冊 hello 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="046c4-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="046c4-178">建立發行定義</span><span class="sxs-lookup"><span data-stu-id="046c4-178">Create a release definition</span></span>

<span data-ttu-id="046c4-179">發行定義指定 hello 處理 Team Services 將會執行 toodeploy hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="046c4-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="046c4-180">toocreate hello Team Services 中的發行定義：</span><span class="sxs-lookup"><span data-stu-id="046c4-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="046c4-181">開啟 hello**版本** 索引標籤的 hello**建置&amp;釋放**集線器，開啟 hello  **+**  hello 清單的發行定義中的下拉式清單並選擇hello**建立發行定義**。</span><span class="sxs-lookup"><span data-stu-id="046c4-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="046c4-182">選取 hello**空**範本，然後選擇 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="046c4-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="046c4-183">在 hello**成品**區段中，按一下 上**連結成品**選擇**Jenkins**。</span><span class="sxs-lookup"><span data-stu-id="046c4-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="046c4-184">選取您的 Jenkins 服務端點連線。</span><span class="sxs-lookup"><span data-stu-id="046c4-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="046c4-185">然後選取 hello Jenkins 來源工作，並選擇 **建立**。</span><span class="sxs-lookup"><span data-stu-id="046c4-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="046c4-186">在 hello 新發行定義中，選擇**+ 加入工作**並加入**Azure 資源群組部署**工作 toohello 預設環境。</span><span class="sxs-lookup"><span data-stu-id="046c4-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="046c4-187">選擇 hello 下拉式箭號下一步 toohello **+ 加入工作**連結並新增部署群組階段 toohello 定義。</span><span class="sxs-lookup"><span data-stu-id="046c4-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![新增部署群組階段](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="046c4-189">在 hello 工作目錄中，開啟 hello**公用程式**區段，並將執行個體的 hello**殼層指令碼**工作。</span><span class="sxs-lookup"><span data-stu-id="046c4-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="046c4-190">hello Azure 資源群組部署工作中使用的 hello 參數範本會設定 hello 系統管理員使用的密碼 tooconnect toohello Vm。</span><span class="sxs-lookup"><span data-stu-id="046c4-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="046c4-191">您提供此密碼與 hello 變數**$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="046c4-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="046c4-192">開啟 hello**變數**] 索引標籤，然後在 [hello**變數**區段中，輸入 hello 名稱`adminpassword`。</span><span class="sxs-lookup"><span data-stu-id="046c4-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="046c4-193">輸入 hello 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="046c4-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="046c4-194">選擇 hello 「 鎖 」 圖示下一步 toohello 值文字方塊 tooprotect hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="046c4-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="046c4-195">設定 hello Azure 資源群組部署工作</span><span class="sxs-lookup"><span data-stu-id="046c4-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="046c4-196">hello **Azure 資源群組部署**工作是使用的 toocreate hello 部署群組。</span><span class="sxs-lookup"><span data-stu-id="046c4-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="046c4-197">進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="046c4-197">Configure it as follows:</span></span>

* <span data-ttu-id="046c4-198">**Azure 訂用帳戶：** hello 下方的清單中選取連接**可用的 Azure 服務連線**。</span><span class="sxs-lookup"><span data-stu-id="046c4-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="046c4-199">如果沒有連線出現，請選擇**管理**，選取**新的服務端點**然後**Azure Resource Manager**，依照 hello 提示。</span><span class="sxs-lookup"><span data-stu-id="046c4-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="046c4-200">傳回 tooyour 發行定義，重新整理 hello **AzureRM 訂用帳戶**清單及選取 hello 所建立的連接。</span><span class="sxs-lookup"><span data-stu-id="046c4-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="046c4-201">**資源群組**： 輸入您稍早建立的 hello 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="046c4-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="046c4-202">**位置**： 選取 hello 部署的區域。</span><span class="sxs-lookup"><span data-stu-id="046c4-202">**Location**: Select a region for hello deployment.</span></span>

  ![建立新的資源群組](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="046c4-204">**範本位置**：`URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="046c4-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="046c4-205">**範本連結**：`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="046c4-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="046c4-206">**範本參數連結**：`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="046c4-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="046c4-207">**覆寫範本參數**: hello 的清單會覆寫值，例如： `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`。</span><span class="sxs-lookup"><span data-stu-id="046c4-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="046c4-208">插入您自己的 hello {預留位置} 的特定值。</span><span class="sxs-lookup"><span data-stu-id="046c4-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="046c4-209">**啟用必要條件**：`Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="046c4-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="046c4-210">**TFS/VSTS 端點**： 選擇**新增**，並在 hello [加入新的 Team Foundation Server/Team Services 連接] 對話方塊中，選取**權杖型驗證**。</span><span class="sxs-lookup"><span data-stu-id="046c4-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="046c4-211">輸入 hello 連接的名稱和您的 team 專案的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="046c4-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="046c4-212">然後產生，並輸入[個人存取權杖 」 (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello 連接 tooyour team 專案。</span><span class="sxs-lookup"><span data-stu-id="046c4-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![建立個人存取權杖](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="046c4-214">**Team 專案**：選取您目前的專案。</span><span class="sxs-lookup"><span data-stu-id="046c4-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="046c4-215">**部署群組**： 輸入 hello 相同部署群組名稱，所使用的 hello**資源群組**參數。</span><span class="sxs-lookup"><span data-stu-id="046c4-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="046c4-216">hello hello Azure 資源群組部署工作的預設設定 toocreate 或因此以累加方式更新資源，以及 toodo。</span><span class="sxs-lookup"><span data-stu-id="046c4-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="046c4-217">hello 工作會建立 hello Vm hello 第一次執行時，之後就加以更新。</span><span class="sxs-lookup"><span data-stu-id="046c4-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="046c4-218">設定 hello 殼層指令碼工作</span><span class="sxs-lookup"><span data-stu-id="046c4-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="046c4-219">hello**殼層指令碼**工作是使用的 tooprovide hello 組態指令碼 toorun 上每個伺服器 tooinstall Node.js 和開始 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="046c4-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="046c4-220">進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="046c4-220">Configure it as follows:</span></span>

* <span data-ttu-id="046c4-221">**指令碼路徑**：`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="046c4-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="046c4-222">**指定工作目錄**：`Checked`</span><span class="sxs-lookup"><span data-stu-id="046c4-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="046c4-223">**工作目錄**：`$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="046c4-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="046c4-224">重新命名並儲存 hello 發行定義</span><span class="sxs-lookup"><span data-stu-id="046c4-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="046c4-225">編輯 hello hello 發行定義 toohello 名稱中指定名稱**建置後動作**hello Jenkins 組建 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="046c4-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="046c4-226">Jenkins 在 hello 來源成品更新時需要此名稱 toobe 無法 tootrigger 新版本。</span><span class="sxs-lookup"><span data-stu-id="046c4-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="046c4-227">（選擇性） 按一下 hello 名稱變更 hello hello 環境名稱。</span><span class="sxs-lookup"><span data-stu-id="046c4-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="046c4-228">選擇 [儲存]，然後選擇 [確定]。</span><span class="sxs-lookup"><span data-stu-id="046c4-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="046c4-229">啟動手動部署</span><span class="sxs-lookup"><span data-stu-id="046c4-229">Start a manual deployment</span></span>

1. <span data-ttu-id="046c4-230">選擇 [+ 發行]，然後選取 [建立發行]。</span><span class="sxs-lookup"><span data-stu-id="046c4-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="046c4-231">選取您已完成的 hello 組建 hello 反白顯示下拉式清單並選擇 **建立**。</span><span class="sxs-lookup"><span data-stu-id="046c4-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="046c4-232">選擇 hello 快顯訊息中的 hello 發行連結。</span><span class="sxs-lookup"><span data-stu-id="046c4-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="046c4-233">例如：「發行「**發行-1**」已建立。」</span><span class="sxs-lookup"><span data-stu-id="046c4-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="046c4-234">開啟 hello**記錄**toowatch hello 版本的主控台輸出索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="046c4-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="046c4-235">在瀏覽器中開啟 hello URL 的其中一部伺服器 hello 您加入 tooyour 部署群組。</span><span class="sxs-lookup"><span data-stu-id="046c4-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="046c4-236">例如，輸入 `http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="046c4-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="046c4-237">啟動 CI/CD 部署</span><span class="sxs-lookup"><span data-stu-id="046c4-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="046c4-238">在 hello 發行定義，請取消選取 hello**啟用**hello 中的核取方塊**控制選項**hello Azure 資源群組部署工作的 hello 設定一節。</span><span class="sxs-lookup"><span data-stu-id="046c4-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="046c4-239">未來的部署 toohello 現有的部署群組，您不需要 toore-執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="046c4-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="046c4-240">請移 toohello 來源 Git 儲存機制，並修改 hello hello 內容**h1** hello 檔案中的標題[app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade)。</span><span class="sxs-lookup"><span data-stu-id="046c4-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="046c4-241">認可變更。</span><span class="sxs-lookup"><span data-stu-id="046c4-241">Commit your change.</span></span>

1. <span data-ttu-id="046c4-242">請稍候幾分鐘，您會看到 hello 中建立新的版本**版本**Team Services 或 TFS 的頁面。</span><span class="sxs-lookup"><span data-stu-id="046c4-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="046c4-243">開啟 hello 發行 toosee hello 部署正在進行中。</span><span class="sxs-lookup"><span data-stu-id="046c4-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="046c4-244">恭喜！</span><span class="sxs-lookup"><span data-stu-id="046c4-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="046c4-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="046c4-245">Next Steps</span></span>

<span data-ttu-id="046c4-246">在本教學課程中，您可以自動使用 Jenkins 組建和版本的 Team Services 應用程式 tooAzure hello 部署。</span><span class="sxs-lookup"><span data-stu-id="046c4-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="046c4-247">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="046c4-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="046c4-248">在 Jenkins 中建置應用程式</span><span class="sxs-lookup"><span data-stu-id="046c4-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="046c4-249">設定適用於 Team Services 整合的 Jenkins</span><span class="sxs-lookup"><span data-stu-id="046c4-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="046c4-250">Azure 虛擬機器建立 hello 部署群組</span><span class="sxs-lookup"><span data-stu-id="046c4-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="046c4-251">建立設定 hello Vm，然後部署 hello 應用程式的發行定義</span><span class="sxs-lookup"><span data-stu-id="046c4-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="046c4-252">前進 toohello 下一個教學課程 toolearn 有關 toodeploy （Linux、 Apache、 MySQL 和 PHP） LAMP 堆疊的方式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="046c4-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="046c4-253">部署 LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="046c4-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)