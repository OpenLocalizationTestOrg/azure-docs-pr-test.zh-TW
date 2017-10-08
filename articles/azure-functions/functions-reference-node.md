---
title: "aaaJavaScript Azure 函式的開發人員參考資料 |Microsoft 文件"
description: "了解 toodevelop 使用 JavaScript 的運作方式。"
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
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="6db49-104">Azure Functions JavaScript 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="6db49-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6db49-105">C# 指令碼</span><span class="sxs-lookup"><span data-stu-id="6db49-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="6db49-106">F# 指令碼</span><span class="sxs-lookup"><span data-stu-id="6db49-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="6db49-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6db49-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="6db49-108">Azure 函式可以讓簡單 tooexport 的函式被當做 hello JavaScript 經驗`context`與 hello 執行階段通訊和用於接收和傳送資料透過繫結的物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="6db49-109">本文章假設，您已閱讀 hello [Azure 函式的開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="6db49-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="6db49-110">匯出函數</span><span class="sxs-lookup"><span data-stu-id="6db49-110">Exporting a function</span></span>
<span data-ttu-id="6db49-111">所有的 JavaScript 函式必須匯出單一`function`透過`module.exports`hello 的執行階段 toofind hello 函式，並執行它。</span><span class="sxs-lookup"><span data-stu-id="6db49-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="6db49-112">此函式一定要包含 `context` 物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="6db49-113">繫結的`direction === "in"`傳遞做為函式引數，也就是說，您可以使用[ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically 處理新的輸入 (例如，藉由使用`arguments.length`tooiterate 透過您的輸入)。</span><span class="sxs-lookup"><span data-stu-id="6db49-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="6db49-114">當您只有單一觸發程序而沒有其他輸入時，這項功能十分便利，因為您可以如預期般存取觸發程序資料，而不需要參考 `context` 物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="6db49-115">hello 引數傳遞時一律是 toohello 函式中發生的 hello 順序沿著*function.json*，即使您未在您匯出的陳述式中指定它們。</span><span class="sxs-lookup"><span data-stu-id="6db49-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="6db49-116">例如，如果您有`function(context, a, b)`並將它變更太`function(context, a)`，您仍然可以取得 hello 值`b`太參考的函式程式碼中`arguments[3]`。</span><span class="sxs-lookup"><span data-stu-id="6db49-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="6db49-117">不論方向的所有繫結會也會傳送 hello 上`context`物件 （請參閱下列指令碼的 hello）。</span><span class="sxs-lookup"><span data-stu-id="6db49-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="6db49-118">context 物件</span><span class="sxs-lookup"><span data-stu-id="6db49-118">context object</span></span>
<span data-ttu-id="6db49-119">hello 執行階段會使用`context`物件 toopass 資料 tooand 從您的函式和 toolet 您與 hello 執行階段通訊。</span><span class="sxs-lookup"><span data-stu-id="6db49-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="6db49-120">hello 內容物件一律為 hello 第一個參數 tooa 函式，因為它有這類方法必須包含`context.done`和`context.log`，這是必要的 toouse hello 執行階段正確。</span><span class="sxs-lookup"><span data-stu-id="6db49-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="6db49-121">您可以命名 hello 物件，您想要的任何內容 (例如，`ctx`或`c`)。</span><span class="sxs-lookup"><span data-stu-id="6db49-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="6db49-122">context.bindings 屬性</span><span class="sxs-lookup"><span data-stu-id="6db49-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="6db49-123">傳回包含所有輸入和輸出資料的具名物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="6db49-124">例如，hello 下列中的繫結定義您*function.json*可讓您存取 hello 從 hello hello 佇列的內容`context.bindings.myInput`物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="6db49-125">context.done 方法</span><span class="sxs-lookup"><span data-stu-id="6db49-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="6db49-126">會通知您的程式碼已完成的 hello 執行階段。</span><span class="sxs-lookup"><span data-stu-id="6db49-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="6db49-127">您必須呼叫`context.done`，或其他 hello 執行階段完全不會知道您的函式已完成，且將會逾時 hello 執行。</span><span class="sxs-lookup"><span data-stu-id="6db49-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="6db49-128">hello`context.done`方法可讓您 toopass 備份使用者定義錯誤 toohello 執行階段和覆寫在 hello hello 屬性的屬性的屬性包`context.bindings`物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="6db49-129">context.log 方法</span><span class="sxs-lookup"><span data-stu-id="6db49-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="6db49-130">可讓您 toowrite toohello 串流主控台記錄在 hello 預設追蹤層級。</span><span class="sxs-lookup"><span data-stu-id="6db49-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="6db49-131">在`context.log`其他記錄的方法，是可讓您撰寫 toohello 其他追蹤層級的主控台記錄檔：</span><span class="sxs-lookup"><span data-stu-id="6db49-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="6db49-132">方法</span><span class="sxs-lookup"><span data-stu-id="6db49-132">Method</span></span>                 | <span data-ttu-id="6db49-133">說明</span><span class="sxs-lookup"><span data-stu-id="6db49-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="6db49-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="6db49-134">**error(_message_)**</span></span>   | <span data-ttu-id="6db49-135">寫入記錄，或更低的 tooerror 層級。</span><span class="sxs-lookup"><span data-stu-id="6db49-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="6db49-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="6db49-136">**warn(_message_)**</span></span>    | <span data-ttu-id="6db49-137">寫入記錄，或更低的 toowarning 層級。</span><span class="sxs-lookup"><span data-stu-id="6db49-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="6db49-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="6db49-138">**info(_message_)**</span></span>    | <span data-ttu-id="6db49-139">寫入記錄，或更低的 tooinfo 層級。</span><span class="sxs-lookup"><span data-stu-id="6db49-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="6db49-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="6db49-140">**verbose(_message_)**</span></span> | <span data-ttu-id="6db49-141">寫入 tooverbose 記錄層級。</span><span class="sxs-lookup"><span data-stu-id="6db49-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="6db49-142">hello 下列範例會寫 toohello 主控台 hello 警告追蹤層級：</span><span class="sxs-lookup"><span data-stu-id="6db49-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="6db49-143">您可以設定在 hello host.json 檔案中，記錄的 hello 追蹤層級臨界值，或將它關閉。</span><span class="sxs-lookup"><span data-stu-id="6db49-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="6db49-144">如需 toowrite toohello 的記錄檔的詳細資訊，請參閱 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="6db49-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="6db49-145">繫結資料類型</span><span class="sxs-lookup"><span data-stu-id="6db49-145">Binding data type</span></span>

