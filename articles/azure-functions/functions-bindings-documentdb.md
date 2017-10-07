---
title: "aaaAzure 函式 Cosmos DB 繫結 |Microsoft 文件"
description: "了解如何在 Azure 函式 toouse Azure Cosmos DB 繫結。"
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a>Azure Functions Cosmos DB 繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

這篇文章說明如何在 Azure 函式的 tooconfigure 和程式碼 Azure Cosmos DB 繫結。 Azure Functions 支援 Cosmos DB 的輸入和輸出繫結。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

如需有關 Cosmos DB 的詳細資訊，請參閱[簡介 tooCosmos DB](../documentdb/documentdb-introduction.md)和[建置 Cosmos DB 主控台應用程式](../documentdb/documentdb-get-started.md)。

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>DocumentDB API 輸入繫結
hello DocumentDB API 輸入繫結擷取 Cosmos DB 文件，並將其傳遞 toohello 名為的 hello 函式的輸入的參數。 判斷識別碼 hello 文件以 hello 函式會叫用的 hello 觸發程序。 

hello DocumentDB API 輸入繫結具有下列屬性中的 hello *function.json*:

- `name`： 使用函式程式碼中的 hello 文件識別名稱
- `type`： 必須設定得 「 documentdb"
- `databaseName`: hello 資料庫包含 hello 文件
- `collectionName`: hello 集合，其中包含 hello 文件
- `id`: hello hello 文件 tooretrieve 的識別碼。 此屬性支援繫結參數。請參閱[toocustom 輸入的屬性繫結中繫結運算式](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression)hello 本文[Azure 函式的觸發程序和繫結概念](functions-triggers-bindings.md)。
- `sqlQuery`：用來擷取多份文件的 Cosmos DB SQL 查詢。 hello 查詢支援執行階段繫結。 例如：`SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: hello 包含 Cosmos DB 連線字串 hello 應用程式設定名稱
- `direction`： 必須設定得`"in"`。

hello 屬性`id`和`sqlQuery`無法同時指定。 如果沒有`id`也`sqlQuery`設定，hello 整個擷取集合。

## <a name="using-a-documentdb-api-input-binding"></a>使用 DocumentDB API 輸入繫結

* 在 C# 和 F # 函式，hello 函式成功，結束時也會自動保存 toohello 透過具名的輸入參數的輸入文件所做的變更。 
* 在 JavaScript 函數中，不會在函數結束時自動執行更新。 請改用`context.bindings.<documentName>In`和`context.bindings.<documentName>Out`toomake 更新。 請參閱 hello [JavaScript 範例](#injavascript)。

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>單一文件的輸入範例
假設您有下列 hello DocumentDB API 輸入 hello 中的繫結`bindings`function.json 的陣列：

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

請參閱 hello 特定語言的範例會使用此輸入繫結 tooupdate hello 文件的文字值。

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>C# 中的輸入範例 #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>F# 中的輸入範例 #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

這個範例需要`project.json`檔案，指定 hello`FSharp.Interop.Dynamic`和`Dynamitey`NuGet 相依性：

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

tooadd`project.json`檔案，請參閱[F # 封裝管理](functions-reference-fsharp.md#package)。

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>以 JavaScript 撰寫的輸入範例

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>具有多份文件的輸入範例

假設您想 tooretrieve SQL 查詢，所指定的多個文件使用佇列觸發程序 toocustomize hello 查詢參數。 

在此範例中，hello 佇列觸發程序提供的參數`departmentId`。佇列訊息的`{ "departmentId" : "Finance" }`會傳回 hello 財務部門的所有記錄。 使用中的 hello 下列*function.json*:

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a>以 C# 撰寫之具有多份文件的輸入範例

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a>以 JavaScript 撰寫之具有多份文件的輸入範例

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <a id="docdboutput"></a>DocumentDB API 輸出繫結
hello DocumentDB API 輸出繫結可讓您撰寫新的文件 tooan Azure Cosmos DB 資料庫。 它有下列屬性中的 hello *function.json*:

- `name`： 識別項在函式程式碼用於 hello 新文件
- `type`： 必須太設定`"documentdb"`
- `databaseName`： 包含 hello 集合將會建立新文件 hello hello 資料庫。
- `collectionName`: hello hello 新文件將會建立的集合。
- `createIfNotExists`： 布林值 tooindicate 是否會建立 hello 集合，如果不存在。 hello 預設值是*false*。 hello 原因為新建立的集合，以使用保留輸送量，具有定價含意。 如需詳細資訊，請瀏覽 hello[定價頁面](https://azure.microsoft.com/pricing/details/documentdb/)。
- `connection`: hello 包含 Cosmos DB 連線字串 hello 應用程式設定名稱
- `direction`： 必須太設定`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>使用 DocumentDB API 輸出繫結
本節說明如何 toouse DocumentDB API 輸出繫結函式程式碼中。

當您撰寫 toohello 輸出參數在函數中，預設資料庫中產生新的文件時，以自動產生的 GUID 為 hello 文件識別碼。 您可以指定 hello 文件識別碼的輸出文件，藉由指定 hello `id` hello 中的 JSON 屬性輸出參數。 

>[!Note]  
>當您指定的現有文件的 hello 識別碼時，則取得 hello 新輸出文件的覆寫。 

toooutput 多份文件，您也可以繫結太`ICollector<T>`或`IAsyncCollector<T>`其中`T`是其中一個支援的 hello 類型。

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>DocumentDB API 輸出繫結範例
假設您有下列 hello DocumentDB API 輸出繫結中 hello `bindings` function.json 的陣列：

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

而且您擁有 hello 遵循格式中接收 JSON 的佇列的佇列輸入繫結：

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

與要 toocreate Cosmos DB 文件以 hello 遵循每一筆記錄的格式：

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

請參閱 hello 特定語言的範例會使用此輸出繫結 tooadd 文件 tooyour 資料庫。

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# 中的輸出範例 #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>F# 中的輸出範例 #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

這個範例需要`project.json`檔案，指定 hello`FSharp.Interop.Dynamic`和`Dynamitey`NuGet 相依性：

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

tooadd`project.json`檔案，請參閱[F # 封裝管理](functions-reference-fsharp.md#package)。

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>以 JavaScript 撰寫的輸出範例

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
