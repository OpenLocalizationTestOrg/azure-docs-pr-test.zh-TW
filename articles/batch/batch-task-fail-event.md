---
title: "Azure Batch 工作失敗事件 | Microsoft Docs"
description: "Batch 工作失敗事件的參考。"
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
ms.openlocfilehash: 08feb4ec34bb1635f8ea744b54a10b677b94ab3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="task-fail-event"></a><span data-ttu-id="12e2a-103">工作失敗事件</span><span class="sxs-lookup"><span data-stu-id="12e2a-103">Task fail event</span></span>

 <span data-ttu-id="12e2a-104">當工作未成功完成時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="12e2a-104">This event is emitted when a task completes with a failure.</span></span> <span data-ttu-id="12e2a-105">目前所有非零的結束代碼皆視為失敗。</span><span class="sxs-lookup"><span data-stu-id="12e2a-105">Currently all nonzero exit codes are considered failures.</span></span> <span data-ttu-id="12e2a-106">除了工作完成事件外，還會發出此事件，此事件可用於偵測工作何時失敗。</span><span class="sxs-lookup"><span data-stu-id="12e2a-106">This event will be emitted *in addition to* a task complete event and can be used to detect when a task has failed.</span></span>


 <span data-ttu-id="12e2a-107">下列範例顯示工作失敗事件內文。</span><span class="sxs-lookup"><span data-stu-id="12e2a-107">The following example shows the body of a task fail event.</span></span>

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
        "exitCode": 1,
        "retryCount": 2,
        "requeueCount": 0
    }
}
```

|<span data-ttu-id="12e2a-108">元素名稱</span><span class="sxs-lookup"><span data-stu-id="12e2a-108">Element name</span></span>|<span data-ttu-id="12e2a-109">類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-109">Type</span></span>|<span data-ttu-id="12e2a-110">注意事項</span><span class="sxs-lookup"><span data-stu-id="12e2a-110">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="12e2a-111">jobId</span><span class="sxs-lookup"><span data-stu-id="12e2a-111">jobId</span></span>|<span data-ttu-id="12e2a-112">String</span><span class="sxs-lookup"><span data-stu-id="12e2a-112">String</span></span>|<span data-ttu-id="12e2a-113">包含工作的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="12e2a-113">The id of the job containing the task.</span></span>|
|<span data-ttu-id="12e2a-114">id</span><span class="sxs-lookup"><span data-stu-id="12e2a-114">id</span></span>|<span data-ttu-id="12e2a-115">String</span><span class="sxs-lookup"><span data-stu-id="12e2a-115">String</span></span>|<span data-ttu-id="12e2a-116">工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="12e2a-116">The id of the task.</span></span>|
|<span data-ttu-id="12e2a-117">taskType</span><span class="sxs-lookup"><span data-stu-id="12e2a-117">taskType</span></span>|<span data-ttu-id="12e2a-118">String</span><span class="sxs-lookup"><span data-stu-id="12e2a-118">String</span></span>|<span data-ttu-id="12e2a-119">工作類型。</span><span class="sxs-lookup"><span data-stu-id="12e2a-119">The type of the task.</span></span> <span data-ttu-id="12e2a-120">可以是 'JobManager'，表示這是作業管理員工作，或是 'User'，表示不是作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="12e2a-120">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="12e2a-121">對於作業準備工作、作業發行工作或開始工作。不會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="12e2a-121">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="12e2a-122">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="12e2a-122">systemTaskVersion</span></span>|<span data-ttu-id="12e2a-123">Int32</span><span class="sxs-lookup"><span data-stu-id="12e2a-123">Int32</span></span>|<span data-ttu-id="12e2a-124">這是作業上的內部重試計數器。</span><span class="sxs-lookup"><span data-stu-id="12e2a-124">This is the internal retry counter on a task.</span></span> <span data-ttu-id="12e2a-125">Batch 服務可在內部重試工作，以處理暫時性問題。</span><span class="sxs-lookup"><span data-stu-id="12e2a-125">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="12e2a-126">這些問題包含內部排程錯誤，或嘗試從不正常狀態的計算節點復原。</span><span class="sxs-lookup"><span data-stu-id="12e2a-126">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="12e2a-127">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="12e2a-127">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="12e2a-128">複雜類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-128">Complex Type</span></span>|<span data-ttu-id="12e2a-129">包含工作執行所在計算節點的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="12e2a-129">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="12e2a-130">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="12e2a-130">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="12e2a-131">複雜類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-131">Complex Type</span></span>|<span data-ttu-id="12e2a-132">指定工作為需要多個計算節點的多重執行個體工作。</span><span class="sxs-lookup"><span data-stu-id="12e2a-132">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="12e2a-133">請參閱 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) (英文) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="12e2a-133">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="12e2a-134">constraints</span><span class="sxs-lookup"><span data-stu-id="12e2a-134">constraints</span></span>](#constraints)|<span data-ttu-id="12e2a-135">複雜類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-135">Complex Type</span></span>|<span data-ttu-id="12e2a-136">套用至此工作的執行限制。</span><span class="sxs-lookup"><span data-stu-id="12e2a-136">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="12e2a-137">executionInfo</span><span class="sxs-lookup"><span data-stu-id="12e2a-137">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="12e2a-138">複雜類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-138">Complex Type</span></span>|<span data-ttu-id="12e2a-139">包含執行工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="12e2a-139">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="12e2a-140"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="12e2a-140"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="12e2a-141">元素名稱</span><span class="sxs-lookup"><span data-stu-id="12e2a-141">Element name</span></span>|<span data-ttu-id="12e2a-142">類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-142">Type</span></span>|<span data-ttu-id="12e2a-143">注意事項</span><span class="sxs-lookup"><span data-stu-id="12e2a-143">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="12e2a-144">poolId</span><span class="sxs-lookup"><span data-stu-id="12e2a-144">poolId</span></span>|<span data-ttu-id="12e2a-145">String</span><span class="sxs-lookup"><span data-stu-id="12e2a-145">String</span></span>|<span data-ttu-id="12e2a-146">工作執行所在集區的識別碼。</span><span class="sxs-lookup"><span data-stu-id="12e2a-146">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="12e2a-147">nodeId</span><span class="sxs-lookup"><span data-stu-id="12e2a-147">nodeId</span></span>|<span data-ttu-id="12e2a-148">String</span><span class="sxs-lookup"><span data-stu-id="12e2a-148">String</span></span>|<span data-ttu-id="12e2a-149">工作執行所在節點的識別碼。</span><span class="sxs-lookup"><span data-stu-id="12e2a-149">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="12e2a-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="12e2a-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="12e2a-151">元素名稱</span><span class="sxs-lookup"><span data-stu-id="12e2a-151">Element name</span></span>|<span data-ttu-id="12e2a-152">類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-152">Type</span></span>|<span data-ttu-id="12e2a-153">注意事項</span><span class="sxs-lookup"><span data-stu-id="12e2a-153">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="12e2a-154">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="12e2a-154">numberOfInstances</span></span>|<span data-ttu-id="12e2a-155">Int32</span><span class="sxs-lookup"><span data-stu-id="12e2a-155">Int32</span></span>|<span data-ttu-id="12e2a-156">工作需要的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="12e2a-156">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="12e2a-157"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="12e2a-157"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="12e2a-158">元素名稱</span><span class="sxs-lookup"><span data-stu-id="12e2a-158">Element name</span></span>|<span data-ttu-id="12e2a-159">類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-159">Type</span></span>|<span data-ttu-id="12e2a-160">注意事項</span><span class="sxs-lookup"><span data-stu-id="12e2a-160">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="12e2a-161">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="12e2a-161">maxTaskRetryCount</span></span>|<span data-ttu-id="12e2a-162">Int32</span><span class="sxs-lookup"><span data-stu-id="12e2a-162">Int32</span></span>|<span data-ttu-id="12e2a-163">工作重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="12e2a-163">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="12e2a-164">如果工作的結束代碼不是零，Batch 服務會重試工作。</span><span class="sxs-lookup"><span data-stu-id="12e2a-164">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="12e2a-165">請注意，這個值會特別控制重試次數。</span><span class="sxs-lookup"><span data-stu-id="12e2a-165">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="12e2a-166">Batch 服務會嘗試工作一次，然後可一直重試直到達此限制。</span><span class="sxs-lookup"><span data-stu-id="12e2a-166">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="12e2a-167">例如，如果重試計數上限為 3，則 Batch 可嘗試工作最多 4 次 (一次首次嘗試，3 次重試)。</span><span class="sxs-lookup"><span data-stu-id="12e2a-167">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="12e2a-168">如果重試計數上限為 0，則 Batch 服務不會重試工作。</span><span class="sxs-lookup"><span data-stu-id="12e2a-168">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="12e2a-169">如果重試計數上限為 -1，則 Batch 服務會無限制地重試工作。</span><span class="sxs-lookup"><span data-stu-id="12e2a-169">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="12e2a-170">預設值為 0 (不重試)。</span><span class="sxs-lookup"><span data-stu-id="12e2a-170">The default value is 0 (no retries).</span></span>|


###  <span data-ttu-id="12e2a-171"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="12e2a-171"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="12e2a-172">元素名稱</span><span class="sxs-lookup"><span data-stu-id="12e2a-172">Element name</span></span>|<span data-ttu-id="12e2a-173">類型</span><span class="sxs-lookup"><span data-stu-id="12e2a-173">Type</span></span>|<span data-ttu-id="12e2a-174">注意事項</span><span class="sxs-lookup"><span data-stu-id="12e2a-174">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="12e2a-175">startTime</span><span class="sxs-lookup"><span data-stu-id="12e2a-175">startTime</span></span>|<span data-ttu-id="12e2a-176">DateTime</span><span class="sxs-lookup"><span data-stu-id="12e2a-176">DateTime</span></span>|<span data-ttu-id="12e2a-177">工作開始執行的時間。</span><span class="sxs-lookup"><span data-stu-id="12e2a-177">The time at which the task started running.</span></span> <span data-ttu-id="12e2a-178">「執行」與 **running** 狀態對應，因此如果工作會指定資源檔或應用程式套件，則開始時間會反映工作開始下載或部署下載項目的時間。</span><span class="sxs-lookup"><span data-stu-id="12e2a-178">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="12e2a-179">如果已重新啟動或重試工作，則這是最近一次工作開始執行的時間。</span><span class="sxs-lookup"><span data-stu-id="12e2a-179">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="12e2a-180">EndTime</span><span class="sxs-lookup"><span data-stu-id="12e2a-180">endTime</span></span>|<span data-ttu-id="12e2a-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="12e2a-181">DateTime</span></span>|<span data-ttu-id="12e2a-182">工作完成的時間。</span><span class="sxs-lookup"><span data-stu-id="12e2a-182">The time at which the task completed.</span></span>|
|<span data-ttu-id="12e2a-183">exitCode</span><span class="sxs-lookup"><span data-stu-id="12e2a-183">exitCode</span></span>|<span data-ttu-id="12e2a-184">Int32</span><span class="sxs-lookup"><span data-stu-id="12e2a-184">Int32</span></span>|<span data-ttu-id="12e2a-185">工作的結束代碼。</span><span class="sxs-lookup"><span data-stu-id="12e2a-185">The exit code of the task.</span></span>|
|<span data-ttu-id="12e2a-186">retryCount</span><span class="sxs-lookup"><span data-stu-id="12e2a-186">retryCount</span></span>|<span data-ttu-id="12e2a-187">Int32</span><span class="sxs-lookup"><span data-stu-id="12e2a-187">Int32</span></span>|<span data-ttu-id="12e2a-188">Batch 服務已重試工作的次數。</span><span class="sxs-lookup"><span data-stu-id="12e2a-188">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="12e2a-189">如果工作結束時的結束代碼不是零，便會重試工作，直到次數達指定的 MaxTaskRetryCount。</span><span class="sxs-lookup"><span data-stu-id="12e2a-189">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="12e2a-190">requeueCount</span><span class="sxs-lookup"><span data-stu-id="12e2a-190">requeueCount</span></span>|<span data-ttu-id="12e2a-191">Int32</span><span class="sxs-lookup"><span data-stu-id="12e2a-191">Int32</span></span>|<span data-ttu-id="12e2a-192">Batch 服務因為使用者要求而將工作重新排入佇列的次數。</span><span class="sxs-lookup"><span data-stu-id="12e2a-192">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="12e2a-193">當使用者將節點從集區中移除 (透過調整集區大小或將集區縮小)，或當作業正停用時，使用者可指定將節點上的執行中工作重新排入佇列以執行。</span><span class="sxs-lookup"><span data-stu-id="12e2a-193">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="12e2a-194">此計數會追蹤因為這些理由而將工作重新排入佇列的次數。</span><span class="sxs-lookup"><span data-stu-id="12e2a-194">This count tracks how many times the task has been requeued for these reasons.</span></span>|
