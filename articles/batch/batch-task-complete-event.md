---
title: "aaa\"Azure 批次工作完成事件 |Microsoft 文件 」"
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
ms.openlocfilehash: c126bf897071c008be3d24190cf77bba5878b807
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="task-complete-event"></a><span data-ttu-id="9c384-103">工作完成事件</span><span class="sxs-lookup"><span data-stu-id="9c384-103">Task complete event</span></span>

 <span data-ttu-id="9c384-104">工作完成後，不論 hello 結束代碼，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="9c384-104">This event is emitted once a task is completed, regardless of hello exit code.</span></span> <span data-ttu-id="9c384-105">這個事件可以是工作中，使用的 toodetermine hello 期間 hello 工作執行的所在位置，以及是否已重試。</span><span class="sxs-lookup"><span data-stu-id="9c384-105">This event can be used toodetermine hello duration of a task, where hello task ran, and whether it was retried.</span></span>


 <span data-ttu-id="9c384-106">hello 下列範例顯示 hello 主體的工作完成事件。</span><span class="sxs-lookup"><span data-stu-id="9c384-106">hello following example shows hello body of a task complete event.</span></span>

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

|<span data-ttu-id="9c384-107">元素名稱</span><span class="sxs-lookup"><span data-stu-id="9c384-107">Element name</span></span>|<span data-ttu-id="9c384-108">類型</span><span class="sxs-lookup"><span data-stu-id="9c384-108">Type</span></span>|<span data-ttu-id="9c384-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="9c384-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9c384-110">jobId</span><span class="sxs-lookup"><span data-stu-id="9c384-110">jobId</span></span>|<span data-ttu-id="9c384-111">String</span><span class="sxs-lookup"><span data-stu-id="9c384-111">String</span></span>|<span data-ttu-id="9c384-112">hello hello 作業包含 hello 工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="9c384-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="9c384-113">id</span><span class="sxs-lookup"><span data-stu-id="9c384-113">id</span></span>|<span data-ttu-id="9c384-114">String</span><span class="sxs-lookup"><span data-stu-id="9c384-114">String</span></span>|<span data-ttu-id="9c384-115">hello hello 工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="9c384-115">hello id of hello task.</span></span>|
|<span data-ttu-id="9c384-116">taskType</span><span class="sxs-lookup"><span data-stu-id="9c384-116">taskType</span></span>|<span data-ttu-id="9c384-117">String</span><span class="sxs-lookup"><span data-stu-id="9c384-117">String</span></span>|<span data-ttu-id="9c384-118">hello hello 工作類型。</span><span class="sxs-lookup"><span data-stu-id="9c384-118">hello type of hello task.</span></span> <span data-ttu-id="9c384-119">可以是 'JobManager'，表示這是作業管理員工作，或是 'User'，表示不是作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="9c384-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="9c384-120">對於作業準備工作、作業發行工作或開始工作。不會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="9c384-120">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="9c384-121">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="9c384-121">systemTaskVersion</span></span>|<span data-ttu-id="9c384-122">Int32</span><span class="sxs-lookup"><span data-stu-id="9c384-122">Int32</span></span>|<span data-ttu-id="9c384-123">這是在工作上的 hello 內部重試計數器。</span><span class="sxs-lookup"><span data-stu-id="9c384-123">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="9c384-124">在內部 hello 批次服務可以重試工作 tooaccount 暫時性的問題。</span><span class="sxs-lookup"><span data-stu-id="9c384-124">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="9c384-125">這些問題可以包含內部排程錯誤或嘗試 toorecover 從運算節點處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="9c384-125">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="9c384-126">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="9c384-126">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="9c384-127">複雜類型</span><span class="sxs-lookup"><span data-stu-id="9c384-127">Complex Type</span></span>|<span data-ttu-id="9c384-128">包含 hello 計算節點的 hello 工作已執行的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9c384-128">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="9c384-129">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="9c384-129">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="9c384-130">複雜類型</span><span class="sxs-lookup"><span data-stu-id="9c384-130">Complex Type</span></span>|<span data-ttu-id="9c384-131">指定該 hello 工作是多個執行個體工作需要多個計算節點。</span><span class="sxs-lookup"><span data-stu-id="9c384-131">Specifies that hello task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="9c384-132">請參閱 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) (英文) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9c384-132">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="9c384-133">constraints</span><span class="sxs-lookup"><span data-stu-id="9c384-133">constraints</span></span>](#constraints)|<span data-ttu-id="9c384-134">複雜類型</span><span class="sxs-lookup"><span data-stu-id="9c384-134">Complex Type</span></span>|<span data-ttu-id="9c384-135">套用 toothis 工作 hello 執行條件約束。</span><span class="sxs-lookup"><span data-stu-id="9c384-135">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="9c384-136">executionInfo</span><span class="sxs-lookup"><span data-stu-id="9c384-136">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="9c384-137">複雜類型</span><span class="sxs-lookup"><span data-stu-id="9c384-137">Complex Type</span></span>|<span data-ttu-id="9c384-138">包含有關 hello hello 工作執行資訊。</span><span class="sxs-lookup"><span data-stu-id="9c384-138">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="9c384-139"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="9c384-139"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="9c384-140">元素名稱</span><span class="sxs-lookup"><span data-stu-id="9c384-140">Element name</span></span>|<span data-ttu-id="9c384-141">類型</span><span class="sxs-lookup"><span data-stu-id="9c384-141">Type</span></span>|<span data-ttu-id="9c384-142">注意事項</span><span class="sxs-lookup"><span data-stu-id="9c384-142">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9c384-143">poolId</span><span class="sxs-lookup"><span data-stu-id="9c384-143">poolId</span></span>|<span data-ttu-id="9c384-144">String</span><span class="sxs-lookup"><span data-stu-id="9c384-144">String</span></span>|<span data-ttu-id="9c384-145">hello hello 集區的 hello 工作已執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="9c384-145">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="9c384-146">nodeId</span><span class="sxs-lookup"><span data-stu-id="9c384-146">nodeId</span></span>|<span data-ttu-id="9c384-147">String</span><span class="sxs-lookup"><span data-stu-id="9c384-147">String</span></span>|<span data-ttu-id="9c384-148">hello hello 節點的 hello 工作已執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="9c384-148">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="9c384-149"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="9c384-149"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="9c384-150">元素名稱</span><span class="sxs-lookup"><span data-stu-id="9c384-150">Element name</span></span>|<span data-ttu-id="9c384-151">類型</span><span class="sxs-lookup"><span data-stu-id="9c384-151">Type</span></span>|<span data-ttu-id="9c384-152">注意事項</span><span class="sxs-lookup"><span data-stu-id="9c384-152">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9c384-153">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="9c384-153">numberOfInstances</span></span>|<span data-ttu-id="9c384-154">Int32</span><span class="sxs-lookup"><span data-stu-id="9c384-154">Int32</span></span>|<span data-ttu-id="9c384-155">hello hello 工作所需的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="9c384-155">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="9c384-156"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="9c384-156"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="9c384-157">元素名稱</span><span class="sxs-lookup"><span data-stu-id="9c384-157">Element name</span></span>|<span data-ttu-id="9c384-158">類型</span><span class="sxs-lookup"><span data-stu-id="9c384-158">Type</span></span>|<span data-ttu-id="9c384-159">注意事項</span><span class="sxs-lookup"><span data-stu-id="9c384-159">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9c384-160">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="9c384-160">maxTaskRetryCount</span></span>|<span data-ttu-id="9c384-161">Int32</span><span class="sxs-lookup"><span data-stu-id="9c384-161">Int32</span></span>|<span data-ttu-id="9c384-162">hello hello 工作可能會重試的次數上限。</span><span class="sxs-lookup"><span data-stu-id="9c384-162">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="9c384-163">如果它的結束代碼是非零值 hello 批次服務會重試工作。</span><span class="sxs-lookup"><span data-stu-id="9c384-163">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="9c384-164">請注意，這個值會特別控制 hello 重試次數。</span><span class="sxs-lookup"><span data-stu-id="9c384-164">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="9c384-165">hello 批次服務將嘗試 hello 工作一次，並重試可能向上 toothis 限制。</span><span class="sxs-lookup"><span data-stu-id="9c384-165">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="9c384-166">例如，如果 hello 最大重試計數為 3，批次會嘗試向上 too4 時間 （一個初始再試一次和重試 3 次） 的工作。</span><span class="sxs-lookup"><span data-stu-id="9c384-166">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="9c384-167">如果 hello 最大重試計數為 0，hello 批次服務不會重試工作。</span><span class="sxs-lookup"><span data-stu-id="9c384-167">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="9c384-168">如果 hello 重試次數上限為-1，hello 批次服務將重試無限制的工作。</span><span class="sxs-lookup"><span data-stu-id="9c384-168">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="9c384-169">hello 預設值為 0 （無重試）。</span><span class="sxs-lookup"><span data-stu-id="9c384-169">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="9c384-170"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="9c384-170"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="9c384-171">元素名稱</span><span class="sxs-lookup"><span data-stu-id="9c384-171">Element name</span></span>|<span data-ttu-id="9c384-172">類型</span><span class="sxs-lookup"><span data-stu-id="9c384-172">Type</span></span>|<span data-ttu-id="9c384-173">注意事項</span><span class="sxs-lookup"><span data-stu-id="9c384-173">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9c384-174">startTime</span><span class="sxs-lookup"><span data-stu-id="9c384-174">startTime</span></span>|<span data-ttu-id="9c384-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c384-175">DateTime</span></span>|<span data-ttu-id="9c384-176">hello 開始執行的 hello 工作時間。</span><span class="sxs-lookup"><span data-stu-id="9c384-176">hello time at which hello task started running.</span></span> <span data-ttu-id="9c384-177">「 執行中 」 對應 toohello**執行**狀態，因此如果 hello 工作指定資源檔或應用程式封裝，然後 hello 開始時間就會反映 hello 啟動下載或部署這些哪個 hello 工作時間。</span><span class="sxs-lookup"><span data-stu-id="9c384-177">'Running' corresponds toohello **running** state, so if hello task specifies resource files or application packages, then hello start time reflects hello time at which hello task started downloading or deploying these.</span></span>  <span data-ttu-id="9c384-178">如果已重新啟動或重試 hello 工作，這是的 hello 最近一次在哪個 hello 工作開始執行。</span><span class="sxs-lookup"><span data-stu-id="9c384-178">If hello task has been restarted or retried, this is hello most recent time at which hello task started running.</span></span>|
|<span data-ttu-id="9c384-179">EndTime</span><span class="sxs-lookup"><span data-stu-id="9c384-179">endTime</span></span>|<span data-ttu-id="9c384-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c384-180">DateTime</span></span>|<span data-ttu-id="9c384-181">hello hello 任務完成時間。</span><span class="sxs-lookup"><span data-stu-id="9c384-181">hello time at which hello task completed.</span></span>|
|<span data-ttu-id="9c384-182">exitCode</span><span class="sxs-lookup"><span data-stu-id="9c384-182">exitCode</span></span>|<span data-ttu-id="9c384-183">Int32</span><span class="sxs-lookup"><span data-stu-id="9c384-183">Int32</span></span>|<span data-ttu-id="9c384-184">hello hello 工作的結束代碼。</span><span class="sxs-lookup"><span data-stu-id="9c384-184">hello exit code of hello task.</span></span>|
|<span data-ttu-id="9c384-185">retryCount</span><span class="sxs-lookup"><span data-stu-id="9c384-185">retryCount</span></span>|<span data-ttu-id="9c384-186">Int32</span><span class="sxs-lookup"><span data-stu-id="9c384-186">Int32</span></span>|<span data-ttu-id="9c384-187">hello hello 工作已 hello 批次服務重試次數。</span><span class="sxs-lookup"><span data-stu-id="9c384-187">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="9c384-188">它會結束，則為非零結束代碼，向上 toohello 指定 MaxTaskRetryCount 重試 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="9c384-188">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="9c384-189">requeueCount</span><span class="sxs-lookup"><span data-stu-id="9c384-189">requeueCount</span></span>|<span data-ttu-id="9c384-190">Int32</span><span class="sxs-lookup"><span data-stu-id="9c384-190">Int32</span></span>|<span data-ttu-id="9c384-191">hello 的 hello 導致使用者要求 hello 工作排 hello 批次服務的次數。</span><span class="sxs-lookup"><span data-stu-id="9c384-191">hello number of times hello task has been requeued by hello Batch service as hello result of a user request.</span></span><br /><br /> <span data-ttu-id="9c384-192">當 hello 使用者移除節點從集區 （調整大小或壓縮 hello 共用） 或 hello 作業時已停用，hello 使用者可以指定執行工作 hello 節點上執行排入佇列。</span><span class="sxs-lookup"><span data-stu-id="9c384-192">When hello user removes nodes from a pool (by resizing or shrinking hello pool) or when hello job is being disabled, hello user can specify that running tasks on hello nodes be requeued for execution.</span></span> <span data-ttu-id="9c384-193">這個計數會追蹤多少次已排入佇列 hello 工作基於這些理由。</span><span class="sxs-lookup"><span data-stu-id="9c384-193">This count tracks how many times hello task has been requeued for these reasons.</span></span>|