<span data-ttu-id="6db49-146">toodefine hello 資料類型的輸入繫結，使用 hello `dataType` hello 繫結的定義中的屬性。</span><span class="sxs-lookup"><span data-stu-id="6db49-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="6db49-147">例如，tooread hello 內容的 HTTP 要求以二進位格式，請使用 hello 類型`binary`:</span><span class="sxs-lookup"><span data-stu-id="6db49-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="6db49-148">`dataType` 也另具有 `stream` 和 `string` 兩種選項。</span><span class="sxs-lookup"><span data-stu-id="6db49-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="6db49-149">寫入追蹤輸出 toohello 主控台</span><span class="sxs-lookup"><span data-stu-id="6db49-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="6db49-150">在函數中，您可以使用 hello`context.log`方法 toowrite 追蹤輸出 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="6db49-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="6db49-151">此時，您不能使用`console.log`toowrite toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="6db49-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="6db49-152">當您呼叫`context.log()`，您的訊息會寫入 toohello 主控台在 hello 預設追蹤層級為 hello_資訊_追蹤層級。</span><span class="sxs-lookup"><span data-stu-id="6db49-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="6db49-153">hello 下列程式碼寫入 toohello 主控台 hello 資訊追蹤層級：</span><span class="sxs-lookup"><span data-stu-id="6db49-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="6db49-154">hello 上述程式碼是下列程式碼的對等 toohello:</span><span class="sxs-lookup"><span data-stu-id="6db49-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="6db49-155">hello 下列程式碼寫入 toohello 主控台 hello 錯誤層級：</span><span class="sxs-lookup"><span data-stu-id="6db49-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="6db49-156">因為_錯誤_hello 最高的追蹤層級，這項追蹤會寫入 toohello 輸出所有的追蹤層級，只要已啟用記錄。</span><span class="sxs-lookup"><span data-stu-id="6db49-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="6db49-157">所有`context.log`方法支援 hello 相同的參數格式支援的 hello Node.js [util.format 方法](https://nodejs.org/api/util.html#util_util_format_format)。</span><span class="sxs-lookup"><span data-stu-id="6db49-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="6db49-158">請考慮下列程式碼，其使用 hello 預設追蹤層級寫入 toohello 主控台 hello:</span><span class="sxs-lookup"><span data-stu-id="6db49-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="6db49-159">您也可以寫入 hello 相同的程式碼中遵循格式 hello:</span><span class="sxs-lookup"><span data-stu-id="6db49-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="6db49-160">設定追蹤層級 hello 主控台記錄</span><span class="sxs-lookup"><span data-stu-id="6db49-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="6db49-161">函式可讓您定義 hello 閾值追蹤層級寫入 toohello 主控台，可讓您輕鬆 toocontrol hello 方式追蹤會寫入 toohello 主控台，從您的函式。</span><span class="sxs-lookup"><span data-stu-id="6db49-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="6db49-162">所有的追蹤寫入 toohello 主控台中，使用 hello tooset hello 閾值`tracing.consoleLevel`hello host.json 檔案中的屬性。</span><span class="sxs-lookup"><span data-stu-id="6db49-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="6db49-163">此設定適用於 tooall 函式應用程式中的函式。</span><span class="sxs-lookup"><span data-stu-id="6db49-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="6db49-164">hello 下列範例會設定 hello 追蹤閾值 tooenable 詳細資訊記錄：</span><span class="sxs-lookup"><span data-stu-id="6db49-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="6db49-165">值的**consoleLevel**對應 hello toohello 名稱`context.log`方法。</span><span class="sxs-lookup"><span data-stu-id="6db49-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="6db49-166">toodisable 所有的追蹤記錄 toohello 主控台設定**consoleLevel** too_off_。</span><span class="sxs-lookup"><span data-stu-id="6db49-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="6db49-167">如需 hello host.json 檔案的詳細資訊，請參閱 hello [host.json 參考主題](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。</span><span class="sxs-lookup"><span data-stu-id="6db49-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="6db49-168">HTTP 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="6db49-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="6db49-169">HTTP 和 webhook 觸發程序和 HTTP 輸出繫結使用要求和回應物件 toorepresent hello HTTP 訊息。</span><span class="sxs-lookup"><span data-stu-id="6db49-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="6db49-170">要求物件</span><span class="sxs-lookup"><span data-stu-id="6db49-170">Request object</span></span>

