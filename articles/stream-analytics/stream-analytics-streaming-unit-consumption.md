---
title: "Azure Stream Analytics： 有效率地最佳化您的工作 toouse 串流單位 |Microsoft 文件"
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
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a><span data-ttu-id="5d69e-104">有效率地最佳化您的工作 toouse 串流單位</span><span class="sxs-lookup"><span data-stu-id="5d69e-104">Optimize your job toouse Streaming Units efficiently</span></span>

<span data-ttu-id="5d69e-105">Azure Stream Analytics 彙總 hello 效能"weight"的資料流處理單位 (SUs) 到執行作業。</span><span class="sxs-lookup"><span data-stu-id="5d69e-105">Azure Stream Analytics aggregates hello performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="5d69e-106">SUs 代表 hello 運算資源的取用的 tooexecute 作業。</span><span class="sxs-lookup"><span data-stu-id="5d69e-106">SUs represent hello computing resources that are consumed tooexecute a job.</span></span> <span data-ttu-id="5d69e-107">SUs 提供方式 toodescribe hello 相對事件處理為基礎的混合測量結果的 CPU、 記憶體容量和讀寫率。</span><span class="sxs-lookup"><span data-stu-id="5d69e-107">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="5d69e-108">這個容量可讓您專注於 hello 查詢邏輯並移除您就不需要 tooknow 儲存層的效能考量，以手動方式，您的工作配置記憶體並及時近似 hello CPU core-所需的計數 toorun 您的工作。</span><span class="sxs-lookup"><span data-stu-id="5d69e-108">This capacity lets you focus on hello query logic and removes you from needing tooknow storage tier performance considerations, allocate memory for your job manually, and approximate hello CPU core-count needed toorun your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="5d69e-109">一個作業需要多少 SU？</span><span class="sxs-lookup"><span data-stu-id="5d69e-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="5d69e-110">選擇的特定作業的必要 SUs 的 hello 數目取決於 hello hello 輸入和 hello 工作內所定義的 hello 查詢的資料分割組態。</span><span class="sxs-lookup"><span data-stu-id="5d69e-110">Choosing hello number of required SUs for a particular job depends on hello partition configuration for hello inputs and hello query that's defined within hello job.</span></span> <span data-ttu-id="5d69e-111">hello**標尺**刀鋒視窗可讓您 tooset hello SUs 的權限數目。</span><span class="sxs-lookup"><span data-stu-id="5d69e-111">hello **Scale** blade allows you tooset hello right number of SUs.</span></span> <span data-ttu-id="5d69e-112">它會是最佳作法 tooallocate 比所需的多個 SUs。</span><span class="sxs-lookup"><span data-stu-id="5d69e-112">It is a best practice tooallocate more SUs than needed.</span></span> <span data-ttu-id="5d69e-113">延遲及輸送量 hello 成本的配置額外的記憶體最佳化 hello Stream Analytics 處理引擎。</span><span class="sxs-lookup"><span data-stu-id="5d69e-113">hello Stream Analytics processing engine optimizes for latency and throughput at hello cost of allocating additional memory.</span></span>

<span data-ttu-id="5d69e-114">Hello 最佳作法一般是未使用之查詢的 6 sus toostart *PARTITION BY*。</span><span class="sxs-lookup"><span data-stu-id="5d69e-114">In general, hello best practice is toostart with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="5d69e-115">使用您在其中修改 hello SUs 數目後代表性的資料量並檢查 hello SU %使用量度量的試驗方法，然後判斷 hello 成問題。</span><span class="sxs-lookup"><span data-stu-id="5d69e-115">Then determine hello sweet spot by using a trial and error method in which you modify hello number of SUs after you pass representative amounts of data and examine hello SU %Utilization metric.</span></span>

<span data-ttu-id="5d69e-116">Azure Stream Analytics 中保留事件視窗中啟動任何處理之前，先呼叫 hello"重新排序緩衝區 」。</span><span class="sxs-lookup"><span data-stu-id="5d69e-116">Azure Stream Analytics keeps events in a window called hello “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="5d69e-117">事件會依照 hello 重新排列視窗內的時間，和後續作業 hello 暫時排序事件。</span><span class="sxs-lookup"><span data-stu-id="5d69e-117">Events are sorted within hello reorder window by time, and subsequent operations are performed on hello temporally sorted events.</span></span> <span data-ttu-id="5d69e-118">依時間排列的事件可確保該 hello 運算子具有入所有資料行的可見性 hello 事件 hello 中的約定的時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="5d69e-118">Reordering events by time ensures that hello operator has visibility into all hello events in hello stipulated timeframe.</span></span> <span data-ttu-id="5d69e-119">它也可讓 hello 運算子執行 hello 必要的處理，以及產生的輸出。</span><span class="sxs-lookup"><span data-stu-id="5d69e-119">It also lets hello operator perform hello requisite processing and produce an output.</span></span> <span data-ttu-id="5d69e-120">這項機制的副作用是 hello hello 重新排列視窗持續時間會因為延遲處理。</span><span class="sxs-lookup"><span data-stu-id="5d69e-120">A side effect of this mechanism is that processing is delayed by hello duration of hello reorder window.</span></span> <span data-ttu-id="5d69e-121">hello hello 作業 （影響 SU 耗用量） 的記憶體耗用量是大小的 hello 數目這個重新排列視窗和 hello 事件包含在它的函式。</span><span class="sxs-lookup"><span data-stu-id="5d69e-121">hello memory footprint of hello job (which affects SU consumption) is a function of hello size of this reorder window and hello number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="5d69e-122">讀取器的 hello 數目變更時升級作業期間，暫時性的警告會寫入 tooaudit 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5d69e-122">When hello number of readers changes during job upgrades, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="5d69e-123">串流分析作業會從這些暫時性問題中自動復原。</span><span class="sxs-lookup"><span data-stu-id="5d69e-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="5d69e-124">常見的高效能記憶體會需要高 SU 使用率來執行作業</span><span class="sxs-lookup"><span data-stu-id="5d69e-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="5d69e-125">分組依據的高基數</span><span class="sxs-lookup"><span data-stu-id="5d69e-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="5d69e-126">內送事件的 hello 基數規定 hello 作業的記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="5d69e-126">hello cardinality of incoming events dictates memory usage for hello job.</span></span>

