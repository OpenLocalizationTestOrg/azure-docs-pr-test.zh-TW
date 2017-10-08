---
title: "aaaAzure 事件中心的診斷記錄檔 |Microsoft 文件"
description: "深入了解如何在 Azure 中建立事件中樞的診斷記錄備份 tooset。"
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="ae5f8-103">事件中樞診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="ae5f8-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="ae5f8-104">您可以檢視 Azure 事件中樞的兩種記錄檔類型：</span><span class="sxs-lookup"><span data-stu-id="ae5f8-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="ae5f8-105">**[活動記錄檔](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="ae5f8-106">這些記錄包含對工作執行之操作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="ae5f8-107">hello 記錄一定會啟用。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="ae5f8-108">**[診斷記錄](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="ae5f8-109">您可以設定診斷記錄，以更深入檢視與作業一起發生的所有事件。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="ae5f8-110">診斷記錄封面活動與 hello 時間之前 hello 作業會刪除，包括更新和 hello 作業執行時所發生的活動，會建立 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="ae5f8-111">開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="ae5f8-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="ae5f8-112">診斷記錄預設為停用。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="ae5f8-113">tooenable 診斷記錄檔：</span><span class="sxs-lookup"><span data-stu-id="ae5f8-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="ae5f8-114">在 hello [Azure 入口網站](https://portal.azure.com)下**監視 + 管理**，按一下 **診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![刀鋒視窗中瀏覽 toodiagnostic 記錄檔](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="ae5f8-116">按一下您想要 toomonitor hello 資源。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="ae5f8-117">按一下 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-117">Click **Turn on diagnostics**.</span></span>

    ![開啟診斷記錄](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="ae5f8-119">針對 [狀態]，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-119">For **Status**, click **On**.</span></span>

    ![將診斷記錄檔的 hello 狀態變更](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="ae5f8-121">您想要; 組 hello 封存目標例如，儲存體帳戶、 事件中心或 Azure 記錄分析。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="ae5f8-122">儲存 hello 新的診斷設定。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="ae5f8-123">新的設定大約會在 10 分鐘內生效。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="ae5f8-124">在這之後，記錄檔都會出現 hello 設定封存目標，在 hello**診斷記錄檔**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="ae5f8-125">如需有關如何設定診斷功能的詳細資訊，請參閱 hello [Azure 診斷的記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="ae5f8-126">診斷記錄類別</span><span class="sxs-lookup"><span data-stu-id="ae5f8-126">Diagnostic logs categories</span></span>
<span data-ttu-id="ae5f8-127">事件中樞會擷取兩種類別的診斷記錄檔：</span><span class="sxs-lookup"><span data-stu-id="ae5f8-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="ae5f8-128">**ArchiveLogs**: tooEvent 集線器封存，具體來說，記錄相關的 tooarchive 錯誤相關的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="ae5f8-129">**OperationalLogs**： 發生什麼事事件中心在作業期間，具體來說，是有關 hello 作業類型，包括建立事件中樞，資源使用，及 hello hello 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="ae5f8-130">診斷記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="ae5f8-130">Diagnostic logs schema</span></span>
<span data-ttu-id="ae5f8-131">所有的記錄檔都會以 JavaScript 物件標記法 (JSON) 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="ae5f8-132">每個項目都有使用 hello 下列各節中所述的 hello 格式的字串欄位。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="ae5f8-133">封存記錄檔結構描述</span><span class="sxs-lookup"><span data-stu-id="ae5f8-133">Archive logs schema</span></span>

<span data-ttu-id="ae5f8-134">封存記錄檔的 JSON 字串包含 hello 下表列出項目：</span><span class="sxs-lookup"><span data-stu-id="ae5f8-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="ae5f8-135">名稱</span><span class="sxs-lookup"><span data-stu-id="ae5f8-135">Name</span></span> | <span data-ttu-id="ae5f8-136">描述</span><span class="sxs-lookup"><span data-stu-id="ae5f8-136">Description</span></span>
------- | -------
<span data-ttu-id="ae5f8-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="ae5f8-137">TaskName</span></span> | <span data-ttu-id="ae5f8-138">Hello 工作失敗的描述。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-138">Description of hello task that failed.</span></span>
<span data-ttu-id="ae5f8-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="ae5f8-139">ActivityId</span></span> | <span data-ttu-id="ae5f8-140">用於追蹤的內部識別碼。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="ae5f8-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="ae5f8-141">trackingId</span></span> | <span data-ttu-id="ae5f8-142">用於追蹤的內部識別碼。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="ae5f8-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="ae5f8-143">resourceId</span></span> | <span data-ttu-id="ae5f8-144">Azure Resource Manager 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="ae5f8-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="ae5f8-145">eventHub</span></span> | <span data-ttu-id="ae5f8-146">事件中樞完整名稱 (包括命名空間名稱)。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="ae5f8-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="ae5f8-147">partitionId</span></span> | <span data-ttu-id="ae5f8-148">要寫入的事件中樞資料分割。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="ae5f8-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="ae5f8-149">archiveStep</span></span> | <span data-ttu-id="ae5f8-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="ae5f8-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="ae5f8-151">startTime</span><span class="sxs-lookup"><span data-stu-id="ae5f8-151">startTime</span></span> | <span data-ttu-id="ae5f8-152">失敗開始時間。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-152">Failure start time.</span></span>
<span data-ttu-id="ae5f8-153">failures</span><span class="sxs-lookup"><span data-stu-id="ae5f8-153">failures</span></span> | <span data-ttu-id="ae5f8-154">發生失敗的次數。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-154">Number of times failure occurred.</span></span>
<span data-ttu-id="ae5f8-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="ae5f8-155">durationInSeconds</span></span> | <span data-ttu-id="ae5f8-156">失敗持續時間。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-156">Duration of failure.</span></span>
<span data-ttu-id="ae5f8-157">Message</span><span class="sxs-lookup"><span data-stu-id="ae5f8-157">message</span></span> | <span data-ttu-id="ae5f8-158">錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-158">Error message.</span></span>
<span data-ttu-id="ae5f8-159">category</span><span class="sxs-lookup"><span data-stu-id="ae5f8-159">category</span></span> | <span data-ttu-id="ae5f8-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="ae5f8-160">ArchiveLogs</span></span>

<span data-ttu-id="ae5f8-161">hello 下列程式碼是封存記錄檔的 JSON 字串的範例：</span><span class="sxs-lookup"><span data-stu-id="ae5f8-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="ae5f8-162">作業記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="ae5f8-162">Operational logs schema</span></span>

<span data-ttu-id="ae5f8-163">作業記錄檔的 JSON 字串包含 hello 下表列出項目：</span><span class="sxs-lookup"><span data-stu-id="ae5f8-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="ae5f8-164">名稱</span><span class="sxs-lookup"><span data-stu-id="ae5f8-164">Name</span></span> | <span data-ttu-id="ae5f8-165">說明</span><span class="sxs-lookup"><span data-stu-id="ae5f8-165">Description</span></span>
------- | -------
<span data-ttu-id="ae5f8-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="ae5f8-166">ActivityId</span></span> | <span data-ttu-id="ae5f8-167">內部識別碼使用 tootrack 用途。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="ae5f8-168">EventName</span><span class="sxs-lookup"><span data-stu-id="ae5f8-168">EventName</span></span> | <span data-ttu-id="ae5f8-169">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-169">Operation name.</span></span>  
<span data-ttu-id="ae5f8-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="ae5f8-170">resourceId</span></span> | <span data-ttu-id="ae5f8-171">Azure Resource Manager 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="ae5f8-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="ae5f8-172">SubscriptionId</span></span> | <span data-ttu-id="ae5f8-173">訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-173">Subscription ID.</span></span>
<span data-ttu-id="ae5f8-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="ae5f8-174">EventTimeString</span></span> | <span data-ttu-id="ae5f8-175">作業時間。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-175">Operation time.</span></span>
<span data-ttu-id="ae5f8-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="ae5f8-176">EventProperties</span></span> | <span data-ttu-id="ae5f8-177">作業屬性。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-177">Operation properties.</span></span>
<span data-ttu-id="ae5f8-178">狀態</span><span class="sxs-lookup"><span data-stu-id="ae5f8-178">Status</span></span> | <span data-ttu-id="ae5f8-179">作業狀態。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-179">Operation status.</span></span>
<span data-ttu-id="ae5f8-180">呼叫者</span><span class="sxs-lookup"><span data-stu-id="ae5f8-180">Caller</span></span> | <span data-ttu-id="ae5f8-181">作業呼叫者 (Azure 入口網站或管理用戶端)。</span><span class="sxs-lookup"><span data-stu-id="ae5f8-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="ae5f8-182">category</span><span class="sxs-lookup"><span data-stu-id="ae5f8-182">category</span></span> | <span data-ttu-id="ae5f8-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="ae5f8-183">OperationalLogs</span></span>

<span data-ttu-id="ae5f8-184">hello 下列程式碼是作業記錄檔的 JSON 字串的範例：</span><span class="sxs-lookup"><span data-stu-id="ae5f8-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="ae5f8-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae5f8-185">Next steps</span></span>
* [<span data-ttu-id="ae5f8-186">簡介 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="ae5f8-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ae5f8-187">事件中樞 API 概觀</span><span class="sxs-lookup"><span data-stu-id="ae5f8-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="ae5f8-188">開始使用事件中樞</span><span class="sxs-lookup"><span data-stu-id="ae5f8-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
