---
title: "aaaScale 資料流分析工作 tooincrease 輸送量 |Microsoft 文件"
description: "了解如何 tooscale 串流分析工作，藉由設定輸入資料分割、 微調 hello 查詢定義，並設定工作資料流處理單位。"
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
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="f09cf-104">向 Azure Stream Analytics 工作 tooincrease 資料流資料處理輸送量</span><span class="sxs-lookup"><span data-stu-id="f09cf-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="f09cf-105">本文章將示範如何 tootune 資料流分析查詢的資料流分析工作的 tooincrease 輸送量。</span><span class="sxs-lookup"><span data-stu-id="f09cf-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="f09cf-106">您將學習如何 tooscale 資料流分析工作設定輸入資料分割、 微調 hello 分析查詢定義，和計算，並設定工作*串流單位*(SUs)。</span><span class="sxs-lookup"><span data-stu-id="f09cf-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="f09cf-107">資料流分析工作的 hello 部分有哪些？</span><span class="sxs-lookup"><span data-stu-id="f09cf-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="f09cf-108">串流分析工作的定義包含輸入、查詢及輸出。</span><span class="sxs-lookup"><span data-stu-id="f09cf-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="f09cf-109">輸入如下： hello 工作位置讀取從 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="f09cf-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="f09cf-110">hello 查詢是使用的 tootransform hello 資料輸入資料流，而 hello 輸出其中 hello 作業會傳送 hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="f09cf-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="f09cf-111">一個工作至少需要一個輸入來源來進行資料串流。</span><span class="sxs-lookup"><span data-stu-id="f09cf-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="f09cf-112">hello 資料流輸入的來源可以儲存在 Azure 事件中心或 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="f09cf-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="f09cf-113">如需詳細資訊，請參閱[簡介 tooAzure Stream Analytics](stream-analytics-introduction.md)和[開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="f09cf-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="f09cf-114">事件中樞和 Azure 儲存體中的分割區</span><span class="sxs-lookup"><span data-stu-id="f09cf-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="f09cf-115">調整資料流分析工作 hello 輸入或輸出中會利用資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="f09cf-116">資料分割可讓您根據分割索引鍵，將資料分成子集。</span><span class="sxs-lookup"><span data-stu-id="f09cf-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="f09cf-117">取用 hello 資料 （例如資料流分析工作） 的處理序可以使用和寫入不同資料分割，以平行方式，會增加輸送量。</span><span class="sxs-lookup"><span data-stu-id="f09cf-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="f09cf-118">使用串流分析時，您可以利用事件中樞和 Blob 儲存體中的分割區。</span><span class="sxs-lookup"><span data-stu-id="f09cf-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="f09cf-119">如需有關資料分割的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="f09cf-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="f09cf-120">事件中樞功能概觀</span><span class="sxs-lookup"><span data-stu-id="f09cf-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="f09cf-121">資料分割</span><span class="sxs-lookup"><span data-stu-id="f09cf-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="f09cf-122">串流單位 (SU)</span><span class="sxs-lookup"><span data-stu-id="f09cf-122">Streaming units (SUs)</span></span>
<span data-ttu-id="f09cf-123">資料流單位 (SUs) 代表 hello 資源且運算能力所需的順序 tooexecute Azure Stream Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="f09cf-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="f09cf-124">SUs 提供方式 toodescribe hello 相對事件處理為基礎的混合測量結果的 CPU、 記憶體容量和讀寫率。</span><span class="sxs-lookup"><span data-stu-id="f09cf-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="f09cf-125">每個 SU 對應 tooroughly 1 MB/秒的輸送量。</span><span class="sxs-lookup"><span data-stu-id="f09cf-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="f09cf-126">選擇多少 SUs 所需的特定作業取決於 hello 輸入 hello 磁碟分割設定以及 hello 工作所定義的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="f09cf-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="f09cf-127">您可以選取工作 SUs tooyour 配額。</span><span class="sxs-lookup"><span data-stu-id="f09cf-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="f09cf-128">根據預設，每個 Azure 訂用帳戶會在特定地區有向上 too50 SUs 所有 hello 分析作業的配額。</span><span class="sxs-lookup"><span data-stu-id="f09cf-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="f09cf-129">超過這個配額影響，請連絡訂用帳戶的 tooincrease SUs [Microsoft 支援服務](http://support.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="f09cf-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="f09cf-130">每個作業有效的 SU 值為 1、3、6 和更大 (以 6 為增量單位)。</span><span class="sxs-lookup"><span data-stu-id="f09cf-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="f09cf-131">窘迫平行作業</span><span class="sxs-lookup"><span data-stu-id="f09cf-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="f09cf-132">*平行*作業是 hello 擴充性最高的案例，我們已在 Azure Stream Analytics。</span><span class="sxs-lookup"><span data-stu-id="f09cf-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="f09cf-133">它會連接一個磁碟分割的 hello 輸入的 tooone hello 查詢 tooone 磁碟分割的 hello 輸出執行個體。</span><span class="sxs-lookup"><span data-stu-id="f09cf-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="f09cf-134">此平行處理原則具有下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f09cf-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="f09cf-135">如果您的查詢邏輯取決於相同金鑰所處理的 hello hello 相同查詢執行個體，您必須確定 hello 事件移 toohello 您輸入的相同資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="f09cf-136">對於事件中心，這表示 hello 事件資料必須擁有 hello **PartitionKey**值的設定。</span><span class="sxs-lookup"><span data-stu-id="f09cf-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="f09cf-137">或者，您可以使用分割的傳送者。</span><span class="sxs-lookup"><span data-stu-id="f09cf-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="f09cf-138">Blob 儲存體，這表示，傳送嗨事件 toohello 相同的磁碟分割資料夾。</span><span class="sxs-lookup"><span data-stu-id="f09cf-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="f09cf-139">如果您的查詢邏輯不需要相同索引鍵 toobe 處理的 hello hello 相同查詢執行個體，您可以忽略這項需求。</span><span class="sxs-lookup"><span data-stu-id="f09cf-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="f09cf-140">簡單的選取-投影-篩選查詢，即為此邏輯的一個例子。</span><span class="sxs-lookup"><span data-stu-id="f09cf-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="f09cf-141">一旦 hello 資料配置在 hello 輸入端上，您必須確定您的查詢資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="f09cf-142">這需要 toouse **Partition By**中所有的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="f09cf-143">允許多個步驟，但它們都必須由 hello 分割成相同的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f09cf-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="f09cf-144">目前，資料分割索引鍵的 hello 必須設定太**PartitionId** hello 作業 toobe 完全平行的順序。</span><span class="sxs-lookup"><span data-stu-id="f09cf-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="f09cf-145">目前，只有事件中樞和 blob 儲存體支援已分割的輸出。</span><span class="sxs-lookup"><span data-stu-id="f09cf-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="f09cf-146">事件中樞輸出中，您必須設定 hello 資料分割索引鍵 toobe **PartitionId**。</span><span class="sxs-lookup"><span data-stu-id="f09cf-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="f09cf-147">針對 blob 儲存體的輸出，您不需要 toodo 任何項目。</span><span class="sxs-lookup"><span data-stu-id="f09cf-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="f09cf-148">hello 輸入的資料分割數目必須等於輸出資料分割的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="f09cf-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="f09cf-149">Blob 儲存體輸出目前不支援分割區。</span><span class="sxs-lookup"><span data-stu-id="f09cf-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="f09cf-150">但是沒關係，因為它繼承 hello 分割 hello 上游查詢的配置。</span><span class="sxs-lookup"><span data-stu-id="f09cf-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="f09cf-151">以下是允許完全平行作業的分割區值範例：</span><span class="sxs-lookup"><span data-stu-id="f09cf-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="f09cf-152">8 個事件中樞輸入分割區和 8 個事件中樞輸出分割區</span><span class="sxs-lookup"><span data-stu-id="f09cf-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="f09cf-153">8 個事件中樞輸入分割區和 blob 儲存體輸出</span><span class="sxs-lookup"><span data-stu-id="f09cf-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="f09cf-154">8 個 blob 儲存體輸入分割區和 blob 儲存體輸出</span><span class="sxs-lookup"><span data-stu-id="f09cf-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="f09cf-155">8 個 blob 儲存體輸入分割區和 8 個事件中樞輸出分割區</span><span class="sxs-lookup"><span data-stu-id="f09cf-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="f09cf-156">hello 下列各節討論是窘迫平行的一些範例案例。</span><span class="sxs-lookup"><span data-stu-id="f09cf-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="f09cf-157">簡單查詢</span><span class="sxs-lookup"><span data-stu-id="f09cf-157">Simple query</span></span>

* <span data-ttu-id="f09cf-158">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f09cf-159">輸出：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="f09cf-160">查詢：</span><span class="sxs-lookup"><span data-stu-id="f09cf-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="f09cf-161">此查詢是簡單的篩選。</span><span class="sxs-lookup"><span data-stu-id="f09cf-161">This query is a simple filter.</span></span> <span data-ttu-id="f09cf-162">因此，我們不需要有關資料分割正在傳送 toohello 事件中心的 hello 輸入 tooworry。</span><span class="sxs-lookup"><span data-stu-id="f09cf-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="f09cf-163">請注意該 hello 查詢包含**由 PartitionId 分割**，因此它可滿足需求 #2 與前面。</span><span class="sxs-lookup"><span data-stu-id="f09cf-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="f09cf-164">Hello 輸出中，我們需要 tooconfigure hello 事件中樞輸出中 hello 作業 toohave hello 資料分割索引鍵集太**PartitionId**。</span><span class="sxs-lookup"><span data-stu-id="f09cf-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="f09cf-165">一次的最後一個檢查是 toomake 確定 hello 輸入的資料分割數目等於 toohello 輸出資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="f09cf-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="f09cf-166">利用群組索引鍵的查詢</span><span class="sxs-lookup"><span data-stu-id="f09cf-166">Query with a grouping key</span></span>

* <span data-ttu-id="f09cf-167">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f09cf-168">輸出：Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="f09cf-168">Output: Blob storage</span></span>

<span data-ttu-id="f09cf-169">查詢：</span><span class="sxs-lookup"><span data-stu-id="f09cf-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="f09cf-170">此查詢含有群組索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f09cf-170">This query has a grouping key.</span></span> <span data-ttu-id="f09cf-171">因此，hello 相同索引鍵需求 toobe hello 同樣的查詢執行個體，這表示，事件必須傳送 toohello 事件中樞分割區的方式處理。</span><span class="sxs-lookup"><span data-stu-id="f09cf-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="f09cf-172">但是，應該使用哪個索引鍵？</span><span class="sxs-lookup"><span data-stu-id="f09cf-172">But which key should be used?</span></span> <span data-ttu-id="f09cf-173">**PartitionId** 是作業邏輯概念。</span><span class="sxs-lookup"><span data-stu-id="f09cf-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="f09cf-174">我們實際上關心的 hello 索引鍵是**TollBoothId**，因此 hello **PartitionKey** hello 事件資料的值應該是**TollBoothId**。</span><span class="sxs-lookup"><span data-stu-id="f09cf-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="f09cf-175">我們可以在 hello 查詢設定**Partition By**太**PartitionId**。</span><span class="sxs-lookup"><span data-stu-id="f09cf-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="f09cf-176">由於 hello 輸出 blob 儲存體，我們不需要有關設定資料分割索引鍵值，根據需求 #4 tooworry。</span><span class="sxs-lookup"><span data-stu-id="f09cf-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="f09cf-177">利用群組索引鍵的多重步驟查詢</span><span class="sxs-lookup"><span data-stu-id="f09cf-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="f09cf-178">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f09cf-179">輸出：具有 8 個分割區的事件中樞執行個體</span><span class="sxs-lookup"><span data-stu-id="f09cf-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="f09cf-180">查詢：</span><span class="sxs-lookup"><span data-stu-id="f09cf-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="f09cf-181">此查詢的群組索引鍵，因此 hello hello 所處理的相同索引鍵需求 toobe 相同的查詢執行個體。</span><span class="sxs-lookup"><span data-stu-id="f09cf-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="f09cf-182">我們可以使用 hello 同樣的策略，如同 hello 先前的範例。</span><span class="sxs-lookup"><span data-stu-id="f09cf-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="f09cf-183">在此情況下，hello 查詢有多個步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="f09cf-184">每個步驟都有 **Partition By PartitionId** 嗎？</span><span class="sxs-lookup"><span data-stu-id="f09cf-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="f09cf-185">是的所以 hello 查詢可滿足需求 #3。</span><span class="sxs-lookup"><span data-stu-id="f09cf-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="f09cf-186">Hello 輸出中，我們需要 tooset hello 資料分割索引鍵太**PartitionId**，如同先前討論一般。</span><span class="sxs-lookup"><span data-stu-id="f09cf-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="f09cf-187">我們也可以查看有 hello 相同數目的資料分割，做為輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="f09cf-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="f09cf-188">「非」窘迫平行的範例情節</span><span class="sxs-lookup"><span data-stu-id="f09cf-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="f09cf-189">Hello 前一節，我們也示範了一些平行的案例。</span><span class="sxs-lookup"><span data-stu-id="f09cf-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="f09cf-190">在本節中，我們會討論不符合所有 hello 需求 toobe 平行的案例。</span><span class="sxs-lookup"><span data-stu-id="f09cf-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="f09cf-191">不相符的分割區計數</span><span class="sxs-lookup"><span data-stu-id="f09cf-191">Mismatched partition count</span></span>
* <span data-ttu-id="f09cf-192">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f09cf-193">輸出：具有 32 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="f09cf-194">在此情況下，不論是哪一個 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="f09cf-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="f09cf-195">如果 hello 輸入的資料分割計數不符合 hello 輸出資料分割計數，不是平行 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="f09cf-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="f09cf-196">不使用事件中樞或 blob 儲存體作為輸出</span><span class="sxs-lookup"><span data-stu-id="f09cf-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="f09cf-197">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f09cf-198">輸出：PowerBI</span><span class="sxs-lookup"><span data-stu-id="f09cf-198">Output: PowerBI</span></span>

<span data-ttu-id="f09cf-199">PowerBI 輸出目前不支援資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="f09cf-200">因此，此情節不是窘迫平行。</span><span class="sxs-lookup"><span data-stu-id="f09cf-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="f09cf-201">具有不同 Partition By 值的多重步驟查詢</span><span class="sxs-lookup"><span data-stu-id="f09cf-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="f09cf-202">輸入：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f09cf-203">輸出：具有 8 個分割區的事件中樞</span><span class="sxs-lookup"><span data-stu-id="f09cf-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="f09cf-204">查詢：</span><span class="sxs-lookup"><span data-stu-id="f09cf-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="f09cf-205">如您所見，會使用第二個步驟的 hello **TollBoothId**為 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f09cf-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="f09cf-206">這個步驟不是 hello 相同 hello 第一個步驟，並因此我們必須 toodo 隨機播放。</span><span class="sxs-lookup"><span data-stu-id="f09cf-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="f09cf-207">hello 前面的範例會顯示某些資料流分析工作太符合 （或不要） 平行的拓撲。</span><span class="sxs-lookup"><span data-stu-id="f09cf-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="f09cf-208">如果它們符合執行，也會具有 hello 可能會達到最大效能。</span><span class="sxs-lookup"><span data-stu-id="f09cf-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="f09cf-209">對於不符合其中一個設定檔的作業，則提供未來更新時的調整指引。</span><span class="sxs-lookup"><span data-stu-id="f09cf-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="f09cf-210">現在，請在 hello 下列各節中使用 hello 一般指引。</span><span class="sxs-lookup"><span data-stu-id="f09cf-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="f09cf-211">計算 hello 最大資料流處理單位作業</span><span class="sxs-lookup"><span data-stu-id="f09cf-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="f09cf-212">可供資料流分析工作的資料流處理單位的 hello 總數取決於 hello hello hello 作業與 hello 資料分割數目的每個步驟所定義的查詢中的步驟數目。</span><span class="sxs-lookup"><span data-stu-id="f09cf-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="f09cf-213">查詢中的步驟</span><span class="sxs-lookup"><span data-stu-id="f09cf-213">Steps in a query</span></span>
<span data-ttu-id="f09cf-214">一個查詢可以有一或多個步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-214">A query can have one or many steps.</span></span> <span data-ttu-id="f09cf-215">每個步驟都 hello 所定義的子查詢**WITH**關鍵字。</span><span class="sxs-lookup"><span data-stu-id="f09cf-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="f09cf-216">hello 查詢超出 hello **WITH**關鍵字 （僅一個查詢） 也會列入步驟中，例如 hello**選取**hello 下列查詢中的陳述式：</span><span class="sxs-lookup"><span data-stu-id="f09cf-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="f09cf-217">此查詢有兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="f09cf-218">此查詢在 hello 文件中稍後詳細討論。</span><span class="sxs-lookup"><span data-stu-id="f09cf-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="f09cf-219">分割步驟</span><span class="sxs-lookup"><span data-stu-id="f09cf-219">Partition a step</span></span>
<span data-ttu-id="f09cf-220">分割步驟需要下列條件的 hello:</span><span class="sxs-lookup"><span data-stu-id="f09cf-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="f09cf-221">必須分割 hello 輸入的來源。</span><span class="sxs-lookup"><span data-stu-id="f09cf-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="f09cf-222">hello**選取**hello 查詢的陳述式必須從資料分割的輸入來源讀取。</span><span class="sxs-lookup"><span data-stu-id="f09cf-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="f09cf-223">hello 步驟內的 hello 查詢都必須有 hello **Partition By**關鍵字。</span><span class="sxs-lookup"><span data-stu-id="f09cf-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="f09cf-224">當查詢資料分割時，hello 輸入的事件處理和彙總中的個別資料分割群組，而且不會產生輸出事件的每個 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="f09cf-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="f09cf-225">如果您想結合彙總，您必須建立第二個的非資料分割步驟 tooaggregate。</span><span class="sxs-lookup"><span data-stu-id="f09cf-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="f09cf-226">計算 hello 串流工作單位的最大值</span><span class="sxs-lookup"><span data-stu-id="f09cf-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="f09cf-227">非資料分割的所有步驟一起就能都相應 toosix 串流單位 (SUs) 的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="f09cf-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="f09cf-228">必須分割 tooadd SUs，步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="f09cf-229">每個分割區可以有 6 個 SU。</span><span class="sxs-lookup"><span data-stu-id="f09cf-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="f09cf-230">查詢</span><span class="sxs-lookup"><span data-stu-id="f09cf-230">Query</span></span></th><th><span data-ttu-id="f09cf-231">Hello 作業的最大 SUs</span><span class="sxs-lookup"><span data-stu-id="f09cf-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="f09cf-232">hello 查詢包含一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="f09cf-233">hello 步驟不是資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="f09cf-234">6</span><span class="sxs-lookup"><span data-stu-id="f09cf-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="f09cf-235">hello 輸入的資料流分割 3。</span><span class="sxs-lookup"><span data-stu-id="f09cf-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="f09cf-236">hello 查詢包含一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="f09cf-237">hello 步驟已分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="f09cf-238">18</span><span class="sxs-lookup"><span data-stu-id="f09cf-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="f09cf-239">hello 查詢包含兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="f09cf-240">Hello 步驟都不會分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="f09cf-241">6</span><span class="sxs-lookup"><span data-stu-id="f09cf-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="f09cf-242">hello 輸入的資料流分割 3。</span><span class="sxs-lookup"><span data-stu-id="f09cf-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="f09cf-243">hello 查詢包含兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-243">hello query contains two steps.</span></span> <span data-ttu-id="f09cf-244">hello 輸入的步驟已分割，而且不 hello 第二個步驟。</span><span class="sxs-lookup"><span data-stu-id="f09cf-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="f09cf-245">hello<strong>選取</strong>陳述式會從資料分割的 hello 輸入讀取。</span><span class="sxs-lookup"><span data-stu-id="f09cf-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="f09cf-246">24 (18 個用於分割的步驟 + 6 個用於非分割的步驟)</span><span class="sxs-lookup"><span data-stu-id="f09cf-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="f09cf-247">調整的範例</span><span class="sxs-lookup"><span data-stu-id="f09cf-247">Examples of scaling</span></span>

<span data-ttu-id="f09cf-248">hello 下列查詢會計算 hello 透過付費站台具有三個 tollbooths 在 3 分鐘期間內的汽車數。</span><span class="sxs-lookup"><span data-stu-id="f09cf-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="f09cf-249">此查詢可以 toosix SUs 向上調整。</span><span class="sxs-lookup"><span data-stu-id="f09cf-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="f09cf-250">多個 toouse SUs 的 hello 查詢、 同時 hello 輸入的資料流和 hello 查詢必須分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="f09cf-251">因為 hello 資料資料流資料分割設定 too3，hello 下列修改過的查詢可以延伸 too18 SUs:</span><span class="sxs-lookup"><span data-stu-id="f09cf-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="f09cf-252">查詢資料分割，會 hello 輸入的事件處理和個別分割區群組中的彙總資料。</span><span class="sxs-lookup"><span data-stu-id="f09cf-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="f09cf-253">每個 hello 群組，也會產生輸出事件。</span><span class="sxs-lookup"><span data-stu-id="f09cf-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="f09cf-254">資料分割可能會導致一些意外的結果時 hello **GROUP BY**欄位不是 hello hello 輸入的資料流中的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f09cf-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="f09cf-255">例如，hello **TollBoothId** hello 先前查詢中的欄位不是 hello 資料分割索引鍵**Input1**。</span><span class="sxs-lookup"><span data-stu-id="f09cf-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="f09cf-256">hello 結果為該 hello 收費站 #1 的資料可以分散在多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="f09cf-257">每個 hello **Input1**資料分割將分別由處理串流分析。</span><span class="sxs-lookup"><span data-stu-id="f09cf-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="f09cf-258">如此一來，多筆記錄的 hello 汽車計數 hello 相同收費站 hello 會建立相同的輪轉視窗中。</span><span class="sxs-lookup"><span data-stu-id="f09cf-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="f09cf-259">如果無法變更 hello 輸入的資料分割索引鍵，即可修正這個問題加入非分割區的步驟，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f09cf-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="f09cf-260">此查詢可以縮放的 too24 SUs。</span><span class="sxs-lookup"><span data-stu-id="f09cf-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="f09cf-261">如果您要聯結兩個資料流，請確定該 hello 資料流分割 hello hello 資料行的資料分割索引鍵，您會使用 toocreate hello 聯結。</span><span class="sxs-lookup"><span data-stu-id="f09cf-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="f09cf-262">也請確定您已擁有 hello 相同數目的兩個資料流中的資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="f09cf-263">設定串流分析串流單位</span><span class="sxs-lookup"><span data-stu-id="f09cf-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="f09cf-264">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f09cf-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f09cf-265">在 hello 清單中的資源，尋找您想 tooscale，然後再開啟它的 hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="f09cf-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="f09cf-266">在 hello 作業刀鋒視窗中，在**設定**，按一下 **標尺**。</span><span class="sxs-lookup"><span data-stu-id="f09cf-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Azure 入口網站串流分析作業組態][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="f09cf-268">使用 hello 滑桿 tooset hello SUs hello 工作。</span><span class="sxs-lookup"><span data-stu-id="f09cf-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="f09cf-269">請注意，您是有限的 toospecific SU 的設定。</span><span class="sxs-lookup"><span data-stu-id="f09cf-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="f09cf-270">監視工作效能</span><span class="sxs-lookup"><span data-stu-id="f09cf-270">Monitor job performance</span></span>
<span data-ttu-id="f09cf-271">您可以使用 hello Azure 入口網站，來追蹤工作的 hello 輸送量：</span><span class="sxs-lookup"><span data-stu-id="f09cf-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Azure 串流分析監視工作][img.stream.analytics.monitor.job]

<span data-ttu-id="f09cf-273">計算預期的 hello hello 工作負載輸送量。</span><span class="sxs-lookup"><span data-stu-id="f09cf-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="f09cf-274">如果少於預期 hello 輸送量，微調 hello 輸入磁碟分割、 微調 hello 查詢，以及加入 SUs tooyour 作業。</span><span class="sxs-lookup"><span data-stu-id="f09cf-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="f09cf-275">以視覺化方式檢視大規模的資料流分析輸送量： hello 覆盆子 Pi 案例</span><span class="sxs-lookup"><span data-stu-id="f09cf-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="f09cf-276">您了解串流分析工作如何調整的 toohelp，我們執行實驗根據來自覆盆子 Pi 裝置的輸入。</span><span class="sxs-lookup"><span data-stu-id="f09cf-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="f09cf-277">此實驗，可讓我們查看 hello 效果對輸送量的多個資料流處理單位和資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="f09cf-278">在此案例中，hello 裝置傳送感應器資料 （用戶端） tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="f09cf-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="f09cf-279">資料流分析處理 hello 資料，並以輸出 tooanother 事件中心傳送的警示或統計資料。</span><span class="sxs-lookup"><span data-stu-id="f09cf-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="f09cf-280">hello 用戶端會以 JSON 格式傳送感應器資料。</span><span class="sxs-lookup"><span data-stu-id="f09cf-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="f09cf-281">hello 資料輸出也是以 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="f09cf-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="f09cf-282">hello 資料看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f09cf-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="f09cf-283">下列查詢的 hello 光線關閉時使用的 toosend 警示：</span><span class="sxs-lookup"><span data-stu-id="f09cf-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="f09cf-284">測量輸送量</span><span class="sxs-lookup"><span data-stu-id="f09cf-284">Measure throughput</span></span>

<span data-ttu-id="f09cf-285">在此情況下，輸送量為 hello 在固定的時間內處理的資料流分析的輸入資料的數量。</span><span class="sxs-lookup"><span data-stu-id="f09cf-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="f09cf-286">（我們單位為 10 分鐘）。tooachieve hello 最佳處理輸送量 hello 輸入資料、 hello 資料流輸入和 hello 查詢已進行資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="f09cf-287">我們包含**count （)**在 hello 查詢 toomeasure 多少輸入的事件已處理。</span><span class="sxs-lookup"><span data-stu-id="f09cf-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="f09cf-288">toomake 確定 hello 工作已不只等候輸入的事件 toocome，大約 300 MB 的輸入資料已預先載入 hello 輸入的事件中樞的每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="f09cf-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="f09cf-289">hello 下表顯示我們增加的資料流單位數目 hello 和事件中心中的 hello 對應的分割區計數時，我們會看見 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="f09cf-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="f09cf-290">輸入資料分割</span><span class="sxs-lookup"><span data-stu-id="f09cf-290">Input Partitions</span></span></th><th><span data-ttu-id="f09cf-291">輸出資料分割</span><span class="sxs-lookup"><span data-stu-id="f09cf-291">Output Partitions</span></span></th><th><span data-ttu-id="f09cf-292">串流處理單位</span><span class="sxs-lookup"><span data-stu-id="f09cf-292">Streaming Units</span></span></th><th><span data-ttu-id="f09cf-293">持續的輸送量</span><span class="sxs-lookup"><span data-stu-id="f09cf-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="f09cf-294">12</span><span class="sxs-lookup"><span data-stu-id="f09cf-294">12</span></span></td>
<td><span data-ttu-id="f09cf-295">12</span><span class="sxs-lookup"><span data-stu-id="f09cf-295">12</span></span></td>
<td><span data-ttu-id="f09cf-296">6</span><span class="sxs-lookup"><span data-stu-id="f09cf-296">6</span></span></td>
<td><span data-ttu-id="f09cf-297">4.06 MB/秒</span><span class="sxs-lookup"><span data-stu-id="f09cf-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f09cf-298">12</span><span class="sxs-lookup"><span data-stu-id="f09cf-298">12</span></span></td>
<td><span data-ttu-id="f09cf-299">12</span><span class="sxs-lookup"><span data-stu-id="f09cf-299">12</span></span></td>
<td><span data-ttu-id="f09cf-300">12</span><span class="sxs-lookup"><span data-stu-id="f09cf-300">12</span></span></td>
<td><span data-ttu-id="f09cf-301">8.06 MB/秒</span><span class="sxs-lookup"><span data-stu-id="f09cf-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f09cf-302">48</span><span class="sxs-lookup"><span data-stu-id="f09cf-302">48</span></span></td>
<td><span data-ttu-id="f09cf-303">48</span><span class="sxs-lookup"><span data-stu-id="f09cf-303">48</span></span></td>
<td><span data-ttu-id="f09cf-304">48</span><span class="sxs-lookup"><span data-stu-id="f09cf-304">48</span></span></td>
<td><span data-ttu-id="f09cf-305">38.32 MB/秒</span><span class="sxs-lookup"><span data-stu-id="f09cf-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f09cf-306">192</span><span class="sxs-lookup"><span data-stu-id="f09cf-306">192</span></span></td>
<td><span data-ttu-id="f09cf-307">192</span><span class="sxs-lookup"><span data-stu-id="f09cf-307">192</span></span></td>
<td><span data-ttu-id="f09cf-308">192</span><span class="sxs-lookup"><span data-stu-id="f09cf-308">192</span></span></td>
<td><span data-ttu-id="f09cf-309">172.67 MB/秒</span><span class="sxs-lookup"><span data-stu-id="f09cf-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f09cf-310">480</span><span class="sxs-lookup"><span data-stu-id="f09cf-310">480</span></span></td>
<td><span data-ttu-id="f09cf-311">480</span><span class="sxs-lookup"><span data-stu-id="f09cf-311">480</span></span></td>
<td><span data-ttu-id="f09cf-312">480</span><span class="sxs-lookup"><span data-stu-id="f09cf-312">480</span></span></td>
<td><span data-ttu-id="f09cf-313">454.27 MB/秒</span><span class="sxs-lookup"><span data-stu-id="f09cf-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f09cf-314">720</span><span class="sxs-lookup"><span data-stu-id="f09cf-314">720</span></span></td>
<td><span data-ttu-id="f09cf-315">720</span><span class="sxs-lookup"><span data-stu-id="f09cf-315">720</span></span></td>
<td><span data-ttu-id="f09cf-316">720</span><span class="sxs-lookup"><span data-stu-id="f09cf-316">720</span></span></td>
<td><span data-ttu-id="f09cf-317">609.69 MB/秒</span><span class="sxs-lookup"><span data-stu-id="f09cf-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="f09cf-318">而且 hello 下列圖形會顯示 hello SUs 與輸送量之間的關聯性的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="f09cf-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="f09cf-320">取得說明</span><span class="sxs-lookup"><span data-stu-id="f09cf-320">Get help</span></span>
<span data-ttu-id="f09cf-321">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="f09cf-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f09cf-322">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f09cf-322">Next steps</span></span>
* [<span data-ttu-id="f09cf-323">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="f09cf-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f09cf-324">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f09cf-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f09cf-325">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="f09cf-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f09cf-326">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="f09cf-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

