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
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="323e8-104">在 Azure Functions 中測試程式碼的策略</span><span class="sxs-lookup"><span data-stu-id="323e8-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="323e8-105">本主題會示範各種方式 tootest 功能，包括使用遵循一般的 hello 接近的 hello:</span><span class="sxs-lookup"><span data-stu-id="323e8-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="323e8-106">HTTP 型的工具，例如 cURL、Postman，甚至是適用於 Web 型觸發程序的網頁瀏覽器</span><span class="sxs-lookup"><span data-stu-id="323e8-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="323e8-107">Azure 儲存體總管 中，tootest Azure 儲存體為基礎的觸發程序</span><span class="sxs-lookup"><span data-stu-id="323e8-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="323e8-108">Hello Azure 函式的入口網站中的測試 索引標籤</span><span class="sxs-lookup"><span data-stu-id="323e8-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="323e8-109">計時器觸發函式</span><span class="sxs-lookup"><span data-stu-id="323e8-109">Timer-triggered function</span></span>
+ <span data-ttu-id="323e8-110">測試應用程式或架構</span><span class="sxs-lookup"><span data-stu-id="323e8-110">Testing application or framework</span></span>

<span data-ttu-id="323e8-111">所有這些測試方法會使用 HTTP 的觸發程序函式可接受透過輸入查詢字串參數或 hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="323e8-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="323e8-112">您可以建立此函數 hello 第一個區段中。</span><span class="sxs-lookup"><span data-stu-id="323e8-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="323e8-113">建立用於測試的函數</span><span class="sxs-lookup"><span data-stu-id="323e8-113">Create a function for testing</span></span>
<span data-ttu-id="323e8-114">本教學課程的大多數時間，我們會使用稍微修改的 hello HttpTrigger JavaScript 函式樣板建立的函式時可用的版本。</span><span class="sxs-lookup"><span data-stu-id="323e8-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="323e8-115">如果您需要建立函式的協助，請檢閱這個[教學課程](functions-create-first-azure-function.md)。</span><span class="sxs-lookup"><span data-stu-id="323e8-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="323e8-116">選擇 hello **HttpTrigger-JavaScript** hello 中建立 hello 測試函式時的範本[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="323e8-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="323e8-117">hello 預設函式樣板基本上是"hello world"函式，以回應 hello 要求內文或查詢字串參數，從上一頁 hello 名稱`name=<your name>`。</span><span class="sxs-lookup"><span data-stu-id="323e8-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="323e8-118">我們會將更新的程式碼 hello tooalso 允許您 tooprovide hello 姓名和地址做為 hello 要求主體中的 JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="323e8-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="323e8-119">然後 hello 函式會回應這些後 toohello 用戶端時使用。</span><span class="sxs-lookup"><span data-stu-id="323e8-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="323e8-120">更新 hello 函式，以下列程式碼，我們將用於測試的 hello:</span><span class="sxs-lookup"><span data-stu-id="323e8-120">Update hello function with hello following code, which we will use for testing:</span></span>

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

## <a name="test-a-function-with-tools"></a><span data-ttu-id="323e8-121">使用工具測試函式</span><span class="sxs-lookup"><span data-stu-id="323e8-121">Test a function with tools</span></span>
<span data-ttu-id="323e8-122">外部 hello Azure 入口網站，有各種工具，您可以使用 tootrigger 函式進行測試。</span><span class="sxs-lookup"><span data-stu-id="323e8-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="323e8-123">這些工具包含 HTTP 測試工具 (包括 UI 型和命令列)、Azure 儲存體存取工具，以及甚至簡易的網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="323e8-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="323e8-124">使用瀏覽器測試</span><span class="sxs-lookup"><span data-stu-id="323e8-124">Test with a browser</span></span>
<span data-ttu-id="323e8-125">hello 網頁瀏覽器是透過 HTTP 的簡單的方式 tootrigger 函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="323e8-126">您可以針對不需要主體承載並僅使用查詢字串參數的 GET 要求使用瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="323e8-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="323e8-127">我們稍早定義複製 hello tootest hello 函式**函式 Url**從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="323e8-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="323e8-128">它有下列形式的 hello:</span><span class="sxs-lookup"><span data-stu-id="323e8-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="323e8-129">附加 hello`name`參數 toohello 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="323e8-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="323e8-130">使用實際的 hello 名稱`<Enter a name here>`預留位置。</span><span class="sxs-lookup"><span data-stu-id="323e8-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="323e8-131">貼上 hello URL 到您的瀏覽器，而且您應該會收到類似 toohello 後的回應。</span><span class="sxs-lookup"><span data-stu-id="323e8-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Chrome 瀏覽器索引標籤具有測試回應的螢幕擷取畫面](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="323e8-133">這個範例是 hello Chrome 瀏覽器，以包裝在 XML 中傳回字串 hello。</span><span class="sxs-lookup"><span data-stu-id="323e8-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="323e8-134">其他瀏覽器顯示只 hello 字串值。</span><span class="sxs-lookup"><span data-stu-id="323e8-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="323e8-135">Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="323e8-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="323e8-136">使用 Postman 測試</span><span class="sxs-lookup"><span data-stu-id="323e8-136">Test with Postman</span></span>
<span data-ttu-id="323e8-137">建議工具 tootest hello 大部分的函式是郵差，hello Chrome 瀏覽器與整合。</span><span class="sxs-lookup"><span data-stu-id="323e8-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="323e8-138">tooinstall 郵差，請參閱[取得郵差](https://www.getpostman.com/)。</span><span class="sxs-lookup"><span data-stu-id="323e8-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="323e8-139">Postman 可對 HTTP 要求的許多其他屬性提供控制。</span><span class="sxs-lookup"><span data-stu-id="323e8-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="323e8-140">使用 hello HTTP 測試工具，系統最熟悉。</span><span class="sxs-lookup"><span data-stu-id="323e8-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="323e8-141">以下是一些替代項目 tooPostman:</span><span class="sxs-lookup"><span data-stu-id="323e8-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="323e8-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="323e8-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="323e8-143">Paw</span><span class="sxs-lookup"><span data-stu-id="323e8-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="323e8-144">具有要求本文中郵差 tootest hello 函式：</span><span class="sxs-lookup"><span data-stu-id="323e8-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="323e8-145">從 hello 啟動郵差**應用程式**在 Chrome 瀏覽器視窗的 hello 左上角的按鈕。</span><span class="sxs-lookup"><span data-stu-id="323e8-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="323e8-146">複製您的**函式 Url**，並將它貼到 Postman 中。</span><span class="sxs-lookup"><span data-stu-id="323e8-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="323e8-147">它包含 hello 存取程式碼查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="323e8-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="323e8-148">變更 hello HTTP 方法太**POST**。</span><span class="sxs-lookup"><span data-stu-id="323e8-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="323e8-149">按一下**主體** > **原始**，並將 JSON 要求主體類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="323e8-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="323e8-150">按一下 [ **傳送**]。</span><span class="sxs-lookup"><span data-stu-id="323e8-150">Click **Send**.</span></span>

<span data-ttu-id="323e8-151">hello 下圖顯示測試的 hello 簡單 echo 函式範例在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="323e8-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Postman 使用者介面的螢幕擷取畫面](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="323e8-153">Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="323e8-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="323e8-154">使用 cURL 從 hello 命令列測試</span><span class="sxs-lookup"><span data-stu-id="323e8-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="323e8-155">當您要測試的軟體時，通常不需要 toolook 任何 hello 命令列 toohelp 偵錯您的應用程式進一步。</span><span class="sxs-lookup"><span data-stu-id="323e8-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="323e8-156">對於測試函式也是如此。</span><span class="sxs-lookup"><span data-stu-id="323e8-156">This is no different with testing functions.</span></span> <span data-ttu-id="323e8-157">請注意，hello cURL 預設以 Linux 為基礎的系統上可用的。</span><span class="sxs-lookup"><span data-stu-id="323e8-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="323e8-158">在 Windows 中，您必須先下載並安裝 hello [cURL 工具](https://curl.haxx.se/)。</span><span class="sxs-lookup"><span data-stu-id="323e8-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="323e8-159">我們稍早定義複製 hello tootest hello 函式**函式 URL**從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="323e8-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="323e8-160">它有下列形式的 hello:</span><span class="sxs-lookup"><span data-stu-id="323e8-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="323e8-161">這是 hello URL，用於觸發您的函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="323e8-162">測試這種情況在 hello 命令列 toomake 使用 hello cURL 命令 GET (`-G`或`--get`) 對 hello 函式要求：</span><span class="sxs-lookup"><span data-stu-id="323e8-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="323e8-163">這個特定的範例要求查詢字串參數，這可以傳遞做為資料 (`-d`) 在 hello cURL 命令：</span><span class="sxs-lookup"><span data-stu-id="323e8-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="323e8-164">執行的 hello 命令，並請參閱 hello 遵循 hello 命令列上的 hello 函式的輸出：</span><span class="sxs-lookup"><span data-stu-id="323e8-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![命令提示字元輸出的螢幕擷取畫面](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="323e8-166">Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="323e8-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="323e8-167">使用儲存體總管測試 blob 觸發程序</span><span class="sxs-lookup"><span data-stu-id="323e8-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="323e8-168">您可以使用 [Azure 儲存體總管](http://storageexplorer.com/)來測試 blob 觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="323e8-169">在 hello [Azure 入口網站]函式應用程式中，建立 C#、 F # 或 JavaScript 的 blob 觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="323e8-170">設定您的 blob 容器的 hello 路徑 toomonitor toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="323e8-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="323e8-171">例如：</span><span class="sxs-lookup"><span data-stu-id="323e8-171">For example:</span></span>

        files
2. <span data-ttu-id="323e8-172">按一下 hello  **+** 按鈕 tooselect 或建立您想要 toouse hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="323e8-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="323e8-173">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="323e8-173">Then click **Create**.</span></span>
3. <span data-ttu-id="323e8-174">以下列文字，hello 建立文字檔，並將它儲存：</span><span class="sxs-lookup"><span data-stu-id="323e8-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="323e8-175">執行[Azure 儲存體總管](http://storageexplorer.com/)，並連接 toohello hello 受監視的儲存體帳戶中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="323e8-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="323e8-176">按一下**上傳**tooupload hello 文字檔案。</span><span class="sxs-lookup"><span data-stu-id="323e8-176">Click **Upload** tooupload hello text file.</span></span>

    ![儲存體總管的螢幕擷取畫面](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="323e8-178">hello 預設 blob 觸發程序函式程式碼會報告 hello 處理 hello 記錄檔中的 hello blob:</span><span class="sxs-lookup"><span data-stu-id="323e8-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="323e8-179">在 Functions 內測試函數</span><span class="sxs-lookup"><span data-stu-id="323e8-179">Test a function within functions</span></span>
<span data-ttu-id="323e8-180">hello Azure 函式的入口網站設計您測試 HTTP 和計時器的 toolet 觸發函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="323e8-181">您也可以建立函式 tootrigger 您要測試其他函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="323e8-182">測試與 hello 函式入口網站執行 按鈕</span><span class="sxs-lookup"><span data-stu-id="323e8-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="323e8-183">hello 入口網站提供**執行**按鈕可讓您 toodo 一些有限的測試。</span><span class="sxs-lookup"><span data-stu-id="323e8-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="323e8-184">您可以使用 [hello] 按鈕，提供要求主體，但您無法提供查詢字串參數，或更新要求標頭。</span><span class="sxs-lookup"><span data-stu-id="323e8-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="323e8-185">測試 hello HTTP 我們在 hello 中加入下列 JSON 的字串類似 toohello 稍早建立的觸發程序函數**要求本文**欄位。</span><span class="sxs-lookup"><span data-stu-id="323e8-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="323e8-186">然後按一下 [hello**執行**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="323e8-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="323e8-187">Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="323e8-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="323e8-188">使用計時器觸發程序測試</span><span class="sxs-lookup"><span data-stu-id="323e8-188">Test with a timer trigger</span></span>
<span data-ttu-id="323e8-189">某些函式不能使用先前所述的 hello 工具充分測試。</span><span class="sxs-lookup"><span data-stu-id="323e8-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="323e8-190">例如，請考量將訊息放入 [Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md)時執行的佇列觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="323e8-191">您可以撰寫程式碼 toodrop 訊息至您的佇列中，這個範例中的主控台專案稍後會提供這份文件。</span><span class="sxs-lookup"><span data-stu-id="323e8-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="323e8-192">不過，還有另一種方法可用來直接使用函式進行測試。</span><span class="sxs-lookup"><span data-stu-id="323e8-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="323e8-193">您可以使用設定了佇列輸出繫結的計時器觸發程序。</span><span class="sxs-lookup"><span data-stu-id="323e8-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="323e8-194">然後，該計時器觸發程序程式碼可以撰寫 hello 測試訊息 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="323e8-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="323e8-195">本節會逐步解說範例。</span><span class="sxs-lookup"><span data-stu-id="323e8-195">This section walks through an example.</span></span>

<span data-ttu-id="323e8-196">如需在 Azure 函式中使用繫結的深入資訊，請參閱 hello [Azure 函式的開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="323e8-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="323e8-197">建立用於測試的佇列觸發程序</span><span class="sxs-lookup"><span data-stu-id="323e8-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="323e8-198">toodemonstrate 這種方式，我們會先建立我們希望 tootest 名為佇列的佇列觸發程序函式`queue-newusers`。</span><span class="sxs-lookup"><span data-stu-id="323e8-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="323e8-199">此函式會處理放入新使用者佇列儲存體的名稱和地址資訊。</span><span class="sxs-lookup"><span data-stu-id="323e8-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="323e8-200">如果您使用不同的佇列名稱，請確定您使用的 hello 名稱符合 toohello[命名的佇列和中繼資料](https://msdn.microsoft.com/library/dd179349.aspx)規則。</span><span class="sxs-lookup"><span data-stu-id="323e8-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="323e8-201">否則，您會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="323e8-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="323e8-202">在 hello [Azure 入口網站]函式應用程式中，按一下 **新函式** > **QueueTrigger-C#**。</span><span class="sxs-lookup"><span data-stu-id="323e8-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="323e8-203">輸入 hello 佇列名稱 toobe 受 hello 佇列函式：</span><span class="sxs-lookup"><span data-stu-id="323e8-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="323e8-204">按一下 hello  **+** 按鈕 tooselect 或建立您想要 toouse hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="323e8-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="323e8-205">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="323e8-205">Then click **Create**.</span></span>
4. <span data-ttu-id="323e8-206">讓這個入口網站的瀏覽器視窗保持開啟，所以您可以監視 hello hello 預設佇列函式範本程式碼的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="323e8-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="323e8-207">建立計時器觸發程序 toodrop hello 佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="323e8-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="323e8-208">開啟 hello [Azure 入口網站]在新的瀏覽器視窗中，並瀏覽 tooyour 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="323e8-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="323e8-209">按一下 [新增函式] > [TimerTrigger - C#]。</span><span class="sxs-lookup"><span data-stu-id="323e8-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="323e8-210">輸入 cron 運算式 tooset 頻率 hello 計時器的程式碼測試您的佇列函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="323e8-211">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="323e8-211">Then click **Create**.</span></span> <span data-ttu-id="323e8-212">如果您想 hello 測試 toorun 每隔 30 秒時，您可以使用下列 hello [CRON 運算式](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="323e8-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="323e8-213">按一下 hello**整合**新計時器觸發程序 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="323e8-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="323e8-214">在 [輸出] 下，按一下 [+ 新輸出]。</span><span class="sxs-lookup"><span data-stu-id="323e8-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="323e8-215">然後按一下 [佇列] 和 [選取]。</span><span class="sxs-lookup"><span data-stu-id="323e8-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="323e8-216">您用於 hello 提示 hello 名稱**佇列訊息物件**。</span><span class="sxs-lookup"><span data-stu-id="323e8-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="323e8-217">您可以使用這個 hello 計時器函式程式碼中。</span><span class="sxs-lookup"><span data-stu-id="323e8-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="323e8-218">輸入要在傳送 hello 訊息 hello 佇列名稱：</span><span class="sxs-lookup"><span data-stu-id="323e8-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="323e8-219">按一下 hello  **+** 按鈕 tooselect hello 儲存體帳戶，而您先前用過了 hello 佇列觸發程序。</span><span class="sxs-lookup"><span data-stu-id="323e8-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="323e8-220">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="323e8-220">Then click **Save**.</span></span>
8. <span data-ttu-id="323e8-221">按一下 hello**開發**計時器觸發程序 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="323e8-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="323e8-222">只要使用的 hello 相同佇列的訊息物件的名稱稍早所示，您可以使用下列 hello C# 計時器函式，程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="323e8-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="323e8-223">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="323e8-223">Then click **Save**.</span></span>

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

<span data-ttu-id="323e8-224">此時，如果您使用的 hello 範例 cron 運算式 hello C# 計時器函式執行每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="323e8-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="323e8-225">hello hello 計時器函式的記錄檔會報告每次執行：</span><span class="sxs-lookup"><span data-stu-id="323e8-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="323e8-226">在 hello 瀏覽器視窗中的 hello 佇列函式，您可以看到每個正在處理的訊息：</span><span class="sxs-lookup"><span data-stu-id="323e8-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="323e8-227">使用程式碼測試函式</span><span class="sxs-lookup"><span data-stu-id="323e8-227">Test a function with code</span></span>
<span data-ttu-id="323e8-228">您可能需要 toocreate 外部的應用程式或架構 tootest 函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="323e8-229">使用 Node.js 程式碼測試 HTTP 觸發程序函式</span><span class="sxs-lookup"><span data-stu-id="323e8-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="323e8-230">您可以使用 Node.js 應用程式 tooexecute HTTP 要求 tootest 您的函式。</span><span class="sxs-lookup"><span data-stu-id="323e8-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="323e8-231">請確定 tooset:</span><span class="sxs-lookup"><span data-stu-id="323e8-231">Make sure tooset:</span></span>

* <span data-ttu-id="323e8-232">hello `host` hello 要求選項 tooyour 函式應用程式主機中。</span><span class="sxs-lookup"><span data-stu-id="323e8-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="323e8-233">您的函式名稱 hello `path`。</span><span class="sxs-lookup"><span data-stu-id="323e8-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="323e8-234">存取程式碼 (`<your code>`) 在 hello `path`。</span><span class="sxs-lookup"><span data-stu-id="323e8-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="323e8-235">程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="323e8-235">Code example:</span></span>

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


<span data-ttu-id="323e8-236">輸出：</span><span class="sxs-lookup"><span data-stu-id="323e8-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="323e8-237">Hello 入口網站中**記錄**視窗中，會輸出類似 toohello 下列已登入執行 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="323e8-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="323e8-238">使用 C# 程式碼測試佇列觸發程序函式</span><span class="sxs-lookup"><span data-stu-id="323e8-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="323e8-239">我們先前所述，您可以使用程式碼 toodrop 訊息佇列中測試佇列觸發程序。</span><span class="sxs-lookup"><span data-stu-id="323e8-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="323e8-240">下列範例程式碼的 hello 根據 hello C# 程式碼中 hello[開始使用 Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="323e8-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="323e8-241">從該連結也可以取得其他語言的程式碼。</span><span class="sxs-lookup"><span data-stu-id="323e8-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="323e8-242">tootest 此主控台應用程式中的程式碼，您必須：</span><span class="sxs-lookup"><span data-stu-id="323e8-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="323e8-243">[Hello app.config 檔案中設定您的儲存體連接字串](../storage/queues/storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="323e8-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="323e8-244">傳遞`name`和`address`為參數 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="323e8-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="323e8-245">例如： `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`。</span><span class="sxs-lookup"><span data-stu-id="323e8-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="323e8-246">（此程式碼接受 hello 姓名和地址之新使用者做為命令列引數在執行階段。）</span><span class="sxs-lookup"><span data-stu-id="323e8-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="323e8-247">範例 C# 程式碼︰</span><span class="sxs-lookup"><span data-stu-id="323e8-247">Example C# code:</span></span>

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

<span data-ttu-id="323e8-248">在 hello 瀏覽器視窗中的 hello 佇列函式，您可以看到每個正在處理的訊息：</span><span class="sxs-lookup"><span data-stu-id="323e8-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure 入口網站]: https://portal.azure.com
