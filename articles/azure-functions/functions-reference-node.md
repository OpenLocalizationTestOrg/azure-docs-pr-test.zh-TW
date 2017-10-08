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
# <a name="azure-functions-javascript-developer-guide"></a>Azure Functions JavaScript 開發人員指南
> [!div class="op_single_selector"]
> * [C# 指令碼](functions-reference-csharp.md)
> * [F# 指令碼](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Azure 函式可以讓簡單 tooexport 的函式被當做 hello JavaScript 經驗`context`與 hello 執行階段通訊和用於接收和傳送資料透過繫結的物件。

本文章假設，您已閱讀 hello [Azure 函式的開發人員參考](functions-reference.md)。

## <a name="exporting-a-function"></a>匯出函數
所有的 JavaScript 函式必須匯出單一`function`透過`module.exports`hello 的執行階段 toofind hello 函式，並執行它。 此函式一定要包含 `context` 物件。

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

繫結的`direction === "in"`傳遞做為函式引數，也就是說，您可以使用[ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically 處理新的輸入 (例如，藉由使用`arguments.length`tooiterate 透過您的輸入)。 當您只有單一觸發程序而沒有其他輸入時，這項功能十分便利，因為您可以如預期般存取觸發程序資料，而不需要參考 `context` 物件。

hello 引數傳遞時一律是 toohello 函式中發生的 hello 順序沿著*function.json*，即使您未在您匯出的陳述式中指定它們。 例如，如果您有`function(context, a, b)`並將它變更太`function(context, a)`，您仍然可以取得 hello 值`b`太參考的函式程式碼中`arguments[3]`。

不論方向的所有繫結會也會傳送 hello 上`context`物件 （請參閱下列指令碼的 hello）。 

## <a name="context-object"></a>context 物件
hello 執行階段會使用`context`物件 toopass 資料 tooand 從您的函式和 toolet 您與 hello 執行階段通訊。

hello 內容物件一律為 hello 第一個參數 tooa 函式，因為它有這類方法必須包含`context.done`和`context.log`，這是必要的 toouse hello 執行階段正確。 您可以命名 hello 物件，您想要的任何內容 (例如，`ctx`或`c`)。

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>context.bindings 屬性

```
context.bindings
```
傳回包含所有輸入和輸出資料的具名物件。 例如，hello 下列中的繫結定義您*function.json*可讓您存取 hello 從 hello hello 佇列的內容`context.bindings.myInput`物件。 

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

### <a name="contextdone-method"></a>context.done 方法
```
context.done([err],[propertyBag])
```

會通知您的程式碼已完成的 hello 執行階段。 您必須呼叫`context.done`，或其他 hello 執行階段完全不會知道您的函式已完成，且將會逾時 hello 執行。 

hello`context.done`方法可讓您 toopass 備份使用者定義錯誤 toohello 執行階段和覆寫在 hello hello 屬性的屬性的屬性包`context.bindings`物件。

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>context.log 方法  

```
context.log(message)
```
可讓您 toowrite toohello 串流主控台記錄在 hello 預設追蹤層級。 在`context.log`其他記錄的方法，是可讓您撰寫 toohello 其他追蹤層級的主控台記錄檔：


| 方法                 | 說明                                |
| ---------------------- | ------------------------------------------ |
| **error(_message_)**   | 寫入記錄，或更低的 tooerror 層級。   |
| **warn(_message_)**    | 寫入記錄，或更低的 toowarning 層級。 |
| **info(_message_)**    | 寫入記錄，或更低的 tooinfo 層級。    |
| **verbose(_message_)** | 寫入 tooverbose 記錄層級。           |

hello 下列範例會寫 toohello 主控台 hello 警告追蹤層級：

```javascript
context.log.warn("Something has happened."); 
```
您可以設定在 hello host.json 檔案中，記錄的 hello 追蹤層級臨界值，或將它關閉。  如需 toowrite toohello 的記錄檔的詳細資訊，請參閱 hello 下一節。

## <a name="binding-data-type"></a>繫結資料類型

toodefine hello 資料類型的輸入繫結，使用 hello `dataType` hello 繫結的定義中的屬性。 例如，tooread hello 內容的 HTTP 要求以二進位格式，請使用 hello 類型`binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

`dataType` 也另具有 `stream` 和 `string` 兩種選項。

## <a name="writing-trace-output-toohello-console"></a>寫入追蹤輸出 toohello 主控台 

在函數中，您可以使用 hello`context.log`方法 toowrite 追蹤輸出 toohello 主控台。 此時，您不能使用`console.log`toowrite toohello 主控台。

當您呼叫`context.log()`，您的訊息會寫入 toohello 主控台在 hello 預設追蹤層級為 hello_資訊_追蹤層級。 hello 下列程式碼寫入 toohello 主控台 hello 資訊追蹤層級：

```javascript
context.log({hello: 'world'});  
```

hello 上述程式碼是下列程式碼的對等 toohello:

```javascript
context.log.info({hello: 'world'});  
```

hello 下列程式碼寫入 toohello 主控台 hello 錯誤層級：

```javascript
context.log.error("An error has occurred.");  
```

因為_錯誤_hello 最高的追蹤層級，這項追蹤會寫入 toohello 輸出所有的追蹤層級，只要已啟用記錄。  


所有`context.log`方法支援 hello 相同的參數格式支援的 hello Node.js [util.format 方法](https://nodejs.org/api/util.html#util_util_format_format)。 請考慮下列程式碼，其使用 hello 預設追蹤層級寫入 toohello 主控台 hello:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

您也可以寫入 hello 相同的程式碼中遵循格式 hello:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>設定追蹤層級 hello 主控台記錄

函式可讓您定義 hello 閾值追蹤層級寫入 toohello 主控台，可讓您輕鬆 toocontrol hello 方式追蹤會寫入 toohello 主控台，從您的函式。 所有的追蹤寫入 toohello 主控台中，使用 hello tooset hello 閾值`tracing.consoleLevel`hello host.json 檔案中的屬性。 此設定適用於 tooall 函式應用程式中的函式。 hello 下列範例會設定 hello 追蹤閾值 tooenable 詳細資訊記錄：

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

值的**consoleLevel**對應 hello toohello 名稱`context.log`方法。 toodisable 所有的追蹤記錄 toohello 主控台設定**consoleLevel** too_off_。 如需 hello host.json 檔案的詳細資訊，請參閱 hello [host.json 參考主題](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。

## <a name="http-triggers-and-bindings"></a>HTTP 觸發程序和繫結

HTTP 和 webhook 觸發程序和 HTTP 輸出繫結使用要求和回應物件 toorepresent hello HTTP 訊息。  

### <a name="request-object"></a>要求物件

hello`request`物件具有下列屬性的 hello:

| 屬性      | 說明                                                    |
| ------------- | -------------------------------------------------------------- |
| _body_        | 包含 hello hello 要求主體的物件。               |
| _headers_     | 物件，包含 hello 要求標頭。                   |
| _method_      | hello hello 要求的 HTTP 方法。                                |
| _originalUrl_ | hello hello 要求 URL。                                        |
| _params_      | 包含 hello hello 要求路由參數的物件。 |
| _查詢_       | 物件，包含 hello 查詢參數。                  |
| _rawBody_     | hello 做為字串的 hello 訊息本文。                           |


### <a name="response-object"></a>回應物件

hello`response`物件具有下列屬性的 hello:

| 屬性  | 說明                                               |
| --------- | --------------------------------------------------------- |
| _body_    | 包含 hello 回應 hello 主體的物件。         |
| _headers_ | 物件，包含 hello 回應標頭。             |
| _isRaw_   | 表示為 hello 回應略過的格式。    |
| _狀態_  | hello 回應 hello HTTP 狀態碼。                     |

### <a name="accessing-hello-request-and-response"></a>存取 hello 要求和回應 

當您使用 HTTP 觸發程序時，您可以存取 hello HTTP 要求和回應物件中任何一種方式：

+ Hello 從名為輸入和輸出繫結。 如此一來，hello HTTP 觸發程序和繫結工作 hello 相同與任何其他繫結。 hello 下列範例會設定 hello 回應物件使用具名`response`繫結： 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ 從`req`和`res`屬性 hello`context`物件。 如此一來，您可以使用 hello 傳統模式 tooaccess HTTP 資料，從 hello 內容物件，而不需要完整 toouse hello`context.bindings.name`模式。 下列範例會示範如何 hello tooaccess hello`req`和`res`hello 物件`context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ 藉由呼叫 `context.done()`。 一種特殊的 HTTP 繫結傳回 hello 回應傳遞 toohello`context.done()`方法。 下列 HTTP hello 輸出繫結定義`$return`輸出參數：

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    此輸出繫結時所預期您 toosupply hello 回應您呼叫`done()`、，如下所示：

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Node 版本和套件管理
在目前鎖定 hello 節點版本`6.5.0`。 我們正在調查加入更多版本並允許設定的支援。

hello 下列步驟可讓您在應用程式函式中包含套件： 

1. 跳過`https://<function_app_name>.scm.azurewebsites.net`。

2. 按一下 [偵錯主控台] > [CMD]。

3. 跳過`D:\home\site\wwwroot`，然後將拖曳您 package.json 檔案 toohello **wwwroot** hello 的上半部 hello 頁面位於資料夾。  
    您也可以上傳檔案 tooyour 函式應用程式，以其他方式。 如需詳細資訊，請參閱[tooupdate 運作應用程式檔案的方式](functions-reference.md#fileupdate)。 

4. Hello package.json 檔案上傳之後，請執行 hello`npm install`命令 hello **Kudu 遠端執行主控台**。  
    這個動作會下載 hello package.json 檔案中指出的 hello 封裝，並重新啟動 hello 函式應用程式。

Hello 您需要安裝的封裝之後，您匯入它們 tooyour 函式呼叫`require('packagename')`，如下列範例中的 hello:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

您應該定義`package.json`hello 函式應用程式根目錄的檔案。 定義的 hello 檔案可讓所有函式在 hello 應用程式共用 hello 相同快取的封裝，可讓 hello 達到最佳效能。 如果發生版本衝突，就可以解決加`package.json`hello 資料夾中的特定函式的檔案。  

## <a name="environment-variables"></a>環境變數
tooget 環境變數或應用程式設定值，使用`process.env`hello 下列程式碼範例所示：

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
## <a name="considerations-for-javascript-functions"></a>JavaScript 函式的考量

當您使用 JavaScript 函式時，必須注意 hello 下列兩個區段中的 hello 考量。

### <a name="choose-single-core-app-service-plans"></a>選擇單一核心 App Service 方案

當您建立使用 hello 應用程式服務方案的函式應用程式時，我們建議您選取單核心計劃，而不是多個核心的計劃。 現在，函式會執行 JavaScript 函式更有效率地單核心 Vm 上，並且使用較大的 Vm 不會產生預期的 hello 效能改進。 如有必要，您可以新增更多單一核心 VM 執行個體來手動進行相應放大，或者您可以啟用自動規模調整。 如需詳細資訊，請參閱[手動或自動調整執行個體計數規模](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)。    

### <a name="typescript-and-coffeescript-support"></a>TypeScript 和 CoffeeScript 支援
直接支援尚未存在自動編譯 TypeScript 或 CoffeeScript 透過 hello 執行階段，因為這類支援需要 toobe 處理 hello runtime 外部，在部署階段。 

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源的 hello:

* [Azure Functions 的最佳做法](functions-best-practices.md)
* [Azure Functions 開發人員參考](functions-reference.md)
* [Azure Functions C# 開發人員參考](functions-reference-csharp.md)
* [Azure Functions F# 開發人員參考](functions-reference-fsharp.md)
* [Azure Functions 觸發程序和繫結](functions-triggers-bindings.md)

