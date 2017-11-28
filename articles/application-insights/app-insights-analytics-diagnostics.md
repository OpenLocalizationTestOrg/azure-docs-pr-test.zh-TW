---
title: "在 Azure Application Insights 中的 web 應用程式效能變更 aaaSmart 診斷 |Microsoft 文件"
description: "自動診斷您 Web 應用程式之效能遙測資料中的突然增加或段差情況。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="14efc-103">診斷您應用程式遙測資料中的突發變更</span><span class="sxs-lookup"><span data-stu-id="14efc-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="14efc-104">*這項功能處於預覽狀態。*</span><span class="sxs-lookup"><span data-stu-id="14efc-104">*This feature is in preview.*</span></span>

<span data-ttu-id="14efc-105">只要按一下，即可診斷您 Web 應用程式的效能或使用情況上的突發變更！</span><span class="sxs-lookup"><span data-stu-id="14efc-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="14efc-106">每當您建立在時間圖表時，會出現 hello 智慧的診斷功能[分析](app-insights-analytics.md)中[Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="14efc-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="14efc-107">無論與您的結果，例如高峰或 dip，hello 趨勢的不尋常變更智慧診斷會識別維度和相關聯的值可能會詳述 hello 變更的模式。</span><span class="sxs-lookup"><span data-stu-id="14efc-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="14efc-108">這可協助您快速診斷 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="14efc-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="14efc-109">在此範例中，智慧診斷已識別的 hello 變更相關聯的屬性值的模式，並反白顯示 hello 與不該模式的結果差異：</span><span class="sxs-lookup"><span data-stu-id="14efc-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![範例分析診斷結果](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="14efc-111">診斷資料變更</span><span class="sxs-lookup"><span data-stu-id="14efc-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="14efc-112">在 [分析] 中執行查詢，並將它轉譯成時間圖表。</span><span class="sxs-lookup"><span data-stu-id="14efc-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="14efc-113">按一下任何醒目提示的尖峰點 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="14efc-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![尖峰點](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="14efc-115">診斷需要幾秒鐘 toodiscover 模式。</span><span class="sxs-lookup"><span data-stu-id="14efc-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="14efc-116">hello 診斷結果索引標籤會顯示說明您的資料不一致的模式。</span><span class="sxs-lookup"><span data-stu-id="14efc-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![結果](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="14efc-118">hello 文字會顯示 hello 維度值出現 toocorrelate 與 hello shift 鍵。</span><span class="sxs-lookup"><span data-stu-id="14efc-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="14efc-119">在此範例中，它是與特定的要求和特定的瀏覽器版本關聯。</span><span class="sxs-lookup"><span data-stu-id="14efc-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="14efc-120">另請注意 hello 兩個元件的 hello 圖，其中 hello 篩選 true 和 false。</span><span class="sxs-lookup"><span data-stu-id="14efc-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="14efc-121">hello false 元件會顯示未變更的趨勢。</span><span class="sxs-lookup"><span data-stu-id="14efc-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="14efc-122">換句話說，沒有任何變更在 hello 遙測結果中，如果我們排除 hello 的診斷所識別的維度有問題的組合。</span><span class="sxs-lookup"><span data-stu-id="14efc-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="14efc-123">相反地，該組合中的 hello 結果並調查 hello 反白顯示區域內顯示重大的變更。</span><span class="sxs-lookup"><span data-stu-id="14efc-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="14efc-124">這會顯示診斷發現說明 hello 變更屬性的組合。</span><span class="sxs-lookup"><span data-stu-id="14efc-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="14efc-125">如果 hello 模式很複雜，您需要比 toohover**全部顯示**toosee hello 維度。</span><span class="sxs-lookup"><span data-stu-id="14efc-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![全部顯示](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="14efc-127">萬一診斷尋找有關 hello '沒有結果' 頁面將會呈現任何顯著的模式 toonotify。</span><span class="sxs-lookup"><span data-stu-id="14efc-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="14efc-128">此時，您可以變更您的查詢。</span><span class="sxs-lookup"><span data-stu-id="14efc-128">At this point, you may change your query.</span></span> <span data-ttu-id="14efc-129">例如，您可以縮小 hello 時間範圍和分類收納中分析查詢，進一步的分析和具有較好的結果。</span><span class="sxs-lookup"><span data-stu-id="14efc-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="14efc-130">特定的頁面上，您的網站發生問題，在特定瀏覽器上 hello 知識為利器，現在可以移至直線 toohello 問題頁面，並調查最近的變更。</span><span class="sxs-lookup"><span data-stu-id="14efc-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="14efc-131">請嘗試 hello 示範</span><span class="sxs-lookup"><span data-stu-id="14efc-131">Try hello demo</span></span>

<span data-ttu-id="14efc-132">[按一下這裡 toosee 示範](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H)針對取樣資料。</span><span class="sxs-lookup"><span data-stu-id="14efc-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="14efc-133">運作方式</span><span class="sxs-lookup"><span data-stu-id="14efc-133">How it works</span></span>

<span data-ttu-id="14efc-134">智慧診斷會使用進階不受監督的機器學習演算法根據 hello [DiffPatterns](app-insights-analytics-reference.md)作業。</span><span class="sxs-lookup"><span data-stu-id="14efc-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="14efc-135">看起來的候選模式，可能會詳述 hello 資料變更。</span><span class="sxs-lookup"><span data-stu-id="14efc-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="14efc-136">它會分析的每個候選位置 hello 度量 hello 影響，並顯示 hello 模式最佳相互關聯與 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="14efc-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="14efc-137">沒有任何診斷點？</span><span class="sxs-lookup"><span data-stu-id="14efc-137">No diagnostic points?</span></span>

<span data-ttu-id="14efc-138">當符合下列準則的 hello 時，只適用於智慧診斷：</span><span class="sxs-lookup"><span data-stu-id="14efc-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="14efc-139">已開啟 [智慧型診斷] 設定。</span><span class="sxs-lookup"><span data-stu-id="14efc-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="14efc-140">尋找在分析中的 hello 設定圖示下。</span><span class="sxs-lookup"><span data-stu-id="14efc-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="14efc-141">hello 智慧診斷 選項中分析設定為已選取。</span><span class="sxs-lookup"><span data-stu-id="14efc-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="14efc-142">時間軸： hello hello 圖表的 x 軸的類型必須是`datetime`。</span><span class="sxs-lookup"><span data-stu-id="14efc-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="14efc-143">折線圖或區域圖：診斷只有在這些類型的圖表才能運作。</span><span class="sxs-lookup"><span data-stu-id="14efc-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="14efc-144">使用`| render timechart`或`| render areachart`結尾 hello 您的查詢，或從 hello 下拉式清單選取器選取線條或區域圖。</span><span class="sxs-lookup"><span data-stu-id="14efc-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="14efc-145">不一致： Hello 資料中必須有重大的不一致。</span><span class="sxs-lookup"><span data-stu-id="14efc-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="14efc-146">足夠的點 tooanalyze。</span><span class="sxs-lookup"><span data-stu-id="14efc-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="14efc-147">不超過一個彙總 hello 查詢中的子句。</span><span class="sxs-lookup"><span data-stu-id="14efc-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="14efc-148">包含名稱定義 hello 之前沒有專案子句摘要子句。</span><span class="sxs-lookup"><span data-stu-id="14efc-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="14efc-149">相關文章</span><span class="sxs-lookup"><span data-stu-id="14efc-149">Related articles</span></span>

 * [<span data-ttu-id="14efc-150">Analytics 教學課程</span><span class="sxs-lookup"><span data-stu-id="14efc-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="14efc-151">[智慧偵測](app-insights-proactive-diagnostics.md)自動警示 tooperformance 問題。</span><span class="sxs-lookup"><span data-stu-id="14efc-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
