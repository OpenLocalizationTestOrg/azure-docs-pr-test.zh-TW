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
# <a name="azure-functions-triggers-and-bindings-concepts"></a><span data-ttu-id="9f32f-104">Azure Functions 觸發程序和繫結概念</span><span class="sxs-lookup"><span data-stu-id="9f32f-104">Azure Functions triggers and bindings concepts</span></span>
<span data-ttu-id="9f32f-105">Azure 的函式可讓您在 Azure 及其他服務的回應 tooevents toowrite 程式碼透過*觸發程序*和*繫結*。</span><span class="sxs-lookup"><span data-stu-id="9f32f-105">Azure Functions allows you toowrite code in response tooevents in Azure and other services, through *triggers* and *bindings*.</span></span> <span data-ttu-id="9f32f-106">此文章是適用於所有支援之程式設計語言的觸發程序和繫結的概念性概觀。</span><span class="sxs-lookup"><span data-stu-id="9f32f-106">This article is a conceptual overview of triggers and bindings for all supported programming languages.</span></span> <span data-ttu-id="9f32f-107">一般 tooall 繫結的功能為此處所述。</span><span class="sxs-lookup"><span data-stu-id="9f32f-107">Features that are common tooall bindings are described here.</span></span>

## <a name="overview"></a><span data-ttu-id="9f32f-108">概觀</span><span class="sxs-lookup"><span data-stu-id="9f32f-108">Overview</span></span>

<span data-ttu-id="9f32f-109">觸發程序和繫結所宣告的方式來 toodefine 函式如何叫用和哪些資料可搭配。</span><span class="sxs-lookup"><span data-stu-id="9f32f-109">Triggers and bindings are a declarative way toodefine how a function is invoked and what data it works with.</span></span> <span data-ttu-id="9f32f-110">「觸發程序」會定義叫用函數的方式。</span><span class="sxs-lookup"><span data-stu-id="9f32f-110">A *trigger* defines how a function is invoked.</span></span> <span data-ttu-id="9f32f-111">一個函數只能恰有一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="9f32f-111">A function must have exactly one trigger.</span></span> <span data-ttu-id="9f32f-112">觸發程序擁有相關資料，通常是觸發 hello 函式的 hello 裝載。</span><span class="sxs-lookup"><span data-stu-id="9f32f-112">Triggers have associated data, which is usually hello payload that triggered hello function.</span></span> 

<span data-ttu-id="9f32f-113">輸入和輸出*繫結*提供宣告式方式 tooconnect toodata 從您的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="9f32f-113">Input and output *bindings* provide a declarative way tooconnect toodata from within your code.</span></span> <span data-ttu-id="9f32f-114">類似 tootriggers，連接字串和其他屬性中指定函式設定。</span><span class="sxs-lookup"><span data-stu-id="9f32f-114">Similar tootriggers, you specify connection strings and other properties in your function configuration.</span></span> <span data-ttu-id="9f32f-115">繫結是選擇性的，而且一個函數可以有多個輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="9f32f-115">Bindings are optional and a function can have multiple input and output bindings.</span></span> 

<span data-ttu-id="9f32f-116">使用觸發程序和繫結，您可以撰寫程式碼更泛用，不會硬 hello 服務與它互動的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9f32f-116">Using triggers and bindings, you can write code that is more generic and does not hardcode hello details of hello services with which it interacts.</span></span> <span data-ttu-id="9f32f-117">來自服務的資料會直接成為函數程式碼的輸入值。</span><span class="sxs-lookup"><span data-stu-id="9f32f-117">Data coming from services simply become input values for your function code.</span></span> <span data-ttu-id="9f32f-118">toooutput 資料 tooanother 服務 （例如建立新的資料列中 Azure 資料表儲存體），使用 hello hello 方法傳回值。</span><span class="sxs-lookup"><span data-stu-id="9f32f-118">toooutput data tooanother service (such as creating a new row in Azure Table Storage), use hello return value of hello method.</span></span> <span data-ttu-id="9f32f-119">或者，如果您需要 toooutput 多個值時，使用協助程式物件。</span><span class="sxs-lookup"><span data-stu-id="9f32f-119">Or, if you need toooutput multiple values, use a helper object.</span></span> <span data-ttu-id="9f32f-120">觸發程序和繫結有**名稱**屬性，這是您在程式碼 tooaccess hello 繫結中使用的識別項。</span><span class="sxs-lookup"><span data-stu-id="9f32f-120">Triggers and bindings have a **name** property, which is an identifier you use in your code tooaccess hello binding.</span></span>

