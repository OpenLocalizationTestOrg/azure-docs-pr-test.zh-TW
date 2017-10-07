---
title: "aaaAzure 事件方格事件結構描述"
description: "描述可供事件的 Azure 事件方格的 hello 屬性。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a>Event Grid 事件結構描述

這篇文章提供 hello 屬性和結構描述的事件。 事件包含一組五個必要字串屬性和一個必要**資料**物件。 hello 屬性都是常見的 tooall 事件，從任何發行者。 hello**資料**物件包含特定 tooeach 發行者的屬性。 如需系統主題，這些屬性是特定 toohello 資源提供者，例如儲存體或事件中心。

事件可以包含多個事件物件的陣列中傳送 tooAzure 事件方格。 如果沒有單一事件，hello 陣列長度為 1。 
 
## <a name="event-properties"></a>事件屬性

所有事件都將都包含 hello 下列最上層資料相同。

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| 主題 | 字串 | 完整資源路徑 toohello 事件來源。 此欄位不可寫入。 |
| 主旨 | 字串 | 發行者端定義的路徑 toohello 事件主體。 |
| eventType | 字串 | 其中一個 hello 註冊事件來源的事件類型。 |
| eventTime | 字串 | hello 時間 hello 事件會產生 hello 提供者的 UTC 時間為基礎。 |
| id | 字串 | Hello 事件的唯一識別碼。 |
| data | 物件 | 事件資料特定 toohello 資源提供者。 |

## <a name="available-event-sources"></a>可用的事件來源

下列事件來源的 hello 發行事件方格透過取用的事件：

* 資源群組 (管理作業)
* Azure 訂用帳戶 (管理作業)
* 事件中樞
* 自訂主題

## <a name="azure-subscriptions"></a>Azure 訂用帳戶

Azure 訂用帳戶現在可從 Azure Resource Manager 發出管理事件，像是在虛擬機器建立時或儲存體帳戶刪除時皆可使用此功能。

### <a name="available-event-types"></a>可用的事件類型

- **Microsoft.Resources.ResourceWriteSuccess**：在資源建立或更新作業成功時引發。  
- **Microsoft.Resources.ResourceWriteFailure**：在資源建立或更新作業失敗時引發。  
- **Microsoft.Resources.ResourceWriteCancel**：在資源建立或更新作業取消時引發。  
- **Microsoft.Resources.ResourceDeleteSuccess**：在資源刪除作業成功時引發。  
- **Microsoft.Resources.ResourceDeleteFailure**：在資源刪除作業失敗時引發。  
- **Microsoft.Resources.ResourceDeleteCancel**：在資源刪除作業取消時引發。 這會在範本部署取消時發生。

### <a name="example-event-schema"></a>事件結構描述範例

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a>資源群組

資源群組現在可從 Azure Resource Manager 發出管理事件，像是在虛擬機器建立時或儲存體帳戶刪除時皆可使用此功能。

### <a name="available-event-types"></a>可用的事件類型

- **Microsoft.Resources.ResourceWriteSuccess**：在資源建立或更新作業成功時引發。  
- **Microsoft.Resources.ResourceWriteFailure**：在資源建立或更新作業失敗時引發。  
- **Microsoft.Resources.ResourceWriteCancel**：在資源建立或更新作業取消時引發。  
- **Microsoft.Resources.ResourceDeleteSuccess**：在資源刪除作業成功時引發。  
- **Microsoft.Resources.ResourceDeleteFailure**：在資源刪除作業失敗時引發。  
- **Microsoft.Resources.ResourceDeleteCancel**：在資源刪除作業取消時引發。 這會在範本部署取消時發生。

### <a name="example-event"></a>事件範例

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a>事件中樞

事件中心事件正在 toostorage 使用 hello 擷取功能會自動傳送檔案時，才發出。

### <a name="available-event-types"></a>可用的事件類型

- **Microsoft.EventHub.CaptureFileCreated**：擷取檔案建立時引發。

### <a name="example-event"></a>事件範例

此範例事件顯示 hello 擷取儲存檔案時引發的事件中樞事件的結構描述。 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a>Azure Blob 儲存體

Azure Blob 儲存體目前提供私人預覽，註冊後可與 Event Grid 整合使用。

### <a name="available-event-types"></a>可用的事件類型

- **Microsoft.Storage.BlobCreated**：blob 建立時引發。
- **Microsoft.Storage.BlobDeleted**：blob 刪除時引發。

### <a name="example-event"></a>事件範例

此範例事件顯示 hello 結構描述建立 blob 時引發的儲存體事件。 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a>自訂主題

您的自訂事件的 hello 資料裝載由您所定義，而且可以是任何也格式的 JSON。 hello 上方層級的資料應包含相同欄位所定義的標準資源事件 hello。 發行事件 toocustom 主題時，您應該考慮模型中路由與篩選您的事件 tooaid hello 主體。

### <a name="example-event"></a>事件範例

hello 下列範例顯示事件，以供自訂主題：
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a>後續步驟

* 如簡介 tooEvent 格線，請參閱[事件方格是什麼？](overview.md)
* toolearn 有關建立事件方格訂用帳戶，請參閱[事件方格訂用帳戶的結構描述](subscription-creation-schema.md)。
