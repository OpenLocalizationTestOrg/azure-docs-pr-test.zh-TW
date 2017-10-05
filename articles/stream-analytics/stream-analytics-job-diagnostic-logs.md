---
title: "使用診斷記錄對 Azure 串流分析進行疑難排解 |Microsoft Docs"
description: "了解如何在 Microsoft Azure 中分析串流分析作業的診斷記錄。"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: ea90a62ffee9c766985f76e1c0abc1585bebc69b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a><span data-ttu-id="d1059-103">使用析診斷記錄對 Azure 串流分進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d1059-103">Troubleshoot Azure Stream Analytics by using diagnostics logs</span></span>

<span data-ttu-id="d1059-104">有時候，Azure 串流分析作業會非預期地停止處理。</span><span class="sxs-lookup"><span data-stu-id="d1059-104">Occasionally, an Azure Stream Analytics job unexpectedly stops processing.</span></span> <span data-ttu-id="d1059-105">請務必要設法解決這類事件的問題。</span><span class="sxs-lookup"><span data-stu-id="d1059-105">It's important to be able to troubleshoot this kind of event.</span></span> <span data-ttu-id="d1059-106">事件發生的原因可能是非預期的查詢結果、裝置的連線狀況，或未預期的服務中斷。</span><span class="sxs-lookup"><span data-stu-id="d1059-106">The event might be caused by an unexpected query result, by connectivity to devices, or by an unexpected service outage.</span></span> <span data-ttu-id="d1059-107">串流分析中的診斷記錄可協助您在事件發生當下找出問題原因，並減少復原時間。</span><span class="sxs-lookup"><span data-stu-id="d1059-107">The diagnostics logs in Stream Analytics can help you identify the cause of issues when they occur, and reduce recovery time.</span></span>

## <a name="log-types"></a><span data-ttu-id="d1059-108">記錄類型</span><span class="sxs-lookup"><span data-stu-id="d1059-108">Log types</span></span>

