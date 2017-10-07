---
title: "aaaAzure 函式儲存體資料表繫結 |Microsoft 文件"
description: "了解如何 toouse Azure 函式中的 Azure 儲存體繫結。"
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a>Azure Functions 儲存體資料表繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

本文說明如何 tooconfigure 和程式碼的 Azure 儲存體資料表 Azure 函式中的繫結。 Azure Functions 支援 Azure 儲存體資料表的輸入和輸出繫結。

hello 儲存體資料表繫結支援下列案例的 hello:

* **讀取 C# 或 Node 函式中的單一資料列** - 設定 `partitionKey` 和 `rowKey`。 hello`filter`和`take`屬性不適用於在此案例中。
* **讀取的 C# 函式中的多個資料列**-hello 函式執行階段提供`IQueryable<T>`物件繫結 toohello 資料表。 類型 `T` 必須衍生自 `TableEntity` 或實作 `ITableEntity`。 hello `partitionKey`， `rowKey`， `filter`，和`take`屬性不適用於在此案例中，您可以使用 hello`IQueryable`物件 toodo 所需的任何篩選。 
* **讀取中節點函式的多個資料列**-設定的 hello`filter`和`take`屬性。 請勿設定 `partitionKey` 或 `rowKey`。
* **C# 函式中寫入一或多個資料列**-hello 函式執行階段提供`ICollector<T>`或`IAsyncCollector<T>`繫結的 toohello 資料表，其中`T`指定 hello 結構描述要 tooadd 的 hello 實體。 一般而言，類型 `T` 會衍生自 `TableEntity` 或實作 `ITableEntity`，但不一定如此。 hello `partitionKey`， `rowKey`， `filter`，和`take`屬性不適用於在此案例中。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>儲存體資料表輸入繫結
hello Azure 儲存體資料表的輸入繫結可讓您 toouse 函式中的儲存體資料表。 

hello 儲存資料表輸入的 tooa 函式會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

請注意 hello 下列： 

* 使用`partitionKey`和`rowKey`一起 tooread 單一實體。 這些屬性是選擇性的。 
* `connection`必須包含 hello 包含儲存體連接字串的應用程式設定名稱。 Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合**您建立儲存體帳戶，或是選取現有的索引標籤會設定此應用程式設定。 您也可以[手動進行此應用程式設定](functions-how-to-use-azure-function-app-settings.md#settings)。  

<a name="inputusage"></a>

## <a name="input-usage"></a>輸入使用方式
在 C# 函數中，您使用繫結 toohello 輸入資料表實體 （或實體） 具名的參數，在您的函式簽章，like `<T> <name>`。
其中`T`是 hello 資料類型的 toodeserialize hello 資料分割，以及`paramName`是您在 hello 中指定的 hello 名稱[輸入繫結](#input)。 Node.js 函式，在您存取 hello 輸入資料表實體 （或實體） 使用`context.bindings.<name>`。

Node.js 或 C# 的函式中可還原序列化 hello 輸入的資料。 還原序列化的 hello 物件具有`RowKey`和`PartitionKey`屬性。

在 C# 函數中，您也可以繫結 tooany 的 hello 下列類型，和執行階段會嘗試的 hello 函式太還原序列化 hello 使用該類型的資料表資料：

* 實作 `ITableEntity` 的任何類型
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>輸入範例
假設您擁有 hello 遵循 function.json，會使用佇列觸發程序 tooread 單一資料表資料列。 hello JSON 指定`PartitionKey`  
 `RowKey`。 `"rowKey": "{queueTrigger}"`表示該 hello 資料列索引鍵來自 hello 佇列的訊息字串。

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
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

請參閱 hello 讀取單一資料表實體的特定語言的範例。

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>C# 中的輸入範例 #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a>F# 中的輸入範例 #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Node.js 中的輸入範例
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>儲存體資料表輸出繫結
hello Azure 儲存體資料表輸出繫結可讓您 toowrite 實體 tooa 函式中的儲存體資料表。 

hello 儲存體資料表輸出的函式使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

請注意 hello 下列： 

* 使用`partitionKey`和`rowKey`一起 toowrite 單一實體。 這些屬性是選擇性的。 您也可以指定`PartitionKey`和`RowKey`當您建立 hello 實體物件函式程式碼中。
* `connection`必須包含 hello 包含儲存體連接字串的應用程式設定名稱。 Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合**您建立儲存體帳戶，或是選取現有的索引標籤會設定此應用程式設定。 您也可以[手動進行此應用程式設定](functions-how-to-use-azure-function-app-settings.md#settings)。 

<a name="outputusage"></a>

## <a name="output-usage"></a>輸出使用方式
在 C# 函數中，您使用繫結 toohello 資料表輸出名為 hello`out`函式簽章中的參數要`out <T> <name>`，其中`T`是 hello 資料類型的 tooserialize hello 資料分割，和`paramName`是 hello 名稱指定在 hello[輸出繫結](#output)。 在 Node.js 函數中，您可以存取 hello 資料表輸出使用`context.bindings.<name>`。

您可以在 Node.js 或 C# 函式中將物件序列化。 在 C# 函數中，您也可以繫結 toohello 下列類型：

* 實作 `ITableEntity` 的任何類型
* `ICollector<T>`(toooutput 多個實體。 請參閱[範例](#outcsharp)。)
* `IAsyncCollector<T>` (`ICollector<T>` 的非同步版本)
* `CloudTable`（使用 hello Azure 儲存體 SDK。 請參閱[範例](#readmulti)。)

<a name="outputsample"></a>

## <a name="output-sample"></a>輸出範例
hello 下列*function.json*和*run.csx*範例會示範如何 toowrite 多個資料表實體。

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

請參閱 hello 建立多個資料表實體的特定語言的範例。

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# 中的輸出範例 #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>F# 中的輸出範例 #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Node.js 中的輸出範例
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a>範例：讀取 C# 中的多個資料表實體  #
hello 下列*function.json*和 C# 程式碼範例會讀取 hello 佇列訊息中指定資料分割索引鍵的實體。

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
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

hello C# 程式碼會將參考 toohello Azure 儲存體 SDK，使得 hello 實體類型可以衍生自`TableEntity`。

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

