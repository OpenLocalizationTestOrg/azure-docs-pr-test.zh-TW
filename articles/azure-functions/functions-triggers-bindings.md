---
title: "以觸發程序與 Azure 功能中的繫結 aaaWork |Microsoft 文件"
description: "您的程式碼執行 tooonline 事件和雲端式服務，了解如何 toouse 觸發程序和 tooconnect Azure 函式中的繫結。"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Azure Functions 觸發程序和繫結概念
Azure 的函式可讓您在 Azure 及其他服務的回應 tooevents toowrite 程式碼透過*觸發程序*和*繫結*。 此文章是適用於所有支援之程式設計語言的觸發程序和繫結的概念性概觀。 一般 tooall 繫結的功能為此處所述。

## <a name="overview"></a>概觀

觸發程序和繫結所宣告的方式來 toodefine 函式如何叫用和哪些資料可搭配。 「觸發程序」會定義叫用函數的方式。 一個函數只能恰有一個觸發程序。 觸發程序擁有相關資料，通常是觸發 hello 函式的 hello 裝載。 

輸入和輸出*繫結*提供宣告式方式 tooconnect toodata 從您的程式碼中。 類似 tootriggers，連接字串和其他屬性中指定函式設定。 繫結是選擇性的，而且一個函數可以有多個輸入和輸出繫結。 

使用觸發程序和繫結，您可以撰寫程式碼更泛用，不會硬 hello 服務與它互動的 hello 詳細資料。 來自服務的資料會直接成為函數程式碼的輸入值。 toooutput 資料 tooanother 服務 （例如建立新的資料列中 Azure 資料表儲存體），使用 hello hello 方法傳回值。 或者，如果您需要 toooutput 多個值時，使用協助程式物件。 觸發程序和繫結有**名稱**屬性，這是您在程式碼 tooaccess hello 繫結中使用的識別項。

您可以設定觸發程序和繫結中 hello**整合**hello Azure 函式的入口網站中的索引標籤。 Hello 幕後 hello UI 修改檔案，稱為*function.json* hello 函式的目錄中的檔案。 您可以編輯此檔案，藉由變更 toohello**進階的編輯器**。

hello 下表顯示 hello 觸發程序和支援的 Azure 函式繫結。 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>範例︰佇列觸發程序和資料表輸出繫結

假設您想 toowrite 新的資料列 tooAzure 資料表儲存體，每當新的訊息會出現在 Azure 佇列儲存體。 此案例可以使用 Azure 佇列觸發程序和資料表輸出繫結來實作。 

佇列觸發程序需要下列資訊在 hello hello**整合** 索引標籤：

* hello 包含 hello hello 佇列儲存體帳戶連接字串的 hello 應用程式設定名稱
* hello 佇列名稱
* hello hello 佇列訊息，您的程式碼 tooread hello 內容中的識別項，例如`order`。

toowrite tooAzure 資料表儲存體，使用下列詳細資料的 hello 的輸出繫結：

* hello 包含 hello hello 資料表儲存體帳戶連接字串的 hello 應用程式設定名稱
* hello 資料表名稱
* 在您的程式碼 toocreate hello 識別碼輸出項目或 hello hello 函式傳回值。

繫結會使用應用程式設定的連接字串 tooenforce hello 最佳練習， *function.json*不包含服務密碼。

然後，使用您在程式碼中提供與 Azure 儲存體 toointegrate hello 識別項。

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

以下是 hello *function.json*對應 toohello 前面程式碼。 請注意該相同的設定可以使用，不論 hello 語言的 hello 函式實作的 hello。

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
tooview 和編輯的 hello 內容*function.json*在 hello Azure 入口網站，按一下 hello**進階的編輯器**選項 hello**整合**函式的索引標籤。

如需程式碼範例及整合 Azure 儲存體的詳細資訊，請參閱 [Azure 儲存體的 Azure Functions 觸發程序和繫結](functions-bindings-storage.md)。

### <a name="binding-direction"></a>繫結方向

所有觸發程序和繫結都具有 `direction` 屬性：

- 觸發程序，hello 方向一律是`in`
- 輸入和輸出繫結使用 `in` 和 `out`
- 某些繫結支援特殊方向 `inout`。 如果您使用`inout`，只有 hello**進階的編輯器**位於 hello**整合** 索引標籤。

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>使用 hello 函式傳回型別 tooreturn 單一輸出

