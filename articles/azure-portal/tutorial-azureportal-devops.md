---
title: "教學課程： 以 hello Azure 入口網站 DevOps |Microsoft 文件"
description: "深入了解 hello hello Azure 入口網站中的各種 DevOps 工作流程。"
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="35efd-103">教學課程： DevOps hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="35efd-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="35efd-104">hello Azure 平台是完整的彈性 DevOps 工作流程。</span><span class="sxs-lookup"><span data-stu-id="35efd-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="35efd-105">在此教學課程中，您將學會如何 hello Azure 入口網站 toodevelop，tooleverage hello 功能測試、 部署、 疑難排解、 監視和管理執行中應用程式。</span><span class="sxs-lookup"><span data-stu-id="35efd-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="35efd-106">本教學課程著重於 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="35efd-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="35efd-107">建立 Web 應用程式並啟用連續部署</span><span class="sxs-lookup"><span data-stu-id="35efd-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="35efd-108">開發和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="35efd-108">Develop and test an app</span></span>
3. <span data-ttu-id="35efd-109">監視和針對應用程式進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="35efd-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="35efd-110">一般應用程式管理工作</span><span class="sxs-lookup"><span data-stu-id="35efd-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="35efd-111">建立 Web 應用程式並啟用連續部署</span><span class="sxs-lookup"><span data-stu-id="35efd-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="35efd-112">建立 Web 應用程式與[Azure App Service](https://azure.microsoft.com/services/app-service/)，會使用在本教學課程的 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="35efd-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="35efd-113">一開始，您將會進行從原始程式碼儲存機制到執行中 Azure 環境的連續部署。</span><span class="sxs-lookup"><span data-stu-id="35efd-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="35efd-114">登入 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="35efd-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="35efd-115">選擇**應用程式服務** &gt; **新增圖示**和輸入的名稱、 選擇您的訂用帳戶，以及為 hello hello 服務容器中建立新的資源群組 tooserve。</span><span class="sxs-lookup"><span data-stu-id="35efd-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="35efd-116">資源群組可讓您 toomanage hello 的解決方案，例如計費、 部署及監視所有以透過單一群組的各個層面[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="35efd-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="35efd-118">幾分鐘後，您的 App Service 便會建立。</span><span class="sxs-lookup"><span data-stu-id="35efd-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="35efd-119">請花幾分鐘的時間 tooexplore hello hello 服務的各種功能表選項 hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="35efd-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="35efd-121">按一下 hello URL。</span><span class="sxs-lookup"><span data-stu-id="35efd-121">Click hello URL.</span></span> <span data-ttu-id="35efd-122">請注意 hello 各種不同的工具和儲存機制的可用選項。</span><span class="sxs-lookup"><span data-stu-id="35efd-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="35efd-123">您也可以使用 hello 語言和您選擇，包括.NET、 Java 和 Ruby 的架構。</span><span class="sxs-lookup"><span data-stu-id="35efd-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="35efd-125">hello Azure 入口網站可讓持續部署簡單的程序，包括只有一些簡單的步驟。</span><span class="sxs-lookup"><span data-stu-id="35efd-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="35efd-126">在 hello Azure 入口網站，選取 從 hello 您剛才建立的應用程式服務的 hello 圖示的 設定。</span><span class="sxs-lookup"><span data-stu-id="35efd-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="35efd-128">從 hello 刀鋒視窗中開啟 hello 右上，捲動 toohello 發行 > 一節。</span><span class="sxs-lookup"><span data-stu-id="35efd-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="35efd-130">接著，設定某些設定 tooenable 的連續部署 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="35efd-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="35efd-131">按一下 部署來源，然後按一下選擇來源。</span><span class="sxs-lookup"><span data-stu-id="35efd-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="35efd-132">請注意 hello 各種選項，您的儲存機制來源。</span><span class="sxs-lookup"><span data-stu-id="35efd-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="35efd-134">在此範例中，請選擇 [GitHub]。</span><span class="sxs-lookup"><span data-stu-id="35efd-134">For this example choose GitHub.</span></span> <span data-ttu-id="35efd-135">選擇性地選擇您所選擇的 hello 儲存機制，並設定 hello 授權認證。</span><span class="sxs-lookup"><span data-stu-id="35efd-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="35efd-137">之後授權 tooyour 儲存機制，然後您可以選擇的專案及您想 toodeploy 的分支。</span><span class="sxs-lookup"><span data-stu-id="35efd-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="35efd-138">下面列出幾個虛構的範例。</span><span class="sxs-lookup"><span data-stu-id="35efd-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="35efd-140">在選擇專案和分支之後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="35efd-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="35efd-141">您應該開始 toosee 通知的部署。</span><span class="sxs-lookup"><span data-stu-id="35efd-141">You should start toosee notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="35efd-143">瀏覽 Azure 以建立 toointegrate hello 原始檔控制儲存機制後 tooGitHub toosee hello webhook。</span><span class="sxs-lookup"><span data-stu-id="35efd-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="35efd-144">hello Azure 入口網站可讓整合與 GitHub 只有一些簡單的步驟。</span><span class="sxs-lookup"><span data-stu-id="35efd-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="35efd-146">toodemonstrate 連續部署，您快速加入一些內容 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="35efd-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="35efd-147">如需簡單範例中，加入範例文字檔案 tooa GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="35efd-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="35efd-148">您是免費 toouse.NET、 Ruby、 Python 或其他類型的應用程式與應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="35efd-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="35efd-149">感覺可用 tooadd 文字檔案時，ASP.NET MVC、 Java 或 Ruby 應用程式 toohello 儲存機制的選擇。</span><span class="sxs-lookup"><span data-stu-id="35efd-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="35efd-151">認可之後變更 tooyour 儲存機制，您會看到新的部署起始 hello 入口網站的通知區域中。</span><span class="sxs-lookup"><span data-stu-id="35efd-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="35efd-152">如果看不到快速變更認可 tooyour 儲存機制之後，請按一下 同步處理。</span><span class="sxs-lookup"><span data-stu-id="35efd-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="35efd-154">此時，如果您再試一次，並載入 hello 應用程式服務的 hello 頁面，您可能會收到 403 錯誤。</span><span class="sxs-lookup"><span data-stu-id="35efd-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="35efd-155">在此範例中，是因為沒有任何一般預設文件的安裝 hello 頁面，例如 index.htm 或 default.html 檔案。</span><span class="sxs-lookup"><span data-stu-id="35efd-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="35efd-156">您可以快速補救這種情況以 hello tooling hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="35efd-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="35efd-157">在 hello Azure 入口網站中選擇 設定&gt;應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="35efd-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="35efd-159">隨即會開啟 [應用程式設定] 的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="35efd-159">A blade opens for application settings.</span></span> <span data-ttu-id="35efd-160">輸入 hello 頁面 」 SamplePage.html"hello 名稱，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="35efd-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="35efd-161">需要幾分鐘的時間 tooexplore hello 其他設定。</span><span class="sxs-lookup"><span data-stu-id="35efd-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![Image14][image14]
15. <span data-ttu-id="35efd-163">選擇性地重新整理您的瀏覽器 URL tooensure 您看到 hello 預期的變更。</span><span class="sxs-lookup"><span data-stu-id="35efd-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="35efd-164">在此情況下，還有一些簡單的文字現在填入 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="35efd-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="35efd-165">每個額外的變更 toohello 儲存機制可能會導致新的自動部署。</span><span class="sxs-lookup"><span data-stu-id="35efd-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![Image15][image15]
    
    <span data-ttu-id="35efd-167">啟用以 hello Azure 入口網站的連續部署是簡單的體驗。</span><span class="sxs-lookup"><span data-stu-id="35efd-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="35efd-168">您也可以建置更複雜的發行管線，並使用現有的原始檔控制和持續整合系統 toodeploy tooAzure，例如運用自動化的建置和發行管理系統的許多其他技術。</span><span class="sxs-lookup"><span data-stu-id="35efd-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="35efd-169">開發和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="35efd-169">Develop and test an app</span></span>
