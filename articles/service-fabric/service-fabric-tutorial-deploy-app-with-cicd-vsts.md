---
title: "aaaDeploy Azure Service Fabric 應用程式使用持續整合 (Team Services) |Microsoft 文件"
description: "深入了解如何 tooset 連續整合和部署使用 Visual Studio Team Services Service Fabric 應用程式。  部署 Azure 應用程式 tooa Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a><span data-ttu-id="13b91-104">部署應用程式與 CI/CD tooa Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="13b91-104">Deploy an application with CI/CD tooa Service Fabric cluster</span></span>
<span data-ttu-id="13b91-105">本教學課程是三個一系列的一部分，並說明如何 tooset 連續整合和部署 Azure Service Fabric 應用程式使用 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="13b91-105">This tutorial is part three of a series and describes how tooset up continuous integration and deployment for an Azure Service Fabric application using Visual Studio Team Services.</span></span>  <span data-ttu-id="13b91-106">現有的 Service Fabric 應用程式需要會在建立 hello 應用程式[建置.NET 應用程式](service-fabric-tutorial-create-dotnet-app.md)用做為範例。</span><span class="sxs-lookup"><span data-stu-id="13b91-106">An existing Service Fabric application is needed, hello application created in [Build a .NET application](service-fabric-tutorial-create-dotnet-app.md) is used as an example.</span></span>

