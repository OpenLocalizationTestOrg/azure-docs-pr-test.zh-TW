---
title: "測試 Azure Functions | Microsoft Docs"
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
ms.openlocfilehash: aca03ba4137893157fcbe6650336782ab88cd234
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="2809f-104">在 Azure Functions 中測試程式碼的策略</span><span class="sxs-lookup"><span data-stu-id="2809f-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="2809f-105">本主題會示範測試函式的各種方法，包括下列一般方式：</span><span class="sxs-lookup"><span data-stu-id="2809f-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span></span>

+ <span data-ttu-id="2809f-106">HTTP 型的工具，例如 cURL、Postman，甚至是適用於 Web 型觸發程序的網頁瀏覽器</span><span class="sxs-lookup"><span data-stu-id="2809f-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="2809f-107">用於測試以 Azure 儲存體為基礎之觸發程序的 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="2809f-107">Azure Storage Explorer, to test Azure Storage-based triggers</span></span>
+ <span data-ttu-id="2809f-108">Azure Functions 入口網站中的 [測試] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="2809f-108">Test tab in the Azure Functions portal</span></span>
+ <span data-ttu-id="2809f-109">計時器觸發函式</span><span class="sxs-lookup"><span data-stu-id="2809f-109">Timer-triggered function</span></span>
+ <span data-ttu-id="2809f-110">測試應用程式或架構</span><span class="sxs-lookup"><span data-stu-id="2809f-110">Testing application or framework</span></span>

<span data-ttu-id="2809f-111">所有測試方法都是使用會透過查詢字串參數或要求主體接受輸入的 HTTP 觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span></span> <span data-ttu-id="2809f-112">您會在第一節中建立此函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-112">You create this function in the first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="2809f-113">建立用於測試的函數</span><span class="sxs-lookup"><span data-stu-id="2809f-113">Create a function for testing</span></span>
<span data-ttu-id="2809f-114">在本教學課程中的大多數時間裡，我們將使用建立函式時可使用的 HttpTrigger JavaScript 函式範本的稍經修改版本。</span><span class="sxs-lookup"><span data-stu-id="2809f-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="2809f-115">如果您需要建立函式的協助，請檢閱這個[教學課程](functions-create-first-azure-function.md)。</span><span class="sxs-lookup"><span data-stu-id="2809f-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="2809f-116">在 [Azure 入口網站]中建立測試函式時，選擇 **HttpTrigger- JavaScript** 範本。</span><span class="sxs-lookup"><span data-stu-id="2809f-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span></span>

<span data-ttu-id="2809f-117">預設函式範本基本上是 "hello world" 函式，可從要求主體或查詢字串參數 `name=<your name>`回應名稱。</span><span class="sxs-lookup"><span data-stu-id="2809f-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="2809f-118">我們將更新程式碼，以讓您在要求主體中以 JSON 內容的形式提供名稱和地址。</span><span class="sxs-lookup"><span data-stu-id="2809f-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span></span> <span data-ttu-id="2809f-119">然後函式會在可使用時將這些內容回應給用戶端。</span><span class="sxs-lookup"><span data-stu-id="2809f-119">Then the function echoes these back to the client when available.</span></span>   

<span data-ttu-id="2809f-120">使用我們將用來測試的下列程式碼更新函式︰</span><span class="sxs-lookup"><span data-stu-id="2809f-120">Update the function with the following code, which we will use for testing:</span></span>

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
            body: "Please pass a name on the query string or in the request body"
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
        echoString += "\n" + "The address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults to 200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="2809f-121">使用工具測試函式</span><span class="sxs-lookup"><span data-stu-id="2809f-121">Test a function with tools</span></span>