<span data-ttu-id="6db49-171">hello`request`物件具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="6db49-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="6db49-172">屬性</span><span class="sxs-lookup"><span data-stu-id="6db49-172">Property</span></span>      | <span data-ttu-id="6db49-173">說明</span><span class="sxs-lookup"><span data-stu-id="6db49-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="6db49-174">_body_</span><span class="sxs-lookup"><span data-stu-id="6db49-174">_body_</span></span>        | <span data-ttu-id="6db49-175">包含 hello hello 要求主體的物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="6db49-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="6db49-176">_headers_</span></span>     | <span data-ttu-id="6db49-177">物件，包含 hello 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="6db49-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="6db49-178">_method_</span><span class="sxs-lookup"><span data-stu-id="6db49-178">_method_</span></span>      | <span data-ttu-id="6db49-179">hello hello 要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="6db49-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="6db49-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="6db49-180">_originalUrl_</span></span> | <span data-ttu-id="6db49-181">hello hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="6db49-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="6db49-182">_params_</span><span class="sxs-lookup"><span data-stu-id="6db49-182">_params_</span></span>      | <span data-ttu-id="6db49-183">包含 hello hello 要求路由參數的物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="6db49-184">_查詢_</span><span class="sxs-lookup"><span data-stu-id="6db49-184">_query_</span></span>       | <span data-ttu-id="6db49-185">物件，包含 hello 查詢參數。</span><span class="sxs-lookup"><span data-stu-id="6db49-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="6db49-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="6db49-186">_rawBody_</span></span>     | <span data-ttu-id="6db49-187">hello 做為字串的 hello 訊息本文。</span><span class="sxs-lookup"><span data-stu-id="6db49-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="6db49-188">回應物件</span><span class="sxs-lookup"><span data-stu-id="6db49-188">Response object</span></span>

