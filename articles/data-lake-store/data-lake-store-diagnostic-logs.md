---
title: "檢視 Azure Data Lake Store 的診斷記錄 | Microsoft Docs"
description: "了解如何設定及存取 Azure Data Lake Store 的診斷記錄  "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="6bb35-103">存取 Azure Data Lake Store 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="6bb35-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="6bb35-104">了解如何啟用 Data Lake Store 帳戶的診斷記錄，以及如何檢視針對帳戶收集的記錄。</span><span class="sxs-lookup"><span data-stu-id="6bb35-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="6bb35-105">組織可以啟用 Azure Data Lake Store 帳戶的診斷記錄，以便收集資料存取稽核記錄，取得如存取資料的使用者清單、資料存取頻率、儲存在帳戶內的資料量等資訊。</span><span class="sxs-lookup"><span data-stu-id="6bb35-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bb35-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="6bb35-106">Prerequisites</span></span>
* <span data-ttu-id="6bb35-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="6bb35-107">**An Azure subscription**.</span></span> <span data-ttu-id="6bb35-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6bb35-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6bb35-109">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="6bb35-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="6bb35-110">遵循 [使用 Azure 入口網站開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="6bb35-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="6bb35-111">啟用 Data Lake Store 帳戶的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="6bb35-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="6bb35-112">登入新的 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6bb35-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6bb35-113">開啟 Data Lake Store 帳戶，接著在 Data Lake Store 帳戶刀鋒視窗中依序按一下 [設定] 和 [診斷記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="6bb35-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="6bb35-114">在 [診斷記錄檔] 刀鋒視窗中，按一下 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="6bb35-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="6bb35-115">![啟用診斷記錄](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "啟用診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="6bb35-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="6bb35-116">在 [診斷]  刀鋒視窗中，變更下列項目以設定診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="6bb35-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="6bb35-117">![啟用診斷記錄](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "啟用診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="6bb35-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="6bb35-118">將 [狀態] 設定為 [開啟] 以啟用診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="6bb35-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="6bb35-119">您可以選擇不同的資料儲存/處理方法。</span><span class="sxs-lookup"><span data-stu-id="6bb35-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="6bb35-120">選取 [封存至儲存體帳戶] 選項可將記錄儲存到 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bb35-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="6bb35-121">如果您想要保存資料以供日後批次處理，可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6bb35-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="6bb35-122">如果您選取此選項，必須提供用來儲存記錄的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6bb35-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="6bb35-123">選取 [串流至事件中樞] 選項可將記錄資料串流到 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="6bb35-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="6bb35-124">如果您有即時分析內送記錄的下游處理管線，很可能會使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="6bb35-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="6bb35-125">如果您選取此選項，必須提供要使用的 Azure 事件中樞詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6bb35-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="6bb35-126">選取 [傳送至 Log Analytics] 選項可使用 Azure Log Analytics 服務來分析產生的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="6bb35-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="6bb35-127">如果您選取此選項，必須提供要用來執行記錄檔分析的 Operations Management Suite 工作區詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6bb35-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="6bb35-128">指定要取得稽核記錄、要求記錄或兩者。</span><span class="sxs-lookup"><span data-stu-id="6bb35-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="6bb35-129">指定的資料的保留天數。</span><span class="sxs-lookup"><span data-stu-id="6bb35-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="6bb35-130">只有在您使用 Azure 儲存體帳戶來封存記錄資料時，才適用保留期。</span><span class="sxs-lookup"><span data-stu-id="6bb35-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="6bb35-131">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6bb35-131">Click **Save**.</span></span>

<span data-ttu-id="6bb35-132">一旦您啟用了診斷設定，即可在 [診斷記錄]  索引標籤中查看記錄。</span><span class="sxs-lookup"><span data-stu-id="6bb35-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="6bb35-133">檢視 Data Lake Store 帳戶的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="6bb35-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="6bb35-134">檢視 Data Lake Store 帳戶的記錄資料有兩種方式。</span><span class="sxs-lookup"><span data-stu-id="6bb35-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="6bb35-135">從 Data Lake Store 帳戶設定檢視</span><span class="sxs-lookup"><span data-stu-id="6bb35-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="6bb35-136">從儲存資料的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6bb35-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="6bb35-137">使用 Data Lake Store 設定檢視</span><span class="sxs-lookup"><span data-stu-id="6bb35-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="6bb35-138">在 Data Lake Store 帳戶的 [設定] 刀鋒視窗中，按一下 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="6bb35-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="6bb35-139">![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="6bb35-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="6bb35-140">在 [診斷記錄] 刀鋒視窗中，您應該會看到依照 [稽核記錄] 和 [要求記錄] 分類的記錄。</span><span class="sxs-lookup"><span data-stu-id="6bb35-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="6bb35-141">要求記錄能擷取所有以 Data Lake Store 帳戶提出的 API 要求。</span><span class="sxs-lookup"><span data-stu-id="6bb35-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="6bb35-142">稽核記錄與要求記錄相似，不過能針對以 Data Lake Store 帳戶執行之作業提供更詳細的明細。</span><span class="sxs-lookup"><span data-stu-id="6bb35-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="6bb35-143">例如，要求記錄中的一個上傳 API 呼叫可能會致使稽核記錄出現多個「附加」作業。</span><span class="sxs-lookup"><span data-stu-id="6bb35-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="6bb35-144">針對每個記錄項目按一下 [下載]  連結來下載記錄。</span><span class="sxs-lookup"><span data-stu-id="6bb35-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="6bb35-145">從包含記錄資料的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6bb35-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="6bb35-146">開啟與與用於記錄的 Data Lake Store 關聯的Azure 儲存體帳戶刀鋒視窗，然後按一下 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="6bb35-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="6bb35-147">[Blob 服務]  刀鋒視窗會列出兩個容器。</span><span class="sxs-lookup"><span data-stu-id="6bb35-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="6bb35-148">![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="6bb35-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="6bb35-149">容器 **insights-logs-audit** 包含稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6bb35-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="6bb35-150">容器 **insights-logs-requests** 包含要求記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6bb35-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="6bb35-151">在這些容器中，紀錄會儲存在下列結構底下。</span><span class="sxs-lookup"><span data-stu-id="6bb35-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="6bb35-152">![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="6bb35-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="6bb35-153">例如，稽核記錄檔的完整路徑可能是 `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="6bb35-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="6bb35-154">同樣的，要求記錄檔的完整路徑可能是 `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="6bb35-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="6bb35-155">了解記錄資料的結構</span><span class="sxs-lookup"><span data-stu-id="6bb35-155">Understand the structure of the log data</span></span>
<span data-ttu-id="6bb35-156">稽核和要求記錄採用 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="6bb35-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="6bb35-157">在本節中，我們要探討要求和稽核記錄的 JSON 結構。</span><span class="sxs-lookup"><span data-stu-id="6bb35-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="6bb35-158">要求記錄</span><span class="sxs-lookup"><span data-stu-id="6bb35-158">Request logs</span></span>
<span data-ttu-id="6bb35-159">以下是採用 JSON 格式之要求記錄中的範例項目。</span><span class="sxs-lookup"><span data-stu-id="6bb35-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="6bb35-160">每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="6bb35-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="6bb35-161">要求記錄的結構描述</span><span class="sxs-lookup"><span data-stu-id="6bb35-161">Request log schema</span></span>
| <span data-ttu-id="6bb35-162">Name</span><span class="sxs-lookup"><span data-stu-id="6bb35-162">Name</span></span> | <span data-ttu-id="6bb35-163">類型</span><span class="sxs-lookup"><span data-stu-id="6bb35-163">Type</span></span> | <span data-ttu-id="6bb35-164">說明</span><span class="sxs-lookup"><span data-stu-id="6bb35-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bb35-165">分析</span><span class="sxs-lookup"><span data-stu-id="6bb35-165">time</span></span> |<span data-ttu-id="6bb35-166">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-166">String</span></span> |<span data-ttu-id="6bb35-167">記錄的時間戳記 (UTC 時間)</span><span class="sxs-lookup"><span data-stu-id="6bb35-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="6bb35-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="6bb35-168">resourceId</span></span> |<span data-ttu-id="6bb35-169">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-169">String</span></span> |<span data-ttu-id="6bb35-170">作業發生之資源的識別碼</span><span class="sxs-lookup"><span data-stu-id="6bb35-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="6bb35-171">category</span><span class="sxs-lookup"><span data-stu-id="6bb35-171">category</span></span> |<span data-ttu-id="6bb35-172">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-172">String</span></span> |<span data-ttu-id="6bb35-173">記錄類別。</span><span class="sxs-lookup"><span data-stu-id="6bb35-173">The log category.</span></span> <span data-ttu-id="6bb35-174">例如， **要求**。</span><span class="sxs-lookup"><span data-stu-id="6bb35-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="6bb35-175">operationName</span><span class="sxs-lookup"><span data-stu-id="6bb35-175">operationName</span></span> |<span data-ttu-id="6bb35-176">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-176">String</span></span> |<span data-ttu-id="6bb35-177">記錄的作業名稱。</span><span class="sxs-lookup"><span data-stu-id="6bb35-177">Name of the operation that is logged.</span></span> <span data-ttu-id="6bb35-178">例如，getfilestatus。</span><span class="sxs-lookup"><span data-stu-id="6bb35-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="6bb35-179">resultType</span><span class="sxs-lookup"><span data-stu-id="6bb35-179">resultType</span></span> |<span data-ttu-id="6bb35-180">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-180">String</span></span> |<span data-ttu-id="6bb35-181">作業的狀態。例如，200。</span><span class="sxs-lookup"><span data-stu-id="6bb35-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="6bb35-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="6bb35-182">callerIpAddress</span></span> |<span data-ttu-id="6bb35-183">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-183">String</span></span> |<span data-ttu-id="6bb35-184">提出要求之用戶端的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="6bb35-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="6bb35-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="6bb35-185">correlationId</span></span> |<span data-ttu-id="6bb35-186">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-186">String</span></span> |<span data-ttu-id="6bb35-187">用來將一組相關記錄項目分組在一起的記錄識別碼</span><span class="sxs-lookup"><span data-stu-id="6bb35-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="6bb35-188">身分識別</span><span class="sxs-lookup"><span data-stu-id="6bb35-188">identity</span></span> |<span data-ttu-id="6bb35-189">Object</span><span class="sxs-lookup"><span data-stu-id="6bb35-189">Object</span></span> |<span data-ttu-id="6bb35-190">產生記錄的身分識別</span><span class="sxs-lookup"><span data-stu-id="6bb35-190">The identity that generated the log</span></span> |
| <span data-ttu-id="6bb35-191">properties</span><span class="sxs-lookup"><span data-stu-id="6bb35-191">properties</span></span> |<span data-ttu-id="6bb35-192">JSON</span><span class="sxs-lookup"><span data-stu-id="6bb35-192">JSON</span></span> |<span data-ttu-id="6bb35-193">如需詳細資料，請參閱下文</span><span class="sxs-lookup"><span data-stu-id="6bb35-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="6bb35-194">要求記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="6bb35-194">Request log properties schema</span></span>
| <span data-ttu-id="6bb35-195">Name</span><span class="sxs-lookup"><span data-stu-id="6bb35-195">Name</span></span> | <span data-ttu-id="6bb35-196">類型</span><span class="sxs-lookup"><span data-stu-id="6bb35-196">Type</span></span> | <span data-ttu-id="6bb35-197">說明</span><span class="sxs-lookup"><span data-stu-id="6bb35-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bb35-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="6bb35-198">HttpMethod</span></span> |<span data-ttu-id="6bb35-199">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-199">String</span></span> |<span data-ttu-id="6bb35-200">作業使用的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="6bb35-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="6bb35-201">例如，GET。</span><span class="sxs-lookup"><span data-stu-id="6bb35-201">For example, GET.</span></span> |
| <span data-ttu-id="6bb35-202">Path</span><span class="sxs-lookup"><span data-stu-id="6bb35-202">Path</span></span> |<span data-ttu-id="6bb35-203">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-203">String</span></span> |<span data-ttu-id="6bb35-204">執行作業的所在路徑</span><span class="sxs-lookup"><span data-stu-id="6bb35-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="6bb35-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="6bb35-205">RequestContentLength</span></span> |<span data-ttu-id="6bb35-206">int</span><span class="sxs-lookup"><span data-stu-id="6bb35-206">int</span></span> |<span data-ttu-id="6bb35-207">HTTP 要求的內容長度</span><span class="sxs-lookup"><span data-stu-id="6bb35-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="6bb35-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="6bb35-208">ClientRequestId</span></span> |<span data-ttu-id="6bb35-209">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-209">String</span></span> |<span data-ttu-id="6bb35-210">可唯一識別要求的識別碼</span><span class="sxs-lookup"><span data-stu-id="6bb35-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="6bb35-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="6bb35-211">StartTime</span></span> |<span data-ttu-id="6bb35-212">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-212">String</span></span> |<span data-ttu-id="6bb35-213">伺服器接收到要求的時間</span><span class="sxs-lookup"><span data-stu-id="6bb35-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="6bb35-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="6bb35-214">EndTime</span></span> |<span data-ttu-id="6bb35-215">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-215">String</span></span> |<span data-ttu-id="6bb35-216">伺服器傳送回應的時間</span><span class="sxs-lookup"><span data-stu-id="6bb35-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="6bb35-217">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="6bb35-217">Audit logs</span></span>
<span data-ttu-id="6bb35-218">以下是採用 JSON 格式之稽核記錄中的範例項目。</span><span class="sxs-lookup"><span data-stu-id="6bb35-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="6bb35-219">每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列</span><span class="sxs-lookup"><span data-stu-id="6bb35-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="6bb35-220">稽核記錄的結構描述</span><span class="sxs-lookup"><span data-stu-id="6bb35-220">Audit log schema</span></span>
| <span data-ttu-id="6bb35-221">Name</span><span class="sxs-lookup"><span data-stu-id="6bb35-221">Name</span></span> | <span data-ttu-id="6bb35-222">類型</span><span class="sxs-lookup"><span data-stu-id="6bb35-222">Type</span></span> | <span data-ttu-id="6bb35-223">說明</span><span class="sxs-lookup"><span data-stu-id="6bb35-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bb35-224">分析</span><span class="sxs-lookup"><span data-stu-id="6bb35-224">time</span></span> |<span data-ttu-id="6bb35-225">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-225">String</span></span> |<span data-ttu-id="6bb35-226">記錄的時間戳記 (UTC 時間)</span><span class="sxs-lookup"><span data-stu-id="6bb35-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="6bb35-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="6bb35-227">resourceId</span></span> |<span data-ttu-id="6bb35-228">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-228">String</span></span> |<span data-ttu-id="6bb35-229">作業發生之資源的識別碼</span><span class="sxs-lookup"><span data-stu-id="6bb35-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="6bb35-230">category</span><span class="sxs-lookup"><span data-stu-id="6bb35-230">category</span></span> |<span data-ttu-id="6bb35-231">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-231">String</span></span> |<span data-ttu-id="6bb35-232">記錄類別。</span><span class="sxs-lookup"><span data-stu-id="6bb35-232">The log category.</span></span> <span data-ttu-id="6bb35-233">例如， **稽核**。</span><span class="sxs-lookup"><span data-stu-id="6bb35-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="6bb35-234">operationName</span><span class="sxs-lookup"><span data-stu-id="6bb35-234">operationName</span></span> |<span data-ttu-id="6bb35-235">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-235">String</span></span> |<span data-ttu-id="6bb35-236">記錄的作業名稱。</span><span class="sxs-lookup"><span data-stu-id="6bb35-236">Name of the operation that is logged.</span></span> <span data-ttu-id="6bb35-237">例如，getfilestatus。</span><span class="sxs-lookup"><span data-stu-id="6bb35-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="6bb35-238">resultType</span><span class="sxs-lookup"><span data-stu-id="6bb35-238">resultType</span></span> |<span data-ttu-id="6bb35-239">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-239">String</span></span> |<span data-ttu-id="6bb35-240">作業的狀態。例如，200。</span><span class="sxs-lookup"><span data-stu-id="6bb35-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="6bb35-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="6bb35-241">correlationId</span></span> |<span data-ttu-id="6bb35-242">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-242">String</span></span> |<span data-ttu-id="6bb35-243">用來將一組相關記錄項目分組在一起的記錄識別碼</span><span class="sxs-lookup"><span data-stu-id="6bb35-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="6bb35-244">身分識別</span><span class="sxs-lookup"><span data-stu-id="6bb35-244">identity</span></span> |<span data-ttu-id="6bb35-245">Object</span><span class="sxs-lookup"><span data-stu-id="6bb35-245">Object</span></span> |<span data-ttu-id="6bb35-246">產生記錄的身分識別</span><span class="sxs-lookup"><span data-stu-id="6bb35-246">The identity that generated the log</span></span> |
| <span data-ttu-id="6bb35-247">properties</span><span class="sxs-lookup"><span data-stu-id="6bb35-247">properties</span></span> |<span data-ttu-id="6bb35-248">JSON</span><span class="sxs-lookup"><span data-stu-id="6bb35-248">JSON</span></span> |<span data-ttu-id="6bb35-249">如需詳細資料，請參閱下文</span><span class="sxs-lookup"><span data-stu-id="6bb35-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="6bb35-250">稽核記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="6bb35-250">Audit log properties schema</span></span>
| <span data-ttu-id="6bb35-251">Name</span><span class="sxs-lookup"><span data-stu-id="6bb35-251">Name</span></span> | <span data-ttu-id="6bb35-252">類型</span><span class="sxs-lookup"><span data-stu-id="6bb35-252">Type</span></span> | <span data-ttu-id="6bb35-253">說明</span><span class="sxs-lookup"><span data-stu-id="6bb35-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bb35-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="6bb35-254">StreamName</span></span> |<span data-ttu-id="6bb35-255">String</span><span class="sxs-lookup"><span data-stu-id="6bb35-255">String</span></span> |<span data-ttu-id="6bb35-256">執行作業的所在路徑</span><span class="sxs-lookup"><span data-stu-id="6bb35-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="6bb35-257">處理記錄資料的範例</span><span class="sxs-lookup"><span data-stu-id="6bb35-257">Samples to process the log data</span></span>
<span data-ttu-id="6bb35-258">Azure Data Lake Store 會提供有關如何處理和分析記錄資料的範例。</span><span class="sxs-lookup"><span data-stu-id="6bb35-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="6bb35-259">您可以在 [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)找到範例。</span><span class="sxs-lookup"><span data-stu-id="6bb35-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="6bb35-260">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6bb35-260">See also</span></span>
* [<span data-ttu-id="6bb35-261">Azure Data Lake Store 概觀</span><span class="sxs-lookup"><span data-stu-id="6bb35-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="6bb35-262">保護資料湖存放區中的資料</span><span class="sxs-lookup"><span data-stu-id="6bb35-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

