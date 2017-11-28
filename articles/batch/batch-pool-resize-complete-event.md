---
title: "aaa\"Azure Batch 集區調整大小完成事件 |Microsoft 文件 」"
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="147f0-103">集區調整大小完成事件</span><span class="sxs-lookup"><span data-stu-id="147f0-103">Pool resize complete event</span></span>

 <span data-ttu-id="147f0-104">集區調整大小完成或失敗時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="147f0-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="147f0-105">hello 下列範例顯示 hello 主體的大小增加，且已順利完成的集區的集區調整大小完成事件。</span><span class="sxs-lookup"><span data-stu-id="147f0-105">hello following example shows hello body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

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
    "resizeError": "hello operation succeeded"
}
```

|<span data-ttu-id="147f0-106">元素</span><span class="sxs-lookup"><span data-stu-id="147f0-106">Element</span></span>|<span data-ttu-id="147f0-107">類型</span><span class="sxs-lookup"><span data-stu-id="147f0-107">Type</span></span>|<span data-ttu-id="147f0-108">注意事項</span><span class="sxs-lookup"><span data-stu-id="147f0-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="147f0-109">id</span><span class="sxs-lookup"><span data-stu-id="147f0-109">id</span></span>|<span data-ttu-id="147f0-110">String</span><span class="sxs-lookup"><span data-stu-id="147f0-110">String</span></span>|<span data-ttu-id="147f0-111">hello hello 集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="147f0-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="147f0-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="147f0-112">nodeDeallocationOption</span></span>|<span data-ttu-id="147f0-113">String</span><span class="sxs-lookup"><span data-stu-id="147f0-113">String</span></span>|<span data-ttu-id="147f0-114">指定當節點可能會移除從 hello 集區中，如果 hello 集區大小減少。</span><span class="sxs-lookup"><span data-stu-id="147f0-114">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="147f0-115">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="147f0-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="147f0-116">**requeue** – 終止執行中工作並重新排入佇列。</span><span class="sxs-lookup"><span data-stu-id="147f0-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="147f0-117">hello 作業啟用時，會再次執行 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="147f0-117">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="147f0-118">一旦工作終止，隨即移除節點。</span><span class="sxs-lookup"><span data-stu-id="147f0-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="147f0-119">**terminate** – 終止執行中工作。</span><span class="sxs-lookup"><span data-stu-id="147f0-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="147f0-120">hello 工作不會執行一次。</span><span class="sxs-lookup"><span data-stu-id="147f0-120">hello tasks will not run again.</span></span> <span data-ttu-id="147f0-121">一旦工作終止，隨即移除節點。</span><span class="sxs-lookup"><span data-stu-id="147f0-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="147f0-122">**taskcompletion** -允許正在執行工作 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="147f0-122">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="147f0-123">等待時不排程任何新的工作。</span><span class="sxs-lookup"><span data-stu-id="147f0-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="147f0-124">所有工作完成時，即移除節點。</span><span class="sxs-lookup"><span data-stu-id="147f0-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="147f0-125">**Retaineddata** -允許正在執行的工作 toocomplete，然後等待所有工作的資料保留週期 tooexpire。</span><span class="sxs-lookup"><span data-stu-id="147f0-125">**Retaineddata** -  Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="147f0-126">等待時不排程任何新的工作。</span><span class="sxs-lookup"><span data-stu-id="147f0-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="147f0-127">當所有工作保留期到期時即移除節點。</span><span class="sxs-lookup"><span data-stu-id="147f0-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="147f0-128">hello 預設值為重新排入佇列。</span><span class="sxs-lookup"><span data-stu-id="147f0-128">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="147f0-129">如果 hello 集區大小增加，則 hello 值會設定太**無效**。</span><span class="sxs-lookup"><span data-stu-id="147f0-129">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="147f0-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="147f0-130">currentDedicated</span></span>|<span data-ttu-id="147f0-131">Int32</span><span class="sxs-lookup"><span data-stu-id="147f0-131">Int32</span></span>|<span data-ttu-id="147f0-132">hello 的運算節點數目目前已指派 toohello 集區。</span><span class="sxs-lookup"><span data-stu-id="147f0-132">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="147f0-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="147f0-133">targetDedicated</span></span>|<span data-ttu-id="147f0-134">Int32</span><span class="sxs-lookup"><span data-stu-id="147f0-134">Int32</span></span>|<span data-ttu-id="147f0-135">hello hello 集區要求的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="147f0-135">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="147f0-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="147f0-136">enableAutoScale</span></span>|<span data-ttu-id="147f0-137">Bool</span><span class="sxs-lookup"><span data-stu-id="147f0-137">Bool</span></span>|<span data-ttu-id="147f0-138">指定是否 hello 集區大小會自動調整一段時間。</span><span class="sxs-lookup"><span data-stu-id="147f0-138">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="147f0-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="147f0-139">isAutoPool</span></span>|<span data-ttu-id="147f0-140">Bool</span><span class="sxs-lookup"><span data-stu-id="147f0-140">Bool</span></span>|<span data-ttu-id="147f0-141">指定是否已透過作業的 AutoPool 機制建立 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="147f0-141">Specifies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="147f0-142">startTime</span><span class="sxs-lookup"><span data-stu-id="147f0-142">startTime</span></span>|<span data-ttu-id="147f0-143">DateTime</span><span class="sxs-lookup"><span data-stu-id="147f0-143">DateTime</span></span>|<span data-ttu-id="147f0-144">啟動 hello hello 集區調整大小的時間。</span><span class="sxs-lookup"><span data-stu-id="147f0-144">hello time hello pool resize started.</span></span>|
|<span data-ttu-id="147f0-145">EndTime</span><span class="sxs-lookup"><span data-stu-id="147f0-145">endTime</span></span>|<span data-ttu-id="147f0-146">DateTime</span><span class="sxs-lookup"><span data-stu-id="147f0-146">DateTime</span></span>|<span data-ttu-id="147f0-147">hello hello 集區調整大小完成的時間。</span><span class="sxs-lookup"><span data-stu-id="147f0-147">hello time hello pool resize completed.</span></span>|
|<span data-ttu-id="147f0-148">ResultCode</span><span class="sxs-lookup"><span data-stu-id="147f0-148">resultCode</span></span>|<span data-ttu-id="147f0-149">String</span><span class="sxs-lookup"><span data-stu-id="147f0-149">String</span></span>|<span data-ttu-id="147f0-150">調整大小的 hello hello 結果。</span><span class="sxs-lookup"><span data-stu-id="147f0-150">hello result of hello resize.</span></span>|
|<span data-ttu-id="147f0-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="147f0-151">resultMessage</span></span>|<span data-ttu-id="147f0-152">String</span><span class="sxs-lookup"><span data-stu-id="147f0-152">String</span></span>|<span data-ttu-id="147f0-153">hello 調整大小錯誤包括 hello 結果的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="147f0-153">hello resize error includes hello details of hello result.</span></span><br /><br /> <span data-ttu-id="147f0-154">如果 hello 調整順利完成它 hello 作業已成功的狀態。</span><span class="sxs-lookup"><span data-stu-id="147f0-154">If hello resize completed successfully it states that hello operation succeeded.</span></span>|
