---
title: "檢視 Azure Data Lake Analytics 的診斷記錄 | Microsoft Docs"
description: "了解如何設定及存取 Azure Data Lake Analytics 的診斷記錄  "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 6c74db1659742aa41306388273bec46800ba7609
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="f2718-103">存取 Azure Data Lake Analytics 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="f2718-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="f2718-104">診斷記錄可讓您收集資料存取稽核線索。</span><span class="sxs-lookup"><span data-stu-id="f2718-104">Diagnostic logging allows you to collect data access audit trails.</span></span> <span data-ttu-id="f2718-105">這些記錄檔可提供如下資訊︰</span><span class="sxs-lookup"><span data-stu-id="f2718-105">These logs provide information such as:</span></span>

* <span data-ttu-id="f2718-106">資料的存取使用者清單。</span><span class="sxs-lookup"><span data-stu-id="f2718-106">A list of users that accessed the data.</span></span>
* <span data-ttu-id="f2718-107">資料的存取頻率。</span><span class="sxs-lookup"><span data-stu-id="f2718-107">How frequently the data is accessed.</span></span>
* <span data-ttu-id="f2718-108">帳戶中儲存的資料量。</span><span class="sxs-lookup"><span data-stu-id="f2718-108">How much data is stored in the account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="f2718-109">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="f2718-109">Enable logging</span></span>

