---
title: "與診斷記錄檔的 Azure Stream Analytics aaaTroubleshoot |Microsoft 文件"
description: "了解 tooanalyze 診斷記錄的方式從資料流分析作業在 Microsoft Azure 中。"
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
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a><span data-ttu-id="2c7ce-103">使用析診斷記錄對 Azure 串流分進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2c7ce-103">Troubleshoot Azure Stream Analytics by using diagnostics logs</span></span>

<span data-ttu-id="2c7ce-104">有時候，Azure 串流分析作業會非預期地停止處理。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-104">Occasionally, an Azure Stream Analytics job unexpectedly stops processing.</span></span> <span data-ttu-id="2c7ce-105">很重要的 toobe 無法 tootroubleshoot 這種事件。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-105">It's important toobe able tootroubleshoot this kind of event.</span></span> <span data-ttu-id="2c7ce-106">hello 事件的原因可能是未預期的查詢結果、 連線 toodevices 或發生未預期的服務中斷。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-106">hello event might be caused by an unexpected query result, by connectivity toodevices, or by an unexpected service outage.</span></span> <span data-ttu-id="2c7ce-107">hello 在 Stream Analytics 中診斷記錄檔可協助您找出問題 hello 原因，當發生，而減少復原時間。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-107">hello diagnostics logs in Stream Analytics can help you identify hello cause of issues when they occur, and reduce recovery time.</span></span>

## <a name="log-types"></a><span data-ttu-id="2c7ce-108">記錄類型</span><span class="sxs-lookup"><span data-stu-id="2c7ce-108">Log types</span></span>

