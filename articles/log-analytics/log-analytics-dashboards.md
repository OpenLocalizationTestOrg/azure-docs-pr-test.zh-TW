---
title: "在 Azure Log Analytics 中建立自訂的儀表板 | Microsoft Docs"
description: "本指南可幫助您了解 Log Analytics 儀表板如何以視覺效果顯示所有儲存的記錄搜尋，讓您以單一方式檢視您的環境。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a90d9c620221bffbb225fb060b997af2f5e90390
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="e1589-103">建立用於 Log Analytics 中的自訂儀表板</span><span class="sxs-lookup"><span data-stu-id="e1589-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="e1589-104">如果您的工作區已升級成[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則您無法建立新的儀表板，或編輯現有的儀表板。</span><span class="sxs-lookup"><span data-stu-id="e1589-104">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="e1589-105">本指南可幫助您了解 Log Analytics 儀表板如何以視覺效果顯示所有儲存的記錄搜尋，讓您以單一方式檢視您的環境。</span><span class="sxs-lookup"><span data-stu-id="e1589-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span></span>

![範例儀表板](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="e1589-107">您在 OMS 入口網站中建立的所有自訂儀表板，也都可在 OMS 行動應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="e1589-107">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span></span> <span data-ttu-id="e1589-108">如需應用程式的詳細資訊，請參閱下列頁面。</span><span class="sxs-lookup"><span data-stu-id="e1589-108">See the following pages for more information about the apps.</span></span>

* [<span data-ttu-id="e1589-109">Microsoft Store 中的 OMS 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="e1589-109">OMS mobile app from the Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="e1589-110">Apple iTunes 中的 OMS 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="e1589-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![行動儀表板](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="e1589-112">如何建立儀表板？</span><span class="sxs-lookup"><span data-stu-id="e1589-112">How do I create my dashboard?</span></span>
<span data-ttu-id="e1589-113">若要開始，請移至 OMS [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="e1589-113">To begin, go to the OMS Overview page.</span></span> <span data-ttu-id="e1589-114">您會在左側看到 [我的儀表板] 圖格。</span><span class="sxs-lookup"><span data-stu-id="e1589-114">You'll see the **My Dashboard** tile on the left.</span></span> <span data-ttu-id="e1589-115">按一下磚，可向下鑽研儀表板。</span><span class="sxs-lookup"><span data-stu-id="e1589-115">Click it to drill down into your dashboard.</span></span>

![概觀](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="e1589-117">新增磚</span><span class="sxs-lookup"><span data-stu-id="e1589-117">Adding a tile</span></span>
<span data-ttu-id="e1589-118">在儀表板中，磚是由您儲存的記錄搜尋所形成。</span><span class="sxs-lookup"><span data-stu-id="e1589-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="e1589-119">OMS 內建許多預先儲存的記錄搜尋，讓您可以隨時開始。</span><span class="sxs-lookup"><span data-stu-id="e1589-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="e1589-120">使用下列步驟來大致了解如何開始。</span><span class="sxs-lookup"><span data-stu-id="e1589-120">Use the following steps that outline how to begin.</span></span>

<span data-ttu-id="e1589-121">在 [我的儀表板] 檢視中，直接按一下 [自訂] 進入自訂模式。</span><span class="sxs-lookup"><span data-stu-id="e1589-121">In the My Dashboard view, simply click **Customize** to enter customize mode.</span></span>

![圖示](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="e1589-123">在頁面右側開啟的面板會顯示工作區所有儲存的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="e1589-123">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="e1589-124">若要以圖格來呈現已儲存的記錄搜尋，請將滑鼠停留在已儲存的搜尋，然後按一下**加號**符號。</span><span class="sxs-lookup"><span data-stu-id="e1589-124">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span></span>

![新增磚 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="e1589-126">當您按一下**加號**符號時，[我的儀表板] 檢視中會出現新的圖格。</span><span class="sxs-lookup"><span data-stu-id="e1589-126">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span></span>

![新增磚 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="e1589-128">編輯磚</span><span class="sxs-lookup"><span data-stu-id="e1589-128">Edit a tile</span></span>
<span data-ttu-id="e1589-129">在 [我的儀表板] 檢視中，直接按一下 [自訂] 進入自訂模式。</span><span class="sxs-lookup"><span data-stu-id="e1589-129">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span></span> <span data-ttu-id="e1589-130">按一下您想要編輯的磚。</span><span class="sxs-lookup"><span data-stu-id="e1589-130">Click the tile you want to edit.</span></span> <span data-ttu-id="e1589-131">右側面板即會變更為可編輯狀態，並提供一組選項：</span><span class="sxs-lookup"><span data-stu-id="e1589-131">The right panel changes to edit, and gives a selection of options:</span></span>

![編輯磚](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![編輯磚](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="e1589-134">磚視覺效果</span><span class="sxs-lookup"><span data-stu-id="e1589-134">Tile visualizations</span></span>
<span data-ttu-id="e1589-135">有三種圖格視覺效果可供您選擇：</span><span class="sxs-lookup"><span data-stu-id="e1589-135">There are three kinds of tile visualizations to choose from:</span></span>

| <span data-ttu-id="e1589-136">圖表類型</span><span class="sxs-lookup"><span data-stu-id="e1589-136">chart type</span></span> | <span data-ttu-id="e1589-137">作用</span><span class="sxs-lookup"><span data-stu-id="e1589-137">what it does</span></span> |
| --- | --- |
| ![長條圖](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="e1589-139">將已儲存之記錄搜尋結果的時間軸顯示為長條圖，或是依欄位顯示結果清單 (根據您的記錄搜尋是否根據欄位彙總結果而定)。</span><span class="sxs-lookup"><span data-stu-id="e1589-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![計量](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="e1589-141">在圖格中以數字顯示記錄搜尋結果總數。</span><span class="sxs-lookup"><span data-stu-id="e1589-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="e1589-142">度量磚可讓您設定一個閾值，當達到該閾值時就讓磚發亮顯示。</span><span class="sxs-lookup"><span data-stu-id="e1589-142">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span></span> |
| ![線條](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="e1589-144">將已儲存之記錄搜尋結果命中和值的時間軸顯示為折線圖。</span><span class="sxs-lookup"><span data-stu-id="e1589-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="e1589-145">閾值</span><span class="sxs-lookup"><span data-stu-id="e1589-145">Threshold</span></span>
<span data-ttu-id="e1589-146">您可以使用「度量」視覺效果在磚上建立閾值。</span><span class="sxs-lookup"><span data-stu-id="e1589-146">You can create a threshold on a tile using the Metric visualization.</span></span> <span data-ttu-id="e1589-147">請選取磚，在磚上建立閾值。</span><span class="sxs-lookup"><span data-stu-id="e1589-147">Select on to create a threshold value on the tile.</span></span> <span data-ttu-id="e1589-148">選擇是否要在值高於或低於選擇的閾值時讓磚發亮顯示，然後在下面設定閾值。</span><span class="sxs-lookup"><span data-stu-id="e1589-148">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span></span>

## <a name="organizing-the-dashboard"></a><span data-ttu-id="e1589-149">排列儀表板</span><span class="sxs-lookup"><span data-stu-id="e1589-149">Organizing the dashboard</span></span>
<span data-ttu-id="e1589-150">若要排列儀表板，請瀏覽到 [我的儀表板] 檢視，然後按一下 [自訂] 進入自訂模式。</span><span class="sxs-lookup"><span data-stu-id="e1589-150">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="e1589-151">按一下並拖曳您想要移動的磚，然後將磚移動到您想要的位置。</span><span class="sxs-lookup"><span data-stu-id="e1589-151">Click and drag the tile you want to move, and move it to where you want your tile to be.</span></span>

![排列儀表板](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="e1589-153">移除磚</span><span class="sxs-lookup"><span data-stu-id="e1589-153">Remove a tile</span></span>
<span data-ttu-id="e1589-154">若要移除圖格，請瀏覽到 [我的儀表板] 檢視，然後按一下 [自訂] 進入自訂模式。</span><span class="sxs-lookup"><span data-stu-id="e1589-154">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="e1589-155">選取您想要移除的圖格，然後在右側面板上選取 [移除圖格] 。</span><span class="sxs-lookup"><span data-stu-id="e1589-155">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span></span>

![移除磚](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="e1589-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1589-157">Next steps</span></span>
* <span data-ttu-id="e1589-158">在 Log Analytics 中建立[警示](log-analytics-alerts.md)，以產生通知並修復問題。</span><span class="sxs-lookup"><span data-stu-id="e1589-158">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span></span>
