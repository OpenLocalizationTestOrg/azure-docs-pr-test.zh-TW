---
title: "aaaDeploy 您的應用程式 tooAzure 和 Azure 堆疊 |Microsoft 文件"
description: "了解 toodeploy 應用程式 tooAzure 和 Azure 的混合式 CI/CD 堆疊的管線。"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: a468d7da6f34d04809ee98463a8c4146da581015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-apps-tooazure-and-azure-stack"></a><span data-ttu-id="d94a7-103">部署應用程式 tooAzure 和 Azure 堆疊</span><span class="sxs-lookup"><span data-stu-id="d94a7-103">Deploy apps tooAzure and Azure Stack</span></span>
<span data-ttu-id="d94a7-104">在混合式[連續整合](https://www.visualstudio.com/learn/what-is-continuous-integration/)/[持續傳遞](https://www.visualstudio.com/learn/what-is-continuous-delivery/)(CI/CD) 管線可讓您 toobuild、 測試及部署您的應用程式 toomultiple 雲端。</span><span class="sxs-lookup"><span data-stu-id="d94a7-104">A hybrid [continuous integration](https://www.visualstudio.com/learn/what-is-continuous-integration/)/[continuous delivery](https://www.visualstudio.com/learn/what-is-continuous-delivery/)(CI/CD) pipeline enables you toobuild, test, and deploy your app toomultiple clouds.</span></span>  <span data-ttu-id="d94a7-105">在本教學課程中，您會建立範例環境 toolearn 混合式 CI/CD 管線可以幫助您：</span><span class="sxs-lookup"><span data-stu-id="d94a7-105">In this tutorial, you build a sample environment toolearn how a hybrid CI/CD pipeline can help you:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="d94a7-106">啟始程式碼認可 tooyour Visual Studio Team Services (VSTS) 儲存機制為基礎的新組建。</span><span class="sxs-lookup"><span data-stu-id="d94a7-106">Initiate a new build based on code commits tooyour Visual Studio Team Services (VSTS) repository.</span></span>
> * <span data-ttu-id="d94a7-107">使用者接受度測試您新建立的程式碼 tooAzure 來自動部署。</span><span class="sxs-lookup"><span data-stu-id="d94a7-107">Automatically deploy your newly built code tooAzure for user acceptance testing.</span></span>
> * <span data-ttu-id="d94a7-108">一旦您的程式碼已通過測試，來自動部署 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d94a7-108">Once your code has passed testing, automatically deploy tooAzure Stack.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="d94a7-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d94a7-109">Prerequisites</span></span>
<span data-ttu-id="d94a7-110">幾個元件需要的 toobuild 混合式 CI/CD 管線，可能需要一些時間 tooprepare。</span><span class="sxs-lookup"><span data-stu-id="d94a7-110">A few components are required toobuild a hybrid CI/CD pipeline, and may take some time tooprepare.</span></span>  <span data-ttu-id="d94a7-111">如果您已經有其中某些元件，請確定它們符合 hello 需求，在開始之前。</span><span class="sxs-lookup"><span data-stu-id="d94a7-111">If you already have some of these components, make sure they meet hello requirements before beginning.</span></span>

<span data-ttu-id="d94a7-112">本主題也假設您擁有 Azure 和 Azure Stack 的部分知識。</span><span class="sxs-lookup"><span data-stu-id="d94a7-112">This topic also assumes that you have some knowledge of Azure and Azure Stack.</span></span> <span data-ttu-id="d94a7-113">如果您想再繼續進行更多的 toolearn，是確定 toostart 使用這些主題：</span><span class="sxs-lookup"><span data-stu-id="d94a7-113">If you want toolearn more before proceeding, be sure toostart with these topics:</span></span>

- [<span data-ttu-id="d94a7-114">簡介 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d94a7-114">Introduction tooAzure</span></span>](https://docs.microsoft.com/azure/fundamentals-introduction-to-azure)
- [<span data-ttu-id="d94a7-115">Azure Stack 重要概念</span><span class="sxs-lookup"><span data-stu-id="d94a7-115">Azure Stack Key Concepts</span></span>](azure-stack-key-features.md)

### <a name="azure"></a><span data-ttu-id="d94a7-116">Azure</span><span class="sxs-lookup"><span data-stu-id="d94a7-116">Azure</span></span>
 - <span data-ttu-id="d94a7-117">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="d94a7-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
 - <span data-ttu-id="d94a7-118">建立 [Web 應用程式](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)，並將其設定為用於 [FTP 發行](../app-service-web/app-service-deploy-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="d94a7-118">Create a [Web App](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md), and configure it for [FTP publishing](../app-service-web/app-service-deploy-ftp.md).</span></span>  <span data-ttu-id="d94a7-119">請記下 hello 新的 Web 應用程式 URL，因為它正稍後使用。</span><span class="sxs-lookup"><span data-stu-id="d94a7-119">Make note of hello new Web App URL, as it is used later.</span></span>


### <a name="azure-stack"></a><span data-ttu-id="d94a7-120">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d94a7-120">Azure Stack</span></span>
 - <span data-ttu-id="d94a7-121">[部署 Azure Stack](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="d94a7-121">[Deploy Azure Stack](azure-stack-run-powershell-script.md).</span></span>  <span data-ttu-id="d94a7-122">hello 安裝程序通常需要幾小時 toocomplete，因此據此計畫。</span><span class="sxs-lookup"><span data-stu-id="d94a7-122">hello installation usually takes a few hours toocomplete, so plan accordingly.</span></span>
 - <span data-ttu-id="d94a7-123">部署[App Service](azure-stack-app-service-deploy.md) PaaS 服務 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d94a7-123">Deploy [App Service](azure-stack-app-service-deploy.md) PaaS services tooAzure Stack.</span></span>
 - <span data-ttu-id="d94a7-124">建立 Web 應用程式，並將其設定為用於 [FTP 發行](azure-stack-app-service-enable-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="d94a7-124">Create a Web App and configure it for [FTP publishing](azure-stack-app-service-enable-ftp.md).</span></span>  <span data-ttu-id="d94a7-125">請記下 hello 新的 Web 應用程式 URL，因為它正稍後使用。</span><span class="sxs-lookup"><span data-stu-id="d94a7-125">Make note of hello new Web App URL, as it is used later.</span></span>  

### <a name="developer-tools"></a><span data-ttu-id="d94a7-126">開發人員工具</span><span class="sxs-lookup"><span data-stu-id="d94a7-126">Developer tools</span></span>
 - <span data-ttu-id="d94a7-127">建立 [VSTS 工作區](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)。</span><span class="sxs-lookup"><span data-stu-id="d94a7-127">Create a [VSTS workspace](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span></span>  <span data-ttu-id="d94a7-128">hello 註冊程序會建立專案，名為"MyFirstProject。 」</span><span class="sxs-lookup"><span data-stu-id="d94a7-128">hello sign-up process creates a project named "MyFirstProject."</span></span>  
 - <span data-ttu-id="d94a7-129">[安裝 Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio)和[tooVSTS 登入](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#connect-and-share-code-from-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="d94a7-129">[Install Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio) and [sign-in tooVSTS](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#connect-and-share-code-from-visual-studio)</span></span>
 - <span data-ttu-id="d94a7-130">Toohello 專案連接和[在本機複製](https://www.visualstudio.com/docs/git/gitquickstart)。</span><span class="sxs-lookup"><span data-stu-id="d94a7-130">Connect toohello project and [clone locally](https://www.visualstudio.com/docs/git/gitquickstart).</span></span>
 - <span data-ttu-id="d94a7-131">在 VSTS 中建立[代理程式集區](https://www.visualstudio.com/docs/build/concepts/agents/pools-queues#creating-agent-pools-and-queues)。</span><span class="sxs-lookup"><span data-stu-id="d94a7-131">Create an [agent pool](https://www.visualstudio.com/docs/build/concepts/agents/pools-queues#creating-agent-pools-and-queues) in VSTS.</span></span>
 - <span data-ttu-id="d94a7-132">安裝 Visual Studio 和部署[VSTS 組建代理程式](https://www.visualstudio.com/docs/build/actions/agents/v2-windows)tooa Azure 堆疊上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d94a7-132">Install Visual Studio and deploy a [VSTS build agent](https://www.visualstudio.com/docs/build/actions/agents/v2-windows) tooa virtual machine on Azure Stack.</span></span> 
 

## <a name="create-app--push-toovsts"></a><span data-ttu-id="d94a7-133">建立應用程式與推入 tooVSTS</span><span class="sxs-lookup"><span data-stu-id="d94a7-133">Create app & push tooVSTS</span></span>

### <a name="create-application"></a><span data-ttu-id="d94a7-134">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="d94a7-134">Create application</span></span>
<span data-ttu-id="d94a7-135">在本節中，您會建立簡單的 ASP.NET 應用程式，並將它推送 tooVSTS。</span><span class="sxs-lookup"><span data-stu-id="d94a7-135">In this section, you create a simple ASP.NET application and push it tooVSTS.</span></span>  <span data-ttu-id="d94a7-136">這些步驟代表 hello 一般開發人員的工作流程，而無法調整為開發人員工具和語言。</span><span class="sxs-lookup"><span data-stu-id="d94a7-136">These steps represent hello normal developer workflow, and could be adapted for developer tools and languages.</span></span> 

1.  <span data-ttu-id="d94a7-137">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d94a7-137">Open Visual Studio.</span></span>
2.  <span data-ttu-id="d94a7-138">從 Team Explorer 空間 hello 和**方案...**區域中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-138">From hello Team Explorer space and **Solutions...** area, click **New**.</span></span>
3.  <span data-ttu-id="d94a7-139">選取 [Visual C#]  >  [Web]  >  [ASP.NET Web 應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="d94a7-139">Select **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
4.  <span data-ttu-id="d94a7-140">提供 hello 應用程式的名稱，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-140">Provide a name for hello application and click **OK**.</span></span>
5.  <span data-ttu-id="d94a7-141">在 hello 下一個畫面上，保留 hello 預設 (Web form)，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-141">On hello next screen, keep hello defaults (Web forms) and click **OK**.</span></span>

### <a name="commit-and-push-changes-toovsts"></a><span data-ttu-id="d94a7-142">認可並推送變更 tooVSTS</span><span class="sxs-lookup"><span data-stu-id="d94a7-142">Commit and push changes tooVSTS</span></span>
1.  <span data-ttu-id="d94a7-143">使用 Team Explorer，在 Visual Studio 中，選取 [hello] 下拉式清單，然後按一下**變更**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-143">Using Team Explorer in Visual Studio, select hello dropdown and click **Changes**.</span></span>
2.  <span data-ttu-id="d94a7-144">提供認可訊息，然後選取 [全部認可]。</span><span class="sxs-lookup"><span data-stu-id="d94a7-144">Provide a commit message and select **Commit all**.</span></span> <span data-ttu-id="d94a7-145">您可能會提示的 toosave hello 方案檔，請按一下 [是] toosave 所有。</span><span class="sxs-lookup"><span data-stu-id="d94a7-145">You may be prompted toosave hello solution file, click yes toosave all.</span></span>
3.  <span data-ttu-id="d94a7-146">經過認可之後，Visual Studio 會詢問 toosync 變更 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="d94a7-146">Once committed, Visual Studio offers toosync changes tooyour project.</span></span> <span data-ttu-id="d94a7-147">選取 [同步]。</span><span class="sxs-lookup"><span data-stu-id="d94a7-147">Select **Sync**.</span></span>

    ![映像顯示 hello 認可螢幕完成認可](./media/azure-stack-solution-pipeline/image1.png)

4.  <span data-ttu-id="d94a7-149">在 hello 同步處理 索引標籤下*連出*，您會看到您新的認可。</span><span class="sxs-lookup"><span data-stu-id="d94a7-149">In hello synchronization tab, under *Outgoing*, you see your new commit.</span></span>  <span data-ttu-id="d94a7-150">選取**推送**toosynchronize hello 變更 tooVSTS。</span><span class="sxs-lookup"><span data-stu-id="d94a7-150">Select **Push** toosynchronize hello change tooVSTS.</span></span>

    ![顯示同步步驟的影像](./media/azure-stack-solution-pipeline/image2.png)

### <a name="review-code-in-vsts"></a><span data-ttu-id="d94a7-152">檢閱 VSTS 中的程式碼</span><span class="sxs-lookup"><span data-stu-id="d94a7-152">Review code in VSTS</span></span>
<span data-ttu-id="d94a7-153">您一次認可變更並推送 tooVSTS，檢查您的程式碼從 hello VSTS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d94a7-153">Once you've committed a change and pushed tooVSTS, check your code from hello VSTS portal.</span></span>  <span data-ttu-id="d94a7-154">選取**程式碼**，然後**檔案**hello 下拉式功能表中。</span><span class="sxs-lookup"><span data-stu-id="d94a7-154">Select **Code**, and then **Files** from hello dropdown menu.</span></span>  <span data-ttu-id="d94a7-155">您可以看到您所建立的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="d94a7-155">You can see hello solution you created.</span></span>

## <a name="create-build-definition"></a><span data-ttu-id="d94a7-156">建立組建定義</span><span class="sxs-lookup"><span data-stu-id="d94a7-156">Create build definition</span></span>
<span data-ttu-id="d94a7-157">hello 建置程序會定義您的應用程式如何建置和封裝部署在每個認可的程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="d94a7-157">hello build process defines how your application is built and packaged for deployment on each commit of code changes.</span></span> <span data-ttu-id="d94a7-158">在本例中，我們使用 hello 包含範本 tooconfigure hello 建置流程的 ASP.NET 應用程式中，雖然這個組態可能是適用於根據您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d94a7-158">In our example, we use hello included template tooconfigure hello build process for an ASP.NET app, though this configuration could be adapted depending on your application.</span></span>

1.  <span data-ttu-id="d94a7-159">登入 tooyour VSTS 工作區，從網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d94a7-159">Sign in tooyour VSTS workspace from a web browser.</span></span>
2.  <span data-ttu-id="d94a7-160">從 hello 的橫幅中，選取**建置和發行**然後**建置**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-160">From hello banner, select **Build & Release**  and then **Builds**.</span></span>
3.  <span data-ttu-id="d94a7-161">選取 [+新增定義]。</span><span class="sxs-lookup"><span data-stu-id="d94a7-161">Click **+ New definition**.</span></span>
4.  <span data-ttu-id="d94a7-162">從範本 hello 清單，選取**ASP.NET （預覽）**選取**套用**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-162">From hello list of templates, select **ASP.NET (Preview)** and select **Apply**.</span></span>
5.  <span data-ttu-id="d94a7-163">修改 hello *MSBuild 引數*欄位*建置方案*逐步執行至：</span><span class="sxs-lookup"><span data-stu-id="d94a7-163">Modify hello *MSBuild Arguments* field in *Build Solution* step to:</span></span>

    `/p:DeployOnBuild=True /p:WebPublishMethod=FileSystem /p:DeployDefaultTarget=WebPublish /p:publishUrl="$(build.artifactstagingdirectory)\\"`

6.  <span data-ttu-id="d94a7-164">選取 hello**選項**索引標籤，然後選取 hello 代理程式佇列 hello 組建代理程式的設定，您部署 tooa 虛擬機器 Azure 堆疊上。</span><span class="sxs-lookup"><span data-stu-id="d94a7-164">Select hello **Options** tab, and select hello agent queue for hello build agent you deployed tooa virtual machine on Azure Stack.</span></span> 
7.  <span data-ttu-id="d94a7-165">選取 hello**觸發程序**索引標籤，然後啟用**連續整合**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-165">Select hello **Triggers** tab, and enable **Continuous Integration**.</span></span>
7.  <span data-ttu-id="d94a7-166">按一下**儲存，並佇列**，然後選取 **儲存**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="d94a7-166">Click **Save & queue** and then select **Save** from hello dropdown.</span></span> 

## <a name="create-release-definition"></a><span data-ttu-id="d94a7-167">建立發行定義</span><span class="sxs-lookup"><span data-stu-id="d94a7-167">Create release definition</span></span>
<span data-ttu-id="d94a7-168">hello 發行程序定義如何從 hello 上一個步驟的組建部署的 tooan 環境。</span><span class="sxs-lookup"><span data-stu-id="d94a7-168">hello release process defines how builds from hello previous step are deployed tooan environment.</span></span>  <span data-ttu-id="d94a7-169">在本教學課程中，我們發行我們與 FTP tooan Azure Web 應用程式的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d94a7-169">In this tutorial, we publish our ASP.NET app with FTP tooan Azure Web App.</span></span> <span data-ttu-id="d94a7-170">tooconfigure 發行 tooAzure，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d94a7-170">tooconfigure a release tooAzure, use hello following steps:</span></span>

1.  <span data-ttu-id="d94a7-171">從 hello VSTS 橫幅中，選取**建置和發行**然後**版本**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-171">From hello VSTS banner, select **Build & Release**  and then **Releases**.</span></span>
2.  <span data-ttu-id="d94a7-172">按一下綠色的 hello **+ 新定義**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-172">Click hello green **+ New definition**.</span></span>
3.  <span data-ttu-id="d94a7-173">選取 [空白] ，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d94a7-173">Select **Empty** and click **Next**.</span></span>
4.  <span data-ttu-id="d94a7-174">核取方塊 hello*連續部署*，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-174">Check hello box for *Continuous deployment*, and then click **Create**.</span></span>

<span data-ttu-id="d94a7-175">現在，您已建立空白的發行定義，並繫結它 toohello 組建，我們將新增 hello Azure 環境的步驟：</span><span class="sxs-lookup"><span data-stu-id="d94a7-175">Now that you've created an empty release definition and tied it toohello build, we add steps for hello Azure environment:</span></span>

1.  <span data-ttu-id="d94a7-176">按一下綠色的 hello  **+**  tooadd 工作。</span><span class="sxs-lookup"><span data-stu-id="d94a7-176">Click hello green **+** tooadd tasks.</span></span>
2.  <span data-ttu-id="d94a7-177">選取**所有**，然後從 [hello] 清單中，加入**FTP 上傳**選取**關閉**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-177">Select **All**, and then from hello list, add **FTP Upload** and select **Close**.</span></span>
3.  <span data-ttu-id="d94a7-178">選取 hello **FTP 上傳**您剛才加入的工作，並設定下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="d94a7-178">Select hello **FTP Upload** task you just added, and configure hello following parameters:</span></span>
    
    | <span data-ttu-id="d94a7-179">參數</span><span class="sxs-lookup"><span data-stu-id="d94a7-179">Parameter</span></span> | <span data-ttu-id="d94a7-180">值</span><span class="sxs-lookup"><span data-stu-id="d94a7-180">Value</span></span> |
    | ----- | ----- |
    |<span data-ttu-id="d94a7-181">驗證方法</span><span class="sxs-lookup"><span data-stu-id="d94a7-181">Authentication Method</span></span>| <span data-ttu-id="d94a7-182">輸入認證</span><span class="sxs-lookup"><span data-stu-id="d94a7-182">Enter Credentials</span></span>|
    |<span data-ttu-id="d94a7-183">伺服器 URL</span><span class="sxs-lookup"><span data-stu-id="d94a7-183">Server URL</span></span> | <span data-ttu-id="d94a7-184">從 Azure 入口網站取出 Web 應用程式 FTP URL</span><span class="sxs-lookup"><span data-stu-id="d94a7-184">Web App FTP URL retrieved from Azure portal</span></span> |
    |<span data-ttu-id="d94a7-185">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d94a7-185">Username</span></span> | <span data-ttu-id="d94a7-186">建立 Web 應用程式的 FTP 認證時所設定的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d94a7-186">Username you configured when creating FTP Credentials for Web App</span></span> |
    |<span data-ttu-id="d94a7-187">密碼</span><span class="sxs-lookup"><span data-stu-id="d94a7-187">Password</span></span> | <span data-ttu-id="d94a7-188">建立 Web 應用程式的 FTP 認證時所建立的密碼</span><span class="sxs-lookup"><span data-stu-id="d94a7-188">Password you created when establishing FTP credentials for Web App</span></span>|
    |<span data-ttu-id="d94a7-189">來源目錄</span><span class="sxs-lookup"><span data-stu-id="d94a7-189">Source Directory</span></span> | <span data-ttu-id="d94a7-190">$(System.DefaultWorkingDirectory)\**\\</span><span class="sxs-lookup"><span data-stu-id="d94a7-190">$(System.DefaultWorkingDirectory)\**\\</span></span> |
    |<span data-ttu-id="d94a7-191">遠端目錄</span><span class="sxs-lookup"><span data-stu-id="d94a7-191">Remote Directory</span></span> | <span data-ttu-id="d94a7-192">/site/wwwroot/</span><span class="sxs-lookup"><span data-stu-id="d94a7-192">/site/wwwroot/</span></span> |
    |<span data-ttu-id="d94a7-193">保留檔案路徑</span><span class="sxs-lookup"><span data-stu-id="d94a7-193">Preserve file paths</span></span> | <span data-ttu-id="d94a7-194">已啟用 (已勾選)</span><span class="sxs-lookup"><span data-stu-id="d94a7-194">Enabled (checked)</span></span>|

4.  <span data-ttu-id="d94a7-195">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="d94a7-195">Click **Save**</span></span>

<span data-ttu-id="d94a7-196">最後，您可以設定 hello 發行定義 toouse hello 代理程式集區包含 hello 代理程式部署使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d94a7-196">Finally, you configure hello release definition toouse hello agent pool containing hello agent deployed using hello following steps:</span></span>
1.  <span data-ttu-id="d94a7-197">選取 hello 發行定義，然後按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-197">Select hello release definition and click **Edit**.</span></span>
2.  <span data-ttu-id="d94a7-198">選取**代理程式上執行**從 hello 中間的資料行。</span><span class="sxs-lookup"><span data-stu-id="d94a7-198">Select **Run on agent** from hello middle column.</span></span>  <span data-ttu-id="d94a7-199">Hello 右邊資料行中，選取 hello 代理程式的佇列包含 hello Azure 堆疊上執行的組建代理程式。</span><span class="sxs-lookup"><span data-stu-id="d94a7-199">In hello right column, select hello agent queue containing hello build agent running on Azure Stack.</span></span>  
    <span data-ttu-id="d94a7-200">![映像顯示設定的發行定義 toouse 特定佇列](./media/azure-stack-solution-pipeline/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d94a7-200">![image showing configuration of release definition toouse specific queue](./media/azure-stack-solution-pipeline/image3.png)</span></span>


## <a name="deploy-your-app-tooazure"></a><span data-ttu-id="d94a7-201">部署應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d94a7-201">Deploy your app tooAzure</span></span>
<span data-ttu-id="d94a7-202">這個步驟會在 Azure 上使用您新建立的 CI/CD 管線 toodeploy hello ASP.NET 應用程式 tooa Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d94a7-202">This step uses your newly built CI/CD pipeline toodeploy hello ASP.NET app tooa Web App on Azure.</span></span> 

1.  <span data-ttu-id="d94a7-203">從 VSTS 中的 hello 橫幅中，選取**建置和發行**，然後選取**建置**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-203">From hello banner in VSTS, select **Build & Release**, and then select **Builds**.</span></span>
2.  <span data-ttu-id="d94a7-204">按一下**...** hello 上建置先前建立的定義，然後選取**新組建排入佇列**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-204">Click **...** on hello build definition previously created, and select **Queue new build**.</span></span>
3.  <span data-ttu-id="d94a7-205">接受 hello 預設值，並按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-205">Accept hello defaults and click **Ok**.</span></span>  <span data-ttu-id="d94a7-206">hello 組建開始，並顯示進度。</span><span class="sxs-lookup"><span data-stu-id="d94a7-206">hello build begins and displays progress.</span></span>
4.  <span data-ttu-id="d94a7-207">Hello 建置完成之後，您可以藉由選取追蹤 hello 狀態**建置和發行**，然後選取**版本**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-207">Once hello build is complete, you can track hello status by selecting **Build & Release** and selecting **Releases**.</span></span>
5.  <span data-ttu-id="d94a7-208">Hello 建置完成之後，請瀏覽 hello 網站使用 hello 時會建立 hello Web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="d94a7-208">After hello build is complete, visit hello website using hello URL noted when creating hello Web App.</span></span>    


## <a name="add-azure-stack-toopipeline"></a><span data-ttu-id="d94a7-209">新增 Azure 堆疊 toopipeline</span><span class="sxs-lookup"><span data-stu-id="d94a7-209">Add Azure Stack toopipeline</span></span>
<span data-ttu-id="d94a7-210">現在，您藉由部署 tooAzure 測試 CI/CD 管線，它會是時間 tooadd Azure 堆疊 toohello 管線。</span><span class="sxs-lookup"><span data-stu-id="d94a7-210">Now that you've tested your CI/CD pipeline by deploying tooAzure, it's time tooadd Azure Stack toohello pipeline.</span></span>  <span data-ttu-id="d94a7-211">在 hello 下列步驟，您可以建立新的環境，並加入 FTP 上傳工作 toodeploy 您應用程式 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d94a7-211">In hello following steps, you create a new environment and add an FTP Upload task toodeploy your app tooAzure Stack.</span></span>  <span data-ttu-id="d94a7-212">您也會加入做為 「 簽署 」 的程式碼發行 tooAzure 堆疊方式 toosimulate 版本位核准者。</span><span class="sxs-lookup"><span data-stu-id="d94a7-212">You also add a release approver, which serves as a way toosimulate "signing off" on a code release tooAzure Stack.</span></span>  

1.  <span data-ttu-id="d94a7-213">在 hello 發行定義中，選取  **+ 加入環境**和**建立新環境**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-213">In hello Release definition, select **+ Add Environment** and **Create new environment**.</span></span>
2.  <span data-ttu-id="d94a7-214">選取 [空白] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d94a7-214">Select **Empty**, click **Next**.</span></span>
3.  <span data-ttu-id="d94a7-215">選取 [特定使用者] 並指定您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d94a7-215">Select **Specific users** and specify your account.</span></span>  <span data-ttu-id="d94a7-216">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="d94a7-216">Select **Create**.</span></span>
4.  <span data-ttu-id="d94a7-217">重新命名選取的 hello 環境 hello 現有名稱，然後輸入*Azure 堆疊*。</span><span class="sxs-lookup"><span data-stu-id="d94a7-217">Rename hello environment by selecting hello existing name and typing *Azure Stack*.</span></span>
5.  <span data-ttu-id="d94a7-218">現在，hello Azure 堆疊環境中，選取項目，然後選取 **新增工作**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-218">Now, selection hello Azure Stack environment, then select **Add tasks**.</span></span>
6.  <span data-ttu-id="d94a7-219">選取 hello **FTP 上傳**工作，並選取**新增**，然後選取**關閉**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-219">Select hello **FTP Upload** task and select **Add**, then select **Close**.</span></span>


### <a name="configure-ftp-task"></a><span data-ttu-id="d94a7-220">設定 FTP 工作</span><span class="sxs-lookup"><span data-stu-id="d94a7-220">Configure FTP task</span></span>
<span data-ttu-id="d94a7-221">既然您已建立版本，您需要設定 hello 發行 toohello Azure 堆疊上的 Web 應用程式所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="d94a7-221">Now that you've created a release, you'll configure hello steps required for publishing toohello Web App on Azure Stack.</span></span>  <span data-ttu-id="d94a7-222">就像您為 Azure 設定 hello FTP 上傳工作，您會設定為 Azure 堆疊 hello 工作：</span><span class="sxs-lookup"><span data-stu-id="d94a7-222">Just like you configured hello FTP Upload task for Azure, you configure hello task for Azure Stack:</span></span>

1.  <span data-ttu-id="d94a7-223">選取 hello **FTP 上傳**您剛才加入的工作，並設定下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="d94a7-223">Select hello **FTP Upload** task you just added, and configure hello following parameters:</span></span>
    
    | <span data-ttu-id="d94a7-224">參數</span><span class="sxs-lookup"><span data-stu-id="d94a7-224">Parameter</span></span> | <span data-ttu-id="d94a7-225">值</span><span class="sxs-lookup"><span data-stu-id="d94a7-225">Value</span></span> |
    | -----     | ----- |
    |<span data-ttu-id="d94a7-226">驗證方法</span><span class="sxs-lookup"><span data-stu-id="d94a7-226">Authentication Method</span></span>| <span data-ttu-id="d94a7-227">輸入認證</span><span class="sxs-lookup"><span data-stu-id="d94a7-227">Enter Credentials</span></span>|
    |<span data-ttu-id="d94a7-228">伺服器 URL</span><span class="sxs-lookup"><span data-stu-id="d94a7-228">Server URL</span></span> | <span data-ttu-id="d94a7-229">從 Azure Stack 入口網站取出 Web 應用程式 FTP URL</span><span class="sxs-lookup"><span data-stu-id="d94a7-229">Web App FTP URL retrieved from Azure Stack portal</span></span> |
    |<span data-ttu-id="d94a7-230">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d94a7-230">Username</span></span> | <span data-ttu-id="d94a7-231">建立 Web 應用程式的 FTP 認證時所設定的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d94a7-231">Username you configured when creating FTP Credentials for Web App</span></span> |
    |<span data-ttu-id="d94a7-232">密碼</span><span class="sxs-lookup"><span data-stu-id="d94a7-232">Password</span></span> | <span data-ttu-id="d94a7-233">建立 Web 應用程式的 FTP 認證時所建立的密碼</span><span class="sxs-lookup"><span data-stu-id="d94a7-233">Password you created when establishing FTP credentials for Web App</span></span>|
    |<span data-ttu-id="d94a7-234">來源目錄</span><span class="sxs-lookup"><span data-stu-id="d94a7-234">Source Directory</span></span> | <span data-ttu-id="d94a7-235">$(System.DefaultWorkingDirectory)\**\\</span><span class="sxs-lookup"><span data-stu-id="d94a7-235">$(System.DefaultWorkingDirectory)\**\\</span></span> |
    |<span data-ttu-id="d94a7-236">遠端目錄</span><span class="sxs-lookup"><span data-stu-id="d94a7-236">Remote Directory</span></span> | <span data-ttu-id="d94a7-237">/site/wwwroot/</span><span class="sxs-lookup"><span data-stu-id="d94a7-237">/site/wwwroot/</span></span>|
    |<span data-ttu-id="d94a7-238">保留檔案路徑</span><span class="sxs-lookup"><span data-stu-id="d94a7-238">Preserve file paths</span></span> | <span data-ttu-id="d94a7-239">已啟用 (已勾選)</span><span class="sxs-lookup"><span data-stu-id="d94a7-239">Enabled (checked)</span></span>|

2.  <span data-ttu-id="d94a7-240">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="d94a7-240">Click **Save**</span></span>

<span data-ttu-id="d94a7-241">最後，設定 hello 發行定義 toouse hello 代理程式集區包含 hello 代理程式部署使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d94a7-241">Finally, configure hello release definition toouse hello agent pool containing hello agent deployed using hello following steps:</span></span>
1.  <span data-ttu-id="d94a7-242">選取 hello 發行定義，然後按一下**編輯**</span><span class="sxs-lookup"><span data-stu-id="d94a7-242">Select hello release definition and click **Edit**</span></span>
2.  <span data-ttu-id="d94a7-243">選取**代理程式上執行**從 hello 中間的資料行。</span><span class="sxs-lookup"><span data-stu-id="d94a7-243">Select **Run on agent** from hello middle column.</span></span> <span data-ttu-id="d94a7-244">Hello 右邊資料行中，選取 hello 代理程式的佇列包含 hello Azure 堆疊上執行的組建代理程式。</span><span class="sxs-lookup"><span data-stu-id="d94a7-244">In hello right column, select hello agent queue containing hello build agent running on Azure Stack.</span></span>  
    <span data-ttu-id="d94a7-245">![映像顯示設定的發行定義 toouse 特定佇列](./media/azure-stack-solution-pipeline/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d94a7-245">![image showing configuration of release definition toouse specific queue](./media/azure-stack-solution-pipeline/image3.png)</span></span>

## <a name="deploy-new-code"></a><span data-ttu-id="d94a7-246">部署新程式碼</span><span class="sxs-lookup"><span data-stu-id="d94a7-246">Deploy new code</span></span>
<span data-ttu-id="d94a7-247">您現在可以測試具有 hello 最後一個步驟發行 tooAzure 堆疊，hello 混合式 CI/CD 管線。</span><span class="sxs-lookup"><span data-stu-id="d94a7-247">You can now test hello hybrid CI/CD pipeline, with hello final step publishing tooAzure Stack.</span></span>  <span data-ttu-id="d94a7-248">本節中，您可以修改 hello 站台的頁尾，並開始透過 hello 管線進行部署。</span><span class="sxs-lookup"><span data-stu-id="d94a7-248">In this section, you modify hello site's footer and start deployment through hello pipeline.</span></span>  <span data-ttu-id="d94a7-249">完成後，您會看到您的變更部署 tooAzure 供檢閱，則一旦核准 hello 版本時，它們並發行的 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d94a7-249">Once complete, you will see your changes deployed tooAzure for review, then once you approve hello release, they are published tooAzure Stack.</span></span>

1. <span data-ttu-id="d94a7-250">在 Visual Studio 中，開啟 hello *site.master*檔案，並變更這一行：</span><span class="sxs-lookup"><span data-stu-id="d94a7-250">In Visual Studio, open hello *site.master* file and change this line:</span></span>
    
    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application</p>
    `

    <span data-ttu-id="d94a7-251">toothis:</span><span class="sxs-lookup"><span data-stu-id="d94a7-251">toothis:</span></span>

    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application delivered by VSTS, Azure, and Azure Stack</p>
    `
3.  <span data-ttu-id="d94a7-252">Hello 將變更認可並同步 tooVSTS。</span><span class="sxs-lookup"><span data-stu-id="d94a7-252">Commit hello changes and sync tooVSTS.</span></span>  
4.  <span data-ttu-id="d94a7-253">從 hello VSTS 工作區中，檢查選取 hello 組建狀態**建置和發行** > **建置**</span><span class="sxs-lookup"><span data-stu-id="d94a7-253">From hello VSTS workspace, check hello build status by selecting **Build & Release** > **Build**</span></span>
5.  <span data-ttu-id="d94a7-254">您將會看到進行中的組建。</span><span class="sxs-lookup"><span data-stu-id="d94a7-254">You will see a build in progress.</span></span>  <span data-ttu-id="d94a7-255">按兩下 hello 狀態，您可以觀看 hello 建置進度。</span><span class="sxs-lookup"><span data-stu-id="d94a7-255">Double-click hello status, and you can watch hello build progress.</span></span>  <span data-ttu-id="d94a7-256">一旦您在 hello 主控台中看到 [已完成的組建]，移動 toocheck hello 發行從**建置和發行** > **釋放**。</span><span class="sxs-lookup"><span data-stu-id="d94a7-256">Once you see "Finished build" in hello console, move on toocheck hello release from **Build & Release** > **Release**.</span></span>  <span data-ttu-id="d94a7-257">按兩下 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="d94a7-257">Double-click hello release.</span></span>
6.  <span data-ttu-id="d94a7-258">您將會收到一則發行需要檢閱的通知。</span><span class="sxs-lookup"><span data-stu-id="d94a7-258">You will receive notification that a release requires review.</span></span> <span data-ttu-id="d94a7-259">檢查 hello Web 應用程式 URL 並確認 hello 新的變更會出現。</span><span class="sxs-lookup"><span data-stu-id="d94a7-259">Check hello Web App URL and verify hello new changes are present.</span></span>  <span data-ttu-id="d94a7-260">核准在 VSTS 中的 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="d94a7-260">Approve hello release in VSTS.</span></span>
    <span data-ttu-id="d94a7-261">![映像顯示設定的發行定義 toouse 特定佇列](./media/azure-stack-solution-pipeline/image4.png)</span><span class="sxs-lookup"><span data-stu-id="d94a7-261">![image showing configuration of release definition toouse specific queue](./media/azure-stack-solution-pipeline/image4.png)</span></span>
    
7.  <span data-ttu-id="d94a7-262">請確認發行 tooAzure 堆疊瀏覽 hello 網站使用 hello 時會建立 hello Web 應用程式的 URL 已完成。</span><span class="sxs-lookup"><span data-stu-id="d94a7-262">Verify publishing tooAzure Stack is complete by visiting hello website using hello URL noted when creating hello Web App.</span></span>
    <span data-ttu-id="d94a7-263">![顯示 ASP.NET 應用程式以及已變更頁尾的影像](./media/azure-stack-solution-pipeline/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d94a7-263">![image showing ASP.NEt app with footer changed](./media/azure-stack-solution-pipeline/image5.png)</span></span>


<span data-ttu-id="d94a7-264">您現在可以使用新的混合式 CI/CD 管線作為其他混合式雲端模式的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="d94a7-264">You can now use your new hybrid CI/CD pipeline as a building block for other hybrid cloud patterns.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d94a7-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d94a7-265">Next steps</span></span>
<span data-ttu-id="d94a7-266">在本教學課程中，您學到如何 toobuild CI/CD 的混合式管線的：</span><span class="sxs-lookup"><span data-stu-id="d94a7-266">In this tutorial, you learned how toobuild a hybrid CI/CD pipeline that:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d94a7-267">會啟動新的組建程式碼認可 tooyour Visual Studio Team Services (VSTS) 儲存機制為基礎。</span><span class="sxs-lookup"><span data-stu-id="d94a7-267">Initiates a new build based on code commits tooyour Visual Studio Team Services (VSTS) repository.</span></span>
> * <span data-ttu-id="d94a7-268">將使用者接受度測試您新建立的程式碼 tooAzure 自動部署。</span><span class="sxs-lookup"><span data-stu-id="d94a7-268">Automatically deploys your newly built code tooAzure for user acceptance testing.</span></span>
> * <span data-ttu-id="d94a7-269">一旦您的程式碼已通過測試，自動將部署 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d94a7-269">Once your code has passed testing, automatically deploys tooAzure Stack.</span></span> 

<span data-ttu-id="d94a7-270">有混合式 CI/CD 管線之後，繼續學習如何針對 Azure 堆疊 toodevelop 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d94a7-270">Now that you have a hybrid CI/CD pipeline, continue by learning how toodevelop apps for Azure Stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d94a7-271">開發 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d94a7-271">Develop for Azure Stack</span></span>](azure-stack-developer.md)


