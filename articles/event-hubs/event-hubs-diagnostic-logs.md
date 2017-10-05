---
title: "Azure 事件中樞診斷記錄 | Microsoft Docs"
description: "了解如何為 Azure 中的事件中樞設定診斷記錄檔。"
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
ms.openlocfilehash: 09bc62f4918635419d74ef3ae400a41d4ce58b5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="2ccb0-103">事件中樞診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="2ccb0-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="2ccb0-104">您可以檢視 Azure 事件中樞的兩種記錄檔類型：</span><span class="sxs-lookup"><span data-stu-id="2ccb0-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="2ccb0-105">**[活動記錄檔](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="2ccb0-106">這些記錄包含對工作執行之操作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="2ccb0-107">系統一律會啟用這些記錄。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-107">The logs are always enabled.</span></span>
* <span data-ttu-id="2ccb0-108">**[診斷記錄](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="2ccb0-109">您可以設定診斷記錄，以更深入檢視與作業一起發生的所有事件。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="2ccb0-110">診斷記錄涵蓋從建立工作到刪除工作期間的活動，包括工作執行時發生的更新與活動。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="2ccb0-111">開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="2ccb0-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="2ccb0-112">診斷記錄預設為停用。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="2ccb0-113">啟用診斷記錄：</span><span class="sxs-lookup"><span data-stu-id="2ccb0-113">To enable diagnostic logs:</span></span>

1.  <span data-ttu-id="2ccb0-114">在 [Azure 入口網站](https://portal.azure.com)的 [監視 + 管理] 下，按一下 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![瀏覽到診斷記錄檔的刀鋒視窗](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="2ccb0-116">按一下您想要監視的資源。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-116">Click the resource you want to monitor.</span></span>

3.  <span data-ttu-id="2ccb0-117">按一下 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-117">Click **Turn on diagnostics**.</span></span>

    ![開啟診斷記錄](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="2ccb0-119">針對 [狀態]，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-119">For **Status**, click **On**.</span></span>

    ![變更診斷記錄檔的狀態](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="2ccb0-121">設定您想要的封存目標，例如儲存體帳戶、事件中樞或 Azure Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="2ccb0-122">儲存新的診斷設定。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="2ccb0-123">新的設定大約會在 10 分鐘內生效。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="2ccb0-124">之後，記錄就會顯示在 [診斷記錄] 刀鋒視窗上已設定的封存目標中。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="2ccb0-125">如需設定診斷的詳細資訊，請參閱 [Azure 診斷記錄概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="2ccb0-126">診斷記錄類別</span><span class="sxs-lookup"><span data-stu-id="2ccb0-126">Diagnostic logs categories</span></span>
<span data-ttu-id="2ccb0-127">事件中樞會擷取兩種類別的診斷記錄檔：</span><span class="sxs-lookup"><span data-stu-id="2ccb0-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="2ccb0-128">**ArchiveLogs**：與「事件中樞」封存相關的記錄，具體而言，就是與封存錯誤相關的記錄。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-128">**ArchiveLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span></span>
* <span data-ttu-id="2ccb0-129">**OperationalLogs**：與「事件中樞」作業期間發生的事件有關的資訊，具體而言，就是作業類型 (包括建立事件中樞)、使用的資源及作業狀態。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="2ccb0-130">診斷記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="2ccb0-130">Diagnostic logs schema</span></span>
<span data-ttu-id="2ccb0-131">所有的記錄檔都會以 JavaScript 物件標記法 (JSON) 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="2ccb0-132">每個項目都具有字串欄位，這些欄位會使用下列小節所述的格式。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-132">Each entry has string fields that use the format described in the following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="2ccb0-133">封存記錄檔結構描述</span><span class="sxs-lookup"><span data-stu-id="2ccb0-133">Archive logs schema</span></span>

<span data-ttu-id="2ccb0-134">封存記錄檔 JSON 字串包括下表所列的元素：</span><span class="sxs-lookup"><span data-stu-id="2ccb0-134">Archive log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="2ccb0-135">名稱</span><span class="sxs-lookup"><span data-stu-id="2ccb0-135">Name</span></span> | <span data-ttu-id="2ccb0-136">描述</span><span class="sxs-lookup"><span data-stu-id="2ccb0-136">Description</span></span>
------- | -------
<span data-ttu-id="2ccb0-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="2ccb0-137">TaskName</span></span> | <span data-ttu-id="2ccb0-138">失敗工作的描述。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-138">Description of the task that failed.</span></span>
<span data-ttu-id="2ccb0-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="2ccb0-139">ActivityId</span></span> | <span data-ttu-id="2ccb0-140">用於追蹤的內部識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="2ccb0-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="2ccb0-141">trackingId</span></span> | <span data-ttu-id="2ccb0-142">用於追蹤的內部識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="2ccb0-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="2ccb0-143">resourceId</span></span> | <span data-ttu-id="2ccb0-144">Azure Resource Manager 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="2ccb0-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="2ccb0-145">eventHub</span></span> | <span data-ttu-id="2ccb0-146">事件中樞完整名稱 (包括命名空間名稱)。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="2ccb0-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="2ccb0-147">partitionId</span></span> | <span data-ttu-id="2ccb0-148">要寫入的事件中樞資料分割。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="2ccb0-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="2ccb0-149">archiveStep</span></span> | <span data-ttu-id="2ccb0-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="2ccb0-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="2ccb0-151">startTime</span><span class="sxs-lookup"><span data-stu-id="2ccb0-151">startTime</span></span> | <span data-ttu-id="2ccb0-152">失敗開始時間。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-152">Failure start time.</span></span>
<span data-ttu-id="2ccb0-153">failures</span><span class="sxs-lookup"><span data-stu-id="2ccb0-153">failures</span></span> | <span data-ttu-id="2ccb0-154">發生失敗的次數。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-154">Number of times failure occurred.</span></span>
<span data-ttu-id="2ccb0-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="2ccb0-155">durationInSeconds</span></span> | <span data-ttu-id="2ccb0-156">失敗持續時間。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-156">Duration of failure.</span></span>
<span data-ttu-id="2ccb0-157">Message</span><span class="sxs-lookup"><span data-stu-id="2ccb0-157">message</span></span> | <span data-ttu-id="2ccb0-158">錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-158">Error message.</span></span>
<span data-ttu-id="2ccb0-159">category</span><span class="sxs-lookup"><span data-stu-id="2ccb0-159">category</span></span> | <span data-ttu-id="2ccb0-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="2ccb0-160">ArchiveLogs</span></span>

<span data-ttu-id="2ccb0-161">下列程式碼是封存記錄 JSON 字串的範例：</span><span class="sxs-lookup"><span data-stu-id="2ccb0-161">The following code is an example of an archive log JSON string:</span></span>

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
     "message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="2ccb0-162">作業記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="2ccb0-162">Operational logs schema</span></span>

<span data-ttu-id="2ccb0-163">作業記錄 JSON 字串包括下表所列的元素：</span><span class="sxs-lookup"><span data-stu-id="2ccb0-163">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="2ccb0-164">名稱</span><span class="sxs-lookup"><span data-stu-id="2ccb0-164">Name</span></span> | <span data-ttu-id="2ccb0-165">說明</span><span class="sxs-lookup"><span data-stu-id="2ccb0-165">Description</span></span>
------- | -------
<span data-ttu-id="2ccb0-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="2ccb0-166">ActivityId</span></span> | <span data-ttu-id="2ccb0-167">用於追蹤目的的內部識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-167">Internal ID, used to track purpose.</span></span>
<span data-ttu-id="2ccb0-168">EventName</span><span class="sxs-lookup"><span data-stu-id="2ccb0-168">EventName</span></span> | <span data-ttu-id="2ccb0-169">作業名稱。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-169">Operation name.</span></span>  
<span data-ttu-id="2ccb0-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="2ccb0-170">resourceId</span></span> | <span data-ttu-id="2ccb0-171">Azure Resource Manager 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="2ccb0-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="2ccb0-172">SubscriptionId</span></span> | <span data-ttu-id="2ccb0-173">訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-173">Subscription ID.</span></span>
<span data-ttu-id="2ccb0-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="2ccb0-174">EventTimeString</span></span> | <span data-ttu-id="2ccb0-175">作業時間。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-175">Operation time.</span></span>
<span data-ttu-id="2ccb0-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="2ccb0-176">EventProperties</span></span> | <span data-ttu-id="2ccb0-177">作業屬性。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-177">Operation properties.</span></span>
<span data-ttu-id="2ccb0-178">狀態</span><span class="sxs-lookup"><span data-stu-id="2ccb0-178">Status</span></span> | <span data-ttu-id="2ccb0-179">作業狀態。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-179">Operation status.</span></span>
<span data-ttu-id="2ccb0-180">呼叫者</span><span class="sxs-lookup"><span data-stu-id="2ccb0-180">Caller</span></span> | <span data-ttu-id="2ccb0-181">作業呼叫者 (Azure 入口網站或管理用戶端)。</span><span class="sxs-lookup"><span data-stu-id="2ccb0-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="2ccb0-182">category</span><span class="sxs-lookup"><span data-stu-id="2ccb0-182">category</span></span> | <span data-ttu-id="2ccb0-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="2ccb0-183">OperationalLogs</span></span>

<span data-ttu-id="2ccb0-184">下列程式碼是作業記錄 JSON 字串的範例：</span><span class="sxs-lookup"><span data-stu-id="2ccb0-184">The following code is an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2ccb0-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ccb0-185">Next steps</span></span>
* [<span data-ttu-id="2ccb0-186">事件中樞簡介</span><span class="sxs-lookup"><span data-stu-id="2ccb0-186">Introduction to Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2ccb0-187">事件中樞 API 概觀</span><span class="sxs-lookup"><span data-stu-id="2ccb0-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="2ccb0-188">開始使用事件中樞</span><span class="sxs-lookup"><span data-stu-id="2ccb0-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
