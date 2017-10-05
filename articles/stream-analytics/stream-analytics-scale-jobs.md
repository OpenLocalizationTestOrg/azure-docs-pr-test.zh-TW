---
title: "調整串流分析工作以增加輸送量 | Microsoft Docs"
description: "了解如何透過設定輸入資料分割、微調查詢定義，及設定工作串流處理單元來調整串流分析工作。"
keywords: "資料串流處理, 串流資料處理, 微調分析"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: ab894976c72ea3785d7f58e51b3dd64511e1e8e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a><span data-ttu-id="b8b1c-104">調整 Azure 串流分析工作，以提高串流資料處理的輸送量</span><span class="sxs-lookup"><span data-stu-id="b8b1c-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span></span>
<span data-ttu-id="b8b1c-105">本文示範如何調整串流分析查詢，以增加串流分析作業的輸送量。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-105">This article shows you how to tune a Stream Analytics query to increase throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="b8b1c-106">您將透過設定輸入分割區、調整分析查詢定義，以及計算和設定作業「串流單位」(SU)，以了解如何調整串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-106">You learn how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a><span data-ttu-id="b8b1c-107">串流分析工作由哪些部分所組成？</span><span class="sxs-lookup"><span data-stu-id="b8b1c-107">What are the parts of a Stream Analytics job?</span></span>
<span data-ttu-id="b8b1c-108">串流分析工作的定義包含輸入、查詢及輸出。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="b8b1c-109">輸入是指作業讀取資料流的來源。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-109">Inputs are where the job reads the data stream from.</span></span> <span data-ttu-id="b8b1c-110">查詢是用來轉換資料輸入資料流，而輸出是作業傳送作業結果的目的地。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-110">The query is used to transform the data input stream, and the output is where the job sends the job results to.</span></span>  

<span data-ttu-id="b8b1c-111">一個工作至少需要一個輸入來源來進行資料串流。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="b8b1c-112">資料流輸入來源可以儲存在 Azure 事件中樞或 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-112">The data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="b8b1c-113">如需詳細資訊，請參閱 [Azure 串流分析簡介](stream-analytics-introduction.md)和[開始使用 Azure 串流分析](stream-analytics-real-time-fraud-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-113">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="b8b1c-114">事件中樞和 Azure 儲存體中的分割區</span><span class="sxs-lookup"><span data-stu-id="b8b1c-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="b8b1c-115">調整串流分析作業需要利用輸入或輸出中的分割區。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-115">Scaling a Stream Analytics job takes advantage of partitions in the input or output.</span></span> <span data-ttu-id="b8b1c-116">資料分割可讓您根據分割索引鍵，將資料分成子集。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="b8b1c-117">取用資料的流程 (例如串流分析作業) 可以平行取用和寫入不同的分割區，這樣可以增加輸送量。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-117">A process that consumes the data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="b8b1c-118">使用串流分析時，您可以利用事件中樞和 Blob 儲存體中的分割區。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="b8b1c-119">如需分割區的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-119">For more information about partitions, see the following articles:</span></span>

