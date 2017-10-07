---
title: "aaaMonitor 和使用 hello Azure 入口網站和 PowerShell 管理管線 |Microsoft 文件"
description: "了解 toouse hello Azure 入口網站和 Azure PowerShell toomonitor 和管理 hello Azure data factory 和您所建立的管線的方式。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="b1acd-103">監視和管理 Azure Data Factory 管線使用 hello Azure 入口網站和 PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1acd-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1acd-104">使用 Azure 入口網站/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1acd-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="b1acd-105">使用監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="b1acd-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="b1acd-106">hello 監督和管理應用程式提供更佳的支援的監視與管理您的資料管線，以及疑難排解任何問題。</span><span class="sxs-lookup"><span data-stu-id="b1acd-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="b1acd-107">如需有關使用 hello 應用程式的詳細資訊，請參閱[監視和管理使用 hello 監視和管理應用程式的 Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="b1acd-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="b1acd-108">本文說明如何 toomonitor、 管理及使用 Azure 入口網站和 PowerShell 偵錯您的管線。</span><span class="sxs-lookup"><span data-stu-id="b1acd-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="b1acd-109">hello 發行項也會提供資訊 toocreate 警示的方式，以及取得有關失敗的通知。</span><span class="sxs-lookup"><span data-stu-id="b1acd-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="b1acd-110">了解管線和活動狀態</span><span class="sxs-lookup"><span data-stu-id="b1acd-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="b1acd-111">Hello Azure 入口網站，您可以使用：</span><span class="sxs-lookup"><span data-stu-id="b1acd-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="b1acd-112">以圖表形式檢視 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b1acd-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="b1acd-113">檢視管線中的活動。</span><span class="sxs-lookup"><span data-stu-id="b1acd-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="b1acd-114">檢視輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="b1acd-114">View input and output datasets.</span></span>

<span data-ttu-id="b1acd-115">本章節也說明從一個狀態 tooanother 狀態轉換的資料集配量的方式。</span><span class="sxs-lookup"><span data-stu-id="b1acd-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="b1acd-116">瀏覽 tooyour 資料處理站</span><span class="sxs-lookup"><span data-stu-id="b1acd-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="b1acd-117">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b1acd-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b1acd-118">按一下**Data factory** hello hello 左邊的功能表上。</span><span class="sxs-lookup"><span data-stu-id="b1acd-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="b1acd-119">如果您沒有看到它，按一下**更多服務 >**，然後按一下 [ **Data factory**下 hello**智慧 + 分析**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="b1acd-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![全部瀏覽 -> Data Factory](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="b1acd-121">在 [hello **Data factory**刀鋒視窗中，選取 hello 您感興趣的 data factory。</span><span class="sxs-lookup"><span data-stu-id="b1acd-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![選取 Data Factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="b1acd-123">您應該會看到 hello 首頁 hello data factory。</span><span class="sxs-lookup"><span data-stu-id="b1acd-123">You should see hello home page for hello data factory.</span></span>

   ![Data Factory 刀鋒視窗](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="b1acd-125">Data Factory 的圖表檢視</span><span class="sxs-lookup"><span data-stu-id="b1acd-125">Diagram view of your data factory</span></span>
<span data-ttu-id="b1acd-126">hello**圖表**檢視的 data factory 提供單一的半透明 toomonitor 窗格及管理 hello data factory 和其資產。</span><span class="sxs-lookup"><span data-stu-id="b1acd-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="b1acd-127">toosee hello**圖表**您的 data factory 的檢視，請按一下**圖表**hello data factory 的 hello 首頁上。</span><span class="sxs-lookup"><span data-stu-id="b1acd-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![圖表檢視](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="b1acd-129">您可以放大、 縮小，縮放 toofit、 縮放 too100%、 鎖定 hello hello 圖表配置和自動定位管線與資料集。</span><span class="sxs-lookup"><span data-stu-id="b1acd-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="b1acd-130">您也可以查看 hello 資料歷程資訊 （也就是顯示選取項目的上游及下游項目）。</span><span class="sxs-lookup"><span data-stu-id="b1acd-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="b1acd-131">管線中的活動</span><span class="sxs-lookup"><span data-stu-id="b1acd-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="b1acd-132">以滑鼠右鍵按一下 hello 管線，然後按一下**開啟管線**toosee hello 中的所有活動的都管線，以及 hello 活動的輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="b1acd-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="b1acd-133">這項功能時，您的管線包含一個以上的活動和您想要的單一管線 toounderstand hello 作業歷程。</span><span class="sxs-lookup"><span data-stu-id="b1acd-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![開啟管線功能表](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="b1acd-135">在下列範例的 hello，您會看到複製活動中使用輸入和輸出的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="b1acd-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![管線中的活動](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="b1acd-137">您可以巡覽的 hello data factory 的回復 toohello 首頁按一下 hello **Data factory** hello hello 左上角的階層連結中的連結。</span><span class="sxs-lookup"><span data-stu-id="b1acd-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![瀏覽後 toodata factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="b1acd-139">在管線內的每個活動檢視 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="b1acd-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="b1acd-140">您可以藉由檢視任何 hello hello 活動所產生的資料集的 hello 狀態檢視 hello 目前活動的狀態。</span><span class="sxs-lookup"><span data-stu-id="b1acd-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="b1acd-141">按兩下 hello **OutputBlobTable**在 hello**圖表**，您可以看到不同的活動執行內的管線所產生的所有 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="b1acd-142">您可以看到 hello 複製活動已順利執行 hello 最後八小時，以及產生 hello 配量在 hello**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="b1acd-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Hello 管線的狀態](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="b1acd-144">hello hello data factory 中的資料集配量可以具有下列狀態的 hello 其中一項：</span><span class="sxs-lookup"><span data-stu-id="b1acd-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="b1acd-145">State</span><span class="sxs-lookup"><span data-stu-id="b1acd-145">State</span></span></th><th align="left"><span data-ttu-id="b1acd-146">子狀態</span><span class="sxs-lookup"><span data-stu-id="b1acd-146">Substate</span></span></th><th align="left"><span data-ttu-id="b1acd-147">說明</span><span class="sxs-lookup"><span data-stu-id="b1acd-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="b1acd-148">等候</span><span class="sxs-lookup"><span data-stu-id="b1acd-148">Waiting</span></span></td><td><span data-ttu-id="b1acd-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="b1acd-149">ScheduleTime</span></span></td><td><span data-ttu-id="b1acd-150">hello 時間未針對 hello 配量 toorun 發生。</span><span class="sxs-lookup"><span data-stu-id="b1acd-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="b1acd-151">DatasetDependencies</span></span></td><td><span data-ttu-id="b1acd-152">hello 上游相依性未準備好。</span><span class="sxs-lookup"><span data-stu-id="b1acd-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="b1acd-153">ComputeResources</span></span></td><td><span data-ttu-id="b1acd-154">hello 計算資源無法使用。</span><span class="sxs-lookup"><span data-stu-id="b1acd-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="b1acd-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="b1acd-156">所有的 hello 活動執行個體都忙於執行其他配量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="b1acd-157">ActivityResume</span></span></td><td><span data-ttu-id="b1acd-158">hello 活動已暫停，直到繼續 hello 活動無法執行 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-159">Retry</span><span class="sxs-lookup"><span data-stu-id="b1acd-159">Retry</span></span></td><td><span data-ttu-id="b1acd-160">正在重試活動執行。</span><span class="sxs-lookup"><span data-stu-id="b1acd-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-161">驗證</span><span class="sxs-lookup"><span data-stu-id="b1acd-161">Validation</span></span></td><td><span data-ttu-id="b1acd-162">驗證尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="b1acd-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="b1acd-163">ValidationRetry</span></span></td><td><span data-ttu-id="b1acd-164">驗證是等待 toobe 重試。</span><span class="sxs-lookup"><span data-stu-id="b1acd-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="b1acd-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="b1acd-165">InProgress</span></span></td><td><span data-ttu-id="b1acd-166">Validating</span><span class="sxs-lookup"><span data-stu-id="b1acd-166">Validating</span></span></td><td><span data-ttu-id="b1acd-167">驗證正在進行中。</span><span class="sxs-lookup"><span data-stu-id="b1acd-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="b1acd-168">正在處理 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="b1acd-169">Failed</span><span class="sxs-lookup"><span data-stu-id="b1acd-169">Failed</span></span></td><td><span data-ttu-id="b1acd-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="b1acd-170">TimedOut</span></span></td><td><span data-ttu-id="b1acd-171">hello 活動的執行時間超過所允許的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="b1acd-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="b1acd-172">Canceled</span></span></td><td><span data-ttu-id="b1acd-173">使用者動作已取消 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-174">驗證</span><span class="sxs-lookup"><span data-stu-id="b1acd-174">Validation</span></span></td><td><span data-ttu-id="b1acd-175">驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="b1acd-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="b1acd-176">hello 配量無法 toobe 產生及/或驗證。</span><span class="sxs-lookup"><span data-stu-id="b1acd-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="b1acd-177">就緒</span><span class="sxs-lookup"><span data-stu-id="b1acd-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="b1acd-178">hello 配量是供取用。</span><span class="sxs-lookup"><span data-stu-id="b1acd-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-179">Skipped</span><span class="sxs-lookup"><span data-stu-id="b1acd-179">Skipped</span></span></td><td><span data-ttu-id="b1acd-180">None</span><span class="sxs-lookup"><span data-stu-id="b1acd-180">None</span></span></td><td><span data-ttu-id="b1acd-181">不是正在處理 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="b1acd-182">None</span><span class="sxs-lookup"><span data-stu-id="b1acd-182">None</span></span></td><td>-</td><td><span data-ttu-id="b1acd-183">配量 tooexist 搭配不同的狀態，但已重設。</span><span class="sxs-lookup"><span data-stu-id="b1acd-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="b1acd-184">您可以檢視 hello 配量的詳細資料，依序按一下 [配量上的項目 hello**最近更新配量**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b1acd-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![配量的詳細資料](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="b1acd-186">如果已經執行多次 hello 配量，您會看到多重資料列的 hello**活動執行**清單。</span><span class="sxs-lookup"><span data-stu-id="b1acd-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="b1acd-187">您可以檢視活動按一下 hello 中的 hello 執行項目，以執行詳細**活動執行**清單。</span><span class="sxs-lookup"><span data-stu-id="b1acd-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="b1acd-188">hello 清單會顯示所有 hello 記錄檔，以及錯誤訊息，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="b1acd-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="b1acd-189">此功能十分有用 tooview 和偵錯記錄檔，而不需要 tooleave 您的 data factory。</span><span class="sxs-lookup"><span data-stu-id="b1acd-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![活動執行詳細資料](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="b1acd-191">如果 hello 配量不在 hello**準備**狀態，您可以看到未準備好並封鎖 hello hello 中執行的目前配量的 hello 上游配量**未就緒的上游配量**清單。</span><span class="sxs-lookup"><span data-stu-id="b1acd-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="b1acd-192">在您的配量時，此功能十分有用**等候**狀態和您想要在等待 toounderstand hello 上游相依性 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![尚未就緒的上游配量](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="b1acd-194">資料集狀態圖表</span><span class="sxs-lookup"><span data-stu-id="b1acd-194">Dataset state diagram</span></span>
<span data-ttu-id="b1acd-195">部署 data factory hello 管線有有效的使用中期間後，hello 資料集配量從一個狀態 tooanother 轉換。</span><span class="sxs-lookup"><span data-stu-id="b1acd-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="b1acd-196">目前，hello 配量狀態會遵循下列狀態圖表 hello:</span><span class="sxs-lookup"><span data-stu-id="b1acd-196">Currently, hello slice status follows hello following state diagram:</span></span>

![狀態圖表](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="b1acd-198">hello data factory 中的資料集的狀態轉換流量是 hello 下列： 等候]-> [進度/中-進行中 （驗證）]-> [已備妥/失敗。</span><span class="sxs-lookup"><span data-stu-id="b1acd-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="b1acd-199">的 hello 配量開始**等候**先決條件 toobe 符合其執行之前所等候的狀態。</span><span class="sxs-lookup"><span data-stu-id="b1acd-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="b1acd-200">Hello 活動開始執行，然後 hello 配量進入**In-progress**狀態。</span><span class="sxs-lookup"><span data-stu-id="b1acd-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="b1acd-201">hello 活動執行可能會成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="b1acd-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="b1acd-202">hello 配量會標示為**準備**或**失敗**根據 hello hello 執行結果。</span><span class="sxs-lookup"><span data-stu-id="b1acd-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="b1acd-203">您可以重設回從 hello hello 配量 toogo**準備**或**失敗**狀態 toohello**等候**狀態。</span><span class="sxs-lookup"><span data-stu-id="b1acd-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="b1acd-204">也可以將 hello 配量狀態太**略過**，這樣就不會執行和不處理 hello 配量的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="b1acd-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="b1acd-205">暫停及繼續管線</span><span class="sxs-lookup"><span data-stu-id="b1acd-205">Pause and resume pipelines</span></span>
<span data-ttu-id="b1acd-206">您可以使用 Azure Powershell 管理您的管線。</span><span class="sxs-lookup"><span data-stu-id="b1acd-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="b1acd-207">例如，您可以執行 Azure PowerShell Cmdlet 來暫停和繼續執行管線。</span><span class="sxs-lookup"><span data-stu-id="b1acd-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="b1acd-208">hello 圖表檢視不支援暫停和繼續管線。</span><span class="sxs-lookup"><span data-stu-id="b1acd-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="b1acd-209">如果您想 toouse 使用者介面時，使用 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1acd-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="b1acd-210">如需有關使用 hello 應用程式的詳細資訊，請參閱[監視和管理使用 hello 監視和管理應用程式的 Data Factory 管線](data-factory-monitor-manage-app.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="b1acd-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="b1acd-211">您可以暫停/暫停管線使用 hello**暫停 AzureRmDataFactoryPipeline** PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b1acd-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="b1acd-212">這個指令程式時，您不想 toorun 管線直到問題得到解決為止。</span><span class="sxs-lookup"><span data-stu-id="b1acd-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="b1acd-213">例如：</span><span class="sxs-lookup"><span data-stu-id="b1acd-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="b1acd-214">Hello 管線與已修正 hello 問題之後，您可以藉由執行下列 PowerShell 命令的 hello 繼續暫停的 hello 管線：</span><span class="sxs-lookup"><span data-stu-id="b1acd-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="b1acd-215">例如：</span><span class="sxs-lookup"><span data-stu-id="b1acd-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="b1acd-216">偵錯管線</span><span class="sxs-lookup"><span data-stu-id="b1acd-216">Debug pipelines</span></span>
<span data-ttu-id="b1acd-217">Azure Data Factory toodebug 為您提供豐富的功能，並使用 hello Azure 入口網站和 Azure PowerShell 來進行疑難排解管線。</span><span class="sxs-lookup"><span data-stu-id="b1acd-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="b1acd-218">[!請注意} 很容易 tootroubleshot 使用錯誤 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1acd-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="b1acd-219">如需有關使用 hello 應用程式的詳細資訊，請參閱[監視和管理使用 hello 監視和管理應用程式的 Data Factory 管線](data-factory-monitor-manage-app.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="b1acd-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="b1acd-220">尋找管線中的錯誤</span><span class="sxs-lookup"><span data-stu-id="b1acd-220">Find errors in a pipeline</span></span>
<span data-ttu-id="b1acd-221">Hello 活動執行會在管線中失敗，hello hello 管線所產生的資料集處於錯誤狀態是因為 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="b1acd-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="b1acd-222">您可以偵錯，並使用下列方法 hello 疑難排解 Azure Data Factory 中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="b1acd-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="b1acd-223">使用 Azure 入口網站 toodebug 錯誤 hello</span><span class="sxs-lookup"><span data-stu-id="b1acd-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="b1acd-224">在 [hello**資料表**刀鋒視窗中，按一下具有 hello hello 問題配量**狀態**設定得**失敗**。</span><span class="sxs-lookup"><span data-stu-id="b1acd-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![含有問題配量的資料表刀鋒視窗](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="b1acd-226">在 [hello**資料配量**刀鋒視窗中，按一下 hello 活動執行失敗。</span><span class="sxs-lookup"><span data-stu-id="b1acd-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![發生錯誤的資料配量](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="b1acd-228">在 [hello**活動執行詳細資料**刀鋒視窗中，您可以下載 hello HDInsight 處理相關聯的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b1acd-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="b1acd-229">按一下**下載**狀態/stderr toodownload hello 錯誤記錄檔，其中包含關於 hello 錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b1acd-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![含有錯誤的活動執行詳細資料刀鋒視窗](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="b1acd-231">使用 PowerShell toodebug 錯誤</span><span class="sxs-lookup"><span data-stu-id="b1acd-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="b1acd-232">啟動 **PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="b1acd-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="b1acd-233">執行 hello **Get AzureRmDataFactorySlice**命令 toosee hello 配量和其狀態。</span><span class="sxs-lookup"><span data-stu-id="b1acd-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="b1acd-234">您應該會看見 hello 狀態顯示為配量**失敗**。</span><span class="sxs-lookup"><span data-stu-id="b1acd-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="b1acd-235">例如：</span><span class="sxs-lookup"><span data-stu-id="b1acd-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="b1acd-236">將 **StartDateTime** 取代為您的管線開始時間。</span><span class="sxs-lookup"><span data-stu-id="b1acd-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="b1acd-237">現在，執行 hello **Get AzureRmDataFactoryRun** cmdlet tooget 詳細 hello 活動執行 hello 配量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="b1acd-238">例如：</span><span class="sxs-lookup"><span data-stu-id="b1acd-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="b1acd-239">StartDateTime hello 值為 hello 您從 hello 上一個步驟記下的 hello 錯誤/問題配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="b1acd-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="b1acd-240">hello 日期-時間應該用雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="b1acd-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="b1acd-241">您應該會看到類似 toohello 下列 hello 錯誤的相關詳細資料的輸出：</span><span class="sxs-lookup"><span data-stu-id="b1acd-241">You should see output with details about hello error that is similar toohello following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="b1acd-242">您可以執行 hello**儲存 AzureRmDataFactoryLog** cmdlet 搭配您從 hello 輸出，請參閱，以及使用 hello 下載 hello 記錄檔的識別碼值 hello **-DownloadLogsoption** hello 指令程式。</span><span class="sxs-lookup"><span data-stu-id="b1acd-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="b1acd-243">重新執行管線中的失敗</span><span class="sxs-lookup"><span data-stu-id="b1acd-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1acd-244">它是更容易 tootroubleshoot 錯誤，而且使用重新執行失敗的配量 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1acd-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="b1acd-245">如需有關使用 hello 應用程式的詳細資訊，請參閱[監視和管理使用 hello 監視和管理應用程式的 Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="b1acd-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="b1acd-246">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b1acd-246">Use hello Azure portal</span></span>
<span data-ttu-id="b1acd-247">在疑難排解和偵錯在管線中的失敗之後，您可重新執行失敗瀏覽 toohello 錯誤配量，然後按一下 hello**執行**hello 命令列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1acd-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![重新執行失敗的配量](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="b1acd-249">萬一 hello 配量驗證失敗是因為原則錯誤 （例如，如果資料無法使用），您可以修正 hello 失敗，並依序按一下 hello 重新驗證**驗證**hello 命令列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1acd-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![修正錯誤並進行驗證](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="b1acd-251">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1acd-251">Use Azure PowerShell</span></span>
<span data-ttu-id="b1acd-252">您可以使用 hello 重新執行失敗**組 AzureRmDataFactorySliceStatus** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b1acd-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="b1acd-253">請參閱 hello[組 AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx)的語法和 hello 指令程式的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b1acd-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="b1acd-254">**範例：**</span><span class="sxs-lookup"><span data-stu-id="b1acd-254">**Example:**</span></span>

<span data-ttu-id="b1acd-255">hello 下列範例會設定所有的扇區的 hello 資料表 'DAWikiAggregatedData' too'Waiting hello 狀態 ' hello Azure data factory 'WikiADF' 中。</span><span class="sxs-lookup"><span data-stu-id="b1acd-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="b1acd-256">設定 too'UpstreamInPipeline 'P' hello '，這表示 hello 資料表的每個配量和所有相依 （上游） 資料表 hello 的狀態會設定 too'Waiting'。</span><span class="sxs-lookup"><span data-stu-id="b1acd-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="b1acd-257">hello 其他可能的值，這個參數為 「 個人 」。</span><span class="sxs-lookup"><span data-stu-id="b1acd-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="b1acd-258">建立警示</span><span class="sxs-lookup"><span data-stu-id="b1acd-258">Create alerts</span></span>
<span data-ttu-id="b1acd-259">當建立、更新或刪除 Azure 資料時 (例如 Data Factory)，Azure 會記錄使用者事件。</span><span class="sxs-lookup"><span data-stu-id="b1acd-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="b1acd-260">您可以對這些事件建立警示。</span><span class="sxs-lookup"><span data-stu-id="b1acd-260">You can create alerts on these events.</span></span> <span data-ttu-id="b1acd-261">您可以使用 Data Factory toocapture 多種標準，以及建立度量的警示。</span><span class="sxs-lookup"><span data-stu-id="b1acd-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="b1acd-262">我們建議您使用事件來進行即時監視，使用度量來做歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="b1acd-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="b1acd-263">事件警示</span><span class="sxs-lookup"><span data-stu-id="b1acd-263">Alerts on events</span></span>
<span data-ttu-id="b1acd-264">Azure 事件可讓您深入了解 Azure 資源的情況。</span><span class="sxs-lookup"><span data-stu-id="b1acd-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="b1acd-265">使用 Azure Data Factory 時，下列情況會產生事件：</span><span class="sxs-lookup"><span data-stu-id="b1acd-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="b1acd-266">建立、更新或刪除 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b1acd-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="b1acd-267">資料處理 (「回合」形式) 已開始或完成。</span><span class="sxs-lookup"><span data-stu-id="b1acd-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="b1acd-268">建立或移除隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b1acd-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="b1acd-269">您可以建立這些使用者事件的警示，並設定它們 toosend 電子郵件通知 toohello 系統管理員和 coadministrators hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1acd-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="b1acd-270">此外，您可以指定符合 hello 條件時，需要 tooreceive 電子郵件通知的使用者的其他電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b1acd-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="b1acd-271">當您要 tooget 在失敗時收到通知，而且不想 toocontinuously 監視您的 data factory，這個功能會很有用。</span><span class="sxs-lookup"><span data-stu-id="b1acd-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="b1acd-272">目前，hello 入口網站不會顯示警示的事件。</span><span class="sxs-lookup"><span data-stu-id="b1acd-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="b1acd-273">使用 hello[監視和管理應用程式](data-factory-monitor-manage-app.md)toosee 所有警示。</span><span class="sxs-lookup"><span data-stu-id="b1acd-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="b1acd-274">指定警示定義</span><span class="sxs-lookup"><span data-stu-id="b1acd-274">Specify an alert definition</span></span>
<span data-ttu-id="b1acd-275">toospecify 警示定義，您會建立描述要 toobe 上發生警示的 hello 作業的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="b1acd-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="b1acd-276">在下列範例的 hello，hello 警示會傳送 hello RunFinished 作業的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="b1acd-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="b1acd-277">toobe 特定電子郵件通知會傳送 hello data factory 中的執行已完成，而且 hello 執行失敗時 (狀態 = FailedExecution)。</span><span class="sxs-lookup"><span data-stu-id="b1acd-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="b1acd-278">您可以移除**子狀態**從 hello JSON 定義，如果您不想 toobe 特定失敗的警示。</span><span class="sxs-lookup"><span data-stu-id="b1acd-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="b1acd-279">此範例會設定您的訂用帳戶中的所有資料處理站的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="b1acd-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="b1acd-280">如果您想 hello 警示 toobe 設定特定的資料處理站，您可以指定資料處理站**resourceUri**在 hello **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="b1acd-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="b1acd-281">hello 下表提供 hello 清單可用的作業和狀態 （和子狀態）。</span><span class="sxs-lookup"><span data-stu-id="b1acd-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="b1acd-282">作業名稱</span><span class="sxs-lookup"><span data-stu-id="b1acd-282">Operation name</span></span> | <span data-ttu-id="b1acd-283">狀態</span><span class="sxs-lookup"><span data-stu-id="b1acd-283">Status</span></span> | <span data-ttu-id="b1acd-284">子狀態</span><span class="sxs-lookup"><span data-stu-id="b1acd-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1acd-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="b1acd-285">RunStarted</span></span> |<span data-ttu-id="b1acd-286">已啟動</span><span class="sxs-lookup"><span data-stu-id="b1acd-286">Started</span></span> |<span data-ttu-id="b1acd-287">啟動中</span><span class="sxs-lookup"><span data-stu-id="b1acd-287">Starting</span></span> |
| <span data-ttu-id="b1acd-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="b1acd-288">RunFinished</span></span> |<span data-ttu-id="b1acd-289">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="b1acd-289">Failed / Succeeded</span></span> |<span data-ttu-id="b1acd-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="b1acd-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="b1acd-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="b1acd-291">Succeeded</span></span><br/><br/><span data-ttu-id="b1acd-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="b1acd-292">FailedExecution</span></span><br/><br/><span data-ttu-id="b1acd-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="b1acd-293">TimedOut</span></span><br/><br/><span data-ttu-id="b1acd-294"><已取消</span><span class="sxs-lookup"><span data-stu-id="b1acd-294"><Canceled</span></span><br/><br/><span data-ttu-id="b1acd-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="b1acd-295">FailedValidation</span></span><br/><br/><span data-ttu-id="b1acd-296">Abandoned</span><span class="sxs-lookup"><span data-stu-id="b1acd-296">Abandoned</span></span> |
| <span data-ttu-id="b1acd-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="b1acd-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="b1acd-298">已啟動</span><span class="sxs-lookup"><span data-stu-id="b1acd-298">Started</span></span> | |
| <span data-ttu-id="b1acd-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="b1acd-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="b1acd-300">Succeeded</span><span class="sxs-lookup"><span data-stu-id="b1acd-300">Succeeded</span></span> | |
| <span data-ttu-id="b1acd-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="b1acd-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="b1acd-302">Succeeded</span><span class="sxs-lookup"><span data-stu-id="b1acd-302">Succeeded</span></span> | |

<span data-ttu-id="b1acd-303">請參閱[建立警示規則](https://msdn.microsoft.com/library/azure/dn510366.aspx)hello hello 範例中使用的 JSON 元素的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b1acd-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="b1acd-304">部署 hello 警示</span><span class="sxs-lookup"><span data-stu-id="b1acd-304">Deploy hello alert</span></span>
<span data-ttu-id="b1acd-305">toodeploy hello 警示，請使用 hello Azure PowerShell 指令程式**新增 AzureRmResourceGroupDeployment**hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b1acd-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="b1acd-306">Hello 資源群組部署已順利完成之後，您會看到下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="b1acd-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="b1acd-307">您可以使用 hello[建立警示規則](https://msdn.microsoft.com/library/azure/dn510366.aspx)REST API toocreate 警示規則。</span><span class="sxs-lookup"><span data-stu-id="b1acd-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="b1acd-308">hello JSON 裝載是類似 toohello JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="b1acd-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="b1acd-309">擷取 Azure 資源群組部署的 hello 的清單</span><span class="sxs-lookup"><span data-stu-id="b1acd-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="b1acd-310">tooretrieve hello 清單部署 Azure 資源群組部署，請使用 hello cmdlet **Get AzureRmResourceGroupDeployment**hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b1acd-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="b1acd-311">使用者事件疑難排解</span><span class="sxs-lookup"><span data-stu-id="b1acd-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="b1acd-312">您可以查看所有 hello 事件產生後按一下 hello**度量和作業**磚。</span><span class="sxs-lookup"><span data-stu-id="b1acd-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![度量和作業圖格](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="b1acd-314">按一下 hello**事件**磚 toosee hello 事件。</span><span class="sxs-lookup"><span data-stu-id="b1acd-314">Click hello **Events** tile toosee hello events.</span></span>

    ![[事件] 磚](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="b1acd-316">在 [hello**事件**刀鋒視窗中，您可以看到事件、 已篩選的事件，等等的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b1acd-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![事件刀鋒視窗](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="b1acd-318">按一下**作業**hello 作業的清單中，會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="b1acd-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![選取作業](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="b1acd-320">按一下**錯誤**hello 錯誤的相關事件 toosee 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b1acd-320">Click an **Error** event toosee details about hello error.</span></span>

    ![事件錯誤](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="b1acd-322">請參閱[Azure Insight cmdlet](https://msdn.microsoft.com/library/mt282452.aspx) PowerShell 指令程式，您可以使用 tooadd，或以移除警示。</span><span class="sxs-lookup"><span data-stu-id="b1acd-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="b1acd-323">以下是一些使用 hello 範例**Get AlertRule** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b1acd-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="b1acd-324">執行的 hello 下列 get-help 命令 toosee 詳細資料及 hello Get AlertRule cmdlet 的範例。</span><span class="sxs-lookup"><span data-stu-id="b1acd-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="b1acd-325">如果您看到 hello 警示產生事件 hello 入口網站的刀鋒視窗，但不是會收到電子郵件通知，請檢查指定的 hello 電子郵件地址從外部寄件者是否設定 tooreceive 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b1acd-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="b1acd-326">電子郵件設定可能已封鎖 hello 警示的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b1acd-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="b1acd-327">度量的警示</span><span class="sxs-lookup"><span data-stu-id="b1acd-327">Alerts on metrics</span></span>
<span data-ttu-id="b1acd-328">您可以在 Data Factory 中擷取各種度量並建立度量警示。</span><span class="sxs-lookup"><span data-stu-id="b1acd-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="b1acd-329">您可以監視和 hello 下列度量資訊。 您的 data factory 中的 hello 扇區上建立警示：</span><span class="sxs-lookup"><span data-stu-id="b1acd-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="b1acd-330">**失敗的執行**</span><span class="sxs-lookup"><span data-stu-id="b1acd-330">**Failed Runs**</span></span>
* <span data-ttu-id="b1acd-331">**成功的執行**</span><span class="sxs-lookup"><span data-stu-id="b1acd-331">**Successful Runs**</span></span>

<span data-ttu-id="b1acd-332">這些度量資訊會很有用，並且協助您 tooget hello data factory 中執行的整體失敗和成功的概觀。</span><span class="sxs-lookup"><span data-stu-id="b1acd-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="b1acd-333">每次有配量執行時就會發出度量。</span><span class="sxs-lookup"><span data-stu-id="b1acd-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="b1acd-334">在 hello 開頭 hello 小時，這些度量會彙總，推入 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1acd-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="b1acd-335">tooenable 度量設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1acd-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="b1acd-336">啟用度量</span><span class="sxs-lookup"><span data-stu-id="b1acd-336">Enable metrics</span></span>
<span data-ttu-id="b1acd-337">tooenable 度量，按一下 [從 hello hello 下列**Data Factory**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="b1acd-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="b1acd-338">[監視] > [度量] > [診斷設定] > [診斷]</span><span class="sxs-lookup"><span data-stu-id="b1acd-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![診斷連結](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="b1acd-340">在 [hello**診斷**刀鋒視窗中，按一下 [**上**，選取 hello 儲存體帳戶，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="b1acd-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![[診斷] 刀鋒視窗](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="b1acd-342">它可能會佔用 hello 度量 toobe hello 上可見的 tooone 小時**監視**刀鋒視窗因為度量彙總每小時發生。</span><span class="sxs-lookup"><span data-stu-id="b1acd-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="b1acd-343">設定度量警示</span><span class="sxs-lookup"><span data-stu-id="b1acd-343">Set up an alert on metrics</span></span>
<span data-ttu-id="b1acd-344">按一下 hello **Data Factory 度量**磚：</span><span class="sxs-lookup"><span data-stu-id="b1acd-344">Click hello **Data Factory metrics** tile:</span></span>

![Data Factory 度量圖格](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="b1acd-346">在 [hello**度量**刀鋒視窗中，按一下 [ **+ 新增警示**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="b1acd-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="b1acd-347">![Data Factory 度量刀鋒視窗 > 新增警示](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="b1acd-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="b1acd-348">在 [hello**加入警示規則**頁面上，執行 hello 下列步驟，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="b1acd-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="b1acd-349">輸入 hello 警示的名稱 (範例: 「 失敗通知 」)。</span><span class="sxs-lookup"><span data-stu-id="b1acd-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="b1acd-350">輸入 hello 警示的描述 (範例: 「 發生失敗時傳送電子郵件 」)。</span><span class="sxs-lookup"><span data-stu-id="b1acd-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="b1acd-351">選取度量 (「失敗的執行」與「成功的執行」)。</span><span class="sxs-lookup"><span data-stu-id="b1acd-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="b1acd-352">指定條件和臨界值。</span><span class="sxs-lookup"><span data-stu-id="b1acd-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="b1acd-353">指定 hello 一段時間。</span><span class="sxs-lookup"><span data-stu-id="b1acd-353">Specify hello period of time.</span></span>
* <span data-ttu-id="b1acd-354">指定 tooowners、 參與者與讀者，是否應傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b1acd-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Data Factory 度量刀鋒視窗 > 新增警示規則](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="b1acd-356">Hello 警示規則已順利新增，hello 刀鋒視窗會關閉，您看到 hello 新的警示上 hello 之後**度量**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b1acd-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Data Factory 度量刀鋒視窗 > 已新增警示](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="b1acd-358">您也應該會看到 hello hello 中的警示數目**警示規則**磚。</span><span class="sxs-lookup"><span data-stu-id="b1acd-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="b1acd-359">按一下 hello**警示規則**磚。</span><span class="sxs-lookup"><span data-stu-id="b1acd-359">Click hello **Alert rules** tile.</span></span>

![Data Factory 度量刀鋒視窗 - 新增規則](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="b1acd-361">在 [hello**警示規則**刀鋒視窗中，您會看到任何現有的警示。</span><span class="sxs-lookup"><span data-stu-id="b1acd-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="b1acd-362">按一下警示，tooadd**新增警示**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="b1acd-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![警示規則刀鋒視窗](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="b1acd-364">警示通知</span><span class="sxs-lookup"><span data-stu-id="b1acd-364">Alert notifications</span></span>
<span data-ttu-id="b1acd-365">Hello 警示規則的比對 hello 條件之後，您應該取得指出啟動 hello 警示的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b1acd-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="b1acd-366">Hello 問題已解決和 hello 警示條件不符合不再之後，您會收到電子郵件，指出 hello 警示已解決。</span><span class="sxs-lookup"><span data-stu-id="b1acd-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="b1acd-367">此行為不同於事件，其會針對警示規則相符的每個失敗傳送通知。</span><span class="sxs-lookup"><span data-stu-id="b1acd-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="b1acd-368">使用 PowerShell 部署警示</span><span class="sxs-lookup"><span data-stu-id="b1acd-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="b1acd-369">您可以部署警示，如度量 hello 相同事件的方式。</span><span class="sxs-lookup"><span data-stu-id="b1acd-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="b1acd-370">**警示定義**</span><span class="sxs-lookup"><span data-stu-id="b1acd-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="b1acd-371">取代*subscriptionId*， *resourceGroupName*，和*dataFactoryName* hello 範例以適當的值。</span><span class="sxs-lookup"><span data-stu-id="b1acd-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="b1acd-372">metricName 目前支援兩個值︰</span><span class="sxs-lookup"><span data-stu-id="b1acd-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="b1acd-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="b1acd-373">FailedRuns</span></span>
* <span data-ttu-id="b1acd-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="b1acd-374">SuccessfulRuns</span></span>

<span data-ttu-id="b1acd-375">**部署 hello 警示**</span><span class="sxs-lookup"><span data-stu-id="b1acd-375">**Deploy hello alert**</span></span>

<span data-ttu-id="b1acd-376">toodeploy hello 警示，請使用 hello Azure PowerShell 指令程式**新增 AzureRmResourceGroupDeployment**hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b1acd-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="b1acd-377">您應該會在部署成功後看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="b1acd-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="b1acd-378">您也可以使用 hello**新增 AlertRule** cmdlet toodeploy 警示規則。</span><span class="sxs-lookup"><span data-stu-id="b1acd-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="b1acd-379">請參閱 hello[新增 AlertRule](https://msdn.microsoft.com/library/mt282468.aspx)如需詳細資訊與範例的主題。</span><span class="sxs-lookup"><span data-stu-id="b1acd-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="b1acd-380">移動資料 factory tooa 不同的資源群組或訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b1acd-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="b1acd-381">您可以移動資料 factory tooa 不同的資源群組或不同的訂用帳戶使用 hello**移動**命令列上的 data factory 的 hello 首頁上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1acd-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![移動 Data Factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="b1acd-383">您也可以移動任何相關的資源 （例如警示與 hello data factory 相關聯），以及 hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="b1acd-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![移動資源對話方塊](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
