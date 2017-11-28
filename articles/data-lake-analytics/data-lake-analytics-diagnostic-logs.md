---
title: "Azure Data Lake Analytics aaaViewing 診斷記錄檔 |Microsoft 文件"
description: "了解如何 toosetup 及存取診斷記錄的 Azure 資料湖分析 "
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
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="86018-103">存取 Azure Data Lake Analytics 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="86018-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="86018-104">診斷記錄可讓您 toocollect 資料存取稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="86018-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="86018-105">這些記錄檔可提供如下資訊︰</span><span class="sxs-lookup"><span data-stu-id="86018-105">These logs provide information such as:</span></span>

* <span data-ttu-id="86018-106">存取 hello 資料的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="86018-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="86018-107">Hello 資料存取的頻率。</span><span class="sxs-lookup"><span data-stu-id="86018-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="86018-108">多少資料會儲存在 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="86018-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="86018-109">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="86018-109">Enable logging</span></span>

1. <span data-ttu-id="86018-110">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="86018-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="86018-111">開啟您的 Data Lake Analytics 帳戶，然後選取**診斷記錄**從 hello__監視器__> 一節。</span><span class="sxs-lookup"><span data-stu-id="86018-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="86018-112">接下來，選取 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="86018-112">Next, select __Turn on diagnostics__.</span></span>

    ![開啟診斷 toocollect 稽核，並要求記錄檔](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="86018-114">從__診斷設定__、 設定 hello 狀態 too__On__，然後選取 記錄選項。</span><span class="sxs-lookup"><span data-stu-id="86018-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="86018-115">![開啟診斷 toocollect 稽核，並要求記錄檔](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "啟用診斷記錄檔")</span><span class="sxs-lookup"><span data-stu-id="86018-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="86018-116">設定**狀態**太**上**tooenable 診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="86018-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="86018-117">您可以選擇 toostore/處理序 hello 資料以三個不同的方式。</span><span class="sxs-lookup"><span data-stu-id="86018-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="86018-118">選取__封存 tooa 儲存體帳戶__toostore 登入 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="86018-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="86018-119">如果您想要 tooarchive hello 資料，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="86018-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="86018-120">如果您選取此選項時，您必須提供 Azure 儲存體帳戶 toosave hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="86018-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="86018-121">選取**串流 tooan 事件中心**toostream 記錄資料 tooan Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="86018-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="86018-122">如果您有即時分析內送記錄的下游處理管線，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="86018-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="86018-123">如果您選取此選項時，您必須提供 hello Azure 事件中心想 toouse hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="86018-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="86018-124">選取__傳送 tooLog 分析__toosend hello 資料 toohello 記錄分析服務。</span><span class="sxs-lookup"><span data-stu-id="86018-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="86018-125">如果您想 toouse 記錄分析 toogather 和分析記錄檔，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="86018-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="86018-126">指定是否要 tooget 稽核記錄檔或要求記錄檔或兩者。</span><span class="sxs-lookup"><span data-stu-id="86018-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="86018-127">要求記錄會擷取每個應用程式開發介面 (API) 的要求。</span><span class="sxs-lookup"><span data-stu-id="86018-127">A request log captures every API request.</span></span> <span data-ttu-id="86018-128">稽核記錄則會記錄該 API 要求觸發的所有作業。</span><span class="sxs-lookup"><span data-stu-id="86018-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="86018-129">如__封存 tooa 儲存體帳戶__，指定 hello 天 tooretain hello 資料數目。</span><span class="sxs-lookup"><span data-stu-id="86018-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="86018-130">按一下 [檔案] 。</span><span class="sxs-lookup"><span data-stu-id="86018-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="86018-131">您必須選取__封存 tooa 儲存體帳戶__，__串流 tooan 事件中心__或__傳送 tooLog 分析__後，再按一下 hello__儲存__ 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86018-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="86018-132">一旦您啟用了診斷設定，您可以傳回 toohello__診斷記錄檔__刀鋒視窗 tooview hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="86018-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="86018-133">檢視記錄檔</span><span class="sxs-lookup"><span data-stu-id="86018-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="86018-134">使用 hello Data Lake Analytics 檢視</span><span class="sxs-lookup"><span data-stu-id="86018-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="86018-135">從您的資料湖分析帳戶刀鋒視窗中，在**監視**，選取**診斷記錄檔**，然後選取項目 toodisplay 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="86018-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="86018-136">![檢視診斷記錄](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="86018-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="86018-137">hello 記錄檔以分類**稽核記錄檔**和**要求記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="86018-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![記錄項目](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="86018-139">要求記錄檔擷取 hello Data Lake Analytics 帳戶上所做的每個應用程式開發介面要求。</span><span class="sxs-lookup"><span data-stu-id="86018-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="86018-140">稽核記錄是類似的 toorequest 記錄，但是提供更詳盡的 hello 作業細分。</span><span class="sxs-lookup"><span data-stu-id="86018-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="86018-141">例如，要求記錄中的一個上傳 API 呼叫可能會致使其稽核記錄出現多個「附加」作業。</span><span class="sxs-lookup"><span data-stu-id="86018-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="86018-142">按一下 hello**下載**記錄的記錄檔項目 toodownload 的連結。</span><span class="sxs-lookup"><span data-stu-id="86018-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="86018-143">使用包含記錄資料的 hello Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="86018-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="86018-144">開啟 Data Lake Analytics 與記錄相關聯的 hello Azure 儲存體帳戶刀鋒視窗，然後按一下__Blob__。</span><span class="sxs-lookup"><span data-stu-id="86018-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="86018-145">hello **Blob 服務**刀鋒視窗會列出兩個容器。</span><span class="sxs-lookup"><span data-stu-id="86018-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="86018-146">![檢視診斷記錄](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="86018-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="86018-147">hello 容器**insights 記錄檔稽核**包含 hello 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="86018-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="86018-148">hello 容器**insights 記錄要求**包含 hello 要求記錄檔。</span><span class="sxs-lookup"><span data-stu-id="86018-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="86018-149">這些容器中，內 hello 記錄檔會儲存在下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="86018-149">Within these containers, hello logs are stored under hello following structure:</span></span>

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
   > <span data-ttu-id="86018-150">hello `##` hello 路徑中的項目包含 hello 年、 月、 日和小時建立記錄檔中的 hello。</span><span class="sxs-lookup"><span data-stu-id="86018-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="86018-151">Data Lake Analytics 每小時會建立一個檔案，因此 `m=` 一律會包含 `00` 值。</span><span class="sxs-lookup"><span data-stu-id="86018-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="86018-152">例如，可能是 hello 完整路徑 tooan 稽核記錄檔：</span><span class="sxs-lookup"><span data-stu-id="86018-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="86018-153">同樣地，可能是 hello 完整路徑 tooa 要求記錄檔：</span><span class="sxs-lookup"><span data-stu-id="86018-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="86018-154">記錄檔結構</span><span class="sxs-lookup"><span data-stu-id="86018-154">Log structure</span></span>

<span data-ttu-id="86018-155">hello 稽核和要求記錄檔會結構化的 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="86018-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="86018-156">要求記錄</span><span class="sxs-lookup"><span data-stu-id="86018-156">Request logs</span></span>

<span data-ttu-id="86018-157">以下是範例項目 hello JSON 格式要求記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="86018-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="86018-158">每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="86018-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="request-log-schema"></a><span data-ttu-id="86018-159">要求記錄的結構描述</span><span class="sxs-lookup"><span data-stu-id="86018-159">Request log schema</span></span>

| <span data-ttu-id="86018-160">Name</span><span class="sxs-lookup"><span data-stu-id="86018-160">Name</span></span> | <span data-ttu-id="86018-161">類型</span><span class="sxs-lookup"><span data-stu-id="86018-161">Type</span></span> | <span data-ttu-id="86018-162">說明</span><span class="sxs-lookup"><span data-stu-id="86018-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86018-163">分析</span><span class="sxs-lookup"><span data-stu-id="86018-163">time</span></span> |<span data-ttu-id="86018-164">String</span><span class="sxs-lookup"><span data-stu-id="86018-164">String</span></span> |<span data-ttu-id="86018-165">hello 時間戳記 （UTC) 的 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="86018-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="86018-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="86018-166">resourceId</span></span> |<span data-ttu-id="86018-167">String</span><span class="sxs-lookup"><span data-stu-id="86018-167">String</span></span> |<span data-ttu-id="86018-168">hello hello 資源作業所需的識別項將會置於</span><span class="sxs-lookup"><span data-stu-id="86018-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="86018-169">category</span><span class="sxs-lookup"><span data-stu-id="86018-169">category</span></span> |<span data-ttu-id="86018-170">String</span><span class="sxs-lookup"><span data-stu-id="86018-170">String</span></span> |<span data-ttu-id="86018-171">hello 記錄類別目錄。</span><span class="sxs-lookup"><span data-stu-id="86018-171">hello log category.</span></span> <span data-ttu-id="86018-172">例如， **要求**。</span><span class="sxs-lookup"><span data-stu-id="86018-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="86018-173">operationName</span><span class="sxs-lookup"><span data-stu-id="86018-173">operationName</span></span> |<span data-ttu-id="86018-174">String</span><span class="sxs-lookup"><span data-stu-id="86018-174">String</span></span> |<span data-ttu-id="86018-175">Hello 作業所記錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="86018-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="86018-176">例如，GetAggregatedJobHistory。</span><span class="sxs-lookup"><span data-stu-id="86018-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="86018-177">resultType</span><span class="sxs-lookup"><span data-stu-id="86018-177">resultType</span></span> |<span data-ttu-id="86018-178">String</span><span class="sxs-lookup"><span data-stu-id="86018-178">String</span></span> |<span data-ttu-id="86018-179">hello 作業的狀態 hello，例如 200。</span><span class="sxs-lookup"><span data-stu-id="86018-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="86018-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="86018-180">callerIpAddress</span></span> |<span data-ttu-id="86018-181">String</span><span class="sxs-lookup"><span data-stu-id="86018-181">String</span></span> |<span data-ttu-id="86018-182">hello 發出 hello 要求的用戶端 hello IP 位址</span><span class="sxs-lookup"><span data-stu-id="86018-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="86018-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="86018-183">correlationId</span></span> |<span data-ttu-id="86018-184">String</span><span class="sxs-lookup"><span data-stu-id="86018-184">String</span></span> |<span data-ttu-id="86018-185">hello hello 記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="86018-185">hello identifier of hello log.</span></span> <span data-ttu-id="86018-186">這個值可以是使用的 toogroup 一組相關的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="86018-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="86018-187">身分識別</span><span class="sxs-lookup"><span data-stu-id="86018-187">identity</span></span> |<span data-ttu-id="86018-188">Object</span><span class="sxs-lookup"><span data-stu-id="86018-188">Object</span></span> |<span data-ttu-id="86018-189">產生的 hello 記錄的 hello 身分識別</span><span class="sxs-lookup"><span data-stu-id="86018-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="86018-190">屬性</span><span class="sxs-lookup"><span data-stu-id="86018-190">properties</span></span> |<span data-ttu-id="86018-191">JSON</span><span class="sxs-lookup"><span data-stu-id="86018-191">JSON</span></span> |<span data-ttu-id="86018-192">請參閱 hello 下一節 （要求記錄檔的屬性結構描述），如需詳細資訊</span><span class="sxs-lookup"><span data-stu-id="86018-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="86018-193">要求記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="86018-193">Request log properties schema</span></span>

| <span data-ttu-id="86018-194">Name</span><span class="sxs-lookup"><span data-stu-id="86018-194">Name</span></span> | <span data-ttu-id="86018-195">類型</span><span class="sxs-lookup"><span data-stu-id="86018-195">Type</span></span> | <span data-ttu-id="86018-196">說明</span><span class="sxs-lookup"><span data-stu-id="86018-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86018-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="86018-197">HttpMethod</span></span> |<span data-ttu-id="86018-198">String</span><span class="sxs-lookup"><span data-stu-id="86018-198">String</span></span> |<span data-ttu-id="86018-199">hello HTTP 方法 hello 作業使用。</span><span class="sxs-lookup"><span data-stu-id="86018-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="86018-200">例如，GET。</span><span class="sxs-lookup"><span data-stu-id="86018-200">For example, GET.</span></span> |
| <span data-ttu-id="86018-201">Path</span><span class="sxs-lookup"><span data-stu-id="86018-201">Path</span></span> |<span data-ttu-id="86018-202">String</span><span class="sxs-lookup"><span data-stu-id="86018-202">String</span></span> |<span data-ttu-id="86018-203">hello 路徑 hello 作業上執行</span><span class="sxs-lookup"><span data-stu-id="86018-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="86018-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="86018-204">RequestContentLength</span></span> |<span data-ttu-id="86018-205">int</span><span class="sxs-lookup"><span data-stu-id="86018-205">int</span></span> |<span data-ttu-id="86018-206">hello hello HTTP 要求內容長度</span><span class="sxs-lookup"><span data-stu-id="86018-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="86018-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="86018-207">ClientRequestId</span></span> |<span data-ttu-id="86018-208">String</span><span class="sxs-lookup"><span data-stu-id="86018-208">String</span></span> |<span data-ttu-id="86018-209">hello 識別碼可唯一識別此要求</span><span class="sxs-lookup"><span data-stu-id="86018-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="86018-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="86018-210">StartTime</span></span> |<span data-ttu-id="86018-211">String</span><span class="sxs-lookup"><span data-stu-id="86018-211">String</span></span> |<span data-ttu-id="86018-212">hello hello 接收伺服器 hello 要求時間</span><span class="sxs-lookup"><span data-stu-id="86018-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="86018-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="86018-213">EndTime</span></span> |<span data-ttu-id="86018-214">String</span><span class="sxs-lookup"><span data-stu-id="86018-214">String</span></span> |<span data-ttu-id="86018-215">hello 的 hello 伺服器送出回應的時間</span><span class="sxs-lookup"><span data-stu-id="86018-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="86018-216">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="86018-216">Audit logs</span></span>

<span data-ttu-id="86018-217">以下是範例項目 hello JSON 格式的稽核記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="86018-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="86018-218">每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="86018-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="audit-log-schema"></a><span data-ttu-id="86018-219">稽核記錄的結構描述</span><span class="sxs-lookup"><span data-stu-id="86018-219">Audit log schema</span></span>

| <span data-ttu-id="86018-220">Name</span><span class="sxs-lookup"><span data-stu-id="86018-220">Name</span></span> | <span data-ttu-id="86018-221">類型</span><span class="sxs-lookup"><span data-stu-id="86018-221">Type</span></span> | <span data-ttu-id="86018-222">說明</span><span class="sxs-lookup"><span data-stu-id="86018-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86018-223">分析</span><span class="sxs-lookup"><span data-stu-id="86018-223">time</span></span> |<span data-ttu-id="86018-224">String</span><span class="sxs-lookup"><span data-stu-id="86018-224">String</span></span> |<span data-ttu-id="86018-225">hello 時間戳記 （UTC) 的 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="86018-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="86018-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="86018-226">resourceId</span></span> |<span data-ttu-id="86018-227">String</span><span class="sxs-lookup"><span data-stu-id="86018-227">String</span></span> |<span data-ttu-id="86018-228">hello hello 資源作業所需的識別項將會置於</span><span class="sxs-lookup"><span data-stu-id="86018-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="86018-229">category</span><span class="sxs-lookup"><span data-stu-id="86018-229">category</span></span> |<span data-ttu-id="86018-230">String</span><span class="sxs-lookup"><span data-stu-id="86018-230">String</span></span> |<span data-ttu-id="86018-231">hello 記錄類別目錄。</span><span class="sxs-lookup"><span data-stu-id="86018-231">hello log category.</span></span> <span data-ttu-id="86018-232">例如， **稽核**。</span><span class="sxs-lookup"><span data-stu-id="86018-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="86018-233">operationName</span><span class="sxs-lookup"><span data-stu-id="86018-233">operationName</span></span> |<span data-ttu-id="86018-234">String</span><span class="sxs-lookup"><span data-stu-id="86018-234">String</span></span> |<span data-ttu-id="86018-235">Hello 作業所記錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="86018-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="86018-236">例如，JobSubmitted。</span><span class="sxs-lookup"><span data-stu-id="86018-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="86018-237">resultType</span><span class="sxs-lookup"><span data-stu-id="86018-237">resultType</span></span> |<span data-ttu-id="86018-238">String</span><span class="sxs-lookup"><span data-stu-id="86018-238">String</span></span> |<span data-ttu-id="86018-239">Hello 作業狀態 (operationName) 子狀態。</span><span class="sxs-lookup"><span data-stu-id="86018-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="86018-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="86018-240">resultSignature</span></span> |<span data-ttu-id="86018-241">String</span><span class="sxs-lookup"><span data-stu-id="86018-241">String</span></span> |<span data-ttu-id="86018-242">在 hello 作業狀態 (operationName) 上的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="86018-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="86018-243">身分識別</span><span class="sxs-lookup"><span data-stu-id="86018-243">identity</span></span> |<span data-ttu-id="86018-244">String</span><span class="sxs-lookup"><span data-stu-id="86018-244">String</span></span> |<span data-ttu-id="86018-245">hello 要求 hello 作業的使用者。</span><span class="sxs-lookup"><span data-stu-id="86018-245">hello user that requested hello operation.</span></span> <span data-ttu-id="86018-246">例如： susan@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="86018-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="86018-247">properties</span><span class="sxs-lookup"><span data-stu-id="86018-247">properties</span></span> |<span data-ttu-id="86018-248">JSON</span><span class="sxs-lookup"><span data-stu-id="86018-248">JSON</span></span> |<span data-ttu-id="86018-249">請參閱 hello 下一節 （稽核記錄檔的屬性結構描述），如需詳細資訊</span><span class="sxs-lookup"><span data-stu-id="86018-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="86018-250">**resultType**和**resultSignature** hello 作業的結果，提供相關資訊，並只能包含一個值，如果作業已完成。</span><span class="sxs-lookup"><span data-stu-id="86018-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="86018-251">例如，只有當 **operationName** 包含 **JobStarted** 或 **JobEnded** 的值時，它們才會包含值。</span><span class="sxs-lookup"><span data-stu-id="86018-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="86018-252">稽核記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="86018-252">Audit log properties schema</span></span>

| <span data-ttu-id="86018-253">Name</span><span class="sxs-lookup"><span data-stu-id="86018-253">Name</span></span> | <span data-ttu-id="86018-254">類型</span><span class="sxs-lookup"><span data-stu-id="86018-254">Type</span></span> | <span data-ttu-id="86018-255">說明</span><span class="sxs-lookup"><span data-stu-id="86018-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="86018-256">JobId</span><span class="sxs-lookup"><span data-stu-id="86018-256">JobId</span></span> |<span data-ttu-id="86018-257">String</span><span class="sxs-lookup"><span data-stu-id="86018-257">String</span></span> |<span data-ttu-id="86018-258">hello ID 指派的 toohello 工作</span><span class="sxs-lookup"><span data-stu-id="86018-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="86018-259">JobName</span><span class="sxs-lookup"><span data-stu-id="86018-259">JobName</span></span> |<span data-ttu-id="86018-260">String</span><span class="sxs-lookup"><span data-stu-id="86018-260">String</span></span> |<span data-ttu-id="86018-261">hello 作業所提供的 hello 名稱</span><span class="sxs-lookup"><span data-stu-id="86018-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="86018-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="86018-262">JobRunTime</span></span> |<span data-ttu-id="86018-263">String</span><span class="sxs-lookup"><span data-stu-id="86018-263">String</span></span> |<span data-ttu-id="86018-264">使用 tooprocess hello 作業 hello 執行階段。</span><span class="sxs-lookup"><span data-stu-id="86018-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="86018-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="86018-265">SubmitTime</span></span> |<span data-ttu-id="86018-266">String</span><span class="sxs-lookup"><span data-stu-id="86018-266">String</span></span> |<span data-ttu-id="86018-267">hello 時間 （以 utc 格式） 提交該 hello 作業</span><span class="sxs-lookup"><span data-stu-id="86018-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="86018-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="86018-268">StartTime</span></span> |<span data-ttu-id="86018-269">String</span><span class="sxs-lookup"><span data-stu-id="86018-269">String</span></span> |<span data-ttu-id="86018-270">hello 時間 hello 作業開始執行之後提交 （以 utc 格式）</span><span class="sxs-lookup"><span data-stu-id="86018-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="86018-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="86018-271">EndTime</span></span> |<span data-ttu-id="86018-272">String</span><span class="sxs-lookup"><span data-stu-id="86018-272">String</span></span> |<span data-ttu-id="86018-273">hello 時間 hello 作業已結束</span><span class="sxs-lookup"><span data-stu-id="86018-273">hello time hello job ended</span></span> |
| <span data-ttu-id="86018-274">平行處理原則</span><span class="sxs-lookup"><span data-stu-id="86018-274">Parallelism</span></span> |<span data-ttu-id="86018-275">String</span><span class="sxs-lookup"><span data-stu-id="86018-275">String</span></span> |<span data-ttu-id="86018-276">Data Lake Analytics 單位提交期間要求此作業的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="86018-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="86018-277">**SubmitTime**、**StartTime**、**EndTime** 和 **Parallelism** 提供作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="86018-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="86018-278">這些項目只會在作業啟動或完成時才包含值。</span><span class="sxs-lookup"><span data-stu-id="86018-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="86018-279">例如， **SubmitTime**只包含值之後**operationName** hello 值**JobSubmitted**。</span><span class="sxs-lookup"><span data-stu-id="86018-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="86018-280">處理序 hello 記錄資料</span><span class="sxs-lookup"><span data-stu-id="86018-280">Process hello log data</span></span>

<span data-ttu-id="86018-281">Azure Data Lake Analytics 提供的範例如何 tooprocess 和分析 hello 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="86018-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="86018-282">您可以找到在 hello 範例[https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)。</span><span class="sxs-lookup"><span data-stu-id="86018-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86018-283">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86018-283">Next steps</span></span>
* [<span data-ttu-id="86018-284">Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="86018-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
