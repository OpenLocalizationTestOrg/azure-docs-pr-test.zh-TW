---
title: "什麼是 Azure Application Insights？ | Microsoft Docs"
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
ms.openlocfilehash: 4b863f7421488a76aab60729286b48b65055d8f4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-application-insights"></a><span data-ttu-id="d2daf-105">什麼是 Application Insights？</span><span class="sxs-lookup"><span data-stu-id="d2daf-105">What is Application Insights?</span></span>
<span data-ttu-id="d2daf-106">Application Insights 是多個平台上的 Web 開發人員所適用的可延伸「應用程式效能管理」(APM) 服務。</span><span class="sxs-lookup"><span data-stu-id="d2daf-106">Application Insights is an extensible Application Performance Management (APM) service for web developers on multiple platforms.</span></span> <span data-ttu-id="d2daf-107">您可以使用它來監視即時 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2daf-107">Use it to monitor your live web application.</span></span> <span data-ttu-id="d2daf-108">它將會自動偵測效能異常。</span><span class="sxs-lookup"><span data-stu-id="d2daf-108">It will automatically detect performance anomalies.</span></span> <span data-ttu-id="d2daf-109">其中包括強大的分析工具可協助您診斷問題，並了解使用者實際如何運用您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2daf-109">It includes powerful analytics tools to help you diagnose issues and to understand what users actually do with your app.</span></span>  <span data-ttu-id="d2daf-110">它是設計來協助您持續改善效能和可用性。</span><span class="sxs-lookup"><span data-stu-id="d2daf-110">It's designed to help you continuously improve  performance and usability.</span></span> <span data-ttu-id="d2daf-111">它適用於各種不同平台上的應用程式，包括裝載在內部部署或雲端的 .NET、Node.js 和 J2EE。</span><span class="sxs-lookup"><span data-stu-id="d2daf-111">It works for apps on a wide variety of platforms including .NET, Node.js and J2EE, hosted on-premises or in the cloud.</span></span> <span data-ttu-id="d2daf-112">它可與您的 devOps 程序整合，並有與各種開發工具的連接點。</span><span class="sxs-lookup"><span data-stu-id="d2daf-112">It  integrates with your devOps process, and has connection points to a variety of development tools.</span></span>

![製作使用者活動統計資料的圖表，或深入特定事件。](./media/app-insights-overview/00-sample.png)

