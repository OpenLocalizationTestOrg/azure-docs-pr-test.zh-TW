---
title: "監視和管理資料管線 - Azure |Microsoft Docs"
description: "了解如何使用監視及管理應用程式來監視及管理 Azure Data Factory 及管線。"
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
ms.openlocfilehash: d5a2d1f3d85b8a2212326cfcfd0ba5d80356b769
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="ddfd8-103">使用監視及管理應用程式，以監視和管理 Azure Data Factory 管線</span><span class="sxs-lookup"><span data-stu-id="ddfd8-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ddfd8-104">使用 Azure 入口網站/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddfd8-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="ddfd8-105">使用監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="ddfd8-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="ddfd8-106">本文說明如何使用監視及管理應用程式來監視、管理與偵錯您的 Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="ddfd8-107">同時也會提供如何建立警示以取得失敗通知的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-107">It also provides information on how to create alerts to get notified on failures.</span></span> <span data-ttu-id="ddfd8-108">您可以藉由觀賞下列影片開始使用應用程式：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-108">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> <span data-ttu-id="ddfd8-109">影片中顯示的使用者介面可能不完全符合您在入口網站中看到的使用者介面。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-109">The user interface shown in the video may not exactly match what you see in the portal.</span></span> <span data-ttu-id="ddfd8-110">它比較舊，但是概念相同。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-110">It's slightly older, but concepts remain the same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="ddfd8-111">啟動監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="ddfd8-111">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="ddfd8-112">若要啟動監視及管理應用程式，針對您的 Data Factory 按一下 [Data Factory] 刀鋒視窗上的 [監視及管理] 圖格。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-112">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Data Factory 首頁上的監視磚](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="ddfd8-114">您應該會看到監視及管理應用程式在個別視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-114">You should see the Monitoring and Management app open in a separate window.</span></span>  

![監視及管理應用程式](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="ddfd8-116">如果您看到網頁瀏覽器停滯在「授權中...」，請清除 [封鎖第三方 Cookie 和站台資料] 核取方塊，或保留選取該核取方塊但建立 **login.microsoftonline.com** 的例外狀況，然後再試一次開啟應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-116">If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>


<span data-ttu-id="ddfd8-117">在中間窗格的 [活動時段] 清單中，您會在每次執行活動時看到活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-117">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="ddfd8-118">例如，如果您有活動排程在五個小時內每小時執行，您會看到與五個資料配量與相關聯的五個活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-118">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="ddfd8-119">如果您沒有在底部的清單中看到活動時段，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-119">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="ddfd8-120">更新頂端的**開始時間**和**結束時間**篩選以符合管線的開始和結束時間，然後按一下 [套用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-120">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="ddfd8-121">[活動時段] 清單不會自動重新整理。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-121">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="ddfd8-122">按一下 [活動時段] 清單中工具列上的 [重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-122">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="ddfd8-123">如果您還沒有用來測試這些步驟的 Data Factory 應用程式，請進行教學課程：[使用 Data Factory 將資料從 Blob 儲存體複製到 SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-123">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="ddfd8-124">了解監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="ddfd8-124">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="ddfd8-125">左側有三個索引標籤︰[資源總管]、[監視檢視] 以及 [警示]。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-125">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="ddfd8-126">預設會選取第一個索引標籤 ([資源總管])。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-126">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="ddfd8-127">資源總管</span><span class="sxs-lookup"><span data-stu-id="ddfd8-127">Resource Explorer</span></span>
<span data-ttu-id="ddfd8-128">這時會顯示下列項目：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-128">You see the following:</span></span>

* <span data-ttu-id="ddfd8-129">左窗格中的資源總管**樹狀檢視**。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-129">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="ddfd8-130">中間窗格頂端的**圖表檢視**。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-130">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="ddfd8-131">中間窗格底部的 [活動時段] 清單。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-131">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="ddfd8-132">右窗格中的 [屬性]、[活動時段總管] 和 [指令碼] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-132">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="ddfd8-133">在資源總管中，您可以在樹狀檢視的 Data Factory 看到所有資源 (管線、資料集、連結的服務)。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="ddfd8-134">當您在 [資源總管] 中選取物件時：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="ddfd8-135">在 [圖表檢視] 中，相關聯的 Data Factory 實體會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-135">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="ddfd8-136">在底部的 [活動時段] 清單中，[相關聯的活動時段](data-factory-scheduling-and-execution.md)已反白顯示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="ddfd8-137">右窗格的 [屬性] 視窗中顯示已選取物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-137">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="ddfd8-138">顯示已選取物件的 JSON 定義 (如果適用的話)。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-138">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="ddfd8-139">例如︰連結的服務、資料集或管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![資源總管](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="ddfd8-141">請參閱[排程和執行](data-factory-scheduling-and-execution.md)文章，了解活動時段的詳細概念性資訊。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-141">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="ddfd8-142">圖表檢視</span><span class="sxs-lookup"><span data-stu-id="ddfd8-142">Diagram View</span></span>
<span data-ttu-id="ddfd8-143">Data Factory 的圖表檢視提供單一窗格，可用來監視和管理 Data Factory 及其資產。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-143">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="ddfd8-144">當您在 [圖表檢視] 中選取 Data Factory 實體 (資料集/管線) 時：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-144">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="ddfd8-145">在樹狀檢視中，Data Factory 實體已選取。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-145">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="ddfd8-146">在 [活動時段] 清單中，相關聯的活動時段已反白顯示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-146">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="ddfd8-147">在 [屬性] 視窗中，會顯示已選取物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-147">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="ddfd8-148">當管線已啟用時 (不在暫停狀態)，它會顯示綠色線條：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-148">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![管線執行中](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="ddfd8-150">您可以暫停、繼續或終止管線，方法是在圖表檢視中選取它，以及使用命令列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-150">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![命令列上的暫停/繼續](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="ddfd8-152">[圖表檢視] 中的管線有三個命令列按鈕。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-152">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="ddfd8-153">第二個按鈕可以讓您暫停管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-153">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="ddfd8-154">暫停不會終止正在執行的活動，還會讓活動繼續完成。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-154">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="ddfd8-155">第三個按鈕會暫停管線，並終止管線正在執行的活動。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-155">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="ddfd8-156">第一個按鈕會讓管線繼續執行。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-156">The first button resumes the pipeline.</span></span> <span data-ttu-id="ddfd8-157">您的管線暫停時，管線的色彩會變更。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-157">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="ddfd8-158">例如，暫停管線看起來像下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-158">For example, a paused pipeline looks like in the following image:</span></span> 

![管線已暫停](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="ddfd8-160">您可以使用 Ctrl 鍵，以多重選取兩個以上的管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-160">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="ddfd8-161">您可以使用命令列按鈕來同時暫停/繼續多個管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-161">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="ddfd8-162">您也可以用滑鼠右鍵按一下管線，並選取選項來暫停、繼續或終止管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-162">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![管線的內容功能表](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="ddfd8-164">按一下 [開啟管線] 選項，查看管線中的所有活動。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-164">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![開啟管線功能表](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="ddfd8-166">在開啟的管線檢視中，您會看到管線裡的所有活動。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-166">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="ddfd8-167">在這個範例中只有一個活動：複製活動。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-167">In this example, there is only one activity: Copy Activity.</span></span> 

![已開啟的管線](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="ddfd8-169">如要回到上一個檢視，請按一下頂端階層連結功能表中的 Data Factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-169">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="ddfd8-170">在管線檢視中，當您選取某個輸出資料集時，或當您把滑鼠游標移動到輸出資料集上時，您會看到該資料集的 [活動時段] 快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-170">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![活動時段快顯視窗](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="ddfd8-172">只要按一下某個活動時段，即可在右窗格的 [屬性] 視窗中看到該活動時段的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-172">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![活動時段屬性](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="ddfd8-174">在右窗格中，切換到 [活動時段總管] 索引標籤，即可看到更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-174">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="ddfd8-176">您也可以在 [嘗試次數] 區段中看到每個活動執行嘗試的**解析的變數**。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-176">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![解析的變數](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="ddfd8-178">切換至 [指令碼]  索引標籤，以查看所選物件的 JSON 指令碼定義。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-178">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![指令碼索引標籤](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="ddfd8-180">您可以在三個地方看到活動時段：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="ddfd8-181">[圖表檢視] \(中間窗格) 中的 [活動時段] 快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-181">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="ddfd8-182">右窗格中的 [活動時段總管]。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-182">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="ddfd8-183">底部窗格中的 [活動時段] 清單。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-183">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="ddfd8-184">在 [活動時段] 快顯視窗和 [活動時段總管] 中，您可以使用向左箭號和向右箭號來捲動至前一週及下一週。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-184">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![活動時段總管的向左/向右箭號](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="ddfd8-186">在 [圖表檢視] 的底部，您會看到 [放大]、[縮小]、[縮放至適當比例]、[顯示比例 100%]、[鎖定配置] 等按鈕。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-186">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="ddfd8-187">[鎖定配置] 按鈕會防止您在 [圖表檢視] 中不小心移動了資料表和管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-187">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="ddfd8-188">此按鈕預設為開啟。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-188">It's on by default.</span></span> <span data-ttu-id="ddfd8-189">但您可以關閉該設定，以便移動圖表中的實體。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-189">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="ddfd8-190">當您關閉該設定，您可以使用上一個按鈕來自動把資料表和管線移動到適當的地方。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-190">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="ddfd8-191">您也可以使用滑鼠滾輪來放大或縮小。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-191">You can also zoom in or out by using the mouse wheel.</span></span>

![圖表檢視縮放命令](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="ddfd8-193">活動時段清單</span><span class="sxs-lookup"><span data-stu-id="ddfd8-193">Activity Windows list</span></span>
<span data-ttu-id="ddfd8-194">中間窗格底端的 [活動時段] 清單會顯示您在 [資源總管] 或 [圖表檢視] 中所選取資料集的所有活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-194">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="ddfd8-195">根據預設，清單是以遞減的順序排列，這代表清單頂端會是最新的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-195">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![活動時段清單](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="ddfd8-197">這份清單不會自動重新整理，因此請使用工具列上 [重新整理] 按鈕來手動重新整理。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-197">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="ddfd8-198">下列為活動時段的狀態：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-198">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="ddfd8-199">狀態</span><span class="sxs-lookup"><span data-stu-id="ddfd8-199">Status</span></span></th><th align="left"><span data-ttu-id="ddfd8-200">子狀態</span><span class="sxs-lookup"><span data-stu-id="ddfd8-200">Substatus</span></span></th><th align="left"><span data-ttu-id="ddfd8-201">說明</span><span class="sxs-lookup"><span data-stu-id="ddfd8-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="ddfd8-202">等候</span><span class="sxs-lookup"><span data-stu-id="ddfd8-202">Waiting</span></span></td><td><span data-ttu-id="ddfd8-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="ddfd8-203">ScheduleTime</span></span></td><td><span data-ttu-id="ddfd8-204">活動時段執行的時間還沒到。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-204">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="ddfd8-205">DatasetDependencies</span></span></td><td><span data-ttu-id="ddfd8-206">上游相依項目尚未就緒。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-206">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="ddfd8-207">ComputeResources</span></span></td><td><span data-ttu-id="ddfd8-208">計算資源無法使用。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-208">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="ddfd8-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="ddfd8-210">所有活動執行個體都在執行其他的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-210">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="ddfd8-211">ActivityResume</span></span></td><td><span data-ttu-id="ddfd8-212">活動已暫停，除非活動繼續，否則無法執行活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-212">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-213">Retry</span><span class="sxs-lookup"><span data-stu-id="ddfd8-213">Retry</span></span></td><td><span data-ttu-id="ddfd8-214">正在重試活動執行。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-214">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-215">驗證</span><span class="sxs-lookup"><span data-stu-id="ddfd8-215">Validation</span></span></td><td><span data-ttu-id="ddfd8-216">驗證尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="ddfd8-217">ValidationRetry</span></span></td><td><span data-ttu-id="ddfd8-218">驗證正在等待重試。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-218">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="ddfd8-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="ddfd8-219">InProgress</span></span></td><td><span data-ttu-id="ddfd8-220">Validating</span><span class="sxs-lookup"><span data-stu-id="ddfd8-220">Validating</span></span></td><td><span data-ttu-id="ddfd8-221">驗證正在進行中。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="ddfd8-222">系統正在處理該活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-222">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="ddfd8-223">Failed</span><span class="sxs-lookup"><span data-stu-id="ddfd8-223">Failed</span></span></td><td><span data-ttu-id="ddfd8-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="ddfd8-224">TimedOut</span></span></td><td><span data-ttu-id="ddfd8-225">活動執行超過活動所允許的時間。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-225">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="ddfd8-226">Canceled</span></span></td><td><span data-ttu-id="ddfd8-227">使用者動作已取消活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-227">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-228">驗證</span><span class="sxs-lookup"><span data-stu-id="ddfd8-228">Validation</span></span></td><td><span data-ttu-id="ddfd8-229">驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="ddfd8-230">無法產生或驗證活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-230">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="ddfd8-231">就緒</span><span class="sxs-lookup"><span data-stu-id="ddfd8-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="ddfd8-232">活動時段已可供使用。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-232">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-233">Skipped</span><span class="sxs-lookup"><span data-stu-id="ddfd8-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="ddfd8-234">活動時段未處理。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-234">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ddfd8-235">None</span><span class="sxs-lookup"><span data-stu-id="ddfd8-235">None</span></span></td><td>-</td><td><span data-ttu-id="ddfd8-236">曾經以不同的狀態存在，但目前已重設的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-236">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="ddfd8-237">當您按一下清單中的某個活動時段時，您會在右側的 [活動時段總管] 或 [屬性] 視窗中看到其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-237">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="ddfd8-239">重新整理活動時段</span><span class="sxs-lookup"><span data-stu-id="ddfd8-239">Refresh activity windows</span></span>
<span data-ttu-id="ddfd8-240">詳細資料並不會自動重新整理，因此您必須使用命令列上的 [重新整理] 按鈕 (第二個按鈕) 來手動重新整理活動時段清單。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-240">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="ddfd8-241">[屬性] 視窗</span><span class="sxs-lookup"><span data-stu-id="ddfd8-241">Properties window</span></span>
<span data-ttu-id="ddfd8-242">[屬性] 視窗在監視及管理應用程式最右側的窗格中。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-242">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![[屬性] 視窗](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="ddfd8-244">它會顯示您在 [資源總管] \(樹狀檢視)、[圖表檢視] 或 [活動時段清單] 中所選取項目的屬性。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-244">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="ddfd8-245">活動時段總管</span><span class="sxs-lookup"><span data-stu-id="ddfd8-245">Activity Window Explorer</span></span>
<span data-ttu-id="ddfd8-246">[活動時段總管] 視窗在監視及管理應用程式最右側的窗格中。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-246">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="ddfd8-247">它會顯示您在 [活動時段] 快顯視窗或 [活動時段清單] 中所選取活動時段的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-247">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="ddfd8-249">您可以切換至另一個活動時段，方法是按一下頂端行事曆檢視中的其他活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-249">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="ddfd8-250">而頂端的 [向左箭號]/[向右箭號] 按鈕可讓您查看上一週/下一週的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-250">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="ddfd8-251">您可以使用底部窗格中的工具列按鈕重新執行活動時段，或是重新整理窗格中的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-251">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="ddfd8-252">指令碼</span><span class="sxs-lookup"><span data-stu-id="ddfd8-252">Script</span></span>
<span data-ttu-id="ddfd8-253">您可以使用 [指令碼] 索引標籤，檢視所選取 Data Factory 實體 (連結服務、資料集或管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-253">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![指令碼索引標籤](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="ddfd8-255">使用系統檢視</span><span class="sxs-lookup"><span data-stu-id="ddfd8-255">Use system views</span></span>
<span data-ttu-id="ddfd8-256">監視及管理應用程式包含預先建置的系統檢視 (**最近的活動時段**、**失敗的活動時段**、**進行中的活動時段**)，可讓您檢視 Data Factory 最近/失敗/進行中的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-256">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="ddfd8-257">只要按一下左側的 [監視檢視]  索引標籤，就能切換到 [監視檢視]。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-257">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![[監視檢視] 索引標籤](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="ddfd8-259">目前，有三個支援的系統檢視。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="ddfd8-260">請選取某個選項，以便在 [活動時段] 清單 (位於中間窗格底部) 中查看最近的活動時段、失敗的活動時段，或進行中的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-260">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="ddfd8-261">當您選取 [最近的活動時段] 選項時，您會看到以 [上次嘗試時間] 的遞減順序排列之所有最近的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-261">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="ddfd8-262">您可以使用 [失敗的活動時段]  檢視，查看清單中所有失敗的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-262">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="ddfd8-263">選取清單中某個失敗的活動時段，就能在 [屬性] 視窗或 [活動時段總管] 中看到該活動時段的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-263">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="ddfd8-264">您也可以下載失敗的活動時段的任何記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="ddfd8-265">排序與篩選活動時段</span><span class="sxs-lookup"><span data-stu-id="ddfd8-265">Sort and filter activity windows</span></span>
<span data-ttu-id="ddfd8-266">在命令列中變更**開始時間**及**結束時間**設定來篩選活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-266">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="ddfd8-267">當您變更開始時間及結束時間之後，請按一下結束時間旁邊的按鈕來重新整理 [活動時段] 清單。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-267">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![開始及結束時間](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="ddfd8-269">目前，監視及管理應用程式中所有時間都是以 UTC 格式來顯示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-269">Currently, all times are in UTC format in the Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="ddfd8-270">請在 [活動時段清單] 中，按一下某個資料行的名稱 (例如：[狀態])。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-270">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![活動時段清單的資料行功能表](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="ddfd8-272">您可以執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="ddfd8-272">You can do the following:</span></span>

* <span data-ttu-id="ddfd8-273">以遞增順序排序。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-273">Sort in ascending order.</span></span>
* <span data-ttu-id="ddfd8-274">以遞減順序排序。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-274">Sort in descending order.</span></span>
* <span data-ttu-id="ddfd8-275">根據一或多個值 (Ready、Waiting 等) 來篩選。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="ddfd8-276">當您在某個資料行上指定篩選條件時，該資料行的篩選器按鈕就會啟用，以指出該資料行中的值為已經過篩選的值。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-276">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![篩選活動時段清單的資料行](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="ddfd8-278">您可以使用相同的快顯視窗來清除篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-278">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="ddfd8-279">如要清除活動時段清單的所有篩選條件，請按一下命令列上的 [清除篩選條件] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-279">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![清除活動時段清單的所有篩選條件](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="ddfd8-281">執行批次動作</span><span class="sxs-lookup"><span data-stu-id="ddfd8-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="ddfd8-282">重新執行已選取的活動時段</span><span class="sxs-lookup"><span data-stu-id="ddfd8-282">Rerun selected activity windows</span></span>
<span data-ttu-id="ddfd8-283">選取某個活動時段、按一下第一個命令列按鈕旁的向下箭號，然後選取 [重新執行] / [搭配管線上游來重新執行]。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-283">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="ddfd8-284">當您選取 [搭配管線上游來重新執行] 時，系統也會傳回所有上游的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-284">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="ddfd8-285">![重新執行某個活動時段](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="ddfd8-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="ddfd8-286">您也可以選取清單中的數個活動時段，然後同時重新執行這些活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-286">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="ddfd8-287">您可能會想要根據狀態 (例如 [失敗]) 來篩選活動時段，然後在修正導致活動時段執行失敗的問題之後，重新執行失敗的活動時段。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-287">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="ddfd8-288">請參閱下一節來取得如何篩選清單中活動時段的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-288">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="ddfd8-289">暫停/繼續多個管線</span><span class="sxs-lookup"><span data-stu-id="ddfd8-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="ddfd8-290">您可以使用 Ctrl 鍵，以多重選取兩個以上的管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-290">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="ddfd8-291">您可以使用命令列按鈕 (在下圖以紅色矩形反白顯示) 來暫停/繼續這些管線。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-291">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![命令列上的暫停/繼續](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="ddfd8-293">建立警示</span><span class="sxs-lookup"><span data-stu-id="ddfd8-293">Create alerts</span></span>
<span data-ttu-id="ddfd8-294">[警示] 頁面可讓您建立警示，以及檢視/編輯/刪除現有的警示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-294">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="ddfd8-295">您也可以停用/啟用警示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="ddfd8-296">若要查看 [警示] 頁面，請按一下 [警示] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-296">To see the Alerts page, click the **Alerts** tab.</span></span>

![[警示] 索引標籤](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="ddfd8-298">如何建立警示</span><span class="sxs-lookup"><span data-stu-id="ddfd8-298">To create an alert</span></span>
1. <span data-ttu-id="ddfd8-299">按一下 [新增警示]  來新增警示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-299">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="ddfd8-300">此時您會看到 [詳細資料] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-300">You see the **Details** page.</span></span>

    ![建立警示：[詳細資料] 頁面](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="ddfd8-302">指定警示的**名稱**和**說明**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-302">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="ddfd8-303">您應該會看到 [篩選]  頁面。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-303">You should see the **Filters** page.</span></span>

    ![建立警示：[篩選器] 頁面](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="ddfd8-305">選取您想要建立 Data Factory 服務警示的**事件**、**狀態**和**子狀態** (選擇性)，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-305">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="ddfd8-306">您應該會看到 [收件者]  頁面。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-306">You should see the **Recipients** page.</span></span>

    ![建立警示：[收件者] 頁面](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="ddfd8-308">選取 [電子郵件訂用帳戶管理員] 選項並/或輸入**其他管理員的電子郵件**，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-308">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="ddfd8-309">此時您應該會看到警示清單。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-309">You should see the alert in the list.</span></span>

    ![警示清單](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="ddfd8-311">請在 [警示] 清單中，使用與警示相關聯的按鈕來編輯/刪除/停用/啟用警示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-311">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="ddfd8-312">事件/狀態/子狀態</span><span class="sxs-lookup"><span data-stu-id="ddfd8-312">Event/status/substatus</span></span>
<span data-ttu-id="ddfd8-313">下列資料表提供可用事件和狀態 (及子狀態) 的清單。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-313">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="ddfd8-314">事件名稱</span><span class="sxs-lookup"><span data-stu-id="ddfd8-314">Event name</span></span> | <span data-ttu-id="ddfd8-315">狀態</span><span class="sxs-lookup"><span data-stu-id="ddfd8-315">Status</span></span> | <span data-ttu-id="ddfd8-316">子狀態</span><span class="sxs-lookup"><span data-stu-id="ddfd8-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ddfd8-317">活動執行已開始</span><span class="sxs-lookup"><span data-stu-id="ddfd8-317">Activity Run Started</span></span> |<span data-ttu-id="ddfd8-318">已啟動</span><span class="sxs-lookup"><span data-stu-id="ddfd8-318">Started</span></span> |<span data-ttu-id="ddfd8-319">啟動中</span><span class="sxs-lookup"><span data-stu-id="ddfd8-319">Starting</span></span> |
| <span data-ttu-id="ddfd8-320">活動執行已結束</span><span class="sxs-lookup"><span data-stu-id="ddfd8-320">Activity Run Finished</span></span> |<span data-ttu-id="ddfd8-321">Succeeded</span><span class="sxs-lookup"><span data-stu-id="ddfd8-321">Succeeded</span></span> |<span data-ttu-id="ddfd8-322">Succeeded</span><span class="sxs-lookup"><span data-stu-id="ddfd8-322">Succeeded</span></span> |
| <span data-ttu-id="ddfd8-323">活動執行已結束</span><span class="sxs-lookup"><span data-stu-id="ddfd8-323">Activity Run Finished</span></span> |<span data-ttu-id="ddfd8-324">Failed</span><span class="sxs-lookup"><span data-stu-id="ddfd8-324">Failed</span></span> |<span data-ttu-id="ddfd8-325">資源配置失敗</span><span class="sxs-lookup"><span data-stu-id="ddfd8-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="ddfd8-326">執行失敗</span><span class="sxs-lookup"><span data-stu-id="ddfd8-326">Failed Execution</span></span><br/><br/><span data-ttu-id="ddfd8-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="ddfd8-327">Timed Out</span></span><br/><br/><span data-ttu-id="ddfd8-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="ddfd8-328">Failed Validation</span></span><br/><br/><span data-ttu-id="ddfd8-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="ddfd8-329">Abandoned</span></span> |
| <span data-ttu-id="ddfd8-330">已開始建立隨選 HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="ddfd8-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="ddfd8-331">已啟動</span><span class="sxs-lookup"><span data-stu-id="ddfd8-331">Started</span></span> |-|
| <span data-ttu-id="ddfd8-332">已成功建立隨選 HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="ddfd8-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="ddfd8-333">Succeeded</span><span class="sxs-lookup"><span data-stu-id="ddfd8-333">Succeeded</span></span> |-|
| <span data-ttu-id="ddfd8-334">已刪除隨選 HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="ddfd8-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="ddfd8-335">Succeeded</span><span class="sxs-lookup"><span data-stu-id="ddfd8-335">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="ddfd8-336">編輯、刪除或停用警示</span><span class="sxs-lookup"><span data-stu-id="ddfd8-336">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="ddfd8-337">使用下列按鈕 (以紅色反白顯示) 來編輯、刪除或停用警示。</span><span class="sxs-lookup"><span data-stu-id="ddfd8-337">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![警示按鈕](./media/data-factory-monitor-manage-app/AlertButtons.png)
