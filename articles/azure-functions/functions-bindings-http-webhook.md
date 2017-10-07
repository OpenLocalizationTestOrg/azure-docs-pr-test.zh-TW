---
title: "aaaAzure 函式 HTTP 和 webhook 繫結 |Microsoft 文件"
description: "了解如何 toouse HTTP 和 webhook 觸發程序和 Azure 函式中的繫結。"
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, webhook, 動態計算, 無伺服器架構, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Azure Functions HTTP 和 Webhook 繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

這篇文章說明如何 tooconfigure 和 http 的工作觸發程序和 Azure 函式中的繫結。
進行這些動作，您可以使用 Azure 函式 toobuild 無伺服器應用程式開發介面和回應 toowebhooks。

Azure 的函式會提供下列繫結的 hello:
- [HTTP 觸發程序](#httptrigger)可讓您透過 HTTP 要求叫用函式。 這可以是自訂的 toorespond 太[webhook](#hooktrigger)。
- [HTTP 輸出繫結](#output)可讓您 toorespond toohello 要求。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>HTTP 觸發程序
hello HTTP 觸發程序將會回應 tooan HTTP 要求中執行您的函式。 您可以加以自訂 toorespond tooa 特定 URL 或一組 HTTP 方法。 HTTP 觸發程序也可以設定的 toorespond toowebhooks。 

如果使用 hello 函式網站，您可以也會開始立即使用 預先製作的範本。 選取**新函式**從 hello"應用程式開發介面 & Webhook"**案例**下拉式清單。 選取其中一個 hello 範本，然後按一下**建立**。

根據預設，HTTP 觸發程序會回應 toohello 要求空本文與 HTTP 200 「 確定 」 狀態碼。 toomodify hello 回應，設定[HTTP 輸出繫結](#output)

### <a name="configuring-an-http-trigger"></a>設定 HTTP 觸發程序
定義 HTTP 觸發程序包括下列 hello 中 JSON 的物件類似 toohello `bindings` function.json 的陣列：

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
hello 繫結支援下列屬性的 hello:

* **名稱**： 需要-hello hello 要求或要求主體函式程式碼中使用的變數名稱。 請參閱[從程式碼使用 HTTP 觸發程序](#httptriggerusage)。
* **型別**： 需要-必須設定太"httpTrigger"。
* **方向**： 需要-必須是 「 位置 」 太設定。
* _authLevel_ ： 這會決定哪些索引鍵，如果有的話，需要 toobe hello 要求上呈現順序 tooinvoke hello 函式中。 請參閱下方的[使用金鑰](#keys)。 hello 值可以是 hello 下列其中一種：
    * _anonymous_：不需要 API 金鑰。
    * _function_：需要函式專屬的 API 金鑰。 如果未提供，這會是 hello 預設值。
    * _系統管理員_: hello 主索引鍵為必要。
* **方法**： 這是 toowhich hello 函式會回應 hello HTTP 方法的陣列。 如果未指定，hello 函式會回應 tooall HTTP 方法。 請參閱[自訂 hello HTTP 端點](#url)。
* **路由**： 這會定義 hello 路由範本，控制 toowhich 要求會回覆您的函式的 Url。 hello 若未提供任何預設值是`<functionname>`。 請參閱[自訂 hello HTTP 端點](#url)。
* **webHookType** ： 這會將 hello HTTP 觸發程序 tooact 設定為 hello 指定提供者的 webhook 線上發生干擾。 hello_方法_屬性不應該設定這個選擇。 請參閱[回應 toowebhooks](#hooktrigger)。 hello 值可以是 hello 下列其中一種：
    * _genericJson_：一般用途的 Webhook 端點，不需要特定提供者的邏輯。
    * _github_ : hello 函式會回應 tooGitHub webhook。 hello _authLevel_屬性不應該設定這個選擇。
    * _slack_ : hello 函式會回應 tooSlack webhook。 hello _authLevel_屬性不應該設定這個選擇。

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>從程式碼使用 HTTP 觸發程序
對於 C# 和 F # 函式，您可以是宣告您的觸發程序輸入 toobe hello 類型`HttpRequestMessage`或自訂型別。 如果您選擇`HttpRequestMessage`，就會得到完整存取 toohello 要求物件。 自訂 （例如 POCO) 類型，函式會嘗試 tooparse hello 要求主體為 JSON toopopulate hello 物件屬性。

Node.js 函式，hello 函式執行階段會提供 hello 要求本文，而不是 hello 要求物件。

請參閱 [HTTP 觸發程序範例](#httptriggersample)以取得範例使用方式。


<a name="output"></a>
## <a name="http-response-output-binding"></a>HTTP 回應輸出繫結
使用 hello HTTP 輸出繫結 toorespond toohello HTTP 要求寄件者。 這個繫結需要 HTTP 觸發程序，並可讓您 toocustomize hello 回應 hello 觸發程序的要求相關聯。 如果沒有提供 HTTP 輸出繫結，HTTP 觸發程序將會傳回 HTTP 200 OK 和空白主體。 

### <a name="configuring-an-http-output-binding"></a>設定 HTTP 輸出繫結
hello HTTP 輸出繫結定義包含下列 hello 中 JSON 的物件類似 toohello `bindings` function.json 的陣列：

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
hello 繫結包含下列屬性的 hello:

* **名稱**： 需要-hello 回應 hello 函式程式碼中使用的變數名稱。 請參閱[從程式碼使用 HTTP 輸出繫結](#outputusage)。
* **型別**： 需要-必須設定太"http"。
* **方向**： 需要-必須設定太"out"。

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>從程式碼使用 HTTP 輸出繫結
您可以使用 hello 輸出參數 (例如，"res 」) toorespond toohello http 或 webhook 呼叫者。 或者，您可以使用標準`Request.CreateResponse()`(C#) 或`context.res`(Node.JS) 模式 tooreturn 您的回應。 如需如何 toouse hello 第二個方法的範例，請參閱[HTTP 觸發程序範例](#httptriggersample)和[Webhook 觸發程序範例](#hooktriggersample)。


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>回應 toowebhooks
HTTP 觸發程序以 hello _webHookType_屬性會設定的 toorespond 太[webhook](https://en.wikipedia.org/wiki/Webhook)。 hello 基本組態會使用 hello"genericJson 」 設定。 這會限制要求 tooonly 與使用 HTTP POST 和以 hello`application/json`內容類型。

hello 觸發程序可以此外是量身訂做的 tooa webhook 特定提供者 (例如[GitHub](https://developer.github.com/webhooks/)和[Slack](https://api.slack.com/outgoing-webhooks))。 如果指定的提供者，則 hello 函式執行階段將會處理 hello 提供者的驗證邏輯為您。  

### <a name="configuring-github-as-a-webhook-provider"></a>將 GitHub 設定為 Webhook 提供者
toorespond tooGitHub webhook，第一次使用了 HTTP 觸發程序，建立您的函式，並設定 hello _webHookType_屬性太"github"。 接著將其 [URL](#url) 和 [API 金鑰](#keys) 複製到您 GitHub 存放庫的 [加入 webhook] 頁面。 若要深入了解，請參閱 GitHub 的[建立 Webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) 文件。

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>將 Slack 設定為 Webhook 提供者
hello Slack 的 webhook 為您產生權杖，而不是讓您指定，因此您必須設定的函式特定金鑰 Slack hello 權杖。 請參閱[使用金鑰](#keys)。

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>自訂 hello HTTP 端點
依預設建立 HTTP 觸發程序，或 WebHook，函式時 hello 函式為可定址與 hello 表單的路由：

    http://<yourapp>.azurewebsites.net/api/<funcname> 

您可以自訂此路由使用選擇性的 hello `route` hello HTTP 觸發程序上的屬性輸入繫結。 例如，hello 遵循*function.json*檔案會定義`route`HTTP 觸發程序的屬性：

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

使用此組態，hello 函式現在是可定址以 hello 遵循而不是 hello 原始路由的路由。

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

這可讓 hello 函式程式碼在 hello 位址、 「 類別目錄 」 和 「 識別碼 」 的 toosupport 兩個參數。 您可以將任何 [Web API 路由條件約束](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints)與您的參數搭配使用。 hello 下列 C# 函式程式碼會使用這兩個參數。

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

以下是相同的路由參數 Node.js 函式程式碼 toouse hello。

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

所有函式路由預設前面都會加上 *api*。 您也可以自訂或移除使用 hello hello 首碼`http.routePrefix`屬性中的您*host.json*檔案。 hello 下列範例會移除 hello *api*路由前置字元，使用空字串 hello 前置詞在 hello *host.json*檔案。

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

如需詳細資訊 tooupdate hello *host.json*函式，請參閱 < 檔案[tooupdate 運作應用程式檔案的方式](functions-reference.md#fileupdate)。 

如需有關您可以在 *host.json* 檔案中設定之其他屬性的資訊，請參閱 [host.json 參考](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。


<a name="keys"></a>
## <a name="working-with-keys"></a>使用金鑰
HttpTriggers 可以利用金鑰來增加安全性。 標準 HttpTrigger 可以使用這些 API 金鑰，為需要 hello 金鑰 toobe hello 要求上呈現。 Webhook 可以使用各種不同的方式，根據哪個 hello 提供者支援的索引鍵 tooauthorize 要求。

金鑰會當作您函數應用程式的一部分儲存於 Azure 中，並在加密後靜置。 tooview 您的金鑰，建立新的或復原金鑰 toonew 值、 導覽 tooone hello 入口網站中函式，並選取 「 管理 」。 

金鑰類型有兩種：
- **主機金鑰**： 共用這些機碼的 hello 函式應用程式內的所有函式。 API 金鑰當做使用時，這些行為允許 hello 函式應用程式內存取 tooany 函式。
- **功能鍵**： 這些金鑰套用只有 toohello 特定函式的定義。 API 金鑰當做使用時，這些只允許存取 toothat 函式。

如需參考，名為每個索引鍵，而且 hello 函式和主機層級沒有 （名為 「 預設 」） 的預設索引鍵。 hello**主要金鑰**預設主機鍵名為"_master 」，為每個函式應用程式定義並無法撤銷。 它會提供系統管理存取權 toohello 執行階段 Api。 使用`"authLevel": "admin"`hello 中繫結 JSON hello 要求上呈現此金鑰 toobe; 任何其他金鑰會導致授權失敗。

> [!NOTE]
> 到期 toohello 提高權限不應與協力廠商共用此機碼或原生用戶端應用程式，將它發佈以 hello 的主要金鑰，授與權限。 當您選擇 hello 管理員授權層級時，請務必謹慎。
> 
> 

### <a name="api-key-authorization"></a>API 金鑰授權
根據預設，HttpTrigger 要求 hello HTTP 要求中的 API 金鑰。 因此您的 HTTP 要求通常看起來像這樣：

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

hello 金鑰可以包含在查詢字串變數，名為`code`、 與以上所述，或可以包含在`x-functions-key`HTTP 標頭。 hello hello 機碼值可以是定義 hello 函式的任何函式索引鍵或所有主機金鑰。

您可以選擇 tooallow 要求沒有金鑰，或指定該 hello 主要金鑰必須使用藉由變更 hello `authLevel` hello 繫結 JSON 中的屬性 (請參閱[HTTP 觸發程序](#httptrigger))。

### <a name="keys-and-webhooks"></a>金鑰和 Webhook
Webhook 授權則 hello webhook 線上發生干擾元件來處理，hello HttpTrigger 和 hello 機制的一部分而異 hello webhook 型別。 不過，每個機制都依賴金鑰。 根據預設，會使用名為 「 預設 」 的 hello 函式索引鍵。 如果您想 toouse 不同的索引鍵，您需要 tooconfigure hello webhook 提供者 toosend hello 金鑰名稱與 hello 要求 hello 下列方式之一：

- **查詢字串**: hello 提供者會將 hello 索引鍵名稱傳入 hello`clientid`查詢字串參數 (例如`https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`)。
- **要求標頭**: hello 提供者會將 hello 索引鍵名稱傳入 hello`x-functions-clientid`標頭。

> [!NOTE]
> 函式金鑰的優先順序高於主機金鑰。 如果兩個索引鍵所定義的名稱相同，hello hello 將使用功能鍵。
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>HTTP 觸發程序範例
假設您有下列 HTTP 觸發程序在 hello hello `bindings` function.json 的陣列：

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

請參閱 hello 特定語言的範例會求取`name`在 hello 查詢字串或 hello hello HTTP 要求主體中的參數。

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.js](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>C# 中的 HTTP 觸發程序範例 #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

您也可以繫結 tooa POCO 而不是`HttpRequestMessage`。 這將 hydrated 從 hello hello 要求，剖析成 JSON 主體。 同樣地，toohello HTTP 回應輸出繫結時，可以傳遞類型，這將會傳回 200 狀態碼的 hello 回應主體。
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>F# 中的 HTTP 觸發程序範例 #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

您需要`project.json`，並使用 NuGet tooreference hello`FSharp.Interop.Dynamic`和`Dynamitey`組件，就像這樣：

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

這將會使用 NuGet toofetch 程式相依性，並將指令碼中參考。

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Node.JS 中的 HTTP 觸發程序範例
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Webhook 範例
假設您有下列 hello 中的 webhook 觸發程序的 hello `bindings` function.json 的陣列：

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

請參閱 GitHub 問題註解記錄檔的 hello 特定語言的範例。

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>C# 中的 Webhook 範例 #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>F# 中的 Webhook 範例 #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Node.JS 中的 Webhook 範例
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

