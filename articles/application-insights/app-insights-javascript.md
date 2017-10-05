---
title: "JavaScript Web App 適用的 Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="b9a22-104">適用於網頁的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="b9a22-104">Application Insights for web pages</span></span>
<span data-ttu-id="b9a22-105">了解您的網頁或應用程式的效能和使用量。</span><span class="sxs-lookup"><span data-stu-id="b9a22-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="b9a22-106">如果將 [Application Insights](app-insights-overview.md) 新增至頁面指令碼，您會取得頁面載入的時間和 AJAX 呼叫、計數和瀏覽器例外狀況與 AJAX 失敗的詳細資料，以及使用者和工作階段計數。</span><span class="sxs-lookup"><span data-stu-id="b9a22-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="b9a22-107">這些項目可以依據頁面、用戶端作業系統和瀏覽器版本、地區位置和其他維度分割。</span><span class="sxs-lookup"><span data-stu-id="b9a22-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="b9a22-108">您可以對失敗計數或緩慢頁面載入設定警示。</span><span class="sxs-lookup"><span data-stu-id="b9a22-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="b9a22-109">而在 JavaScript 程式碼中插入追蹤呼叫，即可追蹤網頁應用程式的各種功能使用方式。</span><span class="sxs-lookup"><span data-stu-id="b9a22-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="b9a22-110">Application Insights 可以使用於任何網頁 - 您剛剛新增 JavaScript 的簡短片段。</span><span class="sxs-lookup"><span data-stu-id="b9a22-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="b9a22-111">如果您的 Web 服務是 [Java](app-insights-java-get-started.md) 或 [ASP.NET](app-insights-asp-net.md)，您可以整合來自您的伺服器和用戶端的遙測。</span><span class="sxs-lookup"><span data-stu-id="b9a22-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![在 portal.azure.com 中，開啟您的應用程式資源，然後按一下 [瀏覽器]](./media/app-insights-javascript/03.png)

