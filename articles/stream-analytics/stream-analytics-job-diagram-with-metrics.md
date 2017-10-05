---
title: "使用作業圖表對 Azure 串流分析進行資料導向偵錯 | Microsoft Docs"
description: "使用作業圖表和計量對串流分析作業進行移難排解。"
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
ms.openlocfilehash: 4e5949232e8377b7697eaebf96eacdc31c4f5422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a><span data-ttu-id="c3e52-103">使用作業圖表進行資料導向偵錯</span><span class="sxs-lookup"><span data-stu-id="c3e52-103">Data-driven debugging by using the job diagram</span></span>

<span data-ttu-id="c3e52-104">在 Azure 入口網站中，[監視] 刀鋒視窗上的作業圖表可協助您將作業流程視覺化。</span><span class="sxs-lookup"><span data-stu-id="c3e52-104">The job diagram on the **Monitoring** blade in the Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="c3e52-105">圖表會顯示輸入、輸出和查詢步驟。</span><span class="sxs-lookup"><span data-stu-id="c3e52-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="c3e52-106">您可以使用作業圖表來檢查每個步驟的計量，以便在進行移難排解時更快速地找出問題來源。</span><span class="sxs-lookup"><span data-stu-id="c3e52-106">You can use the job diagram to examine the metrics for each step, to more quickly isolate the source of a problem when you troubleshoot issues.</span></span>

## <a name="using-the-job-diagram"></a><span data-ttu-id="c3e52-107">使用作業圖表</span><span class="sxs-lookup"><span data-stu-id="c3e52-107">Using the job diagram</span></span>

