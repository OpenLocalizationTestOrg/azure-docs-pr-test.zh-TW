---
title: "aaaTesting Azure 函式 |Microsoft 文件"
description: "使用 Postman、cURL、和 Node.js 來測試您的 Azure Functions。"
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, webhook, 動態計算, 無伺服器架構, 測試"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>在 Azure Functions 中測試程式碼的策略

本主題會示範各種方式 tootest 功能，包括使用遵循一般的 hello 接近的 hello:

+ HTTP 型的工具，例如 cURL、Postman，甚至是適用於 Web 型觸發程序的網頁瀏覽器
+ Azure 儲存體總管 中，tootest Azure 儲存體為基礎的觸發程序
+ Hello Azure 函式的入口網站中的測試 索引標籤
+ 計時器觸發函式
+ 測試應用程式或架構

所有這些測試方法會使用 HTTP 的觸發程序函式可接受透過輸入查詢字串參數或 hello 要求主體。 您可以建立此函數 hello 第一個區段中。

## <a name="create-a-function-for-testing"></a>建立用於測試的函數
本教學課程的大多數時間，我們會使用稍微修改的 hello HttpTrigger JavaScript 函式樣板建立的函式時可用的版本。 如果您需要建立函式的協助，請檢閱這個[教學課程](functions-create-first-azure-function.md)。 選擇 hello **HttpTrigger-JavaScript** hello 中建立 hello 測試函式時的範本[Azure 入口網站]。

hello 預設函式樣板基本上是"hello world"函式，以回應 hello 要求內文或查詢字串參數，從上一頁 hello 名稱`name=<your name>`。  我們會將更新的程式碼 hello tooalso 允許您 tooprovide hello 姓名和地址做為 hello 要求主體中的 JSON 內容。 然後 hello 函式會回應這些後 toohello 用戶端時使用。   

更新 hello 函式，以下列程式碼，我們將用於測試的 hello:

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>使用工具測試函式
外部 hello Azure 入口網站，有各種工具，您可以使用 tootrigger 函式進行測試。 這些工具包含 HTTP 測試工具 (包括 UI 型和命令列)、Azure 儲存體存取工具，以及甚至簡易的網頁瀏覽器。

### <a name="test-with-a-browser"></a>使用瀏覽器測試
hello 網頁瀏覽器是透過 HTTP 的簡單的方式 tootrigger 函式。 您可以針對不需要主體承載並僅使用查詢字串參數的 GET 要求使用瀏覽器。

我們稍早定義複製 hello tootest hello 函式**函式 Url**從 hello 入口網站。 它有下列形式的 hello:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

附加 hello`name`參數 toohello 查詢字串。 使用實際的 hello 名稱`<Enter a name here>`預留位置。

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

貼上 hello URL 到您的瀏覽器，而且您應該會收到類似 toohello 後的回應。

![Chrome 瀏覽器索引標籤具有測試回應的螢幕擷取畫面](./media/functions-test-a-function/browser-test.png)

