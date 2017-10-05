---
title: "Azure 串流分析︰最佳化您的作業以有效率地使用串流單位 |Microsoft Docs"
description: "查詢 Azure 串流分析中關於規模與效能的最佳做法。"
keywords: "串流單位、查詢效能"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 1441a5df4fd92abf85763ca9a1512503b1a0da56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-your-job-to-use-streaming-units-efficiently"></a><span data-ttu-id="83271-104">最佳化您的作業以有效率地使用串流單位</span><span class="sxs-lookup"><span data-stu-id="83271-104">Optimize your job to use Streaming Units efficiently</span></span>

<span data-ttu-id="83271-105">Azure 串流分析會將執行一個作業的效能「權重」彙總為串流單位 (SU)。</span><span class="sxs-lookup"><span data-stu-id="83271-105">Azure Stream Analytics aggregates the performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="83271-106">SU 代表用在執行作業的計算資源。</span><span class="sxs-lookup"><span data-stu-id="83271-106">SUs represent the computing resources that are consumed to execute a job.</span></span> <span data-ttu-id="83271-107">SU 會根據 CPU、記憶體，以及讀寫率的混合量值，提供一個方式來描述相關的事件處理容量。</span><span class="sxs-lookup"><span data-stu-id="83271-107">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="83271-108">此功能可讓您專注在查詢邏輯上，您不必知道儲存層的效能考量、不用手動配置您的作業，以及估計需要多少 CPU 核心計數來及時執行您的作業。</span><span class="sxs-lookup"><span data-stu-id="83271-108">This capacity lets you focus on the query logic and removes you from needing to know storage tier performance considerations, allocate memory for your job manually, and approximate the CPU core-count needed to run your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="83271-109">一個作業需要多少 SU？</span><span class="sxs-lookup"><span data-stu-id="83271-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="83271-110">選擇特定作業所需的 SU 數量取決於輸入的磁碟分割組態以及作業內定義的查詢。</span><span class="sxs-lookup"><span data-stu-id="83271-110">Choosing the number of required SUs for a particular job depends on the partition configuration for the inputs and the query that's defined within the job.</span></span> <span data-ttu-id="83271-111">[規模] 刀鋒視窗可讓您設定正確的 SU 數目。</span><span class="sxs-lookup"><span data-stu-id="83271-111">The **Scale** blade allows you to set the right number of SUs.</span></span> <span data-ttu-id="83271-112">最好作法是配置比所需數目還多的 SU。</span><span class="sxs-lookup"><span data-stu-id="83271-112">It is a best practice to allocate more SUs than needed.</span></span> <span data-ttu-id="83271-113">串流處理引擎會不惜分派額外的記憶體，針對延遲和輸送量進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="83271-113">The Stream Analytics processing engine optimizes for latency and throughput at the cost of allocating additional memory.</span></span>

<span data-ttu-id="83271-114">一般情況下，最佳的作法是對不是使用 *PARTITION BY* 的查詢使用 6 個 SU 開始。</span><span class="sxs-lookup"><span data-stu-id="83271-114">In general, the best practice is to start with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="83271-115">然後使用反覆嘗試的方法來決定最佳配置，這方法就是您可以在傳送代表的資料總數後修改 SU 數目，並且檢查 SU 的 %Utilization 計量。</span><span class="sxs-lookup"><span data-stu-id="83271-115">Then determine the sweet spot by using a trial and error method in which you modify the number of SUs after you pass representative amounts of data and examine the SU %Utilization metric.</span></span>

<span data-ttu-id="83271-116">在 Azure 串流分析開始任何處理作業前，Azure 串流分析會先將事件保留於「重新排序緩衝區」視窗中。</span><span class="sxs-lookup"><span data-stu-id="83271-116">Azure Stream Analytics keeps events in a window called the “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="83271-117">事件會依時間順序排列於重新排序視窗中，並會依事件的暫時排序執行後續作業。</span><span class="sxs-lookup"><span data-stu-id="83271-117">Events are sorted within the reorder window by time, and subsequent operations are performed on the temporally sorted events.</span></span> <span data-ttu-id="83271-118">依時間時重新排列事件可確保運算子會在設定的時間範圍內顯示在所有事件中。</span><span class="sxs-lookup"><span data-stu-id="83271-118">Reordering events by time ensures that the operator has visibility into all the events in the stipulated timeframe.</span></span> <span data-ttu-id="83271-119">這也可讓運算子執行必要處理程序和產生輸出。</span><span class="sxs-lookup"><span data-stu-id="83271-119">It also lets the operator perform the requisite processing and produce an output.</span></span> <span data-ttu-id="83271-120">這項機制的副作用是，處理作業會因重新排列視窗的持續時間而導致延遲。</span><span class="sxs-lookup"><span data-stu-id="83271-120">A side effect of this mechanism is that processing is delayed by the duration of the reorder window.</span></span> <span data-ttu-id="83271-121">該作業的記憶體使用量 (將影響 SU 耗用量) 即是此重新排列視窗的函數大小，以及其中所包含的事件數目。</span><span class="sxs-lookup"><span data-stu-id="83271-121">The memory footprint of the job (which affects SU consumption) is a function of the size of this reorder window and the number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="83271-122">如果在作業升級期間變更讀取器數量，暫時性警告會寫入稽核記錄中。</span><span class="sxs-lookup"><span data-stu-id="83271-122">When the number of readers changes during job upgrades, transient warnings are written to audit logs.</span></span> <span data-ttu-id="83271-123">串流分析作業會從這些暫時性問題中自動復原。</span><span class="sxs-lookup"><span data-stu-id="83271-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="83271-124">常見的高效能記憶體會需要高 SU 使用率來執行作業</span><span class="sxs-lookup"><span data-stu-id="83271-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="83271-125">分組依據的高基數</span><span class="sxs-lookup"><span data-stu-id="83271-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="83271-126">傳入事件的基數指定了工作的記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="83271-126">The cardinality of incoming events dictates memory usage for the job.</span></span>

