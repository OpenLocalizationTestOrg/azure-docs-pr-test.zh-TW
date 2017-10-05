---
title: "Azure Batch 集區調整大小完成事件 | Microsoft Docs"
description: "Batch 集區調整大小完成事件的參考。"
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
ms.openlocfilehash: 7072293d98526812cb42ce9c2f8e33bfcafaa149
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="b9de9-103">集區調整大小完成事件</span><span class="sxs-lookup"><span data-stu-id="b9de9-103">Pool resize complete event</span></span>

 <span data-ttu-id="b9de9-104">集區調整大小完成或失敗時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="b9de9-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="b9de9-105">下列範例顯示大小增加且成功完成的集區其集區調整大小完成事件內文。</span><span class="sxs-lookup"><span data-stu-id="b9de9-105">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "The operation succeeded"
}
```

|<span data-ttu-id="b9de9-106">元素</span><span class="sxs-lookup"><span data-stu-id="b9de9-106">Element</span></span>|<span data-ttu-id="b9de9-107">類型</span><span class="sxs-lookup"><span data-stu-id="b9de9-107">Type</span></span>|<span data-ttu-id="b9de9-108">注意事項</span><span class="sxs-lookup"><span data-stu-id="b9de9-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="b9de9-109">id</span><span class="sxs-lookup"><span data-stu-id="b9de9-109">id</span></span>|<span data-ttu-id="b9de9-110">String</span><span class="sxs-lookup"><span data-stu-id="b9de9-110">String</span></span>|<span data-ttu-id="b9de9-111">集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="b9de9-111">The id of the pool.</span></span>|
|<span data-ttu-id="b9de9-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="b9de9-112">nodeDeallocationOption</span></span>|<span data-ttu-id="b9de9-113">String</span><span class="sxs-lookup"><span data-stu-id="b9de9-113">String</span></span>|<span data-ttu-id="b9de9-114">指定當集區大小一直減少時，會自集區中移除節點。</span><span class="sxs-lookup"><span data-stu-id="b9de9-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="b9de9-115">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="b9de9-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="b9de9-116">**requeue** – 終止執行中工作並重新排入佇列。</span><span class="sxs-lookup"><span data-stu-id="b9de9-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="b9de9-117">當作業啟用時，工作將再次執行。</span><span class="sxs-lookup"><span data-stu-id="b9de9-117">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="b9de9-118">一旦工作終止，隨即移除節點。</span><span class="sxs-lookup"><span data-stu-id="b9de9-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="b9de9-119">**terminate** – 終止執行中工作。</span><span class="sxs-lookup"><span data-stu-id="b9de9-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="b9de9-120">工作將不會再次執行。</span><span class="sxs-lookup"><span data-stu-id="b9de9-120">The tasks will not run again.</span></span> <span data-ttu-id="b9de9-121">一旦工作終止，隨即移除節點。</span><span class="sxs-lookup"><span data-stu-id="b9de9-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="b9de9-122">**taskcompletion** – 允許目前執行中工作完成。</span><span class="sxs-lookup"><span data-stu-id="b9de9-122">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="b9de9-123">等待時不排程任何新的工作。</span><span class="sxs-lookup"><span data-stu-id="b9de9-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="b9de9-124">所有工作完成時，即移除節點。</span><span class="sxs-lookup"><span data-stu-id="b9de9-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="b9de9-125">**Retaineddata** - 允許目前執行中工作完成，然後等待所有工作資料保留期到期。</span><span class="sxs-lookup"><span data-stu-id="b9de9-125">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="b9de9-126">等待時不排程任何新的工作。</span><span class="sxs-lookup"><span data-stu-id="b9de9-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="b9de9-127">當所有工作保留期到期時即移除節點。</span><span class="sxs-lookup"><span data-stu-id="b9de9-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="b9de9-128">預設值為 requeue。</span><span class="sxs-lookup"><span data-stu-id="b9de9-128">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="b9de9-129">如果集區大小增加，則值會設定為 [無效]。</span><span class="sxs-lookup"><span data-stu-id="b9de9-129">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="b9de9-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="b9de9-130">currentDedicated</span></span>|<span data-ttu-id="b9de9-131">Int32</span><span class="sxs-lookup"><span data-stu-id="b9de9-131">Int32</span></span>|<span data-ttu-id="b9de9-132">目前指派至集區的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="b9de9-132">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="b9de9-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="b9de9-133">targetDedicated</span></span>|<span data-ttu-id="b9de9-134">Int32</span><span class="sxs-lookup"><span data-stu-id="b9de9-134">Int32</span></span>|<span data-ttu-id="b9de9-135">向集區要求的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="b9de9-135">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="b9de9-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="b9de9-136">enableAutoScale</span></span>|<span data-ttu-id="b9de9-137">Bool</span><span class="sxs-lookup"><span data-stu-id="b9de9-137">Bool</span></span>|<span data-ttu-id="b9de9-138">指定集區大小是否隨著時間自動調整。</span><span class="sxs-lookup"><span data-stu-id="b9de9-138">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="b9de9-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="b9de9-139">isAutoPool</span></span>|<span data-ttu-id="b9de9-140">Bool</span><span class="sxs-lookup"><span data-stu-id="b9de9-140">Bool</span></span>|<span data-ttu-id="b9de9-141">指定是否已透過作業的 AutoPool 機制建立集區。</span><span class="sxs-lookup"><span data-stu-id="b9de9-141">Specifies whether the pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="b9de9-142">startTime</span><span class="sxs-lookup"><span data-stu-id="b9de9-142">startTime</span></span>|<span data-ttu-id="b9de9-143">DateTime</span><span class="sxs-lookup"><span data-stu-id="b9de9-143">DateTime</span></span>|<span data-ttu-id="b9de9-144">集區調整大小開始時間。</span><span class="sxs-lookup"><span data-stu-id="b9de9-144">The time the pool resize started.</span></span>|
|<span data-ttu-id="b9de9-145">EndTime</span><span class="sxs-lookup"><span data-stu-id="b9de9-145">endTime</span></span>|<span data-ttu-id="b9de9-146">DateTime</span><span class="sxs-lookup"><span data-stu-id="b9de9-146">DateTime</span></span>|<span data-ttu-id="b9de9-147">集區調整大小完成時間。</span><span class="sxs-lookup"><span data-stu-id="b9de9-147">The time the pool resize completed.</span></span>|
|<span data-ttu-id="b9de9-148">ResultCode</span><span class="sxs-lookup"><span data-stu-id="b9de9-148">resultCode</span></span>|<span data-ttu-id="b9de9-149">String</span><span class="sxs-lookup"><span data-stu-id="b9de9-149">String</span></span>|<span data-ttu-id="b9de9-150">調整大小的結果。</span><span class="sxs-lookup"><span data-stu-id="b9de9-150">The result of the resize.</span></span>|
|<span data-ttu-id="b9de9-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="b9de9-151">resultMessage</span></span>|<span data-ttu-id="b9de9-152">String</span><span class="sxs-lookup"><span data-stu-id="b9de9-152">String</span></span>|<span data-ttu-id="b9de9-153">調整大小錯誤中包含結果的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b9de9-153">The resize error includes the details of the result.</span></span><br /><br /> <span data-ttu-id="b9de9-154">如果調整大小已成功完成，表示作業已成功。</span><span class="sxs-lookup"><span data-stu-id="b9de9-154">If the resize completed successfully it states that the operation succeeded.</span></span>|