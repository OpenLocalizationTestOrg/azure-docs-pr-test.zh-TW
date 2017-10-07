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
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="358ae-104">Azure Functions Cosmos DB 繫結</span><span class="sxs-lookup"><span data-stu-id="358ae-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="358ae-105">這篇文章說明如何在 Azure 函式的 tooconfigure 和程式碼 Azure Cosmos DB 繫結。</span><span class="sxs-lookup"><span data-stu-id="358ae-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="358ae-106">Azure Functions 支援 Cosmos DB 的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="358ae-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="358ae-107">如需有關 Cosmos DB 的詳細資訊，請參閱[簡介 tooCosmos DB](../documentdb/documentdb-introduction.md)和[建置 Cosmos DB 主控台應用程式](../documentdb/documentdb-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="358ae-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="358ae-108">DocumentDB API 輸入繫結</span><span class="sxs-lookup"><span data-stu-id="358ae-108">DocumentDB API input binding</span></span>
<span data-ttu-id="358ae-109">hello DocumentDB API 輸入繫結擷取 Cosmos DB 文件，並將其傳遞 toohello 名為的 hello 函式的輸入的參數。</span><span class="sxs-lookup"><span data-stu-id="358ae-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="358ae-110">判斷識別碼 hello 文件以 hello 函式會叫用的 hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="358ae-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="358ae-111">hello DocumentDB API 輸入繫結具有下列屬性中的 hello *function.json*:</span><span class="sxs-lookup"><span data-stu-id="358ae-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="358ae-112">`name`： 使用函式程式碼中的 hello 文件識別名稱</span><span class="sxs-lookup"><span data-stu-id="358ae-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="358ae-113">`type`： 必須設定得 「 documentdb"</span><span class="sxs-lookup"><span data-stu-id="358ae-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="358ae-114">`databaseName`: hello 資料庫包含 hello 文件</span><span class="sxs-lookup"><span data-stu-id="358ae-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="358ae-115">`collectionName`: hello 集合，其中包含 hello 文件</span><span class="sxs-lookup"><span data-stu-id="358ae-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="358ae-116">`id`: hello hello 文件 tooretrieve 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="358ae-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="358ae-117">此屬性支援繫結參數。請參閱[toocustom 輸入的屬性繫結中繫結運算式](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression)hello 本文[Azure 函式的觸發程序和繫結概念](functions-triggers-bindings.md)。</span><span class="sxs-lookup"><span data-stu-id="358ae-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="358ae-118">`sqlQuery`：用來擷取多份文件的 Cosmos DB SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="358ae-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="358ae-119">hello 查詢支援執行階段繫結。</span><span class="sxs-lookup"><span data-stu-id="358ae-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="358ae-120">例如：`SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="358ae-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="358ae-121">`connection`: hello 包含 Cosmos DB 連線字串 hello 應用程式設定名稱</span><span class="sxs-lookup"><span data-stu-id="358ae-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="358ae-122">`direction`： 必須設定得`"in"`。</span><span class="sxs-lookup"><span data-stu-id="358ae-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="358ae-123">hello 屬性`id`和`sqlQuery`無法同時指定。</span><span class="sxs-lookup"><span data-stu-id="358ae-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="358ae-124">如果沒有`id`也`sqlQuery`設定，hello 整個擷取集合。</span><span class="sxs-lookup"><span data-stu-id="358ae-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="358ae-125">使用 DocumentDB API 輸入繫結</span><span class="sxs-lookup"><span data-stu-id="358ae-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="358ae-126">在 C# 和 F # 函式，hello 函式成功，結束時也會自動保存 toohello 透過具名的輸入參數的輸入文件所做的變更。</span><span class="sxs-lookup"><span data-stu-id="358ae-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="358ae-127">在 JavaScript 函數中，不會在函數結束時自動執行更新。</span><span class="sxs-lookup"><span data-stu-id="358ae-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="358ae-128">請改用`context.bindings.<documentName>In`和`context.bindings.<documentName>Out`toomake 更新。</span><span class="sxs-lookup"><span data-stu-id="358ae-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="358ae-129">請參閱 hello [JavaScript 範例](#injavascript)。</span><span class="sxs-lookup"><span data-stu-id="358ae-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="358ae-130">單一文件的輸入範例</span><span class="sxs-lookup"><span data-stu-id="358ae-130">Input sample for single document</span></span>
<span data-ttu-id="358ae-131">假設您有下列 hello DocumentDB API 輸入 hello 中的繫結`bindings`function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="358ae-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="358ae-132">請參閱 hello 特定語言的範例會使用此輸入繫結 tooupdate hello 文件的文字值。</span><span class="sxs-lookup"><span data-stu-id="358ae-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="358ae-133">C#</span><span class="sxs-lookup"><span data-stu-id="358ae-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="358ae-134">F#</span><span class="sxs-lookup"><span data-stu-id="358ae-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="358ae-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="358ae-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="358ae-136">C# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="358ae-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="358ae-137">F# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="358ae-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="358ae-138">這個範例需要`project.json`檔案，指定 hello`FSharp.Interop.Dynamic`和`Dynamitey`NuGet 相依性：</span><span class="sxs-lookup"><span data-stu-id="358ae-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="358ae-139">tooadd`project.json`檔案，請參閱[F # 封裝管理](functions-reference-fsharp.md#package)。</span><span class="sxs-lookup"><span data-stu-id="358ae-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="358ae-140">以 JavaScript 撰寫的輸入範例</span><span class="sxs-lookup"><span data-stu-id="358ae-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="358ae-141">具有多份文件的輸入範例</span><span class="sxs-lookup"><span data-stu-id="358ae-141">Input sample with multiple documents</span></span>

<span data-ttu-id="358ae-142">假設您想 tooretrieve SQL 查詢，所指定的多個文件使用佇列觸發程序 toocustomize hello 查詢參數。</span><span class="sxs-lookup"><span data-stu-id="358ae-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="358ae-143">在此範例中，hello 佇列觸發程序提供的參數`departmentId`。佇列訊息的`{ "departmentId" : "Finance" }`會傳回 hello 財務部門的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="358ae-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="358ae-144">使用中的 hello 下列*function.json*:</span><span class="sxs-lookup"><span data-stu-id="358ae-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="358ae-145">以 C# 撰寫之具有多份文件的輸入範例</span><span class="sxs-lookup"><span data-stu-id="358ae-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="358ae-146">以 JavaScript 撰寫之具有多份文件的輸入範例</span><span class="sxs-lookup"><span data-stu-id="358ae-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="358ae-147"><a id="docdboutput"></a>DocumentDB API 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="358ae-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="358ae-148">hello DocumentDB API 輸出繫結可讓您撰寫新的文件 tooan Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="358ae-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="358ae-149">它有下列屬性中的 hello *function.json*:</span><span class="sxs-lookup"><span data-stu-id="358ae-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="358ae-150">`name`： 識別項在函式程式碼用於 hello 新文件</span><span class="sxs-lookup"><span data-stu-id="358ae-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="358ae-151">`type`： 必須太設定`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="358ae-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="358ae-152">`databaseName`： 包含 hello 集合將會建立新文件 hello hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="358ae-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="358ae-153">`collectionName`: hello hello 新文件將會建立的集合。</span><span class="sxs-lookup"><span data-stu-id="358ae-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="358ae-154">`createIfNotExists`： 布林值 tooindicate 是否會建立 hello 集合，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="358ae-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="358ae-155">hello 預設值是*false*。</span><span class="sxs-lookup"><span data-stu-id="358ae-155">hello default is *false*.</span></span> <span data-ttu-id="358ae-156">hello 原因為新建立的集合，以使用保留輸送量，具有定價含意。</span><span class="sxs-lookup"><span data-stu-id="358ae-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="358ae-157">如需詳細資訊，請瀏覽 hello[定價頁面](https://azure.microsoft.com/pricing/details/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="358ae-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="358ae-158">`connection`: hello 包含 Cosmos DB 連線字串 hello 應用程式設定名稱</span><span class="sxs-lookup"><span data-stu-id="358ae-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="358ae-159">`direction`： 必須太設定`"out"`</span><span class="sxs-lookup"><span data-stu-id="358ae-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="358ae-160">使用 DocumentDB API 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="358ae-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="358ae-161">本節說明如何 toouse DocumentDB API 輸出繫結函式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="358ae-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="358ae-162">當您撰寫 toohello 輸出參數在函數中，預設資料庫中產生新的文件時，以自動產生的 GUID 為 hello 文件識別碼。</span><span class="sxs-lookup"><span data-stu-id="358ae-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="358ae-163">您可以指定 hello 文件識別碼的輸出文件，藉由指定 hello `id` hello 中的 JSON 屬性輸出參數。</span><span class="sxs-lookup"><span data-stu-id="358ae-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="358ae-164">當您指定的現有文件的 hello 識別碼時，則取得 hello 新輸出文件的覆寫。</span><span class="sxs-lookup"><span data-stu-id="358ae-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="358ae-165">toooutput 多份文件，您也可以繫結太`ICollector<T>`或`IAsyncCollector<T>`其中`T`是其中一個支援的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="358ae-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="358ae-166">DocumentDB API 輸出繫結範例</span><span class="sxs-lookup"><span data-stu-id="358ae-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="358ae-167">假設您有下列 hello DocumentDB API 輸出繫結中 hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="358ae-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="358ae-168">而且您擁有 hello 遵循格式中接收 JSON 的佇列的佇列輸入繫結：</span><span class="sxs-lookup"><span data-stu-id="358ae-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="358ae-169">與要 toocreate Cosmos DB 文件以 hello 遵循每一筆記錄的格式：</span><span class="sxs-lookup"><span data-stu-id="358ae-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="358ae-170">請參閱 hello 特定語言的範例會使用此輸出繫結 tooadd 文件 tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="358ae-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="358ae-171">C#</span><span class="sxs-lookup"><span data-stu-id="358ae-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="358ae-172">F#</span><span class="sxs-lookup"><span data-stu-id="358ae-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="358ae-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="358ae-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="358ae-174">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="358ae-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="358ae-175">F# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="358ae-175">Output sample in F#</span></span> #

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

<span data-ttu-id="358ae-176">這個範例需要`project.json`檔案，指定 hello`FSharp.Interop.Dynamic`和`Dynamitey`NuGet 相依性：</span><span class="sxs-lookup"><span data-stu-id="358ae-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="358ae-177">tooadd`project.json`檔案，請參閱[F # 封裝管理](functions-reference-fsharp.md#package)。</span><span class="sxs-lookup"><span data-stu-id="358ae-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="358ae-178">以 JavaScript 撰寫的輸出範例</span><span class="sxs-lookup"><span data-stu-id="358ae-178">Output sample in JavaScript</span></span>

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
