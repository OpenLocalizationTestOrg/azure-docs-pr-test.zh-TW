---
title: "Azure Application Insights 中的 Web 應用程式效能變更智慧型診斷 | Microsoft Docs"
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
ms.openlocfilehash: 5e53bc714d89bf6204681349e7890e0b8fbc7046
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="84869-103">診斷您應用程式遙測資料中的突發變更</span><span class="sxs-lookup"><span data-stu-id="84869-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="84869-104">*這項功能處於預覽狀態。*</span><span class="sxs-lookup"><span data-stu-id="84869-104">*This feature is in preview.*</span></span>

<span data-ttu-id="84869-105">只要按一下，即可診斷您 Web 應用程式的效能或使用情況上的突發變更！</span><span class="sxs-lookup"><span data-stu-id="84869-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="84869-106">每當您在 [Application Insights](app-insights-overview.md) 的[分析](app-insights-analytics.md)中建立時間圖表時，都可以使用「智慧型診斷」功能。</span><span class="sxs-lookup"><span data-stu-id="84869-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="84869-107">每當您的結果趨勢有異常的變更 (例如突然增加或減少的情況) 時，「智慧型診斷」都會識別出可能解釋該變更原因之維度及相關值的模式。</span><span class="sxs-lookup"><span data-stu-id="84869-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="84869-108">這可協助您快速診斷問題。</span><span class="sxs-lookup"><span data-stu-id="84869-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="84869-109">在此範例中，「智慧型診斷」已識別出與變更相關之屬性值的模式，並醒目提示具有該模式的結果與沒有該模式的結果之間的差異：</span><span class="sxs-lookup"><span data-stu-id="84869-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![範例分析診斷結果](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="84869-111">診斷資料變更</span><span class="sxs-lookup"><span data-stu-id="84869-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="84869-112">在 [分析] 中執行查詢，並將它轉譯成時間圖表。</span><span class="sxs-lookup"><span data-stu-id="84869-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="84869-113">按一下任何醒目提示的尖峰點 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="84869-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![尖峰點](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="84869-115">診斷需要幾秒鐘的時間來探索模式。</span><span class="sxs-lookup"><span data-stu-id="84869-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="84869-116">[診斷結果] 索引標籤會顯示可能解釋您資料中斷原因的模式。</span><span class="sxs-lookup"><span data-stu-id="84869-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![結果](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="84869-118">文字會顯示看似與該變動相互關聯的維度值。</span><span class="sxs-lookup"><span data-stu-id="84869-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="84869-119">在此範例中，它是與特定的要求和特定的瀏覽器版本關聯。</span><span class="sxs-lookup"><span data-stu-id="84869-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="84869-120">另請注意，具有 True 和 False 篩選條件的兩個圖表元件。</span><span class="sxs-lookup"><span data-stu-id="84869-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="84869-121">False 元件顯示一個未變更的趨勢。</span><span class="sxs-lookup"><span data-stu-id="84869-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="84869-122">換句話說，如果我們將「診斷」已識別的問題維度組合排除，遙測結果中便沒有任何變更。</span><span class="sxs-lookup"><span data-stu-id="84869-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="84869-123">對照之下，該組合內的結果則在醒目提示的調查區域內顯示劇烈的變更。</span><span class="sxs-lookup"><span data-stu-id="84869-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="84869-124">這表示「診斷」已找到可解釋該變更原因的屬性組合。</span><span class="sxs-lookup"><span data-stu-id="84869-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="84869-125">如果模式相當複雜，您將需要把滑鼠指標停在 [全部顯示] 上來查看維度。</span><span class="sxs-lookup"><span data-stu-id="84869-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![全部顯示](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="84869-127">如果「診斷」找不到任何重要的模式來通知，就會顯示 [沒有結果] 頁面。</span><span class="sxs-lookup"><span data-stu-id="84869-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="84869-128">此時，您可以變更您的查詢。</span><span class="sxs-lookup"><span data-stu-id="84869-128">At this point, you may change your query.</span></span> <span data-ttu-id="84869-129">例如，您可以將 [分析] 查詢中的時間範圍和量化縮小，以供日後分析及可能獲得較佳的結果。</span><span class="sxs-lookup"><span data-stu-id="84869-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="84869-130">在知道您網站的特定頁面於特定瀏覽器上會發生問題之後，您現在可以直接移至問題頁面並調查最近的變更。</span><span class="sxs-lookup"><span data-stu-id="84869-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="84869-131">試用示範</span><span class="sxs-lookup"><span data-stu-id="84869-131">Try the demo</span></span>

<span data-ttu-id="84869-132">[按一下這裡以查看範例資料的相關示範](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H)。</span><span class="sxs-lookup"><span data-stu-id="84869-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="84869-133">運作方式</span><span class="sxs-lookup"><span data-stu-id="84869-133">How it works</span></span>

<span data-ttu-id="84869-134">「智慧型診斷」使用以 [DiffPatterns](app-insights-analytics-reference.md) 作業為基礎、不受監督的進階機器學習演算法。</span><span class="sxs-lookup"><span data-stu-id="84869-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="84869-135">它會尋找可能解釋資料變更原因的候選模式。</span><span class="sxs-lookup"><span data-stu-id="84869-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="84869-136">它會分析每個候選項目對計量的影響，並顯示與該變更最具相互關聯性的模式。</span><span class="sxs-lookup"><span data-stu-id="84869-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="84869-137">沒有任何診斷點？</span><span class="sxs-lookup"><span data-stu-id="84869-137">No diagnostic points?</span></span>

<span data-ttu-id="84869-138">只有在滿足下列條件的情況下，「智慧型診斷」才會運作：</span><span class="sxs-lookup"><span data-stu-id="84869-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="84869-139">已開啟 [智慧型診斷] 設定。</span><span class="sxs-lookup"><span data-stu-id="84869-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="84869-140">請查看 [分析] 中的 [設定] 圖示底下。</span><span class="sxs-lookup"><span data-stu-id="84869-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="84869-141">已選取 [分析] 設定中的 [智慧型診斷] 選項。</span><span class="sxs-lookup"><span data-stu-id="84869-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="84869-142">時間軸：圖表 X 軸的類型必須是 `datetime`。</span><span class="sxs-lookup"><span data-stu-id="84869-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="84869-143">折線圖或區域圖：診斷只有在這些類型的圖表才能運作。</span><span class="sxs-lookup"><span data-stu-id="84869-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="84869-144">請在您的查詢結尾使用 `| render timechart` 或 `| render areachart`；或從下拉式清單選取器中選取 [折線圖] 或 [區域圖]。</span><span class="sxs-lookup"><span data-stu-id="84869-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="84869-145">中斷：資料中必須有明顯的中斷。</span><span class="sxs-lookup"><span data-stu-id="84869-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="84869-146">有足夠的點可供分析。</span><span class="sxs-lookup"><span data-stu-id="84869-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="84869-147">查詢中的 summarize 子句不超過一個。</span><span class="sxs-lookup"><span data-stu-id="84869-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="84869-148">summarize 子句前面沒有任何包含名稱定義的 project 子句。</span><span class="sxs-lookup"><span data-stu-id="84869-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="84869-149">相關文章</span><span class="sxs-lookup"><span data-stu-id="84869-149">Related articles</span></span>

 * [<span data-ttu-id="84869-150">Analytics 教學課程</span><span class="sxs-lookup"><span data-stu-id="84869-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="84869-151">[智慧型偵測](app-insights-proactive-diagnostics.md)會自動向您發出效能問題警示。</span><span class="sxs-lookup"><span data-stu-id="84869-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>