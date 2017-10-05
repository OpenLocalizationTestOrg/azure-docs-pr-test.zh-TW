---
title: "教學課程︰DevOps 與 Azure 入口網站 | Microsoft Docs"
description: "了解 Azure 入口網站中的各種 DevOps 工作流程。"
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
ms.openlocfilehash: eec7d1402bdea4e5433c473dd713eed23aa80464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="a2474-103">教學課程︰DevOps 與 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a2474-103">Tutorial: DevOps with the Azure Portal</span></span>
<span data-ttu-id="a2474-104">Azure 平台充滿著彈性的 DevOps 工作流程。</span><span class="sxs-lookup"><span data-stu-id="a2474-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="a2474-105">在本教學課程中，您將會了解如何運用 Azure 入口網站的功能，來開發、測試、部署、疑難排解、監視和管理執行中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2474-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="a2474-106">本教學課程著重於下列內容︰</span><span class="sxs-lookup"><span data-stu-id="a2474-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="a2474-107">建立 Web 應用程式並啟用連續部署</span><span class="sxs-lookup"><span data-stu-id="a2474-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="a2474-108">開發和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="a2474-108">Develop and test an app</span></span>
3. <span data-ttu-id="a2474-109">監視和針對應用程式進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="a2474-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="a2474-110">一般應用程式管理工作</span><span class="sxs-lookup"><span data-stu-id="a2474-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="a2474-111">建立 Web 應用程式並啟用連續部署</span><span class="sxs-lookup"><span data-stu-id="a2474-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="a2474-112">請使用 [Azure App Service](https://azure.microsoft.com/services/app-service/)來建立 Web 應用程式，以用於本教學課程的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="a2474-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="a2474-113">一開始，您將會進行從原始程式碼儲存機制到執行中 Azure 環境的連續部署。</span><span class="sxs-lookup"><span data-stu-id="a2474-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="a2474-114">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a2474-114">Sign into the Azure Portal</span></span>
2. <span data-ttu-id="a2474-115">選擇 [應用程式服務] &gt; [新增圖示]並輸入名稱，選擇您的訂用帳戶，然後建立要作為服務容器的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="a2474-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="a2474-116">資源群組可讓您管理解決方案的各個層面，例如計費、部署和監視，而這一切全都可以透過 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)以單一群組的形式來進行。</span><span class="sxs-lookup"><span data-stu-id="a2474-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="a2474-118">幾分鐘後，您的 App Service 便會建立。</span><span class="sxs-lookup"><span data-stu-id="a2474-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="a2474-119">請花幾分鐘的時間在入口網站中探索服務的各種功能表選項。</span><span class="sxs-lookup"><span data-stu-id="a2474-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="a2474-121">按一下 URL。</span><span class="sxs-lookup"><span data-stu-id="a2474-121">Click the URL.</span></span> <span data-ttu-id="a2474-122">請注意工具和儲存機制的可用選項變化。</span><span class="sxs-lookup"><span data-stu-id="a2474-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="a2474-123">您也可以使用自己選擇的語言和架構，包括 .NET、Java 和 Ruby。</span><span class="sxs-lookup"><span data-stu-id="a2474-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="a2474-125">Azure 入口網站可讓連續部署變成只須執行幾個簡單步驟的輕鬆程序。</span><span class="sxs-lookup"><span data-stu-id="a2474-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="a2474-126">在 Azure 入口網站中，從您剛才建立的 App Service 的圖示中選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="a2474-126">In the Azure portal, choose settings from the icon for the app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="a2474-128">在右側開啟的刀鋒視窗中，捲動到 [發佈] 區段。</span><span class="sxs-lookup"><span data-stu-id="a2474-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="a2474-130">接著，進行一些設定，讓應用程式能夠進行連續部署。</span><span class="sxs-lookup"><span data-stu-id="a2474-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="a2474-131">按一下 [部署來源]，然後按一下 [選擇來源]。</span><span class="sxs-lookup"><span data-stu-id="a2474-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="a2474-132">請注意儲存機制來源所具有的選項變化。</span><span class="sxs-lookup"><span data-stu-id="a2474-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="a2474-134">在此範例中，請選擇 [GitHub]。</span><span class="sxs-lookup"><span data-stu-id="a2474-134">For this example choose GitHub.</span></span> <span data-ttu-id="a2474-135">選擇性地選擇您所選擇的儲存機制，並設定授權認證。</span><span class="sxs-lookup"><span data-stu-id="a2474-135">Optionally choose the repository of your choice and setup the authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="a2474-137">在授權給儲存機制之後，您接著可以選擇想要部署的專案和分支。</span><span class="sxs-lookup"><span data-stu-id="a2474-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="a2474-138">下面列出幾個虛構的範例。</span><span class="sxs-lookup"><span data-stu-id="a2474-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="a2474-140">在選擇專案和分支之後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a2474-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="a2474-141">您應該會開始看到部署通知。</span><span class="sxs-lookup"><span data-stu-id="a2474-141">You should start to see notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="a2474-143">瀏覽回到 GitHub，以查看為了整合原始檔控制存放庫與 Azure 而建立的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="a2474-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="a2474-144">只須進行一些簡單的步驟，Azure 入口網站即可與 GitHub 整合。</span><span class="sxs-lookup"><span data-stu-id="a2474-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="a2474-146">為了示範連續部署，請快速新增一些內容到儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a2474-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="a2474-147">如需簡單的範例，可將範例文字檔新增至 GitHub 存放庫。</span><span class="sxs-lookup"><span data-stu-id="a2474-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="a2474-148">您可以自由地使用 .NET、Ruby、Python 或其他某些類型的應用程式來搭配 App Service。</span><span class="sxs-lookup"><span data-stu-id="a2474-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="a2474-149">請隨意新增文字檔、ASP.NET MVC、Java 或 Ruby 應用程式到您選擇的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a2474-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="a2474-151">在對儲存機制認可變更之後，您會看到入口網站的通知區域中起始了新的部署。</span><span class="sxs-lookup"><span data-stu-id="a2474-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="a2474-152">在對儲存機制認可之後，如果沒快速看到變更，請按一下 [同步處理]。</span><span class="sxs-lookup"><span data-stu-id="a2474-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="a2474-154">此時，如果您嘗試並載入 App Service 頁面，可能會收到 403 錯誤。</span><span class="sxs-lookup"><span data-stu-id="a2474-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="a2474-155">在此範例中，這是由於頁面 (例如 index.htm 或 default.html 之類的檔案) 沒有典型的預設文件設定。</span><span class="sxs-lookup"><span data-stu-id="a2474-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="a2474-156">使用 Azure 入口網站中的工具，即可快速解決此問題。</span><span class="sxs-lookup"><span data-stu-id="a2474-156">You can quickly remedy this with the tooling in the Azure Portal.</span></span>  <span data-ttu-id="a2474-157">在 Azure 入口網站中，選擇 [設定] &gt; [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="a2474-157">In the Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="a2474-159">隨即會開啟 [應用程式設定] 的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2474-159">A blade opens for application settings.</span></span> <span data-ttu-id="a2474-160">輸入 “SamplePage.html” 頁面的名稱，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a2474-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="a2474-161">花幾分鐘的時間探索其他設定。</span><span class="sxs-lookup"><span data-stu-id="a2474-161">Take a few minutes to explore the other settings.</span></span>
    
    ![Image14][image14]
