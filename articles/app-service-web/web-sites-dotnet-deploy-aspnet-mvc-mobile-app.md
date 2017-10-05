---
title: "在 Azure App Service 中部署 ASP.NET MVC 5 行動 Web 應用程式"
description: "指導您如何使用 ASP.NET MVC 5 Web 應用程式的行動功能，將 Web 應用程式部署到 Azure App Service 的教學課程。"
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: c98e9b485c52a82e5be5c0f6b0b67912d1e890b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="1e1a0-103">在 Azure App Service 中部署 ASP.NET MVC 5 行動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e1a0-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="1e1a0-104">本教學課程指導您如何建置行動便利的 ASP.NET MVC 5 Web 應用程式，並將其部署至 Azure App Service 的基本做法。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span></span> <span data-ttu-id="1e1a0-105">在本教學課程中，您需要 [Visual Studio Express 2013 for Web][Visual Studio Express 2013] 或 Professional Edition 的 Visual Studio (如果您已具備此版本)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="1e1a0-106">您可以使用 [Visual Studio 2015] ，但螢幕擷取畫面將會不同，且您必須使用 ASP.NET 4.x 範本。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="1e1a0-107">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="1e1a0-107">What You'll Build</span></span>
<span data-ttu-id="1e1a0-108">在本教學課程中，您將把行動功能新增至[入門專案][StarterProject]裡提供的簡單會議清單應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span></span> <span data-ttu-id="1e1a0-109">如同在 Internet Explorer 11 F12 開發人員工具的瀏覽器模擬器中所見，以下螢幕擷取畫面示範完成的應用程式中的 ASP.NET 工作階段。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="1e1a0-110">您可以利用 Internet Explorer 11 F12 開發人員工具和 [Fiddler 工具][Fiddler]來偵錯應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="1e1a0-111">您要學習的技術</span><span class="sxs-lookup"><span data-stu-id="1e1a0-111">Skills You'll Learn</span></span>
<span data-ttu-id="1e1a0-112">以下是您要學習的內容：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="1e1a0-113">如何使用 Visual Studio 2013，將 Web 應用程式直接發行到 Azure App Service 中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span></span>
* <span data-ttu-id="1e1a0-114">ASP.NET MVC 5 範本如何使用 CSS Bootstrap 架構，改善行動裝置的顯示畫面。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="1e1a0-115">如何以特定的行動瀏覽器做為目標，建立行動專用的檢視，例如 iPhone 和 Android。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span></span>
* <span data-ttu-id="1e1a0-116">如何建立回應靈敏的檢視 (可回應各種裝置中不同瀏覽器的檢視)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-116">How to create responsive views (views that respond to different browsers across devices)</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="1e1a0-117">設定開發環境</span><span class="sxs-lookup"><span data-stu-id="1e1a0-117">Set up the development environment</span></span>
<span data-ttu-id="1e1a0-118">安裝 Azure SDK for .NET 2.5.1 或更新版本，以設定您的開發環境。 </span><span class="sxs-lookup"><span data-stu-id="1e1a0-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="1e1a0-119">若要安裝 Azure SDK for .NET，請按一下底下連結：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-119">To install the Azure SDK for .NET, click the link below.</span></span> <span data-ttu-id="1e1a0-120">如果您尚未安裝 Visual Studio 2013，按下該連結會進行安裝。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span></span> <span data-ttu-id="1e1a0-121">本教學課程需要 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="1e1a0-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="1e1a0-123">在 [Web Platform Installer] 視窗中，按一下 [安裝]  並繼續進行安裝。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span></span>

<span data-ttu-id="1e1a0-124">您還需要一個行動瀏覽器模擬器。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="1e1a0-125">下列任一項目都可使用：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-125">Any of the following will work:</span></span>

