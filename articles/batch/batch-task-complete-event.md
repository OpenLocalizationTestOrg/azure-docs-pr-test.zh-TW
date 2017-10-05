---
title: "Azure Batch 工作完成事件 | Microsoft Docs"
description: "Batch 工作完成事件的參考。"
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 015adf7dbc47c29a78df4e4889b2ee1ddcccdd8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="task-complete-event"></a><span data-ttu-id="d89db-103">工作完成事件</span><span class="sxs-lookup"><span data-stu-id="d89db-103">Task complete event</span></span>

 <span data-ttu-id="d89db-104">工作完成時就會發出此事件，無論結束代碼為何。</span><span class="sxs-lookup"><span data-stu-id="d89db-104">This event is emitted once a task is completed, regardless of the exit code.</span></span> <span data-ttu-id="d89db-105">此事件可用來判斷工作的持續時間、工作執行的位置，以及是否已重試工作。</span><span class="sxs-lookup"><span data-stu-id="d89db-105">This event can be used to determine the duration of a task, where the task ran, and whether it was retried.</span></span>


 <span data-ttu-id="d89db-106">下列範例顯示工作完成事件內文。</span><span class="sxs-lookup"><span data-stu-id="d89db-106">The following example shows the body of a task complete event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|<span data-ttu-id="d89db-107">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d89db-107">Element name</span></span>|<span data-ttu-id="d89db-108">類型</span><span class="sxs-lookup"><span data-stu-id="d89db-108">Type</span></span>|<span data-ttu-id="d89db-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="d89db-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d89db-110">jobId</span><span class="sxs-lookup"><span data-stu-id="d89db-110">jobId</span></span>|<span data-ttu-id="d89db-111">String</span><span class="sxs-lookup"><span data-stu-id="d89db-111">String</span></span>|<span data-ttu-id="d89db-112">包含工作的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="d89db-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="d89db-113">id</span><span class="sxs-lookup"><span data-stu-id="d89db-113">id</span></span>|<span data-ttu-id="d89db-114">String</span><span class="sxs-lookup"><span data-stu-id="d89db-114">String</span></span>|<span data-ttu-id="d89db-115">工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="d89db-115">The id of the task.</span></span>|