* [<span data-ttu-id="b8b1c-120">事件中樞功能概觀</span><span class="sxs-lookup"><span data-stu-id="b8b1c-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="b8b1c-121">資料分割</span><span class="sxs-lookup"><span data-stu-id="b8b1c-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="b8b1c-122">串流單位 (SU)</span><span class="sxs-lookup"><span data-stu-id="b8b1c-122">Streaming units (SUs)</span></span>
<span data-ttu-id="b8b1c-123">串流單位 (SU) 代表執行 Azure 串流分析作業所需的資源和運算能力。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-123">Streaming units (SUs) represent the resources and computing power that are required in order to execute an Azure Stream Analytics job.</span></span> <span data-ttu-id="b8b1c-124">SU 會根據 CPU、記憶體，以及讀寫率的混合量值，提供一個方式來描述相關的事件處理容量。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-124">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="b8b1c-125">每個 SU 相當於大約 1 MB/秒的輸送量。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-125">Each SU corresponds to roughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="b8b1c-126">選擇特定工作所需的 SU 數量，取決於輸入的分割組態和針對作業所定義的查詢。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-126">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and on the query defined for the job.</span></span> <span data-ttu-id="b8b1c-127">您為作業選取的 SU 以您的配額為上限。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-127">You can select up to your quota in SUs for a job.</span></span> <span data-ttu-id="b8b1c-128">根據預設，對於特定區域中的所有分析作業，每個 Azure 訂用帳戶的配額上限為 50 個 SU。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-128">By default, each Azure subscription has a quota of up to 50 SUs for all the analytics jobs in a specific region.</span></span> <span data-ttu-id="b8b1c-129">若要為您的訂用帳戶增加超出此配額的 SU，請連絡 [Microsoft 支援服務](http://support.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-129">To increase SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="b8b1c-130">每個作業有效的 SU 值為 1、3、6 和更大 (以 6 為增量單位)。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="b8b1c-131">窘迫平行作業</span><span class="sxs-lookup"><span data-stu-id="b8b1c-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="b8b1c-132">「窘迫平行」作業是我們在 Azure 串流分析中調整性最高的情節。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-132">An *embarrassingly parallel* job is the most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="b8b1c-133">它將對於查詢執行個體之輸入的某個資料分割，連接到輸出的某個資料分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-133">It connects one partition of the input to one instance of the query to one partition of the output.</span></span> <span data-ttu-id="b8b1c-134">此平行處理原則具有下列需求︰</span><span class="sxs-lookup"><span data-stu-id="b8b1c-134">This parallelism has the following requirements:</span></span>

1. <span data-ttu-id="b8b1c-135">如果查詢邏輯相依於同一個查詢執行個體所處理的相同索引鍵，則您必須確保事件會傳送至輸入的相同分割區。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-135">If your query logic depends on the same key being processed by the same query instance, you must make sure that the events go to the same partition of your input.</span></span> <span data-ttu-id="b8b1c-136">對於事件中樞，這表示事件資料必須設定 **PartitionKey** 值。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-136">For event hubs, this means that the event data must have the **PartitionKey** value set.</span></span> <span data-ttu-id="b8b1c-137">或者，您可以使用分割的傳送者。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="b8b1c-138">對於 Blob 儲存體，這表示事件會傳送至相同的磁碟分割資料夾。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-138">For blob storage, this means that the events are sent to the same partition folder.</span></span> <span data-ttu-id="b8b1c-139">如果查詢邏輯並不需要同一個查詢執行個體所處理的相同索引鍵，您可以忽略這項需求。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-139">If your query logic does not require the same key to be processed by the same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="b8b1c-140">簡單的選取-投影-篩選查詢，即為此邏輯的一個例子。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="b8b1c-141">當資料放在輸入端時，您必須確保查詢已分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-141">Once the data is laid out on the input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="b8b1c-142">所有步驟中都必須使用 **Partition By**。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-142">This requires you to use **Partition By** in all the steps.</span></span> <span data-ttu-id="b8b1c-143">您可以使用多個步驟，但全部都必須依相同的索引鍵來分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-143">Multiple steps are allowed, but they all must be partitioned by the same key.</span></span> <span data-ttu-id="b8b1c-144">目前，資料分割索引鍵必須設定為 **PartitionId**，作業才能完全平行。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-144">Currently, the partitioning key must be set to **PartitionId** in order for the job to be fully parallel.</span></span>  

3. <span data-ttu-id="b8b1c-145">目前，只有事件中樞和 blob 儲存體支援已分割的輸出。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="b8b1c-146">於事件中樞輸出，您必須將分割區索引鍵設定為 **PartitionId**。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-146">For event hub output, you must configure the partition key to be **PartitionId**.</span></span> <span data-ttu-id="b8b1c-147">對於 blob 儲存體輸出，您不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-147">For blob storage output, you don't have to do anything.</span></span>  

4. <span data-ttu-id="b8b1c-148">輸入分割區的數目必須等於輸出分割區的數目。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-148">The number of input partitions must equal the number of output partitions.</span></span> <span data-ttu-id="b8b1c-149">Blob 儲存體輸出目前不支援分割區。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="b8b1c-150">但是沒關係，因為它會繼承上游查詢的資料分割配置。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-150">But that's okay, because it inherits the partitioning scheme of the upstream query.</span></span> <span data-ttu-id="b8b1c-151">以下是允許完全平行作業的分割區值範例：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="b8b1c-152">8 個事件中樞輸入分割區和 8 個事件中樞輸出分割區</span><span class="sxs-lookup"><span data-stu-id="b8b1c-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="b8b1c-153">8 個事件中樞輸入分割區和 blob 儲存體輸出</span><span class="sxs-lookup"><span data-stu-id="b8b1c-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="b8b1c-154">8 個 blob 儲存體輸入分割區和 blob 儲存體輸出</span><span class="sxs-lookup"><span data-stu-id="b8b1c-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="b8b1c-155">8 個 blob 儲存體輸入分割區和 8 個事件中樞輸出分割區</span><span class="sxs-lookup"><span data-stu-id="b8b1c-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="b8b1c-156">以下幾節討論一些窘迫平行的範例情節。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-156">The following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="b8b1c-157">簡單查詢</span><span class="sxs-lookup"><span data-stu-id="b8b1c-157">Simple query</span></span>

* <span data-ttu-id="b8b1c-158">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="b8b1c-159">輸出：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="b8b1c-160">查詢：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="b8b1c-161">此查詢是簡單的篩選。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-161">This query is a simple filter.</span></span> <span data-ttu-id="b8b1c-162">因此，我們不需要擔心將傳送到事件中樞的輸入分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-162">Therefore, we don't need to worry about partitioning the input that is being sent to the event hub.</span></span> <span data-ttu-id="b8b1c-163">請注意，此查詢包含 **Partition By PartitionId**，因此滿足稍早的需求 #2。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-163">Notice that the query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="b8b1c-164">對於輸出，我們必須將作業中的事件中樞輸出設定為讓分割區索引鍵設為 **PartitionId**。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-164">For the output, we need to configure the event hub output in the job to have the parition key set to **PartitionId**.</span></span> <span data-ttu-id="b8b1c-165">最後一項檢查是確保輸入分割區數目等於輸出分割區數目。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-165">One last check is to make sure that the number of input partitions is equal to the number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="b8b1c-166">利用群組索引鍵的查詢</span><span class="sxs-lookup"><span data-stu-id="b8b1c-166">Query with a grouping key</span></span>

* <span data-ttu-id="b8b1c-167">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="b8b1c-168">輸出：Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b8b1c-168">Output: Blob storage</span></span>

<span data-ttu-id="b8b1c-169">查詢：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="b8b1c-170">此查詢含有群組索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-170">This query has a grouping key.</span></span> <span data-ttu-id="b8b1c-171">因此，相同的索引鍵必須由相同的查詢執行個體來處理，這表示事件必須以分割形式傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-171">Therefore, the same key needs to be processed by the same query instance, which means that events must be sent to the event hub in a partitioned manner.</span></span> <span data-ttu-id="b8b1c-172">但是，應該使用哪個索引鍵？</span><span class="sxs-lookup"><span data-stu-id="b8b1c-172">But which key should be used?</span></span> <span data-ttu-id="b8b1c-173">**PartitionId** 是作業邏輯概念。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="b8b1c-174">我們真正關心的索引鍵是 **TollBoothId**，因此，事件資料的 **PartitionKey** 值應該是 **TollBoothId**。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-174">The key we actually care about is **TollBoothId**, so the **PartitionKey** value of the event data should be **TollBoothId**.</span></span> <span data-ttu-id="b8b1c-175">在作法上，我們在查詢中將 **Partition By** 設定為 **PartitionId**。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-175">We do this in the query by setting **Partition By** to **PartitionId**.</span></span> <span data-ttu-id="b8b1c-176">因為輸出是 blob 儲存體，所以我們不需要擔心設定分割區索引鍵值，以滿足需求 #4。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-176">Since the output is blob storage, we don't need to worry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="b8b1c-177">利用群組索引鍵的多重步驟查詢</span><span class="sxs-lookup"><span data-stu-id="b8b1c-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="b8b1c-178">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="b8b1c-179">輸出：具有 8 個分割區的事件中樞執行個體</span><span class="sxs-lookup"><span data-stu-id="b8b1c-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="b8b1c-180">查詢：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="b8b1c-181">這個查詢有群組索引鍵，因此，相同的索引鍵必須由相同的查詢執行個體來處理。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-181">This query has a grouping key, so the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="b8b1c-182">我們可以採用上一個範例中相同的策略。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-182">We can use the same strategy as in the previous example.</span></span> <span data-ttu-id="b8b1c-183">在此案例中，查詢有多個步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-183">In this case, the query has multiple steps.</span></span> <span data-ttu-id="b8b1c-184">每個步驟都有 **Partition By PartitionId** 嗎？</span><span class="sxs-lookup"><span data-stu-id="b8b1c-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="b8b1c-185">是，所以查詢滿足需求 #3。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-185">Yes, so the query fulfills requirement #3.</span></span> <span data-ttu-id="b8b1c-186">對於輸出，我們需要將分割區索引鍵設定為 **PartitionId**，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-186">For the output, we need to set the partition key to **PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="b8b1c-187">我們也可以看到它的分割區數目與輸入的分割區數目相同。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-187">We can also see that it has the same number of partitions as the input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="b8b1c-188">「非」窘迫平行的範例情節</span><span class="sxs-lookup"><span data-stu-id="b8b1c-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="b8b1c-189">在上一節，我們示範一些窘迫平行情節。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-189">In the previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="b8b1c-190">在本節中，我們要討論的情節不符合成為窘迫平行的所有需求。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-190">In this section, we discuss scenarios that don't meet all the requirements to be embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="b8b1c-191">不相符的分割區計數</span><span class="sxs-lookup"><span data-stu-id="b8b1c-191">Mismatched partition count</span></span>
* <span data-ttu-id="b8b1c-192">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="b8b1c-193">輸出：具有 32 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="b8b1c-194">在此案例中，查詢並不重要。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-194">In this case, it doesn't matter what the query is.</span></span> <span data-ttu-id="b8b1c-195">如果輸入分割區計數不符合輸出分割區計數，則拓撲不是窘迫平行。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-195">If the input partition count doesn't match the output partition count, the topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="b8b1c-196">不使用事件中樞或 blob 儲存體作為輸出</span><span class="sxs-lookup"><span data-stu-id="b8b1c-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="b8b1c-197">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="b8b1c-198">輸出：PowerBI</span><span class="sxs-lookup"><span data-stu-id="b8b1c-198">Output: PowerBI</span></span>

<span data-ttu-id="b8b1c-199">PowerBI 輸出目前不支援資料分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="b8b1c-200">因此，此情節不是窘迫平行。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="b8b1c-201">具有不同 Partition By 值的多重步驟查詢</span><span class="sxs-lookup"><span data-stu-id="b8b1c-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="b8b1c-202">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="b8b1c-203">輸出：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="b8b1c-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="b8b1c-204">查詢：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="b8b1c-205">如您所見，第二個步驟把[TollBoothId]  當做資料分割索引鍵來使用。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-205">As you can see, the second step uses **TollBoothId** as the partitioning key.</span></span> <span data-ttu-id="b8b1c-206">此步驟和第一個步驟不同，因此需要變換一下。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-206">This step is not the same as the first step, and it therefore requires us to do a shuffle.</span></span> 

<span data-ttu-id="b8b1c-207">上述範例示範一些符合 (或不符合) 窘迫平行拓撲的串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-207">The preceding examples show some Stream Analytics jobs that conform to (or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="b8b1c-208">如果符合，則可能有最大調整幅度。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-208">If they do conform, they have the potential for maximum scale.</span></span> <span data-ttu-id="b8b1c-209">對於不符合其中一個設定檔的作業，則提供未來更新時的調整指引。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="b8b1c-210">現在，請在下列各節中使用一般指引。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-210">For now, use the general guidance in the following sections.</span></span>

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a><span data-ttu-id="b8b1c-211">計算工作的最大串流處理單元</span><span class="sxs-lookup"><span data-stu-id="b8b1c-211">Calculate the maximum streaming units of a job</span></span>
<span data-ttu-id="b8b1c-212">資料流分析工作可使用的串流處理單元總數，取決於為工作定義之查詢中的步驟數目，和每個步驟的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-212">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="b8b1c-213">查詢中的步驟</span><span class="sxs-lookup"><span data-stu-id="b8b1c-213">Steps in a query</span></span>
<span data-ttu-id="b8b1c-214">一個查詢可以有一或多個步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-214">A query can have one or many steps.</span></span> <span data-ttu-id="b8b1c-215">每個步驟都是使用 **WITH** 關鍵字定義的子查詢。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-215">Each step is a subquery defined by the **WITH** keyword.</span></span> <span data-ttu-id="b8b1c-216">在 **WITH** 關鍵字外的查詢 (只有一個查詢) 也視為一個步驟，例如下列查詢中的 **SELECT** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-216">The query that is outside the **WITH** keyword (one query only) is also counted as a step, such as the **SELECT** statement in the following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="b8b1c-217">此查詢有兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="b8b1c-218">本文稍後會詳細討論此查詢。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-218">This query is discussed in more detail later in the article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="b8b1c-219">分割步驟</span><span class="sxs-lookup"><span data-stu-id="b8b1c-219">Partition a step</span></span>
<span data-ttu-id="b8b1c-220">要分割步驟必須符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-220">Partitioning a step requires the following conditions:</span></span>

* <span data-ttu-id="b8b1c-221">必須分割輸入來源。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-221">The input source must be partitioned.</span></span> 
* <span data-ttu-id="b8b1c-222">查詢的 **SELECT** 陳述式必須讀取某個已分割的輸入來源。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-222">The **SELECT** statement of the query must read from a partitioned input source.</span></span>
* <span data-ttu-id="b8b1c-223">步驟內的查詢必須有 **Partition By** 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-223">The query within the step must have the **Partition By** keyword.</span></span>

<span data-ttu-id="b8b1c-224">分割查詢時，將會在個別的分割區群組中處理和彙總輸入事件，然後為每個群組產生輸出事件。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-224">When a query is partitioned, the input events are processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span></span> <span data-ttu-id="b8b1c-225">如果需要合併的彙總，您必須建立第二個非分割步驟來彙總。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-225">If you want a combined aggregate, you must create a second non-partitioned step to aggregate.</span></span>

### <a name="calculate-the-max-streaming-units-for-a-job"></a><span data-ttu-id="b8b1c-226">計算工作的最大串流處理單元</span><span class="sxs-lookup"><span data-stu-id="b8b1c-226">Calculate the max streaming units for a job</span></span>
<span data-ttu-id="b8b1c-227">所有非分割步驟合起來，可將串流分析作業調整為最多 6 個串流單元 (SU)。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-227">All non-partitioned steps together can scale up to six streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="b8b1c-228">若要新增 SU，必須分割步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-228">To add SUs, a step must be partitioned.</span></span> <span data-ttu-id="b8b1c-229">每個分割區可以有 6 個 SU。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="b8b1c-230">查詢</span><span class="sxs-lookup"><span data-stu-id="b8b1c-230">Query</span></span></th><th><span data-ttu-id="b8b1c-231">作業的最多 SU</span><span class="sxs-lookup"><span data-stu-id="b8b1c-231">Max SUs for the job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="b8b1c-232">查詢包含一個步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-232">The query contains one step.</span></span></li>
<li><span data-ttu-id="b8b1c-233">步驟未分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-233">The step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="b8b1c-234">6</span><span class="sxs-lookup"><span data-stu-id="b8b1c-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="b8b1c-235">輸入資料流分割時會除以 3。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-235">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="b8b1c-236">查詢包含一個步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-236">The query contains one step.</span></span></li>
<li><span data-ttu-id="b8b1c-237">步驟進行分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-237">The step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="b8b1c-238">18</span><span class="sxs-lookup"><span data-stu-id="b8b1c-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="b8b1c-239">查詢包含兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-239">The query contains two steps.</span></span></li>
<li><span data-ttu-id="b8b1c-240">兩個步驟都不會分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-240">Neither of the steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="b8b1c-241">6</span><span class="sxs-lookup"><span data-stu-id="b8b1c-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="b8b1c-242">輸入資料流分割時會除以 3。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-242">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="b8b1c-243">查詢包含兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-243">The query contains two steps.</span></span> <span data-ttu-id="b8b1c-244">輸入步驟會分割，而第二個步驟則否。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-244">The input step is partitioned and the second step is not.</span></span></li>
<li><span data-ttu-id="b8b1c-245"><strong>SELECT</strong> 陳述式會讀取分割的輸入。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-245">The <strong>SELECT</strong> statement reads from the partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="b8b1c-246">24 (18 個用於分割的步驟 + 6 個用於非分割的步驟)</span><span class="sxs-lookup"><span data-stu-id="b8b1c-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="b8b1c-247">調整的範例</span><span class="sxs-lookup"><span data-stu-id="b8b1c-247">Examples of scaling</span></span>

<span data-ttu-id="b8b1c-248">下列查詢會計算三分鐘內通過收費站 (有三個收費亭) 的車流量。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-248">The following query calculates the number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="b8b1c-249">此查詢可以調整為最多 6 個 SU。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-249">This query can be scaled up to six SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="b8b1c-250">若要讓查詢使用更多 SU，輸入資料流和查詢都必須分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-250">To use more SUs for the query, both the input data stream and the query must be partitioned.</span></span> <span data-ttu-id="b8b1c-251">因為資料流分割區設為 3，以下修改的查詢可以調整為最多 18 個 SU：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-251">Since the data stream partition is set to 3, the following modified query can be scaled up to 18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="b8b1c-252">分割查詢時將會處理輸入事件並將其彙總在個別的資料分割群組中。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-252">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="b8b1c-253">也會為每個群組產生輸出事件。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-253">Output events are also generated for each of the groups.</span></span> <span data-ttu-id="b8b1c-254">當 **GROUP BY** 欄位不是輸入資料流中的分割區索引鍵時，資料分割可能會導致某些非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-254">Partitioning can cause some unexpected results when the **GROUP BY** field is not the partition key in the input data stream.</span></span> <span data-ttu-id="b8b1c-255">例如，上一個查詢中的 **TollBoothId** 欄位不是 **Input1** 的分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-255">For example, the **TollBoothId** field in the previous query is not the partition key of **Input1**.</span></span> <span data-ttu-id="b8b1c-256">結果是收費亭 #1 的資料可能分散在多個分割區。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-256">The result is that the data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="b8b1c-257">串流分析會個別處理每個 **Input1** 分割區。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-257">Each of the **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="b8b1c-258">因此，在相同的輪轉視窗中，相同收費亭的汽車計數會建立多筆記錄。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-258">As a result, multiple records of the car count for the same tollbooth in the same Tumbling window will be created.</span></span> <span data-ttu-id="b8b1c-259">如果輸入分割區索引鍵無法變更，可藉由新增非分割步驟來解決此問題，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-259">If the input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in the following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="b8b1c-260">此查詢可以調整為 24 個 SU。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-260">This query can be scaled to 24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="b8b1c-261">如果您要聯結兩個資料流，請確定以您用來建立聯結的資料行的分割區索引鍵來分割資料流。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-261">If you are joining two streams, make sure that the streams are partitioned by the partition key of the column that you use to create the joins.</span></span> <span data-ttu-id="b8b1c-262">也請確定兩個資料流中的分割區數目相同。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-262">Also make sure that you have the same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="b8b1c-263">設定串流分析串流單位</span><span class="sxs-lookup"><span data-stu-id="b8b1c-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="b8b1c-264">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-264">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8b1c-265">在資源清單中，尋找並開啟您想要調整的串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-265">In the list of resources, find the Stream Analytics job that you want to scale and then open it.</span></span>
3. <span data-ttu-id="b8b1c-266">在作業刀鋒視窗中，按一下 [設定] 底下的 [調整]。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-266">In the job blade, under **Configure**, click **Scale**.</span></span>

    ![Azure 入口網站串流分析作業組態][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="b8b1c-268">使用滑桿來設定作業的 SU。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-268">Use the slider to set the SUs for the job.</span></span> <span data-ttu-id="b8b1c-269">請注意，您只能調整特定的 SU 設定。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-269">Notice that you are limited to specific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="b8b1c-270">監視工作效能</span><span class="sxs-lookup"><span data-stu-id="b8b1c-270">Monitor job performance</span></span>
<span data-ttu-id="b8b1c-271">您可以使用 Azure 入口網站來追蹤作業的輸送量：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-271">Using the Azure portal, you can track the throughput of a job:</span></span>

![Azure 串流分析監視工作][img.stream.analytics.monitor.job]

<span data-ttu-id="b8b1c-273">計算工作負載的預期輸送量。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-273">Calculate the expected throughput of the workload.</span></span> <span data-ttu-id="b8b1c-274">如果輸送量少於預期，請調整輸入分割區、調整查詢，並將 SU 新增至作業。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-274">If the throughput is less than expected, tune the input partition, tune the query, and add SUs to your job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-the-raspberry-pi-scenario"></a><span data-ttu-id="b8b1c-275">視覺化大規模串流分析輸送量：Raspberry Pi 情節</span><span class="sxs-lookup"><span data-stu-id="b8b1c-275">Visualize Stream Analytics throughput at scale: the Raspberry Pi scenario</span></span>
<span data-ttu-id="b8b1c-276">為了協助您了解串流分析作業如何調整，我們已根據來自 Raspberry Pi 裝置的輸入完成一項實驗。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-276">To help you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="b8b1c-277">此實驗讓我們看到對多個串流單位和分割區的輸送量造成的影響。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-277">This experiment let us see the effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="b8b1c-278">在此情節中，裝置會將感應器資料 (用戶端) 傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-278">In this scenario, the device sends sensor data (clients) to an event hub.</span></span> <span data-ttu-id="b8b1c-279">串流分析會處理資料，並將警示或統計資料當作輸出傳送到另一個事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-279">Streaming Analytics processes the data and sends an alert or statistics as an output to another event hub.</span></span> 

<span data-ttu-id="b8b1c-280">用戶端會以 JSON 格式傳送感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-280">The client sends sensor data in JSON format.</span></span> <span data-ttu-id="b8b1c-281">資料輸出也是 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-281">The data output is also in JSON format.</span></span> <span data-ttu-id="b8b1c-282">資料如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-282">The data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="b8b1c-283">下列查詢用於關閉燈光開關時傳送警示：</span><span class="sxs-lookup"><span data-stu-id="b8b1c-283">The following query is used to send an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="b8b1c-284">測量輸送量</span><span class="sxs-lookup"><span data-stu-id="b8b1c-284">Measure throughput</span></span>

<span data-ttu-id="b8b1c-285">在此案例中，輸送量是串流分析在固定時間內處理的輸入資料量。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-285">In this context, throughput is the amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="b8b1c-286">(我們測量 10 分鐘。)為了以最佳方式處理輸入資料的輸送量，資料流輸入和查詢都必須分割。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-286">(We measured for 10 minutes.) To achieve the best processing throughput for the input data, both the data stream input and the query were  partitioned.</span></span> <span data-ttu-id="b8b1c-287">我們在查詢中包含 **COUNT()** 來測量已處理的輸入事件數目。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-287">We included **COUNT()** in the query to measure how many input events were processed.</span></span> <span data-ttu-id="b8b1c-288">為了確保作業不會單純地等待輸入事件到來，輸入事件中樞的每個分割區都已預先載入大約 300 MB 的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-288">To make sure the job was not simply waiting for input events to come, each partition of the input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="b8b1c-289">下表顯示我們在增加串流單位數目時所看到的結果，以及事件中樞裡對應的分割區計數。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-289">The following table shows the results we saw when we increased the number of streaming units and the corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="b8b1c-290">輸入資料分割</span><span class="sxs-lookup"><span data-stu-id="b8b1c-290">Input Partitions</span></span></th><th><span data-ttu-id="b8b1c-291">輸出資料分割</span><span class="sxs-lookup"><span data-stu-id="b8b1c-291">Output Partitions</span></span></th><th><span data-ttu-id="b8b1c-292">串流處理單位</span><span class="sxs-lookup"><span data-stu-id="b8b1c-292">Streaming Units</span></span></th><th><span data-ttu-id="b8b1c-293">持續的輸送量</span><span class="sxs-lookup"><span data-stu-id="b8b1c-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="b8b1c-294">12</span><span class="sxs-lookup"><span data-stu-id="b8b1c-294">12</span></span></td>
<td><span data-ttu-id="b8b1c-295">12</span><span class="sxs-lookup"><span data-stu-id="b8b1c-295">12</span></span></td>
<td><span data-ttu-id="b8b1c-296">6</span><span class="sxs-lookup"><span data-stu-id="b8b1c-296">6</span></span></td>
<td><span data-ttu-id="b8b1c-297">4.06 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8b1c-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="b8b1c-298">12</span><span class="sxs-lookup"><span data-stu-id="b8b1c-298">12</span></span></td>
<td><span data-ttu-id="b8b1c-299">12</span><span class="sxs-lookup"><span data-stu-id="b8b1c-299">12</span></span></td>
<td><span data-ttu-id="b8b1c-300">12</span><span class="sxs-lookup"><span data-stu-id="b8b1c-300">12</span></span></td>
<td><span data-ttu-id="b8b1c-301">8.06 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8b1c-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="b8b1c-302">48</span><span class="sxs-lookup"><span data-stu-id="b8b1c-302">48</span></span></td>
<td><span data-ttu-id="b8b1c-303">48</span><span class="sxs-lookup"><span data-stu-id="b8b1c-303">48</span></span></td>
<td><span data-ttu-id="b8b1c-304">48</span><span class="sxs-lookup"><span data-stu-id="b8b1c-304">48</span></span></td>
<td><span data-ttu-id="b8b1c-305">38.32 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8b1c-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="b8b1c-306">192</span><span class="sxs-lookup"><span data-stu-id="b8b1c-306">192</span></span></td>
<td><span data-ttu-id="b8b1c-307">192</span><span class="sxs-lookup"><span data-stu-id="b8b1c-307">192</span></span></td>
<td><span data-ttu-id="b8b1c-308">192</span><span class="sxs-lookup"><span data-stu-id="b8b1c-308">192</span></span></td>
<td><span data-ttu-id="b8b1c-309">172.67 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8b1c-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="b8b1c-310">480</span><span class="sxs-lookup"><span data-stu-id="b8b1c-310">480</span></span></td>
<td><span data-ttu-id="b8b1c-311">480</span><span class="sxs-lookup"><span data-stu-id="b8b1c-311">480</span></span></td>
<td><span data-ttu-id="b8b1c-312">480</span><span class="sxs-lookup"><span data-stu-id="b8b1c-312">480</span></span></td>
<td><span data-ttu-id="b8b1c-313">454.27 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8b1c-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="b8b1c-314">720</span><span class="sxs-lookup"><span data-stu-id="b8b1c-314">720</span></span></td>
<td><span data-ttu-id="b8b1c-315">720</span><span class="sxs-lookup"><span data-stu-id="b8b1c-315">720</span></span></td>
<td><span data-ttu-id="b8b1c-316">720</span><span class="sxs-lookup"><span data-stu-id="b8b1c-316">720</span></span></td>
<td><span data-ttu-id="b8b1c-317">609.69 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8b1c-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="b8b1c-318">下圖顯示 SU 和輸送量之間的關聯性視覺效果。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-318">And the following graph shows a visualization of the relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="b8b1c-320">取得說明</span><span class="sxs-lookup"><span data-stu-id="b8b1c-320">Get help</span></span>
<span data-ttu-id="b8b1c-321">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="b8b1c-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8b1c-322">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8b1c-322">Next steps</span></span>
* [<span data-ttu-id="b8b1c-323">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="b8b1c-323">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b8b1c-324">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b8b1c-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b8b1c-325">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="b8b1c-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b8b1c-326">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="b8b1c-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