<span data-ttu-id="c3e52-108">當串流作業執行時，在 Azure 入口網站中的 [支援+疑難排解] 下選取 [作業圖表]：</span><span class="sxs-lookup"><span data-stu-id="c3e52-108">In the Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![作業圖表與計量 - 位置](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="c3e52-110">選取每個查詢步驟，可在查詢編輯窗格中看到對應的區段。</span><span class="sxs-lookup"><span data-stu-id="c3e52-110">Select each query step to see the corresponding section in a query editing pane.</span></span> <span data-ttu-id="c3e52-111">步驟的計量圖表會顯示在頁面上的下方窗格中。</span><span class="sxs-lookup"><span data-stu-id="c3e52-111">A metric chart for the step is displayed in a lower pane on the page.</span></span>

![作業圖表與計量 - 基本作業](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="c3e52-113">若要查看 Azure 事件中樞的分割區，請選取 **. . .**</span><span class="sxs-lookup"><span data-stu-id="c3e52-113">To see the partitions of the Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="c3e52-114">操作功能表隨即出現。</span><span class="sxs-lookup"><span data-stu-id="c3e52-114">A context menu appears.</span></span> <span data-ttu-id="c3e52-115">您也可以看到輸入的合併。</span><span class="sxs-lookup"><span data-stu-id="c3e52-115">You also can see the input merger.</span></span>

![作業圖表與計量 - 展開分割區](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="c3e52-117">若只要查看單一分割區的計量圖表，請選取分割區節點。</span><span class="sxs-lookup"><span data-stu-id="c3e52-117">To see the metric chart for only a single partition, select the partition node.</span></span> <span data-ttu-id="c3e52-118">計量資訊會顯示在頁面底部。</span><span class="sxs-lookup"><span data-stu-id="c3e52-118">The metrics are shown at the bottom of the page.</span></span>

![作業圖表與計量 - 其他計量](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="c3e52-120">若要查看合併的計量圖表，請選取合併節點。</span><span class="sxs-lookup"><span data-stu-id="c3e52-120">To see the metrics chart for a merger, select the merger node.</span></span> <span data-ttu-id="c3e52-121">下列圖表顯示沒有任何事件遭到捨棄或調整。</span><span class="sxs-lookup"><span data-stu-id="c3e52-121">The following chart shows that no events were dropped or adjusted.</span></span>

![作業圖表與計量 - 格線](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="c3e52-123">若要查看的計量值和時間的詳細資訊，請指向圖表。</span><span class="sxs-lookup"><span data-stu-id="c3e52-123">To see the details of the metric value and time, point to the chart.</span></span>

![作業圖表與計量 - 暫留](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="c3e52-125">使用計量進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="c3e52-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="c3e52-126">**QueryLastProcessedTime** 計量表示特定步驟收到資料的時間。</span><span class="sxs-lookup"><span data-stu-id="c3e52-126">The **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="c3e52-127">藉由觀看拓撲，您可以從輸出處理器回溯的工作看出哪個階段沒有接收資料。</span><span class="sxs-lookup"><span data-stu-id="c3e52-127">By looking at the topology, you can work backward from the output processor to see which step is not receiving data.</span></span> <span data-ttu-id="c3e52-128">如果步驟沒有取得資料，請移至該步驟之前的查詢步驟。</span><span class="sxs-lookup"><span data-stu-id="c3e52-128">If a step is not getting data, go to the query step just before it.</span></span> <span data-ttu-id="c3e52-129">檢查先前查詢步驟中是否有時間範圍，以及時間分配是否足夠讓其輸出資料。</span><span class="sxs-lookup"><span data-stu-id="c3e52-129">Check whether the preceding query step has a time window, and if enough time has passed for it to output data.</span></span> <span data-ttu-id="c3e52-130">(請注意，時間範圍會以小時分配。)</span><span class="sxs-lookup"><span data-stu-id="c3e52-130">(Note that time windows are snapped to the hour.)</span></span>
 
<span data-ttu-id="c3e52-131">若前一個查步驟為輸入處理器，使用輸入計量可協助回答下列預定問題。</span><span class="sxs-lookup"><span data-stu-id="c3e52-131">If the preceding query step is an input processor, use the input metrics to help answer the following targeted questions.</span></span> <span data-ttu-id="c3e52-132">這可協助您判斷作業是否正在從輸入來源取得資料。</span><span class="sxs-lookup"><span data-stu-id="c3e52-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="c3e52-133">如果查詢已分割，則檢查每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="c3e52-133">If the query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="c3e52-134">已讀取多少資料？</span><span class="sxs-lookup"><span data-stu-id="c3e52-134">How much data is being read?</span></span>

*   <span data-ttu-id="c3e52-135">**InputEventsSourcesTotal** 是讀取的資料單位數目。</span><span class="sxs-lookup"><span data-stu-id="c3e52-135">**InputEventsSourcesTotal** is the number of data units read.</span></span> <span data-ttu-id="c3e52-136">例如，Blob 的數目。</span><span class="sxs-lookup"><span data-stu-id="c3e52-136">For example, the number of blobs.</span></span>
*   <span data-ttu-id="c3e52-137">**InputEventsTotal** 是讀取的事件數目。</span><span class="sxs-lookup"><span data-stu-id="c3e52-137">**InputEventsTotal** is the number of events read.</span></span> <span data-ttu-id="c3e52-138">此度量適用於每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="c3e52-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="c3e52-139">**InputEventsTotal** 是讀取的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="c3e52-139">**InputEventsInBytesTotal** is the number of bytes read.</span></span>
*   <span data-ttu-id="c3e52-140">**InputEventsLastArrivalTime** 會更新每個收到事件的加入佇列時間。</span><span class="sxs-lookup"><span data-stu-id="c3e52-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="c3e52-141">時間是否正在前進？</span><span class="sxs-lookup"><span data-stu-id="c3e52-141">Is time moving forward?</span></span> <span data-ttu-id="c3e52-142">若實際事件已讀取，則可能無需加上標點符號。</span><span class="sxs-lookup"><span data-stu-id="c3e52-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="c3e52-143">**InputEventsLastPunctuationTime** 指出何時加上了標點符號，使時間能繼續前進。</span><span class="sxs-lookup"><span data-stu-id="c3e52-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued to keep time moving forward.</span></span> <span data-ttu-id="c3e52-144">若未加上標點符號，可能使資料流程遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="c3e52-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-the-input"></a><span data-ttu-id="c3e52-145">在輸入中是否有任何錯誤？</span><span class="sxs-lookup"><span data-stu-id="c3e52-145">Are there any errors in the input?</span></span>

*   <span data-ttu-id="c3e52-146">**InputEventsEventDataNullTotal** 是具有 Null 資料的事件計數。</span><span class="sxs-lookup"><span data-stu-id="c3e52-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="c3e52-147">**InputEventsSerializerErrorsTotal** 是無法正確還原序列化的事件計數。</span><span class="sxs-lookup"><span data-stu-id="c3e52-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="c3e52-148">**InputEventsDegradedTotal** 是有其他還原序列化以外問題的事件計數。</span><span class="sxs-lookup"><span data-stu-id="c3e52-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="c3e52-149">事件遭到捨棄或調整？</span><span class="sxs-lookup"><span data-stu-id="c3e52-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="c3e52-150">**InputEventsEarlyTotal** 是在高水位線之前，具有應用程式時間戳記的事件數目。</span><span class="sxs-lookup"><span data-stu-id="c3e52-150">**InputEventsEarlyTotal** is the number of events that have an application timestamp before the high watermark.</span></span>
*   <span data-ttu-id="c3e52-151">**InputEventsLateTotal** 是在高水位線之後，具有應用程式時間戳記的事件數目。</span><span class="sxs-lookup"><span data-stu-id="c3e52-151">**InputEventsLateTotal** is the number of events that have an application timestamp after the high watermark.</span></span>
*   <span data-ttu-id="c3e52-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** 是在作業開始時間之前已捨棄的事件數目。</span><span class="sxs-lookup"><span data-stu-id="c3e52-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is the number events dropped before the job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="c3e52-153">讀取資料的速度太慢了嗎？</span><span class="sxs-lookup"><span data-stu-id="c3e52-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="c3e52-154">**InputEventsSourcesBackloggedTotal** 會告訴您事件中樞及 Azure IoT 中樞輸入還需要讀取多少訊息數量。</span><span class="sxs-lookup"><span data-stu-id="c3e52-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need to be read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="c3e52-155">取得說明</span><span class="sxs-lookup"><span data-stu-id="c3e52-155">Get help</span></span>
<span data-ttu-id="c3e52-156">如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="c3e52-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3e52-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3e52-157">Next steps</span></span>
* [<span data-ttu-id="c3e52-158">串流分析介紹</span><span class="sxs-lookup"><span data-stu-id="c3e52-158">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c3e52-159">開始使用串流分析</span><span class="sxs-lookup"><span data-stu-id="c3e52-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c3e52-160">調整串流分析作業</span><span class="sxs-lookup"><span data-stu-id="c3e52-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c3e52-161">串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="c3e52-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c3e52-162">串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="c3e52-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