15. <span data-ttu-id="a2474-163">選擇性地重新整理瀏覽器 URL，以確保您會看到預期的變更。</span><span class="sxs-lookup"><span data-stu-id="a2474-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="a2474-164">在本例中，還有一些簡單的文字現在正在填入頁面。</span><span class="sxs-lookup"><span data-stu-id="a2474-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="a2474-165">儲存機制的每項額外變更都會導致進行新的自動部署。</span><span class="sxs-lookup"><span data-stu-id="a2474-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![Image15][image15]
    
    <span data-ttu-id="a2474-167">透過 Azure 入口網站啟用連續部署是很輕鬆的體驗。</span><span class="sxs-lookup"><span data-stu-id="a2474-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span></span> <span data-ttu-id="a2474-168">您也可以建置更複雜的發行管線，並搭配現有原始檔控制和連續整合系統，使用其他許多技術來部署至 Azure，例如運用自動化建置和發行管理系統。</span><span class="sxs-lookup"><span data-stu-id="a2474-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="a2474-169">開發和測試應用程式</span><span class="sxs-lookup"><span data-stu-id="a2474-169">Develop and test an app</span></span>
<span data-ttu-id="a2474-170">接下來，對程式碼基底進行一些變更，並快速部署這些變更。</span><span class="sxs-lookup"><span data-stu-id="a2474-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="a2474-171">您也會針對 Web 應用程式設定一些效能測試。</span><span class="sxs-lookup"><span data-stu-id="a2474-171">You will also setup up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="a2474-172">在 Azure 入口網站中，從瀏覽窗格選擇應用程式服務，並找到您的 App Service。</span><span class="sxs-lookup"><span data-stu-id="a2474-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![Image16][image16]
2. <span data-ttu-id="a2474-174">按一下 [工具]</span><span class="sxs-lookup"><span data-stu-id="a2474-174">Click Tools</span></span>
   
   ![Image17][image17]