<span data-ttu-id="b9a22-113">您需要 [Microsoft Azure](https://azure.com)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9a22-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="b9a22-114">如果您的小組擁有組織訂用帳戶，請洽詢擁有者將您的 Microsoft 帳戶新增至其中。</span><span class="sxs-lookup"><span data-stu-id="b9a22-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="b9a22-115">開發和小規模的使用不需要任何成本。</span><span class="sxs-lookup"><span data-stu-id="b9a22-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="b9a22-116">為您的網頁設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="b9a22-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="b9a22-117">將載入器程式碼片段新增至您的網頁，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b9a22-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="b9a22-118">開啟或建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="b9a22-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="b9a22-119">Application Insights 資源是您的頁面的效能和使用量相關資料顯示的位置。</span><span class="sxs-lookup"><span data-stu-id="b9a22-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="b9a22-120">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b9a22-121">如果您已經設定好應用程式伺服器端的監視，您已經擁有資源：</span><span class="sxs-lookup"><span data-stu-id="b9a22-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![選擇 [瀏覽]、[開發人員服務]、[Application Insights]。](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="b9a22-123">如果您沒有資源，請建立資源：</span><span class="sxs-lookup"><span data-stu-id="b9a22-123">If you don't have one, create it:</span></span>

![選擇 [新增]、[開發人員服務]、[Application Insights]。](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="b9a22-125">*已經有問題了嗎？*</span><span class="sxs-lookup"><span data-stu-id="b9a22-125">*Questions already?*</span></span> <span data-ttu-id="b9a22-126">[建立資源的詳細資訊](app-insights-create-new-resource.md)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9a22-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="b9a22-127">將 SDK 指令碼加入至您的應用程式或網頁</span><span class="sxs-lookup"><span data-stu-id="b9a22-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="b9a22-128">在快速入門中，取得網頁指令碼：</span><span class="sxs-lookup"><span data-stu-id="b9a22-128">In Quick Start, get the script for web pages:</span></span>

![在您的應用程式概觀刀鋒視窗中，選擇 [快速入門]，取得程式碼以監視我的網頁。](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="b9a22-131">在您想要追蹤的每一頁的 `</head>` 標記之前插入指令碼。如果您的網站有主版頁面，您可以那裡放入指令碼。</span><span class="sxs-lookup"><span data-stu-id="b9a22-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="b9a22-132">例如：</span><span class="sxs-lookup"><span data-stu-id="b9a22-132">For example:</span></span>

* <span data-ttu-id="b9a22-133">在 ASP.NET MVC 專案中，可放在 `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="b9a22-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="b9a22-134">在 SharePoint 網站中，在控制台中開啟 [站台設定/主要頁面](app-insights-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="b9a22-135">指令碼包含檢測金鑰，會將資料導向您的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="b9a22-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="b9a22-136">([進一步說明指令碼。](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="b9a22-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="b9a22-137">*(如果您使用的是已知網頁架構，請在 Application Insights 配接器附近尋找。例如，有 [AngularJS 模組](http://ngmodules.org/modules/angular-appinsights)。)*</span><span class="sxs-lookup"><span data-stu-id="b9a22-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="b9a22-138">詳細組態</span><span class="sxs-lookup"><span data-stu-id="b9a22-138">Detailed configuration</span></span>
<span data-ttu-id="b9a22-139">您可以設定數種 [參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) ，但是在大部分情況下，您應該不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="b9a22-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="b9a22-140">例如，您可以停用或限制每個頁面檢視報告的 Ajax 呼叫的數目 (以減少流量)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="b9a22-141">或者您可以設定偵錯模式，讓遙測透過管線迅速移動而不需要批次處理。</span><span class="sxs-lookup"><span data-stu-id="b9a22-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="b9a22-142">若要設定這些參數，在程式碼片段中尋找這一行，並在後面加入多個以逗號分隔的項目：</span><span class="sxs-lookup"><span data-stu-id="b9a22-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="b9a22-143">[可用參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) 包括：</span><span class="sxs-lookup"><span data-stu-id="b9a22-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="b9a22-144"><a name="run"></a>執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b9a22-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="b9a22-145">執行您的 Web 應用程式，稍微使用一下來產生遙測，並等候數秒鐘。</span><span class="sxs-lookup"><span data-stu-id="b9a22-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="b9a22-146">您可以在開發電腦上使用 **F5** 執行應用程式，或發佈應用程式讓使用者處理。</span><span class="sxs-lookup"><span data-stu-id="b9a22-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="b9a22-147">如果您想要檢查 Web 應用程式傳送至 Application Insights 的遙測，請使用您瀏覽器的偵錯工具 (在許多瀏覽器上為**F12** )。</span><span class="sxs-lookup"><span data-stu-id="b9a22-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="b9a22-148">資料會傳送至 dc.services.visualstudio.com。</span><span class="sxs-lookup"><span data-stu-id="b9a22-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="b9a22-149">探索瀏覽器效能資料</span><span class="sxs-lookup"><span data-stu-id="b9a22-149">Explore your browser performance data</span></span>
<span data-ttu-id="b9a22-150">開啟 [瀏覽器] 刀鋒視窗，以顯示使用者瀏覽器的彙總效能資料。</span><span class="sxs-lookup"><span data-stu-id="b9a22-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![在 portal.azure.com 中，開啟您的應用程式資源然後按一下 [設定]、[瀏覽器]。](./media/app-insights-javascript/03.png)

<span data-ttu-id="b9a22-152">*仍沒有資料？按一下頁面頂端的 [重新整理]。仍然沒有嗎？請參閱[疑難排解](app-insights-troubleshoot-faq.md)。*</span><span class="sxs-lookup"><span data-stu-id="b9a22-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="b9a22-153">[瀏覽器] 刀鋒視窗是[計量瀏覽器刀鋒視窗](app-insights-metrics-explorer.md)，具有預設篩選器與圖表選項。</span><span class="sxs-lookup"><span data-stu-id="b9a22-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="b9a22-154">如果您想要的話，可以編輯時間範圍、篩選器和圖表設定，並將結果儲存為我的最愛。</span><span class="sxs-lookup"><span data-stu-id="b9a22-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="b9a22-155">按一下 [還原預設值]  以返回原始刀鋒視窗設定。</span><span class="sxs-lookup"><span data-stu-id="b9a22-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="b9a22-156">頁面載入效能</span><span class="sxs-lookup"><span data-stu-id="b9a22-156">Page load performance</span></span>
<span data-ttu-id="b9a22-157">最上層是頁面載入時間的分段圖表。</span><span class="sxs-lookup"><span data-stu-id="b9a22-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="b9a22-158">圖表高度總計表示從您的應用程式載入頁面並且在您的使用者瀏覽器中顯示頁面的平均時間。</span><span class="sxs-lookup"><span data-stu-id="b9a22-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="b9a22-159">時間是從瀏覽器傳送初始 HTTP 要求開始測量，直到已經處理所有同步載入事件，包括版面配置和執行中指令碼。</span><span class="sxs-lookup"><span data-stu-id="b9a22-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="b9a22-160">不包含例如從 AJAX 呼叫載入 Web 組件的非同步工作。</span><span class="sxs-lookup"><span data-stu-id="b9a22-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="b9a22-161">圖表會將總頁面載入時間分段為 [W3C 所定義的標準時間](http://www.w3.org/TR/navigation-timing/#processing-model)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="b9a22-162">請注意，「網路連接」  時間通常低於您所預期的時間，因為它是從瀏覽器到伺服器之所有要求的平均值。</span><span class="sxs-lookup"><span data-stu-id="b9a22-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="b9a22-163">許多個別要求的連接時間為 0，因為已經有與伺服器的作用中連線。</span><span class="sxs-lookup"><span data-stu-id="b9a22-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="b9a22-164">載入緩慢？</span><span class="sxs-lookup"><span data-stu-id="b9a22-164">Slow loading?</span></span>
<span data-ttu-id="b9a22-165">頁面載入緩慢是您的使用者不滿的主要來源。</span><span class="sxs-lookup"><span data-stu-id="b9a22-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="b9a22-166">如果圖表指出頁面載入緩慢，很容易就能執行某些診斷研究。</span><span class="sxs-lookup"><span data-stu-id="b9a22-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="b9a22-167">圖表會顯示您的應用程式中所有頁面載入的平均時間。</span><span class="sxs-lookup"><span data-stu-id="b9a22-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="b9a22-168">若要查看問題是否僅限於特定頁面，請進一步查看刀鋒視窗，其中有依據網頁 URL 分段的方格：</span><span class="sxs-lookup"><span data-stu-id="b9a22-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="b9a22-169">請注意頁面檢視計數和標準差。</span><span class="sxs-lookup"><span data-stu-id="b9a22-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="b9a22-170">如果頁面計數非常低，則問題不太會影響使用者。</span><span class="sxs-lookup"><span data-stu-id="b9a22-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="b9a22-171">高的標準差 (相當於平均值本身) 表示個別測量之間的變化。</span><span class="sxs-lookup"><span data-stu-id="b9a22-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="b9a22-172">**放大某個 URL 和整頁檢視。**</span><span class="sxs-lookup"><span data-stu-id="b9a22-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="b9a22-173">按一下任何頁面名稱，即可查看針對該 URL 篩選的瀏覽器圖表的刀鋒視窗，接著是網頁檢視的執行個體。</span><span class="sxs-lookup"><span data-stu-id="b9a22-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="b9a22-174">按一下 `...` 以取得該事件之屬性的完整清單，或檢查 Ajax 呼叫和相關的事件。</span><span class="sxs-lookup"><span data-stu-id="b9a22-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="b9a22-175">如果它們是同步的，緩慢的 Ajax 呼叫會影響整體頁面載入時間。</span><span class="sxs-lookup"><span data-stu-id="b9a22-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="b9a22-176">相關的事件包含伺服器要求相同的 URL (如果您已在 Web 伺服器上設定 Application Insights)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="b9a22-177">**經過一段時間的網頁效能。**</span><span class="sxs-lookup"><span data-stu-id="b9a22-177">**Page performance over time.**</span></span> <span data-ttu-id="b9a22-178">回到 [瀏覽器] 刀鋒視窗，將 [頁面檢視載入時間] 方格變更為折線圖，以查看在特定時間是否有尖峰：</span><span class="sxs-lookup"><span data-stu-id="b9a22-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![按一下方格的標頭，然後選取新的圖表類型](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="b9a22-180">**依據其他維度來分段。**</span><span class="sxs-lookup"><span data-stu-id="b9a22-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="b9a22-181">或許您的網頁在特定瀏覽器、用戶端作業系統或使用者位置載入時較緩慢？</span><span class="sxs-lookup"><span data-stu-id="b9a22-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="b9a22-182">加入具有 **Group-by** 維度的圖表和實驗。</span><span class="sxs-lookup"><span data-stu-id="b9a22-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="b9a22-183">AJAX 效能</span><span class="sxs-lookup"><span data-stu-id="b9a22-183">AJAX Performance</span></span>
<span data-ttu-id="b9a22-184">請確定您的網頁中的任何 AJAX 呼叫執行狀況良好。</span><span class="sxs-lookup"><span data-stu-id="b9a22-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="b9a22-185">它們通常是用來以非同步方式填入網頁的組件。</span><span class="sxs-lookup"><span data-stu-id="b9a22-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="b9a22-186">雖然可能會立即載入整個網頁，您的使用者可能會對於盯著空白網頁組件，等候其中的資料出現感到挫折。</span><span class="sxs-lookup"><span data-stu-id="b9a22-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="b9a22-187">從您的網頁進行的 AJAX 呼叫會顯示在 [瀏覽器] 刀鋒視窗中做為相依項目。</span><span class="sxs-lookup"><span data-stu-id="b9a22-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="b9a22-188">在刀鋒視窗的上方有摘要圖表：</span><span class="sxs-lookup"><span data-stu-id="b9a22-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="b9a22-189">在下方有詳細方格：</span><span class="sxs-lookup"><span data-stu-id="b9a22-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="b9a22-190">按一下任何資料列以取得特定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b9a22-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="b9a22-191">如果您刪除刀鋒視窗上的 [瀏覽器] 篩選器，伺服器和 AJAX 相依項目會包含在這些圖表中。</span><span class="sxs-lookup"><span data-stu-id="b9a22-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="b9a22-192">按一下 [還原預設值] 以重新設定篩選器。</span><span class="sxs-lookup"><span data-stu-id="b9a22-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="b9a22-193">**若要深入失敗的 Ajax 呼叫** ，請向下捲動至 [相依性失敗] 方格，然後按一下資料列以查看特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="b9a22-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="b9a22-194">按一下 `...` 以取得 Ajax 呼叫的完整遙測。</span><span class="sxs-lookup"><span data-stu-id="b9a22-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="b9a22-195">未報告任何 Ajax 呼叫？</span><span class="sxs-lookup"><span data-stu-id="b9a22-195">No Ajax calls reported?</span></span>
<span data-ttu-id="b9a22-196">Ajax 呼叫包含從您的網頁指令碼所做的任何 HTTP/HTTPS 呼叫。</span><span class="sxs-lookup"><span data-stu-id="b9a22-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="b9a22-197">如果您沒有看到這些報告，請檢查程式碼片段未設定 `disableAjaxTracking` 或 `maxAjaxCallsPerView` [參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="b9a22-198">瀏覽器例外狀況</span><span class="sxs-lookup"><span data-stu-id="b9a22-198">Browser exceptions</span></span>
<span data-ttu-id="b9a22-199">在 [瀏覽器] 刀鋒視窗上，有例外狀況摘要圖表，進一步的刀鋒視窗中有例外狀況類型的方格。</span><span class="sxs-lookup"><span data-stu-id="b9a22-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="b9a22-200">如果您沒有看到報告的瀏覽器例外狀況，請檢查程式碼片段未設定 `disableExceptionTracking` [參數](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="b9a22-201">檢查個別的頁面檢視事件</span><span class="sxs-lookup"><span data-stu-id="b9a22-201">Inspect individual page view events</span></span>

<span data-ttu-id="b9a22-202">頁面檢視遙測資料一般是由 Application Insights 進行分析，而您只會看見以所有使用者為單位平均計算的累積報告。</span><span class="sxs-lookup"><span data-stu-id="b9a22-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="b9a22-203">然而在偵錯時，您也可以查看個別的頁面檢視事件。</span><span class="sxs-lookup"><span data-stu-id="b9a22-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="b9a22-204">在 [Diagnostic Search] 分頁中，將 [篩選器] 設定為 [網頁檢視]。</span><span class="sxs-lookup"><span data-stu-id="b9a22-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="b9a22-205">選取任一事件以查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b9a22-205">Select any event to see more detail.</span></span> <span data-ttu-id="b9a22-206">在詳細資料頁面中，按一下 "..." 來查看更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b9a22-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="b9a22-207">如果您使用 [搜尋](app-insights-diagnostic-search.md)，請注意，您必須比對完整字詞："Abou" 和 "bout" 與 "About" 不相符。</span><span class="sxs-lookup"><span data-stu-id="b9a22-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="b9a22-208">您也可以使用功能強大的 [Log Analytics 查詢語言](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table)來搜尋頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="b9a22-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="b9a22-209">頁面檢視屬性</span><span class="sxs-lookup"><span data-stu-id="b9a22-209">Page view properties</span></span>
* <span data-ttu-id="b9a22-210">**頁面檢視持續時間**</span><span class="sxs-lookup"><span data-stu-id="b9a22-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="b9a22-211">根據預設，載入頁面所花費的時間，從用戶端要求到完整載入 (包括輔助檔案，但不包括非同步工作，例如 Ajax 呼叫)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="b9a22-212">如果您在[頁面設定](#detailed-configuration)中設定 `overridePageViewDuration`，則為用戶端要求到執行第一個 `trackPageView` 之間的間隔。</span><span class="sxs-lookup"><span data-stu-id="b9a22-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="b9a22-213">如果您在指令碼的初始設定之後將 trackPageView 從一般位置移走，它會反映不同的值。</span><span class="sxs-lookup"><span data-stu-id="b9a22-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="b9a22-214">如果設定了 `overridePageViewDuration`，且 `trackPageView()` 呼叫中有提供持續時間引數，則會改為使用引數值。</span><span class="sxs-lookup"><span data-stu-id="b9a22-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="b9a22-215">自訂頁面計數</span><span class="sxs-lookup"><span data-stu-id="b9a22-215">Custom page counts</span></span>
<span data-ttu-id="b9a22-216">依預設，每當用戶端瀏覽器載入新頁面時，頁面計數便會發生。</span><span class="sxs-lookup"><span data-stu-id="b9a22-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="b9a22-217">不過您也許會想要計算其他頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="b9a22-217">But you might want to count additional page views.</span></span> <span data-ttu-id="b9a22-218">例如，由於頁面可能會將內容顯示在索引標籤中，因此您想要在使用者切換索引標籤時計算一次頁面。</span><span class="sxs-lookup"><span data-stu-id="b9a22-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="b9a22-219">抑或是頁面中的 JavaScript 程式碼可能會在未變更瀏覽器 URL 的情況下載入新內容。</span><span class="sxs-lookup"><span data-stu-id="b9a22-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="b9a22-220">請將與以下範例相似的 JavaScript 呼叫插入用戶端程式碼中的適當位置：</span><span class="sxs-lookup"><span data-stu-id="b9a22-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="b9a22-221">頁面名稱可能會含有與 URL 相同的字元，不過 "#" 或 "?" 之後的任何字元都會遭到忽略。</span><span class="sxs-lookup"><span data-stu-id="b9a22-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="b9a22-222">使用情況追蹤</span><span class="sxs-lookup"><span data-stu-id="b9a22-222">Usage tracking</span></span>
<span data-ttu-id="b9a22-223">想要了解使用者如何使用您的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="b9a22-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="b9a22-224">深入了解使用情況追蹤</span><span class="sxs-lookup"><span data-stu-id="b9a22-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="b9a22-225">[深入了解自訂事件和計量 API](app-insights-api-custom-events-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="b9a22-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="b9a22-226"><a name="video"></a> 影片</span><span class="sxs-lookup"><span data-stu-id="b9a22-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="b9a22-227"><a name="next"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9a22-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="b9a22-228">追蹤流量</span><span class="sxs-lookup"><span data-stu-id="b9a22-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="b9a22-229">自訂事件和計量</span><span class="sxs-lookup"><span data-stu-id="b9a22-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="b9a22-230">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="b9a22-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

