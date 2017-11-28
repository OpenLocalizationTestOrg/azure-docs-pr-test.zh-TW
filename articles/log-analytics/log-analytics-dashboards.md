---
title: "aaaCreate Azure 記錄分析的自訂儀表板 |Microsoft 文件"
description: "本指南將協助您了解如何記錄分析儀表板可以視覺效果顯示所有儲存的記錄搜尋，提供您單一透鏡 tooview 您的環境。"
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
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="5d5da-103">建立用於 Log Analytics 中的自訂儀表板</span><span class="sxs-lookup"><span data-stu-id="5d5da-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="5d5da-104">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則您無法建立新的儀表板，或編輯現有的儀表板。</span><span class="sxs-lookup"><span data-stu-id="5d5da-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="5d5da-105">本指南將協助您了解如何記錄分析儀表板可以視覺效果顯示所有儲存的記錄搜尋，提供您單一透鏡 tooview 您的環境。</span><span class="sxs-lookup"><span data-stu-id="5d5da-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![範例儀表板](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="5d5da-107">所有 hello 自訂儀表板，您建立 hello OMS 入口網站中也都可用於 hello OMS 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d5da-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="5d5da-108">Hello 遵循頁面 hello 應用程式的詳細資訊，請參閱。</span><span class="sxs-lookup"><span data-stu-id="5d5da-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="5d5da-109">OMS hello Microsoft Store 從行動裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="5d5da-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="5d5da-110">Apple iTunes 中的 OMS 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="5d5da-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![行動儀表板](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="5d5da-112">如何建立儀表板？</span><span class="sxs-lookup"><span data-stu-id="5d5da-112">How do I create my dashboard?</span></span>
<span data-ttu-id="5d5da-113">toobegin 移 toohello OMS 概觀頁面。</span><span class="sxs-lookup"><span data-stu-id="5d5da-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="5d5da-114">您會看到 hello**我的儀表板**hello 左側的方塊。</span><span class="sxs-lookup"><span data-stu-id="5d5da-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="5d5da-115">它 toodrill 向下一直按到您的儀表板。</span><span class="sxs-lookup"><span data-stu-id="5d5da-115">Click it toodrill down into your dashboard.</span></span>

![概觀](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="5d5da-117">新增磚</span><span class="sxs-lookup"><span data-stu-id="5d5da-117">Adding a tile</span></span>
<span data-ttu-id="5d5da-118">在儀表板中，磚是由您儲存的記錄搜尋所形成。</span><span class="sxs-lookup"><span data-stu-id="5d5da-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="5d5da-119">OMS 內建許多預先儲存的記錄搜尋，讓您可以隨時開始。</span><span class="sxs-lookup"><span data-stu-id="5d5da-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="5d5da-120">如何使用 hello 下列步驟會該大綱 toobegin。</span><span class="sxs-lookup"><span data-stu-id="5d5da-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="5d5da-121">在 hello 我的儀表板檢視，只要按一下**自訂**tooenter 自訂模式。</span><span class="sxs-lookup"><span data-stu-id="5d5da-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![圖示](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="5d5da-123">開啟右邊 hello hello 頁面 hello 面板會顯示所有您的工作區儲存的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="5d5da-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="5d5da-124">toovisualize 儲存的記錄搜尋為圖格，將滑鼠停留在儲存的搜尋，然後按一下hello**加上**符號。</span><span class="sxs-lookup"><span data-stu-id="5d5da-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![新增磚 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="5d5da-126">當您按一下 hello**加上**符號、 新的磚會出現在 hello 我的儀表板檢視。</span><span class="sxs-lookup"><span data-stu-id="5d5da-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![新增磚 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="5d5da-128">編輯磚</span><span class="sxs-lookup"><span data-stu-id="5d5da-128">Edit a tile</span></span>
<span data-ttu-id="5d5da-129">在 hello 我的儀表板檢視，只要按一下**自訂**tooenter 自訂模式。</span><span class="sxs-lookup"><span data-stu-id="5d5da-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="5d5da-130">按一下您想要 tooedit hello 磚。</span><span class="sxs-lookup"><span data-stu-id="5d5da-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="5d5da-131">hello 右方面板變更 tooedit，並提供一組選項：</span><span class="sxs-lookup"><span data-stu-id="5d5da-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![編輯磚](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![編輯磚](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="5d5da-134">磚視覺效果</span><span class="sxs-lookup"><span data-stu-id="5d5da-134">Tile visualizations</span></span>
<span data-ttu-id="5d5da-135">有三種磚視覺效果 toochoose 從：</span><span class="sxs-lookup"><span data-stu-id="5d5da-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="5d5da-136">圖表類型</span><span class="sxs-lookup"><span data-stu-id="5d5da-136">chart type</span></span> | <span data-ttu-id="5d5da-137">作用</span><span class="sxs-lookup"><span data-stu-id="5d5da-137">what it does</span></span> |
| --- | --- |
| ![長條圖](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="5d5da-139">將已儲存之記錄搜尋結果的時間軸顯示為長條圖，或是依欄位顯示結果清單 (根據您的記錄搜尋是否根據欄位彙總結果而定)。</span><span class="sxs-lookup"><span data-stu-id="5d5da-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![計量](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="5d5da-141">在圖格中以數字顯示記錄搜尋結果總數。</span><span class="sxs-lookup"><span data-stu-id="5d5da-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="5d5da-142">度量磚可讓您 tooset 就磚發亮顯示 hello 達到 hello 閾值時的臨界值。</span><span class="sxs-lookup"><span data-stu-id="5d5da-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![線條](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="5d5da-144">將已儲存之記錄搜尋結果命中和值的時間軸顯示為折線圖。</span><span class="sxs-lookup"><span data-stu-id="5d5da-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="5d5da-145">閾值</span><span class="sxs-lookup"><span data-stu-id="5d5da-145">Threshold</span></span>
<span data-ttu-id="5d5da-146">您可以使用 hello 度量 」 視覺效果在磚上建立閾值。</span><span class="sxs-lookup"><span data-stu-id="5d5da-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="5d5da-147">選取上 toocreate hello 磚上的臨界值。</span><span class="sxs-lookup"><span data-stu-id="5d5da-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="5d5da-148">選擇是否 toohighlight hello 磚 hello 值高於或低於選擇的 hello 閾值時，然後設定下列 hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="5d5da-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="5d5da-149">組織 hello 儀表板</span><span class="sxs-lookup"><span data-stu-id="5d5da-149">Organizing hello dashboard</span></span>
<span data-ttu-id="5d5da-150">tooorganize 儀表板，瀏覽 toohello 我的儀表板檢視，然後按一下**自訂**tooenter 自訂模式。</span><span class="sxs-lookup"><span data-stu-id="5d5da-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="5d5da-151">按一下並拖曳您想 toomove，並將其移 toowhere 想磚 toobe hello 磚。</span><span class="sxs-lookup"><span data-stu-id="5d5da-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![排列儀表板](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="5d5da-153">移除磚</span><span class="sxs-lookup"><span data-stu-id="5d5da-153">Remove a tile</span></span>
<span data-ttu-id="5d5da-154">tooremove 磚，請瀏覽 toohello 我的儀表板檢視，然後按一下**自訂**tooenter 自訂模式。</span><span class="sxs-lookup"><span data-stu-id="5d5da-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="5d5da-155">選取 hello 磚 tooremove，然後在 hello 右面板上選取**移除磚**。</span><span class="sxs-lookup"><span data-stu-id="5d5da-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![移除磚](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="5d5da-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d5da-157">Next steps</span></span>
* <span data-ttu-id="5d5da-158">建立[警示](log-analytics-alerts.md)記錄分析 toogenerate 通知和 tooremediate 問題中。</span><span class="sxs-lookup"><span data-stu-id="5d5da-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