<span data-ttu-id="35efd-170">接下來，進行一些變更 toohello 程式碼基底和這些變更，快速部署。</span><span class="sxs-lookup"><span data-stu-id="35efd-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="35efd-171">您也會設定一些效能測試 hello Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="35efd-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="35efd-172">Hello Azure 入口網站中從 hello 瀏覽窗格中，選擇應用程式服務，並找出您的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="35efd-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![Image16][image16]
2. <span data-ttu-id="35efd-174">按一下 [工具]</span><span class="sxs-lookup"><span data-stu-id="35efd-174">Click Tools</span></span>
   
   ![Image17][image17]
3. <span data-ttu-id="35efd-176">請注意 hello 開發工具 底下。</span><span class="sxs-lookup"><span data-stu-id="35efd-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="35efd-177">有數種有用的工具這裡可讓我們 toowork 與應用程式而不需離開 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="35efd-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="35efd-178">按一下 [主控台]。</span><span class="sxs-lookup"><span data-stu-id="35efd-178">Click on Console.</span></span>
   
   ![Image18][image18]
4. <span data-ttu-id="35efd-180">在 hello 主控台視窗中，您可以為您的應用程式發出即時命令。</span><span class="sxs-lookup"><span data-stu-id="35efd-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="35efd-181">型別 hello dir 命令並按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="35efd-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="35efd-182">請注意，需要較高權限的命令不會運作。</span><span class="sxs-lookup"><span data-stu-id="35efd-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![Image19][image19]
5. <span data-ttu-id="35efd-184">移回 toohello 開發類別目錄，然後選擇 Visual Studio Online。</span><span class="sxs-lookup"><span data-stu-id="35efd-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="35efd-185">注意：Visual Studio Online 現已更名為 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="35efd-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![Image20][image20]
6. <span data-ttu-id="35efd-187">開啟您的應用程式的 hello 瀏覽器中編輯體驗。</span><span class="sxs-lookup"><span data-stu-id="35efd-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![Image21][image21]
7. <span data-ttu-id="35efd-189">隨即會為應用程式安裝 Web 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="35efd-189">A web extension installs for your app.</span></span> <span data-ttu-id="35efd-190">擴充功能快速且輕鬆地新增功能 tooapps 在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="35efd-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="35efd-191">請注意一些 hello hello 以下螢幕擷取畫面中，您可以使用其他擴充功能類型。</span><span class="sxs-lookup"><span data-stu-id="35efd-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![Image22][image22]
8. <span data-ttu-id="35efd-193">一旦 hello Visual Studio Online 擴充功能安裝，請按一下 移至。</span><span class="sxs-lookup"><span data-stu-id="35efd-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![Image23][image23]
9. <span data-ttu-id="35efd-195">在瀏覽器索引標籤隨即開啟，您會看到直接在 hello 瀏覽器中的開發 IDE。</span><span class="sxs-lookup"><span data-stu-id="35efd-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="35efd-196">請注意 hello 經驗以下是在 Chrome 中。</span><span class="sxs-lookup"><span data-stu-id="35efd-196">Notice hello experience below is in Chrome.</span></span>
   
   ![Image24][image24]
