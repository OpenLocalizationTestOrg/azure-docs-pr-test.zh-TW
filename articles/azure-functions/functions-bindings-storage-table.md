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
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="dd991-104">Azure Functions 儲存體資料表繫結</span><span class="sxs-lookup"><span data-stu-id="dd991-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="dd991-105">本文說明如何 tooconfigure 和程式碼的 Azure 儲存體資料表 Azure 函式中的繫結。</span><span class="sxs-lookup"><span data-stu-id="dd991-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="dd991-106">Azure Functions 支援 Azure 儲存體資料表的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="dd991-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="dd991-107">hello 儲存體資料表繫結支援下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd991-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="dd991-108">**讀取 C# 或 Node 函式中的單一資料列** - 設定 `partitionKey` 和 `rowKey`。</span><span class="sxs-lookup"><span data-stu-id="dd991-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="dd991-109">hello`filter`和`take`屬性不適用於在此案例中。</span><span class="sxs-lookup"><span data-stu-id="dd991-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="dd991-110">**讀取的 C# 函式中的多個資料列**-hello 函式執行階段提供`IQueryable<T>`物件繫結 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="dd991-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="dd991-111">類型 `T` 必須衍生自 `TableEntity` 或實作 `ITableEntity`。</span><span class="sxs-lookup"><span data-stu-id="dd991-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="dd991-112">hello `partitionKey`， `rowKey`， `filter`，和`take`屬性不適用於在此案例中，您可以使用 hello`IQueryable`物件 toodo 所需的任何篩選。</span><span class="sxs-lookup"><span data-stu-id="dd991-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="dd991-113">**讀取中節點函式的多個資料列**-設定的 hello`filter`和`take`屬性。</span><span class="sxs-lookup"><span data-stu-id="dd991-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="dd991-114">請勿設定 `partitionKey` 或 `rowKey`。</span><span class="sxs-lookup"><span data-stu-id="dd991-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="dd991-115">**C# 函式中寫入一或多個資料列**-hello 函式執行階段提供`ICollector<T>`或`IAsyncCollector<T>`繫結的 toohello 資料表，其中`T`指定 hello 結構描述要 tooadd 的 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="dd991-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="dd991-116">一般而言，類型 `T` 會衍生自 `TableEntity` 或實作 `ITableEntity`，但不一定如此。</span><span class="sxs-lookup"><span data-stu-id="dd991-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="dd991-117">hello `partitionKey`， `rowKey`， `filter`，和`take`屬性不適用於在此案例中。</span><span class="sxs-lookup"><span data-stu-id="dd991-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="dd991-118">儲存體資料表輸入繫結</span><span class="sxs-lookup"><span data-stu-id="dd991-118">Storage table input binding</span></span>
<span data-ttu-id="dd991-119">hello Azure 儲存體資料表的輸入繫結可讓您 toouse 函式中的儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="dd991-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="dd991-120">hello 儲存資料表輸入的 tooa 函式會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="dd991-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="dd991-121">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="dd991-121">Note hello following:</span></span> 

