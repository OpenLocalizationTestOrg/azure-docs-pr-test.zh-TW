---
title: "將您的應用程式部署至 Azure 和 Azure Stack | Microsoft Docs"
description: "了解如何使用混合式 CI/CD 管線將應用程式部署至 Azure 和 Azure Stack。"
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
ms.openlocfilehash: 019d743b0b3104e16a6690f438e7841fa63f09d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-apps-to-azure-and-azure-stack"></a><span data-ttu-id="66441-103">將應用程式部署至 Azure 和 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="66441-103">Deploy apps to Azure and Azure Stack</span></span>
<span data-ttu-id="66441-104">混合式[持續整合](https://www.visualstudio.com/learn/what-is-continuous-integration/)/[持續傳遞](https://www.visualstudio.com/learn/what-is-continuous-delivery/) (CI/CD) 管線可讓您建置、測試以及將應用程式部署至多個雲端。</span><span class="sxs-lookup"><span data-stu-id="66441-104">A hybrid [continuous integration](https://www.visualstudio.com/learn/what-is-continuous-integration/)/[continuous delivery](https://www.visualstudio.com/learn/what-is-continuous-delivery/)(CI/CD) pipeline enables you to build, test, and deploy your app to multiple clouds.</span></span>  <span data-ttu-id="66441-105">在本教學課程中，您會建立一個範例環境以了解混合式 CI/CD 管線可以協助您的方式：</span><span class="sxs-lookup"><span data-stu-id="66441-105">In this tutorial, you build a sample environment to learn how a hybrid CI/CD pipeline can help you:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="66441-106">根據 Visual Studio Team Services (VSTS) 存放庫的程式碼認可起始新的組建。</span><span class="sxs-lookup"><span data-stu-id="66441-106">Initiate a new build based on code commits to your Visual Studio Team Services (VSTS) repository.</span></span>
> * <span data-ttu-id="66441-107">自動將您新建置的程式碼部署至 Azure 以進行使用者驗收測試。</span><span class="sxs-lookup"><span data-stu-id="66441-107">Automatically deploy your newly built code to Azure for user acceptance testing.</span></span>
> * <span data-ttu-id="66441-108">一旦您的程式碼已通過測試，便會自動部署至 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="66441-108">Once your code has passed testing, automatically deploy to Azure Stack.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="66441-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="66441-109">Prerequisites</span></span>
<span data-ttu-id="66441-110">建置混合式 CI/CD 管線所需的幾個元件，且可能需要一些時間來準備。</span><span class="sxs-lookup"><span data-stu-id="66441-110">A few components are required to build a hybrid CI/CD pipeline, and may take some time to prepare.</span></span>  <span data-ttu-id="66441-111">如果您已擁有其中部分元件，請在開始之前確定它們符合需求。</span><span class="sxs-lookup"><span data-stu-id="66441-111">If you already have some of these components, make sure they meet the requirements before beginning.</span></span>

<span data-ttu-id="66441-112">本主題也假設您擁有 Azure 和 Azure Stack 的部分知識。</span><span class="sxs-lookup"><span data-stu-id="66441-112">This topic also assumes that you have some knowledge of Azure and Azure Stack.</span></span> <span data-ttu-id="66441-113">如果您想要深入了解之後再繼續，請務必從這些主題開始：</span><span class="sxs-lookup"><span data-stu-id="66441-113">If you want to learn more before proceeding, be sure to start with these topics:</span></span>

- [<span data-ttu-id="66441-114">Azure 簡介</span><span class="sxs-lookup"><span data-stu-id="66441-114">Introduction to Azure</span></span>](https://docs.microsoft.com/azure/fundamentals-introduction-to-azure)
- [<span data-ttu-id="66441-115">Azure Stack 重要概念</span><span class="sxs-lookup"><span data-stu-id="66441-115">Azure Stack Key Concepts</span></span>](azure-stack-key-features.md)

### <a name="azure"></a><span data-ttu-id="66441-116">Azure</span><span class="sxs-lookup"><span data-stu-id="66441-116">Azure</span></span>
 - <span data-ttu-id="66441-117">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="66441-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
 - <span data-ttu-id="66441-118">建立 [Web 應用程式](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)，並將其設定為用於 [FTP 發行](../app-service-web/app-service-deploy-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="66441-118">Create a [Web App](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md), and configure it for [FTP publishing](../app-service-web/app-service-deploy-ftp.md).</span></span>  <span data-ttu-id="66441-119">記下新的 Web 應用程式 URL，因為稍後將會用到。</span><span class="sxs-lookup"><span data-stu-id="66441-119">Make note of the new Web App URL, as it is used later.</span></span>


### <a name="azure-stack"></a><span data-ttu-id="66441-120">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="66441-120">Azure Stack</span></span>
 - <span data-ttu-id="66441-121">[部署 Azure Stack](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="66441-121">[Deploy Azure Stack](azure-stack-run-powershell-script.md).</span></span>  <span data-ttu-id="66441-122">安裝程序通常需要幾個小時才能完成，因此請據以規劃時段。</span><span class="sxs-lookup"><span data-stu-id="66441-122">The installation usually takes a few hours to complete, so plan accordingly.</span></span>
 - <span data-ttu-id="66441-123">將 [App Service](azure-stack-app-service-deploy.md) PaaS 服務部署至 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="66441-123">Deploy [App Service](azure-stack-app-service-deploy.md) PaaS services to Azure Stack.</span></span>
 - <span data-ttu-id="66441-124">建立 Web 應用程式，並將其設定為用於 [FTP 發行](azure-stack-app-service-enable-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="66441-124">Create a Web App and configure it for [FTP publishing](azure-stack-app-service-enable-ftp.md).</span></span>  <span data-ttu-id="66441-125">記下新的 Web 應用程式 URL，因為稍後將會用到。</span><span class="sxs-lookup"><span data-stu-id="66441-125">Make note of the new Web App URL, as it is used later.</span></span>  

### <a name="developer-tools"></a><span data-ttu-id="66441-126">開發人員工具</span><span class="sxs-lookup"><span data-stu-id="66441-126">Developer tools</span></span>
 - <span data-ttu-id="66441-127">建立 [VSTS 工作區](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)。</span><span class="sxs-lookup"><span data-stu-id="66441-127">Create a [VSTS workspace](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span></span>  <span data-ttu-id="66441-128">註冊程序會建立名為「MyFirstProject」的專案。</span><span class="sxs-lookup"><span data-stu-id="66441-128">The sign-up process creates a project named "MyFirstProject."</span></span>  
 - <span data-ttu-id="66441-129">[安裝 Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio) 並[登入 VSTS](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#connect-and-share-code-from-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="66441-129">[Install Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio) and [sign-in to VSTS](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#connect-and-share-code-from-visual-studio)</span></span>
 - <span data-ttu-id="66441-130">連線至專案並[在本機複製](https://www.visualstudio.com/docs/git/gitquickstart)。</span><span class="sxs-lookup"><span data-stu-id="66441-130">Connect to the project and [clone locally](https://www.visualstudio.com/docs/git/gitquickstart).</span></span>
 - <span data-ttu-id="66441-131">在 VSTS 中建立[代理程式集區](https://www.visualstudio.com/docs/build/concepts/agents/pools-queues#creating-agent-pools-and-queues)。</span><span class="sxs-lookup"><span data-stu-id="66441-131">Create an [agent pool](https://www.visualstudio.com/docs/build/concepts/agents/pools-queues#creating-agent-pools-and-queues) in VSTS.</span></span>
 - <span data-ttu-id="66441-132">安裝 Visual Studio 並將 [VSTS 組建代理程式](https://www.visualstudio.com/docs/build/actions/agents/v2-windows)部署至 Azure Stack 上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="66441-132">Install Visual Studio and deploy a [VSTS build agent](https://www.visualstudio.com/docs/build/actions/agents/v2-windows) to a virtual machine on Azure Stack.</span></span> 
 

## <a name="create-app--push-to-vsts"></a><span data-ttu-id="66441-133">建立應用程式並推送至 VSTS</span><span class="sxs-lookup"><span data-stu-id="66441-133">Create app & push to VSTS</span></span>

### <a name="create-application"></a><span data-ttu-id="66441-134">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="66441-134">Create application</span></span>
<span data-ttu-id="66441-135">在本節中，您會建立簡單的 ASP.NET 應用程式，並將其推送至 VSTS。</span><span class="sxs-lookup"><span data-stu-id="66441-135">In this section, you create a simple ASP.NET application and push it to VSTS.</span></span>  <span data-ttu-id="66441-136">這些步驟代表一般開發人員的工作流程，且能夠針對開發人員工具和語言進行調整。</span><span class="sxs-lookup"><span data-stu-id="66441-136">These steps represent the normal developer workflow, and could be adapted for developer tools and languages.</span></span> 

1.  <span data-ttu-id="66441-137">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="66441-137">Open Visual Studio.</span></span>
2.  <span data-ttu-id="66441-138">從 Team Explorer 空間和 [解決方案] 區域中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="66441-138">From the Team Explorer space and **Solutions...** area, click **New**.</span></span>
3.  <span data-ttu-id="66441-139">選取 [Visual C#]  >  [Web]  >  [ASP.NET Web 應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="66441-139">Select **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
4.  <span data-ttu-id="66441-140">提供應用程式的名稱，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="66441-140">Provide a name for the application and click **OK**.</span></span>
5.  <span data-ttu-id="66441-141">在下一個畫面上，保留預設值 (Web Form)，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="66441-141">On the next screen, keep the defaults (Web forms) and click **OK**.</span></span>

### <a name="commit-and-push-changes-to-vsts"></a><span data-ttu-id="66441-142">認可並推送變更至 VSTS</span><span class="sxs-lookup"><span data-stu-id="66441-142">Commit and push changes to VSTS</span></span>
1.  <span data-ttu-id="66441-143">使用 Visual Studio 中的 Team Explorer，接著選取下拉式功能表，然後按一下 [變更]。</span><span class="sxs-lookup"><span data-stu-id="66441-143">Using Team Explorer in Visual Studio, select the dropdown and click **Changes**.</span></span>
2.  <span data-ttu-id="66441-144">提供認可訊息，然後選取 [全部認可]。</span><span class="sxs-lookup"><span data-stu-id="66441-144">Provide a commit message and select **Commit all**.</span></span> <span data-ttu-id="66441-145">系統可能會提示您儲存解決方案檔案，請按一下 [是] 以全部儲存。</span><span class="sxs-lookup"><span data-stu-id="66441-145">You may be prompted to save the solution file, click yes to save all.</span></span>
3.  <span data-ttu-id="66441-146">經過認可之後，Visual Studio 會要求將變更同步至您的專案。</span><span class="sxs-lookup"><span data-stu-id="66441-146">Once committed, Visual Studio offers to sync changes to your project.</span></span> <span data-ttu-id="66441-147">選取 [同步]。</span><span class="sxs-lookup"><span data-stu-id="66441-147">Select **Sync**.</span></span>

    ![完成認可之後顯示認可畫面的影像](./media/azure-stack-solution-pipeline/image1.png)

4.  <span data-ttu-id="66441-149">在 [同步處理] 索引標籤中的 [傳出] 下，您會看到新的認可。</span><span class="sxs-lookup"><span data-stu-id="66441-149">In the synchronization tab, under *Outgoing*, you see your new commit.</span></span>  <span data-ttu-id="66441-150">選取 [推送] 以將變更同步至 VSTS。</span><span class="sxs-lookup"><span data-stu-id="66441-150">Select **Push** to synchronize the change to VSTS.</span></span>

    ![顯示同步步驟的影像](./media/azure-stack-solution-pipeline/image2.png)

### <a name="review-code-in-vsts"></a><span data-ttu-id="66441-152">檢閱 VSTS 中的程式碼</span><span class="sxs-lookup"><span data-stu-id="66441-152">Review code in VSTS</span></span>
<span data-ttu-id="66441-153">認可變更並推送至 VSTS 之後，請從 VSTS 入口網站檢查您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="66441-153">Once you've committed a change and pushed to VSTS, check your code from the VSTS portal.</span></span>  <span data-ttu-id="66441-154">選取 [程式碼]，然後從下拉式功能表中選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="66441-154">Select **Code**, and then **Files** from the dropdown menu.</span></span>  <span data-ttu-id="66441-155">您可以看到已建立的解決方案。</span><span class="sxs-lookup"><span data-stu-id="66441-155">You can see the solution you created.</span></span>

## <a name="create-build-definition"></a><span data-ttu-id="66441-156">建立組建定義</span><span class="sxs-lookup"><span data-stu-id="66441-156">Create build definition</span></span>
<span data-ttu-id="66441-157">建置程序會定義應用程式的建置和封裝方式，以便針對每個程式碼變更的認可進行部署。</span><span class="sxs-lookup"><span data-stu-id="66441-157">The build process defines how your application is built and packaged for deployment on each commit of code changes.</span></span> <span data-ttu-id="66441-158">在此範例中，儘管可能會根據您的應用程式調整此組態，我們仍會使用包含的範本來設定 ASP.NET 應用程式的建置程序。</span><span class="sxs-lookup"><span data-stu-id="66441-158">In our example, we use the included template to configure the build process for an ASP.NET app, though this configuration could be adapted depending on your application.</span></span>

1.  <span data-ttu-id="66441-159">從網頁瀏覽器登入您的 VSTS 工作區。</span><span class="sxs-lookup"><span data-stu-id="66441-159">Sign in to your VSTS workspace from a web browser.</span></span>
2.  <span data-ttu-id="66441-160">從橫幅中從選取 [建置與發行]，然後選取 [建置]。</span><span class="sxs-lookup"><span data-stu-id="66441-160">From the banner, select **Build & Release**  and then **Builds**.</span></span>
3.  <span data-ttu-id="66441-161">選取 [+新增定義]。</span><span class="sxs-lookup"><span data-stu-id="66441-161">Click **+ New definition**.</span></span>
4.  <span data-ttu-id="66441-162">從範本的清單中，選取 [ASP.NET (預覽)]，然後選取 [套用]。</span><span class="sxs-lookup"><span data-stu-id="66441-162">From the list of templates, select **ASP.NET (Preview)** and select **Apply**.</span></span>
5.  <span data-ttu-id="66441-163">將 [建置方案] 步驟中的 [MSBuild 引數] 欄位修改為：</span><span class="sxs-lookup"><span data-stu-id="66441-163">Modify the *MSBuild Arguments* field in *Build Solution* step to:</span></span>

    `/p:DeployOnBuild=True /p:WebPublishMethod=FileSystem /p:DeployDefaultTarget=WebPublish /p:publishUrl="$(build.artifactstagingdirectory)\\"`

6.  <span data-ttu-id="66441-164">選取 [選項] 索引標籤，然後選取您部署至 Azure Stack 上虛擬機器之組建代理程式的代理程式佇列。</span><span class="sxs-lookup"><span data-stu-id="66441-164">Select the **Options** tab, and select the agent queue for the build agent you deployed to a virtual machine on Azure Stack.</span></span> 
7.  <span data-ttu-id="66441-165">選取 [觸發程序] 索引標籤，然後啟用 [持續整合]。</span><span class="sxs-lookup"><span data-stu-id="66441-165">Select the **Triggers** tab, and enable **Continuous Integration**.</span></span>
7.  <span data-ttu-id="66441-166">按一下 [儲存與佇列]，然後從下拉式功能表選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="66441-166">Click **Save & queue** and then select **Save** from the dropdown.</span></span> 

## <a name="create-release-definition"></a><span data-ttu-id="66441-167">建立發行定義</span><span class="sxs-lookup"><span data-stu-id="66441-167">Create release definition</span></span>
<span data-ttu-id="66441-168">發行程序會定義組建如何從上一個步驟部署至環境。</span><span class="sxs-lookup"><span data-stu-id="66441-168">The release process defines how builds from the previous step are deployed to an environment.</span></span>  <span data-ttu-id="66441-169">在本教學課程中，我們將使用 FTP 將 ASP.NET 應用程式發行至 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66441-169">In this tutorial, we publish our ASP.NET app with FTP to an Azure Web App.</span></span> <span data-ttu-id="66441-170">若要設定 Azure 的發行，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66441-170">To configure a release to Azure, use the following steps:</span></span>

1.  <span data-ttu-id="66441-171">從 VSTS 橫幅中從選取 [建置與發行]，然後選取 [建置]。</span><span class="sxs-lookup"><span data-stu-id="66441-171">From the VSTS banner, select **Build & Release**  and then **Releases**.</span></span>
2.  <span data-ttu-id="66441-172">按一下綠色的 [+ 新定義]。</span><span class="sxs-lookup"><span data-stu-id="66441-172">Click the green **+ New definition**.</span></span>
3.  <span data-ttu-id="66441-173">選取 [空白] ，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="66441-173">Select **Empty** and click **Next**.</span></span>
4.  <span data-ttu-id="66441-174">勾選 [持續部署] 的核取方塊，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="66441-174">Check the box for *Continuous deployment*, and then click **Create**.</span></span>

<span data-ttu-id="66441-175">現在，您已建立空白的發行定義並將其連結至組建，而我們會加入 Azure 環境的步驟：</span><span class="sxs-lookup"><span data-stu-id="66441-175">Now that you've created an empty release definition and tied it to the build, we add steps for the Azure environment:</span></span>

1.  <span data-ttu-id="66441-176">按一下綠色的  **+**  來加入工作。</span><span class="sxs-lookup"><span data-stu-id="66441-176">Click the green **+** to add tasks.</span></span>
2.  <span data-ttu-id="66441-177">選取 [所有]，接著從清單中新增 [FTP 上傳]，然後選取 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="66441-177">Select **All**, and then from the list, add **FTP Upload** and select **Close**.</span></span>
3.  <span data-ttu-id="66441-178">選取您剛才新增的 [FTP 上傳] 工作，並設定下列參數：</span><span class="sxs-lookup"><span data-stu-id="66441-178">Select the **FTP Upload** task you just added, and configure the following parameters:</span></span>
    
    | <span data-ttu-id="66441-179">參數</span><span class="sxs-lookup"><span data-stu-id="66441-179">Parameter</span></span> | <span data-ttu-id="66441-180">值</span><span class="sxs-lookup"><span data-stu-id="66441-180">Value</span></span> |
    | ----- | ----- |
    |<span data-ttu-id="66441-181">驗證方法</span><span class="sxs-lookup"><span data-stu-id="66441-181">Authentication Method</span></span>| <span data-ttu-id="66441-182">輸入認證</span><span class="sxs-lookup"><span data-stu-id="66441-182">Enter Credentials</span></span>|
    |<span data-ttu-id="66441-183">伺服器 URL</span><span class="sxs-lookup"><span data-stu-id="66441-183">Server URL</span></span> | <span data-ttu-id="66441-184">從 Azure 入口網站取出 Web 應用程式 FTP URL</span><span class="sxs-lookup"><span data-stu-id="66441-184">Web App FTP URL retrieved from Azure portal</span></span> |
    |<span data-ttu-id="66441-185">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="66441-185">Username</span></span> | <span data-ttu-id="66441-186">建立 Web 應用程式的 FTP 認證時所設定的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="66441-186">Username you configured when creating FTP Credentials for Web App</span></span> |
    |<span data-ttu-id="66441-187">密碼</span><span class="sxs-lookup"><span data-stu-id="66441-187">Password</span></span> | <span data-ttu-id="66441-188">建立 Web 應用程式的 FTP 認證時所建立的密碼</span><span class="sxs-lookup"><span data-stu-id="66441-188">Password you created when establishing FTP credentials for Web App</span></span>|
    |<span data-ttu-id="66441-189">來源目錄</span><span class="sxs-lookup"><span data-stu-id="66441-189">Source Directory</span></span> | <span data-ttu-id="66441-190">$(System.DefaultWorkingDirectory)\**\\</span><span class="sxs-lookup"><span data-stu-id="66441-190">$(System.DefaultWorkingDirectory)\**\\</span></span> |
    |<span data-ttu-id="66441-191">遠端目錄</span><span class="sxs-lookup"><span data-stu-id="66441-191">Remote Directory</span></span> | <span data-ttu-id="66441-192">/site/wwwroot/</span><span class="sxs-lookup"><span data-stu-id="66441-192">/site/wwwroot/</span></span> |
    |<span data-ttu-id="66441-193">保留檔案路徑</span><span class="sxs-lookup"><span data-stu-id="66441-193">Preserve file paths</span></span> | <span data-ttu-id="66441-194">已啟用 (已勾選)</span><span class="sxs-lookup"><span data-stu-id="66441-194">Enabled (checked)</span></span>|

4.  <span data-ttu-id="66441-195">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="66441-195">Click **Save**</span></span>

<span data-ttu-id="66441-196">最後，您可以設定要使用代理程式集區的發行定義，而其中包含使用下列步驟部署的代理程式：</span><span class="sxs-lookup"><span data-stu-id="66441-196">Finally, you configure the release definition to use the agent pool containing the agent deployed using the following steps:</span></span>
1.  <span data-ttu-id="66441-197">選取發行定義，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="66441-197">Select the release definition and click **Edit**.</span></span>
2.  <span data-ttu-id="66441-198">從中間的資料行中選取 [在代理程式上執行]。</span><span class="sxs-lookup"><span data-stu-id="66441-198">Select **Run on agent** from the middle column.</span></span>  <span data-ttu-id="66441-199">在右邊的資料行中，選取包含在 Azure Stack 上執行之組建代理程式的代理程式佇列。</span><span class="sxs-lookup"><span data-stu-id="66441-199">In the right column, select the agent queue containing the build agent running on Azure Stack.</span></span>  
    <span data-ttu-id="66441-200">![顯示發行定義組態以使用特定佇列的影像](./media/azure-stack-solution-pipeline/image3.png)</span><span class="sxs-lookup"><span data-stu-id="66441-200">![image showing configuration of release definition to use specific queue](./media/azure-stack-solution-pipeline/image3.png)</span></span>


## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="66441-201">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="66441-201">Deploy your app to Azure</span></span>
<span data-ttu-id="66441-202">此步驟會使用新建立的 CI/CD 管線將 ASP.NET 應用程式部署至 Azure 上的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66441-202">This step uses your newly built CI/CD pipeline to deploy the ASP.NET app to a Web App on Azure.</span></span> 

1.  <span data-ttu-id="66441-203">從 VSTS 中的橫幅選取 [建置與發行]，然後選取 [建置]。</span><span class="sxs-lookup"><span data-stu-id="66441-203">From the banner in VSTS, select **Build & Release**, and then select **Builds**.</span></span>
2.  <span data-ttu-id="66441-204">在先前已建立的組建定義上按一下 [...]，並選取 [將新組建排入佇列]。</span><span class="sxs-lookup"><span data-stu-id="66441-204">Click **...** on the build definition previously created, and select **Queue new build**.</span></span>
3.  <span data-ttu-id="66441-205">接受預設值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="66441-205">Accept the defaults and click **Ok**.</span></span>  <span data-ttu-id="66441-206">組建隨即開始，並顯示進度。</span><span class="sxs-lookup"><span data-stu-id="66441-206">The build begins and displays progress.</span></span>
4.  <span data-ttu-id="66441-207">當組建完成之後，您可以藉由選取 [建置與發行]，然後選取 [發行] 來追蹤狀態。</span><span class="sxs-lookup"><span data-stu-id="66441-207">Once the build is complete, you can track the status by selecting **Build & Release** and selecting **Releases**.</span></span>
5.  <span data-ttu-id="66441-208">組建完成之後，請使用建立 Web 應用程式時所記下的 URL 來造訪網站。</span><span class="sxs-lookup"><span data-stu-id="66441-208">After the build is complete, visit the website using the URL noted when creating the Web App.</span></span>    


## <a name="add-azure-stack-to-pipeline"></a><span data-ttu-id="66441-209">將 Azure Stack 新增至管線</span><span class="sxs-lookup"><span data-stu-id="66441-209">Add Azure Stack to pipeline</span></span>
<span data-ttu-id="66441-210">現在您已透過部署至 Azure 測試過 CI/CD 管線，便可以開始將 Azure Stack 新增至管線。</span><span class="sxs-lookup"><span data-stu-id="66441-210">Now that you've tested your CI/CD pipeline by deploying to Azure, it's time to add Azure Stack to the pipeline.</span></span>  <span data-ttu-id="66441-211">在下列步驟中，您會建立新的環境並新增 FTP 上傳的工作，以便將您的應用程式部署至 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="66441-211">In the following steps, you create a new environment and add an FTP Upload task to deploy your app to Azure Stack.</span></span>  <span data-ttu-id="66441-212">您也可以新增發行核准者作為模擬對發行至 Azure Stack 程式碼進行「簽署」的方式。</span><span class="sxs-lookup"><span data-stu-id="66441-212">You also add a release approver, which serves as a way to simulate "signing off" on a code release to Azure Stack.</span></span>  

1.  <span data-ttu-id="66441-213">在發行定義中，選取 [+ 新增環境] 和 [建立新環境]。</span><span class="sxs-lookup"><span data-stu-id="66441-213">In the Release definition, select **+ Add Environment** and **Create new environment**.</span></span>
2.  <span data-ttu-id="66441-214">選取 [空白] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="66441-214">Select **Empty**, click **Next**.</span></span>
3.  <span data-ttu-id="66441-215">選取 [特定使用者] 並指定您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="66441-215">Select **Specific users** and specify your account.</span></span>  <span data-ttu-id="66441-216">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="66441-216">Select **Create**.</span></span>
4.  <span data-ttu-id="66441-217">透過選取現有的名稱，然後輸入 Azure Stack 以重新命名環境。</span><span class="sxs-lookup"><span data-stu-id="66441-217">Rename the environment by selecting the existing name and typing *Azure Stack*.</span></span>
5.  <span data-ttu-id="66441-218">現在，選取 Azure Stack 環境，然後選取 [新增工作]。</span><span class="sxs-lookup"><span data-stu-id="66441-218">Now, selection the Azure Stack environment, then select **Add tasks**.</span></span>
6.  <span data-ttu-id="66441-219">選取 [FTP 上傳] 工作，接著選取 [新增]，然後選取 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="66441-219">Select the **FTP Upload** task and select **Add**, then select **Close**.</span></span>


### <a name="configure-ftp-task"></a><span data-ttu-id="66441-220">設定 FTP 工作</span><span class="sxs-lookup"><span data-stu-id="66441-220">Configure FTP task</span></span>
<span data-ttu-id="66441-221">現在您已建立版本，您將需要設定發行至 Azure Stack 上 Web 應用程式所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="66441-221">Now that you've created a release, you'll configure the steps required for publishing to the Web App on Azure Stack.</span></span>  <span data-ttu-id="66441-222">如同您為 Azure 設定 FTP 上傳工作，您可以設定 Azure Stack 的工作：</span><span class="sxs-lookup"><span data-stu-id="66441-222">Just like you configured the FTP Upload task for Azure, you configure the task for Azure Stack:</span></span>

1.  <span data-ttu-id="66441-223">選取您剛才新增的 [FTP 上傳] 工作，並設定下列參數：</span><span class="sxs-lookup"><span data-stu-id="66441-223">Select the **FTP Upload** task you just added, and configure the following parameters:</span></span>
    
    | <span data-ttu-id="66441-224">參數</span><span class="sxs-lookup"><span data-stu-id="66441-224">Parameter</span></span> | <span data-ttu-id="66441-225">值</span><span class="sxs-lookup"><span data-stu-id="66441-225">Value</span></span> |
    | -----     | ----- |
    |<span data-ttu-id="66441-226">驗證方法</span><span class="sxs-lookup"><span data-stu-id="66441-226">Authentication Method</span></span>| <span data-ttu-id="66441-227">輸入認證</span><span class="sxs-lookup"><span data-stu-id="66441-227">Enter Credentials</span></span>|
    |<span data-ttu-id="66441-228">伺服器 URL</span><span class="sxs-lookup"><span data-stu-id="66441-228">Server URL</span></span> | <span data-ttu-id="66441-229">從 Azure Stack 入口網站取出 Web 應用程式 FTP URL</span><span class="sxs-lookup"><span data-stu-id="66441-229">Web App FTP URL retrieved from Azure Stack portal</span></span> |
    |<span data-ttu-id="66441-230">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="66441-230">Username</span></span> | <span data-ttu-id="66441-231">建立 Web 應用程式的 FTP 認證時所設定的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="66441-231">Username you configured when creating FTP Credentials for Web App</span></span> |
    |<span data-ttu-id="66441-232">密碼</span><span class="sxs-lookup"><span data-stu-id="66441-232">Password</span></span> | <span data-ttu-id="66441-233">建立 Web 應用程式的 FTP 認證時所建立的密碼</span><span class="sxs-lookup"><span data-stu-id="66441-233">Password you created when establishing FTP credentials for Web App</span></span>|
    |<span data-ttu-id="66441-234">來源目錄</span><span class="sxs-lookup"><span data-stu-id="66441-234">Source Directory</span></span> | <span data-ttu-id="66441-235">$(System.DefaultWorkingDirectory)\**\\</span><span class="sxs-lookup"><span data-stu-id="66441-235">$(System.DefaultWorkingDirectory)\**\\</span></span> |
    |<span data-ttu-id="66441-236">遠端目錄</span><span class="sxs-lookup"><span data-stu-id="66441-236">Remote Directory</span></span> | <span data-ttu-id="66441-237">/site/wwwroot/</span><span class="sxs-lookup"><span data-stu-id="66441-237">/site/wwwroot/</span></span>|
    |<span data-ttu-id="66441-238">保留檔案路徑</span><span class="sxs-lookup"><span data-stu-id="66441-238">Preserve file paths</span></span> | <span data-ttu-id="66441-239">已啟用 (已勾選)</span><span class="sxs-lookup"><span data-stu-id="66441-239">Enabled (checked)</span></span>|

2.  <span data-ttu-id="66441-240">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="66441-240">Click **Save**</span></span>

<span data-ttu-id="66441-241">最後，設定要使用代理程式集區的發行定義，而其中包含使用下列步驟部署的代理程式：</span><span class="sxs-lookup"><span data-stu-id="66441-241">Finally, configure the release definition to use the agent pool containing the agent deployed using the following steps:</span></span>
1.  <span data-ttu-id="66441-242">選取發行定義，然後按一下 [編輯]</span><span class="sxs-lookup"><span data-stu-id="66441-242">Select the release definition and click **Edit**</span></span>
2.  <span data-ttu-id="66441-243">從中間的資料行中選取 [在代理程式上執行]。</span><span class="sxs-lookup"><span data-stu-id="66441-243">Select **Run on agent** from the middle column.</span></span> <span data-ttu-id="66441-244">在右邊的資料行中，選取包含在 Azure Stack 上執行之組建代理程式的代理程式佇列。</span><span class="sxs-lookup"><span data-stu-id="66441-244">In the right column, select the agent queue containing the build agent running on Azure Stack.</span></span>  
    <span data-ttu-id="66441-245">![顯示發行定義組態以使用特定佇列的影像](./media/azure-stack-solution-pipeline/image3.png)</span><span class="sxs-lookup"><span data-stu-id="66441-245">![image showing configuration of release definition to use specific queue](./media/azure-stack-solution-pipeline/image3.png)</span></span>

## <a name="deploy-new-code"></a><span data-ttu-id="66441-246">部署新程式碼</span><span class="sxs-lookup"><span data-stu-id="66441-246">Deploy new code</span></span>
<span data-ttu-id="66441-247">您現在可以測試混合式 CI/CD 管線，以及發行至 Azure Stack 的最後一個步驟。</span><span class="sxs-lookup"><span data-stu-id="66441-247">You can now test the hybrid CI/CD pipeline, with the final step publishing to Azure Stack.</span></span>  <span data-ttu-id="66441-248">在本節中，您會修改網站的頁尾，並透過管線開始部署。</span><span class="sxs-lookup"><span data-stu-id="66441-248">In this section, you modify the site's footer and start deployment through the pipeline.</span></span>  <span data-ttu-id="66441-249">完成後，您將會看到變更部署至 Azure 以供檢閱，然後在核准發行之後，即會發行至 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="66441-249">Once complete, you will see your changes deployed to Azure for review, then once you approve the release, they are published to Azure Stack.</span></span>

1. <span data-ttu-id="66441-250">在 Visual Studio 中，開啟 site.master 檔案，並變更這一行：</span><span class="sxs-lookup"><span data-stu-id="66441-250">In Visual Studio, open the *site.master* file and change this line:</span></span>
    
    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application</p>
    `

    <span data-ttu-id="66441-251">變更為以下程式碼：</span><span class="sxs-lookup"><span data-stu-id="66441-251">to this:</span></span>

    `
        <p>&copy; <%: DateTime.Now.Year %> - My ASP.NET Application delivered by VSTS, Azure, and Azure Stack</p>
    `
3.  <span data-ttu-id="66441-252">認可變更並同步至 VSTS。</span><span class="sxs-lookup"><span data-stu-id="66441-252">Commit the changes and sync to VSTS.</span></span>  
4.  <span data-ttu-id="66441-253">從 VSTS 工作區中，透過選取 [建置與發行]  > [建置] 來檢查組建狀態</span><span class="sxs-lookup"><span data-stu-id="66441-253">From the VSTS workspace, check the build status by selecting **Build & Release** > **Build**</span></span>
5.  <span data-ttu-id="66441-254">您將會看到進行中的組建。</span><span class="sxs-lookup"><span data-stu-id="66441-254">You will see a build in progress.</span></span>  <span data-ttu-id="66441-255">按兩下 [狀態]，即可觀看組建進度。</span><span class="sxs-lookup"><span data-stu-id="66441-255">Double-click the status, and you can watch the build progress.</span></span>  <span data-ttu-id="66441-256">當您在主控台中看見 [已完成的組建] 時，請繼續從 [建置與發行]  > [發行] 檢查發行。</span><span class="sxs-lookup"><span data-stu-id="66441-256">Once you see "Finished build" in the console, move on to check the release from **Build & Release** > **Release**.</span></span>  <span data-ttu-id="66441-257">按兩下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="66441-257">Double-click the release.</span></span>
6.  <span data-ttu-id="66441-258">您將會收到一則發行需要檢閱的通知。</span><span class="sxs-lookup"><span data-stu-id="66441-258">You will receive notification that a release requires review.</span></span> <span data-ttu-id="66441-259">請檢查 Web 應用程式 URL 並確認新的變更會出現。</span><span class="sxs-lookup"><span data-stu-id="66441-259">Check the Web App URL and verify the new changes are present.</span></span>  <span data-ttu-id="66441-260">核准 VSTS 中的發行。</span><span class="sxs-lookup"><span data-stu-id="66441-260">Approve the release in VSTS.</span></span>
    <span data-ttu-id="66441-261">![顯示發行定義組態以使用特定佇列的影像](./media/azure-stack-solution-pipeline/image4.png)</span><span class="sxs-lookup"><span data-stu-id="66441-261">![image showing configuration of release definition to use specific queue](./media/azure-stack-solution-pipeline/image4.png)</span></span>
    
7.  <span data-ttu-id="66441-262">透過建立 Web 應用程式時所記下的 URL 來造訪網站，以確認發行至 Azure Stack 的作業已完成。</span><span class="sxs-lookup"><span data-stu-id="66441-262">Verify publishing to Azure Stack is complete by visiting the website using the URL noted when creating the Web App.</span></span>
    <span data-ttu-id="66441-263">![顯示 ASP.NET 應用程式以及已變更頁尾的影像](./media/azure-stack-solution-pipeline/image5.png)</span><span class="sxs-lookup"><span data-stu-id="66441-263">![image showing ASP.NEt app with footer changed](./media/azure-stack-solution-pipeline/image5.png)</span></span>


<span data-ttu-id="66441-264">您現在可以使用新的混合式 CI/CD 管線作為其他混合式雲端模式的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="66441-264">You can now use your new hybrid CI/CD pipeline as a building block for other hybrid cloud patterns.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66441-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66441-265">Next steps</span></span>
<span data-ttu-id="66441-266">在本教學課程中，您已學到如何建置一個混合式 CI/CD 管線：</span><span class="sxs-lookup"><span data-stu-id="66441-266">In this tutorial, you learned how to build a hybrid CI/CD pipeline that:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="66441-267">根據 Visual Studio Team Services (VSTS) 存放庫的程式碼認可起始新的建置。</span><span class="sxs-lookup"><span data-stu-id="66441-267">Initiates a new build based on code commits to your Visual Studio Team Services (VSTS) repository.</span></span>
> * <span data-ttu-id="66441-268">自動將您新建置的程式碼部署至 Azure 以進行使用者驗收測試。</span><span class="sxs-lookup"><span data-stu-id="66441-268">Automatically deploys your newly built code to Azure for user acceptance testing.</span></span>
> * <span data-ttu-id="66441-269">一旦您的程式碼已通過測試，便會自動部署至 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="66441-269">Once your code has passed testing, automatically deploys to Azure Stack.</span></span> 

<span data-ttu-id="66441-270">現在，您擁有一個混合式 CI/CD 管線，請繼續了解如何開發 Azure Stack 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="66441-270">Now that you have a hybrid CI/CD pipeline, continue by learning how to develop apps for Azure Stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="66441-271">開發 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="66441-271">Develop for Azure Stack</span></span>](azure-stack-developer.md)