|<span data-ttu-id="d89db-116">taskType</span><span class="sxs-lookup"><span data-stu-id="d89db-116">taskType</span></span>|<span data-ttu-id="d89db-117">String</span><span class="sxs-lookup"><span data-stu-id="d89db-117">String</span></span>|<span data-ttu-id="d89db-118">工作類型。</span><span class="sxs-lookup"><span data-stu-id="d89db-118">The type of the task.</span></span> <span data-ttu-id="d89db-119">可以是 'JobManager'，表示這是作業管理員工作，或是 'User'，表示不是作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="d89db-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="d89db-120">對於作業準備工作、作業發行工作或開始工作。不會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="d89db-120">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="d89db-121">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="d89db-121">systemTaskVersion</span></span>|<span data-ttu-id="d89db-122">Int32</span><span class="sxs-lookup"><span data-stu-id="d89db-122">Int32</span></span>|<span data-ttu-id="d89db-123">這是作業上的內部重試計數器。</span><span class="sxs-lookup"><span data-stu-id="d89db-123">This is the internal retry counter on a task.</span></span> <span data-ttu-id="d89db-124">Batch 服務可在內部重試工作，以處理暫時性問題。</span><span class="sxs-lookup"><span data-stu-id="d89db-124">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="d89db-125">這些問題包含內部排程錯誤，或嘗試從不正常狀態的計算節點復原。</span><span class="sxs-lookup"><span data-stu-id="d89db-125">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="d89db-126">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="d89db-126">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="d89db-127">複雜類型</span><span class="sxs-lookup"><span data-stu-id="d89db-127">Complex Type</span></span>|<span data-ttu-id="d89db-128">包含工作執行所在計算節點的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d89db-128">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="d89db-129">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="d89db-129">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="d89db-130">複雜類型</span><span class="sxs-lookup"><span data-stu-id="d89db-130">Complex Type</span></span>|<span data-ttu-id="d89db-131">指定工作為需要多個計算節點的多重執行個體工作。</span><span class="sxs-lookup"><span data-stu-id="d89db-131">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="d89db-132">請參閱 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) (英文) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d89db-132">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="d89db-133">constraints</span><span class="sxs-lookup"><span data-stu-id="d89db-133">constraints</span></span>](#constraints)|<span data-ttu-id="d89db-134">複雜類型</span><span class="sxs-lookup"><span data-stu-id="d89db-134">Complex Type</span></span>|<span data-ttu-id="d89db-135">套用至此工作的執行限制。</span><span class="sxs-lookup"><span data-stu-id="d89db-135">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="d89db-136">executionInfo</span><span class="sxs-lookup"><span data-stu-id="d89db-136">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="d89db-137">複雜類型</span><span class="sxs-lookup"><span data-stu-id="d89db-137">Complex Type</span></span>|<span data-ttu-id="d89db-138">包含執行工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d89db-138">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="d89db-139"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="d89db-139"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="d89db-140">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d89db-140">Element name</span></span>|<span data-ttu-id="d89db-141">類型</span><span class="sxs-lookup"><span data-stu-id="d89db-141">Type</span></span>|<span data-ttu-id="d89db-142">注意事項</span><span class="sxs-lookup"><span data-stu-id="d89db-142">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d89db-143">poolId</span><span class="sxs-lookup"><span data-stu-id="d89db-143">poolId</span></span>|<span data-ttu-id="d89db-144">String</span><span class="sxs-lookup"><span data-stu-id="d89db-144">String</span></span>|<span data-ttu-id="d89db-145">工作執行所在集區的識別碼。</span><span class="sxs-lookup"><span data-stu-id="d89db-145">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="d89db-146">nodeId</span><span class="sxs-lookup"><span data-stu-id="d89db-146">nodeId</span></span>|<span data-ttu-id="d89db-147">String</span><span class="sxs-lookup"><span data-stu-id="d89db-147">String</span></span>|<span data-ttu-id="d89db-148">工作執行所在節點的識別碼。</span><span class="sxs-lookup"><span data-stu-id="d89db-148">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="d89db-149"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="d89db-149"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="d89db-150">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d89db-150">Element name</span></span>|<span data-ttu-id="d89db-151">類型</span><span class="sxs-lookup"><span data-stu-id="d89db-151">Type</span></span>|<span data-ttu-id="d89db-152">注意事項</span><span class="sxs-lookup"><span data-stu-id="d89db-152">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d89db-153">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="d89db-153">numberOfInstances</span></span>|<span data-ttu-id="d89db-154">Int32</span><span class="sxs-lookup"><span data-stu-id="d89db-154">Int32</span></span>|<span data-ttu-id="d89db-155">工作需要的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="d89db-155">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="d89db-156"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="d89db-156"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="d89db-157">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d89db-157">Element name</span></span>|<span data-ttu-id="d89db-158">類型</span><span class="sxs-lookup"><span data-stu-id="d89db-158">Type</span></span>|<span data-ttu-id="d89db-159">注意事項</span><span class="sxs-lookup"><span data-stu-id="d89db-159">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d89db-160">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="d89db-160">maxTaskRetryCount</span></span>|<span data-ttu-id="d89db-161">Int32</span><span class="sxs-lookup"><span data-stu-id="d89db-161">Int32</span></span>|<span data-ttu-id="d89db-162">工作重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="d89db-162">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="d89db-163">如果工作的結束代碼不是零，Batch 服務會重試工作。</span><span class="sxs-lookup"><span data-stu-id="d89db-163">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="d89db-164">請注意，這個值會特別控制重試次數。</span><span class="sxs-lookup"><span data-stu-id="d89db-164">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="d89db-165">Batch 服務會嘗試工作一次，然後可一直重試直到達此限制。</span><span class="sxs-lookup"><span data-stu-id="d89db-165">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="d89db-166">例如，如果重試計數上限為 3，則 Batch 可嘗試工作最多 4 次 (一次首次嘗試，3 次重試)。</span><span class="sxs-lookup"><span data-stu-id="d89db-166">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="d89db-167">如果重試計數上限為 0，則 Batch 服務不會重試工作。</span><span class="sxs-lookup"><span data-stu-id="d89db-167">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="d89db-168">如果重試計數上限為 -1，則 Batch 服務會無限制地重試工作。</span><span class="sxs-lookup"><span data-stu-id="d89db-168">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="d89db-169">預設值為 0 (不重試)。</span><span class="sxs-lookup"><span data-stu-id="d89db-169">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="d89db-170"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="d89db-170"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="d89db-171">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d89db-171">Element name</span></span>|<span data-ttu-id="d89db-172">類型</span><span class="sxs-lookup"><span data-stu-id="d89db-172">Type</span></span>|<span data-ttu-id="d89db-173">注意事項</span><span class="sxs-lookup"><span data-stu-id="d89db-173">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d89db-174">startTime</span><span class="sxs-lookup"><span data-stu-id="d89db-174">startTime</span></span>|<span data-ttu-id="d89db-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="d89db-175">DateTime</span></span>|<span data-ttu-id="d89db-176">工作開始執行的時間。</span><span class="sxs-lookup"><span data-stu-id="d89db-176">The time at which the task started running.</span></span> <span data-ttu-id="d89db-177">「執行」與 **running** 狀態對應，因此如果工作會指定資源檔或應用程式套件，則開始時間會反映工作開始下載或部署下載項目的時間。</span><span class="sxs-lookup"><span data-stu-id="d89db-177">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="d89db-178">如果已重新啟動或重試工作，則這是最近一次工作開始執行的時間。</span><span class="sxs-lookup"><span data-stu-id="d89db-178">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="d89db-179">EndTime</span><span class="sxs-lookup"><span data-stu-id="d89db-179">endTime</span></span>|<span data-ttu-id="d89db-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="d89db-180">DateTime</span></span>|<span data-ttu-id="d89db-181">工作完成的時間。</span><span class="sxs-lookup"><span data-stu-id="d89db-181">The time at which the task completed.</span></span>|
|<span data-ttu-id="d89db-182">exitCode</span><span class="sxs-lookup"><span data-stu-id="d89db-182">exitCode</span></span>|<span data-ttu-id="d89db-183">Int32</span><span class="sxs-lookup"><span data-stu-id="d89db-183">Int32</span></span>|<span data-ttu-id="d89db-184">工作的結束代碼。</span><span class="sxs-lookup"><span data-stu-id="d89db-184">The exit code of the task.</span></span>|
|<span data-ttu-id="d89db-185">retryCount</span><span class="sxs-lookup"><span data-stu-id="d89db-185">retryCount</span></span>|<span data-ttu-id="d89db-186">Int32</span><span class="sxs-lookup"><span data-stu-id="d89db-186">Int32</span></span>|<span data-ttu-id="d89db-187">Batch 服務已重試工作的次數。</span><span class="sxs-lookup"><span data-stu-id="d89db-187">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="d89db-188">如果工作結束時的結束代碼不是零，便會重試工作，直到次數達指定的 MaxTaskRetryCount。</span><span class="sxs-lookup"><span data-stu-id="d89db-188">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="d89db-189">requeueCount</span><span class="sxs-lookup"><span data-stu-id="d89db-189">requeueCount</span></span>|<span data-ttu-id="d89db-190">Int32</span><span class="sxs-lookup"><span data-stu-id="d89db-190">Int32</span></span>|<span data-ttu-id="d89db-191">Batch 服務因為使用者要求而將工作重新排入佇列的次數。</span><span class="sxs-lookup"><span data-stu-id="d89db-191">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="d89db-192">當使用者將節點從集區中移除 (透過調整集區大小或將集區縮小)，或當作業正停用時，使用者可指定將節點上的執行中工作重新排入佇列以執行。</span><span class="sxs-lookup"><span data-stu-id="d89db-192">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="d89db-193">此計數會追蹤因為這些理由而將工作重新排入佇列的次數。</span><span class="sxs-lookup"><span data-stu-id="d89db-193">This count tracks how many times the task has been requeued for these reasons.</span></span>|