* <span data-ttu-id="1e1a0-126">[Internet Explorer 11 F12 開發人員工具][EmulatorIE11]中的瀏覽器模擬器 (使用於所有行動瀏覽器螢幕擷取畫面中)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="1e1a0-127">它具有 Windows Phone 8、Windows Phone 7 和 Apple iPad 的使用者代理程式字串預設項目。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="1e1a0-128">[Google Chrome DevTools][EmulatorChrome] (英文) 中的瀏覽器模擬器。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="1e1a0-129">它包含許多 Android 裝置，以及 Apple iPhone、Apple iPad 和 Amazon Kindle Fire 的預設項目。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="1e1a0-130">它也會模擬觸控事件。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-130">It also emulates touch events.</span></span>
* <span data-ttu-id="1e1a0-131">[Opera Mobile 模擬器][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="1e1a0-132">此處提供具有 C\# 原始程式碼的 Visual Studio 專案來幫助您完成本主題：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-132">Visual Studio projects with C\# source code are available to accompany this topic:</span></span>

* <span data-ttu-id="1e1a0-133">[入門專案下載][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="1e1a0-134">[完成專案下載][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="1e1a0-135"><a name="bkmk_DeployStarterProject"></a>將入門專案部署至 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e1a0-135"><a name="bkmk_DeployStarterProject"></a>Deploy the starter project to an Azure web app</span></span>
1. <span data-ttu-id="1e1a0-136">下載會議清單應用程式[入門專案][StarterProject] (英文)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-136">Download the conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="1e1a0-137">接著在 Windows 檔案總管中，以滑鼠右鍵按一下以下載的 ZIP 檔案並選擇 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="1e1a0-138">在 [內容] 對話方塊中，選擇 [解除封鎖] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-138">In the **Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="1e1a0-139">(取消封鎖後，當您嘗試使用從網路下載的 .zip 檔案時，就不會出現安全性警告。)</span><span class="sxs-lookup"><span data-stu-id="1e1a0-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>
4. <span data-ttu-id="1e1a0-140">以滑鼠右鍵按一下 ZIP 檔案並選取 [全部解壓縮]  來解壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span></span> 
5. <span data-ttu-id="1e1a0-141">在 Visual Studio 中，開啟 C#\Mvc5Mobile.sln 檔案。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="1e1a0-142">在 [方案總管] 中，於專案上按一下滑鼠右鍵，再按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-142">In Solution Explorer, right-click the project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="1e1a0-143">在 [發佈 Web] 中，按一下 [Microsoft Azure App Service] 。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="1e1a0-144">如果您尚未登入 Azure，請按一下 [新增帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="1e1a0-145">依照提示來登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-145">Follow the prompts to log into your Azure account.</span></span>
10. <span data-ttu-id="1e1a0-146">[App Service] 對話方塊現在應該會顯示您已登入。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-146">The App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="1e1a0-147">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="1e1a0-148">在 [Web 應用程式名稱]  欄位中，指定唯一的應用程式名稱前置詞。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-148">In the **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="1e1a0-149">您的完整 Web 應用程式名稱將是 &lt;prefix>.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="1e1a0-150">另外，請在 [資源群組] 中選取或指定新的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="1e1a0-151">然後，按一下 [新增]  來建立新的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-151">Then, click **New** to create a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="1e1a0-152">設定新的 App Service 方案並按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-152">Configure the new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="1e1a0-153">返回 [建立 App Service] 對話方塊中，按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-153">Back in the Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="1e1a0-154">Azure 資源建立之後，隨即會將新應用程式的設定填入 [發佈 Web] 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span></span> <span data-ttu-id="1e1a0-155">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="1e1a0-156">當 Visual Studio 完成將入門專案發行至 Azure Web 應用程式之後，隨即會開啟桌面瀏覽器以顯示作用中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span></span>
15. <span data-ttu-id="1e1a0-157">啟動行動瀏覽器模擬器，將會議應用程式的 URL (*<prefix>*.azurewebsites.net) 複製到模擬器中，然後按一下右上角的按鈕，並選取 [ **依標籤瀏覽**]。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="1e1a0-158">若您使用 Internet Explorer 11 做為預設瀏覽器，只要輸入 `F12`，再按鍵 `Ctrl+8`，然後將瀏覽器設定檔變更為 **Windows Phone** 即可。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span></span> <span data-ttu-id="1e1a0-159">下圖顯示直向模式的 *AllTags* 檢視 (透過選擇 [ **依標籤瀏覽**])。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="1e1a0-160">當您在 Visual Studio 中偵錯 MVC 5 應用程式時，可以再次將 Web 應用程式發行至 Azure，直接從行動瀏覽器或瀏覽器模擬器確認作用中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="1e1a0-161">該顯示內容在行動裝置上非常清楚易讀。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-161">The display is very readable on a mobile device.</span></span> <span data-ttu-id="1e1a0-162">您也可以看到一些 Bootstrap CSS 架構所套用的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span></span>
<span data-ttu-id="1e1a0-163">按一下 [ **ASP.NET** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-163">Click the **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="1e1a0-164">ASP.NET 標籤檢視會縮放至適合螢幕的大小，而這是 Bootstrap 自動為您執行的效果。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="1e1a0-165">但您可以改善此檢視，使其更適合行動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-165">However, you can improve this view to better suit the mobile browser.</span></span> <span data-ttu-id="1e1a0-166">例如，[ **日期** ] 欄非常難以閱讀。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-166">For example, the **Date** column is difficult to read.</span></span> <span data-ttu-id="1e1a0-167">您將在稍後的教學課程中變更 *AllTags* 檢視，使其更適合行動用途。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span></span>

## <span data-ttu-id="1e1a0-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS 架構</span><span class="sxs-lookup"><span data-stu-id="1e1a0-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="1e1a0-169">MVC 5 範本中的新功能是內建的 Bootstrap 支援。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-169">New in the MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="1e1a0-170">您已經看到它是如何即時改善應用程式中的不同檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-170">You have already seen how it immediately improves the different views in your application.</span></span> <span data-ttu-id="1e1a0-171">例如，頂端的導覽列會在瀏覽器寬度較小時自動摺疊。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span></span> <span data-ttu-id="1e1a0-172">嘗試在桌面瀏覽器上重新調整瀏覽器視窗的大小，並觀察導覽列如何改變它的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span></span> <span data-ttu-id="1e1a0-173">這就是內建於 Bootstrap 中回應靈敏的 Web 設計。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-173">This is the responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="1e1a0-174">若要查看 Web 應用程式沒有 Bootstrap 時的外觀，請開啟 App\_Start\\BundleConfig.cs，並註解化包含 bootstrap.js 和 bootstrap.css 的行。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="1e1a0-175">以下程式碼顯示在執行這些變更之後， `RegisterBundles` 方法的最後兩個陳述式：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="1e1a0-176">按下 `Ctrl+F5` 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-176">Press `Ctrl+F5` to run the application.</span></span>

<span data-ttu-id="1e1a0-177">您會發現可摺疊的導覽列現在只是一般的未排序清單。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="1e1a0-178">再按一下 [依標籤瀏覽]，然後按一下 [ASP.NET]。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="1e1a0-179">您現在可以在行動模擬器檢視中看到檢視已不再縮放至適合螢幕的大小，且您必須橫向捲動才能看到右邊的表格。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="1e1a0-180">復原這些變更，並重新整理行動瀏覽器，以確認適合行動的顯示畫面已還原。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="1e1a0-181">Bootstrap 並非專屬於 ASP.NET MVC 5，您也可以在所有 Web 應用程式中利用這些功能。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="1e1a0-182">但它目前內建於 ASP.NET MVC 5 專案範本中，所以 MVC 5 Web 應用程式可根據預設利用 Bootstrap。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="1e1a0-183">如需 Bootstrap 的詳細資訊，請移至 [Bootstrap][BootstrapSite] 網站。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="1e1a0-184">您將在下一節看到如何提供行動瀏覽器專用的檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-184">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <span data-ttu-id="1e1a0-185"><a name="bkmk_overrideviews"></a> 覆寫檢視、配置與部分檢視</span><span class="sxs-lookup"><span data-stu-id="1e1a0-185"><a name="bkmk_overrideviews"></a> Override the Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="1e1a0-186">您可以覆寫大多數的行動瀏覽器、個別行動瀏覽器或任何特定瀏覽器的所有檢視，包含配置及部分檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="1e1a0-187">若要提供行動裝置專屬的檢視，您可以複製檢視檔案並將 *.Mobile* 新增至檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="1e1a0-188">例如，若要建立行動 [索引] 檢視，您可以將 Views\\Home\\Index.cshtml 複製到 Views\\Home\\Index.Mobile.cshtml。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="1e1a0-189">本節將建立行動裝置專屬的配置檔案。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="1e1a0-190">一開始，請將 Views\\Shared\\\_Layout.cshtml 複製到 Views\\Shared\\\_Layout.Mobile.cshtml。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="1e1a0-191">開啟 \_Layout.Mobile.cshtml，並將標題從 **MVC5 Application** 變更為 **MVC5 Application (Mobile)**。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="1e1a0-192">在每個導覽列的 `Html.ActionLink` 呼叫當中，移除每個 *ActionLink*連結中的「Browse by」。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="1e1a0-193">以下程式碼顯示行動配置檔案的已完成之 `<ul class="nav navbar-nav">` 標籤。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="1e1a0-194">將 Views\\Home\\AllTags.cshtml 檔案複製到 Views\\Home\\AllTags.Mobile.cshtml。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="1e1a0-195">開啟新檔案並將 `<h2>` 元素從 "Tags" 變更為 "Tags (M)"：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="1e1a0-196">使用桌面瀏覽器及行動瀏覽器模擬器，瀏覽至標籤頁面。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="1e1a0-197">行動瀏覽器模擬器會顯示您執行的兩項變更 (\_Layout.Mobile.cshtml 的標題及 AllTags.Mobile.cshtml 的標題)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="1e1a0-198">相較之下，桌面顯示則沒有變更 (\_Layout.cshtml 和 AllTags.cshtml 的標題)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="1e1a0-199"><a name="bkmk_browserviews"></a> 建立瀏覽器專用的檢視</span><span class="sxs-lookup"><span data-stu-id="1e1a0-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="1e1a0-200">除了行動與桌面專用的檢視之外，您還可以為個別瀏覽器建立檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="1e1a0-201">例如，您可以為 iPhone 或 Android 瀏覽器建立專用的檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span></span> <span data-ttu-id="1e1a0-202">在本節中，您要建立 iPhone 瀏覽器的配置，以及 iPhone 版的 *AllTags* 檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="1e1a0-203">開啟 Global.asax 檔案，並將以下程式碼加入 `Application_Start` 方法的底部。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="1e1a0-204">此程式碼會定義要比對每個連入要求且名為 "iPhone" 的新顯示模式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="1e1a0-205">若連入的要求符合您定義的條件 (亦即使用者代理程式包含 "iPhone" 字串)，則 ASP.NET MVC 會尋找名稱包含 "iPhone" 字尾的檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="1e1a0-206">新增行動瀏覽器專用的顯示模式時，例如 iPhone 和 Android，請務必將第一個引數設為 `0` (插入於清單的頂端)，才能確保瀏覽器的專用模式會優先於行動範本 (*.Mobile.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="1e1a0-207">若位於清單頂端的是行動範本，則會優先選取該行動範本，而不是您想要的顯示模式 (第一個相符的會成功，而行動範本符合所有行動瀏覽器)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="1e1a0-208">以滑鼠右鍵按一下程式碼的 `DefaultDisplayMode`，選擇 [解析]，然後選擇 `using System.Web.WebPages;`。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="1e1a0-209">這麼做會將參考加入定義 `DisplayModeProvider` 和 `DefaultDisplayMode` 類型的 `System.Web.WebPages` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="1e1a0-210">或者，您可以手動將以下的行加入檔案的 `using` 區段即可。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="1e1a0-211">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-211">Save the changes.</span></span> <span data-ttu-id="1e1a0-212">將 Views\\Shared\\\_Layout.Mobile.cshtml 檔案複製到 Views\\Shared\\\_Layout.iPhone.cshtml。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="1e1a0-213">開啟新檔案，然後將標題從 `MVC5 Application (Mobile)` 變更為 `MVC5 Application (iPhone)`。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="1e1a0-214">將 Views\\Home\\AllTags.Mobile.cshtml 檔案複製到 Views\\Home\\AllTags.iPhone.cshtml。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="1e1a0-215">在新檔案中，將 `<h2>` 元素從「Tags (M)」變更為「Tags (iPhone)」。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="1e1a0-216">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-216">Run the application.</span></span> <span data-ttu-id="1e1a0-217">執行行動瀏覽器模擬器，請確認其使用者代理程式設為「iPhone」，然後瀏覽至 *AllTags* 檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="1e1a0-218">若您使用 Internet Explorer 11 F12 開發人員工具中的模擬器，請將模擬設為以下內容：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span></span>

* <span data-ttu-id="1e1a0-219">瀏覽器設定檔 = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="1e1a0-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="1e1a0-220">使用者代理程式字串 =  **Custom**</span><span class="sxs-lookup"><span data-stu-id="1e1a0-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="1e1a0-221">自訂字串 = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="1e1a0-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="1e1a0-222">以下螢幕擷取畫面顯示在 Internet Explorer 11 F12 開發人員工具的模擬器中，使用自訂使用者代理程式字串 (此為 iPhone 5C 使用者代理程式字串) 呈現的 *AllTags* 檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="1e1a0-223">在行動瀏覽器中，選取 [演講者] 連結。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-223">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="1e1a0-224">由於沒有行動檢視 (AllSpeakers.Mobile.cshtml)，預設的演講者檢視 (AllSpeakers.cshtml) 會透過行動配置檢視 (\_Layout.Mobile.cshtml) 來呈現。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="1e1a0-225">如下所示，標題 **MVC5 Application (Mobile)** 定義於 \_Layout.Mobile.cshtml 中。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="1e1a0-226">您可以在 Views\\\_ViewStart.cshtml 檔案中，將 `RequireConsistentDisplayMode` 設為 `true`，即可全域停用預設 (非行動) 檢視，使其無法在行動配置內呈現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="1e1a0-227">當 `RequireConsistentDisplayMode` 設為 `true` 時，行動配置 (\_Layout.Mobile.cshtml) 僅能用於行動檢視 (例如，檢視檔案的格式為 **ViewName**.Mobile.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="1e1a0-228">若行動配置不適用於您的非行動檢視，您可以將 `RequireConsistentDisplayMode` 設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="1e1a0-229">以下螢幕擷取畫面顯示當 `RequireConsistentDisplayMode` 設為 `true` 時，[演講者] 頁面的呈現方式 (頂端導覽列中沒有「(Mobile)」字串)。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="1e1a0-230">您可以在檢視檔案中將 `RequireConsistentDisplayMode` 設為 `false`，以停用特定檢視中的一致顯示模式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="1e1a0-231">Views\\Home\\AllSpeakers.cshtml 檔案中的以下標記會將 `RequireConsistentDisplayMode` 設為 `false`：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="1e1a0-232">在本節中，我們已了解如何建立行動配置和檢視，以及如何為特定裝置 (例如 iPhone) 建立配置和檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span>
<span data-ttu-id="1e1a0-233">不過，Bootstrap CSS 架構的主要優點是回應靈敏的配置，這表示單一樣式表可以套用到桌面、電話和平板電腦瀏覽器中，並建立一致的外觀及操作。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span></span> <span data-ttu-id="1e1a0-234">您將在下一節看到如何利用 Bootstrap 建立適合行動裝置的檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span></span>

## <span data-ttu-id="1e1a0-235"><a name="bkmk_Improvespeakerslist"></a> 改善演講者清單</span><span class="sxs-lookup"><span data-stu-id="1e1a0-235"><a name="bkmk_Improvespeakerslist"></a> Improve the Speakers List</span></span>
<span data-ttu-id="1e1a0-236">如您適才所見，行動裝置上的 [ *演講者* ] 檢視已可讀取，但是連結卻非常微小而不容易點選。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="1e1a0-237">在本節中，您要使 *AllSpeakers* 檢視適合行動用途，以顯示大尺寸又容易點選的連結，並包含可快速找到演講者的搜尋方塊。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="1e1a0-238">您可以使用 Bootstrap [連結清單群組][linked list group]樣式改善 [演講者] 檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span></span> <span data-ttu-id="1e1a0-239">在 Views\\Home\\AllSpeakers.cshtml 中，使用以下程式碼取代 Razor 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="1e1a0-240">`<div>` 標籤中的 `class="list-group"` 屬性會套用 Bootstrap 清單樣式，且 `class="input-group-item"` 屬性會將 Bootstrap 清單項目樣式套用至每個連結。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span></span>

<span data-ttu-id="1e1a0-241">重新整理行動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-241">Refresh the mobile browser.</span></span> <span data-ttu-id="1e1a0-242">更新的檢視如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-242">The updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="1e1a0-243">Bootstrap [連結清單群組][linked list group]樣式讓每個連結的整個方塊都可以點選，以提供更好的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="1e1a0-244">切換成桌面檢視，會發現此檢視也有一致的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-244">Switch to the desktop view and observe the consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="1e1a0-245">雖然已經改善行動瀏覽器檢視，但要瀏覽冗長的演講者清單還是很不方便。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="1e1a0-246">Bootstrap 並沒有現成的搜尋篩選功能，但您可以用數行程式碼來新增此功能。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="1e1a0-247">首先要先將搜尋方塊新增至檢視，然後與 JavaScript 程式碼連結，以取得篩選功能。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span></span> <span data-ttu-id="1e1a0-248">在 Views\\Home\\AllSpeakers.cshtml 中，在 \<h2\> 標籤後面加入 \<form\> 標籤，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="1e1a0-249">請注意，`<form>` 和 `<input>` 標籤都已套用 Bootstrap 樣式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span></span> <span data-ttu-id="1e1a0-250">`<span>` 元素會將 Bootstrap [glyphicon][glyphicon] 新增至搜尋方塊。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span></span>

<span data-ttu-id="1e1a0-251">在 Scripts 資料夾中，加入名為 filter.js 的 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="1e1a0-252">開啟該檔案，並將以下程式碼貼入其中：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-252">Open the file and paste the following code into it:</span></span>

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="1e1a0-253">您也需要在註冊的套件中包含 filter.js。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-253">You also need to include filter.js in your registered bundles.</span></span> <span data-ttu-id="1e1a0-254">開啟 App\_Start\\BundleConfig.cs，並變更第一組套件。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span></span> <span data-ttu-id="1e1a0-255">變更第一個 `bundles.Add` 陳述式 (針對 **jquery** 套件)，使其包含 Scripts\\filter.js，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="1e1a0-256">**jquery** 套件已經由預設的 \_Layout 檢視呈現。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span></span> <span data-ttu-id="1e1a0-257">您可以在稍後利用相同的 JavaScript 程式碼，將篩選功能套用至其他清單檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span></span>

<span data-ttu-id="1e1a0-258">請重新整理行動瀏覽器，並移至 *AllSpeakers* 檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span></span> <span data-ttu-id="1e1a0-259">在搜尋方塊中，輸入 "sc"。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-259">In the search box, type "sc".</span></span> <span data-ttu-id="1e1a0-260">此時應該會根據您的搜尋字串，篩選出演講者清單。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-260">The speakers list should now be filtered according to your search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="1e1a0-261"><a name="bkmk_improvetags"></a> 改善標籤清單</span><span class="sxs-lookup"><span data-stu-id="1e1a0-261"><a name="bkmk_improvetags"></a> Improve the Tags List</span></span>
<span data-ttu-id="1e1a0-262">就像 [演講者] 檢視，您可以在行動裝置上閱讀 [標籤] 檢視，但連結卻非常微小而不容易點選。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="1e1a0-263">若您使用先前描述的程式碼變更 (但在 Views\\Home\\AllTags.cshtml 中要包含以下 `Html.ActionLink` 方法語法)，就可以像修正 [演講者] 檢視一樣修正[標籤] 檢視：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="1e1a0-264">重新整理後的桌面瀏覽器外觀如下：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-264">The refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="1e1a0-265">而重新整理後的行動瀏覽器外觀如下：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-265">And the refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="1e1a0-266">若您發現行動瀏覽器中仍顯示原始的清單格式，想知道設好的 Bootstrap 樣式有什麼問題，這其實是您先前建立行動專用檢視的動作所產生的結果。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span></span> <span data-ttu-id="1e1a0-267">然而，既然您使用 Bootstrap CSS 架構建立回應靈敏的 Web 設計，請移除這些行動專用的檢視和行動專用的配置檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span></span> <span data-ttu-id="1e1a0-268">完成移除後，再重新整理行動瀏覽器，就會顯示 Bootstrap 樣式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="1e1a0-269"><a name="bkmk_improvedates"></a> 改善日期清單</span><span class="sxs-lookup"><span data-stu-id="1e1a0-269"><a name="bkmk_improvedates"></a> Improve the Dates List</span></span>
<span data-ttu-id="1e1a0-270">若您使用先前描述的程式碼變更 (但在 Views\\Home\\AllDates.cshtml 中要包含以下 `Html.ActionLink` 方法語法)，就可以像改善 [演講者] 和 [標籤] 檢視一樣改善 [日期] 檢視：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="1e1a0-271">重新整理後，您會獲得如下的行動瀏覽器檢視：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="1e1a0-272">您可以依照日期，組織時間日期值，以進一步改善 [ *日期* ] 檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-272">You can further improve the *Dates* view by organizing the date-time values by date.</span></span> <span data-ttu-id="1e1a0-273">這可以透過 Bootstrap [面板][panels]樣式來完成。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-273">This can be done with the Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="1e1a0-274">以下列程式碼取代 Views\\Home\\AllDates.cshtml 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="1e1a0-275">此程式碼會為清單中每個不同的日期建立個別 `<div class="panel panel-primary">` 標籤，並分別為連結使用如上所述的[連結清單群組][linked list group]。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="1e1a0-276">以下是此程式碼執行時行動瀏覽器的樣貌：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-276">Here's what the mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="1e1a0-277">切換成桌面瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-277">Switch to the desktop browser.</span></span> <span data-ttu-id="1e1a0-278">然後會再次發現有一致的外觀。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-278">Again, note the consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="1e1a0-279"><a name="bkmk_improvesessionstable"></a> 改善 SessionsTable 檢視</span><span class="sxs-lookup"><span data-stu-id="1e1a0-279"><a name="bkmk_improvesessionstable"></a> Improve the SessionsTable View</span></span>
<span data-ttu-id="1e1a0-280">您要在本節中使 *SessionsTable* 檢視更適合行動用途。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="1e1a0-281">這項變更比先前的變更更加廣泛。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-281">This change is more extensive the previous changes.</span></span>

<span data-ttu-id="1e1a0-282">在行動瀏覽器中，點選 [標籤] 按鈕，然後在搜尋方塊中輸入 `asp`。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="1e1a0-283">點選 **ASP.NET** 連結。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-283">Tap the **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="1e1a0-284">如您所見，顯示畫面會格式化為表格，目前這表格設計為可在桌面瀏覽器中檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span></span> <span data-ttu-id="1e1a0-285">但在行動瀏覽器上則有點難以閱讀。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-285">However, it's a little bit difficult to read on a mobile browser.</span></span> <span data-ttu-id="1e1a0-286">若要修正此問題，請開啟 Views\\Home\\SessionsTable.cshtml，然後使用下列程式碼取代檔案內容：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="1e1a0-287">此程式碼會執行 3 個動作：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-287">The code does 3 things:</span></span>

* <span data-ttu-id="1e1a0-288">使用 Bootstrap [自訂連結清單群組][custom linked list group]，以垂直方式格式化工作階段資訊，使您可以在行動瀏覽器上閱讀所有資訊 (使用 list-group-item-text 之類的類別)</span><span class="sxs-lookup"><span data-stu-id="1e1a0-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="1e1a0-289">將[方格系統][grid system]套用至配置，讓工作階段項目能在桌面瀏覽器中水平流動，並在行動瀏覽器中垂直流動 (使用 col-md-4 類別)</span><span class="sxs-lookup"><span data-stu-id="1e1a0-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span></span>
* <span data-ttu-id="1e1a0-290">使用[回應靈敏的公用程式][responsive utilities]，於行動瀏覽器中檢視時，隱藏工作階段標籤 (使用 hidden-xs 類別)</span><span class="sxs-lookup"><span data-stu-id="1e1a0-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span></span>

<span data-ttu-id="1e1a0-291">您也可以點選標題連結，以進入個別工作階段。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-291">You can also tap a title link to go to the respective session.</span></span> <span data-ttu-id="1e1a0-292">下圖反映了程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-292">The image below reflects the code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="1e1a0-293">您自動套用的 Bootstrap 方格系統會在行動瀏覽器中自動以垂直方式排列工作階段。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span></span> <span data-ttu-id="1e1a0-294">此外，請注意標籤並未顯示。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-294">Also, notice that the tags are not shown.</span></span> <span data-ttu-id="1e1a0-295">切換成桌面瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-295">Switch to the desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="1e1a0-296">在桌面瀏覽器，您會發現有顯示標籤。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-296">In the desktop browser, notice that the tags are now displayed.</span></span> <span data-ttu-id="1e1a0-297">而且您還會看到套用的 Bootstrap 方格系統以兩欄方式排列工作階段項目。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span></span> <span data-ttu-id="1e1a0-298">若您放大瀏覽器，會發現排列變更為三欄式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span></span>

## <span data-ttu-id="1e1a0-299"><a name="bkmk_improvesessionbycode"></a> 改善 SessionByCode 檢視</span><span class="sxs-lookup"><span data-stu-id="1e1a0-299"><a name="bkmk_improvesessionbycode"></a> Improve the SessionByCode View</span></span>
<span data-ttu-id="1e1a0-300">最後，您要修正 *SessionByCode* 檢視，使其適合行動用途。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span></span>

<span data-ttu-id="1e1a0-301">在行動瀏覽器中，點選 [標籤] 按鈕，然後在搜尋方塊中輸入 `asp`。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="1e1a0-302">點選 **ASP.NET** 連結。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-302">Tap the **ASP.NET** link.</span></span> <span data-ttu-id="1e1a0-303">隨即會顯示 ASP.NET 標籤的工作階段。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-303">Sessions for the ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="1e1a0-304">選擇 **使用 ASP.NET 和 AngularJS 建置單一頁面應用程式** 連結。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="1e1a0-305">預設的桌面檢視雖然不錯，但您可以使用一些 Bootstrap GUI 元件輕鬆地改善它的外觀。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="1e1a0-306">開啟 Views\\Home\\SessionByCode.cshtml，並以下列標記取代內容：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="1e1a0-307">新的標記會使用 Bootstrap 的面板樣式改善行動檢視。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span></span> 

<span data-ttu-id="1e1a0-308">重新整理行動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-308">Refresh the mobile browser.</span></span> <span data-ttu-id="1e1a0-309">下圖反映您剛做的程式碼變更：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-309">The following image reflects the code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="1e1a0-310">總結與複習</span><span class="sxs-lookup"><span data-stu-id="1e1a0-310">Wrap Up and Review</span></span>
<span data-ttu-id="1e1a0-311">本教學課程已示範如何使用 ASP.NET MVC 5 開發適合行動的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e1a0-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span></span> <span data-ttu-id="1e1a0-312">其中包含：</span><span class="sxs-lookup"><span data-stu-id="1e1a0-312">These include:</span></span>

* <span data-ttu-id="1e1a0-313">將 ASP.NET MVC 5 應用程式部署至 App Service Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e1a0-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span></span>
* <span data-ttu-id="1e1a0-314">使用 Bootstrap 建立 MVC 5 應用程式中回應靈敏的 Web 配置</span><span class="sxs-lookup"><span data-stu-id="1e1a0-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="1e1a0-315">以全域方式覆寫個別檢視的配置、檢視和部分檢視</span><span class="sxs-lookup"><span data-stu-id="1e1a0-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="1e1a0-316">使用 `RequireConsistentDisplayMode` 屬性，控制配置和部分覆寫的強制執行</span><span class="sxs-lookup"><span data-stu-id="1e1a0-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="1e1a0-317">建立以特定瀏覽器做為目標的檢視，例如 iPhone 瀏覽器</span><span class="sxs-lookup"><span data-stu-id="1e1a0-317">Create views that target specific browsers, such as the iPhone browser</span></span>
* <span data-ttu-id="1e1a0-318">在 Razor 程式碼中套用 Boostrap 樣式</span><span class="sxs-lookup"><span data-stu-id="1e1a0-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="1e1a0-319">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1e1a0-319">See Also</span></span>
* [<span data-ttu-id="1e1a0-320">回應性 Web 設計的 9 個基本原則</span><span class="sxs-lookup"><span data-stu-id="1e1a0-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="1e1a0-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="1e1a0-322">[官方 Bootstrap 部落格][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="1e1a0-323">[Tutorial Republic 的 Twitter Bootstrap 教學課程][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="1e1a0-324">[Bootstrap 練習場][The Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-324">[The Bootstrap Playground][The Bootstrap Playground]</span></span>
* <span data-ttu-id="1e1a0-325">[W3C 推薦的行動 Web 應用程式最佳做法][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="1e1a0-326">[W3C 針對媒體查詢的候選推薦做法][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="1e1a0-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="1e1a0-327">變更的項目</span><span class="sxs-lookup"><span data-stu-id="1e1a0-327">What's changed</span></span>
* <span data-ttu-id="1e1a0-328">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1e1a0-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[The Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

