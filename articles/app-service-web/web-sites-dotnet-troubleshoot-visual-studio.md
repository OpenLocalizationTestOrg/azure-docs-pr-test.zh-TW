---
title: "使用 Visual Studio 疑難排解 Azure App Service 中的 Web 應用程式"
description: "了解如何使用 Visual Studio 2013 內建的遠端偵錯、追蹤和記錄工具，來疑難排解 Azure Web 應用程式。"
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
ms.openlocfilehash: abfd9a4c1b346377d7f1fc30455a1487b113537d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a><span data-ttu-id="45ace-103">使用 Visual Studio 疑難排解 Azure App Service 中的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="45ace-103">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="45ace-104">Overview</span><span class="sxs-lookup"><span data-stu-id="45ace-104">Overview</span></span>
<span data-ttu-id="45ace-105">本教學課程示範如何使用 Visual Studio 工具，協助偵錯 [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 中的 Web 應用程式，方法是以[偵錯模式](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)從遠端執行，或者檢視應用程式記錄與 Web 伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-105">This tutorial shows how to use Visual Studio tools that help debug a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), by running in [debug mode](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) remotely or by viewing application logs and web server logs.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="45ace-106">您將了解：</span><span class="sxs-lookup"><span data-stu-id="45ace-106">You'll learn:</span></span>

* <span data-ttu-id="45ace-107">Visual Studio 中提供的 Azure Web 應用程式管理功能有哪些。</span><span class="sxs-lookup"><span data-stu-id="45ace-107">Which Azure web app management functions are available in Visual Studio.</span></span>
* <span data-ttu-id="45ace-108">如何使用 Visual Studio 遠端檢視，對遠端 Web 應用程式進行快速變更。</span><span class="sxs-lookup"><span data-stu-id="45ace-108">How to use Visual Studio remote view to make quick changes in a remote web app.</span></span>
* <span data-ttu-id="45ace-109">在 Azure 中執行專案時，如何同時針對 Web 應用程式和 WebJob 從遠端執行偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="45ace-109">How to run debug mode remotely while a project is running in Azure, both for a web app and for a WebJob.</span></span>
* <span data-ttu-id="45ace-110">如何建立應用程式追蹤記錄，並在應用程式建立記錄時加以檢視。</span><span class="sxs-lookup"><span data-stu-id="45ace-110">How to create application trace logs and view them while the application is creating them.</span></span>
* <span data-ttu-id="45ace-111">如何檢視 Web 伺服器記錄，包括詳細的錯誤訊息與失敗的要求追蹤。</span><span class="sxs-lookup"><span data-stu-id="45ace-111">How to view web server logs, including detailed error messages and failed request tracing.</span></span>
* <span data-ttu-id="45ace-112">如何將診斷記錄傳送至 Azure 儲存體帳戶並在該處檢視。</span><span class="sxs-lookup"><span data-stu-id="45ace-112">How to send diagnostic logs to an Azure Storage account and view them there.</span></span>

<span data-ttu-id="45ace-113">如果您有 Visual Studio Ultimate，您也可以使用 [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) 進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="45ace-113">If you have Visual Studio Ultimate, you can also use [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) for debugging.</span></span> <span data-ttu-id="45ace-114">本教學課程未涵蓋 IntelliTrace。</span><span class="sxs-lookup"><span data-stu-id="45ace-114">IntelliTrace is not covered in this tutorial.</span></span>

## <span data-ttu-id="45ace-115"><a name="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="45ace-115"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="45ace-116">本教學課程可運用於開發環境、Web 專案與您在[開始使用 Azure 和 ASP.NET][GetStarted] 中所設定的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45ace-116">This tutorial works with the development environment, web project, and Azure web app that you set up in [Get started with Azure and ASP.NET][GetStarted].</span></span> <span data-ttu-id="45ace-117">針對 WebJobs 區段，您將會用到您在[開始使用 Azure WebJobs SDK][GetStartedWJ] 中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45ace-117">For the WebJobs sections, you'll need the application that you create in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span></span>

<span data-ttu-id="45ace-118">本教學課程中所提供的程式碼範例適用於 C# MVC Web 應用程式，但是疑難排解程序則是與 Visual Basic 和 Web Form 應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="45ace-118">The code samples shown in this tutorial are for a C# MVC web application, but the troubleshooting procedures are the same for Visual Basic and Web Forms applications.</span></span>

<span data-ttu-id="45ace-119">此教學課程假設您使用 Visual Studio 2015 或 2013。</span><span class="sxs-lookup"><span data-stu-id="45ace-119">The tutorial assumes you're using Visual Studio 2015 or 2013.</span></span> <span data-ttu-id="45ace-120">如果您使用 Visual Studio 2013，WebJobs 功能需要 [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="45ace-120">If you're using Visual Studio 2013, the WebJobs features require [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) or later.</span></span>

<span data-ttu-id="45ace-121">串流記錄功能僅適用於鎖定 .NET Framework 4 或更新版本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45ace-121">The streaming logs feature only works for applications that target .NET Framework 4 or later.</span></span>

## <span data-ttu-id="45ace-122"><a name="sitemanagement"></a>Web 應用程式組態與管理</span><span class="sxs-lookup"><span data-stu-id="45ace-122"><a name="sitemanagement"></a>Web app configuration and management</span></span>
<span data-ttu-id="45ace-123">Visual Studio 可讓您存取 [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)中可用的 Web 應用程式管理功能與組態設定的子集。</span><span class="sxs-lookup"><span data-stu-id="45ace-123">Visual Studio provides access to a subset of the web app management functions and configuration settings available in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="45ace-124">本節將說明使用 **伺服器總管**可用的項目。</span><span class="sxs-lookup"><span data-stu-id="45ace-124">In this section you'll see what's available by using **Server Explorer**.</span></span> <span data-ttu-id="45ace-125">若要查看最新的 Azure 整合功能，也請試試 **雲端總管** 。</span><span class="sxs-lookup"><span data-stu-id="45ace-125">To see the latest Azure integration features, try out **Cloud Explorer** also.</span></span> <span data-ttu-id="45ace-126">您可以同時從 [檢視]  功能表開啟這兩個視窗。</span><span class="sxs-lookup"><span data-stu-id="45ace-126">You can open both windows from the **View** menu.</span></span>

1. <span data-ttu-id="45ace-127">如果您尚未在 Visual Studio 中登入 Azure，按一下 [伺服器總管] 中的 [連線到 Azure] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45ace-127">If you aren't already signed in to Azure in Visual Studio, click the **Connect to Azure** button in **Server Explorer**.</span></span>

    <span data-ttu-id="45ace-128">替代方式為安裝可讓您存取帳戶的管理憑證。</span><span class="sxs-lookup"><span data-stu-id="45ace-128">An alternative is to install a management certificate that enables access to your account.</span></span> <span data-ttu-id="45ace-129">如果您選擇安裝憑證，請以滑鼠右鍵按一下 [伺服器總管] 中的 [Azure] 節點，然後按一下內容功能表中的 [管理與篩選訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="45ace-129">If you choose to install a certificate, right-click the **Azure** node in **Server Explorer**, and then click **Manage and Filter Subscriptions** in the context menu.</span></span> <span data-ttu-id="45ace-130">在 [管理 Azure 訂閱] 對話方塊中，按一下 [憑證] 索引標籤，再按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="45ace-130">In the **Manage Azure Subscriptions** dialog box, click the **Certificates** tab, and then click **Import**.</span></span> <span data-ttu-id="45ace-131">請依照指示下載，然後匯入您 Azure 帳戶的訂用帳戶檔案 (亦稱為 *.publishsettings* 檔案)。</span><span class="sxs-lookup"><span data-stu-id="45ace-131">Follow the directions to download and then import a subscription file (also called a *.publishsettings* file) for your Azure account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="45ace-132">如果您下載了訂用帳戶檔案，請將其儲存到原始程式碼目錄以外的資料夾 (例如在 Downloads 資料夾)，然後在匯入完成後刪除該檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-132">If you download a subscription file, save it to a folder outside your source code directories (for example, in the Downloads folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="45ace-133">惡意使用者一旦能夠存取此訂閱檔案，就能夠編輯、建立和刪除您的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="45ace-133">A malicious user who gains access to the subscription file can edit, create, and delete your Azure services.</span></span>
   >
   >

    <span data-ttu-id="45ace-134">如需從 Visual Studio 連線至 Azure 資源的詳細資訊，請參閱 [管理帳戶、訂閱和系統管理角色](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert)。</span><span class="sxs-lookup"><span data-stu-id="45ace-134">For more information about connecting to Azure resources from Visual Studio, see [Manage Accounts, Subscriptions, and Administrative Roles](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).</span></span>
2. <span data-ttu-id="45ace-135">在 [伺服器總管] 中，展開 [Azure]，然後展開 [App Service]。</span><span class="sxs-lookup"><span data-stu-id="45ace-135">In **Server Explorer**, expand **Azure** and expand **App Service**.</span></span>
3. <span data-ttu-id="45ace-136">展開資源群組 (其包含您在[開始使用 Azure 和 ASP.NET][GetStarted] 中建立的 Web 應用程式)，使用滑鼠右鍵按一下 Web 應用程式節點，然後按一下 [檢視設定]。</span><span class="sxs-lookup"><span data-stu-id="45ace-136">Expand the resource group that includes the web app that you created in [Getting started with Azure and ASP.NET][GetStarted], and then right-click the web app node and click **View Settings**.</span></span>

    ![在伺服器總管中檢視設定](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    <span data-ttu-id="45ace-138">[Azure Web App]  索引標籤隨即顯示，而您會看到 Visual Studio 中所提供的 Web 應用程式管理與組態工作。</span><span class="sxs-lookup"><span data-stu-id="45ace-138">The **Azure Web App** tab appears, and you can see there the web app management and configuration tasks that are available in Visual Studio.</span></span>

    ![Azure Web 應用程式視窗](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    <span data-ttu-id="45ace-140">在本教學課程中，您將使用記錄與追蹤下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="45ace-140">In this tutorial you'll be using the logging and tracing drop-downs.</span></span> <span data-ttu-id="45ace-141">您也會使用遠端偵錯功能，但是將以不同的方式來加以啟用。</span><span class="sxs-lookup"><span data-stu-id="45ace-141">You'll also use remote debugging but you'll use a different method to enable it.</span></span>

    <span data-ttu-id="45ace-142">如需此視窗中 [應用程式設定] 與 [連接字串] 方塊的詳細資訊，請參閱 [Azure Web Apps：應用程式設定與連接字串如何運作](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45ace-142">For information about the App Settings and Connection Strings boxes in this window, see [Azure Web Apps: How Application Strings and Connection Strings Work](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

    <span data-ttu-id="45ace-143">若您想要執行無法在此視窗中完成的 Web 應用程式管理工作，請按一下 [在管理入口網站中開啟]  ，以開啟 Azure 入口網站的瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="45ace-143">If you want to perform a web app management task that can't be done in this window, click **Open in Management Portal** to open a browser window to the Azure portal.</span></span>

## <span data-ttu-id="45ace-144"><a name="remoteview"></a>在伺服器總管中存取 Web 應用程式檔案</span><span class="sxs-lookup"><span data-stu-id="45ace-144"><a name="remoteview"></a>Access web app files in Server Explorer</span></span>
<span data-ttu-id="45ace-145">部署 Web 專案時，通常會將 Web.config 檔案中的 `customErrors` 旗標設為 `On` 或 `RemoteOnly`，這表示出現問題時，您將不會收到有用的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="45ace-145">You typically deploy a web project with the `customErrors` flag in the Web.config file set to `On` or `RemoteOnly`, which means you don't get a helpful error message when something goes wrong.</span></span> <span data-ttu-id="45ace-146">對許多錯誤而言，您只會看到如下列之一的頁面。</span><span class="sxs-lookup"><span data-stu-id="45ace-146">For many errors all you get is a page like one of the following ones.</span></span>

<span data-ttu-id="45ace-147">**'/' 應用程式中有伺服器錯誤：**</span><span class="sxs-lookup"><span data-stu-id="45ace-147">**Server Error in '/' Application:**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

<span data-ttu-id="45ace-149">**發生錯誤：**</span><span class="sxs-lookup"><span data-stu-id="45ace-149">**An error occurred:**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

<span data-ttu-id="45ace-151">**網站無法顯示頁面**</span><span class="sxs-lookup"><span data-stu-id="45ace-151">**The website cannot display the page**</span></span>

![Unhelpful error page](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

<span data-ttu-id="45ace-153">要找到錯誤原因最簡單的方式，往往就是啟用詳細的錯誤訊息，而以上第一個螢幕擷取畫面說明的是其做法。</span><span class="sxs-lookup"><span data-stu-id="45ace-153">Frequently the easiest way to find the cause of the error is to enable detailed error messages, which the first of the preceding screenshots explains how to do.</span></span> <span data-ttu-id="45ace-154">該做法需要在部署的 Web.config 檔案中進行變更。</span><span class="sxs-lookup"><span data-stu-id="45ace-154">That requires a change in the deployed Web.config file.</span></span> <span data-ttu-id="45ace-155">您可以編輯專案中的 *Web.config* 檔案並重新部署專案，或建立 [Web.config 轉換](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations)並部署偵錯組建，但還有更快的方法：在 [方案總管] 中使用 [遠端檢視] 功能，直接檢視及編輯遠端 Web 應用程式上的檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-155">You could edit the *Web.config* file in the project and redeploy the project, or create a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) and deploy a debug build, but there's a quicker way: in **Solution Explorer** you can directly view and edit files in the remote web app by using the *remote view* feature.</span></span>

1. <span data-ttu-id="45ace-156">在 [伺服器總管] 中，依序展開 [Azure]、[App Service] 和 Web 應用程式所在的資源群組，然後展開 Web 應用程式的節點。</span><span class="sxs-lookup"><span data-stu-id="45ace-156">In **Server Explorer**, expand **Azure**, expand **App Service**, expand the resource group that your web app is located in, and then expand the node for your web app.</span></span>

    <span data-ttu-id="45ace-157">您會看到可供您存取 Web 應用程式內容檔案與記錄檔的節點。</span><span class="sxs-lookup"><span data-stu-id="45ace-157">You see nodes that give you access to the web app's content files and log files.</span></span>
2. <span data-ttu-id="45ace-158">展開 [檔案]  節點，然後按兩下 *Web.config* 檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-158">Expand the **Files** node, and double-click the *Web.config* file.</span></span>

    ![開啟 Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    <span data-ttu-id="45ace-160">Visual Studio 會從遠端 Web 應用程式開啟 Web.config 檔案，然後在標題列中的檔案名稱旁邊顯示 [遠端]。</span><span class="sxs-lookup"><span data-stu-id="45ace-160">Visual Studio opens the Web.config file from the remote web app and shows [Remote] next to the file name in the title bar.</span></span>
3. <span data-ttu-id="45ace-161">將下列字行新增至 `system.web` 元素：</span><span class="sxs-lookup"><span data-stu-id="45ace-161">Add the following line to the `system.web` element:</span></span>

    `<customErrors mode="Off"></customErrors>`

    ![編輯 Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. <span data-ttu-id="45ace-163">重新整理顯示沒有幫助的錯誤訊息的瀏覽器，現在您就會看到詳細的錯誤訊息，例如以下範例：</span><span class="sxs-lookup"><span data-stu-id="45ace-163">Refresh the browser that is showing the unhelpful error message, and now you get a detailed error message, such as the following example:</span></span>

    ![詳細的錯誤訊息](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    <span data-ttu-id="45ace-165">(顯示的錯誤是透過將紅色字行新增至 *Views\Home\Index.cshtml* 中來加以建立。)</span><span class="sxs-lookup"><span data-stu-id="45ace-165">(The error shown was created by adding the line shown in red to *Views\Home\Index.cshtml*.)</span></span>

<span data-ttu-id="45ace-166">能夠讀取與編輯您的 Azure Web 應用程式上的檔案，使得疑難排解作業更為輕鬆，編輯 Web.config 檔案僅僅是其中一個範例案例。</span><span class="sxs-lookup"><span data-stu-id="45ace-166">Editing the Web.config file is only one example of scenarios in which the ability to read and edit files on your Azure web app make troubleshooting easier.</span></span>

## <span data-ttu-id="45ace-167"><a name="remotedebug"></a>遠端偵錯 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="45ace-167"><a name="remotedebug"></a>Remote debugging web apps</span></span>
<span data-ttu-id="45ace-168">如果詳細的錯誤訊息無法提供足夠的資訊，而且您無法在本機重現錯誤，另一個疑難排解的方式則是在遠端於偵錯模式中執行。</span><span class="sxs-lookup"><span data-stu-id="45ace-168">If the detailed error message doesn't provide enough information, and you can't re-create the error locally, another way to troubleshoot is to run in debug mode remotely.</span></span> <span data-ttu-id="45ace-169">您可以設定中斷點、直接操作記憶體、逐步執行程式碼，甚至變更程式碼路徑。</span><span class="sxs-lookup"><span data-stu-id="45ace-169">You can set breakpoints, manipulate memory directly, step through code, and even change the code path.</span></span>

<span data-ttu-id="45ace-170">遠端偵錯無法在 Visual Studio 的 Express 版本中運作。</span><span class="sxs-lookup"><span data-stu-id="45ace-170">Remote debugging does not work in Express editions of Visual Studio.</span></span>

<span data-ttu-id="45ace-171">本節說明如何使用您在[開始使用 Azure 和 ASP.NET][GetStarted] 中建立的專案進行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="45ace-171">This section shows how to debug remotely using the project you create in [Getting started with Azure and ASP.NET][GetStarted].</span></span>

1. <span data-ttu-id="45ace-172">開啟您在[開始使用 Azure 和 ASP.NET][GetStarted] 中建立的 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="45ace-172">Open the web project that you created in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
2. <span data-ttu-id="45ace-173">開啟 *Controllers\HomeController.cs*。</span><span class="sxs-lookup"><span data-stu-id="45ace-173">Open *Controllers\HomeController.cs*.</span></span>
3. <span data-ttu-id="45ace-174">刪除 `About()` 方法，然後插入以下程式碼加以取代。</span><span class="sxs-lookup"><span data-stu-id="45ace-174">Delete the `About()` method and insert the following code in its place.</span></span>

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "The current time is " + currentTime;
            return View();
        }
4. <span data-ttu-id="45ace-175">[在 `ViewBag.Message`這行設定中斷點](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45ace-175">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on the `ViewBag.Message` line.</span></span>
5. <span data-ttu-id="45ace-176">在 [方案總管] 中，於專案上按一下滑鼠右鍵，再按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="45ace-176">In **Solution Explorer**, right-click the project, and click **Publish**.</span></span>
6. <span data-ttu-id="45ace-177">在 [設定檔] 下拉式清單中，選取您在[開始使用 Azure 和 ASP.NET][GetStarted] 中使用的相同設定檔。</span><span class="sxs-lookup"><span data-stu-id="45ace-177">In the **Profile** drop-down list, select the same profile that you used in [Getting started with Azure and ASP.NET][GetStarted].</span></span>
7. <span data-ttu-id="45ace-178">按一下 [設定] 索引標籤，然後將 [組態] 變更為 [偵錯]，然後按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="45ace-178">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span></span>

    ![於偵錯模式中發行](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. <span data-ttu-id="45ace-180">當部署完成且您的瀏覽器開啟至 Web 應用程式的 Azure URL 之後，請關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="45ace-180">After deployment finishes and your browser opens to the Azure URL of your web app, close the browser.</span></span>
9. <span data-ttu-id="45ace-181">在 [伺服器總管] 中，以滑鼠右鍵按一下您的 Web 應用程式，接著按一下 [連結偵錯工具]。</span><span class="sxs-lookup"><span data-stu-id="45ace-181">In **Server Explorer**, right-click your web app, and then click **Attach Debugger**.</span></span>

    ![連結偵錯工具](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    <span data-ttu-id="45ace-183">瀏覽器會自動開啟至您在 Azure 中執行的首頁。</span><span class="sxs-lookup"><span data-stu-id="45ace-183">The browser automatically opens to your home page running in Azure.</span></span> <span data-ttu-id="45ace-184">您可能需要等候 20 秒左右的時間，讓 Azure 設定要偵錯的伺服器。</span><span class="sxs-lookup"><span data-stu-id="45ace-184">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span></span> <span data-ttu-id="45ace-185">通常只有當您第一次在 Web 應用程式上執行偵錯模式時，才會出現這個延遲現象。</span><span class="sxs-lookup"><span data-stu-id="45ace-185">This delay only happens the first time you run in debug mode on a web app.</span></span> <span data-ttu-id="45ace-186">後續 48 小時內再次啟動的偵錯程序將不會再出現任何延遲。</span><span class="sxs-lookup"><span data-stu-id="45ace-186">Subsequent times within the next 48 hours when you start debugging again there won't be a delay.</span></span>

    <span data-ttu-id="45ace-187">**注意︰**如果您有任何啟動偵錯工具的問題，請試著使用**雲端總管**執行，而不是**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="45ace-187">**Note:** If you have any trouble starting the debugger, try to do it by using **Cloud Explorer** instead of **Server Explorer**.</span></span>
10. <span data-ttu-id="45ace-188">按一下功能表中的 [關於]  。</span><span class="sxs-lookup"><span data-stu-id="45ace-188">Click **About** in the menu.</span></span>

     <span data-ttu-id="45ace-189">Visual Studio 會在中斷點處停止，而程式碼是在 Azure 中執行，而不是在您的本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="45ace-189">Visual Studio stops on the breakpoint, and the code is running in Azure, not on your local computer.</span></span>
11. <span data-ttu-id="45ace-190">將滑鼠移至 `currentTime` 變數上，以查看時間值。</span><span class="sxs-lookup"><span data-stu-id="45ace-190">Hover over the `currentTime` variable to see the time value.</span></span>

     ![檢視 Azure 偵錯模式中執行的變數](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     <span data-ttu-id="45ace-192">您在 Azure 伺服器時間上看到的時間，可能與您的本機電腦所在的時區不同。</span><span class="sxs-lookup"><span data-stu-id="45ace-192">The time you see is the Azure server time, which may be in a different time zone than your local computer.</span></span>
12. <span data-ttu-id="45ace-193">為 `currentTime` 變數輸入新的值，例如「現在於 Azure 中執行」。</span><span class="sxs-lookup"><span data-stu-id="45ace-193">Enter a new value for the `currentTime` variable, such as "Now running in Azure".</span></span>
13. <span data-ttu-id="45ace-194">按 F5 繼續執行。</span><span class="sxs-lookup"><span data-stu-id="45ace-194">Press F5 to continue running.</span></span>

     <span data-ttu-id="45ace-195">Azure 中執行的 [關於] 頁面會顯示您輸入到 currentTime 變數中的新值。</span><span class="sxs-lookup"><span data-stu-id="45ace-195">The About page running in Azure displays the new value that you entered into the currentTime variable.</span></span>

     ![含有新值的關於頁面](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <span data-ttu-id="45ace-197"><a name="remotedebugwj"></a> 遠端偵錯 WebJobs</span><span class="sxs-lookup"><span data-stu-id="45ace-197"><a name="remotedebugwj"></a> Remote debugging WebJobs</span></span>
<span data-ttu-id="45ace-198">本節說明如何使用您在 [開始使用 Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md)中建立的專案和 Web 應用程式進行遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="45ace-198">This section shows how to debug remotely using the project and web app you create in [Get Started with the Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

<span data-ttu-id="45ace-199">本節顯示的功能僅適用於 Visual Studio 2013 含 Update 4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="45ace-199">The features shown in this section are available only in Visual Studio 2013 with Update 4 or later.</span></span>

<span data-ttu-id="45ace-200">遠端偵錯僅適用於連續的 WebJobs。</span><span class="sxs-lookup"><span data-stu-id="45ace-200">Remote debugging only works with continuous WebJobs.</span></span> <span data-ttu-id="45ace-201">排程與隨選 WebJobs 不支援偵錯。</span><span class="sxs-lookup"><span data-stu-id="45ace-201">Scheduled and on-demand WebJobs don't support debugging.</span></span>

1. <span data-ttu-id="45ace-202">開啟您在[開始使用 Azure WebJobs SDK][GetStartedWJ] 中建立的 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="45ace-202">Open the web project that you created in [Get Started with the Azure WebJobs SDK][GetStartedWJ].</span></span>
2. <span data-ttu-id="45ace-203">在 ContosoAdsWebJob 專案中，開啟 *Functions.cs*。</span><span class="sxs-lookup"><span data-stu-id="45ace-203">In the ContosoAdsWebJob project, open *Functions.cs*.</span></span>
3. <span data-ttu-id="45ace-204">在 `GnerateThumbnail` 方法的第一個陳述式上[設定中斷點](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45ace-204">[Set a breakpoint](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) on the first statement in the `GnerateThumbnail` method.</span></span>

    ![設定中斷點](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. <span data-ttu-id="45ace-206">在 [方案總管] 中，以滑鼠右鍵按一下 Web 專案 (不是 WebJob 專案)，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="45ace-206">In **Solution Explorer**, right-click the web project (not the WebJob project), and click **Publish**.</span></span>
5. <span data-ttu-id="45ace-207">在 [設定檔]  下拉式清單中，選取您在 [開始使用 Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md)中所使用的相同設定檔。</span><span class="sxs-lookup"><span data-stu-id="45ace-207">In the **Profile** drop-down list, select the same profile that you used in [Get Started with the Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>
6. <span data-ttu-id="45ace-208">按一下 [設定] 索引標籤，然後將 [組態] 變更為 [偵錯]，然後按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="45ace-208">Click the **Settings** tab, and change **Configuration** to **Debug**, and then click **Publish**.</span></span>

    <span data-ttu-id="45ace-209">Visual Studio 會部署 Web 和 WebJob 專案，且在瀏覽器中開啟您 Web 應用程式的 Azure URL。</span><span class="sxs-lookup"><span data-stu-id="45ace-209">Visual Studio deploys the web and WebJob projects, and your browser opens to the Azure URL of your web app.</span></span>
7. <span data-ttu-id="45ace-210">在 [伺服器總管] 中，依序展開 [Azure] > [App Service] > 您的資源群組Web > 您的 Web 應用程式 > [WebJob] > [連續]，然後使用滑鼠右鍵按一下 [ContosoAdsWebJob]。</span><span class="sxs-lookup"><span data-stu-id="45ace-210">In **Server Explorer** expand **Azure > App Service > your resource group > your web app > WebJobs > Continuous**, and then right-click **ContosoAdsWebJob**.</span></span>
8. <span data-ttu-id="45ace-211">按一下 [連結偵錯工具] 。</span><span class="sxs-lookup"><span data-stu-id="45ace-211">Click **Attach Debugger**.</span></span>

    ![連結偵錯工具](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    <span data-ttu-id="45ace-213">瀏覽器會自動開啟至您在 Azure 中執行的首頁。</span><span class="sxs-lookup"><span data-stu-id="45ace-213">The browser automatically opens to your home page running in Azure.</span></span> <span data-ttu-id="45ace-214">您可能需要等候 20 秒左右的時間，讓 Azure 設定要偵錯的伺服器。</span><span class="sxs-lookup"><span data-stu-id="45ace-214">You might have to wait 20 seconds or so while Azure sets up the server for debugging.</span></span> <span data-ttu-id="45ace-215">通常只有當您第一次在 Web 應用程式上執行偵錯模式時，才會出現這個延遲現象。</span><span class="sxs-lookup"><span data-stu-id="45ace-215">This delay only happens the first time you run in debug mode on a web app.</span></span> <span data-ttu-id="45ace-216">如果您在 48 小時內執行，則下一次連結偵錯工具時將不會出現延遲。</span><span class="sxs-lookup"><span data-stu-id="45ace-216">The next time you attach the debugger there won't be a delay, if you do it within 48 hours.</span></span>
9. <span data-ttu-id="45ace-217">在開啟至 Contoso 廣告首頁的 Web 瀏覽器中，建立新的廣告。</span><span class="sxs-lookup"><span data-stu-id="45ace-217">In the web browser that is opened to the Contoso Ads home page, create a new ad.</span></span>

    <span data-ttu-id="45ace-218">建立廣告會建立將由 WebJob 挑選並處理的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="45ace-218">Creating an ad causes a queue message to be created, which will be picked up by the WebJob and processed.</span></span> <span data-ttu-id="45ace-219">當 WebJobs SDK 呼叫函數來處理佇列訊息時，程式碼便會叫用中斷點。</span><span class="sxs-lookup"><span data-stu-id="45ace-219">When the WebJobs SDK calls the function to process the queue message, the code will hit your breakpoint.</span></span>
10. <span data-ttu-id="45ace-220">當偵錯工具在中斷點出現中斷時，您可以檢查並變更在雲端執行程式時的變數值。</span><span class="sxs-lookup"><span data-stu-id="45ace-220">When the debugger breaks at your breakpoint, you can examine and change variable values while the program is running the cloud.</span></span> <span data-ttu-id="45ace-221">在下圖中，偵錯工具顯示已傳遞到 GenerateThumbnail 方法的 blobInfo 物件內容。</span><span class="sxs-lookup"><span data-stu-id="45ace-221">In the following illustration the debugger shows the contents of the blobInfo object that was passed to the GenerateThumbnail method.</span></span>

     ![偵錯工具中的 blobInfo 物件](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. <span data-ttu-id="45ace-223">按 F5 繼續執行。</span><span class="sxs-lookup"><span data-stu-id="45ace-223">Press F5 to continue running.</span></span>

     <span data-ttu-id="45ace-224">GenerateThumbnail 方法完成建立縮圖。</span><span class="sxs-lookup"><span data-stu-id="45ace-224">The GenerateThumbnail method finishes creating the thumbnail.</span></span>
12. <span data-ttu-id="45ace-225">在瀏覽器中重新整理索引頁面，您便會看見縮圖。</span><span class="sxs-lookup"><span data-stu-id="45ace-225">In the browser, refresh the Index page and you see the thumbnail.</span></span>
13. <span data-ttu-id="45ace-226">在 Visual Studio 中，按 SHIFT+F5 停止偵錯。</span><span class="sxs-lookup"><span data-stu-id="45ace-226">In Visual Studio, press SHIFT+F5 to stop debugging.</span></span>
14. <span data-ttu-id="45ace-227">在 [伺服器總管] 中，以滑鼠右鍵在 [伺服器總管] 中，以滑鼠右鍵按一下 ContosoAdsWebJob 節點，然後按一下 [檢視儀表板]。</span><span class="sxs-lookup"><span data-stu-id="45ace-227">In **Server Explorer**, right-click the ContosoAdsWebJob node and click **View Dashboard**.</span></span>
15. <span data-ttu-id="45ace-228">使用您的 Azure 認證登入，然後按一下 WebJob 名稱，可前往 WebJob 的頁面。</span><span class="sxs-lookup"><span data-stu-id="45ace-228">Sign in with your Azure credentials, and then click the WebJob name to go to the page for your WebJob.</span></span>

     ![按一下 ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     <span data-ttu-id="45ace-230">儀表板會顯示最近執行的 GenerateThumbnail 函數。</span><span class="sxs-lookup"><span data-stu-id="45ace-230">The Dashboard shows that the GenerateThumbnail function executed recently.</span></span>

     <span data-ttu-id="45ace-231">(下次按一下 [檢視儀表板] 時，您無需登入，瀏覽器便會直接進入您的 WebJob 頁面。)</span><span class="sxs-lookup"><span data-stu-id="45ace-231">(The next time you click **View Dashboard**, you don't have to sign in, and the browser goes directly to the page for your WebJob.)</span></span>
16. <span data-ttu-id="45ace-232">按一下函數名稱可查看執行函數的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="45ace-232">Click the function name to see details about the function execution.</span></span>

     ![函數詳細資料](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

<span data-ttu-id="45ace-234">如果函數會[撰寫記錄](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)，您可以按一下 [ToggleOutput] 查看這些記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-234">If your function [wrote logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), you could click **ToggleOutput** to see them.</span></span>

## <a name="notes-about-remote-debugging"></a><span data-ttu-id="45ace-235">遠端偵錯注意事項</span><span class="sxs-lookup"><span data-stu-id="45ace-235">Notes about remote debugging</span></span>
* <span data-ttu-id="45ace-236">不建議在生產環境中執行偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="45ace-236">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="45ace-237">如果您的生產 Web 應用程式並未調升規模到多個伺服器執行個體，偵錯就會防止 Web 伺服器回應其他要求。</span><span class="sxs-lookup"><span data-stu-id="45ace-237">If your production web app is not scaled out to multiple server instances, debugging will prevent the web server from responding to other requests.</span></span> <span data-ttu-id="45ace-238">如果您不具備多個 Web 伺服器執行個體，當您連結至偵錯工具時，會取得一個隨機產生的執行個體，而且您將無法確認後續瀏覽器要求是否會通往該執行個體。</span><span class="sxs-lookup"><span data-stu-id="45ace-238">If you do have multiple web server instances, when you attach to the debugger you'll get a random instance, and you have no way to ensure that subsequent browser requests will go to that instance.</span></span> <span data-ttu-id="45ace-239">此外，通常我們不會將偵錯組建部署到生產環境中，而且版本組建的編譯器最佳化作業將會使系統無法逐行顯示您的來源程式碼中所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="45ace-239">Also, you typically don't deploy a debug build to production, and compiler optimizations for release builds might make it impossible to show what is happening line by line in your source code.</span></span> <span data-ttu-id="45ace-240">針對生產環境問題的疑難排解，您的最佳資源將是應用程式追蹤與 Web 伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-240">For troubleshooting production problems, your best resource is application tracing and web server logs.</span></span>
* <span data-ttu-id="45ace-241">進行遠端偵錯時，避免長時間在中斷點停止運作。</span><span class="sxs-lookup"><span data-stu-id="45ace-241">Avoid long stops at breakpoints when remote debugging.</span></span> <span data-ttu-id="45ace-242">Azure 會將停止超過幾分鐘的處理序視為無回應的處理序，並將其關閉。</span><span class="sxs-lookup"><span data-stu-id="45ace-242">Azure treats a process that is stopped for longer than a few minutes as an unresponsive process, and shuts it down.</span></span>
* <span data-ttu-id="45ace-243">在偵錯期間，伺服器會將資料傳送至 Visual Studio，進而影響頻寬付費情況。</span><span class="sxs-lookup"><span data-stu-id="45ace-243">While you're debugging, the server is sending data to Visual Studio, which could affect bandwidth charges.</span></span> <span data-ttu-id="45ace-244">如需關於頻寬費率的詳細資訊，請參閱 [Azure 定價](https://azure.microsoft.com/pricing/calculator/)。</span><span class="sxs-lookup"><span data-stu-id="45ace-244">For information about bandwidth rates, see [Azure Pricing](https://azure.microsoft.com/pricing/calculator/).</span></span>
* <span data-ttu-id="45ace-245">確保 *Web.config* 檔案裡 `compilation` 元素中的 `debug` 屬性設為 true。</span><span class="sxs-lookup"><span data-stu-id="45ace-245">Make sure that the `debug` attribute of the `compilation` element in the *Web.config* file is set to true.</span></span> <span data-ttu-id="45ace-246">在發行偵錯組建組態時，該值預設會設為 true。</span><span class="sxs-lookup"><span data-stu-id="45ace-246">It is set to true by default when you publish a debug build configuration.</span></span>

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* <span data-ttu-id="45ace-247">如果您發現偵錯工具無法逐步執行您要偵錯的程式碼，可能需要變更「Just My Code」設定。</span><span class="sxs-lookup"><span data-stu-id="45ace-247">If you find that the debugger won't step into code that you want to debug, you might have to change the Just My Code setting.</span></span>  <span data-ttu-id="45ace-248">如需詳細資訊，請參閱 [將逐步執行限制於 Just My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code)。</span><span class="sxs-lookup"><span data-stu-id="45ace-248">For more information, see [Restrict stepping to Just My Code](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).</span></span>
* <span data-ttu-id="45ace-249">當您啟用遠端偵錯功能時，伺服器上會啟動計時器，並在 48 小時後自動關閉此功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-249">A timer starts on the server when you enable the remote debugging feature, and after 48 hours the feature is automatically turned off.</span></span> <span data-ttu-id="45ace-250">此 48 小時的限制是為了安全與效能起見而設計的功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-250">This 48 hour limit is done for security and performance reasons.</span></span> <span data-ttu-id="45ace-251">若需要，您可以輕鬆開啟這項功能，次數不限。</span><span class="sxs-lookup"><span data-stu-id="45ace-251">You can easily turn the feature back on as many times as you like.</span></span> <span data-ttu-id="45ace-252">當您不需要偵錯時，建議您將其保持為停用。</span><span class="sxs-lookup"><span data-stu-id="45ace-252">We recommend leaving it disabled when you are not actively debugging.</span></span>
* <span data-ttu-id="45ace-253">您可以手動將偵錯工具附加至任何處理序，不僅止於 Web 應用程式處理序 (w3wp.exe)。</span><span class="sxs-lookup"><span data-stu-id="45ace-253">You can manually attach the debugger to any process, not only the web app process (w3wp.exe).</span></span> <span data-ttu-id="45ace-254">如需如何在 Visual Studio 中使用偵錯模式的詳細資訊，請參閱 [Visual Studio 偵錯](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45ace-254">For more information about how to use debug mode in Visual Studio, see [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).</span></span>

## <span data-ttu-id="45ace-255"><a name="logsoverview"></a>診斷記錄概觀</span><span class="sxs-lookup"><span data-stu-id="45ace-255"><a name="logsoverview"></a>Diagnostic logs overview</span></span>
<span data-ttu-id="45ace-256">在 Azure Web 應用程式中執行的 ASP.NET 應用程式，可建立下列各種記錄：</span><span class="sxs-lookup"><span data-stu-id="45ace-256">An ASP.NET application that runs in an Azure web app can create the following kinds of logs:</span></span>

* <span data-ttu-id="45ace-257">**應用程式追蹤記錄**</span><span class="sxs-lookup"><span data-stu-id="45ace-257">**Application tracing logs**</span></span><br/>
  <span data-ttu-id="45ace-258">此應用程式會呼叫 [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) 類別的方法來建立這些記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-258">The application creates these logs by calling methods of the [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) class.</span></span>
* <span data-ttu-id="45ace-259">**Web 伺服器記錄**</span><span class="sxs-lookup"><span data-stu-id="45ace-259">**Web server logs**</span></span><br/>
  <span data-ttu-id="45ace-260">Web 伺服器會為每個通往 Web 應用程式的 HTTP 要求建立記錄項目。</span><span class="sxs-lookup"><span data-stu-id="45ace-260">The web server creates a log entry for every HTTP request to the web app.</span></span>
* <span data-ttu-id="45ace-261">**詳細的錯誤訊息記錄**</span><span class="sxs-lookup"><span data-stu-id="45ace-261">**Detailed error message logs**</span></span><br/>
  <span data-ttu-id="45ace-262">Web 伺服器會針對失敗的 HTTP 要求 (產生狀態碼 400 或以上的要求) 建立含有一些額外資訊的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="45ace-262">The web server creates an HTML page with some additional information for failed HTTP requests (those that result in status code 400 or greater).</span></span>
* <span data-ttu-id="45ace-263">**失敗要求追蹤記錄**</span><span class="sxs-lookup"><span data-stu-id="45ace-263">**Failed request tracing logs**</span></span><br/>
  <span data-ttu-id="45ace-264">Web 伺服器會針對失敗的 HTTP 要求建立含有詳細追蹤資訊的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-264">The web server creates an XML file with detailed tracing information for failed HTTP requests.</span></span> <span data-ttu-id="45ace-265">Web 伺服器會一併提供 XSL 檔案，在瀏覽器中格式化 XML。</span><span class="sxs-lookup"><span data-stu-id="45ace-265">The web server also provides an XSL file to format the XML in a browser.</span></span>

<span data-ttu-id="45ace-266">記錄功能會影響 Web 應用程式效能，因此 Azure 可讓您視需要啟用或停用每一種記錄類型。</span><span class="sxs-lookup"><span data-stu-id="45ace-266">Logging affects web app performance, so Azure gives you the ability to enable or disable each type of log as needed.</span></span> <span data-ttu-id="45ace-267">對於應用程式記錄，您可以指定只寫入高於特定嚴重性層級的記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-267">For application logs, you can specify that only logs above a certain severity level should be written.</span></span> <span data-ttu-id="45ace-268">當您建立新的 Web 應用程式時，預設會停用所有記錄功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-268">When you create a new web app, by default all logging is disabled.</span></span>

<span data-ttu-id="45ace-269">記錄會寫入 Web 應用程式的檔案系統中 *LogFiles* 資料夾內的檔案，而且可以透過 FTP 存取此檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-269">Logs are written to files in a *LogFiles* folder in the file system of your web app and are accessible via FTP.</span></span> <span data-ttu-id="45ace-270">Web 伺服器記錄與應用程式記錄也可以寫入至 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ace-270">Web server logs and application logs can also be written to an Azure Storage account.</span></span> <span data-ttu-id="45ace-271">您可以在儲存體帳戶中保留大於檔案系統可容納的記錄檔數量。</span><span class="sxs-lookup"><span data-stu-id="45ace-271">You can retain a greater volume of logs in a storage account than is possible in the file system.</span></span> <span data-ttu-id="45ace-272">當您使用檔案系統時，最大的記錄檔大小為 100 MB。</span><span class="sxs-lookup"><span data-stu-id="45ace-272">You're limited to a maximum of 100 megabytes of logs when you use the file system.</span></span> <span data-ttu-id="45ace-273">(檔案系統記錄僅適用於短期保留之用。</span><span class="sxs-lookup"><span data-stu-id="45ace-273">(File system logs are only for short-term retention.</span></span> <span data-ttu-id="45ace-274">Azure 會在達到此上限之後刪除舊的記錄檔以騰出空間給新的記錄檔使用。)</span><span class="sxs-lookup"><span data-stu-id="45ace-274">Azure deletes old log files to make room for new ones after the limit is reached.)</span></span>  

## <span data-ttu-id="45ace-275"><a name="apptracelogs"></a>建立並檢視應用程式追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-275"><a name="apptracelogs"></a>Create and view application trace logs</span></span>
<span data-ttu-id="45ace-276">您將在本節執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="45ace-276">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="45ace-277">將追蹤陳述式新增至您在[開始使用 Azure 和 ASP.NET][GetStarted] 中建立的 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="45ace-277">Add tracing statements to the web project that you created in [Get started with Azure and ASP.NET][GetStarted].</span></span>
* <span data-ttu-id="45ace-278">當您在本機上執行專案時檢視記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-278">View the logs when you run the project locally.</span></span>
* <span data-ttu-id="45ace-279">依原樣檢視 Azure 中執行的應用程式所產生的記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-279">View the logs as they are generated by the application running in Azure.</span></span>

<span data-ttu-id="45ace-280">如需如何在 WebJobs 中建立應用程式記錄的詳細資訊，請參閱 [如何運用 WebJobs SDK 來使用 Azure 佇列儲存體 - 如何寫入記錄](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)。</span><span class="sxs-lookup"><span data-stu-id="45ace-280">For information about how to create application logs in WebJobs, see [How to work with Azure queue storage using the WebJobs SDK - How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs).</span></span> <span data-ttu-id="45ace-281">下列有關在 Azure 中檢視記錄和控制記錄儲存方式的指示也同樣適用於 WebJobs 所建立的應用程式記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-281">The following instructions for viewing logs and controlling how they're stored in Azure apply also to application logs created by WebJobs.</span></span>

### <a name="add-tracing-statements-to-the-application"></a><span data-ttu-id="45ace-282">將追蹤陳述式新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="45ace-282">Add tracing statements to the application</span></span>
1. <span data-ttu-id="45ace-283">開啟 *Controllers\HomeController.cs*，然後使用下列程式碼來取代`Index`、`About` 和 `Contact` 方法，以便為 `System.Diagnostics` 加入 `Trace` 陳述式與 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="45ace-283">Open *Controllers\HomeController.cs*, and replace the `Index`, `About`, and `Contact` methods with the following code in order to add `Trace` statements and a `using` statement for `System.Diagnostics`:</span></span>

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template to jump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying the Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on the About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on the Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. <span data-ttu-id="45ace-284">將 `using System.Diagnostics;` 陳述式新增至檔案頂端。</span><span class="sxs-lookup"><span data-stu-id="45ace-284">Add a `using System.Diagnostics;` statement to the top of the file.</span></span>

### <a name="view-the-tracing-output-locally"></a><span data-ttu-id="45ace-285">在本機檢視追蹤輸出</span><span class="sxs-lookup"><span data-stu-id="45ace-285">View the tracing output locally</span></span>
1. <span data-ttu-id="45ace-286">按 F5 以在偵錯模式中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="45ace-286">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="45ace-287">預設的追蹤接聽程式會將所有追蹤輸出連同其他「偵錯」輸出，一起寫入到 [輸出]  視窗。</span><span class="sxs-lookup"><span data-stu-id="45ace-287">The default trace listener writes all trace output to the **Output** window, along with other Debug output.</span></span> <span data-ttu-id="45ace-288">下圖顯示您加入 `Index` 方法的追蹤陳述式的輸出。</span><span class="sxs-lookup"><span data-stu-id="45ace-288">The following illustration shows the output from the trace statements that you added to the `Index` method.</span></span>

    ![偵錯視窗中的追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    <span data-ttu-id="45ace-290">以下步驟說明如何在網頁中檢視追蹤輸出，而不需在偵錯模式中編譯。</span><span class="sxs-lookup"><span data-stu-id="45ace-290">The following steps show how to view trace output in a web page, without compiling in debug mode.</span></span>
2. <span data-ttu-id="45ace-291">開啟應用程式 Web.config 檔 (專案資料夾中的那個) 並將 `<system.diagnostics>` 元素新增至檔案結尾 `</configuration>` 元素關閉處前：</span><span class="sxs-lookup"><span data-stu-id="45ace-291">Open the application Web.config file (the one located in the project folder) and add a `<system.diagnostics>` element at the end of the file just before the closing `</configuration>` element:</span></span>

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

    <span data-ttu-id="45ace-292">`WebPageTraceListener` 可讓您藉由瀏覽至 `/trace.axd` 來檢視追蹤輸出。</span><span class="sxs-lookup"><span data-stu-id="45ace-292">The `WebPageTraceListener` lets you view trace output by browsing to `/trace.axd`.</span></span>
3. <span data-ttu-id="45ace-293">在 Web.config 檔案的 `<system.web>` 下方，加入<a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">追蹤元素</a>，如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="45ace-293">Add a <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">trace element</a> under `<system.web>` in the Web.config file, such as the following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. <span data-ttu-id="45ace-294">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="45ace-294">Press CTRL+F5 to run the application.</span></span>
5. <span data-ttu-id="45ace-295">在瀏覽器視窗的網址列中，將 *trace.axd* 新增至 URL，然後按 Enter (URL 類似於 http://localhost:53370/trace.axd)。</span><span class="sxs-lookup"><span data-stu-id="45ace-295">In the address bar of the browser window, add *trace.axd* to the URL, and then press Enter (the URL will be similar to http://localhost:53370/trace.axd).</span></span>
6. <span data-ttu-id="45ace-296">在 [應用程式追蹤] 頁面上，按一下第一行 (不是 BrowserLink 行) 上的 [檢視詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="45ace-296">On the **Application Trace** page, click **View Details** on the first line (not the BrowserLink line).</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    <span data-ttu-id="45ace-298">[要求詳細資訊] 頁面隨即顯示，而且在 [追蹤資訊] 區段中，您會看到先前加入 `Index` 方法的追蹤陳述式輸出。</span><span class="sxs-lookup"><span data-stu-id="45ace-298">The **Request Details** page appears, and in the **Trace Information** section you see the output from the trace statements that you added to the `Index` method.</span></span>

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    <span data-ttu-id="45ace-300">根據預設， `trace.axd` 只能在本機使用。</span><span class="sxs-lookup"><span data-stu-id="45ace-300">By default, `trace.axd` is only available locally.</span></span> <span data-ttu-id="45ace-301">如果您想從遠端 Web 應用程式使用它，可以將 `localOnly="false"` 加入 *Web.config* 檔案中的 `trace` 元素，如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="45ace-301">If you wanted to make it available from a remote web app, you could add `localOnly="false"` to the `trace` element in the *Web.config* file, as shown in the following example:</span></span>

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    <span data-ttu-id="45ace-302">但是，為了安全起見，通常不建議在生產 Web 應用程式中啟用 `trace.axd` ，而以下各節將為您說明如何用更簡易的方式，在 Azure Web 應用程式中讀取追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-302">However, enabling `trace.axd` in a production web app is generally not recommended for security reasons, and in the following sections you'll see an easier way to read tracing logs in an Azure web app.</span></span>

### <a name="view-the-tracing-output-in-azure"></a><span data-ttu-id="45ace-303">在 Azure 中檢視追蹤輸出</span><span class="sxs-lookup"><span data-stu-id="45ace-303">View the tracing output in Azure</span></span>
1. <span data-ttu-id="45ace-304">在 [方案總管] 中，於 Web 專案上按一下滑鼠右鍵，再按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="45ace-304">In **Solution Explorer**, right-click the web project and click **Publish**.</span></span>
2. <span data-ttu-id="45ace-305">在 [發佈 Web] 對話方塊中，按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="45ace-305">In the **Publish Web** dialog box, click **Publish**.</span></span>

    <span data-ttu-id="45ace-306">當 Visual Studio 成功發行您的更新後，將會開啟瀏覽器視窗至您的首頁 (假設您並未清除 [連線] 索引標籤上的 [目的地 URL])。</span><span class="sxs-lookup"><span data-stu-id="45ace-306">After Visual Studio publishes your update, it opens a browser window to your home page (assuming you didn't clear **Destination URL** on the **Connection** tab).</span></span>
3. <span data-ttu-id="45ace-307">在 [伺服器總管] 中，以滑鼠右鍵按一下您的 Web 應用程式，然後選取 [檢視串流記錄]。</span><span class="sxs-lookup"><span data-stu-id="45ace-307">In **Server Explorer**, right-click your web app and select **View Streaming Logs**.</span></span>

    ![在內容功能表中檢視串流記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    <span data-ttu-id="45ace-309">[輸出]  視窗會顯示您已連線至記錄串流服務，並每一分鐘將沒有要顯示的記錄新增一行通知文字。</span><span class="sxs-lookup"><span data-stu-id="45ace-309">The **Output** window shows that you are connected to the log-streaming service, and adds a notification line each minute that goes by without a log to display.</span></span>

    ![在內容功能表中檢視串流記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. <span data-ttu-id="45ace-311">在顯示您的應用程式首頁的瀏覽器視窗中，按一下 [連絡人] 。</span><span class="sxs-lookup"><span data-stu-id="45ace-311">In the browser window that shows your application home page, click **Contact**.</span></span>

    <span data-ttu-id="45ace-312">幾秒鐘後，您加入 `Contact` 方法的錯誤層級追蹤輸出便會顯示在 [輸出] 視窗。</span><span class="sxs-lookup"><span data-stu-id="45ace-312">Within a few seconds the output from the error-level trace you added to the `Contact` method appears in the **Output** window.</span></span>

    ![輸出視窗中的錯誤追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    <span data-ttu-id="45ace-314">Visual Studio 只會顯示錯誤層級追蹤，因為那是您在啟用記錄監視服務時的預設設定。</span><span class="sxs-lookup"><span data-stu-id="45ace-314">Visual Studio is only showing error-level traces because that is the default setting when you enable the log monitoring service.</span></span> <span data-ttu-id="45ace-315">建立新的 Azure Web 應用程式時，預設會停用所有記錄功能，正如同稍早您在開啟設定頁面時所見：</span><span class="sxs-lookup"><span data-stu-id="45ace-315">When you create a new Azure web app, all logging is disabled by default, as you saw when you opened the settings page earlier:</span></span>

    ![應用程式記錄功能關閉](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    <span data-ttu-id="45ace-317">不過，當您選取 [檢視串流記錄] 時，Visual Studio 會自動將 [Application Logging (File System)] 變更為 [錯誤]，代表回報的會是錯誤層級記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-317">However, when you selected **View Streaming Logs**, Visual Studio automatically changed **Application Logging(File System)** to **Error**, which means error-level logs get reported.</span></span> <span data-ttu-id="45ace-318">為了查看所有的追蹤記錄，您可以將此設定變更為 [詳細資訊] 。</span><span class="sxs-lookup"><span data-stu-id="45ace-318">In order to see all of your tracing logs, you can change this setting to **Verbose**.</span></span> <span data-ttu-id="45ace-319">當您選取低於錯誤的嚴重性層級時，將一併回報較高嚴重性層級的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-319">When you select a severity level lower than error, all logs for higher severity levels are also reported.</span></span> <span data-ttu-id="45ace-320">因此當您選取詳細資訊時，您會同時看到資訊、警告與錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-320">So when you select verbose, you also see information, warning, and error logs.</span></span>  

1. <span data-ttu-id="45ace-321">在 [伺服器總管] 中，以滑鼠右鍵按一下 Web 應用程式，然後按一下 [檢視設定] \(如同您稍早所做的動作)。</span><span class="sxs-lookup"><span data-stu-id="45ace-321">In **Server Explorer**, right-click the web app, and then click **View Settings** as you did earlier.</span></span>
2. <span data-ttu-id="45ace-322">將 [Application Logging (File System)] 變更為 [詳細資訊]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="45ace-322">Change **Application Logging (File System)** to **Verbose**, and then click **Save**.</span></span>

    ![將追蹤層級設定為詳細資訊](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. <span data-ttu-id="45ace-324">在顯示您的 [連絡人] 頁面的瀏覽器視窗中，依序按一下 [首頁]、[關於]、[連絡人]。</span><span class="sxs-lookup"><span data-stu-id="45ace-324">In the browser window that is now showing your **Contact** page, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="45ace-325">在幾秒鐘內，[輸出]  視窗就會顯示您的所有追蹤輸出。</span><span class="sxs-lookup"><span data-stu-id="45ace-325">Within a few seconds, the **Output** window shows all of your tracing output.</span></span>

    ![詳細資訊追蹤輸出](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    <span data-ttu-id="45ace-327">在本節中，您已使用 Azure Web 應用程式設定來啟用與停用記錄功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-327">In this section you enabled and disabled logging by using Azure web app settings.</span></span> <span data-ttu-id="45ace-328">您也可以修改 Web.config 檔案，來啟用與停用追蹤接聽程式。</span><span class="sxs-lookup"><span data-stu-id="45ace-328">You can also enable and disable trace listeners by modifying the Web.config file.</span></span> <span data-ttu-id="45ace-329">不過，修改 Web.config 檔案會導致應用程式網域回收，而透過 Web 應用程式設定來啟用記錄功能則不會有這種現象。</span><span class="sxs-lookup"><span data-stu-id="45ace-329">However, modifying the Web.config file causes the app domain to recycle, while enabling logging via the web app configuration doesn't do that.</span></span> <span data-ttu-id="45ace-330">如果此問題需要經過長時間才會重現或是間歇性出現，則回收應用程式網域可能「修正」此問題，並強迫您等候問題再次發生。</span><span class="sxs-lookup"><span data-stu-id="45ace-330">If the problem takes a long time to reproduce, or is intermittent, recycling the app domain might "fix" it and force you to wait until it happens again.</span></span> <span data-ttu-id="45ace-331">在 Azure 中啟用診斷功能不會出現此情況，因此您可以立即開始擷取錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="45ace-331">Enabling diagnostics in Azure doesn't do this, so you can start capturing error information immediately.</span></span>

### <a name="output-window-features"></a><span data-ttu-id="45ace-332">輸出視窗功能</span><span class="sxs-lookup"><span data-stu-id="45ace-332">Output window features</span></span>
<span data-ttu-id="45ace-333">[輸出] 視窗的 [Azure 記錄] 索引標籤具有多個按鈕與一個文字方塊：</span><span class="sxs-lookup"><span data-stu-id="45ace-333">The **Azure Logs** tab of the **Output** Window has several buttons and a text box:</span></span>

![記錄索引標籤按鈕](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

<span data-ttu-id="45ace-335">這些物件可執行下列功能：</span><span class="sxs-lookup"><span data-stu-id="45ace-335">These perform the following functions:</span></span>

* <span data-ttu-id="45ace-336">清除 [輸出]  視窗。</span><span class="sxs-lookup"><span data-stu-id="45ace-336">Clear the **Output** window.</span></span>
* <span data-ttu-id="45ace-337">啟用或停用自動換行。</span><span class="sxs-lookup"><span data-stu-id="45ace-337">Enable or disable word wrap.</span></span>
* <span data-ttu-id="45ace-338">啟動或停止監視記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-338">Start or stop monitoring logs.</span></span>
* <span data-ttu-id="45ace-339">指定要監視的記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-339">Specify which logs to monitor.</span></span>
* <span data-ttu-id="45ace-340">下載記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-340">Download logs.</span></span>
* <span data-ttu-id="45ace-341">依據搜尋字串或規則運算式篩選記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-341">Filter logs based on a search string or a regular expression.</span></span>
* <span data-ttu-id="45ace-342">關閉 [輸出]  視窗。</span><span class="sxs-lookup"><span data-stu-id="45ace-342">Close the **Output** window.</span></span>

<span data-ttu-id="45ace-343">如果您輸入搜尋字串或是規則運算式，則 Visual Studio 會篩選用戶端的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="45ace-343">If you enter a search string or regular expression, Visual Studio filters logging information at the client.</span></span> <span data-ttu-id="45ace-344">亦即，您可以等到 [輸出]  視窗顯示記錄後輸入條件，這樣您不需重新產生記錄便能直接變更篩選條件。</span><span class="sxs-lookup"><span data-stu-id="45ace-344">That means you can enter the criteria after the logs are displayed in the **Output** window and you can change filtering criteria without having to regenerate the logs.</span></span>

## <span data-ttu-id="45ace-345"><a name="webserverlogs"></a>檢視 Web 伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-345"><a name="webserverlogs"></a>View web server logs</span></span>
<span data-ttu-id="45ace-346">Web 伺服器記錄會記下 Web 應用程式的所有 HTTP 活動。</span><span class="sxs-lookup"><span data-stu-id="45ace-346">Web server logs record all HTTP activity for the web app.</span></span> <span data-ttu-id="45ace-347">為了在 [輸出]  視窗中看見這些記錄，您必須針對 Web 應用程式啟用它們，然後告訴 Visual Studio 您想要監視它們。</span><span class="sxs-lookup"><span data-stu-id="45ace-347">In order to see them in the **Output** window you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span></span>

1. <span data-ttu-id="45ace-348">在您從 [伺服器總管] 開啟的 [Azure Web 應用程式設定] 索引標籤中，將 [Web 伺服器記錄] 變更為 [開啟]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="45ace-348">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change Web Server Logging to **On**, and then click **Save**.</span></span>

    ![啟用 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. <span data-ttu-id="45ace-350">在 [輸出] 視窗中，按一下 [指定要監視的 Azure 記錄] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45ace-350">In the **Output** Window, click the **Specify which Azure logs to monitor** button.</span></span>

    ![指定要監視的 Azure 記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. <span data-ttu-id="45ace-352">在 [Azure 記錄選項] 對話方塊中，選取 [Web 伺服器記錄]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="45ace-352">In the **Azure Logging Options** dialog box, select **Web server logs**, and then click **OK**.</span></span>

    ![監視 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. <span data-ttu-id="45ace-354">在顯示 Web 應用程式的瀏覽器視窗中，依序按一下 [首頁]、[關於] 和 [連絡人]。</span><span class="sxs-lookup"><span data-stu-id="45ace-354">In the browser window that shows the web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

    <span data-ttu-id="45ace-355">通常會先產生應用程式記錄，然後才是 Web 伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-355">The application logs generally appear first, followed by the web server logs.</span></span> <span data-ttu-id="45ace-356">您可能需要等候一小段時間，記錄才會顯示。</span><span class="sxs-lookup"><span data-stu-id="45ace-356">You might have to wait a while for the logs to appear.</span></span>

    ![輸出視窗中的 Web 伺服器記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

<span data-ttu-id="45ace-358">根據預設，當您第一次使用 Visual Studio 啟用 Web 伺服器記錄時，Azure 會將記錄寫入檔案系統。</span><span class="sxs-lookup"><span data-stu-id="45ace-358">By default, when you first enable web server logs by using Visual Studio, Azure writes the logs to the file system.</span></span> <span data-ttu-id="45ace-359">作為替代方式，您可以使用 Azure 入口網站來指定應該將 Web 伺服器記錄寫入儲存體帳戶中的某個 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="45ace-359">As an alternative, you can use the Azure portal to specify that web server logs should be written to a blob container in a storage account.</span></span>

<span data-ttu-id="45ace-360">如果您使用入口網站對 Azure 儲存體帳戶啟用 Web 伺服器記錄功能，然後在 Visual Studio 中停用記錄功能，當您在 Visual Studio 中重新啟用記錄功能時，將會還原您的儲存體帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="45ace-360">If you use the portal to enable web server logging to an Azure storage account, and then disable logging in Visual Studio, when you re-enable logging in Visual Studio your storage account settings are restored.</span></span>

## <span data-ttu-id="45ace-361"><a name="detailederrorlogs"></a>檢視詳細的錯誤訊息記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-361"><a name="detailederrorlogs"></a>View detailed error message logs</span></span>
<span data-ttu-id="45ace-362">針對導致錯誤回應代碼 (400 或以上) 之 HTTP 要求，詳細的錯誤訊息記錄可提供部分額外資訊。</span><span class="sxs-lookup"><span data-stu-id="45ace-362">Detailed error logs provide some additional information about HTTP requests that result in error response codes (400 or above).</span></span> <span data-ttu-id="45ace-363">為了在 [輸出]  視窗中看見這些記錄，您必須針對 Web 應用程式啟用它們，然後告訴 Visual Studio 您想要監視它們。</span><span class="sxs-lookup"><span data-stu-id="45ace-363">In order to see them in the **Output** window, you have to enable them for the web app and tell Visual Studio that you want to monitor them.</span></span>

1. <span data-ttu-id="45ace-364">在您從 [伺服器總管] 開啟的 [Azure Web 應用程式組態] 索引標籤中，將 [詳細錯誤訊息] 變更為 [開啟]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="45ace-364">In the **Azure Web App Configuration** tab that you opened from **Server Explorer**, change **Detailed Error Messages** to **On**, and then click **Save**.</span></span>

    ![啟用詳細的錯誤訊息](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. <span data-ttu-id="45ace-366">在 [輸出] 視窗中，按一下 [指定要監視的 Azure 記錄] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="45ace-366">In the **Output** Window, click the **Specify which Azure logs to monitor** button.</span></span>
3. <span data-ttu-id="45ace-367">在 [Azure 記錄選項] 對話方塊中，按一下 [所有記錄]、[確定]。</span><span class="sxs-lookup"><span data-stu-id="45ace-367">In the **Azure Logging Options** dialog box, click **All logs**, and then click **OK**.</span></span>

    ![監視所有記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. <span data-ttu-id="45ace-369">在瀏覽器視窗的網址列中，為 URL 加入額外的字元以引發 404 錯誤 (例如， `http://localhost:53370/Home/Contactx`)，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="45ace-369">In the address bar of the browser window, add an extra character to the URL to cause a 404 error (for example, `http://localhost:53370/Home/Contactx`), and press Enter.</span></span>

    <span data-ttu-id="45ace-370">幾秒鐘之後，詳細的錯誤記錄就會顯示在 Visual Studio 的 [輸出]  視窗。</span><span class="sxs-lookup"><span data-stu-id="45ace-370">After several seconds the detailed error log appears in the Visual Studio **Output** window.</span></span>

    ![輸出視窗中的詳細的錯誤記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    <span data-ttu-id="45ace-372">按住 Ctrl 鍵並按一下該連結，可在瀏覽器中查看格式化的記錄輸出：</span><span class="sxs-lookup"><span data-stu-id="45ace-372">Control+click the link to see the log output formatted in a browser:</span></span>

    ![瀏覽器視窗中的詳細的錯誤記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <span data-ttu-id="45ace-374"><a name="downloadlogs"></a>下載檔案系統記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-374"><a name="downloadlogs"></a>Download file system logs</span></span>
<span data-ttu-id="45ace-375">任何您可在 [輸出]  視窗中監視的記錄，也能下載為 *.zip* 檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-375">Any logs that you can monitor in the **Output** window can also be downloaded as a *.zip* file.</span></span>

1. <span data-ttu-id="45ace-376">在 [輸出] 視窗中，按一下 [Download Streaming Logs]。</span><span class="sxs-lookup"><span data-stu-id="45ace-376">In the **Output** window, click **Download Streaming Logs**.</span></span>

    ![記錄索引標籤按鈕](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    <span data-ttu-id="45ace-378">[檔案總管] 會開啟至您的 *Downloads* 資料夾，並選取下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-378">File Explorer opens to your *Downloads* folder with the downloaded file selected.</span></span>

    ![下載的檔案](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. <span data-ttu-id="45ace-380">將 *.zip* 檔案解壓縮後，您會看到下列資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="45ace-380">Extract the *.zip* file, and you see the following folder structure:</span></span>

    ![下載的檔案](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * <span data-ttu-id="45ace-382">應用程式追蹤記錄位於 LogFiles\Application 資料夾的 .txt 檔案中。</span><span class="sxs-lookup"><span data-stu-id="45ace-382">Application tracing logs are in *.txt* files in the *LogFiles\Application* folder.</span></span>
   * <span data-ttu-id="45ace-383">Web 伺服器記錄位於 LogFiles\http\RawLogs 資料夾的 .log 檔案中。</span><span class="sxs-lookup"><span data-stu-id="45ace-383">Web server logs are in *.log* files in the *LogFiles\http\RawLogs* folder.</span></span> <span data-ttu-id="45ace-384">您可以使用 [記錄檔剖析器](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) (英文) 之類的工具來檢視與操作這些檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-384">You can use a tool such as [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) to view and manipulate these files.</span></span>
   * <span data-ttu-id="45ace-385">詳細的錯誤訊息記錄位於 LogFiles\DetailedErrors 資料夾的 .html 檔案中。</span><span class="sxs-lookup"><span data-stu-id="45ace-385">Detailed error message logs are in *.html* files in the *LogFiles\DetailedErrors* folder.</span></span>

     <span data-ttu-id="45ace-386">(deployments 資料夾用於存放來源控制發行功能所建立的檔案，它與 Visual Studio 發行功能沒有任何關聯。</span><span class="sxs-lookup"><span data-stu-id="45ace-386">(The *deployments* folder is for files created by source control publishing; it doesn't have anything related to Visual Studio publishing.</span></span> <span data-ttu-id="45ace-387">Git 資料夾則用於存放與來源控制發行功能相關的追蹤記錄，以及記錄檔案串流服務。)</span><span class="sxs-lookup"><span data-stu-id="45ace-387">The *Git* folder is for traces related to source control publishing and the log file streaming service.)</span></span>  

## <span data-ttu-id="45ace-388"><a name="storagelogs"></a>檢視儲存體記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-388"><a name="storagelogs"></a>View storage logs</span></span>
<span data-ttu-id="45ace-389">應用程式追蹤記錄也可以傳送至 Azure 儲存體帳戶，以便您在 Visual Studio 中加以檢視。</span><span class="sxs-lookup"><span data-stu-id="45ace-389">Application tracing logs can also be sent to an Azure storage account, and you can view them in Visual Studio.</span></span> <span data-ttu-id="45ace-390">若要這麼做，請建立一個儲存體帳戶，並在傳統入口網站中啟用儲存體記錄，然後透過 [Azure Web 應用程式] 視窗的 [記錄] 索引標籤來檢視它們。</span><span class="sxs-lookup"><span data-stu-id="45ace-390">To do that you'll create a storage account, enable storage logs in the classic portal, and view them in the **Logs** tab of the **Azure Web App** window.</span></span>

<span data-ttu-id="45ace-391">您可以將記錄傳送至以下任意或所有目的地 (共三個)：</span><span class="sxs-lookup"><span data-stu-id="45ace-391">You can send logs to any or all of three destinations:</span></span>

* <span data-ttu-id="45ace-392">檔案系統。</span><span class="sxs-lookup"><span data-stu-id="45ace-392">The file system.</span></span>
* <span data-ttu-id="45ace-393">儲存體帳戶資料表。</span><span class="sxs-lookup"><span data-stu-id="45ace-393">Storage account tables.</span></span>
* <span data-ttu-id="45ace-394">儲存體帳戶 Blob。</span><span class="sxs-lookup"><span data-stu-id="45ace-394">Storage account blobs.</span></span>

<span data-ttu-id="45ace-395">您可以為每個目的地指定不同的嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="45ace-395">You can specify a different severity level for each destination.</span></span>

<span data-ttu-id="45ace-396">資料表可讓您輕鬆地在線上檢視記錄的詳細資料，而且資料表還支援串流；您可以查詢資料表中的記錄，並即時看到正在建立的新記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-396">Tables make it easy to view details of logs online, and they support streaming; you can query logs in tables and see new logs as they are being created.</span></span> <span data-ttu-id="45ace-397">Blob 則可讓您輕鬆地將記錄下載到檔案，並運用 HDInsight 加以分析，因為 HDInsight 知道如何處理 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="45ace-397">Blobs make it easy to download logs in files and to analyze them using HDInsight, because HDInsight knows how to work with blob storage.</span></span> <span data-ttu-id="45ace-398">如需詳細資訊，請參閱 **資料儲存體選項 (運用 Azure 建構真實的雲端應用程式)** 中的 [Hadoop 與 MapReduce](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options)(英文)。</span><span class="sxs-lookup"><span data-stu-id="45ace-398">For more information, see **Hadoop and MapReduce** in [Data Storage Options (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).</span></span>

<span data-ttu-id="45ace-399">您目前已將檔案系統記錄設為詳細資訊層級；以下步驟將帶您逐步設定資訊層級記錄，以便傳送至儲存體帳戶資料表。</span><span class="sxs-lookup"><span data-stu-id="45ace-399">You currently have file system logs set to verbose level; the following steps walk you through setting up information level logs to go to storage account tables.</span></span> <span data-ttu-id="45ace-400">資訊層級代表所有藉由呼叫 `Trace.TraceInformation`、`Trace.TraceWarning` 與 `Trace.TraceError` 的記錄都會顯示出來，但不會顯示藉由呼叫 `Trace.WriteLine` 所建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-400">Information level means all logs created by calling `Trace.TraceInformation`, `Trace.TraceWarning`, and `Trace.TraceError` will be displayed, but not logs created by calling `Trace.WriteLine`.</span></span>

<span data-ttu-id="45ace-401">與檔案系統相較之下，儲存體帳戶可提供更多的儲存體與較長的記錄保留時間。</span><span class="sxs-lookup"><span data-stu-id="45ace-401">Storage accounts offer more storage and longer-lasting retention for logs compared to the file system.</span></span> <span data-ttu-id="45ace-402">將應用程式追蹤記錄傳送至儲存體的另一項好處，就是您可以從每個記錄中獲得更多的額外資訊，而檔案系統記錄則無法提供。</span><span class="sxs-lookup"><span data-stu-id="45ace-402">Another advantage of sending application tracing logs to storage is that you get some additional information with each log that you don't get from file system logs.</span></span>

1. <span data-ttu-id="45ace-403">以滑鼠右鍵按一下 Azure 節點下的 [儲存體]，然後按一下 [建立儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="45ace-403">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>

![建立儲存體帳戶](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. <span data-ttu-id="45ace-405">在 [建立儲存體帳戶]  對話方塊中，輸入儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="45ace-405">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="45ace-406">這個名稱必須是唯一的 (其他 Azure 儲存體帳戶不可以有相同的名稱)。</span><span class="sxs-lookup"><span data-stu-id="45ace-406">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="45ace-407">如果您輸入的名稱已在使用中，您可以變更此名稱。</span><span class="sxs-lookup"><span data-stu-id="45ace-407">If the name you enter is already in use you'll get a chance to change it.</span></span>

    <span data-ttu-id="45ace-408">存取儲存體帳戶的 URL 會是 *{name}*.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="45ace-408">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
2. <span data-ttu-id="45ace-409">將 [區域或同質群組]  下拉式清單設為離您最近的區域。</span><span class="sxs-lookup"><span data-stu-id="45ace-409">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="45ace-410">此設定會指定哪個 Azure 資料中心將會主控您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ace-410">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="45ace-411">在本教學課程中，您的決定並不會造成明顯的差異，但對於生產 Web 應用程式而言，您會希望 Web 伺服器和儲存體帳戶是在相同區域內，以便將延遲和資料輸出費用降到最低。</span><span class="sxs-lookup"><span data-stu-id="45ace-411">For this tutorial your choice won't make a noticeable difference, but for a production web app you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="45ace-412">您稍後將建立的 Web 應用程式的執行區域應該盡可能接近可存取您 Web 應用程式的瀏覽器，以便將延遲降至最低。</span><span class="sxs-lookup"><span data-stu-id="45ace-412">The web app (which you'll create later) should run in a region as close as possible to the browsers accessing your web app in order to minimize latency.</span></span>
3. <span data-ttu-id="45ace-413">將 [複寫] 下拉式清單設為 [本機備援]。</span><span class="sxs-lookup"><span data-stu-id="45ace-413">Set the **Replication** drop-down list to **Locally redundant**.</span></span>
   
    <span data-ttu-id="45ace-414">對儲存體帳戶啟用地理區域複寫時，儲存內容會複寫至次要資料中心，以便能在主要位置發生嚴重災難時容錯移轉至該位置。</span><span class="sxs-lookup"><span data-stu-id="45ace-414">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="45ace-415">地理區域複寫會引發額外成本。</span><span class="sxs-lookup"><span data-stu-id="45ace-415">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="45ace-416">對於測試和開發帳戶，您通常不會想要付費使用地理區域複寫功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-416">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="45ace-417">如需詳細資訊，請參閱 [建立、管理或刪除儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="45ace-417">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
4. <span data-ttu-id="45ace-418">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="45ace-418">Click **Create**.</span></span>

    ![New storage account](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. <span data-ttu-id="45ace-420">在 Visual Studio 的 [Azure Web 應用程式] 視窗中，按一下 [記錄] 索引標籤，然後按一下 [設定管理入口網站中的記錄]。</span><span class="sxs-lookup"><span data-stu-id="45ace-420">In the Visual Studio **Azure Web App** window, click the **Logs** tab, and then click **Configure Logging in Management Portal**.</span></span>

    <!-- todo:screenshot of new portal if the VS page link goes to new portal -->
    ![設定記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    <span data-ttu-id="45ace-422">這會在傳統入口網站中開啟您 Web 應用程式的 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="45ace-422">This opens the **Configure** tab in the classic portal for your web app.</span></span>
6. <span data-ttu-id="45ace-423">在傳統入口網站的 [設定] 索引標籤中，向下捲動至應用程式診斷區段，然後將 [應用程式記錄 (表格儲存體)] 變更為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="45ace-423">In the classic portal's **Configure** tab, scroll down to the application diagnostics section, and then change **Application Logging (Table Storage)** to **On**.</span></span>
7. <span data-ttu-id="45ace-424">將 [記錄層級] 變更為 [資訊]。</span><span class="sxs-lookup"><span data-stu-id="45ace-424">Change **Logging Level** to **Information**.</span></span>
8. <span data-ttu-id="45ace-425">按一下 [管理資料表儲存體] 。</span><span class="sxs-lookup"><span data-stu-id="45ace-425">Click **Manage Table Storage**.</span></span>

    ![按一下 [管理資料表儲存體]](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    <span data-ttu-id="45ace-427">如果您擁有不只一個儲存體帳戶，則可以在 [Manage table storage for application diagnostics]  方塊中選擇您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ace-427">In the **Manage table storage for application diagnostics** box, you can choose your storage account if you have more than one.</span></span> <span data-ttu-id="45ace-428">您可以建立新的資料表，或是使用現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="45ace-428">You can create a new table or use an existing one.</span></span>

    ![管理資料表儲存體](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. <span data-ttu-id="45ace-430">在 [Manage table storage for application diagnostics]  方塊中，按一下核取方塊以關閉該方塊。</span><span class="sxs-lookup"><span data-stu-id="45ace-430">In the **Manage table storage for application diagnostics** box click the check mark to close the box.</span></span>
10. <span data-ttu-id="45ace-431">在傳統入口網站的 [設定] 索引標籤中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="45ace-431">In the classic portal's **Configure** tab, click **Save**.</span></span>
11. <span data-ttu-id="45ace-432">在顯示應用程式 Web 應用程式的瀏覽器視窗中，依序按一下 [首頁]、[關於] 和 [連絡人]。</span><span class="sxs-lookup"><span data-stu-id="45ace-432">In the browser window that displays the application web app, click **Home**, then click **About**, and then click **Contact**.</span></span>

     <span data-ttu-id="45ace-433">瀏覽這些網頁所產生的記錄資訊將會寫入儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ace-433">The logging information produced by browsing these web pages will be written to the storage account.</span></span>
12. <span data-ttu-id="45ace-434">在 Visual Studio 的 [Azure Web 應用程式] 視窗的 [記錄] 索引標籤中，按一下 [診斷摘要] 下方的 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="45ace-434">In the **Logs** tab of the **Azure Web App** window in Visual Studio, click **Refresh** under **Diagnostic Summary**.</span></span>

     ![按一下 [重新整理]](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     <span data-ttu-id="45ace-436">[Diagnostic Summary]  區段預設會顯示最後 15 分鐘的記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-436">The **Diagnostic Summary** section shows logs for the last 15 minutes by default.</span></span> <span data-ttu-id="45ace-437">您可以變更期間以檢視更多記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-437">You can change the period to see more logs.</span></span>

     <span data-ttu-id="45ace-438">(如果出現「找不到資料表」錯誤，請確認您所瀏覽的頁面在您啟用了 [Application Logging (Storage)] 與按一下 [儲存] 之後，能夠進行追蹤作業。)</span><span class="sxs-lookup"><span data-stu-id="45ace-438">(If you get a "table not found" error, verify that you browsed to the pages that do the tracing after you enabled **Application Logging (Storage)** and after you clicked **Save**.)</span></span>

     ![儲存體記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     <span data-ttu-id="45ace-440">請注意，在此檢視中您會看到每個記錄的 [處理序識別碼] 與 [執行緒識別碼]，而這是檔案系統記錄所無法提供。</span><span class="sxs-lookup"><span data-stu-id="45ace-440">Notice that in this view you see **Process ID** and **Thread ID** for each log, which you don't get in the file system logs.</span></span> <span data-ttu-id="45ace-441">您可以直接檢視 Azure 儲存體資料表來查看其他欄位。</span><span class="sxs-lookup"><span data-stu-id="45ace-441">You can see additional fields by viewing the Azure storage table directly.</span></span>
13. <span data-ttu-id="45ace-442">按一下 [View all application logs] 。</span><span class="sxs-lookup"><span data-stu-id="45ace-442">Click **View all application logs**.</span></span>

     <span data-ttu-id="45ace-443">追蹤記錄資料表會顯示在 Azure 儲存體資料表檢視器中。</span><span class="sxs-lookup"><span data-stu-id="45ace-443">The trace log table appears in the Azure storage table viewer.</span></span>

     <span data-ttu-id="45ace-444">(如果出現「序列未包含項目」錯誤，請開啟 [伺服器總管] 並展開 [Azure] 節點下方的儲存體帳戶節點，然後以滑鼠右鍵按一下 [資料表] 並按一下 [重新整理]。)</span><span class="sxs-lookup"><span data-stu-id="45ace-444">(If you get a "sequence contains no elements" error, open **Server Explorer**, expand the node for your storage account under the **Azure** node, and then right-click **Tables** and click **Refresh**.)</span></span>

     ![資料表檢視中的儲存體記錄](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     <span data-ttu-id="45ace-446">此檢視會顯示在其他任何檢視中都不會看到的額外欄位。</span><span class="sxs-lookup"><span data-stu-id="45ace-446">This view shows additional fields you don't see in any other views.</span></span> <span data-ttu-id="45ace-447">此檢視還可讓您藉由特殊的查詢產生器 UI 來篩選記錄，以便建構查詢。</span><span class="sxs-lookup"><span data-stu-id="45ace-447">This view also enables you to filter logs by using special Query Builder UI for constructing a query.</span></span> <span data-ttu-id="45ace-448">如需詳細資訊，請參閱 [使用伺服器總管瀏覽儲存體資源](http://msdn.microsoft.com/library/ff683677.aspx)中的「使用表格資源 - 篩選實體」。</span><span class="sxs-lookup"><span data-stu-id="45ace-448">For more information, see Working with Table Resources - Filtering Entities in [Browsing Storage Resources with Server Explorer](http://msdn.microsoft.com/library/ff683677.aspx).</span></span>
14. <span data-ttu-id="45ace-449">若要查看單一資料列的詳細資訊，請按兩下其中一個資料列。</span><span class="sxs-lookup"><span data-stu-id="45ace-449">To look at the details for a single row, double-click one of the rows.</span></span>

     ![伺服器總管中的追蹤資料表](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <span data-ttu-id="45ace-451"><a name="failedrequestlogs"></a>檢視失敗要求追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-451"><a name="failedrequestlogs"></a>View failed request tracing logs</span></span>
<span data-ttu-id="45ace-452">當您需要了解 IIS 如何處理 HTTP 要求的詳細資料時，例如在 URL 重新寫入或是出現驗證問題等情況，失敗要求追蹤記錄就會很有用。</span><span class="sxs-lookup"><span data-stu-id="45ace-452">Failed request tracing logs are useful when you need to understand the details of how IIS is handling an HTTP request, in scenarios such as URL rewriting or authentication problems.</span></span>

<span data-ttu-id="45ace-453">Azure Web 應用程式會使用 IIS 7.0 及更新版本所提供的相同失敗要求追蹤功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-453">Azure web apps use the same failed request tracing functionality that has been available with IIS 7.0 and later.</span></span> <span data-ttu-id="45ace-454">但您無法存取用來設定哪些錯誤會被記錄下來的 IIS 設定。</span><span class="sxs-lookup"><span data-stu-id="45ace-454">You don't have access to the IIS settings that configure which errors get logged, however.</span></span> <span data-ttu-id="45ace-455">當您啟用失敗要求追蹤時，將擷取所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="45ace-455">When you enable failed request tracing, all errors are captured.</span></span>

<span data-ttu-id="45ace-456">您可以使用 Visual Studio 來啟用失敗要求追蹤，但是您無法在 Visual Studio 中加以檢視。</span><span class="sxs-lookup"><span data-stu-id="45ace-456">You can enable failed request tracing by using Visual Studio, but you can't view them in Visual Studio.</span></span> <span data-ttu-id="45ace-457">這些記錄是 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-457">These logs are XML files.</span></span> <span data-ttu-id="45ace-458">串流記錄服務只會監視被當作可在純文字模式中讀取的檔案：.txt、.html 與 .log 檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-458">The streaming log service only monitors files that are deemed readable in plain text mode:  *.txt*, *.html*, and *.log* files.</span></span>

<span data-ttu-id="45ace-459">您可以直接在瀏覽器中透過 FTP，或是在本機使用 FTP 工具將記錄下載到本機電腦中之後檢視失敗要求追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-459">You can view failed request tracing logs in a browser directly via FTP or locally after using an FTP tool to download them to your local computer.</span></span> <span data-ttu-id="45ace-460">在本節中，您將在瀏覽器中直接檢視。</span><span class="sxs-lookup"><span data-stu-id="45ace-460">In this section you'll view them in a browser directly.</span></span>

1. <span data-ttu-id="45ace-461">在您從 [伺服器總管] 開啟的 [Azure Web 應用程式] 視窗之 [組態] 索引標籤中，將 [失敗要求追蹤] 變更為 [開啟]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="45ace-461">In the **Configuration** tab of the **Azure Web App** window that you opened from **Server Explorer**, change **Failed Request Tracing** to **On**, and then click **Save**.</span></span>

    ![啟用失敗要求追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. <span data-ttu-id="45ace-463">在顯示 Web 應用程式的瀏覽器視窗網址列中，將額外字元新增至 URL 並按 Enter 鍵以引發 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="45ace-463">In the address bar of the browser window that shows the web app, add an extra character to the URL and click Enter to cause a 404 error.</span></span>

    <span data-ttu-id="45ace-464">這麼做會讓系統建立失敗要求追蹤記錄，以下步驟將說明如何檢視或下載記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-464">This causes a failed request tracing log to be created, and the following steps show how to view or download the log.</span></span>
3. <span data-ttu-id="45ace-465">在 Visual Studio 中，於 [Azure Web 應用程式] 視窗的 [組態] 索引標籤中按一下 [在管理入口網站中開啟]。</span><span class="sxs-lookup"><span data-stu-id="45ace-465">In Visual Studio, in the **Configuration** tab of the **Azure Web App** window, click **Open in Management Portal**.</span></span>
4. <span data-ttu-id="45ace-466">在 [Azure 入口網站](https://portal.azure.com)適用於 Web 應用程式的 [設定] 刀鋒視窗中，按一下 [部署認證]，然後輸入新的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="45ace-466">In the [Azure Portal](https://portal.azure.com) **Settings** blade for your web app, click **Deployment credentials**, and then enter a new user name and password.</span></span>

    ![新的 FTP 使用者名稱與密碼](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    <span data-ttu-id="45ace-468">**當您登入時，必須使用此完整使用者名稱搭配 Web 應用程式名稱前置詞。</span><span class="sxs-lookup"><span data-stu-id="45ace-468">**When you log in, you have to use the full user name with the web app name prefixed to it.</span></span> <span data-ttu-id="45ace-469">例如，若您輸入使用者名稱 "myid"，而網站為 "myexample"，則會登入為 "myexample\myid"。</span><span class="sxs-lookup"><span data-stu-id="45ace-469">For example, if you enter "myid" as a user name and the site is "myexample", you log in as "myexample\myid".</span></span>
5. <span data-ttu-id="45ace-470">在新的瀏覽器視窗中，前往您 Web 應用程式之 [Web 應用程式] 刀鋒視窗的 [FTP 主機名稱] 或 [FTPS 主機名稱] 下方所示的 URL。</span><span class="sxs-lookup"><span data-stu-id="45ace-470">In a new browser window, go to the URL that is shown under **FTP hostname** or **FTPS hostname** in the **Web App** blade for your web app.</span></span>
6. <span data-ttu-id="45ace-471">使用您先前建立的 FTP 認證登入 (包括該使用者名稱的 Web 應用程式名稱前置詞)。</span><span class="sxs-lookup"><span data-stu-id="45ace-471">Log in using the FTP credentials that you created earlier (including the web app name prefix for the user name).</span></span>

    <span data-ttu-id="45ace-472">瀏覽器會顯示 Web 應用程式的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="45ace-472">The browser shows the root folder of the web app.</span></span>
7. <span data-ttu-id="45ace-473">開啟 *LogFiles* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="45ace-473">Open the *LogFiles* folder.</span></span>

    ![開啟 LogFiles 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. <span data-ttu-id="45ace-475">開啟名為 W3SVC 並加上數值的資料夾。</span><span class="sxs-lookup"><span data-stu-id="45ace-475">Open the folder that is named W3SVC plus a numeric value.</span></span>

    ![開啟 W3SVC 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    <span data-ttu-id="45ace-477">該資料夾包含了一些 XML 檔案 (內含任何您在啟用失敗要求追蹤功能後所記錄的錯誤)，以及一個可供瀏覽器用來格式化該 XML 檔案的 XSL 檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-477">The folder contains XML files for any errors that have been logged after you enabled failed request tracing, and an XSL file that a browser can use to format the XML.</span></span>

    ![W3SVC 資料夾](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. <span data-ttu-id="45ace-479">按一下 XML 檔案，以取得您想要檢視其追蹤資訊的失敗要求。</span><span class="sxs-lookup"><span data-stu-id="45ace-479">Click the XML file for the failed request that you want to see tracing information for.</span></span>

    <span data-ttu-id="45ace-480">下圖顯示錯誤範例追蹤資訊的片段。</span><span class="sxs-lookup"><span data-stu-id="45ace-480">The following illustration shows part of the tracing information for a sample error.</span></span>

    ![瀏覽器中的失敗要求追蹤](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <span data-ttu-id="45ace-482"><a name="nextsteps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="45ace-482"><a name="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="45ace-483">在了解 Visual Studio 如何讓您輕鬆地檢視 Azure Web 應用程式所建立的記錄之後，</span><span class="sxs-lookup"><span data-stu-id="45ace-483">You've seen how Visual Studio makes it easy to view logs created by an Azure web app.</span></span> <span data-ttu-id="45ace-484">下列各節提供相關主題的更多資源連結：</span><span class="sxs-lookup"><span data-stu-id="45ace-484">The following sections provide links to more resources on related topics:</span></span>

* <span data-ttu-id="45ace-485">Azure Web 應用程式疑難排解</span><span class="sxs-lookup"><span data-stu-id="45ace-485">Azure web app troubleshooting</span></span>
* <span data-ttu-id="45ace-486">Visual Studio 偵錯</span><span class="sxs-lookup"><span data-stu-id="45ace-486">Debugging in Visual Studio</span></span>
* <span data-ttu-id="45ace-487">在 Azure 中遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="45ace-487">Remote debugging in Azure</span></span>
* <span data-ttu-id="45ace-488">在 ASP.NET 應用程式中追蹤</span><span class="sxs-lookup"><span data-stu-id="45ace-488">Tracing in ASP.NET applications</span></span>
* <span data-ttu-id="45ace-489">分析 Web 伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-489">Analyzing web server logs</span></span>
* <span data-ttu-id="45ace-490">分析失敗要求追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-490">Analyzing failed request tracing logs</span></span>
* <span data-ttu-id="45ace-491">偵錯雲端服務</span><span class="sxs-lookup"><span data-stu-id="45ace-491">Debugging Cloud Services</span></span>

### <a name="azure-web-app-troubleshooting"></a><span data-ttu-id="45ace-492">Azure Web 應用程式疑難排解</span><span class="sxs-lookup"><span data-stu-id="45ace-492">Azure web app troubleshooting</span></span>
<span data-ttu-id="45ace-493">如需在 Azure App Service 中疑難排解 Web 應用程式的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="45ace-493">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

* [<span data-ttu-id="45ace-494">如何監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="45ace-494">How to monitor web apps</span></span>](/manage/services/web-sites/how-to-monitor-websites/)
* <span data-ttu-id="45ace-495">[使用 Visual Studio 2013 調查 Azure Web 應用程式中的記憶體流失](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45ace-495">[Investigating Memory Leaks in Azure Web Apps with Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx).</span></span> <span data-ttu-id="45ace-496">Microsoft ALM 部落格文章，討論 Visual Studio 中分析 Managed 記憶體問題的功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-496">Microsoft ALM blog post about Visual Studio features for analyzing managed memory issues.</span></span>
* <span data-ttu-id="45ace-497">[您應該了解的 Azure Web 應用程式線上工具](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/)。</span><span class="sxs-lookup"><span data-stu-id="45ace-497">[Azure web apps online tools you should know about](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/).</span></span> <span data-ttu-id="45ace-498">取自 Amit Apple 的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="45ace-498">Blog post by Amit Apple.</span></span>

<span data-ttu-id="45ace-499">如需特定疑難排解問題的說明，請在下列任一個論壇中開啟一段討論串：</span><span class="sxs-lookup"><span data-stu-id="45ace-499">For help with a specific troubleshooting question, start a thread in one of the following forums:</span></span>

* <span data-ttu-id="45ace-500">[ASP.NET 網站上的 Azure 論壇](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET)。</span><span class="sxs-lookup"><span data-stu-id="45ace-500">[The Azure forum on the ASP.NET site](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).</span></span>
* <span data-ttu-id="45ace-501">[MSDN 上的 Azure 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/)。</span><span class="sxs-lookup"><span data-stu-id="45ace-501">[The Azure forum on MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).</span></span>
* <span data-ttu-id="45ace-502">[StackOverflow.com](http://www.stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="45ace-502">[StackOverflow.com](http://www.stackoverflow.com).</span></span>

### <a name="debugging-in-visual-studio"></a><span data-ttu-id="45ace-503">Visual Studio 偵錯</span><span class="sxs-lookup"><span data-stu-id="45ace-503">Debugging in Visual Studio</span></span>
<span data-ttu-id="45ace-504">如需如何在 Visual Studio 中使用偵錯模式的詳細資訊，請參閱[在 Visual Studio 中偵錯 MSDN 主題](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx)與 [Visual Studio 2010 的偵錯秘訣](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45ace-504">For more information about how to use debug mode in Visual Studio, see the [Debugging in Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN topic and [Debugging Tips with Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).</span></span>

### <a name="remote-debugging-in-azure"></a><span data-ttu-id="45ace-505">在 Azure 中遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="45ace-505">Remote debugging in Azure</span></span>
<span data-ttu-id="45ace-506">如需針對 Azure Web 應用程式與 WebJob 進行遠端偵錯的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="45ace-506">For more information about remote debugging for Azure web apps and WebJobs, see the following resources:</span></span>

* <span data-ttu-id="45ace-507">[遠端偵錯 Azure App Service Web Apps 的簡介](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="45ace-507">[Introduction to Remote Debugging Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).</span></span>
* [<span data-ttu-id="45ace-508">遠端偵錯 Azure App Service Web Apps 的簡介第 2 部分 - 內部遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="45ace-508">Introduction to Remote Debugging Azure App Service Web Apps part 2 - Inside Remote debugging</span></span>](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [<span data-ttu-id="45ace-509">遠端偵錯 Azure App Service Web Apps 的簡介第 3 部分 - 多重執行個體環境和 GIT</span><span class="sxs-lookup"><span data-stu-id="45ace-509">Introduction to Remote Debugging on Azure App Service Web Apps part 3 - Multi-Instance environment and GIT</span></span>](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [<span data-ttu-id="45ace-510">WebJobs 偵錯 (影片)</span><span class="sxs-lookup"><span data-stu-id="45ace-510">WebJobs Debugging (video)</span></span>](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

<span data-ttu-id="45ace-511">如果您的 Web 應用程式使用 Azure Web API 或行動服務後端，而您需要加以偵錯，請參閱 [在 Visual Studio 中對 .NET 後端進行偵錯](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45ace-511">If your web app uses an Azure Web API or Mobile Services back-end and you need to debug that, see [Debugging .NET Backend in Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).</span></span>

### <a name="tracing-in-aspnet-applications"></a><span data-ttu-id="45ace-512">在 ASP.NET 應用程式中追蹤</span><span class="sxs-lookup"><span data-stu-id="45ace-512">Tracing in ASP.NET applications</span></span>
<span data-ttu-id="45ace-513">網際網路上找不到關於 ASP.NET 追蹤功能詳盡且具時效性的說明。</span><span class="sxs-lookup"><span data-stu-id="45ace-513">There are no thorough and up-to-date introductions to ASP.NET tracing available on the Internet.</span></span> <span data-ttu-id="45ace-514">您所能做的，就是從專為 Web Form 所撰寫的一些舊有簡介資料下手，因為 MVC 是最近才問世的技術，並以著重在特定議題的較新的部落格文章來做為補充。</span><span class="sxs-lookup"><span data-stu-id="45ace-514">The best you can do is get started with old introductory materials written for Web Forms because MVC didn't exist yet, and supplement that with newer blog posts that focus on specific issues.</span></span> <span data-ttu-id="45ace-515">以下資源是您開始了解這項技術的一些好去處：</span><span class="sxs-lookup"><span data-stu-id="45ace-515">Some good places to start are the following resources:</span></span>

* <span data-ttu-id="45ace-516">[監視與遙測 (運用 Azure 建構真實的雲端應用程式) (英文)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry)。</span><span class="sxs-lookup"><span data-stu-id="45ace-516">[Monitoring and Telemetry (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).</span></span><br>
  <span data-ttu-id="45ace-517">針對追蹤 Azure 雲端應用程式所建議的電子書章節。</span><span class="sxs-lookup"><span data-stu-id="45ace-517">E-book chapter with recommendations for tracing in Azure cloud applications.</span></span>
* [<span data-ttu-id="45ace-518">ASP.NET 追蹤</span><span class="sxs-lookup"><span data-stu-id="45ace-518">ASP.NET Tracing</span></span>](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  <span data-ttu-id="45ace-519">舊有但仍是該主題的基本簡介的良好資源。</span><span class="sxs-lookup"><span data-stu-id="45ace-519">Old but still a good resource for a basic introduction to the subject.</span></span>
* [<span data-ttu-id="45ace-520">追蹤接聽程式</span><span class="sxs-lookup"><span data-stu-id="45ace-520">Trace Listeners</span></span>](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  <span data-ttu-id="45ace-521">內含有關追蹤接聽程式的資訊，但是沒有提到 [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx)。</span><span class="sxs-lookup"><span data-stu-id="45ace-521">Information about trace listeners but doesn't mention the [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).</span></span>
* [<span data-ttu-id="45ace-522">逐步解說︰整合 ASP.NET 追蹤與 System.Diagnostics 追蹤</span><span class="sxs-lookup"><span data-stu-id="45ace-522">Walkthrough: Integrating ASP.NET Tracing with System.Diagnostics Tracing</span></span>](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  <span data-ttu-id="45ace-523">(英文) 同樣為舊有的資料，但是內含簡介文章沒有提到的一些額外資訊。</span><span class="sxs-lookup"><span data-stu-id="45ace-523">This too is old, but includes some additional information that the introductory article doesn't cover.</span></span>
* [<span data-ttu-id="45ace-524">追蹤 ASP.NET MVC Razor 檢視</span><span class="sxs-lookup"><span data-stu-id="45ace-524">Tracing in ASP.NET MVC Razor Views</span></span>](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  <span data-ttu-id="45ace-525">除了追蹤 Razor 檢視之外，該文同時說明了如何建立錯誤篩選條件以便記錄 MVC 應用程式所出現的所有未處理的例外。</span><span class="sxs-lookup"><span data-stu-id="45ace-525">Besides tracing in Razor views, the post also explains how to create an error filter in order to log all unhandled exceptions in an MVC application.</span></span> <span data-ttu-id="45ace-526">如需如何記錄 Web Form 應用程式中所有未處理的例外項目的詳細資訊，請參閱 MSDN 上 [完整的錯誤處理常式範例](http://msdn.microsoft.com/library/bb397417.aspx) (英文) 的 Global.asax 範例。</span><span class="sxs-lookup"><span data-stu-id="45ace-526">For information about how to log all unhandled exceptions in a Web Forms application, see the Global.asax example in [Complete Example for Error Handlers](http://msdn.microsoft.com/library/bb397417.aspx) on MSDN.</span></span> <span data-ttu-id="45ace-527">無論是 MVC 還是 Web Form，如果您想要記錄特定例外，但是讓預設的架構處理功能生效，則您可以如以下範例所示捕捉並重新擲回這些例外：</span><span class="sxs-lookup"><span data-stu-id="45ace-527">In either MVC or Web Forms, if you want to log certain exceptions but let the default framework handling take effect for them, you can catch and rethrow as in the following example:</span></span>

        try
        {
           // Your code that might cause an exception to be thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [<span data-ttu-id="45ace-528">從 Azure 命令列串流診斷追蹤記錄 (加上 Glimpse！)</span><span class="sxs-lookup"><span data-stu-id="45ace-528">Streaming Diagnostics Trace Logging from the Azure Command Line (plus Glimpse!)</span></span>](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  <span data-ttu-id="45ace-529">如何使用命令列來執行本教學課程所示範的 Visual Studio 步驟。</span><span class="sxs-lookup"><span data-stu-id="45ace-529">How to use the command line to do what this tutorial shows how to do in Visual Studio.</span></span> <span data-ttu-id="45ace-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) (英文) 工具可供您偵錯 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45ace-530">[Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) is a tool for debugging ASP.NET applications.</span></span>
* <span data-ttu-id="45ace-531">[使用 Azure Web Apps 記錄和診斷功能 - 與 David Ebbo 合作](/documentation/videos/azure-web-site-logging-and-diagnostics/)以及[來自 Web Apps 的串流記錄 - 與 David Ebbo 合作](/documentation/videos/log-streaming-with-azure-web-sites/)</span><span class="sxs-lookup"><span data-stu-id="45ace-531">[Using Web Apps Logging and Diagnostics - with David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) and [Streaming Logs from Web Apps - with David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)</span></span><br>
  <span data-ttu-id="45ace-532">(英文) 影片，由 Scott Hanselman 與 David Ebbo 共同錄製。</span><span class="sxs-lookup"><span data-stu-id="45ace-532">Videos by Scott Hanselman and David Ebbo.</span></span>

<span data-ttu-id="45ace-533">針對錯誤記錄，做為撰寫自己的追蹤程式碼的替代方法，便是使用開放原始碼的記錄架構，例如 [ELMAH](http://nuget.org/packages/elmah/)。</span><span class="sxs-lookup"><span data-stu-id="45ace-533">For error logging, an alternative to writing your own tracing code is to use an open-source logging framework such as [ELMAH](http://nuget.org/packages/elmah/).</span></span> <span data-ttu-id="45ace-534">如需詳細資訊，請參閱 [Scott Hanselman 關於 ELMAH 的部落格文章](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)(英文)。</span><span class="sxs-lookup"><span data-stu-id="45ace-534">For more information, see [Scott Hanselman's blog posts about ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).</span></span>

<span data-ttu-id="45ace-535">此外，如果您想要從 Azure 取得串流記錄，則您不需要使用 ASP.NET 或 System.Diagnostics 追蹤功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-535">Also, note that you don't have to use ASP.NET or System.Diagnostics tracing if you want to get streaming logs from Azure.</span></span> <span data-ttu-id="45ace-536">Azure Web 應用程式串流記錄服務會串流它在 LogFiles 資料夾所找到的任何 .txt、.html 或 .log 檔案。</span><span class="sxs-lookup"><span data-stu-id="45ace-536">The Azure web app streaming log service will stream any *.txt*, *.html*, or *.log* file that it finds in the *LogFiles* folder.</span></span> <span data-ttu-id="45ace-537">因此，您可以建立自己的記錄系統以寫入 Web 應用程式的檔案系統，而您的檔案將自動進行串流與下載。</span><span class="sxs-lookup"><span data-stu-id="45ace-537">Therefore, you could create your own logging system that writes to the file system of the web app, and your file will be automatically streamed and downloaded.</span></span> <span data-ttu-id="45ace-538">您只需撰寫會在 d:\home\logfiles 資料夾中建立相關檔案的應用程式碼。</span><span class="sxs-lookup"><span data-stu-id="45ace-538">All you have to do is write application code that creates files in the *d:\home\logfiles* folder.</span></span>

### <a name="analyzing-web-server-logs"></a><span data-ttu-id="45ace-539">分析 Web 伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-539">Analyzing web server logs</span></span>
<span data-ttu-id="45ace-540">如需分析 Web 伺服器記錄的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="45ace-540">For more information about analyzing web server logs, see the following resources:</span></span>

* [<span data-ttu-id="45ace-541">LogParser</span><span class="sxs-lookup"><span data-stu-id="45ace-541">LogParser</span></span>](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  <span data-ttu-id="45ace-542">用於檢視 Web 伺服器記錄 (*.log* 檔案) 中資料的工具。</span><span class="sxs-lookup"><span data-stu-id="45ace-542">A tool for viewing data in web server logs (*.log* files).</span></span>
* [<span data-ttu-id="45ace-543">疑難排解 IIS 效能問題或使用 LogParser 的應用程式錯誤</span><span class="sxs-lookup"><span data-stu-id="45ace-543">Troubleshooting IIS Performance Issues or Application Errors using LogParser </span></span>](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  <span data-ttu-id="45ace-544">此篇介紹可以用來分析 Web 伺服器記錄的 Log Parser 工具。</span><span class="sxs-lookup"><span data-stu-id="45ace-544">An introduction to the Log Parser tool that you can use to analyze web server logs.</span></span>
* [<span data-ttu-id="45ace-545">Robert McMurray 關於使用 LogParser 的部落格文章</span><span class="sxs-lookup"><span data-stu-id="45ace-545">Blog posts by Robert McMurray on using LogParser</span></span>](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [<span data-ttu-id="45ace-546">IIS 7.0、IIS 7.5 與 IIS 8.0 中的 HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="45ace-546">The HTTP status code in IIS 7.0, IIS 7.5, and IIS 8.0</span></span>](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a><span data-ttu-id="45ace-547">分析失敗要求追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="45ace-547">Analyzing failed request tracing logs</span></span>
<span data-ttu-id="45ace-548">Microsoft TechNet 網站內的 [使用失敗要求追蹤](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) (英文) 小節可能有助您了解如何使用這些記錄。</span><span class="sxs-lookup"><span data-stu-id="45ace-548">The Microsoft TechNet website includes a [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) section which may be helpful for understanding how to use these logs.</span></span> <span data-ttu-id="45ace-549">不過，本文主要著重在 IIS 內設定失敗要求追蹤功能，這是您無法在 Azure Web Apps 中執行的功能。</span><span class="sxs-lookup"><span data-stu-id="45ace-549">However, this documentation focuses mainly on configuring failed request tracing in IIS, which you can't do in Azure Web Apps.</span></span>

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
