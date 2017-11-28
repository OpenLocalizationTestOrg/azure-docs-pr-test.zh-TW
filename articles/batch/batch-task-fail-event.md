---
title: "aaa\"Azure 批次工作失敗事件 |Microsoft 文件 」"
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
ms.openlocfilehash: e92604671650900072ba27f807501b704329e865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="task-fail-event"></a><span data-ttu-id="fe221-103">工作失敗事件</span><span class="sxs-lookup"><span data-stu-id="fe221-103">Task fail event</span></span>

 <span data-ttu-id="fe221-104">當工作未成功完成時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="fe221-104">This event is emitted when a task completes with a failure.</span></span> <span data-ttu-id="fe221-105">目前所有非零的結束代碼皆視為失敗。</span><span class="sxs-lookup"><span data-stu-id="fe221-105">Currently all nonzero exit codes are considered failures.</span></span> <span data-ttu-id="fe221-106">會發出這個事件*除了*工作完成事件，而且可以是使用的 toodetect，工作失敗時。</span><span class="sxs-lookup"><span data-stu-id="fe221-106">This event will be emitted *in addition to* a task complete event and can be used toodetect when a task has failed.</span></span>


 <span data-ttu-id="fe221-107">hello 下列範例顯示 hello 工作主體失敗事件。</span><span class="sxs-lookup"><span data-stu-id="fe221-107">hello following example shows hello body of a task fail event.</span></span>

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