<span data-ttu-id="83271-127">例如，在 `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`，與**叢集**相關的數字是查詢基數。</span><span class="sxs-lookup"><span data-stu-id="83271-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, the number associated with **clustered** is the cardinality of the query.</span></span>

<span data-ttu-id="83271-128">若要減少高基數造成的問題，須使用 **PARTITION BY** 來增加分割區以擴展查詢。</span><span class="sxs-lookup"><span data-stu-id="83271-128">To mitigate issues that are caused by high cardinality, scale out the query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="83271-129">*叢集*數目在這裡是 GROUP BY 的基數。</span><span class="sxs-lookup"><span data-stu-id="83271-129">The number of *clustered* is the cardinality of GROUP BY here.</span></span>

<span data-ttu-id="83271-130">查詢分割後，便會分散到多個節點。</span><span class="sxs-lookup"><span data-stu-id="83271-130">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="83271-131">如此一來，進入到每個節點的事件數目便會降低，因此也降低了重新排列緩衝區的大小。</span><span class="sxs-lookup"><span data-stu-id="83271-131">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> <span data-ttu-id="83271-132">您也應該依據 partitionid 分割事件中樞的分割區。</span><span class="sxs-lookup"><span data-stu-id="83271-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="83271-133">JOIN 的高量不相符事件計數</span><span class="sxs-lookup"><span data-stu-id="83271-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="83271-134">在 JOIN 中有高量不相符的事件數目，會影響查詢的記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="83271-134">The number of unmatched events in a JOIN affects the memory utilization of the query.</span></span> <span data-ttu-id="83271-135">例如，有個查詢是要找出產生點擊數的廣告曝光數：</span><span class="sxs-lookup"><span data-stu-id="83271-135">For example, take a query that is looking to find the number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="83271-136">在此案例中，很可能會顯示許多廣告，但只產生少數點擊數。</span><span class="sxs-lookup"><span data-stu-id="83271-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="83271-137">這類的結果就需要可將所有事件保留在同個時間範圍的作業。</span><span class="sxs-lookup"><span data-stu-id="83271-137">Such a result would require the job to keep all the events within the time window.</span></span> <span data-ttu-id="83271-138">範圍大小和事件出現率與記憶體耗用量成正比。</span><span class="sxs-lookup"><span data-stu-id="83271-138">The amount of memory consumed is proportional to the window size and event rate.</span></span> 

<span data-ttu-id="83271-139">若要減少這種情況下，須使用「PARTITION BY」來增加分割區以擴展查詢。</span><span class="sxs-lookup"><span data-stu-id="83271-139">To mitigate this situation, scale out the query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="83271-140">查詢分割後，便會分散到多個處理節點。</span><span class="sxs-lookup"><span data-stu-id="83271-140">After the query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="83271-141">如此一來，進入到每個節點的事件數目便會降低，因此也降低了重新排列緩衝區的大小。</span><span class="sxs-lookup"><span data-stu-id="83271-141">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="83271-142">大量的順序錯亂事件</span><span class="sxs-lookup"><span data-stu-id="83271-142">Large number of out of order events</span></span> 

<span data-ttu-id="83271-143">在大型時間範圍內的大量順序錯亂事件會導致「重新排序」規模變得更大。</span><span class="sxs-lookup"><span data-stu-id="83271-143">A large number of out of order events within a large time window causes the size of the "reorder buffer" to be larger.</span></span> <span data-ttu-id="83271-144">若要減少這種情況下，須使用「PARTITION BY」來增加分割區以調整查詢規模。</span><span class="sxs-lookup"><span data-stu-id="83271-144">To mitigate this situation, scale the query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="83271-145">查詢分割後，便會分散到多個節點。</span><span class="sxs-lookup"><span data-stu-id="83271-145">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="83271-146">如此一來，進入到每個節點的事件數目便會降低，因此也降低了重新排列緩衝區的大小。</span><span class="sxs-lookup"><span data-stu-id="83271-146">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="83271-147">取得說明</span><span class="sxs-lookup"><span data-stu-id="83271-147">Get help</span></span>
<span data-ttu-id="83271-148">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="83271-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="83271-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="83271-149">Next steps</span></span>
* [<span data-ttu-id="83271-150">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="83271-150">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="83271-151">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="83271-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="83271-152">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="83271-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="83271-153">Azure 串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="83271-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="83271-154">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="83271-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
