---
title: "aaaAzure Application Insights for JavaScript web 應用程式 |Microsoft 文件"
description: "取得頁面檢視和工作階段計數、Web 用戶端資料，並追蹤使用量模式。 Detect exceptions and performance issues in JavaScript web pages."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="a6577-104">適用於網頁的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6577-104">Application Insights for web pages</span></span>
<span data-ttu-id="a6577-105">了解 hello 效能和網頁或應用程式的使用方式。</span><span class="sxs-lookup"><span data-stu-id="a6577-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="a6577-106">如果您將加入[Application Insights](app-insights-overview.md) tooyour 頁面指令碼，取得頁面載入和 AJAX 呼叫、 計數和瀏覽器例外狀況和 AJAX 失敗，以及使用者和工作階段計數的詳細資料的執行時間。</span><span class="sxs-lookup"><span data-stu-id="a6577-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="a6577-107">這些項目可以依據頁面、用戶端作業系統和瀏覽器版本、地區位置和其他維度分割。</span><span class="sxs-lookup"><span data-stu-id="a6577-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="a6577-108">您可以對失敗計數或緩慢頁面載入設定警示。</span><span class="sxs-lookup"><span data-stu-id="a6577-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="a6577-109">並在 JavaScript 程式碼中插入追蹤呼叫，您可以追蹤 hello 的網頁應用程式的不同功能使用方式。</span><span class="sxs-lookup"><span data-stu-id="a6577-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="a6577-110">Application Insights 可以使用於任何網頁 - 您剛剛新增 JavaScript 的簡短片段。</span><span class="sxs-lookup"><span data-stu-id="a6577-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="a6577-111">如果您的 Web 服務是 [Java](app-insights-java-get-started.md) 或 [ASP.NET](app-insights-asp-net.md)，您可以整合來自您的伺服器和用戶端的遙測。</span><span class="sxs-lookup"><span data-stu-id="a6577-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![在 portal.azure.com 中，開啟您的應用程式資源，然後按一下 [瀏覽器]](./media/app-insights-javascript/03.png)

