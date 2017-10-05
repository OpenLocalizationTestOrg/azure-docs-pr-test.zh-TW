---
title: "Azure Functions Cosmos DB 繫結 | Microsoft Docs"
description: "了解如何在 Azure Functions 中使用 Azure Cosmos DB 繫結。"
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
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="e0dd3-104">Azure Functions Cosmos DB 繫結</span><span class="sxs-lookup"><span data-stu-id="e0dd3-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e0dd3-105">本文說明如何在 Azure Functions 中設定 Azure Cosmos DB 繫結和撰寫其程式碼。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="e0dd3-106">Azure Functions 支援 Cosmos DB 的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="e0dd3-107">如需 Cosmos DB 的詳細資訊，請參閱 [Cosmos DB 簡介](../documentdb/documentdb-introduction.md)和[建置 Cosmos DB 主控台應用程式](../documentdb/documentdb-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="e0dd3-108">DocumentDB API 輸入繫結</span><span class="sxs-lookup"><span data-stu-id="e0dd3-108">DocumentDB API input binding</span></span>
<span data-ttu-id="e0dd3-109">DocumentDB API 輸入繫結會擷取 Cosmos DB 文件，並將它傳遞給函式的具名輸入參數。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="e0dd3-110">您可以根據叫用該函式的觸發程序來判斷文件識別碼。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="e0dd3-111">DocumentDB API 輸入繫結在 *function.json* 中具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e0dd3-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="e0dd3-112">`name`︰函數程式碼中用於文件的識別碼名稱</span><span class="sxs-lookup"><span data-stu-id="e0dd3-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="e0dd3-113">`type`︰必須設定為 "documentdb"</span><span class="sxs-lookup"><span data-stu-id="e0dd3-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="e0dd3-114">`databaseName`︰包含文件的資料庫</span><span class="sxs-lookup"><span data-stu-id="e0dd3-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="e0dd3-115">`collectionName`︰包含文件的集合</span><span class="sxs-lookup"><span data-stu-id="e0dd3-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="e0dd3-116">`id`︰要擷取之文件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="e0dd3-117">此屬性支援繫結參數；請參閱 [Azure Functions 觸發程序和繫結概念](functions-triggers-bindings.md)一文中的[在繫結運算式中繫結到自訂輸入屬性](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression)。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="e0dd3-118">`sqlQuery`：用來擷取多份文件的 Cosmos DB SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="e0dd3-119">此查詢支援執行階段繫結。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-119">The query supports runtime bindings.</span></span> <span data-ttu-id="e0dd3-120">例如：`SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="e0dd3-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="e0dd3-121">`connection`：包含 Cosmos DB 連接字串的應用程式設定名稱</span><span class="sxs-lookup"><span data-stu-id="e0dd3-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="e0dd3-122">`direction`：必須設定為 `"in"`。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="e0dd3-123">不可同時指定 `id` 和 `sqlQuery`。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="e0dd3-124">如果既未設定 `id` 也未設定 `sqlQuery`，則會擷取整個集合。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="e0dd3-125">使用 DocumentDB API 輸入繫結</span><span class="sxs-lookup"><span data-stu-id="e0dd3-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="e0dd3-126">在 C# 和 F# 函式中，當函式順利結束時，系統會自動保留透過具名輸入參數對輸入文件所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="e0dd3-127">在 JavaScript 函數中，不會在函數結束時自動執行更新。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="e0dd3-128">請改用 `context.bindings.<documentName>In` 和 `context.bindings.<documentName>Out` 來進行更新。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="e0dd3-129">請參閱 [JavaScript 範例](#injavascript)。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="e0dd3-130">單一文件的輸入範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-130">Input sample for single document</span></span>
<span data-ttu-id="e0dd3-131">假設您在 function.json 的 `bindings` 陣列中有下列 DocumentDB API 輸入繫結︰</span><span class="sxs-lookup"><span data-stu-id="e0dd3-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="e0dd3-132">請參閱使用此輸入繫結來更新文件的文字值的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="e0dd3-133">C#</span><span class="sxs-lookup"><span data-stu-id="e0dd3-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="e0dd3-134">F#</span><span class="sxs-lookup"><span data-stu-id="e0dd3-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="e0dd3-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e0dd3-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="e0dd3-136">C# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="e0dd3-137">F# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="e0dd3-138">此範例需要一個指定 `FSharp.Interop.Dynamic` 和 `Dynamitey` NuGet 相依性的 `project.json` 檔案︰</span><span class="sxs-lookup"><span data-stu-id="e0dd3-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="e0dd3-139">若要新增 `project.json` 檔案，請參閱 [F# 封裝管理](functions-reference-fsharp.md#package)。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="e0dd3-140">以 JavaScript 撰寫的輸入範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="e0dd3-141">具有多份文件的輸入範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-141">Input sample with multiple documents</span></span>

<span data-ttu-id="e0dd3-142">假設您想要使用佇列觸發程序來自訂查詢參數，以擷取 SQL 查詢所指定的多份文件。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="e0dd3-143">在此範例中，佇列觸發程序會提供參數 `departmentId`。`{ "departmentId" : "Finance" }` 的佇列訊息會傳回財務部門的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="e0dd3-144">請在 *function.json* 中使用下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="e0dd3-144">Use the following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="e0dd3-145">以 C# 撰寫之具有多份文件的輸入範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="e0dd3-146">以 JavaScript 撰寫之具有多份文件的輸入範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="e0dd3-147"><a id="docdboutput"></a>DocumentDB API 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e0dd3-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="e0dd3-148">DocumentDB API 輸出繫結可讓您將新的文件寫入 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="e0dd3-149">它在 *function.json* 中具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e0dd3-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="e0dd3-150">`name`︰函數程式碼中用於新文件的識別碼</span><span class="sxs-lookup"><span data-stu-id="e0dd3-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="e0dd3-151">`type`：必須設定為 `"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="e0dd3-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="e0dd3-152">`databaseName` ︰包含其中將建立新文件之集合的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="e0dd3-153">`collectionName` ︰其中將建立新文件的集合。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="e0dd3-154">`createIfNotExists`︰一個布林值，用來指出當集合不存在時是否要建立集合。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="e0dd3-155">預設值為 *false*。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-155">The default is *false*.</span></span> <span data-ttu-id="e0dd3-156">因為新集合會使用保留的輸送量建立，其具有價格含意。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="e0dd3-157">如需詳細資訊，請瀏覽 [定價頁面](https://azure.microsoft.com/pricing/details/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="e0dd3-158">`connection`：包含 Cosmos DB 連接字串的應用程式設定名稱</span><span class="sxs-lookup"><span data-stu-id="e0dd3-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="e0dd3-159">`direction`：必須設定為 `"out"`</span><span class="sxs-lookup"><span data-stu-id="e0dd3-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="e0dd3-160">使用 DocumentDB API 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="e0dd3-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="e0dd3-161">本節說明如何在您的函式程式碼中使用您的 DocumentDB API 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="e0dd3-162">在函式中寫入輸出參數時，依預設會在資料庫中產生新文件，使用自動產生的 GUID 做為文件識別碼。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="e0dd3-163">您可以藉由在輸出參數中指定 `id` JSON 屬性來指定輸出文件的文件識別碼。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="e0dd3-164">當您指定現有文件的識別碼時，新的輸出文件會覆寫現有文件。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="e0dd3-165">如果要輸出多個文件，您也可以繫結至 `ICollector<T>` 或 `IAsyncCollector<T>`，`T` 表示其中一種支援的類型。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="e0dd3-166">DocumentDB API 輸出繫結範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="e0dd3-167">假設您在 function.json 的 `bindings` 陣列中有下列 DocumentDB API 輸出繫結︰</span><span class="sxs-lookup"><span data-stu-id="e0dd3-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="e0dd3-168">而且您有可接收 JSON 佇列的佇列輸入繫結，其格式如下︰</span><span class="sxs-lookup"><span data-stu-id="e0dd3-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="e0dd3-169">而且您想要針對每一筆記錄建立下列格式的 Cosmos DB 文件︰</span><span class="sxs-lookup"><span data-stu-id="e0dd3-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="e0dd3-170">請參閱使用此輸出繫結將文件新增至您的資料庫的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="e0dd3-171">C#</span><span class="sxs-lookup"><span data-stu-id="e0dd3-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="e0dd3-172">F#</span><span class="sxs-lookup"><span data-stu-id="e0dd3-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="e0dd3-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e0dd3-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="e0dd3-174">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="e0dd3-175">F# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-175">Output sample in F#</span></span> #

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

<span data-ttu-id="e0dd3-176">此範例需要一個指定 `FSharp.Interop.Dynamic` 和 `Dynamitey` NuGet 相依性的 `project.json` 檔案︰</span><span class="sxs-lookup"><span data-stu-id="e0dd3-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="e0dd3-177">若要新增 `project.json` 檔案，請參閱 [F# 封裝管理](functions-reference-fsharp.md#package)。</span><span class="sxs-lookup"><span data-stu-id="e0dd3-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="e0dd3-178">以 JavaScript 撰寫的輸出範例</span><span class="sxs-lookup"><span data-stu-id="e0dd3-178">Output sample in JavaScript</span></span>

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
