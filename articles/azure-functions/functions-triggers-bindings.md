---
title: "在 Azure Functions 中使用觸發程序和繫結 | Microsoft Docs"
description: "了解如何在 Azure Functions 中使用觸發程序和繫結，將您的程式碼執行連接到線上事件和雲端服務。"
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
ms.openlocfilehash: cc41debb2523df77be4db05817a4c7ac55604439
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="25201-104">Azure Functions 觸發程序和繫結概念</span><span class="sxs-lookup"><span data-stu-id="25201-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="25201-105">Azure Functions 可讓您撰寫程式碼，以透過「觸發程序」和「繫結」回應 Azure 和其他服務中的事件。</span><span class="sxs-lookup"><span data-stu-id="25201-105">Azure Functions allows you to write code in response to events in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="25201-106">此文章是適用於所有支援之程式設計語言的觸發程序和繫結的概念性概觀。</span><span class="sxs-lookup"><span data-stu-id="25201-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="25201-107">這裡描述所有繫結的通用功能。</span><span class="sxs-lookup"><span data-stu-id="25201-107">Features that are common to all bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="25201-108">概觀</span><span class="sxs-lookup"><span data-stu-id="25201-108">Overview</span></span>

<span data-ttu-id="25201-109">觸發程序和繫結是定義叫用函數的方式與其處理之資料的宣告式方法。</span><span class="sxs-lookup"><span data-stu-id="25201-109">Triggers and bindings are a declarative way to define how a function is invoked and what data it works with.</span></span> <span data-ttu-id="25201-110">「觸發程序」會定義叫用函數的方式。</span><span class="sxs-lookup"><span data-stu-id="25201-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="25201-111">一個函數只能恰有一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="25201-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="25201-112">觸發程序具有相關聯的資料，它通常是觸發函數的承載。</span><span class="sxs-lookup"><span data-stu-id="25201-112">Triggers have associated data, which is usually the payload that triggered the function.</span></span> 

<span data-ttu-id="25201-113">輸入和輸出「繫結」提供從您的程式碼內連線到資料的宣告式方法。</span><span class="sxs-lookup"><span data-stu-id="25201-113">Input and output *bindings* provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="25201-114">類似於觸發程序，您需要在函數組態中指定連接字串和其他屬性。</span><span class="sxs-lookup"><span data-stu-id="25201-114">Similar to triggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="25201-115">繫結是選擇性的，而且一個函數可以有多個輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="25201-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="25201-116">使用觸發程序和繫結，您可以撰寫較泛型的程式碼，而不是以硬式編碼的方式撰寫要互動之服務的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="25201-116">Using triggers and bindings, you can write code that is more generic and does not hardcode the details of the services with which it interacts.</span></span> <span data-ttu-id="25201-117">來自服務的資料會直接成為函數程式碼的輸入值。</span><span class="sxs-lookup"><span data-stu-id="25201-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="25201-118">若要將資料輸出到其他服務 (例如在 Azure 表格儲存體中建立新的資料列)，請使用方法的傳回值。</span><span class="sxs-lookup"><span data-stu-id="25201-118">To output data to another service (such as creating a new row in Azure Table Storage), use the return value of the method.</span></span> <span data-ttu-id="25201-119">或者，如果您需要輸出多個值，請使用協助程式物件。</span><span class="sxs-lookup"><span data-stu-id="25201-119">Or, if you need to output multiple values, use a helper object.</span></span> <span data-ttu-id="25201-120">觸發程序和繫結有 **name** 屬性，它是您在程式碼中用來存取繫結的識別項。</span><span class="sxs-lookup"><span data-stu-id="25201-120">Triggers and bindings have a **name** property, which is an identifier you use in your code to access the binding.</span></span>

<span data-ttu-id="25201-121">您可以在 Azure Functions 入口網站的 [整合] 索引標籤中設定觸發程序和繫結。</span><span class="sxs-lookup"><span data-stu-id="25201-121">You can configure triggers and bindings in the **Integrate** tab in the Azure Functions portal.</span></span> <span data-ttu-id="25201-122">實際上，UI 會修改函數目錄中名稱為 *function.json* 的檔案。</span><span class="sxs-lookup"><span data-stu-id="25201-122">Under the covers, the UI modifies a file called *function.json* file in the function directory.</span></span> <span data-ttu-id="25201-123">您可以變更為 [進階編輯器] 以編輯這個檔案。</span><span class="sxs-lookup"><span data-stu-id="25201-123">You can edit this file by changing to the **Advanced editor**.</span></span>