這個範例是 hello Chrome 瀏覽器，以包裝在 XML 中傳回字串 hello。 其他瀏覽器顯示只 hello 字串值。

Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>使用 Postman 測試
建議工具 tootest hello 大部分的函式是郵差，hello Chrome 瀏覽器與整合。 tooinstall 郵差，請參閱[取得郵差](https://www.getpostman.com/)。 Postman 可對 HTTP 要求的許多其他屬性提供控制。

> [!TIP]
> 使用 hello HTTP 測試工具，系統最熟悉。 以下是一些替代項目 tooPostman:  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Paw](https://luckymarmot.com/paw)  
>
>

具有要求本文中郵差 tootest hello 函式：

1. 從 hello 啟動郵差**應用程式**在 Chrome 瀏覽器視窗的 hello 左上角的按鈕。
2. 複製您的**函式 Url**，並將它貼到 Postman 中。 它包含 hello 存取程式碼查詢字串參數。
3. 變更 hello HTTP 方法太**POST**。
4. 按一下**主體** > **原始**，並將 JSON 要求主體類似 toohello 下列：

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. 按一下 [ **傳送**]。

hello 下圖顯示測試的 hello 簡單 echo 函式範例在本教學課程。

![Postman 使用者介面的螢幕擷取畫面](./media/functions-test-a-function/postman-test.png)

Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>使用 cURL 從 hello 命令列測試
當您要測試的軟體時，通常不需要 toolook 任何 hello 命令列 toohelp 偵錯您的應用程式進一步。 對於測試函式也是如此。 請注意，hello cURL 預設以 Linux 為基礎的系統上可用的。 在 Windows 中，您必須先下載並安裝 hello [cURL 工具](https://curl.haxx.se/)。

我們稍早定義複製 hello tootest hello 函式**函式 URL**從 hello 入口網站。 它有下列形式的 hello:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

這是 hello URL，用於觸發您的函式。 測試這種情況在 hello 命令列 toomake 使用 hello cURL 命令 GET (`-G`或`--get`) 對 hello 函式要求：

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

這個特定的範例要求查詢字串參數，這可以傳遞做為資料 (`-d`) 在 hello cURL 命令：

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

執行的 hello 命令，並請參閱 hello 遵循 hello 命令列上的 hello 函式的輸出：

![命令提示字元輸出的螢幕擷取畫面](./media/functions-test-a-function/curl-test.png)

Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>使用儲存體總管測試 blob 觸發程序
您可以使用 [Azure 儲存體總管](http://storageexplorer.com/)來測試 blob 觸發程序函式。

1. 在 hello [Azure 入口網站]函式應用程式中，建立 C#、 F # 或 JavaScript 的 blob 觸發程序函式。 設定您的 blob 容器的 hello 路徑 toomonitor toohello 名稱。 例如：

        files
2. 按一下 hello  **+** 按鈕 tooselect 或建立您想要 toouse hello 儲存體帳戶。 然後按一下 [ **建立**]。
3. 以下列文字，hello 建立文字檔，並將它儲存：

        A text file for blob trigger function testing.
4. 執行[Azure 儲存體總管](http://storageexplorer.com/)，並連接 toohello hello 受監視的儲存體帳戶中的 blob 容器。
5. 按一下**上傳**tooupload hello 文字檔案。

    ![儲存體總管的螢幕擷取畫面](./media/functions-test-a-function/azure-storage-explorer-test.png)

hello 預設 blob 觸發程序函式程式碼會報告 hello 處理 hello 記錄檔中的 hello blob:

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>在 Functions 內測試函數
hello Azure 函式的入口網站設計您測試 HTTP 和計時器的 toolet 觸發函式。 您也可以建立函式 tootrigger 您要測試其他函式。

### <a name="test-with-hello-functions-portal-run-button"></a>測試與 hello 函式入口網站執行 按鈕
hello 入口網站提供**執行**按鈕可讓您 toodo 一些有限的測試。 您可以使用 [hello] 按鈕，提供要求主體，但您無法提供查詢字串參數，或更新要求標頭。

測試 hello HTTP 我們在 hello 中加入下列 JSON 的字串類似 toohello 稍早建立的觸發程序函數**要求本文**欄位。 然後按一下 [hello**執行**] 按鈕。

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>使用計時器觸發程序測試
某些函式不能使用先前所述的 hello 工具充分測試。 例如，請考量將訊息放入 [Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md)時執行的佇列觸發程序函式。 您可以撰寫程式碼 toodrop 訊息至您的佇列中，這個範例中的主控台專案稍後會提供這份文件。 不過，還有另一種方法可用來直接使用函式進行測試。  

您可以使用設定了佇列輸出繫結的計時器觸發程序。 然後，該計時器觸發程序程式碼可以撰寫 hello 測試訊息 toohello 佇列。 本節會逐步解說範例。

如需在 Azure 函式中使用繫結的深入資訊，請參閱 hello [Azure 函式的開發人員參考](functions-reference.md)。

#### <a name="create-a-queue-trigger-for-testing"></a>建立用於測試的佇列觸發程序
toodemonstrate 這種方式，我們會先建立我們希望 tootest 名為佇列的佇列觸發程序函式`queue-newusers`。 此函式會處理放入新使用者佇列儲存體的名稱和地址資訊。

> [!NOTE]
> 如果您使用不同的佇列名稱，請確定您使用的 hello 名稱符合 toohello[命名的佇列和中繼資料](https://msdn.microsoft.com/library/dd179349.aspx)規則。 否則，您會收到錯誤。
>
>

1. 在 hello [Azure 入口網站]函式應用程式中，按一下 **新函式** > **QueueTrigger-C#**。
2. 輸入 hello 佇列名稱 toobe 受 hello 佇列函式：

        queue-newusers
3. 按一下 hello  **+** 按鈕 tooselect 或建立您想要 toouse hello 儲存體帳戶。 然後按一下 [ **建立**]。
4. 讓這個入口網站的瀏覽器視窗保持開啟，所以您可以監視 hello hello 預設佇列函式範本程式碼的記錄項目。

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>建立計時器觸發程序 toodrop hello 佇列中的訊息
1. 開啟 hello [Azure 入口網站]在新的瀏覽器視窗中，並瀏覽 tooyour 函式應用程式。
2. 按一下 [新增函式] > [TimerTrigger - C#]。 輸入 cron 運算式 tooset 頻率 hello 計時器的程式碼測試您的佇列函式。 然後按一下 [ **建立**]。 如果您想 hello 測試 toorun 每隔 30 秒時，您可以使用下列 hello [CRON 運算式](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. 按一下 hello**整合**新計時器觸發程序 索引標籤。
4. 在 [輸出] 下，按一下 [+ 新輸出]。 然後按一下 [佇列] 和 [選取]。
5. 您用於 hello 提示 hello 名稱**佇列訊息物件**。 您可以使用這個 hello 計時器函式程式碼中。

        myQueue
6. 輸入要在傳送 hello 訊息 hello 佇列名稱：

        queue-newusers
7. 按一下 hello  **+** 按鈕 tooselect hello 儲存體帳戶，而您先前用過了 hello 佇列觸發程序。 然後按一下 [儲存] 。
8. 按一下 hello**開發**計時器觸發程序 索引標籤。
9. 只要使用的 hello 相同佇列的訊息物件的名稱稍早所示，您可以使用下列 hello C# 計時器函式，程式碼的 hello。 然後按一下 [儲存] 。

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

此時，如果您使用的 hello 範例 cron 運算式 hello C# 計時器函式執行每隔 30 秒。 hello hello 計時器函式的記錄檔會報告每次執行：

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

在 hello 瀏覽器視窗中的 hello 佇列函式，您可以看到每個正在處理的訊息：

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>使用程式碼測試函式
您可能需要 toocreate 外部的應用程式或架構 tootest 函式。

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>使用 Node.js 程式碼測試 HTTP 觸發程序函式
您可以使用 Node.js 應用程式 tooexecute HTTP 要求 tootest 您的函式。
請確定 tooset:

* hello `host` hello 要求選項 tooyour 函式應用程式主機中。
* 您的函式名稱 hello `path`。
* 存取程式碼 (`<your code>`) 在 hello `path`。

程式碼範例：

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


輸出：

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>使用 C# 程式碼測試佇列觸發程序函式 #
我們先前所述，您可以使用程式碼 toodrop 訊息佇列中測試佇列觸發程序。 下列範例程式碼的 hello 根據 hello C# 程式碼中 hello[開始使用 Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md)教學課程。 從該連結也可以取得其他語言的程式碼。

tootest 此主控台應用程式中的程式碼，您必須：

* [Hello app.config 檔案中設定您的儲存體連接字串](../storage/queues/storage-dotnet-how-to-use-queues.md)。
* 傳遞`name`和`address`為參數 toohello 應用程式。 例如： `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`。 （此程式碼接受 hello 姓名和地址之新使用者做為命令列引數在執行階段。）

範例 C# 程式碼︰

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

在 hello 瀏覽器視窗中的 hello 佇列函式，您可以看到每個正在處理的訊息：

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure 入口網站]: https://portal.azure.com
