---
title: "Azure Batch 工作開始事件 | Microsoft Docs"
description: "Batch 工作開始事件的參考。"
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="2f317-103">工作開始事件</span><span class="sxs-lookup"><span data-stu-id="2f317-103">Task start event</span></span>

 <span data-ttu-id="2f317-104">一旦排程器已排程工作在計算節點上執行時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="2f317-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="2f317-105">請注意，如果工作已重試或重新排入佇列，則系統會為相同的工作再次發出此事件，但重試計數與系統工作版本將會隨之更新。</span><span class="sxs-lookup"><span data-stu-id="2f317-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="2f317-106">下列範例顯示工作開始事件內文。</span><span class="sxs-lookup"><span data-stu-id="2f317-106">The following example shows the body of a task start event.</span></span>

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
        "retryCount": 0
    }
}
```

|<span data-ttu-id="2f317-107">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2f317-107">Element name</span></span>|<span data-ttu-id="2f317-108">類型</span><span class="sxs-lookup"><span data-stu-id="2f317-108">Type</span></span>|<span data-ttu-id="2f317-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="2f317-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2f317-110">jobId</span><span class="sxs-lookup"><span data-stu-id="2f317-110">jobId</span></span>|<span data-ttu-id="2f317-111">String</span><span class="sxs-lookup"><span data-stu-id="2f317-111">String</span></span>|<span data-ttu-id="2f317-112">包含工作的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="2f317-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="2f317-113">id</span><span class="sxs-lookup"><span data-stu-id="2f317-113">id</span></span>|<span data-ttu-id="2f317-114">String</span><span class="sxs-lookup"><span data-stu-id="2f317-114">String</span></span>|<span data-ttu-id="2f317-115">工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="2f317-115">The id of the task.</span></span>|
|<span data-ttu-id="2f317-116">taskType</span><span class="sxs-lookup"><span data-stu-id="2f317-116">taskType</span></span>|<span data-ttu-id="2f317-117">String</span><span class="sxs-lookup"><span data-stu-id="2f317-117">String</span></span>|<span data-ttu-id="2f317-118">工作類型。</span><span class="sxs-lookup"><span data-stu-id="2f317-118">The type of the task.</span></span> <span data-ttu-id="2f317-119">可以是 'JobManager'，表示這是作業管理員工作，或是 'User'，表示不是作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="2f317-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="2f317-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="2f317-120">systemTaskVersion</span></span>|<span data-ttu-id="2f317-121">Int32</span><span class="sxs-lookup"><span data-stu-id="2f317-121">Int32</span></span>|<span data-ttu-id="2f317-122">這是作業上的內部重試計數器。</span><span class="sxs-lookup"><span data-stu-id="2f317-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="2f317-123">Batch 服務可在內部重試工作，以處理暫時性問題。</span><span class="sxs-lookup"><span data-stu-id="2f317-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="2f317-124">這些問題包含內部排程錯誤，或嘗試從不正常狀態的計算節點復原。</span><span class="sxs-lookup"><span data-stu-id="2f317-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="2f317-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="2f317-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="2f317-126">複雜類型</span><span class="sxs-lookup"><span data-stu-id="2f317-126">Complex Type</span></span>|<span data-ttu-id="2f317-127">包含工作執行所在計算節點的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2f317-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="2f317-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="2f317-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="2f317-129">複雜類型</span><span class="sxs-lookup"><span data-stu-id="2f317-129">Complex Type</span></span>|<span data-ttu-id="2f317-130">指定工作為需要多個計算節點的多重執行個體工作。</span><span class="sxs-lookup"><span data-stu-id="2f317-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="2f317-131">請參閱 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) (英文) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2f317-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="2f317-132">constraints</span><span class="sxs-lookup"><span data-stu-id="2f317-132">constraints</span></span>](#constraints)|<span data-ttu-id="2f317-133">複雜類型</span><span class="sxs-lookup"><span data-stu-id="2f317-133">Complex Type</span></span>|<span data-ttu-id="2f317-134">套用至此工作的執行限制。</span><span class="sxs-lookup"><span data-stu-id="2f317-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="2f317-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="2f317-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="2f317-136">複雜類型</span><span class="sxs-lookup"><span data-stu-id="2f317-136">Complex Type</span></span>|<span data-ttu-id="2f317-137">包含執行工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2f317-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="2f317-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="2f317-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="2f317-139">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2f317-139">Element name</span></span>|<span data-ttu-id="2f317-140">類型</span><span class="sxs-lookup"><span data-stu-id="2f317-140">Type</span></span>|<span data-ttu-id="2f317-141">注意事項</span><span class="sxs-lookup"><span data-stu-id="2f317-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2f317-142">poolId</span><span class="sxs-lookup"><span data-stu-id="2f317-142">poolId</span></span>|<span data-ttu-id="2f317-143">String</span><span class="sxs-lookup"><span data-stu-id="2f317-143">String</span></span>|<span data-ttu-id="2f317-144">工作執行所在集區的識別碼。</span><span class="sxs-lookup"><span data-stu-id="2f317-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="2f317-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="2f317-145">nodeId</span></span>|<span data-ttu-id="2f317-146">String</span><span class="sxs-lookup"><span data-stu-id="2f317-146">String</span></span>|<span data-ttu-id="2f317-147">工作執行所在節點的識別碼。</span><span class="sxs-lookup"><span data-stu-id="2f317-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="2f317-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="2f317-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="2f317-149">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2f317-149">Element name</span></span>|<span data-ttu-id="2f317-150">類型</span><span class="sxs-lookup"><span data-stu-id="2f317-150">Type</span></span>|<span data-ttu-id="2f317-151">注意事項</span><span class="sxs-lookup"><span data-stu-id="2f317-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2f317-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="2f317-152">numberOfInstances</span></span>|<span data-ttu-id="2f317-153">int</span><span class="sxs-lookup"><span data-stu-id="2f317-153">Int</span></span>|<span data-ttu-id="2f317-154">工作需要的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="2f317-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="2f317-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="2f317-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="2f317-156">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2f317-156">Element name</span></span>|<span data-ttu-id="2f317-157">類型</span><span class="sxs-lookup"><span data-stu-id="2f317-157">Type</span></span>|<span data-ttu-id="2f317-158">注意事項</span><span class="sxs-lookup"><span data-stu-id="2f317-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2f317-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="2f317-159">maxTaskRetryCount</span></span>|<span data-ttu-id="2f317-160">Int32</span><span class="sxs-lookup"><span data-stu-id="2f317-160">Int32</span></span>|<span data-ttu-id="2f317-161">工作重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="2f317-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="2f317-162">如果工作的結束代碼不是零，Batch 服務會重試工作。</span><span class="sxs-lookup"><span data-stu-id="2f317-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="2f317-163">請注意，這個值會特別控制重試次數。</span><span class="sxs-lookup"><span data-stu-id="2f317-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="2f317-164">Batch 服務會嘗試工作一次，然後可一直重試直到達此限制。</span><span class="sxs-lookup"><span data-stu-id="2f317-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="2f317-165">例如，如果重試計數上限為 3，則 Batch 可嘗試工作最多 4 次 (一次首次嘗試，3 次重試)。</span><span class="sxs-lookup"><span data-stu-id="2f317-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="2f317-166">如果重試計數上限為 0，則 Batch 服務不會重試工作。</span><span class="sxs-lookup"><span data-stu-id="2f317-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="2f317-167">如果重試計數上限為 -1，則 Batch 服務會無限制地重試工作。</span><span class="sxs-lookup"><span data-stu-id="2f317-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="2f317-168">預設值為 0 (不重試)。</span><span class="sxs-lookup"><span data-stu-id="2f317-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="2f317-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="2f317-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="2f317-170">元素名稱</span><span class="sxs-lookup"><span data-stu-id="2f317-170">Element name</span></span>|<span data-ttu-id="2f317-171">類型</span><span class="sxs-lookup"><span data-stu-id="2f317-171">Type</span></span>|<span data-ttu-id="2f317-172">注意事項</span><span class="sxs-lookup"><span data-stu-id="2f317-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2f317-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="2f317-173">retryCount</span></span>|<span data-ttu-id="2f317-174">Int32</span><span class="sxs-lookup"><span data-stu-id="2f317-174">Int32</span></span>|<span data-ttu-id="2f317-175">Batch 服務已重試工作的次數。</span><span class="sxs-lookup"><span data-stu-id="2f317-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="2f317-176">如果工作結束時的結束代碼不是零，便會重試工作，直到次數達指定的 MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="2f317-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