1. <span data-ttu-id="f2718-110">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f2718-110">Sign on to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f2718-111">開啟 Data Lake Analytics 帳戶，然後從 [監視] 區段選取 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="f2718-111">Open your Data Lake Analytics account and select **Diagnostic logs** from the __Monitor__ section.</span></span> <span data-ttu-id="f2718-112">接下來，選取 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="f2718-112">Next, select __Turn on diagnostics__.</span></span>

    ![開啟診斷以收集稽核和要求記錄](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="f2718-114">從 [診斷設定] 中，將狀態設為 [啟用]，然後選取記錄選項。</span><span class="sxs-lookup"><span data-stu-id="f2718-114">From __Diagnostics settings__, set the status to __On__ and select logging options.</span></span>

    <span data-ttu-id="f2718-115">![開啟診斷以收集稽核和要求記錄](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "啟用診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="f2718-115">![Turn on diagnostics to collect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="f2718-116">將 [狀態] 設定為 [開啟] 以啟用診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="f2718-116">Set **Status** to **On** to enable diagnostic logging.</span></span>

   * <span data-ttu-id="f2718-117">您可以選擇三種不同的資料儲存/處理方法。</span><span class="sxs-lookup"><span data-stu-id="f2718-117">You can choose to store/process the data in three different ways.</span></span>

     * <span data-ttu-id="f2718-118">選取 [封存至儲存體帳戶] 可將記錄儲存到 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2718-118">Select __Archive to a storage account__ to store logs in an Azure storage account.</span></span> <span data-ttu-id="f2718-119">如果您想要封存資料，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="f2718-119">Use this option if you want to archive the data.</span></span> <span data-ttu-id="f2718-120">如果您選取此選項，必須提供用來儲存記錄的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2718-120">If you select this option, you must provide an Azure storage account to save the logs to.</span></span>

     * <span data-ttu-id="f2718-121">選取 [串流至事件中樞] 可將記錄資料串流到 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="f2718-121">Select **Stream to an Event Hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="f2718-122">如果您有即時分析內送記錄的下游處理管線，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="f2718-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="f2718-123">如果您選取此選項，必須提供要使用的 Azure 事件中樞詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f2718-123">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

     * <span data-ttu-id="f2718-124">選取 [傳送至 Log Analytics] 可將資料傳送至 Log Analytics 服務。</span><span class="sxs-lookup"><span data-stu-id="f2718-124">Select __Send to Log Analytics__ to send the data to the Log Analytics service.</span></span> <span data-ttu-id="f2718-125">如果您想要使用 Log Analytics 來收集和分析記錄，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="f2718-125">Use this option if you want to use Log Analytics to gather and analyze logs.</span></span>
   * <span data-ttu-id="f2718-126">指定要取得稽核記錄、要求記錄或兩者。</span><span class="sxs-lookup"><span data-stu-id="f2718-126">Specify whether you want to get audit logs or request logs or both.</span></span>  <span data-ttu-id="f2718-127">要求記錄會擷取每個應用程式開發介面 (API) 的要求。</span><span class="sxs-lookup"><span data-stu-id="f2718-127">A request log captures every API request.</span></span> <span data-ttu-id="f2718-128">稽核記錄則會記錄該 API 要求觸發的所有作業。</span><span class="sxs-lookup"><span data-stu-id="f2718-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="f2718-129">針對 [封存至儲存體帳戶]，請指定要保留資料的天數。</span><span class="sxs-lookup"><span data-stu-id="f2718-129">For __Archive to a storage account__, specify the number of days to retain the data.</span></span>

   * <span data-ttu-id="f2718-130">按一下 [檔案] 。</span><span class="sxs-lookup"><span data-stu-id="f2718-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f2718-131">您必須先選取 [封存至儲存體帳戶]、[串流至事件中樞] 或 [傳送至 Log Analytics]，再按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f2718-131">You must select either __Archive to a storage account__, __Stream to an Event Hub__ or __Send to Log Analytics__ before clicking the __Save__ button.</span></span>

<span data-ttu-id="f2718-132">一旦您啟用了診斷設定，即可返回 [診斷記錄] 刀鋒視窗來檢視記錄。</span><span class="sxs-lookup"><span data-stu-id="f2718-132">Once you have enabled diagnostic settings, you can return to the __Diagnostics logs__ blade to view the logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="f2718-133">檢視記錄檔</span><span class="sxs-lookup"><span data-stu-id="f2718-133">View logs</span></span>

### <a name="use-the-data-lake-analytics-view"></a><span data-ttu-id="f2718-134">使用 Data Lake Analytics 檢視</span><span class="sxs-lookup"><span data-stu-id="f2718-134">Use the Data Lake Analytics view</span></span>

1. <span data-ttu-id="f2718-135">從 [Data Lake Analytics 帳戶] 刀鋒視窗的 [監視] 下，選取 [診斷記錄]，然後選取要顯示記錄的項目。</span><span class="sxs-lookup"><span data-stu-id="f2718-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry to display logs for.</span></span>

    <span data-ttu-id="f2718-136">![檢視診斷記錄](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="f2718-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="f2718-137">記錄類別分為 [稽核記錄] 和 [要求記錄]。</span><span class="sxs-lookup"><span data-stu-id="f2718-137">The logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![記錄項目](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="f2718-139">要求記錄能擷取所有以 Data Lake Analytics 帳戶提出的 API 要求。</span><span class="sxs-lookup"><span data-stu-id="f2718-139">Request logs capture every API request made on the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="f2718-140">稽核記錄與要求記錄相似，不過能針對作業提供更詳細的明細。</span><span class="sxs-lookup"><span data-stu-id="f2718-140">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations.</span></span> <span data-ttu-id="f2718-141">例如，要求記錄中的一個上傳 API 呼叫可能會致使其稽核記錄出現多個「附加」作業。</span><span class="sxs-lookup"><span data-stu-id="f2718-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="f2718-142">針對記錄項目按一下 [下載]  連結來下載該記錄。</span><span class="sxs-lookup"><span data-stu-id="f2718-142">Click the **Download** link for a log entry to download that log.</span></span>

### <a name="use-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="f2718-143">使用包含記錄資料的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f2718-143">Use the Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="f2718-144">開啟與用於記錄之 Data Lake Analytics 建立關聯的Azure 儲存體帳戶刀鋒視窗，然後按一下 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="f2718-144">Open the Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="f2718-145">[Blob 服務]  刀鋒視窗會列出兩個容器。</span><span class="sxs-lookup"><span data-stu-id="f2718-145">The **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="f2718-146">![檢視診斷記錄](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="f2718-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="f2718-147">容器 **insights-logs-audit** 包含稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f2718-147">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="f2718-148">容器 **insights-logs-requests** 包含要求記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f2718-148">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="f2718-149">在這些容器中，記錄會儲存在下列結構底下：</span><span class="sxs-lookup"><span data-stu-id="f2718-149">Within these containers, the logs are stored under the following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="f2718-150">[Blob 服務] `##` 項目包含記錄檔的建立年、月、日和小時。</span><span class="sxs-lookup"><span data-stu-id="f2718-150">The `##` entries in the path contain the year, month, day, and hour in which the log was created.</span></span> <span data-ttu-id="f2718-151">Data Lake Analytics 每小時會建立一個檔案，因此 `m=` 一律會包含 `00` 值。</span><span class="sxs-lookup"><span data-stu-id="f2718-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="f2718-152">例如，稽核記錄檔的完整路徑可能是：</span><span class="sxs-lookup"><span data-stu-id="f2718-152">As an example, the complete path to an audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="f2718-153">同樣的，要求記錄檔的完整路徑可能是：</span><span class="sxs-lookup"><span data-stu-id="f2718-153">Similarly, the complete path to a request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="f2718-154">記錄檔結構</span><span class="sxs-lookup"><span data-stu-id="f2718-154">Log structure</span></span>

<span data-ttu-id="f2718-155">稽核和要求記錄採用結構化 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="f2718-155">The audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="f2718-156">要求記錄</span><span class="sxs-lookup"><span data-stu-id="f2718-156">Request logs</span></span>

<span data-ttu-id="f2718-157">以下是採用 JSON 格式之要求記錄中的範例項目。</span><span class="sxs-lookup"><span data-stu-id="f2718-157">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="f2718-158">每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="f2718-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="f2718-159">要求記錄的結構描述</span><span class="sxs-lookup"><span data-stu-id="f2718-159">Request log schema</span></span>

| <span data-ttu-id="f2718-160">Name</span><span class="sxs-lookup"><span data-stu-id="f2718-160">Name</span></span> | <span data-ttu-id="f2718-161">類型</span><span class="sxs-lookup"><span data-stu-id="f2718-161">Type</span></span> | <span data-ttu-id="f2718-162">說明</span><span class="sxs-lookup"><span data-stu-id="f2718-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2718-163">分析</span><span class="sxs-lookup"><span data-stu-id="f2718-163">time</span></span> |<span data-ttu-id="f2718-164">String</span><span class="sxs-lookup"><span data-stu-id="f2718-164">String</span></span> |<span data-ttu-id="f2718-165">記錄的時間戳記 (UTC 時間)</span><span class="sxs-lookup"><span data-stu-id="f2718-165">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="f2718-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="f2718-166">resourceId</span></span> |<span data-ttu-id="f2718-167">String</span><span class="sxs-lookup"><span data-stu-id="f2718-167">String</span></span> |<span data-ttu-id="f2718-168">執行作業所在資源的識別碼</span><span class="sxs-lookup"><span data-stu-id="f2718-168">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="f2718-169">category</span><span class="sxs-lookup"><span data-stu-id="f2718-169">category</span></span> |<span data-ttu-id="f2718-170">String</span><span class="sxs-lookup"><span data-stu-id="f2718-170">String</span></span> |<span data-ttu-id="f2718-171">記錄類別。</span><span class="sxs-lookup"><span data-stu-id="f2718-171">The log category.</span></span> <span data-ttu-id="f2718-172">例如， **要求**。</span><span class="sxs-lookup"><span data-stu-id="f2718-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="f2718-173">operationName</span><span class="sxs-lookup"><span data-stu-id="f2718-173">operationName</span></span> |<span data-ttu-id="f2718-174">String</span><span class="sxs-lookup"><span data-stu-id="f2718-174">String</span></span> |<span data-ttu-id="f2718-175">記錄的作業名稱。</span><span class="sxs-lookup"><span data-stu-id="f2718-175">Name of the operation that is logged.</span></span> <span data-ttu-id="f2718-176">例如，GetAggregatedJobHistory。</span><span class="sxs-lookup"><span data-stu-id="f2718-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="f2718-177">resultType</span><span class="sxs-lookup"><span data-stu-id="f2718-177">resultType</span></span> |<span data-ttu-id="f2718-178">String</span><span class="sxs-lookup"><span data-stu-id="f2718-178">String</span></span> |<span data-ttu-id="f2718-179">作業的狀態。例如，200。</span><span class="sxs-lookup"><span data-stu-id="f2718-179">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="f2718-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="f2718-180">callerIpAddress</span></span> |<span data-ttu-id="f2718-181">String</span><span class="sxs-lookup"><span data-stu-id="f2718-181">String</span></span> |<span data-ttu-id="f2718-182">提出要求之用戶端的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f2718-182">The IP address of the client making the request</span></span> |
| <span data-ttu-id="f2718-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="f2718-183">correlationId</span></span> |<span data-ttu-id="f2718-184">String</span><span class="sxs-lookup"><span data-stu-id="f2718-184">String</span></span> |<span data-ttu-id="f2718-185">角色的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f2718-185">The identifier of the log.</span></span> <span data-ttu-id="f2718-186">此值可用來群組一組相關的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="f2718-186">This value can be used to group a set of related log entries.</span></span> |
| <span data-ttu-id="f2718-187">身分識別</span><span class="sxs-lookup"><span data-stu-id="f2718-187">identity</span></span> |<span data-ttu-id="f2718-188">Object</span><span class="sxs-lookup"><span data-stu-id="f2718-188">Object</span></span> |<span data-ttu-id="f2718-189">產生記錄的身分識別</span><span class="sxs-lookup"><span data-stu-id="f2718-189">The identity that generated the log</span></span> |
| <span data-ttu-id="f2718-190">properties</span><span class="sxs-lookup"><span data-stu-id="f2718-190">properties</span></span> |<span data-ttu-id="f2718-191">JSON</span><span class="sxs-lookup"><span data-stu-id="f2718-191">JSON</span></span> |<span data-ttu-id="f2718-192">請參閱下一節 (要求記錄檔屬性結構描述) 以取得詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f2718-192">See the next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="f2718-193">要求記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="f2718-193">Request log properties schema</span></span>

| <span data-ttu-id="f2718-194">Name</span><span class="sxs-lookup"><span data-stu-id="f2718-194">Name</span></span> | <span data-ttu-id="f2718-195">類型</span><span class="sxs-lookup"><span data-stu-id="f2718-195">Type</span></span> | <span data-ttu-id="f2718-196">說明</span><span class="sxs-lookup"><span data-stu-id="f2718-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2718-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="f2718-197">HttpMethod</span></span> |<span data-ttu-id="f2718-198">String</span><span class="sxs-lookup"><span data-stu-id="f2718-198">String</span></span> |<span data-ttu-id="f2718-199">作業使用的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f2718-199">The HTTP Method used for the operation.</span></span> <span data-ttu-id="f2718-200">例如，GET。</span><span class="sxs-lookup"><span data-stu-id="f2718-200">For example, GET.</span></span> |
| <span data-ttu-id="f2718-201">Path</span><span class="sxs-lookup"><span data-stu-id="f2718-201">Path</span></span> |<span data-ttu-id="f2718-202">String</span><span class="sxs-lookup"><span data-stu-id="f2718-202">String</span></span> |<span data-ttu-id="f2718-203">執行作業的所在路徑</span><span class="sxs-lookup"><span data-stu-id="f2718-203">The path the operation was performed on</span></span> |
| <span data-ttu-id="f2718-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="f2718-204">RequestContentLength</span></span> |<span data-ttu-id="f2718-205">int</span><span class="sxs-lookup"><span data-stu-id="f2718-205">int</span></span> |<span data-ttu-id="f2718-206">HTTP 要求的內容長度</span><span class="sxs-lookup"><span data-stu-id="f2718-206">The content length of the HTTP request</span></span> |
| <span data-ttu-id="f2718-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="f2718-207">ClientRequestId</span></span> |<span data-ttu-id="f2718-208">String</span><span class="sxs-lookup"><span data-stu-id="f2718-208">String</span></span> |<span data-ttu-id="f2718-209">可唯一識別此要求的識別碼</span><span class="sxs-lookup"><span data-stu-id="f2718-209">The identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="f2718-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="f2718-210">StartTime</span></span> |<span data-ttu-id="f2718-211">String</span><span class="sxs-lookup"><span data-stu-id="f2718-211">String</span></span> |<span data-ttu-id="f2718-212">伺服器接收到要求的時間</span><span class="sxs-lookup"><span data-stu-id="f2718-212">The time at which the server received the request</span></span> |
| <span data-ttu-id="f2718-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="f2718-213">EndTime</span></span> |<span data-ttu-id="f2718-214">String</span><span class="sxs-lookup"><span data-stu-id="f2718-214">String</span></span> |<span data-ttu-id="f2718-215">伺服器傳送回應的時間</span><span class="sxs-lookup"><span data-stu-id="f2718-215">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="f2718-216">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="f2718-216">Audit logs</span></span>

<span data-ttu-id="f2718-217">以下是採用 JSON 格式之稽核記錄中的範例項目。</span><span class="sxs-lookup"><span data-stu-id="f2718-217">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="f2718-218">每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="f2718-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="f2718-219">稽核記錄的結構描述</span><span class="sxs-lookup"><span data-stu-id="f2718-219">Audit log schema</span></span>

| <span data-ttu-id="f2718-220">Name</span><span class="sxs-lookup"><span data-stu-id="f2718-220">Name</span></span> | <span data-ttu-id="f2718-221">類型</span><span class="sxs-lookup"><span data-stu-id="f2718-221">Type</span></span> | <span data-ttu-id="f2718-222">說明</span><span class="sxs-lookup"><span data-stu-id="f2718-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2718-223">分析</span><span class="sxs-lookup"><span data-stu-id="f2718-223">time</span></span> |<span data-ttu-id="f2718-224">String</span><span class="sxs-lookup"><span data-stu-id="f2718-224">String</span></span> |<span data-ttu-id="f2718-225">記錄的時間戳記 (UTC 時間)</span><span class="sxs-lookup"><span data-stu-id="f2718-225">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="f2718-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="f2718-226">resourceId</span></span> |<span data-ttu-id="f2718-227">String</span><span class="sxs-lookup"><span data-stu-id="f2718-227">String</span></span> |<span data-ttu-id="f2718-228">執行作業所在資源的識別碼</span><span class="sxs-lookup"><span data-stu-id="f2718-228">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="f2718-229">category</span><span class="sxs-lookup"><span data-stu-id="f2718-229">category</span></span> |<span data-ttu-id="f2718-230">String</span><span class="sxs-lookup"><span data-stu-id="f2718-230">String</span></span> |<span data-ttu-id="f2718-231">記錄類別。</span><span class="sxs-lookup"><span data-stu-id="f2718-231">The log category.</span></span> <span data-ttu-id="f2718-232">例如， **稽核**。</span><span class="sxs-lookup"><span data-stu-id="f2718-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="f2718-233">operationName</span><span class="sxs-lookup"><span data-stu-id="f2718-233">operationName</span></span> |<span data-ttu-id="f2718-234">String</span><span class="sxs-lookup"><span data-stu-id="f2718-234">String</span></span> |<span data-ttu-id="f2718-235">記錄的作業名稱。</span><span class="sxs-lookup"><span data-stu-id="f2718-235">Name of the operation that is logged.</span></span> <span data-ttu-id="f2718-236">例如，JobSubmitted。</span><span class="sxs-lookup"><span data-stu-id="f2718-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="f2718-237">resultType</span><span class="sxs-lookup"><span data-stu-id="f2718-237">resultType</span></span> |<span data-ttu-id="f2718-238">String</span><span class="sxs-lookup"><span data-stu-id="f2718-238">String</span></span> |<span data-ttu-id="f2718-239">作業狀態 (operationName) 的子狀態。</span><span class="sxs-lookup"><span data-stu-id="f2718-239">A substatus for the job status (operationName).</span></span> |
| <span data-ttu-id="f2718-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="f2718-240">resultSignature</span></span> |<span data-ttu-id="f2718-241">String</span><span class="sxs-lookup"><span data-stu-id="f2718-241">String</span></span> |<span data-ttu-id="f2718-242">作業狀態 (operationName) 的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f2718-242">Additional details on the job status (operationName).</span></span> |
| <span data-ttu-id="f2718-243">身分識別</span><span class="sxs-lookup"><span data-stu-id="f2718-243">identity</span></span> |<span data-ttu-id="f2718-244">String</span><span class="sxs-lookup"><span data-stu-id="f2718-244">String</span></span> |<span data-ttu-id="f2718-245">要求作業的使用者。</span><span class="sxs-lookup"><span data-stu-id="f2718-245">The user that requested the operation.</span></span> <span data-ttu-id="f2718-246">例如，susan@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="f2718-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="f2718-247">properties</span><span class="sxs-lookup"><span data-stu-id="f2718-247">properties</span></span> |<span data-ttu-id="f2718-248">JSON</span><span class="sxs-lookup"><span data-stu-id="f2718-248">JSON</span></span> |<span data-ttu-id="f2718-249">請參閱下一節 (稽核記錄檔屬性結構描述) 以取得詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f2718-249">See the next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="f2718-250">**resultType** 和 **resultSignature** 會提供作業結果的相關資訊，並且只會在作業完成時才包含值。</span><span class="sxs-lookup"><span data-stu-id="f2718-250">**resultType** and **resultSignature** provide information on the result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="f2718-251">例如，只有當 **operationName** 包含 **JobStarted** 或 **JobEnded** 的值時，它們才會包含值。</span><span class="sxs-lookup"><span data-stu-id="f2718-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="f2718-252">稽核記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="f2718-252">Audit log properties schema</span></span>

| <span data-ttu-id="f2718-253">Name</span><span class="sxs-lookup"><span data-stu-id="f2718-253">Name</span></span> | <span data-ttu-id="f2718-254">類型</span><span class="sxs-lookup"><span data-stu-id="f2718-254">Type</span></span> | <span data-ttu-id="f2718-255">說明</span><span class="sxs-lookup"><span data-stu-id="f2718-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2718-256">JobId</span><span class="sxs-lookup"><span data-stu-id="f2718-256">JobId</span></span> |<span data-ttu-id="f2718-257">String</span><span class="sxs-lookup"><span data-stu-id="f2718-257">String</span></span> |<span data-ttu-id="f2718-258">指派給作業的識別碼</span><span class="sxs-lookup"><span data-stu-id="f2718-258">The ID assigned to the job</span></span> |
| <span data-ttu-id="f2718-259">JobName</span><span class="sxs-lookup"><span data-stu-id="f2718-259">JobName</span></span> |<span data-ttu-id="f2718-260">String</span><span class="sxs-lookup"><span data-stu-id="f2718-260">String</span></span> |<span data-ttu-id="f2718-261">為作業提供的名稱</span><span class="sxs-lookup"><span data-stu-id="f2718-261">The name that was provided for the job</span></span> |
| <span data-ttu-id="f2718-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="f2718-262">JobRunTime</span></span> |<span data-ttu-id="f2718-263">String</span><span class="sxs-lookup"><span data-stu-id="f2718-263">String</span></span> |<span data-ttu-id="f2718-264">用來處理作業的執行階段</span><span class="sxs-lookup"><span data-stu-id="f2718-264">The runtime used to process the job</span></span> |
| <span data-ttu-id="f2718-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="f2718-265">SubmitTime</span></span> |<span data-ttu-id="f2718-266">String</span><span class="sxs-lookup"><span data-stu-id="f2718-266">String</span></span> |<span data-ttu-id="f2718-267">作業提交時間 (UTC 格式)</span><span class="sxs-lookup"><span data-stu-id="f2718-267">The time (in UTC) that the job was submitted</span></span> |
| <span data-ttu-id="f2718-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="f2718-268">StartTime</span></span> |<span data-ttu-id="f2718-269">String</span><span class="sxs-lookup"><span data-stu-id="f2718-269">String</span></span> |<span data-ttu-id="f2718-270">作業在提交後開始執行的時間 (UTC 格式)</span><span class="sxs-lookup"><span data-stu-id="f2718-270">The time the job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="f2718-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="f2718-271">EndTime</span></span> |<span data-ttu-id="f2718-272">String</span><span class="sxs-lookup"><span data-stu-id="f2718-272">String</span></span> |<span data-ttu-id="f2718-273">作業結束時間</span><span class="sxs-lookup"><span data-stu-id="f2718-273">The time the job ended</span></span> |
| <span data-ttu-id="f2718-274">平行處理原則</span><span class="sxs-lookup"><span data-stu-id="f2718-274">Parallelism</span></span> |<span data-ttu-id="f2718-275">String</span><span class="sxs-lookup"><span data-stu-id="f2718-275">String</span></span> |<span data-ttu-id="f2718-276">在提交期間為此作業要求的 Data Lake Analytics 單位數目</span><span class="sxs-lookup"><span data-stu-id="f2718-276">The number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="f2718-277">**SubmitTime**、**StartTime**、**EndTime** 和 **Parallelism** 提供作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f2718-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="f2718-278">這些項目只會在作業啟動或完成時才包含值。</span><span class="sxs-lookup"><span data-stu-id="f2718-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="f2718-279">例如，**SubmitTime** 只會在 **operationName** 具有 **JobSubmitted** 值之後包含值。</span><span class="sxs-lookup"><span data-stu-id="f2718-279">For example, **SubmitTime** only contains a value after **operationName** has the value **JobSubmitted**.</span></span>

## <a name="process-the-log-data"></a><span data-ttu-id="f2718-280">處理記錄資料</span><span class="sxs-lookup"><span data-stu-id="f2718-280">Process the log data</span></span>

<span data-ttu-id="f2718-281">Azure Data Lake Analytics 會提供有關如何處理和分析記錄資料的範例。</span><span class="sxs-lookup"><span data-stu-id="f2718-281">Azure Data Lake Analytics provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="f2718-282">您可以在 [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)找到範例。</span><span class="sxs-lookup"><span data-stu-id="f2718-282">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2718-283">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2718-283">Next steps</span></span>
* [<span data-ttu-id="f2718-284">Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="f2718-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