<span data-ttu-id="6db49-189">hello`response`物件具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="6db49-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="6db49-190">屬性</span><span class="sxs-lookup"><span data-stu-id="6db49-190">Property</span></span>  | <span data-ttu-id="6db49-191">說明</span><span class="sxs-lookup"><span data-stu-id="6db49-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="6db49-192">_body_</span><span class="sxs-lookup"><span data-stu-id="6db49-192">_body_</span></span>    | <span data-ttu-id="6db49-193">包含 hello 回應 hello 主體的物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="6db49-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="6db49-194">_headers_</span></span> | <span data-ttu-id="6db49-195">物件，包含 hello 回應標頭。</span><span class="sxs-lookup"><span data-stu-id="6db49-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="6db49-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="6db49-196">_isRaw_</span></span>   | <span data-ttu-id="6db49-197">表示為 hello 回應略過的格式。</span><span class="sxs-lookup"><span data-stu-id="6db49-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="6db49-198">_狀態_</span><span class="sxs-lookup"><span data-stu-id="6db49-198">_status_</span></span>  | <span data-ttu-id="6db49-199">hello 回應 hello HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="6db49-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="6db49-200">存取 hello 要求和回應</span><span class="sxs-lookup"><span data-stu-id="6db49-200">Accessing hello request and response</span></span> 

