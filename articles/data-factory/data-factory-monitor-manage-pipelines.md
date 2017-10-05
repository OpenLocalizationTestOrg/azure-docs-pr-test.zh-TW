---
title: "使用 Azure 入口網站和 PowerShell 監視和管理管線 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站和 Azure PowerShell 監視並管理您建立的 Azure 資料處理站和管線。"
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
ms.openlocfilehash: 61bb5379cd94dd00814e14420947e7783999ff0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="f1afd-103">使用 Azure 入口網站和 PowerShell 監視和管理 Azure Data Factory 管線</span><span class="sxs-lookup"><span data-stu-id="f1afd-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1afd-104">使用 Azure 入口網站/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1afd-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="f1afd-105">使用監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="f1afd-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="f1afd-106">監視及管理應用程式對監視及管理您的資料管線，以及針對任何問題進行疑難排解，提供更佳的支援。</span><span class="sxs-lookup"><span data-stu-id="f1afd-106">The monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="f1afd-107">如需使用應用程式的詳細資訊，請參閱[使用監視及管理應用程式來監視及管理 Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-107">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="f1afd-108">本文描述如何使用 Azure 入口網站和 PowerShell 來監視、管理和偵錯您的管線。</span><span class="sxs-lookup"><span data-stu-id="f1afd-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="f1afd-109">本文也會提供如何建立警示和取得失敗通知的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f1afd-109">The article also provides information on how to create alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="f1afd-110">了解管線和活動狀態</span><span class="sxs-lookup"><span data-stu-id="f1afd-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="f1afd-111">藉由使用 Azure 入口網站，您可以：</span><span class="sxs-lookup"><span data-stu-id="f1afd-111">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="f1afd-112">以圖表形式檢視 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="f1afd-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="f1afd-113">檢視管線中的活動。</span><span class="sxs-lookup"><span data-stu-id="f1afd-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="f1afd-114">檢視輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="f1afd-114">View input and output datasets.</span></span>