<span data-ttu-id="25201-124">下表顯示 Azure Functions 支援的觸發程序和繫結。</span><span class="sxs-lookup"><span data-stu-id="25201-124">The following table shows the triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="25201-125">範例︰佇列觸發程序和資料表輸出繫結</span><span class="sxs-lookup"><span data-stu-id="25201-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="25201-126">假設您想要每當新訊息出現在 Azure 佇列儲存體時，就在 Azure 表格儲存體寫入新的資料列。</span><span class="sxs-lookup"><span data-stu-id="25201-126">Suppose you want to write a new row to Azure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="25201-127">此案例可以使用 Azure 佇列觸發程序和資料表輸出繫結來實作。</span><span class="sxs-lookup"><span data-stu-id="25201-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="25201-128">佇列觸發程序需要 [整合] 索引標籤中的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="25201-128">A queue trigger requires the following information in the **Integrate** tab:</span></span>

* <span data-ttu-id="25201-129">包含佇列的儲存體帳戶連接字串之應用程式設定的名稱</span><span class="sxs-lookup"><span data-stu-id="25201-129">The name of the app setting that contains the storage account connection string for the queue</span></span>
* <span data-ttu-id="25201-130">佇列名稱</span><span class="sxs-lookup"><span data-stu-id="25201-130">The queue name</span></span>
* <span data-ttu-id="25201-131">程式碼中讀取佇列訊息內容所需的識別項，例如 `order`。</span><span class="sxs-lookup"><span data-stu-id="25201-131">The identifier in your code to read the contents of the queue message, such as `order`.</span></span>

<span data-ttu-id="25201-132">若要寫入 Azure 表格儲存體，可以使用包含下列詳細資料的輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="25201-132">To write to Azure Table Storage, use an output binding with the following details:</span></span>

* <span data-ttu-id="25201-133">包含資料表的儲存體帳戶連接字串之應用程式設定的名稱</span><span class="sxs-lookup"><span data-stu-id="25201-133">The name of the app setting that contains the storage account connection string for the table</span></span>
* <span data-ttu-id="25201-134">資料表名稱</span><span class="sxs-lookup"><span data-stu-id="25201-134">The table name</span></span>
* <span data-ttu-id="25201-135">程式碼中建立輸出項目的識別項，或來自函數的傳回值。</span><span class="sxs-lookup"><span data-stu-id="25201-135">The identifier in your code to create output items, or the return value from the function.</span></span>

<span data-ttu-id="25201-136">繫結將應用程式設定用於連接字串，以強制遵循 *function.json* 不包含服務祕密的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="25201-136">Bindings use app settings for connection strings to enforce the best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="25201-137">然後，在程式碼中使用提供的識別項來與 Azure 儲存體整合。</span><span class="sxs-lookup"><span data-stu-id="25201-137">Then, use the identifiers you provided to integrate with Azure Storage in your code.</span></span>

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The method return value creates a new row in Table Storage
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
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
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

<span data-ttu-id="25201-138">以下是對應上述程式碼的 *function.json*。</span><span class="sxs-lookup"><span data-stu-id="25201-138">Here is the *function.json* that corresponds to the preceding code.</span></span> <span data-ttu-id="25201-139">請注意，無論函數實作的語言為何，仍可以使用相同的設定。</span><span class="sxs-lookup"><span data-stu-id="25201-139">Note that the same configuration can be used, regardless of the language of the function implementation.</span></span>

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
<span data-ttu-id="25201-140">若要在 Azure 入口網站中檢視及編輯 *function.json* 的內容，請按一下函數的 [整合] 索引標籤上的 [進階編輯器] 選項。</span><span class="sxs-lookup"><span data-stu-id="25201-140">To view and edit the contents of *function.json* in the Azure portal, click the **Advanced editor** option on the **Integrate** tab of your function.</span></span>

