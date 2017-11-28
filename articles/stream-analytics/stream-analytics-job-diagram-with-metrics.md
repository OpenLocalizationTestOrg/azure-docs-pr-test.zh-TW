---
title: "aaa Azure Stream Analytics 資料導向使用偵錯 hello 工作圖表 |Microsoft 文件"
description: "疑難排解使用 hello 工作圖表和度量的串流分析工作。"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="98b24-103">資料驅動的偵錯使用 hello 工作圖表</span><span class="sxs-lookup"><span data-stu-id="98b24-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="98b24-104">hello 工作圖表上 hello**監視**hello Azure 入口網站中的刀鋒視窗可協助您以視覺化方式檢視您工作的管線。</span><span class="sxs-lookup"><span data-stu-id="98b24-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="98b24-105">圖表會顯示輸入、輸出和查詢步驟。</span><span class="sxs-lookup"><span data-stu-id="98b24-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="98b24-106">您可以針對每個步驟使用 hello 工作圖表 tooexamine hello 度量，toomore 迅速隔離 hello 問題來源，當您疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="98b24-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="98b24-107">您可以使用 hello 工作圖表</span><span class="sxs-lookup"><span data-stu-id="98b24-107">Using hello job diagram</span></span>

<span data-ttu-id="98b24-108">在 hello Azure 入口網站中的資料流分析工作，而下**支援 + 疑難排解**，選取**工作圖表**:</span><span class="sxs-lookup"><span data-stu-id="98b24-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![作業圖表與計量 - 位置](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="98b24-110">在查詢編輯窗格中選取每個查詢步驟 toosee hello 對應的章節。</span><span class="sxs-lookup"><span data-stu-id="98b24-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="98b24-111">Hello 步驟的度量圖表會顯示在 hello 頁面的下方窗格中。</span><span class="sxs-lookup"><span data-stu-id="98b24-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![作業圖表與計量 - 基本作業](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="98b24-113">toosee hello 資料分割的 hello Azure 事件中樞輸入，選取**...**</span><span class="sxs-lookup"><span data-stu-id="98b24-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="98b24-114">操作功能表隨即出現。</span><span class="sxs-lookup"><span data-stu-id="98b24-114">A context menu appears.</span></span> <span data-ttu-id="98b24-115">您也可以看到 hello 輸入的合併。</span><span class="sxs-lookup"><span data-stu-id="98b24-115">You also can see hello input merger.</span></span>

