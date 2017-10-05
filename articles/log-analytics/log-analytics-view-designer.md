---
title: "在 OMS Log Analytics 中建立檢視以分析資料 | Microsoft Docs"
description: "Log Analytics 中的檢視設計工具可讓您建立要在 OMS 和 Azure 入口網站中顯示的自訂檢視，以及包含 OMS 存放庫中不同資料的視覺效果。 本文包含檢視設計工具的概觀以及建立和編輯自訂檢視的程序。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: e3c463d749dc4179df58286b9bb75584880a6bc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-view-designer-to-create-custom-views-in-log-analytics"></a><span data-ttu-id="c69c9-104">在 Log Analytics 中使用檢視表設計工具來建立自訂檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-104">Use View Designer to create custom views in Log Analytics</span></span>
<span data-ttu-id="c69c9-105">[Log Analytics](log-analytics-overview.md) 中的檢視設計工具可讓您在 OMS 主控台中建立自訂檢視，其中包含 OMS 存放庫中不同資料的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c69c9-105">The View Designer in [Log Analytics](log-analytics-overview.md) allows you to create custom views in the OMS console that contain different visualizations of data in the OMS repository.</span></span> <span data-ttu-id="c69c9-106">本文包含檢視設計工具的概觀以及建立和編輯自訂檢視的程序。</span><span class="sxs-lookup"><span data-stu-id="c69c9-106">This article contains an overview of View Designer and procedures for creating and editing custom views.</span></span>

<span data-ttu-id="c69c9-107">其他與檢視設計工具相關的文章︰</span><span class="sxs-lookup"><span data-stu-id="c69c9-107">Other articles available for View Designer are:</span></span>

* <span data-ttu-id="c69c9-108">[圖格參考](log-analytics-view-designer-tiles.md) - 可用於自訂檢視之每個圖格的設定參考。</span><span class="sxs-lookup"><span data-stu-id="c69c9-108">[Tile reference](log-analytics-view-designer-tiles.md) - Reference of the settings for each of the tiles available to use in your custom views.</span></span>
* <span data-ttu-id="c69c9-109">[視覺效果組件參考](log-analytics-view-designer-parts.md) - 可用於自訂檢視之每個圖格的設定參考。</span><span class="sxs-lookup"><span data-stu-id="c69c9-109">[Visualization part reference](log-analytics-view-designer-parts.md) - Reference of the settings for each of the tiles available to use in your custom views.</span></span>

