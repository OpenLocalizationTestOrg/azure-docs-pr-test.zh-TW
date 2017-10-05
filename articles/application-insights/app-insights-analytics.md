---
title: "分析 - 強大的 Azure Application Insights 搜尋工具 | Microsoft Docs"
description: "分析概觀，強大的 Application Insights 診斷搜尋工具。 "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8174745a00a107eea648b223a00466b6a7f37331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="4909f-103">Application Insights 中的分析</span><span class="sxs-lookup"><span data-stu-id="4909f-103">Analytics in Application Insights</span></span>
<span data-ttu-id="4909f-104">[分析](app-insights-analytics.md)是 [Application Insights](app-insights-overview.md) 的強大搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="4909f-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="4909f-105">這些分頁說明 Log Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="4909f-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="4909f-106">**[觀看簡介影片](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**。</span><span class="sxs-lookup"><span data-stu-id="4909f-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="4909f-107">如果您的應用程式還未將資料傳送至 Application Insights，則**[在我們的模擬資料上測試分析](https://analytics.applicationinsights.io/demo)**。</span><span class="sxs-lookup"><span data-stu-id="4909f-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="4909f-108">**[SQL 使用者的功能提要](https://aka.ms/sql-analytics)**會翻譯成最常見的習慣用語。</span><span class="sxs-lookup"><span data-stu-id="4909f-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="4909f-109">**[語言參考](app-insights-analytics-reference.md)** 了解如何使用 Log Analytics 查詢語言的分析查詢語言的所有強大功能。</span><span class="sxs-lookup"><span data-stu-id="4909f-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="4909f-110">分析中的查詢功能</span><span class="sxs-lookup"><span data-stu-id="4909f-110">Queries in Analytics</span></span>
<span data-ttu-id="4909f-111">標準的查詢是一個「來源」資料表，後面接著一系列由 `|` 隔開的「運算子」。</span><span class="sxs-lookup"><span data-stu-id="4909f-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="4909f-112">例如，讓我們來了解海德拉巴的市民在一天當中的哪些時間試用我們的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4909f-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="4909f-113">同時我們要看看針對他們的 HTTP 要求傳回哪些結果碼。</span><span class="sxs-lookup"><span data-stu-id="4909f-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="4909f-114">我們會計算不同的用戶端 IP 位址，並以過去 7 天每天的小時為單位將它們群組。</span><span class="sxs-lookup"><span data-stu-id="4909f-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="4909f-115">若要取得過去 24 小時之外的結果，請在查詢中明確包含 'timestamp'，或使用時間範圍下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="4909f-115">To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.</span></span>
>

<span data-ttu-id="4909f-116">使用橫條圖展示來顯示結果，選擇以不同的回應碼來堆疊結果：</span><span class="sxs-lookup"><span data-stu-id="4909f-116">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![選擇橫條圖、X 和 Y 軸，然後分割](./media/app-insights-analytics/020.png)

<span data-ttu-id="4909f-118">看來我們的應用程式在海德拉巴的午休時間及就寢時間最受歡迎。</span><span class="sxs-lookup"><span data-stu-id="4909f-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="4909f-119">(而且我們應該調查那些 500 的代碼。)</span><span class="sxs-lookup"><span data-stu-id="4909f-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="4909f-120">也有強大的統計運算功能︰</span><span class="sxs-lookup"><span data-stu-id="4909f-120">There are also powerful statistical operations:</span></span>

![統計查詢的結果](./media/app-insights-analytics/025.png)

<span data-ttu-id="4909f-122">這個語言具有許多吸引人的功能︰</span><span class="sxs-lookup"><span data-stu-id="4909f-122">The language has many attractive features:</span></span>


* <span data-ttu-id="4909f-123">[篩選](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) 未經處理的應用程式遙測，包括您的自訂屬性和計量。</span><span class="sxs-lookup"><span data-stu-id="4909f-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="4909f-124">[加入](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) 多個資料表 – 將要求與頁面檢視、相依性呼叫、例外狀況和記錄追蹤相互關聯。</span><span class="sxs-lookup"><span data-stu-id="4909f-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="4909f-125">功能強大的統計 [彙總](https://docs.loganalytics.io/learn/tutorials/aggregations.html)。</span><span class="sxs-lookup"><span data-stu-id="4909f-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="4909f-126">功能如同 SQL 一般強大，但更容易用來進行複雜的查詢︰您可以使用管線將資料從某一個基本運算傳送到下一個運算，而不需使用巢串陳述式。</span><span class="sxs-lookup"><span data-stu-id="4909f-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="4909f-127">立即且功能強大的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="4909f-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="4909f-128">[將圖表釘選到 Azure 儀表板](app-insights-analytics-using.md#pin-to-dashboard)。</span><span class="sxs-lookup"><span data-stu-id="4909f-128">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="4909f-129">[將查詢匯出至 Power BI](app-insights-analytics-using.md#export-to-power-bi)。</span><span class="sxs-lookup"><span data-stu-id="4909f-129">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="4909f-130">您可以使用 [REST API](https://dev.applicationinsights.io/) 以程式設計方式 (例如從 Powershell) 執行查詢。</span><span class="sxs-lookup"><span data-stu-id="4909f-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="4909f-131">連接到您的 Application Insights 資料</span><span class="sxs-lookup"><span data-stu-id="4909f-131">Connect to your Application Insights data</span></span>
<span data-ttu-id="4909f-132">在 Application Insights 中，從 app 的 [概觀刀鋒視窗](app-insights-dashboards.md) 開啟 [分析]：</span><span class="sxs-lookup"><span data-stu-id="4909f-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![開啟 portal.azure.com，開啟您的 Application Insights 資源，然後按一下 [分析]。](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="4909f-134">影片</span><span class="sxs-lookup"><span data-stu-id="4909f-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="4909f-135">查詢範例</span><span class="sxs-lookup"><span data-stu-id="4909f-135">Query examples</span></span>

<span data-ttu-id="4909f-136">請嘗試下列逐步解說，以了解 Analytics 的強大功能：</span><span class="sxs-lookup"><span data-stu-id="4909f-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>

 *  [<span data-ttu-id="4909f-137">自動診斷要求持續時間中的突增和步驟跳躍 (英文)</span><span class="sxs-lookup"><span data-stu-id="4909f-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="4909f-138">以時間序列分析對效能降低進行分析 (英文)</span><span class="sxs-lookup"><span data-stu-id="4909f-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="4909f-139">以 autocluster 和 diffpatterns 分析應用程式失敗 (英文)</span><span class="sxs-lookup"><span data-stu-id="4909f-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="4909f-140">搭配時間序列分析的進階圖形偵測 (英文)</span><span class="sxs-lookup"><span data-stu-id="4909f-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="4909f-141">使用滑動視窗作業分析應用程式使用情況 (累積的 MAU/DAU 等等) (英文)</span><span class="sxs-lookup"><span data-stu-id="4909f-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="4909f-142">[根據偵錯記錄檔的分析來偵測服務中斷 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true)，以及[這篇 (英文)](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics) 相對應的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="4909f-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="4909f-143">[使用簡單的偵錯記錄檔來分析應用程式的效能 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true)，以及[這篇 (英文)](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/) 相對應的部落格文章</span><span class="sxs-lookup"><span data-stu-id="4909f-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="4909f-144">[使用簡單的偵錯記錄檔來測量程式碼流程中每個步驟的持續時間 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true)，以及[這篇 (英文)](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/) 相對應的部落格文章</span><span class="sxs-lookup"><span data-stu-id="4909f-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="4909f-145">[使用簡單的偵錯記錄檔來分析並行 (英文)](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true)，以及[這篇 (英文)](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/) 相對應的部落格文章</span><span class="sxs-lookup"><span data-stu-id="4909f-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="4909f-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4909f-146">Next steps</span></span>
* <span data-ttu-id="4909f-147">我們建議您從 [語言教學](app-insights-analytics-tour.md)開始。</span><span class="sxs-lookup"><span data-stu-id="4909f-147">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="4909f-148">深入了解如何[使用分析](app-insights-analytics-using.md)。</span><span class="sxs-lookup"><span data-stu-id="4909f-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="4909f-149">[語言參考](app-insights-analytics-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="4909f-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
