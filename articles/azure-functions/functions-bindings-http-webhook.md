---
title: "Azure Functions HTTP 和 Webhook 繫結 | Microsoft Docs"
description: "了解如何在 Azure Functions 中使用 HTTP 和 Webhook 觸發程序與繫結。"
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
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="b4281-104">Azure Functions HTTP 和 Webhook 繫結</span><span class="sxs-lookup"><span data-stu-id="b4281-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b4281-105">這篇文章說明如何在 Azure Functions 中設定並使用 HTTP 觸發程序和繫結。</span><span class="sxs-lookup"><span data-stu-id="b4281-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="b4281-106">利用這些資訊，您就可以使用 Azure Functions 建置無伺服器 API 並回應 Webhook。</span><span class="sxs-lookup"><span data-stu-id="b4281-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="b4281-107">Azure Functions 提供下列繫結：</span><span class="sxs-lookup"><span data-stu-id="b4281-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="b4281-108">[HTTP 觸發程序](#httptrigger)可讓您透過 HTTP 要求叫用函式。</span><span class="sxs-lookup"><span data-stu-id="b4281-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="b4281-109">您可以將它自訂來回應 [Webhook](#hooktrigger)。</span><span class="sxs-lookup"><span data-stu-id="b4281-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="b4281-110">[HTTP 輸出繫結](#output)可讓您回應要求。</span><span class="sxs-lookup"><span data-stu-id="b4281-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="b4281-111">HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b4281-111">HTTP trigger</span></span>
<span data-ttu-id="b4281-112">HTTP 觸發程序將會執行您的函式，以回應 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="b4281-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="b4281-113">您可以自訂它來回應特定的 URL 或一組 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="b4281-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="b4281-114">也可以設定 HTTP 觸發程序來回應 Webhook。</span><span class="sxs-lookup"><span data-stu-id="b4281-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="b4281-115">如果使用 Functions 入口網站，您也可以使用預先製作的範本立即開始。</span><span class="sxs-lookup"><span data-stu-id="b4281-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="b4281-116">選取 [新函式] 然後從 [案例] 下拉式清單選擇 [API 與 Webhook]。</span><span class="sxs-lookup"><span data-stu-id="b4281-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="b4281-117">選取其中一個範本，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b4281-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="b4281-118">根據預設，HTTP 觸發程序會以 HTTP 200 OK 的狀態碼和空白主體回應要求。</span><span class="sxs-lookup"><span data-stu-id="b4281-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="b4281-119">若要修改回應，請設定 [HTTP 輸出繫結](#output)</span><span class="sxs-lookup"><span data-stu-id="b4281-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="b4281-120">設定 HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b4281-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="b4281-121">HTTP 觸發程序是藉由在 function.json 的 `bindings` 陣列中包含類似下列的 JSON 物件來定義：</span><span class="sxs-lookup"><span data-stu-id="b4281-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

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
<span data-ttu-id="b4281-122">繫結支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b4281-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="b4281-123">**name**：必要項目，函式程式碼中用於要求或要求主體的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="b4281-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="b4281-124">請參閱[從程式碼使用 HTTP 觸發程序](#httptriggerusage)。</span><span class="sxs-lookup"><span data-stu-id="b4281-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="b4281-125">**type**：必要項目，必須設定為 "httpTrigger"。</span><span class="sxs-lookup"><span data-stu-id="b4281-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="b4281-126">**direction**：必要項目，必須設定為 "in"。</span><span class="sxs-lookup"><span data-stu-id="b4281-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="b4281-127">_authLevel_：這會決定要求上必須存在哪些金鑰 (若有的話) 以叫用函式。</span><span class="sxs-lookup"><span data-stu-id="b4281-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="b4281-128">請參閱下方的[使用金鑰](#keys)。</span><span class="sxs-lookup"><span data-stu-id="b4281-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="b4281-129">值可以是下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="b4281-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="b4281-130">_anonymous_：不需要 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="b4281-131">_function_：需要函式專屬的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="b4281-132">如果沒有提供任何值，此為預設值。</span><span class="sxs-lookup"><span data-stu-id="b4281-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="b4281-133">_admin_：需要主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="b4281-134">**methods**：此為函式將回應的 HTTP 方法陣列。</span><span class="sxs-lookup"><span data-stu-id="b4281-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="b4281-135">如果未指定，函式將會回應所有的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="b4281-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="b4281-136">請參閱[自訂 HTTP 端點](#url)。</span><span class="sxs-lookup"><span data-stu-id="b4281-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="b4281-137">**route**：這會定義路由範本，控制函式將回應哪些要求 URL。</span><span class="sxs-lookup"><span data-stu-id="b4281-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="b4281-138">如果沒有提供任何值，預設值為 `<functionname>`。</span><span class="sxs-lookup"><span data-stu-id="b4281-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="b4281-139">請參閱[自訂 HTTP 端點](#url)。</span><span class="sxs-lookup"><span data-stu-id="b4281-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="b4281-140">**webHookType**：這會設定 HTTP 觸發程序做為指定提供者的 Webhook 接收器。</span><span class="sxs-lookup"><span data-stu-id="b4281-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="b4281-141">如果選擇此項目，則不應設定 _methods_ 屬性。</span><span class="sxs-lookup"><span data-stu-id="b4281-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="b4281-142">請參閱[回應 Webhook](#hooktrigger)。</span><span class="sxs-lookup"><span data-stu-id="b4281-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="b4281-143">值可以是下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="b4281-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="b4281-144">_genericJson_：一般用途的 Webhook 端點，不需要特定提供者的邏輯。</span><span class="sxs-lookup"><span data-stu-id="b4281-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="b4281-145">_github_：函式將回應 GitHub Webhook。</span><span class="sxs-lookup"><span data-stu-id="b4281-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="b4281-146">如果選擇此項目，則不應設定 _authLevel_ 屬性。</span><span class="sxs-lookup"><span data-stu-id="b4281-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="b4281-147">_github_：函式將回應 Slack Webhook。</span><span class="sxs-lookup"><span data-stu-id="b4281-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="b4281-148">如果選擇此項目，則不應設定 _authLevel_ 屬性。</span><span class="sxs-lookup"><span data-stu-id="b4281-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="b4281-149">從程式碼使用 HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b4281-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="b4281-150">針對 C# 和 F# 函式，您可以宣告觸發程序輸入的類型為 `HttpRequestMessage` 或自訂類型。</span><span class="sxs-lookup"><span data-stu-id="b4281-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="b4281-151">如果您選擇 `HttpRequestMessage`，那您將會取得要求物件的完整存取權。</span><span class="sxs-lookup"><span data-stu-id="b4281-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="b4281-152">對於自訂類型 (例如 POCO)，Functions 會嘗試將要求主體剖析為 JSON 以填入物件屬性。</span><span class="sxs-lookup"><span data-stu-id="b4281-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="b4281-153">對於 Node.js 函式，Functions 執行階段提供要求主體而非要求物件。</span><span class="sxs-lookup"><span data-stu-id="b4281-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="b4281-154">請參閱 [HTTP 觸發程序範例](#httptriggersample)以取得範例使用方式。</span><span class="sxs-lookup"><span data-stu-id="b4281-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="b4281-155">HTTP 回應輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b4281-155">HTTP response output binding</span></span>
<span data-ttu-id="b4281-156">使用 HTTP 輸出繫結來回應 HTTP 要求傳送者。</span><span class="sxs-lookup"><span data-stu-id="b4281-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="b4281-157">此繫結需要 HTTP 觸發程序，並可讓您自訂與觸發程序要求相關聯的回應。</span><span class="sxs-lookup"><span data-stu-id="b4281-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="b4281-158">如果沒有提供 HTTP 輸出繫結，HTTP 觸發程序將會傳回 HTTP 200 OK 和空白主體。</span><span class="sxs-lookup"><span data-stu-id="b4281-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="b4281-159">設定 HTTP 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b4281-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="b4281-160">HTTP 輸出繫結是藉由在 function.json 的 `bindings` 陣列中包含類似下列的 JSON 物件來定義：</span><span class="sxs-lookup"><span data-stu-id="b4281-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="b4281-161">繫結包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b4281-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="b4281-162">**name**：必要項目，函式程式碼中用於回應的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="b4281-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="b4281-163">請參閱[從程式碼使用 HTTP 輸出繫結](#outputusage)。</span><span class="sxs-lookup"><span data-stu-id="b4281-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="b4281-164">**type**：必要項目，必須設定為 "http"。</span><span class="sxs-lookup"><span data-stu-id="b4281-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="b4281-165">**direction**：必要項目，必須設定為 "out"。</span><span class="sxs-lookup"><span data-stu-id="b4281-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="b4281-166">從程式碼使用 HTTP 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b4281-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="b4281-167">您可以使用輸出參數 (例如 "res") 來回應 http 或 Webhook 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="b4281-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="b4281-168">或者，您可以使用標準 `Request.CreateResponse()` (C#) 或 `context.res` (Node.JS) 模式來傳回您的回應。</span><span class="sxs-lookup"><span data-stu-id="b4281-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="b4281-169">如需有關如何使用第二個方法的範例，請參閱 [HTTP 觸發程序範例](#httptriggersample)和 [Webhook 觸發程序範例](#hooktriggersample)。</span><span class="sxs-lookup"><span data-stu-id="b4281-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="b4281-170">回應 Webhook</span><span class="sxs-lookup"><span data-stu-id="b4281-170">Responding to webhooks</span></span>
<span data-ttu-id="b4281-171">含有 _webHookType_ 屬性的 HTTP 觸發程序將會設定為回應 [Webhook](https://en.wikipedia.org/wiki/Webhook)。</span><span class="sxs-lookup"><span data-stu-id="b4281-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="b4281-172">基本組態會使用 "genericJson" 設定。</span><span class="sxs-lookup"><span data-stu-id="b4281-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="b4281-173">這會將要求限制為只有那些使用 HTTP POST 和包含 `application/json` 內容類型的要求。</span><span class="sxs-lookup"><span data-stu-id="b4281-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="b4281-174">觸發程序可另外針對特定的 Webhook 提供者進行調整 (例如 [GitHub](https://developer.github.com/webhooks/) 和 [Slack](https://api.slack.com/outgoing-webhooks))。</span><span class="sxs-lookup"><span data-stu-id="b4281-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="b4281-175">如果指定了提供者，Functions 執行階段就可為您處理提供者的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="b4281-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="b4281-176">將 GitHub 設定為 Webhook 提供者</span><span class="sxs-lookup"><span data-stu-id="b4281-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="b4281-177">若要回應 GitHub Webhook，請先建立含有 HTTP 觸發程序的函式，然後將 _webHookType_ 屬性設定為 "github"。</span><span class="sxs-lookup"><span data-stu-id="b4281-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="b4281-178">接著將其 [URL](#url) 和 [API 金鑰](#keys) 複製到您 GitHub 存放庫的 [加入 webhook] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b4281-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="b4281-179">若要深入了解，請參閱 GitHub 的[建立 Webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) 文件。</span><span class="sxs-lookup"><span data-stu-id="b4281-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="b4281-180">將 Slack 設定為 Webhook 提供者</span><span class="sxs-lookup"><span data-stu-id="b4281-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="b4281-181">Slack webhook 會為您產生權杖，而不是由您指定，因此您必須使用 Slack 的權杖來設定函式專屬的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="b4281-182">請參閱[使用金鑰](#keys)。</span><span class="sxs-lookup"><span data-stu-id="b4281-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="b4281-183">自訂 HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="b4281-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="b4281-184">根據預設，當您為 HTTP 觸發程序或 WebHook 建立函式時，將可藉由下列形式的路由來定址該函式：</span><span class="sxs-lookup"><span data-stu-id="b4281-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="b4281-185">您可以在 HTTP 觸發程序的輸入繫結上使用選擇性的 `route` 屬性來自訂此路由。</span><span class="sxs-lookup"><span data-stu-id="b4281-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="b4281-186">舉例來說，下列 *function.json* 檔案定義了 HTTP 觸發程序的 `route` 屬性：</span><span class="sxs-lookup"><span data-stu-id="b4281-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="b4281-187">在使用此設定的情況下，現在便可使用下列路由來定址該函式，而不需使用原始路由。</span><span class="sxs-lookup"><span data-stu-id="b4281-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="b4281-188">這可讓該函式程式碼在位址中支援兩個參數，即 "category" 和 "id"。</span><span class="sxs-lookup"><span data-stu-id="b4281-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="b4281-189">您可以將任何 [Web API 路由條件約束](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints)與您的參數搭配使用。</span><span class="sxs-lookup"><span data-stu-id="b4281-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="b4281-190">下列 C# 函式程式碼會同時利用這兩個參數。</span><span class="sxs-lookup"><span data-stu-id="b4281-190">The following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="b4281-191">以下是使用相同路由參數的 Node.js 函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="b4281-191">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="b4281-192">所有函式路由預設前面都會加上 *api*。</span><span class="sxs-lookup"><span data-stu-id="b4281-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="b4281-193">您也可以在 *host.json* 檔案中使用 `http.routePrefix` 屬性來自訂或移除前置詞。</span><span class="sxs-lookup"><span data-stu-id="b4281-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="b4281-194">下列範例會在 *host.json* 檔案中使用空字串作為前置詞來移除 *api* 路由前置詞。</span><span class="sxs-lookup"><span data-stu-id="b4281-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="b4281-195">如需有關如何更新您函數 *host.json* 檔案的詳細資訊，請參閱[如何更新函數應用程式檔案](functions-reference.md#fileupdate)。</span><span class="sxs-lookup"><span data-stu-id="b4281-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="b4281-196">如需有關您可以在 *host.json* 檔案中設定之其他屬性的資訊，請參閱 [host.json 參考](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。</span><span class="sxs-lookup"><span data-stu-id="b4281-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="b4281-197">使用金鑰</span><span class="sxs-lookup"><span data-stu-id="b4281-197">Working with keys</span></span>
<span data-ttu-id="b4281-198">HttpTriggers 可以利用金鑰來增加安全性。</span><span class="sxs-lookup"><span data-stu-id="b4281-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="b4281-199">標準 HttpTrigger 可以將這些金鑰做為 API 金鑰，要求金鑰必須存在於要求上。</span><span class="sxs-lookup"><span data-stu-id="b4281-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="b4281-200">Webhook 可以以多種方式使用金鑰授權要求，視提供者支援的方式而定。</span><span class="sxs-lookup"><span data-stu-id="b4281-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="b4281-201">金鑰會當作您函數應用程式的一部分儲存於 Azure 中，並在加密後靜置。</span><span class="sxs-lookup"><span data-stu-id="b4281-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="b4281-202">若要檢視您的金鑰，請建立新的金鑰或將金鑰輪替為新的值，瀏覽至入口網站中您的其中一個函式，然後選取 [管理]。</span><span class="sxs-lookup"><span data-stu-id="b4281-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="b4281-203">金鑰類型有兩種：</span><span class="sxs-lookup"><span data-stu-id="b4281-203">There are two types of keys:</span></span>
- <span data-ttu-id="b4281-204">**主機金鑰**：這些金鑰由函數應用程式中所有的函式共用。</span><span class="sxs-lookup"><span data-stu-id="b4281-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="b4281-205">當做為 API 金鑰使用時，這些金鑰會允許存取函數應用程式中的任何函式。</span><span class="sxs-lookup"><span data-stu-id="b4281-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="b4281-206">**函式金鑰**：這些金鑰僅適用於據以定義它們的特定函式。</span><span class="sxs-lookup"><span data-stu-id="b4281-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="b4281-207">當做為 API 金鑰使用時，這些金鑰僅允許存取該函式。</span><span class="sxs-lookup"><span data-stu-id="b4281-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="b4281-208">每個金鑰均為具名以供參考，並且在函式和主機層級有一預設金鑰 (名稱為 "default")。</span><span class="sxs-lookup"><span data-stu-id="b4281-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="b4281-209">「主要金鑰」是預設的主機金鑰，名稱為 "_master"，它是針對每個函數應用程式所定義且無法撤銷。</span><span class="sxs-lookup"><span data-stu-id="b4281-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="b4281-210">它會提供執行階段 API 的系統管理存取權。</span><span class="sxs-lookup"><span data-stu-id="b4281-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="b4281-211">在繫結 JSON 中使用 `"authLevel": "admin"` 會要求此金鑰必須存在於要求上；任何其他金鑰將會導致授權失敗。</span><span class="sxs-lookup"><span data-stu-id="b4281-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="b4281-212">由於主要金鑰會授與提高的權限，因此您不應該與第三方共用此金鑰，或是將它散發到原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4281-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="b4281-213">當您選擇管理授權層級時，請務必謹慎。</span><span class="sxs-lookup"><span data-stu-id="b4281-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="b4281-214">API 金鑰授權</span><span class="sxs-lookup"><span data-stu-id="b4281-214">API key authorization</span></span>
<span data-ttu-id="b4281-215">根據預設，HttpTrigger 會在 HTTP 要求中要求 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="b4281-216">因此您的 HTTP 要求通常看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="b4281-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="b4281-217">金鑰可包含在名為 `code` 的查詢字串變數中 (如上所述)，或是包含在 `x-functions-key` HTTP 標頭中。</span><span class="sxs-lookup"><span data-stu-id="b4281-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="b4281-218">金鑰的值可以是針對函式定義的任何函式金鑰，或是任何主機金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="b4281-219">您可以選擇在不需要金鑰的情況下允許要求，或是指定必須使用主要金鑰，方法是變更繫結 JSON 中的 `authLevel` 屬性 (請參閱 [HTTP 觸發程序](#httptrigger))。</span><span class="sxs-lookup"><span data-stu-id="b4281-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="b4281-220">金鑰和 Webhook</span><span class="sxs-lookup"><span data-stu-id="b4281-220">Keys and webhooks</span></span>
<span data-ttu-id="b4281-221">Webhook 授權是由 Webhook 接收器元件 (HttpTrigger 的一部分) 處理，處理機制則根據 Webhook 的類型而異。</span><span class="sxs-lookup"><span data-stu-id="b4281-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="b4281-222">不過，每個機制都依賴金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="b4281-223">根據預設，將會使用名稱為 "default" 的函式金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="b4281-224">如果您想要使用不同的金鑰，您必須設定 Webhook 提供者以下列其中一種方式將金鑰名稱隨著要求一起傳送：</span><span class="sxs-lookup"><span data-stu-id="b4281-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="b4281-225">**查詢字串**：提供者在 `clientid` 查詢字串參數中傳遞金鑰名稱 (例如 `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`)。</span><span class="sxs-lookup"><span data-stu-id="b4281-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="b4281-226">**要求標頭**︰提供者在 `x-functions-clientid` 標頭中傳遞金鑰名稱。</span><span class="sxs-lookup"><span data-stu-id="b4281-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="b4281-227">函式金鑰的優先順序高於主機金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="b4281-228">如果兩個金鑰是以相同的名稱定義，將會使用函式金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4281-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="b4281-229">HTTP 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b4281-229">HTTP trigger samples</span></span>
<span data-ttu-id="b4281-230">假設您 function.json 的 `bindings` 陣列中有下列 HTTP 觸發程序：</span><span class="sxs-lookup"><span data-stu-id="b4281-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="b4281-231">請參閱在查詢字串或 HTTP 要求主體中尋找 `name` 參數的語言特定範例。</span><span class="sxs-lookup"><span data-stu-id="b4281-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="b4281-232">C#</span><span class="sxs-lookup"><span data-stu-id="b4281-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="b4281-233">F#</span><span class="sxs-lookup"><span data-stu-id="b4281-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="b4281-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="b4281-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="b4281-235">C# 中的 HTTP 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b4281-235">HTTP trigger sample in C#</span></span> #
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

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="b4281-236">您也可以繫結到 POCO，不是 `HttpRequestMessage`。</span><span class="sxs-lookup"><span data-stu-id="b4281-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="b4281-237">這會從要求主體水合，剖析成 JSON。</span><span class="sxs-lookup"><span data-stu-id="b4281-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="b4281-238">同樣地，類型可以傳遞至 HTTP 回應輸出繫結，而這會傳回為狀態碼 200 的回應主體。</span><span class="sxs-lookup"><span data-stu-id="b4281-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="b4281-239">F# 中的 HTTP 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b4281-239">HTTP trigger sample in F#</span></span> #
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="b4281-240">您需要 `project.json` 檔案，以使用 NuGet 來參考 `FSharp.Interop.Dynamic` 和 `Dynamitey` 組件，例如︰</span><span class="sxs-lookup"><span data-stu-id="b4281-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="b4281-241">這會使用 NuGet 來擷取相依性，並會在指令碼中加以參考。</span><span class="sxs-lookup"><span data-stu-id="b4281-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="b4281-242">Node.JS 中的 HTTP 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b4281-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="b4281-243">Webhook 範例</span><span class="sxs-lookup"><span data-stu-id="b4281-243">Webhook samples</span></span>
<span data-ttu-id="b4281-244">假設您 function.json 的`bindings` 陣列中有下列 Webhook 觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="b4281-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="b4281-245">請參閱會記錄 GitHub 問題註解的語言特定範例。</span><span class="sxs-lookup"><span data-stu-id="b4281-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="b4281-246">C#</span><span class="sxs-lookup"><span data-stu-id="b4281-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="b4281-247">F#</span><span class="sxs-lookup"><span data-stu-id="b4281-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="b4281-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="b4281-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="b4281-249">C# 中的 Webhook 範例</span><span class="sxs-lookup"><span data-stu-id="b4281-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="b4281-250">F# 中的 Webhook 範例</span><span class="sxs-lookup"><span data-stu-id="b4281-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="b4281-251">Node.JS 中的 Webhook 範例</span><span class="sxs-lookup"><span data-stu-id="b4281-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="b4281-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4281-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