<span data-ttu-id="a6577-113">您需要訂用帳戶[Microsoft Azure](https://azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a6577-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="a6577-114">如果您的小組有組織的訂用帳戶，詢問您 Microsoft 帳戶 tooit hello 擁有者 tooadd。</span><span class="sxs-lookup"><span data-stu-id="a6577-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="a6577-115">開發和小規模的使用不需要任何成本。</span><span class="sxs-lookup"><span data-stu-id="a6577-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="a6577-116">為您的網頁設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6577-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="a6577-117">加入 hello 載入器程式碼片段 tooyour 網頁，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a6577-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="a6577-118">開啟或建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="a6577-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="a6577-119">hello Application Insights 資源是其中會顯示網頁的效能和使用方式的相關資料。</span><span class="sxs-lookup"><span data-stu-id="a6577-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="a6577-120">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a6577-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="a6577-121">如果您已經設定 hello 伺服器端應用程式的監視，您已經擁有的資源：</span><span class="sxs-lookup"><span data-stu-id="a6577-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![選擇 [瀏覽]、[開發人員服務]、[Application Insights]。](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="a6577-123">如果您沒有資源，請建立資源：</span><span class="sxs-lookup"><span data-stu-id="a6577-123">If you don't have one, create it:</span></span>

![選擇 [新增]、[開發人員服務]、[Application Insights]。](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="a6577-125">*已經有問題了嗎？*</span><span class="sxs-lookup"><span data-stu-id="a6577-125">*Questions already?*</span></span> <span data-ttu-id="a6577-126">[建立資源的詳細資訊](app-insights-create-new-resource.md)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a6577-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="a6577-127">新增 hello SDK 指令碼 tooyour 應用程式或 web 網頁</span><span class="sxs-lookup"><span data-stu-id="a6577-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="a6577-128">在 快速入門中，取得網頁 hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="a6577-128">In Quick Start, get hello script for web pages:</span></span>

![在您的應用程式概觀刀鋒視窗中，選擇 [快速啟動]，取得程式碼 toomonitor 我的網頁。](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="a6577-131">插入 hello 指令碼之前 hello`</head>`標記要 tootrack 的每一頁。</span><span class="sxs-lookup"><span data-stu-id="a6577-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="a6577-132">如果您的網站有主版頁面，您可以那里出 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a6577-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="a6577-133">例如：</span><span class="sxs-lookup"><span data-stu-id="a6577-133">For example:</span></span>

* <span data-ttu-id="a6577-134">在 ASP.NET MVC 專案中，可放在 `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="a6577-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="a6577-135">在 SharePoint 網站上 hello [控制台] 中，開啟[站台設定 / 主版頁面](app-insights-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="a6577-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="a6577-136">hello 指令碼包含 hello 將導向 hello 資料 tooyour Application Insights 資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6577-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="a6577-137">([Hello 指令碼的所需的深入說明。](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="a6577-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="a6577-138">*(如果您使用的是已知網頁架構，請在 Application Insights 配接器附近尋找。例如，有 [AngularJS 模組](http://ngmodules.org/modules/angular-appinsights)。)*</span><span class="sxs-lookup"><span data-stu-id="a6577-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="a6577-139">詳細組態</span><span class="sxs-lookup"><span data-stu-id="a6577-139">Detailed configuration</span></span>
<span data-ttu-id="a6577-140">您可以設定數種 [參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) ，但是在大部分情況下，您應該不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="a6577-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="a6577-141">比方說，您可以停用或限制 hello Ajax 呼叫每個頁面檢視 （tooreduce 流量） 報告的數目。</span><span class="sxs-lookup"><span data-stu-id="a6577-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="a6577-142">或者，您可以設定偵錯模式 toohave 遙測逐一快速 hello 管線，而不在批次。</span><span class="sxs-lookup"><span data-stu-id="a6577-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="a6577-143">tooset 這些參數中，尋找在 hello 程式碼片段中，這一行，並在它之後新增多個以逗號分隔的項目：</span><span class="sxs-lookup"><span data-stu-id="a6577-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="a6577-144">hello[可用參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)包括：</span><span class="sxs-lookup"><span data-stu-id="a6577-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="a6577-145"><a name="run"></a>執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="a6577-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="a6577-146">執行您 web 應用程式，請使用它時 toogenerate 遙測，並稍候幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="a6577-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="a6577-147">您可以執行使用 hello **F5**您的開發電腦上的主要或將它發行，並且讓使用者開始處理它。</span><span class="sxs-lookup"><span data-stu-id="a6577-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="a6577-148">如果您想 toocheck hello 遙測 web 應用程式正在傳送 tooApplication 深入資訊，請使用您的瀏覽器偵錯工具 (**F12**許多瀏覽器上)。</span><span class="sxs-lookup"><span data-stu-id="a6577-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="a6577-149">資料會傳送 toodc.services.visualstudio.com。</span><span class="sxs-lookup"><span data-stu-id="a6577-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="a6577-150">探索瀏覽器效能資料</span><span class="sxs-lookup"><span data-stu-id="a6577-150">Explore your browser performance data</span></span>
<span data-ttu-id="a6577-151">從使用者的瀏覽器開啟 hello 瀏覽器刀鋒視窗 tooshow 彙總的效能資料。</span><span class="sxs-lookup"><span data-stu-id="a6577-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![在 portal.azure.com 中，開啟您的應用程式資源然後按一下 [設定]、[瀏覽器]。](./media/app-insights-javascript/03.png)

<span data-ttu-id="a6577-153">*仍沒有資料？按一下**重新整理**hello 頁面頂端的 hello。仍然沒有嗎？請參閱[疑難排解](app-insights-troubleshoot-faq.md)。*</span><span class="sxs-lookup"><span data-stu-id="a6577-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="a6577-154">hello 瀏覽器刀鋒視窗是[計量瀏覽器刀鋒視窗](app-insights-metrics-explorer.md)預設篩選器與圖表選項。</span><span class="sxs-lookup"><span data-stu-id="a6577-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="a6577-155">如果您想要並儲存為我的最愛的 hello 結果，您可以編輯 hello 時間範圍、 篩選和圖表組態。</span><span class="sxs-lookup"><span data-stu-id="a6577-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="a6577-156">按一下**還原成預設值**tooget 後 toohello 原始刀鋒視窗中設定。</span><span class="sxs-lookup"><span data-stu-id="a6577-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="a6577-157">頁面載入效能</span><span class="sxs-lookup"><span data-stu-id="a6577-157">Page load performance</span></span>
<span data-ttu-id="a6577-158">在 hello top 將不分割的頁面載入時間圖表。</span><span class="sxs-lookup"><span data-stu-id="a6577-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="a6577-159">hello 總 hello 圖表高度表示從您的應用程式使用者的瀏覽器中的 hello 的平均時間 tooload 和顯示頁面。</span><span class="sxs-lookup"><span data-stu-id="a6577-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="a6577-160">hello 時間的測量從 hello 瀏覽器傳送 hello 初始 HTTP 要求，直到所有同步已處理的事件，包括版面配置和執行指令碼的負載。</span><span class="sxs-lookup"><span data-stu-id="a6577-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="a6577-161">不包含例如從 AJAX 呼叫載入 Web 組件的非同步工作。</span><span class="sxs-lookup"><span data-stu-id="a6577-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="a6577-162">hello 圖表 hello 總頁面載入時間分成 hello [W3C 所定義的標準時間](http://www.w3.org/TR/navigation-timing/#processing-model)。</span><span class="sxs-lookup"><span data-stu-id="a6577-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="a6577-163">請注意該 hello*網路連接*時間通常是比您所料，因為它是從 hello 瀏覽器 toohello 伺服器的所有要求的平均值。</span><span class="sxs-lookup"><span data-stu-id="a6577-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="a6577-164">許多個別的要求有連接時間為 0，因為已經有使用中連接 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a6577-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="a6577-165">載入緩慢？</span><span class="sxs-lookup"><span data-stu-id="a6577-165">Slow loading?</span></span>
<span data-ttu-id="a6577-166">頁面載入緩慢是您的使用者不滿的主要來源。</span><span class="sxs-lookup"><span data-stu-id="a6577-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="a6577-167">如果 hello 圖表表示慢速網頁載入時，很容易 toodo 一些診斷研究。</span><span class="sxs-lookup"><span data-stu-id="a6577-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="a6577-168">hello 圖表可顯示應用程式中的所有載入頁面的 hello 平均值。</span><span class="sxs-lookup"><span data-stu-id="a6577-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="a6577-169">toosee 如果 hello 問題侷 tooparticular 頁面，進一步向下 hello 刀鋒視窗的外觀，其中有是區隔的方格頁面 URL:</span><span class="sxs-lookup"><span data-stu-id="a6577-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="a6577-170">請注意 hello 頁面檢視計數和標準差。</span><span class="sxs-lookup"><span data-stu-id="a6577-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="a6577-171">如果非常低 hello 頁面計數，然後 hello 問題不會影響使用者很多。</span><span class="sxs-lookup"><span data-stu-id="a6577-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="a6577-172">高標準差 （比較 toohello 平均本身），表示大量的個別度量之間的變化。</span><span class="sxs-lookup"><span data-stu-id="a6577-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="a6577-173">**放大某個 URL 和整頁檢視。**</span><span class="sxs-lookup"><span data-stu-id="a6577-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="a6577-174">按一下任何頁面名稱 toosee 刀鋒視窗中的瀏覽器圖表篩選只 toothat URL;然後執行個體上的頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="a6577-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="a6577-175">按一下`...`的事件屬性的完整清單，或檢查 hello Ajax 呼叫和相關的事件。</span><span class="sxs-lookup"><span data-stu-id="a6577-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="a6577-176">速度較慢的 Ajax 呼叫影響 hello 整體頁面載入時間，如果不同步。</span><span class="sxs-lookup"><span data-stu-id="a6577-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="a6577-177">相關的事件包括 hello 的伺服器要求相同的 URL （如果您已設定 web 伺服器上的 Application Insights）。</span><span class="sxs-lookup"><span data-stu-id="a6577-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="a6577-178">**經過一段時間的網頁效能。**</span><span class="sxs-lookup"><span data-stu-id="a6577-178">**Page performance over time.**</span></span> <span data-ttu-id="a6577-179">回在 hello 瀏覽器刀鋒視窗中，變更 hello 網頁檢視載入時間格線行圖表 toosee 在特定時間尖峰一樣：</span><span class="sxs-lookup"><span data-stu-id="a6577-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![按一下 hello hello 方格標頭，然後選取新的圖表類型](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="a6577-181">**依據其他維度來分段。**</span><span class="sxs-lookup"><span data-stu-id="a6577-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="a6577-182">或許您的網頁會慢 tooload 上特定瀏覽器、 用戶端作業系統或使用者的位置？</span><span class="sxs-lookup"><span data-stu-id="a6577-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="a6577-183">將新的圖表和試驗 hello **Group by**維度。</span><span class="sxs-lookup"><span data-stu-id="a6577-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="a6577-184">AJAX 效能</span><span class="sxs-lookup"><span data-stu-id="a6577-184">AJAX Performance</span></span>
<span data-ttu-id="a6577-185">請確定您的網頁中的任何 AJAX 呼叫執行狀況良好。</span><span class="sxs-lookup"><span data-stu-id="a6577-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="a6577-186">這些通常是頁面的您使用的 toofill 部分以非同步的方式。</span><span class="sxs-lookup"><span data-stu-id="a6577-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="a6577-187">Hello 整體頁面可能會載入迅速，雖然您的使用者可能被搖頭由盯著空白 web 組件，等候中的資料 tooappear。</span><span class="sxs-lookup"><span data-stu-id="a6577-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="a6577-188">AJAX 呼叫從您網頁會顯示 hello 瀏覽器刀鋒視窗上，做為相依性。</span><span class="sxs-lookup"><span data-stu-id="a6577-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="a6577-189">有 hello 的 hello 刀鋒視窗的上半部中的摘要圖表：</span><span class="sxs-lookup"><span data-stu-id="a6577-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="a6577-190">在下方有詳細方格：</span><span class="sxs-lookup"><span data-stu-id="a6577-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="a6577-191">按一下任何資料列以取得特定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a6577-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="a6577-192">如果您刪除 hello hello 刀鋒視窗上的瀏覽器篩選時，伺服器和 AJAX 相依性會包含在這些圖表中。</span><span class="sxs-lookup"><span data-stu-id="a6577-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="a6577-193">按一下 還原成預設值 tooreconfigure hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="a6577-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="a6577-194">**執行失敗的 Ajax 呼叫 toodrill**向 toohello 相依性失敗方格中，捲動，然後按一下資料列的 toosee 特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="a6577-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="a6577-195">按一下`...`Ajax 呼叫 hello 完整遙測。</span><span class="sxs-lookup"><span data-stu-id="a6577-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="a6577-196">未報告任何 Ajax 呼叫？</span><span class="sxs-lookup"><span data-stu-id="a6577-196">No Ajax calls reported?</span></span>
<span data-ttu-id="a6577-197">Ajax 呼叫包含從您網頁的 hello 指令碼進行的任何 HTTP/HTTPS 呼叫。</span><span class="sxs-lookup"><span data-stu-id="a6577-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="a6577-198">如果您沒有看到這些報告，請檢查該 hello 程式碼片段不會設定 hello`disableAjaxTracking`或`maxAjaxCallsPerView`[參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)。</span><span class="sxs-lookup"><span data-stu-id="a6577-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="a6577-199">瀏覽器例外狀況</span><span class="sxs-lookup"><span data-stu-id="a6577-199">Browser exceptions</span></span>
<span data-ttu-id="a6577-200">在 hello 瀏覽器刀鋒視窗中，沒有例外狀況的摘要圖表，以及一個例外狀況類型的進一步向下 hello 刀鋒視窗中的方格。</span><span class="sxs-lookup"><span data-stu-id="a6577-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="a6577-201">如果看不到瀏覽器例外狀況的報告，請檢查該 hello 程式碼片段不會設定 hello `disableExceptionTracking` [參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)。</span><span class="sxs-lookup"><span data-stu-id="a6577-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="a6577-202">檢查個別的頁面檢視事件</span><span class="sxs-lookup"><span data-stu-id="a6577-202">Inspect individual page view events</span></span>

<span data-ttu-id="a6577-203">頁面檢視遙測資料一般是由 Application Insights 進行分析，而您只會看見以所有使用者為單位平均計算的累積報告。</span><span class="sxs-lookup"><span data-stu-id="a6577-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="a6577-204">然而在偵錯時，您也可以查看個別的頁面檢視事件。</span><span class="sxs-lookup"><span data-stu-id="a6577-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="a6577-205">在 hello 診斷搜尋刀鋒視窗中，設定篩選 tooPage 檢視。</span><span class="sxs-lookup"><span data-stu-id="a6577-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="a6577-206">選取任何事件 toosee 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a6577-206">Select any event toosee more detail.</span></span> <span data-ttu-id="a6577-207">在 [hello 詳細資料] 頁面上，按一下"…"toosee 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a6577-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="a6577-208">如果您使用[搜尋](app-insights-diagnostic-search.md)，通知您有全字拼寫須相符 toomatch: 「 關於 」 和 「 記載"不符合 「 關於 」。</span><span class="sxs-lookup"><span data-stu-id="a6577-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="a6577-209">您也可以使用 hello 強大[記錄分析查詢語言](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table)toosearch 頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="a6577-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="a6577-210">頁面檢視屬性</span><span class="sxs-lookup"><span data-stu-id="a6577-210">Page view properties</span></span>
* <span data-ttu-id="a6577-211">**頁面檢視持續時間**</span><span class="sxs-lookup"><span data-stu-id="a6577-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="a6577-212">根據預設，hello 次採用 tooload hello 頁面上，從用戶端要求 toofull 負載 （包括但不包括非同步工作，例如 Ajax 呼叫的輔助檔案）。</span><span class="sxs-lookup"><span data-stu-id="a6577-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="a6577-213">如果您設定`overridePageViewDuration`在 hello[頁面設定](#detailed-configuration)，第一次 hello hello 的用戶端要求 tooexecution 間隔`trackPageView`。</span><span class="sxs-lookup"><span data-stu-id="a6577-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="a6577-214">如果您可以從其一般位置移動 trackPageView hello 初始化 hello 指令碼之後，它會反映不同的值。</span><span class="sxs-lookup"><span data-stu-id="a6577-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="a6577-215">如果`overridePageViewDuration`組和持續時間在 hello 提供引數則是`trackPageView()`呼叫，則會改為使用 hello 引數值。</span><span class="sxs-lookup"><span data-stu-id="a6577-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="a6577-216">自訂頁面計數</span><span class="sxs-lookup"><span data-stu-id="a6577-216">Custom page counts</span></span>
<span data-ttu-id="a6577-217">根據預設，頁面計數，就會發生每個新的頁面載入 hello 用戶端瀏覽器的時間。</span><span class="sxs-lookup"><span data-stu-id="a6577-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="a6577-218">但是，您可能想 toocount 額外的頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="a6577-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="a6577-219">例如，頁面可能會顯示其內容索引標籤中，且想 toocount 頁面時 hello 使用者切換索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a6577-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="a6577-220">或 hello 頁面中的 JavaScript 程式碼可能會載入新的內容，而不需要變更 hello 瀏覽器的 URL。</span><span class="sxs-lookup"><span data-stu-id="a6577-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="a6577-221">Hello 適當點，用戶端程式碼中插入 JavaScript 呼叫像這樣：</span><span class="sxs-lookup"><span data-stu-id="a6577-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="a6577-222">hello 頁面名稱只能包含的 hello 相同字元做為 URL，但任何項目之後"#"或"？"會被忽略。</span><span class="sxs-lookup"><span data-stu-id="a6577-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="a6577-223">使用情況追蹤</span><span class="sxs-lookup"><span data-stu-id="a6577-223">Usage tracking</span></span>
<span data-ttu-id="a6577-224">想出您的使用者利用您的應用程式執行 toofind 嗎？</span><span class="sxs-lookup"><span data-stu-id="a6577-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="a6577-225">深入了解使用情況追蹤</span><span class="sxs-lookup"><span data-stu-id="a6577-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="a6577-226">[深入了解自訂事件和計量 API](app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="a6577-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="a6577-227"><a name="video"></a> 影片</span><span class="sxs-lookup"><span data-stu-id="a6577-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="a6577-228"><a name="next"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6577-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="a6577-229">追蹤流量</span><span class="sxs-lookup"><span data-stu-id="a6577-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="a6577-230">自訂事件和計量</span><span class="sxs-lookup"><span data-stu-id="a6577-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="a6577-231">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="a6577-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

