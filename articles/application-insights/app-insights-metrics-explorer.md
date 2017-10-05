---
title: "在 Azure Application Insights 中探索計量 | Microsoft Docs"
description: "如何解譯計量瀏覽器上的圖表，以及如何自訂計量瀏覽器刀鋒視窗。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: a13500284caab79bbe221060ccf3d925ffb1fab5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="f8469-103">在 Application Insights 中探索度量</span><span class="sxs-lookup"><span data-stu-id="f8469-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="f8469-104">[Application Insights][start] 中的度量為從您的應用程式傳送的遙測中的測量值和事件計數。</span><span class="sxs-lookup"><span data-stu-id="f8469-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="f8469-105">它們幫助您偵測效能問題，並觀察使用應用程式方式的趨勢。</span><span class="sxs-lookup"><span data-stu-id="f8469-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="f8469-106">標準度量的範圍很廣泛，而您也可以建立自己的自訂度量和事件。</span><span class="sxs-lookup"><span data-stu-id="f8469-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="f8469-107">度量和事件計數會顯示在彙總值 (例如總和、平均或計數) 的圖表中。</span><span class="sxs-lookup"><span data-stu-id="f8469-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="f8469-108">以下是一組範例圖表︰</span><span class="sxs-lookup"><span data-stu-id="f8469-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="f8469-109">您可在 Application Insights 入口網站中找到度量圖表。</span><span class="sxs-lookup"><span data-stu-id="f8469-109">You find metrics charts everywhere in the Application Insights portal.</span></span> <span data-ttu-id="f8469-110">在大部分情況下，您可以自訂它們，而且您可以將更多圖表新增至刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f8469-110">In most cases, they can be customized, and you can add more charts to the blade.</span></span> <span data-ttu-id="f8469-111">從 [概觀] 刀鋒視窗中，按一下以取得更詳細的圖表 (有「伺服器」之類的標題)，或按一下 [計量瀏覽器]，以開啟新的刀鋒視窗讓您建立自訂圖表。</span><span class="sxs-lookup"><span data-stu-id="f8469-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="f8469-112">時間範圍</span><span class="sxs-lookup"><span data-stu-id="f8469-112">Time range</span></span>
<span data-ttu-id="f8469-113">您可以在任何刀鋒視窗上變更圖表或格線涵蓋的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="f8469-113">You can change the Time range covered by the charts or grids on any blade.</span></span>

