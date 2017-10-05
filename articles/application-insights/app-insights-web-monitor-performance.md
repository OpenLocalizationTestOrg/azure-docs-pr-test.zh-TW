---
title: "使用 Application Insights 來監視應用程式的健康情況和流量"
description: "開始使用 Application Insights。 分析內部部署或 Microsoft Azure 應用程式的使用情況、可用性和效能。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 5b7b1f4a53cd2624ee8e2ab684ba6ba63252674f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="b2d50-104">監視 Web 應用程式的效能</span><span class="sxs-lookup"><span data-stu-id="b2d50-104">Monitor performance in web applications</span></span>


<span data-ttu-id="b2d50-105">確認應用程式的運作狀況良好，以及迅速找出任何失敗。</span><span class="sxs-lookup"><span data-stu-id="b2d50-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="b2d50-106">[Application Insights][start] 能指出任何效能問題和例外狀況，以及協助您尋找及診斷根本原因。</span><span class="sxs-lookup"><span data-stu-id="b2d50-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose the root causes.</span></span>

<span data-ttu-id="b2d50-107">Application Insights 可以監視 Java 和 ASP.NET Web 應用程式與服務、WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="b2d50-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="b2d50-108">這些服務可以裝載在內部部署、虛擬機器上，或作為 Microsoft Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="b2d50-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="b2d50-109">用戶端方面，Application Insights 可從網頁及各種裝置 (包括 iOS、Android 和 Windows 市集應用程式) 上取得遙測。</span><span class="sxs-lookup"><span data-stu-id="b2d50-109">On the client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="b2d50-110">我們讓尋找您的 Web 應用程式中緩慢執行分頁有新的體驗。</span><span class="sxs-lookup"><span data-stu-id="b2d50-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="b2d50-111">如果您沒有它的存取權，藉由使用[預覽刀鋒視窗](app-insights-previews.md)以設定預覽選項來啟用它。</span><span class="sxs-lookup"><span data-stu-id="b2d50-111">If you don't have access to it, enable it by configuring your preview options with the [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="b2d50-112">在[使用互動式效能調查尋找及修正效能瓶頸](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation)中深入了解這個新體驗。</span><span class="sxs-lookup"><span data-stu-id="b2d50-112">Read about this new experience in [Find and fix performance bottlenecks with the interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="b2d50-113"><a name="setup"></a>設定效能監視</span><span class="sxs-lookup"><span data-stu-id="b2d50-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="b2d50-114">如果您尚未將 Application Insights 新增至專案中 (亦即專案沒有 ApplicationInsights.config)，請選擇以下任一種方法來開始使用：</span><span class="sxs-lookup"><span data-stu-id="b2d50-114">If you haven't yet added Application Insights to your project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways to get started:</span></span>

