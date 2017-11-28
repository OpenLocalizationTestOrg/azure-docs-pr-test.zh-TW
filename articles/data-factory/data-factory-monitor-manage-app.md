---
title: "aaaMonitor 及管理在資料管線-Azure |Microsoft 文件"
description: "了解 toouse hello 監視和管理應用程式 toomonitor 和管理 Azure data factory 管線和管線的方式。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="52084-103">監視和管理 Azure Data Factory 管線使用 hello 監視和管理應用程式</span><span class="sxs-lookup"><span data-stu-id="52084-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="52084-104">使用 Azure 入口網站/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52084-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="52084-105">使用監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="52084-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="52084-106">本文說明 toouse hello 監視和管理應用程式 toomonitor、 管理和偵錯您的 Data Factory 管線的方式。</span><span class="sxs-lookup"><span data-stu-id="52084-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="52084-107">它也提供 toocreate 發出 tooget 在失敗時收到通知的警示資訊。</span><span class="sxs-lookup"><span data-stu-id="52084-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="52084-108">您可以開始使用 hello 應用程式所遵循的看 hello 視訊：</span><span class="sxs-lookup"><span data-stu-id="52084-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="52084-109">hello 使用者介面顯示 hello 視訊可能不完全與 hello 入口網站中看到的內容。</span><span class="sxs-lookup"><span data-stu-id="52084-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="52084-110">舊一點，但概念還是維持不 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="52084-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="52084-111">啟動 hello 監視和管理應用程式</span><span class="sxs-lookup"><span data-stu-id="52084-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="52084-112">toolaunch hello 監視和管理應用程式中，按一下 hello**監視和管理**磚 hello **Data Factory** data factory 的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![監視在 hello Data Factory 首頁上的磚](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="52084-114">您應該會看到 hello 監視和管理應用程式在個別視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="52084-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![監視及管理應用程式](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="52084-116">如果您看到該 hello 網頁瀏覽器卡在 授權，清除 hello**封鎖第三方 cookie 和站台資料**- 核取方塊或保留選取它，建立的例外狀況**login.microsoftonline.com**然後再試一次 tooopen hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="52084-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="52084-117">Hello 中間窗格中的 hello 活動視窗清單，您會看到每次執行活動的活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="52084-118">例如，如果您的 hello 活動排程 toorun 每小時 5 小時以上，您會看到五個資料配量與相關聯的五個活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="52084-119">如果您沒有看到活動 windows hello hello 底部的清單中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="52084-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="52084-120">更新 hello**開始時間**和**結束時間**篩選在 hello 頂端 toomatch hello 開始和結束時間的管線，，然後按一下hello**套用** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="52084-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="52084-121">hello 活動視窗清單不會自動重新整理。</span><span class="sxs-lookup"><span data-stu-id="52084-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="52084-122">按一下 hello**重新整理**hello hello 工具列上的按鈕**活動 Windows**清單。</span><span class="sxs-lookup"><span data-stu-id="52084-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="52084-123">如果您沒有 Data Factory 的應用程式 tootest 這些步驟，請勿 hello 教學課程：[從 Blob 儲存體 tooSQL 資料庫使用 Data Factory 複製資料](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="52084-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="52084-124">了解 hello 監視和管理應用程式</span><span class="sxs-lookup"><span data-stu-id="52084-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="52084-125">有三個索引標籤左側 hello:**資源總管**，**監視檢視**，和**警示**。</span><span class="sxs-lookup"><span data-stu-id="52084-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="52084-126">hello 第一個索引標籤 (**資源總管**) 預設會選取。</span><span class="sxs-lookup"><span data-stu-id="52084-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="52084-127">資源總管</span><span class="sxs-lookup"><span data-stu-id="52084-127">Resource Explorer</span></span>
<span data-ttu-id="52084-128">您會看到下列 hello:</span><span class="sxs-lookup"><span data-stu-id="52084-128">You see hello following:</span></span>

* <span data-ttu-id="52084-129">資源總管 hello**樹狀檢視**hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="52084-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="52084-130">hello**圖表檢視**在 hello 中間窗格中的 hello 最上方。</span><span class="sxs-lookup"><span data-stu-id="52084-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="52084-131">hello**活動 Windows**在 hello 中間窗格中的 hello 下方的清單。</span><span class="sxs-lookup"><span data-stu-id="52084-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="52084-132">hello**屬性**，**活動視窗總管**，和**指令碼**hello 右窗格中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52084-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="52084-133">在資源總管 中，您會看到 hello data factory 中的樹狀檢視中的所有資源 （管線、 資料集、 連結的服務）。</span><span class="sxs-lookup"><span data-stu-id="52084-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="52084-134">當您在 [資源總管] 中選取物件時：</span><span class="sxs-lookup"><span data-stu-id="52084-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="52084-135">hello 相關聯的實體會反白顯示 hello 圖表檢視中的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="52084-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="52084-136">[相關聯活動 windows](data-factory-scheduling-and-execution.md) hello 活動視窗底部 hello 清單中反白顯示。</span><span class="sxs-lookup"><span data-stu-id="52084-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="52084-137">hello 右窗格中，hello hello 所選物件的屬性會顯示 hello 屬性 視窗中。</span><span class="sxs-lookup"><span data-stu-id="52084-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="52084-138">顯示 hello hello 所選取物件的 JSON 定義時，如果適用的話。</span><span class="sxs-lookup"><span data-stu-id="52084-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="52084-139">例如︰連結的服務、資料集或管線。</span><span class="sxs-lookup"><span data-stu-id="52084-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![資源總管](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="52084-141">請參閱 hello[排程與執行](data-factory-scheduling-and-execution.md)文件以取得詳細的概念性資訊，關於活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="52084-142">圖表檢視</span><span class="sxs-lookup"><span data-stu-id="52084-142">Diagram View</span></span>
<span data-ttu-id="52084-143">hello data factory 的圖表檢視會提供單一的半透明 toomonitor 窗格，以及管理 data factory 和及其資產。</span><span class="sxs-lookup"><span data-stu-id="52084-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="52084-144">當您在 hello 圖表檢視中選取的 Data Factory 實體 （資料集/管線）：</span><span class="sxs-lookup"><span data-stu-id="52084-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="52084-145">hello 資料 factory 實體 hello 樹狀結構檢視中選取。</span><span class="sxs-lookup"><span data-stu-id="52084-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="52084-146">hello 相關聯的 windows hello 活動視窗 清單中反白顯示的活動。</span><span class="sxs-lookup"><span data-stu-id="52084-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="52084-147">hello hello 所選物件的屬性會顯示 hello 屬性 視窗中。</span><span class="sxs-lookup"><span data-stu-id="52084-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="52084-148">Hello 管線 （不在暫停狀態） 啟用時，它會顯示綠色列：</span><span class="sxs-lookup"><span data-stu-id="52084-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![管線執行中](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="52084-150">您可以暫停、 繼續或終止 hello 圖表檢視中選取它，並使用 hello 按鈕 hello 命令列上的管線。</span><span class="sxs-lookup"><span data-stu-id="52084-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![暫停/繼續 hello 命令列上](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="52084-152">有三個命令 列按鈕的 hello 圖表檢視中的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="52084-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="52084-153">您可以使用 hello 第二個按鈕 toopause hello 管線。</span><span class="sxs-lookup"><span data-stu-id="52084-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="52084-154">暫停不會終止 hello 目前正在執行的活動，並讓他們繼續 toocompletion。</span><span class="sxs-lookup"><span data-stu-id="52084-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="52084-155">hello 第三個按鈕暫停 hello 管線，並終止其現有的執行活動。</span><span class="sxs-lookup"><span data-stu-id="52084-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="52084-156">hello 第一個按鈕繼續 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="52084-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="52084-157">當您的管線已暫停，hello hello 管線變更色彩。</span><span class="sxs-lookup"><span data-stu-id="52084-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="52084-158">例如，暫停的管線看起來像在下列映像的 hello:</span><span class="sxs-lookup"><span data-stu-id="52084-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![管線已暫停](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="52084-160">您可以複選的兩個或多個管線使用 hello Ctrl 鍵。</span><span class="sxs-lookup"><span data-stu-id="52084-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="52084-161">您可以使用 hello 命令列按鈕 toopause/繼續多個管線，一次。</span><span class="sxs-lookup"><span data-stu-id="52084-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="52084-162">您也可以以滑鼠右鍵按一下管線並選取選項 toosuspend 繼續或終止管線。</span><span class="sxs-lookup"><span data-stu-id="52084-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![管線的內容功能表](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="52084-164">按一下 hello**開啟管線**選項 toosee hello 管線中的所有 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="52084-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![開啟管線功能表](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="52084-166">在開啟的 hello 管線檢視中，您會看到 hello 管線中的所有活動。</span><span class="sxs-lookup"><span data-stu-id="52084-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="52084-167">在這個範例中只有一個活動：複製活動。</span><span class="sxs-lookup"><span data-stu-id="52084-167">In this example, there is only one activity: Copy Activity.</span></span> 

![已開啟的管線](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="52084-169">toogo 回 toohello 前一個檢視中，按一下 hello hello 上方的階層連結功能表中的 hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="52084-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="52084-170">在 hello 管線檢視中，當您選取的輸出資料集，或當您將滑鼠移 hello 輸出資料集，您會看到該資料集的 hello 活動 Windows 快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![活動時段快顯視窗](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="52084-172">您可以按一下活動視窗 toosee 詳細資料，hello**屬性**hello 右窗格中的視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![活動時段屬性](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="52084-174">Hello 右窗格中，切換 toohello**活動視窗總管**索引標籤上的 toosee 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52084-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="52084-176">另請參閱**解析變數**每次執行的嘗試在 hello 活動**嘗試**> 一節。</span><span class="sxs-lookup"><span data-stu-id="52084-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![解析的變數](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="52084-178">切換 toohello**指令碼**toosee hello JSON 指令碼定義 hello 所選物件的索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="52084-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![指令碼索引標籤](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="52084-180">您可以在三個地方看到活動時段：</span><span class="sxs-lookup"><span data-stu-id="52084-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="52084-181">hello 活動 Windows hello 圖表檢視 （中間窗格） 中的快顯。</span><span class="sxs-lookup"><span data-stu-id="52084-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="52084-182">hello 右窗格中的 hello 活動 Windows 檔案總管。</span><span class="sxs-lookup"><span data-stu-id="52084-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="52084-183">hello 活動 Windows hello 下方窗格中的清單。</span><span class="sxs-lookup"><span data-stu-id="52084-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="52084-184">在 hello 活動 Windows 快顯視窗和活動 Windows 檔案總管 中，您可以捲動 toohello 前一週和 hello 使用下一週 hello 左邊和右邊的箭號。</span><span class="sxs-lookup"><span data-stu-id="52084-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![活動時段總管的向左/向右箭號](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="52084-186">在 hello hello 圖表檢視底部，您會看到這些按鈕： 放大、 縮小、 縮放 tooFit 縮放 100%，而鎖定配置。</span><span class="sxs-lookup"><span data-stu-id="52084-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="52084-187">hello**鎖定配置**按鈕會讓您不小心移動了資料表和管線 hello 圖表檢視中。</span><span class="sxs-lookup"><span data-stu-id="52084-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="52084-188">此按鈕預設為開啟。</span><span class="sxs-lookup"><span data-stu-id="52084-188">It's on by default.</span></span> <span data-ttu-id="52084-189">您可以將它關閉，並在 hello 圖表中四處移動實體。</span><span class="sxs-lookup"><span data-stu-id="52084-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="52084-190">當您將它關閉時，您可以使用 hello 最後一個按鈕 tooautomatically 位置資料表和管線。</span><span class="sxs-lookup"><span data-stu-id="52084-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="52084-191">您也可以使用 hello 滑鼠滾輪，放大或縮小。</span><span class="sxs-lookup"><span data-stu-id="52084-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![圖表檢視縮放命令](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="52084-193">活動時段清單</span><span class="sxs-lookup"><span data-stu-id="52084-193">Activity Windows list</span></span>
<span data-ttu-id="52084-194">在 hello hello 中間窗格底部的 hello 活動視窗清單會顯示您選取 hello 資源總管或 hello 圖表檢視中的 hello 資料集的所有活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="52084-195">根據預設，hello 清單是依遞減順序表示，您會看見 hello 最新活動視窗頂端 hello。</span><span class="sxs-lookup"><span data-stu-id="52084-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![活動時段清單](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="52084-197">這份清單不會自動重新整理，因此 hello 工具列 toomanually 上的使用 hello 重新整理按鈕重新整理。</span><span class="sxs-lookup"><span data-stu-id="52084-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="52084-198">活動視窗可以是其中一種 hello 下列狀態：</span><span class="sxs-lookup"><span data-stu-id="52084-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="52084-199">狀態</span><span class="sxs-lookup"><span data-stu-id="52084-199">Status</span></span></th><th align="left"><span data-ttu-id="52084-200">子狀態</span><span class="sxs-lookup"><span data-stu-id="52084-200">Substatus</span></span></th><th align="left"><span data-ttu-id="52084-201">說明</span><span class="sxs-lookup"><span data-stu-id="52084-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="52084-202">等候</span><span class="sxs-lookup"><span data-stu-id="52084-202">Waiting</span></span></td><td><span data-ttu-id="52084-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="52084-203">ScheduleTime</span></span></td><td><span data-ttu-id="52084-204">hello 時間未針對 hello 活動視窗 toorun 發生。</span><span class="sxs-lookup"><span data-stu-id="52084-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="52084-205">DatasetDependencies</span></span></td><td><span data-ttu-id="52084-206">hello 上游相依性未準備好。</span><span class="sxs-lookup"><span data-stu-id="52084-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="52084-207">ComputeResources</span></span></td><td><span data-ttu-id="52084-208">hello 計算資源無法使用。</span><span class="sxs-lookup"><span data-stu-id="52084-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="52084-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="52084-210">所有的 hello 活動執行個體都忙於執行其他活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="52084-211">ActivityResume</span></span></td><td><span data-ttu-id="52084-212">hello 活動已暫停，直到它繼續時，無法執行 hello 活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-213">Retry</span><span class="sxs-lookup"><span data-stu-id="52084-213">Retry</span></span></td><td><span data-ttu-id="52084-214">正在重試 hello 活動執行。</span><span class="sxs-lookup"><span data-stu-id="52084-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-215">驗證</span><span class="sxs-lookup"><span data-stu-id="52084-215">Validation</span></span></td><td><span data-ttu-id="52084-216">驗證尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="52084-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="52084-217">ValidationRetry</span></span></td><td><span data-ttu-id="52084-218">驗證是等待 toobe 重試。</span><span class="sxs-lookup"><span data-stu-id="52084-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="52084-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="52084-219">InProgress</span></span></td><td><span data-ttu-id="52084-220">Validating</span><span class="sxs-lookup"><span data-stu-id="52084-220">Validating</span></span></td><td><span data-ttu-id="52084-221">驗證正在進行中。</span><span class="sxs-lookup"><span data-stu-id="52084-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="52084-222">正在處理 hello 活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="52084-223">Failed</span><span class="sxs-lookup"><span data-stu-id="52084-223">Failed</span></span></td><td><span data-ttu-id="52084-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="52084-224">TimedOut</span></span></td><td><span data-ttu-id="52084-225">hello 活動的執行時間超過所允許的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="52084-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="52084-226">Canceled</span></span></td><td><span data-ttu-id="52084-227">hello 活動視窗已取消的使用者動作。</span><span class="sxs-lookup"><span data-stu-id="52084-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-228">驗證</span><span class="sxs-lookup"><span data-stu-id="52084-228">Validation</span></span></td><td><span data-ttu-id="52084-229">驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="52084-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="52084-230">hello 活動視窗無法 toobe 產生或驗證。</span><span class="sxs-lookup"><span data-stu-id="52084-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="52084-231">就緒</span><span class="sxs-lookup"><span data-stu-id="52084-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="52084-232">hello 活動視窗已準備好耗用量。</span><span class="sxs-lookup"><span data-stu-id="52084-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-233">Skipped</span><span class="sxs-lookup"><span data-stu-id="52084-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="52084-234">未處理 hello 活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="52084-235">None</span><span class="sxs-lookup"><span data-stu-id="52084-235">None</span></span></td><td>-</td><td><span data-ttu-id="52084-236">活動視窗 tooexist 搭配不同的狀態，但已重設。</span><span class="sxs-lookup"><span data-stu-id="52084-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="52084-237">當您按一下活動視窗 hello 清單中的時，您會看到相關的詳細資料，在 hello**活動 Windows 檔案總管**或 hello**屬性**上 hello 右視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="52084-239">重新整理活動時段</span><span class="sxs-lookup"><span data-stu-id="52084-239">Refresh activity windows</span></span>
<span data-ttu-id="52084-240">hello 詳細資料不會自動重新整理，因此使用 hello 命令列 toomanually 重新整理 hello 活動 windows 清單中的 [hello 重新整理] 按鈕 （hello 第二個按鈕）。</span><span class="sxs-lookup"><span data-stu-id="52084-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="52084-241">[屬性] 視窗</span><span class="sxs-lookup"><span data-stu-id="52084-241">Properties window</span></span>
<span data-ttu-id="52084-242">hello 屬性 視窗是在 hello 最右邊的窗格中的 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="52084-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![[屬性] 視窗](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="52084-244">它會顯示您選取 hello 資源總管 （樹狀結構檢視） 中的 hello 項目的屬性或活動視窗清單。</span><span class="sxs-lookup"><span data-stu-id="52084-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="52084-245">活動時段總管</span><span class="sxs-lookup"><span data-stu-id="52084-245">Activity Window Explorer</span></span>
<span data-ttu-id="52084-246">hello**活動視窗總管**視窗是在 hello hello 監視和管理應用程式的最右邊的窗格中。</span><span class="sxs-lookup"><span data-stu-id="52084-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="52084-247">它會顯示有關您在 hello 活動 Windows 快顯視窗或 hello 活動視窗 清單中選取的 hello 活動視窗的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52084-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="52084-249">您可以切換 tooanother 活動視窗頂端 hello hello 行事曆 檢視中按一下。</span><span class="sxs-lookup"><span data-stu-id="52084-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="52084-250">您也可以使用 hello 左側的箭號右邊的箭號按鈕，在 hello 頂端 toosee 活動 windows hello 從上一週，或 hello 下週。</span><span class="sxs-lookup"><span data-stu-id="52084-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="52084-251">您可以使用 hello 底部窗格 toorerun hello 活動視窗中的 hello 工具列按鈕，或重新整理在 hello 窗格中的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52084-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="52084-252">指令碼</span><span class="sxs-lookup"><span data-stu-id="52084-252">Script</span></span>
<span data-ttu-id="52084-253">您可以使用 hello**指令碼** 索引標籤 tooview hello hello 的 JSON 定義會選取 Data Factory 實體 （連結的服務、 資料集或管線）。</span><span class="sxs-lookup"><span data-stu-id="52084-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![指令碼索引標籤](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="52084-255">使用系統檢視</span><span class="sxs-lookup"><span data-stu-id="52084-255">Use system views</span></span>
<span data-ttu-id="52084-256">hello 監視和管理應用程式包含預先建立的系統檢視表 (**最近活動 windows**，**失敗活動 windows**，**進行中活動 windows**)，可讓您針對您的 data factory tooview 最近/失敗/進行中活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="52084-257">切換 toohello**監視檢視**hello 左側，按一下索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52084-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![[監視檢視] 索引標籤](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="52084-259">目前，有三個支援的系統檢視。</span><span class="sxs-lookup"><span data-stu-id="52084-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="52084-260">選取選項 toosee 最近活動 windows、 失敗的活動視窗或進行中活動 windows hello 活動視窗 （在 hello hello 中間窗格底端） 清單中的。</span><span class="sxs-lookup"><span data-stu-id="52084-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="52084-261">當您選取 hello**最近活動 windows**選項，您會看到所有的最近活動 windows hello 的遞減順序**上次嘗試時間**。</span><span class="sxs-lookup"><span data-stu-id="52084-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="52084-262">您可以使用 hello**失敗活動 windows**檢視 toosee 所有失敗的活動 windows hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="52084-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="52084-263">選取失敗的活動視窗中將 hello 清單 toosee 詳細資訊，請參閱 hello**屬性**視窗或 hello**活動視窗總管**。</span><span class="sxs-lookup"><span data-stu-id="52084-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="52084-264">您也可以下載失敗的活動時段的任何記錄檔。</span><span class="sxs-lookup"><span data-stu-id="52084-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="52084-265">排序與篩選活動時段</span><span class="sxs-lookup"><span data-stu-id="52084-265">Sort and filter activity windows</span></span>
<span data-ttu-id="52084-266">變更 hello**開始時間**和**結束時間**hello 命令列 toofilter 活動視窗中的設定。</span><span class="sxs-lookup"><span data-stu-id="52084-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="52084-267">變更 hello 開始時間和結束時間之後，按一下 hello 按鈕下一步 toohello 結束時間 toorefresh hello 活動視窗清單。</span><span class="sxs-lookup"><span data-stu-id="52084-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![開始及結束時間](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="52084-269">目前，所有時間都都以 UTC 格式 hello 監視和管理應用程式中。</span><span class="sxs-lookup"><span data-stu-id="52084-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="52084-270">在 hello**活動視窗清單**，按一下 hello 的資料行的名稱 (例如： 狀態)。</span><span class="sxs-lookup"><span data-stu-id="52084-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![活動時段清單的資料行功能表](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="52084-272">您可以執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="52084-272">You can do hello following:</span></span>

* <span data-ttu-id="52084-273">以遞增順序排序。</span><span class="sxs-lookup"><span data-stu-id="52084-273">Sort in ascending order.</span></span>
* <span data-ttu-id="52084-274">以遞減順序排序。</span><span class="sxs-lookup"><span data-stu-id="52084-274">Sort in descending order.</span></span>
* <span data-ttu-id="52084-275">根據一或多個值 (Ready、Waiting 等) 來篩選。</span><span class="sxs-lookup"><span data-stu-id="52084-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="52084-276">當您在資料行上指定篩選器時，您會看見 hello 篩選按鈕啟用該資料行，這表示 hello 資料行中的 hello 值已篩選的值。</span><span class="sxs-lookup"><span data-stu-id="52084-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Hello 活動視窗清單的資料行上篩選](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="52084-278">您可以使用 hello 相同的快顯視窗 tooclear 篩選。</span><span class="sxs-lookup"><span data-stu-id="52084-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="52084-279">tooclear 所有篩選 hello 活動視窗的清單，請按一下 hello 命令列上的 hello 清除篩選按鈕。</span><span class="sxs-lookup"><span data-stu-id="52084-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![清除所有篩選器，如 hello 活動視窗清單](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="52084-281">執行批次動作</span><span class="sxs-lookup"><span data-stu-id="52084-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="52084-282">重新執行已選取的活動時段</span><span class="sxs-lookup"><span data-stu-id="52084-282">Rerun selected activity windows</span></span>
<span data-ttu-id="52084-283">選取活動視窗，按一下向下箭號，第一個命令列按鈕 hello，hello 並選取**重新執行** / **重新執行與上游管線中**。</span><span class="sxs-lookup"><span data-stu-id="52084-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="52084-284">當您選取 hello**重新執行與上游管線中**選項時，它可重新執行所有的上游活動視窗以及。</span><span class="sxs-lookup"><span data-stu-id="52084-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="52084-285">![重新執行某個活動時段](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="52084-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="52084-286">也可以在 hello 清單中選取多個活動視窗並且在 hello 予以重新執行相同的時間。</span><span class="sxs-lookup"><span data-stu-id="52084-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="52084-287">您可能想 toofilter 活動 windows hello 狀態為基礎 (例如：**失敗**)-，然後更正，導致 hello 活動 windows toofail hello 問題之後重新執行失敗的 hello 活動視窗。</span><span class="sxs-lookup"><span data-stu-id="52084-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="52084-288">請參閱下列區段，如需詳細資訊，關於篩選活動 windows hello 清單中的 hello。</span><span class="sxs-lookup"><span data-stu-id="52084-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="52084-289">暫停/繼續多個管線</span><span class="sxs-lookup"><span data-stu-id="52084-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="52084-290">您可以使用 hello Ctrl 鍵的多重選取的兩個或多個管線。</span><span class="sxs-lookup"><span data-stu-id="52084-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="52084-291">您可以使用 hello 命令 列按鈕 （這會反白顯示 hello 下列映像中的 hello 紅色矩形） toopause/繼續它們。</span><span class="sxs-lookup"><span data-stu-id="52084-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![暫停/繼續 hello 命令列上](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="52084-293">建立警示</span><span class="sxs-lookup"><span data-stu-id="52084-293">Create alerts</span></span>
<span data-ttu-id="52084-294">hello**警示**頁面可讓您建立警示及檢視/編輯/刪除現有的警示。</span><span class="sxs-lookup"><span data-stu-id="52084-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="52084-295">您也可以停用/啟用警示。</span><span class="sxs-lookup"><span data-stu-id="52084-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="52084-296">toosee hello 警示 頁面上，按一下 hello**警示** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="52084-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![[警示] 索引標籤](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="52084-298">toocreate 警示</span><span class="sxs-lookup"><span data-stu-id="52084-298">toocreate an alert</span></span>
1. <span data-ttu-id="52084-299">按一下**新增警示**tooadd 警示。</span><span class="sxs-lookup"><span data-stu-id="52084-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="52084-300">您會看到 hello**詳細資料**頁面。</span><span class="sxs-lookup"><span data-stu-id="52084-300">You see hello **Details** page.</span></span>

    ![建立警示：[詳細資料] 頁面](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="52084-302">指定 hello**名稱**和**描述**hello 警示，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="52084-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="52084-303">您應該會看見 hello**篩選**頁面。</span><span class="sxs-lookup"><span data-stu-id="52084-303">You should see hello **Filters** page.</span></span>

    ![建立警示：[篩選器] 頁面](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="52084-305">選取 hello**事件**，**狀態**，和**子狀態**（選擇性） 您想 toocreate Data Factory 服務警示，並按一下**下一步**.</span><span class="sxs-lookup"><span data-stu-id="52084-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="52084-306">您應該會看見 hello**收件者**頁面。</span><span class="sxs-lookup"><span data-stu-id="52084-306">You should see hello **Recipients** page.</span></span>

    ![建立警示：[收件者] 頁面](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="52084-308">選取 hello**電子郵件訂閱管理員**選項及/或輸入**其他管理員電子郵件**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="52084-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="52084-309">您應該會看到 hello 清單中的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="52084-309">You should see hello alert in hello list.</span></span>

    ![警示清單](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="52084-311">在 hello 警示清單中，使用與 hello 警示 tooedit/刪除/停用/啟用警示相關聯的 hello 按鈕。</span><span class="sxs-lookup"><span data-stu-id="52084-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="52084-312">事件/狀態/子狀態</span><span class="sxs-lookup"><span data-stu-id="52084-312">Event/status/substatus</span></span>
<span data-ttu-id="52084-313">hello 下表提供 hello 清單可用的事件和狀態 （和子狀態）。</span><span class="sxs-lookup"><span data-stu-id="52084-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="52084-314">事件名稱</span><span class="sxs-lookup"><span data-stu-id="52084-314">Event name</span></span> | <span data-ttu-id="52084-315">狀態</span><span class="sxs-lookup"><span data-stu-id="52084-315">Status</span></span> | <span data-ttu-id="52084-316">子狀態</span><span class="sxs-lookup"><span data-stu-id="52084-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="52084-317">活動執行已開始</span><span class="sxs-lookup"><span data-stu-id="52084-317">Activity Run Started</span></span> |<span data-ttu-id="52084-318">已啟動</span><span class="sxs-lookup"><span data-stu-id="52084-318">Started</span></span> |<span data-ttu-id="52084-319">啟動中</span><span class="sxs-lookup"><span data-stu-id="52084-319">Starting</span></span> |
| <span data-ttu-id="52084-320">活動執行已結束</span><span class="sxs-lookup"><span data-stu-id="52084-320">Activity Run Finished</span></span> |<span data-ttu-id="52084-321">Succeeded</span><span class="sxs-lookup"><span data-stu-id="52084-321">Succeeded</span></span> |<span data-ttu-id="52084-322">Succeeded</span><span class="sxs-lookup"><span data-stu-id="52084-322">Succeeded</span></span> |
| <span data-ttu-id="52084-323">活動執行已結束</span><span class="sxs-lookup"><span data-stu-id="52084-323">Activity Run Finished</span></span> |<span data-ttu-id="52084-324">Failed</span><span class="sxs-lookup"><span data-stu-id="52084-324">Failed</span></span> |<span data-ttu-id="52084-325">資源配置失敗</span><span class="sxs-lookup"><span data-stu-id="52084-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="52084-326">執行失敗</span><span class="sxs-lookup"><span data-stu-id="52084-326">Failed Execution</span></span><br/><br/><span data-ttu-id="52084-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="52084-327">Timed Out</span></span><br/><br/><span data-ttu-id="52084-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="52084-328">Failed Validation</span></span><br/><br/><span data-ttu-id="52084-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="52084-329">Abandoned</span></span> |
| <span data-ttu-id="52084-330">已開始建立隨選 HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="52084-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="52084-331">已啟動</span><span class="sxs-lookup"><span data-stu-id="52084-331">Started</span></span> |-|
| <span data-ttu-id="52084-332">已成功建立隨選 HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="52084-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="52084-333">Succeeded</span><span class="sxs-lookup"><span data-stu-id="52084-333">Succeeded</span></span> |-|
| <span data-ttu-id="52084-334">已刪除隨選 HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="52084-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="52084-335">Succeeded</span><span class="sxs-lookup"><span data-stu-id="52084-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="52084-336">tooedit、 刪除或停用警示</span><span class="sxs-lookup"><span data-stu-id="52084-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="52084-337">使用下列按鈕 （以紅色反白顯示） tooedit、 刪除或停用警示的 hello。</span><span class="sxs-lookup"><span data-stu-id="52084-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![警示按鈕](./media/data-factory-monitor-manage-app/AlertButtons.png)
