---
title: "Azure 串流分析的疑難排解指南 | Microsoft Docs"
description: "如何對您的串流分析作業進行疑難排解"
keywords: "疑難排解指南"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 8ecf279047f06691cef1bc0db06888974405a9f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a><span data-ttu-id="68383-104">Azure 串流分析的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="68383-104">Troubleshooting guide for Azure Stream Analytics</span></span>

<span data-ttu-id="68383-105">第一眼看到 Azure 串流分析的疑難排解作業時，您可能會覺得這是複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="68383-105">Azure Stream Analytics troubleshooting can appear to be a complex effort at first glance.</span></span> <span data-ttu-id="68383-106">在與許多使用者合作後，我們建立了本指南來協助您簡化程序，並移除輸入、輸出、查詢和函式的任何猜測工作。</span><span class="sxs-lookup"><span data-stu-id="68383-106">After working with many users, we have created this guide to help streamline the process and remove the guesswork about your inputs, outputs, queries, and functions.</span></span>

## <a name="troubleshoot-your-stream-analytics-job"></a><span data-ttu-id="68383-107">對您的串流分析作業進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="68383-107">Troubleshoot your Stream Analytics job</span></span>

<span data-ttu-id="68383-108">為取得串流分析作業的最佳疑難排解結果，請使用下列指導方針︰</span><span class="sxs-lookup"><span data-stu-id="68383-108">For best results in troubleshooting your Stream Analytics job, use the following guidelines:</span></span>

1.  <span data-ttu-id="68383-109">測試連線：</span><span class="sxs-lookup"><span data-stu-id="68383-109">Test your connectivity:</span></span>
    - <span data-ttu-id="68383-110">針對各個輸入和輸出使用 [測試連線] 按鈕，驗證輸入及輸出的連線能力。</span><span class="sxs-lookup"><span data-stu-id="68383-110">Verify connectivity to inputs and outputs by using the **Test Connection** button for each input and output.</span></span>

