---
title: "在 Visual Studio 中分析趨勢 | Microsoft Docs"
description: "在 Visual Studio 中分析、 視覺化及探索您的 Application Insights 遙測的趨勢。"
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 13fca37303296355ce601333b13110d04fa5fa4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="analyzing-trends-in-visual-studio"></a><span data-ttu-id="8ab83-103">在 Visual Studio 中分析趨勢 | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8ab83-103">Analyzing Trends in Visual Studio</span></span>
<span data-ttu-id="8ab83-104">「Application Insights 趨勢」工具會以視覺化方式呈現 Web 應用程式的重要遙測事件如何隨著時間變更，協助您快速識別問題和異常。</span><span class="sxs-lookup"><span data-stu-id="8ab83-104">The Application Insights Trends tool visualizes how your web application's important telemetry events change over time, helping you quickly identify problems and anomalies.</span></span> <span data-ttu-id="8ab83-105">將您連結至更詳細的診斷資訊，「趨勢」可協助您改善應用程式效能、追蹤例外狀況的原因，以及揭露您的自訂事件情資。</span><span class="sxs-lookup"><span data-stu-id="8ab83-105">By linking you to more detailed diagnostic information, Trends can help you improve your app's performance, track down the causes of exceptions, and uncover insights from your custom events.</span></span>