<span data-ttu-id="2c7ce-109">串流分析提供開兩種記錄類型：</span><span class="sxs-lookup"><span data-stu-id="2c7ce-109">Stream Analytics offers two types of logs:</span></span> 
* <span data-ttu-id="2c7ce-110">[活動記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (一律開啟)。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-110">[Activity logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (always on).</span></span> <span data-ttu-id="2c7ce-111">活動記錄可讓您對所執行作業有深入的了解。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-111">Activity logs give insights into operations performed on jobs.</span></span>
* <span data-ttu-id="2c7ce-112">[診斷記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (可設定)。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-112">[Diagnostics logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configurable).</span></span> <span data-ttu-id="2c7ce-113">診斷記錄可讓您更深入地了所有與作業相關的發生事件。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-113">Diagnostics logs provide richer insights into everything that happens with a job.</span></span> <span data-ttu-id="2c7ce-114">診斷記錄建立 hello 作業時，開始和結束時刪除 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-114">Diagnostics logs start when hello job is created, and end when hello job is deleted.</span></span> <span data-ttu-id="2c7ce-115">它們所涵蓋事件 hello 作業更新時以及它正在執行。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-115">They cover events when hello job is updated and while it’s running.</span></span>

> [!NOTE]
> <span data-ttu-id="2c7ce-116">您可以使用服務，例如 Azure 儲存體、 Azure 事件中樞和 Azure Log Analytics tooanalyze 不合格資料。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-116">You can use services like Azure Storage, Azure Event Hubs, and Azure Log Analytics tooanalyze nonconforming data.</span></span> <span data-ttu-id="2c7ce-117">您負責根據 hello 定價模型針對這些服務。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-117">You are charged based on hello pricing model for those services.</span></span>
>

## <a name="turn-on-diagnostics-logs"></a><span data-ttu-id="2c7ce-118">開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="2c7ce-118">Turn on diagnostics logs</span></span>

<span data-ttu-id="2c7ce-119">診斷記錄預設為 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-119">Diagnostics logs are **off** by default.</span></span> <span data-ttu-id="2c7ce-120">tooturn 診斷記錄檔，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2c7ce-120">tooturn on diagnostics logs, complete these steps:</span></span>

1.  <span data-ttu-id="2c7ce-121">登入 toohello Azure 入口網站，並移 toohello 串流處理作業 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-121">Sign in toohello Azure portal, and go toohello streaming job blade.</span></span> <span data-ttu-id="2c7ce-122">在 [監視] 下，選取 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-122">Under **Monitoring**, select **Diagnostics logs**.</span></span>

    ![刀鋒視窗中瀏覽 toodiagnostics 記錄檔](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  <span data-ttu-id="2c7ce-124">選取 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-124">Select **Turn on diagnostics**.</span></span>

    ![開啟診斷記錄](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  <span data-ttu-id="2c7ce-126">在 hello**診斷設定** 頁面上，針對**狀態**，選取**上**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-126">On hello **Diagnostics settings** page, for **Status**, select **On**.</span></span>

    ![變更診斷記錄的狀態](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  <span data-ttu-id="2c7ce-128">Hello 封存目標 （儲存體帳戶，事件中心，記錄分析） 您想要的設定。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-128">Set up hello archival target (storage account, event hub, Log Analytics) that you want.</span></span> <span data-ttu-id="2c7ce-129">然後，選取您想 toocollect （執行、 撰寫） 的記錄檔的 hello 類別。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-129">Then, select hello categories of logs that you want toocollect (Execution, Authoring).</span></span> 

5.  <span data-ttu-id="2c7ce-130">儲存 hello 新的診斷組態。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-130">Save hello new diagnostics configuration.</span></span>

<span data-ttu-id="2c7ce-131">hello 診斷組態才會大約 10 分鐘 tootake 生效。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-131">hello diagnostics configuration takes about 10 minutes tootake effect.</span></span> <span data-ttu-id="2c7ce-132">在這之後，hello 記錄開始出現在設定的 hello 保存目標 (您可以看到這些 hello**診斷記錄檔**頁面):</span><span class="sxs-lookup"><span data-stu-id="2c7ce-132">After that, hello logs start appearing in hello configured archival target (you can see these on hello **Diagnostics logs** page):</span></span>

![刀鋒視窗中瀏覽 toodiagnostics 記錄保存的目標](./media/stream-analytics-job-diagnostic-logs/image4.png)

<span data-ttu-id="2c7ce-134">如需有關診斷設定的詳細資訊，請參閱[收集並取用來自 Azure 資源的診斷資料](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-134">For more information about configuring diagnostics, see [Collect and consume diagnostics data from your Azure resources](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).</span></span>

## <a name="diagnostics-log-categories"></a><span data-ttu-id="2c7ce-135">診斷記錄類別</span><span class="sxs-lookup"><span data-stu-id="2c7ce-135">Diagnostics log categories</span></span>

<span data-ttu-id="2c7ce-136">我們目前會擷取兩種診斷記錄︰</span><span class="sxs-lookup"><span data-stu-id="2c7ce-136">Currently, we capture two categories of diagnostics logs:</span></span>

* <span data-ttu-id="2c7ce-137">**編寫**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-137">**Authoring**.</span></span> <span data-ttu-id="2c7ce-138">擷取會記錄事件的撰寫作業的相關的 toojob： 建立工作，加入和刪除輸入和輸出，新增和更新 hello 查詢、 啟動和停止 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-138">Captures log events that are related toojob authoring operations: job creation, adding and deleting inputs and outputs, adding and updating hello query, starting and stopping hello job.</span></span>
* <span data-ttu-id="2c7ce-139">**執行**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-139">**Execution**.</span></span> <span data-ttu-id="2c7ce-140">擷取作業執行期間發生的事件︰</span><span class="sxs-lookup"><span data-stu-id="2c7ce-140">Captures events that occur during job execution:</span></span>
    * <span data-ttu-id="2c7ce-141">連線錯誤</span><span class="sxs-lookup"><span data-stu-id="2c7ce-141">Connectivity errors</span></span>
    * <span data-ttu-id="2c7ce-142">資料處理錯誤，包括：</span><span class="sxs-lookup"><span data-stu-id="2c7ce-142">Data processing errors, including:</span></span>
        * <span data-ttu-id="2c7ce-143">事件不符合 toohello 查詢定義 （不相符的欄位類型和值，遺漏的欄位，以及等等）</span><span class="sxs-lookup"><span data-stu-id="2c7ce-143">Events that don’t conform toohello query definition (mismatched field types and values, missing fields, and so on)</span></span>
        * <span data-ttu-id="2c7ce-144">運算式評估錯誤</span><span class="sxs-lookup"><span data-stu-id="2c7ce-144">Expression evaluation errors</span></span>
    * <span data-ttu-id="2c7ce-145">其他事件和錯誤</span><span class="sxs-lookup"><span data-stu-id="2c7ce-145">Other events and errors</span></span>

## <a name="diagnostics-logs-schema"></a><span data-ttu-id="2c7ce-146">診斷記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="2c7ce-146">Diagnostics logs schema</span></span>

<span data-ttu-id="2c7ce-147">所有記錄會儲存為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-147">All logs are stored in JSON format.</span></span> <span data-ttu-id="2c7ce-148">每個項目具有下列共通的字串欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c7ce-148">Each entry has hello following common string fields:</span></span>

<span data-ttu-id="2c7ce-149">名稱</span><span class="sxs-lookup"><span data-stu-id="2c7ce-149">Name</span></span> | <span data-ttu-id="2c7ce-150">說明</span><span class="sxs-lookup"><span data-stu-id="2c7ce-150">Description</span></span>
------- | -------
<span data-ttu-id="2c7ce-151">分析</span><span class="sxs-lookup"><span data-stu-id="2c7ce-151">time</span></span> | <span data-ttu-id="2c7ce-152">時間戳記 （UTC) 的 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-152">Timestamp (in UTC) of hello log.</span></span>
<span data-ttu-id="2c7ce-153">resourceId</span><span class="sxs-lookup"><span data-stu-id="2c7ce-153">resourceId</span></span> | <span data-ttu-id="2c7ce-154">Hello 作業的 hello 資源 ID 已進行，以大寫。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-154">ID of hello resource that hello operation took place on, in upper case.</span></span> <span data-ttu-id="2c7ce-155">其中包括 hello 訂用帳戶 ID、 hello 資源群組，以及 hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-155">It includes hello subscription ID, hello resource group, and hello job name.</span></span> <span data-ttu-id="2c7ce-156">例如，**/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-156">For example, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.</span></span>
<span data-ttu-id="2c7ce-157">category</span><span class="sxs-lookup"><span data-stu-id="2c7ce-157">category</span></span> | <span data-ttu-id="2c7ce-158">記錄類別 (**執行**或**編寫**)。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-158">Log category, either **Execution** or **Authoring**.</span></span>
<span data-ttu-id="2c7ce-159">operationName</span><span class="sxs-lookup"><span data-stu-id="2c7ce-159">operationName</span></span> | <span data-ttu-id="2c7ce-160">Hello 作業所記錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-160">Name of hello operation that is logged.</span></span> <span data-ttu-id="2c7ce-161">例如，**傳送事件： SQL 輸出寫入失敗 toomysqloutput**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-161">For example, **Send Events: SQL Output write failure toomysqloutput**.</span></span>
<span data-ttu-id="2c7ce-162">status</span><span class="sxs-lookup"><span data-stu-id="2c7ce-162">status</span></span> | <span data-ttu-id="2c7ce-163">Hello 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-163">Status of hello operation.</span></span> <span data-ttu-id="2c7ce-164">例如，**失敗**或**成功**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-164">For example, **Failed** or **Succeeded**.</span></span>
<span data-ttu-id="2c7ce-165">層級</span><span class="sxs-lookup"><span data-stu-id="2c7ce-165">level</span></span> | <span data-ttu-id="2c7ce-166">記錄層級。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-166">Log level.</span></span> <span data-ttu-id="2c7ce-167">例如，**錯誤**、**警告**或**資訊**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-167">For example, **Error**, **Warning**, or **Informational**.</span></span>
<span data-ttu-id="2c7ce-168">屬性</span><span class="sxs-lookup"><span data-stu-id="2c7ce-168">properties</span></span> | <span data-ttu-id="2c7ce-169">記錄項目特定詳細資料 (序列化為 JSON 字串)。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-169">Log entry-specific detail, serialized as a JSON string.</span></span> <span data-ttu-id="2c7ce-170">如需詳細資訊，請參閱下列各節的 hello。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-170">For more information, see hello following sections.</span></span>

### <a name="execution-log-properties-schema"></a><span data-ttu-id="2c7ce-171">執行記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="2c7ce-171">Execution log properties schema</span></span>

<span data-ttu-id="2c7ce-172">執行記錄包含在執行串流分析作業期間所發生事件的資訊。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-172">Execution logs have information about events that happened during Stream Analytics job execution.</span></span> <span data-ttu-id="2c7ce-173">hello 結構描述的內容會因 hello 事件類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-173">hello schema of properties varies, depending on hello type of event.</span></span> <span data-ttu-id="2c7ce-174">目前，我們有下列類型的執行記錄的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c7ce-174">Currently, we have hello following types of execution logs:</span></span>

### <a name="data-errors"></a><span data-ttu-id="2c7ce-175">資料錯誤</span><span class="sxs-lookup"><span data-stu-id="2c7ce-175">Data errors</span></span>

<span data-ttu-id="2c7ce-176">這個類別的記錄檔，是 hello 作業正在處理資料時，就會發生任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-176">Any error that occurs while hello job is processing data is in this category of logs.</span></span> <span data-ttu-id="2c7ce-177">這些記錄最常於資料讀取、序列化和寫入作業時建立。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-177">These logs most often are created during data read, serialization, and write operations.</span></span> <span data-ttu-id="2c7ce-178">這些記錄不包含連線錯誤。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-178">These logs do not include connectivity errors.</span></span> <span data-ttu-id="2c7ce-179">連線錯誤視為一般事件。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-179">Connectivity errors are treated as generic events.</span></span>

<span data-ttu-id="2c7ce-180">名稱</span><span class="sxs-lookup"><span data-stu-id="2c7ce-180">Name</span></span> | <span data-ttu-id="2c7ce-181">說明</span><span class="sxs-lookup"><span data-stu-id="2c7ce-181">Description</span></span>
------- | -------
<span data-ttu-id="2c7ce-182">來源</span><span class="sxs-lookup"><span data-stu-id="2c7ce-182">Source</span></span> | <span data-ttu-id="2c7ce-183">輸入或輸出發生 hello 錯誤 hello 作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-183">Name of hello job input or output where hello error occurred.</span></span>
<span data-ttu-id="2c7ce-184">訊息</span><span class="sxs-lookup"><span data-stu-id="2c7ce-184">Message</span></span> | <span data-ttu-id="2c7ce-185">與 hello 錯誤相關聯的訊息。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-185">Message associated with hello error.</span></span>
<span data-ttu-id="2c7ce-186">類型</span><span class="sxs-lookup"><span data-stu-id="2c7ce-186">Type</span></span> | <span data-ttu-id="2c7ce-187">錯誤類型。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-187">Type of error.</span></span> <span data-ttu-id="2c7ce-188">例如，**DataConversionError**、**CsvParserError** 或 **ServiceBusPropertyColumnMissingError**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-188">For example, **DataConversionError**, **CsvParserError**, or **ServiceBusPropertyColumnMissingError**.</span></span>
<span data-ttu-id="2c7ce-189">資料</span><span class="sxs-lookup"><span data-stu-id="2c7ce-189">Data</span></span> | <span data-ttu-id="2c7ce-190">包含有用的資料 tooaccurately 找出 hello hello 錯誤來源。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-190">Contains data that is useful tooaccurately locate hello source of hello error.</span></span> <span data-ttu-id="2c7ce-191">主旨 tootruncation，視大小而定。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-191">Subject tootruncation, depending on size.</span></span>

<span data-ttu-id="2c7ce-192">根據 hello **operationName**值，資料錯誤有下列結構描述的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c7ce-192">Depending on hello **operationName** value, data errors have hello following schema:</span></span>
* <span data-ttu-id="2c7ce-193">**序列化事件**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-193">**Serialize events**.</span></span> <span data-ttu-id="2c7ce-194">序列化事件會在事件讀取作業期間發生。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-194">Serialize events occur during event read operations.</span></span> <span data-ttu-id="2c7ce-195">當 hello hello 輸入的資料不符合 hello 查詢結構描述的其中一個原因而發生：</span><span class="sxs-lookup"><span data-stu-id="2c7ce-195">They occur when hello data at hello input does not satisfy hello query schema for one of these reasons:</span></span>
    * <span data-ttu-id="2c7ce-196">*事件 (de) 期間的類型不符序列化*： 識別造成 hello 錯誤 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-196">*Type mismatch during event (de)serialize*: Identifies hello field that's causing hello error.</span></span>
    * <span data-ttu-id="2c7ce-197">*無法讀取事件、 無效的序列化*： 列出發生 hello 錯誤 hello 輸入資料中的 hello 位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-197">*Cannot read an event, invalid serialization*: Lists information about hello location in hello input data where hello error occurred.</span></span> <span data-ttu-id="2c7ce-198">包含 blob 名稱的 blob 輸入、 位移和 hello 資料的範例。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-198">Includes blob name for blob input, offset, and a sample of hello data.</span></span>
* <span data-ttu-id="2c7ce-199">**傳送事件**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-199">**Send events**.</span></span> <span data-ttu-id="2c7ce-200">傳送事件會發生在寫入作業期間。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-200">Send events occur during write operations.</span></span> <span data-ttu-id="2c7ce-201">它們可識別 hello 造成 hello 錯誤的事件資料流處理。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-201">They identify hello streaming event that caused hello error.</span></span>

### <a name="generic-events"></a><span data-ttu-id="2c7ce-202">一般事件</span><span class="sxs-lookup"><span data-stu-id="2c7ce-202">Generic events</span></span>

<span data-ttu-id="2c7ce-203">一般事件涵蓋所有其他事件。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-203">Generic events cover everything else.</span></span>

<span data-ttu-id="2c7ce-204">名稱</span><span class="sxs-lookup"><span data-stu-id="2c7ce-204">Name</span></span> | <span data-ttu-id="2c7ce-205">說明</span><span class="sxs-lookup"><span data-stu-id="2c7ce-205">Description</span></span>
-------- | --------
<span data-ttu-id="2c7ce-206">錯誤</span><span class="sxs-lookup"><span data-stu-id="2c7ce-206">Error</span></span> | <span data-ttu-id="2c7ce-207">(選用) 錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-207">(optional) Error information.</span></span> <span data-ttu-id="2c7ce-208">這通常是例外狀況資訊 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-208">Usually, this is exception information, if it's available.</span></span>
<span data-ttu-id="2c7ce-209">訊息</span><span class="sxs-lookup"><span data-stu-id="2c7ce-209">Message</span></span>| <span data-ttu-id="2c7ce-210">記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-210">Log message.</span></span>
<span data-ttu-id="2c7ce-211">類型</span><span class="sxs-lookup"><span data-stu-id="2c7ce-211">Type</span></span> | <span data-ttu-id="2c7ce-212">訊息類型。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-212">Type of message.</span></span> <span data-ttu-id="2c7ce-213">將對應 toointernal 分類的錯誤。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-213">Maps toointernal categorization of errors.</span></span> <span data-ttu-id="2c7ce-214">例如，**JobValidationError**或 **BlobOutputAdapterInitializationFailure**。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-214">For example, **JobValidationError** or **BlobOutputAdapterInitializationFailure**.</span></span>
<span data-ttu-id="2c7ce-215">相互關連識別碼</span><span class="sxs-lookup"><span data-stu-id="2c7ce-215">Correlation ID</span></span> | <span data-ttu-id="2c7ce-216">[GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier)可唯一識別 hello 作業執行。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-216">[GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) that uniquely identifies hello job execution.</span></span> <span data-ttu-id="2c7ce-217">所有的執行記錄項目從 hello 時間 hello 作業啟動，直到 hello 作業停止擁有 hello 相同**相互關聯識別碼**值。</span><span class="sxs-lookup"><span data-stu-id="2c7ce-217">All execution log entries from hello time hello job starts until hello job stops have hello same **Correlation ID** value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c7ce-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c7ce-218">Next steps</span></span>

* [<span data-ttu-id="2c7ce-219">簡介 tooStream 分析</span><span class="sxs-lookup"><span data-stu-id="2c7ce-219">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2c7ce-220">開始使用串流分析</span><span class="sxs-lookup"><span data-stu-id="2c7ce-220">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2c7ce-221">調整串流分析作業</span><span class="sxs-lookup"><span data-stu-id="2c7ce-221">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2c7ce-222">串流分析查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="2c7ce-222">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2c7ce-223">串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="2c7ce-223">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
