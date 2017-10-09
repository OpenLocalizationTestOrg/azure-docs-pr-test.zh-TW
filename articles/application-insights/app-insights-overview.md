---
title: "aaa Azure Application Insights 是什麼？ | Microsoft Docs"
description: "即時 Web 應用程式的應用程式效能管理和使用量追蹤。  偵測、分級和診斷問題，了解人們如何使用您的應用程式。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 379721d1-0f82-445a-b416-45b94cb969ec
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/14/2017
ms.author: bwren
ms.openlocfilehash: d2596f53a36991fcd08551e6395ece68a5801e39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-insights"></a><span data-ttu-id="701b1-105">什麼是 Application Insights？</span><span class="sxs-lookup"><span data-stu-id="701b1-105">What is Application Insights?</span></span>
<span data-ttu-id="701b1-106">Application Insights 是多個平台上的 Web 開發人員所適用的可延伸「應用程式效能管理」(APM) 服務。</span><span class="sxs-lookup"><span data-stu-id="701b1-106">Application Insights is an extensible Application Performance Management (APM) service for web developers on multiple platforms.</span></span> <span data-ttu-id="701b1-107">它使用 toomonitor 即時 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="701b1-107">Use it toomonitor your live web application.</span></span> <span data-ttu-id="701b1-108">它將會自動偵測效能異常。</span><span class="sxs-lookup"><span data-stu-id="701b1-108">It will automatically detect performance anomalies.</span></span> <span data-ttu-id="701b1-109">它包括強大的分析工具 toohelp 您診斷問題和 toounderstand 哪些使用者實際執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="701b1-109">It includes powerful analytics tools toohelp you diagnose issues and toounderstand what users actually do with your app.</span></span>  <span data-ttu-id="701b1-110">其設計目的是 toohelp 持續改善效能和可用性。</span><span class="sxs-lookup"><span data-stu-id="701b1-110">It's designed toohelp you continuously improve  performance and usability.</span></span> <span data-ttu-id="701b1-111">這也適用於應用程式上各種不同的平台包括.NET、 Node.js 和 J2EE，裝載在內部部署或 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="701b1-111">It works for apps on a wide variety of platforms including .NET, Node.js and J2EE, hosted on-premises or in hello cloud.</span></span> <span data-ttu-id="701b1-112">它與您的 devOps 程序整合，並已連線點 tooa 各種不同的開發工具。</span><span class="sxs-lookup"><span data-stu-id="701b1-112">It  integrates with your devOps process, and has connection points tooa variety of development tools.</span></span>

![製作使用者活動統計資料的圖表，或深入特定事件。](./media/app-insights-overview/00-sample.png)