<span data-ttu-id="9f32f-121">您可以設定觸發程序和繫結中 hello**整合**hello Azure 函式的入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9f32f-121">You can configure triggers and bindings in hello **Integrate** tab in hello Azure Functions portal.</span></span> <span data-ttu-id="9f32f-122">Hello 幕後 hello UI 修改檔案，稱為*function.json* hello 函式的目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="9f32f-122">Under hello covers, hello UI modifies a file called *function.json* file in hello function directory.</span></span> <span data-ttu-id="9f32f-123">您可以編輯此檔案，藉由變更 toohello**進階的編輯器**。</span><span class="sxs-lookup"><span data-stu-id="9f32f-123">You can edit this file by changing toohello **Advanced editor**.</span></span>

<span data-ttu-id="9f32f-124">hello 下表顯示 hello 觸發程序和支援的 Azure 函式繫結。</span><span class="sxs-lookup"><span data-stu-id="9f32f-124">hello following table shows hello triggers and bindings that are supported with Azure Functions.</span></span> 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a><span data-ttu-id="9f32f-125">範例︰佇列觸發程序和資料表輸出繫結</span><span class="sxs-lookup"><span data-stu-id="9f32f-125">Example: queue trigger and table output binding</span></span>

<span data-ttu-id="9f32f-126">假設您想 toowrite 新的資料列 tooAzure 資料表儲存體，每當新的訊息會出現在 Azure 佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="9f32f-126">Suppose you want toowrite a new row tooAzure Table Storage whenever a new message appears in Azure Queue Storage.</span></span> <span data-ttu-id="9f32f-127">此案例可以使用 Azure 佇列觸發程序和資料表輸出繫結來實作。</span><span class="sxs-lookup"><span data-stu-id="9f32f-127">This scenario can be implemented using an Azure Queue trigger and a Table output binding.</span></span> 

<span data-ttu-id="9f32f-128">佇列觸發程序需要下列資訊在 hello hello**整合** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="9f32f-128">A queue trigger requires hello following information in hello **Integrate** tab:</span></span>

* <span data-ttu-id="9f32f-129">hello 包含 hello hello 佇列儲存體帳戶連接字串的 hello 應用程式設定名稱</span><span class="sxs-lookup"><span data-stu-id="9f32f-129">hello name of hello app setting that contains hello storage account connection string for hello queue</span></span>
* <span data-ttu-id="9f32f-130">hello 佇列名稱</span><span class="sxs-lookup"><span data-stu-id="9f32f-130">hello queue name</span></span>
* <span data-ttu-id="9f32f-131">hello hello 佇列訊息，您的程式碼 tooread hello 內容中的識別項，例如`order`。</span><span class="sxs-lookup"><span data-stu-id="9f32f-131">hello identifier in your code tooread hello contents of hello queue message, such as `order`.</span></span>

<span data-ttu-id="9f32f-132">toowrite tooAzure 資料表儲存體，使用下列詳細資料的 hello 的輸出繫結：</span><span class="sxs-lookup"><span data-stu-id="9f32f-132">toowrite tooAzure Table Storage, use an output binding with hello following details:</span></span>

* <span data-ttu-id="9f32f-133">hello 包含 hello hello 資料表儲存體帳戶連接字串的 hello 應用程式設定名稱</span><span class="sxs-lookup"><span data-stu-id="9f32f-133">hello name of hello app setting that contains hello storage account connection string for hello table</span></span>
* <span data-ttu-id="9f32f-134">hello 資料表名稱</span><span class="sxs-lookup"><span data-stu-id="9f32f-134">hello table name</span></span>
* <span data-ttu-id="9f32f-135">在您的程式碼 toocreate hello 識別碼輸出項目或 hello hello 函式傳回值。</span><span class="sxs-lookup"><span data-stu-id="9f32f-135">hello identifier in your code toocreate output items, or hello return value from hello function.</span></span>

<span data-ttu-id="9f32f-136">繫結會使用應用程式設定的連接字串 tooenforce hello 最佳練習， *function.json*不包含服務密碼。</span><span class="sxs-lookup"><span data-stu-id="9f32f-136">Bindings use app settings for connection strings tooenforce hello best practice that *function.json* does not contain service secrets.</span></span>

