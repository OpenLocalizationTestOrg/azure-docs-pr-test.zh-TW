---
title: "aaaExploring 中 Azure Application Insights 計量 |Microsoft 文件"
description: "Toointerpret 圖上度量總管 中，以及如何 toocustomize 度量總管刀鋒視窗。"
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
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="38e8f-103">在 Application Insights 中探索度量</span><span class="sxs-lookup"><span data-stu-id="38e8f-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="38e8f-104">[Application Insights][start] 中的度量為從您的應用程式傳送的遙測中的測量值和事件計數。</span><span class="sxs-lookup"><span data-stu-id="38e8f-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="38e8f-105">它們幫助您偵測效能問題，並觀察使用應用程式方式的趨勢。</span><span class="sxs-lookup"><span data-stu-id="38e8f-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="38e8f-106">標準度量的範圍很廣泛，而您也可以建立自己的自訂度量和事件。</span><span class="sxs-lookup"><span data-stu-id="38e8f-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="38e8f-107">度量和事件計數會顯示在彙總值 (例如總和、平均或計數) 的圖表中。</span><span class="sxs-lookup"><span data-stu-id="38e8f-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="38e8f-108">以下是一組範例圖表︰</span><span class="sxs-lookup"><span data-stu-id="38e8f-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="38e8f-109">Hello Application Insights 入口網站中找到 everywhere 度量圖表。</span><span class="sxs-lookup"><span data-stu-id="38e8f-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="38e8f-110">在大部分情況下，可以自訂它們，，您可以加入多個圖表 toohello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="38e8f-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="38e8f-111">從 hello 概觀刀鋒視窗中，按一下 透過 toomore 詳細的圖表 （其中的標題，例如 「 伺服器 」），或按一下**計量瀏覽器**tooopen 您可以在其中建立自訂圖表的新刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="38e8f-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="38e8f-112">時間範圍</span><span class="sxs-lookup"><span data-stu-id="38e8f-112">Time range</span></span>
<span data-ttu-id="38e8f-113">您可以變更 hello hello 圖表或任何刀鋒視窗上的資料格中所涵蓋的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="38e8f-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![開啟 hello 概觀刀鋒視窗中的 hello Azure 入口網站中的應用程式](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="38e8f-115">如果您預期的部分資料尚未出現，請按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="38e8f-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="38e8f-116">圖表重新整理它們自己的間隔，但 hello 間隔更大的時間範圍較長時間。</span><span class="sxs-lookup"><span data-stu-id="38e8f-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="38e8f-117">它可以拖曳至圖表，需要一些時間，資料 toocome hello 分析管線。</span><span class="sxs-lookup"><span data-stu-id="38e8f-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="38e8f-118">toozoom 入部分圖表中，拖曳它：</span><span class="sxs-lookup"><span data-stu-id="38e8f-118">toozoom into part of a chart, drag over it:</span></span>

