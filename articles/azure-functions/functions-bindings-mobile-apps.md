---
title: "aaaAzure 函式行動裝置應用程式繫結 |Microsoft 文件"
description: "了解如何在 Azure 函式 toouse Azure 行動應用程式繫結。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="6a8d3-104">Azure Functions Mobile Apps 繫結</span><span class="sxs-lookup"><span data-stu-id="6a8d3-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="6a8d3-105">這篇文章說明如何 tooconfigure 和程式碼[Azure 行動應用程式](../app-service-mobile/app-service-mobile-value-prop.md)Azure 函式中的繫結。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="6a8d3-106">Azure Functions 支援 Mobile Apps 的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="6a8d3-107">hello 行動應用程式輸入和輸出繫結可讓您[讀取和寫入 toodata 資料表](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations)行動應用程式中。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="6a8d3-108">Mobile Apps 輸入繫結</span><span class="sxs-lookup"><span data-stu-id="6a8d3-108">Mobile Apps input binding</span></span>
<span data-ttu-id="6a8d3-109">hello 行動應用程式的輸入繫結從行動資料表端點載入一筆記錄，並將其傳遞到您的函式。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="6a8d3-110">在 C# 和 F # 函式中，任何所做的變更 toohello 記錄會傳送 hello 函式已順利結束時回復 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="6a8d3-111">hello 行動應用程式輸入 tooa 函式會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="6a8d3-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="6a8d3-112">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="6a8d3-112">Note hello following:</span></span>

* <span data-ttu-id="6a8d3-113">`id`可以是靜態，或根據 hello 函式會叫用的 hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="6a8d3-114">例如，如果您使用[佇列觸發程序]()那麼函式，然後`"id": "{queueTrigger}"`hello 記錄識別碼 tooretrieve 時，會使用 hello hello 佇列訊息的字串值。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="6a8d3-115">`connection`應該包含 hello 的應用程式中函式，其中包含行動應用程式的 hello URL 的應用程式設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="6a8d3-116">hello 函式會使用此 URL tooconstruct hello 所需的 REST 作業對您的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="6a8d3-117">您[函式應用程式中建立的應用程式設定]()包含行動裝置應用程式的 URL (如下所示`http://<appname>.azurewebsites.net`)，然後指定 hello hello 應用程式設定名稱在 hello`connection`您輸入的繫結中的屬性。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="6a8d3-118">您需要 toospecify`apiKey`如果您[實作 Node.js 行動裝置應用程式後端中的 API 金鑰](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key)，或[實作.NET 行動裝置應用程式後端中的 API 金鑰](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="6a8d3-119">toodo，您[函式應用程式中建立的應用程式設定]()包含 hello API 金鑰，然後新增 hello `apiKey` hello hello 應用程式設定名稱與您輸入繫結中的屬性。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="6a8d3-120">不能與您的行動裝置應用程式用戶端共用此 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="6a8d3-121">它應該只是分散式安全地 tooservice 端用戶端，例如 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="6a8d3-122">Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="6a8d3-123">這可保護您的敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="6a8d3-124">輸入使用方式</span><span class="sxs-lookup"><span data-stu-id="6a8d3-124">Input usage</span></span>
<span data-ttu-id="6a8d3-125">本節說明 toouse 行動應用程式輸入的方式繫結函式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="6a8d3-126">Hello hello 記錄指定找到資料表和記錄識別碼，它會傳遞至名為的 hello [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm)參數 (或在 Node.js 傳遞 hello`context.bindings.<name>`物件)。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="6a8d3-127">當找不到 hello 記錄時，hello 參數是`null`。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="6a8d3-128">在 C# 和 F # 函式，進行輸入 toohello 記錄 （也就是輸入參數） 的任何變更會自動傳送後 toohello 行動應用程式資料表 hello 函式已順利結束時。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="6a8d3-129">在 Node.js 函數中，使用`context.bindings.<name>`tooaccess hello 輸入的記錄。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="6a8d3-130">您無法在 Node.js 中修改記錄。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="6a8d3-131">輸入範例</span><span class="sxs-lookup"><span data-stu-id="6a8d3-131">Input sample</span></span>
<span data-ttu-id="6a8d3-132">假設您有下列 function.json hello，來擷取行動裝置應用程式資料表的記錄識別碼 hello 佇列觸發程序的訊息為 hello:</span><span class="sxs-lookup"><span data-stu-id="6a8d3-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="6a8d3-133">請參閱使用 hello hello 繫結中的輸入資料錄的 hello 特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="6a8d3-134">hello C# 和 F # 範例也會修改 hello 記錄`text`屬性。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="6a8d3-135">C#</span><span class="sxs-lookup"><span data-stu-id="6a8d3-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="6a8d3-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="6a8d3-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="6a8d3-137">C# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="6a8d3-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="6a8d3-138">Node.js 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="6a8d3-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="6a8d3-139">Mobile Apps 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="6a8d3-139">Mobile Apps output binding</span></span>
<span data-ttu-id="6a8d3-140">使用 hello 行動應用程式輸出繫結 toowrite 新的記錄 tooa 行動應用程式資料表端點。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="6a8d3-141">hello 行動應用程式輸出的函式使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="6a8d3-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="6a8d3-142">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="6a8d3-142">Note hello following:</span></span>

* <span data-ttu-id="6a8d3-143">`connection`應該包含 hello 的應用程式中函式，其中包含行動應用程式的 hello URL 的應用程式設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="6a8d3-144">hello 函式會使用此 URL tooconstruct hello 所需的 REST 作業對您的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="6a8d3-145">您[函式應用程式中建立的應用程式設定]()包含行動裝置應用程式的 URL (如下所示`http://<appname>.azurewebsites.net`)，然後指定 hello hello 應用程式設定名稱在 hello`connection`您輸入的繫結中的屬性。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="6a8d3-146">您需要 toospecify`apiKey`如果您[實作 Node.js 行動裝置應用程式後端中的 API 金鑰](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key)，或[實作.NET 行動裝置應用程式後端中的 API 金鑰](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="6a8d3-147">toodo，您[函式應用程式中建立的應用程式設定]()包含 hello API 金鑰，然後新增 hello `apiKey` hello hello 應用程式設定名稱與您輸入繫結中的屬性。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="6a8d3-148">不能與您的行動裝置應用程式用戶端共用此 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="6a8d3-149">它應該只是分散式安全地 tooservice 端用戶端，例如 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="6a8d3-150">Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="6a8d3-151">這可保護您的敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="6a8d3-152">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="6a8d3-152">Output usage</span></span>
<span data-ttu-id="6a8d3-153">本節說明如何 toouse 行動應用程式輸出繫結函式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="6a8d3-154">在 C# 函數中，使用指名的輸出參數的型別`out object`tooaccess hello 輸出記錄。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="6a8d3-155">在 Node.js 函數中，使用`context.bindings.<name>`tooaccess hello 輸出記錄。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="6a8d3-156">輸出範例</span><span class="sxs-lookup"><span data-stu-id="6a8d3-156">Output sample</span></span>
<span data-ttu-id="6a8d3-157">假設您有下列 function.json，可定義佇列的觸發程序和行動應用程式輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="6a8d3-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="6a8d3-158">請參閱 hello hello 行動應用程式資料表端點 hello hello 佇列訊息內容中建立一筆記錄的特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="6a8d3-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="6a8d3-159">C#</span><span class="sxs-lookup"><span data-stu-id="6a8d3-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="6a8d3-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="6a8d3-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="6a8d3-161">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="6a8d3-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="6a8d3-162">Node.js 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="6a8d3-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="6a8d3-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a8d3-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