<span data-ttu-id="5d69e-127">例如，在`SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`，hello 與相關聯的數字**叢集**是 hello 查詢的 hello 基數。</span><span class="sxs-lookup"><span data-stu-id="5d69e-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello number associated with **clustered** is hello cardinality of hello query.</span></span>

<span data-ttu-id="5d69e-128">toomitigate 問題所造成的高基數，藉由增加使用的資料分割延展 hello 查詢**PARTITION BY**。</span><span class="sxs-lookup"><span data-stu-id="5d69e-128">toomitigate issues that are caused by high cardinality, scale out hello query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="5d69e-129">hello 數目*叢集*是 hello 的基數 GROUP BY 這裡。</span><span class="sxs-lookup"><span data-stu-id="5d69e-129">hello number of *clustered* is hello cardinality of GROUP BY here.</span></span>

<span data-ttu-id="5d69e-130">分割 hello 查詢之後，它是分散在多個節點。</span><span class="sxs-lookup"><span data-stu-id="5d69e-130">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="5d69e-131">如此一來，hello 進入到每個節點中的事件數目會降低，這又可以降低 hello hello 重新排序緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="5d69e-131">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> <span data-ttu-id="5d69e-132">您也應該依據 partitionid 分割事件中樞的分割區。</span><span class="sxs-lookup"><span data-stu-id="5d69e-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="5d69e-133">JOIN 的高量不相符事件計數</span><span class="sxs-lookup"><span data-stu-id="5d69e-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="5d69e-134">不相符的事件聯結中的 hello 數目會影響 hello 查詢 hello 記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="5d69e-134">hello number of unmatched events in a JOIN affects hello memory utilization of hello query.</span></span> <span data-ttu-id="5d69e-135">例如，採用正在尋找的廣告效果 toofind hello 數目，會產生按下的查詢：</span><span class="sxs-lookup"><span data-stu-id="5d69e-135">For example, take a query that is looking toofind hello number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="5d69e-136">在此案例中，很可能會顯示許多廣告，但只產生少數點擊數。</span><span class="sxs-lookup"><span data-stu-id="5d69e-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="5d69e-137">這類結果需要 hello 作業 tookeep hello 的時間間隔內的所有 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="5d69e-137">Such a result would require hello job tookeep all hello events within hello time window.</span></span> <span data-ttu-id="5d69e-138">hello 耗用數量是記憶體的成比例 toohello 視窗大小和事件速率。</span><span class="sxs-lookup"><span data-stu-id="5d69e-138">hello amount of memory consumed is proportional toohello window size and event rate.</span></span> 

<span data-ttu-id="5d69e-139">toomitigate 此情況下，向外延展藉由增加 hello 查詢分割分割區藉由使用。</span><span class="sxs-lookup"><span data-stu-id="5d69e-139">toomitigate this situation, scale out hello query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="5d69e-140">分割 hello 查詢之後，它是分散在多個處理節點。</span><span class="sxs-lookup"><span data-stu-id="5d69e-140">After hello query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="5d69e-141">如此一來，hello 進入到每個節點中的事件數目會降低，這又可以降低 hello hello 重新排序緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="5d69e-141">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="5d69e-142">大量的順序錯亂事件</span><span class="sxs-lookup"><span data-stu-id="5d69e-142">Large number of out of order events</span></span> 

<span data-ttu-id="5d69e-143">大量的大型的時間間隔內的失序的事件會造成較大 hello"重新排序緩衝區"toobe hello 大小。</span><span class="sxs-lookup"><span data-stu-id="5d69e-143">A large number of out of order events within a large time window causes hello size of hello "reorder buffer" toobe larger.</span></span> <span data-ttu-id="5d69e-144">toomitigate 此情況下，藉由增加小數位數 hello 查詢分割分割區藉由使用。</span><span class="sxs-lookup"><span data-stu-id="5d69e-144">toomitigate this situation, scale hello query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="5d69e-145">分割 hello 查詢之後，它是分散在多個節點。</span><span class="sxs-lookup"><span data-stu-id="5d69e-145">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="5d69e-146">如此一來，hello 進入到每個節點中的事件數目會降低，這又可以降低 hello hello 重新排序緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="5d69e-146">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="5d69e-147">取得說明</span><span class="sxs-lookup"><span data-stu-id="5d69e-147">Get help</span></span>
<span data-ttu-id="5d69e-148">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="5d69e-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d69e-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d69e-149">Next steps</span></span>
* [<span data-ttu-id="5d69e-150">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="5d69e-150">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5d69e-151">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5d69e-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5d69e-152">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="5d69e-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5d69e-153">Azure 串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="5d69e-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5d69e-154">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="5d69e-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