<span data-ttu-id="d1059-109">串流分析提供開兩種記錄類型：</span><span class="sxs-lookup"><span data-stu-id="d1059-109">Stream Analytics offers two types of logs:</span></span> 
* <span data-ttu-id="d1059-110">[活動記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (一律開啟)。</span><span class="sxs-lookup"><span data-stu-id="d1059-110">[Activity logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (always on).</span></span> <span data-ttu-id="d1059-111">活動記錄可讓您對所執行作業有深入的了解。</span><span class="sxs-lookup"><span data-stu-id="d1059-111">Activity logs give insights into operations performed on jobs.</span></span>
* <span data-ttu-id="d1059-112">[診斷記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (可設定)。</span><span class="sxs-lookup"><span data-stu-id="d1059-112">[Diagnostics logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configurable).</span></span> <span data-ttu-id="d1059-113">診斷記錄可讓您更深入地了所有與作業相關的發生事件。</span><span class="sxs-lookup"><span data-stu-id="d1059-113">Diagnostics logs provide richer insights into everything that happens with a job.</span></span> <span data-ttu-id="d1059-114">診斷記錄會在作業建立時開始執行，並在作業刪除時結束。</span><span class="sxs-lookup"><span data-stu-id="d1059-114">Diagnostics logs start when the job is created, and end when the job is deleted.</span></span> <span data-ttu-id="d1059-115">這些記錄涵蓋作業更新時與作業執行時的情形。</span><span class="sxs-lookup"><span data-stu-id="d1059-115">They cover events when the job is updated and while it’s running.</span></span>

> [!NOTE]
> <span data-ttu-id="d1059-116">您可以使用 Azure 儲存體、Azure 事件中樞和 Azure Log Analytics 等服務來分析不一致的資料。</span><span class="sxs-lookup"><span data-stu-id="d1059-116">You can use services like Azure Storage, Azure Event Hubs, and Azure Log Analytics to analyze nonconforming data.</span></span> <span data-ttu-id="d1059-117">這些服務將會依據各自的計價模式向您收取費用。</span><span class="sxs-lookup"><span data-stu-id="d1059-117">You are charged based on the pricing model for those services.</span></span>
>

## <a name="turn-on-diagnostics-logs"></a><span data-ttu-id="d1059-118">開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d1059-118">Turn on diagnostics logs</span></span>

<span data-ttu-id="d1059-119">診斷記錄預設為 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="d1059-119">Diagnostics logs are **off** by default.</span></span> <span data-ttu-id="d1059-120">若要開啟診斷記錄，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="d1059-120">To turn on diagnostics logs, complete these steps:</span></span>

1.  <span data-ttu-id="d1059-121">登入 Azure 入口網站並前往串流作業刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d1059-121">Sign in to the Azure portal, and go to the streaming job blade.</span></span> <span data-ttu-id="d1059-122">在 [監視] 下，選取 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="d1059-122">Under **Monitoring**, select **Diagnostics logs**.</span></span>

    ![瀏覽到診斷記錄的刀鋒視窗](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  <span data-ttu-id="d1059-124">選取 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="d1059-124">Select **Turn on diagnostics**.</span></span>

    ![開啟診斷記錄](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  <span data-ttu-id="d1059-126">在 [診斷設定] 頁面的 [狀態]  上，選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="d1059-126">On the **Diagnostics settings** page, for **Status**, select **On**.</span></span>

    ![變更診斷記錄的狀態](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  <span data-ttu-id="d1059-128">設定封存目標 (儲存體帳戶、事件中樞、Log Analytics)。</span><span class="sxs-lookup"><span data-stu-id="d1059-128">Set up the archival target (storage account, event hub, Log Analytics) that you want.</span></span> <span data-ttu-id="d1059-129">然後選取您要收集的記錄類別 (執行、編寫)。</span><span class="sxs-lookup"><span data-stu-id="d1059-129">Then, select the categories of logs that you want to collect (Execution, Authoring).</span></span> 

5.  <span data-ttu-id="d1059-130">儲存新的診斷組態。</span><span class="sxs-lookup"><span data-stu-id="d1059-130">Save the new diagnostics configuration.</span></span>

<span data-ttu-id="d1059-131">設定診斷大約需要 10 分鐘才會生效。</span><span class="sxs-lookup"><span data-stu-id="d1059-131">The diagnostics configuration takes about 10 minutes to take effect.</span></span> <span data-ttu-id="d1059-132">之後，記錄會開始出現在設定的封存目標中 (您可以在 [診斷記錄]頁面中看到這些記錄)：</span><span class="sxs-lookup"><span data-stu-id="d1059-132">After that, the logs start appearing in the configured archival target (you can see these on the **Diagnostics logs** page):</span></span>

![瀏覽到診斷記錄的刀鋒視窗 - 封存目標](./media/stream-analytics-job-diagnostic-logs/image4.png)

<span data-ttu-id="d1059-134">如需有關診斷設定的詳細資訊，請參閱[收集並取用來自 Azure 資源的診斷資料](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)。</span><span class="sxs-lookup"><span data-stu-id="d1059-134">For more information about configuring diagnostics, see [Collect and consume diagnostics data from your Azure resources](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).</span></span>

## <a name="diagnostics-log-categories"></a><span data-ttu-id="d1059-135">診斷記錄類別</span><span class="sxs-lookup"><span data-stu-id="d1059-135">Diagnostics log categories</span></span>

<span data-ttu-id="d1059-136">我們目前會擷取兩種診斷記錄︰</span><span class="sxs-lookup"><span data-stu-id="d1059-136">Currently, we capture two categories of diagnostics logs:</span></span>

* <span data-ttu-id="d1059-137">**編寫**。</span><span class="sxs-lookup"><span data-stu-id="d1059-137">**Authoring**.</span></span> <span data-ttu-id="d1059-138">擷取作業編寫相關記錄：作業建立、新增及刪除輸入與輸出、新增及更新查詢、開始及停止作業。</span><span class="sxs-lookup"><span data-stu-id="d1059-138">Captures log events that are related to job authoring operations: job creation, adding and deleting inputs and outputs, adding and updating the query, starting and stopping the job.</span></span>
* <span data-ttu-id="d1059-139">**執行**。</span><span class="sxs-lookup"><span data-stu-id="d1059-139">**Execution**.</span></span> <span data-ttu-id="d1059-140">擷取作業執行期間發生的事件︰</span><span class="sxs-lookup"><span data-stu-id="d1059-140">Captures events that occur during job execution:</span></span>
    * <span data-ttu-id="d1059-141">連線錯誤</span><span class="sxs-lookup"><span data-stu-id="d1059-141">Connectivity errors</span></span>
    * <span data-ttu-id="d1059-142">資料處理錯誤，包括：</span><span class="sxs-lookup"><span data-stu-id="d1059-142">Data processing errors, including:</span></span>
        * <span data-ttu-id="d1059-143">不符合查詢定義的事件 (不相符的欄位類型與值或遺漏欄位等)</span><span class="sxs-lookup"><span data-stu-id="d1059-143">Events that don’t conform to the query definition (mismatched field types and values, missing fields, and so on)</span></span>
        * <span data-ttu-id="d1059-144">運算式評估錯誤</span><span class="sxs-lookup"><span data-stu-id="d1059-144">Expression evaluation errors</span></span>
    * <span data-ttu-id="d1059-145">其他事件和錯誤</span><span class="sxs-lookup"><span data-stu-id="d1059-145">Other events and errors</span></span>

## <a name="diagnostics-logs-schema"></a><span data-ttu-id="d1059-146">診斷記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="d1059-146">Diagnostics logs schema</span></span>

<span data-ttu-id="d1059-147">所有記錄會儲存為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="d1059-147">All logs are stored in JSON format.</span></span> <span data-ttu-id="d1059-148">每個項目皆包含下列常見的字串欄位︰</span><span class="sxs-lookup"><span data-stu-id="d1059-148">Each entry has the following common string fields:</span></span>

<span data-ttu-id="d1059-149">名稱</span><span class="sxs-lookup"><span data-stu-id="d1059-149">Name</span></span> | <span data-ttu-id="d1059-150">說明</span><span class="sxs-lookup"><span data-stu-id="d1059-150">Description</span></span>
------- | -------
<span data-ttu-id="d1059-151">分析</span><span class="sxs-lookup"><span data-stu-id="d1059-151">time</span></span> | <span data-ttu-id="d1059-152">記錄的時間戳記 (UTC 時間)。</span><span class="sxs-lookup"><span data-stu-id="d1059-152">Timestamp (in UTC) of the log.</span></span>
<span data-ttu-id="d1059-153">resourceId</span><span class="sxs-lookup"><span data-stu-id="d1059-153">resourceId</span></span> | <span data-ttu-id="d1059-154">作業執行資源的識別碼 (大寫)。</span><span class="sxs-lookup"><span data-stu-id="d1059-154">ID of the resource that the operation took place on, in upper case.</span></span> <span data-ttu-id="d1059-155">其中包含訂用帳戶識別碼、資源群組，以及作業名稱。</span><span class="sxs-lookup"><span data-stu-id="d1059-155">It includes the subscription ID, the resource group, and the job name.</span></span> <span data-ttu-id="d1059-156">例如，**/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**。</span><span class="sxs-lookup"><span data-stu-id="d1059-156">For example, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.</span></span>
<span data-ttu-id="d1059-157">category</span><span class="sxs-lookup"><span data-stu-id="d1059-157">category</span></span> | <span data-ttu-id="d1059-158">記錄類別 (**執行**或**編寫**)。</span><span class="sxs-lookup"><span data-stu-id="d1059-158">Log category, either **Execution** or **Authoring**.</span></span>
<span data-ttu-id="d1059-159">operationName</span><span class="sxs-lookup"><span data-stu-id="d1059-159">operationName</span></span> | <span data-ttu-id="d1059-160">記錄的作業名稱。</span><span class="sxs-lookup"><span data-stu-id="d1059-160">Name of the operation that is logged.</span></span> <span data-ttu-id="d1059-161">例如，**傳送事件︰SQL 輸出將失敗寫入 mysqloutput**。</span><span class="sxs-lookup"><span data-stu-id="d1059-161">For example, **Send Events: SQL Output write failure to mysqloutput**.</span></span>
<span data-ttu-id="d1059-162">status</span><span class="sxs-lookup"><span data-stu-id="d1059-162">status</span></span> | <span data-ttu-id="d1059-163">作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="d1059-163">Status of the operation.</span></span> <span data-ttu-id="d1059-164">例如，**失敗**或**成功**。</span><span class="sxs-lookup"><span data-stu-id="d1059-164">For example, **Failed** or **Succeeded**.</span></span>
<span data-ttu-id="d1059-165">層級</span><span class="sxs-lookup"><span data-stu-id="d1059-165">level</span></span> | <span data-ttu-id="d1059-166">記錄層級。</span><span class="sxs-lookup"><span data-stu-id="d1059-166">Log level.</span></span> <span data-ttu-id="d1059-167">例如，**錯誤**、**警告**或**資訊**。</span><span class="sxs-lookup"><span data-stu-id="d1059-167">For example, **Error**, **Warning**, or **Informational**.</span></span>
<span data-ttu-id="d1059-168">屬性</span><span class="sxs-lookup"><span data-stu-id="d1059-168">properties</span></span> | <span data-ttu-id="d1059-169">記錄項目特定詳細資料 (序列化為 JSON 字串)。</span><span class="sxs-lookup"><span data-stu-id="d1059-169">Log entry-specific detail, serialized as a JSON string.</span></span> <span data-ttu-id="d1059-170">如需詳細資訊，請參閱下列幾節。</span><span class="sxs-lookup"><span data-stu-id="d1059-170">For more information, see the following sections.</span></span>

### <a name="execution-log-properties-schema"></a><span data-ttu-id="d1059-171">執行記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="d1059-171">Execution log properties schema</span></span>

<span data-ttu-id="d1059-172">執行記錄包含在執行串流分析作業期間所發生事件的資訊。</span><span class="sxs-lookup"><span data-stu-id="d1059-172">Execution logs have information about events that happened during Stream Analytics job execution.</span></span> <span data-ttu-id="d1059-173">屬性結構描述會根據事件類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="d1059-173">The schema of properties varies, depending on the type of event.</span></span> <span data-ttu-id="d1059-174">我們目前有下列類型的執行記錄︰</span><span class="sxs-lookup"><span data-stu-id="d1059-174">Currently, we have the following types of execution logs:</span></span>

### <a name="data-errors"></a><span data-ttu-id="d1059-175">資料錯誤</span><span class="sxs-lookup"><span data-stu-id="d1059-175">Data errors</span></span>

<span data-ttu-id="d1059-176">作業處理資料時發生的任何錯誤皆包含於此類記錄中。</span><span class="sxs-lookup"><span data-stu-id="d1059-176">Any error that occurs while the job is processing data is in this category of logs.</span></span> <span data-ttu-id="d1059-177">這些記錄最常於資料讀取、序列化和寫入作業時建立。</span><span class="sxs-lookup"><span data-stu-id="d1059-177">These logs most often are created during data read, serialization, and write operations.</span></span> <span data-ttu-id="d1059-178">這些記錄不包含連線錯誤。</span><span class="sxs-lookup"><span data-stu-id="d1059-178">These logs do not include connectivity errors.</span></span> <span data-ttu-id="d1059-179">連線錯誤視為一般事件。</span><span class="sxs-lookup"><span data-stu-id="d1059-179">Connectivity errors are treated as generic events.</span></span>

<span data-ttu-id="d1059-180">名稱</span><span class="sxs-lookup"><span data-stu-id="d1059-180">Name</span></span> | <span data-ttu-id="d1059-181">說明</span><span class="sxs-lookup"><span data-stu-id="d1059-181">Description</span></span>
------- | -------
<span data-ttu-id="d1059-182">來源</span><span class="sxs-lookup"><span data-stu-id="d1059-182">Source</span></span> | <span data-ttu-id="d1059-183">發生錯誤的作業輸入或輸出名稱。</span><span class="sxs-lookup"><span data-stu-id="d1059-183">Name of the job input or output where the error occurred.</span></span>
<span data-ttu-id="d1059-184">訊息</span><span class="sxs-lookup"><span data-stu-id="d1059-184">Message</span></span> | <span data-ttu-id="d1059-185">與錯誤相關的訊息。</span><span class="sxs-lookup"><span data-stu-id="d1059-185">Message associated with the error.</span></span>
<span data-ttu-id="d1059-186">類型</span><span class="sxs-lookup"><span data-stu-id="d1059-186">Type</span></span> | <span data-ttu-id="d1059-187">錯誤類型。</span><span class="sxs-lookup"><span data-stu-id="d1059-187">Type of error.</span></span> <span data-ttu-id="d1059-188">例如，**DataConversionError**、**CsvParserError** 或 **ServiceBusPropertyColumnMissingError**。</span><span class="sxs-lookup"><span data-stu-id="d1059-188">For example, **DataConversionError**, **CsvParserError**, or **ServiceBusPropertyColumnMissingError**.</span></span>
<span data-ttu-id="d1059-189">資料</span><span class="sxs-lookup"><span data-stu-id="d1059-189">Data</span></span> | <span data-ttu-id="d1059-190">包含有助於正確找到錯誤來源的資料。</span><span class="sxs-lookup"><span data-stu-id="d1059-190">Contains data that is useful to accurately locate the source of the error.</span></span> <span data-ttu-id="d1059-191">視其大小，資料可能會遭到截斷。</span><span class="sxs-lookup"><span data-stu-id="d1059-191">Subject to truncation, depending on size.</span></span>

<span data-ttu-id="d1059-192">資料錯誤會隨 **operationName** 值的不同而有下列結構描述：</span><span class="sxs-lookup"><span data-stu-id="d1059-192">Depending on the **operationName** value, data errors have the following schema:</span></span>
* <span data-ttu-id="d1059-193">**序列化事件**。</span><span class="sxs-lookup"><span data-stu-id="d1059-193">**Serialize events**.</span></span> <span data-ttu-id="d1059-194">序列化事件會在事件讀取作業期間發生。</span><span class="sxs-lookup"><span data-stu-id="d1059-194">Serialize events occur during event read operations.</span></span> <span data-ttu-id="d1059-195">當輸入上的資料不符合查詢結構描述時就會發生這類事件，發生原因可能是下列其中一個：</span><span class="sxs-lookup"><span data-stu-id="d1059-195">They occur when the data at the input does not satisfy the query schema for one of these reasons:</span></span>
    * <span data-ttu-id="d1059-196">*事件 (還原) 序列化期間類型不相符*：找出造成錯誤的欄位。</span><span class="sxs-lookup"><span data-stu-id="d1059-196">*Type mismatch during event (de)serialize*: Identifies the field that's causing the error.</span></span>
    * <span data-ttu-id="d1059-197">*無法讀取事件，序列化無效*：針對發生錯誤的輸入資料位置列出資訊。</span><span class="sxs-lookup"><span data-stu-id="d1059-197">*Cannot read an event, invalid serialization*: Lists information about the location in the input data where the error occurred.</span></span> <span data-ttu-id="d1059-198">包含 Blob 輸入的 Blob 名稱、位移和資料範例。</span><span class="sxs-lookup"><span data-stu-id="d1059-198">Includes blob name for blob input, offset, and a sample of the data.</span></span>
* <span data-ttu-id="d1059-199">**傳送事件**。</span><span class="sxs-lookup"><span data-stu-id="d1059-199">**Send events**.</span></span> <span data-ttu-id="d1059-200">傳送事件會發生在寫入作業期間。</span><span class="sxs-lookup"><span data-stu-id="d1059-200">Send events occur during write operations.</span></span> <span data-ttu-id="d1059-201">這些事件會識別造成錯誤的串流事件。</span><span class="sxs-lookup"><span data-stu-id="d1059-201">They identify the streaming event that caused the error.</span></span>

### <a name="generic-events"></a><span data-ttu-id="d1059-202">一般事件</span><span class="sxs-lookup"><span data-stu-id="d1059-202">Generic events</span></span>

<span data-ttu-id="d1059-203">一般事件涵蓋所有其他事件。</span><span class="sxs-lookup"><span data-stu-id="d1059-203">Generic events cover everything else.</span></span>

<span data-ttu-id="d1059-204">名稱</span><span class="sxs-lookup"><span data-stu-id="d1059-204">Name</span></span> | <span data-ttu-id="d1059-205">說明</span><span class="sxs-lookup"><span data-stu-id="d1059-205">Description</span></span>
-------- | --------
<span data-ttu-id="d1059-206">錯誤</span><span class="sxs-lookup"><span data-stu-id="d1059-206">Error</span></span> | <span data-ttu-id="d1059-207">(選用) 錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="d1059-207">(optional) Error information.</span></span> <span data-ttu-id="d1059-208">這通常是例外狀況資訊 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="d1059-208">Usually, this is exception information, if it's available.</span></span>
<span data-ttu-id="d1059-209">訊息</span><span class="sxs-lookup"><span data-stu-id="d1059-209">Message</span></span>| <span data-ttu-id="d1059-210">記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="d1059-210">Log message.</span></span>
<span data-ttu-id="d1059-211">類型</span><span class="sxs-lookup"><span data-stu-id="d1059-211">Type</span></span> | <span data-ttu-id="d1059-212">訊息類型。</span><span class="sxs-lookup"><span data-stu-id="d1059-212">Type of message.</span></span> <span data-ttu-id="d1059-213">對應至錯誤的內部分類。</span><span class="sxs-lookup"><span data-stu-id="d1059-213">Maps to internal categorization of errors.</span></span> <span data-ttu-id="d1059-214">例如，**JobValidationError**或 **BlobOutputAdapterInitializationFailure**。</span><span class="sxs-lookup"><span data-stu-id="d1059-214">For example, **JobValidationError** or **BlobOutputAdapterInitializationFailure**.</span></span>
<span data-ttu-id="d1059-215">相互關連識別碼</span><span class="sxs-lookup"><span data-stu-id="d1059-215">Correlation ID</span></span> | <span data-ttu-id="d1059-216">唯一識別作業執行的 [GUID (英文)](https://en.wikipedia.org/wiki/Universally_unique_identifier)。</span><span class="sxs-lookup"><span data-stu-id="d1059-216">[GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) that uniquely identifies the job execution.</span></span> <span data-ttu-id="d1059-217">從作業開始直到作業停止的所有執行記錄項目皆具有同一個**相互關聯識別碼**值。</span><span class="sxs-lookup"><span data-stu-id="d1059-217">All execution log entries from the time the job starts until the job stops have the same **Correlation ID** value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1059-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1059-218">Next steps</span></span>

* [<span data-ttu-id="d1059-219">串流分析介紹</span><span class="sxs-lookup"><span data-stu-id="d1059-219">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d1059-220">開始使用串流分析</span><span class="sxs-lookup"><span data-stu-id="d1059-220">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d1059-221">調整串流分析作業</span><span class="sxs-lookup"><span data-stu-id="d1059-221">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d1059-222">串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="d1059-222">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d1059-223">串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="d1059-223">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