3. <span data-ttu-id="a2474-176">注意 [工具] 底下的 [開發] 類別。</span><span class="sxs-lookup"><span data-stu-id="a2474-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="a2474-177">這裡有幾個實用的工具，可供我們使用應用程式，但不需要離開 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a2474-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span></span> <span data-ttu-id="a2474-178">按一下 [主控台]。</span><span class="sxs-lookup"><span data-stu-id="a2474-178">Click on Console.</span></span>
   
   ![Image18][image18]
4. <span data-ttu-id="a2474-180">在 [主控台] 視窗中，您可以為您的應用程式發出即時命令。</span><span class="sxs-lookup"><span data-stu-id="a2474-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="a2474-181">輸入 dir 命令，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="a2474-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="a2474-182">請注意，需要較高權限的命令不會運作。</span><span class="sxs-lookup"><span data-stu-id="a2474-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![Image19][image19]
5. <span data-ttu-id="a2474-184">回到 [開發] 類別，然後選擇 [Visual Studio Online]。</span><span class="sxs-lookup"><span data-stu-id="a2474-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="a2474-185">注意：Visual Studio Online 現已更名為 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="a2474-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![Image20][image20]
6. <span data-ttu-id="a2474-187">開啟應用程式的瀏覽器中編輯體驗。</span><span class="sxs-lookup"><span data-stu-id="a2474-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![Image21][image21]
7. <span data-ttu-id="a2474-189">隨即會為應用程式安裝 Web 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="a2474-189">A web extension installs for your app.</span></span> <span data-ttu-id="a2474-190">擴充功能可快速且輕鬆地將功能新增至 Azure 中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2474-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="a2474-191">請注意以下螢幕擷取畫面中可用的一些其他擴充功能類型。</span><span class="sxs-lookup"><span data-stu-id="a2474-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![Image22][image22]
8. <span data-ttu-id="a2474-193">在安裝 Visual Studio Online 擴充功能之後，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="a2474-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![Image23][image23]
9. <span data-ttu-id="a2474-195">隨即會開啟瀏覽器索引標籤，供您直接在瀏覽器中看到開發 IDE。</span><span class="sxs-lookup"><span data-stu-id="a2474-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="a2474-196">請注意，下面的體驗是在 Chrome 中。</span><span class="sxs-lookup"><span data-stu-id="a2474-196">Notice the experience below is in Chrome.</span></span>
   
   ![Image24][image24]
