---
title: "在 Visual Studio 中的 aaaAnalyzing 趨勢 |Microsoft 文件"
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
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a><span data-ttu-id="5afe6-103">在 Visual Studio 中分析趨勢 | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5afe6-103">Analyzing Trends in Visual Studio</span></span>
<span data-ttu-id="5afe6-104">hello Application Insights Trends 工具視覺化檢視如何 web 應用程式的重要的遙測事件會隨時間變更，可幫助您快速識別出問題與異常狀況。</span><span class="sxs-lookup"><span data-stu-id="5afe6-104">hello Application Insights Trends tool visualizes how your web application's important telemetry events change over time, helping you quickly identify problems and anomalies.</span></span> <span data-ttu-id="5afe6-105">您可以將您連結 toomore 詳細的診斷資訊，趨勢可協助您改善應用程式效能，追蹤 hello 原因的例外狀況，並展現從您的自訂事件的深入見解。</span><span class="sxs-lookup"><span data-stu-id="5afe6-105">By linking you toomore detailed diagnostic information, Trends can help you improve your app's performance, track down hello causes of exceptions, and uncover insights from your custom events.</span></span>

![範例趨勢視窗](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a><span data-ttu-id="5afe6-107">針對 Application Insights 設定您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5afe6-107">Configure your web app for Application Insights</span></span>

<span data-ttu-id="5afe6-108">如果您尚未這麼做，請[針對 Application Insights 設定您的 Web 應用程式](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5afe6-108">If you haven't done this already, [configure your web app for Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5afe6-109">這可讓它 toosend 遙測 toohello Application Insights 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5afe6-109">This allows it toosend telemetry toohello Application Insights portal.</span></span> <span data-ttu-id="5afe6-110">hello 趨勢工具會從該處讀取 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="5afe6-110">hello Trends tool reads hello telemetry from there.</span></span>

<span data-ttu-id="5afe6-111">在 Visual Studio 2015 Update 3 及更新版本中可取得 Application Insights 趨勢。</span><span class="sxs-lookup"><span data-stu-id="5afe6-111">Application Insights Trends is available in Visual Studio 2015 Update 3 and later.</span></span>

## <a name="open-application-insights-trends"></a><span data-ttu-id="5afe6-112">開啟 Application Insights 趨勢</span><span class="sxs-lookup"><span data-stu-id="5afe6-112">Open Application Insights Trends</span></span>
<span data-ttu-id="5afe6-113">tooopen hello Application Insights Trends 視窗：</span><span class="sxs-lookup"><span data-stu-id="5afe6-113">tooopen hello Application Insights Trends window:</span></span>

* <span data-ttu-id="5afe6-114">從 hello Application Insights 工具列按鈕，選擇 **瀏覽遙測趨勢**，或</span><span class="sxs-lookup"><span data-stu-id="5afe6-114">From hello Application Insights toolbar button, choose **Explore Telemetry Trends**, or</span></span>
* <span data-ttu-id="5afe6-115">Hello 專案內容功能表中選擇**Application Insights > 瀏覽遙測趨勢**，或</span><span class="sxs-lookup"><span data-stu-id="5afe6-115">From hello project context menu, choose **Application Insights > Explore Telemetry Trends**, or</span></span>
* <span data-ttu-id="5afe6-116">從 hello Visual Studio 功能表列上選擇 **檢視 > 其他視窗 > Application Insights Trends**。</span><span class="sxs-lookup"><span data-stu-id="5afe6-116">From hello Visual Studio menu bar, choose **View > Other Windows > Application Insights Trends**.</span></span>

<span data-ttu-id="5afe6-117">您可能會看到提示 tooselect 資源。</span><span class="sxs-lookup"><span data-stu-id="5afe6-117">You may see a prompt tooselect a resource.</span></span> <span data-ttu-id="5afe6-118">按一下**選取資源**，請使用 Azure 訂用帳戶，登入，然後從您想其 tooanalyze 遙測趨勢的 hello 清單中選擇的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="5afe6-118">Click **Select a resource**, sign in with an Azure subscription, then choose an Application Insights resource from hello list for which you'd like tooanalyze telemetry trends.</span></span>

## <a name="choose-a-trend-analysis"></a><span data-ttu-id="5afe6-119">選擇趨勢分析</span><span class="sxs-lookup"><span data-stu-id="5afe6-119">Choose a trend analysis</span></span>
![趨勢分析的常見類型功能表](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

<span data-ttu-id="5afe6-121">開始使用所選擇的其中五個一般趨勢分析，從 hello 過去 24 小時內每個分析資料：</span><span class="sxs-lookup"><span data-stu-id="5afe6-121">Get started by choosing from one of five common trend analyses, each analyzing data from hello last 24 hours:</span></span>

* <span data-ttu-id="5afe6-122">**調查您伺服器要求的效能問題**-提出的要求 tooyour 服務，依回應時間</span><span class="sxs-lookup"><span data-stu-id="5afe6-122">**Investigate performance issues with your server requests** - Requests made tooyour service, grouped by response times</span></span>
* <span data-ttu-id="5afe6-123">**分析伺服器要求中的錯誤**-提出的要求 tooyour 服務，依 HTTP 回應碼</span><span class="sxs-lookup"><span data-stu-id="5afe6-123">**Analyze errors in your server requests** - Requests made tooyour service, grouped by HTTP response code</span></span>
* <span data-ttu-id="5afe6-124">**檢查您的應用程式中的 hello 例外狀況**-例外狀況，從您的服務，依例外狀況類型</span><span class="sxs-lookup"><span data-stu-id="5afe6-124">**Examine hello exceptions in your application** - Exceptions from your service, grouped by exception type</span></span>
* <span data-ttu-id="5afe6-125">**檢查您的應用程式相依性的 hello 效能**-服務您的服務，稱為依回應時間</span><span class="sxs-lookup"><span data-stu-id="5afe6-125">**Check hello performance of your application's dependencies** - Services called by your service, grouped by response times</span></span>
* <span data-ttu-id="5afe6-126">**檢查您的自訂事件** - 您為服務設定的自訂事件 (依事件類型分組)。</span><span class="sxs-lookup"><span data-stu-id="5afe6-126">**Inspect your custom events** - Custom events you've set up for your service, grouped by event type.</span></span>

<span data-ttu-id="5afe6-127">稍後從 hello 使用預先建立的分析這些項目**檢視遙測分析的一般類型**在 hello hello 趨勢視窗左上角的按鈕。</span><span class="sxs-lookup"><span data-stu-id="5afe6-127">These pre-built analyses are available later from hello **View common types of telemetry analysis** button in hello upper-left corner of hello Trends window.</span></span>

## <a name="visualize-trends-in-your-application"></a><span data-ttu-id="5afe6-128">以視覺化方式呈現您的應用程式的趨勢</span><span class="sxs-lookup"><span data-stu-id="5afe6-128">Visualize trends in your application</span></span>
<span data-ttu-id="5afe6-129">Application Insights 趨勢會從您的應用程式的遙測建立時間序列視覺效果。</span><span class="sxs-lookup"><span data-stu-id="5afe6-129">Application Insights Trends creates a time series visualization from your app's telemetry.</span></span> <span data-ttu-id="5afe6-130">每一個時間序列視覺效果會顯示某些時間範圍內一種類型的遙測 (依該遙測的其中一個屬性分組)。</span><span class="sxs-lookup"><span data-stu-id="5afe6-130">Each time series visualization displays one type of telemetry, grouped by one property of that telemetry, over some time range.</span></span> <span data-ttu-id="5afe6-131">例如，您可以依 hello 國家 （地區） 將它們產生，透過 hello 過去 24 小時的 tooview 伺服器要求。</span><span class="sxs-lookup"><span data-stu-id="5afe6-131">For example, you might want tooview server requests, grouped by hello country from which they originated, over hello last 24 hours.</span></span> <span data-ttu-id="5afe6-132">在此範例中，hello 視覺效果上的每個泡泡會在一小時期間代表某些國家/地區的 hello 伺服器要求的計數。</span><span class="sxs-lookup"><span data-stu-id="5afe6-132">In this example, each bubble on hello visualization would represent a count of hello server requests for some country/region during one hour.</span></span>

<span data-ttu-id="5afe6-133">使用 hello 控制項上方的 hello 視窗 tooadjust hello 檢視哪些類型的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="5afe6-133">Use hello controls at hello top of hello window tooadjust what types of telemetry you view.</span></span> <span data-ttu-id="5afe6-134">首先，選擇您感興趣的 hello 遙測類型：</span><span class="sxs-lookup"><span data-stu-id="5afe6-134">First, choose hello telemetry types in which you're interested:</span></span>

* <span data-ttu-id="5afe6-135">**遙測類型** - 伺服器要求、例外狀況、相依性或自訂事件</span><span class="sxs-lookup"><span data-stu-id="5afe6-135">**Telemetry Type** - Server requests, exceptions, depdendencies, or custom events</span></span>
* <span data-ttu-id="5afe6-136">**時間範圍**-從過去 30 分鐘 toohello hello 過去 3 天的任何位置</span><span class="sxs-lookup"><span data-stu-id="5afe6-136">**Time Range** - Anywhere from hello last 30 minutes toohello last 3 days</span></span>
* <span data-ttu-id="5afe6-137">**分組依據** - 例外狀況類型、問題識別碼、國家/區域等等。</span><span class="sxs-lookup"><span data-stu-id="5afe6-137">**Group By** - Exception type, problem ID, country/region, and more.</span></span>

<span data-ttu-id="5afe6-138">然後，按一下 **分析遙測**toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="5afe6-138">Then, click **Analyze Telemetry** toorun hello query.</span></span>

<span data-ttu-id="5afe6-139">toonavigate 之間在 hello 視覺效果 （泡泡）：</span><span class="sxs-lookup"><span data-stu-id="5afe6-139">toonavigate between bubbles in hello visualization:</span></span>

* <span data-ttu-id="5afe6-140">按一下 tooselect 泡泡，就會更新在 hello hello 視窗中，彙總只 hello 事件發生在特定時間週期內的底部 hello 篩選</span><span class="sxs-lookup"><span data-stu-id="5afe6-140">Click tooselect a bubble, which updates hello filters at hello bottom of hello window, summarizing just hello events that occurred during a specific time period</span></span>
* <span data-ttu-id="5afe6-141">按兩下泡泡 toonavigate toohello 搜尋工具，並查看所有在該時間內發生的 hello 個別遙測事件</span><span class="sxs-lookup"><span data-stu-id="5afe6-141">Double-click a bubble toonavigate toohello Search tool and see all of hello individual telemetry events that occured during that time period</span></span>
* <span data-ttu-id="5afe6-142">Ctrl 按一下泡泡 toode 選取它 hello 視覺效果中。</span><span class="sxs-lookup"><span data-stu-id="5afe6-142">Ctrl-click a bubble toode-select it in hello visualization.</span></span>

> [!TIP]
> <span data-ttu-id="5afe6-143">hello 趨勢，並搜尋工具一起運作 toohelp 您之間數千個遙測事件服務中找出 hello 的問題的原因。</span><span class="sxs-lookup"><span data-stu-id="5afe6-143">hello Trends and Search tools work together toohelp you pinpoint hello causes of issues in your service among thousands of telemetry events.</span></span> <span data-ttu-id="5afe6-144">例如，如果您的客戶在某個下午通知您的應用程式較無回應，請開始使用「趨勢」。</span><span class="sxs-lookup"><span data-stu-id="5afe6-144">For example, if one afternoon your customers notice your app is being less responsive, start with Trends.</span></span> <span data-ttu-id="5afe6-145">分析提出的要求 tooyour 服務透過 hello 過去幾小時，依回應時間分組。</span><span class="sxs-lookup"><span data-stu-id="5afe6-145">Analyze requests made tooyour service over hello past several hours, grouped by response time.</span></span> <span data-ttu-id="5afe6-146">查看是否有非常大量的慢速要求。</span><span class="sxs-lookup"><span data-stu-id="5afe6-146">See if there's an unusually large cluster of slow requests.</span></span> <span data-ttu-id="5afe6-147">然後按兩下該泡泡 toogo toohello 搜尋工具，篩選的 toothose 要求事件。</span><span class="sxs-lookup"><span data-stu-id="5afe6-147">Then double click that bubble toogo toohello Search tool, filtered toothose request events.</span></span> <span data-ttu-id="5afe6-148">從搜尋中，您可以瀏覽 hello 內容的要求，並瀏覽 toohello 程式碼牽涉到 tooresolve hello 問題。</span><span class="sxs-lookup"><span data-stu-id="5afe6-148">From Search, you can explore hello contents of those requests and navigate toohello code involved tooresolve hello issue.</span></span>
> 
> 

## <a name="filter"></a><span data-ttu-id="5afe6-149">Filter</span><span class="sxs-lookup"><span data-stu-id="5afe6-149">Filter</span></span>
<span data-ttu-id="5afe6-150">探索更特定的趨勢與 hello 篩選器控制項在 hello hello 視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="5afe6-150">Discover more specific trends with hello filter controls at hello bottom of hello window.</span></span> <span data-ttu-id="5afe6-151">tooapply 篩選中，按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="5afe6-151">tooapply a filter, click on its name.</span></span> <span data-ttu-id="5afe6-152">您可以快速切換不同的篩選器可能會隱藏您遙測的特定維度中的 toodiscover 趨勢。</span><span class="sxs-lookup"><span data-stu-id="5afe6-152">You can quickly switch between different filters toodiscover trends that may be hiding in a particular dimension of your telemetry.</span></span> <span data-ttu-id="5afe6-153">如果您套用在一個維度中，例如例外狀況類型篩選其他維度中的篩選器會保留可點選，即使檔案會呈現灰色。tooun-套用篩選，再按一次。</span><span class="sxs-lookup"><span data-stu-id="5afe6-153">If you apply a filter in one dimension, like Exception Type, filters in other dimensions remain clickable even though they appear grayed-out. tooun-apply a filter, click it again.</span></span> <span data-ttu-id="5afe6-154">按一下 Ctrl 以 tooselect 中的多個篩選條件 hello 相同的維度。</span><span class="sxs-lookup"><span data-stu-id="5afe6-154">Ctrl-click tooselect multiple filters in hello same dimension.</span></span>

![趨勢篩選器](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

<span data-ttu-id="5afe6-156">如果您想 tooapply 多個篩選條件嗎？</span><span class="sxs-lookup"><span data-stu-id="5afe6-156">What if you want tooapply multiple filters?</span></span> 

1. <span data-ttu-id="5afe6-157">套用 hello 第一個篩選器。</span><span class="sxs-lookup"><span data-stu-id="5afe6-157">Apply hello first filter.</span></span> 
2. <span data-ttu-id="5afe6-158">按一下 hello**套用選取的篩選並再次查詢**hello 名稱 hello 維度的第一個篩選按鈕。</span><span class="sxs-lookup"><span data-stu-id="5afe6-158">Click hello **Apply selected filters and query again** button by hello name of hello dimension of your first filter.</span></span> <span data-ttu-id="5afe6-159">這會重新查詢您遙測符合 hello 第一個篩選條件的事件。</span><span class="sxs-lookup"><span data-stu-id="5afe6-159">This will re-query your telemetry for only events that match hello first filter.</span></span> 
3. <span data-ttu-id="5afe6-160">套用第二個篩選器。</span><span class="sxs-lookup"><span data-stu-id="5afe6-160">Apply a second filter.</span></span> 
4. <span data-ttu-id="5afe6-161">重複您遙測的特定子集 hello 程序 toofind 趨勢。</span><span class="sxs-lookup"><span data-stu-id="5afe6-161">Repeat hello process toofind trends in specific subsets of your telemetry.</span></span> <span data-ttu-id="5afe6-162">例如，名為 "GET Home/Index"「且」來自德國「且」收到 500 回應碼的伺服器要求。</span><span class="sxs-lookup"><span data-stu-id="5afe6-162">For example, server requests named "GET Home/Index" *and* that came from Germany *and* that received a 500 response code.</span></span> 

<span data-ttu-id="5afe6-163">tooun-套用這些篩選條件的其中一個，請按一下 hello**移除選取的篩選，並再次查詢**hello 維度 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5afe6-163">tooun-apply one of these filters, click hello **Remove selected filters and query again** button for hello dimension.</span></span>

![多個篩選器](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a><span data-ttu-id="5afe6-165">尋找異常</span><span class="sxs-lookup"><span data-stu-id="5afe6-165">Find anomalies</span></span>
<span data-ttu-id="5afe6-166">hello 趨勢工具可以反白顯示泡泡在 hello 異常比較的 tooother （泡泡） 事件的相同時間序列。</span><span class="sxs-lookup"><span data-stu-id="5afe6-166">hello Trends tool can highlight bubbles of events that are anomalous compared tooother bubbles in hello same time series.</span></span> <span data-ttu-id="5afe6-167">在 hello 檢視類型下拉式清單中，選擇 **時間貯體 （反白顯示異常狀況） 中的計數**或**時間貯體 （反白顯示異常狀況） 中的百分比**。</span><span class="sxs-lookup"><span data-stu-id="5afe6-167">In hello View Type dropdown, choose **Counts in time bucket (highlight anomalies)** or **Percentages in time bucket (highlight anomalies)**.</span></span> <span data-ttu-id="5afe6-168">紅色泡泡為異常。</span><span class="sxs-lookup"><span data-stu-id="5afe6-168">Red bubbles are anomalous.</span></span> <span data-ttu-id="5afe6-169">計數/百分比超過 2.1 時間 hello hello 計數/百分比超過兩個時間週期 （48 小時，如果您正在檢視 hello 最後 24 小時等等）。 hello 中發生的標準差 （泡泡） 所定義的異常狀況。</span><span class="sxs-lookup"><span data-stu-id="5afe6-169">Anomalies are defined as bubbles with counts/percentages exceeding 2.1 times hello standard deviation of hello counts/percentages that occured in hello past two time periods (48 hours if you're viewing hello last 24 hours, etc.).</span></span>

![彩色的點表示異常](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> <span data-ttu-id="5afe6-171">在小型泡泡的時間序列中尋找可能看起來大小相似的離群值時，醒目提示異常特別實用。</span><span class="sxs-lookup"><span data-stu-id="5afe6-171">Highlighting anomalies is especially helpful for finding outliers in time series of small bubbles that may otherwise look similarly sized.</span></span>  
> 
> 

## <span data-ttu-id="5afe6-172"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="5afe6-172"><a name="next"></a>Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="5afe6-173">**[在 Visual Studio 中使用 Application Insights](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="5afe6-173">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="5afe6-174">搜尋遙測、查看 CodeLens 中的資料，以及設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="5afe6-174">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="5afe6-175">盡在 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="5afe6-175">All within Visual Studio.</span></span> |![Hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights 搜尋](./media/app-insights-visual-studio-trends/34.png) |
| <span data-ttu-id="5afe6-177">**[新增更多測試](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="5afe6-177">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="5afe6-178">監視使用狀況、可用性、相依性、例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5afe6-178">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="5afe6-179">整合來自記錄架構的追蹤。</span><span class="sxs-lookup"><span data-stu-id="5afe6-179">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="5afe6-180">撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="5afe6-180">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| <span data-ttu-id="5afe6-182">**[使用 hello Application Insights 入口網站](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="5afe6-182">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="5afe6-183">儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及遙測匯出等功能。</span><span class="sxs-lookup"><span data-stu-id="5afe6-183">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