<span data-ttu-id="2809f-122">在 Azure 入口網站之外，您可以使用數種工具來針對測試觸發函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span></span> <span data-ttu-id="2809f-123">這些工具包含 HTTP 測試工具 (包括 UI 型和命令列)、Azure 儲存體存取工具，以及甚至簡易的網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="2809f-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="2809f-124">使用瀏覽器測試</span><span class="sxs-lookup"><span data-stu-id="2809f-124">Test with a browser</span></span>
<span data-ttu-id="2809f-125">網頁瀏覽器是透過 HTTP 觸發函數的簡易方法。</span><span class="sxs-lookup"><span data-stu-id="2809f-125">The web browser is a simple way to trigger functions via HTTP.</span></span> <span data-ttu-id="2809f-126">您可以針對不需要主體承載並僅使用查詢字串參數的 GET 要求使用瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="2809f-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="2809f-127">若要測試稍早定義的函式，請從入口網站複製**函式 URL** 。</span><span class="sxs-lookup"><span data-stu-id="2809f-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span></span> <span data-ttu-id="2809f-128">其具備下列格式：</span><span class="sxs-lookup"><span data-stu-id="2809f-128">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="2809f-129">將 `name` 參數附加至查詢字串。</span><span class="sxs-lookup"><span data-stu-id="2809f-129">Append the `name` parameter to the query string.</span></span> <span data-ttu-id="2809f-130">針對 `<Enter a name here>` 預留位置使用實際的名稱。</span><span class="sxs-lookup"><span data-stu-id="2809f-130">Use an actual name for the `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="2809f-131">將此 URL 貼入瀏覽器，應該會得到預似以下的回應。</span><span class="sxs-lookup"><span data-stu-id="2809f-131">Paste the URL into your browser, and you should get a response similar to the following.</span></span>

![Chrome 瀏覽器索引標籤具有測試回應的螢幕擷取畫面](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="2809f-133">此範例使用 Chrome 瀏覽器，它會將傳回字串包裝在 XML 中。</span><span class="sxs-lookup"><span data-stu-id="2809f-133">This example is the Chrome browser, which wraps the returned string in XML.</span></span> <span data-ttu-id="2809f-134">其他瀏覽器只會顯示字串值。</span><span class="sxs-lookup"><span data-stu-id="2809f-134">Other browsers display just the string value.</span></span>

<span data-ttu-id="2809f-135">在入口網站 [記錄] 視窗中，執行函式時會記錄類似下面的輸出︰</span><span class="sxs-lookup"><span data-stu-id="2809f-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected to log-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="2809f-136">使用 Postman 測試</span><span class="sxs-lookup"><span data-stu-id="2809f-136">Test with Postman</span></span>
<span data-ttu-id="2809f-137">測試多數函數的建議工具是 Postman，它能與 Chrome 瀏覽器整合。</span><span class="sxs-lookup"><span data-stu-id="2809f-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span></span> <span data-ttu-id="2809f-138">若要安裝 Postman，請參閱 [取得 Postman](https://www.getpostman.com/)。</span><span class="sxs-lookup"><span data-stu-id="2809f-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="2809f-139">Postman 可對 HTTP 要求的許多其他屬性提供控制。</span><span class="sxs-lookup"><span data-stu-id="2809f-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="2809f-140">請使用您最熟悉的 HTTP 測試工具。</span><span class="sxs-lookup"><span data-stu-id="2809f-140">Use the HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="2809f-141">以下是 Postman 的一些替代方案︰</span><span class="sxs-lookup"><span data-stu-id="2809f-141">Here are some alternatives to Postman:</span></span>  
>
> * [<span data-ttu-id="2809f-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="2809f-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="2809f-143">Paw</span><span class="sxs-lookup"><span data-stu-id="2809f-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="2809f-144">若要在 Postman 中測試要求主體的函數︰</span><span class="sxs-lookup"><span data-stu-id="2809f-144">To test the function with a request body in Postman:</span></span>

1. <span data-ttu-id="2809f-145">從 Chrome 瀏覽器視窗左上角的 [應用程式] 按鈕啟動 Postman。</span><span class="sxs-lookup"><span data-stu-id="2809f-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="2809f-146">複製您的**函式 Url**，並將它貼到 Postman 中。</span><span class="sxs-lookup"><span data-stu-id="2809f-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="2809f-147">它包含存取程式碼查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="2809f-147">It includes the access code query string parameter.</span></span>
3. <span data-ttu-id="2809f-148">將 HTTP 方法變更為 **POST**。</span><span class="sxs-lookup"><span data-stu-id="2809f-148">Change the HTTP method to **POST**.</span></span>
4. <span data-ttu-id="2809f-149">按一下 [主體] > [原始]，並新增類似以下的 JSON 要求主體︰</span><span class="sxs-lookup"><span data-stu-id="2809f-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="2809f-150">按一下 [傳送] 。</span><span class="sxs-lookup"><span data-stu-id="2809f-150">Click **Send**.</span></span>

<span data-ttu-id="2809f-151">下圖顯示在本教學課程中測試簡單的回應函數範例。</span><span class="sxs-lookup"><span data-stu-id="2809f-151">The following image shows testing the simple echo function example in this tutorial.</span></span>

![Postman 使用者介面的螢幕擷取畫面](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="2809f-153">在入口網站 [記錄] 視窗中，執行函式時會記錄類似下面的輸出︰</span><span class="sxs-lookup"><span data-stu-id="2809f-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-the-command-line"></a><span data-ttu-id="2809f-154">從命令列透過 cURL 進行測試</span><span class="sxs-lookup"><span data-stu-id="2809f-154">Test with cURL from the command line</span></span>
<span data-ttu-id="2809f-155">測試軟體時往往只需要命令列即可協助偵錯您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2809f-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span></span> <span data-ttu-id="2809f-156">對於測試函式也是如此。</span><span class="sxs-lookup"><span data-stu-id="2809f-156">This is no different with testing functions.</span></span> <span data-ttu-id="2809f-157">請注意，以 Linux 為基礎的系統預設可以使用 cURL。</span><span class="sxs-lookup"><span data-stu-id="2809f-157">Note that the cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="2809f-158">在 Windows 上，您必須先下載並安裝 [cURL 工具 (英文)](https://curl.haxx.se/)。</span><span class="sxs-lookup"><span data-stu-id="2809f-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="2809f-159">若要測試稍早定義的函式，請從入口網站複製**函式 URL**。</span><span class="sxs-lookup"><span data-stu-id="2809f-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span></span> <span data-ttu-id="2809f-160">其具備下列格式：</span><span class="sxs-lookup"><span data-stu-id="2809f-160">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="2809f-161">這是用來觸發函式的 URL。</span><span class="sxs-lookup"><span data-stu-id="2809f-161">This is the URL for triggering your function.</span></span> <span data-ttu-id="2809f-162">在命令列上使用 cURL 命令來測試它，以針對函式執行 GET (`-G` 或 `--get`) 要求︰</span><span class="sxs-lookup"><span data-stu-id="2809f-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="2809f-163">這個特定範例需要在 cURL 命令中將查詢字串參數傳遞做為資料 (`-d`)︰</span><span class="sxs-lookup"><span data-stu-id="2809f-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="2809f-164">執行該命令後，您會在命令列上看到函式的下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2809f-164">Run the command, and you see the following output of the function on the command line:</span></span>

![命令提示字元輸出的螢幕擷取畫面](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="2809f-166">在入口網站 [記錄] 視窗中，執行函式時會記錄類似下面的輸出︰</span><span class="sxs-lookup"><span data-stu-id="2809f-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected to log-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="2809f-167">使用儲存體總管測試 blob 觸發程序</span><span class="sxs-lookup"><span data-stu-id="2809f-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="2809f-168">您可以使用 [Azure 儲存體總管](http://storageexplorer.com/)來測試 blob 觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="2809f-169">在您函式應用程式的 [Azure 入口網站]中，建立 C#、F# 或 JavaScript Blob 觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="2809f-170">將要監視的路徑設定為您的 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="2809f-170">Set the path to monitor to the name of your blob container.</span></span> <span data-ttu-id="2809f-171">例如：</span><span class="sxs-lookup"><span data-stu-id="2809f-171">For example:</span></span>

        files
2. <span data-ttu-id="2809f-172">按一下 **+** 按鈕以選取或建立您想要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2809f-172">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="2809f-173">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="2809f-173">Then click **Create**.</span></span>
3. <span data-ttu-id="2809f-174">建立含有下列內容的文字檔，並儲存該檔案：</span><span class="sxs-lookup"><span data-stu-id="2809f-174">Create a text file with the following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="2809f-175">執行 [Azure 儲存體總管](http://storageexplorer.com/)，並連線要監視的儲存體帳戶中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="2809f-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span></span>
5. <span data-ttu-id="2809f-176">按一下 [上傳] 以上傳文字檔案。</span><span class="sxs-lookup"><span data-stu-id="2809f-176">Click **Upload** to upload the text file.</span></span>

    ![儲存體總管的螢幕擷取畫面](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="2809f-178">預設 blob 觸發程序的函式程式碼將會在記錄中報告 blob 的處理：</span><span class="sxs-lookup"><span data-stu-id="2809f-178">The default blob trigger function code reports the processing of the blob in the logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected to log-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="2809f-179">在 Functions 內測試函數</span><span class="sxs-lookup"><span data-stu-id="2809f-179">Test a function within functions</span></span>
<span data-ttu-id="2809f-180">Azure Functions 入口網站是為了讓您測試 HTTP 和計時器觸發的函數而設計。</span><span class="sxs-lookup"><span data-stu-id="2809f-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="2809f-181">您也可以建立函數以觸發其他您正在測試的函數。</span><span class="sxs-lookup"><span data-stu-id="2809f-181">You can also create functions to trigger other functions that you are testing.</span></span>

### <a name="test-with-the-functions-portal-run-button"></a><span data-ttu-id="2809f-182">使用 Functions 入口網站的執行按鈕測試</span><span class="sxs-lookup"><span data-stu-id="2809f-182">Test with the Functions portal Run button</span></span>
<span data-ttu-id="2809f-183">入口網站提供 [執行] 按鈕，可讓您執行一些有限的測試。</span><span class="sxs-lookup"><span data-stu-id="2809f-183">The portal provides a **Run** button that you can use to do some limited testing.</span></span> <span data-ttu-id="2809f-184">您可以使用按鈕提供要求主體，但無法提供查詢字串參數或更新要求標頭。</span><span class="sxs-lookup"><span data-stu-id="2809f-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="2809f-185">藉由在 [要求主體] 欄位中新增類似以下的 JSON 字串，來測試我們稍早建立的 HTTP 觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span></span> <span data-ttu-id="2809f-186">然後按一下 [執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2809f-186">Then click the **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="2809f-187">在入口網站 [記錄] 視窗中，執行函式時會記錄類似下面的輸出︰</span><span class="sxs-lookup"><span data-stu-id="2809f-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="2809f-188">使用計時器觸發程序測試</span><span class="sxs-lookup"><span data-stu-id="2809f-188">Test with a timer trigger</span></span>
<span data-ttu-id="2809f-189">有些函式無法適當地使用先前所述的工具進行測試。</span><span class="sxs-lookup"><span data-stu-id="2809f-189">Some functions can't be adequately tested with the tools mentioned previously.</span></span> <span data-ttu-id="2809f-190">例如，請考量將訊息放入 [Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md)時執行的佇列觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="2809f-191">您一律可以撰寫程式碼來將訊息放入佇列，本文稍後會提供在主控台專案中進行此動作的範例。</span><span class="sxs-lookup"><span data-stu-id="2809f-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="2809f-192">不過，還有另一種方法可用來直接使用函式進行測試。</span><span class="sxs-lookup"><span data-stu-id="2809f-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="2809f-193">您可以使用設定了佇列輸出繫結的計時器觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2809f-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="2809f-194">該計時器觸發程序程式碼會接著將測試訊息寫入至佇列。</span><span class="sxs-lookup"><span data-stu-id="2809f-194">That timer trigger code can then write the test messages to the queue.</span></span> <span data-ttu-id="2809f-195">本節會逐步解說範例。</span><span class="sxs-lookup"><span data-stu-id="2809f-195">This section walks through an example.</span></span>

<span data-ttu-id="2809f-196">如需使用 Azure Function 搭配使用繫結的深入資訊，請參閱 [Azure Functions 開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="2809f-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="2809f-197">建立用於測試的佇列觸發程序</span><span class="sxs-lookup"><span data-stu-id="2809f-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="2809f-198">為了示範此方法，我們會先建立要對名為 `queue-newusers`的佇列進行測試的佇列觸發程序函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span></span> <span data-ttu-id="2809f-199">此函式會處理放入新使用者佇列儲存體的名稱和地址資訊。</span><span class="sxs-lookup"><span data-stu-id="2809f-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="2809f-200">如果您使用不同的佇列名稱，請確定您使用的名稱符合 [命名佇列和中繼資料](https://msdn.microsoft.com/library/dd179349.aspx) 的規則。</span><span class="sxs-lookup"><span data-stu-id="2809f-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="2809f-201">否則，您會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="2809f-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="2809f-202">在函式應用程式的 [Azure 入口網站]中，按一下 [新增函式] > [QueueTrigger - C#]。</span><span class="sxs-lookup"><span data-stu-id="2809f-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="2809f-203">輸入要使用佇列函式監視的佇列名稱：</span><span class="sxs-lookup"><span data-stu-id="2809f-203">Enter the queue name to be monitored by the queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="2809f-204">按一下 **+** 按鈕以選取或建立您想要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2809f-204">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="2809f-205">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="2809f-205">Then click **Create**.</span></span>
4. <span data-ttu-id="2809f-206">將此入口網站瀏覽器視窗保持開啟，使得您可以監視預設的佇列函式範本程式碼的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="2809f-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-to-drop-a-message-in-the-queue"></a><span data-ttu-id="2809f-207">建立要將訊息放在佇列中的計時器觸發程序</span><span class="sxs-lookup"><span data-stu-id="2809f-207">Create a timer trigger to drop a message in the queue</span></span>
1. <span data-ttu-id="2809f-208">在新的瀏覽器視窗中開啟 [Azure 入口網站]，並瀏覽至您的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="2809f-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span></span>
2. <span data-ttu-id="2809f-209">按一下 [新增函式] > [TimerTrigger - C#]。</span><span class="sxs-lookup"><span data-stu-id="2809f-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="2809f-210">輸入 cron 運算式來設定計時器程式碼會測試您的佇列函式的頻率。</span><span class="sxs-lookup"><span data-stu-id="2809f-210">Enter a cron expression to set how often the timer code tests your queue function.</span></span> <span data-ttu-id="2809f-211">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="2809f-211">Then click **Create**.</span></span> <span data-ttu-id="2809f-212">如果您想要每隔 30 秒執行測試，您可以使用下列 [CRON 運算式](https://wikipedia.org/wiki/Cron#CRON_expression)：</span><span class="sxs-lookup"><span data-stu-id="2809f-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="2809f-213">按一下新計時器觸發程序的 [整合]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2809f-213">Click the **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="2809f-214">在 [輸出] 下，按一下 [+ 新輸出]。</span><span class="sxs-lookup"><span data-stu-id="2809f-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="2809f-215">然後按一下 [佇列] 和 [選取]。</span><span class="sxs-lookup"><span data-stu-id="2809f-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="2809f-216">記下您用於**佇列訊息物件**的名稱。</span><span class="sxs-lookup"><span data-stu-id="2809f-216">Note the name you use for the **queue message object**.</span></span> <span data-ttu-id="2809f-217">您可以在計時器函式程式碼中使用它。</span><span class="sxs-lookup"><span data-stu-id="2809f-217">You use this in the timer function code.</span></span>

        myQueue
6. <span data-ttu-id="2809f-218">輸入會傳送訊息的目標佇列名稱︰</span><span class="sxs-lookup"><span data-stu-id="2809f-218">Enter the queue name where the message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="2809f-219">按一下 **+** 按鈕以選取您先前用於佇列觸發程序的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2809f-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span></span> <span data-ttu-id="2809f-220">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2809f-220">Then click **Save**.</span></span>
8. <span data-ttu-id="2809f-221">按一下計時器觸發程序的 [開發]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2809f-221">Click the **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="2809f-222">只要使用稍早顯示的相同佇列訊息物件名稱，您即可以對 C# 計時器函式使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="2809f-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span></span> <span data-ttu-id="2809f-223">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2809f-223">Then click **Save**.</span></span>

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

<span data-ttu-id="2809f-224">目前，如果您已使用範例 cron 運算式，C# 計時器函式會每隔 30 秒執行。</span><span class="sxs-lookup"><span data-stu-id="2809f-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span></span> <span data-ttu-id="2809f-225">計時器函式的記錄會報告每次執行︰</span><span class="sxs-lookup"><span data-stu-id="2809f-225">The logs for the timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="2809f-226">在佇列函式的瀏覽器視窗中，您會看到正在處理的每個訊息︰</span><span class="sxs-lookup"><span data-stu-id="2809f-226">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="2809f-227">使用程式碼測試函式</span><span class="sxs-lookup"><span data-stu-id="2809f-227">Test a function with code</span></span>
<span data-ttu-id="2809f-228">您需要建立外部應用程式或架構以測試您的函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-228">You may need to create an external application or framework to test your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="2809f-229">使用 Node.js 程式碼測試 HTTP 觸發程序函式</span><span class="sxs-lookup"><span data-stu-id="2809f-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="2809f-230">您可以使用 Node.js App 來執行 HTTP 要求，以測試您的函式。</span><span class="sxs-lookup"><span data-stu-id="2809f-230">You can use a Node.js app to execute an HTTP request to test your function.</span></span>
<span data-ttu-id="2809f-231">請務必設定：</span><span class="sxs-lookup"><span data-stu-id="2809f-231">Make sure to set:</span></span>

* <span data-ttu-id="2809f-232">要求選項中的 `host` 設為您的函式應用程式主機。</span><span class="sxs-lookup"><span data-stu-id="2809f-232">The `host` in the request options to your function app host.</span></span>
* <span data-ttu-id="2809f-233">在 `path` 中設定您的函數名稱。</span><span class="sxs-lookup"><span data-stu-id="2809f-233">Your function name in the `path`.</span></span>
* <span data-ttu-id="2809f-234">在 `path` 中設定您的存取程式碼 (`<your code>`)。</span><span class="sxs-lookup"><span data-stu-id="2809f-234">Your access code (`<your code>`) in the `path`.</span></span>

<span data-ttu-id="2809f-235">程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="2809f-235">Code example:</span></span>

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


<span data-ttu-id="2809f-236">輸出：</span><span class="sxs-lookup"><span data-stu-id="2809f-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    The address you provided is Dallas, T.X. 75201

<span data-ttu-id="2809f-237">在入口網站 [記錄] 視窗中，執行函式時會記錄類似下面的輸出︰</span><span class="sxs-lookup"><span data-stu-id="2809f-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="2809f-238">使用 C# 程式碼測試佇列觸發程序函式</span><span class="sxs-lookup"><span data-stu-id="2809f-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="2809f-239">我們稍早提到，您可以透過使用程式碼在您的佇列中放置訊息來測試佇列觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2809f-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span></span> <span data-ttu-id="2809f-240">下列範例程式碼是基於[開始使用 Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md)教學課程中提供的 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="2809f-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="2809f-241">從該連結也可以取得其他語言的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2809f-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="2809f-242">若要在主控台應用程式中測試此程式碼，您必須︰</span><span class="sxs-lookup"><span data-stu-id="2809f-242">To test this code in a console app, you must:</span></span>

* <span data-ttu-id="2809f-243">[在 app.config 檔案中設定儲存體連接字串](../storage/queues/storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="2809f-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="2809f-244">傳遞 `name` 和 `address` 做為應用程式的參數。</span><span class="sxs-lookup"><span data-stu-id="2809f-244">Pass a `name` and `address` as parameters to the app.</span></span> <span data-ttu-id="2809f-245">例如， `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`。</span><span class="sxs-lookup"><span data-stu-id="2809f-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="2809f-246">(在執行階段期間，此程式碼會接受新使用者名稱和地址做為命令列引數。)</span><span class="sxs-lookup"><span data-stu-id="2809f-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="2809f-247">範例 C# 程式碼︰</span><span class="sxs-lookup"><span data-stu-id="2809f-247">Example C# code:</span></span>

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

    // Create the queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference to a queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create the queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it to the queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message to " + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="2809f-248">在佇列函式的瀏覽器視窗中，您會看到正在處理的每個訊息︰</span><span class="sxs-lookup"><span data-stu-id="2809f-248">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure 入口網站]: https://portal.azure.com
