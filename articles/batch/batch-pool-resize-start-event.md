---
title: "aaa\"Azure Batch 集區調整大小開始事件 |Microsoft 文件 」"
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="ceb98-103">集區調整大小開始事件</span><span class="sxs-lookup"><span data-stu-id="ceb98-103">Pool resize start event</span></span>

 <span data-ttu-id="ceb98-104">集區調整大小開始時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="ceb98-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="ceb98-105">由於 hello 集區調整大小是非同步的事件，您可以預期發出一次 hello 的調整大小作業的集區調整大小完成事件 toobe 完成。</span><span class="sxs-lookup"><span data-stu-id="ceb98-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="ceb98-106">下列範例顯示 hello 0 too2 節點手動調整大小集區的集區調整大小開始事件的本文 hello 調整大小。</span><span class="sxs-lookup"><span data-stu-id="ceb98-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="ceb98-107">元素</span><span class="sxs-lookup"><span data-stu-id="ceb98-107">Element</span></span>|<span data-ttu-id="ceb98-108">類型</span><span class="sxs-lookup"><span data-stu-id="ceb98-108">Type</span></span>|<span data-ttu-id="ceb98-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="ceb98-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="ceb98-110">poolId</span><span class="sxs-lookup"><span data-stu-id="ceb98-110">poolId</span></span>|<span data-ttu-id="ceb98-111">String</span><span class="sxs-lookup"><span data-stu-id="ceb98-111">String</span></span>|<span data-ttu-id="ceb98-112">hello hello 集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="ceb98-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="ceb98-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="ceb98-113">nodeDeallocationOption</span></span>|<span data-ttu-id="ceb98-114">String</span><span class="sxs-lookup"><span data-stu-id="ceb98-114">String</span></span>|<span data-ttu-id="ceb98-115">指定當節點可能會移除從 hello 集區中，如果 hello 集區大小減少。</span><span class="sxs-lookup"><span data-stu-id="ceb98-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="ceb98-116">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="ceb98-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="ceb98-117">**requeue** – 終止執行中工作並重新排入佇列。</span><span class="sxs-lookup"><span data-stu-id="ceb98-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="ceb98-118">hello 作業啟用時，會再次執行 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="ceb98-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="ceb98-119">一旦工作終止，隨即移除節點。</span><span class="sxs-lookup"><span data-stu-id="ceb98-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="ceb98-120">**terminate** – 終止執行中工作。</span><span class="sxs-lookup"><span data-stu-id="ceb98-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="ceb98-121">hello 工作不會執行一次。</span><span class="sxs-lookup"><span data-stu-id="ceb98-121">hello tasks will not run again.</span></span> <span data-ttu-id="ceb98-122">一旦工作終止，隨即移除節點。</span><span class="sxs-lookup"><span data-stu-id="ceb98-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="ceb98-123">**taskcompletion** -允許正在執行工作 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="ceb98-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="ceb98-124">等待時不排程任何新的工作。</span><span class="sxs-lookup"><span data-stu-id="ceb98-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="ceb98-125">所有工作完成時，即移除節點。</span><span class="sxs-lookup"><span data-stu-id="ceb98-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="ceb98-126">**Retaineddata** -允許正在執行的工作 toocomplete，然後等待所有工作的資料保留週期 tooexpire。</span><span class="sxs-lookup"><span data-stu-id="ceb98-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="ceb98-127">等待時不排程任何新的工作。</span><span class="sxs-lookup"><span data-stu-id="ceb98-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="ceb98-128">當所有工作保留期到期時即移除節點。</span><span class="sxs-lookup"><span data-stu-id="ceb98-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="ceb98-129">hello 預設值為重新排入佇列。</span><span class="sxs-lookup"><span data-stu-id="ceb98-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="ceb98-130">如果 hello 集區大小增加，則 hello 值會設定太**無效**。</span><span class="sxs-lookup"><span data-stu-id="ceb98-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="ceb98-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="ceb98-131">currentDedicated</span></span>|<span data-ttu-id="ceb98-132">Int32</span><span class="sxs-lookup"><span data-stu-id="ceb98-132">Int32</span></span>|<span data-ttu-id="ceb98-133">hello 的運算節點數目目前已指派 toohello 集區。</span><span class="sxs-lookup"><span data-stu-id="ceb98-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="ceb98-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="ceb98-134">targetDedicated</span></span>|<span data-ttu-id="ceb98-135">Int32</span><span class="sxs-lookup"><span data-stu-id="ceb98-135">Int32</span></span>|<span data-ttu-id="ceb98-136">hello hello 集區要求的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="ceb98-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="ceb98-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="ceb98-137">enableAutoScale</span></span>|<span data-ttu-id="ceb98-138">Bool</span><span class="sxs-lookup"><span data-stu-id="ceb98-138">Bool</span></span>|<span data-ttu-id="ceb98-139">指定是否 hello 集區大小會自動調整一段時間。</span><span class="sxs-lookup"><span data-stu-id="ceb98-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="ceb98-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="ceb98-140">isAutoPool</span></span>|<span data-ttu-id="ceb98-141">Bool</span><span class="sxs-lookup"><span data-stu-id="ceb98-141">Bool</span></span>|<span data-ttu-id="ceb98-142">指定是否已透過作業的 AutoPool 機制建立 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="ceb98-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
