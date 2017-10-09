---
title: "aaaAzure 函式的 Blob 儲存體繫結 |Microsoft 文件"
description: "了解觸發 toouse Azure 儲存體的方式，在 Azure 函式中的繫結。"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Azure Functions Blob 儲存體繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

這篇文章說明如何 tooconfigure 地使用 Azure 功能中的 Azure Blob 儲存體繫結。 Azure Functions 支援適用於 Azure Blob 儲存體的觸發程序、輸入和輸出繫結。 如需所有繫結中可用的功能，請參閱 [Azure Functions 觸發程序和繫結概念](functions-triggers-bindings.md)。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> 不支援[僅限 blob 儲存體帳戶](../storage/common/storage-create-storage-account.md#blob-storage-accounts)。 Blob 儲存體觸發程序和繫結需要一般用途的儲存體帳戶。 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>Blob 儲存體觸發程序和繫結

使用 hello Azure Blob 儲存體觸發程序，便會在偵測到新的或更新的 blob 時，呼叫您的函式程式碼。 輸入的 toohello 函式，提供 hello blob 內容。

定義使用 hello blob 儲存體觸發程序**整合**hello 函式的入口網站中的索引標籤。 hello 入口網站會建立下列 hello 中的定義的 hello**繫結**區段*function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

Blob 輸入和輸出繫結透過定義`blob`hello 繫結類型為：

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* hello`path`屬性支援繫結運算式和篩選參數。 請參閱[名稱模式](#pattern)。
* hello`connection`屬性必須包含 hello 包含儲存體連接字串的應用程式設定名稱。 Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合** 索引標籤會將此應用程式設定，當您選取的儲存體帳戶。

> [!NOTE]
> 當您使用的 blob 觸發程序消耗計劃時，可以有向上 tooa 10 分鐘的延遲之後函式應用程式已進入閒置處理新的 blob。 Hello 函式應用程式執行之後，blob 會立即處理。 此初始 tooavoid 延遲，請考慮下列選項的 hello 的其中一個：
> - 使用 App Service 方案並啟用「永遠開啟」。
> - 使用處理，例如包含 hello blob 名稱的佇列訊息另一個的機制 tootrigger hello blob。 如需範例，請參閱[具有 blob 輸入繫結的佇列觸發程序](#input-sample)。

<a name="pattern"></a>

### <a name="name-patterns"></a>名稱模式
您可以指定 blob 名稱模式中 hello`path`屬性，可以篩選或繫結運算式。 請參閱[繫結運算式和模式](functions-triggers-bindings.md#binding-expressions-and-patterns)。

比方說，toofilter tooblobs 開頭為 「 原始 」 hello 字串使用下列定義 hello。 這個路徑尋找名為 blob*原始 Blob1.txt*在 hello*輸入*容器和 hello hello 值`name`函式程式碼中的變數是`Blob1`。

```json
"path": "input/original-{name}",
```

toobind toohello blob 檔案名稱和副檔名分別使用兩種模式。 此路徑也會尋找名為 blob*原始 Blob1.txt*，和 hello hello 值`blobname`和`blobextension`函式程式碼中的變數*原始 Blob1*和*txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

您可以使用固定的值 hello 副檔名限制 hello 檔案類型的 blob。 比方說，tootrigger 只能在.png 檔案上使用 hello 下列模式：

```json
"path": "samples/{name}.png",
```

大括號是名稱模式中的特殊字元。 toospecify blob 名稱 hello 名稱中有大括號，您可以逸出 hello 使用兩個大括號的大括號。 hello 下列範例會尋找名為 blob *{20140101}-soundfile.mp3*在 hello*映像*容器和 hello `name` hello 函式程式碼中變數的值是*soundfile.mp3*。 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>觸發程序中繼資料

hello blob 觸發程序會提供數個中繼資料屬性。 這些屬性可作為其他繫結中繫結運算式的一部分或程式碼中的參數使用。 這些值有 hello 相同的語意[CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet)。

- **BlobTrigger**： 輸入 `string`。 hello 觸發 blob 路徑
- **URI**： 輸入 `System.Uri`。 hello 主要位置的 hello blob 的 URI。
- **屬性**： 輸入 `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`。 hello blob 的系統屬性。
- **中繼資料**： 輸入 `IDictionary<string,string>`。 hello hello blob 的使用者定義中繼資料。

<a name="receipts"></a>

### <a name="blob-receipts"></a>Blob 回條
hello Azure 函式執行階段會確保沒有任何 blob 觸發程序函式取得呼叫一次以上的 hello 相同的新功能或更新 blob。 如果已處理指定的 blob 版本 toodetermine，它會維護*blob 回條*。

Azure 的函式存放區 blob 容器中的回條*azure webjobs 託管*hello 函式應用程式的 Azure 儲存體帳戶中 (hello 應用程式設定所定義`AzureWebJobsStorage`)。 Blob 的回條具有 hello 下列資訊：

* hello 觸發函式 (「*&lt;函式應用程式名稱 >*。函式。*&lt;函式名稱 >*"，例如:"MyFunctionApp.Functions.CopyBlob")
* hello 容器名稱
* hello blob 類型 （"BlockBlob"或"PageBlob"）
* hello blob 名稱
* hello ETag (例如 blob 版本識別碼:"0x8D1DC6E70A277EF")

tooforce 重新處理的 blob，blob 的 hello blob 回條刪除 hello *azure webjobs 託管*容器以手動方式。

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>處理有害的 blob
當指定 blob 的 blob 觸發程序函式失敗時，Azure Functions 預設一共會重試該函式 5 次。 

如果所有 5 次嘗試失敗，Azure 函式會將名為訊息 tooa 儲存體佇列*webjobs-blobtrigger-有害*。 hello 佇列訊息的有害的 blob 是 JSON 物件，包含下列屬性的 hello:

* FunctionId (hello 格式*&lt;函式應用程式名稱 >*。函式。*&lt;函式名稱 >*)
* BlobType ("BlockBlob" 或 "PageBlob")
* ContainerName
* BlobName
* ETag (Blob 版本識別碼，例如："0x8D1DC6E70A277EF")

### <a name="blob-polling-for-large-containers"></a>大型容器的 Blob 輪詢
如果受監視的 hello blob 容器包含超過 10,000 個 blob，hello 函式執行階段掃描記錄檔 toowatch 的新增或變更的 blob。 此程序不是即時。 函式可能不會觸發直到幾分鐘的時間或更久之後建立 hello 的 blob。 此外，[會以「最大努力」建立儲存體記錄](/rest/api/storageservices/About-Storage-Analytics-Logging)。 並不保證會擷取所有的事件。 在某些情況下可能會遺失記錄檔。 如果您需要更快或更可靠的 blob 處理，請考慮建立[佇列訊息](../storage/queues/storage-dotnet-how-to-use-queues.md)當您建立 hello blob。 然後，使用[佇列觸發程序](functions-bindings-storage-queue.md)而不是 blob 觸發程序 tooprocess hello blob。

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>使用 blob 觸發程序和輸入繫結
在.NET 函式，存取 hello blob 資料使用的方法參數，例如`Stream paramName`。 在這裡，`paramName`是您在 hello 中指定的 hello 值[觸發程序組態](#trigger)。 在 Node.js 函數中，輸入使用的 blob 資料存取 hello `context.bindings.<name>`。

在.NET 中，您可以結合 hello 型別的 tooany hello 下面的清單中。 如果用作輸入繫結，其中一些類型需要 *function.json* 中的 `inout` 繫結方向。 因此您必須使用進階編輯器 hello hello 標準編輯器中，不被支援這個方向。

* `TextReader`
* `Stream`
* `ICloudBlob` (需要 "inout" 繫結方向)
* `CloudBlockBlob` (需要 "inout" 繫結方向)
* `CloudPageBlob` (需要 "inout" 繫結方向)
* `CloudAppendBlob` (需要 "inout" 繫結方向)

如果預期文字 blob，您也可以繫結 tooa.NET`string`型別。 這只被建議如果 hello blob 大小很小，如 hello 整個 blob 內容會載入記憶體。 通常，它是比 toouse`Stream`或`CloudBlockBlob`型別。

## <a name="trigger-sample"></a>觸發程序範例
假設您有下列定義的 blob 儲存體觸發程序的 function.json hello:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

請參閱記錄 hello toohello 受監視的容器加入每一個 blob 內容的 hello 特定語言的範例。

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>C# 中的 Blob 觸發程序範例 #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Node.js 中的觸發程序範例

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>使用 blob 輸出繫結

在.NET 函數中，您應該使用`out string`函式簽章中使用其中一個 hello hello 下列清單中的型別參數。 Node.js 函式，在您存取 hello 輸出 blob 使用`context.bindings.<name>`。

.NET 函式中，您可以輸出 tooany 的 hello 下列類型：

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>具有 blob 輸入和輸出的佇列觸發程序範例
假設您有下列 function.json hello，定義[佇列儲存體觸發程序](functions-bindings-storage-queue.md)、 blob 儲存體輸入和輸出 blob 儲存體。 請注意 hello 使用 hello`queueTrigger`中繼資料屬性。 在輸入和輸出的 hello blob`path`屬性：

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

請參閱複製 hello 輸入的 blob toohello 輸出 blob 的 hello 特定語言的範例。

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>C# 中的 blob 繫結範例 #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Node.js 中的 blob 繫結範例

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