10. <span data-ttu-id="35efd-198">您可以執行數個活動，例如編輯檔案、 新增檔案和資料夾，以及下載 hello 即時網站內容。</span><span class="sxs-lookup"><span data-stu-id="35efd-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="35efd-199">使快速編輯 toohello SamplePage.html 檔案。</span><span class="sxs-lookup"><span data-stu-id="35efd-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![Image25][image25]
11. <span data-ttu-id="35efd-201">在幾分鐘後，會自動儲存 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="35efd-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="35efd-202">如果您瀏覽後 toohello 頁面，您可以看到 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="35efd-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="35efd-203">請記住，這類即時編輯很可能不適用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="35efd-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="35efd-204">不過，hello 工具讓您可以非常輕易 toomake 快速變更的開發人員和測試環境。</span><span class="sxs-lookup"><span data-stu-id="35efd-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="35efd-207">移回 toohello 工具刀鋒視窗然後 hello 開發在分類底下，按一下 效能測試。</span><span class="sxs-lookup"><span data-stu-id="35efd-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![Image28][image28]
13. <span data-ttu-id="35efd-209">您需要 tooset team services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="35efd-209">You need tooset a team services account.</span></span> <span data-ttu-id="35efd-210">如需詳細資訊，請參閱此處︰ [建立 Team Services 帳戶](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="35efd-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="35efd-211">按一下新 toocreate 效能測試。</span><span class="sxs-lookup"><span data-stu-id="35efd-211">Click on New toocreate a performance test.</span></span>
    
    ![Image29][image29]
    
    <span data-ttu-id="35efd-213">設定 hello 各種值，然後按一下 執行於 hello 下方 hello 對話方塊 tooinitiate 效能測試的測試。</span><span class="sxs-lookup"><span data-stu-id="35efd-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![Image30][image30]
    
    ![Image31][image31]
15. <span data-ttu-id="35efd-216">一旦 hello 測試便會開始執行，您可以監視 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="35efd-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![Image32][image32]
    
    <span data-ttu-id="35efd-218">一旦 hello 測試完成時，按一下即可在 hello 結果顯示更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="35efd-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![Image33][image33]
16. <span data-ttu-id="35efd-220">在此範例中，您會建立小型測試回合，因此沒有有限的資料 tooanalyze，但是您可以查看各種度量，以及重新執行您的測試從這個檢視。</span><span class="sxs-lookup"><span data-stu-id="35efd-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="35efd-221">建立、 執行和分析簡單的程序的 web 效能測試，可讓 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="35efd-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="35efd-222">hello 以下螢幕擷取畫面顯示 hello 效能資料。</span><span class="sxs-lookup"><span data-stu-id="35efd-222">hello screenshots below display hello performance data.</span></span>
    
    ![Image34][image34]
    
    ![Image35][image35]
    
    ![Image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="35efd-226">監視和針對應用程式進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="35efd-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="35efd-227">Azure 提供許多用來監視和針對執行中應用程式進行疑難排解的功能。</span><span class="sxs-lookup"><span data-stu-id="35efd-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="35efd-228">在我們的 Web 應用程式的 hello Azure 入口網站中選擇 [工具]。</span><span class="sxs-lookup"><span data-stu-id="35efd-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![Image37][image37]
2. <span data-ttu-id="35efd-230">Hello 疑難排解類別 下方，注意到 hello 各種選擇的執行中應用程式中使用工具 tootroubleshoot 潛在問題。</span><span class="sxs-lookup"><span data-stu-id="35efd-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="35efd-231">您可以執行監視即時 HTTP 流量、啟用自我修復、檢視記錄檔等等的作業。</span><span class="sxs-lookup"><span data-stu-id="35efd-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![Image38][image38]
3. <span data-ttu-id="35efd-233">選擇網站度量 tooquickly get 某些 HTTP 代碼的檢視。</span><span class="sxs-lookup"><span data-stu-id="35efd-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="35efd-235">選擇 [診斷即服務]。</span><span class="sxs-lookup"><span data-stu-id="35efd-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="35efd-236">選擇 [應用程式類型]，然後選擇 [執行]。</span><span class="sxs-lookup"><span data-stu-id="35efd-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="35efd-238">隨即會開始收集。</span><span class="sxs-lookup"><span data-stu-id="35efd-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="35efd-240">您可以選擇 hello 適當記錄 toodiagnose 潛在問題。</span><span class="sxs-lookup"><span data-stu-id="35efd-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="35efd-241">您需要 tooenable 記錄 toosee，例如 HTTP 記錄檔中的所有 hello 可用資料的選項。</span><span class="sxs-lookup"><span data-stu-id="35efd-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="35efd-243">您可以下載並分析 DebugDiag hello 記憶體傾印檔案，即可分析報表 toohelp 尋找潛在問題。</span><span class="sxs-lookup"><span data-stu-id="35efd-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="35efd-245">tooview 更多資料，您需要 tooenable 額外的記錄功能。</span><span class="sxs-lookup"><span data-stu-id="35efd-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="35efd-246">在 hello Azure 入口網站，瀏覽 toohello Web 應用程式並選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="35efd-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="35efd-248">向下捲動 toohello 功能類別目錄，然後選擇 診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="35efd-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="35efd-250">請注意 hello 記錄的各種選項。</span><span class="sxs-lookup"><span data-stu-id="35efd-250">Notice hello various options for logging.</span></span> <span data-ttu-id="35efd-251">開啟 [Web 伺服器記錄]，並按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="35efd-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="35efd-253">移回 toohello hello 應用程式的工具區域並選擇 診斷 做為服務，然後按一下 執行 toorerun hello 資料收集。</span><span class="sxs-lookup"><span data-stu-id="35efd-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="35efd-255">啟用 hello HTTP 記錄設定，您現在會看到針對 HTTP 記錄檔中收集的資料。</span><span class="sxs-lookup"><span data-stu-id="35efd-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="35efd-257">按一下 hello HTML 檔案記錄檔，您就可以產生豐富的瀏覽器為基礎的報表做進一步調查。</span><span class="sxs-lookup"><span data-stu-id="35efd-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="35efd-259">移回 toohello 工具 > 一節中的 hello 應用程式的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="35efd-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="35efd-260">捲動 toohello 工具 > 一節，並選擇處理序總管。</span><span class="sxs-lookup"><span data-stu-id="35efd-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="35efd-262">藉由選擇處理序總管，您即可檢視執行中處理序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="35efd-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="35efd-263">通知低於您可以切入到處理程序，然後即使清除來自 hello Azure 入口網站的所有處理程序。</span><span class="sxs-lookup"><span data-stu-id="35efd-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="35efd-266">Hello 左移回 toohello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="35efd-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="35efd-267">按一下 [新增支援要求]。</span><span class="sxs-lookup"><span data-stu-id="35efd-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="35efd-269">Hello 刀鋒視窗上 hello 右中，從您可以填寫 hello 問題的詳細、 輸入人員連絡資訊，且即使上傳診斷資料。</span><span class="sxs-lookup"><span data-stu-id="35efd-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="35efd-270">hello Azure 入口網站可讓您使用 Microsoft 支援順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="35efd-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="35efd-273">hello Azure 入口網站可協助提供功能強大且熟悉的工具體驗 toohelp 監視和疑難排解執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="35efd-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="35efd-274">您也是可以 tootake 動作快速執行工作，例如回收處理程序、 啟用和停用各種資料集合，以及甚至整合與 Microsoft 專業人員支援。</span><span class="sxs-lookup"><span data-stu-id="35efd-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="35efd-275">一般應用程式管理</span><span class="sxs-lookup"><span data-stu-id="35efd-275">General Application Management</span></span>
<span data-ttu-id="35efd-276">當管理應用程式時，您通常需要 tooperform 各式各樣的活動，例如設定的備份策略、 實作和管理身分識別提供者，以及設定以角色為基礎的存取控制。</span><span class="sxs-lookup"><span data-stu-id="35efd-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="35efd-277">與 hello 其他 DevOps 體驗，如 hello Azure 平台整合直接在 hello 入口網站，這些工作。</span><span class="sxs-lookup"><span data-stu-id="35efd-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="35efd-278">保持的 tooensure hello Web 應用程式安全，防止資料遺失您需要 tooconfigure 備份。</span><span class="sxs-lookup"><span data-stu-id="35efd-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="35efd-279">瀏覽 toohello 設定 Web 應用程式 區域。</span><span class="sxs-lookup"><span data-stu-id="35efd-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="35efd-281">在 hello 刀鋒視窗上 hello 右中，捲動 toohello 功能類別。</span><span class="sxs-lookup"><span data-stu-id="35efd-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="35efd-283">選擇的備份。hello 右邊會開啟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="35efd-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="35efd-285">按一下 設定，從上 hello 右 hello 刀鋒視窗中選擇儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="35efd-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="35efd-287">現在建立，並選擇您的備份儲存體容器 toohold。</span><span class="sxs-lookup"><span data-stu-id="35efd-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="35efd-288">按一下 建立在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="35efd-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="35efd-289">然後，選取 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="35efd-289">Then select hello container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="35efd-291">一旦您已選擇 hello 容器，您可以設定排程，以及安裝備份為您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="35efd-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="35efd-292">此案例中，按一下儲存圖示 hello。</span><span class="sxs-lookup"><span data-stu-id="35efd-292">For this scenario, click hello save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="35efd-294">儲存之後，請備份捲動 hello 左側後 toohello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="35efd-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="35efd-295">按一下 立即備份 tooback hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="35efd-295">Click Backup Now tooback hello application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="35efd-297">幾分鐘後，您便會看到建立了備份。</span><span class="sxs-lookup"><span data-stu-id="35efd-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="35efd-298">請注意 hello 立即還原 hello 螢幕擷取畫面下方的選項。</span><span class="sxs-lookup"><span data-stu-id="35efd-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="35efd-300">按一下 立即還原，並檢查 hello 選項 toohello 刀鋒視窗上 hello 右。</span><span class="sxs-lookup"><span data-stu-id="35efd-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="35efd-301">您可以選擇適當的備份和輕鬆還原 tooan 先前狀態在必要時。</span><span class="sxs-lookup"><span data-stu-id="35efd-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="35efd-302">hello Azure 入口網站有幫助我們 hello 應用程式的簡單的災害復原策略，輕鬆啟用。</span><span class="sxs-lookup"><span data-stu-id="35efd-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="35efd-304">移回 toohello 設定 刀鋒視窗左側 hello，並在 功能，並選擇 驗證/授權。</span><span class="sxs-lookup"><span data-stu-id="35efd-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="35efd-306">在上 hello 右 hello 刀鋒視窗中選擇應用程式服務驗證。</span><span class="sxs-lookup"><span data-stu-id="35efd-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="35efd-307">請注意 hello 各種選項，您可以使用常用的提供者設定。</span><span class="sxs-lookup"><span data-stu-id="35efd-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="35efd-309">選擇您所選擇的 hello 提供者，並注意 hello hello 範圍選項。</span><span class="sxs-lookup"><span data-stu-id="35efd-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="35efd-310">您可以提供應用程式識別碼和應用程式密碼，以及快速啟用 hello 應用程式的 Facebook 驗證。</span><span class="sxs-lookup"><span data-stu-id="35efd-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="35efd-311">hello Azure 入口網站啟用驗證做為應用程式的周全的解決方案。</span><span class="sxs-lookup"><span data-stu-id="35efd-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="35efd-313">移回 toohello 設定 刀鋒視窗，然後選擇使用者 hello 資源管理類別之下。</span><span class="sxs-lookup"><span data-stu-id="35efd-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="35efd-315">在上 hello 右 hello 刀鋒視窗中檢查 hello 新增角色和使用者的各種選項。</span><span class="sxs-lookup"><span data-stu-id="35efd-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="35efd-316">hello Azure 入口網站可讓您輕鬆地 hello 應用程式，控制 RBAC （角色型存取控制）。</span><span class="sxs-lookup"><span data-stu-id="35efd-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="35efd-318">摘要</span><span class="sxs-lookup"><span data-stu-id="35efd-318">Summary</span></span>
<span data-ttu-id="35efd-319">本教學課程所示範一些 hello 電源以 hello Azure 平台快速啟用 web 應用程式中的連續部署，執行各種開發和測試活動、 監視與疑難排解即時應用程式，以及最後管理金鑰例如災害復原、 識別和以角色為基礎的存取控制策略。</span><span class="sxs-lookup"><span data-stu-id="35efd-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="35efd-320">hello Azure 平台可讓這些 DevOps 工作流程中，整合式的體驗，可有效率地在 hello 工作的內容中。</span><span class="sxs-lookup"><span data-stu-id="35efd-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35efd-321">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35efd-321">Next steps</span></span>
* <span data-ttu-id="35efd-322">Azure 資源管理員是很重要的 hello Azure 平台上啟用 DevOps。</span><span class="sxs-lookup"><span data-stu-id="35efd-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="35efd-323">toolearn 更造訪[Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="35efd-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="35efd-324">關於 Azure App Service 部署，請瀏覽的 toolearn[部署您的應用程式 tooAzure 應用程式服務](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="35efd-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
