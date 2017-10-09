---
title: "aaaAzure 事件方格訂用帳戶的結構描述"
description: "描述 Azure 事件方格 tooan 事件訂閱的 hello 屬性。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a>事件格線訂用帳戶的結構描述

toocreate 事件方格訂用帳戶，您傳送要求 toohello Create Event 訂用帳戶作業。 使用下列格式的 hello:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

例如，toocreate 事件訂閱名為儲存體帳戶`examplestorage`資源群組中名為`examplegroup`，使用 hello 下列格式：

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

hello 文章說明 hello 屬性和 hello hello 要求主體的結構描述。
 
## <a name="event-subscription-properties"></a>事件訂用帳戶屬性

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| 目的地 | 物件 | hello 定義 hello 端點的物件。 |
| filter | 物件 | 篩選 hello 事件類型的選擇性欄位。 |

### <a name="destination-object"></a>目的地物件

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| endpointType | 字串 | hello hello 訂用帳戶 （webhook/HTTP，事件中心或佇列） 的端點類型。 | 
| endpointUrl | 字串 |  | 

### <a name="filter-object"></a>篩選物件

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| includedEventTypes | array | 比對這些事件的型別名稱的完全相符 tooone hello hello 事件訊息中的事件類型時。 事件名稱與 hello 事件來源的 hello 註冊事件類型名稱不相符時，會引發錯誤。 預設會符合所有事件類型。 |
| subjectBeginsWith | 字串 | 前置詞比對篩選 toohello 主旨欄位 hello 事件訊息中。 hello 預設值或空字串比對所有。 | 
| subjectEndsWith | 字串 | 後置詞比對篩選 toohello 主旨欄位 hello 事件訊息中。 hello 預設值或空字串比對所有。 |
| subjectIsCaseSensitive | 字串 | 控制篩選的區分大小寫比對。 |


## <a name="example-subscription-schema"></a>範例訂用帳戶的結構描述

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>後續步驟

* 如簡介 tooEvent 格線，請參閱[事件方格是什麼？](overview.md)
