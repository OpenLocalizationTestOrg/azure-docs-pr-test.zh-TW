---
title: "aaa\"Azure 批次工作開始事件 |Microsoft 文件 」"
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="8b88d-103">工作開始事件</span><span class="sxs-lookup"><span data-stu-id="8b88d-103">Task start event</span></span>

 <span data-ttu-id="8b88d-104">此事件就會發出工作已排定的 toostart 計算節點上後，由 hello 排程器。</span><span class="sxs-lookup"><span data-stu-id="8b88d-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="8b88d-105">請注意，是否 hello 將工作重試或排入佇列將會發出這個事件一次 hello 相同的工作，但 hello 重試計數和系統工作的版本會隨之更新。</span><span class="sxs-lookup"><span data-stu-id="8b88d-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="8b88d-106">hello 下列範例顯示 hello 主體工作開始事件。</span><span class="sxs-lookup"><span data-stu-id="8b88d-106">hello following example shows hello body of a task start event.</span></span>

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

|<span data-ttu-id="8b88d-107">元素名稱</span><span class="sxs-lookup"><span data-stu-id="8b88d-107">Element name</span></span>|<span data-ttu-id="8b88d-108">類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-108">Type</span></span>|<span data-ttu-id="8b88d-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="8b88d-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="8b88d-110">jobId</span><span class="sxs-lookup"><span data-stu-id="8b88d-110">jobId</span></span>|<span data-ttu-id="8b88d-111">String</span><span class="sxs-lookup"><span data-stu-id="8b88d-111">String</span></span>|<span data-ttu-id="8b88d-112">hello hello 作業包含 hello 工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="8b88d-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="8b88d-113">id</span><span class="sxs-lookup"><span data-stu-id="8b88d-113">id</span></span>|<span data-ttu-id="8b88d-114">String</span><span class="sxs-lookup"><span data-stu-id="8b88d-114">String</span></span>|<span data-ttu-id="8b88d-115">hello hello 工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="8b88d-115">hello id of hello task.</span></span>|
|<span data-ttu-id="8b88d-116">taskType</span><span class="sxs-lookup"><span data-stu-id="8b88d-116">taskType</span></span>|<span data-ttu-id="8b88d-117">String</span><span class="sxs-lookup"><span data-stu-id="8b88d-117">String</span></span>|<span data-ttu-id="8b88d-118">hello hello 工作類型。</span><span class="sxs-lookup"><span data-stu-id="8b88d-118">hello type of hello task.</span></span> <span data-ttu-id="8b88d-119">可以是 'JobManager'，表示這是作業管理員工作，或是 'User'，表示不是作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="8b88d-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="8b88d-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="8b88d-120">systemTaskVersion</span></span>|<span data-ttu-id="8b88d-121">Int32</span><span class="sxs-lookup"><span data-stu-id="8b88d-121">Int32</span></span>|<span data-ttu-id="8b88d-122">這是在工作上的 hello 內部重試計數器。</span><span class="sxs-lookup"><span data-stu-id="8b88d-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="8b88d-123">在內部 hello 批次服務可以重試工作 tooaccount 暫時性的問題。</span><span class="sxs-lookup"><span data-stu-id="8b88d-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="8b88d-124">這些問題可以包含內部排程錯誤或嘗試 toorecover 從運算節點處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="8b88d-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="8b88d-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="8b88d-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="8b88d-126">複雜類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-126">Complex Type</span></span>|<span data-ttu-id="8b88d-127">包含 hello 計算節點的 hello 工作已執行的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8b88d-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="8b88d-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="8b88d-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="8b88d-129">複雜類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-129">Complex Type</span></span>|<span data-ttu-id="8b88d-130">指定該 hello 工作需要多個計算節點的多個執行個體工作。</span><span class="sxs-lookup"><span data-stu-id="8b88d-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="8b88d-131">請參閱 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) (英文) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8b88d-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="8b88d-132">constraints</span><span class="sxs-lookup"><span data-stu-id="8b88d-132">constraints</span></span>](#constraints)|<span data-ttu-id="8b88d-133">複雜類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-133">Complex Type</span></span>|<span data-ttu-id="8b88d-134">套用 toothis 工作 hello 執行條件約束。</span><span class="sxs-lookup"><span data-stu-id="8b88d-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="8b88d-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="8b88d-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="8b88d-136">複雜類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-136">Complex Type</span></span>|<span data-ttu-id="8b88d-137">包含有關 hello hello 工作執行資訊。</span><span class="sxs-lookup"><span data-stu-id="8b88d-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="8b88d-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="8b88d-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="8b88d-139">元素名稱</span><span class="sxs-lookup"><span data-stu-id="8b88d-139">Element name</span></span>|<span data-ttu-id="8b88d-140">類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-140">Type</span></span>|<span data-ttu-id="8b88d-141">注意事項</span><span class="sxs-lookup"><span data-stu-id="8b88d-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="8b88d-142">poolId</span><span class="sxs-lookup"><span data-stu-id="8b88d-142">poolId</span></span>|<span data-ttu-id="8b88d-143">String</span><span class="sxs-lookup"><span data-stu-id="8b88d-143">String</span></span>|<span data-ttu-id="8b88d-144">hello hello 集區的 hello 工作已執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="8b88d-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="8b88d-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="8b88d-145">nodeId</span></span>|<span data-ttu-id="8b88d-146">String</span><span class="sxs-lookup"><span data-stu-id="8b88d-146">String</span></span>|<span data-ttu-id="8b88d-147">hello hello 節點的 hello 工作已執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="8b88d-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="8b88d-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="8b88d-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="8b88d-149">元素名稱</span><span class="sxs-lookup"><span data-stu-id="8b88d-149">Element name</span></span>|<span data-ttu-id="8b88d-150">類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-150">Type</span></span>|<span data-ttu-id="8b88d-151">注意事項</span><span class="sxs-lookup"><span data-stu-id="8b88d-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="8b88d-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="8b88d-152">numberOfInstances</span></span>|<span data-ttu-id="8b88d-153">int</span><span class="sxs-lookup"><span data-stu-id="8b88d-153">Int</span></span>|<span data-ttu-id="8b88d-154">hello hello 工作所需的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="8b88d-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="8b88d-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="8b88d-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="8b88d-156">元素名稱</span><span class="sxs-lookup"><span data-stu-id="8b88d-156">Element name</span></span>|<span data-ttu-id="8b88d-157">類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-157">Type</span></span>|<span data-ttu-id="8b88d-158">注意事項</span><span class="sxs-lookup"><span data-stu-id="8b88d-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="8b88d-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="8b88d-159">maxTaskRetryCount</span></span>|<span data-ttu-id="8b88d-160">Int32</span><span class="sxs-lookup"><span data-stu-id="8b88d-160">Int32</span></span>|<span data-ttu-id="8b88d-161">hello hello 工作可能會重試的次數上限。</span><span class="sxs-lookup"><span data-stu-id="8b88d-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="8b88d-162">如果它的結束代碼是非零值 hello 批次服務會重試工作。</span><span class="sxs-lookup"><span data-stu-id="8b88d-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="8b88d-163">請注意，這個值會特別控制 hello 重試次數。</span><span class="sxs-lookup"><span data-stu-id="8b88d-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="8b88d-164">hello 批次服務將嘗試 hello 工作一次，並重試可能向上 toothis 限制。</span><span class="sxs-lookup"><span data-stu-id="8b88d-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="8b88d-165">例如，如果 hello 最大重試計數為 3，批次會嘗試向上 too4 時間 （一個初始再試一次和重試 3 次） 的工作。</span><span class="sxs-lookup"><span data-stu-id="8b88d-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="8b88d-166">如果 hello 最大重試計數為 0，hello 批次服務不會重試工作。</span><span class="sxs-lookup"><span data-stu-id="8b88d-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="8b88d-167">如果 hello 重試次數上限為-1，hello 批次服務將重試無限制的工作。</span><span class="sxs-lookup"><span data-stu-id="8b88d-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="8b88d-168">hello 預設值為 0 （無重試）。</span><span class="sxs-lookup"><span data-stu-id="8b88d-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="8b88d-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="8b88d-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="8b88d-170">元素名稱</span><span class="sxs-lookup"><span data-stu-id="8b88d-170">Element name</span></span>|<span data-ttu-id="8b88d-171">類型</span><span class="sxs-lookup"><span data-stu-id="8b88d-171">Type</span></span>|<span data-ttu-id="8b88d-172">注意事項</span><span class="sxs-lookup"><span data-stu-id="8b88d-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="8b88d-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="8b88d-173">retryCount</span></span>|<span data-ttu-id="8b88d-174">Int32</span><span class="sxs-lookup"><span data-stu-id="8b88d-174">Int32</span></span>|<span data-ttu-id="8b88d-175">hello hello 工作已 hello 批次服務重試次數。</span><span class="sxs-lookup"><span data-stu-id="8b88d-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="8b88d-176">如果它，則為非零結束代碼，結束 toohello 上指定的 MaxTaskRetryCount，則重試 hello 工作</span><span class="sxs-lookup"><span data-stu-id="8b88d-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
