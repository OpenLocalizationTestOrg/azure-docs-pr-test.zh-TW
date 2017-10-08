---
title: "Azure Data Lake Store aaaViewing 診斷記錄檔 |Microsoft 文件"
description: "了解如何為 Azure Data Lake Store 的 toosetup 及存取診斷記錄檔 "
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
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="028a5-103">存取 Azure Data Lake Store 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="028a5-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="028a5-104">深入了解如何針對您的帳戶收集 tooenable Data Lake Store 帳戶和 tooview hello 的記錄檔的診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="028a5-104">Learn about how tooenable diagnostic logging for your Data Lake Store account and how tooview hello logs collected for your account.</span></span>

<span data-ttu-id="028a5-105">組織可以啟用其帳戶 toocollect 資料存取稽核記錄，提供使用者存取 hello data hello 資料存取的頻率、 資料量的資訊，例如清單會儲存在 hello 的 Azure Data Lake Store 的診斷記錄帳戶等等。</span><span class="sxs-lookup"><span data-stu-id="028a5-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account toocollect data access audit trails that provides information such as list of users accessing hello data, how frequently hello data is accessed, how much data is stored in hello account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="028a5-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="028a5-106">Prerequisites</span></span>
* <span data-ttu-id="028a5-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="028a5-107">**An Azure subscription**.</span></span> <span data-ttu-id="028a5-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="028a5-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="028a5-109">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="028a5-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="028a5-110">請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="028a5-110">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="028a5-111">啟用 Data Lake Store 帳戶的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="028a5-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="028a5-112">登入新 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="028a5-112">Sign on toohello new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="028a5-113">開啟 Data Lake Store 帳戶，接著在 Data Lake Store 帳戶刀鋒視窗中依序按一下 [設定] 和 [診斷記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="028a5-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="028a5-114">在 hello**診斷記錄檔**刀鋒視窗中，按一下 **開啟診斷**。</span><span class="sxs-lookup"><span data-stu-id="028a5-114">In hello **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="028a5-115">![啟用診斷記錄](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "啟用診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="028a5-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="028a5-116">在 hello**診斷**刀鋒視窗中，進行下列變更 tooconfigure 診斷記錄的 hello。</span><span class="sxs-lookup"><span data-stu-id="028a5-116">In hello **Diagnostic** blade, make hello following changes tooconfigure diagnostic logging.</span></span>
   
    <span data-ttu-id="028a5-117">![啟用診斷記錄](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "啟用診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="028a5-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="028a5-118">設定**狀態**太**上**tooenable 診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="028a5-118">Set **Status** too**On** tooenable diagnostic logging.</span></span>
   * <span data-ttu-id="028a5-119">您可以選擇 toostore/處理序 hello 資料不同的方式。</span><span class="sxs-lookup"><span data-stu-id="028a5-119">You can choose toostore/process hello data in different ways.</span></span>
     
        * <span data-ttu-id="028a5-120">選取 hello 選項太**封存 tooa 儲存體帳戶**toostore 記錄 tooan Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="028a5-120">Select hello option too**Archive tooa storage account** toostore logs tooan Azure Storage account.</span></span> <span data-ttu-id="028a5-121">如果您想要將在日後會處理批次的 tooarchive hello 資料，您可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="028a5-121">You use this option if you want tooarchive hello data that will be batch-processed at a later date.</span></span> <span data-ttu-id="028a5-122">如果您選取這個選項必須提供 Azure 儲存體帳戶 toosave hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="028a5-122">If you select this option you must provide an Azure Storage account toosave hello logs to.</span></span>
        
        * <span data-ttu-id="028a5-123">選取 hello 選項太**資料流 tooan 事件中心**toostream 記錄資料 tooan Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="028a5-123">Select hello option too**Stream tooan event hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="028a5-124">最有可能您會使用這個選項有下游處理管線 tooanalyze 連入即時記錄檔。</span><span class="sxs-lookup"><span data-stu-id="028a5-124">Most likely you will use this option if you have a downstream processing pipeline tooanalyze incoming logs at real time.</span></span> <span data-ttu-id="028a5-125">如果您選取此選項時，您必須提供 hello Azure 事件中心想 toouse hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="028a5-125">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

        * <span data-ttu-id="028a5-126">選取 hello 選項太**傳送 tooLog 分析**toouse hello Azure 記錄分析服務 tooanalyze hello 產生記錄檔資料。</span><span class="sxs-lookup"><span data-stu-id="028a5-126">Select hello option too**Send tooLog Analytics** toouse hello Azure Log Analytics service tooanalyze hello generated log data.</span></span> <span data-ttu-id="028a5-127">如果您選取此選項時，您必須提供 hello 詳細說明 hello Operations Management Suite 工作區，您就可以使用 hello 執行記錄分析。</span><span class="sxs-lookup"><span data-stu-id="028a5-127">If you select this option, you must provide hello details for hello Operations Management Suite workspace that you would use hello perform log analysis.</span></span>
     
   * <span data-ttu-id="028a5-128">指定是否要 tooget 稽核記錄檔或要求記錄檔或兩者。</span><span class="sxs-lookup"><span data-stu-id="028a5-128">Specify whether you want tooget audit logs or request logs or both.</span></span>
   * <span data-ttu-id="028a5-129">指定必須保留 hello 資料的 hello 天數。</span><span class="sxs-lookup"><span data-stu-id="028a5-129">Specify hello number of days for which hello data must be retained.</span></span> <span data-ttu-id="028a5-130">只有適用於您要使用 Azure 儲存體帳戶 tooarchive 記錄資料保留。</span><span class="sxs-lookup"><span data-stu-id="028a5-130">Retention is only applicable if you are using Azure storage account tooarchive log data.</span></span>
   * <span data-ttu-id="028a5-131">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="028a5-131">Click **Save**.</span></span>

<span data-ttu-id="028a5-132">一旦您啟用了診斷設定，您可以觀看 hello 登入 hello**診斷記錄檔** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="028a5-132">Once you have enabled diagnostic settings, you can watch hello logs in hello **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="028a5-133">檢視 Data Lake Store 帳戶的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="028a5-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="028a5-134">有兩種方式的 Data Lake Store 帳戶 tooview hello 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="028a5-134">There are two ways tooview hello log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="028a5-135">從 hello Data Lake Store 帳戶檢視設定</span><span class="sxs-lookup"><span data-stu-id="028a5-135">From hello Data Lake Store account settings view</span></span>
* <span data-ttu-id="028a5-136">從儲存 hello 資料 hello Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="028a5-136">From hello Azure Storage account where hello data is stored</span></span>

### <a name="using-hello-data-lake-store-settings-view"></a><span data-ttu-id="028a5-137">使用 hello 資料湖存放區設定檢視</span><span class="sxs-lookup"><span data-stu-id="028a5-137">Using hello Data Lake Store Settings view</span></span>
1. <span data-ttu-id="028a5-138">在 Data Lake Store 帳戶的 [設定] 刀鋒視窗中，按一下 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="028a5-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="028a5-139">![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="028a5-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="028a5-140">在 hello**診斷記錄檔**刀鋒視窗中，您應該會看見 hello 記錄依分類**稽核記錄檔**和**要求記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="028a5-140">In hello **Diagnostic Logs** blade, you should see hello logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="028a5-141">要求記錄檔擷取 hello Data Lake Store 帳戶上所做的每個應用程式開發介面要求。</span><span class="sxs-lookup"><span data-stu-id="028a5-141">Request logs capture every API request made on hello Data Lake Store account.</span></span>
   * <span data-ttu-id="028a5-142">稽核記錄是類似的 toorequest 記錄，但是提供更詳盡的 hello Data Lake Store 帳戶上所執行的 hello 作業細分。</span><span class="sxs-lookup"><span data-stu-id="028a5-142">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations being performed on hello Data Lake Store account.</span></span> <span data-ttu-id="028a5-143">例如，單一的上傳應用程式開發介面呼叫要求記錄檔中可能會導致 hello 稽核記錄中的多個 「 附加 」 作業。</span><span class="sxs-lookup"><span data-stu-id="028a5-143">For example, a single upload API call in request logs might result in multiple "Append" operations in hello audit logs.</span></span>
3. <span data-ttu-id="028a5-144">按一下 hello**下載**針對每個連結記錄項目 toodownload hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="028a5-144">Click hello **Download** link against each log entry toodownload hello logs.</span></span>

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="028a5-145">從 hello Azure 儲存體帳戶，其中包含記錄資料</span><span class="sxs-lookup"><span data-stu-id="028a5-145">From hello Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="028a5-146">開啟記錄，與資料湖存放區相關聯的 hello Azure 儲存體帳戶刀鋒視窗，然後按一下Blob。</span><span class="sxs-lookup"><span data-stu-id="028a5-146">Open hello Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="028a5-147">hello **Blob 服務**刀鋒視窗會列出兩個容器。</span><span class="sxs-lookup"><span data-stu-id="028a5-147">hello **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="028a5-148">![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="028a5-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="028a5-149">hello 容器**insights 記錄檔稽核**包含 hello 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="028a5-149">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="028a5-150">hello 容器**insights 記錄要求**包含 hello 要求記錄檔。</span><span class="sxs-lookup"><span data-stu-id="028a5-150">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="028a5-151">這些容器中，內 hello 記錄檔會儲存在下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="028a5-151">Within these containers, hello logs are stored under hello following structure.</span></span>
   
    <span data-ttu-id="028a5-152">![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "檢視診斷記錄")</span><span class="sxs-lookup"><span data-stu-id="028a5-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="028a5-153">例如，可能是 hello 完整路徑 tooan 稽核記錄檔`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="028a5-153">As an example, hello complete path tooan audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="028a5-154">Hello 完整路徑 tooa 要求記錄檔可能是 similary，`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="028a5-154">Similary, hello complete path tooa request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-hello-structure-of-hello-log-data"></a><span data-ttu-id="028a5-155">了解 hello hello 記錄資料結構</span><span class="sxs-lookup"><span data-stu-id="028a5-155">Understand hello structure of hello log data</span></span>
<span data-ttu-id="028a5-156">hello 稽核，並要求記錄檔是以 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="028a5-156">hello audit and request logs are in a JSON format.</span></span> <span data-ttu-id="028a5-157">在本節中，我們會查看 hello 結構的 JSON 的要求，稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="028a5-157">In this section, we look at hello structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="028a5-158">要求記錄</span><span class="sxs-lookup"><span data-stu-id="028a5-158">Request logs</span></span>
<span data-ttu-id="028a5-159">以下是範例項目 hello JSON 格式要求記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="028a5-159">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="028a5-160">每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="028a5-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="request-log-schema"></a><span data-ttu-id="028a5-161">要求記錄的結構描述</span><span class="sxs-lookup"><span data-stu-id="028a5-161">Request log schema</span></span>
| <span data-ttu-id="028a5-162">Name</span><span class="sxs-lookup"><span data-stu-id="028a5-162">Name</span></span> | <span data-ttu-id="028a5-163">類型</span><span class="sxs-lookup"><span data-stu-id="028a5-163">Type</span></span> | <span data-ttu-id="028a5-164">說明</span><span class="sxs-lookup"><span data-stu-id="028a5-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="028a5-165">分析</span><span class="sxs-lookup"><span data-stu-id="028a5-165">time</span></span> |<span data-ttu-id="028a5-166">String</span><span class="sxs-lookup"><span data-stu-id="028a5-166">String</span></span> |<span data-ttu-id="028a5-167">hello 時間戳記 （UTC) 的 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="028a5-167">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="028a5-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="028a5-168">resourceId</span></span> |<span data-ttu-id="028a5-169">String</span><span class="sxs-lookup"><span data-stu-id="028a5-169">String</span></span> |<span data-ttu-id="028a5-170">hello hello 資源作業所需的 ID 將會置於</span><span class="sxs-lookup"><span data-stu-id="028a5-170">hello ID of hello resource that operation took place on</span></span> |
| <span data-ttu-id="028a5-171">category</span><span class="sxs-lookup"><span data-stu-id="028a5-171">category</span></span> |<span data-ttu-id="028a5-172">String</span><span class="sxs-lookup"><span data-stu-id="028a5-172">String</span></span> |<span data-ttu-id="028a5-173">hello 記錄類別目錄。</span><span class="sxs-lookup"><span data-stu-id="028a5-173">hello log category.</span></span> <span data-ttu-id="028a5-174">例如， **要求**。</span><span class="sxs-lookup"><span data-stu-id="028a5-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="028a5-175">operationName</span><span class="sxs-lookup"><span data-stu-id="028a5-175">operationName</span></span> |<span data-ttu-id="028a5-176">String</span><span class="sxs-lookup"><span data-stu-id="028a5-176">String</span></span> |<span data-ttu-id="028a5-177">Hello 作業所記錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="028a5-177">Name of hello operation that is logged.</span></span> <span data-ttu-id="028a5-178">例如，getfilestatus。</span><span class="sxs-lookup"><span data-stu-id="028a5-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="028a5-179">resultType</span><span class="sxs-lookup"><span data-stu-id="028a5-179">resultType</span></span> |<span data-ttu-id="028a5-180">String</span><span class="sxs-lookup"><span data-stu-id="028a5-180">String</span></span> |<span data-ttu-id="028a5-181">hello 作業的狀態 hello，例如 200。</span><span class="sxs-lookup"><span data-stu-id="028a5-181">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="028a5-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="028a5-182">callerIpAddress</span></span> |<span data-ttu-id="028a5-183">String</span><span class="sxs-lookup"><span data-stu-id="028a5-183">String</span></span> |<span data-ttu-id="028a5-184">hello 發出 hello 要求的用戶端 hello IP 位址</span><span class="sxs-lookup"><span data-stu-id="028a5-184">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="028a5-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="028a5-185">correlationId</span></span> |<span data-ttu-id="028a5-186">String</span><span class="sxs-lookup"><span data-stu-id="028a5-186">String</span></span> |<span data-ttu-id="028a5-187">hello 識別碼 hello 記錄檔可以 toogroup 同時使用一組相關的記錄項目</span><span class="sxs-lookup"><span data-stu-id="028a5-187">hello id of hello log that can used toogroup together a set of related log entries</span></span> |
| <span data-ttu-id="028a5-188">身分識別</span><span class="sxs-lookup"><span data-stu-id="028a5-188">identity</span></span> |<span data-ttu-id="028a5-189">Object</span><span class="sxs-lookup"><span data-stu-id="028a5-189">Object</span></span> |<span data-ttu-id="028a5-190">產生的 hello 記錄的 hello 身分識別</span><span class="sxs-lookup"><span data-stu-id="028a5-190">hello identity that generated hello log</span></span> |
| <span data-ttu-id="028a5-191">屬性</span><span class="sxs-lookup"><span data-stu-id="028a5-191">properties</span></span> |<span data-ttu-id="028a5-192">JSON</span><span class="sxs-lookup"><span data-stu-id="028a5-192">JSON</span></span> |<span data-ttu-id="028a5-193">如需詳細資料，請參閱下文</span><span class="sxs-lookup"><span data-stu-id="028a5-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="028a5-194">要求記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="028a5-194">Request log properties schema</span></span>
| <span data-ttu-id="028a5-195">Name</span><span class="sxs-lookup"><span data-stu-id="028a5-195">Name</span></span> | <span data-ttu-id="028a5-196">類型</span><span class="sxs-lookup"><span data-stu-id="028a5-196">Type</span></span> | <span data-ttu-id="028a5-197">說明</span><span class="sxs-lookup"><span data-stu-id="028a5-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="028a5-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="028a5-198">HttpMethod</span></span> |<span data-ttu-id="028a5-199">String</span><span class="sxs-lookup"><span data-stu-id="028a5-199">String</span></span> |<span data-ttu-id="028a5-200">hello HTTP 方法 hello 作業使用。</span><span class="sxs-lookup"><span data-stu-id="028a5-200">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="028a5-201">例如，GET。</span><span class="sxs-lookup"><span data-stu-id="028a5-201">For example, GET.</span></span> |
| <span data-ttu-id="028a5-202">Path</span><span class="sxs-lookup"><span data-stu-id="028a5-202">Path</span></span> |<span data-ttu-id="028a5-203">String</span><span class="sxs-lookup"><span data-stu-id="028a5-203">String</span></span> |<span data-ttu-id="028a5-204">hello 路徑 hello 作業上執行</span><span class="sxs-lookup"><span data-stu-id="028a5-204">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="028a5-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="028a5-205">RequestContentLength</span></span> |<span data-ttu-id="028a5-206">int</span><span class="sxs-lookup"><span data-stu-id="028a5-206">int</span></span> |<span data-ttu-id="028a5-207">hello hello HTTP 要求內容長度</span><span class="sxs-lookup"><span data-stu-id="028a5-207">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="028a5-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="028a5-208">ClientRequestId</span></span> |<span data-ttu-id="028a5-209">String</span><span class="sxs-lookup"><span data-stu-id="028a5-209">String</span></span> |<span data-ttu-id="028a5-210">hello 可唯一識別這個要求識別碼</span><span class="sxs-lookup"><span data-stu-id="028a5-210">hello Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="028a5-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="028a5-211">StartTime</span></span> |<span data-ttu-id="028a5-212">String</span><span class="sxs-lookup"><span data-stu-id="028a5-212">String</span></span> |<span data-ttu-id="028a5-213">hello hello 接收伺服器 hello 要求時間</span><span class="sxs-lookup"><span data-stu-id="028a5-213">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="028a5-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="028a5-214">EndTime</span></span> |<span data-ttu-id="028a5-215">String</span><span class="sxs-lookup"><span data-stu-id="028a5-215">String</span></span> |<span data-ttu-id="028a5-216">hello 的 hello 伺服器送出回應的時間</span><span class="sxs-lookup"><span data-stu-id="028a5-216">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="028a5-217">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="028a5-217">Audit logs</span></span>
<span data-ttu-id="028a5-218">以下是範例項目 hello JSON 格式的稽核記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="028a5-218">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="028a5-219">每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列</span><span class="sxs-lookup"><span data-stu-id="028a5-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

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

#### <a name="audit-log-schema"></a><span data-ttu-id="028a5-220">稽核記錄的結構描述</span><span class="sxs-lookup"><span data-stu-id="028a5-220">Audit log schema</span></span>
| <span data-ttu-id="028a5-221">Name</span><span class="sxs-lookup"><span data-stu-id="028a5-221">Name</span></span> | <span data-ttu-id="028a5-222">類型</span><span class="sxs-lookup"><span data-stu-id="028a5-222">Type</span></span> | <span data-ttu-id="028a5-223">說明</span><span class="sxs-lookup"><span data-stu-id="028a5-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="028a5-224">分析</span><span class="sxs-lookup"><span data-stu-id="028a5-224">time</span></span> |<span data-ttu-id="028a5-225">String</span><span class="sxs-lookup"><span data-stu-id="028a5-225">String</span></span> |<span data-ttu-id="028a5-226">hello 時間戳記 （UTC) 的 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="028a5-226">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="028a5-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="028a5-227">resourceId</span></span> |<span data-ttu-id="028a5-228">String</span><span class="sxs-lookup"><span data-stu-id="028a5-228">String</span></span> |<span data-ttu-id="028a5-229">hello hello 資源作業所需的 ID 將會置於</span><span class="sxs-lookup"><span data-stu-id="028a5-229">hello ID of hello resource that operation took place on</span></span> |
| <span data-ttu-id="028a5-230">category</span><span class="sxs-lookup"><span data-stu-id="028a5-230">category</span></span> |<span data-ttu-id="028a5-231">String</span><span class="sxs-lookup"><span data-stu-id="028a5-231">String</span></span> |<span data-ttu-id="028a5-232">hello 記錄類別目錄。</span><span class="sxs-lookup"><span data-stu-id="028a5-232">hello log category.</span></span> <span data-ttu-id="028a5-233">例如， **稽核**。</span><span class="sxs-lookup"><span data-stu-id="028a5-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="028a5-234">operationName</span><span class="sxs-lookup"><span data-stu-id="028a5-234">operationName</span></span> |<span data-ttu-id="028a5-235">String</span><span class="sxs-lookup"><span data-stu-id="028a5-235">String</span></span> |<span data-ttu-id="028a5-236">Hello 作業所記錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="028a5-236">Name of hello operation that is logged.</span></span> <span data-ttu-id="028a5-237">例如，getfilestatus。</span><span class="sxs-lookup"><span data-stu-id="028a5-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="028a5-238">resultType</span><span class="sxs-lookup"><span data-stu-id="028a5-238">resultType</span></span> |<span data-ttu-id="028a5-239">String</span><span class="sxs-lookup"><span data-stu-id="028a5-239">String</span></span> |<span data-ttu-id="028a5-240">hello 作業的狀態 hello，例如 200。</span><span class="sxs-lookup"><span data-stu-id="028a5-240">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="028a5-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="028a5-241">correlationId</span></span> |<span data-ttu-id="028a5-242">String</span><span class="sxs-lookup"><span data-stu-id="028a5-242">String</span></span> |<span data-ttu-id="028a5-243">hello 識別碼 hello 記錄檔可以 toogroup 同時使用一組相關的記錄項目</span><span class="sxs-lookup"><span data-stu-id="028a5-243">hello id of hello log that can used toogroup together a set of related log entries</span></span> |
| <span data-ttu-id="028a5-244">身分識別</span><span class="sxs-lookup"><span data-stu-id="028a5-244">identity</span></span> |<span data-ttu-id="028a5-245">Object</span><span class="sxs-lookup"><span data-stu-id="028a5-245">Object</span></span> |<span data-ttu-id="028a5-246">產生的 hello 記錄的 hello 身分識別</span><span class="sxs-lookup"><span data-stu-id="028a5-246">hello identity that generated hello log</span></span> |
| <span data-ttu-id="028a5-247">屬性</span><span class="sxs-lookup"><span data-stu-id="028a5-247">properties</span></span> |<span data-ttu-id="028a5-248">JSON</span><span class="sxs-lookup"><span data-stu-id="028a5-248">JSON</span></span> |<span data-ttu-id="028a5-249">如需詳細資料，請參閱下文</span><span class="sxs-lookup"><span data-stu-id="028a5-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="028a5-250">稽核記錄屬性結構描述</span><span class="sxs-lookup"><span data-stu-id="028a5-250">Audit log properties schema</span></span>
| <span data-ttu-id="028a5-251">Name</span><span class="sxs-lookup"><span data-stu-id="028a5-251">Name</span></span> | <span data-ttu-id="028a5-252">類型</span><span class="sxs-lookup"><span data-stu-id="028a5-252">Type</span></span> | <span data-ttu-id="028a5-253">說明</span><span class="sxs-lookup"><span data-stu-id="028a5-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="028a5-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="028a5-254">StreamName</span></span> |<span data-ttu-id="028a5-255">String</span><span class="sxs-lookup"><span data-stu-id="028a5-255">String</span></span> |<span data-ttu-id="028a5-256">hello 路徑 hello 作業上執行</span><span class="sxs-lookup"><span data-stu-id="028a5-256">hello path hello operation was performed on</span></span> |

## <a name="samples-tooprocess-hello-log-data"></a><span data-ttu-id="028a5-257">範例 tooprocess hello 記錄資料</span><span class="sxs-lookup"><span data-stu-id="028a5-257">Samples tooprocess hello log data</span></span>
<span data-ttu-id="028a5-258">Azure Data Lake Store 提供的範例如何 tooprocess 和分析 hello 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="028a5-258">Azure Data Lake Store provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="028a5-259">您可以找到在 hello 範例[https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)。</span><span class="sxs-lookup"><span data-stu-id="028a5-259">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="028a5-260">另請參閱</span><span class="sxs-lookup"><span data-stu-id="028a5-260">See also</span></span>
* [<span data-ttu-id="028a5-261">Azure Data Lake Store 概觀</span><span class="sxs-lookup"><span data-stu-id="028a5-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="028a5-262">保護資料湖存放區中的資料</span><span class="sxs-lookup"><span data-stu-id="028a5-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

