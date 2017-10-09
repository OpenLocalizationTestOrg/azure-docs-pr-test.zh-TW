---
title: "Azure Stream Analytics 的 aaaTroubleshooting 指南 |Microsoft 文件"
description: "如何 tootroubleshoot 串流分析工作"
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
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a><span data-ttu-id="18655-104">Azure 串流分析的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="18655-104">Troubleshooting guide for Azure Stream Analytics</span></span>

<span data-ttu-id="18655-105">Azure Stream Analytics 疑難排解可能會出現 toobe 複雜工作第一眼看起來。</span><span class="sxs-lookup"><span data-stu-id="18655-105">Azure Stream Analytics troubleshooting can appear toobe a complex effort at first glance.</span></span> <span data-ttu-id="18655-106">之後使用許多使用者，我們已建立此指南 toohelp 簡化 hello 程序，並移除 hello 猜測有關輸入、 輸出、 查詢和函式。</span><span class="sxs-lookup"><span data-stu-id="18655-106">After working with many users, we have created this guide toohelp streamline hello process and remove hello guesswork about your inputs, outputs, queries, and functions.</span></span>

## <a name="troubleshoot-your-stream-analytics-job"></a><span data-ttu-id="18655-107">對您的串流分析作業進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="18655-107">Troubleshoot your Stream Analytics job</span></span>

<span data-ttu-id="18655-108">疑難排解資料流分析工作的最佳結果，請使用下列指導方針的 hello:</span><span class="sxs-lookup"><span data-stu-id="18655-108">For best results in troubleshooting your Stream Analytics job, use hello following guidelines:</span></span>

1.  <span data-ttu-id="18655-109">測試連線：</span><span class="sxs-lookup"><span data-stu-id="18655-109">Test your connectivity:</span></span>
    - <span data-ttu-id="18655-110">請確認連線 tooinputs 和輸出使用 hello**測試連接**針對每個輸入及輸出 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18655-110">Verify connectivity tooinputs and outputs by using hello **Test Connection** button for each input and output.</span></span>