![拖曳過圖表的一部分。](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="38e8f-120">按一下 hello 復原縮放按鈕 toorestore 它。</span><span class="sxs-lookup"><span data-stu-id="38e8f-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="38e8f-121">資料粒度和點值</span><span class="sxs-lookup"><span data-stu-id="38e8f-121">Granularity and point values</span></span>
<span data-ttu-id="38e8f-122">此時將滑鼠游標移 hello 圖表 toodisplay hello hello 度量值。</span><span class="sxs-lookup"><span data-stu-id="38e8f-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Hello 滑鼠停留在圖表](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="38e8f-124">在特定時間點的 hello 標準 hello 值是進行彙總 hello 前面取樣間隔。</span><span class="sxs-lookup"><span data-stu-id="38e8f-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="38e8f-125">hello 取樣間隔時間內或 「 資料粒度 」 會顯示在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="38e8f-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![刀鋒視窗中的 hello 標頭。](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="38e8f-127">您可以調整 hello 時間範圍 刀鋒視窗中的資料粒度 hello:</span><span class="sxs-lookup"><span data-stu-id="38e8f-127">You can adjust hello granularity in hello Time range blade:</span></span>

![刀鋒視窗中的 hello 標頭。](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="38e8f-129">hello 資料粒度可用取決於您所選取的 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="38e8f-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="38e8f-130">hello 明確的資料粒度是替代項目 toohello 「 自動 」 資料粒度的 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="38e8f-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="38e8f-131">編輯圖表和格線</span><span class="sxs-lookup"><span data-stu-id="38e8f-131">Editing charts and grids</span></span>
<span data-ttu-id="38e8f-132">tooadd 新的圖表 toohello 刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="38e8f-132">tooadd a new chart toohello blade:</span></span>

![在 [計量瀏覽器] 中，選擇 [加入圖表]](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="38e8f-134">選取**編輯**上現有或新的圖表 tooedit 什麼它會顯示：</span><span class="sxs-lookup"><span data-stu-id="38e8f-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![選取一或多個度量](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="38e8f-136">雖然可以一起顯示的 hello 組合的限制，您可以在圖表上，顯示多個度量。</span><span class="sxs-lookup"><span data-stu-id="38e8f-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="38e8f-137">當您選擇一個計量，某些 hello 其他人已停用。</span><span class="sxs-lookup"><span data-stu-id="38e8f-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="38e8f-138">如果您已編碼[自訂度量][ track]到應用程式 （呼叫 tooTrackMetric 和 TrackEvent） 就會列在此處。</span><span class="sxs-lookup"><span data-stu-id="38e8f-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="38e8f-139">分段資料</span><span class="sxs-lookup"><span data-stu-id="38e8f-139">Segment your data</span></span>
<span data-ttu-id="38e8f-140">您可以分割度量屬性-例如，toocompare 頁面檢視因不同作業系統的用戶端上。</span><span class="sxs-lookup"><span data-stu-id="38e8f-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="38e8f-141">選取圖表或格線、 切換群組，並挑選由屬性 toogroup:</span><span class="sxs-lookup"><span data-stu-id="38e8f-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![選取 [分組開啟]，然後在 [群組依據] 中選取屬性](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="38e8f-143">當您使用群組時，則 hello 區域和橫條圖類型會提供堆疊的顯示。</span><span class="sxs-lookup"><span data-stu-id="38e8f-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="38e8f-144">這是適合其中 hello 彙總方法為 Sum。</span><span class="sxs-lookup"><span data-stu-id="38e8f-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="38e8f-145">但是 hello 彙總類型的平均，選擇 hello 線條或格線顯示的型別。</span><span class="sxs-lookup"><span data-stu-id="38e8f-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="38e8f-146">如果您已編碼[自訂度量][ track]到應用程式和包含屬性值，您將無法 tooselect hello 清單中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="38e8f-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="38e8f-147">是 hello 圖太小，分割的資料嗎？</span><span class="sxs-lookup"><span data-stu-id="38e8f-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="38e8f-148">調整其高度：</span><span class="sxs-lookup"><span data-stu-id="38e8f-148">Adjust its height:</span></span>

![調整 hello 滑桿](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="38e8f-150">彙總類型</span><span class="sxs-lookup"><span data-stu-id="38e8f-150">Aggregation types</span></span>
<span data-ttu-id="38e8f-151">在預設的 hello 端 hello 圖例通常會顯示彙總的 hello 值段 hello hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="38e8f-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="38e8f-152">如果您將滑鼠停留在 hello 圖表，則會在該點顯示 hello 值。</span><span class="sxs-lookup"><span data-stu-id="38e8f-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="38e8f-153">Hello 圖表上的每個資料點是收到 hello 上述取樣間隔或 「 資料粒度 」 中的 hello 資料值的彙總。</span><span class="sxs-lookup"><span data-stu-id="38e8f-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="38e8f-154">hello 資料粒度會顯示在頂端 hello hello 刀鋒視窗中，而且隨著 hello hello 圖表的整體的時幅。</span><span class="sxs-lookup"><span data-stu-id="38e8f-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="38e8f-155">度量可以用不同方式彙總：</span><span class="sxs-lookup"><span data-stu-id="38e8f-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="38e8f-156">**計數**是收到 hello 取樣間隔中的 hello 事件的計數。</span><span class="sxs-lookup"><span data-stu-id="38e8f-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="38e8f-157">它用於事件，例如要求。</span><span class="sxs-lookup"><span data-stu-id="38e8f-157">It is used for events such as requests.</span></span> <span data-ttu-id="38e8f-158">Hello 高度 hello 圖的變化表示 hello 速率 hello 事件就會發生變化。</span><span class="sxs-lookup"><span data-stu-id="38e8f-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="38e8f-159">但請注意，hello 數字的值變更時變更 hello 取樣間隔。</span><span class="sxs-lookup"><span data-stu-id="38e8f-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="38e8f-160">**Sum**加總 hello 收到 hello 取樣間隔內或 hello 段 hello 圖表上的所有 hello 資料點的值。</span><span class="sxs-lookup"><span data-stu-id="38e8f-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="38e8f-161">**平均**除以 hello 的 hello 收到 hello 間隔內的資料點的數目總和。</span><span class="sxs-lookup"><span data-stu-id="38e8f-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="38e8f-162">**唯一** ：計數會用於使用者及帳戶的計數。</span><span class="sxs-lookup"><span data-stu-id="38e8f-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="38e8f-163">Hello 取樣間隔期間或在 hello 段 hello 圖表，hello 圖會顯示不同的使用者出現在該時間的 hello 計數。</span><span class="sxs-lookup"><span data-stu-id="38e8f-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="38e8f-164">**%** - 每個彙總百分比版本只會搭配分段圖表使用。</span><span class="sxs-lookup"><span data-stu-id="38e8f-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="38e8f-165">too100%加總 hello 和 hello 圖表可顯示總計的不同元件的 hello 相對比重。</span><span class="sxs-lookup"><span data-stu-id="38e8f-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![百分比彙總](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="38e8f-167">變更 hello 彙總類型</span><span class="sxs-lookup"><span data-stu-id="38e8f-167">Change hello aggregation type</span></span>

![編輯 hello 圖表，然後選取 彙總](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="38e8f-169">當您建立新的圖表，或當所有的度量資訊會被取消選取時，會顯示 hello 預設方法，針對每個標準：</span><span class="sxs-lookup"><span data-stu-id="38e8f-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![取消選取所有度量 toosee hello 預設值](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="38e8f-171">釘選 Y 軸</span><span class="sxs-lookup"><span data-stu-id="38e8f-171">Pin Y-axis</span></span> 
<span data-ttu-id="38e8f-172">根據預設圖表可顯示 Y 軸值從零到 hello 資料範圍，toogive hello 值的配量的視覺表示法中的最大值為止。</span><span class="sxs-lookup"><span data-stu-id="38e8f-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="38e8f-173">但在某些情況下以上 hello 配量可能很有趣 toovisually 檢查值的些微變更。</span><span class="sxs-lookup"><span data-stu-id="38e8f-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="38e8f-174">針對自訂類似此使用 hello y 軸範圍編輯功能 toopin hello y 軸最小值或最大值所需的位置。</span><span class="sxs-lookup"><span data-stu-id="38e8f-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="38e8f-175">按一下 [進階設定] 核取方塊 toobring 向上 hello y 軸範圍設定</span><span class="sxs-lookup"><span data-stu-id="38e8f-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![按一下 [進階設定]、選取 [自訂範圍]，然後指定最小值與最大值](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="38e8f-177">篩選資料</span><span class="sxs-lookup"><span data-stu-id="38e8f-177">Filter your data</span></span>
<span data-ttu-id="38e8f-178">將選取的屬性值的 toosee 只 hello 度量：</span><span class="sxs-lookup"><span data-stu-id="38e8f-178">toosee just hello metrics for a selected set of property values:</span></span>

![按一下 [篩選器]，然後檢查一些值](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="38e8f-180">如果您沒有選取任何特定屬性的值，它具有 hello 相同選取全部： 內容上沒有任何篩選條件。</span><span class="sxs-lookup"><span data-stu-id="38e8f-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="38e8f-181">請注意 hello 計算的事件，連同每個屬性值。</span><span class="sxs-lookup"><span data-stu-id="38e8f-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="38e8f-182">當您選取一個屬性的值時，hello 計算以及其他屬性的值會進行調整。</span><span class="sxs-lookup"><span data-stu-id="38e8f-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="38e8f-183">篩選會在刀鋒視窗上套用 tooall hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="38e8f-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="38e8f-184">如果您想要不同的篩選器套用 toodifferent 圖表，建立並儲存不同的度量資訊的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="38e8f-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="38e8f-185">如果您想要可以使您可以看到它們彼此釘選不同刀鋒 toohello 儀表板的圖表。</span><span class="sxs-lookup"><span data-stu-id="38e8f-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="38e8f-186">移除 Bot 和 Web 測試流量</span><span class="sxs-lookup"><span data-stu-id="38e8f-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="38e8f-187">使用 hello 篩選**即時或綜合流量**並檢查**真實**。</span><span class="sxs-lookup"><span data-stu-id="38e8f-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="38e8f-188">您也可以依 **綜合流量的來源**篩選。</span><span class="sxs-lookup"><span data-stu-id="38e8f-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="38e8f-189">tooadd 屬性 toohello 篩選器清單</span><span class="sxs-lookup"><span data-stu-id="38e8f-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="38e8f-190">您希望您自己選擇的類別 toofilter 遙測？</span><span class="sxs-lookup"><span data-stu-id="38e8f-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="38e8f-191">例如，您可能將使用者劃分成不同的類別，且您想要依照這些類別來分割資料。</span><span class="sxs-lookup"><span data-stu-id="38e8f-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="38e8f-192">[建立您自己的屬性](app-insights-api-custom-events-metrics.md#properties)。</span><span class="sxs-lookup"><span data-stu-id="38e8f-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="38e8f-193">設定[遙測初始設定式](app-insights-api-custom-events-metrics.md#defaults)toohave 它出現在所有遙測-包括 hello 標準遙測傳送的不同 SDK 模組。</span><span class="sxs-lookup"><span data-stu-id="38e8f-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="38e8f-194">編輯 hello 圖表類型</span><span class="sxs-lookup"><span data-stu-id="38e8f-194">Edit hello chart type</span></span>
<span data-ttu-id="38e8f-195">請注意您可以在格線與圖形之間切換：</span><span class="sxs-lookup"><span data-stu-id="38e8f-195">Notice that you can switch between grids and graphs:</span></span>

![選取格線或圖表，然後選擇圖表類型](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="38e8f-197">儲存您的度量刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="38e8f-197">Save your metrics blade</span></span>
<span data-ttu-id="38e8f-198">建立一些圖表後，請將它們儲存為我的最愛。</span><span class="sxs-lookup"><span data-stu-id="38e8f-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="38e8f-199">您可以選擇是否 tooshare 它與其他小組成員，如果您使用組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="38e8f-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![選擇 [我的最愛]](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="38e8f-201">同樣地，toosee hello 刀鋒視窗**移 toohello 概觀刀鋒視窗**並開啟 [我的最愛]:</span><span class="sxs-lookup"><span data-stu-id="38e8f-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![在 hello 概觀刀鋒視窗中，選擇 我的最愛](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="38e8f-203">如果您儲存時，您可以選擇相對的時間範圍，將會與 hello 最新度量更新 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="38e8f-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="38e8f-204">如果您選擇的絕對時間範圍，它會顯示 hello 每次相同的資料。</span><span class="sxs-lookup"><span data-stu-id="38e8f-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="38e8f-205">重設 hello 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="38e8f-205">Reset hello blade</span></span>
<span data-ttu-id="38e8f-206">如果您編輯刀鋒視窗，但您希望然後 tooget 後 toohello 原始儲存集，只要按一下 重設。</span><span class="sxs-lookup"><span data-stu-id="38e8f-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![在頂端的公制總管 hello hello 按鈕](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="38e8f-208">即時計量串流</span><span class="sxs-lookup"><span data-stu-id="38e8f-208">Live metrics stream</span></span>

<span data-ttu-id="38e8f-209">如需更加立即的遙測檢視，請開啟[即時串流](app-insights-live-stream.md)。</span><span class="sxs-lookup"><span data-stu-id="38e8f-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="38e8f-210">大部分的度量資訊會需要幾分鐘的時間 tooappear，因為 hello 處理序的彙總。</span><span class="sxs-lookup"><span data-stu-id="38e8f-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="38e8f-211">相較之下，即時計量已針對低延遲進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="38e8f-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="38e8f-212">設定警示</span><span class="sxs-lookup"><span data-stu-id="38e8f-212">Set alerts</span></span>
<span data-ttu-id="38e8f-213">收到的異常值的任何度量，電子郵件通知的 toobe 加入警示。</span><span class="sxs-lookup"><span data-stu-id="38e8f-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="38e8f-214">您可以選擇 toosend hello 電子郵件 toohello 帳戶系統管理員或 toospecific 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="38e8f-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![在 [計量瀏覽器] 中，選擇 [警示規則]，然後選擇 [加入警示]](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="38e8f-216">[深入了解警示][alerts]。</span><span class="sxs-lookup"><span data-stu-id="38e8f-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="38e8f-217">連續匯出</span><span class="sxs-lookup"><span data-stu-id="38e8f-217">Continuous Export</span></span>
<span data-ttu-id="38e8f-218">如果您想要連續匯出資料，讓您能夠在外部加以處理，請考慮使用 [連續匯出](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="38e8f-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="38e8f-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="38e8f-219">Power BI</span></span>
<span data-ttu-id="38e8f-220">如果您想要有更豐富您的資料檢視，您可以[匯出 tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx)。</span><span class="sxs-lookup"><span data-stu-id="38e8f-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="38e8f-221">Analytics</span><span class="sxs-lookup"><span data-stu-id="38e8f-221">Analytics</span></span>
<span data-ttu-id="38e8f-222">[分析](app-insights-analytics.md)是更具彈性的方式 tooanalyze 您使用強大的查詢語言的遙測。</span><span class="sxs-lookup"><span data-stu-id="38e8f-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="38e8f-223">如果您想 toocombine 或計算結果的度量，或執行您的應用程式最近效能的深入瀏覽，請使用它。</span><span class="sxs-lookup"><span data-stu-id="38e8f-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="38e8f-224">從度量的圖表，您可以按一下 hello 分析圖示 tooget 直接 toohello 相等分析查詢。</span><span class="sxs-lookup"><span data-stu-id="38e8f-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="38e8f-225">疑難排解</span><span class="sxs-lookup"><span data-stu-id="38e8f-225">Troubleshooting</span></span>
<span data-ttu-id="38e8f-226">*我看不到我的圖表上的任何資料。*</span><span class="sxs-lookup"><span data-stu-id="38e8f-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="38e8f-227">篩選會套用 tooall hello 圖表 hello 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="38e8f-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="38e8f-228">請確定，而您要將焦點放在圖表上，您未設定排除在另一台的所有 hello 資料的篩選。</span><span class="sxs-lookup"><span data-stu-id="38e8f-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="38e8f-229">如果您想在不同的圖表上 tooset 不同的篩選器，建立它們在不同的刀鋒視窗，將它們儲存成個別的 [我的最愛]。</span><span class="sxs-lookup"><span data-stu-id="38e8f-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="38e8f-230">如果您想，您可以將其釘選 toohello 儀表板，讓您可以看到它們彼此。</span><span class="sxs-lookup"><span data-stu-id="38e8f-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="38e8f-231">如果您未在 hello 度量定義的屬性來分組圖表，然後將不會有 hello 圖表上。</span><span class="sxs-lookup"><span data-stu-id="38e8f-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="38e8f-232">請嘗試清除 [分組依據]，或選擇不同的群組屬性。</span><span class="sxs-lookup"><span data-stu-id="38e8f-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="38e8f-233">效能資料 (CPU、IO 速率等等) 適用於 Java Web 服務、Windows 傳統型應用程式、[IIS Web 應用程式和服務 (若您安裝狀態監視器)](app-insights-monitor-performance-live-website-now.md) 和 [Azure 雲端服務](app-insights-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="38e8f-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="38e8f-234">它不適用於 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="38e8f-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="38e8f-235">影片</span><span class="sxs-lookup"><span data-stu-id="38e8f-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="38e8f-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38e8f-236">Next steps</span></span>
* [<span data-ttu-id="38e8f-237">使用 Application Insights 監視使用情況</span><span class="sxs-lookup"><span data-stu-id="38e8f-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="38e8f-238">使用診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="38e8f-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