<span data-ttu-id="9f32f-137">然後，使用您在程式碼中提供與 Azure 儲存體 toointegrate hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="9f32f-137">Then, use hello identifiers you provided toointegrate with Azure Storage in your code.</span></span>

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

<span data-ttu-id="9f32f-138">以下是 hello *function.json*對應 toohello 前面程式碼。</span><span class="sxs-lookup"><span data-stu-id="9f32f-138">Here is hello *function.json* that corresponds toohello preceding code.</span></span> <span data-ttu-id="9f32f-139">請注意該相同的設定可以使用，不論 hello 語言的 hello 函式實作的 hello。</span><span class="sxs-lookup"><span data-stu-id="9f32f-139">Note that hello same configuration can be used, regardless of hello language of hello function implementation.</span></span>

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
<span data-ttu-id="9f32f-140">tooview 和編輯的 hello 內容*function.json*在 hello Azure 入口網站，按一下 hello**進階的編輯器**選項 hello**整合**函式的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9f32f-140">tooview and edit hello contents of *function.json* in hello Azure portal, click hello **Advanced editor** option on hello **Integrate** tab of your function.</span></span>

<span data-ttu-id="9f32f-141">如需程式碼範例及整合 Azure 儲存體的詳細資訊，請參閱 [Azure 儲存體的 Azure Functions 觸發程序和繫結](functions-bindings-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="9f32f-141">For more code examples and details on integrating with Azure Storage, see [Azure Functions triggers and bindings for Azure Storage](functions-bindings-storage.md).</span></span>

### <a name="binding-direction"></a><span data-ttu-id="9f32f-142">繫結方向</span><span class="sxs-lookup"><span data-stu-id="9f32f-142">Binding direction</span></span>

<span data-ttu-id="9f32f-143">所有觸發程序和繫結都具有 `direction` 屬性：</span><span class="sxs-lookup"><span data-stu-id="9f32f-143">All triggers and bindings have a `direction` property:</span></span>

- <span data-ttu-id="9f32f-144">觸發程序，hello 方向一律是`in`</span><span class="sxs-lookup"><span data-stu-id="9f32f-144">For triggers, hello direction is always `in`</span></span>
- <span data-ttu-id="9f32f-145">輸入和輸出繫結使用 `in` 和 `out`</span><span class="sxs-lookup"><span data-stu-id="9f32f-145">Input and output bindings use `in` and `out`</span></span>
- <span data-ttu-id="9f32f-146">某些繫結支援特殊方向 `inout`。</span><span class="sxs-lookup"><span data-stu-id="9f32f-146">Some bindings support a special direction `inout`.</span></span> <span data-ttu-id="9f32f-147">如果您使用`inout`，只有 hello**進階的編輯器**位於 hello**整合** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9f32f-147">If you use `inout`, only hello **Advanced editor** is available in hello **Integrate** tab.</span></span>

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a><span data-ttu-id="9f32f-148">使用 hello 函式傳回型別 tooreturn 單一輸出</span><span class="sxs-lookup"><span data-stu-id="9f32f-148">Using hello function return type tooreturn a single output</span></span>

<span data-ttu-id="9f32f-149">hello 前面的範例顯示如何 toouse hello 函式傳回值 tooprovide 輸出 tooa 繫結，這利用 hello 特殊的 name 參數來達成`$return`。</span><span class="sxs-lookup"><span data-stu-id="9f32f-149">hello preceding example shows how toouse hello function return value tooprovide output tooa binding, which is achieved by using hello special name parameter `$return`.</span></span> <span data-ttu-id="9f32f-150">(這只支援有傳回值的語言，例如 C#、JavaScript 和 F#)。如果函式具有多個輸出繫結，使用`$return`只為其中一個 hello 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="9f32f-150">(This is only supported in languages that have a return value, such as C#, JavaScript, and F#.) If a function has multiple output bindings, use `$return` for only one of hello output bindings.</span></span> 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

<span data-ttu-id="9f32f-151">以下顯示 hello 範例如何傳回類型 C#、 JavaScript 和 F # 中的輸出繫結搭配使用。</span><span class="sxs-lookup"><span data-stu-id="9f32f-151">hello examples below show how return types are used with output bindings in C#, JavaScript, and F#.</span></span>

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

## <a name="binding-datatype-property"></a><span data-ttu-id="9f32f-152">繫結 dataType 屬性</span><span class="sxs-lookup"><span data-stu-id="9f32f-152">Binding dataType property</span></span>

<span data-ttu-id="9f32f-153">在.NET 中，用於輸入資料中的 hello 類型 toodefine hello 資料型別。</span><span class="sxs-lookup"><span data-stu-id="9f32f-153">In .NET, use hello types toodefine hello data type for input data.</span></span> <span data-ttu-id="9f32f-154">例如，使用`string`佇列觸發程序，以二進位位元組陣列 tooread toobind toohello 文字。</span><span class="sxs-lookup"><span data-stu-id="9f32f-154">For instance, use `string` toobind toohello text of a queue trigger and a byte array tooread as binary.</span></span>

<span data-ttu-id="9f32f-155">對於 JavaScript 等動態具類型的語言，使用 hello `dataType` hello 繫結的定義中的屬性。</span><span class="sxs-lookup"><span data-stu-id="9f32f-155">For languages that are dynamically typed such as JavaScript, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="9f32f-156">例如，tooread hello 內容的 HTTP 要求以二進位格式，請使用 hello 類型`binary`:</span><span class="sxs-lookup"><span data-stu-id="9f32f-156">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="9f32f-157">`dataType` 也另具有 `stream` 和 `string` 兩種選項。</span><span class="sxs-lookup"><span data-stu-id="9f32f-157">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="resolving-app-settings"></a><span data-ttu-id="9f32f-158">解析應用程式設定</span><span class="sxs-lookup"><span data-stu-id="9f32f-158">Resolving app settings</span></span>
<span data-ttu-id="9f32f-159">為了遵循最佳做法，祕密和連接字串應使用應用程式設定來管理，而不是使用組態檔。</span><span class="sxs-lookup"><span data-stu-id="9f32f-159">As a best practice, secrets and connection strings should be managed using app settings, rather than configuration files.</span></span> <span data-ttu-id="9f32f-160">這會限制存取 toothese 機密資料，並使其安全 toostore *function.json*公用的原始檔控制儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="9f32f-160">This limits access toothese secrets and makes it safe toostore *function.json* in a public source control repository.</span></span>

<span data-ttu-id="9f32f-161">每當您想要根據 hello 環境 toochange 設定時，應用程式設定也很有用。</span><span class="sxs-lookup"><span data-stu-id="9f32f-161">App settings are also useful whenever you want toochange configuration based on hello environment.</span></span> <span data-ttu-id="9f32f-162">例如，在測試環境中，您可能想 toomonitor 不同的佇列或 blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="9f32f-162">For example, in a test environment, you may want toomonitor a different queue or blob storage container.</span></span>

<span data-ttu-id="9f32f-163">只要某個值是以百分比符號括住 (例如 `%MyAppSetting%`)，就會解析應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="9f32f-163">App settings are resolved whenever a value is enclosed in percent signs, such as `%MyAppSetting%`.</span></span> <span data-ttu-id="9f32f-164">請注意該 hello`connection`的觸發程序和繫結的屬性是特殊案例，並自動解析為應用程式設定的值。</span><span class="sxs-lookup"><span data-stu-id="9f32f-164">Note that hello `connection` property of triggers and bindings is a special case and automatically resolves values as app settings.</span></span> 

<span data-ttu-id="9f32f-165">hello 下列範例會使用應用程式設定的佇列觸發程序`%input-queue-name%`toodefine hello 佇列 tootrigger 上的。</span><span class="sxs-lookup"><span data-stu-id="9f32f-165">hello following example is a queue trigger that uses an app setting `%input-queue-name%` toodefine hello queue tootrigger on.</span></span>

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

## <a name="trigger-metadata-properties"></a><span data-ttu-id="9f32f-166">觸發程序中繼資料屬性</span><span class="sxs-lookup"><span data-stu-id="9f32f-166">Trigger metadata properties</span></span>

<span data-ttu-id="9f32f-167">在加法 toohello 資料承載中提供的觸發程序 （例如觸發函式的 hello 佇列訊息），許多觸發程序會提供額外的中繼資料值。</span><span class="sxs-lookup"><span data-stu-id="9f32f-167">In addition toohello data payload provided by a trigger (such as hello queue message that triggered a function), many triggers provide additional metadata values.</span></span> <span data-ttu-id="9f32f-168">這些值可用來當做輸入參數，以 C# 和 F # 類型或屬性上 hello`context.bindings`在 JavaScript 中的物件。</span><span class="sxs-lookup"><span data-stu-id="9f32f-168">These values can be used as input parameters in C# and F# or properties on hello `context.bindings` object in JavaScript.</span></span> 

<span data-ttu-id="9f32f-169">例如，佇列觸發程序支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="9f32f-169">For example, a queue trigger supports hello following properties:</span></span>

* <span data-ttu-id="9f32f-170">QueueTrigger - 如果是有效字串，便觸發訊息內容</span><span class="sxs-lookup"><span data-stu-id="9f32f-170">QueueTrigger - triggering message content if a valid string</span></span>
* <span data-ttu-id="9f32f-171">DequeueCount</span><span class="sxs-lookup"><span data-stu-id="9f32f-171">DequeueCount</span></span>
* <span data-ttu-id="9f32f-172">ExpirationTime</span><span class="sxs-lookup"><span data-stu-id="9f32f-172">ExpirationTime</span></span>
* <span data-ttu-id="9f32f-173">識別碼</span><span class="sxs-lookup"><span data-stu-id="9f32f-173">Id</span></span>
* <span data-ttu-id="9f32f-174">InsertionTime</span><span class="sxs-lookup"><span data-stu-id="9f32f-174">InsertionTime</span></span>
* <span data-ttu-id="9f32f-175">NextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="9f32f-175">NextVisibleTime</span></span>
* <span data-ttu-id="9f32f-176">PopReceipt</span><span class="sxs-lookup"><span data-stu-id="9f32f-176">PopReceipt</span></span>

<span data-ttu-id="9f32f-177">Hello 對應的參考主題說明的每個觸發程序的中繼資料屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9f32f-177">Details of metadata properties for each trigger are described in hello corresponding reference topic.</span></span> <span data-ttu-id="9f32f-178">文件集也會提供 hello**整合**hello 入口網站，在 [hello] 索引標籤**文件**hello 繫結設定區域下的一節。</span><span class="sxs-lookup"><span data-stu-id="9f32f-178">Documentation is also available in hello **Integrate** tab of hello portal, in hello **Documentation** section below hello binding configuration area.</span></span>  

<span data-ttu-id="9f32f-179">例如，因為 blob 觸發程序有一些延遲，所以您可以使用佇列觸發程序 toorun 您的函式 (請參閱[Blob 儲存體觸發程序](functions-bindings-storage-blob.md#storage-blob-trigger)。</span><span class="sxs-lookup"><span data-stu-id="9f32f-179">For example, since blob triggers have some delays, you can use a queue trigger toorun your function (see [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger).</span></span> <span data-ttu-id="9f32f-180">hello 佇列訊息會包含 hello blob filename tootrigger 上。</span><span class="sxs-lookup"><span data-stu-id="9f32f-180">hello queue message would contain hello blob filename tootrigger on.</span></span> <span data-ttu-id="9f32f-181">使用 hello`queueTrigger`中繼資料屬性，您可以在您的設定，而不是您的程式碼中指定此行為。</span><span class="sxs-lookup"><span data-stu-id="9f32f-181">Using hello `queueTrigger` metadata property, you can specify this behavior all in your configuration, rather than your code.</span></span>

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

<span data-ttu-id="9f32f-182">從觸發程序的中繼資料屬性也可用在*繫結運算式*另一個繫結，以遵循 > 一節中所述的 hello。</span><span class="sxs-lookup"><span data-stu-id="9f32f-182">Metadata properties from a trigger can also be used in a *binding expression* for another binding, as described in hello following section.</span></span>

## <a name="binding-expressions-and-patterns"></a><span data-ttu-id="9f32f-183">繫結運算式和模式</span><span class="sxs-lookup"><span data-stu-id="9f32f-183">Binding expressions and patterns</span></span>

<span data-ttu-id="9f32f-184">Hello 的觸發程序和繫結功能最強大的功能之一是*運算式繫結*。</span><span class="sxs-lookup"><span data-stu-id="9f32f-184">One of hello most powerful features of triggers and bindings is *binding expressions*.</span></span> <span data-ttu-id="9f32f-185">在繫結中，您可以定義模式運算式，並將它用於其他繫結或您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9f32f-185">Within your binding, you can define pattern expressions which can then be used in other bindings or your code.</span></span> <span data-ttu-id="9f32f-186">觸發程序的中繼資料也可以用於繫結 hello 範例 hello 前面一節中所顯示的運算式。</span><span class="sxs-lookup"><span data-stu-id="9f32f-186">Trigger metadata can also be used in binding expressions, as show in hello sample in hello preceding section.</span></span>

<span data-ttu-id="9f32f-187">例如，假設您想要在特定的 blob 儲存體容器，類似 toohello tooresize 影像**影像大小調整程式**hello 範本**新函式**頁面。</span><span class="sxs-lookup"><span data-stu-id="9f32f-187">For example, suppose you want tooresize images in particular blob storage container, similar toohello **Image Resizer** template in hello **New Function** page.</span></span> <span data-ttu-id="9f32f-188">跳過**新函式**]-> [語言**C#** ]-> [案例**範例** -> **ImageResizer CSharp**。</span><span class="sxs-lookup"><span data-stu-id="9f32f-188">Go too**New Function** -> Language **C#** -> Scenario **Samples** -> **ImageResizer-CSharp**.</span></span> 

<span data-ttu-id="9f32f-189">以下是 hello *function.json*定義：</span><span class="sxs-lookup"><span data-stu-id="9f32f-189">Here is hello *function.json* definition:</span></span>

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

<span data-ttu-id="9f32f-190">請注意該 hello `filename` hello blob 觸發程序的定義以及 hello blob 中使用參數輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="9f32f-190">Notice that hello `filename` parameter is used in both hello blob trigger definition as well as hello blob output binding.</span></span> <span data-ttu-id="9f32f-191">這個參數也可以用於函數程式碼。</span><span class="sxs-lookup"><span data-stu-id="9f32f-191">This parameter can also be used in function code.</span></span>

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


### <a name="random-guids"></a><span data-ttu-id="9f32f-192">隨機 GUID</span><span class="sxs-lookup"><span data-stu-id="9f32f-192">Random GUIDs</span></span>
<span data-ttu-id="9f32f-193">Azure 的函式提供在您的繫結，透過 hello 中產生 Guid 的便利性語法`{rand-guid}`繫結運算式。</span><span class="sxs-lookup"><span data-stu-id="9f32f-193">Azure Functions provides a convenience syntax for generating GUIDs in your bindings, through hello `{rand-guid}` binding expression.</span></span> <span data-ttu-id="9f32f-194">hello 下列範例會使用這個 toogenerate 唯一 blob 名稱：</span><span class="sxs-lookup"><span data-stu-id="9f32f-194">hello following example uses this toogenerate a unique blob name:</span></span> 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a><span data-ttu-id="9f32f-195">目前時間</span><span class="sxs-lookup"><span data-stu-id="9f32f-195">Current time</span></span>

<span data-ttu-id="9f32f-196">您可以使用 hello 繫結運算式`DateTime`，這會解析太`DateTime.UtcNow`。</span><span class="sxs-lookup"><span data-stu-id="9f32f-196">You can use hello binding expression `DateTime`, which resolves too`DateTime.UtcNow`.</span></span>

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a><span data-ttu-id="9f32f-197">繫結運算式中的繫結 toocustom 輸入的屬性</span><span class="sxs-lookup"><span data-stu-id="9f32f-197">Bind toocustom input properties in a binding expression</span></span>

<span data-ttu-id="9f32f-198">繫結運算式也可以參考本身 hello 觸發程序內容中所定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="9f32f-198">Binding expressions can also reference properties that are defined in hello trigger payload itself.</span></span> <span data-ttu-id="9f32f-199">比方說，您可能想 toodynamically 繫結 tooa blob 儲存體檔案從 webhook 中提供的檔名。</span><span class="sxs-lookup"><span data-stu-id="9f32f-199">For example, you may want toodynamically bind tooa blob storage file from a filename provided in a webhook.</span></span>

<span data-ttu-id="9f32f-200">比方說，hello 遵循*function.json*會使用稱為屬性`BlobName`hello 觸發程序的內容：</span><span class="sxs-lookup"><span data-stu-id="9f32f-200">For example, hello following *function.json* uses a property called `BlobName` from hello trigger payload:</span></span>

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

<span data-ttu-id="9f32f-201">tooaccomplish 這在 C# 和 F # 中，您必須定義 hello 觸發程序內容中所定義將還原序列化的 hello 欄位 POCO。</span><span class="sxs-lookup"><span data-stu-id="9f32f-201">tooaccomplish this in C# and F#, you must define a POCO that defines hello fields that will be deserialized in hello trigger payload.</span></span>

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

<span data-ttu-id="9f32f-202">在 JavaScript 中，JSON 還原序列化會自動執行，您可以直接使用 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="9f32f-202">In JavaScript, JSON deserialization is automatically performed and you can use hello properties directly.</span></span>

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

## <a name="configuring-binding-data-at-runtime"></a><span data-ttu-id="9f32f-203">在執行階段設定繫結資料</span><span class="sxs-lookup"><span data-stu-id="9f32f-203">Configuring binding data at runtime</span></span>

<span data-ttu-id="9f32f-204">在 C# 和其他.NET 語言，您可以使用命令式繫結模式，但不要的 toohello 中的宣告式繫結為*function.json*。</span><span class="sxs-lookup"><span data-stu-id="9f32f-204">In C# and other .NET languages, you can use an imperative binding pattern, as opposed toohello declarative bindings in *function.json*.</span></span> <span data-ttu-id="9f32f-205">命令式的繫結時，必須在執行階段，而不是設計階段計算 toobe 繫結參數。</span><span class="sxs-lookup"><span data-stu-id="9f32f-205">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="9f32f-206">詳細資訊，請參閱 toolearn[在執行階段透過命令式繫結的繫結](functions-reference-csharp.md#imperative-bindings)hello C# 開發人員參考資料中。</span><span class="sxs-lookup"><span data-stu-id="9f32f-206">toolearn more, see [Binding at runtime via imperative bindings](functions-reference-csharp.md#imperative-bindings) in hello C# developer reference.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f32f-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f32f-207">Next steps</span></span>
<span data-ttu-id="9f32f-208">如需有關特定繫結的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="9f32f-208">For more information on a specific binding, see hello following articles:</span></span>

- [<span data-ttu-id="9f32f-209">HTTP 和 Webhook</span><span class="sxs-lookup"><span data-stu-id="9f32f-209">HTTP and webhooks</span></span>](functions-bindings-http-webhook.md)
- [<span data-ttu-id="9f32f-210">計時器</span><span class="sxs-lookup"><span data-stu-id="9f32f-210">Timer</span></span>](functions-bindings-timer.md)
- [<span data-ttu-id="9f32f-211">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="9f32f-211">Queue storage</span></span>](functions-bindings-storage-queue.md)
- [<span data-ttu-id="9f32f-212">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="9f32f-212">Blob storage</span></span>](functions-bindings-storage-blob.md)
- [<span data-ttu-id="9f32f-213">資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="9f32f-213">Table storage</span></span>](functions-bindings-storage-table.md)
- [<span data-ttu-id="9f32f-214">事件中樞</span><span class="sxs-lookup"><span data-stu-id="9f32f-214">Event Hub</span></span>](functions-bindings-event-hubs.md)
- [<span data-ttu-id="9f32f-215">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="9f32f-215">Service Bus</span></span>](functions-bindings-service-bus.md)
- [<span data-ttu-id="9f32f-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9f32f-216">Cosmos DB</span></span>](functions-bindings-documentdb.md)
- [<span data-ttu-id="9f32f-217">SendGrid</span><span class="sxs-lookup"><span data-stu-id="9f32f-217">SendGrid</span></span>](functions-bindings-sendgrid.md)
- [<span data-ttu-id="9f32f-218">Twilio</span><span class="sxs-lookup"><span data-stu-id="9f32f-218">Twilio</span></span>](functions-bindings-twilio.md)
- [<span data-ttu-id="9f32f-219">通知中樞</span><span class="sxs-lookup"><span data-stu-id="9f32f-219">Notification Hubs</span></span>](functions-bindings-notification-hubs.md)
- [<span data-ttu-id="9f32f-220">行動應用程式</span><span class="sxs-lookup"><span data-stu-id="9f32f-220">Mobile Apps</span></span>](functions-bindings-mobile-apps.md)
- [<span data-ttu-id="9f32f-221">外部檔案</span><span class="sxs-lookup"><span data-stu-id="9f32f-221">External file</span></span>](functions-bindings-external-file.md)