* <span data-ttu-id="dd991-122">使用`partitionKey`和`rowKey`一起 tooread 單一實體。</span><span class="sxs-lookup"><span data-stu-id="dd991-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="dd991-123">這些屬性是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="dd991-123">These properties are optional.</span></span> 
* <span data-ttu-id="dd991-124">`connection`必須包含 hello 包含儲存體連接字串的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="dd991-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="dd991-125">Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合**您建立儲存體帳戶，或是選取現有的索引標籤會設定此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="dd991-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="dd991-126">您也可以[手動進行此應用程式設定](functions-how-to-use-azure-function-app-settings.md#settings)。</span><span class="sxs-lookup"><span data-stu-id="dd991-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="dd991-127">輸入使用方式</span><span class="sxs-lookup"><span data-stu-id="dd991-127">Input usage</span></span>
<span data-ttu-id="dd991-128">在 C# 函數中，您使用繫結 toohello 輸入資料表實體 （或實體） 具名的參數，在您的函式簽章，like `<T> <name>`。</span><span class="sxs-lookup"><span data-stu-id="dd991-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="dd991-129">其中`T`是 hello 資料類型的 toodeserialize hello 資料分割，以及`paramName`是您在 hello 中指定的 hello 名稱[輸入繫結](#input)。</span><span class="sxs-lookup"><span data-stu-id="dd991-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="dd991-130">Node.js 函式，在您存取 hello 輸入資料表實體 （或實體） 使用`context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="dd991-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="dd991-131">Node.js 或 C# 的函式中可還原序列化 hello 輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="dd991-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="dd991-132">還原序列化的 hello 物件具有`RowKey`和`PartitionKey`屬性。</span><span class="sxs-lookup"><span data-stu-id="dd991-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="dd991-133">在 C# 函數中，您也可以繫結 tooany 的 hello 下列類型，和執行階段會嘗試的 hello 函式太還原序列化 hello 使用該類型的資料表資料：</span><span class="sxs-lookup"><span data-stu-id="dd991-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="dd991-134">實作 `ITableEntity` 的任何類型</span><span class="sxs-lookup"><span data-stu-id="dd991-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="dd991-135">輸入範例</span><span class="sxs-lookup"><span data-stu-id="dd991-135">Input sample</span></span>
<span data-ttu-id="dd991-136">假設您擁有 hello 遵循 function.json，會使用佇列觸發程序 tooread 單一資料表資料列。</span><span class="sxs-lookup"><span data-stu-id="dd991-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="dd991-137">hello JSON 指定`PartitionKey`  
 `RowKey`。</span><span class="sxs-lookup"><span data-stu-id="dd991-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="dd991-138">`"rowKey": "{queueTrigger}"`表示該 hello 資料列索引鍵來自 hello 佇列的訊息字串。</span><span class="sxs-lookup"><span data-stu-id="dd991-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="dd991-139">請參閱 hello 讀取單一資料表實體的特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="dd991-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="dd991-140">C#</span><span class="sxs-lookup"><span data-stu-id="dd991-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="dd991-141">F#</span><span class="sxs-lookup"><span data-stu-id="dd991-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="dd991-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="dd991-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="dd991-143">C# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="dd991-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="dd991-144">F# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="dd991-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="dd991-145">Node.js 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="dd991-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="dd991-146">儲存體資料表輸出繫結</span><span class="sxs-lookup"><span data-stu-id="dd991-146">Storage table output binding</span></span>
<span data-ttu-id="dd991-147">hello Azure 儲存體資料表輸出繫結可讓您 toowrite 實體 tooa 函式中的儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="dd991-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="dd991-148">hello 儲存體資料表輸出的函式使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="dd991-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="dd991-149">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="dd991-149">Note hello following:</span></span> 

* <span data-ttu-id="dd991-150">使用`partitionKey`和`rowKey`一起 toowrite 單一實體。</span><span class="sxs-lookup"><span data-stu-id="dd991-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="dd991-151">這些屬性是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="dd991-151">These properties are optional.</span></span> <span data-ttu-id="dd991-152">您也可以指定`PartitionKey`和`RowKey`當您建立 hello 實體物件函式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="dd991-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="dd991-153">`connection`必須包含 hello 包含儲存體連接字串的應用程式設定名稱。</span><span class="sxs-lookup"><span data-stu-id="dd991-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="dd991-154">Hello Azure 入口網站，在 hello 標準編輯器中 hello**整合**您建立儲存體帳戶，或是選取現有的索引標籤會設定此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="dd991-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="dd991-155">您也可以[手動進行此應用程式設定](functions-how-to-use-azure-function-app-settings.md#settings)。</span><span class="sxs-lookup"><span data-stu-id="dd991-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="dd991-156">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="dd991-156">Output usage</span></span>
<span data-ttu-id="dd991-157">在 C# 函數中，您使用繫結 toohello 資料表輸出名為 hello`out`函式簽章中的參數要`out <T> <name>`，其中`T`是 hello 資料類型的 tooserialize hello 資料分割，和`paramName`是 hello 名稱指定在 hello[輸出繫結](#output)。</span><span class="sxs-lookup"><span data-stu-id="dd991-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="dd991-158">在 Node.js 函數中，您可以存取 hello 資料表輸出使用`context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="dd991-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="dd991-159">您可以在 Node.js 或 C# 函式中將物件序列化。</span><span class="sxs-lookup"><span data-stu-id="dd991-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="dd991-160">在 C# 函數中，您也可以繫結 toohello 下列類型：</span><span class="sxs-lookup"><span data-stu-id="dd991-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="dd991-161">實作 `ITableEntity` 的任何類型</span><span class="sxs-lookup"><span data-stu-id="dd991-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="dd991-162">`ICollector<T>`(toooutput 多個實體。</span><span class="sxs-lookup"><span data-stu-id="dd991-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="dd991-163">請參閱[範例](#outcsharp)。)</span><span class="sxs-lookup"><span data-stu-id="dd991-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="dd991-164">`IAsyncCollector<T>` (`ICollector<T>` 的非同步版本)</span><span class="sxs-lookup"><span data-stu-id="dd991-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="dd991-165">`CloudTable`（使用 hello Azure 儲存體 SDK。</span><span class="sxs-lookup"><span data-stu-id="dd991-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="dd991-166">請參閱[範例](#readmulti)。)</span><span class="sxs-lookup"><span data-stu-id="dd991-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="dd991-167">輸出範例</span><span class="sxs-lookup"><span data-stu-id="dd991-167">Output sample</span></span>
<span data-ttu-id="dd991-168">hello 下列*function.json*和*run.csx*範例會示範如何 toowrite 多個資料表實體。</span><span class="sxs-lookup"><span data-stu-id="dd991-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="dd991-169">請參閱 hello 建立多個資料表實體的特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="dd991-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="dd991-170">C#</span><span class="sxs-lookup"><span data-stu-id="dd991-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="dd991-171">F#</span><span class="sxs-lookup"><span data-stu-id="dd991-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="dd991-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="dd991-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="dd991-173">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="dd991-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="dd991-174">F# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="dd991-174">Output sample in F#</span></span> #
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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="dd991-175">Node.js 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="dd991-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="dd991-176">範例：讀取 C# 中的多個資料表實體</span><span class="sxs-lookup"><span data-stu-id="dd991-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="dd991-177">hello 下列*function.json*和 C# 程式碼範例會讀取 hello 佇列訊息中指定資料分割索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="dd991-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="dd991-178">hello C# 程式碼會將參考 toohello Azure 儲存體 SDK，使得 hello 實體類型可以衍生自`TableEntity`。</span><span class="sxs-lookup"><span data-stu-id="dd991-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dd991-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd991-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

