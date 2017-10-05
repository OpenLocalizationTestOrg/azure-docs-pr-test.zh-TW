---
title: "適用於 Azure Functions 的 JavaScript 開發人員參考 | Microsoft Docs"
description: "了解如何使用 JavaScript 開發函式。"
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="d5577-104">Azure Functions JavaScript 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="d5577-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5577-105">C# 指令碼</span><span class="sxs-lookup"><span data-stu-id="d5577-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="d5577-106">F# 指令碼</span><span class="sxs-lookup"><span data-stu-id="d5577-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="d5577-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d5577-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="d5577-108">Azure Functions 的 JavaScript 體驗能讓您輕鬆地匯出函式，系統會以 `context` 物件的形式傳遞函式，以便與執行階段通訊，以及透過繫結接收和傳送資料。</span><span class="sxs-lookup"><span data-stu-id="d5577-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="d5577-109">本文假設您已經讀過 [Azure Functions 開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="d5577-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="d5577-110">匯出函數</span><span class="sxs-lookup"><span data-stu-id="d5577-110">Exporting a function</span></span>
<span data-ttu-id="d5577-111">所有 JavaScript 函式都必須透過 `module.exports` 匯出單一 `function`，如此執行階段才能找到函式並執行它。</span><span class="sxs-lookup"><span data-stu-id="d5577-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="d5577-112">此函式一定要包含 `context` 物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="d5577-113">`direction === "in"` 的繫結會和函式引數一起傳遞，這表示您可以使用 [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) 以動態方式處理新的輸入 (例如，藉由使用 `arguments.length` 來反覆查看您的所有輸入)。</span><span class="sxs-lookup"><span data-stu-id="d5577-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="d5577-114">當您只有單一觸發程序而沒有其他輸入時，這項功能十分便利，因為您可以如預期般存取觸發程序資料，而不需要參考 `context` 物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="d5577-115">引數一律會以它們在 *function.json* 中出現的順序傳遞至函式，即使您未在匯出陳述式中指定它們也一樣。</span><span class="sxs-lookup"><span data-stu-id="d5577-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="d5577-116">例如，如果您有 `function(context, a, b)` 並將它變更為 `function(context, a)`，您仍然可以在函式程式碼中藉由參考 `arguments[3]` 來取得 `b` 的值。</span><span class="sxs-lookup"><span data-stu-id="d5577-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="d5577-117">所有繫結 (不論方向為何) 也都會在 `context` 物件上傳遞 (請參閱下列指令碼)。</span><span class="sxs-lookup"><span data-stu-id="d5577-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="d5577-118">context 物件</span><span class="sxs-lookup"><span data-stu-id="d5577-118">context object</span></span>
<span data-ttu-id="d5577-119">執行階段使用 `context` 物件來將資料傳遞至函式並從中傳出，而且可讓您與執行階段進行通訊。</span><span class="sxs-lookup"><span data-stu-id="d5577-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="d5577-120">內容物件一律為函式的第一個參數而且一律必須包含，因為它具有像是 `context.done` 和 `context.log` 的方法，而您必須要有這些方法才能正確地使用執行階段。</span><span class="sxs-lookup"><span data-stu-id="d5577-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="d5577-121">您可以任意方式命名物件 (例如 `ctx` 或 `c`)。</span><span class="sxs-lookup"><span data-stu-id="d5577-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="d5577-122">context.bindings 屬性</span><span class="sxs-lookup"><span data-stu-id="d5577-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="d5577-123">傳回包含所有輸入和輸出資料的具名物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="d5577-124">例如，*function.json* 中的下列繫結定義可讓您從 `context.bindings.myInput` 物件存取佇列的內容。</span><span class="sxs-lookup"><span data-stu-id="d5577-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="d5577-125">context.done 方法</span><span class="sxs-lookup"><span data-stu-id="d5577-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="d5577-126">通知執行階段，您的程式碼已完成。</span><span class="sxs-lookup"><span data-stu-id="d5577-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="d5577-127">您必須呼叫 `context.done`，否則執行階段不會知道您的函式已完成，而且執行會逾時。</span><span class="sxs-lookup"><span data-stu-id="d5577-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="d5577-128">`context.done` 方法可讓您執行下列兩個動作：將使用者定義的錯誤傳回執行階段，以及傳回會覆寫 `context.bindings` 物件上屬性之屬性的屬性包。</span><span class="sxs-lookup"><span data-stu-id="d5577-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="d5577-129">context.log 方法</span><span class="sxs-lookup"><span data-stu-id="d5577-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="d5577-130">可讓您寫入預設追蹤層級的資料流主控台記錄。</span><span class="sxs-lookup"><span data-stu-id="d5577-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="d5577-131">`context.log` 上有其他可用的記錄方法，可讓您在其他追蹤層級寫入主控台記錄中︰</span><span class="sxs-lookup"><span data-stu-id="d5577-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="d5577-132">方法</span><span class="sxs-lookup"><span data-stu-id="d5577-132">Method</span></span>                 | <span data-ttu-id="d5577-133">說明</span><span class="sxs-lookup"><span data-stu-id="d5577-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="d5577-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="d5577-134">**error(_message_)**</span></span>   | <span data-ttu-id="d5577-135">寫入錯誤層級或更低層級的記錄。</span><span class="sxs-lookup"><span data-stu-id="d5577-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="d5577-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="d5577-136">**warn(_message_)**</span></span>    | <span data-ttu-id="d5577-137">寫入警告層級或更低層級的記錄。</span><span class="sxs-lookup"><span data-stu-id="d5577-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="d5577-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="d5577-138">**info(_message_)**</span></span>    | <span data-ttu-id="d5577-139">寫入資訊層級或更低層級的記錄。</span><span class="sxs-lookup"><span data-stu-id="d5577-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="d5577-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="d5577-140">**verbose(_message_)**</span></span> | <span data-ttu-id="d5577-141">寫入詳細資訊層級記錄。</span><span class="sxs-lookup"><span data-stu-id="d5577-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="d5577-142">下列範例會依警告追蹤層級寫入主控台︰</span><span class="sxs-lookup"><span data-stu-id="d5577-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="d5577-143">您可以在 host.json 檔案中設定用於記錄的追蹤層級閾值，或將它關閉。</span><span class="sxs-lookup"><span data-stu-id="d5577-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="d5577-144">如需如何寫入記錄的詳細資訊，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="d5577-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="d5577-145">繫結資料類型</span><span class="sxs-lookup"><span data-stu-id="d5577-145">Binding data type</span></span>