2.  <span data-ttu-id="68383-111">檢查您的輸入資料：</span><span class="sxs-lookup"><span data-stu-id="68383-111">Examine your input data:</span></span>
    - <span data-ttu-id="68383-112">若要驗證輸入資料是否正流入事件中樞，請使用[服務匯流排總管](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a)與 Azure 事件中樞連線 (若有使用事件中樞輸入)。</span><span class="sxs-lookup"><span data-stu-id="68383-112">To verify that input data is flowing into Event Hub, use [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) to connect to Azure Event Hub (if Event Hub input is used).</span></span>  
    - <span data-ttu-id="68383-113">針對各個輸入使用 [**範例資料**](stream-analytics-sample-data-input.md) 按鈕，並下載輸入範例資料。</span><span class="sxs-lookup"><span data-stu-id="68383-113">Use the [**Sample Data**](stream-analytics-sample-data-input.md) button for each input, and download the input sample data.</span></span>
    - <span data-ttu-id="68383-114">檢查範例資料以了解資料形式︰結構描述和[資料類型](https://msdn.microsoft.com/library/azure/dn835065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="68383-114">Inspect the sample data to understand the shape of the data: the schema and the [data types](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

3.  <span data-ttu-id="68383-115">測試查詢︰</span><span class="sxs-lookup"><span data-stu-id="68383-115">Test your query:</span></span>
    - <span data-ttu-id="68383-116">在 [查詢] 索引標籤中，使用 [測試] 按鈕來測試查詢並使用已下載的範例資料來[測試查詢](stream-analytics-test-query.md)。</span><span class="sxs-lookup"><span data-stu-id="68383-116">On the **Query** tab, use the **Test** button to test the query, and use the downloaded sample data to [test the query](stream-analytics-test-query.md).</span></span> <span data-ttu-id="68383-117">檢查是否有任何錯誤並嘗試修正。</span><span class="sxs-lookup"><span data-stu-id="68383-117">Examine any errors and attempt to correct them.</span></span>
    - <span data-ttu-id="68383-118">如果您使用 [**Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx)，請確定事件有大於[作業開始時間](stream-analytics-out-of-order-and-late-events.md)的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="68383-118">If you use [**Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), verify that the events have timestamps greater than the [job start time](stream-analytics-out-of-order-and-late-events.md).</span></span>

4.  <span data-ttu-id="68383-119">對應用程式進行偵錯：</span><span class="sxs-lookup"><span data-stu-id="68383-119">Debug your query:</span></span>
    - <span data-ttu-id="68383-120">從簡單的 select 陳述式到需多個步驟且複雜的彙總，以漸進方式重新建置查詢。</span><span class="sxs-lookup"><span data-stu-id="68383-120">Rebuild the query progressively from simple select statement to more complex aggregates by using steps.</span></span> <span data-ttu-id="68383-121">若要逐步建置查詢邏輯，請使用 [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) 子句。</span><span class="sxs-lookup"><span data-stu-id="68383-121">To build up the query logic step by step, use [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) clauses.</span></span>
    - <span data-ttu-id="68383-122">使用 [SELECT INTO](stream-analytics-select-into.md) 對查詢步驟進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="68383-122">Use [SELECT INTO](stream-analytics-select-into.md) to debug query steps.</span></span>

5.  <span data-ttu-id="68383-123">排除常見的錯誤，例如︰</span><span class="sxs-lookup"><span data-stu-id="68383-123">Eliminate common pitfalls, such as:</span></span>
    - <span data-ttu-id="68383-124">查詢中的 [**WHERE**](https://msdn.microsoft.com/library/azure/dn835048.aspx) 子句篩選出所有事件，造成無法產生任何輸出作業。</span><span class="sxs-lookup"><span data-stu-id="68383-124">A [**WHERE**](https://msdn.microsoft.com/library/azure/dn835048.aspx) clause in the query filtered out all events, preventing any output from being generated.</span></span>
    - <span data-ttu-id="68383-125">當您使用視窗函式時，請等候完整的視窗運作時間，以查看查詢的輸出。</span><span class="sxs-lookup"><span data-stu-id="68383-125">When you use window functions, wait for the entire window duration to see an output from the query.</span></span>
    - <span data-ttu-id="68383-126">事件的時間戳記早於作業開始時間，因此事件遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="68383-126">The timestamp for events precedes the job start time and, therefore, events are being dropped.</span></span>

6.  <span data-ttu-id="68383-127">使用事件順序︰</span><span class="sxs-lookup"><span data-stu-id="68383-127">Use event ordering:</span></span>
    - <span data-ttu-id="68383-128">若前述步驟皆運作正常，請移至 [設定] 刀鋒視窗，並選取[**事件排序**](stream-analytics-out-of-order-and-late-events.md)。</span><span class="sxs-lookup"><span data-stu-id="68383-128">If all the previous steps worked fine, go to the **Settings** blade and select [**Event Ordering**](stream-analytics-out-of-order-and-late-events.md).</span></span> <span data-ttu-id="68383-129">請確定此原則已設定為適用於您的情況。</span><span class="sxs-lookup"><span data-stu-id="68383-129">Verify that this policy is configured for what makes sense in your scenario.</span></span> <span data-ttu-id="68383-130">如果您使用 [測試] 按鈕測試查詢，則不會套用原則。</span><span class="sxs-lookup"><span data-stu-id="68383-130">The policy is *not* applied when you use the **Test** button to test the query.</span></span> <span data-ttu-id="68383-131">此結果是在瀏覽器中進行測試與在生產環境中執行作業之間的一個差異。</span><span class="sxs-lookup"><span data-stu-id="68383-131">This result is one difference between testing in-browser versus running the job in production.</span></span>

7.  <span data-ttu-id="68383-132">使用計量進行偵錯：</span><span class="sxs-lookup"><span data-stu-id="68383-132">Debug by using metrics:</span></span>
    - <span data-ttu-id="68383-133">若已經過預定的持續時間 (以查詢為基礎)，而您沒有收到輸出，請嘗試下列方法︰</span><span class="sxs-lookup"><span data-stu-id="68383-133">If you obtain no output after the expected duration (based on the query), try the following:</span></span>
        - <span data-ttu-id="68383-134">請查看 [監視] 索引標籤上的[**監視計量**](stream-analytics-monitoring.md)。因為是彙總值，計量會延遲幾分鐘顯示。</span><span class="sxs-lookup"><span data-stu-id="68383-134">Look at [**Monitoring Metrics**](stream-analytics-monitoring.md) on the **Monitor** tab. Because the values are aggregated, the metrics are delayed by a few minutes.</span></span>
            - <span data-ttu-id="68383-135">若輸入事件 > 0，則作業可以讀取輸入資料。</span><span class="sxs-lookup"><span data-stu-id="68383-135">If Input Events > 0, the job is able to read input data.</span></span> <span data-ttu-id="68383-136">如果輸入事件不是 > 0，然後︰</span><span class="sxs-lookup"><span data-stu-id="68383-136">If Input Events is not > 0, then:</span></span>
                - <span data-ttu-id="68383-137">若要查看資料來源是否為有效資料，請使用[服務匯流排總管](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a)進行檢查。</span><span class="sxs-lookup"><span data-stu-id="68383-137">To see whether the data source has valid data, check it by using [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a).</span></span> <span data-ttu-id="68383-138">此項檢查適用於使用事件中樞作為輸入的作業。</span><span class="sxs-lookup"><span data-stu-id="68383-138">This check applies if the job is using Event Hub as input.</span></span>
                - <span data-ttu-id="68383-139">請檢查資料序列化格式及資料編碼是否正確。</span><span class="sxs-lookup"><span data-stu-id="68383-139">Check to see whether the data serialization format and data encoding are as expected.</span></span>
                - <span data-ttu-id="68383-140">如果該作業使用事件中樞，請檢查訊息本文是否為 *Null*。</span><span class="sxs-lookup"><span data-stu-id="68383-140">If the job is using an Event Hub, check to see whether the body of the message is *Null*.</span></span>
            - <span data-ttu-id="68383-141">若資料轉換錯誤 > 0 且持續增加中，則可能符合下列情況：</span><span class="sxs-lookup"><span data-stu-id="68383-141">If Data Conversion Errors > 0 and climbing, the following might be true:</span></span>
                - <span data-ttu-id="68383-142">作業可能無法還原序列化事件。</span><span class="sxs-lookup"><span data-stu-id="68383-142">The job might not be able to de-serialize the events.</span></span>
                - <span data-ttu-id="68383-143">事件結構描述可能與查詢中事件的定義或預期結構描述不相符。</span><span class="sxs-lookup"><span data-stu-id="68383-143">The event schema might not match the defined or expected schema of the events in the query.</span></span>
                - <span data-ttu-id="68383-144">事件中某些欄位的資料類型可能不符合預期類型。</span><span class="sxs-lookup"><span data-stu-id="68383-144">The datatypes of some of the fields in the event might not match expectations.</span></span>
            - <span data-ttu-id="68383-145">如果執行階段錯誤 > 0，則表示作業可以接收資料，但在處理查詢時會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="68383-145">If Runtime Errors > 0, it means that the job can receive the data but is generating errors while processing the query.</span></span>
                - <span data-ttu-id="68383-146">若要找出錯誤，請前往[稽核記錄](../azure-resource-manager/resource-group-audit.md)，並篩選*失敗*狀態。</span><span class="sxs-lookup"><span data-stu-id="68383-146">To find the errors, go to the [Audit Logs](../azure-resource-manager/resource-group-audit.md) and filter on *Failed* status.</span></span>
            - <span data-ttu-id="68383-147">如果 InputEvents > 0 且 OutputEvents = 0，則表示符合下列其中一個情況︰</span><span class="sxs-lookup"><span data-stu-id="68383-147">If InputEvents > 0 and OutputEvents = 0, it means that one of the following is true:</span></span>
                - <span data-ttu-id="68383-148">查詢處理產生了零個輸出事件。</span><span class="sxs-lookup"><span data-stu-id="68383-148">Query processing resulted in zero output events.</span></span>
                - <span data-ttu-id="68383-149">事件或其欄位可能格式錯誤，因此在查詢處理後導致零個輸出。</span><span class="sxs-lookup"><span data-stu-id="68383-149">Events or its fields might be malformed, resulting in zero output after query processing.</span></span>
                - <span data-ttu-id="68383-150">由於連線或驗證問題使然，作業無法推送資料至輸出[接收](stream-analytics-select-into.md)。</span><span class="sxs-lookup"><span data-stu-id="68383-150">The job was unable to push data to the [output sink](stream-analytics-select-into.md) for connectivity or authentication reasons.</span></span>
        - <span data-ttu-id="68383-151">在所有前述錯誤案例中，作業記錄訊息說明了其他詳細資料 (包括目前所發生的事)，僅有查詢邏輯篩選掉所有事件的案例除外。</span><span class="sxs-lookup"><span data-stu-id="68383-151">In all the previously mentioned error cases, operations log messages explain additional details (including what is happening), except in cases where the query logic filtered out all events.</span></span> <span data-ttu-id="68383-152">如果多事件處理產生錯誤，串流分析會在 10 分鐘內將同類型的前三個錯誤記錄到作業記錄中。</span><span class="sxs-lookup"><span data-stu-id="68383-152">If the processing of multiple events generates errors, Stream Analytics logs the first three error messages of the same type within 10 minutes to Operations logs.</span></span> <span data-ttu-id="68383-153">接著會隱藏其他完全相同的錯誤並顯示錯誤訊息，內容為「錯誤發生次數太頻繁，因此隱藏這些錯誤」。</span><span class="sxs-lookup"><span data-stu-id="68383-153">It then suppresses additional identical errors with a message that reads “Errors are happening too rapidly, these are being suppressed.”</span></span>

8. <span data-ttu-id="68383-154">使用稽核和診斷記錄進行偵錯：</span><span class="sxs-lookup"><span data-stu-id="68383-154">Debug by using audit and diagnostic logs:</span></span>
    - <span data-ttu-id="68383-155">使用[稽核記錄](../azure-resource-manager/resource-group-audit.md)，並透過篩選找出錯誤並進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="68383-155">Use [Audit Logs](../azure-resource-manager/resource-group-audit.md), and filter to identify and debug errors.</span></span>
    - <span data-ttu-id="68383-156">使用[作業診斷記錄](stream-analytics-job-diagnostic-logs.md)找出錯誤並進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="68383-156">Use [job diagnostic logs](stream-analytics-job-diagnostic-logs.md) to identify and debug errors.</span></span>

9. <span data-ttu-id="68383-157">檢查輸出︰</span><span class="sxs-lookup"><span data-stu-id="68383-157">Examine the outputs:</span></span>
    - <span data-ttu-id="68383-158">當作業狀態為「執行」時，依據查詢中所設定的持續時間而定，您可以在接收資料來源中看到輸出。</span><span class="sxs-lookup"><span data-stu-id="68383-158">When the job status is *Running*, depending on the duration that's stipulated in the query, you can see the output in the sink data source.</span></span>
    - <span data-ttu-id="68383-159">如果您無法看到要傳送至特定輸出類型的輸出，請將其重新導向至較不複雜的類型，例如 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="68383-159">If you cannot see outputs that are going to a specific output type, redirect them to an output type that is less complex, such as an Azure Blob.</span></span> <span data-ttu-id="68383-160">透過使用儲存體總管，您可以查看是否可以看到輸出。</span><span class="sxs-lookup"><span data-stu-id="68383-160">By using Storage Explorer, check to see whether the output can be seen.</span></span> <span data-ttu-id="68383-161">此外，請確定輸出上是否有節流限制阻擋了資料接收。</span><span class="sxs-lookup"><span data-stu-id="68383-161">Additionally, verify whether throttling limits at the output are preventing data from being received.</span></span>

10. <span data-ttu-id="68383-162">搭配使用資料流分析與作業圖表計量︰</span><span class="sxs-lookup"><span data-stu-id="68383-162">Use data-flow analysis with job diagram metrics:</span></span>
    - <span data-ttu-id="68383-163">若要分析資料流程與識別問題，請使用[作業圖表與計量](stream-analytics-job-diagram-with-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="68383-163">To analyze data flow and identify issues, use the [job diagram with metrics](stream-analytics-job-diagram-with-metrics.md).</span></span>

11. <span data-ttu-id="68383-164">建立支援案例：</span><span class="sxs-lookup"><span data-stu-id="68383-164">Open a support case:</span></span>
    - <span data-ttu-id="68383-165">最後，如果所有解決方案均失敗，請使用包含您作業的訂用帳戶識別碼來建立 Microsoft 支援服務案例。</span><span class="sxs-lookup"><span data-stu-id="68383-165">Finally, if all else fails, open a Microsoft support case by using the SubscriptionID that contains your job.</span></span>

## <a name="get-help"></a><span data-ttu-id="68383-166">取得說明</span><span class="sxs-lookup"><span data-stu-id="68383-166">Get help</span></span>

<span data-ttu-id="68383-167">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="68383-167">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68383-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68383-168">Next steps</span></span>

* [<span data-ttu-id="68383-169">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="68383-169">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="68383-170">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="68383-170">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="68383-171">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="68383-171">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="68383-172">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="68383-172">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="68383-173">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="68383-173">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
