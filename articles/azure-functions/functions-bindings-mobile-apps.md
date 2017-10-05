---
title: "Azure Functions Mobile Apps 繫結 | Microsoft Docs"
description: "了解如何在 Azure Functions 中使用 Azure Mobile Apps 繫結。"
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
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="767c8-104">Azure Functions Mobile Apps 繫結</span><span class="sxs-lookup"><span data-stu-id="767c8-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="767c8-105">這篇文章說明如何在 Azure Functions 中為 [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) 繫結進行設定及撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="767c8-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="767c8-106">Azure Functions 支援 Mobile Apps 的輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="767c8-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="767c8-107">Mobile Apps 輸入和輸出繫結可讓您在行動裝置應用程式中[對資料表往返讀取和寫入資料](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations)。</span><span class="sxs-lookup"><span data-stu-id="767c8-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="767c8-108">Mobile Apps 輸入繫結</span><span class="sxs-lookup"><span data-stu-id="767c8-108">Mobile Apps input binding</span></span>
<span data-ttu-id="767c8-109">Mobile Apps 輸入繫結會從行動資料表端點載入記錄，並將它傳遞到您的函式。</span><span class="sxs-lookup"><span data-stu-id="767c8-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="767c8-110">在 C# 和 F# 函式中，當函式成功結束時，會將記錄所做的任何變更自動傳回資料表。</span><span class="sxs-lookup"><span data-stu-id="767c8-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="767c8-111">函式的 Mobile Apps 輸入會使用 function.json `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="767c8-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="767c8-112">請注意：</span><span class="sxs-lookup"><span data-stu-id="767c8-112">Note the following:</span></span>

* <span data-ttu-id="767c8-113">`id` 可以是靜態，或基於叫用函式的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="767c8-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="767c8-114">例如，如果您對函式使用[佇列觸發程序]()，則 `"id": "{queueTrigger}"` 會使用佇列訊息的字串值做為要擷取的記錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="767c8-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="767c8-115">`connection` 應該包含函式應用程式中應用程式設定的名稱，因而包含行動裝置應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="767c8-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="767c8-116">函式會使用此 URL 針對您的行動裝置應用程式建構所需的 REST 作業。</span><span class="sxs-lookup"><span data-stu-id="767c8-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="767c8-117">您會[在包含您的行動裝置應用程式 URL 的函式應用程式中建立應用程式設定]() (看起來類似 `http://<appname>.azurewebsites.net`)，然後在輸入繫結的 `connection` 屬性中指定應用程式設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="767c8-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="767c8-118">如果您[在您的 Node.js 行動裝置應用程式後端中實作 API 金鑰](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key)，或[在您的 .NET 行動裝置應用程式後端中實作 API 金鑰](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)，則必須指定 `apiKey`。</span><span class="sxs-lookup"><span data-stu-id="767c8-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="767c8-119">若要這樣做，您會[在包含 API 金鑰的函式應用程式中建立應用程式設定]()，然後在具有應用程式設定名稱的輸入繫結中新增 `apiKey` 屬性。</span><span class="sxs-lookup"><span data-stu-id="767c8-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="767c8-120">不能與您的行動裝置應用程式用戶端共用此 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="767c8-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="767c8-121">只應該安全地散佈給服務端用戶端，如 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="767c8-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="767c8-122">Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="767c8-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="767c8-123">這可保護您的敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="767c8-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="767c8-124">輸入使用方式</span><span class="sxs-lookup"><span data-stu-id="767c8-124">Input usage</span></span>
<span data-ttu-id="767c8-125">本節說明如何在您的函式程式碼中使用您的 Mobile Apps 輸入繫結。</span><span class="sxs-lookup"><span data-stu-id="767c8-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="767c8-126">找到具有指定的資料表和記錄識別碼的記錄時，它會傳遞到具名 [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) 參數 (或在 Node.js 中，則會傳遞到 `context.bindings.<name>` 物件)。</span><span class="sxs-lookup"><span data-stu-id="767c8-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="767c8-127">找不到記錄時，參數為 `null`。</span><span class="sxs-lookup"><span data-stu-id="767c8-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="767c8-128">在 C# 和 F# 函式中，當函式成功結束時，會將對輸入記錄 (輸入參數) 所做的任何變更自動傳送回 Mobile Apps。</span><span class="sxs-lookup"><span data-stu-id="767c8-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="767c8-129">在 Node.js 函式中，使用 `context.bindings.<name>` 來存取輸入記錄。</span><span class="sxs-lookup"><span data-stu-id="767c8-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="767c8-130">您無法在 Node.js 中修改記錄。</span><span class="sxs-lookup"><span data-stu-id="767c8-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="767c8-131">輸入範例</span><span class="sxs-lookup"><span data-stu-id="767c8-131">Input sample</span></span>
<span data-ttu-id="767c8-132">假設您有下列 function.json，其擷取具有下列訊息佇列觸發程序識別碼的 Mobile App 資料表記錄︰</span><span class="sxs-lookup"><span data-stu-id="767c8-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

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