<span data-ttu-id="d5577-146">若要定義輸入繫結的資料類型，請使用繫結定義中的 `dataType` 屬性。</span><span class="sxs-lookup"><span data-stu-id="d5577-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="d5577-147">例如，若要以二進位格式讀取 HTTP 要求的內容，請使用類型 `binary`：</span><span class="sxs-lookup"><span data-stu-id="d5577-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="d5577-148">`dataType` 也另具有 `stream` 和 `string` 兩種選項。</span><span class="sxs-lookup"><span data-stu-id="d5577-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="d5577-149">將追蹤輸出寫入主控台中</span><span class="sxs-lookup"><span data-stu-id="d5577-149">Writing trace output to the console</span></span> 

<span data-ttu-id="d5577-150">在 Functions 中，您可以使用 `context.log` 方法，將追蹤輸出寫入主控台中。</span><span class="sxs-lookup"><span data-stu-id="d5577-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="d5577-151">此時，您不能使用 `console.log` 來寫入主控台中。</span><span class="sxs-lookup"><span data-stu-id="d5577-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="d5577-152">當您呼叫 `context.log()` 時，會在預設追蹤層級 (也就是「資訊」追蹤層級) 將您的訊息寫入主控台中。</span><span class="sxs-lookup"><span data-stu-id="d5577-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="d5577-153">下列程式碼會依資訊追蹤層級寫入主控台中︰</span><span class="sxs-lookup"><span data-stu-id="d5577-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="d5577-154">上述程式碼相當於下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="d5577-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="d5577-155">下列程式碼會依錯誤層級寫入主控台中︰</span><span class="sxs-lookup"><span data-stu-id="d5577-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="d5577-156">因為 _error_ 是最高追蹤層級，所以只要啟用記錄，這項追蹤就會寫入所有追蹤層級的輸出。</span><span class="sxs-lookup"><span data-stu-id="d5577-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="d5577-157">所有 `context.log` 方法都與 Node.js [util.format 方法 (英文)](https://nodejs.org/api/util.html#util_util_format_format) 支援相同的參數格式。</span><span class="sxs-lookup"><span data-stu-id="d5577-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="d5577-158">請考慮下列程式碼，它會使用預設追蹤層級寫入至主控台︰</span><span class="sxs-lookup"><span data-stu-id="d5577-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="d5577-159">您也能以下列格式撰寫相同的程式碼：</span><span class="sxs-lookup"><span data-stu-id="d5577-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="d5577-160">設定用於主控台記錄的追蹤層級</span><span class="sxs-lookup"><span data-stu-id="d5577-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="d5577-161">Functions 讓您定義寫入至主控台的閾值追蹤層級，這可讓您輕鬆地控制追蹤從函式寫入主控台的方式。</span><span class="sxs-lookup"><span data-stu-id="d5577-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="d5577-162">若要設定寫入至主控台之所有追蹤的閾值，請使用 host.json 檔案中的 `tracing.consoleLevel` 屬性。</span><span class="sxs-lookup"><span data-stu-id="d5577-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="d5577-163">這個設定會套用到函式應用程式中的所有函式。</span><span class="sxs-lookup"><span data-stu-id="d5577-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="d5577-164">下列範例會設定追蹤閾值來啟用詳細資訊記錄︰</span><span class="sxs-lookup"><span data-stu-id="d5577-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="d5577-165">**consoleLevel** 的值對應至 `context.log` 方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5577-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="d5577-166">若要停用主控台的所有追蹤記錄，請將 **consoleLevel** 設為 _off_。</span><span class="sxs-lookup"><span data-stu-id="d5577-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="d5577-167">如需 host.json 檔案的詳細資訊，請參閱 [host.json 參考主題](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) (英文)。</span><span class="sxs-lookup"><span data-stu-id="d5577-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="d5577-168">HTTP 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="d5577-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="d5577-169">HTTP 和 Webhook 觸發程序以及 HTTP 輸出繫結會使用要求和回應物件來代表 HTTP 傳訊。</span><span class="sxs-lookup"><span data-stu-id="d5577-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="d5577-170">要求物件</span><span class="sxs-lookup"><span data-stu-id="d5577-170">Request object</span></span>