10. <span data-ttu-id="a2474-198">您可以執行數個活動，例如編輯檔案、新增檔案與資料夾，以及從即時網站下載內容。</span><span class="sxs-lookup"><span data-stu-id="a2474-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="a2474-199">快速編輯 SamplePage.html 檔案。</span><span class="sxs-lookup"><span data-stu-id="a2474-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![Image25][image25]
11. <span data-ttu-id="a2474-201">幾分鐘後，便會自動儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a2474-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="a2474-202">如果您往回瀏覽至網頁，就可以看到變更。</span><span class="sxs-lookup"><span data-stu-id="a2474-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="a2474-203">請記住，這類即時編輯很可能不適用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="a2474-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="a2474-204">不過，這些工具可以輕易地快速變更開發和測試環境。</span><span class="sxs-lookup"><span data-stu-id="a2474-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="a2474-207">回到 [工具] 刀鋒視窗，然後按一下 [開發] 類別下的 [效能測試]。</span><span class="sxs-lookup"><span data-stu-id="a2474-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![Image28][image28]
13. <span data-ttu-id="a2474-209">您需要設定 Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2474-209">You need to set a team services account.</span></span> <span data-ttu-id="a2474-210">如需詳細資訊，請參閱此處︰ [建立 Team Services 帳戶](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="a2474-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="a2474-211">按一下 [新增] 以建立效能測試。</span><span class="sxs-lookup"><span data-stu-id="a2474-211">Click on New to create a performance test.</span></span>
    
    ![Image29][image29]
    
    <span data-ttu-id="a2474-213">設定各種值，然後按一下對話方塊底部的 [執行測試] 以起始效能測試。</span><span class="sxs-lookup"><span data-stu-id="a2474-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![Image30][image30]
    
    ![Image31][image31]
15. <span data-ttu-id="a2474-216">在測試開始執行之後，您可以監視狀態。</span><span class="sxs-lookup"><span data-stu-id="a2474-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![Image32][image32]
    
    <span data-ttu-id="a2474-218">在測試完成時，按一下結果以顯示詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a2474-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![Image33][image33]
