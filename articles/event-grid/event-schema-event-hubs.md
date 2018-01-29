---
title: "Azure Event Grid 事件中樞事件結構描述"
description: "描述 Azure Event Grid 中事件中樞事件的屬性"
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 11/07/2017
ms.author: tomfitz
ms.openlocfilehash: 80959ee589a1cfcf317a98c3bafd7f92c796fc2d
ms.sourcegitcommit: 6a22af82b88674cd029387f6cedf0fb9f8830afd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/11/2017
---
# <a name="azure-event-grid-event-schema-for-event-hubs"></a>Azure Event Grid 事件中樞事件結構描述

本文提供事件中樞事件的屬性與結構描述。 如需事件結構描述的簡介，請參閱 [Azure Event Grid 事件結構描述](event-schema.md)。

### <a name="available-event-types"></a>可用的事件類型

當擷取檔案建立時，事件中樞會引發 **Microsoft.EventHub.CaptureFileCreated** 事件類型。

## <a name="example-event"></a>事件範例

此範例顯示在擷取功能儲存檔案時引發之事件中樞事件的結構描述： 

```json
[
    {
        "topic": "/subscriptions/<guid>/resourcegroups/rgDataMigrationSample/providers/Microsoft.EventHub/namespaces/tfdatamigratens",
        "subject": "eventhubs/hubdatamigration",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-08-31T19:12:46.0498024Z",
        "id": "14e87d03-6fbf-4bb2-9a21-92bd1281f247",
        "data": {
            "fileUrl": "https://tf0831datamigrate.blob.core.windows.net/windturbinecapture/tfdatamigratens/hubdatamigration/1/2017/08/31/19/11/45.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 249168,
            "eventCount": 1500,
            "firstSequenceNumber": 2400,
            "lastSequenceNumber": 3899,
            "firstEnqueueTime": "2017-08-31T19:12:14.674Z",
            "lastEnqueueTime": "2017-08-31T19:12:44.309Z"
        }
    }
]
```

## <a name="event-properties"></a>事件屬性

事件具有下列的最高層級資料：

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| 主題 | 字串 | 事件來源的完整資源路徑。 此欄位不可寫入。 |
| 主旨 | 字串 | 發行者定義事件主體的路徑。 |
| eventType | 字串 | 此事件來源已註冊的事件類型之一。 |
| eventTime | 字串 | 事件產生的時間，以提供者之 UTC 時間為準。 |
| id | 字串 | 事件的唯一識別碼。 |
| data | 物件 | 事件中樞事件資料。 |

資料物件具有下列屬性：

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| fileUrl | 字串 | 擷取檔案的路徑。 |
| fileType | 字串 | 擷取檔案的檔案類型。 |
| partitionId | 字串 | 分區識別碼。 |
| sizeInBytes | integer | 檔案大小。 |
| eventCount | integer | 檔案中的事件數目。 |
| firstSequenceNumber | integer | 來自佇列的最小序號。 |
| lastSequenceNumber | integer | 來自佇列的最後一個序號。 |
| firstEnqueueTime | 字串 | 來自佇列的第一個時間。 |
| lastEnqueueTime | 字串 | 來自佇列的最後一個時間。 |

## <a name="next-steps"></a>後續步驟

* 如需 Azure Event Grid 的簡介，請參閱[什麼是 Event Grid？](overview.md)
* 若要了解 Event Grid 訂用帳戶的建立，請參閱 [Event Grid 訂用帳戶結構描述](subscription-creation-schema.md)。
* 如需處理事件中樞事件的詳細資訊，請參閱[將巨量資料串流至資料倉儲](event-grid-event-hubs-integration.md)。