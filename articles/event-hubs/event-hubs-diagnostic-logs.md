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
# <a name="event-hubs-diagnostic-logs"></a>事件中樞診斷記錄檔

您可以檢視 Azure 事件中樞的兩種記錄檔類型：
* **[活動記錄檔](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**。 這些記錄包含對工作執行之操作的相關資訊。 hello 記錄一定會啟用。
* **[診斷記錄](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**。 您可以設定診斷記錄，以更深入檢視與作業一起發生的所有事件。 診斷記錄封面活動與 hello 時間之前 hello 作業會刪除，包括更新和 hello 作業執行時所發生的活動，會建立 hello 作業。

## <a name="turn-on-diagnostic-logs"></a>開啟診斷記錄
診斷記錄預設為停用。 tooenable 診斷記錄檔：

1.  在 hello [Azure 入口網站](https://portal.azure.com)下**監視 + 管理**，按一下 **診斷記錄檔**。

    ![刀鋒視窗中瀏覽 toodiagnostic 記錄檔](./media/event-hubs-diagnostic-logs/image1.png)

2.  按一下您想要 toomonitor hello 資源。

3.  按一下 [開啟診斷]。

    ![開啟診斷記錄](./media/event-hubs-diagnostic-logs/image2.png)

4.  針對 [狀態]，按一下 [開啟]。

    ![將診斷記錄檔的 hello 狀態變更](./media/event-hubs-diagnostic-logs/image3.png)

5.  您想要; 組 hello 封存目標例如，儲存體帳戶、 事件中心或 Azure 記錄分析。

6.  儲存 hello 新的診斷設定。

新的設定大約會在 10 分鐘內生效。 在這之後，記錄檔都會出現 hello 設定封存目標，在 hello**診斷記錄檔**刀鋒視窗。

如需有關如何設定診斷功能的詳細資訊，請參閱 hello [Azure 診斷的記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)。

## <a name="diagnostic-logs-categories"></a>診斷記錄類別
事件中樞會擷取兩種類別的診斷記錄檔：

* **ArchiveLogs**: tooEvent 集線器封存，具體來說，記錄相關的 tooarchive 錯誤相關的記錄檔。
* **OperationalLogs**： 發生什麼事事件中心在作業期間，具體來說，是有關 hello 作業類型，包括建立事件中樞，資源使用，及 hello hello 作業的狀態。

## <a name="diagnostic-logs-schema"></a>診斷記錄結構描述
所有的記錄檔都會以 JavaScript 物件標記法 (JSON) 格式儲存。 每個項目都有使用 hello 下列各節中所述的 hello 格式的字串欄位。

### <a name="archive-logs-schema"></a>封存記錄檔結構描述

封存記錄檔的 JSON 字串包含 hello 下表列出項目：

名稱 | 描述
------- | -------
TaskName | Hello 工作失敗的描述。
ActivityId | 用於追蹤的內部識別碼。
trackingId | 用於追蹤的內部識別碼。
resourceId | Azure Resource Manager 資源識別碼。
eventHub | 事件中樞完整名稱 (包括命名空間名稱)。
partitionId | 要寫入的事件中樞資料分割。
archiveStep | ArchiveFlushWriter
startTime | 失敗開始時間。
failures | 發生失敗的次數。
durationInSeconds | 失敗持續時間。
Message | 錯誤訊息。
category | ArchiveLogs

hello 下列程式碼是封存記錄檔的 JSON 字串的範例：

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

### <a name="operational-logs-schema"></a>作業記錄結構描述

作業記錄檔的 JSON 字串包含 hello 下表列出項目：

名稱 | 說明
------- | -------
ActivityId | 內部識別碼使用 tootrack 用途。
EventName | 作業名稱。  
resourceId | Azure Resource Manager 資源識別碼。
SubscriptionId | 訂用帳戶 ID。
EventTimeString | 作業時間。
EventProperties | 作業屬性。
狀態 | 作業狀態。
呼叫者 | 作業呼叫者 (Azure 入口網站或管理用戶端)。
category | OperationalLogs

hello 下列程式碼是作業記錄檔的 JSON 字串的範例：

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

## <a name="next-steps"></a>後續步驟
* [簡介 tooEvent 集線器](event-hubs-what-is-event-hubs.md)
* [事件中樞 API 概觀](event-hubs-api-overview.md)
* [開始使用事件中樞](event-hubs-csharp-ephcs-getstarted.md)