![開啟 Azure 入口網站中應用程式的 [概觀] 刀鋒視窗](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="f8469-115">如果您預期的部分資料尚未出現，請按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="f8469-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="f8469-116">圖表本身會定期重新整理，但是時間範圍越大，間隔時間會越長。</span><span class="sxs-lookup"><span data-stu-id="f8469-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span></span> <span data-ttu-id="f8469-117">資料從分析管線往圖表上顯示可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="f8469-117">It can take a while for data to come through the analysis pipeline onto a chart.</span></span>

<span data-ttu-id="f8469-118">若要放大圖表的局部，請拖曳過該部分︰</span><span class="sxs-lookup"><span data-stu-id="f8469-118">To zoom into part of a chart, drag over it:</span></span>

![拖曳過圖表的一部分。](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="f8469-120">按一下 [復原縮放] 按鈕可將它還原。</span><span class="sxs-lookup"><span data-stu-id="f8469-120">Click the Undo Zoom button to restore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="f8469-121">資料粒度和點值</span><span class="sxs-lookup"><span data-stu-id="f8469-121">Granularity and point values</span></span>
<span data-ttu-id="f8469-122">將滑鼠移至圖表上可顯示該點度量的值。</span><span class="sxs-lookup"><span data-stu-id="f8469-122">Hover your mouse over the chart to display the values of the metrics at that point.</span></span>

![將滑鼠移至圖表上](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="f8469-124">特定點的度量值會繼著前一個取樣間隔而彙總。</span><span class="sxs-lookup"><span data-stu-id="f8469-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span></span>

<span data-ttu-id="f8469-125">取樣間隔或「資料粒度」會顯示在刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="f8469-125">The sampling interval or "granularity" is shown at the top of the blade.</span></span>

![刀鋒視窗的標題。](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="f8469-127">您可以在時間範圍刀鋒視窗中調整資料粒度：</span><span class="sxs-lookup"><span data-stu-id="f8469-127">You can adjust the granularity in the Time range blade:</span></span>

![刀鋒視窗的標題。](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="f8469-129">可提供的資料粒度取決於您選取的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="f8469-129">The granularities available depend on the time range you select.</span></span> <span data-ttu-id="f8469-130">明確的資料粒度可替代時間範圍內的「自動」資料粒度。</span><span class="sxs-lookup"><span data-stu-id="f8469-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="f8469-131">編輯圖表和格線</span><span class="sxs-lookup"><span data-stu-id="f8469-131">Editing charts and grids</span></span>
<span data-ttu-id="f8469-132">若要對刀鋒視窗加入新圖表：</span><span class="sxs-lookup"><span data-stu-id="f8469-132">To add a new chart to the blade:</span></span>

![在 [計量瀏覽器] 中，選擇 [加入圖表]](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="f8469-134">選取現有或新圖表上的 [編輯]  來編輯其顯示的內容：</span><span class="sxs-lookup"><span data-stu-id="f8469-134">Select **Edit** on an existing or new chart to edit what it shows:</span></span>

![選取一或多個度量](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="f8469-136">您可以在圖表上顯示一個以上的度量，不過，可以一起顯示的組合有一些限制。</span><span class="sxs-lookup"><span data-stu-id="f8469-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span></span> <span data-ttu-id="f8469-137">只要您選取一個度量，便會停用某些其他度量。</span><span class="sxs-lookup"><span data-stu-id="f8469-137">As soon as you choose one metric, some of the others are disabled.</span></span>

<span data-ttu-id="f8469-138">如果您編寫[自訂度量][track]到您的應用程式 (對 TrackMetric 和 TrackEvent 呼叫)，會在這裡予以列出。</span><span class="sxs-lookup"><span data-stu-id="f8469-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="f8469-139">分段資料</span><span class="sxs-lookup"><span data-stu-id="f8469-139">Segment your data</span></span>
<span data-ttu-id="f8469-140">您可以依照屬性分割度量 - 例如，比較使用不同作業系統的用戶端上的頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="f8469-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span></span>

<span data-ttu-id="f8469-141">選取圖表或格線，將分組切換成開啟，並選取要分組依據的屬性：</span><span class="sxs-lookup"><span data-stu-id="f8469-141">Select a chart or grid, switch on grouping and pick a property to group by:</span></span>

![選取 [分組開啟]，然後在 [群組依據] 中選取屬性](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="f8469-143">當您使用群組時，[區域] 及 [橫條圖] 類型會提供堆疊的顯示。</span><span class="sxs-lookup"><span data-stu-id="f8469-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="f8469-144">這適合於 [彙總] 方法是 [加總] 的情況。</span><span class="sxs-lookup"><span data-stu-id="f8469-144">This is suitable where the Aggregation method is Sum.</span></span> <span data-ttu-id="f8469-145">但如果彙總類型是 [平均]，則選擇 [線條] 或[格線] 顯示類型。</span><span class="sxs-lookup"><span data-stu-id="f8469-145">But where the aggregation type is Average, choose the Line or Grid display types.</span></span>
>
>

<span data-ttu-id="f8469-146">如果您將自訂度量編寫至您的應用程式，並且它們包含[屬性值][track]，將可以在清單中選取屬性。</span><span class="sxs-lookup"><span data-stu-id="f8469-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span></span>

<span data-ttu-id="f8469-147">圖表是否對分段的資料來說太小？</span><span class="sxs-lookup"><span data-stu-id="f8469-147">Is the chart too small for segmented data?</span></span> <span data-ttu-id="f8469-148">調整其高度：</span><span class="sxs-lookup"><span data-stu-id="f8469-148">Adjust its height:</span></span>

![調整滑桿](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="f8469-150">彙總類型</span><span class="sxs-lookup"><span data-stu-id="f8469-150">Aggregation types</span></span>
<span data-ttu-id="f8469-151">旁邊的圖例通常預設會顯示圖表在這段期間的彙總值。</span><span class="sxs-lookup"><span data-stu-id="f8469-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span></span> <span data-ttu-id="f8469-152">如果您將滑鼠停留在圖表上，它會顯示在該點的值。</span><span class="sxs-lookup"><span data-stu-id="f8469-152">If you hover over the chart, it shows the value at that point.</span></span>

<span data-ttu-id="f8469-153">圖表上的每個資料點是在先前取樣間隔或「資料粒度」中所收到的資料值彙總。</span><span class="sxs-lookup"><span data-stu-id="f8469-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span></span> <span data-ttu-id="f8469-154">資料粒度會顯示在刀鋒視窗頂端，並隨著圖表的時幅而有所不同。</span><span class="sxs-lookup"><span data-stu-id="f8469-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span></span>

<span data-ttu-id="f8469-155">度量可以用不同方式彙總：</span><span class="sxs-lookup"><span data-stu-id="f8469-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="f8469-156">**計數**是在取樣間隔中接收到的事件計數。</span><span class="sxs-lookup"><span data-stu-id="f8469-156">**Count** is a count of the events received in the sampling interval.</span></span> <span data-ttu-id="f8469-157">它用於事件，例如要求。</span><span class="sxs-lookup"><span data-stu-id="f8469-157">It is used for events such as requests.</span></span> <span data-ttu-id="f8469-158">圖表的高度變化指出事件發生的速率變化。</span><span class="sxs-lookup"><span data-stu-id="f8469-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span></span> <span data-ttu-id="f8469-159">但請注意，數字的值會隨變更取樣間隔而變更。</span><span class="sxs-lookup"><span data-stu-id="f8469-159">But note that the numeric value changes when you change the sampling interval.</span></span>
* <span data-ttu-id="f8469-160">**總和** ：將取樣間隔或圖表期間收到的所有資料點的值相加。</span><span class="sxs-lookup"><span data-stu-id="f8469-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span></span>
* <span data-ttu-id="f8469-161">**平均** ：將總和除以間隔期間收到的資料點數目。</span><span class="sxs-lookup"><span data-stu-id="f8469-161">**Average** divides the Sum by the number of data points received over the interval.</span></span>
* <span data-ttu-id="f8469-162">**唯一** ：計數會用於使用者及帳戶的計數。</span><span class="sxs-lookup"><span data-stu-id="f8469-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="f8469-163">在取樣間隔或圖表期間，圖形顯示在該時間看到的不同使用者的計數。</span><span class="sxs-lookup"><span data-stu-id="f8469-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span></span>
* <span data-ttu-id="f8469-164">**%** - 每個彙總百分比版本只會搭配分段圖表使用。</span><span class="sxs-lookup"><span data-stu-id="f8469-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="f8469-165">總計永遠會加總至 100%，圖表會顯示總計的不同元件之相對貢獻。</span><span class="sxs-lookup"><span data-stu-id="f8469-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span></span>

    ![百分比彙總](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a><span data-ttu-id="f8469-167">變更彙總類型</span><span class="sxs-lookup"><span data-stu-id="f8469-167">Change the aggregation type</span></span>

![編輯圖表，然後選取彙總](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="f8469-169">當您建立新的圖表或所有度量皆已取消選取時，會顯示每個度量的預設方法：</span><span class="sxs-lookup"><span data-stu-id="f8469-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![取消選取所有度量以查看預設值](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="f8469-171">釘選 Y 軸</span><span class="sxs-lookup"><span data-stu-id="f8469-171">Pin Y-axis</span></span> 
<span data-ttu-id="f8469-172">根據預設，圖表會顯示資料範圍中從零到最大值的 Y 軸值，以提供值配量的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="f8469-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span></span> <span data-ttu-id="f8469-173">但是在某些超過配量的情況下，以視覺化方式檢查值的些微變化可能有興趣。</span><span class="sxs-lookup"><span data-stu-id="f8469-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span></span> <span data-ttu-id="f8469-174">對於類似這種的自訂，請使用 Y 軸範圍編輯功能，將 Y 軸的最小值或最大值釘選在所要的位置。</span><span class="sxs-lookup"><span data-stu-id="f8469-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="f8469-175">按一下 [進階設定] 核取方塊以顯示 [Y 軸範圍] 設定</span><span class="sxs-lookup"><span data-stu-id="f8469-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span></span>

![按一下 [進階設定]、選取 [自訂範圍]，然後指定最小值與最大值](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="f8469-177">篩選資料</span><span class="sxs-lookup"><span data-stu-id="f8469-177">Filter your data</span></span>
<span data-ttu-id="f8469-178">若只要查看選取的一組屬性值的度量：</span><span class="sxs-lookup"><span data-stu-id="f8469-178">To see just the metrics for a selected set of property values:</span></span>

![按一下 [篩選器]，然後檢查一些值](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="f8469-180">如果您不為特定屬性選取任何值，這與將它們全選相同：該屬性上沒有篩選器。</span><span class="sxs-lookup"><span data-stu-id="f8469-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="f8469-181">請注意每個屬性值旁的事件計數。</span><span class="sxs-lookup"><span data-stu-id="f8469-181">Notice the counts of events alongside each property value.</span></span> <span data-ttu-id="f8469-182">選取一個屬性的值時，會調整計數與其他屬性值。</span><span class="sxs-lookup"><span data-stu-id="f8469-182">When you select values of one property, the counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="f8469-183">篩選會套用至刀鋒視窗上的所有圖表。</span><span class="sxs-lookup"><span data-stu-id="f8469-183">Filters apply to all the charts on a blade.</span></span> <span data-ttu-id="f8469-184">如果您要將不同的篩選套用到不同的圖表，請建立並儲存不同的計量刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f8469-184">If you want different filters applied to different charts, create and save different metrics blades.</span></span> <span data-ttu-id="f8469-185">如果想要，您可以將不同刀鋒視窗中的圖表釘選到儀表板，以便並排查看兩者。</span><span class="sxs-lookup"><span data-stu-id="f8469-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="f8469-186">移除 Bot 和 Web 測試流量</span><span class="sxs-lookup"><span data-stu-id="f8469-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="f8469-187">使用篩選器**真實或綜合流量**並勾選**真實**。</span><span class="sxs-lookup"><span data-stu-id="f8469-187">Use the filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="f8469-188">您也可以依 **綜合流量的來源**篩選。</span><span class="sxs-lookup"><span data-stu-id="f8469-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="to-add-properties-to-the-filter-list"></a><span data-ttu-id="f8469-189">將屬性加入篩選器清單</span><span class="sxs-lookup"><span data-stu-id="f8469-189">To add properties to the filter list</span></span>
<span data-ttu-id="f8469-190">您要根據自己選擇的類別篩選遙測嗎？</span><span class="sxs-lookup"><span data-stu-id="f8469-190">Would you like to filter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="f8469-191">例如，您可能將使用者劃分成不同的類別，且您想要依照這些類別來分割資料。</span><span class="sxs-lookup"><span data-stu-id="f8469-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="f8469-192">[建立您自己的屬性](app-insights-api-custom-events-metrics.md#properties)。</span><span class="sxs-lookup"><span data-stu-id="f8469-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="f8469-193">在 [遙測初始設定式](app-insights-api-custom-events-metrics.md#defaults) 中設定，以使其顯示在所有遙測中 - 包括不同 SDK 模組所傳送的標準遙測。</span><span class="sxs-lookup"><span data-stu-id="f8469-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-the-chart-type"></a><span data-ttu-id="f8469-194">編輯圖表類型</span><span class="sxs-lookup"><span data-stu-id="f8469-194">Edit the chart type</span></span>
<span data-ttu-id="f8469-195">請注意您可以在格線與圖形之間切換：</span><span class="sxs-lookup"><span data-stu-id="f8469-195">Notice that you can switch between grids and graphs:</span></span>

![選取格線或圖表，然後選擇圖表類型](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="f8469-197">儲存您的度量刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="f8469-197">Save your metrics blade</span></span>
<span data-ttu-id="f8469-198">建立一些圖表後，請將它們儲存為我的最愛。</span><span class="sxs-lookup"><span data-stu-id="f8469-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="f8469-199">如果您使用組織帳戶，可以選擇是否要將它與他小組成員分享。</span><span class="sxs-lookup"><span data-stu-id="f8469-199">You can choose whether to share it with other team members, if you use an organizational account.</span></span>

![選擇 [我的最愛]](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="f8469-201">若要再次查看分頁，請 **前往 [概觀] 分頁** ，並開啟 [我的最愛]：</span><span class="sxs-lookup"><span data-stu-id="f8469-201">To see the blade again, **go to the overview blade** and open Favorites:</span></span>

![在 [概觀] 刀鋒視窗中，選擇 [我的最愛]](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="f8469-203">如果儲存時選擇「相對」時間範圍，會以最新度量更新刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f8469-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span></span> <span data-ttu-id="f8469-204">如果選擇「絕對」時間範圍，它會每次都顯示相同資料。</span><span class="sxs-lookup"><span data-stu-id="f8469-204">If you chose Absolute time range, it will show the same data every time.</span></span>

## <a name="reset-the-blade"></a><span data-ttu-id="f8469-205">重設刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="f8469-205">Reset the blade</span></span>
<span data-ttu-id="f8469-206">如果您編輯刀鋒視窗，但之後想要回到原始儲存的集合，只需要按一下 [重設]。</span><span class="sxs-lookup"><span data-stu-id="f8469-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span></span>

![在 [計量瀏覽器] 上方的按鈕中](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="f8469-208">即時計量串流</span><span class="sxs-lookup"><span data-stu-id="f8469-208">Live metrics stream</span></span>

<span data-ttu-id="f8469-209">如需更加立即的遙測檢視，請開啟[即時串流](app-insights-live-stream.md)。</span><span class="sxs-lookup"><span data-stu-id="f8469-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="f8469-210">因為彙總程序，大部分的計量需要數分鐘才會出現。</span><span class="sxs-lookup"><span data-stu-id="f8469-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span></span> <span data-ttu-id="f8469-211">相較之下，即時計量已針對低延遲進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="f8469-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="f8469-212">設定警示</span><span class="sxs-lookup"><span data-stu-id="f8469-212">Set alerts</span></span>
<span data-ttu-id="f8469-213">若要在任何度量有不尋常的值時收到電子郵件通知，請加入警示。</span><span class="sxs-lookup"><span data-stu-id="f8469-213">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="f8469-214">您可以選擇將電子郵件傳送給帳戶管理員，或傳送給特定的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="f8469-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![在 [計量瀏覽器] 中，選擇 [警示規則]，然後選擇 [加入警示]](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="f8469-216">[深入了解警示][alerts]。</span><span class="sxs-lookup"><span data-stu-id="f8469-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="f8469-217">連續匯出</span><span class="sxs-lookup"><span data-stu-id="f8469-217">Continuous Export</span></span>
<span data-ttu-id="f8469-218">如果您想要連續匯出資料，讓您能夠在外部加以處理，請考慮使用 [連續匯出](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="f8469-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="f8469-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="f8469-219">Power BI</span></span>
<span data-ttu-id="f8469-220">如果您希望更完整地檢視您的資料，您可以 [匯出至 Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8469-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="f8469-221">Analytics</span><span class="sxs-lookup"><span data-stu-id="f8469-221">Analytics</span></span>
<span data-ttu-id="f8469-222">[分析](app-insights-analytics.md) 是使用強大的查詢語言來分析遙測的更靈活方式。</span><span class="sxs-lookup"><span data-stu-id="f8469-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="f8469-223">如果您想要合併或計算計量的結果，或執行您應用程式近期效能的深入探索，請使用它。</span><span class="sxs-lookup"><span data-stu-id="f8469-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="f8469-224">從計量圖表中，您可以按一下 [分析] 圖示，直接前往對應的分析查詢。</span><span class="sxs-lookup"><span data-stu-id="f8469-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f8469-225">疑難排解</span><span class="sxs-lookup"><span data-stu-id="f8469-225">Troubleshooting</span></span>
<span data-ttu-id="f8469-226">*我看不到我的圖表上的任何資料。*</span><span class="sxs-lookup"><span data-stu-id="f8469-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="f8469-227">篩選會套用至刀鋒視窗上的所有圖表。</span><span class="sxs-lookup"><span data-stu-id="f8469-227">Filters apply to all the charts on the blade.</span></span> <span data-ttu-id="f8469-228">請確定，當您將焦點放在某個圖表時，您未在其他圖表上設定會排除所有資料的篩選。</span><span class="sxs-lookup"><span data-stu-id="f8469-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span></span>

    <span data-ttu-id="f8469-229">如果您想要在不同的圖表上設定不同的篩選，請在不同的刀鋒視窗中建立圖表，將它們儲存為個別的最愛圖表。</span><span class="sxs-lookup"><span data-stu-id="f8469-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="f8469-230">如果想要，您可以將這些圖表釘選到儀表板，以便並排查看兩者。</span><span class="sxs-lookup"><span data-stu-id="f8469-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="f8469-231">如果您依據計量上未定義的屬性將圖表分組，則圖表上不會有任何資料。</span><span class="sxs-lookup"><span data-stu-id="f8469-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span></span> <span data-ttu-id="f8469-232">請嘗試清除 [分組依據]，或選擇不同的群組屬性。</span><span class="sxs-lookup"><span data-stu-id="f8469-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="f8469-233">效能資料 (CPU、IO 速率等等) 適用於 Java Web 服務、Windows 傳統型應用程式、[IIS Web 應用程式和服務 (若您安裝狀態監視器)](app-insights-monitor-performance-live-website-now.md) 和 [Azure 雲端服務](app-insights-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="f8469-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="f8469-234">它不適用於 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="f8469-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="f8469-235">影片</span><span class="sxs-lookup"><span data-stu-id="f8469-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="f8469-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8469-236">Next steps</span></span>
* [<span data-ttu-id="f8469-237">使用 Application Insights 監視使用情況</span><span class="sxs-lookup"><span data-stu-id="f8469-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="f8469-238">使用診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="f8469-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
