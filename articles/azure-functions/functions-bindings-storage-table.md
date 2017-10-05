---
title: "Azure Functions 儲存體資料表繫結 | Microsoft Docs"
description: "了解如何在 Azure Functions 中使用 Azure 儲存體繫結。"
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
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="ea319-104">Azure Functions 儲存體資料表繫結</span><span class="sxs-lookup"><span data-stu-id="ea319-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ea319-105">本文說明如何在 Azure Functions 中為 Azure 儲存體資料表繫結進行設定及撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="ea319-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="ea319-106">Azure Functions 支援 Azure 儲存體資料表的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="ea319-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="ea319-107">儲存體資料表繫結支援下列案例：</span><span class="sxs-lookup"><span data-stu-id="ea319-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="ea319-108">**讀取 C# 或 Node 函式中的單一資料列** - 設定 `partitionKey` 和 `rowKey`。</span><span class="sxs-lookup"><span data-stu-id="ea319-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="ea319-109">此案例中不使用 `filter` 和 `take` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ea319-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="ea319-110">**讀取 C# 函式中的多個資料列** - Functions 執行階段會提供一個繫結至資料表的 `IQueryable<T>` 物件。</span><span class="sxs-lookup"><span data-stu-id="ea319-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="ea319-111">類型 `T` 必須衍生自 `TableEntity` 或實作 `ITableEntity`。</span><span class="sxs-lookup"><span data-stu-id="ea319-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="ea319-112">此案例中不使用 `partitionKey`、`rowKey`、`filter` 和 `take`屬性；您可以使用 `IQueryable` 物件來執行任何所需的篩選。</span><span class="sxs-lookup"><span data-stu-id="ea319-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="ea319-113">**讀取 Node 函式中的多個資料列** - 設定 `filter` 和 `take` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ea319-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="ea319-114">請勿設定 `partitionKey` 或 `rowKey`。</span><span class="sxs-lookup"><span data-stu-id="ea319-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="ea319-115">**在 C# 函式中寫入一或多個資料列** - Functions 執行階段會提供一個繫結至資料表的 `ICollector<T>` 或 `IAsyncCollector<T>`，其中 `T` 指定您想要新增之實體的結構描述。</span><span class="sxs-lookup"><span data-stu-id="ea319-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="ea319-116">一般而言，類型 `T` 會衍生自 `TableEntity` 或實作 `ITableEntity`，但不一定如此。</span><span class="sxs-lookup"><span data-stu-id="ea319-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="ea319-117">此案例中不使用 `partitionKey`、`rowKey`、`filter` 和 `take` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ea319-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="ea319-118">儲存體資料表輸入繫結</span><span class="sxs-lookup"><span data-stu-id="ea319-118">Storage table input binding</span></span>
<span data-ttu-id="ea319-119">Azure 儲存體資料表輸入繫結可讓您在您的函式中使用儲存資料表。</span><span class="sxs-lookup"><span data-stu-id="ea319-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="ea319-120">函式的儲存體資料表輸入會使用 function.json `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="ea319-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="ea319-121">請注意：</span><span class="sxs-lookup"><span data-stu-id="ea319-121">Note the following:</span></span> 

* <span data-ttu-id="ea319-122">一起使用 `partitionKey` 和 `rowKey` 來讀取單一實體。</span><span class="sxs-lookup"><span data-stu-id="ea319-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="ea319-123">這些屬性是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="ea319-123">These properties are optional.</span></span> 
* <span data-ttu-id="ea319-124">`connection` 必須包含儲存體連接字串的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="ea319-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="ea319-125">在 Azure 入口網站中，當您建立儲存體帳戶或選取一個現有的儲存體帳戶時，[整合] 索引標籤中的標準編輯器可設定此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ea319-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="ea319-126">您也可以[手動進行此應用程式設定](functions-how-to-use-azure-function-app-settings.md#settings)。</span><span class="sxs-lookup"><span data-stu-id="ea319-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="ea319-127">輸入使用方式</span><span class="sxs-lookup"><span data-stu-id="ea319-127">Input usage</span></span>
<span data-ttu-id="ea319-128">在 C# 函式中，您使用在您函式簽章中的具名參數 (例如 `<T> <name>`) 繫結至資料表實體 (或多個實體)。</span><span class="sxs-lookup"><span data-stu-id="ea319-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="ea319-129">其中 `T` 是您要用來還原序列化資料的資料類型，而 `paramName` 是您在 [輸入繫結](#input) 中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="ea319-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="ea319-130">在 Node.js 函式中，您會使用 `context.bindings.<name>` 來存取輸入資料表實體 (或多個實體)。</span><span class="sxs-lookup"><span data-stu-id="ea319-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ea319-131">可以在 Node.js 或 C# 函式中將輸入資料還原序列化。</span><span class="sxs-lookup"><span data-stu-id="ea319-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="ea319-132">還原序列化的物件具有 `RowKey` 和 `PartitionKey` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ea319-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="ea319-133">在 C# 函式中，您也可以繫結至下列任何類型，Functions 的執行階段會嘗試使用該類型還原序列化資料表資料︰</span><span class="sxs-lookup"><span data-stu-id="ea319-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="ea319-134">實作 `ITableEntity` 的任何類型</span><span class="sxs-lookup"><span data-stu-id="ea319-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="ea319-135">輸入範例</span><span class="sxs-lookup"><span data-stu-id="ea319-135">Input sample</span></span>
<span data-ttu-id="ea319-136">假設您有下列 function.json，其使用佇列觸發程序來讀取單一資料表資料列。</span><span class="sxs-lookup"><span data-stu-id="ea319-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="ea319-137">JSON 會指定 `PartitionKey` 
`RowKey`。</span><span class="sxs-lookup"><span data-stu-id="ea319-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="ea319-138">`"rowKey": "{queueTrigger}"` 表示資料列索引鍵來自佇列訊息字串。</span><span class="sxs-lookup"><span data-stu-id="ea319-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

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