<span data-ttu-id="d2daf-114">[看一下簡介動畫](https://www.youtube.com/watch?v=fX2NtGrh-Y0)。</span><span class="sxs-lookup"><span data-stu-id="d2daf-114">[Take a look at the intro animation](https://www.youtube.com/watch?v=fX2NtGrh-Y0).</span></span>

## <a name="how-does-application-insights-work"></a><span data-ttu-id="d2daf-115">Application Insights 的運作方式</span><span class="sxs-lookup"><span data-stu-id="d2daf-115">How does Application Insights work?</span></span>
<span data-ttu-id="d2daf-116">您會在應用程式中安裝小型檢測套件，並且在 Microsoft Azure 入口網站中設定 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="d2daf-116">You install a small instrumentation package in your application, and set up an Application Insights resource in the Microsoft Azure portal.</span></span> <span data-ttu-id="d2daf-117">此檢測套件會監視您的應用程式，並將遙測資料傳送至入口網站。</span><span class="sxs-lookup"><span data-stu-id="d2daf-117">The instrumentation monitors your app and sends telemetry data to the portal.</span></span> <span data-ttu-id="d2daf-118">(應用程式可以在任何地方執行 - 不一定要裝載於 Azure 中。)</span><span class="sxs-lookup"><span data-stu-id="d2daf-118">(The application can run anywhere - it doesn't have to be hosted in Azure.)</span></span>

<span data-ttu-id="d2daf-119">您不僅可以檢測 Web 服務應用程式，也可以檢測任何背景元件以及網頁本身中的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="d2daf-119">You can instrument not only the web service application, but also any background components, and the JavaScript in the web pages themselves.</span></span> 

![您應用程式中的 Application Insights 檢測功能會將遙測傳送到 Application Insights 資源。](./media/app-insights-overview/01-scheme.png)


<span data-ttu-id="d2daf-121">此外，您可以從主機環境 (例如效能計數器、Azure 診斷或 Docker 記錄) 提取遙測資料。</span><span class="sxs-lookup"><span data-stu-id="d2daf-121">In addition, you can pull in telemetry from the host environments such as performance counters, Azure diagnostics, or Docker logs.</span></span> <span data-ttu-id="d2daf-122">您也可以設定會定期將綜合要求傳送至 Web 服務的 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="d2daf-122">You can also set up web tests that periodically send synthetic requests to your web service.</span></span>

<span data-ttu-id="d2daf-123">上述所有遙測串流都會整合於 Azure 入口網站中，您可在其中將強大的分析和搜尋工具套用於未經處理的資料。</span><span class="sxs-lookup"><span data-stu-id="d2daf-123">All these telemetry streams are integrated in the Azure portal, where you can apply powerful analytic and search tools to the raw data.</span></span>


### <a name="whats-the-overhead"></a><span data-ttu-id="d2daf-124">負荷為何？</span><span class="sxs-lookup"><span data-stu-id="d2daf-124">What's the overhead?</span></span>
<span data-ttu-id="d2daf-125">對您的應用程式效能的影響很小。</span><span class="sxs-lookup"><span data-stu-id="d2daf-125">The impact on your app's performance is very small.</span></span> <span data-ttu-id="d2daf-126">追蹤呼叫非封鎖性，而且會在個別的執行緒中分批傳送。</span><span class="sxs-lookup"><span data-stu-id="d2daf-126">Tracking calls are non-blocking, and are batched and sent in a separate thread.</span></span>

## <a name="what-does-application-insights-monitor"></a><span data-ttu-id="d2daf-127">Application Insights 可監視什麼？</span><span class="sxs-lookup"><span data-stu-id="d2daf-127">What does Application Insights monitor?</span></span>

<span data-ttu-id="d2daf-128">Application Insights 是以開發小組為目標，以協助您了解您的應用程式的執行和使用情況。</span><span class="sxs-lookup"><span data-stu-id="d2daf-128">Application Insights is aimed at the development team, to help you understand how your app is performing and how it's being used.</span></span> <span data-ttu-id="d2daf-129">它可監視︰</span><span class="sxs-lookup"><span data-stu-id="d2daf-129">It monitors:</span></span>

* <span data-ttu-id="d2daf-130">**要求率、回應時間和失敗率** - 找出哪些頁面在每天哪些時段最受歡迎，以及使用者位於何處。</span><span class="sxs-lookup"><span data-stu-id="d2daf-130">**Request rates, response times, and failure rates** - Find out which pages are most popular, at what times of day, and where your users are.</span></span> <span data-ttu-id="d2daf-131">查看哪些頁面的表現最好。</span><span class="sxs-lookup"><span data-stu-id="d2daf-131">See which pages perform best.</span></span> <span data-ttu-id="d2daf-132">如果您的回應時間和失敗率隨著要求增加而提高，您或許有資源配置問題。</span><span class="sxs-lookup"><span data-stu-id="d2daf-132">If your response times and failure rates go high when there are more requests, then perhaps you have a resourcing problem.</span></span> 
* <span data-ttu-id="d2daf-133">**相依比率、回應時間和失敗率** - 找出外部服務是否會使您降低效能。</span><span class="sxs-lookup"><span data-stu-id="d2daf-133">**Dependency rates, response times, and failure rates** - Find out whether external services are slowing you down.</span></span>
* <span data-ttu-id="d2daf-134">**例外狀況** - 分析彙總統計資料，或挑選特定執行個體並深入了解堆疊追蹤和相關要求。</span><span class="sxs-lookup"><span data-stu-id="d2daf-134">**Exceptions** - Analyse the aggregated statistics, or pick specific instances and drill into the stack trace and related requests.</span></span> <span data-ttu-id="d2daf-135">伺服器和瀏覽器例外狀況都會報告。</span><span class="sxs-lookup"><span data-stu-id="d2daf-135">Both server and browser exceptions are reported.</span></span>
* <span data-ttu-id="d2daf-136">**頁面檢視和載入效能** - 由使用者的瀏覽器報告。</span><span class="sxs-lookup"><span data-stu-id="d2daf-136">**Page views and load performance** - reported by your users' browsers.</span></span>
* <span data-ttu-id="d2daf-137">來自網頁的 **AJAX 呼叫** - 比率、回應時間和失敗率。</span><span class="sxs-lookup"><span data-stu-id="d2daf-137">**AJAX calls** from web pages - rates, response times, and failure rates.</span></span>
* <span data-ttu-id="d2daf-138">**使用者和工作階段計數**。</span><span class="sxs-lookup"><span data-stu-id="d2daf-138">**User and session counts**.</span></span>
* <span data-ttu-id="d2daf-139">Windows 或 Linux 伺服器電腦中的**效能計數器**，例如 CPU、記憶體和網路使用量。</span><span class="sxs-lookup"><span data-stu-id="d2daf-139">**Performance counters** from your Windows or Linux server machines, such as CPU, memory, and network usage.</span></span> 
* <span data-ttu-id="d2daf-140">來自 Docker 或 Azure 的**主機診斷**。</span><span class="sxs-lookup"><span data-stu-id="d2daf-140">**Host diagnostics** from Docker or Azure.</span></span> 
* <span data-ttu-id="d2daf-141">來自您應用程式的**診斷追蹤記錄檔** - 讓您使追蹤事件與要求相互關聯。</span><span class="sxs-lookup"><span data-stu-id="d2daf-141">**Diagnostic trace logs** from your app - so that you can correlate trace events with requests.</span></span>
* <span data-ttu-id="d2daf-142">您在用戶端或伺服器程式碼中自行撰寫的**自訂事件和計量**，可追蹤商業事件，例如售出的項目或獲勝的遊戲。</span><span class="sxs-lookup"><span data-stu-id="d2daf-142">**Custom events and metrics** that you write yourself in the client or server code, to track business events such as items sold or games won.</span></span>

## <a name="where-do-i-see-my-telemetry"></a><span data-ttu-id="d2daf-143">哪裡可以查看我的遙測？</span><span class="sxs-lookup"><span data-stu-id="d2daf-143">Where do I see my telemetry?</span></span>

<span data-ttu-id="d2daf-144">有許多方式可以探索您的資料。</span><span class="sxs-lookup"><span data-stu-id="d2daf-144">There are plenty of ways to explore your data.</span></span> <span data-ttu-id="d2daf-145">請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="d2daf-145">Check out these articles:</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="d2daf-146">**智慧型偵測和手動警示**</span><span class="sxs-lookup"><span data-stu-id="d2daf-146">**Smart detection and manual alerts**</span></span>](app-insights-proactive-diagnostics.md)<br/><span data-ttu-id="d2daf-147">如果在常見模式之外發生一些狀況，則自動警示會適應您應用程式的一般遙測和觸發程式模式。</span><span class="sxs-lookup"><span data-stu-id="d2daf-147">Automatic alerts adapt to your app's normal patterns of telemetry and trigger when there's something outside the usual pattern.</span></span> <span data-ttu-id="d2daf-148">您也可以在自訂或標準計量的特定層級上[設定警示](app-insights-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="d2daf-148">You can also [set alerts](app-insights-alerts.md) on particular levels of custom or standard metrics.</span></span> |![警示範例](./media/app-insights-overview/alerts-tn.png) |
| [<span data-ttu-id="d2daf-150">**應用程式對應**</span><span class="sxs-lookup"><span data-stu-id="d2daf-150">**Application map**</span></span>](app-insights-app-map.md)<br/><span data-ttu-id="d2daf-151">應用程式的元件，包含重要計量和警示。</span><span class="sxs-lookup"><span data-stu-id="d2daf-151">The components of your app, with key metrics and alerts.</span></span> |![應用程式對應](./media/app-insights-overview/appmap-tn.png)  |
| [<span data-ttu-id="d2daf-153">**分析工具**</span><span class="sxs-lookup"><span data-stu-id="d2daf-153">**Profiler**</span></span>](app-insights-profiler.md)<br/><span data-ttu-id="d2daf-154">檢查取樣要求的執行設定檔。</span><span class="sxs-lookup"><span data-stu-id="d2daf-154">Inspect the execution profiles of sampled requests.</span></span> |![分析工具](./media/app-insights-overview/profiler.png) |
| [<span data-ttu-id="d2daf-156">**使用量分析**</span><span class="sxs-lookup"><span data-stu-id="d2daf-156">**Usage analysis**</span></span>](app-insights-usage-overview.md)<br/><span data-ttu-id="d2daf-157">分析使用者區隔和保留期。</span><span class="sxs-lookup"><span data-stu-id="d2daf-157">Analyze user segmentation and retention.</span></span>|![保留期工具](./media/app-insights-overview/retention.png) |
| [<span data-ttu-id="d2daf-159">**執行個體資料的診斷搜尋**</span><span class="sxs-lookup"><span data-stu-id="d2daf-159">**Diagnostic search for instance data**</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="d2daf-160">搜尋和篩選事件，例如要求、例外狀況、相依性呼叫、記錄追蹤，以及頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="d2daf-160">Search and filter events such as requests, exceptions, dependency calls, log traces, and page views.</span></span>  |![搜尋遙測](./media/app-insights-overview/search-tn.png) |
| [<span data-ttu-id="d2daf-162">**彙總資料的計量瀏覽器**</span><span class="sxs-lookup"><span data-stu-id="d2daf-162">**Metrics Explorer for aggregated data**</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="d2daf-163">瀏覽、篩選和分割彙總的資料，例如，要求、錯誤和例外狀況的比率；回應時間、頁面載入時間。</span><span class="sxs-lookup"><span data-stu-id="d2daf-163">Explore, filter, and segment aggregated data such as rates of requests, failures, and exceptions; response times, page load times.</span></span> |![度量](./media/app-insights-overview/metrics-tn.png) |
| [<span data-ttu-id="d2daf-165">**儀表板**</span><span class="sxs-lookup"><span data-stu-id="d2daf-165">**Dashboards**</span></span>](app-insights-dashboards.md#dashboards)<br/><span data-ttu-id="d2daf-166">來自多個資源的交互式資料並與其他人員共用。</span><span class="sxs-lookup"><span data-stu-id="d2daf-166">Mash up data from multiple resources and share with others.</span></span> <span data-ttu-id="d2daf-167">非常適用於多元件的應用程式，以及小組聊天室中的連續顯示。</span><span class="sxs-lookup"><span data-stu-id="d2daf-167">Great for multi-component applications, and for continuous display in the team room.</span></span> |![儀表板範例](./media/app-insights-overview/dashboard-tn.png) |
| [<span data-ttu-id="d2daf-169">**即時計量串流**</span><span class="sxs-lookup"><span data-stu-id="d2daf-169">**Live Metrics Stream**</span></span>](app-insights-live-stream.md)<br/><span data-ttu-id="d2daf-170">當您部署新的組建時，請觀看這些近乎即時的效能指標，以確定一切如預期運作。</span><span class="sxs-lookup"><span data-stu-id="d2daf-170">When you deploy a new build, watch these near-real-time performance indicators to make sure everything works as expected.</span></span> |![即時計量範例](./media/app-insights-overview/live-metrics-tn.png) |
| [<span data-ttu-id="d2daf-172">**分析**</span><span class="sxs-lookup"><span data-stu-id="d2daf-172">**Analytics**</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="d2daf-173">使用這個功能強大的查詢語言，回答有關您應用程式效能和使用方式的艱難問題。</span><span class="sxs-lookup"><span data-stu-id="d2daf-173">Answer tough questions about your app's performance and usage by using this powerful query language.</span></span> |![分析範例](./media/app-insights-overview/analytics-tn.png) |
| [<span data-ttu-id="d2daf-175">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="d2daf-175">**Visual Studio**</span></span>](app-insights-visual-studio.md)<br/><span data-ttu-id="d2daf-176">查看程式碼中的效能資料。</span><span class="sxs-lookup"><span data-stu-id="d2daf-176">See performance data in the code.</span></span> <span data-ttu-id="d2daf-177">從堆疊追蹤移至程式碼。</span><span class="sxs-lookup"><span data-stu-id="d2daf-177">Go to code from stack traces.</span></span>|![Visual Studio](./media/app-insights-overview/visual-studio-tn.png) |
| [<span data-ttu-id="d2daf-179">**快照集偵錯工具**</span><span class="sxs-lookup"><span data-stu-id="d2daf-179">**Snapshot debugger**</span></span>](app-insights-snapshot-debugger.md)<br/><span data-ttu-id="d2daf-180">使用參數值，對取樣自即時作業的快照集進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="d2daf-180">Debug snapshots sampled from live operations, with parameter values.</span></span>|![Visual Studio](./media/app-insights-overview/snapshot.png) |
| [<span data-ttu-id="d2daf-182">**Power BI**</span><span class="sxs-lookup"><span data-stu-id="d2daf-182">**Power BI**</span></span>](app-insights-export-power-bi.md)<br/><span data-ttu-id="d2daf-183">整合使用量計量和其他商業智慧。</span><span class="sxs-lookup"><span data-stu-id="d2daf-183">Integrate usage metrics with other business intelligence.</span></span>| ![Power BI](./media/app-insights-overview/power-bi.png)|
| [<span data-ttu-id="d2daf-185">**REST API**</span><span class="sxs-lookup"><span data-stu-id="d2daf-185">**REST API**</span></span>](https://dev.applicationinsights.io/)<br/><span data-ttu-id="d2daf-186">撰寫程式碼，對您的計量和未經處理資料執行查詢。</span><span class="sxs-lookup"><span data-stu-id="d2daf-186">Write code to run queries over your metrics and raw data.</span></span>| ![REST API](./media/app-insights-overview/rest-tn.png) |
| [<span data-ttu-id="d2daf-188">**連續匯出**</span><span class="sxs-lookup"><span data-stu-id="d2daf-188">**Continuous export**</span></span>](app-insights-export-telemetry.md)<br/><span data-ttu-id="d2daf-189">立即將送達的未經處理資料大量匯出至儲存體。</span><span class="sxs-lookup"><span data-stu-id="d2daf-189">Bulk export of raw data to storage as soon as it arrives.</span></span> |![匯出](./media/app-insights-overview/export-tn.png) |

## <a name="how-do-i-use-application-insights"></a><span data-ttu-id="d2daf-191">如何使用 Application Insights？</span><span class="sxs-lookup"><span data-stu-id="d2daf-191">How do I use Application Insights?</span></span>

### <a name="monitor"></a><span data-ttu-id="d2daf-192">監視</span><span class="sxs-lookup"><span data-stu-id="d2daf-192">Monitor</span></span>
<span data-ttu-id="d2daf-193">在應用程式中安裝 Application Insights、設定[可用性 Web 測試](app-insights-monitor-web-app-availability.md)，以及︰</span><span class="sxs-lookup"><span data-stu-id="d2daf-193">Install Application Insights in your app, set up [availability web tests](app-insights-monitor-web-app-availability.md), and:</span></span>

* <span data-ttu-id="d2daf-194">設定小組聊天室的[儀表板](app-insights-dashboards.md)，以持續關注相依項目、頁面載入和 AJAX 呼叫的載入、回應性和效能。</span><span class="sxs-lookup"><span data-stu-id="d2daf-194">Set up a [dashboard](app-insights-dashboards.md) for your team room to keep an eye on load, responsiveness, and the performance of your dependencies, page loads, and AJAX calls.</span></span>
* <span data-ttu-id="d2daf-195">探索哪些是最慢和最失敗的要求。</span><span class="sxs-lookup"><span data-stu-id="d2daf-195">Discover which are the slowest and most failing requests.</span></span>
* <span data-ttu-id="d2daf-196">在部署新版本時觀看[即時串流](app-insights-live-stream.md)，立即知曉任何效能降低情形。</span><span class="sxs-lookup"><span data-stu-id="d2daf-196">Watch [Live Stream](app-insights-live-stream.md) when you deploy a new release, to know immediately about any degradation.</span></span>

### <a name="detect-diagnose"></a><span data-ttu-id="d2daf-197">偵測、診斷</span><span class="sxs-lookup"><span data-stu-id="d2daf-197">Detect, Diagnose</span></span>
<span data-ttu-id="d2daf-198">當您收到警示或發現問題︰</span><span class="sxs-lookup"><span data-stu-id="d2daf-198">When you receive an alert or discover a problem:</span></span>

* <span data-ttu-id="d2daf-199">評估有多少使用者受到影響。</span><span class="sxs-lookup"><span data-stu-id="d2daf-199">Assess how many users are affected.</span></span>
* <span data-ttu-id="d2daf-200">將失敗與例外狀況、相依項目呼叫和追蹤相互關聯。</span><span class="sxs-lookup"><span data-stu-id="d2daf-200">Correlate failures with exceptions, dependency calls and traces.</span></span>
* <span data-ttu-id="d2daf-201">檢查分析工具、快照集、堆疊傾印和追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="d2daf-201">Examine profiler, snapshots, stack dumps, and trace logs.</span></span>

### <a name="build-measure-learn"></a><span data-ttu-id="d2daf-202">建置、測量、學習</span><span class="sxs-lookup"><span data-stu-id="d2daf-202">Build, Measure, Learn</span></span>
<span data-ttu-id="d2daf-203">[測量所部署之各個新功能的效果](app-insights-usage-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d2daf-203">[Measure the effectiveness](app-insights-usage-overview.md) of each new feature that you deploy.</span></span>

* <span data-ttu-id="d2daf-204">計劃測量客戶使用新 UX 或商務功能的情況。</span><span class="sxs-lookup"><span data-stu-id="d2daf-204">Plan to measure how customers use new UX or business features.</span></span>
* <span data-ttu-id="d2daf-205">在程式碼中撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="d2daf-205">Write custom telemetry into your code.</span></span>
* <span data-ttu-id="d2daf-206">讓下一個開發週期以遙測的真憑實據做為根據。</span><span class="sxs-lookup"><span data-stu-id="d2daf-206">Base the next development cycle on hard evidence from your telemetry.</span></span>

## <a name="get-started"></a><span data-ttu-id="d2daf-207">開始使用</span><span class="sxs-lookup"><span data-stu-id="d2daf-207">Get started</span></span>
<span data-ttu-id="d2daf-208">Application Insights 是 Microsoft Azure 中裝載的多項服務之一，而遙測資料會送至該處進行分析及呈現。</span><span class="sxs-lookup"><span data-stu-id="d2daf-208">Application Insights is one of the many services hosted within Microsoft Azure, and telemetry is sent there for analysis and presentation.</span></span> <span data-ttu-id="d2daf-209">所以在執行任何動作前，您需要 [Microsoft Azure](http://azure.com)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d2daf-209">So before you do anything else, you'll need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="d2daf-210">您可免費註冊，而且如果選擇 Application Insights 的基本[價格方案](https://azure.microsoft.com/pricing/details/application-insights/)，在您的應用程式成長到有大量使用量之前，不會有任何變更。</span><span class="sxs-lookup"><span data-stu-id="d2daf-210">It's free to sign up, and if you choose the basic [pricing plan](https://azure.microsoft.com/pricing/details/application-insights/) of Application Insights, there's no charge until your application has grown to have substantial usage.</span></span> <span data-ttu-id="d2daf-211">如果您的組織已經有訂用帳戶，他們可能會將您的 Microsoft 帳戶新增至其中。</span><span class="sxs-lookup"><span data-stu-id="d2daf-211">If your organization already has a subscription, they could add your Microsoft account to it.</span></span>

<span data-ttu-id="d2daf-212">有數種方式可以開始使用。</span><span class="sxs-lookup"><span data-stu-id="d2daf-212">There are several ways to get started.</span></span> <span data-ttu-id="d2daf-213">從最適合您的方式著手。</span><span class="sxs-lookup"><span data-stu-id="d2daf-213">Begin with whichever works best for you.</span></span> <span data-ttu-id="d2daf-214">您可以稍後新增其他帳戶。</span><span class="sxs-lookup"><span data-stu-id="d2daf-214">You can add the others later.</span></span>

* <span data-ttu-id="d2daf-215">**在執行階段：檢測伺服器上的 Web 應用程式。**</span><span class="sxs-lookup"><span data-stu-id="d2daf-215">**At run time: instrument your web app on the server.**</span></span> <span data-ttu-id="d2daf-216">避免對程式碼進行任何更新。</span><span class="sxs-lookup"><span data-stu-id="d2daf-216">Avoids any update to the code.</span></span> <span data-ttu-id="d2daf-217">您需要您的伺服器的系統管理員存取權。</span><span class="sxs-lookup"><span data-stu-id="d2daf-217">You need admin access to your server.</span></span>
  * [<span data-ttu-id="d2daf-218">**內部部署或 VM 上的 IIS**</span><span class="sxs-lookup"><span data-stu-id="d2daf-218">**IIS on-premises or on a VM**</span></span>](app-insights-monitor-performance-live-website-now.md)
  * [<span data-ttu-id="d2daf-219">**Azure Web 應用程式或 VM**</span><span class="sxs-lookup"><span data-stu-id="d2daf-219">**Azure web app or VM**</span></span>](app-insights-monitor-performance-live-website-now.md)
  * [<span data-ttu-id="d2daf-220">**J2EE**</span><span class="sxs-lookup"><span data-stu-id="d2daf-220">**J2EE**</span></span>](app-insights-java-live.md)
* <span data-ttu-id="d2daf-221">**在開發階段：將 Application Insights 加入至您的程式碼。**</span><span class="sxs-lookup"><span data-stu-id="d2daf-221">**At development time: add Application Insights to your code.**</span></span> <span data-ttu-id="d2daf-222">可讓您撰寫自訂遙測及檢測後端和桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2daf-222">Allows you to write custom telemetry and to instrument back-end and desktop apps.</span></span>
  * <span data-ttu-id="d2daf-223">[Visual Studio](app-insights-asp-net.md) 2013 Update 2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d2daf-223">[Visual Studio](app-insights-asp-net.md) 2013 update 2 or later.</span></span>
  * <span data-ttu-id="d2daf-224">[Eclipse](app-insights-java-eclipse.md) 或 [其他工具](app-insights-java-get-started.md) 中的 Java</span><span class="sxs-lookup"><span data-stu-id="d2daf-224">Java in [Eclipse](app-insights-java-eclipse.md) or [other tools](app-insights-java-get-started.md)</span></span>
  * [<span data-ttu-id="d2daf-225">Node.js</span><span class="sxs-lookup"><span data-stu-id="d2daf-225">Node.js</span></span>](app-insights-nodejs.md)
  * [<span data-ttu-id="d2daf-226">其他平台</span><span class="sxs-lookup"><span data-stu-id="d2daf-226">Other platforms</span></span>](app-insights-platforms.md)
* <span data-ttu-id="d2daf-227">**[檢測您的網頁](app-insights-javascript.md)**的頁面檢視、AJAX 和其他用戶端遙測。</span><span class="sxs-lookup"><span data-stu-id="d2daf-227">**[Instrument your web pages](app-insights-javascript.md)** for page view, AJAX and other client-side telemetry.</span></span>
* <span data-ttu-id="d2daf-228">**[可用性集合](app-insights-monitor-web-app-availability.md)** - 定期從我們的伺服器 ping 您的網站。</span><span class="sxs-lookup"><span data-stu-id="d2daf-228">**[Availability tests](app-insights-monitor-web-app-availability.md)** - ping your website regularly from our servers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d2daf-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2daf-229">Next steps</span></span>
<span data-ttu-id="d2daf-230">在執行階段開始使用︰</span><span class="sxs-lookup"><span data-stu-id="d2daf-230">Get started at runtime with:</span></span>

* [<span data-ttu-id="d2daf-231">IIS 伺服器</span><span class="sxs-lookup"><span data-stu-id="d2daf-231">IIS server</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="d2daf-232">J2EE 伺服器</span><span class="sxs-lookup"><span data-stu-id="d2daf-232">J2EE server</span></span>](app-insights-java-live.md)

<span data-ttu-id="d2daf-233">在開發階段開始使用︰</span><span class="sxs-lookup"><span data-stu-id="d2daf-233">Get started at development time with:</span></span>

* [<span data-ttu-id="d2daf-234">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d2daf-234">ASP.NET</span></span>](app-insights-asp-net.md)
* [<span data-ttu-id="d2daf-235">Java</span><span class="sxs-lookup"><span data-stu-id="d2daf-235">Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="d2daf-236">Node.js</span><span class="sxs-lookup"><span data-stu-id="d2daf-236">Node.js</span></span>](app-insights-nodejs.md)

## <a name="support-and-feedback"></a><span data-ttu-id="d2daf-237">支援與意見反應</span><span class="sxs-lookup"><span data-stu-id="d2daf-237">Support and feedback</span></span>
* <span data-ttu-id="d2daf-238">疑難排解與問題：</span><span class="sxs-lookup"><span data-stu-id="d2daf-238">Questions and Issues:</span></span>
  * <span data-ttu-id="d2daf-239">[疑難排解][qna]</span><span class="sxs-lookup"><span data-stu-id="d2daf-239">[Troubleshooting][qna]</span></span>
  * [<span data-ttu-id="d2daf-240">MSDN 論壇</span><span class="sxs-lookup"><span data-stu-id="d2daf-240">MSDN Forum</span></span>](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=ApplicationInsights)
  * [<span data-ttu-id="d2daf-241">StackOverflow</span><span class="sxs-lookup"><span data-stu-id="d2daf-241">StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)
* <span data-ttu-id="d2daf-242">您的建議：</span><span class="sxs-lookup"><span data-stu-id="d2daf-242">Your suggestions:</span></span>
  * [<span data-ttu-id="d2daf-243">UserVoice</span><span class="sxs-lookup"><span data-stu-id="d2daf-243">UserVoice</span></span>](https://visualstudio.uservoice.com/forums/357324)
* <span data-ttu-id="d2daf-244">部落格：</span><span class="sxs-lookup"><span data-stu-id="d2daf-244">Blog:</span></span>
  * [<span data-ttu-id="d2daf-245">Application Insights 部落格</span><span class="sxs-lookup"><span data-stu-id="d2daf-245">Application Insights blog</span></span>](https://azure.microsoft.com/blog/tag/application-insights)

## <a name="videos"></a><span data-ttu-id="d2daf-246">影片</span><span class="sxs-lookup"><span data-stu-id="d2daf-246">Videos</span></span>

<span data-ttu-id="d2daf-247">[![動畫簡介](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)</span><span class="sxs-lookup"><span data-stu-id="d2daf-247">[![Animated introduction](./media/app-insights-overview/video-front-1.png)](https://www.youtube.com/watch?v=fX2NtGrh-Y0)</span></span>

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