>[!NOTE]
> <span data-ttu-id="c69c9-110">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則所有檢視中的查詢必須以[新的查詢語言](https://go.microsoft.com/fwlink/?linkid=856078)撰寫。</span><span class="sxs-lookup"><span data-stu-id="c69c9-110">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then queries in all views must be written in the [new query language](https://go.microsoft.com/fwlink/?linkid=856078).</span></span>  <span data-ttu-id="c69c9-111">在工作區升級之前建立的任何檢視都會自動轉換。</span><span class="sxs-lookup"><span data-stu-id="c69c9-111">Any views that were created before the workspace was upgraded will be automtically converted.</span></span>

## <a name="concepts"></a><span data-ttu-id="c69c9-112">概念</span><span class="sxs-lookup"><span data-stu-id="c69c9-112">Concepts</span></span>
<span data-ttu-id="c69c9-113">以檢視設計工具建立的檢視包含下表中的各部分。</span><span class="sxs-lookup"><span data-stu-id="c69c9-113">Views created with the View Designer contain the elements in the following table.</span></span>

| <span data-ttu-id="c69c9-114">部分</span><span class="sxs-lookup"><span data-stu-id="c69c9-114">Part</span></span> | <span data-ttu-id="c69c9-115">說明</span><span class="sxs-lookup"><span data-stu-id="c69c9-115">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c69c9-116">圖格</span><span class="sxs-lookup"><span data-stu-id="c69c9-116">Tile</span></span> |<span data-ttu-id="c69c9-117">顯示在主要 Log Analytics 概觀儀表板上。</span><span class="sxs-lookup"><span data-stu-id="c69c9-117">Displayed on the main Log Analytics Overview dashboard.</span></span>  <span data-ttu-id="c69c9-118">是自訂檢視包含之資訊的視覺化摘要。</span><span class="sxs-lookup"><span data-stu-id="c69c9-118">Includes a visual summarizing of the information contained in the custom View.</span></span>  <span data-ttu-id="c69c9-119">不同的圖格類型提供 OMS 存放庫中不同記錄的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c69c9-119">Different Tile types provide different visualizations of records in the OMS repository.</span></span>  <span data-ttu-id="c69c9-120">按一下圖格即可開啟其自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-120">Click on the Tile to open the Custom View.</span></span> |
| <span data-ttu-id="c69c9-121">自訂檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-121">Custom View</span></span> |<span data-ttu-id="c69c9-122">會在使用者按一下圖格時顯示。</span><span class="sxs-lookup"><span data-stu-id="c69c9-122">Displayed when the user clicks on the Tile.</span></span>  <span data-ttu-id="c69c9-123">包含一或多個視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="c69c9-123">Contains one or more visualization parts.</span></span> |
| <span data-ttu-id="c69c9-124">視覺效果組件</span><span class="sxs-lookup"><span data-stu-id="c69c9-124">Visualization Parts</span></span> |<span data-ttu-id="c69c9-125">根據一或多個針對 OMS 存放庫中資料進行[記錄搜尋](log-analytics-log-searches.md)，所得結果的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c69c9-125">Visualization of data in the OMS repository based on one or more [log searches](log-analytics-log-searches.md).</span></span>  <span data-ttu-id="c69c9-126">大部分組件包含標頭 (提供高階的視覺效果) 和前幾名搜尋結果清單。</span><span class="sxs-lookup"><span data-stu-id="c69c9-126">Most parts will include a Header that provides a high level visualization and a List of the top results.</span></span>  <span data-ttu-id="c69c9-127">不同的組件類型提供 OMS 存放庫中不同記錄的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c69c9-127">Different part types provide different visualizations of records in the OMS repository.</span></span>  <span data-ttu-id="c69c9-128">按一下組件中的項目可執行記錄檔搜尋以提供詳細的記錄。</span><span class="sxs-lookup"><span data-stu-id="c69c9-128">Click on elements in the part to perform a log search providing detailed records.</span></span> |

![檢視設計工具概觀](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-to-your-workspace"></a><span data-ttu-id="c69c9-130">將檢視設計工具新增至工作區</span><span class="sxs-lookup"><span data-stu-id="c69c9-130">Add View Designer to your workspace</span></span>
<span data-ttu-id="c69c9-131">檢視設計工具為預覽版，您必須選取 OMS 入口網站的 [設定] 區段中的 [預覽功能]，將它新增至您的工作區。</span><span class="sxs-lookup"><span data-stu-id="c69c9-131">While View Designer is in preview, you must add it to your workspace by selecting **Preview Features** in the **Settings** section of the OMS portal.</span></span>

![啟用預覽](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a><span data-ttu-id="c69c9-133">建立和編輯檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-133">Creating and editing views</span></span>
### <a name="create-a-new-view"></a><span data-ttu-id="c69c9-134">建立新的檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-134">Create a new view</span></span>
<span data-ttu-id="c69c9-135">按一下主要 OMS 儀表板中的 [檢視表設計工具] 圖格，即可在**檢視表設計工具**中開啟新的檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-135">Open a new view in the **View Designer** by clicking on the View Designer tile in the main OMS dashboard.</span></span>

![檢視設計工具圖格](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a><span data-ttu-id="c69c9-137">編輯現有檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-137">Edit an existing view</span></span>
<span data-ttu-id="c69c9-138">若要在檢視表設計工具中編輯現有檢視，按一下主要 OMS 儀表板中該檢視的圖格即可開啟它。</span><span class="sxs-lookup"><span data-stu-id="c69c9-138">To edit an existing view in the View Designer, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="c69c9-139">然後按一下 [編輯] 按鈕在檢視設計工具中開啟該檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-139">Then click the **Edit** button to open the view in the View Designer.</span></span>

![編輯檢視](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a><span data-ttu-id="c69c9-141">複製現有檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-141">Clone an existing view</span></span>
<span data-ttu-id="c69c9-142">複製檢視時，它會建立新的檢視，並且在檢視設計工具中開啟。</span><span class="sxs-lookup"><span data-stu-id="c69c9-142">When you clone a view, it creates a new view and opens it in the View Designer.</span></span>  <span data-ttu-id="c69c9-143">新檢視會有與原始檢視相同的名稱再加上「複製」二字。</span><span class="sxs-lookup"><span data-stu-id="c69c9-143">The new view will have the same name as the original with "Copy" appended to the end of it.</span></span>  <span data-ttu-id="c69c9-144">若要複製檢視，按一下主要 OMS 儀表板中該現有檢視的圖格即可開啟它。</span><span class="sxs-lookup"><span data-stu-id="c69c9-144">To clone a view, open the existing view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="c69c9-145">然後按一下 [複製] 按鈕在檢視設計工具中開啟該檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-145">Then click the **Clone** button to open the view in the View Designer.</span></span>

![複製檢視](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a><span data-ttu-id="c69c9-147">刪除現有檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-147">Delete an existing view</span></span>
<span data-ttu-id="c69c9-148">若要刪除現有檢視，按一下主要 OMS 儀表板中該檢視的圖格即可開啟它。</span><span class="sxs-lookup"><span data-stu-id="c69c9-148">To delete an existing view, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="c69c9-149">然後按一下 [編輯] 按鈕在檢視設計工具中開啟該檢視，接著按一下 [刪除檢視]。</span><span class="sxs-lookup"><span data-stu-id="c69c9-149">Then click the **Edit** button to open the view in the View Designer, and click **Delete View**.</span></span>

![刪除檢視](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a><span data-ttu-id="c69c9-151">匯出現有檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-151">Export an existing view</span></span>
<span data-ttu-id="c69c9-152">您可以將檢視匯出至 JSON 檔案，用於匯入另一個工作區，或在 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)中使用。</span><span class="sxs-lookup"><span data-stu-id="c69c9-152">You can export a view to a JSON file that you can import into another workspace or use in an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="c69c9-153">若要匯出現有檢視，按一下主要 OMS 儀表板中該檢視的圖格即可開啟它。</span><span class="sxs-lookup"><span data-stu-id="c69c9-153">To export an existing view, open the view by clicking on its tile in the main OMS dashboard.</span></span>  <span data-ttu-id="c69c9-154">然後按一下 [匯出] 按鈕便可在瀏覽器的下載資料夾中建立檔案。</span><span class="sxs-lookup"><span data-stu-id="c69c9-154">Then click the **Export** button to create a file in the browser's download folder.</span></span>  <span data-ttu-id="c69c9-155">檔案的名稱是檢視的名稱，副檔名為 omsview。</span><span class="sxs-lookup"><span data-stu-id="c69c9-155">The name of the file will be the name of the view with the extension *omsview*.</span></span>

![匯出檢視](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a><span data-ttu-id="c69c9-157">匯入現有檢視</span><span class="sxs-lookup"><span data-stu-id="c69c9-157">Import an existing view</span></span>
<span data-ttu-id="c69c9-158">您可以匯入您從其他管理群組匯出的 omsview 檔案。</span><span class="sxs-lookup"><span data-stu-id="c69c9-158">You can import an *omsview* file that you exported from another management group.</span></span>  <span data-ttu-id="c69c9-159">若要匯入現有檢視，請先建立新的檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-159">To import an existing view, first create a new view.</span></span>  <span data-ttu-id="c69c9-160">然後按一下 [匯入] 按鈕，並選取該 omsview 檔案。</span><span class="sxs-lookup"><span data-stu-id="c69c9-160">Then click the **Import** button and select the *omsview* file.</span></span>  <span data-ttu-id="c69c9-161">檔案中的組態將會複製到現有的檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-161">The configuration in the file will be copied into the existing view.</span></span>

![匯出檢視](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a><span data-ttu-id="c69c9-163">使用檢視設計工具</span><span class="sxs-lookup"><span data-stu-id="c69c9-163">Working with View Designer</span></span>
<span data-ttu-id="c69c9-164">檢視設計工具有三個窗格。</span><span class="sxs-lookup"><span data-stu-id="c69c9-164">The View Designer has three panes.</span></span>  <span data-ttu-id="c69c9-165">**設計**窗格呈現自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-165">The **Design** pane represents the custom view.</span></span>  <span data-ttu-id="c69c9-166">當您從 [控制] 窗格將圖格和組件新增至 [設計]，就會將它們新增檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-166">When you add tiles and parts from the **Control** pane to the **Design** pane they are added to the view.</span></span>  <span data-ttu-id="c69c9-167">[屬性] 窗格會列出圖格或選取組件的屬性。</span><span class="sxs-lookup"><span data-stu-id="c69c9-167">The **Properties** pane will display the properties for the tile or selected part.</span></span>

![[檢視設計工具]](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a><span data-ttu-id="c69c9-169">設定檢視圖格</span><span class="sxs-lookup"><span data-stu-id="c69c9-169">Configure view tile</span></span>
<span data-ttu-id="c69c9-170">自訂檢視可以只有單一圖格。</span><span class="sxs-lookup"><span data-stu-id="c69c9-170">A custom view can have only a single tile.</span></span>  <span data-ttu-id="c69c9-171">選取 [控制] 窗格中的 [圖格] 索引標籤來檢視目前圖格或選取另一個圖格。</span><span class="sxs-lookup"><span data-stu-id="c69c9-171">Select the **Tile** tab in the **Control** pane to view the current tile or select an alternate one.</span></span>  <span data-ttu-id="c69c9-172">[屬性] 窗格會列出目前圖格的屬性。</span><span class="sxs-lookup"><span data-stu-id="c69c9-172">The **Properties** pane will display the properties for the current tile.</span></span>  <span data-ttu-id="c69c9-173">根據 [圖格參考](log-analytics-view-designer-tiles.md) 中的詳細資訊來設定圖格屬性，然後按一下 [套用] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="c69c9-173">Configure the tile properties according to the detailed information in the [Tile Reference](log-analytics-view-designer-tiles.md) and click **Apply** to save changes.</span></span>

### <a name="configure-visualization-parts"></a><span data-ttu-id="c69c9-174">設定視覺效果組件</span><span class="sxs-lookup"><span data-stu-id="c69c9-174">Configure visualization parts</span></span>
<span data-ttu-id="c69c9-175">檢視可以包含任意數目的視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="c69c9-175">A view can include any number of visualization parts.</span></span>  <span data-ttu-id="c69c9-176">選取 [檢視] 索引標籤，然後要新增至檢視的視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="c69c9-176">Select the **View** tab and then a visualization part to add to the view.</span></span>  <span data-ttu-id="c69c9-177">[屬性] 窗格會列出選取組件的屬性。</span><span class="sxs-lookup"><span data-stu-id="c69c9-177">The **Properties** pane will display the properties for the selected part.</span></span>  <span data-ttu-id="c69c9-178">根據 [視覺效果組件參考](log-analytics-view-designer-parts.md) 中的詳細資訊來設定檢視的屬性，然後按一下 [套用] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="c69c9-178">Configure the view properties according to the detailed information in the [Visualization part reference](log-analytics-view-designer-parts.md) and click **Apply** to save changes.</span></span>

### <a name="delete-a-visualization-part"></a><span data-ttu-id="c69c9-179">刪除視覺效果組件</span><span class="sxs-lookup"><span data-stu-id="c69c9-179">Delete a visualization part</span></span>
<span data-ttu-id="c69c9-180">按一下組件右上角的 [X] 按鈕，即可從檢視中移除視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="c69c9-180">You can remove a visualization part from the view by clicking the **X** button in the top right corner of the part.</span></span>

### <a name="rearrange-visualization-parts"></a><span data-ttu-id="c69c9-181">重新整理視覺效果組件</span><span class="sxs-lookup"><span data-stu-id="c69c9-181">Rearrange visualization parts</span></span>
<span data-ttu-id="c69c9-182">檢視只有一列視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="c69c9-182">Views only have one row of visualization parts.</span></span>  <span data-ttu-id="c69c9-183">按一下現有組件並拖曳至新的位置，即可重新排列檢視中的組件。</span><span class="sxs-lookup"><span data-stu-id="c69c9-183">Rearrange existing parts in a view by clicking and dragging them to a new location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c69c9-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c69c9-184">Next steps</span></span>
* <span data-ttu-id="c69c9-185">將[圖格](log-analytics-view-designer-tiles.md)新增至您的自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-185">Add [Tiles](log-analytics-view-designer-tiles.md) to your custom view.</span></span>
* <span data-ttu-id="c69c9-186">將[視覺效果組件](log-analytics-view-designer-parts.md)新增至您的自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="c69c9-186">Add [Visualization Parts](log-analytics-view-designer-parts.md) to your custom view.</span></span>
