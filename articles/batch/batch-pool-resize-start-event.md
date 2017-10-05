---
title: "Azure Batch 集區調整大小開始事件 | Microsoft Docs"
description: "Batch 集區調整大小開始事件的參考。"
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
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="8d6b1-103">集區調整大小開始事件</span><span class="sxs-lookup"><span data-stu-id="8d6b1-103">Pool resize start event</span></span>

 <span data-ttu-id="8d6b1-104">集區調整大小開始時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="8d6b1-105">由於集區調整大小為非同步事件，因此您可以預期當調整大小作業完成時，就會發出集區調整大小完成事件。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="8d6b1-106">下列範例顯示以手動調整大小的方式將集區大小從 0 調整為 2 個節點的集區調整大小開始事件內文。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="8d6b1-107">元素</span><span class="sxs-lookup"><span data-stu-id="8d6b1-107">Element</span></span>|<span data-ttu-id="8d6b1-108">類型</span><span class="sxs-lookup"><span data-stu-id="8d6b1-108">Type</span></span>|<span data-ttu-id="8d6b1-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="8d6b1-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="8d6b1-110">poolId</span><span class="sxs-lookup"><span data-stu-id="8d6b1-110">poolId</span></span>|<span data-ttu-id="8d6b1-111">String</span><span class="sxs-lookup"><span data-stu-id="8d6b1-111">String</span></span>|<span data-ttu-id="8d6b1-112">集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-112">The id of the pool.</span></span>|
|<span data-ttu-id="8d6b1-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="8d6b1-113">nodeDeallocationOption</span></span>|<span data-ttu-id="8d6b1-114">String</span><span class="sxs-lookup"><span data-stu-id="8d6b1-114">String</span></span>|<span data-ttu-id="8d6b1-115">指定當集區大小一直減少時，會自集區中移除節點。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="8d6b1-116">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="8d6b1-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="8d6b1-117">**requeue** – 終止執行中工作並重新排入佇列。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="8d6b1-118">當作業啟用時，工作將再次執行。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="8d6b1-119">一旦工作終止，隨即移除節點。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="8d6b1-120">**terminate** – 終止執行中工作。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="8d6b1-121">工作將不會再次執行。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-121">The tasks will not run again.</span></span> <span data-ttu-id="8d6b1-122">一旦工作終止，隨即移除節點。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="8d6b1-123">**taskcompletion** – 允許目前執行中工作完成。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="8d6b1-124">等待時不排程任何新的工作。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="8d6b1-125">所有工作完成時，即移除節點。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="8d6b1-126">**Retaineddata** - 允許目前執行中工作完成，然後等待所有工作資料保留期到期。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="8d6b1-127">等待時不排程任何新的工作。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="8d6b1-128">當所有工作保留期到期時即移除節點。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="8d6b1-129">預設值為 requeue。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="8d6b1-130">如果集區大小增加，則值會設定為 [無效]。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="8d6b1-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="8d6b1-131">currentDedicated</span></span>|<span data-ttu-id="8d6b1-132">Int32</span><span class="sxs-lookup"><span data-stu-id="8d6b1-132">Int32</span></span>|<span data-ttu-id="8d6b1-133">目前指派至集區的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="8d6b1-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="8d6b1-134">targetDedicated</span></span>|<span data-ttu-id="8d6b1-135">Int32</span><span class="sxs-lookup"><span data-stu-id="8d6b1-135">Int32</span></span>|<span data-ttu-id="8d6b1-136">向集區要求的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="8d6b1-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="8d6b1-137">enableAutoScale</span></span>|<span data-ttu-id="8d6b1-138">Bool</span><span class="sxs-lookup"><span data-stu-id="8d6b1-138">Bool</span></span>|<span data-ttu-id="8d6b1-139">指定集區大小是否隨著時間自動調整。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="8d6b1-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="8d6b1-140">isAutoPool</span></span>|<span data-ttu-id="8d6b1-141">Bool</span><span class="sxs-lookup"><span data-stu-id="8d6b1-141">Bool</span></span>|<span data-ttu-id="8d6b1-142">指定是否已透過作業的 AutoPool 機制建立集區。</span><span class="sxs-lookup"><span data-stu-id="8d6b1-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