<span data-ttu-id="d5577-171">`request` 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="d5577-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="d5577-172">屬性</span><span class="sxs-lookup"><span data-stu-id="d5577-172">Property</span></span>      | <span data-ttu-id="d5577-173">說明</span><span class="sxs-lookup"><span data-stu-id="d5577-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="d5577-174">_body_</span><span class="sxs-lookup"><span data-stu-id="d5577-174">_body_</span></span>        | <span data-ttu-id="d5577-175">包含要求本文的物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="d5577-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="d5577-176">_headers_</span></span>     | <span data-ttu-id="d5577-177">包含要求標頭的物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="d5577-178">_method_</span><span class="sxs-lookup"><span data-stu-id="d5577-178">_method_</span></span>      | <span data-ttu-id="d5577-179">要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="d5577-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="d5577-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="d5577-180">_originalUrl_</span></span> | <span data-ttu-id="d5577-181">要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="d5577-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="d5577-182">_params_</span><span class="sxs-lookup"><span data-stu-id="d5577-182">_params_</span></span>      | <span data-ttu-id="d5577-183">包含要求之路由傳送參數的物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="d5577-184">_查詢_</span><span class="sxs-lookup"><span data-stu-id="d5577-184">_query_</span></span>       | <span data-ttu-id="d5577-185">包含查詢參數的物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="d5577-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="d5577-186">_rawBody_</span></span>     | <span data-ttu-id="d5577-187">字串格式的訊息內文。</span><span class="sxs-lookup"><span data-stu-id="d5577-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="d5577-188">回應物件</span><span class="sxs-lookup"><span data-stu-id="d5577-188">Response object</span></span>