2.  <span data-ttu-id="18655-111">檢查您的輸入資料：</span><span class="sxs-lookup"><span data-stu-id="18655-111">Examine your input data:</span></span>
    - <span data-ttu-id="18655-112">輸入資料的 tooverify 流入事件中樞，請使用[Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure 事件中心 （如果使用事件中樞輸入）。</span><span class="sxs-lookup"><span data-stu-id="18655-112">tooverify that input data is flowing into Event Hub, use [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure Event Hub (if Event Hub input is used).</span></span>  
    - <span data-ttu-id="18655-113">使用 hello [**範例資料**](stream-analytics-sample-data-input.md)按鈕的每個輸入，並下載 hello 輸入的範例資料。</span><span class="sxs-lookup"><span data-stu-id="18655-113">Use hello [**Sample Data**](stream-analytics-sample-data-input.md) button for each input, and download hello input sample data.</span></span>
    - <span data-ttu-id="18655-114">檢查 hello 範例資料 toounderstand hello hello 資料圖形： hello 結構描述和 hello[資料型別](https://msdn.microsoft.com/library/azure/dn835065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="18655-114">Inspect hello sample data toounderstand hello shape of hello data: hello schema and hello [data types](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

3.  <span data-ttu-id="18655-115">測試查詢︰</span><span class="sxs-lookup"><span data-stu-id="18655-115">Test your query:</span></span>
    - <span data-ttu-id="18655-116">在 hello**查詢**索引標籤上，使用 hello**測試**按鈕 tootest hello 查詢，並使用下載的 hello 範例資料太[測試 hello 查詢](stream-analytics-test-query.md)。</span><span class="sxs-lookup"><span data-stu-id="18655-116">On hello **Query** tab, use hello **Test** button tootest hello query, and use hello downloaded sample data too[test hello query](stream-analytics-test-query.md).</span></span> <span data-ttu-id="18655-117">檢查任何錯誤，並嘗試 toocorrect 它們。</span><span class="sxs-lookup"><span data-stu-id="18655-117">Examine any errors and attempt toocorrect them.</span></span>
    - <span data-ttu-id="18655-118">如果您使用[ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx)，請確認 hello 事件有時間戳記大於 hello[工作開始時間](stream-analytics-out-of-order-and-late-events.md)。</span><span class="sxs-lookup"><span data-stu-id="18655-118">If you use [**Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), verify that hello events have timestamps greater than hello [job start time](stream-analytics-out-of-order-and-late-events.md).</span></span>

4.  <span data-ttu-id="18655-119">對應用程式進行偵錯：</span><span class="sxs-lookup"><span data-stu-id="18655-119">Debug your query:</span></span>
    - <span data-ttu-id="18655-120">使用步驟重建 hello 逐漸從簡單的 select 陳述式 toomore 複雜的彙總的查詢。</span><span class="sxs-lookup"><span data-stu-id="18655-120">Rebuild hello query progressively from simple select statement toomore complex aggregates by using steps.</span></span> <span data-ttu-id="18655-121">toobuild 向上 hello 查詢邏輯逐步解說，使用[WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx)子句。</span><span class="sxs-lookup"><span data-stu-id="18655-121">toobuild up hello query logic step by step, use [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) clauses.</span></span>
    - <span data-ttu-id="18655-122">使用[SELECT INTO](stream-analytics-select-into.md) toodebug 查詢步驟。</span><span class="sxs-lookup"><span data-stu-id="18655-122">Use [SELECT INTO](stream-analytics-select-into.md) toodebug query steps.</span></span>

5.  <span data-ttu-id="18655-123">排除常見的錯誤，例如︰</span><span class="sxs-lookup"><span data-stu-id="18655-123">Eliminate common pitfalls, such as:</span></span>
    - <span data-ttu-id="18655-124">A [**其中**](https://msdn.microsoft.com/library/azure/dn835048.aspx) hello 查詢子句篩選掉所有的事件，防止產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="18655-124">A [**WHERE**](https://msdn.microsoft.com/library/azure/dn835048.aspx) clause in hello query filtered out all events, preventing any output from being generated.</span></span>
    - <span data-ttu-id="18655-125">當您使用視窗函式時，等到 hello 整個視窗持續時間 toosee hello 查詢的輸出。</span><span class="sxs-lookup"><span data-stu-id="18655-125">When you use window functions, wait for hello entire window duration toosee an output from hello query.</span></span>
    - <span data-ttu-id="18655-126">hello 事件時間戳記之前 hello 工作開始時間，因此，正在捨棄事件。</span><span class="sxs-lookup"><span data-stu-id="18655-126">hello timestamp for events precedes hello job start time and, therefore, events are being dropped.</span></span>

6.  <span data-ttu-id="18655-127">使用事件順序︰</span><span class="sxs-lookup"><span data-stu-id="18655-127">Use event ordering:</span></span>
    - <span data-ttu-id="18655-128">如果所有 hello 可以正常運作的上一個步驟，請移至 toohello**設定**刀鋒視窗，然後選取[**事件順序**](stream-analytics-out-of-order-and-late-events.md)。</span><span class="sxs-lookup"><span data-stu-id="18655-128">If all hello previous steps worked fine, go toohello **Settings** blade and select [**Event Ordering**](stream-analytics-out-of-order-and-late-events.md).</span></span> <span data-ttu-id="18655-129">請確定此原則已設定為適用於您的情況。</span><span class="sxs-lookup"><span data-stu-id="18655-129">Verify that this policy is configured for what makes sense in your scenario.</span></span> <span data-ttu-id="18655-130">hello 原則是*不*時使用 hello 套用**測試**按鈕 tootest hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="18655-130">hello policy is *not* applied when you use hello **Test** button tootest hello query.</span></span> <span data-ttu-id="18655-131">這個結果會測試在瀏覽器與生產環境中執行 hello 工作之間的差異。</span><span class="sxs-lookup"><span data-stu-id="18655-131">This result is one difference between testing in-browser versus running hello job in production.</span></span>

7.  <span data-ttu-id="18655-132">使用計量進行偵錯：</span><span class="sxs-lookup"><span data-stu-id="18655-132">Debug by using metrics:</span></span>
    - <span data-ttu-id="18655-133">如果 hello 預期的持續時間 （根據 hello 查詢） 之後，您會不取得任何輸出，請嘗試下列 hello:</span><span class="sxs-lookup"><span data-stu-id="18655-133">If you obtain no output after hello expected duration (based on hello query), try hello following:</span></span>
        - <span data-ttu-id="18655-134">查看[**監視度量**](stream-analytics-monitoring.md)上 hello**監視器** 索引標籤。Hello 值會彙總，因為 hello 度量會延遲幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="18655-134">Look at [**Monitoring Metrics**](stream-analytics-monitoring.md) on hello **Monitor** tab. Because hello values are aggregated, hello metrics are delayed by a few minutes.</span></span>
            - <span data-ttu-id="18655-135">如果輸入事件 > 0，hello 作業是無法 tooread 輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="18655-135">If Input Events > 0, hello job is able tooread input data.</span></span> <span data-ttu-id="18655-136">如果輸入事件不是 > 0，然後︰</span><span class="sxs-lookup"><span data-stu-id="18655-136">If Input Events is not > 0, then:</span></span>
                - <span data-ttu-id="18655-137">toosee hello 資料來源是否為有效的資料，請檢查它使用[Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a)。</span><span class="sxs-lookup"><span data-stu-id="18655-137">toosee whether hello data source has valid data, check it by using [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a).</span></span> <span data-ttu-id="18655-138">如果 hello 作業使用事件中心做為輸入，適用於這項檢查。</span><span class="sxs-lookup"><span data-stu-id="18655-138">This check applies if hello job is using Event Hub as input.</span></span>
                - <span data-ttu-id="18655-139">檢查 toosee hello 資料序列化格式資料的編碼方式並不會如預期般。</span><span class="sxs-lookup"><span data-stu-id="18655-139">Check toosee whether hello data serialization format and data encoding are as expected.</span></span>
                - <span data-ttu-id="18655-140">如果 hello 作業使用事件中心，請檢查 toosee hello hello 訊息本文是否*Null*。</span><span class="sxs-lookup"><span data-stu-id="18655-140">If hello job is using an Event Hub, check toosee whether hello body of hello message is *Null*.</span></span>
            - <span data-ttu-id="18655-141">如果資料轉換錯誤 > 0，上升 hello 下列條件可能會為 true:</span><span class="sxs-lookup"><span data-stu-id="18655-141">If Data Conversion Errors > 0 and climbing, hello following might be true:</span></span>
                - <span data-ttu-id="18655-142">hello 作業可能不是能 toode-序列化 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="18655-142">hello job might not be able toode-serialize hello events.</span></span>
                - <span data-ttu-id="18655-143">hello 事件結構描述可能不符合定義的 hello 或預期的結構描述的 hello hello 查詢中的事件。</span><span class="sxs-lookup"><span data-stu-id="18655-143">hello event schema might not match hello defined or expected schema of hello events in hello query.</span></span>
                - <span data-ttu-id="18655-144">hello 的一些 hello 事件中的 hello 欄位的資料類型可能不符合預期。</span><span class="sxs-lookup"><span data-stu-id="18655-144">hello datatypes of some of hello fields in hello event might not match expectations.</span></span>
            - <span data-ttu-id="18655-145">如果執行階段錯誤 > 0，這表示該 hello 工作可以接收 hello 資料，但處理 hello 查詢時產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="18655-145">If Runtime Errors > 0, it means that hello job can receive hello data but is generating errors while processing hello query.</span></span>
                - <span data-ttu-id="18655-146">toofind hello 錯誤，請移 toohello[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)和篩選*失敗*狀態。</span><span class="sxs-lookup"><span data-stu-id="18655-146">toofind hello errors, go toohello [Audit Logs](../azure-resource-manager/resource-group-audit.md) and filter on *Failed* status.</span></span>
            - <span data-ttu-id="18655-147">如果 InputEvents > 0 和 OutputEvents = 0，則表示 hello 下列其中一項成立：</span><span class="sxs-lookup"><span data-stu-id="18655-147">If InputEvents > 0 and OutputEvents = 0, it means that one of hello following is true:</span></span>
                - <span data-ttu-id="18655-148">查詢處理產生了零個輸出事件。</span><span class="sxs-lookup"><span data-stu-id="18655-148">Query processing resulted in zero output events.</span></span>
                - <span data-ttu-id="18655-149">事件或其欄位可能格式錯誤，因此在查詢處理後導致零個輸出。</span><span class="sxs-lookup"><span data-stu-id="18655-149">Events or its fields might be malformed, resulting in zero output after query processing.</span></span>
                - <span data-ttu-id="18655-150">hello 工作已無法 toopush 資料 toohello[輸出接收](stream-analytics-select-into.md)連線或驗證的原因。</span><span class="sxs-lookup"><span data-stu-id="18655-150">hello job was unable toopush data toohello [output sink](stream-analytics-select-into.md) for connectivity or authentication reasons.</span></span>
        - <span data-ttu-id="18655-151">在所有 hello 先前所述錯誤情況下，作業記錄檔訊息的說明 （包括發生什麼事，） 的其他詳細資料的情況下 hello 查詢邏輯篩除的所有事件除外。</span><span class="sxs-lookup"><span data-stu-id="18655-151">In all hello previously mentioned error cases, operations log messages explain additional details (including what is happening), except in cases where hello query logic filtered out all events.</span></span> <span data-ttu-id="18655-152">如果多個事件的 hello 處理產生錯誤，記錄資料流分析記錄檔 hello 的 hello 相同的型別 tooOperations 10 分鐘內的前三個錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="18655-152">If hello processing of multiple events generates errors, Stream Analytics logs hello first three error messages of hello same type within 10 minutes tooOperations logs.</span></span> <span data-ttu-id="18655-153">接著會隱藏其他完全相同的錯誤並顯示錯誤訊息，內容為「錯誤發生次數太頻繁，因此隱藏這些錯誤」。</span><span class="sxs-lookup"><span data-stu-id="18655-153">It then suppresses additional identical errors with a message that reads “Errors are happening too rapidly, these are being suppressed.”</span></span>

8. <span data-ttu-id="18655-154">使用稽核和診斷記錄進行偵錯：</span><span class="sxs-lookup"><span data-stu-id="18655-154">Debug by using audit and diagnostic logs:</span></span>
    - <span data-ttu-id="18655-155">使用[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)，以及篩選 tooidentify 和偵錯錯誤。</span><span class="sxs-lookup"><span data-stu-id="18655-155">Use [Audit Logs](../azure-resource-manager/resource-group-audit.md), and filter tooidentify and debug errors.</span></span>
    - <span data-ttu-id="18655-156">使用[作業診斷記錄](stream-analytics-job-diagnostic-logs.md)tooidentify 和偵錯錯誤。</span><span class="sxs-lookup"><span data-stu-id="18655-156">Use [job diagnostic logs](stream-analytics-job-diagnostic-logs.md) tooidentify and debug errors.</span></span>

9. <span data-ttu-id="18655-157">檢查有 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="18655-157">Examine hello outputs:</span></span>
    - <span data-ttu-id="18655-158">Hello 工作狀態時*執行*，端視在 hello 查詢中，您可以看到 hello 接收資料來源中的 hello 輸出約定的 hello 持續時間。</span><span class="sxs-lookup"><span data-stu-id="18655-158">When hello job status is *Running*, depending on hello duration that's stipulated in hello query, you can see hello output in hello sink data source.</span></span>
    - <span data-ttu-id="18655-159">如果看不到要 tooa 特定的輸出類型的輸出，將他們重新導向 tooan 較不複雜，例如 Azure Blob 的輸出類型。</span><span class="sxs-lookup"><span data-stu-id="18655-159">If you cannot see outputs that are going tooa specific output type, redirect them tooan output type that is less complex, such as an Azure Blob.</span></span> <span data-ttu-id="18655-160">藉由使用儲存體總管，檢查 toosee 是否可以看見 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="18655-160">By using Storage Explorer, check toosee whether hello output can be seen.</span></span> <span data-ttu-id="18655-161">此外，確認是否在 hello 輸出節流限制防止資料被接收。</span><span class="sxs-lookup"><span data-stu-id="18655-161">Additionally, verify whether throttling limits at hello output are preventing data from being received.</span></span>

10. <span data-ttu-id="18655-162">搭配使用資料流分析與作業圖表計量︰</span><span class="sxs-lookup"><span data-stu-id="18655-162">Use data-flow analysis with job diagram metrics:</span></span>
    - <span data-ttu-id="18655-163">tooanalyze 資料流動，且找出問題，使用 hello[具有度量的作業圖表](stream-analytics-job-diagram-with-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="18655-163">tooanalyze data flow and identify issues, use hello [job diagram with metrics](stream-analytics-job-diagram-with-metrics.md).</span></span>

11. <span data-ttu-id="18655-164">建立支援案例：</span><span class="sxs-lookup"><span data-stu-id="18655-164">Open a support case:</span></span>
    - <span data-ttu-id="18655-165">最後，如果所有解決方案均失敗，請開啟 Microsoft 支援案例使用 hello 訂用帳戶 Id，其中包含您的工作。</span><span class="sxs-lookup"><span data-stu-id="18655-165">Finally, if all else fails, open a Microsoft support case by using hello SubscriptionID that contains your job.</span></span>

## <a name="get-help"></a><span data-ttu-id="18655-166">取得說明</span><span class="sxs-lookup"><span data-stu-id="18655-166">Get help</span></span>

<span data-ttu-id="18655-167">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="18655-167">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18655-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18655-168">Next steps</span></span>

* [<span data-ttu-id="18655-169">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="18655-169">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="18655-170">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="18655-170">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="18655-171">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="18655-171">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="18655-172">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="18655-172">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="18655-173">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="18655-173">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
