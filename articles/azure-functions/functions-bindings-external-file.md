---
title: "aaaAzure 函式的外部檔案繫結 （預覽） |Microsoft 文件"
description: "使用 Azure Functions 中的外部檔案繫結"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a>Azure Functions 外部檔案繫結 (預覽)
本文將說明如何 toomanipulate 檔案從不同 SaaS 提供者 （例如 OneDrive、 Dropbox） 內您利用內建繫結的函式。 Azure Functions 支援適用於外部檔案的觸發程序、輸入和輸出繫結。

這個繫結 tooSaaS 提供者，會建立應用程式開發介面的連接，或使用來自函式應用程式的資源群組的現有應用程式開發介面連線。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>支援的檔案連線

|連接器|觸發程序|輸入|輸出|
|:-----|:---:|:---:|:---:|
|[Box](https://www.box.com)|x|x|x
|[Dropbox](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[商務用 OneDrive](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Google Drive](https://www.google.com/drive/)||x|x|

> [!NOTE]
> 外部檔案連線也可以用在 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) 中

## <a name="external-file-trigger-binding"></a>外部檔案觸發程序繫結

hello Azure 外部檔案觸發程序可讓您監視遠端資料夾，並執行您的函式程式碼，偵測到變更時。

hello 外部檔案觸發程序會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a>名稱模式
您可以指定檔案名稱模式中 hello`path`屬性。 參考的 hello 資料夾必須存在於 hello SaaS 提供者。
範例：

```json
"path": "input/original-{name}",
```

此路徑會尋找名為*原始 File1.txt*在 hello*輸入*資料夾，然後 hello hello 值`name`函式程式碼中的變數會是`File1.txt`。

另一個範例：

```json
"path": "input/{filename}.{fileextension}",
```

此路徑也會尋找名為*原始 File1.txt*，和 hello hello 值`filename`和`fileextension`函式程式碼中的變數會是*原始 File1*和*txt*。

您可以限制 hello 檔案類型的檔案副檔名為 hello 使用固定的值。 例如：

```json
"path": "samples/{name}.png",
```

在此情況下，只有*.png*檔案在 hello*範例*資料夾觸發程序 hello 函式。

大括號是名稱模式中的特殊字元。 大括號名稱中含有 hello、 double hello 大括號 toospecify 檔案名稱。
例如：

```json
"path": "images/{{20140101}}-{name}",
```

此路徑會尋找名為*{20140101}-soundfile.mp3*在 hello*映像*資料夾，然後 hello `name` hello 函式程式碼中的變數值會是*soundfile.mp3*.

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a>處理有害的檔案
外部檔案的觸發程序函式失敗時，Azure 函式重試該函式 too5 時間 （包括 hello 第一次嘗試） 的預設值為指定的檔案。
如果所有 5 次嘗試失敗，函式會將名為訊息 tooa 儲存體佇列*webjobs-apihubtrigger-有害*。 hello 佇列訊息的有害的檔案是包含下列屬性的 hello 的 JSON 物件：

* FunctionId (hello 格式*&lt;函式應用程式名稱 >*。函式。*&lt;函式名稱 >*)
* FileType
* FolderName
* FileName
* ETag (檔案版本識別碼，例如："0x8D1DC6E70A277EF")


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>觸發程序使用方式
在 C# 函數中，您 toohello 輸入的檔案將資料繫結函式簽章中使用具名的參數，例如`<T> <name>`。
其中`T`是 hello 資料類型的 toodeserialize hello 資料分割，以及`paramName`是您在指定的 hello 名稱[觸發 JSON](#trigger)。 Node.js 函式，在您存取 hello 輸入的檔資料使用`context.bindings.<name>`。

hello 檔案可以還原序列化為任何下列類型的 hello:

* 任何[物件 (機器翻譯)](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的檔案資料。
  如果您宣告自訂的輸入的類型 (例如`FooType`)，Azure 函式會嘗試 toodeserialize hello JSON 資料到您指定的型別。
* 字串 - 適用於文字檔案資料。

在 C# 函式，您也可以繫結 tooany 的 hello 下列類型，並 hello 函式執行階段會嘗試使用該類型的 hello 檔案資料還原序列化：

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>觸發程序範例
假設您有下列 function.json hello，定義檔案外部觸發程序：

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

請參閱記錄 hello toohello 監控的資料夾加入每個檔案內容的 hello 特定語言的範例。

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>C# 中的觸發程序使用方式 #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a>Node.js 中的觸發程序使用方式

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>外部檔案輸入繫結
hello Azure 外部的檔案輸入繫結可讓您 toouse 函式中的外部資料夾中的檔案。

hello 外部檔案輸入的 tooa 函式會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

請注意 hello 下列：

* `path`必須包含 hello 資料夾名稱和 hello 檔案名稱。 例如，如果您有[佇列觸發程序](functions-bindings-storage-queue.md)在您的函式，您可以使用`"path": "samples-workitems/{queueTrigger}"`toopoint tooa 檔案在 hello`samples-workitems`資料夾名稱符合 hello hello 觸發程序的訊息中指定的檔案名稱。   

<a name="inputusage"></a>

## <a name="input-usage"></a>輸入使用方式
在 C# 函數中，您 toohello 輸入的檔案將資料繫結函式簽章中使用具名的參數，例如`<T> <name>`。
其中`T`是 hello 資料類型的 toodeserialize hello 資料分割，以及`paramName`是您在指定的 hello 名稱[輸入繫結](#input)。 Node.js 函式，在您存取 hello 輸入的檔資料使用`context.bindings.<name>`。

hello 檔案可以還原序列化為任何下列類型的 hello:

* 任何[物件 (機器翻譯)](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的檔案資料。
  如果您宣告自訂的輸入的類型 (例如`InputType`)，Azure 函式會嘗試 toodeserialize hello JSON 資料到您指定的型別。
* 字串 - 適用於文字檔案資料。

在 C# 函式，您也可以繫結 tooany 的 hello 下列類型，並 hello 函式執行階段會嘗試使用該類型的 hello 檔案資料還原序列化：

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>外部檔案輸出繫結
hello Azure 外部的檔案輸出繫結可讓您在您的函式的 toowrite files tooan 外部資料夾。

輸出的函式使用下列 JSON 物件中 hello hello hello 外部檔案`bindings`function.json 的陣列：

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

請注意 hello 下列：

* `path`必須包含 hello 資料夾名稱和到 hello 檔案名稱 toowrite。 例如，如果您有[佇列觸發程序](functions-bindings-storage-queue.md)在您的函式，您可以使用`"path": "samples-workitems/{queueTrigger}"`toopoint tooa 檔案在 hello`samples-workitems`資料夾名稱符合 hello hello 觸發程序的訊息中指定的檔案名稱。   

<a name="outputusage"></a>

## <a name="output-usage"></a>輸出使用方式
在 C# 函數中，您使用繫結 toohello 輸出檔名為 hello`out`函式簽章中的參數喜歡`out <T> <name>`，其中`T`是 hello 資料類型的 tooserialize hello 資料分割，和`paramName`是 hello 名稱指定在[輸出繫結](#output)。 Node.js 函式，在您存取 hello 輸出檔案使用`context.bindings.<name>`。

您可以撰寫使用任何下列類型的 hello toohello 輸出檔：

* 任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化。
  如果您宣告自訂輸出型別 (例如`out OutputType paramName`)，Azure 函式會嘗試 tooserialize 物件為 JSON。 如果 hello 函式結束時，hello 輸出參數為 null，hello 函式執行階段會建立檔案為 null 的物件。
* 字串 - (`out string paramName`) 適用於文字檔案資料。 hello 函式執行階段建立檔案，只有當 hello 函式結束時，字串參數為非 null。

您也可以輸出 tooany hello 下列類型的 C# 函式中：

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>輸入 + 輸出範例
假設您有下列 function.json hello，定義[儲存體佇列觸發程序](functions-bindings-storage-queue.md)、 外部檔案輸入和輸出的外部檔案：

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

請參閱 hello 複製 hello 輸入的檔 toohello 輸出檔案的特定語言的範例。

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>C# 中的使用方式 #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a>Node.js 中的使用方式

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