![範例趨勢視窗](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a><span data-ttu-id="8ab83-107">針對 Application Insights 設定您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8ab83-107">Configure your web app for Application Insights</span></span>

<span data-ttu-id="8ab83-108">如果您尚未這麼做，請[針對 Application Insights 設定您的 Web 應用程式](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8ab83-108">If you haven't done this already, [configure your web app for Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="8ab83-109">這可讓它將遙測資料傳送至 Application Insights 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8ab83-109">This allows it to send telemetry to the Application Insights portal.</span></span> <span data-ttu-id="8ab83-110">趨勢工具會從那裡讀取遙測資料。</span><span class="sxs-lookup"><span data-stu-id="8ab83-110">The Trends tool reads the telemetry from there.</span></span>

<span data-ttu-id="8ab83-111">在 Visual Studio 2015 Update 3 及更新版本中可取得 Application Insights 趨勢。</span><span class="sxs-lookup"><span data-stu-id="8ab83-111">Application Insights Trends is available in Visual Studio 2015 Update 3 and later.</span></span>

## <a name="open-application-insights-trends"></a><span data-ttu-id="8ab83-112">開啟 Application Insights 趨勢</span><span class="sxs-lookup"><span data-stu-id="8ab83-112">Open Application Insights Trends</span></span>
<span data-ttu-id="8ab83-113">若要開啟 [Application Insights 趨勢] 視窗：</span><span class="sxs-lookup"><span data-stu-id="8ab83-113">To open the Application Insights Trends window:</span></span>

* <span data-ttu-id="8ab83-114">從 Application Insights 工具列按鈕，選擇 [探索遙測趨勢] ，或</span><span class="sxs-lookup"><span data-stu-id="8ab83-114">From the Application Insights toolbar button, choose **Explore Telemetry Trends**, or</span></span>
* <span data-ttu-id="8ab83-115">從專案操作功能表，選擇 [Application Insights] > [探索遙測趨勢]，或</span><span class="sxs-lookup"><span data-stu-id="8ab83-115">From the project context menu, choose **Application Insights > Explore Telemetry Trends**, or</span></span>
* <span data-ttu-id="8ab83-116">從 Visual Studio 功能表列，選擇 [檢視] > [其他視窗] > [Application Insights 趨勢]。</span><span class="sxs-lookup"><span data-stu-id="8ab83-116">From the Visual Studio menu bar, choose **View > Other Windows > Application Insights Trends**.</span></span>

<span data-ttu-id="8ab83-117">您可能會看到選取資源的提示。</span><span class="sxs-lookup"><span data-stu-id="8ab83-117">You may see a prompt to select a resource.</span></span> <span data-ttu-id="8ab83-118">按一下 [選取資源] ，登入 Azure 訂用帳戶，然後從您要分析遙測趨勢的清單中選擇 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="8ab83-118">Click **Select a resource**, sign in with an Azure subscription, then choose an Application Insights resource from the list for which you'd like to analyze telemetry trends.</span></span>

## <a name="choose-a-trend-analysis"></a><span data-ttu-id="8ab83-119">選擇趨勢分析</span><span class="sxs-lookup"><span data-stu-id="8ab83-119">Choose a trend analysis</span></span>
![趨勢分析的常見類型功能表](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

<span data-ttu-id="8ab83-121">首先選擇其中一個通用趨勢分析 (共 5 個)，而這些通用趨勢分析會各自分析過去 24 小時內的資料︰</span><span class="sxs-lookup"><span data-stu-id="8ab83-121">Get started by choosing from one of five common trend analyses, each analyzing data from the last 24 hours:</span></span>

* <span data-ttu-id="8ab83-122">**調查伺服器要求的效能問題** - 對您的服務所做的要求 (依回應時間分組)</span><span class="sxs-lookup"><span data-stu-id="8ab83-122">**Investigate performance issues with your server requests** - Requests made to your service, grouped by response times</span></span>
* <span data-ttu-id="8ab83-123">**分析伺服器要求中的錯誤** - 對您的服務所做的要求 (依 HTTP 回應碼分組)</span><span class="sxs-lookup"><span data-stu-id="8ab83-123">**Analyze errors in your server requests** - Requests made to your service, grouped by HTTP response code</span></span>
* <span data-ttu-id="8ab83-124">**檢查應用程式中的例外狀況** - 您的服務的例外狀況 (依例外狀況類型分組)</span><span class="sxs-lookup"><span data-stu-id="8ab83-124">**Examine the exceptions in your application** - Exceptions from your service, grouped by exception type</span></span>
* <span data-ttu-id="8ab83-125">**檢查應用程式相依項目的效能** - 您的服務所呼叫的服務 (依回應時間分組)</span><span class="sxs-lookup"><span data-stu-id="8ab83-125">**Check the performance of your application's dependencies** - Services called by your service, grouped by response times</span></span>
* <span data-ttu-id="8ab83-126">**檢查您的自訂事件** - 您為服務設定的自訂事件 (依事件類型分組)。</span><span class="sxs-lookup"><span data-stu-id="8ab83-126">**Inspect your custom events** - Custom events you've set up for your service, grouped by event type.</span></span>

<span data-ttu-id="8ab83-127">稍後可從 [趨勢] 視窗左上角的 [檢視常見的遙測分析類型]  按鈕取得這些預先建置的分析。</span><span class="sxs-lookup"><span data-stu-id="8ab83-127">These pre-built analyses are available later from the **View common types of telemetry analysis** button in the upper-left corner of the Trends window.</span></span>

## <a name="visualize-trends-in-your-application"></a><span data-ttu-id="8ab83-128">以視覺化方式呈現您的應用程式的趨勢</span><span class="sxs-lookup"><span data-stu-id="8ab83-128">Visualize trends in your application</span></span>
<span data-ttu-id="8ab83-129">Application Insights 趨勢會從您的應用程式的遙測建立時間序列視覺效果。</span><span class="sxs-lookup"><span data-stu-id="8ab83-129">Application Insights Trends creates a time series visualization from your app's telemetry.</span></span> <span data-ttu-id="8ab83-130">每一個時間序列視覺效果會顯示某些時間範圍內一種類型的遙測 (依該遙測的其中一個屬性分組)。</span><span class="sxs-lookup"><span data-stu-id="8ab83-130">Each time series visualization displays one type of telemetry, grouped by one property of that telemetry, over some time range.</span></span> <span data-ttu-id="8ab83-131">例如，您可能想要檢視過去 24 小時內的伺服器要求 (依源自的國家/地區分組)。</span><span class="sxs-lookup"><span data-stu-id="8ab83-131">For example, you might want to view server requests, grouped by the country from which they originated, over the last 24 hours.</span></span> <span data-ttu-id="8ab83-132">在此範例中，視覺效果上的每個泡泡會代表在一小時期間內某個國家/區域的伺服器要求計數。</span><span class="sxs-lookup"><span data-stu-id="8ab83-132">In this example, each bubble on the visualization would represent a count of the server requests for some country/region during one hour.</span></span>

<span data-ttu-id="8ab83-133">使用視窗頂端的控制項來調整您可檢視的遙測類型。</span><span class="sxs-lookup"><span data-stu-id="8ab83-133">Use the controls at the top of the window to adjust what types of telemetry you view.</span></span> <span data-ttu-id="8ab83-134">首先，選擇您感興趣的遙測類型︰</span><span class="sxs-lookup"><span data-stu-id="8ab83-134">First, choose the telemetry types in which you're interested:</span></span>

* <span data-ttu-id="8ab83-135">**遙測類型** - 伺服器要求、例外狀況、相依性或自訂事件</span><span class="sxs-lookup"><span data-stu-id="8ab83-135">**Telemetry Type** - Server requests, exceptions, depdendencies, or custom events</span></span>
* <span data-ttu-id="8ab83-136">**時間範圍** - 從過去 30 分鐘到過去 3 天的任何時間</span><span class="sxs-lookup"><span data-stu-id="8ab83-136">**Time Range** - Anywhere from the last 30 minutes to the last 3 days</span></span>
* <span data-ttu-id="8ab83-137">**分組依據** - 例外狀況類型、問題識別碼、國家/區域等等。</span><span class="sxs-lookup"><span data-stu-id="8ab83-137">**Group By** - Exception type, problem ID, country/region, and more.</span></span>

<span data-ttu-id="8ab83-138">然後，按一下 [分析遙測]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="8ab83-138">Then, click **Analyze Telemetry** to run the query.</span></span>

<span data-ttu-id="8ab83-139">若要在視覺效果中的泡泡之間巡覽︰</span><span class="sxs-lookup"><span data-stu-id="8ab83-139">To navigate between bubbles in the visualization:</span></span>

* <span data-ttu-id="8ab83-140">按一下以選取泡泡，該泡泡會更新視窗底部的篩選器，而且只彙整在特定期間內發生的事件</span><span class="sxs-lookup"><span data-stu-id="8ab83-140">Click to select a bubble, which updates the filters at the bottom of the window, summarizing just the events that occurred during a specific time period</span></span>
* <span data-ttu-id="8ab83-141">按兩下泡泡以瀏覽至「搜尋」工具，並查看在該時間內發生的所有個別遙測事件</span><span class="sxs-lookup"><span data-stu-id="8ab83-141">Double-click a bubble to navigate to the Search tool and see all of the individual telemetry events that occured during that time period</span></span>
* <span data-ttu-id="8ab83-142">按住 CTRL 鍵並按一下泡泡，以在視覺效果中取消選取該泡泡。</span><span class="sxs-lookup"><span data-stu-id="8ab83-142">Ctrl-click a bubble to de-select it in the visualization.</span></span>

> [!TIP]
> <span data-ttu-id="8ab83-143">「趨勢」和「搜尋」工具一起運作，可協助您在數千個遙測事件中找出您服務的問題原因。</span><span class="sxs-lookup"><span data-stu-id="8ab83-143">The Trends and Search tools work together to help you pinpoint the causes of issues in your service among thousands of telemetry events.</span></span> <span data-ttu-id="8ab83-144">例如，如果您的客戶在某個下午通知您的應用程式較無回應，請開始使用「趨勢」。</span><span class="sxs-lookup"><span data-stu-id="8ab83-144">For example, if one afternoon your customers notice your app is being less responsive, start with Trends.</span></span> <span data-ttu-id="8ab83-145">分析在過去幾個小時內對您的服務所做的要求 (依回應時間分組)。</span><span class="sxs-lookup"><span data-stu-id="8ab83-145">Analyze requests made to your service over the past several hours, grouped by response time.</span></span> <span data-ttu-id="8ab83-146">查看是否有非常大量的慢速要求。</span><span class="sxs-lookup"><span data-stu-id="8ab83-146">See if there's an unusually large cluster of slow requests.</span></span> <span data-ttu-id="8ab83-147">然後連按兩下該泡泡來移至「搜尋」工具 (已篩選成這些要求事件)。</span><span class="sxs-lookup"><span data-stu-id="8ab83-147">Then double click that bubble to go to the Search tool, filtered to those request events.</span></span> <span data-ttu-id="8ab83-148">在「搜尋」中，您可以探索這些要求的內容並巡覽至相關程式碼來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="8ab83-148">From Search, you can explore the contents of those requests and navigate to the code involved to resolve the issue.</span></span>
> 
> 

## <a name="filter"></a><span data-ttu-id="8ab83-149">篩選器</span><span class="sxs-lookup"><span data-stu-id="8ab83-149">Filter</span></span>
<span data-ttu-id="8ab83-150">使用視窗底部的篩選控制項，探索更明確的趨勢。</span><span class="sxs-lookup"><span data-stu-id="8ab83-150">Discover more specific trends with the filter controls at the bottom of the window.</span></span> <span data-ttu-id="8ab83-151">若要套用篩選器，請按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="8ab83-151">To apply a filter, click on its name.</span></span> <span data-ttu-id="8ab83-152">您可以快速切換不同的篩選器，以探索可能隱藏在遙測的特定維度中的趨勢。</span><span class="sxs-lookup"><span data-stu-id="8ab83-152">You can quickly switch between different filters to discover trends that may be hiding in a particular dimension of your telemetry.</span></span> <span data-ttu-id="8ab83-153">如果您在一個維度 (如例外狀況類型) 中套用一個篩選器，則其他維度中的篩選器即使呈現灰色，仍然可加以點選。若要取消套用篩選器，請再按一次。</span><span class="sxs-lookup"><span data-stu-id="8ab83-153">If you apply a filter in one dimension, like Exception Type, filters in other dimensions remain clickable even though they appear grayed-out. To un-apply a filter, click it again.</span></span> <span data-ttu-id="8ab83-154">按住 CTRL 鍵並按一下滑鼠，以選取相同維度中的多個篩選器。</span><span class="sxs-lookup"><span data-stu-id="8ab83-154">Ctrl-click to select multiple filters in the same dimension.</span></span>

![趨勢篩選器](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

<span data-ttu-id="8ab83-156">如果您想要套用多個篩選器，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="8ab83-156">What if you want to apply multiple filters?</span></span> 

1. <span data-ttu-id="8ab83-157">套用第一個篩選器。</span><span class="sxs-lookup"><span data-stu-id="8ab83-157">Apply the first filter.</span></span> 
2. <span data-ttu-id="8ab83-158">按一下第一個篩選器的維度名稱旁邊的 [套用選取的篩選器並再次查詢]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8ab83-158">Click the **Apply selected filters and query again** button by the name of the dimension of your first filter.</span></span> <span data-ttu-id="8ab83-159">這只會重新查詢您的遙測中符合第一個篩選條件的事件。</span><span class="sxs-lookup"><span data-stu-id="8ab83-159">This will re-query your telemetry for only events that match the first filter.</span></span> 
3. <span data-ttu-id="8ab83-160">套用第二個篩選器。</span><span class="sxs-lookup"><span data-stu-id="8ab83-160">Apply a second filter.</span></span> 
4. <span data-ttu-id="8ab83-161">重複此程序以在遙測的特定子集中尋找趨勢。</span><span class="sxs-lookup"><span data-stu-id="8ab83-161">Repeat the process to find trends in specific subsets of your telemetry.</span></span> <span data-ttu-id="8ab83-162">例如，名為 "GET Home/Index"「且」來自德國「且」收到 500 回應碼的伺服器要求。</span><span class="sxs-lookup"><span data-stu-id="8ab83-162">For example, server requests named "GET Home/Index" *and* that came from Germany *and* that received a 500 response code.</span></span> 

<span data-ttu-id="8ab83-163">若要取消套用上述其中一個篩選器，請按一下維度的 [移除選取的篩選器並再次查詢]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8ab83-163">To un-apply one of these filters, click the **Remove selected filters and query again** button for the dimension.</span></span>

![多個篩選器](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a><span data-ttu-id="8ab83-165">尋找異常</span><span class="sxs-lookup"><span data-stu-id="8ab83-165">Find anomalies</span></span>
<span data-ttu-id="8ab83-166">「趨勢」工具會醒目提示異常的事件泡泡 (相較於同一個時間序列中的其他泡泡)。</span><span class="sxs-lookup"><span data-stu-id="8ab83-166">The Trends tool can highlight bubbles of events that are anomalous compared to other bubbles in the same time series.</span></span> <span data-ttu-id="8ab83-167">在 [檢視類型] 下拉式清單中，選擇 [時間值區中的計數 (醒目提示異常)] 或 [時間值區中的百分比 (醒目提示異常)]。</span><span class="sxs-lookup"><span data-stu-id="8ab83-167">In the View Type dropdown, choose **Counts in time bucket (highlight anomalies)** or **Percentages in time bucket (highlight anomalies)**.</span></span> <span data-ttu-id="8ab83-168">紅色泡泡為異常。</span><span class="sxs-lookup"><span data-stu-id="8ab83-168">Red bubbles are anomalous.</span></span> <span data-ttu-id="8ab83-169">異常的定義是計數/百分比超過 2.1 乘以在過去兩個時間週期 (如果您正在檢視過去 24 小時的資料，則為 48 小時) 內發生之計數/百分比的標準差的泡泡。</span><span class="sxs-lookup"><span data-stu-id="8ab83-169">Anomalies are defined as bubbles with counts/percentages exceeding 2.1 times the standard deviation of the counts/percentages that occured in the past two time periods (48 hours if you're viewing the last 24 hours, etc.).</span></span>

![彩色的點表示異常](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> <span data-ttu-id="8ab83-171">在小型泡泡的時間序列中尋找可能看起來大小相似的離群值時，醒目提示異常特別實用。</span><span class="sxs-lookup"><span data-stu-id="8ab83-171">Highlighting anomalies is especially helpful for finding outliers in time series of small bubbles that may otherwise look similarly sized.</span></span>  
> 
> 

## <span data-ttu-id="8ab83-172"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="8ab83-172"><a name="next"></a>Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="8ab83-173">**[在 Visual Studio 中使用 Application Insights](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="8ab83-173">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="8ab83-174">搜尋遙測、查看 CodeLens 中的資料，以及設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="8ab83-174">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="8ab83-175">盡在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="8ab83-175">All within Visual Studio.</span></span> |![以滑鼠右鍵按一下專案，然後選擇 [Application Insights]、[搜尋]](./media/app-insights-visual-studio-trends/34.png) |
| <span data-ttu-id="8ab83-177">**[新增更多測試](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="8ab83-177">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="8ab83-178">監視使用狀況、可用性、相依性、例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8ab83-178">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="8ab83-179">整合來自記錄架構的追蹤。</span><span class="sxs-lookup"><span data-stu-id="8ab83-179">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="8ab83-180">撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="8ab83-180">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| <span data-ttu-id="8ab83-182">**[使用 Application Insights 入口網站](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="8ab83-182">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="8ab83-183">儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及遙測匯出等功能。</span><span class="sxs-lookup"><span data-stu-id="8ab83-183">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