<span data-ttu-id="6db49-201">當您使用 HTTP 觸發程序時，您可以存取 hello HTTP 要求和回應物件中任何一種方式：</span><span class="sxs-lookup"><span data-stu-id="6db49-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="6db49-202">Hello 從名為輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="6db49-202">From hello named input and output bindings.</span></span> <span data-ttu-id="6db49-203">如此一來，hello HTTP 觸發程序和繫結工作 hello 相同與任何其他繫結。</span><span class="sxs-lookup"><span data-stu-id="6db49-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="6db49-204">hello 下列範例會設定 hello 回應物件使用具名`response`繫結：</span><span class="sxs-lookup"><span data-stu-id="6db49-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="6db49-205">從`req`和`res`屬性 hello`context`物件。</span><span class="sxs-lookup"><span data-stu-id="6db49-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="6db49-206">如此一來，您可以使用 hello 傳統模式 tooaccess HTTP 資料，從 hello 內容物件，而不需要完整 toouse hello`context.bindings.name`模式。</span><span class="sxs-lookup"><span data-stu-id="6db49-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="6db49-207">下列範例會示範如何 hello tooaccess hello`req`和`res`hello 物件`context`:</span><span class="sxs-lookup"><span data-stu-id="6db49-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="6db49-208">藉由呼叫 `context.done()`。</span><span class="sxs-lookup"><span data-stu-id="6db49-208">By calling `context.done()`.</span></span> <span data-ttu-id="6db49-209">一種特殊的 HTTP 繫結傳回 hello 回應傳遞 toohello`context.done()`方法。</span><span class="sxs-lookup"><span data-stu-id="6db49-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="6db49-210">下列 HTTP hello 輸出繫結定義`$return`輸出參數：</span><span class="sxs-lookup"><span data-stu-id="6db49-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="6db49-211">此輸出繫結時所預期您 toosupply hello 回應您呼叫`done()`、，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6db49-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="6db49-212">Node 版本和套件管理</span><span class="sxs-lookup"><span data-stu-id="6db49-212">Node version and Package Management</span></span>
<span data-ttu-id="6db49-213">在目前鎖定 hello 節點版本`6.5.0`。</span><span class="sxs-lookup"><span data-stu-id="6db49-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="6db49-214">我們正在調查加入更多版本並允許設定的支援。</span><span class="sxs-lookup"><span data-stu-id="6db49-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="6db49-215">hello 下列步驟可讓您在應用程式函式中包含套件：</span><span class="sxs-lookup"><span data-stu-id="6db49-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="6db49-216">跳過`https://<function_app_name>.scm.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="6db49-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="6db49-217">按一下 [偵錯主控台] > [CMD]。</span><span class="sxs-lookup"><span data-stu-id="6db49-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="6db49-218">跳過`D:\home\site\wwwroot`，然後將拖曳您 package.json 檔案 toohello **wwwroot** hello 的上半部 hello 頁面位於資料夾。</span><span class="sxs-lookup"><span data-stu-id="6db49-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="6db49-219">您也可以上傳檔案 tooyour 函式應用程式，以其他方式。</span><span class="sxs-lookup"><span data-stu-id="6db49-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="6db49-220">如需詳細資訊，請參閱[tooupdate 運作應用程式檔案的方式](functions-reference.md#fileupdate)。</span><span class="sxs-lookup"><span data-stu-id="6db49-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="6db49-221">Hello package.json 檔案上傳之後，請執行 hello`npm install`命令 hello **Kudu 遠端執行主控台**。</span><span class="sxs-lookup"><span data-stu-id="6db49-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="6db49-222">這個動作會下載 hello package.json 檔案中指出的 hello 封裝，並重新啟動 hello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="6db49-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="6db49-223">Hello 您需要安裝的封裝之後，您匯入它們 tooyour 函式呼叫`require('packagename')`，如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="6db49-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="6db49-224">您應該定義`package.json`hello 函式應用程式根目錄的檔案。</span><span class="sxs-lookup"><span data-stu-id="6db49-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="6db49-225">定義的 hello 檔案可讓所有函式在 hello 應用程式共用 hello 相同快取的封裝，可讓 hello 達到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="6db49-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="6db49-226">如果發生版本衝突，就可以解決加`package.json`hello 資料夾中的特定函式的檔案。</span><span class="sxs-lookup"><span data-stu-id="6db49-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="6db49-227">環境變數</span><span class="sxs-lookup"><span data-stu-id="6db49-227">Environment variables</span></span>
<span data-ttu-id="6db49-228">tooget 環境變數或應用程式設定值，使用`process.env`hello 下列程式碼範例所示：</span><span class="sxs-lookup"><span data-stu-id="6db49-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="6db49-229">JavaScript 函式的考量</span><span class="sxs-lookup"><span data-stu-id="6db49-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="6db49-230">當您使用 JavaScript 函式時，必須注意 hello 下列兩個區段中的 hello 考量。</span><span class="sxs-lookup"><span data-stu-id="6db49-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="6db49-231">選擇單一核心 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="6db49-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="6db49-232">當您建立使用 hello 應用程式服務方案的函式應用程式時，我們建議您選取單核心計劃，而不是多個核心的計劃。</span><span class="sxs-lookup"><span data-stu-id="6db49-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="6db49-233">現在，函式會執行 JavaScript 函式更有效率地單核心 Vm 上，並且使用較大的 Vm 不會產生預期的 hello 效能改進。</span><span class="sxs-lookup"><span data-stu-id="6db49-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="6db49-234">如有必要，您可以新增更多單一核心 VM 執行個體來手動進行相應放大，或者您可以啟用自動規模調整。</span><span class="sxs-lookup"><span data-stu-id="6db49-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="6db49-235">如需詳細資訊，請參閱[手動或自動調整執行個體計數規模](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6db49-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="6db49-236">TypeScript 和 CoffeeScript 支援</span><span class="sxs-lookup"><span data-stu-id="6db49-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="6db49-237">直接支援尚未存在自動編譯 TypeScript 或 CoffeeScript 透過 hello 執行階段，因為這類支援需要 toobe 處理 hello runtime 外部，在部署階段。</span><span class="sxs-lookup"><span data-stu-id="6db49-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6db49-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6db49-238">Next steps</span></span>
<span data-ttu-id="6db49-239">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="6db49-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="6db49-240">Azure Functions 的最佳做法</span><span class="sxs-lookup"><span data-stu-id="6db49-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="6db49-241">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="6db49-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="6db49-242">Azure Functions C# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="6db49-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="6db49-243">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="6db49-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="6db49-244">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="6db49-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

