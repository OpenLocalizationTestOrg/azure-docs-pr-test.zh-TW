---
title: "Azure 服務匯流排診斷記錄 | Microsoft Docs"
description: "了解如何為 Azure 中的「服務匯流排」設定診斷記錄。"
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: 72e18444c83b84c5191a0aab3dc6983517167dd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="fa342-103">服務匯流排診斷記錄</span><span class="sxs-lookup"><span data-stu-id="fa342-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="fa342-104">您可以檢視「Azure 服務匯流排」的兩種記錄：</span><span class="sxs-lookup"><span data-stu-id="fa342-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="fa342-105">**[活動記錄](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**。</span><span class="sxs-lookup"><span data-stu-id="fa342-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="fa342-106">這些記錄包含在工作上執行之操作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fa342-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="fa342-107">系統一律會啟用這些記錄。</span><span class="sxs-lookup"><span data-stu-id="fa342-107">The logs are always enabled.</span></span>
* <span data-ttu-id="fa342-108">**[診斷記錄](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**。</span><span class="sxs-lookup"><span data-stu-id="fa342-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="fa342-109">您可以設定診斷記錄，以取得在工作內所發生之所有事件的更詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fa342-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="fa342-110">診斷記錄涵蓋從建立工作到刪除工作期間的活動，包括工作執行時發生的更新與活動。</span><span class="sxs-lookup"><span data-stu-id="fa342-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="fa342-111">開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="fa342-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="fa342-112">診斷記錄預設為停用。</span><span class="sxs-lookup"><span data-stu-id="fa342-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="fa342-113">若要啟用診斷記錄，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fa342-113">To enable diagnostic logs, perform the following steps:</span></span>

1.  <span data-ttu-id="fa342-114">在 [Azure 入口網站](https://portal.azure.com)的 [監視 + 管理] 下，按一下 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="fa342-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![瀏覽到診斷記錄的刀鋒視窗](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="fa342-116">按一下您想要監視的資源。</span><span class="sxs-lookup"><span data-stu-id="fa342-116">Click the resource you want to monitor.</span></span>  

3.  <span data-ttu-id="fa342-117">按一下 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="fa342-117">Click **Turn on diagnostics**.</span></span>

    ![開啟診斷記錄](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="fa342-119">針對 [狀態]，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="fa342-119">For **Status**, click **On**.</span></span>

    ![變更診斷記錄狀態](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="fa342-121">設定您要使用的封存目標，例如儲存體帳戶、事件中樞或 Azure Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="fa342-121">Set the archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="fa342-122">儲存新的診斷設定。</span><span class="sxs-lookup"><span data-stu-id="fa342-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="fa342-123">新的設定大約會在 10 分鐘內生效。</span><span class="sxs-lookup"><span data-stu-id="fa342-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="fa342-124">之後，記錄就會顯示在 [診斷記錄] 刀鋒視窗上已設定的封存目標中。</span><span class="sxs-lookup"><span data-stu-id="fa342-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="fa342-125">如需設定診斷的詳細資訊，請參閱 [Azure 診斷記錄概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="fa342-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="fa342-126">診斷記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="fa342-126">Diagnostic logs schema</span></span>

<span data-ttu-id="fa342-127">所有的記錄檔都會以 JavaScript 物件標記法 (JSON) 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="fa342-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="fa342-128">每個項目都具有字串欄位，這些欄位會使用下列小節所述的格式。</span><span class="sxs-lookup"><span data-stu-id="fa342-128">Each entry has string fields that use the format described in the following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="fa342-129">作業記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="fa342-129">Operational logs schema</span></span>

<span data-ttu-id="fa342-130">**OperationalLogs** 類別中的記錄會擷取「服務匯流排」作業期間發生的事項。</span><span class="sxs-lookup"><span data-stu-id="fa342-130">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="fa342-131">具體而言，這些記錄會擷取作業類型，包括建立佇列、使用的資源，以及作業狀態。</span><span class="sxs-lookup"><span data-stu-id="fa342-131">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span></span>

<span data-ttu-id="fa342-132">作業記錄 JSON 字串包括下表所列的元素：</span><span class="sxs-lookup"><span data-stu-id="fa342-132">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="fa342-133">名稱</span><span class="sxs-lookup"><span data-stu-id="fa342-133">Name</span></span> | <span data-ttu-id="fa342-134">說明</span><span class="sxs-lookup"><span data-stu-id="fa342-134">Description</span></span>
------- | -------
<span data-ttu-id="fa342-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="fa342-135">ActivityId</span></span> | <span data-ttu-id="fa342-136">用於追蹤的內部識別碼</span><span class="sxs-lookup"><span data-stu-id="fa342-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="fa342-137">EventName</span><span class="sxs-lookup"><span data-stu-id="fa342-137">EventName</span></span> | <span data-ttu-id="fa342-138">作業名稱</span><span class="sxs-lookup"><span data-stu-id="fa342-138">Operation name</span></span>           
<span data-ttu-id="fa342-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="fa342-139">resourceId</span></span> | <span data-ttu-id="fa342-140">Azure Resource Manager 資源識別碼</span><span class="sxs-lookup"><span data-stu-id="fa342-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="fa342-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="fa342-141">SubscriptionId</span></span> | <span data-ttu-id="fa342-142">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="fa342-142">Subscription ID</span></span>
<span data-ttu-id="fa342-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="fa342-143">EventTimeString</span></span> | <span data-ttu-id="fa342-144">作業時間</span><span class="sxs-lookup"><span data-stu-id="fa342-144">Operation time</span></span>
<span data-ttu-id="fa342-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="fa342-145">EventProperties</span></span> | <span data-ttu-id="fa342-146">作業屬性</span><span class="sxs-lookup"><span data-stu-id="fa342-146">Operation properties</span></span>
<span data-ttu-id="fa342-147">狀態</span><span class="sxs-lookup"><span data-stu-id="fa342-147">Status</span></span> | <span data-ttu-id="fa342-148">作業狀態</span><span class="sxs-lookup"><span data-stu-id="fa342-148">Operation status</span></span>
<span data-ttu-id="fa342-149">呼叫者</span><span class="sxs-lookup"><span data-stu-id="fa342-149">Caller</span></span> | <span data-ttu-id="fa342-150">作業呼叫者 (Azure 入口網站或管理用戶端)</span><span class="sxs-lookup"><span data-stu-id="fa342-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="fa342-151">category</span><span class="sxs-lookup"><span data-stu-id="fa342-151">category</span></span> | <span data-ttu-id="fa342-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="fa342-152">OperationalLogs</span></span>

<span data-ttu-id="fa342-153">以下是作業記錄 JSON 字串的範例：</span><span class="sxs-lookup"><span data-stu-id="fa342-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="fa342-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa342-154">Next steps</span></span>

<span data-ttu-id="fa342-155">請造訪下列連結以深入了解服務匯流排：</span><span class="sxs-lookup"><span data-stu-id="fa342-155">Visit the following links to learn more about Service Bus:</span></span>

* [<span data-ttu-id="fa342-156">服務匯流排簡介</span><span class="sxs-lookup"><span data-stu-id="fa342-156">Introduction to Service Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="fa342-157">開始使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="fa342-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