<span data-ttu-id="701b1-114">[看看 hello 簡介動畫](https://www.youtube.com/watch?v=fX2NtGrh-Y0)。</span><span class="sxs-lookup"><span data-stu-id="701b1-114">[Take a look at hello intro animation](https://www.youtube.com/watch?v=fX2NtGrh-Y0).</span></span>

## <a name="how-does-application-insights-work"></a><span data-ttu-id="701b1-115">Application Insights 的運作方式</span><span class="sxs-lookup"><span data-stu-id="701b1-115">How does Application Insights work?</span></span>
<span data-ttu-id="701b1-116">您安裝應用程式中的小型檢測封裝，並設定好 hello Microsoft Azure 入口網站中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="701b1-116">You install a small instrumentation package in your application, and set up an Application Insights resource in hello Microsoft Azure portal.</span></span> <span data-ttu-id="701b1-117">hello 檢測監視您的應用程式，並傳送遙測資料 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="701b1-117">hello instrumentation monitors your app and sends telemetry data toohello portal.</span></span> <span data-ttu-id="701b1-118">（hello 應用程式可以執行任何位置-沒有 toobe Azure 中裝載）。</span><span class="sxs-lookup"><span data-stu-id="701b1-118">(hello application can run anywhere - it doesn't have toobe hosted in Azure.)</span></span>

<span data-ttu-id="701b1-119">您可以檢測不僅 hello web 服務應用程式，而且還要有任何背景元件，並 hello 本身 hello web 網頁中的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="701b1-119">You can instrument not only hello web service application, but also any background components, and hello JavaScript in hello web pages themselves.</span></span> 

![在您的應用程式中的應用程式 Insights 檢測會傳送遙測 tooyour Application Insights 資源。](./media/app-insights-overview/01-scheme.png)


<span data-ttu-id="701b1-121">此外，您可以提取遙測的 hello 主機環境，例如效能計數器、 Azure 診斷或 Docker 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="701b1-121">In addition, you can pull in telemetry from hello host environments such as performance counters, Azure diagnostics, or Docker logs.</span></span> <span data-ttu-id="701b1-122">您也可以設定定期傳送綜合要求 tooyour web 服務的 web 測試。</span><span class="sxs-lookup"><span data-stu-id="701b1-122">You can also set up web tests that periodically send synthetic requests tooyour web service.</span></span>

<span data-ttu-id="701b1-123">所有這些遙測資料流中經過整合 hello Azure 入口網站，可以套用強大分析與搜尋工具 toohello 未經處理資料。</span><span class="sxs-lookup"><span data-stu-id="701b1-123">All these telemetry streams are integrated in hello Azure portal, where you can apply powerful analytic and search tools toohello raw data.</span></span>


### <a name="whats-hello-overhead"></a><span data-ttu-id="701b1-124">Hello 負擔是什麼？</span><span class="sxs-lookup"><span data-stu-id="701b1-124">What's hello overhead?</span></span>
<span data-ttu-id="701b1-125">hello 對您的應用程式效能影響會很小。</span><span class="sxs-lookup"><span data-stu-id="701b1-125">hello impact on your app's performance is very small.</span></span> <span data-ttu-id="701b1-126">追蹤呼叫非封鎖性，而且會在個別的執行緒中分批傳送。</span><span class="sxs-lookup"><span data-stu-id="701b1-126">Tracking calls are non-blocking, and are batched and sent in a separate thread.</span></span>

## <a name="what-does-application-insights-monitor"></a><span data-ttu-id="701b1-127">Application Insights 可監視什麼？</span><span class="sxs-lookup"><span data-stu-id="701b1-127">What does Application Insights monitor?</span></span>

<span data-ttu-id="701b1-128">Application Insights 旨在 hello 開發團隊，toohelp 您了解如何執行您的應用程式，以及如何被使用。</span><span class="sxs-lookup"><span data-stu-id="701b1-128">Application Insights is aimed at hello development team, toohelp you understand how your app is performing and how it's being used.</span></span> <span data-ttu-id="701b1-129">它可監視︰</span><span class="sxs-lookup"><span data-stu-id="701b1-129">It monitors:</span></span>

* <span data-ttu-id="701b1-130">**要求率、回應時間和失敗率** - 找出哪些頁面在每天哪些時段最受歡迎，以及使用者位於何處。</span><span class="sxs-lookup"><span data-stu-id="701b1-130">**Request rates, response times, and failure rates** - Find out which pages are most popular, at what times of day, and where your users are.</span></span> <span data-ttu-id="701b1-131">查看哪些頁面的表現最好。</span><span class="sxs-lookup"><span data-stu-id="701b1-131">See which pages perform best.</span></span> <span data-ttu-id="701b1-132">如果您的回應時間和失敗率隨著要求增加而提高，您或許有資源配置問題。</span><span class="sxs-lookup"><span data-stu-id="701b1-132">If your response times and failure rates go high when there are more requests, then perhaps you have a resourcing problem.</span></span> 
* <span data-ttu-id="701b1-133">**相依比率、回應時間和失敗率** - 找出外部服務是否會使您降低效能。</span><span class="sxs-lookup"><span data-stu-id="701b1-133">**Dependency rates, response times, and failure rates** - Find out whether external services are slowing you down.</span></span>
* <span data-ttu-id="701b1-134">**例外狀況**-分析 hello 彙總統計資料，或選擇特定執行個體和下鑽研至 hello 堆疊追蹤和相關的要求。</span><span class="sxs-lookup"><span data-stu-id="701b1-134">**Exceptions** - Analyse hello aggregated statistics, or pick specific instances and drill into hello stack trace and related requests.</span></span> <span data-ttu-id="701b1-135">伺服器和瀏覽器例外狀況都會報告。</span><span class="sxs-lookup"><span data-stu-id="701b1-135">Both server and browser exceptions are reported.</span></span>
* <span data-ttu-id="701b1-136">**頁面檢視和載入效能** - 由使用者的瀏覽器報告。</span><span class="sxs-lookup"><span data-stu-id="701b1-136">**Page views and load performance** - reported by your users' browsers.</span></span>
* <span data-ttu-id="701b1-137">來自網頁的 **AJAX 呼叫** - 比率、回應時間和失敗率。</span><span class="sxs-lookup"><span data-stu-id="701b1-137">**AJAX calls** from web pages - rates, response times, and failure rates.</span></span>
* <span data-ttu-id="701b1-138">**使用者和工作階段計數**。</span><span class="sxs-lookup"><span data-stu-id="701b1-138">**User and session counts**.</span></span>
* <span data-ttu-id="701b1-139">Windows 或 Linux 伺服器電腦中的**效能計數器**，例如 CPU、記憶體和網路使用量。</span><span class="sxs-lookup"><span data-stu-id="701b1-139">**Performance counters** from your Windows or Linux server machines, such as CPU, memory, and network usage.</span></span> 
* <span data-ttu-id="701b1-140">來自 Docker 或 Azure 的**主機診斷**。</span><span class="sxs-lookup"><span data-stu-id="701b1-140">**Host diagnostics** from Docker or Azure.</span></span> 
* <span data-ttu-id="701b1-141">來自您應用程式的**診斷追蹤記錄檔** - 讓您使追蹤事件與要求相互關聯。</span><span class="sxs-lookup"><span data-stu-id="701b1-141">**Diagnostic trace logs** from your app - so that you can correlate trace events with requests.</span></span>
* <span data-ttu-id="701b1-142">**自訂事件和度量**，您自行撰寫 hello 用戶端或伺服器程式碼中，tootrack 商務事件，例如項目已售出或遊戲成交。</span><span class="sxs-lookup"><span data-stu-id="701b1-142">**Custom events and metrics** that you write yourself in hello client or server code, tootrack business events such as items sold or games won.</span></span>

## <a name="where-do-i-see-my-telemetry"></a><span data-ttu-id="701b1-143">哪裡可以查看我的遙測？</span><span class="sxs-lookup"><span data-stu-id="701b1-143">Where do I see my telemetry?</span></span>

<span data-ttu-id="701b1-144">有許多方式 tooexplore 您的資料。</span><span class="sxs-lookup"><span data-stu-id="701b1-144">There are plenty of ways tooexplore your data.</span></span> <span data-ttu-id="701b1-145">請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="701b1-145">Check out these articles:</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="701b1-146">**智慧型偵測和手動警示**</span><span class="sxs-lookup"><span data-stu-id="701b1-146">**Smart detection and manual alerts**</span></span>](app-insights-proactive-diagnostics.md)<br/><span data-ttu-id="701b1-147">警示自動調整 tooyour 應用程式的遙測和觸發程序的一般模式有任務在身時外 hello 一般模式。</span><span class="sxs-lookup"><span data-stu-id="701b1-147">Automatic alerts adapt tooyour app's normal patterns of telemetry and trigger when there's something outside hello usual pattern.</span></span> <span data-ttu-id="701b1-148">您也可以在自訂或標準計量的特定層級上[設定警示](app-insights-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="701b1-148">You can also [set alerts](app-insights-alerts.md) on particular levels of custom or standard metrics.</span></span> |![警示範例](./media/app-insights-overview/alerts-tn.png) |
| [<span data-ttu-id="701b1-150">**應用程式對應**</span><span class="sxs-lookup"><span data-stu-id="701b1-150">**Application map**</span></span>](app-insights-app-map.md)<br/><span data-ttu-id="701b1-151">您的應用程式，警示的關鍵計量與 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="701b1-151">hello components of your app, with key metrics and alerts.</span></span> |![應用程式對應](./media/app-insights-overview/appmap-tn.png)  |
| [<span data-ttu-id="701b1-153">**分析工具**</span><span class="sxs-lookup"><span data-stu-id="701b1-153">**Profiler**</span></span>](app-insights-profiler.md)<br/><span data-ttu-id="701b1-154">檢查 hello 執行設定檔的取樣的要求。</span><span class="sxs-lookup"><span data-stu-id="701b1-154">Inspect hello execution profiles of sampled requests.</span></span> |![分析工具](./media/app-insights-overview/profiler.png) |
| [<span data-ttu-id="701b1-156">**使用量分析**</span><span class="sxs-lookup"><span data-stu-id="701b1-156">**Usage analysis**</span></span>](app-insights-usage-overview.md)<br/><span data-ttu-id="701b1-157">分析使用者區隔和保留期。</span><span class="sxs-lookup"><span data-stu-id="701b1-157">Analyze user segmentation and retention.</span></span>|![保留期工具](./media/app-insights-overview/retention.png) |
| [<span data-ttu-id="701b1-159">**執行個體資料的診斷搜尋**</span><span class="sxs-lookup"><span data-stu-id="701b1-159">**Diagnostic search for instance data**</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="701b1-160">搜尋和篩選事件，例如要求、例外狀況、相依性呼叫、記錄追蹤，以及頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="701b1-160">Search and filter events such as requests, exceptions, dependency calls, log traces, and page views.</span></span>  |![搜尋遙測](./media/app-insights-overview/search-tn.png) |
| [<span data-ttu-id="701b1-162">**彙總資料的計量瀏覽器**</span><span class="sxs-lookup"><span data-stu-id="701b1-162">**Metrics Explorer for aggregated data**</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="701b1-163">瀏覽、篩選和分割彙總的資料，例如，要求、錯誤和例外狀況的比率；回應時間、頁面載入時間。</span><span class="sxs-lookup"><span data-stu-id="701b1-163">Explore, filter, and segment aggregated data such as rates of requests, failures, and exceptions; response times, page load times.</span></span> |![度量](./media/app-insights-overview/metrics-tn.png) |
| [<span data-ttu-id="701b1-165">**儀表板**</span><span class="sxs-lookup"><span data-stu-id="701b1-165">**Dashboards**</span></span>](app-insights-dashboards.md#dashboards)<br/><span data-ttu-id="701b1-166">來自多個資源的交互式資料並與其他人員共用。</span><span class="sxs-lookup"><span data-stu-id="701b1-166">Mash up data from multiple resources and share with others.</span></span> <span data-ttu-id="701b1-167">多元件的應用程式，然後連續顯示 hello 小組室中很棒。</span><span class="sxs-lookup"><span data-stu-id="701b1-167">Great for multi-component applications, and for continuous display in hello team room.</span></span> |![儀表板範例](./media/app-insights-overview/dashboard-tn.png) |
| [<span data-ttu-id="701b1-169">**即時計量串流**</span><span class="sxs-lookup"><span data-stu-id="701b1-169">**Live Metrics Stream**</span></span>](app-insights-live-stream.md)<br/><span data-ttu-id="701b1-170">當您部署新組建時，觀賞這些接近即時的效能指標 toomake 確定一切如預期運作。</span><span class="sxs-lookup"><span data-stu-id="701b1-170">When you deploy a new build, watch these near-real-time performance indicators toomake sure everything works as expected.</span></span> |![即時計量範例](./media/app-insights-overview/live-metrics-tn.png) |
| [<span data-ttu-id="701b1-172">**分析**</span><span class="sxs-lookup"><span data-stu-id="701b1-172">**Analytics**</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="701b1-173">使用這個功能強大的查詢語言，回答有關您應用程式效能和使用方式的艱難問題。</span><span class="sxs-lookup"><span data-stu-id="701b1-173">Answer tough questions about your app's performance and usage by using this powerful query language.</span></span> |![分析範例](./media/app-insights-overview/analytics-tn.png) |
| [<span data-ttu-id="701b1-175">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="701b1-175">**Visual Studio**</span></span>](app-insights-visual-studio.md)<br/><span data-ttu-id="701b1-176">請參閱 hello 程式碼中的效能資料。</span><span class="sxs-lookup"><span data-stu-id="701b1-176">See performance data in hello code.</span></span> <span data-ttu-id="701b1-177">移 toocode 從堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="701b1-177">Go toocode from stack traces.</span></span>|![Visual Studio](./media/app-insights-overview/visual-studio-tn.png) |
| [<span data-ttu-id="701b1-179">**快照集偵錯工具**</span><span class="sxs-lookup"><span data-stu-id="701b1-179">**Snapshot debugger**</span></span>](app-insights-snapshot-debugger.md)<br/><span data-ttu-id="701b1-180">使用參數值，對取樣自即時作業的快照集進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="701b1-180">Debug snapshots sampled from live operations, with parameter values.</span></span>|![Visual Studio](./media/app-insights-overview/snapshot.png) |
| [<span data-ttu-id="701b1-182">**Power BI**</span><span class="sxs-lookup"><span data-stu-id="701b1-182">**Power BI**</span></span>](app-insights-export-power-bi.md)<br/><span data-ttu-id="701b1-183">整合使用量計量和其他商業智慧。</span><span class="sxs-lookup"><span data-stu-id="701b1-183">Integrate usage metrics with other business intelligence.</span></span>| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [<span data-ttu-id="701b1-185">**REST API**</span><span class="sxs-lookup"><span data-stu-id="701b1-185">**REST API**</span></span>](https://dev.applicationinsights.io/)<br/><span data-ttu-id="701b1-186">撰寫程式碼 toorun 查詢透過您的度量和原始資料。</span><span class="sxs-lookup"><span data-stu-id="701b1-186">Write code toorun queries over your metrics and raw data.</span></span>| ![REST API](./media/app-insights-overview/rest-tn.png) |
| [<span data-ttu-id="701b1-188">**連續匯出**</span><span class="sxs-lookup"><span data-stu-id="701b1-188">**Continuous export**</span></span>](app-insights-export-telemetry.md)<br/><span data-ttu-id="701b1-189">到達時，大量匯出的未經處理資料 toostorage。</span><span class="sxs-lookup"><span data-stu-id="701b1-189">Bulk export of raw data toostorage as soon as it arrives.</span></span> |![匯出](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a><span data-ttu-id="701b1-191">如何使用 Application Insights？</span><span class="sxs-lookup"><span data-stu-id="701b1-191">How do I use Application Insights?</span></span>

### <a name="monitor"></a><span data-ttu-id="701b1-192">監視</span><span class="sxs-lookup"><span data-stu-id="701b1-192">Monitor</span></span>
<span data-ttu-id="701b1-193">在應用程式中安裝 Application Insights、設定[可用性 Web 測試](app-insights-monitor-web-app-availability.md)，以及︰</span><span class="sxs-lookup"><span data-stu-id="701b1-193">Install Application Insights in your app, set up [availability web tests](app-insights-monitor-web-app-availability.md), and:</span></span>

* <span data-ttu-id="701b1-194">設定[儀表板](app-insights-dashboards.md)載入、 回應性，與 hello 效能的程式相依性，您小組室 tookeep，頁面載入和 AJAX 呼叫。</span><span class="sxs-lookup"><span data-stu-id="701b1-194">Set up a [dashboard](app-insights-dashboards.md) for your team room tookeep an eye on load, responsiveness, and hello performance of your dependencies, page loads, and AJAX calls.</span></span>
* <span data-ttu-id="701b1-195">探索哪些是最慢的 hello 和大部分的失敗要求。</span><span class="sxs-lookup"><span data-stu-id="701b1-195">Discover which are hello slowest and most failing requests.</span></span>
* <span data-ttu-id="701b1-196">監看式[即時資料流](app-insights-live-stream.md)當您部署新的版本，tooknow 立即有關任何降低的情形。</span><span class="sxs-lookup"><span data-stu-id="701b1-196">Watch [Live Stream](app-insights-live-stream.md) when you deploy a new release, tooknow immediately about any degradation.</span></span>

### <a name="detect-diagnose"></a><span data-ttu-id="701b1-197">偵測、診斷</span><span class="sxs-lookup"><span data-stu-id="701b1-197">Detect, Diagnose</span></span>
<span data-ttu-id="701b1-198">當您收到警示或發現問題︰</span><span class="sxs-lookup"><span data-stu-id="701b1-198">When you receive an alert or discover a problem:</span></span>

* <span data-ttu-id="701b1-199">評估有多少使用者受到影響。</span><span class="sxs-lookup"><span data-stu-id="701b1-199">Assess how many users are affected.</span></span>
* <span data-ttu-id="701b1-200">將失敗與例外狀況、相依項目呼叫和追蹤相互關聯。</span><span class="sxs-lookup"><span data-stu-id="701b1-200">Correlate failures with exceptions, dependency calls and traces.</span></span>
* <span data-ttu-id="701b1-201">檢查分析工具、快照集、堆疊傾印和追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="701b1-201">Examine profiler, snapshots, stack dumps, and trace logs.</span></span>

### <a name="build-measure-learn"></a><span data-ttu-id="701b1-202">建置、測量、學習</span><span class="sxs-lookup"><span data-stu-id="701b1-202">Build, Measure, Learn</span></span>
<span data-ttu-id="701b1-203">[測量 hello 效能](app-insights-usage-overview.md)的每個您所部署的新功能。</span><span class="sxs-lookup"><span data-stu-id="701b1-203">[Measure hello effectiveness](app-insights-usage-overview.md) of each new feature that you deploy.</span></span>

* <span data-ttu-id="701b1-204">計劃 toomeasure 客戶如何使用新的 UX 或商務功能。</span><span class="sxs-lookup"><span data-stu-id="701b1-204">Plan toomeasure how customers use new UX or business features.</span></span>
* <span data-ttu-id="701b1-205">在程式碼中撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="701b1-205">Write custom telemetry into your code.</span></span>
* <span data-ttu-id="701b1-206">從您的遙測基底 hello 下一個開發循環上硬碟的辨識項。</span><span class="sxs-lookup"><span data-stu-id="701b1-206">Base hello next development cycle on hard evidence from your telemetry.</span></span>

## <a name="get-started"></a><span data-ttu-id="701b1-207">開始使用</span><span class="sxs-lookup"><span data-stu-id="701b1-207">Get started</span></span>
<span data-ttu-id="701b1-208">Application Insights 是 hello 的裝載於 Microsoft Azure 和遙測中的許多服務有傳送進行分析及簡報。</span><span class="sxs-lookup"><span data-stu-id="701b1-208">Application Insights is one of hello many services hosted within Microsoft Azure, and telemetry is sent there for analysis and presentation.</span></span> <span data-ttu-id="701b1-209">讓您執行其他動作之前，您需要訂用帳戶太[Microsoft Azure](http://azure.com)。</span><span class="sxs-lookup"><span data-stu-id="701b1-209">So before you do anything else, you'll need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="701b1-210">免費 toosign，而且如果您選擇 hello 基本[定價方案](https://azure.microsoft.com/pricing/details/application-insights/)的 Application Insights 是免費直到您的應用程式變得 toohave 大量使用。</span><span class="sxs-lookup"><span data-stu-id="701b1-210">It's free toosign up, and if you choose hello basic [pricing plan](https://azure.microsoft.com/pricing/details/application-insights/) of Application Insights, there's no charge until your application has grown toohave substantial usage.</span></span> <span data-ttu-id="701b1-211">如果您的組織已有訂用帳戶，他們可以加入您的 Microsoft 帳戶 tooit。</span><span class="sxs-lookup"><span data-stu-id="701b1-211">If your organization already has a subscription, they could add your Microsoft account tooit.</span></span>

<span data-ttu-id="701b1-212">有數種方式啟動 tooget。</span><span class="sxs-lookup"><span data-stu-id="701b1-212">There are several ways tooget started.</span></span> <span data-ttu-id="701b1-213">從最適合您的方式著手。</span><span class="sxs-lookup"><span data-stu-id="701b1-213">Begin with whichever works best for you.</span></span> <span data-ttu-id="701b1-214">您可以加入稍後 hello 其他人。</span><span class="sxs-lookup"><span data-stu-id="701b1-214">You can add hello others later.</span></span>

* <span data-ttu-id="701b1-215">**在執行階段： 檢測 hello 伺服器上的 web 應用程式。**</span><span class="sxs-lookup"><span data-stu-id="701b1-215">**At run time: instrument your web app on hello server.**</span></span> <span data-ttu-id="701b1-216">可避免任何更新 toohello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="701b1-216">Avoids any update toohello code.</span></span> <span data-ttu-id="701b1-217">您需要系統管理員存取 tooyour 伺服器。</span><span class="sxs-lookup"><span data-stu-id="701b1-217">You need admin access tooyour server.</span></span>
  * [<span data-ttu-id="701b1-218">**內部部署或 VM 上的 IIS**</span><span class="sxs-lookup"><span data-stu-id="701b1-218">**IIS on-premises or on a VM**</span></span>](app-insights-monitor-performance-live-website-now.md)
  * [<span data-ttu-id="701b1-219">**Azure Web 應用程式或 VM**</span><span class="sxs-lookup"><span data-stu-id="701b1-219">**Azure web app or VM**</span></span>](app-insights-monitor-performance-live-website-now.md)
  * [<span data-ttu-id="701b1-220">**J2EE**</span><span class="sxs-lookup"><span data-stu-id="701b1-220">**J2EE**</span></span>](app-insights-java-live.md)
* <span data-ttu-id="701b1-221">**在開發階段： 加入 Application Insights tooyour 程式碼。**</span><span class="sxs-lookup"><span data-stu-id="701b1-221">**At development time: add Application Insights tooyour code.**</span></span> <span data-ttu-id="701b1-222">可讓您 toowrite 自訂遙測和 tooinstrument 後端及桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="701b1-222">Allows you toowrite custom telemetry and tooinstrument back-end and desktop apps.</span></span>
  * <span data-ttu-id="701b1-223">[Visual Studio](app-insights-asp-net.md) 2013 Update 2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="701b1-223">[Visual Studio](app-insights-asp-net.md) 2013 update 2 or later.</span></span>
  * <span data-ttu-id="701b1-224">[Eclipse](app-insights-java-eclipse.md) 或 [其他工具](app-insights-java-get-started.md) 中的 Java</span><span class="sxs-lookup"><span data-stu-id="701b1-224">Java in [Eclipse](app-insights-java-eclipse.md) or [other tools](app-insights-java-get-started.md)</span></span>
  * [<span data-ttu-id="701b1-225">Node.js</span><span class="sxs-lookup"><span data-stu-id="701b1-225">Node.js</span></span>](app-insights-nodejs.md)
  * [<span data-ttu-id="701b1-226">其他平台</span><span class="sxs-lookup"><span data-stu-id="701b1-226">Other platforms</span></span>](app-insights-platforms.md)
* <span data-ttu-id="701b1-227">**[檢測您的網頁](app-insights-javascript.md)**的頁面檢視、AJAX 和其他用戶端遙測。</span><span class="sxs-lookup"><span data-stu-id="701b1-227">**[Instrument your web pages](app-insights-javascript.md)** for page view, AJAX and other client-side telemetry.</span></span>
* <span data-ttu-id="701b1-228">**[可用性集合](app-insights-monitor-web-app-availability.md)** - 定期從我們的伺服器 ping 您的網站。</span><span class="sxs-lookup"><span data-stu-id="701b1-228">**[Availability tests](app-insights-monitor-web-app-availability.md)** - ping your website regularly from our servers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="701b1-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="701b1-229">Next steps</span></span>
<span data-ttu-id="701b1-230">在執行階段開始使用︰</span><span class="sxs-lookup"><span data-stu-id="701b1-230">Get started at runtime with:</span></span>

* [<span data-ttu-id="701b1-231">IIS 伺服器</span><span class="sxs-lookup"><span data-stu-id="701b1-231">IIS server</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="701b1-232">J2EE 伺服器</span><span class="sxs-lookup"><span data-stu-id="701b1-232">J2EE server</span></span>](app-insights-java-live.md)

<span data-ttu-id="701b1-233">在開發階段開始使用︰</span><span class="sxs-lookup"><span data-stu-id="701b1-233">Get started at development time with:</span></span>

* [<span data-ttu-id="701b1-234">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="701b1-234">ASP.NET</span></span>](app-insights-asp-net.md)
* [<span data-ttu-id="701b1-235">Java</span><span class="sxs-lookup"><span data-stu-id="701b1-235">Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="701b1-236">Node.js</span><span class="sxs-lookup"><span data-stu-id="701b1-236">Node.js</span></span>](app-insights-nodejs.md)

## <a name="support-and-feedback"></a><span data-ttu-id="701b1-237">支援與意見反應</span><span class="sxs-lookup"><span data-stu-id="701b1-237">Support and feedback</span></span>
* <span data-ttu-id="701b1-238">疑難排解與問題：</span><span class="sxs-lookup"><span data-stu-id="701b1-238">Questions and Issues:</span></span>
  * <span data-ttu-id="701b1-239">[疑難排解][qna]</span><span class="sxs-lookup"><span data-stu-id="701b1-239">[Troubleshooting][qna]</span></span>
  * [<span data-ttu-id="701b1-240">MSDN 論壇</span><span class="sxs-lookup"><span data-stu-id="701b1-240">MSDN Forum</span></span>](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [<span data-ttu-id="701b1-241">StackOverflow</span><span class="sxs-lookup"><span data-stu-id="701b1-241">StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)
* <span data-ttu-id="701b1-242">您的建議：</span><span class="sxs-lookup"><span data-stu-id="701b1-242">Your suggestions:</span></span>
  * [<span data-ttu-id="701b1-243">UserVoice</span><span class="sxs-lookup"><span data-stu-id="701b1-243">UserVoice</span></span>](https://visualstudio.uservoice.com/forums/357324)
* <span data-ttu-id="701b1-244">部落格：</span><span class="sxs-lookup"><span data-stu-id="701b1-244">Blog:</span></span>
  * [<span data-ttu-id="701b1-245">Application Insights 部落格</span><span class="sxs-lookup"><span data-stu-id="701b1-245">Application Insights blog</span></span>](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a><span data-ttu-id="701b1-246">影片</span><span class="sxs-lookup"><span data-stu-id="701b1-246">Videos</span></span>

<span data-ttu-id="701b1-247">[![動畫簡介](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)</span><span class="sxs-lookup"><span data-stu-id="701b1-247">[![Animated introduction](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

<!--Link references-->

[android]: https://github.com/Microsoft/ApplicationInsights-Android
[azure]: ../insights-perf-analytics.md
[client]: app-insights-javascript.md
[desktop]: app-insights-windows-desktop.md
[detect]: app-insights-detect-triage-diagnose.md
[greenbrown]: app-insights-asp-net.md
[ios]: https://github.com/Microsoft/ApplicationInsights-iOS
[java]: app-insights-java-get-started.md
[knowUsers]: app-insights-web-track-usage.md
[platforms]: app-insights-platforms.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
