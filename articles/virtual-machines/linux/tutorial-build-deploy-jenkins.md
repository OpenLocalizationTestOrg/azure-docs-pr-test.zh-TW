---
title: "透過 Team Services 將 CI/CD 從 Jenkins 部署到 Azure VM | Microsoft Docs"
description: "透過 Visual Studio Team Services (VSTS) 或 Microsoft Team Foundation Server (TFS) 中的 Release Management，使用 Jenkins 將 Node.js 應用程式的持續整合 (CI) 和持續部署 (CD) 安裝至 Azure VM"
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
ms.openlocfilehash: a40e26a8681df31fad664e4d1df4c1513311900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-linux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="170d1-103">使用 Jenkins 和 Team Services 將您的應用程式部署至 Linux Vm</span><span class="sxs-lookup"><span data-stu-id="170d1-103">Deploy your app to Linux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="170d1-104">持續整合 (CI) 與持續部署 (CD) 是讓您可以建置、發行和部署程式碼的管道。</span><span class="sxs-lookup"><span data-stu-id="170d1-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="170d1-105">Team Services 提供了一組完整且功能齊全的 CI/CD 自動化工具以便部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="170d1-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment to Azure.</span></span> <span data-ttu-id="170d1-106">Jenkins 是廣為使用的第三方 CI/CD 伺服器型工具，也提供 CI/CD 自動化。</span><span class="sxs-lookup"><span data-stu-id="170d1-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="170d1-107">您可以同時使用這兩者來自訂雲端應用程式或服務的傳遞方式。</span><span class="sxs-lookup"><span data-stu-id="170d1-107">You can use both together to customize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="170d1-108">在此教學課程中，您可以使用 Jenkins 建置 **Node.js Web 應用程式**，並使用 Visual Studio Team Services 將其部署至包含 Linux 虛擬機器的[部署群組](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/)。</span><span class="sxs-lookup"><span data-stu-id="170d1-108">In this tutorial, you use Jenkins to build a **Node.js web app**, and Visual Studio Team Services to deploy it to a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="170d1-109">您將：</span><span class="sxs-lookup"><span data-stu-id="170d1-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="170d1-110">在 Jenkins 中建置應用程式</span><span class="sxs-lookup"><span data-stu-id="170d1-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="170d1-111">設定適用於 Team Services 整合的 Jenkins</span><span class="sxs-lookup"><span data-stu-id="170d1-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="170d1-112">建立 Azure 虛擬機器的部署群組</span><span class="sxs-lookup"><span data-stu-id="170d1-112">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="170d1-113">建立發行定義以設定 VM 及部署應用程式</span><span class="sxs-lookup"><span data-stu-id="170d1-113">Create a release definition that configures the VMs and deploys the app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="170d1-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="170d1-114">Before you begin</span></span>