<span data-ttu-id="f1afd-115">本節也描述資料集配量從某個狀態轉換至另一個狀態的方法。</span><span class="sxs-lookup"><span data-stu-id="f1afd-115">This section also describes how a dataset slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="f1afd-116">瀏覽至您的 Data Factory</span><span class="sxs-lookup"><span data-stu-id="f1afd-116">Navigate to your data factory</span></span>
1. <span data-ttu-id="f1afd-117">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f1afd-118">按一下左邊功能表的 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-118">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="f1afd-119">如果沒看見，請按一下 [更多服務]，然後在 [智慧 + 分析] 類別底下按一下 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-119">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![全部瀏覽 -> Data Factory](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="f1afd-121">在 [Data Factory] 刀鋒視窗中，選取您感興趣的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="f1afd-121">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![選取 Data Factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="f1afd-123">您應該會看到 Data Factory 的首頁。</span><span class="sxs-lookup"><span data-stu-id="f1afd-123">You should see the home page for the data factory.</span></span>

   ![Data Factory 刀鋒視窗](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="f1afd-125">Data Factory 的圖表檢視</span><span class="sxs-lookup"><span data-stu-id="f1afd-125">Diagram view of your data factory</span></span>
<span data-ttu-id="f1afd-126">Data Factory 的 [圖表] 檢視提供單一窗格，可用來監視和管理 Data Factory 及其資產。</span><span class="sxs-lookup"><span data-stu-id="f1afd-126">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span> <span data-ttu-id="f1afd-127">若要查看 Data Factory 的 [圖表] 檢視，請按一下 Data Factory 首頁上的 [圖表]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-127">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![圖表檢視](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="f1afd-129">您可以將圖表配置放大、縮小、縮放至適當比例、放大到 100% 和鎖定，以及自動定位管線和資料集。</span><span class="sxs-lookup"><span data-stu-id="f1afd-129">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="f1afd-130">您也可以查看資料歷程資訊 (也就是顯示所選取項目的上游和下游項目)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-130">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="f1afd-131">管線中的活動</span><span class="sxs-lookup"><span data-stu-id="f1afd-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="f1afd-132">在管線上按一下滑鼠右鍵，然後按一下 [開啟管線]，就能查看所有管線中的活動，以及活動的輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="f1afd-132">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="f1afd-133">當您的管線有超過一個的活動且您想了解單一管線的作業歷程時，這個功能會非常有用。</span><span class="sxs-lookup"><span data-stu-id="f1afd-133">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![開啟管線功能表](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="f1afd-135">在下列範例中，您會在具有輸入與輸出的管線中看到複製活動。</span><span class="sxs-lookup"><span data-stu-id="f1afd-135">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![管線中的活動](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="f1afd-137">您可以按一下左上角階層連結中的 [Data Factory] 連結，瀏覽回 Data Factory 首頁。</span><span class="sxs-lookup"><span data-stu-id="f1afd-137">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![瀏覽回到 Data Factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="f1afd-139">管線中每個活動的檢視狀態</span><span class="sxs-lookup"><span data-stu-id="f1afd-139">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="f1afd-140">您可以藉由檢視活動所產生的任何資料集的狀態，查看活動的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="f1afd-140">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="f1afd-141">按兩次 [圖表] 中的 **OutputBlobTable**，您就會看到管線中不同活動執行時所產生的所有配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-141">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="f1afd-142">您可以看到複製活動在過去八個月來每個月都執行成功，且所產生的配量都處於「就緒」狀態。</span><span class="sxs-lookup"><span data-stu-id="f1afd-142">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![管線的狀態](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="f1afd-144">Data Factory 中的資料集配量可以有下列狀態之一：</span><span class="sxs-lookup"><span data-stu-id="f1afd-144">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="f1afd-145">State</span><span class="sxs-lookup"><span data-stu-id="f1afd-145">State</span></span></th><th align="left"><span data-ttu-id="f1afd-146">子狀態</span><span class="sxs-lookup"><span data-stu-id="f1afd-146">Substate</span></span></th><th align="left"><span data-ttu-id="f1afd-147">說明</span><span class="sxs-lookup"><span data-stu-id="f1afd-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="f1afd-148">等候</span><span class="sxs-lookup"><span data-stu-id="f1afd-148">Waiting</span></span></td><td><span data-ttu-id="f1afd-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="f1afd-149">ScheduleTime</span></span></td><td><span data-ttu-id="f1afd-150">尚未到達執行配量的時間。</span><span class="sxs-lookup"><span data-stu-id="f1afd-150">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="f1afd-151">DatasetDependencies</span></span></td><td><span data-ttu-id="f1afd-152">上游相依項目尚未就緒。</span><span class="sxs-lookup"><span data-stu-id="f1afd-152">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="f1afd-153">ComputeResources</span></span></td><td><span data-ttu-id="f1afd-154">計算資源無法使用。</span><span class="sxs-lookup"><span data-stu-id="f1afd-154">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="f1afd-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="f1afd-156">所有活動執行個體都忙於執行其他配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-156">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="f1afd-157">ActivityResume</span></span></td><td><span data-ttu-id="f1afd-158">活動已暫停，除非活動繼續，否則無法執行配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-158">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-159">Retry</span><span class="sxs-lookup"><span data-stu-id="f1afd-159">Retry</span></span></td><td><span data-ttu-id="f1afd-160">正在重試活動執行。</span><span class="sxs-lookup"><span data-stu-id="f1afd-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-161">驗證</span><span class="sxs-lookup"><span data-stu-id="f1afd-161">Validation</span></span></td><td><span data-ttu-id="f1afd-162">驗證尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="f1afd-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="f1afd-163">ValidationRetry</span></span></td><td><span data-ttu-id="f1afd-164">驗證正在等待重試。</span><span class="sxs-lookup"><span data-stu-id="f1afd-164">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="f1afd-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="f1afd-165">InProgress</span></span></td><td><span data-ttu-id="f1afd-166">Validating</span><span class="sxs-lookup"><span data-stu-id="f1afd-166">Validating</span></span></td><td><span data-ttu-id="f1afd-167">驗證正在進行中。</span><span class="sxs-lookup"><span data-stu-id="f1afd-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="f1afd-168">正在處理配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-168">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="f1afd-169">Failed</span><span class="sxs-lookup"><span data-stu-id="f1afd-169">Failed</span></span></td><td><span data-ttu-id="f1afd-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="f1afd-170">TimedOut</span></span></td><td><span data-ttu-id="f1afd-171">活動執行超過活動所允許的時間。</span><span class="sxs-lookup"><span data-stu-id="f1afd-171">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="f1afd-172">Canceled</span></span></td><td><span data-ttu-id="f1afd-173">配量已由使用者動作取消。</span><span class="sxs-lookup"><span data-stu-id="f1afd-173">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-174">驗證</span><span class="sxs-lookup"><span data-stu-id="f1afd-174">Validation</span></span></td><td><span data-ttu-id="f1afd-175">驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="f1afd-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="f1afd-176">無法產生及/或驗證配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-176">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="f1afd-177">就緒</span><span class="sxs-lookup"><span data-stu-id="f1afd-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="f1afd-178">配量已就緒，可供取用。</span><span class="sxs-lookup"><span data-stu-id="f1afd-178">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-179">Skipped</span><span class="sxs-lookup"><span data-stu-id="f1afd-179">Skipped</span></span></td><td><span data-ttu-id="f1afd-180">None</span><span class="sxs-lookup"><span data-stu-id="f1afd-180">None</span></span></td><td><span data-ttu-id="f1afd-181">配量並未進行處理。</span><span class="sxs-lookup"><span data-stu-id="f1afd-181">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f1afd-182">None</span><span class="sxs-lookup"><span data-stu-id="f1afd-182">None</span></span></td><td>-</td><td><span data-ttu-id="f1afd-183">配量曾經是不同狀態，但已重設。</span><span class="sxs-lookup"><span data-stu-id="f1afd-183">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="f1afd-184">按一下 [最近更新的配量] 刀鋒視窗中的配量項目，即可檢視有關配量的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f1afd-184">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![配量的詳細資料](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="f1afd-186">若已多次執行配量，則您會在 [活動執行]  清單中看到多個資料列。</span><span class="sxs-lookup"><span data-stu-id="f1afd-186">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="f1afd-187">您可按一下 [ **活動執行** ] 清單中的執行項目，檢視有關活動執行的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f1afd-187">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="f1afd-188">此清單會顯示所有記錄檔，且如果有錯誤訊息的話，也會一併展示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-188">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="f1afd-189">這個功能非常實用，您可以檢視和偵錯記錄檔而不必離開您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="f1afd-189">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![活動執行詳細資料](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="f1afd-191">若配量不是處於 [就緒] 狀態，您可以在 [未就緒的上游配量] 清單中看到未就緒且阻礙目前配量執行的上游配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-191">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="f1afd-192">當您的配量處於 [等候] 狀態且您想要了解配量等候的上游相依項目時，此功能相當有用。</span><span class="sxs-lookup"><span data-stu-id="f1afd-192">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![尚未就緒的上游配量](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="f1afd-194">資料集狀態圖表</span><span class="sxs-lookup"><span data-stu-id="f1afd-194">Dataset state diagram</span></span>
<span data-ttu-id="f1afd-195">在部署了 Data Factory 且管線具有有效的使用中週期後，資料集配量就會從某種狀態轉換為另一種狀態。</span><span class="sxs-lookup"><span data-stu-id="f1afd-195">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="f1afd-196">目前配量狀態遵循下列的狀態圖表：</span><span class="sxs-lookup"><span data-stu-id="f1afd-196">Currently, the slice status follows the following state diagram:</span></span>

![狀態圖表](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="f1afd-198">Data Factory 內的資料集狀態轉換流程如下：等候中 -> 進行中/進行中 (驗證中) -> 就緒/失敗。</span><span class="sxs-lookup"><span data-stu-id="f1afd-198">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="f1afd-199">配量一開始的狀態是**等候**，在等到先決條件符合後才會執行。</span><span class="sxs-lookup"><span data-stu-id="f1afd-199">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="f1afd-200">接著，活動會開始執行，配量則進入 [進行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="f1afd-200">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="f1afd-201">活動執行可能成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="f1afd-201">The activity execution might succeed or fail.</span></span> <span data-ttu-id="f1afd-202">根據執行的結果，配量會標示為 [就緒] 或 [失敗]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-202">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="f1afd-203">您可以重設配量，以從 [就緒] 或 [失敗] 狀態返回 [等候] 狀態。</span><span class="sxs-lookup"><span data-stu-id="f1afd-203">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="f1afd-204">您也可以將配量狀態標記為 [略過]，這會防止活動執行且不會處理該配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-204">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="f1afd-205">暫停及繼續管線</span><span class="sxs-lookup"><span data-stu-id="f1afd-205">Pause and resume pipelines</span></span>
<span data-ttu-id="f1afd-206">您可以使用 Azure Powershell 管理您的管線。</span><span class="sxs-lookup"><span data-stu-id="f1afd-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="f1afd-207">例如，您可以執行 Azure PowerShell Cmdlet 來暫停和繼續執行管線。</span><span class="sxs-lookup"><span data-stu-id="f1afd-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="f1afd-208">圖表檢視不支援暫停和繼續管線。</span><span class="sxs-lookup"><span data-stu-id="f1afd-208">The diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="f1afd-209">如果您想要使用使用者介面，請使用監視及管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1afd-209">If you want to use an user interface, use the monitoring and managing application.</span></span> <span data-ttu-id="f1afd-210">如需使用應用程式的詳細資訊，請參閱[使用監視及管理應用程式來監視及管理 Data Factory 管線](data-factory-monitor-manage-app.md)一文。</span><span class="sxs-lookup"><span data-stu-id="f1afd-210">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="f1afd-211">您可以使用 **Suspend-AzureRmDataFactoryPipeline** PowerShell Cmdlet 來暫停/暫止管線。</span><span class="sxs-lookup"><span data-stu-id="f1afd-211">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="f1afd-212">若您在問題獲得解決之前不想執行管線，此 Cmdlet 非常有用。</span><span class="sxs-lookup"><span data-stu-id="f1afd-212">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="f1afd-213">例如：</span><span class="sxs-lookup"><span data-stu-id="f1afd-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="f1afd-214">在修正管線的問題後，您可以執行下列 PowerShell 命令來繼續暫止的管線：</span><span class="sxs-lookup"><span data-stu-id="f1afd-214">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="f1afd-215">例如：</span><span class="sxs-lookup"><span data-stu-id="f1afd-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="f1afd-216">偵錯管線</span><span class="sxs-lookup"><span data-stu-id="f1afd-216">Debug pipelines</span></span>
<span data-ttu-id="f1afd-217">Azure Data Factory 提供了許多功能供您使用 Azure 入口網站和 Azure PowerShell 來對管線進行偵錯和疑難排解。</span><span class="sxs-lookup"><span data-stu-id="f1afd-217">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="f1afd-218">[!NOTE} 使用監視及管理應用程式針對錯誤進行疑難排解更加容易。</span><span class="sxs-lookup"><span data-stu-id="f1afd-218">[!NOTE} It is much easier to troubleshot errors using the Monitoring & Management App.</span></span> <span data-ttu-id="f1afd-219">如需使用應用程式的詳細資訊，請參閱[使用監視及管理應用程式來監視及管理 Data Factory 管線](data-factory-monitor-manage-app.md)一文。</span><span class="sxs-lookup"><span data-stu-id="f1afd-219">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="f1afd-220">尋找管線中的錯誤</span><span class="sxs-lookup"><span data-stu-id="f1afd-220">Find errors in a pipeline</span></span>
<span data-ttu-id="f1afd-221">如果管線中的活動執行失敗，管線所產生的資料集會因為該失敗而處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="f1afd-221">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="f1afd-222">您可以使用下列方法，在 Azure Data Factory 中偵錯和疑難排解錯誤。</span><span class="sxs-lookup"><span data-stu-id="f1afd-222">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="f1afd-223">使用 Azure 入口網站偵錯錯誤</span><span class="sxs-lookup"><span data-stu-id="f1afd-223">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="f1afd-224">在 [資料表] 刀鋒視窗中，按一下 [狀態] 設為 [失敗] 的問題配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-224">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![含有問題配量的資料表刀鋒視窗](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="f1afd-226">在 [資料配量] 刀鋒視窗中，按一下失敗的活動執行。</span><span class="sxs-lookup"><span data-stu-id="f1afd-226">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![發生錯誤的資料配量](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="f1afd-228">在 [活動執行詳細資料] 刀鋒視窗中，您可以下載與 HDInsight 處理相關聯的檔案。</span><span class="sxs-lookup"><span data-stu-id="f1afd-228">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="f1afd-229">按一下 Status/stderr 中的 [下載] 以下載包含錯誤詳細資料的錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f1afd-229">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![含有錯誤的活動執行詳細資料刀鋒視窗](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="f1afd-231">使用 PowerShell 偵錯錯誤</span><span class="sxs-lookup"><span data-stu-id="f1afd-231">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="f1afd-232">啟動 **PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="f1afd-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="f1afd-233">執行 **Get-AzureRmDataFactorySlice** 命令來查看配量及其狀態。</span><span class="sxs-lookup"><span data-stu-id="f1afd-233">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="f1afd-234">您應該會看到狀態為 [失敗] 的配量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-234">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="f1afd-235">例如：</span><span class="sxs-lookup"><span data-stu-id="f1afd-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="f1afd-236">將 **StartDateTime** 取代為您的管線開始時間。</span><span class="sxs-lookup"><span data-stu-id="f1afd-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="f1afd-237">現在，執行 **Get-AzureRmDataFactoryRun** Cmdlet，以取得關於此配量之活動執行的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f1afd-237">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="f1afd-238">例如：</span><span class="sxs-lookup"><span data-stu-id="f1afd-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="f1afd-239">StartDateTime 的值就是您在上一步驟記下的錯誤/問題配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="f1afd-239">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="f1afd-240">date-time 應該用雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="f1afd-240">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="f1afd-241">您應該會看到含有此錯誤詳細資料的輸出，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f1afd-241">You should see output with details about the error that is similar to the following:</span></span>

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
5. <span data-ttu-id="f1afd-242">您可以使用在輸出中看見的 ID 值執行 **Save-AzureRmDataFactoryLog** Cmdlet，並在 Cmdlet 中使用 **-DownloadLogsoption** 來下載記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f1afd-242">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="f1afd-243">重新執行管線中的失敗</span><span class="sxs-lookup"><span data-stu-id="f1afd-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1afd-244">使用監視及管理應用程式針對錯誤進行疑難排解以及重新執行失敗的配量更加容易。</span><span class="sxs-lookup"><span data-stu-id="f1afd-244">It's easier to troubleshoot errors and rerun failed slices by using the Monitoring & Management App.</span></span> <span data-ttu-id="f1afd-245">如需使用應用程式的詳細資訊，請參閱[使用監視及管理應用程式來監視及管理 Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-245">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-the-azure-portal"></a><span data-ttu-id="f1afd-246">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f1afd-246">Use the Azure portal</span></span>
<span data-ttu-id="f1afd-247">在對管線中的失敗進行疑難排解和偵錯後，您可以瀏覽到錯誤配量並按一下命令列上的 [執行] 按鈕，重新執行失敗。</span><span class="sxs-lookup"><span data-stu-id="f1afd-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![重新執行失敗的配量](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="f1afd-249">萬一原則失敗而導致配量驗證失敗 (例如：沒有可用資料)，您可以修正失敗並重新驗證，方法是按一下命令列上的 [驗證] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1afd-249">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>

![修正錯誤並進行驗證](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="f1afd-251">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1afd-251">Use Azure PowerShell</span></span>
<span data-ttu-id="f1afd-252">您可以使用 **Set-AzureRmDataFactorySliceStatus** Cmdlet 來重新執行失敗。</span><span class="sxs-lookup"><span data-stu-id="f1afd-252">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="f1afd-253">如需該 Cmdlet 的語法及其他詳細資料，請參閱 [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="f1afd-253">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="f1afd-254">**範例：**</span><span class="sxs-lookup"><span data-stu-id="f1afd-254">**Example:**</span></span>

<span data-ttu-id="f1afd-255">下列範例把 Azure Data Factory 'WikiADF' 中 'DAWikiAggregatedData' 資料表的所有配量狀態都設為 'Waiting'。</span><span class="sxs-lookup"><span data-stu-id="f1afd-255">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="f1afd-256">'UpdateType' 已設為 'UpstreamInPipeline'，這代表資料表中每個配量的狀態以及所有相依 (上游) 資料表的狀態都設為 'Waiting'。</span><span class="sxs-lookup"><span data-stu-id="f1afd-256">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="f1afd-257">此參數的另一個可能值為 'Individual'。</span><span class="sxs-lookup"><span data-stu-id="f1afd-257">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="f1afd-258">建立警示</span><span class="sxs-lookup"><span data-stu-id="f1afd-258">Create alerts</span></span>
<span data-ttu-id="f1afd-259">當建立、更新或刪除 Azure 資料時 (例如 Data Factory)，Azure 會記錄使用者事件。</span><span class="sxs-lookup"><span data-stu-id="f1afd-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="f1afd-260">您可以對這些事件建立警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-260">You can create alerts on these events.</span></span> <span data-ttu-id="f1afd-261">您可以使用 Data Factory 擷取各種度量並建立度量警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-261">You can use Data Factory to capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="f1afd-262">我們建議您使用事件來進行即時監視，使用度量來做歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="f1afd-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="f1afd-263">事件警示</span><span class="sxs-lookup"><span data-stu-id="f1afd-263">Alerts on events</span></span>
<span data-ttu-id="f1afd-264">Azure 事件可讓您深入了解 Azure 資源的情況。</span><span class="sxs-lookup"><span data-stu-id="f1afd-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="f1afd-265">使用 Azure Data Factory 時，下列情況會產生事件：</span><span class="sxs-lookup"><span data-stu-id="f1afd-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="f1afd-266">建立、更新或刪除 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="f1afd-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="f1afd-267">資料處理 (「回合」形式) 已開始或完成。</span><span class="sxs-lookup"><span data-stu-id="f1afd-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="f1afd-268">建立或移除隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f1afd-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="f1afd-269">您可以針對這些使用者事件建立警示，並設定它們傳送電子郵件通知給訂用帳戶的管理員和共同管理員。</span><span class="sxs-lookup"><span data-stu-id="f1afd-269">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span></span> <span data-ttu-id="f1afd-270">此外，您還可以指定使用者的其他電子郵件地址，當條件符合時，這些使用者需要收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="f1afd-270">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span></span> <span data-ttu-id="f1afd-271">此功能在您想要取得有關失敗的通知且不想要持續監視您的 Data Factory 時會非常有用。</span><span class="sxs-lookup"><span data-stu-id="f1afd-271">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="f1afd-272">入口網站目前無法顯示事件警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-272">Currently, the portal doesn't show alerts on events.</span></span> <span data-ttu-id="f1afd-273">使用[監視及管理應用程式](data-factory-monitor-manage-app.md)來查看所有警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-273">Use the [Monitoring and Management app](data-factory-monitor-manage-app.md) to see all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="f1afd-274">指定警示定義</span><span class="sxs-lookup"><span data-stu-id="f1afd-274">Specify an alert definition</span></span>
<span data-ttu-id="f1afd-275">若要指定警示定義，您需要建立 JSON 檔案來描述您想要接獲通知的作業。</span><span class="sxs-lookup"><span data-stu-id="f1afd-275">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span></span> <span data-ttu-id="f1afd-276">在下列範例中，警示會針對 RunFinished 作業傳送電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="f1afd-276">In the following example, the alert sends an email notification for the RunFinished operation.</span></span> <span data-ttu-id="f1afd-277">具體而言，當 Data Factory 中完成一個回合，而且執行失敗時 (Status = FailedExecution)，就會傳送電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="f1afd-277">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span></span>

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
                "description": "One or more of the data slices for the Azure Data Factory has failed processing.",
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

<span data-ttu-id="f1afd-278">如果不想接獲特定失敗的通知，您可以移除 JSON 定義中的 **subStatus**。</span><span class="sxs-lookup"><span data-stu-id="f1afd-278">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span></span>

<span data-ttu-id="f1afd-279">此範例會為您的訂用帳戶中所有 Data Factory 設定警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-279">This example sets up the alert for all data factories in your subscription.</span></span> <span data-ttu-id="f1afd-280">如果您想要為特定 Data Factory 設定警示，可以在 **dataSource** 指定 Data Factory 的 **resourceUri**：</span><span class="sxs-lookup"><span data-stu-id="f1afd-280">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="f1afd-281">下列表格提供可用作業與狀態 (及子狀態) 的清單。</span><span class="sxs-lookup"><span data-stu-id="f1afd-281">The following table provides the list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="f1afd-282">作業名稱</span><span class="sxs-lookup"><span data-stu-id="f1afd-282">Operation name</span></span> | <span data-ttu-id="f1afd-283">狀態</span><span class="sxs-lookup"><span data-stu-id="f1afd-283">Status</span></span> | <span data-ttu-id="f1afd-284">子狀態</span><span class="sxs-lookup"><span data-stu-id="f1afd-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1afd-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="f1afd-285">RunStarted</span></span> |<span data-ttu-id="f1afd-286">已啟動</span><span class="sxs-lookup"><span data-stu-id="f1afd-286">Started</span></span> |<span data-ttu-id="f1afd-287">啟動中</span><span class="sxs-lookup"><span data-stu-id="f1afd-287">Starting</span></span> |
| <span data-ttu-id="f1afd-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="f1afd-288">RunFinished</span></span> |<span data-ttu-id="f1afd-289">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="f1afd-289">Failed / Succeeded</span></span> |<span data-ttu-id="f1afd-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="f1afd-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="f1afd-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="f1afd-291">Succeeded</span></span><br/><br/><span data-ttu-id="f1afd-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="f1afd-292">FailedExecution</span></span><br/><br/><span data-ttu-id="f1afd-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="f1afd-293">TimedOut</span></span><br/><br/><span data-ttu-id="f1afd-294"><已取消</span><span class="sxs-lookup"><span data-stu-id="f1afd-294"><Canceled</span></span><br/><br/><span data-ttu-id="f1afd-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="f1afd-295">FailedValidation</span></span><br/><br/><span data-ttu-id="f1afd-296">Abandoned</span><span class="sxs-lookup"><span data-stu-id="f1afd-296">Abandoned</span></span> |
| <span data-ttu-id="f1afd-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="f1afd-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="f1afd-298">已啟動</span><span class="sxs-lookup"><span data-stu-id="f1afd-298">Started</span></span> | |
| <span data-ttu-id="f1afd-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="f1afd-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="f1afd-300">Succeeded</span><span class="sxs-lookup"><span data-stu-id="f1afd-300">Succeeded</span></span> | |
| <span data-ttu-id="f1afd-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="f1afd-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="f1afd-302">Succeeded</span><span class="sxs-lookup"><span data-stu-id="f1afd-302">Succeeded</span></span> | |

<span data-ttu-id="f1afd-303">如需範例中所使用之 JSON 元素的詳細資料，請參閱[建立警示規則](https://msdn.microsoft.com/library/azure/dn510366.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span></span>

#### <a name="deploy-the-alert"></a><span data-ttu-id="f1afd-304">部署警示</span><span class="sxs-lookup"><span data-stu-id="f1afd-304">Deploy the alert</span></span>
<span data-ttu-id="f1afd-305">如果要部署警示，請使用 Azure PowerShell Cmdlet **New-AzureRmResourceGroupDeployment**，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f1afd-305">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="f1afd-306">成功完成資源群組部署之後，您會看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="f1afd-306">After the resource group deployment has finished successfully, you see the following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - The StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts to remove this parameter.
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
> <span data-ttu-id="f1afd-307">您可以使用 [建立警示規則](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API 來建立警示規則。</span><span class="sxs-lookup"><span data-stu-id="f1afd-307">You can use the [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API to create an alert rule.</span></span> <span data-ttu-id="f1afd-308">JSON 承載類似於 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="f1afd-308">The JSON payload is similar to the JSON example.</span></span>  


#### <a name="retrieve-the-list-of-azure-resource-group-deployments"></a><span data-ttu-id="f1afd-309">擷取 Azure 資源群組部署的清單</span><span class="sxs-lookup"><span data-stu-id="f1afd-309">Retrieve the list of Azure resource group deployments</span></span>
<span data-ttu-id="f1afd-310">如果要擷取已部署的 Azure 資源群組部署清單，請使用 Cmdlet **Get-AzureRmResourceGroupDeployment**，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f1afd-310">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

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

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="f1afd-311">使用者事件疑難排解</span><span class="sxs-lookup"><span data-stu-id="f1afd-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="f1afd-312">您可以看到在按一下 [度量和作業] 圖格後產生的所有事件。</span><span class="sxs-lookup"><span data-stu-id="f1afd-312">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span></span>

    ![度量和作業圖格](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="f1afd-314">按一下 [事件] 圖格來查看事件。</span><span class="sxs-lookup"><span data-stu-id="f1afd-314">Click the **Events** tile to see the events.</span></span>

    ![[事件] 磚](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="f1afd-316">在 [事件] 刀鋒視窗中，您可以查看事件、篩選事件等項目的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f1afd-316">On the **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![事件刀鋒視窗](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="f1afd-318">在作業清單中按一下導致錯誤的 [作業]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-318">Click an **Operation** in the operations list that causes an error.</span></span>

    ![選取作業](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="f1afd-320">按一下 [錯誤] 事件，以查看錯誤的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f1afd-320">Click an **Error** event to see details about the error.</span></span>

    ![事件錯誤](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="f1afd-322">如需可用於新增、取得或移除警示的 PowerShell Cmdlet，請參閱 [Azure Insight Cmdlet](https://msdn.microsoft.com/library/mt282452.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span></span> <span data-ttu-id="f1afd-323">以下是一些關於使用 **Get AlertRule** Cmdlet 的範例：</span><span class="sxs-lookup"><span data-stu-id="f1afd-323">Here are a few examples of using the **Get-AlertRule** cmdlet:</span></span>

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
Description : One or more of the data slices for the Azure Data Factory has failed processing.
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

<span data-ttu-id="f1afd-324">執行下列 get-help 命令，以查看關於 Get-AlertRule Cmdlet 的詳細資訊和範例。</span><span class="sxs-lookup"><span data-stu-id="f1afd-324">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="f1afd-325">如果您在入口網站刀鋒視窗上看到產生警示的事件但沒有收到電子郵件通知，請檢查指定的電子郵件地址是否設定為接收來自外部寄件者的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f1afd-325">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span></span> <span data-ttu-id="f1afd-326">警示的電子郵件可能遭到您的電子郵件設定封鎖。</span><span class="sxs-lookup"><span data-stu-id="f1afd-326">The alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="f1afd-327">度量的警示</span><span class="sxs-lookup"><span data-stu-id="f1afd-327">Alerts on metrics</span></span>
<span data-ttu-id="f1afd-328">您可以在 Data Factory 中擷取各種度量並建立度量警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="f1afd-329">您可以針對您 Data Factory 配量的下列度量進行監視和建立警示：</span><span class="sxs-lookup"><span data-stu-id="f1afd-329">You can monitor and create alerts on the following metrics for the slices in your data factory:</span></span>

* <span data-ttu-id="f1afd-330">**失敗的執行**</span><span class="sxs-lookup"><span data-stu-id="f1afd-330">**Failed Runs**</span></span>
* <span data-ttu-id="f1afd-331">**成功的執行**</span><span class="sxs-lookup"><span data-stu-id="f1afd-331">**Successful Runs**</span></span>

<span data-ttu-id="f1afd-332">這些度量很實用，並且可讓您在 Data Factory 取得整體失敗和成功執行的概觀。</span><span class="sxs-lookup"><span data-stu-id="f1afd-332">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span></span> <span data-ttu-id="f1afd-333">每次有配量執行時就會發出度量。</span><span class="sxs-lookup"><span data-stu-id="f1afd-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="f1afd-334">整點時，這些度量會彙總並推送至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1afd-334">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span></span> <span data-ttu-id="f1afd-335">若要啟用度量，請設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1afd-335">To enable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="f1afd-336">啟用度量</span><span class="sxs-lookup"><span data-stu-id="f1afd-336">Enable metrics</span></span>
<span data-ttu-id="f1afd-337">若要啟用度量，請從 [Data Factory] 刀鋒視窗按一下下列選項：</span><span class="sxs-lookup"><span data-stu-id="f1afd-337">To enable metrics, click the following from the **Data Factory** blade:</span></span>

<span data-ttu-id="f1afd-338">[監視] > [度量] > [診斷設定] > [診斷]</span><span class="sxs-lookup"><span data-stu-id="f1afd-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![診斷連結](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="f1afd-340">在 [診斷] 刀鋒視窗中，按一下 [啟用]，選取儲存體帳戶，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-340">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span></span>

![[診斷] 刀鋒視窗](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="f1afd-342">最長可能需要一小時才能在 [監視] 刀鋒視窗中看見度量，因為度量是每小時彙總一次。</span><span class="sxs-lookup"><span data-stu-id="f1afd-342">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="f1afd-343">設定度量警示</span><span class="sxs-lookup"><span data-stu-id="f1afd-343">Set up an alert on metrics</span></span>
<span data-ttu-id="f1afd-344">按一下 [Data Factory 度量] 圖格︰</span><span class="sxs-lookup"><span data-stu-id="f1afd-344">Click the **Data Factory metrics** tile:</span></span>

![Data Factory 度量圖格](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="f1afd-346">在 [度量] 刀鋒視窗中，按一下工具列上的 [+ 新增警示]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-346">On the **Metric** blade, click **+ Add alert** on the toolbar.</span></span>
<span data-ttu-id="f1afd-347">![Data Factory 度量刀鋒視窗 > 新增警示](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="f1afd-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="f1afd-348">在 [新增警示規則] 頁面上執行下列步驟，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-348">On the **Add an alert rule** page, do the following steps, and click **OK**.</span></span>

* <span data-ttu-id="f1afd-349">輸入警示的名稱 (範例︰「失敗警示」)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-349">Enter a name for the alert (example: "failed alert").</span></span>
* <span data-ttu-id="f1afd-350">輸入警示的描述 (範例︰「發生失敗時傳送電子郵件」)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-350">Enter a description for the alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="f1afd-351">選取度量 (「失敗的執行」與「成功的執行」)。</span><span class="sxs-lookup"><span data-stu-id="f1afd-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="f1afd-352">指定條件和臨界值。</span><span class="sxs-lookup"><span data-stu-id="f1afd-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="f1afd-353">指定期間。</span><span class="sxs-lookup"><span data-stu-id="f1afd-353">Specify the period of time.</span></span>
* <span data-ttu-id="f1afd-354">指定是否應傳送電子郵件給擁有者、參與者和讀取者。</span><span class="sxs-lookup"><span data-stu-id="f1afd-354">Specify whether an email should be sent to owners, contributors, and readers.</span></span>

![Data Factory 度量刀鋒視窗 > 新增警示規則](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="f1afd-356">成功新增警示規則後，刀鋒視窗會隨即關閉，而您會在 [度量] 刀鋒視窗上看到新的警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-356">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span></span>

![Data Factory 度量刀鋒視窗 > 已新增警示](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="f1afd-358">您也應該會在 [警示規則] 圖格上看到警示數目。</span><span class="sxs-lookup"><span data-stu-id="f1afd-358">You should also see the number of alerts in the **Alert rules** tile.</span></span> <span data-ttu-id="f1afd-359">按一下 [警示規則] 圖格。</span><span class="sxs-lookup"><span data-stu-id="f1afd-359">Click the **Alert rules** tile.</span></span>

![Data Factory 度量刀鋒視窗 - 新增規則](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="f1afd-361">在 [警示規則] 刀鋒視窗中，您會看到任何現有的警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-361">On the **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="f1afd-362">若要新增警示，請按一下工具列上的 [新增警示]。</span><span class="sxs-lookup"><span data-stu-id="f1afd-362">To add an alert, click **Add alert** on the toolbar.</span></span>

![警示規則刀鋒視窗](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="f1afd-364">警示通知</span><span class="sxs-lookup"><span data-stu-id="f1afd-364">Alert notifications</span></span>
<span data-ttu-id="f1afd-365">警示規則與條件相符後，您應該會收到指出警示已啟用的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f1afd-365">After the alert rule matches the condition, you should get an email that says the alert is activated.</span></span> <span data-ttu-id="f1afd-366">在問題獲得解決且警示條件不再符合任何規則後，您就會收到指出警示已獲得解決的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f1afd-366">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span></span>

<span data-ttu-id="f1afd-367">此行為不同於事件，其會針對警示規則相符的每個失敗傳送通知。</span><span class="sxs-lookup"><span data-stu-id="f1afd-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="f1afd-368">使用 PowerShell 部署警示</span><span class="sxs-lookup"><span data-stu-id="f1afd-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="f1afd-369">您可以使用部署事件警示的相同方法來部署度量警示。</span><span class="sxs-lookup"><span data-stu-id="f1afd-369">You can deploy alerts for metrics the same way that you do for events.</span></span>

<span data-ttu-id="f1afd-370">**警示定義**</span><span class="sxs-lookup"><span data-stu-id="f1afd-370">**Alert definition**</span></span>

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

<span data-ttu-id="f1afd-371">以適當的值取代範例中的 subscriptionId、resourceGroupName、和 dataFactoryName。</span><span class="sxs-lookup"><span data-stu-id="f1afd-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span></span>

<span data-ttu-id="f1afd-372">metricName 目前支援兩個值︰</span><span class="sxs-lookup"><span data-stu-id="f1afd-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="f1afd-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="f1afd-373">FailedRuns</span></span>
* <span data-ttu-id="f1afd-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="f1afd-374">SuccessfulRuns</span></span>

<span data-ttu-id="f1afd-375">**部署警示**</span><span class="sxs-lookup"><span data-stu-id="f1afd-375">**Deploy the alert**</span></span>

<span data-ttu-id="f1afd-376">如果要部署警示，請使用 Azure PowerShell Cmdlet **New-AzureRmResourceGroupDeployment**，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f1afd-376">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="f1afd-377">您應該會在部署成功後看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="f1afd-377">You should see following message after a successful deployment:</span></span>

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

<span data-ttu-id="f1afd-378">您也可以使用 **Add-AlertRule** Cmdlet 來部署警示規則。</span><span class="sxs-lookup"><span data-stu-id="f1afd-378">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span></span> <span data-ttu-id="f1afd-379">如需詳細資料及範例，請參閱 [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="f1afd-379">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="f1afd-380">將 Data Factory 移至另一個資源群組或訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f1afd-380">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="f1afd-381">您可以使用 Data Factory 首頁上的 [移動]  命令列按鈕，將 Data Factory 移至另一個資源群組或訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1afd-381">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![移動 Data Factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="f1afd-383">您也可以將任何相關資源 (例如與 Data Factory 相關聯的警示) 連同 Data Factory 一起移動。</span><span class="sxs-lookup"><span data-stu-id="f1afd-383">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![移動資源對話方塊](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