<span data-ttu-id="d5577-189">`response` 物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="d5577-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="d5577-190">屬性</span><span class="sxs-lookup"><span data-stu-id="d5577-190">Property</span></span>  | <span data-ttu-id="d5577-191">說明</span><span class="sxs-lookup"><span data-stu-id="d5577-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="d5577-192">_body_</span><span class="sxs-lookup"><span data-stu-id="d5577-192">_body_</span></span>    | <span data-ttu-id="d5577-193">包含回應本文的物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="d5577-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="d5577-194">_headers_</span></span> | <span data-ttu-id="d5577-195">包含回應標頭的物件。</span><span class="sxs-lookup"><span data-stu-id="d5577-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="d5577-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="d5577-196">_isRaw_</span></span>   | <span data-ttu-id="d5577-197">表示略過回應的格式。</span><span class="sxs-lookup"><span data-stu-id="d5577-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="d5577-198">_狀態_</span><span class="sxs-lookup"><span data-stu-id="d5577-198">_status_</span></span>  | <span data-ttu-id="d5577-199">回應的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="d5577-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="d5577-200">存取要求和回應</span><span class="sxs-lookup"><span data-stu-id="d5577-200">Accessing the request and response</span></span> 

<span data-ttu-id="d5577-201">使用 HTTP 觸發程序時，您可以使用三種方式來存取 HTTP 要求和回應物件︰</span><span class="sxs-lookup"><span data-stu-id="d5577-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="d5577-202">從具名輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="d5577-202">From the named input and output bindings.</span></span> <span data-ttu-id="d5577-203">如此一來，HTTP 觸發程序和繫結的運作方式會與任何其他繫結相同。</span><span class="sxs-lookup"><span data-stu-id="d5577-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="d5577-204">下列範例會使用具名 `response` 繫結來設定回應物件：</span><span class="sxs-lookup"><span data-stu-id="d5577-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="d5577-205">從 `context` 物件的 `req` 和 `res` 屬性中。</span><span class="sxs-lookup"><span data-stu-id="d5577-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="d5577-206">如此一來，您可以使用傳統模式來存取內容物件中的 HTTP 資料，而不需使用完整 `context.bindings.name` 模式。</span><span class="sxs-lookup"><span data-stu-id="d5577-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="d5577-207">下列範例示範如何存取 `context` 上的 `req` 和 `res` 物件：</span><span class="sxs-lookup"><span data-stu-id="d5577-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="d5577-208">藉由呼叫 `context.done()`。</span><span class="sxs-lookup"><span data-stu-id="d5577-208">By calling `context.done()`.</span></span> <span data-ttu-id="d5577-209">特殊類型的 HTTP 繫結，會傳回傳遞到 `context.done()` 方法的回應。</span><span class="sxs-lookup"><span data-stu-id="d5577-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="d5577-210">下列 HTTP 輸出繫結定義 `$return` 輸出參數︰</span><span class="sxs-lookup"><span data-stu-id="d5577-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="d5577-211">此輸出繫結需要您在呼叫 `done()` 時提供回應，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d5577-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="d5577-212">Node 版本和套件管理</span><span class="sxs-lookup"><span data-stu-id="d5577-212">Node version and Package Management</span></span>
<span data-ttu-id="d5577-213">Node 版本目前鎖定在 `6.5.0`。</span><span class="sxs-lookup"><span data-stu-id="d5577-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="d5577-214">我們正在調查加入更多版本並允許設定的支援。</span><span class="sxs-lookup"><span data-stu-id="d5577-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="d5577-215">下列步驟可讓您在函式應用程式中納入套件︰</span><span class="sxs-lookup"><span data-stu-id="d5577-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="d5577-216">移至 `https://<function_app_name>.scm.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="d5577-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="d5577-217">按一下 [偵錯主控台] > [CMD]。</span><span class="sxs-lookup"><span data-stu-id="d5577-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="d5577-218">移至 `D:\home\site\wwwroot`，然後將 package.json 檔案拖曳至頁面上半部的 **wwwroot** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d5577-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="d5577-219">您也可以使用其他方法將檔案上傳至函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5577-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="d5577-220">如需詳細資訊，請參閱[如何更新函式應用程式檔案](functions-reference.md#fileupdate)。</span><span class="sxs-lookup"><span data-stu-id="d5577-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="d5577-221">上傳 package.json 檔案之後，請在 **Kudu 遠端執行主控台**中執行 `npm install` 命令。</span><span class="sxs-lookup"><span data-stu-id="d5577-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="d5577-222">此動作會下載 package.json 檔案中指出的套件，並重新啟動函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5577-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="d5577-223">安裝您需要的套件之後，請呼叫 `require('packagename')` 將它們匯入您的函式，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d5577-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="d5577-224">您應該定義函式應用程式根目錄的 `package.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d5577-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="d5577-225">定義檔案可讓應用程式中的所有函式共用相同的快取套件，以提供最佳效能。</span><span class="sxs-lookup"><span data-stu-id="d5577-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="d5577-226">發生版本衝突時，您可以在特定函式的資料夾中新增 `package.json` 檔案來解決它。</span><span class="sxs-lookup"><span data-stu-id="d5577-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="d5577-227">環境變數</span><span class="sxs-lookup"><span data-stu-id="d5577-227">Environment variables</span></span>
<span data-ttu-id="d5577-228">若要取得環境變數或應用程式設定值，請使用 `process.env`，如下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="d5577-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="d5577-229">JavaScript 函式的考量</span><span class="sxs-lookup"><span data-stu-id="d5577-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="d5577-230">當您使用 JavaScript 函式時，請留意下列兩節中的考量事項。</span><span class="sxs-lookup"><span data-stu-id="d5577-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="d5577-231">選擇單一核心 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="d5577-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="d5577-232">當您建立使用 App Service 方案的函數應用程式時，建議您選取單一核心方案，而非具有多核心的方案。</span><span class="sxs-lookup"><span data-stu-id="d5577-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="d5577-233">目前 Functions 在單一核心 VM 上執行 JavaScript 函式會較有效率，而使用較大的 VM 並不會產生預期的效能改進。</span><span class="sxs-lookup"><span data-stu-id="d5577-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="d5577-234">如有必要，您可以新增更多單一核心 VM 執行個體來手動進行相應放大，或者您可以啟用自動規模調整。</span><span class="sxs-lookup"><span data-stu-id="d5577-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="d5577-235">如需詳細資訊，請參閱[手動或自動調整執行個體計數規模](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d5577-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="d5577-236">TypeScript 和 CoffeeScript 支援</span><span class="sxs-lookup"><span data-stu-id="d5577-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="d5577-237">由於目前仍沒有針對透過執行階段自動編譯 TypeScript 或 CoffeeScript 的直接支援，因此需要在部署時期於執行階段之外處理這些支援。</span><span class="sxs-lookup"><span data-stu-id="d5577-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d5577-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5577-238">Next steps</span></span>
<span data-ttu-id="d5577-239">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="d5577-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="d5577-240">Azure Functions 的最佳做法</span><span class="sxs-lookup"><span data-stu-id="d5577-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="d5577-241">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="d5577-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="d5577-242">Azure Functions C# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="d5577-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="d5577-243">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="d5577-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="d5577-244">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="d5577-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