16. <span data-ttu-id="a2474-220">在此範例中，您建立了小型測試執行，所以可供分析的資料有限，但您可以查看各種度量，以及從這個檢視重新執行測試。</span><span class="sxs-lookup"><span data-stu-id="a2474-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="a2474-221">Azure 入口網站可以讓建立、執行和分析 Web 效能測試變成簡單的程序。</span><span class="sxs-lookup"><span data-stu-id="a2474-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="a2474-222">以下螢幕擷取畫面會顯示效能資料。</span><span class="sxs-lookup"><span data-stu-id="a2474-222">The screenshots below display the performance data.</span></span>
    
    ![Image34][image34]
    
    ![Image35][image35]
    
    ![Image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="a2474-226">監視和針對應用程式進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="a2474-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="a2474-227">Azure 提供許多用來監視和針對執行中應用程式進行疑難排解的功能。</span><span class="sxs-lookup"><span data-stu-id="a2474-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="a2474-228">在我們的 Web 應用程式的 Azure 入口網站中選擇 [工具]。</span><span class="sxs-lookup"><span data-stu-id="a2474-228">In the Azure Portal for our Web app choose Tools.</span></span>
   
   ![Image37][image37]
2. <span data-ttu-id="a2474-230">在 [疑難排解] 類別下，請注意各種使用工具來針對執行中應用程式潛在問題進行疑難排解的選項。</span><span class="sxs-lookup"><span data-stu-id="a2474-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="a2474-231">您可以執行監視即時 HTTP 流量、啟用自我修復、檢視記錄檔等等的作業。</span><span class="sxs-lookup"><span data-stu-id="a2474-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![Image38][image38]
3. <span data-ttu-id="a2474-233">選擇 [網站度量]，快速檢視某些 HTTP 代碼。</span><span class="sxs-lookup"><span data-stu-id="a2474-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="a2474-235">選擇 [診斷即服務]。</span><span class="sxs-lookup"><span data-stu-id="a2474-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="a2474-236">選擇 [應用程式類型]，然後選擇 [執行]。</span><span class="sxs-lookup"><span data-stu-id="a2474-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="a2474-238">隨即會開始收集。</span><span class="sxs-lookup"><span data-stu-id="a2474-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="a2474-240">您可以選擇適當的記錄檔來診斷潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="a2474-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="a2474-241">您必須啟用記錄功能，才能查看所有可用的資料選項，例如 HTTP 記錄。</span><span class="sxs-lookup"><span data-stu-id="a2474-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="a2474-243">按一下 [記憶體傾印] 檔案，即可下載並分析 DebugDiag 分析報告，以協助找出潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="a2474-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="a2474-245">若要檢視更多資料，您必須啟用其他記錄功能。</span><span class="sxs-lookup"><span data-stu-id="a2474-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="a2474-246">在 Azure 入口網站中，瀏覽至 Web 應用程式並選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="a2474-246">In the Azure Portal, navigate to the Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="a2474-248">向下捲動至 [功能] 類別，並選擇 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="a2474-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="a2474-250">請注意記錄功能的各種選項。</span><span class="sxs-lookup"><span data-stu-id="a2474-250">Notice the various options for logging.</span></span> <span data-ttu-id="a2474-251">開啟 [Web 伺服器記錄]，並按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a2474-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="a2474-253">回到應用程式的工具區域，並選擇 [診斷即服務]，然後按一下 [執行] 以重新執行資料收集。</span><span class="sxs-lookup"><span data-stu-id="a2474-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="a2474-255">在啟用 HTTP 記錄設定的情況下，您現在會看到針對 HTTP 記錄收集的資料。</span><span class="sxs-lookup"><span data-stu-id="a2474-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="a2474-257">按一下 HTML 檔案記錄，就會產生豐富的瀏覽器型報告，以便進行進一步的調查。</span><span class="sxs-lookup"><span data-stu-id="a2474-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="a2474-259">回到應用程式在 Azure 入口網站中的 [工具] 區段。</span><span class="sxs-lookup"><span data-stu-id="a2474-259">Move back to the tools section in the Azure Portal for the app.</span></span> <span data-ttu-id="a2474-260">捲動至 [工具] 區段，然後選擇 [處理序總管]。</span><span class="sxs-lookup"><span data-stu-id="a2474-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="a2474-262">藉由選擇處理序總管，您即可檢視執行中處理序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a2474-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="a2474-263">請注意下面，您可以深入探索處理序，甚至是刪除處理序，全都透過 Azure 入口網站來進行。</span><span class="sxs-lookup"><span data-stu-id="a2474-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="a2474-266">回到左側的 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2474-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="a2474-267">按一下 [新增支援要求]。</span><span class="sxs-lookup"><span data-stu-id="a2474-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="a2474-269">在右側的刀鋒視窗中，您可以填寫問題的詳細資料、輸入連絡人資訊，甚至是上傳診斷資料。</span><span class="sxs-lookup"><span data-stu-id="a2474-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="a2474-270">Azure 入口網站可讓使用 Microsoft 支援變成順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="a2474-270">The Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="a2474-273">Azure 入口網站可協助提供強大且熟悉的工具體驗，來協助監視和針對執行中的應用程式進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="a2474-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="a2474-274">您也可以透過執行各種工作，例如回收處理序、啟用和停用各種資料收集，甚至是與 Microsoft 專業支援服務整合，以快速地採取行動。</span><span class="sxs-lookup"><span data-stu-id="a2474-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="a2474-275">一般應用程式管理</span><span class="sxs-lookup"><span data-stu-id="a2474-275">General Application Management</span></span>
<span data-ttu-id="a2474-276">在管理應用程式時，您經常必須執行各式各樣的活動，例如設定備份策略、實作和管理識別提供者，以及設定角色型存取控制。</span><span class="sxs-lookup"><span data-stu-id="a2474-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="a2474-277">和其他 DevOps 體驗一樣，Azure 平台會將這些工作直接整合到入口網站。</span><span class="sxs-lookup"><span data-stu-id="a2474-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="a2474-278">為了確保 Web 應用程式安全無虞，不會遺失資料，您必須設定備份。</span><span class="sxs-lookup"><span data-stu-id="a2474-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="a2474-279">請瀏覽至 Web 應用程式的 [設定] 區域。</span><span class="sxs-lookup"><span data-stu-id="a2474-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="a2474-281">在右側的刀鋒視窗中，向下捲動至 [功能] 類別。</span><span class="sxs-lookup"><span data-stu-id="a2474-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="a2474-283">選擇 [備份]；右側隨即會開啟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2474-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="a2474-285">按一下 [設定]，在右側的刀鋒視窗中選擇儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2474-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="a2474-287">現在，建立並選擇儲存體容器以保存備份。</span><span class="sxs-lookup"><span data-stu-id="a2474-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="a2474-288">按一下刀鋒視窗底部的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a2474-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="a2474-289">然後選取容器。</span><span class="sxs-lookup"><span data-stu-id="a2474-289">Then select the container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="a2474-291">在選擇容器之後，即可設定排程，以及設定資料庫的備份。</span><span class="sxs-lookup"><span data-stu-id="a2474-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="a2474-292">在此案例中，按一下 [儲存] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a2474-292">For this scenario, click the save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="a2474-294">在儲存之後，往回捲動至位於左側的刀鋒視窗來找到 [備份]。</span><span class="sxs-lookup"><span data-stu-id="a2474-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="a2474-295">按一下 [立即備份] 以備份應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2474-295">Click Backup Now to back the application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="a2474-297">幾分鐘後，您便會看到建立了備份。</span><span class="sxs-lookup"><span data-stu-id="a2474-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="a2474-298">請注意以下螢幕擷取畫面上的 [立即還原] 選項。</span><span class="sxs-lookup"><span data-stu-id="a2474-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="a2474-300">按一下 [立即還原]，並檢查右側的刀鋒視窗選項。</span><span class="sxs-lookup"><span data-stu-id="a2474-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="a2474-301">您可以選擇適當的備份，並視需要輕鬆地還原成先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="a2474-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="a2474-302">Azure 入口網站已幫助我們輕鬆地啟用應用程式的簡單災害復原策略。</span><span class="sxs-lookup"><span data-stu-id="a2474-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="a2474-304">回到左側的 [設定] 刀鋒視窗，並選擇 [功能] 底下的 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="a2474-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="a2474-306">在右側的刀鋒視窗中，選擇 [App Service 驗證]。</span><span class="sxs-lookup"><span data-stu-id="a2474-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="a2474-307">請注意您可以針對熱門提供者設定的各種選項。</span><span class="sxs-lookup"><span data-stu-id="a2474-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="a2474-309">選擇您所選擇的提供者，並注意該範圍的選項。</span><span class="sxs-lookup"><span data-stu-id="a2474-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="a2474-310">您可以提供 [應用程式識別碼] 與 [應用程式密碼]，並快速啟用應用程式的 Facebook 驗證。</span><span class="sxs-lookup"><span data-stu-id="a2474-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="a2474-311">Azure 入口網站可讓驗證做為應用程式的周全解決方案。</span><span class="sxs-lookup"><span data-stu-id="a2474-311">The Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="a2474-313">回到 [設定] 刀鋒視窗，並選擇 [資源管理] 類別底下的 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="a2474-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="a2474-315">在右側的刀鋒視窗中，檢查各種用來新增角色和使用者的選項。</span><span class="sxs-lookup"><span data-stu-id="a2474-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="a2474-316">Azure 入口網站可讓您輕鬆控制應用程式的 RBAC (角色型存取控制)。</span><span class="sxs-lookup"><span data-stu-id="a2474-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="a2474-318">摘要</span><span class="sxs-lookup"><span data-stu-id="a2474-318">Summary</span></span>
<span data-ttu-id="a2474-319">本教學課程透過快速啟用 Web 應用程式的連續部署、執行各種開發和測試活動、監視和針對 Live App 進行疑難排解，以及最終管理金鑰策略 (例如災害復原、身分識別和角色型存取控制)，示範了 Azure 平台的部分功能。</span><span class="sxs-lookup"><span data-stu-id="a2474-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="a2474-320">Azure 平台可讓這些 DevOps 工作流程獲得整合的體驗，而且您可以透過讓手邊的工作保持在環境中而能有效率地工作。</span><span class="sxs-lookup"><span data-stu-id="a2474-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2474-321">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2474-321">Next steps</span></span>
* <span data-ttu-id="a2474-322">Azure Resource Manager 對於在 Azure 平台上啟用 DevOps 來說至關重要。</span><span class="sxs-lookup"><span data-stu-id="a2474-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="a2474-323">若要深入了解，請造訪 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a2474-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="a2474-324">若要深入了解 Azure App Service 部署，請瀏覽 [將您的應用程式部署至 Azure App Service](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="a2474-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span></span>

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