hello 前面的範例顯示如何 toouse hello 函式傳回值 tooprovide 輸出 tooa 繫結，這利用 hello 特殊的 name 參數來達成`$return`。 (這只支援有傳回值的語言，例如 C#、JavaScript 和 F#)。如果函式具有多個輸出繫結，使用`$return`只為其中一個 hello 輸出繫結。 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

以下顯示 hello 範例如何傳回類型 C#、 JavaScript 和 F # 中的輸出繫結搭配使用。

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>繫結 dataType 屬性

在.NET 中，用於輸入資料中的 hello 類型 toodefine hello 資料型別。 例如，使用`string`佇列觸發程序，以二進位位元組陣列 tooread toobind toohello 文字。

對於 JavaScript 等動態具類型的語言，使用 hello `dataType` hello 繫結的定義中的屬性。 例如，tooread hello 內容的 HTTP 要求以二進位格式，請使用 hello 類型`binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

`dataType` 也另具有 `stream` 和 `string` 兩種選項。

## <a name="resolving-app-settings"></a>解析應用程式設定
為了遵循最佳做法，祕密和連接字串應使用應用程式設定來管理，而不是使用組態檔。 這會限制存取 toothese 機密資料，並使其安全 toostore *function.json*公用的原始檔控制儲存機制中。

每當您想要根據 hello 環境 toochange 設定時，應用程式設定也很有用。 例如，在測試環境中，您可能想 toomonitor 不同的佇列或 blob 儲存體容器。

只要某個值是以百分比符號括住 (例如 `%MyAppSetting%`)，就會解析應用程式設定。 請注意該 hello`connection`的觸發程序和繫結的屬性是特殊案例，並自動解析為應用程式設定的值。 

hello 下列範例會使用應用程式設定的佇列觸發程序`%input-queue-name%`toodefine hello 佇列 tootrigger 上的。

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>觸發程序中繼資料屬性

在加法 toohello 資料承載中提供的觸發程序 （例如觸發函式的 hello 佇列訊息），許多觸發程序會提供額外的中繼資料值。 這些值可用來當做輸入參數，以 C# 和 F # 類型或屬性上 hello`context.bindings`在 JavaScript 中的物件。 

例如，佇列觸發程序支援 hello 下列屬性：

* QueueTrigger - 如果是有效字串，便觸發訊息內容
* DequeueCount
* ExpirationTime
* 識別碼
* InsertionTime
* NextVisibleTime
* PopReceipt

Hello 對應的參考主題說明的每個觸發程序的中繼資料屬性的詳細資料。 文件集也會提供 hello**整合**hello 入口網站，在 [hello] 索引標籤**文件**hello 繫結設定區域下的一節。  

例如，因為 blob 觸發程序有一些延遲，所以您可以使用佇列觸發程序 toorun 您的函式 (請參閱[Blob 儲存體觸發程序](functions-bindings-storage-blob.md#storage-blob-trigger)。 hello 佇列訊息會包含 hello blob filename tootrigger 上。 使用 hello`queueTrigger`中繼資料屬性，您可以在您的設定，而不是您的程式碼中指定此行為。

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

從觸發程序的中繼資料屬性也可用在*繫結運算式*另一個繫結，以遵循 > 一節中所述的 hello。

## <a name="binding-expressions-and-patterns"></a>繫結運算式和模式

Hello 的觸發程序和繫結功能最強大的功能之一是*運算式繫結*。 在繫結中，您可以定義模式運算式，並將它用於其他繫結或您的程式碼。 觸發程序的中繼資料也可以用於繫結 hello 範例 hello 前面一節中所顯示的運算式。

例如，假設您想要在特定的 blob 儲存體容器，類似 toohello tooresize 影像**影像大小調整程式**hello 範本**新函式**頁面。 跳過**新函式**]-> [語言**C#** ]-> [案例**範例** -> **ImageResizer CSharp**。 

以下是 hello *function.json*定義：

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

請注意該 hello `filename` hello blob 觸發程序的定義以及 hello blob 中使用參數輸出繫結。 這個參數也可以用於函數程式碼。

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>隨機 GUID
Azure 的函式提供在您的繫結，透過 hello 中產生 Guid 的便利性語法`{rand-guid}`繫結運算式。 hello 下列範例會使用這個 toogenerate 唯一 blob 名稱： 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>目前時間

您可以使用 hello 繫結運算式`DateTime`，這會解析太`DateTime.UtcNow`。

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>繫結運算式中的繫結 toocustom 輸入的屬性

繫結運算式也可以參考本身 hello 觸發程序內容中所定義的屬性。 比方說，您可能想 toodynamically 繫結 tooa blob 儲存體檔案從 webhook 中提供的檔名。

比方說，hello 遵循*function.json*會使用稱為屬性`BlobName`hello 觸發程序的內容：

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish 這在 C# 和 F # 中，您必須定義 hello 觸發程序內容中所定義將還原序列化的 hello 欄位 POCO。

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

在 JavaScript 中，JSON 還原序列化會自動執行，您可以直接使用 hello 屬性。

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>在執行階段設定繫結資料

在 C# 和其他.NET 語言，您可以使用命令式繫結模式，但不要的 toohello 中的宣告式繫結為*function.json*。 命令式的繫結時，必須在執行階段，而不是設計階段計算 toobe 繫結參數。 詳細資訊，請參閱 toolearn[在執行階段透過命令式繫結的繫結](functions-reference-csharp.md#imperative-bindings)hello C# 開發人員參考資料中。

## <a name="next-steps"></a>後續步驟
如需有關特定繫結的詳細資訊，請參閱下列文章 hello:

- [HTTP 和 Webhook](functions-bindings-http-webhook.md)
- [計時器](functions-bindings-timer.md)
- [佇列儲存體](functions-bindings-storage-queue.md)
- [Blob 儲存體](functions-bindings-storage-blob.md)
- [資料表儲存體](functions-bindings-storage-table.md)
- [事件中樞](functions-bindings-event-hubs.md)
- [服務匯流排](functions-bindings-service-bus.md)
- [Cosmos DB](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [通知中樞](functions-bindings-notification-hubs.md)
- [行動應用程式](functions-bindings-mobile-apps.md)
- [外部檔案](functions-bindings-external-file.md)