<span data-ttu-id="25201-141">如需程式碼範例及整合 Azure 儲存體的詳細資訊，請參閱 [Azure 儲存體的 Azure Functions 觸發程序和繫結](functions-bindings-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="25201-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="25201-142">繫結方向</span><span class="sxs-lookup"><span data-stu-id="25201-142">Binding direction</span></span>

<span data-ttu-id="25201-143">所有觸發程序和繫結都具有 `direction` 屬性：</span><span class="sxs-lookup"><span data-stu-id="25201-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="25201-144">對於觸發程序，方向一律為 `in`</span><span class="sxs-lookup"><span data-stu-id="25201-144">For triggers, the direction is always `in`</span></span>
- <span data-ttu-id="25201-145">輸入和輸出繫結使用 `in` 和 `out`</span><span class="sxs-lookup"><span data-stu-id="25201-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="25201-146">某些繫結支援特殊方向 `inout`。</span><span class="sxs-lookup"><span data-stu-id="25201-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="25201-147">如果您使用 `inout`，則 [整合] 索引標籤中只有 [進階編輯器] 可供使用。</span><span class="sxs-lookup"><span data-stu-id="25201-147">If you use `inout`, only the **Advanced editor** is available in the **Integrate** tab.</span></span>

## <a name="using-the-function-return-type-to-return-a-single-output"></a><span data-ttu-id="25201-148">使用函數傳回類型來傳回單一輸出</span><span class="sxs-lookup"><span data-stu-id="25201-148">Using the function return type to return a single output</span></span>

<span data-ttu-id="25201-149">上述範例顯示如何使用函數傳回值，來提供輸出值給繫結，方法是使用特殊名稱參數 `$return`</span><span class="sxs-lookup"><span data-stu-id="25201-149">The preceding example shows how to use the function return value to provide output to a binding, which is achieved by using the special name parameter `$return`.</span></span> <span data-ttu-id="25201-150">(這只支援有傳回值的語言，例如 C#、JavaScript 和 F#)。如果函數有多個輸出繫結，請只將 `$return` 用於其中一個輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="25201-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of the output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="25201-151">下列範例顯示如何在 C#、JavaScript 和 F# 中搭配輸出繫結使用傳回類型。</span><span class="sxs-lookup"><span data-stu-id="25201-151">The examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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
// JavaScript: return a value in the second parameter to context.done
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

## <a name="binding-datatype-property"></a><span data-ttu-id="25201-152">繫結 dataType 屬性</span><span class="sxs-lookup"><span data-stu-id="25201-152">Binding dataType property</span></span>

<span data-ttu-id="25201-153">在.NET 中會使用類型定義輸入資料的資料類型。</span><span class="sxs-lookup"><span data-stu-id="25201-153">In .NET, use the types to define the data type for input data.</span></span> <span data-ttu-id="25201-154">例如，使用 `string` 繫結至要以二進位格式讀取之佇列觸發程序和位元組陣列的文字。</span><span class="sxs-lookup"><span data-stu-id="25201-154">For instance, use `string` to bind to the text of a queue trigger and a byte array to read as binary.</span></span>

<span data-ttu-id="25201-155">對於 JavaScript 等具有動態類型的語言，則會在繫結定義中使用 `dataType` 屬性。</span><span class="sxs-lookup"><span data-stu-id="25201-155">For languages that are dynamically typed such as JavaScript, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="25201-156">例如，若要以二進位格式讀取 HTTP 要求的內容，請使用類別 `binary`：</span><span class="sxs-lookup"><span data-stu-id="25201-156">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="25201-157">`dataType` 也另具有 `stream` 和 `string` 兩種選項。</span><span class="sxs-lookup"><span data-stu-id="25201-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="25201-158">解析應用程式設定</span><span class="sxs-lookup"><span data-stu-id="25201-158">Resolving app settings</span></span>
<span data-ttu-id="25201-159">為了遵循最佳做法，祕密和連接字串應使用應用程式設定來管理，而不是使用組態檔。</span><span class="sxs-lookup"><span data-stu-id="25201-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="25201-160">這會限制對這些祕密的存取，並保護儲存在公用原始檔控制存放庫的 *function.json*。</span><span class="sxs-lookup"><span data-stu-id="25201-160">This limits access to these secrets and makes it safe to store *function.json* in a public source control repository.</span></span>

<span data-ttu-id="25201-161">當您想要根據環境來變更設定時，應用程式設定也很有用。</span><span class="sxs-lookup"><span data-stu-id="25201-161">App settings are also useful whenever you want to change configuration based on the environment.</span></span> <span data-ttu-id="25201-162">例如，在測試環境中，您可能會想要監視不同佇列或 Blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="25201-162">For example, in a test environment, you may want to monitor a different queue or blob storage container.</span></span>

<span data-ttu-id="25201-163">只要某個值是以百分比符號括住 (例如 `%MyAppSetting%`)，就會解析應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="25201-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="25201-164">請注意，觸發程序和繫結的 `connection` 屬性是特殊案例，且會自動將值解析為應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="25201-164">Note that the `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="25201-165">下列範例是使用應用程式設定 `%input-queue-name%` 來定義要觸發之佇列的佇列觸發程序。</span><span class="sxs-lookup"><span data-stu-id="25201-165">The following example is a queue trigger that uses an app setting `%input-queue-name%` to define the queue to trigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="25201-166">觸發程序中繼資料屬性</span><span class="sxs-lookup"><span data-stu-id="25201-166">Trigger metadata properties</span></span>

<span data-ttu-id="25201-167">除了觸發程序提供的資料承載 (例如觸發函數的佇列訊息) 之外，許多觸發程序都提供額外的中繼資料值。</span><span class="sxs-lookup"><span data-stu-id="25201-167">In addition to the data payload provided by a trigger (such as the queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="25201-168">這些值可以在 C# 和 F# 中作為輸入參數使用，或在 JavaScript 中做為 `context.bindings` 物件上的屬性使用。</span><span class="sxs-lookup"><span data-stu-id="25201-168">These values can be used as input parameters in C# and F# or properties on the `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="25201-169">例如，佇列觸發程序支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="25201-169">For example, a queue trigger supports the following properties:</span></span>

* <span data-ttu-id="25201-170">QueueTrigger - 如果是有效字串，便觸發訊息內容</span><span class="sxs-lookup"><span data-stu-id="25201-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="25201-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="25201-171">DequeueCount</span></span>
* <span data-ttu-id="25201-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="25201-172">ExpirationTime</span></span>
* <span data-ttu-id="25201-173">識別碼</span><span class="sxs-lookup"><span data-stu-id="25201-173">Id</span></span>
* <span data-ttu-id="25201-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="25201-174">InsertionTime</span></span>
* <span data-ttu-id="25201-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="25201-175">NextVisibleTime</span></span>
* <span data-ttu-id="25201-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="25201-176">PopReceipt</span></span>

<span data-ttu-id="25201-177">在對應的參考主題中，會描述每個觸發程序之中繼資料屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="25201-177">Details of metadata properties for each trigger are described in the corresponding reference topic.</span></span> <span data-ttu-id="25201-178">您也可以在入口網站的 [整合] 索引標籤中，繫結設定區域之下的 [文件] 區段取得文件。</span><span class="sxs-lookup"><span data-stu-id="25201-178">Documentation is also available in the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.</span></span>  

<span data-ttu-id="25201-179">例如，因為 Blob 觸發程序會有一些延遲，所以您可以使用佇列觸發程序來執行您的函數 (請參閱 [Blob 儲存體觸發程序](functions-bindings-storage-blob.md#storage-blob-trigger)。</span><span class="sxs-lookup"><span data-stu-id="25201-179">For example, since blob triggers have some delays, you can use a queue trigger to run your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="25201-180">佇列訊息會包含要在其上觸發的 Blob 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="25201-180">The queue message would contain the blob filename to trigger on.</span></span> <span data-ttu-id="25201-181">使用 `queueTrigger` 中繼資料屬性，您只要在設定中就能指定此行為，而不需在程式碼中指定。</span><span class="sxs-lookup"><span data-stu-id="25201-181">Using the `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="25201-182">您也可以將來自觸發程序的中繼資料屬性用於其他繫結中的「繫結運算式」，如下節所述。</span><span class="sxs-lookup"><span data-stu-id="25201-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in the following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="25201-183">繫結運算式和模式</span><span class="sxs-lookup"><span data-stu-id="25201-183">Binding expressions and patterns</span></span>

<span data-ttu-id="25201-184">觸發程序和繫結其中一個最強大的功能就是「繫結運算式」。</span><span class="sxs-lookup"><span data-stu-id="25201-184">One of the most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="25201-185">在繫結中，您可以定義模式運算式，並將它用於其他繫結或您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="25201-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="25201-186">觸發程序中繼資料也可以用於繫結運算式，如上一節中的範例所示。</span><span class="sxs-lookup"><span data-stu-id="25201-186">Trigger metadata can also be used in binding expressions, as show in the sample in the preceding section.</span></span>

<span data-ttu-id="25201-187">例如，當您想要調整特定 Blob 儲存體容器中的影像大小時，就如同 [新函數] 頁面中的 [Image Resizer] \(影像大小重新調整器) 範本。</span><span class="sxs-lookup"><span data-stu-id="25201-187">For example, suppose you want to resize images in particular blob storage container, similar to the **Image Resizer** template in the **New Function** page.</span></span> <span data-ttu-id="25201-188">移至 [新函數] -> [語言 C#] -> [案例範例] -> [ImageResizer-CSharp]。</span><span class="sxs-lookup"><span data-stu-id="25201-188">Go to **New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="25201-189">以下是 *function.json* 定義：</span><span class="sxs-lookup"><span data-stu-id="25201-189">Here is the *function.json* definition:</span></span>

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

<span data-ttu-id="25201-190">請注意，`filename` 參數用於 Blob 觸發程序定義以及 Blob 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="25201-190">Notice that the `filename` parameter is used in both the blob trigger definition as well as the blob output binding.</span></span> <span data-ttu-id="25201-191">這個參數也可以用於函數程式碼。</span><span class="sxs-lookup"><span data-stu-id="25201-191">This parameter can also be used in function code.</span></span>

```csharp
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a><span data-ttu-id="25201-192">隨機 GUID</span><span class="sxs-lookup"><span data-stu-id="25201-192">Random GUIDs</span></span>
<span data-ttu-id="25201-193">Azure Functions 透過 `{rand-guid}` 繫結運算式，提供在繫結中產生 GUID 的便利語法。</span><span class="sxs-lookup"><span data-stu-id="25201-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through the `{rand-guid}` binding expression.</span></span> <span data-ttu-id="25201-194">下列範例使用此語法產生唯一的 Blob 名稱：</span><span class="sxs-lookup"><span data-stu-id="25201-194">The following example uses this to generate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="25201-195">目前時間</span><span class="sxs-lookup"><span data-stu-id="25201-195">Current time</span></span>

<span data-ttu-id="25201-196">您可以使用繫結運算式 `DateTime`，系統會將其解析為 `DateTime.UtcNow`。</span><span class="sxs-lookup"><span data-stu-id="25201-196">You can use the binding expression `DateTime`, which resolves to `DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-to-custom-input-properties-in-a-binding-expression"></a><span data-ttu-id="25201-197">在繫結運算式中繫結到自訂輸入屬性</span><span class="sxs-lookup"><span data-stu-id="25201-197">Bind to custom input properties in a binding expression</span></span>

<span data-ttu-id="25201-198">繫結運算式也可以參考在其觸發程序承載中定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="25201-198">Binding expressions can also reference properties that are defined in the trigger payload itself.</span></span> <span data-ttu-id="25201-199">例如，您可能想要從在 Webhook 中提供的檔案名稱動態地繫結到 Blob 儲存體檔案。</span><span class="sxs-lookup"><span data-stu-id="25201-199">For example, you may want to dynamically bind to a blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="25201-200">例如，下列 *function.json* 使用來自觸發程序承載且稱為 `BlobName` 的屬性：</span><span class="sxs-lookup"><span data-stu-id="25201-200">For example, the following *function.json* uses a property called `BlobName` from the trigger payload:</span></span>

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

<span data-ttu-id="25201-201">若要在 C# 和 F# 中完成此動作，您必須定義一個 POCO，以定義將在觸發程序承載中還原序列化的欄位。</span><span class="sxs-lookup"><span data-stu-id="25201-201">To accomplish this in C# and F#, you must define a POCO that defines the fields that will be deserialized in the trigger payload.</span></span>

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

<span data-ttu-id="25201-202">在 JavaScript 中，會自動執行 JSON 還原序列化，且您可以直接使用該屬性。</span><span class="sxs-lookup"><span data-stu-id="25201-202">In JavaScript, JSON deserialization is automatically performed and you can use the properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="25201-203">在執行階段設定繫結資料</span><span class="sxs-lookup"><span data-stu-id="25201-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="25201-204">在 C# 和其他 .NET 語言中，您可以使用相對於 function.json 中宣告式繫結的命令式繫結模式。</span><span class="sxs-lookup"><span data-stu-id="25201-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in *function.json*.</span></span> <span data-ttu-id="25201-205">當繫結參數需要在執行階段而不是設計階段中計算時，命令式繫結非常有用。</span><span class="sxs-lookup"><span data-stu-id="25201-205">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="25201-206">若要深入了解，請參閱 C# 開發人員參考中的[在執行階段透過命令式繫結進行繫結](functions-reference-csharp.md#imperative-bindings)。</span><span class="sxs-lookup"><span data-stu-id="25201-206">To learn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in the C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25201-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="25201-207">Next steps</span></span>
<span data-ttu-id="25201-208">如需特定繫結的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="25201-208">For more information on a specific binding, see the following articles:</span></span>

- [<span data-ttu-id="25201-209">HTTP 和 Webhook</span><span class="sxs-lookup"><span data-stu-id="25201-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="25201-210">計時器</span><span class="sxs-lookup"><span data-stu-id="25201-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="25201-211">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="25201-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="25201-212">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="25201-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="25201-213">資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="25201-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="25201-214">事件中樞</span><span class="sxs-lookup"><span data-stu-id="25201-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="25201-215">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="25201-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="25201-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="25201-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="25201-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="25201-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="25201-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="25201-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="25201-219">通知中樞</span><span class="sxs-lookup"><span data-stu-id="25201-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="25201-220">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="25201-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="25201-221">外部檔案</span><span class="sxs-lookup"><span data-stu-id="25201-221">External file</span></span>](functions-bindings-external-file.md)
