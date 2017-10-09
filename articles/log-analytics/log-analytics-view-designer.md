---
title: "OMS 記錄分析 aaaCreate 檢視 tooanalyze 資料 |Microsoft 文件"
description: "檢視表設計工具中記錄分析可讓您 toocreate 自訂檢視會顯示在 hello OMS 和 Azure 入口網站，並包含不同的視覺效果 hello OMS 儲存機制中的資料。 本文包含檢視設計工具的概觀以及建立和編輯自訂檢視的程序。"
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
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a><span data-ttu-id="b85cb-104">在 記錄分析中使用檢視表設計工具 toocreate 自訂檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-104">Use View Designer toocreate custom views in Log Analytics</span></span>
<span data-ttu-id="b85cb-105">hello 檢視表設計工具中[記錄分析](log-analytics-overview.md)可讓您 toocreate 自訂檢視 hello OMS 主控台中包含不同的視覺效果 hello OMS 儲存機制中的資料。</span><span class="sxs-lookup"><span data-stu-id="b85cb-105">hello View Designer in [Log Analytics](log-analytics-overview.md) allows you toocreate custom views in hello OMS console that contain different visualizations of data in hello OMS repository.</span></span> <span data-ttu-id="b85cb-106">本文包含檢視設計工具的概觀以及建立和編輯自訂檢視的程序。</span><span class="sxs-lookup"><span data-stu-id="b85cb-106">This article contains an overview of View Designer and procedures for creating and editing custom views.</span></span>

<span data-ttu-id="b85cb-107">其他與檢視設計工具相關的文章︰</span><span class="sxs-lookup"><span data-stu-id="b85cb-107">Other articles available for View Designer are:</span></span>

* <span data-ttu-id="b85cb-108">[磚參考](log-analytics-view-designer-tiles.md)-參考的每一個 hello hello 設定磚可用 toouse 中自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-108">[Tile reference](log-analytics-view-designer-tiles.md) - Reference of hello settings for each of hello tiles available toouse in your custom views.</span></span>
* <span data-ttu-id="b85cb-109">[視覺效果部分參考](log-analytics-view-designer-parts.md)-參考的每一個 hello hello 設定磚可用 toouse 中自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-109">[Visualization part reference](log-analytics-view-designer-parts.md) - Reference of hello settings for each of hello tiles available toouse in your custom views.</span></span>