* <span data-ttu-id="170d1-115">您需要 Jenkins 帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="170d1-115">You need access to a Jenkins account.</span></span> <span data-ttu-id="170d1-116">如果您尚未建立 Jenkins 伺服器，請參閱 [Jenkins 文件](https://jenkins.io/doc/)。</span><span class="sxs-lookup"><span data-stu-id="170d1-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="170d1-117">登入您的 Team Services 帳戶 (`https://{youraccount}.visualstudio.com`)。</span><span class="sxs-lookup"><span data-stu-id="170d1-117">Sign in to your Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="170d1-118">您可以取得[免費的 Team Services 帳戶](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308)。</span><span class="sxs-lookup"><span data-stu-id="170d1-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="170d1-119">如需詳細資訊，請參閱＜[連線至 Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services)＞。</span><span class="sxs-lookup"><span data-stu-id="170d1-119">For more information, see [Connect to Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="170d1-120">如果您的 Team Services 帳戶中沒有個人存取權杖 (PAT)，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="170d1-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="170d1-121">Jenkins 需要這項資訊來存取您的 Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="170d1-121">Jenkins requires this information to access your Team Services account.</span></span>
  <span data-ttu-id="170d1-122">請閱讀＜[如何建立 Team Services 和 TFS 的個人存取權杖](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)＞，以了解如何產生個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="170d1-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to learn how to generate one.</span></span>

## <a name="get-the-sample-app"></a><span data-ttu-id="170d1-123">取得範例應用程式</span><span class="sxs-lookup"><span data-stu-id="170d1-123">Get the sample app</span></span>

<span data-ttu-id="170d1-124">您需要可部署的應用程式 (儲存在 Git 存放庫)。</span><span class="sxs-lookup"><span data-stu-id="170d1-124">You need an app to deploy stored in a Git repository.</span></span>
<span data-ttu-id="170d1-125">在本教學課程中，我們建議您使用[從 GitHub 中取得的此範例應用程式](https://github.com/azooinmyluggage/fabrikam-node)。</span><span class="sxs-lookup"><span data-stu-id="170d1-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="170d1-126">建立此應用程式的分支並記下位置 (URL)，此教學課程的後續步驟中會用到此位置。</span><span class="sxs-lookup"><span data-stu-id="170d1-126">Create a fork of this app and take note of the location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="170d1-127">將分支設為**公用**，以便之後可輕易連線到 GitHub。</span><span class="sxs-lookup"><span data-stu-id="170d1-127">Make the fork **public** to simplify connecting to GitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="170d1-128">如需詳細資訊，請參閱＜[建立存放庫的分支](https://help.github.com/articles/fork-a-repo/)＞和＜[將私密存放庫設為公用](https://help.github.com/articles/making-a-private-repository-public/)＞。</span><span class="sxs-lookup"><span data-stu-id="170d1-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="170d1-129">應用程式是使用 [Yeoman](http://yeoman.io/learning/index.html) 建置的；可使用 **Express**、**bower** 和 **grunt**；而且具有一些 **npm** 套件作為相依項目。</span><span class="sxs-lookup"><span data-stu-id="170d1-129">The app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="170d1-130">範例應用程式包含一組 [Azure Resource Manager 範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)，用於動態地建立虛擬機器，以便在 Azure 上進行部署。</span><span class="sxs-lookup"><span data-stu-id="170d1-130">The sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used to dynamically create the virtual machines for deployment on Azure.</span></span> <span data-ttu-id="170d1-131">這些範本會由 [Team Services 發行定義](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions)中的工作使用。</span><span class="sxs-lookup"><span data-stu-id="170d1-131">These templates are used by tasks in the [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="170d1-132">主要範本會建立網路安全性群組、虛擬機器和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="170d1-132">The main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="170d1-133">並指派公用 IP 位址和開啟輸入連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="170d1-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="170d1-134">主要範本也會新增由部署群組使用的標記，以選取要接收部署的機器。</span><span class="sxs-lookup"><span data-stu-id="170d1-134">It also adds a tag that is used by the deployment group to select the machines to receive the deployment.</span></span>
>
> <span data-ttu-id="170d1-135">此範例也包含設定 Nginx 和部署應用程式的指令碼。</span><span class="sxs-lookup"><span data-stu-id="170d1-135">The sample also contains a script that sets up Nginx and deploys the app.</span></span> <span data-ttu-id="170d1-136">其執行於每部虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="170d1-136">It is executed on each of the virtual machines.</span></span> <span data-ttu-id="170d1-137">具體來說，指令碼會安裝節點、Nginx 和 PM2，以及設定 Nginx 和 PM2，然後啟動節點應用程式。</span><span class="sxs-lookup"><span data-stu-id="170d1-137">Specifically, the script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts the Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="170d1-138">設定 Jenkins 外掛程式</span><span class="sxs-lookup"><span data-stu-id="170d1-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="170d1-139">首先，您必須設定兩個 Jenkins 外掛程式，用於 **NodeJS**，以及**與 Team Services 整合**。</span><span class="sxs-lookup"><span data-stu-id="170d1-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="170d1-140">開啟您的 Jenkins 帳戶，然後選擇 [管理 Jenkins]。</span><span class="sxs-lookup"><span data-stu-id="170d1-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="170d1-141">在 [管理 Jenkins] 頁面中，選擇 [管理外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="170d1-141">In the **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="170d1-142">篩選清單以找出 **NodeJS** 外掛程式並安裝，無須重新啟動。</span><span class="sxs-lookup"><span data-stu-id="170d1-142">Filter the list to locate the **NodeJS** plugin and install it without restart.</span></span>

   ![將 NodeJS 外掛程式新增至 Jenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="170d1-144">篩選清單以找出 **Team Foundation Server** 外掛程式並安裝。</span><span class="sxs-lookup"><span data-stu-id="170d1-144">Filter the list to find the **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="170d1-145">(此外掛程式適用於 Team Services 和 Team Foundation Server。)不需要重新啟動 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="170d1-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="170d1-146">設定適用於 Node.js 的 Jenkins 組建</span><span class="sxs-lookup"><span data-stu-id="170d1-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="170d1-147">在 Jenkins 中建立新的組建專案並加以設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="170d1-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="170d1-148">在 [一般] 索引標籤中，輸入組建專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="170d1-148">In the **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="170d1-149">在 [原始程式碼管理] 索引標籤中，選取**Git**，然後輸入包含應用程式程式碼的存放庫與分支詳細資料。</span><span class="sxs-lookup"><span data-stu-id="170d1-149">In the **Source Code Management** tab, select **Git** and enter the details of the repository and the branch containing your app code.</span></span>

   ![將存放庫新增至組建](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="170d1-151">如果您的存放庫不是公用的，請選擇 [新增]，並提供認證以便進行連線。</span><span class="sxs-lookup"><span data-stu-id="170d1-151">If your repository is not public, choose **Add** and provide credentials to connect to it.</span></span>

1. <span data-ttu-id="170d1-152">在 [組建觸發程序] 索引標籤上，選取 [Poll SCM]\(輪詢 SCM\)，並輸入排程 `H/03 * * * *`，每隔三分鐘輪詢 Git 存放庫以檢查變更。</span><span class="sxs-lookup"><span data-stu-id="170d1-152">In the **Build Triggers** tab, select **Poll SCM** and enter the schedule `H/03 * * * *` to poll the Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="170d1-153">在 [組建環境] 索引標籤上，選取 [Provide Node &amp; npm bin/ folder PATH]\(提供節點與 npm bin/ 資料夾路徑\)，並輸入 `NodeJS` 作為 Node JS 安裝值。</span><span class="sxs-lookup"><span data-stu-id="170d1-153">In the **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for the Node JS Installation value.</span></span> <span data-ttu-id="170d1-154">將 **npmrc 檔案**的設定保留為「使用系統預設值」。</span><span class="sxs-lookup"><span data-stu-id="170d1-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="170d1-155">在 [組建] 索引標籤上，輸入命令 `npm install`，以確保所有相依項目都會更新。</span><span class="sxs-lookup"><span data-stu-id="170d1-155">In the **Build** tab, enter the command `npm install` to ensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="170d1-156">設定適用於 Team Services 整合的 Jenkins</span><span class="sxs-lookup"><span data-stu-id="170d1-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="170d1-157">在 [建置後動作] 索引標籤上，針對 [要封存的檔案] 輸入 `**/*` 以包含所有檔案。</span><span class="sxs-lookup"><span data-stu-id="170d1-157">In the **Post-build Actions** tab, for **Files to archive**, enter `**/*` to include all files.</span></span>

1. <span data-ttu-id="170d1-158">針對 [觸發 TFS/Team Services 中的發行]，輸入帳戶的完整 URL (例如 `https://your-account-name.visualstudio.com`)、專案名稱、版本定義的名稱 (稍後建立) 和認證，以便與您的帳戶連線。</span><span class="sxs-lookup"><span data-stu-id="170d1-158">For **Trigger release in TFS/Team Services**, enter the full URL of your account (such as `https://your-account-name.visualstudio.com`), the project name, a name for the release definition (created later), and the credentials to connect to your account.</span></span>
   <span data-ttu-id="170d1-159">需要您的使用者名稱和您稍早建立的 PAT。</span><span class="sxs-lookup"><span data-stu-id="170d1-159">You need your user name and the PAT you created earlier.</span></span> 

   ![設定 Jenkins 建置後動作](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="170d1-161">儲存組建專案。</span><span class="sxs-lookup"><span data-stu-id="170d1-161">Save the build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="170d1-162">建立 Jenkins 服務端點</span><span class="sxs-lookup"><span data-stu-id="170d1-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="170d1-163">服務端點可讓 Team Services 與 Jenkins 連線。</span><span class="sxs-lookup"><span data-stu-id="170d1-163">A service endpoint allows Team Services to connect to Jenkins.</span></span>

1. <span data-ttu-id="170d1-164">開啟 Team Services 中的 [服務] 頁面，並開啟 [新的服務端點] 清單，然後選擇 [Jenkins]。</span><span class="sxs-lookup"><span data-stu-id="170d1-164">Open the **Services** page in Team Services, open the **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![新增 Jenkins 端點](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="170d1-166">輸入您用來表示此連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="170d1-166">Enter a name you will use to refer to this connection.</span></span>

1. <span data-ttu-id="170d1-167">輸入您的 Jenkins 伺服器 URL，並核取 [接受未受信任的 SSL 憑證] 選項。</span><span class="sxs-lookup"><span data-stu-id="170d1-167">Enter the URL of your Jenkins server, and tick the **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="170d1-168">輸入您 Jenkins 帳戶的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="170d1-168">Enter the user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="170d1-169">選擇 [驗證連線] 以檢查資訊是否正確。</span><span class="sxs-lookup"><span data-stu-id="170d1-169">Choose **Verify connection** to check that the information is correct.</span></span>

1. <span data-ttu-id="170d1-170">選擇 [確定] 以建立服務端點。</span><span class="sxs-lookup"><span data-stu-id="170d1-170">Choose **OK** to create the service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="170d1-171">建立部署群組</span><span class="sxs-lookup"><span data-stu-id="170d1-171">Create a deployment group</span></span>

<span data-ttu-id="170d1-172">您需要[部署群組](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/)以包含虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="170d1-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) to  contain the virtual machines.</span></span>

1. <span data-ttu-id="170d1-173">開啟 [組建與發行] 中樞裡的 [版本] 索引標籤，然後開啟 [部署群組] 索引標籤，並選擇 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="170d1-173">Open the **Releases** tab of the **Build &amp; Release** hub, then open the **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="170d1-174">輸入部署群組的名稱和選擇性說明。</span><span class="sxs-lookup"><span data-stu-id="170d1-174">Enter a name for the deployment group, and an optional description.</span></span>
   <span data-ttu-id="170d1-175">然後選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="170d1-175">Then choose **Create**.</span></span>

<span data-ttu-id="170d1-176">當 Azure 資源群組部署工作使用 Azure Resource Manager 範本執行時，該工作會建立與註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="170d1-176">The Azure Resource Group Deployment task creates and registers the VMs when it runs using the Azure Resource Manager template.</span></span>
<span data-ttu-id="170d1-177">您不需要自行建立與註冊虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="170d1-177">You don't need to create and register the virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="170d1-178">建立發行定義</span><span class="sxs-lookup"><span data-stu-id="170d1-178">Create a release definition</span></span>

<span data-ttu-id="170d1-179">發行定義會指定 Team Services 要執行的流程，以部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="170d1-179">A release definition specifies the process Team Services will execute to deploy the app.</span></span>
<span data-ttu-id="170d1-180">在 Team Services 中建立發行定義：</span><span class="sxs-lookup"><span data-stu-id="170d1-180">To create the release definition in Team Services:</span></span>

1. <span data-ttu-id="170d1-181">開啟 [組建與發行] 中樞裡的 [發行] 索引標籤，並開啟發行定義中的 **+** 下拉式清單，然後選取 [建立發行定義]。</span><span class="sxs-lookup"><span data-stu-id="170d1-181">Open the **Releases** tab of the **Build &amp; Release** hub, open the **+** drop-down in the list of release definitions, and choose the **Create release definition**.</span></span> 

1. <span data-ttu-id="170d1-182">選取 [空白] 範本，並選擇 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="170d1-182">Select the **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="170d1-183">在 [成品] 區段中，按一下 [連結成品]，並選擇 [Jenkins]。</span><span class="sxs-lookup"><span data-stu-id="170d1-183">In the **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="170d1-184">選取您的 Jenkins 服務端點連線。</span><span class="sxs-lookup"><span data-stu-id="170d1-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="170d1-185">然後選取 Jenkins 來源作業，並選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="170d1-185">Then select the Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="170d1-186">在新的發行定義中，選擇 [+ 加入工作]，並將 **Azure 資源群組部署** 工作新增至預設環境。</span><span class="sxs-lookup"><span data-stu-id="170d1-186">In the new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task to the default environment.</span></span>

1. <span data-ttu-id="170d1-187">選擇 [+ 加入工作] 連結旁的下拉箭頭，然後將部署群組階段新增至定義。</span><span class="sxs-lookup"><span data-stu-id="170d1-187">Choose the drop down arrow next to the **+ Add tasks** link and add a deployment group phase to the definition.</span></span>

   ![新增部署群組階段](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="170d1-189">在工作目錄中，開啟 [公用程式] 區段，然後新增**殼層指令碼**工作的執行個體。</span><span class="sxs-lookup"><span data-stu-id="170d1-189">In the Task catalog, open the **Utility** section and add an instance of the **Shell Script** task.</span></span>

1. <span data-ttu-id="170d1-190">Azure 資源群組部署工作中使用的參數範本會設定系統管理員密碼，以用來與 VM 連線。</span><span class="sxs-lookup"><span data-stu-id="170d1-190">The parameters template used in the Azure Resource Group Deployment task sets the admin password used to connect to the VMs.</span></span>
   <span data-ttu-id="170d1-191">您會使用變數 **$(adminpassword)** 來提供此密碼：</span><span class="sxs-lookup"><span data-stu-id="170d1-191">You provide this password with the variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="170d1-192">開啟 [變數] 索引標籤，然後在 [變數] 區段中輸入名稱 `adminpassword`。</span><span class="sxs-lookup"><span data-stu-id="170d1-192">Open the **Variables** tab and, in the **Variables** section, enter the name `adminpassword`.</span></span>

   - <span data-ttu-id="170d1-193">輸入系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="170d1-193">Enter the administrator password.</span></span>

   - <span data-ttu-id="170d1-194">選擇值文字方塊旁的「掛鎖」圖示來保護密碼。</span><span class="sxs-lookup"><span data-stu-id="170d1-194">Choose the "padlock" icon next to the value textbox to protect the password.</span></span> 

## <a name="configure-the-azure-resource-group-deployment-task"></a><span data-ttu-id="170d1-195">設定 Azure 資源群組部署工作</span><span class="sxs-lookup"><span data-stu-id="170d1-195">Configure the Azure Resource Group Deployment task</span></span>

<span data-ttu-id="170d1-196">**Azure 資源群組部署**工作可用來建立部署群組。</span><span class="sxs-lookup"><span data-stu-id="170d1-196">The **Azure Resource Group Deployment** task is used to create the deployment group.</span></span> <span data-ttu-id="170d1-197">進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="170d1-197">Configure it as follows:</span></span>

* <span data-ttu-id="170d1-198">**Azure 訂用帳戶：**從 [可用的 Azure 服務連線] 下方的清單選取連線。</span><span class="sxs-lookup"><span data-stu-id="170d1-198">**Azure Subscription:** Select a connection from the list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="170d1-199">如果沒有顯示任何連線，請選擇 [管理]，並選取 [新的服務端點]與 [Azure Resource Manager]，然後依循提示操作。</span><span class="sxs-lookup"><span data-stu-id="170d1-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow the prompts.</span></span>
  <span data-ttu-id="170d1-200">返回您的發行定義，重新整理 [AzureRM 訂用帳戶] 清單，並選取您建立的連線。</span><span class="sxs-lookup"><span data-stu-id="170d1-200">Return to your release definition, refresh the **AzureRM Subscription** list, and select the connection you created.</span></span>

* <span data-ttu-id="170d1-201">**資源群組**：輸入您稍早建立的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="170d1-201">**Resource group**: Enter a name of the resource group you created earlier.</span></span>

* <span data-ttu-id="170d1-202">**位置**：選取部署地區。</span><span class="sxs-lookup"><span data-stu-id="170d1-202">**Location**: Select a region for the deployment.</span></span>

  ![建立新的資源群組](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="170d1-204">**範本位置**：`URL of the file`</span><span class="sxs-lookup"><span data-stu-id="170d1-204">**Template location**: `URL of the file`</span></span>

* <span data-ttu-id="170d1-205">**範本連結**：`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="170d1-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="170d1-206">**範本參數連結**：`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="170d1-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="170d1-207">**覆寫範本參數**：覆寫值的清單，例如：`-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`。</span><span class="sxs-lookup"><span data-stu-id="170d1-207">**Override template parameters**: A list of the override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="170d1-208">在 {預留位置} 插入您自己的特定值。</span><span class="sxs-lookup"><span data-stu-id="170d1-208">Insert your own specific values for the {placeholders}.</span></span> 

* <span data-ttu-id="170d1-209">**啟用必要條件**：`Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="170d1-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="170d1-210">**TFS/VSTS 端點**：選擇 [新增]，然後在 [新增 Team Foundation Server/Team Services 連線] 對話方塊中，選取 [權杖型驗證]。</span><span class="sxs-lookup"><span data-stu-id="170d1-210">**TFS/VSTS endpoint**: Choose **Add** and, in the "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="170d1-211">輸入連線的名稱和您的 Team 專案 URL。</span><span class="sxs-lookup"><span data-stu-id="170d1-211">Enter a name of the connection and the URL of your team project.</span></span> <span data-ttu-id="170d1-212">接著產生並輸入[個人存取權杖 (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)，以驗證 Team 專案上的連線。</span><span class="sxs-lookup"><span data-stu-id="170d1-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to authenticate the connection to your team project.</span></span>

  ![建立個人存取權杖](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="170d1-214">**Team 專案**：選取您目前的專案。</span><span class="sxs-lookup"><span data-stu-id="170d1-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="170d1-215">**部署群組**：輸入部署群組名稱，需與**資源群組**參數所用的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="170d1-215">**Deployment Group**: Enter the same deployment group name as you used for the **Resource group** parameter.</span></span>

<span data-ttu-id="170d1-216">Azure 資源群組部署工作的預設設定是要建立或更新資源，並漸進式地執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="170d1-216">The default settings for the Azure Resource Group Deployment task are to create or update a resource, and to do so incrementally.</span></span> <span data-ttu-id="170d1-217">此工作會在第一次執行時建立 VM，而之後只進行更新。</span><span class="sxs-lookup"><span data-stu-id="170d1-217">The task creates the VMs the first time it runs, and subsequently just update them.</span></span>

## <a name="configure-the-shell-script-task"></a><span data-ttu-id="170d1-218">設定殼層指令碼工作</span><span class="sxs-lookup"><span data-stu-id="170d1-218">Configure the Shell Script task</span></span>

<span data-ttu-id="170d1-219">**殼層指令碼**工作用來提供每個伺服器上要執行的指令碼組態，以安裝 Node.js 並啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="170d1-219">The **Shell Script** task is used to provide the configuration for a script to run on each server to install Node.js and start the app.</span></span> <span data-ttu-id="170d1-220">進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="170d1-220">Configure it as follows:</span></span>

* <span data-ttu-id="170d1-221">**指令碼路徑**：`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="170d1-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="170d1-222">**指定工作目錄**：`Checked`</span><span class="sxs-lookup"><span data-stu-id="170d1-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="170d1-223">**工作目錄**：`$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="170d1-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-the-release-definition"></a><span data-ttu-id="170d1-224">重新命名和儲存發行定義</span><span class="sxs-lookup"><span data-stu-id="170d1-224">Rename and save the release definition</span></span>

1. <span data-ttu-id="170d1-225">將發行定義的名稱編輯為 [建置後動作] 索引標籤中 (位於 Jenkins 組建) 指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="170d1-225">Edit the name of the release definition to the name you specified in the **Post-build Actions** tab of the build in Jenkins.</span></span> <span data-ttu-id="170d1-226">當來源成品更新時，Jenkins 需要此名稱才可觸發新的發行。</span><span class="sxs-lookup"><span data-stu-id="170d1-226">Jenkins requires this name to be able to trigger a new release when the source artifacts are updated.</span></span>

1. <span data-ttu-id="170d1-227">(選擇性) 按一下環境名稱可變更名稱。</span><span class="sxs-lookup"><span data-stu-id="170d1-227">Optionally, change the name of the environment by clicking on the name.</span></span> 

1. <span data-ttu-id="170d1-228">選擇 [儲存]，然後選擇 [確定]。</span><span class="sxs-lookup"><span data-stu-id="170d1-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="170d1-229">啟動手動部署</span><span class="sxs-lookup"><span data-stu-id="170d1-229">Start a manual deployment</span></span>

1. <span data-ttu-id="170d1-230">選擇 [+ 發行]，然後選取 [建立發行]。</span><span class="sxs-lookup"><span data-stu-id="170d1-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="170d1-231">在反白顯示的下拉式清單中選取您完成的組建，並選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="170d1-231">Select the build you completed in the highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="170d1-232">在快顯視窗訊息中選擇發行連結。</span><span class="sxs-lookup"><span data-stu-id="170d1-232">Choose the release link in the popup message.</span></span> <span data-ttu-id="170d1-233">例如：「發行「**發行-1**」已建立。」</span><span class="sxs-lookup"><span data-stu-id="170d1-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="170d1-234">開啟 [記錄] 索引標籤以查看發行主控台輸出。</span><span class="sxs-lookup"><span data-stu-id="170d1-234">Open the **Logs** tab to watch the release console output.</span></span>

1. <span data-ttu-id="170d1-235">在瀏覽器中，開啟您在部署群組中新增的其中一個伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="170d1-235">In your browser, open the URL of one of the servers you added to your deployment group.</span></span> <span data-ttu-id="170d1-236">例如，輸入 `http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="170d1-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="170d1-237">啟動 CI/CD 部署</span><span class="sxs-lookup"><span data-stu-id="170d1-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="170d1-238">在發行定義中，從 Azure 資源群組部署工作設定上的 [控制選項] 區段中，取消核取 [啟用] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="170d1-238">In the release definition, uncheck the **Enabled** checkbox in the **Control Options** section of the settings for the Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="170d1-239">未來若要在現有部署群組上進行部署時，您將不需要重新執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="170d1-239">For future deployments to the existing deployment group, you do not need to re-execute this task.</span></span>

1. <span data-ttu-id="170d1-240">移至來源 Git 存放庫，並修改 [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade) 檔案中的 **h1** 標題。</span><span class="sxs-lookup"><span data-stu-id="170d1-240">Go to the source Git repository and modify the contents of the **h1** heading in the file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="170d1-241">認可變更。</span><span class="sxs-lookup"><span data-stu-id="170d1-241">Commit your change.</span></span>

1. <span data-ttu-id="170d1-242">稍待幾分鐘後，您會在 Team Services 或 TFS 的 [發行] 頁面上看到新的發行。</span><span class="sxs-lookup"><span data-stu-id="170d1-242">After a few minutes, you will see a new release created in the **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="170d1-243">開啟發行以查看正在進行的部署。</span><span class="sxs-lookup"><span data-stu-id="170d1-243">Open the release to see the deployment taking place.</span></span> <span data-ttu-id="170d1-244">恭喜！</span><span class="sxs-lookup"><span data-stu-id="170d1-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="170d1-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="170d1-245">Next Steps</span></span>

<span data-ttu-id="170d1-246">在本教學課程中，您已會使用 Jenkins 組建和 Team Services (用於發行) 將應用程式自動部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="170d1-246">In this tutorial, you automated the deployment of an app to Azure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="170d1-247">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="170d1-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="170d1-248">在 Jenkins 中建置應用程式</span><span class="sxs-lookup"><span data-stu-id="170d1-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="170d1-249">設定適用於 Team Services 整合的 Jenkins</span><span class="sxs-lookup"><span data-stu-id="170d1-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="170d1-250">建立 Azure 虛擬機器的部署群組</span><span class="sxs-lookup"><span data-stu-id="170d1-250">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="170d1-251">建立發行定義以設定 VM 及部署應用程式</span><span class="sxs-lookup"><span data-stu-id="170d1-251">Create a release definition that configures the VMs and deploys the app</span></span>

<span data-ttu-id="170d1-252">前進到下一個教學課程，以了解如何部署 LAMP (Linux、Apache、MySQL 和 PHP) 堆疊。</span><span class="sxs-lookup"><span data-stu-id="170d1-252">Advance to the next tutorial to learn more about how to deploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="170d1-253">部署 LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="170d1-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)