<span data-ttu-id="ea319-139">請參閱可讀取單一資料表實體的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="ea319-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="ea319-140">C#</span><span class="sxs-lookup"><span data-stu-id="ea319-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="ea319-141">F#</span><span class="sxs-lookup"><span data-stu-id="ea319-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="ea319-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="ea319-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="ea319-143">C# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="ea319-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="ea319-144">F# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="ea319-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="ea319-145">Node.js 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="ea319-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="ea319-146">儲存體資料表輸出繫結</span><span class="sxs-lookup"><span data-stu-id="ea319-146">Storage table output binding</span></span>
<span data-ttu-id="ea319-147">Azure 儲存體資料表輸出繫結可讓您在函式中將實體寫入儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="ea319-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="ea319-148">函式的儲存體資料表輸出會使用 function.json `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="ea319-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="ea319-149">請注意：</span><span class="sxs-lookup"><span data-stu-id="ea319-149">Note the following:</span></span> 

* <span data-ttu-id="ea319-150">一起使用 `partitionKey` 和 `rowKey` 來寫入單一實體。</span><span class="sxs-lookup"><span data-stu-id="ea319-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="ea319-151">這些屬性是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="ea319-151">These properties are optional.</span></span> <span data-ttu-id="ea319-152">在您的函式程式碼中建立實體物件時，您也可以指定 `PartitionKey` 和 `RowKey`。</span><span class="sxs-lookup"><span data-stu-id="ea319-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="ea319-153">`connection` 必須包含儲存體連接字串的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="ea319-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="ea319-154">在 Azure 入口網站中，當您建立儲存體帳戶或選取一個現有的儲存體帳戶時，[整合] 索引標籤中的標準編輯器可設定此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ea319-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="ea319-155">您也可以[手動進行此應用程式設定](functions-how-to-use-azure-function-app-settings.md#settings)。</span><span class="sxs-lookup"><span data-stu-id="ea319-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="ea319-156">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="ea319-156">Output usage</span></span>
<span data-ttu-id="ea319-157">在 C# 函式中，您使用函式簽章中名為 `out` 的參數 (例如 `out <T> <name>`) 繫結至資料表輸出，其中 `T` 是您想要用來序列化資料的資料類型，而 `paramName` 是您在 [輸出繫結](#output) 中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="ea319-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="ea319-158">在 Node.js 函式中，您會使用 `context.bindings.<name>` 來存取資料表輸出。</span><span class="sxs-lookup"><span data-stu-id="ea319-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ea319-159">您可以在 Node.js 或 C# 函式中將物件序列化。</span><span class="sxs-lookup"><span data-stu-id="ea319-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="ea319-160">在 C# 函式中，您也可以繫結至下列類型︰</span><span class="sxs-lookup"><span data-stu-id="ea319-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="ea319-161">實作 `ITableEntity` 的任何類型</span><span class="sxs-lookup"><span data-stu-id="ea319-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="ea319-162">`ICollector<T>` (可輸出多個實體。</span><span class="sxs-lookup"><span data-stu-id="ea319-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="ea319-163">請參閱[範例](#outcsharp)。)</span><span class="sxs-lookup"><span data-stu-id="ea319-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="ea319-164">`IAsyncCollector<T>` (`ICollector<T>` 的非同步版本)</span><span class="sxs-lookup"><span data-stu-id="ea319-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="ea319-165">`CloudTable` (使用「Azure 儲存體 SDK」。</span><span class="sxs-lookup"><span data-stu-id="ea319-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="ea319-166">請參閱[範例](#readmulti)。)</span><span class="sxs-lookup"><span data-stu-id="ea319-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="ea319-167">輸出範例</span><span class="sxs-lookup"><span data-stu-id="ea319-167">Output sample</span></span>
<span data-ttu-id="ea319-168">下列 *function.json* 和 *run.csx* 範例示範如何在 C# 中撰寫多個資料表實體。</span><span class="sxs-lookup"><span data-stu-id="ea319-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

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

<span data-ttu-id="ea319-169">請參閱可建立多個資料表實體的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="ea319-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="ea319-170">C#</span><span class="sxs-lookup"><span data-stu-id="ea319-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="ea319-171">F#</span><span class="sxs-lookup"><span data-stu-id="ea319-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="ea319-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="ea319-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="ea319-173">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="ea319-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="ea319-174">F# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="ea319-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="ea319-175">Node.js 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="ea319-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="ea319-176">範例：讀取 C# 中的多個資料表實體</span><span class="sxs-lookup"><span data-stu-id="ea319-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="ea319-177">下列「function.json」  和 C# 程式碼範例會讀取佇列訊息中指定的資料分割金鑰的實體。</span><span class="sxs-lookup"><span data-stu-id="ea319-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

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

<span data-ttu-id="ea319-178">C# 程式碼會新增對「Azure 儲存體 SDK」的參考，讓實體類型可以衍生自 `TableEntity`。</span><span class="sxs-lookup"><span data-stu-id="ea319-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ea319-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea319-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

