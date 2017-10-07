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
# <a name="service-bus-diagnostic-logs"></a>服務匯流排診斷記錄

您可以檢視「Azure 服務匯流排」的兩種記錄：
* **[活動記錄](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**。 這些記錄包含在工作上執行之操作的相關資訊。 hello 記錄一定會啟用。
* **[診斷記錄](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**。 您可以設定診斷記錄，以取得在工作內所發生之所有事件的更詳細資訊。 診斷記錄封面活動與 hello 時間之前 hello 作業會刪除，包括更新和 hello 作業執行時所發生的活動，會建立 hello 作業。

## <a name="turn-on-diagnostic-logs"></a>開啟診斷記錄

診斷記錄預設為停用。 tooenable 診斷記錄檔，執行下列步驟的 hello:

1.  在 hello [Azure 入口網站](https://portal.azure.com)下**監視 + 管理**，按一下 **診斷記錄檔**。

    ![刀鋒視窗中瀏覽 toodiagnostic 記錄檔](./media/service-bus-diagnostic-logs/image1.png)

2. 按一下您想要 toomonitor hello 資源。  

3.  按一下 [開啟診斷]。

    ![開啟診斷記錄](./media/service-bus-diagnostic-logs/image2.png)

4.  針對 [狀態]，按一下 [開啟]。

    ![變更診斷記錄狀態](./media/service-bus-diagnostic-logs/image3.png)

5.  您想要; 組 hello 封存目標例如，儲存體帳戶、 事件中心或 Azure 記錄分析。

6.  儲存 hello 新的診斷設定。

新的設定大約會在 10 分鐘內生效。 在這之後，記錄檔都會出現 hello 設定封存目標，在 hello**診斷記錄檔**刀鋒視窗。

如需有關如何設定診斷功能的詳細資訊，請參閱 hello [Azure 診斷的記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)。

## <a name="diagnostic-logs-schema"></a>診斷記錄結構描述

所有的記錄檔都會以 JavaScript 物件標記法 (JSON) 格式儲存。 每個項目都有使用 hello 之後 > 一節中所述的 hello 格式的字串欄位。

## <a name="operational-logs-schema"></a>作業記錄結構描述

登入 hello **OperationalLogs**類別擷取服務匯流排作業期間進行的作業。 具體來說，這些記錄檔擷取 hello 作業類型，包括佇列建立時，資源使用，且 hello hello 作業的狀態。

作業記錄檔的 JSON 字串包含 hello 下表列出項目：

名稱 | 說明
------- | -------
ActivityId | 用於追蹤的內部識別碼
EventName | 作業名稱           
resourceId | Azure Resource Manager 資源識別碼
SubscriptionId | 訂用帳戶識別碼
EventTimeString | 作業時間
EventProperties | 作業屬性
狀態 | 作業狀態
呼叫者 | 作業呼叫者 (Azure 入口網站或管理用戶端)
category | OperationalLogs

以下是作業記錄 JSON 字串的範例：

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

## <a name="next-steps"></a>後續步驟

請造訪下列連結 toolearn 更多有關 Service Bus hello:

* [簡介 tooService 匯流排](service-bus-messaging-overview.md)
* [開始使用服務匯流排](service-bus-dotnet-get-started-with-queues.md)