>[!NOTE]
> <span data-ttu-id="b85cb-110">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則必須寫入所有檢視中的查詢中 hello[新的查詢語言](https://go.microsoft.com/fwlink/?linkid=856078)。</span><span class="sxs-lookup"><span data-stu-id="b85cb-110">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then queries in all views must be written in hello [new query language](https://go.microsoft.com/fwlink/?linkid=856078).</span></span>  <span data-ttu-id="b85cb-111">Hello 工作區已升級之前建立的任何檢視會 automtically 轉換。</span><span class="sxs-lookup"><span data-stu-id="b85cb-111">Any views that were created before hello workspace was upgraded will be automtically converted.</span></span>

## <a name="concepts"></a><span data-ttu-id="b85cb-112">概念</span><span class="sxs-lookup"><span data-stu-id="b85cb-112">Concepts</span></span>
<span data-ttu-id="b85cb-113">建立以 hello 檢視表設計工具檢視包含 hello hello 下表中的項目。</span><span class="sxs-lookup"><span data-stu-id="b85cb-113">Views created with hello View Designer contain hello elements in hello following table.</span></span>

| <span data-ttu-id="b85cb-114">部分</span><span class="sxs-lookup"><span data-stu-id="b85cb-114">Part</span></span> | <span data-ttu-id="b85cb-115">說明</span><span class="sxs-lookup"><span data-stu-id="b85cb-115">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b85cb-116">圖格</span><span class="sxs-lookup"><span data-stu-id="b85cb-116">Tile</span></span> |<span data-ttu-id="b85cb-117">顯示在 hello 主要記錄檔分析概觀儀表板上。</span><span class="sxs-lookup"><span data-stu-id="b85cb-117">Displayed on hello main Log Analytics Overview dashboard.</span></span>  <span data-ttu-id="b85cb-118">包含 hello 所包含的 hello 視覺化摘要自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-118">Includes a visual summarizing of hello information contained in hello custom View.</span></span>  <span data-ttu-id="b85cb-119">不同類型的磚會提供不同的視覺效果 hello OMS 儲存機制中的記錄。</span><span class="sxs-lookup"><span data-stu-id="b85cb-119">Different Tile types provide different visualizations of records in hello OMS repository.</span></span>  <span data-ttu-id="b85cb-120">按一下 hello 磚 tooopen hello 的自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-120">Click on hello Tile tooopen hello Custom View.</span></span> |
| <span data-ttu-id="b85cb-121">自訂檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-121">Custom View</span></span> |<span data-ttu-id="b85cb-122">當 hello 使用者在 hello 並排顯示。</span><span class="sxs-lookup"><span data-stu-id="b85cb-122">Displayed when hello user clicks on hello Tile.</span></span>  <span data-ttu-id="b85cb-123">包含一或多個視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="b85cb-123">Contains one or more visualization parts.</span></span> |
| <span data-ttu-id="b85cb-124">視覺效果組件</span><span class="sxs-lookup"><span data-stu-id="b85cb-124">Visualization Parts</span></span> |<span data-ttu-id="b85cb-125">Hello OMS 儲存機制中的資料視覺效果是根據一或多個[記錄搜尋](log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="b85cb-125">Visualization of data in hello OMS repository based on one or more [log searches](log-analytics-log-searches.md).</span></span>  <span data-ttu-id="b85cb-126">大部分的組件會包含提供高層級的視覺效果的標頭以及一份 hello 前的結果。</span><span class="sxs-lookup"><span data-stu-id="b85cb-126">Most parts will include a Header that provides a high level visualization and a List of hello top results.</span></span>  <span data-ttu-id="b85cb-127">不同的組件類型提供不同的視覺效果 hello OMS 儲存機制中的記錄。</span><span class="sxs-lookup"><span data-stu-id="b85cb-127">Different part types provide different visualizations of records in hello OMS repository.</span></span>  <span data-ttu-id="b85cb-128">按一下 hello 一部分 tooperform 中的項目提供詳細的記錄的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="b85cb-128">Click on elements in hello part tooperform a log search providing detailed records.</span></span> |

![檢視設計工具概觀](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a><span data-ttu-id="b85cb-130">加入檢視表設計工具 tooyour 工作區</span><span class="sxs-lookup"><span data-stu-id="b85cb-130">Add View Designer tooyour workspace</span></span>
<span data-ttu-id="b85cb-131">在預覽中檢視表設計工具時，您必須將它加入 tooyour 工作區選取**預覽功能**在 hello**設定**hello OMS 入口網站的區段。</span><span class="sxs-lookup"><span data-stu-id="b85cb-131">While View Designer is in preview, you must add it tooyour workspace by selecting **Preview Features** in hello **Settings** section of hello OMS portal.</span></span>

![啟用預覽](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a><span data-ttu-id="b85cb-133">建立和編輯檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-133">Creating and editing views</span></span>
### <a name="create-a-new-view"></a><span data-ttu-id="b85cb-134">建立新的檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-134">Create a new view</span></span>
<span data-ttu-id="b85cb-135">開啟新的檢視中 hello**檢視表設計工具**hello 檢視表設計工具上的 並排顯示 hello 主要 OMS 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="b85cb-135">Open a new view in hello **View Designer** by clicking on hello View Designer tile in hello main OMS dashboard.</span></span>

![檢視設計工具圖格](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a><span data-ttu-id="b85cb-137">編輯現有檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-137">Edit an existing view</span></span>
<span data-ttu-id="b85cb-138">tooedit hello 檢視設計工具中，按一下其 hello 主要 OMS 儀表板磚上開啟 hello 檢視中現有的檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-138">tooedit an existing view in hello View Designer, open hello view by clicking on its tile in hello main OMS dashboard.</span></span>  <span data-ttu-id="b85cb-139">然後按一下 hello**編輯**按鈕 tooopen hello 檢視表設計工具中的 hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-139">Then click hello **Edit** button tooopen hello view in hello View Designer.</span></span>

![編輯檢視](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a><span data-ttu-id="b85cb-141">複製現有檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-141">Clone an existing view</span></span>
<span data-ttu-id="b85cb-142">當您複製檢視時，它會建立新的檢視，並且在 hello 檢視表設計工具中開啟。</span><span class="sxs-lookup"><span data-stu-id="b85cb-142">When you clone a view, it creates a new view and opens it in hello View Designer.</span></span>  <span data-ttu-id="b85cb-143">hello 新檢視會有相同的名稱，為 「 複製 」 附加的 toohello 結尾它與原始的 hello hello。</span><span class="sxs-lookup"><span data-stu-id="b85cb-143">hello new view will have hello same name as hello original with "Copy" appended toohello end of it.</span></span>  <span data-ttu-id="b85cb-144">tooclone] 檢視中，開啟 hello hello 主要 OMS 儀表板中的磚上的 [現有的檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-144">tooclone a view, open hello existing view by clicking on its tile in hello main OMS dashboard.</span></span>  <span data-ttu-id="b85cb-145">然後按一下 hello**複製**按鈕 tooopen hello 檢視表設計工具中的 hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-145">Then click hello **Clone** button tooopen hello view in hello View Designer.</span></span>

![複製檢視](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a><span data-ttu-id="b85cb-147">刪除現有檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-147">Delete an existing view</span></span>
<span data-ttu-id="b85cb-148">toodelete 現有的檢視，開啟 hello 檢視其 hello 主要 OMS 儀表板磚上按一下。</span><span class="sxs-lookup"><span data-stu-id="b85cb-148">toodelete an existing view, open hello view by clicking on its tile in hello main OMS dashboard.</span></span>  <span data-ttu-id="b85cb-149">然後按一下 hello**編輯**按鈕 tooopen hello 檢視在 hello 檢視表設計工具，然後按一下**刪除檢視**。</span><span class="sxs-lookup"><span data-stu-id="b85cb-149">Then click hello **Edit** button tooopen hello view in hello View Designer, and click **Delete View**.</span></span>

![刪除檢視](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a><span data-ttu-id="b85cb-151">匯出現有檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-151">Export an existing view</span></span>
<span data-ttu-id="b85cb-152">您可以匯出檢視 tooa JSON 檔案，您可以匯入至另一個工作區，或在使用[Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="b85cb-152">You can export a view tooa JSON file that you can import into another workspace or use in an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="b85cb-153">tooexport 現有的檢視，開啟 hello 檢視其 hello 主要 OMS 儀表板磚上按一下。</span><span class="sxs-lookup"><span data-stu-id="b85cb-153">tooexport an existing view, open hello view by clicking on its tile in hello main OMS dashboard.</span></span>  <span data-ttu-id="b85cb-154">然後按一下 hello**匯出**按鈕 toocreate hello 瀏覽器的下載資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="b85cb-154">Then click hello **Export** button toocreate a file in hello browser's download folder.</span></span>  <span data-ttu-id="b85cb-155">hello hello 檔案名稱會是副檔名為 hello hello 檢視 hello 名稱*omsview*。</span><span class="sxs-lookup"><span data-stu-id="b85cb-155">hello name of hello file will be hello name of hello view with hello extension *omsview*.</span></span>

![匯出檢視](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a><span data-ttu-id="b85cb-157">匯入現有檢視</span><span class="sxs-lookup"><span data-stu-id="b85cb-157">Import an existing view</span></span>
<span data-ttu-id="b85cb-158">您可以匯入您從其他管理群組匯出的 omsview 檔案。</span><span class="sxs-lookup"><span data-stu-id="b85cb-158">You can import an *omsview* file that you exported from another management group.</span></span>  <span data-ttu-id="b85cb-159">tooimport 現有的檢視，第一次建立新的檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-159">tooimport an existing view, first create a new view.</span></span>  <span data-ttu-id="b85cb-160">然後按一下 hello**匯入**按鈕並選取 hello *omsview*檔案。</span><span class="sxs-lookup"><span data-stu-id="b85cb-160">Then click hello **Import** button and select hello *omsview* file.</span></span>  <span data-ttu-id="b85cb-161">hello 檔案中的 hello 組態將會複製到 hello 現有檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-161">hello configuration in hello file will be copied into hello existing view.</span></span>

![匯出檢視](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a><span data-ttu-id="b85cb-163">使用檢視設計工具</span><span class="sxs-lookup"><span data-stu-id="b85cb-163">Working with View Designer</span></span>
<span data-ttu-id="b85cb-164">hello 檢視表設計工具有三個窗格。</span><span class="sxs-lookup"><span data-stu-id="b85cb-164">hello View Designer has three panes.</span></span>  <span data-ttu-id="b85cb-165">hello**設計**窗格代表 hello 自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-165">hello **Design** pane represents hello custom view.</span></span>  <span data-ttu-id="b85cb-166">當您將加入圖格和組件從 hello**控制項**窗格 toohello**設計**它們的窗格加入 toohello 檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-166">When you add tiles and parts from hello **Control** pane toohello **Design** pane they are added toohello view.</span></span>  <span data-ttu-id="b85cb-167">hello**屬性**窗格會顯示 hello 屬性 hello 磚或選取的組件。</span><span class="sxs-lookup"><span data-stu-id="b85cb-167">hello **Properties** pane will display hello properties for hello tile or selected part.</span></span>

![[檢視設計工具]](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a><span data-ttu-id="b85cb-169">設定檢視圖格</span><span class="sxs-lookup"><span data-stu-id="b85cb-169">Configure view tile</span></span>
<span data-ttu-id="b85cb-170">自訂檢視可以只有單一圖格。</span><span class="sxs-lookup"><span data-stu-id="b85cb-170">A custom view can have only a single tile.</span></span>  <span data-ttu-id="b85cb-171">選取 hello**磚** 索引標籤中 hello**控制項**窗格 tooview hello 目前磚，或選取替代的那一個。</span><span class="sxs-lookup"><span data-stu-id="b85cb-171">Select hello **Tile** tab in hello **Control** pane tooview hello current tile or select an alternate one.</span></span>  <span data-ttu-id="b85cb-172">hello**屬性**窗格會顯示 hello 目前 tile hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="b85cb-172">hello **Properties** pane will display hello properties for hello current tile.</span></span>  <span data-ttu-id="b85cb-173">設定 hello 圖格屬性，根據 toohello 詳細的資訊在 hello[磚參考](log-analytics-view-designer-tiles.md)按一下**套用**toosave 變更。</span><span class="sxs-lookup"><span data-stu-id="b85cb-173">Configure hello tile properties according toohello detailed information in hello [Tile Reference](log-analytics-view-designer-tiles.md) and click **Apply** toosave changes.</span></span>

### <a name="configure-visualization-parts"></a><span data-ttu-id="b85cb-174">設定視覺效果組件</span><span class="sxs-lookup"><span data-stu-id="b85cb-174">Configure visualization parts</span></span>
<span data-ttu-id="b85cb-175">檢視可以包含任意數目的視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="b85cb-175">A view can include any number of visualization parts.</span></span>  <span data-ttu-id="b85cb-176">選取 hello**檢視**索引標籤，然後視覺效果部分 tooadd toohello 檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-176">Select hello **View** tab and then a visualization part tooadd toohello view.</span></span>  <span data-ttu-id="b85cb-177">hello**屬性**窗格會顯示 hello hello 選取組件的屬性。</span><span class="sxs-lookup"><span data-stu-id="b85cb-177">hello **Properties** pane will display hello properties for hello selected part.</span></span>  <span data-ttu-id="b85cb-178">設定 hello 檢視根據 toohello 屬性的詳細資訊，在 hello[視覺效果部分參考](log-analytics-view-designer-parts.md)按一下**套用**toosave 變更。</span><span class="sxs-lookup"><span data-stu-id="b85cb-178">Configure hello view properties according toohello detailed information in hello [Visualization part reference](log-analytics-view-designer-parts.md) and click **Apply** toosave changes.</span></span>

### <a name="delete-a-visualization-part"></a><span data-ttu-id="b85cb-179">刪除視覺效果組件</span><span class="sxs-lookup"><span data-stu-id="b85cb-179">Delete a visualization part</span></span>
<span data-ttu-id="b85cb-180">您可以從 hello 檢視移除視覺效果的一部分，依序按一下 hello **X** hello 右上角的 hello 組件中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b85cb-180">You can remove a visualization part from hello view by clicking hello **X** button in hello top right corner of hello part.</span></span>

### <a name="rearrange-visualization-parts"></a><span data-ttu-id="b85cb-181">重新整理視覺效果組件</span><span class="sxs-lookup"><span data-stu-id="b85cb-181">Rearrange visualization parts</span></span>
<span data-ttu-id="b85cb-182">檢視只有一列視覺效果組件。</span><span class="sxs-lookup"><span data-stu-id="b85cb-182">Views only have one row of visualization parts.</span></span>  <span data-ttu-id="b85cb-183">按一下並拖曳它們 tooa 新位置，重新排列在檢視中的現有組件。</span><span class="sxs-lookup"><span data-stu-id="b85cb-183">Rearrange existing parts in a view by clicking and dragging them tooa new location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b85cb-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b85cb-184">Next steps</span></span>
* <span data-ttu-id="b85cb-185">新增[磚](log-analytics-view-designer-tiles.md)tooyour 自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-185">Add [Tiles](log-analytics-view-designer-tiles.md) tooyour custom view.</span></span>
* <span data-ttu-id="b85cb-186">新增[視覺效果部分](log-analytics-view-designer-parts.md)tooyour 自訂檢視。</span><span class="sxs-lookup"><span data-stu-id="b85cb-186">Add [Visualization Parts](log-analytics-view-designer-parts.md) tooyour custom view.</span></span>
