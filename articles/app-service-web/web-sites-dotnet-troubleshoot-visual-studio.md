---
title: "aaaTroubleshoot 中使用 Visual Studio 的 Azure App Service web 應用程式"
description: "了解如何 tootroubleshoot Azure web 應用程式使用遠端偵錯、 追蹤和記錄工具內建的 tooVisual Studio 2013。"
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a><span data-ttu-id="65165-103">使用 Visual Studio 疑難排解 Azure App Service 中的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="65165-103">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="65165-104">概觀</span><span class="sxs-lookup"><span data-stu-id="65165-104">Overview</span></span>
<span data-ttu-id="65165-105">本教學課程示範如何 toouse Visual Studio 工具，可協助偵錯 web 應用程式中的[App Service](http://go.microsoft.com/fwlink/?LinkId=529714)，在執行[偵錯模式](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)遠端或藉由檢視應用程式記錄檔和 web 伺服器記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-105">This tutorial shows how toouse Visual Studio tools that help debug a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), by running in [debug mode](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) remotely or by viewing application logs and web server logs.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="65165-106">您將了解：</span><span class="sxs-lookup"><span data-stu-id="65165-106">You'll learn:</span></span>

* <span data-ttu-id="65165-107">Visual Studio 中提供的 Azure Web 應用程式管理功能有哪些。</span><span class="sxs-lookup"><span data-stu-id="65165-107">Which Azure web app management functions are available in Visual Studio.</span></span>
* <span data-ttu-id="65165-108">如何 toouse Visual Studio 遠端檢視 toomake 快速變更遠端 web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="65165-108">How toouse Visual Studio remote view toomake quick changes in a remote web app.</span></span>
* <span data-ttu-id="65165-109">如何 toorun 從遠端同時在專案的偵錯模式是在 Azure 中執行，web 應用程式和 web 工作。</span><span class="sxs-lookup"><span data-stu-id="65165-109">How toorun debug mode remotely while a project is running in Azure, both for a web app and for a WebJob.</span></span>
* <span data-ttu-id="65165-110">如何 toocreate 應用程式追蹤記錄檔，並檢視時 hello 應用程式會建立它們。</span><span class="sxs-lookup"><span data-stu-id="65165-110">How toocreate application trace logs and view them while hello application is creating them.</span></span>
* <span data-ttu-id="65165-111">如何 tooview web 伺服器記錄檔，包括詳細的錯誤訊息和失敗的要求追蹤。</span><span class="sxs-lookup"><span data-stu-id="65165-111">How tooview web server logs, including detailed error messages and failed request tracing.</span></span>
* <span data-ttu-id="65165-112">如何 toosend 診斷記錄 tooan Azure 儲存體帳戶，並那里檢視。</span><span class="sxs-lookup"><span data-stu-id="65165-112">How toosend diagnostic logs tooan Azure Storage account and view them there.</span></span>

<span data-ttu-id="65165-113">如果您有 Visual Studio Ultimate，您也可以使用 [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) 進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="65165-113">If you have Visual Studio Ultimate, you can also use [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) for debugging.</span></span> <span data-ttu-id="65165-114">本教學課程未涵蓋 IntelliTrace。</span><span class="sxs-lookup"><span data-stu-id="65165-114">IntelliTrace is not covered in this tutorial.</span></span>

## <span data-ttu-id="65165-115"><a name="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="65165-115"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="65165-116">本教學課程適用於 hello 開發環境、 web 專案和您在設定的 Azure web 應用程式[開始使用 Azure 和 ASP.NET][GetStarted]。</span><span class="sxs-lookup"><span data-stu-id="65165-116">This tutorial works with hello development environment, web project, and Azure web app that you set up in [Get started with Azure and ASP.NET][GetStarted].</span></span> <span data-ttu-id="65165-117">Hello WebJobs 的區段中，您將需要 hello 應用程式中建立[hello Azure WebJobs SDK 快速入門][GetStartedWJ]。</span><span class="sxs-lookup"><span data-stu-id="65165-117">For hello WebJobs sections, you'll need hello application that you create in [Get Started with hello Azure WebJobs SDK][GetStartedWJ].</span></span>

<span data-ttu-id="65165-118">hello 程式碼範例顯示在本教學課程適用於 C# MVC web 應用程式，但是 hello 疑難排解程序是 hello Visual Basic 和 Web Form 應用程式相同。</span><span class="sxs-lookup"><span data-stu-id="65165-118">hello code samples shown in this tutorial are for a C# MVC web application, but hello troubleshooting procedures are hello same for Visual Basic and Web Forms applications.</span></span>

<span data-ttu-id="65165-119">hello 教學課程假設您使用 Visual Studio 2015 或 2013年。</span><span class="sxs-lookup"><span data-stu-id="65165-119">hello tutorial assumes you're using Visual Studio 2015 or 2013.</span></span> <span data-ttu-id="65165-120">如果您使用 Visual Studio 2013，hello WebJobs 功能都需要[Update 4](http://go.microsoft.com/fwlink/?LinkID=510314)或更新版本。</span><span class="sxs-lookup"><span data-stu-id="65165-120">If you're using Visual Studio 2013, hello WebJobs features require [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) or later.</span></span>

<span data-ttu-id="65165-121">hello 資料流記錄功能只適用於.NET Framework 4 或更新版本為目標的應用程式。</span><span class="sxs-lookup"><span data-stu-id="65165-121">hello streaming logs feature only works for applications that target .NET Framework 4 or later.</span></span>

## <span data-ttu-id="65165-122"><a name="sitemanagement"></a>Web 應用程式組態與管理</span><span class="sxs-lookup"><span data-stu-id="65165-122"><a name="sitemanagement"></a>Web app configuration and management</span></span>
<span data-ttu-id="65165-123">Visual Studio 提供存取 tooa 子集 hello web 應用程式管理功能和 hello 中可用的組態設定[Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)。</span><span class="sxs-lookup"><span data-stu-id="65165-123">Visual Studio provides access tooa subset of hello web app management functions and configuration settings available in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="65165-124">本節將說明使用 **伺服器總管**可用的項目。</span><span class="sxs-lookup"><span data-stu-id="65165-124">In this section you'll see what's available by using **Server Explorer**.</span></span> <span data-ttu-id="65165-125">toosee hello 最新 Azure 整合的功能，現在試試看**Cloud Explorer**也。</span><span class="sxs-lookup"><span data-stu-id="65165-125">toosee hello latest Azure integration features, try out **Cloud Explorer** also.</span></span> <span data-ttu-id="65165-126">您可以從 hello 開啟這兩個視窗**檢視**功能表。</span><span class="sxs-lookup"><span data-stu-id="65165-126">You can open both windows from hello **View** menu.</span></span>

1. <span data-ttu-id="65165-127">如果您未登入 tooAzure Visual Studio 中，按一下 hello**連接 tooAzure**按鈕**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="65165-127">If you aren't already signed in tooAzure in Visual Studio, click hello **Connect tooAzure** button in **Server Explorer**.</span></span>

    <span data-ttu-id="65165-128">替代方式是 tooinstall 啟用存取 tooyour 帳戶的管理憑證。</span><span class="sxs-lookup"><span data-stu-id="65165-128">An alternative is tooinstall a management certificate that enables access tooyour account.</span></span> <span data-ttu-id="65165-129">如果您選擇 tooinstall 憑證，以滑鼠右鍵按一下 hello **Azure**節點**伺服器總管**，然後按一下**管理和篩選訂閱**hello 內容功能表中。</span><span class="sxs-lookup"><span data-stu-id="65165-129">If you choose tooinstall a certificate, right-click hello **Azure** node in **Server Explorer**, and then click **Manage and Filter Subscriptions** in hello context menu.</span></span> <span data-ttu-id="65165-130">在 hello**管理 Azure 訂用帳戶**對話方塊方塊中，按一下 hello**憑證**索引標籤，然後再按一下**匯入**。</span><span class="sxs-lookup"><span data-stu-id="65165-130">In hello **Manage Azure Subscriptions** dialog box, click hello **Certificates** tab, and then click **Import**.</span></span> <span data-ttu-id="65165-131">請遵循 hello 指示 toodownload，然後再匯入訂用帳戶檔案 (也稱為*.publishsettings*檔案) 為您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="65165-131">Follow hello directions toodownload and then import a subscription file (also called a *.publishsettings* file) for your Azure account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="65165-132">如果您下載訂閱檔案、 資料夾會儲存在它 tooa 外部來源的程式碼目錄 （例如，在 hello 下載資料夾中），然後再刪除它一次 hello 匯入已完成。</span><span class="sxs-lookup"><span data-stu-id="65165-132">If you download a subscription file, save it tooa folder outside your source code directories (for example, in hello Downloads folder), and then delete it once hello import has completed.</span></span> <span data-ttu-id="65165-133">惡意使用者獲得存取 toohello 訂用帳戶檔案，可以編輯、 建立，並刪除您的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="65165-133">A malicious user who gains access toohello subscription file can edit, create, and delete your Azure services.</span></span>
   >
   >

    <span data-ttu-id="65165-134">如需從 Visual Studio 中連接 tooAzure 資源的詳細資訊，請參閱[管理帳戶、 訂用帳戶及管理角色](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert)。</span><span class="sxs-lookup"><span data-stu-id="65165-134">For more information about connecting tooAzure resources from Visual Studio, see [Manage Accounts, Subscriptions, and Administrative Roles](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).</span></span>
2. <span data-ttu-id="65165-135">在 [伺服器總管] 中，展開 [Azure]，然後展開 [App Service]。</span><span class="sxs-lookup"><span data-stu-id="65165-135">In **Server Explorer**, expand **Azure** and expand **App Service**.</span></span>
3. <span data-ttu-id="65165-136">展開包含您在建立 hello web 應用程式的 hello 資源群組[開始使用 Azure 和 ASP.NET][GetStarted]，然後以滑鼠右鍵按一下 hello web 應用程式節點，再按一下**的檢視設定**.</span><span class="sxs-lookup"><span data-stu-id="65165-136">Expand hello resource group that includes hello web app that you created in [Getting started with Azure and ASP.NET][GetStarted], and then right-click hello web app node and click **View Settings**.</span></span>

    ![在伺服器總管中檢視設定](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    <span data-ttu-id="65165-138">hello **Azure Web 應用程式**索引標籤會出現，以及您可以看到那里 hello web 應用程式管理和設定工作在 Visual Studio 中可用。</span><span class="sxs-lookup"><span data-stu-id="65165-138">hello **Azure Web App** tab appears, and you can see there hello web app management and configuration tasks that are available in Visual Studio.</span></span>

    ![Azure Web 應用程式視窗](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    <span data-ttu-id="65165-140">在本教學課程將 hello 記錄和追蹤的下拉式清單使用。</span><span class="sxs-lookup"><span data-stu-id="65165-140">In this tutorial you'll be using hello logging and tracing drop-downs.</span></span> <span data-ttu-id="65165-141">您也可以使用遠端偵錯，但是您將使用不同的方法 tooenable 它。</span><span class="sxs-lookup"><span data-stu-id="65165-141">You'll also use remote debugging but you'll use a different method tooenable it.</span></span>

    <span data-ttu-id="65165-142">此視窗中的 hello 應用程式設定和連接字串方塊的相關資訊，請參閱[Azure Web 應用程式： 如何應用程式字串與連接字串工作](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65165-142">For information about hello App Settings and Connection Strings boxes in this window, see [Azure Web Apps: How Application Strings and Connection Strings Work](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

    <span data-ttu-id="65165-143">如果您想 tooperform web 應用程式管理工作無法完成在此視窗中，按一下**管理入口網站中開啟**tooopen 瀏覽器視窗 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="65165-143">If you want tooperform a web app management task that can't be done in this window, click **Open in Management Portal** tooopen a browser window toohello Azure portal.</span></span>

## <span data-ttu-id="65165-144"><a name="remoteview"></a>在伺服器總管中存取 Web 應用程式檔案</span><span class="sxs-lookup"><span data-stu-id="65165-144"><a name="remoteview"></a>Access web app files in Server Explorer</span></span>
<span data-ttu-id="65165-145">您通常會部署 web 專案以 hello`customErrors`加上旗標 hello Web.config 檔案組太`On`或`RemoteOnly`，這表示不會很有幫助的錯誤訊息時項目發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="65165-145">You typically deploy a web project with hello `customErrors` flag in hello Web.config file set too`On` or `RemoteOnly`, which means you don't get a helpful error message when something goes wrong.</span></span> <span data-ttu-id="65165-146">許多錯誤您得到的也是 hello 的類似是 hello 的下列其中一個頁面。</span><span class="sxs-lookup"><span data-stu-id="65165-146">For many errors all you get is a page like one of hello following ones.</span></span>

<span data-ttu-id="65165-147">**'/' 應用程式中有伺服器錯誤：**</span><span class="sxs-lookup"><span data-stu-id="65165-147">**Server Error in '/' Application:**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

<span data-ttu-id="65165-149">**發生錯誤：**</span><span class="sxs-lookup"><span data-stu-id="65165-149">**An error occurred:**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

<span data-ttu-id="65165-151">**hello 網站無法顯示 hello 頁面**</span><span class="sxs-lookup"><span data-stu-id="65165-151">**hello website cannot display hello page**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

<span data-ttu-id="65165-153">Hello 最簡單方式 toofind hello hello 項錯誤的原因通常是 tooenable hello hello 前面螢幕擷取畫面中的第一個詳細的錯誤訊息說明如何 toodo。</span><span class="sxs-lookup"><span data-stu-id="65165-153">Frequently hello easiest way toofind hello cause of hello error is tooenable detailed error messages, which hello first of hello preceding screenshots explains how toodo.</span></span> <span data-ttu-id="65165-154">需要 hello 中的變更已部署 Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="65165-154">That requires a change in hello deployed Web.config file.</span></span> <span data-ttu-id="65165-155">您可以編輯 hello *Web.config* hello 專案和重新部署的 hello 專案，在檔案或建立[Web.config 轉換](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations)和部署偵錯組建，但還有更快的方法： 在**方案總管**直接檢視和編輯 hello 遠端 web 應用程式中的檔案使用 hello*遠端檢視*功能。</span><span class="sxs-lookup"><span data-stu-id="65165-155">You could edit hello *Web.config* file in hello project and redeploy hello project, or create a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) and deploy a debug build, but there's a quicker way: in **Solution Explorer** you can directly view and edit files in hello remote web app by using hello *remote view* feature.</span></span>

1. <span data-ttu-id="65165-156">在**伺服器總管**，依序展開**Azure**，依序展開**App Service**、 依序展開 hello 資源群組中，位於您 web 應用程式和 web 應用程式的 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="65165-156">In **Server Explorer**, expand **Azure**, expand **App Service**, expand hello resource group that your web app is located in, and then expand hello node for your web app.</span></span>

    <span data-ttu-id="65165-157">您會看到節點可讓您存取 toohello web 應用程式的內容檔案和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-157">You see nodes that give you access toohello web app's content files and log files.</span></span>
2. <span data-ttu-id="65165-158">展開 hello**檔案** 節點，然後按兩下 hello *Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="65165-158">Expand hello **Files** node, and double-click hello *Web.config* file.</span></span>

    ![開啟 Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    <span data-ttu-id="65165-160">Visual Studio 會從 hello 遠端 web 應用程式開啟 hello Web.config 檔案，並顯示 hello 標題列中的 [遠端] 的下一個 toohello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="65165-160">Visual Studio opens hello Web.config file from hello remote web app and shows [Remote] next toohello file name in hello title bar.</span></span>
3. <span data-ttu-id="65165-161">加入下列行 toohello hello`system.web`項目：</span><span class="sxs-lookup"><span data-stu-id="65165-161">Add hello following line toohello `system.web` element:</span></span>

    `<customErrors mode="Off"></customErrors>`

    ![編輯 Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. <span data-ttu-id="65165-163">重新整理顯示 hello 無用的錯誤訊息： hello 瀏覽器，現在您可以取得詳細的錯誤訊息，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="65165-163">Refresh hello browser that is showing hello unhelpful error message, and now you get a detailed error message, such as hello following example:</span></span>

    ![詳細的錯誤訊息](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    <span data-ttu-id="65165-165">(將顯示為紅色太 hello 一行加入建立顯示 hello 錯誤*Views\Home\Index.cshtml*。)</span><span class="sxs-lookup"><span data-stu-id="65165-165">(hello error shown was created by adding hello line shown in red too*Views\Home\Index.cshtml*.)</span></span>

<span data-ttu-id="65165-166">編輯 hello Web.config 檔案是一個範例在哪些 hello 能力 tooread 和編輯的檔案，Azure web 應用程式上進行疑難排解的案例。</span><span class="sxs-lookup"><span data-stu-id="65165-166">Editing hello Web.config file is only one example of scenarios in which hello ability tooread and edit files on your Azure web app make troubleshooting easier.</span></span>

## <span data-ttu-id="65165-167"><a name="remotedebug"></a>遠端偵錯 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="65165-167"><a name="remotedebug"></a>Remote debugging web apps</span></span>
<span data-ttu-id="65165-168">如果 hello 詳細的錯誤訊息不會提供足夠的資訊，而且您無法重新建立本機 hello 錯誤，另一個方式 tootroubleshoot 就是從遠端 toorun 偵錯模式中。</span><span class="sxs-lookup"><span data-stu-id="65165-168">If hello detailed error message doesn't provide enough information, and you can't re-create hello error locally, another way tootroubleshoot is toorun in debug mode remotely.</span></span> <span data-ttu-id="65165-169">您可以設定中斷點、 直接管理記憶體、 逐步執行程式碼，以及甚至變更 hello 程式碼路徑。</span><span class="sxs-lookup"><span data-stu-id="65165-169">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path.</span></span>

<span data-ttu-id="65165-170">遠端偵錯無法在 Visual Studio 的 Express 版本中運作。</span><span class="sxs-lookup"><span data-stu-id="65165-170">Remote debugging does not work in Express editions of Visual Studio.</span></span>

<span data-ttu-id="65165-171">本節說明如何從遠端使用 hello toodebug 您專案中建立[開始使用 Azure 和 ASP.NET][GetStarted]。</span><span class="sxs-lookup"><span data-stu-id="65165-171">This section shows how toodebug remotely using hello project you create in [Getting started with Azure and ASP.NET][GetStarted].</span></span>

1. <span data-ttu-id="65165-172">開啟 hello web 專案中建立[開始使用 Azure 和 ASP.NET][GetStarted]。</span><span class="sxs-lookup"><span data-stu-id="65165-172">Open hello web project that you created in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
2. <span data-ttu-id="65165-173">開啟 *Controllers\HomeController.cs*。</span><span class="sxs-lookup"><span data-stu-id="65165-173">Open *Controllers\HomeController.cs*.</span></span>
3. <span data-ttu-id="65165-174">刪除 hello`About()`中其所在位置的方法，並插入 hello 下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="65165-174">Delete hello `About()` method and insert hello following code in its place.</span></span>

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. <span data-ttu-id="65165-175">[設定中斷點](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)上 hello`ViewBag.Message`列。</span><span class="sxs-lookup"><span data-stu-id="65165-175">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on hello `ViewBag.Message` line.</span></span>
5. <span data-ttu-id="65165-176">在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="65165-176">In **Solution Explorer**, right-click hello project, and click **Publish**.</span></span>
6. <span data-ttu-id="65165-177">在 hello**設定檔**下拉式清單中，選取 hello 相同設定檔中使用該您[開始使用 Azure 和 ASP.NET][GetStarted]。</span><span class="sxs-lookup"><span data-stu-id="65165-177">In hello **Profile** drop-down list, select hello same profile that you used in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
7. <span data-ttu-id="65165-178">按一下 hello**設定**索引標籤，然後變更**組態**太**偵錯**，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="65165-178">Click hello **Settings** tab, and change **Configuration** too**Debug**, and then click **Publish**.</span></span>

    ![於偵錯模式中發行](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. <span data-ttu-id="65165-180">在部署之後完成，您的瀏覽器會開啟 toohello Azure web 應用程式，關閉 hello 瀏覽器的 URL。</span><span class="sxs-lookup"><span data-stu-id="65165-180">After deployment finishes and your browser opens toohello Azure URL of your web app, close hello browser.</span></span>
9. <span data-ttu-id="65165-181">在 [伺服器總管] 中，以滑鼠右鍵按一下您的 Web 應用程式，接著按一下 [連結偵錯工具]。</span><span class="sxs-lookup"><span data-stu-id="65165-181">In **Server Explorer**, right-click your web app, and then click **Attach Debugger**.</span></span>

    ![連結偵錯工具](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    <span data-ttu-id="65165-183">hello 瀏覽器會自動開啟 tooyour 首頁上，在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="65165-183">hello browser automatically opens tooyour home page running in Azure.</span></span> <span data-ttu-id="65165-184">您可能會有 toowait 20 秒或因此而 Azure 會設定 hello 伺服器進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="65165-184">You might have toowait 20 seconds or so while Azure sets up hello server for debugging.</span></span> <span data-ttu-id="65165-185">此延遲時間只會發生 hello 偵錯模式中執行 web 應用程式的第一次。</span><span class="sxs-lookup"><span data-stu-id="65165-185">This delay only happens hello first time you run in debug mode on a web app.</span></span> <span data-ttu-id="65165-186">後續時間內 hello 未來的 48 小時，當您啟動偵錯一次將不會有延遲。</span><span class="sxs-lookup"><span data-stu-id="65165-186">Subsequent times within hello next 48 hours when you start debugging again there won't be a delay.</span></span>

    <span data-ttu-id="65165-187">**注意：**如果您有任何無法啟動 hello 偵錯工具，再試一次 toodo 它使用**Cloud Explorer**而不是**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="65165-187">**Note:** If you have any trouble starting hello debugger, try toodo it by using **Cloud Explorer** instead of **Server Explorer**.</span></span>
10. <span data-ttu-id="65165-188">按一下**有關**hello 功能表中。</span><span class="sxs-lookup"><span data-stu-id="65165-188">Click **About** in hello menu.</span></span>

     <span data-ttu-id="65165-189">Visual Studio 停止 hello 中斷點並 hello 程式碼在 Azure 中，不在本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="65165-189">Visual Studio stops on hello breakpoint, and hello code is running in Azure, not on your local computer.</span></span>
11. <span data-ttu-id="65165-190">將滑鼠停留在 hello`currentTime`變數 toosee hello 時間值。</span><span class="sxs-lookup"><span data-stu-id="65165-190">Hover over hello `currentTime` variable toosee hello time value.</span></span>

     ![檢視 Azure 偵錯模式中執行的變數](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     <span data-ttu-id="65165-192">您會看到的 hello 時間是 hello Azure 的伺服器時間，可能在不同的時區，於本機電腦。</span><span class="sxs-lookup"><span data-stu-id="65165-192">hello time you see is hello Azure server time, which may be in a different time zone than your local computer.</span></span>
12. <span data-ttu-id="65165-193">輸入新的值為 hello`currentTime`變數，例如 「 現在在 Azure 中執行 」。</span><span class="sxs-lookup"><span data-stu-id="65165-193">Enter a new value for hello `currentTime` variable, such as "Now running in Azure".</span></span>
13. <span data-ttu-id="65165-194">按 F5 toocontinue 執行。</span><span class="sxs-lookup"><span data-stu-id="65165-194">Press F5 toocontinue running.</span></span>

     <span data-ttu-id="65165-195">hello 有關在 Azure 中執行的頁面會顯示您輸入 hello currentTime 變數 hello 新值。</span><span class="sxs-lookup"><span data-stu-id="65165-195">hello About page running in Azure displays hello new value that you entered into hello currentTime variable.</span></span>

     ![含有新值的關於頁面](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <span data-ttu-id="65165-197"><a name="remotedebugwj"></a> 遠端偵錯 WebJobs</span><span class="sxs-lookup"><span data-stu-id="65165-197"><a name="remotedebugwj"></a> Remote debugging WebJobs</span></span>
<span data-ttu-id="65165-198">本節說明如何從遠端使用 hello 專案和 web 應用程式的 toodebug 您在中建立[hello Azure WebJobs SDK 快速入門](websites-dotnet-webjobs-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="65165-198">This section shows how toodebug remotely using hello project and web app you create in [Get Started with hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

<span data-ttu-id="65165-199">本節中所顯示的 hello 功能只在 Visual Studio 2013 Update 4 或更新版本可用。</span><span class="sxs-lookup"><span data-stu-id="65165-199">hello features shown in this section are available only in Visual Studio 2013 with Update 4 or later.</span></span>

<span data-ttu-id="65165-200">遠端偵錯僅適用於連續的 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="65165-200">Remote debugging only works with continuous WebJobs.</span></span> <span data-ttu-id="65165-201">排程與隨選 WebJobs 不支援偵錯。</span><span class="sxs-lookup"><span data-stu-id="65165-201">Scheduled and on-demand WebJobs don't support debugging.</span></span>

1. <span data-ttu-id="65165-202">開啟 hello web 專案中建立[hello Azure WebJobs SDK 快速入門][GetStartedWJ]。</span><span class="sxs-lookup"><span data-stu-id="65165-202">Open hello web project that you created in [Get Started with hello Azure WebJobs SDK][GetStartedWJ].</span></span>
2. <span data-ttu-id="65165-203">在 hello ContosoAdsWebJob 專案中，開啟*Functions.cs*。</span><span class="sxs-lookup"><span data-stu-id="65165-203">In hello ContosoAdsWebJob project, open *Functions.cs*.</span></span>
3. <span data-ttu-id="65165-204">[設定中斷點](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)hello hello 第一個陳述式`GnerateThumbnail`方法。</span><span class="sxs-lookup"><span data-stu-id="65165-204">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on hello first statement in hello `GnerateThumbnail` method.</span></span>

    ![設定中斷點](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. <span data-ttu-id="65165-206">在**方案總管 中**，以滑鼠右鍵按一下 hello web 專案 （非 hello WebJob 專案），然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="65165-206">In **Solution Explorer**, right-click hello web project (not hello WebJob project), and click **Publish**.</span></span>
5. <span data-ttu-id="65165-207">在 hello**設定檔**下拉式清單中，選取 hello 相同設定檔中使用該您[hello Azure WebJobs SDK 快速入門](websites-dotnet-webjobs-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="65165-207">In hello **Profile** drop-down list, select hello same profile that you used in [Get Started with hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>
6. <span data-ttu-id="65165-208">按一下 hello**設定**索引標籤，然後變更**組態**太**偵錯**，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="65165-208">Click hello **Settings** tab, and change **Configuration** too**Debug**, and then click **Publish**.</span></span>

    <span data-ttu-id="65165-209">Visual Studio 會部署 hello web 和 WebJob 專案和您的瀏覽器會開啟 toohello Azure web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="65165-209">Visual Studio deploys hello web and WebJob projects, and your browser opens toohello Azure URL of your web app.</span></span>
7. <span data-ttu-id="65165-210">在 [伺服器總管] 中，依序展開 [Azure] > [App Service] > 您的資源群組Web > 您的 Web 應用程式 > [WebJob] > [連續]，然後使用滑鼠右鍵按一下 [ContosoAdsWebJob]。</span><span class="sxs-lookup"><span data-stu-id="65165-210">In **Server Explorer** expand **Azure > App Service > your resource group > your web app > WebJobs > Continuous**, and then right-click **ContosoAdsWebJob**.</span></span>
8. <span data-ttu-id="65165-211">按一下 [連結偵錯工具] 。</span><span class="sxs-lookup"><span data-stu-id="65165-211">Click **Attach Debugger**.</span></span>

    ![連結偵錯工具](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    <span data-ttu-id="65165-213">hello 瀏覽器會自動開啟 tooyour 首頁上，在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="65165-213">hello browser automatically opens tooyour home page running in Azure.</span></span> <span data-ttu-id="65165-214">您可能會有 toowait 20 秒或因此而 Azure 會設定 hello 伺服器進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="65165-214">You might have toowait 20 seconds or so while Azure sets up hello server for debugging.</span></span> <span data-ttu-id="65165-215">此延遲時間只會發生 hello 偵錯模式中執行 web 應用程式的第一次。</span><span class="sxs-lookup"><span data-stu-id="65165-215">This delay only happens hello first time you run in debug mode on a web app.</span></span> <span data-ttu-id="65165-216">hello 下一次附加 hello 偵錯有工具將不會有延遲，如果您在 48 小時內操作。</span><span class="sxs-lookup"><span data-stu-id="65165-216">hello next time you attach hello debugger there won't be a delay, if you do it within 48 hours.</span></span>
9. <span data-ttu-id="65165-217">在 hello web 瀏覽器開啟的 toohello Contoso 廣告首頁上，建立新的廣告。</span><span class="sxs-lookup"><span data-stu-id="65165-217">In hello web browser that is opened toohello Contoso Ads home page, create a new ad.</span></span>

    <span data-ttu-id="65165-218">建立 ad 將會導致佇列訊息 toobe 建立，這會由 hello WebJob 挑選並處理。</span><span class="sxs-lookup"><span data-stu-id="65165-218">Creating an ad causes a queue message toobe created, which will be picked up by hello WebJob and processed.</span></span> <span data-ttu-id="65165-219">當 hello WebJobs SDK 呼叫 hello 函式 tooprocess hello 佇列訊息時，hello 程式碼會叫用中斷點。</span><span class="sxs-lookup"><span data-stu-id="65165-219">When hello WebJobs SDK calls hello function tooprocess hello queue message, hello code will hit your breakpoint.</span></span>
10. <span data-ttu-id="65165-220">Hello 偵錯工具在中斷點中斷時，您可以檢查，並執行 hello 雲端 hello 程式時，變更變數的值。</span><span class="sxs-lookup"><span data-stu-id="65165-220">When hello debugger breaks at your breakpoint, you can examine and change variable values while hello program is running hello cloud.</span></span> <span data-ttu-id="65165-221">在 hello 下列圖例 hello 偵錯工具會顯示 hello hello blobInfo 物件傳來 toohello GenerateThumbnail 方法的內容。</span><span class="sxs-lookup"><span data-stu-id="65165-221">In hello following illustration hello debugger shows hello contents of hello blobInfo object that was passed toohello GenerateThumbnail method.</span></span>

     ![偵錯工具中的 blobInfo 物件](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. <span data-ttu-id="65165-223">按 F5 toocontinue 執行。</span><span class="sxs-lookup"><span data-stu-id="65165-223">Press F5 toocontinue running.</span></span>

     <span data-ttu-id="65165-224">hello GenerateThumbnail 方法完成建立 hello 縮圖。</span><span class="sxs-lookup"><span data-stu-id="65165-224">hello GenerateThumbnail method finishes creating hello thumbnail.</span></span>
12. <span data-ttu-id="65165-225">在 hello 瀏覽器中重新整理 hello 索引頁面，您會看見 hello 縮圖。</span><span class="sxs-lookup"><span data-stu-id="65165-225">In hello browser, refresh hello Index page and you see hello thumbnail.</span></span>
13. <span data-ttu-id="65165-226">在 Visual Studio 中，請按 SHIFT + F5 toostop 偵錯。</span><span class="sxs-lookup"><span data-stu-id="65165-226">In Visual Studio, press SHIFT+F5 toostop debugging.</span></span>
14. <span data-ttu-id="65165-227">在**伺服器總管**，hello ContosoAdsWebJob 節點上按一下滑鼠右鍵，然後按一下**檢視儀表板**。</span><span class="sxs-lookup"><span data-stu-id="65165-227">In **Server Explorer**, right-click hello ContosoAdsWebJob node and click **View Dashboard**.</span></span>
15. <span data-ttu-id="65165-228">使用您的 Azure 認證，登入，然後按一下 hello WebJob 名稱 toogo toohello 頁面上您的 web 工作。</span><span class="sxs-lookup"><span data-stu-id="65165-228">Sign in with your Azure credentials, and then click hello WebJob name toogo toohello page for your WebJob.</span></span>

     ![按一下 ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     <span data-ttu-id="65165-230">hello 儀表板會顯示該 hello GenerateThumbnail 最近執行的函式。</span><span class="sxs-lookup"><span data-stu-id="65165-230">hello Dashboard shows that hello GenerateThumbnail function executed recently.</span></span>

     <span data-ttu-id="65165-231">(hello 您按一下 下一次**檢視儀表板**、 您沒有在中，toosign 和 hello 瀏覽器連結直接 toohello 頁面為您的 web 工作。)</span><span class="sxs-lookup"><span data-stu-id="65165-231">(hello next time you click **View Dashboard**, you don't have toosign in, and hello browser goes directly toohello page for your WebJob.)</span></span>
16. <span data-ttu-id="65165-232">按一下 hello 函式名稱 toosee 詳細 hello 函式執行。</span><span class="sxs-lookup"><span data-stu-id="65165-232">Click hello function name toosee details about hello function execution.</span></span>

     ![函數詳細資料](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

<span data-ttu-id="65165-234">如果您的函式[寫入記錄檔](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)，您可以按一下**ToggleOutput** toosee 它們。</span><span class="sxs-lookup"><span data-stu-id="65165-234">If your function [wrote logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), you could click **ToggleOutput** toosee them.</span></span>

## <a name="notes-about-remote-debugging"></a><span data-ttu-id="65165-235">遠端偵錯注意事項</span><span class="sxs-lookup"><span data-stu-id="65165-235">Notes about remote debugging</span></span>
* <span data-ttu-id="65165-236">不建議在生產環境中執行偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="65165-236">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="65165-237">如果您的生產環境 web 應用程式未向外延展 toomultiple 伺服器執行個體中，偵錯會使 hello 回應 tooother 要求 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="65165-237">If your production web app is not scaled out toomultiple server instances, debugging will prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="65165-238">如果您這樣做有多個 web 伺服器執行個體，當您附加 toohello 偵錯工具就會是隨機的執行個體，而且您有任何方式 tooensure 該後續的瀏覽器要求將會傳送 toothat 執行個體。</span><span class="sxs-lookup"><span data-stu-id="65165-238">If you do have multiple web server instances, when you attach toohello debugger you'll get a random instance, and you have no way tooensure that subsequent browser requests will go toothat instance.</span></span> <span data-ttu-id="65165-239">此外，您通常不會部署偵錯組建 tooproduction，而且編譯器最佳化的發行組建可能會使它不可能發生什麼事的 tooshow 一行一行地在原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="65165-239">Also, you typically don't deploy a debug build tooproduction, and compiler optimizations for release builds might make it impossible tooshow what is happening line by line in your source code.</span></span> <span data-ttu-id="65165-240">針對生產環境問題的疑難排解，您的最佳資源將是應用程式追蹤與 Web 伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-240">For troubleshooting production problems, your best resource is application tracing and web server logs.</span></span>
* <span data-ttu-id="65165-241">進行遠端偵錯時，避免長時間在中斷點停止運作。</span><span class="sxs-lookup"><span data-stu-id="65165-241">Avoid long stops at breakpoints when remote debugging.</span></span> <span data-ttu-id="65165-242">Azure 會將停止超過幾分鐘的處理序視為無回應的處理序，並將其關閉。</span><span class="sxs-lookup"><span data-stu-id="65165-242">Azure treats a process that is stopped for longer than a few minutes as an unresponsive process, and shuts it down.</span></span>
* <span data-ttu-id="65165-243">您正在偵錯時，hello 伺服器傳送資料 tooVisual Studio 中，但是可能會影響頻寬費用。</span><span class="sxs-lookup"><span data-stu-id="65165-243">While you're debugging, hello server is sending data tooVisual Studio, which could affect bandwidth charges.</span></span> <span data-ttu-id="65165-244">如需關於頻寬費率的詳細資訊，請參閱 [Azure 定價](https://azure.microsoft.com/pricing/calculator/)。</span><span class="sxs-lookup"><span data-stu-id="65165-244">For information about bandwidth rates, see [Azure Pricing](https://azure.microsoft.com/pricing/calculator/).</span></span>
* <span data-ttu-id="65165-245">請確定該 hello`debug`屬性 hello `compilation` hello 中的項目*Web.config* tootrue 設定檔。</span><span class="sxs-lookup"><span data-stu-id="65165-245">Make sure that hello `debug` attribute of hello `compilation` element in hello *Web.config* file is set tootrue.</span></span> <span data-ttu-id="65165-246">當您發行偵錯版組建組態時，它是預設設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="65165-246">It is set tootrue by default when you publish a debug build configuration.</span></span>

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* <span data-ttu-id="65165-247">如果您發現該 hello 偵錯工具不會逐步執行您想 toodebug 程式碼，您可能必須 toochange hello Just My Code 設定。</span><span class="sxs-lookup"><span data-stu-id="65165-247">If you find that hello debugger won't step into code that you want toodebug, you might have toochange hello Just My Code setting.</span></span>  <span data-ttu-id="65165-248">如需詳細資訊，請參閱[限制逐步執行 tooJust My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code)。</span><span class="sxs-lookup"><span data-stu-id="65165-248">For more information, see [Restrict stepping tooJust My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).</span></span>
* <span data-ttu-id="65165-249">當您啟用 hello 遠端偵錯功能，且在 48 小時後 hello 功能會自動關閉 hello 伺服器上會啟動計時器。</span><span class="sxs-lookup"><span data-stu-id="65165-249">A timer starts on hello server when you enable hello remote debugging feature, and after 48 hours hello feature is automatically turned off.</span></span> <span data-ttu-id="65165-250">此 48 小時的限制是為了安全與效能起見而設計的功能。</span><span class="sxs-lookup"><span data-stu-id="65165-250">This 48 hour limit is done for security and performance reasons.</span></span> <span data-ttu-id="65165-251">您可以輕鬆地 hello 功能重新開啟您要的次數。</span><span class="sxs-lookup"><span data-stu-id="65165-251">You can easily turn hello feature back on as many times as you like.</span></span> <span data-ttu-id="65165-252">當您不需要偵錯時，建議您將其保持為停用。</span><span class="sxs-lookup"><span data-stu-id="65165-252">We recommend leaving it disabled when you are not actively debugging.</span></span>
* <span data-ttu-id="65165-253">您可以手動附加 hello 偵錯工具 tooany 程序，不只 hello web 應用程式處理序 (w3wp.exe)。</span><span class="sxs-lookup"><span data-stu-id="65165-253">You can manually attach hello debugger tooany process, not only hello web app process (w3wp.exe).</span></span> <span data-ttu-id="65165-254">如需如何 toouse 偵錯 Visual Studio 中的模式的詳細資訊，請參閱[Visual Studio 偵錯](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65165-254">For more information about how toouse debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).</span></span>

## <span data-ttu-id="65165-255"><a name="logsoverview"></a>診斷記錄概觀</span><span class="sxs-lookup"><span data-stu-id="65165-255"><a name="logsoverview"></a>Diagnostic logs overview</span></span>
<span data-ttu-id="65165-256">Azure web 應用程式中執行的 ASP.NET 應用程式可以建立下列類型的記錄檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="65165-256">An ASP.NET application that runs in an Azure web app can create hello following kinds of logs:</span></span>

* <span data-ttu-id="65165-257">**應用程式追蹤記錄**</span><span class="sxs-lookup"><span data-stu-id="65165-257">**Application tracing logs**</span></span><br/>
  <span data-ttu-id="65165-258">hello 應用程式會建立這些記錄檔藉由呼叫方法的 hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="65165-258">hello application creates these logs by calling methods of hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) class.</span></span>
* <span data-ttu-id="65165-259">**Web 伺服器記錄**</span><span class="sxs-lookup"><span data-stu-id="65165-259">**Web server logs**</span></span><br/>
  <span data-ttu-id="65165-260">hello web 伺服器會建立每個 HTTP 要求 toohello web 應用程式的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="65165-260">hello web server creates a log entry for every HTTP request toohello web app.</span></span>
* <span data-ttu-id="65165-261">**詳細的錯誤訊息記錄**</span><span class="sxs-lookup"><span data-stu-id="65165-261">**Detailed error message logs**</span></span><br/>
  <span data-ttu-id="65165-262">hello web 伺服器會建立 HTML 網頁失敗的 HTTP 要求 （其會導致狀態碼 400 或更新版本） 的一些額外資訊。</span><span class="sxs-lookup"><span data-stu-id="65165-262">hello web server creates an HTML page with some additional information for failed HTTP requests (those that result in status code 400 or greater).</span></span>
* <span data-ttu-id="65165-263">**失敗要求追蹤記錄**</span><span class="sxs-lookup"><span data-stu-id="65165-263">**Failed request tracing logs**</span></span><br/>
  <span data-ttu-id="65165-264">hello web 伺服器會建立為失敗的 HTTP 要求的詳細的追蹤資訊的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="65165-264">hello web server creates an XML file with detailed tracing information for failed HTTP requests.</span></span> <span data-ttu-id="65165-265">hello web 伺服器也會提供 XSL 檔案 tooformat hello XML 的瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="65165-265">hello web server also provides an XSL file tooformat hello XML in a browser.</span></span>

<span data-ttu-id="65165-266">記錄影響 web 應用程式效能，因此 Azure 可讓您 hello 能力 tooenable 或視需要停用記錄檔的每個型別。</span><span class="sxs-lookup"><span data-stu-id="65165-266">Logging affects web app performance, so Azure gives you hello ability tooenable or disable each type of log as needed.</span></span> <span data-ttu-id="65165-267">對於應用程式記錄，您可以指定只寫入高於特定嚴重性層級的記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-267">For application logs, you can specify that only logs above a certain severity level should be written.</span></span> <span data-ttu-id="65165-268">當您建立新的 Web 應用程式時，預設會停用所有記錄功能。</span><span class="sxs-lookup"><span data-stu-id="65165-268">When you create a new web app, by default all logging is disabled.</span></span>

<span data-ttu-id="65165-269">記錄檔寫入 toofiles *LogFiles* hello 您 web 應用程式，並且是可透過 FTP 存取的檔案系統中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="65165-269">Logs are written toofiles in a *LogFiles* folder in hello file system of your web app and are accessible via FTP.</span></span> <span data-ttu-id="65165-270">Web 伺服器記錄檔和應用程式記錄檔也可以寫入 tooan Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65165-270">Web server logs and application logs can also be written tooan Azure Storage account.</span></span> <span data-ttu-id="65165-271">您可以保留更大的磁碟區的儲存體帳戶，而不是在 hello 檔案系統中的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-271">You can retain a greater volume of logs in a storage account than is possible in hello file system.</span></span> <span data-ttu-id="65165-272">當您使用 hello 檔案系統時，您限制的 tooa 最大值是 100 mb 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-272">You're limited tooa maximum of 100 megabytes of logs when you use hello file system.</span></span> <span data-ttu-id="65165-273">(檔案系統記錄僅適用於短期保留之用。</span><span class="sxs-lookup"><span data-stu-id="65165-273">(File system logs are only for short-term retention.</span></span> <span data-ttu-id="65165-274">Azure 後，刪除舊記錄檔 toomake 出空間給新的 hello 限制為止。）</span><span class="sxs-lookup"><span data-stu-id="65165-274">Azure deletes old log files toomake room for new ones after hello limit is reached.)</span></span>  

## <span data-ttu-id="65165-275"><a name="apptracelogs"></a>建立並檢視應用程式追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="65165-275"><a name="apptracelogs"></a>Create and view application trace logs</span></span>
<span data-ttu-id="65165-276">本節中，您將會執行下列工作 hello:</span><span class="sxs-lookup"><span data-stu-id="65165-276">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="65165-277">將追蹤陳述式 toohello web 專案中建立[開始使用 Azure 和 ASP.NET][GetStarted]。</span><span class="sxs-lookup"><span data-stu-id="65165-277">Add tracing statements toohello web project that you created in [Get started with Azure and ASP.NET][GetStarted].</span></span>
* <span data-ttu-id="65165-278">當您在本機執行 hello 專案時，請檢視 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-278">View hello logs when you run hello project locally.</span></span>
* <span data-ttu-id="65165-279">在 Azure 中執行的 hello 應用程式所產生時，請檢視 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-279">View hello logs as they are generated by hello application running in Azure.</span></span>

<span data-ttu-id="65165-280">如需 toocreate 應用程式在 WebJobs 的記錄檔資訊，請參閱[如何與 Azure 佇列儲存體使用 toowork hello WebJobs SDK-toowrite 記錄的方式](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)。</span><span class="sxs-lookup"><span data-stu-id="65165-280">For information about how toocreate application logs in WebJobs, see [How toowork with Azure queue storage using hello WebJobs SDK - How toowrite logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs).</span></span> <span data-ttu-id="65165-281">hello 下列指示來檢視記錄檔與控制它們如何儲存在 Azure 中適用於也 tooapplication WebJobs 所建立的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-281">hello following instructions for viewing logs and controlling how they're stored in Azure apply also tooapplication logs created by WebJobs.</span></span>

### <a name="add-tracing-statements-toohello-application"></a><span data-ttu-id="65165-282">加入追蹤陳述式 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="65165-282">Add tracing statements toohello application</span></span>
1. <span data-ttu-id="65165-283">開啟*Controllers\HomeController.cs*，並取代 hello `Index`， `About`，和`Contact`方法以 hello 下列程式碼中順序 tooadd`Trace`陳述式和`using`陳述式如`System.Diagnostics`:</span><span class="sxs-lookup"><span data-stu-id="65165-283">Open *Controllers\HomeController.cs*, and replace hello `Index`, `About`, and `Contact` methods with hello following code in order tooadd `Trace` statements and a `using` statement for `System.Diagnostics`:</span></span>

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. <span data-ttu-id="65165-284">新增`using System.Diagnostics;`hello 檔案的陳述式 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="65165-284">Add a `using System.Diagnostics;` statement toohello top of hello file.</span></span>

### <a name="view-hello-tracing-output-locally"></a><span data-ttu-id="65165-285">在本機輸出檢視 hello 追蹤</span><span class="sxs-lookup"><span data-stu-id="65165-285">View hello tracing output locally</span></span>
1. <span data-ttu-id="65165-286">按下 F5 toorun hello 應用程式中的偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="65165-286">Press F5 toorun hello application in debug mode.</span></span>

    <span data-ttu-id="65165-287">hello 預設追蹤接聽項寫入所有的追蹤輸出 toohello**輸出**視窗中的，連同其他偵錯輸出。</span><span class="sxs-lookup"><span data-stu-id="65165-287">hello default trace listener writes all trace output toohello **Output** window, along with other Debug output.</span></span> <span data-ttu-id="65165-288">hello 如下圖所示 hello hello 輸出追蹤陳述式，就像加入 toohello`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="65165-288">hello following illustration shows hello output from hello trace statements that you added toohello `Index` method.</span></span>

    ![偵錯視窗中的追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    <span data-ttu-id="65165-290">hello 下列步驟顯示如何 tooview 追蹤輸出網頁，而不需要在偵錯模式中編譯。</span><span class="sxs-lookup"><span data-stu-id="65165-290">hello following steps show how tooview trace output in a web page, without compiling in debug mode.</span></span>
2. <span data-ttu-id="65165-291">開啟 hello 應用程式 Web.config 檔案 (其中一個位於 hello 專案資料夾中的 hello)，然後加入`<system.diagnostics>`hello hello 結尾之前的 hello 檔案結尾處的項目`</configuration>`項目：</span><span class="sxs-lookup"><span data-stu-id="65165-291">Open hello application Web.config file (hello one located in hello project folder) and add a `<system.diagnostics>` element at hello end of hello file just before hello closing `</configuration>` element:</span></span>

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    <span data-ttu-id="65165-292">hello`WebPageTraceListener`可讓您檢視追蹤輸出，藉由瀏覽過`/trace.axd`。</span><span class="sxs-lookup"><span data-stu-id="65165-292">hello `WebPageTraceListener` lets you view trace output by browsing too`/trace.axd`.</span></span>
3. <span data-ttu-id="65165-293">新增<a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">追蹤項目</a>下`<system.web>`在 hello Web.config 檔案中，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="65165-293">Add a <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace element</a> under `<system.web>` in hello Web.config file, such as hello following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. <span data-ttu-id="65165-294">按 CTRL + F5 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65165-294">Press CTRL+F5 toorun hello application.</span></span>
5. <span data-ttu-id="65165-295">在 hello hello 瀏覽器視窗的網址列中加入*trace.axd* toohello URL，然後按 Enter （hello URL 會類似 toohttp://localhost:53370/trace.axd）。</span><span class="sxs-lookup"><span data-stu-id="65165-295">In hello address bar of hello browser window, add *trace.axd* toohello URL, and then press Enter (hello URL will be similar toohttp://localhost:53370/trace.axd).</span></span>
6. <span data-ttu-id="65165-296">在 hello**應用程式追蹤**頁面上，按一下**檢視詳細資料**hello 第一行 (無法 hello BrowserLink 列)。</span><span class="sxs-lookup"><span data-stu-id="65165-296">On hello **Application Trace** page, click **View Details** on hello first line (not hello BrowserLink line).</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    <span data-ttu-id="65165-298">hello**要求詳細資料**頁面出現時，在 hello**追蹤資訊**> 一節，您會看到您加入 toohello hello 追蹤陳述式從 hello 輸出`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="65165-298">hello **Request Details** page appears, and in hello **Trace Information** section you see hello output from hello trace statements that you added toohello `Index` method.</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    <span data-ttu-id="65165-300">根據預設， `trace.axd` 只能在本機使用。</span><span class="sxs-lookup"><span data-stu-id="65165-300">By default, `trace.axd` is only available locally.</span></span> <span data-ttu-id="65165-301">如果您想 toomake 它可從遠端的 web 應用程式，您可以加入`localOnly="false"`toohello `trace` hello 中的項目*Web.config*檔案 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="65165-301">If you wanted toomake it available from a remote web app, you could add `localOnly="false"` toohello `trace` element in hello *Web.config* file, as shown in hello following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    <span data-ttu-id="65165-302">不過，啟用`trace.axd`在生產環境中的 web 應用程式通常不建議基於安全性理由，並在 hello 下列各節中，您會看到您更輕鬆的方式 tooread 追蹤記錄的 Azure web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="65165-302">However, enabling `trace.axd` in a production web app is generally not recommended for security reasons, and in hello following sections you'll see an easier way tooread tracing logs in an Azure web app.</span></span>

### <a name="view-hello-tracing-output-in-azure"></a><span data-ttu-id="65165-303">在 Azure 中檢視 hello 追蹤輸出</span><span class="sxs-lookup"><span data-stu-id="65165-303">View hello tracing output in Azure</span></span>
1. <span data-ttu-id="65165-304">在**方案總管 中**，hello web 專案上按一下滑鼠右鍵，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="65165-304">In **Solution Explorer**, right-click hello web project and click **Publish**.</span></span>
2. <span data-ttu-id="65165-305">在 hello**發行 Web**對話方塊中，按一下 **發行**。</span><span class="sxs-lookup"><span data-stu-id="65165-305">In hello **Publish Web** dialog box, click **Publish**.</span></span>

    <span data-ttu-id="65165-306">Visual Studio 發行您的更新之後，它會開啟瀏覽器視窗 tooyour 首頁 (假設未清除**目的地 URL**上 hello**連接** 索引標籤)。</span><span class="sxs-lookup"><span data-stu-id="65165-306">After Visual Studio publishes your update, it opens a browser window tooyour home page (assuming you didn't clear **Destination URL** on hello **Connection** tab).</span></span>
3. <span data-ttu-id="65165-307">在 [伺服器總管] 中，以滑鼠右鍵按一下您的 Web 應用程式，然後選取 [檢視串流記錄]。</span><span class="sxs-lookup"><span data-stu-id="65165-307">In **Server Explorer**, right-click your web app and select **View Streaming Logs**.</span></span>

    ![在內容功能表中檢視串流記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    <span data-ttu-id="65165-309">hello**輸出**視窗會顯示您所連接的 toohello 記錄串流服務，並會將通知行記錄 toodisplay 不會按照每一分鐘。</span><span class="sxs-lookup"><span data-stu-id="65165-309">hello **Output** window shows that you are connected toohello log-streaming service, and adds a notification line each minute that goes by without a log toodisplay.</span></span>

    ![在內容功能表中檢視串流記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. <span data-ttu-id="65165-311">在 hello 瀏覽器視窗，其中顯示您應用程式的首頁，按一下 **連絡人**。</span><span class="sxs-lookup"><span data-stu-id="65165-311">In hello browser window that shows your application home page, click **Contact**.</span></span>

    <span data-ttu-id="65165-312">您在幾秒 hello 來自 hello 錯誤層級的追蹤輸出內加入 toohello`Contact`方法會出現在 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="65165-312">Within a few seconds hello output from hello error-level trace you added toohello `Contact` method appears in hello **Output** window.</span></span>

    ![輸出視窗中的錯誤追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    <span data-ttu-id="65165-314">Visual Studio 只會顯示錯誤層級追蹤，因為這是當您啟用 hello 記錄檔監視服務的 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="65165-314">Visual Studio is only showing error-level traces because that is hello default setting when you enable hello log monitoring service.</span></span> <span data-ttu-id="65165-315">當您建立新的 Azure web 應用程式時，所有的記錄預設會停用，因為先前開啟 hello 設定 頁面時看見：</span><span class="sxs-lookup"><span data-stu-id="65165-315">When you create a new Azure web app, all logging is disabled by default, as you saw when you opened hello settings page earlier:</span></span>

    ![應用程式記錄功能關閉](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    <span data-ttu-id="65165-317">不過，當您選取**檢視串流記錄**，Visual Studio 會自動變更**應用程式 Logging(File System)**太**錯誤**，這表示錯誤層級記錄檔報告。</span><span class="sxs-lookup"><span data-stu-id="65165-317">However, when you selected **View Streaming Logs**, Visual Studio automatically changed **Application Logging(File System)** too**Error**, which means error-level logs get reported.</span></span> <span data-ttu-id="65165-318">在追蹤記錄的所有訂單 toosee，您可以變更此設定太**Verbose**。</span><span class="sxs-lookup"><span data-stu-id="65165-318">In order toosee all of your tracing logs, you can change this setting too**Verbose**.</span></span> <span data-ttu-id="65165-319">當您選取低於錯誤的嚴重性層級時，將一併回報較高嚴重性層級的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-319">When you select a severity level lower than error, all logs for higher severity levels are also reported.</span></span> <span data-ttu-id="65165-320">因此當您選取詳細資訊時，您會同時看到資訊、警告與錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-320">So when you select verbose, you also see information, warning, and error logs.</span></span>  

1. <span data-ttu-id="65165-321">在**伺服器總管**hello web 應用程式，以滑鼠右鍵按一下，然後按**檢視設定**如先前般。</span><span class="sxs-lookup"><span data-stu-id="65165-321">In **Server Explorer**, right-click hello web app, and then click **View Settings** as you did earlier.</span></span>
2. <span data-ttu-id="65165-322">變更**的應用程式記錄 （檔案系統）**太**Verbose**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="65165-322">Change **Application Logging (File System)** too**Verbose**, and then click **Save**.</span></span>

    ![設定追蹤層級 tooVerbose](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. <span data-ttu-id="65165-324">現在顯示 hello 瀏覽器視窗中您**連絡人**頁面上，按一下**首頁**，然後按一下**有關**，然後按一下**連絡人**。</span><span class="sxs-lookup"><span data-stu-id="65165-324">In hello browser window that is now showing your **Contact** page, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="65165-325">在幾秒內，hello**輸出** 視窗會顯示所有的追蹤輸出。</span><span class="sxs-lookup"><span data-stu-id="65165-325">Within a few seconds, hello **Output** window shows all of your tracing output.</span></span>

    ![詳細資訊追蹤輸出](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    <span data-ttu-id="65165-327">在本節中，您已使用 Azure Web 應用程式設定來啟用與停用記錄功能。</span><span class="sxs-lookup"><span data-stu-id="65165-327">In this section you enabled and disabled logging by using Azure web app settings.</span></span> <span data-ttu-id="65165-328">您也可以啟用和停用透過修改 hello Web.config 檔案的追蹤接聽項。</span><span class="sxs-lookup"><span data-stu-id="65165-328">You can also enable and disable trace listeners by modifying hello Web.config file.</span></span> <span data-ttu-id="65165-329">不過，修改 hello Web.config 檔案會導致 hello 應用程式網域 toorecycle，但在啟用記錄功能，透過 hello web 應用程式設定並不需要的。</span><span class="sxs-lookup"><span data-stu-id="65165-329">However, modifying hello Web.config file causes hello app domain toorecycle, while enabling logging via hello web app configuration doesn't do that.</span></span> <span data-ttu-id="65165-330">如果 hello 問題會很長的時間 tooreproduce，或斷斷續續，回收 hello 應用程式定義域可能"修正 」 並強迫您 toowait 直到它再次發生。</span><span class="sxs-lookup"><span data-stu-id="65165-330">If hello problem takes a long time tooreproduce, or is intermittent, recycling hello app domain might "fix" it and force you toowait until it happens again.</span></span> <span data-ttu-id="65165-331">在 Azure 中啟用診斷功能不會出現此情況，因此您可以立即開始擷取錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="65165-331">Enabling diagnostics in Azure doesn't do this, so you can start capturing error information immediately.</span></span>

### <a name="output-window-features"></a><span data-ttu-id="65165-332">輸出視窗功能</span><span class="sxs-lookup"><span data-stu-id="65165-332">Output window features</span></span>
<span data-ttu-id="65165-333">hello **Azure 記錄檔** 索引標籤的 hello**輸出**視窗有數個按鈕和文字方塊：</span><span class="sxs-lookup"><span data-stu-id="65165-333">hello **Azure Logs** tab of hello **Output** Window has several buttons and a text box:</span></span>

![記錄索引標籤按鈕](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

<span data-ttu-id="65165-335">這些執行 hello 下列函式：</span><span class="sxs-lookup"><span data-stu-id="65165-335">These perform hello following functions:</span></span>

* <span data-ttu-id="65165-336">清除 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="65165-336">Clear hello **Output** window.</span></span>
* <span data-ttu-id="65165-337">啟用或停用自動換行。</span><span class="sxs-lookup"><span data-stu-id="65165-337">Enable or disable word wrap.</span></span>
* <span data-ttu-id="65165-338">啟動或停止監視記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-338">Start or stop monitoring logs.</span></span>
* <span data-ttu-id="65165-339">指定的記錄 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="65165-339">Specify which logs toomonitor.</span></span>
* <span data-ttu-id="65165-340">下載記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-340">Download logs.</span></span>
* <span data-ttu-id="65165-341">依據搜尋字串或規則運算式篩選記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-341">Filter logs based on a search string or a regular expression.</span></span>
* <span data-ttu-id="65165-342">關閉 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="65165-342">Close hello **Output** window.</span></span>

<span data-ttu-id="65165-343">如果您輸入搜尋字串或規則運算式時，Visual Studio 會篩選在 hello 用戶端記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="65165-343">If you enter a search string or regular expression, Visual Studio filters logging information at hello client.</span></span> <span data-ttu-id="65165-344">這表示 hello 顯示 hello 記錄檔之後，您可以輸入 hello 準則**輸出**視窗，而且您可以變更篩選條件而不需要 tooregenerate hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-344">That means you can enter hello criteria after hello logs are displayed in hello **Output** window and you can change filtering criteria without having tooregenerate hello logs.</span></span>

## <span data-ttu-id="65165-345"><a name="webserverlogs"></a>檢視 Web 伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="65165-345"><a name="webserverlogs"></a>View web server logs</span></span>
<span data-ttu-id="65165-346">Web 伺服器記錄檔記錄所有 HTTP 活動 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65165-346">Web server logs record all HTTP activity for hello web app.</span></span> <span data-ttu-id="65165-347">在順序 toosee 中 hello**輸出**視窗有 tooenable hello 的 web 應用程式，並告知 Visual Studio 的 toomonitor 它們。</span><span class="sxs-lookup"><span data-stu-id="65165-347">In order toosee them in hello **Output** window you have tooenable them for hello web app and tell Visual Studio that you want toomonitor them.</span></span>

1. <span data-ttu-id="65165-348">在 hello **Azure Web 應用程式組態** 索引標籤中開啟**伺服器總管**，也變更 Web 伺服器記錄**上**，然後按一下**儲存**.</span><span class="sxs-lookup"><span data-stu-id="65165-348">In hello **Azure Web App Configuration** tab that you opened from **Server Explorer**, change Web Server Logging too**On**, and then click **Save**.</span></span>

    ![啟用 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. <span data-ttu-id="65165-350">在 [hello**輸出**視窗中，按一下 hello**指定哪些 Azure 記錄檔 toomonitor** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65165-350">In hello **Output** Window, click hello **Specify which Azure logs toomonitor** button.</span></span>

    ![指定哪些 Azure 記錄檔 toomonitor](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. <span data-ttu-id="65165-352">在 hello **Azure 記錄選項**對話方塊中，選取**Web 伺服器記錄檔**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="65165-352">In hello **Azure Logging Options** dialog box, select **Web server logs**, and then click **OK**.</span></span>

    ![監視 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. <span data-ttu-id="65165-354">在顯示 hello web 應用程式的 hello 瀏覽器視窗中按一下**首頁**，然後按一下**有關**，然後按一下**連絡人**。</span><span class="sxs-lookup"><span data-stu-id="65165-354">In hello browser window that shows hello web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="65165-355">hello 應用程式記錄檔通常會先出現，後面接著 hello web 伺服器記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-355">hello application logs generally appear first, followed by hello web server logs.</span></span> <span data-ttu-id="65165-356">您可能必須 toowait hello 一些記錄 tooappear。</span><span class="sxs-lookup"><span data-stu-id="65165-356">You might have toowait a while for hello logs tooappear.</span></span>

    ![輸出視窗中的 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

<span data-ttu-id="65165-358">根據預設，當您第一次啟用 web 伺服器記錄檔時使用 Visual Studio 中，Azure 會寫入 hello 記錄 toohello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="65165-358">By default, when you first enable web server logs by using Visual Studio, Azure writes hello logs toohello file system.</span></span> <span data-ttu-id="65165-359">或者，您可以使用 hello Azure 入口網站 web 伺服器記錄檔的 toospecify 應該要撰寫 tooa blob 容器的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65165-359">As an alternative, you can use hello Azure portal toospecify that web server logs should be written tooa blob container in a storage account.</span></span>

<span data-ttu-id="65165-360">如果您使用 hello tooenable 入口網站的 web 伺服器記錄 tooan Azure 儲存體帳戶，然後再停用記錄在 Visual Studio 中，當您重新啟用登入 Visual Studio 會還原您的儲存體帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="65165-360">If you use hello portal tooenable web server logging tooan Azure storage account, and then disable logging in Visual Studio, when you re-enable logging in Visual Studio your storage account settings are restored.</span></span>

## <span data-ttu-id="65165-361"><a name="detailederrorlogs"></a>檢視詳細的錯誤訊息記錄</span><span class="sxs-lookup"><span data-stu-id="65165-361"><a name="detailederrorlogs"></a>View detailed error message logs</span></span>
<span data-ttu-id="65165-362">針對導致錯誤回應代碼 (400 或以上) 之 HTTP 要求，詳細的錯誤訊息記錄可提供部分額外資訊。</span><span class="sxs-lookup"><span data-stu-id="65165-362">Detailed error logs provide some additional information about HTTP requests that result in error response codes (400 or above).</span></span> <span data-ttu-id="65165-363">在訂單 toosee 中 hello**輸出**視窗中，您有 tooenable hello 的 web 應用程式，並告知 Visual Studio 的 toomonitor 它們。</span><span class="sxs-lookup"><span data-stu-id="65165-363">In order toosee them in hello **Output** window, you have tooenable them for hello web app and tell Visual Studio that you want toomonitor them.</span></span>

1. <span data-ttu-id="65165-364">在 [hello **Azure Web 應用程式組態**] 索引標籤中開啟**伺服器總管**，變更**詳細的錯誤訊息**太**上**，和然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="65165-364">In hello **Azure Web App Configuration** tab that you opened from **Server Explorer**, change **Detailed Error Messages** too**On**, and then click **Save**.</span></span>

    ![啟用詳細的錯誤訊息](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. <span data-ttu-id="65165-366">在 [hello**輸出**視窗中，按一下 hello**指定哪些 Azure 記錄檔 toomonitor** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65165-366">In hello **Output** Window, click hello **Specify which Azure logs toomonitor** button.</span></span>
3. <span data-ttu-id="65165-367">在 hello **Azure 記錄選項**對話方塊中，按一下**所有記錄檔**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="65165-367">In hello **Azure Logging Options** dialog box, click **All logs**, and then click **OK**.</span></span>

    ![監視所有記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. <span data-ttu-id="65165-369">在 hello hello 瀏覽器視窗的網址列中加入額外的字元 toohello URL toocause 404 錯誤 (例如， `http://localhost:53370/Home/Contactx`)，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="65165-369">In hello address bar of hello browser window, add an extra character toohello URL toocause a 404 error (for example, `http://localhost:53370/Home/Contactx`), and press Enter.</span></span>

    <span data-ttu-id="65165-370">幾秒之後 hello 詳細的錯誤記錄檔會出現在 Visual Studio hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="65165-370">After several seconds hello detailed error log appears in hello Visual Studio **Output** window.</span></span>

    ![輸出視窗中的詳細的錯誤記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    <span data-ttu-id="65165-372">控制並按一下滑鼠左鍵 hello 連結 toosee hello 記錄輸出格式的瀏覽器中：</span><span class="sxs-lookup"><span data-stu-id="65165-372">Control+click hello link toosee hello log output formatted in a browser:</span></span>

    ![瀏覽器視窗中的詳細的錯誤記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <span data-ttu-id="65165-374"><a name="downloadlogs"></a>下載檔案系統記錄</span><span class="sxs-lookup"><span data-stu-id="65165-374"><a name="downloadlogs"></a>Download file system logs</span></span>
<span data-ttu-id="65165-375">您可以在 hello 監視任何記錄檔**輸出**視窗也可以下載為*.zip*檔案。</span><span class="sxs-lookup"><span data-stu-id="65165-375">Any logs that you can monitor in hello **Output** window can also be downloaded as a *.zip* file.</span></span>

1. <span data-ttu-id="65165-376">在 hello**輸出**視窗中，按一下**下載串流記錄**。</span><span class="sxs-lookup"><span data-stu-id="65165-376">In hello **Output** window, click **Download Streaming Logs**.</span></span>

    ![記錄索引標籤按鈕](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    <span data-ttu-id="65165-378">檔案總管 中開啟 tooyour*下載*資料夾以 hello 下載選取的檔案。</span><span class="sxs-lookup"><span data-stu-id="65165-378">File Explorer opens tooyour *Downloads* folder with hello downloaded file selected.</span></span>

    ![下載的檔案](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. <span data-ttu-id="65165-380">擷取 hello *.zip*檔案，而且您會看到下列資料夾結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="65165-380">Extract hello *.zip* file, and you see hello following folder structure:</span></span>

    ![下載的檔案](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * <span data-ttu-id="65165-382">應用程式的追蹤記錄檔位於*.txt*檔案在 hello *LogFiles\Application*資料夾。</span><span class="sxs-lookup"><span data-stu-id="65165-382">Application tracing logs are in *.txt* files in hello *LogFiles\Application* folder.</span></span>
   * <span data-ttu-id="65165-383">Web 伺服器記錄檔位於*.log*檔案在 hello *LogFiles\http\RawLogs*資料夾。</span><span class="sxs-lookup"><span data-stu-id="65165-383">Web server logs are in *.log* files in hello *LogFiles\http\RawLogs* folder.</span></span> <span data-ttu-id="65165-384">您可以使用一種工具，例如[記錄檔剖析器](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659)tooview 和管理這些檔案。</span><span class="sxs-lookup"><span data-stu-id="65165-384">You can use a tool such as [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview and manipulate these files.</span></span>
   * <span data-ttu-id="65165-385">詳細的錯誤訊息記錄檔位於*.html*檔案在 hello *LogFiles\DetailedErrors*資料夾。</span><span class="sxs-lookup"><span data-stu-id="65165-385">Detailed error message logs are in *.html* files in hello *LogFiles\DetailedErrors* folder.</span></span>

     <span data-ttu-id="65165-386">(hello*部署*原始檔控制發行; 建立檔案的資料夾是沒有任何項目相關的 tooVisual Studio 發行功能。</span><span class="sxs-lookup"><span data-stu-id="65165-386">(hello *deployments* folder is for files created by source control publishing; it doesn't have anything related tooVisual Studio publishing.</span></span> <span data-ttu-id="65165-387">hello *Git*資料夾是追蹤相關的 toosource 控制發行和 hello 記錄檔案串流服務。)</span><span class="sxs-lookup"><span data-stu-id="65165-387">hello *Git* folder is for traces related toosource control publishing and hello log file streaming service.)</span></span>  

## <span data-ttu-id="65165-388"><a name="storagelogs"></a>檢視儲存體記錄</span><span class="sxs-lookup"><span data-stu-id="65165-388"><a name="storagelogs"></a>View storage logs</span></span>
<span data-ttu-id="65165-389">應用程式的追蹤記錄檔也可以傳送 tooan Azure 儲存體帳戶，您可以在 Visual Studio 中檢視它們。</span><span class="sxs-lookup"><span data-stu-id="65165-389">Application tracing logs can also be sent tooan Azure storage account, and you can view them in Visual Studio.</span></span> <span data-ttu-id="65165-390">您會建立儲存體帳戶、 啟用 hello 傳統入口網站中的儲存體記錄及檢視這些 hello toodo**記錄** 索引標籤的 hello **Azure Web 應用程式**視窗。</span><span class="sxs-lookup"><span data-stu-id="65165-390">toodo that you'll create a storage account, enable storage logs in hello classic portal, and view them in hello **Logs** tab of hello **Azure Web App** window.</span></span>

<span data-ttu-id="65165-391">您可以傳送記錄檔 tooany 或所有三個目的地：</span><span class="sxs-lookup"><span data-stu-id="65165-391">You can send logs tooany or all of three destinations:</span></span>

* <span data-ttu-id="65165-392">hello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="65165-392">hello file system.</span></span>
* <span data-ttu-id="65165-393">儲存體帳戶資料表。</span><span class="sxs-lookup"><span data-stu-id="65165-393">Storage account tables.</span></span>
* <span data-ttu-id="65165-394">儲存體帳戶 Blob。</span><span class="sxs-lookup"><span data-stu-id="65165-394">Storage account blobs.</span></span>

<span data-ttu-id="65165-395">您可以為每個目的地指定不同的嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="65165-395">You can specify a different severity level for each destination.</span></span>

<span data-ttu-id="65165-396">資料表可讓您輕鬆 tooview 上線，記錄檔的詳細資料，以及它們支援資料流。您可以查詢資料表中的記錄檔，並查看新的記錄檔，正在建立時的方式。</span><span class="sxs-lookup"><span data-stu-id="65165-396">Tables make it easy tooview details of logs online, and they support streaming; you can query logs in tables and see new logs as they are being created.</span></span> <span data-ttu-id="65165-397">輕鬆 toodownload 記錄檔中的檔案和 tooanalyze blob 讓它們使用 HDInsight，因為 HDInsight 知道如何使用 blob 儲存體 toowork。</span><span class="sxs-lookup"><span data-stu-id="65165-397">Blobs make it easy toodownload logs in files and tooanalyze them using HDInsight, because HDInsight knows how toowork with blob storage.</span></span> <span data-ttu-id="65165-398">如需詳細資訊，請參閱 **資料儲存體選項 (運用 Azure 建構真實的雲端應用程式)** 中的 [Hadoop 與 MapReduce](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options)(英文)。</span><span class="sxs-lookup"><span data-stu-id="65165-398">For more information, see **Hadoop and MapReduce** in [Data Storage Options (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).</span></span>

<span data-ttu-id="65165-399">您目前沒有檔案系統記錄檔集 tooverbose 層級;hello 下列步驟引導您設定的資訊層級的記錄檔 toogo toostorage 帳戶資料表。</span><span class="sxs-lookup"><span data-stu-id="65165-399">You currently have file system logs set tooverbose level; hello following steps walk you through setting up information level logs toogo toostorage account tables.</span></span> <span data-ttu-id="65165-400">資訊層級代表所有藉由呼叫 `Trace.TraceInformation`、`Trace.TraceWarning` 與 `Trace.TraceError` 的記錄都會顯示出來，但不會顯示藉由呼叫 `Trace.WriteLine` 所建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-400">Information level means all logs created by calling `Trace.TraceInformation`, `Trace.TraceWarning`, and `Trace.TraceError` will be displayed, but not logs created by calling `Trace.WriteLine`.</span></span>

<span data-ttu-id="65165-401">儲存體帳戶提供更多的儲存體和記錄檔的長期保留比較 toohello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="65165-401">Storage accounts offer more storage and longer-lasting retention for logs compared toohello file system.</span></span> <span data-ttu-id="65165-402">追蹤記錄檔 toostorage 傳送應用程式的另一個好處就是您取得一些額外的資訊不會從檔案系統記錄檔的每個記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-402">Another advantage of sending application tracing logs toostorage is that you get some additional information with each log that you don't get from file system logs.</span></span>

1. <span data-ttu-id="65165-403">以滑鼠右鍵按一下**儲存體**底下 hello Azure 的節點，然後按一下**建立儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="65165-403">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>

![建立儲存體帳戶](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. <span data-ttu-id="65165-405">在 [hello**建立儲存體帳戶**] 對話方塊中，輸入 hello 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="65165-405">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="65165-406">hello 名稱必須是必須是唯一的 (沒有其他的 Azure 儲存體帳戶可以有 hello 相同的名稱)。</span><span class="sxs-lookup"><span data-stu-id="65165-406">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="65165-407">如果您輸入的 hello 名稱已在使用您會得到機會 toochange 它。</span><span class="sxs-lookup"><span data-stu-id="65165-407">If hello name you enter is already in use you'll get a chance toochange it.</span></span>

    <span data-ttu-id="65165-408">hello 儲存體帳戶將會是 URL tooaccess *{name}*。.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="65165-408">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
2. <span data-ttu-id="65165-409">設定 hello**地區或同質群組**下拉式選單 toohello 區域最接近 tooyou。</span><span class="sxs-lookup"><span data-stu-id="65165-409">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="65165-410">此設定會指定哪個 Azure 資料中心將會主控您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65165-410">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="65165-411">此教學課程中您選擇不明顯的差異，但生產環境 web 應用程式要為您的 web 伺服器和您在 hello 的儲存體帳戶 toobe 相同區域 toominimize 延遲和資料輸出費用。</span><span class="sxs-lookup"><span data-stu-id="65165-411">For this tutorial your choice won't make a noticeable difference, but for a production web app you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="65165-412">hello web 應用程式 （您將在稍後建立） 應該在為關閉，可能 toohello 瀏覽器存取 web 應用程式的順序 toominimize 延遲地區執行。</span><span class="sxs-lookup"><span data-stu-id="65165-412">hello web app (which you'll create later) should run in a region as close as possible toohello browsers accessing your web app in order toominimize latency.</span></span>
3. <span data-ttu-id="65165-413">設定 hello**複寫**下拉式清單也列出**本機備援**。</span><span class="sxs-lookup"><span data-stu-id="65165-413">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>
   
    <span data-ttu-id="65165-414">儲存體帳戶啟用地理複寫時，儲存的 hello 內容是複寫的 tooa 次要資料中心 tooenable 容錯移轉 toothat 位置發生重大災害 hello 主要位置中。</span><span class="sxs-lookup"><span data-stu-id="65165-414">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="65165-415">地理區域複寫會引發額外成本。</span><span class="sxs-lookup"><span data-stu-id="65165-415">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="65165-416">針對測試和開發的帳戶，您通常不想要 toopay 地理複寫。</span><span class="sxs-lookup"><span data-stu-id="65165-416">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="65165-417">如需詳細資訊，請參閱 [建立、管理或刪除儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="65165-417">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
4. <span data-ttu-id="65165-418">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="65165-418">Click **Create**.</span></span>

    ![New storage account](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. <span data-ttu-id="65165-420">Hello Visual Studio 中**Azure Web 應用程式**視窗中，按一下 hello**記錄**索引標籤，然後再按一下**管理入口網站中設定記錄**。</span><span class="sxs-lookup"><span data-stu-id="65165-420">In hello Visual Studio **Azure Web App** window, click hello **Logs** tab, and then click **Configure Logging in Management Portal**.</span></span>

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![設定記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    <span data-ttu-id="65165-422">這會開啟 hello**設定**hello 傳統入口網站 web 應用程式中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="65165-422">This opens hello **Configure** tab in hello classic portal for your web app.</span></span>
6. <span data-ttu-id="65165-423">Hello 傳統入口網站中的**設定**索引標籤上，向下捲動 toohello 應用程式診斷 區段，然後再變更**的應用程式記錄 （資料表儲存體）**太**上**。</span><span class="sxs-lookup"><span data-stu-id="65165-423">In hello classic portal's **Configure** tab, scroll down toohello application diagnostics section, and then change **Application Logging (Table Storage)** too**On**.</span></span>
7. <span data-ttu-id="65165-424">變更**記錄層級**太**資訊**。</span><span class="sxs-lookup"><span data-stu-id="65165-424">Change **Logging Level** too**Information**.</span></span>
8. <span data-ttu-id="65165-425">按一下 [管理資料表儲存體] 。</span><span class="sxs-lookup"><span data-stu-id="65165-425">Click **Manage Table Storage**.</span></span>

    ![按一下 [管理資料表儲存體]](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    <span data-ttu-id="65165-427">在 [hello**管理資料表儲存體應用程式診斷**] 方塊中，您可以選擇儲存體帳戶，如果您有一個以上。</span><span class="sxs-lookup"><span data-stu-id="65165-427">In hello **Manage table storage for application diagnostics** box, you can choose your storage account if you have more than one.</span></span> <span data-ttu-id="65165-428">您可以建立新的資料表，或是使用現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="65165-428">You can create a new table or use an existing one.</span></span>

    ![管理資料表儲存體](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. <span data-ttu-id="65165-430">在 hello**管理資料表儲存體應用程式診斷**方塊按一下 hello 核取記號 tooclose hello 方塊。</span><span class="sxs-lookup"><span data-stu-id="65165-430">In hello **Manage table storage for application diagnostics** box click hello check mark tooclose hello box.</span></span>
10. <span data-ttu-id="65165-431">Hello 傳統入口網站中的**設定**索引標籤上，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="65165-431">In hello classic portal's **Configure** tab, click **Save**.</span></span>
11. <span data-ttu-id="65165-432">在顯示 hello 應用程式的 web 應用程式的 hello 瀏覽器視窗中按一下**首頁**，然後按一下**有關**，然後按一下**連絡人**。</span><span class="sxs-lookup"><span data-stu-id="65165-432">In hello browser window that displays hello application web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

     <span data-ttu-id="65165-433">產生瀏覽這些網頁的 hello 記錄資訊會寫入 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65165-433">hello logging information produced by browsing these web pages will be written toohello storage account.</span></span>
12. <span data-ttu-id="65165-434">在 hello**記錄檔**hello 索引標籤**Azure Web 應用程式**視窗在 Visual Studio 中，按一下 **重新整理**下**診斷摘要**。</span><span class="sxs-lookup"><span data-stu-id="65165-434">In hello **Logs** tab of hello **Azure Web App** window in Visual Studio, click **Refresh** under **Diagnostic Summary**.</span></span>

     ![按一下 [重新整理]](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     <span data-ttu-id="65165-436">hello**診斷摘要**區段預設會顯示記錄檔中的 hello 過去 15 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="65165-436">hello **Diagnostic Summary** section shows logs for hello last 15 minutes by default.</span></span> <span data-ttu-id="65165-437">您可以變更 hello 期間 toosee 詳細的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-437">You can change hello period toosee more logs.</span></span>

     <span data-ttu-id="65165-438">(如果您收到 「 找不到資料表 」 錯誤，請確認您已經瀏覽 toohello 頁面執行 hello 追蹤在您啟用之後，**的應用程式記錄 （儲存體）**並在您按一下之後**儲存**。)</span><span class="sxs-lookup"><span data-stu-id="65165-438">(If you get a "table not found" error, verify that you browsed toohello pages that do hello tracing after you enabled **Application Logging (Storage)** and after you clicked **Save**.)</span></span>

     ![儲存體記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     <span data-ttu-id="65165-440">請注意，在此檢視您看到**處理序識別碼**和**Thread ID**針對每個記錄檔，就無法取得 hello 檔案系統記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="65165-440">Notice that in this view you see **Process ID** and **Thread ID** for each log, which you don't get in hello file system logs.</span></span> <span data-ttu-id="65165-441">您可以直接檢視 hello Azure 儲存體資料表，以查看其他欄位。</span><span class="sxs-lookup"><span data-stu-id="65165-441">You can see additional fields by viewing hello Azure storage table directly.</span></span>
13. <span data-ttu-id="65165-442">按一下 [View all application logs] 。</span><span class="sxs-lookup"><span data-stu-id="65165-442">Click **View all application logs**.</span></span>

     <span data-ttu-id="65165-443">hello 追蹤記錄檔資料表會出現在 hello Azure 儲存體資料表檢視器。</span><span class="sxs-lookup"><span data-stu-id="65165-443">hello trace log table appears in hello Azure storage table viewer.</span></span>

     <span data-ttu-id="65165-444">(如果您收到 「 序列包含任何項目 」 的錯誤，請開啟**伺服器總管**，展開您的儲存體帳戶下 hello hello 節點**Azure**節點，然後再以滑鼠右鍵按一下**資料表**按一下**重新整理**。)</span><span class="sxs-lookup"><span data-stu-id="65165-444">(If you get a "sequence contains no elements" error, open **Server Explorer**, expand hello node for your storage account under hello **Azure** node, and then right-click **Tables** and click **Refresh**.)</span></span>

     ![資料表檢視中的儲存體記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     <span data-ttu-id="65165-446">此檢視會顯示在其他任何檢視中都不會看到的額外欄位。</span><span class="sxs-lookup"><span data-stu-id="65165-446">This view shows additional fields you don't see in any other views.</span></span> <span data-ttu-id="65165-447">此檢視也可讓您 toofilter 記錄來建構查詢中使用特殊的查詢產生器 UI。</span><span class="sxs-lookup"><span data-stu-id="65165-447">This view also enables you toofilter logs by using special Query Builder UI for constructing a query.</span></span> <span data-ttu-id="65165-448">如需詳細資訊，請參閱 [使用伺服器總管瀏覽儲存體資源](http://msdn.microsoft.com/library/ff683677.aspx)中的「使用表格資源 - 篩選實體」。</span><span class="sxs-lookup"><span data-stu-id="65165-448">For more information, see Working with Table Resources - Filtering Entities in [Browsing Storage Resources with Server Explorer](http://msdn.microsoft.com/library/ff683677.aspx).</span></span>
14. <span data-ttu-id="65165-449">toolook 在 hello 詳細資料，是單一資料列中，按兩下 hello 資料列的其中一個。</span><span class="sxs-lookup"><span data-stu-id="65165-449">toolook at hello details for a single row, double-click one of hello rows.</span></span>

     ![伺服器總管中的追蹤資料表](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <span data-ttu-id="65165-451"><a name="failedrequestlogs"></a>檢視失敗要求追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="65165-451"><a name="failedrequestlogs"></a>View failed request tracing logs</span></span>
<span data-ttu-id="65165-452">當您需要的 IIS 中的案例，例如 URL 重寫或驗證問題的 HTTP 要求中的特殊處理的 toounderstand hello 詳細資料，失敗的要求追蹤記錄檔很有用。</span><span class="sxs-lookup"><span data-stu-id="65165-452">Failed request tracing logs are useful when you need toounderstand hello details of how IIS is handling an HTTP request, in scenarios such as URL rewriting or authentication problems.</span></span>

<span data-ttu-id="65165-453">Azure web 應用程式使用 hello 相同失敗要求的追蹤功能已可透過 IIS 7.0 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="65165-453">Azure web apps use hello same failed request tracing functionality that has been available with IIS 7.0 and later.</span></span> <span data-ttu-id="65165-454">您沒有存取 toohello IIS 設定，以設定哪些錯誤會記錄，不過。</span><span class="sxs-lookup"><span data-stu-id="65165-454">You don't have access toohello IIS settings that configure which errors get logged, however.</span></span> <span data-ttu-id="65165-455">當您啟用失敗要求追蹤時，將擷取所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="65165-455">When you enable failed request tracing, all errors are captured.</span></span>

<span data-ttu-id="65165-456">您可以使用 Visual Studio 來啟用失敗要求追蹤，但是您無法在 Visual Studio 中加以檢視。</span><span class="sxs-lookup"><span data-stu-id="65165-456">You can enable failed request tracing by using Visual Studio, but you can't view them in Visual Studio.</span></span> <span data-ttu-id="65165-457">這些記錄是 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="65165-457">These logs are XML files.</span></span> <span data-ttu-id="65165-458">hello 串流記錄服務只會監視會被視為在純文字模式下可讀取的檔案： *.txt*， *.html*，和*.log*檔案。</span><span class="sxs-lookup"><span data-stu-id="65165-458">hello streaming log service only monitors files that are deemed readable in plain text mode:  *.txt*, *.html*, and *.log* files.</span></span>

<span data-ttu-id="65165-459">您可以直接透過 FTP 或在本機使用 FTP 工具 toodownload 之後在瀏覽器中檢視失敗的要求追蹤記錄它們 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="65165-459">You can view failed request tracing logs in a browser directly via FTP or locally after using an FTP tool toodownload them tooyour local computer.</span></span> <span data-ttu-id="65165-460">在本節中，您將在瀏覽器中直接檢視。</span><span class="sxs-lookup"><span data-stu-id="65165-460">In this section you'll view them in a browser directly.</span></span>

1. <span data-ttu-id="65165-461">在 [hello**組態**hello] 索引標籤**Azure Web 應用程式**視窗中開啟**伺服器總管**，變更**失敗要求的追蹤**太**上**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="65165-461">In hello **Configuration** tab of hello **Azure Web App** window that you opened from **Server Explorer**, change **Failed Request Tracing** too**On**, and then click **Save**.</span></span>

    ![啟用失敗要求追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. <span data-ttu-id="65165-463">在 hello hello 顯示 hello web 應用程式的瀏覽器視窗的網址列中加入額外的字元 toohello URL，然後按一下 Enter toocause 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="65165-463">In hello address bar of hello browser window that shows hello web app, add an extra character toohello URL and click Enter toocause a 404 error.</span></span>

    <span data-ttu-id="65165-464">這會導致建立失敗的要求追蹤記錄檔 toobe 和 hello 下列步驟顯示如何 tooview 或下載 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-464">This causes a failed request tracing log toobe created, and hello following steps show how tooview or download hello log.</span></span>
3. <span data-ttu-id="65165-465">在 Visual Studio，在 hello**組態**] 索引標籤的 hello **Azure Web 應用程式**視窗中，按一下 [**管理入口網站中開啟**。</span><span class="sxs-lookup"><span data-stu-id="65165-465">In Visual Studio, in hello **Configuration** tab of hello **Azure Web App** window, click **Open in Management Portal**.</span></span>
4. <span data-ttu-id="65165-466">在 hello [Azure 入口網站](https://portal.azure.com)**設定**刀鋒視窗，web 應用程式中，按一下**部署認證**，然後輸入新的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="65165-466">In hello [Azure Portal](https://portal.azure.com) **Settings** blade for your web app, click **Deployment credentials**, and then enter a new user name and password.</span></span>

    ![新的 FTP 使用者名稱與密碼](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    <span data-ttu-id="65165-468">* * 當您登入，您會有與 hello web 應用程式名稱的前置詞 tooit toouse hello 完整使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="65165-468">**When you log in, you have toouse hello full user name with hello web app name prefixed tooit.</span></span> <span data-ttu-id="65165-469">例如，如果您輸入 「 myid"做為使用者名稱，而且 hello 站台 」 myexample 」，您身分登入 」 myexample\myid"。</span><span class="sxs-lookup"><span data-stu-id="65165-469">For example, if you enter "myid" as a user name and hello site is "myexample", you log in as "myexample\myid".</span></span>
5. <span data-ttu-id="65165-470">在新的瀏覽器視窗中，移會顯示在下方的 toohello URL **FTP 主機名稱**或**FTPS 主機名稱**在 hello **Web 應用程式**web 應用程式 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="65165-470">In a new browser window, go toohello URL that is shown under **FTP hostname** or **FTPS hostname** in hello **Web App** blade for your web app.</span></span>
6. <span data-ttu-id="65165-471">使用您稍早 （包括 hello web 應用程式的名稱前置詞 hello 使用者名稱） 所建立的 hello FTP 認證登入。</span><span class="sxs-lookup"><span data-stu-id="65165-471">Log in using hello FTP credentials that you created earlier (including hello web app name prefix for hello user name).</span></span>

    <span data-ttu-id="65165-472">hello 瀏覽器顯示 hello hello web 應用程式的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="65165-472">hello browser shows hello root folder of hello web app.</span></span>
7. <span data-ttu-id="65165-473">開啟 hello *LogFiles*資料夾。</span><span class="sxs-lookup"><span data-stu-id="65165-473">Open hello *LogFiles* folder.</span></span>

    ![開啟 LogFiles 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. <span data-ttu-id="65165-475">開啟 hello 資料夾名為 W3SVC 加上數字的值。</span><span class="sxs-lookup"><span data-stu-id="65165-475">Open hello folder that is named W3SVC plus a numeric value.</span></span>

    ![開啟 W3SVC 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    <span data-ttu-id="65165-477">hello 資料夾包含已記錄在您啟用失敗的要求追蹤之後的任何錯誤的 XML 檔案和瀏覽器可以使用 tooformat hello XML XSL 檔。</span><span class="sxs-lookup"><span data-stu-id="65165-477">hello folder contains XML files for any errors that have been logged after you enabled failed request tracing, and an XSL file that a browser can use tooformat hello XML.</span></span>

    ![W3SVC 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. <span data-ttu-id="65165-479">按一下您想要針對 toosee 追蹤資訊的 hello 失敗要求的 hello XML 檔。</span><span class="sxs-lookup"><span data-stu-id="65165-479">Click hello XML file for hello failed request that you want toosee tracing information for.</span></span>

    <span data-ttu-id="65165-480">hello 如下圖所示的範例錯誤 hello 追蹤資訊的一部分。</span><span class="sxs-lookup"><span data-stu-id="65165-480">hello following illustration shows part of hello tracing information for a sample error.</span></span>

    ![瀏覽器中的失敗要求追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <span data-ttu-id="65165-482"><a name="nextsteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="65165-482"><a name="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="65165-483">您已經看到如何 Visual Studio 可讓您輕鬆 tooview Azure web 應用程式所建立的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-483">You've seen how Visual Studio makes it easy tooview logs created by an Azure web app.</span></span> <span data-ttu-id="65165-484">hello 下列各節提供連結 toomore 資源相關主題：</span><span class="sxs-lookup"><span data-stu-id="65165-484">hello following sections provide links toomore resources on related topics:</span></span>

* <span data-ttu-id="65165-485">Azure Web 應用程式疑難排解</span><span class="sxs-lookup"><span data-stu-id="65165-485">Azure web app troubleshooting</span></span>
* <span data-ttu-id="65165-486">Visual Studio 偵錯</span><span class="sxs-lookup"><span data-stu-id="65165-486">Debugging in Visual Studio</span></span>
* <span data-ttu-id="65165-487">在 Azure 中遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="65165-487">Remote debugging in Azure</span></span>
* <span data-ttu-id="65165-488">在 ASP.NET 應用程式中追蹤</span><span class="sxs-lookup"><span data-stu-id="65165-488">Tracing in ASP.NET applications</span></span>
* <span data-ttu-id="65165-489">分析 Web 伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="65165-489">Analyzing web server logs</span></span>
* <span data-ttu-id="65165-490">分析失敗要求追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="65165-490">Analyzing failed request tracing logs</span></span>
* <span data-ttu-id="65165-491">偵錯雲端服務</span><span class="sxs-lookup"><span data-stu-id="65165-491">Debugging Cloud Services</span></span>

### <a name="azure-web-app-troubleshooting"></a><span data-ttu-id="65165-492">Azure Web 應用程式疑難排解</span><span class="sxs-lookup"><span data-stu-id="65165-492">Azure web app troubleshooting</span></span>
<span data-ttu-id="65165-493">如需疑難排解在 Azure App Service web 應用程式的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="65165-493">For more information about troubleshooting web apps in Azure App Service, see hello following resources:</span></span>

* [<span data-ttu-id="65165-494">如何 toomonitor web 應用程式</span><span class="sxs-lookup"><span data-stu-id="65165-494">How toomonitor web apps</span></span>](/manage/services/web-sites/how-to-monitor-websites/)
* <span data-ttu-id="65165-495">[使用 Visual Studio 2013 調查 Azure Web 應用程式中的記憶體流失](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65165-495">[Investigating Memory Leaks in Azure Web Apps with Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx).</span></span> <span data-ttu-id="65165-496">Microsoft ALM 部落格文章，討論 Visual Studio 中分析 Managed 記憶體問題的功能。</span><span class="sxs-lookup"><span data-stu-id="65165-496">Microsoft ALM blog post about Visual Studio features for analyzing managed memory issues.</span></span>
* <span data-ttu-id="65165-497">[您應該了解的 Azure Web 應用程式線上工具](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/)。</span><span class="sxs-lookup"><span data-stu-id="65165-497">[Azure web apps online tools you should know about](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/).</span></span> <span data-ttu-id="65165-498">取自 Amit Apple 的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="65165-498">Blog post by Amit Apple.</span></span>

<span data-ttu-id="65165-499">有關特定疑難排解問題，請啟動執行緒 hello 遵循論壇的其中一個：</span><span class="sxs-lookup"><span data-stu-id="65165-499">For help with a specific troubleshooting question, start a thread in one of hello following forums:</span></span>

* <span data-ttu-id="65165-500">[hello hello ASP.NET 網站上的 Azure 論壇](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET)。</span><span class="sxs-lookup"><span data-stu-id="65165-500">[hello Azure forum on hello ASP.NET site](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).</span></span>
* <span data-ttu-id="65165-501">[hello MSDN 上的 Azure 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/)。</span><span class="sxs-lookup"><span data-stu-id="65165-501">[hello Azure forum on MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).</span></span>
* <span data-ttu-id="65165-502">[StackOverflow.com](http://www.stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="65165-502">[StackOverflow.com](http://www.stackoverflow.com).</span></span>

### <a name="debugging-in-visual-studio"></a><span data-ttu-id="65165-503">Visual Studio 偵錯</span><span class="sxs-lookup"><span data-stu-id="65165-503">Debugging in Visual Studio</span></span>
<span data-ttu-id="65165-504">如需有關如何 toouse 偵錯 Visual Studio 中的模式的詳細資訊，請參閱 hello [Visual Studio 偵錯](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)MSDN 主題和[偵錯秘訣與 Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65165-504">For more information about how toouse debug mode in Visual Studio, see hello [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN topic and [Debugging Tips with Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).</span></span>

### <a name="remote-debugging-in-azure"></a><span data-ttu-id="65165-505">在 Azure 中遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="65165-505">Remote debugging in Azure</span></span>
<span data-ttu-id="65165-506">如需 Azure web 應用程式和 Webjob 的遠端偵錯的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="65165-506">For more information about remote debugging for Azure web apps and WebJobs, see hello following resources:</span></span>

* <span data-ttu-id="65165-507">[簡介 tooRemote 偵錯 Azure App Service Web 應用程式](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="65165-507">[Introduction tooRemote Debugging Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).</span></span>
* [<span data-ttu-id="65165-508">簡介 tooRemote 偵錯 Azure App Service Web 應用程式第 2 部-內遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="65165-508">Introduction tooRemote Debugging Azure App Service Web Apps part 2 - Inside Remote debugging</span></span>](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [<span data-ttu-id="65165-509">簡介 tooRemote Azure App Service Web 應用程式組件 3-多重執行個體環境和 GIT 上偵錯</span><span class="sxs-lookup"><span data-stu-id="65165-509">Introduction tooRemote Debugging on Azure App Service Web Apps part 3 - Multi-Instance environment and GIT</span></span>](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [<span data-ttu-id="65165-510">WebJobs 偵錯 (影片)</span><span class="sxs-lookup"><span data-stu-id="65165-510">WebJobs Debugging (video)</span></span>](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

<span data-ttu-id="65165-511">如果您的 web 應用程式使用 Azure Web 應用程式開發介面或行動服務後端，而且需要請參閱 toodebug [Visual Studio 中偵錯.NET 後端](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65165-511">If your web app uses an Azure Web API or Mobile Services back-end and you need toodebug that, see [Debugging .NET Backend in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).</span></span>

### <a name="tracing-in-aspnet-applications"></a><span data-ttu-id="65165-512">在 ASP.NET 應用程式中追蹤</span><span class="sxs-lookup"><span data-stu-id="65165-512">Tracing in ASP.NET applications</span></span>
<span data-ttu-id="65165-513">有追蹤 hello 網際網路上沒有完整且最新的介紹 tooASP.NET。</span><span class="sxs-lookup"><span data-stu-id="65165-513">There are no thorough and up-to-date introductions tooASP.NET tracing available on hello Internet.</span></span> <span data-ttu-id="65165-514">hello 最佳做法被開始使用舊的簡介資料寫入如需 Web Form 因為 MVC 不存在，而且補充的較新的部落格文章著重於特定的問題。</span><span class="sxs-lookup"><span data-stu-id="65165-514">hello best you can do is get started with old introductory materials written for Web Forms because MVC didn't exist yet, and supplement that with newer blog posts that focus on specific issues.</span></span> <span data-ttu-id="65165-515">某些有用位置 toostart 是 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="65165-515">Some good places toostart are hello following resources:</span></span>

* <span data-ttu-id="65165-516">[監視與遙測 (運用 Azure 建構真實的雲端應用程式) (英文)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry)。</span><span class="sxs-lookup"><span data-stu-id="65165-516">[Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).</span></span><br>
  <span data-ttu-id="65165-517">針對追蹤 Azure 雲端應用程式所建議的電子書章節。</span><span class="sxs-lookup"><span data-stu-id="65165-517">E-book chapter with recommendations for tracing in Azure cloud applications.</span></span>
* [<span data-ttu-id="65165-518">ASP.NET 追蹤</span><span class="sxs-lookup"><span data-stu-id="65165-518">ASP.NET Tracing</span></span>](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  <span data-ttu-id="65165-519">舊但仍是絕佳的資源的基本介紹 toohello 主旨。</span><span class="sxs-lookup"><span data-stu-id="65165-519">Old but still a good resource for a basic introduction toohello subject.</span></span>
* [<span data-ttu-id="65165-520">追蹤接聽程式</span><span class="sxs-lookup"><span data-stu-id="65165-520">Trace Listeners</span></span>](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  <span data-ttu-id="65165-521">追蹤接聽程式的相關資訊，但不會有提及 hello[組態區段](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65165-521">Information about trace listeners but doesn't mention hello [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).</span></span>
* [<span data-ttu-id="65165-522">逐步解說︰整合 ASP.NET 追蹤與 System.Diagnostics 追蹤</span><span class="sxs-lookup"><span data-stu-id="65165-522">Walkthrough: Integrating ASP.NET Tracing with System.Diagnostics Tracing</span></span>](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  <span data-ttu-id="65165-523">這太老舊，但包含一些額外資訊 hello 入門文件未涵蓋的範圍。</span><span class="sxs-lookup"><span data-stu-id="65165-523">This too is old, but includes some additional information that hello introductory article doesn't cover.</span></span>
* [<span data-ttu-id="65165-524">追蹤 ASP.NET MVC Razor 檢視</span><span class="sxs-lookup"><span data-stu-id="65165-524">Tracing in ASP.NET MVC Razor Views</span></span>](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  <span data-ttu-id="65165-525">Razor 檢視中的追蹤，除了 hello 文章也會說明如何 toocreate 錯誤篩選中的順序 toolog MVC 應用程式中的所有未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="65165-525">Besides tracing in Razor views, hello post also explains how toocreate an error filter in order toolog all unhandled exceptions in an MVC application.</span></span> <span data-ttu-id="65165-526">如需所有 toolog 的未都處理例外狀況，在 Web Form 應用程式，請參閱 hello Global.asax 範例[錯誤處理常式的完整範例](http://msdn.microsoft.com/library/bb397417.aspx)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="65165-526">For information about how toolog all unhandled exceptions in a Web Forms application, see hello Global.asax example in [Complete Example for Error Handlers](http://msdn.microsoft.com/library/bb397417.aspx) on MSDN.</span></span> <span data-ttu-id="65165-527">在 MVC 或 Web Form 中，如果您想 toolog 某些例外狀況，但讓 hello 預設架構處理生效，您可以攔截並重新擲回如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="65165-527">In either MVC or Web Forms, if you want toolog certain exceptions but let hello default framework handling take effect for them, you can catch and rethrow as in hello following example:</span></span>

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [<span data-ttu-id="65165-528">資料流從 hello Azure 命令列的診斷追蹤記錄 （加上初探 ！）</span><span class="sxs-lookup"><span data-stu-id="65165-528">Streaming Diagnostics Trace Logging from hello Azure Command Line (plus Glimpse!)</span></span>](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  <span data-ttu-id="65165-529">如何 toouse hello 命令列 toodo 此教學課程顯示如何在 Visual Studio 中的 toodo。</span><span class="sxs-lookup"><span data-stu-id="65165-529">How toouse hello command line toodo what this tutorial shows how toodo in Visual Studio.</span></span> <span data-ttu-id="65165-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) (英文) 工具可供您偵錯 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65165-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is a tool for debugging ASP.NET applications.</span></span>
* <span data-ttu-id="65165-531">[使用 Azure Web Apps 記錄和診斷功能 - 與 David Ebbo 合作](/documentation/videos/azure-web-site-logging-and-diagnostics/)以及[來自 Web Apps 的串流記錄 - 與 David Ebbo 合作](/documentation/videos/log-streaming-with-azure-web-sites/)</span><span class="sxs-lookup"><span data-stu-id="65165-531">[Using Web Apps Logging and Diagnostics - with David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) and [Streaming Logs from Web Apps - with David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)</span></span><br>
  <span data-ttu-id="65165-532">(英文) 影片，由 Scott Hanselman 與 David Ebbo 共同錄製。</span><span class="sxs-lookup"><span data-stu-id="65165-532">Videos by Scott Hanselman and David Ebbo.</span></span>

<span data-ttu-id="65165-533">錯誤記錄的替代 toowriting 您自己的追蹤程式碼是 toouse 開放原始碼記錄架構，例如[ELMAH](http://nuget.org/packages/elmah/)。</span><span class="sxs-lookup"><span data-stu-id="65165-533">For error logging, an alternative toowriting your own tracing code is toouse an open-source logging framework such as [ELMAH](http://nuget.org/packages/elmah/).</span></span> <span data-ttu-id="65165-534">如需詳細資訊，請參閱 [Scott Hanselman 關於 ELMAH 的部落格文章](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)(英文)。</span><span class="sxs-lookup"><span data-stu-id="65165-534">For more information, see [Scott Hanselman's blog posts about ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).</span></span>

<span data-ttu-id="65165-535">另外請注意您不需要 toouse ASP.NET，或如果您想串流處理 tooget System.Diagnostics 追蹤會記錄來自 Azure。</span><span class="sxs-lookup"><span data-stu-id="65165-535">Also, note that you don't have toouse ASP.NET or System.Diagnostics tracing if you want tooget streaming logs from Azure.</span></span> <span data-ttu-id="65165-536">hello Azure web 應用程式串流記錄服務會串流任何*.txt*， *.html*，或*.log*在 hello 中找到的檔案*LogFiles*資料夾。</span><span class="sxs-lookup"><span data-stu-id="65165-536">hello Azure web app streaming log service will stream any *.txt*, *.html*, or *.log* file that it finds in hello *LogFiles* folder.</span></span> <span data-ttu-id="65165-537">因此，您可以建立自己的記錄系統寫入 toohello 檔案系統的 hello web 應用程式，而且您的檔案會自動串流處理並下載。</span><span class="sxs-lookup"><span data-stu-id="65165-537">Therefore, you could create your own logging system that writes toohello file system of hello web app, and your file will be automatically streamed and downloaded.</span></span> <span data-ttu-id="65165-538">您只需要 toodo 會寫入應用程式程式碼檔案建立在 hello *d:\home\logfiles*資料夾。</span><span class="sxs-lookup"><span data-stu-id="65165-538">All you have toodo is write application code that creates files in hello *d:\home\logfiles* folder.</span></span>

### <a name="analyzing-web-server-logs"></a><span data-ttu-id="65165-539">分析 Web 伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="65165-539">Analyzing web server logs</span></span>
<span data-ttu-id="65165-540">如需分析 web 伺服器記錄檔的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="65165-540">For more information about analyzing web server logs, see hello following resources:</span></span>

* [<span data-ttu-id="65165-541">LogParser</span><span class="sxs-lookup"><span data-stu-id="65165-541">LogParser</span></span>](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  <span data-ttu-id="65165-542">用於檢視 Web 伺服器記錄 (*.log* 檔案) 中資料的工具。</span><span class="sxs-lookup"><span data-stu-id="65165-542">A tool for viewing data in web server logs (*.log* files).</span></span>
* [<span data-ttu-id="65165-543">疑難排解 IIS 效能問題或使用 LogParser 的應用程式錯誤</span><span class="sxs-lookup"><span data-stu-id="65165-543">Troubleshooting IIS Performance Issues or Application Errors using LogParser </span></span>](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  <span data-ttu-id="65165-544">您可以使用 tooanalyze web 伺服器的簡介 toohello 記錄檔剖析器工具記錄。</span><span class="sxs-lookup"><span data-stu-id="65165-544">An introduction toohello Log Parser tool that you can use tooanalyze web server logs.</span></span>
* [<span data-ttu-id="65165-545">Robert McMurray 關於使用 LogParser 的部落格文章</span><span class="sxs-lookup"><span data-stu-id="65165-545">Blog posts by Robert McMurray on using LogParser</span></span>](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [<span data-ttu-id="65165-546">hello IIS 7.0、 IIS 7.5 和 IIS 8.0 中的 HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="65165-546">hello HTTP status code in IIS 7.0, IIS 7.5, and IIS 8.0</span></span>](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a><span data-ttu-id="65165-547">分析失敗要求追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="65165-547">Analyzing failed request tracing logs</span></span>
<span data-ttu-id="65165-548">hello Microsoft TechNet 網站包含[使用失敗要求的追蹤](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing)區段，這可能有助於了解如何 toouse 這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="65165-548">hello Microsoft TechNet website includes a [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section which may be helpful for understanding how toouse these logs.</span></span> <span data-ttu-id="65165-549">不過，本文主要著重在 IIS 內設定失敗要求追蹤功能，這是您無法在 Azure Web Apps 中執行的功能。</span><span class="sxs-lookup"><span data-stu-id="65165-549">However, this documentation focuses mainly on configuring failed request tracing in IIS, which you can't do in Azure Web Apps.</span></span>

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