<span data-ttu-id="767c8-133">請參閱使用來自繫結之輸入記錄的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="767c8-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="767c8-134">C# 和 F# 範例也會修改記錄的 `text` 屬性。</span><span class="sxs-lookup"><span data-stu-id="767c8-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="767c8-135">C#</span><span class="sxs-lookup"><span data-stu-id="767c8-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="767c8-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="767c8-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="767c8-137">C# 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="767c8-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="767c8-138">Node.js 中的輸入範例</span><span class="sxs-lookup"><span data-stu-id="767c8-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="767c8-139">Mobile Apps 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="767c8-139">Mobile Apps output binding</span></span>
<span data-ttu-id="767c8-140">使用 Mobile Apps 輸出繫結將新記錄寫入至 Mobile Apps 資料表端點。</span><span class="sxs-lookup"><span data-stu-id="767c8-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="767c8-141">函式的 Mobile Apps 輸出會使用 function.json `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="767c8-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="767c8-142">請注意：</span><span class="sxs-lookup"><span data-stu-id="767c8-142">Note the following:</span></span>

* <span data-ttu-id="767c8-143">`connection` 應該包含函式應用程式中應用程式設定的名稱，因而包含行動裝置應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="767c8-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="767c8-144">函式會使用此 URL 針對您的行動裝置應用程式建構所需的 REST 作業。</span><span class="sxs-lookup"><span data-stu-id="767c8-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="767c8-145">您會[在包含您的行動裝置應用程式 URL 的函式應用程式中建立應用程式設定]() (看起來類似 `http://<appname>.azurewebsites.net`)，然後在輸入繫結的 `connection` 屬性中指定應用程式設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="767c8-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="767c8-146">如果您[在您的 Node.js 行動裝置應用程式後端中實作 API 金鑰](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key)，或[在您的 .NET 行動裝置應用程式後端中實作 API 金鑰](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)，則必須指定 `apiKey`。</span><span class="sxs-lookup"><span data-stu-id="767c8-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="767c8-147">若要這樣做，您會[在包含 API 金鑰的函式應用程式中建立應用程式設定]()，然後在具有應用程式設定名稱的輸入繫結中新增 `apiKey` 屬性。</span><span class="sxs-lookup"><span data-stu-id="767c8-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="767c8-148">不能與您的行動裝置應用程式用戶端共用此 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="767c8-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="767c8-149">只應該安全地散佈給服務端用戶端，如 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="767c8-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="767c8-150">Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="767c8-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="767c8-151">這可保護您的敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="767c8-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="767c8-152">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="767c8-152">Output usage</span></span>
<span data-ttu-id="767c8-153">本節說明如何在您的函式程式碼中使用您的 Mobile Apps 輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="767c8-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="767c8-154">在 C# 函式中，使用類型 `out object` 的具名輸出參數來存取輸出記錄。</span><span class="sxs-lookup"><span data-stu-id="767c8-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="767c8-155">在 Node.js 函式中，使用 `context.bindings.<name>` 來存取輸出記錄。</span><span class="sxs-lookup"><span data-stu-id="767c8-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="767c8-156">輸出範例</span><span class="sxs-lookup"><span data-stu-id="767c8-156">Output sample</span></span>
<span data-ttu-id="767c8-157">假設您有下列 function.json，其定義一個佇列觸發程序和一個 Mobile Apps 輸出︰</span><span class="sxs-lookup"><span data-stu-id="767c8-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="767c8-158">請參閱會在 Mobile Apps 資料表端點建立一筆記錄與佇列訊息內容的特定語言範例。</span><span class="sxs-lookup"><span data-stu-id="767c8-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="767c8-159">C#</span><span class="sxs-lookup"><span data-stu-id="767c8-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="767c8-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="767c8-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="767c8-161">C# 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="767c8-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="767c8-162">Node.js 中的輸出範例</span><span class="sxs-lookup"><span data-stu-id="767c8-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="767c8-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="767c8-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