![作業圖表與計量 - 展開分割區](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="98b24-117">toosee hello 度量圖表只單一分割區，選取 hello 分割節點。</span><span class="sxs-lookup"><span data-stu-id="98b24-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="98b24-118">hello 度量資訊會顯示在 hello hello 頁面底部。</span><span class="sxs-lookup"><span data-stu-id="98b24-118">hello metrics are shown at hello bottom of hello page.</span></span>

![作業圖表與計量 - 其他計量](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="98b24-120">toosee hello 合併時，選取 hello 合併節點的度量圖表。</span><span class="sxs-lookup"><span data-stu-id="98b24-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="98b24-121">hello 下列圖表顯示任何事件已捨棄或調整。</span><span class="sxs-lookup"><span data-stu-id="98b24-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![作業圖表與計量 - 格線](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="98b24-123">hello 公制值和時間，點 toohello 圖表 toosee hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="98b24-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![作業圖表與計量 - 暫留](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="98b24-125">使用計量進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="98b24-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="98b24-126">hello **QueryLastProcessedTime**公制表示特定的步驟時收到的資料。</span><span class="sxs-lookup"><span data-stu-id="98b24-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="98b24-127">藉由查看 hello 拓撲，您可以向後從工作 hello 輸出處理器 toosee 哪些步驟並未收到的資料。</span><span class="sxs-lookup"><span data-stu-id="98b24-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="98b24-128">如果步驟沒有取得資料，請移 toohello 它之前的查詢步驟。</span><span class="sxs-lookup"><span data-stu-id="98b24-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="98b24-129">檢查是否 hello 上述查詢步驟都有時間視窗中，而且如果它有充裕的時間 toooutput 資料。</span><span class="sxs-lookup"><span data-stu-id="98b24-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="98b24-130">（請注意，時間視窗包括 貼齊的 toohello 小時。）</span><span class="sxs-lookup"><span data-stu-id="98b24-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="98b24-131">如果 hello 上述的查詢步驟輸入的處理器，請使用下列目標的問題 hello 輸入的度量 toohelp 回應 hello。</span><span class="sxs-lookup"><span data-stu-id="98b24-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="98b24-132">這可協助您判斷作業是否正在從輸入來源取得資料。</span><span class="sxs-lookup"><span data-stu-id="98b24-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="98b24-133">如果已分割 hello 查詢，檢查每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="98b24-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="98b24-134">已讀取多少資料？</span><span class="sxs-lookup"><span data-stu-id="98b24-134">How much data is being read?</span></span>

*   <span data-ttu-id="98b24-135">**InputEventsSourcesTotal**是 hello 數目讀取資料單元。</span><span class="sxs-lookup"><span data-stu-id="98b24-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="98b24-136">例如，hello blob 的數目。</span><span class="sxs-lookup"><span data-stu-id="98b24-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="98b24-137">**InputEventsTotal**是 hello 讀取的事件數目。</span><span class="sxs-lookup"><span data-stu-id="98b24-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="98b24-138">此度量適用於每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="98b24-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="98b24-139">**InputEventsInBytesTotal**是 hello 讀取的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="98b24-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="98b24-140">**InputEventsLastArrivalTime** 會更新每個收到事件的加入佇列時間。</span><span class="sxs-lookup"><span data-stu-id="98b24-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="98b24-141">時間是否正在前進？</span><span class="sxs-lookup"><span data-stu-id="98b24-141">Is time moving forward?</span></span> <span data-ttu-id="98b24-142">若實際事件已讀取，則可能無需加上標點符號。</span><span class="sxs-lookup"><span data-stu-id="98b24-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="98b24-143">**InputEventsLastPunctuationTime**表示當標點符號已發出 tookeep 時間移動向前復原。</span><span class="sxs-lookup"><span data-stu-id="98b24-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="98b24-144">若未加上標點符號，可能使資料流程遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="98b24-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="98b24-145">Hello 輸入中是否有任何錯誤？</span><span class="sxs-lookup"><span data-stu-id="98b24-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="98b24-146">**InputEventsEventDataNullTotal** 是具有 Null 資料的事件計數。</span><span class="sxs-lookup"><span data-stu-id="98b24-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="98b24-147">**InputEventsSerializerErrorsTotal** 是無法正確還原序列化的事件計數。</span><span class="sxs-lookup"><span data-stu-id="98b24-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="98b24-148">**InputEventsDegradedTotal** 是有其他還原序列化以外問題的事件計數。</span><span class="sxs-lookup"><span data-stu-id="98b24-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="98b24-149">事件遭到捨棄或調整？</span><span class="sxs-lookup"><span data-stu-id="98b24-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="98b24-150">**InputEventsEarlyTotal**是 hello 具有應用程式之前的時間戳記 hello 高水位線的事件數目。</span><span class="sxs-lookup"><span data-stu-id="98b24-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="98b24-151">**InputEventsLateTotal**是 hello hello 高水位線之後，擁有應用程式時間戳記的事件數目。</span><span class="sxs-lookup"><span data-stu-id="98b24-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="98b24-152">**InputEventsDroppedBeforeApplicationStartTimeTotal**是 hello 的事件數 hello 工作開始時間之前卸除。</span><span class="sxs-lookup"><span data-stu-id="98b24-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="98b24-153">讀取資料的速度太慢了嗎？</span><span class="sxs-lookup"><span data-stu-id="98b24-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="98b24-154">**InputEventsSourcesBackloggedTotal**告訴您需要更多的訊息數量的 toobe 事件中樞與 Azure IoT 中樞的輸入中讀取。</span><span class="sxs-lookup"><span data-stu-id="98b24-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="98b24-155">取得說明</span><span class="sxs-lookup"><span data-stu-id="98b24-155">Get help</span></span>
<span data-ttu-id="98b24-156">如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="98b24-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="98b24-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98b24-157">Next steps</span></span>
* [<span data-ttu-id="98b24-158">簡介 tooStream 分析</span><span class="sxs-lookup"><span data-stu-id="98b24-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="98b24-159">開始使用串流分析</span><span class="sxs-lookup"><span data-stu-id="98b24-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="98b24-160">調整串流分析作業</span><span class="sxs-lookup"><span data-stu-id="98b24-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="98b24-161">串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="98b24-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="98b24-162">串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="98b24-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