* [<span data-ttu-id="b2d50-115">ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b2d50-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="b2d50-116">加入例外狀況監視</span><span class="sxs-lookup"><span data-stu-id="b2d50-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="b2d50-117">加入相依性監視</span><span class="sxs-lookup"><span data-stu-id="b2d50-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="b2d50-118">J2EE Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b2d50-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="b2d50-119">加入相依性監視</span><span class="sxs-lookup"><span data-stu-id="b2d50-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="b2d50-120"><a name="view"></a>探索效能度量</span><span class="sxs-lookup"><span data-stu-id="b2d50-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="b2d50-121">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至您為應用程式設定的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="b2d50-121">In [the Azure portal](https://portal.azure.com), browse to the Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="b2d50-122">概觀刀鋒視窗會顯示基本的效能資料：</span><span class="sxs-lookup"><span data-stu-id="b2d50-122">The overview blade shows basic performance data:</span></span>

<span data-ttu-id="b2d50-123">按一下任一圖表可查看詳細資料，也能查看較長期的結果。</span><span class="sxs-lookup"><span data-stu-id="b2d50-123">Click any chart to see more detail, and to see results for a longer period.</span></span> <span data-ttu-id="b2d50-124">例如，按一下 [要求] 磚，然後選取時間範圍：</span><span class="sxs-lookup"><span data-stu-id="b2d50-124">For example, click the Requests tile and then select a time range:</span></span>

![按一下詳細資料的方式來選取時間範圍](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="b2d50-126">按一下圖表以選擇它要顯示的度量，或是加入新圖表並選取其度量：</span><span class="sxs-lookup"><span data-stu-id="b2d50-126">Click a chart to choose which metrics it displays, or add a new chart and select its metrics:</span></span>

![按一下圖形以選擇度量](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="b2d50-128">**取消核取所有度量** 可查看所有可供選擇的項目。</span><span class="sxs-lookup"><span data-stu-id="b2d50-128">**Uncheck all the metrics** to see the full selection that is available.</span></span> <span data-ttu-id="b2d50-129">度量分為多個群組；當您選取群組的任何成員時，只有該群組的其他成員會出現。</span><span class="sxs-lookup"><span data-stu-id="b2d50-129">The metrics fall into groups; when any member of a group is selected, only the other members of that group appear.</span></span>

## <span data-ttu-id="b2d50-130"><a name="metrics"></a>這具有哪些意義？</span><span class="sxs-lookup"><span data-stu-id="b2d50-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="b2d50-131">效能磚和報告</span><span class="sxs-lookup"><span data-stu-id="b2d50-131">Performance tiles and reports</span></span>
<span data-ttu-id="b2d50-132">您可以取用多種效能計量。</span><span class="sxs-lookup"><span data-stu-id="b2d50-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="b2d50-133">我們從預設顯示在應用程式分頁中的度量開始討論。</span><span class="sxs-lookup"><span data-stu-id="b2d50-133">Let's start with those that appear by default on the application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="b2d50-134">要求</span><span class="sxs-lookup"><span data-stu-id="b2d50-134">Requests</span></span>
<span data-ttu-id="b2d50-135">在指定期間內接收到的 HTTP 要求數量。</span><span class="sxs-lookup"><span data-stu-id="b2d50-135">The number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="b2d50-136">將此度量與其他報告中的結果比較，可了解應用程式在各種負載下的行為。</span><span class="sxs-lookup"><span data-stu-id="b2d50-136">Compare this with the results on other reports to see how your app behaves as the load varies.</span></span>

<span data-ttu-id="b2d50-137">HTTP 要求包括分頁、資料及映像的所有 GET 或 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="b2d50-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="b2d50-138">按一下磚可取得特定 URL 的計數。</span><span class="sxs-lookup"><span data-stu-id="b2d50-138">Click on the tile to get counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="b2d50-139">平均回應時間</span><span class="sxs-lookup"><span data-stu-id="b2d50-139">Average response time</span></span>
<span data-ttu-id="b2d50-140">測量從 Web 要求進入應用程式到傳回回應之間的時間。</span><span class="sxs-lookup"><span data-stu-id="b2d50-140">Measures the time between a web request entering your application and the response being returned.</span></span>

<span data-ttu-id="b2d50-141">資料點會指出移動平均值。</span><span class="sxs-lookup"><span data-stu-id="b2d50-141">The points show a moving average.</span></span> <span data-ttu-id="b2d50-142">在有許多要求的情況下，可能會有一些要求偏離平均值，但在圖表中沒有顯著的高低起伏。</span><span class="sxs-lookup"><span data-stu-id="b2d50-142">If there are a lot of requests, there might be some that deviate from the average without an obvious peak or dip in the graph.</span></span>

<span data-ttu-id="b2d50-143">找尋異常的高峰。</span><span class="sxs-lookup"><span data-stu-id="b2d50-143">Look for unusual peaks.</span></span> <span data-ttu-id="b2d50-144">一般來說，當要求增加時，回應時間也會上升。</span><span class="sxs-lookup"><span data-stu-id="b2d50-144">In general, expect response time to rise with a rise in requests.</span></span> <span data-ttu-id="b2d50-145">如果出現不相稱的上升跡象，表示應用程式可能遭遇到資源限制 (例如，應用程式使用之服務的 CPU 或容量)。</span><span class="sxs-lookup"><span data-stu-id="b2d50-145">If the rise is disproportionate, your app might be hitting a resource limit such as CPU or the capacity of a service it uses.</span></span>

<span data-ttu-id="b2d50-146">按一下圖格可取得特定 URL 的時間。</span><span class="sxs-lookup"><span data-stu-id="b2d50-146">Click the tile to get times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="b2d50-147">最慢的要求</span><span class="sxs-lookup"><span data-stu-id="b2d50-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="b2d50-148">顯示可能需要進行效能調整的要求。</span><span class="sxs-lookup"><span data-stu-id="b2d50-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="b2d50-149">失敗的要求</span><span class="sxs-lookup"><span data-stu-id="b2d50-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="b2d50-150">丟出無法攔截之例外狀況的要求計數。</span><span class="sxs-lookup"><span data-stu-id="b2d50-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="b2d50-151">按一下磚可查看特定失敗的詳細資料；選取個別要求可查看要求的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b2d50-151">Click the tile to see the details of specific failures, and select an individual request to see its detail.</span></span> 

<span data-ttu-id="b2d50-152">系統只會針對各項檢查保留一個具代表性的失敗範例。</span><span class="sxs-lookup"><span data-stu-id="b2d50-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="b2d50-153">其他度量</span><span class="sxs-lookup"><span data-stu-id="b2d50-153">Other metrics</span></span>
<span data-ttu-id="b2d50-154">若要查看其他可顯示的度量，請按一下圖表，然後取消選取所有度量以查看可供使用的完整集合。</span><span class="sxs-lookup"><span data-stu-id="b2d50-154">To see what other metrics you can display, click a graph, and then deselect all the metrics to see the full available set.</span></span> <span data-ttu-id="b2d50-155">按一下 (i) 可查看各項度量的定義。</span><span class="sxs-lookup"><span data-stu-id="b2d50-155">Click (i) to see each metric's definition.</span></span>

![取消選取所有度量以查看完整的集合](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="b2d50-157">選取任何計量將會停用其他計量，使其無法顯示在同一個圖表中。</span><span class="sxs-lookup"><span data-stu-id="b2d50-157">Selecting any metric disables the others that can't appear on the same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="b2d50-158">設定警示</span><span class="sxs-lookup"><span data-stu-id="b2d50-158">Set alerts</span></span>
<span data-ttu-id="b2d50-159">若要在任何度量有不尋常的值時收到電子郵件通知，請加入警示。</span><span class="sxs-lookup"><span data-stu-id="b2d50-159">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="b2d50-160">您可以選擇將電子郵件傳送給帳戶管理員，或傳送給特定的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b2d50-160">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="b2d50-161">設定其他屬性之前的資源。</span><span class="sxs-lookup"><span data-stu-id="b2d50-161">Set the resource before the other properties.</span></span> <span data-ttu-id="b2d50-162">如果您想要設定效能或使用度量的相關警示，請勿選擇 webtest 資源。</span><span class="sxs-lookup"><span data-stu-id="b2d50-162">Don't choose the webtest resources if you want to set alerts on performance or usage metrics.</span></span>

<span data-ttu-id="b2d50-163">請小心注意系統要求您輸入臨界值時所使用的單位。</span><span class="sxs-lookup"><span data-stu-id="b2d50-163">Be careful to note the units in which you're asked to enter the threshold value.</span></span>

<bpt id="p1">*</bpt>I don't see the Add Alert button.<ept id="p1">*</ept> <span data-ttu-id="b2d50-165">我沒有看到 [新增警示] 按鈕 - 您只擁有此群組帳戶的唯讀權限嗎？</span><span class="sxs-lookup"><span data-stu-id="b2d50-165">- Is this a group account to which you have read-only access?</span></span> <span data-ttu-id="b2d50-166">請洽詢帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="b2d50-166">Check with the account administrator.</span></span>

## <span data-ttu-id="b2d50-167"><a name="diagnosis"></a>診斷問題</span><span class="sxs-lookup"><span data-stu-id="b2d50-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="b2d50-168">以下是幾個尋找及診斷效能問題的訣竅：</span><span class="sxs-lookup"><span data-stu-id="b2d50-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="b2d50-169">設定 [Web 測試][availability]，以在網站故障、回應異常或過於緩慢時收到警示。</span><span class="sxs-lookup"><span data-stu-id="b2d50-169">Set up [web tests][availability] to be alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="b2d50-170">比較要求計數與其他度量，了解失敗或回應過慢的情況是否與負載有關。</span><span class="sxs-lookup"><span data-stu-id="b2d50-170">Compare the Request count with other metrics to see if failures or slow response are related to load.</span></span>
* <span data-ttu-id="b2d50-171">在程式碼中[插入及搜尋追蹤陳述式][diagnostic]有助於找出問題所在。</span><span class="sxs-lookup"><span data-stu-id="b2d50-171">[Insert and search trace statements][diagnostic] in your code to help pinpoint problems.</span></span>
* <span data-ttu-id="b2d50-172">使用[即時計量資料流][livestream]監視作業中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2d50-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="b2d50-173">使用[快照集偵錯工具][snapshot]擷取 .Net 應用程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="b2d50-173">Capture the state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="b2d50-174">使用互動式效能調查尋找及修正效能瓶頸</span><span class="sxs-lookup"><span data-stu-id="b2d50-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="b2d50-175">您可以使用新的 Application Insights 互動式效能調查，以找出減緩整體效能的 Web 應用程式區域。</span><span class="sxs-lookup"><span data-stu-id="b2d50-175">You can use the new Application Insights interactive performance investigation to locate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="b2d50-176">您可以快速地找出減緩速度的特定分頁，並且使用[分析工具](app-insights-profiler.md)以查看這些分頁之間是否有相互關聯。</span><span class="sxs-lookup"><span data-stu-id="b2d50-176">You can quickly find specific pages that are slowing down, and use the [Profiling tool](app-insights-profiler.md) to see if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="b2d50-177">建立一份執行緩慢分頁的清單</span><span class="sxs-lookup"><span data-stu-id="b2d50-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="b2d50-178">找出效能問題的第一個步驟是取得緩慢回應分頁的清單。</span><span class="sxs-lookup"><span data-stu-id="b2d50-178">The first step for finding performance issues is to get a list of the slow responding pages.</span></span> <span data-ttu-id="b2d50-179">下列螢幕擷取畫面示範如何使用 [效能] 刀鋒視窗取得一份要進一步調查的潛在分頁清單。</span><span class="sxs-lookup"><span data-stu-id="b2d50-179">The screen shot below demonstrates using the Performance blade to get a list of potential pages to investigate further.</span></span> <span data-ttu-id="b2d50-180">您可以從這個分頁快速地查看應用程式的回應時間在大約下午 6:00 時以及再次於大約下午 10 點時減緩。</span><span class="sxs-lookup"><span data-stu-id="b2d50-180">You can quickly see from this page that there was a slow-down in the response time of the app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="b2d50-181">您也可以看到 GET 客戶/詳細資料作業有一些長時間執行的作業，回應時間中間值為 507.05 毫秒。</span><span class="sxs-lookup"><span data-stu-id="b2d50-181">You can also see that the GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Application Insights 互動式效能](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="b2d50-183">向下鑽研特定分頁</span><span class="sxs-lookup"><span data-stu-id="b2d50-183">Drill down on specific pages</span></span>

<span data-ttu-id="b2d50-184">您有了應用程式效能的快照集之後，您可以取得更多特定執行緩慢作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b2d50-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="b2d50-185">按一下清單中的任何作業以查看詳細資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b2d50-185">Click on any operation in the list to see the details as shown below.</span></span> <span data-ttu-id="b2d50-186">您可以從圖表中查看效能是否以相依性為基礎。</span><span class="sxs-lookup"><span data-stu-id="b2d50-186">From the chart you can see if the performance was based on a dependency.</span></span> <span data-ttu-id="b2d50-187">您也可以查看有多少使用者遇到各種不同的回應時間。</span><span class="sxs-lookup"><span data-stu-id="b2d50-187">You can also see how many users experienced the various response times.</span></span> 

![Application Insights 作業刀鋒視窗](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="b2d50-189">在特定時間週期向下鑽研</span><span class="sxs-lookup"><span data-stu-id="b2d50-189">Drill down on a specific time period</span></span>

<span data-ttu-id="b2d50-190">您識別要調查的時間點之後，更進一步向下鑽研以查看可能導致效能減緩的特定作業。</span><span class="sxs-lookup"><span data-stu-id="b2d50-190">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="b2d50-191">當您按一下特定時間點時，會取得分頁的詳細資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b2d50-191">When you click on a specific point in time you get the details of the page as shown below.</span></span> <span data-ttu-id="b2d50-192">在以下範例中，您可以看到針對指定時間週期列出的作業，以及伺服器回應碼和作業持續時間。</span><span class="sxs-lookup"><span data-stu-id="b2d50-192">In the example below you can see the operations listed for a given time period along with the server response codes and the operation duration.</span></span> <span data-ttu-id="b2d50-193">如果您需要將此資訊傳送給開發小組，您也有開啟 TFS 工作項目的 URL。</span><span class="sxs-lookup"><span data-stu-id="b2d50-193">You also have the url for opening a TFS work item if you need to send this information to your development team.</span></span>

![Application Insights 時間配量](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="b2d50-195">在特定作業向下鑽研</span><span class="sxs-lookup"><span data-stu-id="b2d50-195">Drill down on a specific operation</span></span>

<span data-ttu-id="b2d50-196">您識別要調查的時間點之後，更進一步向下鑽研以查看可能導致效能減緩的特定作業。</span><span class="sxs-lookup"><span data-stu-id="b2d50-196">After you have identified a point in time to investigate, drill down even further to look at the specific operations that might have caused the performance slow-down.</span></span> <span data-ttu-id="b2d50-197">從清單按一下作業，以查看作業的詳細資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b2d50-197">Click on an operation from the list to see the details of the operation as shown below.</span></span> <span data-ttu-id="b2d50-198">在此範例中，您可以看到作業失敗，且 Application Insights 提供應用程式擲回之例外狀況的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b2d50-198">In this example you can see that the operation failed, and Application Insights has provided the details of the exception the application threw.</span></span> <span data-ttu-id="b2d50-199">同樣地，您可以從這個刀鋒視窗輕鬆地建立 TFS 工作項目。</span><span class="sxs-lookup"><span data-stu-id="b2d50-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Application Insights 作業刀鋒視窗](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="b2d50-201"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="b2d50-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="b2d50-202">[Web 測試][availability] - 定期從全世界傳送 Web 要求給應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2d50-202">[Web tests][availability] - Have web requests sent to your application at regular intervals from around the world.</span></span>

<span data-ttu-id="b2d50-203">[擷取及搜尋診斷追蹤][diagnostic] - 插入追蹤呼叫並詳查結果，以便找出問題所在。</span><span class="sxs-lookup"><span data-stu-id="b2d50-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through the results to pinpoint issues.</span></span>

<span data-ttu-id="b2d50-204">[流量追蹤][usage] - 了解使用者使用應用程式的情況。</span><span class="sxs-lookup"><span data-stu-id="b2d50-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="b2d50-205">[疑難排解][qna] - 以及問答集</span><span class="sxs-lookup"><span data-stu-id="b2d50-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