<span data-ttu-id="13b91-107">在 hello 系列的一部分三，您將學習如何：</span><span class="sxs-lookup"><span data-stu-id="13b91-107">In part three of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="13b91-108">加入原始檔控制 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="13b91-108">Add source control tooyour project</span></span>
> * <span data-ttu-id="13b91-109">在 Team Services 中建立組建定義</span><span class="sxs-lookup"><span data-stu-id="13b91-109">Create a build definition in Team Services</span></span>
> * <span data-ttu-id="13b91-110">在 Team Services 中建立發行定義</span><span class="sxs-lookup"><span data-stu-id="13b91-110">Create a release definition in Team Services</span></span>
> * <span data-ttu-id="13b91-111">自動部署和升級應用程式</span><span class="sxs-lookup"><span data-stu-id="13b91-111">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="13b91-112">在本教學課程系列中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="13b91-112">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="13b91-113">建置 .NET Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="13b91-113">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * [<span data-ttu-id="13b91-114">部署 hello 應用程式 tooa 遠端叢集</span><span class="sxs-lookup"><span data-stu-id="13b91-114">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * <span data-ttu-id="13b91-115">使用 Visual Studio Team Services 設定 CI/CD</span><span class="sxs-lookup"><span data-stu-id="13b91-115">Configure CI/CD using Visual Studio Team Services</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13b91-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="13b91-116">Prerequisites</span></span>
<span data-ttu-id="13b91-117">開始進行本教學課程之前：</span><span class="sxs-lookup"><span data-stu-id="13b91-117">Before you begin this tutorial:</span></span>
- <span data-ttu-id="13b91-118">如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="13b91-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="13b91-119">[安裝 Visual Studio 2017](https://www.visualstudio.com/)並安裝 hello **Azure 開發**和**ASP.NET 及 web 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="13b91-119">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="13b91-120">安裝 hello Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="13b91-120">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)
- <span data-ttu-id="13b91-121">建立 Service Fabric 應用程式，例如[遵循本教學課程](service-fabric-tutorial-create-dotnet-app.md)。</span><span class="sxs-lookup"><span data-stu-id="13b91-121">Create a Service Fabric application, for example by [following this tutorial](service-fabric-tutorial-create-dotnet-app.md).</span></span> 
- <span data-ttu-id="13b91-122">在 Azure 上建立 Windows Service Fabric 叢集，例如[遵循本教學課程](service-fabric-tutorial-create-cluster-azure-ps.md)</span><span class="sxs-lookup"><span data-stu-id="13b91-122">Create a Windows Service Fabric cluster on Azure, for example by [following this tutorial](service-fabric-tutorial-create-cluster-azure-ps.md)</span></span>
- <span data-ttu-id="13b91-123">建立 [Team Services 帳戶](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)。</span><span class="sxs-lookup"><span data-stu-id="13b91-123">Create a [Team Services account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span></span>

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="13b91-124">下載 hello 投票範例應用程式</span><span class="sxs-lookup"><span data-stu-id="13b91-124">Download hello Voting sample application</span></span>
<span data-ttu-id="13b91-125">如果您未建立 hello 投票範例應用程式[第一部此教學課程系列的](service-fabric-tutorial-create-dotnet-app.md)，您可以下載它。</span><span class="sxs-lookup"><span data-stu-id="13b91-125">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="13b91-126">在命令視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="13b91-126">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a><span data-ttu-id="13b91-127">下載發行設定檔</span><span class="sxs-lookup"><span data-stu-id="13b91-127">Prepare a publish profile</span></span>
<span data-ttu-id="13b91-128">現在，您已經[建立的應用程式](service-fabric-tutorial-create-dotnet-app.md)，而且有[部署 hello 應用程式 tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md)，您已準備好 tooset 連續整合。</span><span class="sxs-lookup"><span data-stu-id="13b91-128">Now that you've [created an application](service-fabric-tutorial-create-dotnet-app.md) and have [deployed hello application tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), you're ready tooset up continuous integration.</span></span>  <span data-ttu-id="13b91-129">首先，準備用於應用程式中的發行設定檔的 Team Services 中執行的 hello 部署程序。</span><span class="sxs-lookup"><span data-stu-id="13b91-129">First, prepare a publish profile within your application for use by hello deployment process that executes within Team Services.</span></span>  <span data-ttu-id="13b91-130">hello 發行設定檔應該是您先前建立的設定的 tootarget hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="13b91-130">hello publish profile should be configured tootarget hello cluster that you've previously created.</span></span>  <span data-ttu-id="13b91-131">啟動 Visual Studio，並開啟現有的 Service Fabric 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="13b91-131">Start Visual Studio and open an existing Service Fabric application project.</span></span>  <span data-ttu-id="13b91-132">在**方案總管 中**，hello 應用程式上按一下滑鼠右鍵，然後選取**發行...**.</span><span class="sxs-lookup"><span data-stu-id="13b91-132">In **Solution Explorer**, right-click hello application and select **Publish...**.</span></span>

<span data-ttu-id="13b91-133">選擇目標設定檔內的連續整合流程您應用程式專案 toouse，例如雲端。</span><span class="sxs-lookup"><span data-stu-id="13b91-133">Choose a target profile within your application project toouse for your continuous integration workflow, for example Cloud.</span></span>  <span data-ttu-id="13b91-134">指定 hello 叢集連線端點。</span><span class="sxs-lookup"><span data-stu-id="13b91-134">Specify hello cluster connection endpoint.</span></span>  <span data-ttu-id="13b91-135">檢查 hello**升級 hello 應用程式**核取方塊，讓您的應用程式升級的 Team Services 中的每個部署。</span><span class="sxs-lookup"><span data-stu-id="13b91-135">Check hello **Upgrade hello Application** checkbox so that your application upgrades for each deployment in Team Services.</span></span>  <span data-ttu-id="13b91-136">按一下 hello**儲存**超連結 toosave hello 設定 toohello 發行設定檔，然後按一下**取消**tooclose hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="13b91-136">Click hello **Save** hyperlink toosave hello settings toohello publish profile and then click **Cancel** tooclose hello dialog box.</span></span>  

![推送設定檔][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a><span data-ttu-id="13b91-138">共用您 Visual Studio 方案 tooa 新 Team Services 的 Git 儲存機制</span><span class="sxs-lookup"><span data-stu-id="13b91-138">Share your Visual Studio solution tooa new Team Services Git repo</span></span>
<span data-ttu-id="13b91-139">共用 tooa team 專案，因此您可以產生 Team Services 中的建置您的應用程式原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="13b91-139">Share your application source files tooa team project in Team Services so you can generate builds.</span></span>  

<span data-ttu-id="13b91-140">選取建立新本機 Git 儲存機制專案**新增 tooSource 控制項** -> **Git** hello 右下角的 Visual Studio 中的 hello 狀態列上。</span><span class="sxs-lookup"><span data-stu-id="13b91-140">Create a new local Git repo for your project by selecting **Add tooSource Control** -> **Git** on hello status bar in hello lower right-hand corner of Visual Studio.</span></span> 

<span data-ttu-id="13b91-141">在 hello**推播**檢視中**Team Explorer**，選取 hello**發行 Git 儲存機制**按鈕底下**推送 tooVisual Studio Team Services**。</span><span class="sxs-lookup"><span data-stu-id="13b91-141">In hello **Push** view in **Team Explorer**, select hello **Publish Git Repo** button under **Push tooVisual Studio Team Services**.</span></span>

![推送 Git 儲存機制][push-git-repo]

<span data-ttu-id="13b91-143">請確認您的電子郵件，然後選取您的帳戶在 hello **Team Services 網域**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="13b91-143">Verify your email and select your account in hello **Team Services Domain** drop-down.</span></span> <span data-ttu-id="13b91-144">輸入您的儲存機制名稱，並選取 [發佈儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="13b91-144">Enter your repository name and select **Publish repository**.</span></span>

![推送 Git 儲存機制][publish-code]

<span data-ttu-id="13b91-146">發行 hello 儲存機制為 hello 本機儲存機制名稱相同的 hello 與您帳戶中建立新的 team 專案。</span><span class="sxs-lookup"><span data-stu-id="13b91-146">Publishing hello repo creates a new team project in your account with hello same name as hello local repo.</span></span> <span data-ttu-id="13b91-147">toocreate hello 儲存機制，在現有 team 專案中，按一下**進階**下一步太**儲存機制**命名，並選取 team 專案。</span><span class="sxs-lookup"><span data-stu-id="13b91-147">toocreate hello repo in an existing team project, click **Advanced** next too**Repository** name and select a team project.</span></span> <span data-ttu-id="13b91-148">您也可以選取 hello web 上檢視您的程式碼**hello web 上可以看到**。</span><span class="sxs-lookup"><span data-stu-id="13b91-148">You can view your code on hello web by selecting **See it on hello web**.</span></span>

## <a name="configure-continuous-delivery-with-vsts"></a><span data-ttu-id="13b91-149">設定 VSTS 的持續傳遞</span><span class="sxs-lookup"><span data-stu-id="13b91-149">Configure Continuous Delivery with VSTS</span></span>
<span data-ttu-id="13b91-150">Team Services 組建定義描述由一組循序執行的組建步驟所組成的工作流程。</span><span class="sxs-lookup"><span data-stu-id="13b91-150">A Team Services build definition describes a workflow that is composed of a set of build steps that are executed sequentially.</span></span> <span data-ttu-id="13b91-151">建立組建定義，會產生 Service Fabric 應用程式封裝時，其他的成品、 toodeploy tooa Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="13b91-151">Create a build definition that that produces a Service Fabric application package, and other artifacts, toodeploy tooa Service Fabric cluster.</span></span> <span data-ttu-id="13b91-152">深入了解 [Team Services 組建定義](https://www.visualstudio.com/docs/build/define/create)。</span><span class="sxs-lookup"><span data-stu-id="13b91-152">Learn more about [Team Services build definitions](https://www.visualstudio.com/docs/build/define/create).</span></span> 

<span data-ttu-id="13b91-153">Team Services 發行定義描述將部署應用程式封裝 tooa 叢集工作流程。</span><span class="sxs-lookup"><span data-stu-id="13b91-153">A Team Services release definition describes a workflow that deploys an application package tooa cluster.</span></span> <span data-ttu-id="13b91-154">Hello 一起使用時，組建定義，並發行定義執行開頭為與叢集中執行的應用程式的來源檔案 tooending hello 整個工作流程。</span><span class="sxs-lookup"><span data-stu-id="13b91-154">When used together, hello build definition and release definition execute hello entire workflow starting with source files tooending with a running application in your cluster.</span></span> <span data-ttu-id="13b91-155">深入了解 Team Services [發行定義](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)。</span><span class="sxs-lookup"><span data-stu-id="13b91-155">Learn more about Team Services [release definitions](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).</span></span>

### <a name="create-a-build-definition"></a><span data-ttu-id="13b91-156">建立組建定義</span><span class="sxs-lookup"><span data-stu-id="13b91-156">Create a build definition</span></span>
<span data-ttu-id="13b91-157">開啟網頁瀏覽器並瀏覽在 tooyour 新 team 專案： https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting。</span><span class="sxs-lookup"><span data-stu-id="13b91-157">Open a web browser and navigate tooyour new team project at: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting .</span></span> 

<span data-ttu-id="13b91-158">選取 hello**建置和發行**索引標籤，然後**建置**，然後**+ 新定義**。</span><span class="sxs-lookup"><span data-stu-id="13b91-158">Select hello **Build & Release** tab, then **Builds**, then **+ New definition**.</span></span>  <span data-ttu-id="13b91-159">在**選取範本**，選取 hello **Azure Service Fabric 應用程式**範本，然後按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="13b91-159">In **Select a template**, select hello **Azure Service Fabric Application** template and click **Apply**.</span></span> 

![選擇組建範本][select-build-template] 

<span data-ttu-id="13b91-161">hello 投票應用程式包含.NET Core 專案，因此加入還原 hello 相依性的工作。</span><span class="sxs-lookup"><span data-stu-id="13b91-161">hello voting application contains a .NET Core project, so add a task that restores hello dependencies.</span></span> <span data-ttu-id="13b91-162">在 hello**工作**檢視中，選取**+ 加入工作**在 hello 左下方。</span><span class="sxs-lookup"><span data-stu-id="13b91-162">In hello **Tasks** view, select **+ Add Task** in hello bottom left.</span></span> <span data-ttu-id="13b91-163">搜尋 「 命令列"toofind hello 命令列工作，然後按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="13b91-163">Search on "Command Line" toofind hello command-line task, then click **Add**.</span></span> 

![新增工作][add-task] 

<span data-ttu-id="13b91-165">在 hello 新工作中，「 執行 dotnet.exe 」 中輸入**顯示名稱**中的"dotnet.exe"**工具**，和 「 還原 」 中**引數**。</span><span class="sxs-lookup"><span data-stu-id="13b91-165">In hello new task, enter "Run dotnet.exe" in **Display name**, "dotnet.exe" in **Tool**, and "restore" in **Arguments**.</span></span> 

![新增工作][new-task] 

<span data-ttu-id="13b91-167">在 hello**觸發程序**檢視中，按一下 hello**啟用此觸發程序**下切換**連續整合**。</span><span class="sxs-lookup"><span data-stu-id="13b91-167">In hello **Triggers** view, click hello **Enable this trigger** switch under **Continuous Integration**.</span></span> 

<span data-ttu-id="13b91-168">選取**儲存，並佇列**並輸入"裝載 VS2017 」 為 hello**代理程式佇列**。</span><span class="sxs-lookup"><span data-stu-id="13b91-168">Select **Save & queue** and enter "Hosted VS2017" as hello **Agent queue**.</span></span> <span data-ttu-id="13b91-169">選取**佇列**toomanually 啟動組建。</span><span class="sxs-lookup"><span data-stu-id="13b91-169">Select **Queue** toomanually start a build.</span></span>  <span data-ttu-id="13b91-170">推送或簽入時也會觸發組建。</span><span class="sxs-lookup"><span data-stu-id="13b91-170">Builds also triggers upon push or check-in.</span></span>

<span data-ttu-id="13b91-171">toocheck 組建進度、 交換器 toohello**建置** 索引標籤。一旦您確認 hello 組建執行成功，定義來部署您的應用程式 tooa 叢集發行定義。</span><span class="sxs-lookup"><span data-stu-id="13b91-171">toocheck your build progress, switch toohello **Builds** tab.  Once you verify that hello build executes successfully, define a release definition that deploys your application tooa cluster.</span></span> 

### <a name="create-a-release-definition"></a><span data-ttu-id="13b91-172">建立發行定義</span><span class="sxs-lookup"><span data-stu-id="13b91-172">Create a release definition</span></span>  

<span data-ttu-id="13b91-173">選取 hello**建置和發行**索引標籤，然後**版本**，然後**+ 新定義**。</span><span class="sxs-lookup"><span data-stu-id="13b91-173">Select hello **Build & Release** tab, then **Releases**, then **+ New definition**.</span></span>  <span data-ttu-id="13b91-174">在**建立發行定義**，選取 hello **Azure Service Fabric 部署**範本從 hello 清單，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="13b91-174">In **Create release definition**, select hello **Azure Service Fabric Deployment** template from hello list and click **Next**.</span></span>  <span data-ttu-id="13b91-175">選取 hello**建置**來源，請檢查 hello**連續部署**方塊，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="13b91-175">Select hello **Build** source, check hello **Continuous deployment** box, and click **Create**.</span></span> 

<span data-ttu-id="13b91-176">在 hello**環境**檢視中，按一下**新增**toohello 右邊**叢集連線**。</span><span class="sxs-lookup"><span data-stu-id="13b91-176">In hello **Environments** view, click **Add** toohello right of **Cluster Connection**.</span></span>  <span data-ttu-id="13b91-177">指定 hello 叢集 」 mysftestcluster"，"tcp://mysftestcluster.westus.cloudapp.azure.com:19000 」，和 hello Azure Active Directory 或憑證認證的叢集端點的連接名稱。</span><span class="sxs-lookup"><span data-stu-id="13b91-177">Specify a connection name of "mysftestcluster", a cluster endpoint of "tcp://mysftestcluster.westus.cloudapp.azure.com:19000", and hello Azure Active Directory or certificate credentials for hello cluster.</span></span> <span data-ttu-id="13b91-178">對於 Azure Active Directory 認證，請定義您想要在 hello toouse tooconnect toohello 叢集 hello 認證**Username**和**密碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="13b91-178">For Azure Active Directory credentials, define hello credentials you want toouse tooconnect toohello cluster in hello **Username** and **Password** fields.</span></span> <span data-ttu-id="13b91-179">以憑證為基礎的驗證，定義 hello Base64 編碼的 hello 用戶端憑證檔案，在 hello**用戶端憑證**欄位。</span><span class="sxs-lookup"><span data-stu-id="13b91-179">For certificate-based authentication, define hello Base64 encoding of hello client certificate file in hello **Client Certificate** field.</span></span>  <span data-ttu-id="13b91-180">請參閱 hello 說明快顯視窗，該欄位有關的資訊 tooget 該值。</span><span class="sxs-lookup"><span data-stu-id="13b91-180">See hello help pop-up on that field for info on how tooget that value.</span></span>  <span data-ttu-id="13b91-181">如果您的憑證是否受密碼保護，定義 hello 密碼 hello**密碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="13b91-181">If your certificate is password-protected, define hello password in hello **Password** field.</span></span>  <span data-ttu-id="13b91-182">按一下**儲存**toosave hello 發行定義。</span><span class="sxs-lookup"><span data-stu-id="13b91-182">Click **Save** toosave hello release definition.</span></span>

![新增叢集連線][add-cluster-connection] 

<span data-ttu-id="13b91-184">按一下 [在代理程式上執行]，然後針對 [部署佇列] 選取 [Hosted VS2017]。</span><span class="sxs-lookup"><span data-stu-id="13b91-184">Click **Run on agent**, then select **Hosted VS2017** for **Deployment queue**.</span></span> <span data-ttu-id="13b91-185">按一下**儲存**toosave hello 發行定義。</span><span class="sxs-lookup"><span data-stu-id="13b91-185">Click **Save** toosave hello release definition.</span></span>

![在代理程式上執行][run-on-agent]

<span data-ttu-id="13b91-187">選取**+ 釋放** -> **建立發行** -> **建立**toomanually 建立發行。</span><span class="sxs-lookup"><span data-stu-id="13b91-187">Select **+Release** -> **Create Release** -> **Create** toomanually create a release.</span></span>  <span data-ttu-id="13b91-188">請確認已成功將 hello 部署 hello 應用程式正在執行 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="13b91-188">Verify that hello deployment succeeded and hello application is running in hello cluster.</span></span>  <span data-ttu-id="13b91-189">開啟網頁瀏覽器並瀏覽過[http://mysftestcluster.westus.cloudapp.azure.com:19080/總管/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/)。</span><span class="sxs-lookup"><span data-stu-id="13b91-189">Open a web browser and navigate too[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="13b91-190">請注意此範例中是"1.0.0.20170616.3 」 中的 hello 應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="13b91-190">Note hello application version, in this example it is "1.0.0.20170616.3".</span></span> 

## <a name="commit-and-push-changes-trigger-a-release"></a><span data-ttu-id="13b91-191">認可並推送變更，觸發發行程序</span><span class="sxs-lookup"><span data-stu-id="13b91-191">Commit and push changes, trigger a release</span></span>
<span data-ttu-id="13b91-192">hello 連續整合管線的 tooverify 正在運作的一些程式碼將變更簽入 tooTeam 服務。</span><span class="sxs-lookup"><span data-stu-id="13b91-192">tooverify that hello continuous integration pipeline is functioning by checking in some code changes tooTeam Services.</span></span>    

<span data-ttu-id="13b91-193">您撰寫程式碼時，Visual Studio 會自動追蹤您的變更。</span><span class="sxs-lookup"><span data-stu-id="13b91-193">As you write your code, your changes are automatically tracked by Visual Studio.</span></span> <span data-ttu-id="13b91-194">認可變更 tooyour 本機 Git 儲存機制，藉由選取 hello 暫止的變更圖示 （</span><span class="sxs-lookup"><span data-stu-id="13b91-194">Commit changes tooyour local Git repository by selecting hello pending changes icon (</span></span>![Pending][pending]<span data-ttu-id="13b91-196">) 從在 hello 右下方的 hello 狀態列。</span><span class="sxs-lookup"><span data-stu-id="13b91-196">) from hello status bar in hello bottom right.</span></span>

<span data-ttu-id="13b91-197">在 hello**變更**檢視在 Team Explorer 中，加入描述您的更新的訊息和認可您的變更。</span><span class="sxs-lookup"><span data-stu-id="13b91-197">On hello **Changes** view in Team Explorer, add a message describing your update and commit your changes.</span></span>

![全部認可][changes]

<span data-ttu-id="13b91-199">選取 hello 未發行的變更狀態列圖示 (![未發行的變更][unpublished-changes]) 或 hello Team 總管 中的同步處理檢視。</span><span class="sxs-lookup"><span data-stu-id="13b91-199">Select hello unpublished changes status bar icon (![Unpublished changes][unpublished-changes]) or hello Sync view in Team Explorer.</span></span> <span data-ttu-id="13b91-200">選取**推送**tooupdate Team Services/TFS 中程式碼。</span><span class="sxs-lookup"><span data-stu-id="13b91-200">Select **Push** tooupdate your code in Team Services/TFS.</span></span>

![推送變更][push]

<span data-ttu-id="13b91-202">推送 hello 變更 tooTeam 服務會自動觸發程序建置。</span><span class="sxs-lookup"><span data-stu-id="13b91-202">Pushing hello changes tooTeam Services automatically triggers a build.</span></span>  <span data-ttu-id="13b91-203">Hello 組建定義已成功完成時，發行就會自動建立，並開始升級 hello hello 叢集上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="13b91-203">When hello build definition successfully completes, a release is automatically created and starts upgrading hello application on hello cluster.</span></span>

<span data-ttu-id="13b91-204">toocheck 組建進度、 交換器 toohello**建置**索引標籤中**Team Explorer** Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="13b91-204">toocheck your build progress, switch toohello **Builds** tab in **Team Explorer** in Visual Studio.</span></span>  <span data-ttu-id="13b91-205">一旦您確認 hello 組建執行成功，定義來部署您的應用程式 tooa 叢集發行定義。</span><span class="sxs-lookup"><span data-stu-id="13b91-205">Once you verify that hello build executes successfully, define a release definition that deploys your application tooa cluster.</span></span>

<span data-ttu-id="13b91-206">請確認已成功將 hello 部署 hello 應用程式正在執行 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="13b91-206">Verify that hello deployment succeeded and hello application is running in hello cluster.</span></span>  <span data-ttu-id="13b91-207">開啟網頁瀏覽器並瀏覽過[http://mysftestcluster.westus.cloudapp.azure.com:19080/總管/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/)。</span><span class="sxs-lookup"><span data-stu-id="13b91-207">Open a web browser and navigate too[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="13b91-208">請注意此範例中是"1.0.0.20170815.3 」 中的 hello 應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="13b91-208">Note hello application version, in this example it is "1.0.0.20170815.3".</span></span>

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a><span data-ttu-id="13b91-210">更新 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="13b91-210">Update hello application</span></span>
<span data-ttu-id="13b91-211">在 hello 應用程式進行程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="13b91-211">Make code changes in hello application.</span></span>  <span data-ttu-id="13b91-212">儲存並認可 hello 變更，hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="13b91-212">Save and commit hello changes, following hello previous steps.</span></span>

<span data-ttu-id="13b91-213">一旦 hello 升級的 hello 應用程式開始，您可以觀看 hello Service Fabric 總管中的升級進度：</span><span class="sxs-lookup"><span data-stu-id="13b91-213">Once hello upgrade of hello application begins, you can watch hello upgrade progress in Service Fabric Explorer:</span></span>

![Service Fabric Explorer][sfx2]

<span data-ttu-id="13b91-215">hello 應用程式升級可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="13b91-215">hello application upgrade may take several minutes.</span></span> <span data-ttu-id="13b91-216">Hello 升級完成後，hello 應用程式將會執行下一版的 hello。</span><span class="sxs-lookup"><span data-stu-id="13b91-216">When hello upgrade is complete, hello application will be running hello next version.</span></span>  <span data-ttu-id="13b91-217">在此範例中為 "1.0.0.20170815.4"。</span><span class="sxs-lookup"><span data-stu-id="13b91-217">In this example "1.0.0.20170815.4".</span></span>

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a><span data-ttu-id="13b91-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13b91-219">Next steps</span></span>
<span data-ttu-id="13b91-220">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="13b91-220">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="13b91-221">加入原始檔控制 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="13b91-221">Add source control tooyour project</span></span>
> * <span data-ttu-id="13b91-222">建立組建定義</span><span class="sxs-lookup"><span data-stu-id="13b91-222">Create a build definition</span></span>
> * <span data-ttu-id="13b91-223">建立發行定義</span><span class="sxs-lookup"><span data-stu-id="13b91-223">Create a release definition</span></span>
> * <span data-ttu-id="13b91-224">自動部署和升級應用程式</span><span class="sxs-lookup"><span data-stu-id="13b91-224">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="13b91-225">既然您已部署應用程式，並設定連續整合，請嘗試下列 hello:</span><span class="sxs-lookup"><span data-stu-id="13b91-225">Now that you have deployed an application and configured continuous integration, try hello following:</span></span>
- [<span data-ttu-id="13b91-226">升級應用程式</span><span class="sxs-lookup"><span data-stu-id="13b91-226">Upgrade an app</span></span>](service-fabric-application-upgrade.md)
- [<span data-ttu-id="13b91-227">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="13b91-227">Test an app</span></span>](service-fabric-testability-overview.md) 
- [<span data-ttu-id="13b91-228">監視與診斷</span><span class="sxs-lookup"><span data-stu-id="13b91-228">Monitor and diagnose</span></span>](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png