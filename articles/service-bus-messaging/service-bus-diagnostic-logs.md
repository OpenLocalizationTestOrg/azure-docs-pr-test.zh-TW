---
title: "aaaAzure Service Bus 診斷記錄檔 |Microsoft 文件"
description: "深入了解如何在 Azure 中的服務匯流排的診斷記錄備份 tooset。"
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
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="a5e34-103">服務匯流排診斷記錄</span><span class="sxs-lookup"><span data-stu-id="a5e34-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="a5e34-104">您可以檢視「Azure 服務匯流排」的兩種記錄：</span><span class="sxs-lookup"><span data-stu-id="a5e34-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="a5e34-105">**[活動記錄](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**。</span><span class="sxs-lookup"><span data-stu-id="a5e34-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="a5e34-106">這些記錄包含在工作上執行之操作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a5e34-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="a5e34-107">hello 記錄一定會啟用。</span><span class="sxs-lookup"><span data-stu-id="a5e34-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="a5e34-108">**[診斷記錄](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**。</span><span class="sxs-lookup"><span data-stu-id="a5e34-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="a5e34-109">您可以設定診斷記錄，以取得在工作內所發生之所有事件的更詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a5e34-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="a5e34-110">診斷記錄封面活動與 hello 時間之前 hello 作業會刪除，包括更新和 hello 作業執行時所發生的活動，會建立 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="a5e34-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="a5e34-111">開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="a5e34-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="a5e34-112">診斷記錄預設為停用。</span><span class="sxs-lookup"><span data-stu-id="a5e34-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="a5e34-113">tooenable 診斷記錄檔，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a5e34-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="a5e34-114">在 hello [Azure 入口網站](https://portal.azure.com)下**監視 + 管理**，按一下 **診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="a5e34-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![刀鋒視窗中瀏覽 toodiagnostic 記錄檔](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="a5e34-116">按一下您想要 toomonitor hello 資源。</span><span class="sxs-lookup"><span data-stu-id="a5e34-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="a5e34-117">按一下 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="a5e34-117">Click **Turn on diagnostics**.</span></span>

    ![開啟診斷記錄](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="a5e34-119">針對 [狀態]，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="a5e34-119">For **Status**, click **On**.</span></span>

    ![變更診斷記錄狀態](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="a5e34-121">您想要; 組 hello 封存目標例如，儲存體帳戶、 事件中心或 Azure 記錄分析。</span><span class="sxs-lookup"><span data-stu-id="a5e34-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="a5e34-122">儲存 hello 新的診斷設定。</span><span class="sxs-lookup"><span data-stu-id="a5e34-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="a5e34-123">新的設定大約會在 10 分鐘內生效。</span><span class="sxs-lookup"><span data-stu-id="a5e34-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="a5e34-124">在這之後，記錄檔都會出現 hello 設定封存目標，在 hello**診斷記錄檔**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5e34-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="a5e34-125">如需有關如何設定診斷功能的詳細資訊，請參閱 hello [Azure 診斷的記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="a5e34-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="a5e34-126">診斷記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="a5e34-126">Diagnostic logs schema</span></span>

<span data-ttu-id="a5e34-127">所有的記錄檔都會以 JavaScript 物件標記法 (JSON) 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="a5e34-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="a5e34-128">每個項目都有使用 hello 之後 > 一節中所述的 hello 格式的字串欄位。</span><span class="sxs-lookup"><span data-stu-id="a5e34-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="a5e34-129">作業記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="a5e34-129">Operational logs schema</span></span>

<span data-ttu-id="a5e34-130">登入 hello **OperationalLogs**類別擷取服務匯流排作業期間進行的作業。</span><span class="sxs-lookup"><span data-stu-id="a5e34-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="a5e34-131">具體來說，這些記錄檔擷取 hello 作業類型，包括佇列建立時，資源使用，且 hello hello 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="a5e34-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="a5e34-132">作業記錄檔的 JSON 字串包含 hello 下表列出項目：</span><span class="sxs-lookup"><span data-stu-id="a5e34-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="a5e34-133">名稱</span><span class="sxs-lookup"><span data-stu-id="a5e34-133">Name</span></span> | <span data-ttu-id="a5e34-134">說明</span><span class="sxs-lookup"><span data-stu-id="a5e34-134">Description</span></span>
------- | -------
<span data-ttu-id="a5e34-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="a5e34-135">ActivityId</span></span> | <span data-ttu-id="a5e34-136">用於追蹤的內部識別碼</span><span class="sxs-lookup"><span data-stu-id="a5e34-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="a5e34-137">EventName</span><span class="sxs-lookup"><span data-stu-id="a5e34-137">EventName</span></span> | <span data-ttu-id="a5e34-138">作業名稱</span><span class="sxs-lookup"><span data-stu-id="a5e34-138">Operation name</span></span>           
<span data-ttu-id="a5e34-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="a5e34-139">resourceId</span></span> | <span data-ttu-id="a5e34-140">Azure Resource Manager 資源識別碼</span><span class="sxs-lookup"><span data-stu-id="a5e34-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="a5e34-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a5e34-141">SubscriptionId</span></span> | <span data-ttu-id="a5e34-142">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="a5e34-142">Subscription ID</span></span>
<span data-ttu-id="a5e34-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="a5e34-143">EventTimeString</span></span> | <span data-ttu-id="a5e34-144">作業時間</span><span class="sxs-lookup"><span data-stu-id="a5e34-144">Operation time</span></span>
<span data-ttu-id="a5e34-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="a5e34-145">EventProperties</span></span> | <span data-ttu-id="a5e34-146">作業屬性</span><span class="sxs-lookup"><span data-stu-id="a5e34-146">Operation properties</span></span>
<span data-ttu-id="a5e34-147">狀態</span><span class="sxs-lookup"><span data-stu-id="a5e34-147">Status</span></span> | <span data-ttu-id="a5e34-148">作業狀態</span><span class="sxs-lookup"><span data-stu-id="a5e34-148">Operation status</span></span>
<span data-ttu-id="a5e34-149">呼叫者</span><span class="sxs-lookup"><span data-stu-id="a5e34-149">Caller</span></span> | <span data-ttu-id="a5e34-150">作業呼叫者 (Azure 入口網站或管理用戶端)</span><span class="sxs-lookup"><span data-stu-id="a5e34-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="a5e34-151">category</span><span class="sxs-lookup"><span data-stu-id="a5e34-151">category</span></span> | <span data-ttu-id="a5e34-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="a5e34-152">OperationalLogs</span></span>

<span data-ttu-id="a5e34-153">以下是作業記錄 JSON 字串的範例：</span><span class="sxs-lookup"><span data-stu-id="a5e34-153">Here's an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a5e34-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5e34-154">Next steps</span></span>

<span data-ttu-id="a5e34-155">請造訪下列連結 toolearn 更多有關 Service Bus hello:</span><span class="sxs-lookup"><span data-stu-id="a5e34-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="a5e34-156">簡介 tooService 匯流排</span><span class="sxs-lookup"><span data-stu-id="a5e34-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="a5e34-157">開始使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="a5e34-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