|<span data-ttu-id="fe221-108">元素名稱</span><span class="sxs-lookup"><span data-stu-id="fe221-108">Element name</span></span>|<span data-ttu-id="fe221-109">類型</span><span class="sxs-lookup"><span data-stu-id="fe221-109">Type</span></span>|<span data-ttu-id="fe221-110">注意事項</span><span class="sxs-lookup"><span data-stu-id="fe221-110">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="fe221-111">jobId</span><span class="sxs-lookup"><span data-stu-id="fe221-111">jobId</span></span>|<span data-ttu-id="fe221-112">String</span><span class="sxs-lookup"><span data-stu-id="fe221-112">String</span></span>|<span data-ttu-id="fe221-113">hello hello 作業包含 hello 工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="fe221-113">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="fe221-114">id</span><span class="sxs-lookup"><span data-stu-id="fe221-114">id</span></span>|<span data-ttu-id="fe221-115">String</span><span class="sxs-lookup"><span data-stu-id="fe221-115">String</span></span>|<span data-ttu-id="fe221-116">hello hello 工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="fe221-116">hello id of hello task.</span></span>|
|<span data-ttu-id="fe221-117">taskType</span><span class="sxs-lookup"><span data-stu-id="fe221-117">taskType</span></span>|<span data-ttu-id="fe221-118">String</span><span class="sxs-lookup"><span data-stu-id="fe221-118">String</span></span>|<span data-ttu-id="fe221-119">hello hello 工作類型。</span><span class="sxs-lookup"><span data-stu-id="fe221-119">hello type of hello task.</span></span> <span data-ttu-id="fe221-120">可以是 'JobManager'，表示這是作業管理員工作，或是 'User'，表示不是作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="fe221-120">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="fe221-121">對於作業準備工作、作業發行工作或開始工作。不會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="fe221-121">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="fe221-122">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="fe221-122">systemTaskVersion</span></span>|<span data-ttu-id="fe221-123">Int32</span><span class="sxs-lookup"><span data-stu-id="fe221-123">Int32</span></span>|<span data-ttu-id="fe221-124">這是在工作上的 hello 內部重試計數器。</span><span class="sxs-lookup"><span data-stu-id="fe221-124">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="fe221-125">在內部 hello 批次服務可以重試工作 tooaccount 暫時性的問題。</span><span class="sxs-lookup"><span data-stu-id="fe221-125">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="fe221-126">這些問題可以包含內部排程錯誤或嘗試 toorecover 從運算節點處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="fe221-126">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="fe221-127">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="fe221-127">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="fe221-128">複雜類型</span><span class="sxs-lookup"><span data-stu-id="fe221-128">Complex Type</span></span>|<span data-ttu-id="fe221-129">包含 hello 計算節點的 hello 工作已執行的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fe221-129">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="fe221-130">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="fe221-130">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="fe221-131">複雜類型</span><span class="sxs-lookup"><span data-stu-id="fe221-131">Complex Type</span></span>|<span data-ttu-id="fe221-132">指定該 hello 工作是多個執行個體工作需要多個計算節點。</span><span class="sxs-lookup"><span data-stu-id="fe221-132">Specifies that hello task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="fe221-133">請參閱 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) (英文) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fe221-133">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="fe221-134">constraints</span><span class="sxs-lookup"><span data-stu-id="fe221-134">constraints</span></span>](#constraints)|<span data-ttu-id="fe221-135">複雜類型</span><span class="sxs-lookup"><span data-stu-id="fe221-135">Complex Type</span></span>|<span data-ttu-id="fe221-136">套用 toothis 工作 hello 執行條件約束。</span><span class="sxs-lookup"><span data-stu-id="fe221-136">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="fe221-137">executionInfo</span><span class="sxs-lookup"><span data-stu-id="fe221-137">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="fe221-138">複雜類型</span><span class="sxs-lookup"><span data-stu-id="fe221-138">Complex Type</span></span>|<span data-ttu-id="fe221-139">包含有關 hello hello 工作執行資訊。</span><span class="sxs-lookup"><span data-stu-id="fe221-139">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="fe221-140"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="fe221-140"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="fe221-141">元素名稱</span><span class="sxs-lookup"><span data-stu-id="fe221-141">Element name</span></span>|<span data-ttu-id="fe221-142">類型</span><span class="sxs-lookup"><span data-stu-id="fe221-142">Type</span></span>|<span data-ttu-id="fe221-143">注意事項</span><span class="sxs-lookup"><span data-stu-id="fe221-143">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="fe221-144">poolId</span><span class="sxs-lookup"><span data-stu-id="fe221-144">poolId</span></span>|<span data-ttu-id="fe221-145">String</span><span class="sxs-lookup"><span data-stu-id="fe221-145">String</span></span>|<span data-ttu-id="fe221-146">hello hello 集區的 hello 工作已執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="fe221-146">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="fe221-147">nodeId</span><span class="sxs-lookup"><span data-stu-id="fe221-147">nodeId</span></span>|<span data-ttu-id="fe221-148">String</span><span class="sxs-lookup"><span data-stu-id="fe221-148">String</span></span>|<span data-ttu-id="fe221-149">hello hello 節點的 hello 工作已執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="fe221-149">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="fe221-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="fe221-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="fe221-151">元素名稱</span><span class="sxs-lookup"><span data-stu-id="fe221-151">Element name</span></span>|<span data-ttu-id="fe221-152">類型</span><span class="sxs-lookup"><span data-stu-id="fe221-152">Type</span></span>|<span data-ttu-id="fe221-153">注意事項</span><span class="sxs-lookup"><span data-stu-id="fe221-153">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="fe221-154">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="fe221-154">numberOfInstances</span></span>|<span data-ttu-id="fe221-155">Int32</span><span class="sxs-lookup"><span data-stu-id="fe221-155">Int32</span></span>|<span data-ttu-id="fe221-156">hello hello 工作所需的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="fe221-156">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="fe221-157"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="fe221-157"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="fe221-158">元素名稱</span><span class="sxs-lookup"><span data-stu-id="fe221-158">Element name</span></span>|<span data-ttu-id="fe221-159">類型</span><span class="sxs-lookup"><span data-stu-id="fe221-159">Type</span></span>|<span data-ttu-id="fe221-160">注意事項</span><span class="sxs-lookup"><span data-stu-id="fe221-160">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="fe221-161">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="fe221-161">maxTaskRetryCount</span></span>|<span data-ttu-id="fe221-162">Int32</span><span class="sxs-lookup"><span data-stu-id="fe221-162">Int32</span></span>|<span data-ttu-id="fe221-163">hello hello 工作可能會重試的次數上限。</span><span class="sxs-lookup"><span data-stu-id="fe221-163">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="fe221-164">如果它的結束代碼是非零值 hello 批次服務會重試工作。</span><span class="sxs-lookup"><span data-stu-id="fe221-164">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="fe221-165">請注意，這個值會特別控制 hello 重試次數。</span><span class="sxs-lookup"><span data-stu-id="fe221-165">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="fe221-166">hello 批次服務將嘗試 hello 工作一次，並重試可能向上 toothis 限制。</span><span class="sxs-lookup"><span data-stu-id="fe221-166">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="fe221-167">例如，如果 hello 最大重試計數為 3，批次會嘗試向上 too4 時間 （一個初始再試一次和重試 3 次） 的工作。</span><span class="sxs-lookup"><span data-stu-id="fe221-167">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="fe221-168">如果 hello 最大重試計數為 0，hello 批次服務不會重試工作。</span><span class="sxs-lookup"><span data-stu-id="fe221-168">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="fe221-169">如果 hello 重試次數上限為-1，hello 批次服務將重試無限制的工作。</span><span class="sxs-lookup"><span data-stu-id="fe221-169">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="fe221-170">hello 預設值為 0 （無重試）。</span><span class="sxs-lookup"><span data-stu-id="fe221-170">hello default value is 0 (no retries).</span></span>|


###  <span data-ttu-id="fe221-171"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="fe221-171"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="fe221-172">元素名稱</span><span class="sxs-lookup"><span data-stu-id="fe221-172">Element name</span></span>|<span data-ttu-id="fe221-173">類型</span><span class="sxs-lookup"><span data-stu-id="fe221-173">Type</span></span>|<span data-ttu-id="fe221-174">注意事項</span><span class="sxs-lookup"><span data-stu-id="fe221-174">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="fe221-175">startTime</span><span class="sxs-lookup"><span data-stu-id="fe221-175">startTime</span></span>|<span data-ttu-id="fe221-176">DateTime</span><span class="sxs-lookup"><span data-stu-id="fe221-176">DateTime</span></span>|<span data-ttu-id="fe221-177">hello 開始執行的 hello 工作時間。</span><span class="sxs-lookup"><span data-stu-id="fe221-177">hello time at which hello task started running.</span></span> <span data-ttu-id="fe221-178">「 執行中 」 對應 toohello**執行**狀態，因此如果 hello 工作指定資源檔或應用程式封裝，然後 hello 開始時間就會反映 hello 啟動下載或部署這些哪個 hello 工作時間。</span><span class="sxs-lookup"><span data-stu-id="fe221-178">'Running' corresponds toohello **running** state, so if hello task specifies resource files or application packages, then hello start time reflects hello time at which hello task started downloading or deploying these.</span></span>  <span data-ttu-id="fe221-179">如果已重新啟動或重試 hello 工作，這是的 hello 最近一次在哪個 hello 工作開始執行。</span><span class="sxs-lookup"><span data-stu-id="fe221-179">If hello task has been restarted or retried, this is hello most recent time at which hello task started running.</span></span>|
|<span data-ttu-id="fe221-180">EndTime</span><span class="sxs-lookup"><span data-stu-id="fe221-180">endTime</span></span>|<span data-ttu-id="fe221-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="fe221-181">DateTime</span></span>|<span data-ttu-id="fe221-182">hello hello 任務完成時間。</span><span class="sxs-lookup"><span data-stu-id="fe221-182">hello time at which hello task completed.</span></span>|
|<span data-ttu-id="fe221-183">exitCode</span><span class="sxs-lookup"><span data-stu-id="fe221-183">exitCode</span></span>|<span data-ttu-id="fe221-184">Int32</span><span class="sxs-lookup"><span data-stu-id="fe221-184">Int32</span></span>|<span data-ttu-id="fe221-185">hello hello 工作的結束代碼。</span><span class="sxs-lookup"><span data-stu-id="fe221-185">hello exit code of hello task.</span></span>|
|<span data-ttu-id="fe221-186">retryCount</span><span class="sxs-lookup"><span data-stu-id="fe221-186">retryCount</span></span>|<span data-ttu-id="fe221-187">Int32</span><span class="sxs-lookup"><span data-stu-id="fe221-187">Int32</span></span>|<span data-ttu-id="fe221-188">hello hello 工作已 hello 批次服務重試次數。</span><span class="sxs-lookup"><span data-stu-id="fe221-188">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="fe221-189">它會結束，則為非零結束代碼，向上 toohello 指定 MaxTaskRetryCount 重試 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="fe221-189">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="fe221-190">requeueCount</span><span class="sxs-lookup"><span data-stu-id="fe221-190">requeueCount</span></span>|<span data-ttu-id="fe221-191">Int32</span><span class="sxs-lookup"><span data-stu-id="fe221-191">Int32</span></span>|<span data-ttu-id="fe221-192">hello 的 hello 導致使用者要求 hello 工作排 hello 批次服務的次數。</span><span class="sxs-lookup"><span data-stu-id="fe221-192">hello number of times hello task has been requeued by hello Batch service as hello result of a user request.</span></span><br /><br /> <span data-ttu-id="fe221-193">當 hello 使用者移除節點從集區 （調整大小或壓縮 hello 共用） 或 hello 作業時已停用，hello 使用者可以指定執行工作 hello 節點上執行排入佇列。</span><span class="sxs-lookup"><span data-stu-id="fe221-193">When hello user removes nodes from a pool (by resizing or shrinking hello pool) or when hello job is being disabled, hello user can specify that running tasks on hello nodes be requeued for execution.</span></span> <span data-ttu-id="fe221-194">這個計數會追蹤多少次已排入佇列 hello 工作基於這些理由。</span><span class="sxs-lookup"><span data-stu-id="fe221-194">This count tracks how many times hello task has been requeued for these reasons.</span></span>|
