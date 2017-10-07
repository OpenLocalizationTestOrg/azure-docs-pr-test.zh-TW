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
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="b99c1-104">Azure Functions HTTP 和 Webhook 繫結</span><span class="sxs-lookup"><span data-stu-id="b99c1-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b99c1-105">這篇文章說明如何 tooconfigure 和 http 的工作觸發程序和 Azure 函式中的繫結。</span><span class="sxs-lookup"><span data-stu-id="b99c1-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="b99c1-106">進行這些動作，您可以使用 Azure 函式 toobuild 無伺服器應用程式開發介面和回應 toowebhooks。</span><span class="sxs-lookup"><span data-stu-id="b99c1-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="b99c1-107">Azure 的函式會提供下列繫結的 hello:</span><span class="sxs-lookup"><span data-stu-id="b99c1-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="b99c1-108">[HTTP 觸發程序](#httptrigger)可讓您透過 HTTP 要求叫用函式。</span><span class="sxs-lookup"><span data-stu-id="b99c1-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="b99c1-109">這可以是自訂的 toorespond 太[webhook](#hooktrigger)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="b99c1-110">[HTTP 輸出繫結](#output)可讓您 toorespond toohello 要求。</span><span class="sxs-lookup"><span data-stu-id="b99c1-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="b99c1-111">HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b99c1-111">HTTP trigger</span></span>
<span data-ttu-id="b99c1-112">hello HTTP 觸發程序將會回應 tooan HTTP 要求中執行您的函式。</span><span class="sxs-lookup"><span data-stu-id="b99c1-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="b99c1-113">您可以加以自訂 toorespond tooa 特定 URL 或一組 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="b99c1-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="b99c1-114">HTTP 觸發程序也可以設定的 toorespond toowebhooks。</span><span class="sxs-lookup"><span data-stu-id="b99c1-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="b99c1-115">如果使用 hello 函式網站，您可以也會開始立即使用 預先製作的範本。</span><span class="sxs-lookup"><span data-stu-id="b99c1-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="b99c1-116">選取**新函式**從 hello"應用程式開發介面 & Webhook"**案例**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="b99c1-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="b99c1-117">選取其中一個 hello 範本，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="b99c1-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="b99c1-118">根據預設，HTTP 觸發程序會回應 toohello 要求空本文與 HTTP 200 「 確定 」 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="b99c1-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="b99c1-119">toomodify hello 回應，設定[HTTP 輸出繫結](#output)</span><span class="sxs-lookup"><span data-stu-id="b99c1-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="b99c1-120">設定 HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b99c1-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="b99c1-121">定義 HTTP 觸發程序包括下列 hello 中 JSON 的物件類似 toohello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="b99c1-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

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
<span data-ttu-id="b99c1-122">hello 繫結支援下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="b99c1-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="b99c1-123">**名稱**： 需要-hello hello 要求或要求主體函式程式碼中使用的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="b99c1-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="b99c1-124">請參閱[從程式碼使用 HTTP 觸發程序](#httptriggerusage)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="b99c1-125">**型別**： 需要-必須設定太"httpTrigger"。</span><span class="sxs-lookup"><span data-stu-id="b99c1-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="b99c1-126">**方向**： 需要-必須是 「 位置 」 太設定。</span><span class="sxs-lookup"><span data-stu-id="b99c1-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="b99c1-127">_authLevel_ ： 這會決定哪些索引鍵，如果有的話，需要 toobe hello 要求上呈現順序 tooinvoke hello 函式中。</span><span class="sxs-lookup"><span data-stu-id="b99c1-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="b99c1-128">請參閱下方的[使用金鑰](#keys)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="b99c1-129">hello 值可以是 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="b99c1-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="b99c1-130">_anonymous_：不需要 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b99c1-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="b99c1-131">_function_：需要函式專屬的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b99c1-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="b99c1-132">如果未提供，這會是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="b99c1-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="b99c1-133">_系統管理員_: hello 主索引鍵為必要。</span><span class="sxs-lookup"><span data-stu-id="b99c1-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="b99c1-134">**方法**： 這是 toowhich hello 函式會回應 hello HTTP 方法的陣列。</span><span class="sxs-lookup"><span data-stu-id="b99c1-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="b99c1-135">如果未指定，hello 函式會回應 tooall HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="b99c1-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="b99c1-136">請參閱[自訂 hello HTTP 端點](#url)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="b99c1-137">**路由**： 這會定義 hello 路由範本，控制 toowhich 要求會回覆您的函式的 Url。</span><span class="sxs-lookup"><span data-stu-id="b99c1-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="b99c1-138">hello 若未提供任何預設值是`<functionname>`。</span><span class="sxs-lookup"><span data-stu-id="b99c1-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="b99c1-139">請參閱[自訂 hello HTTP 端點](#url)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="b99c1-140">**webHookType** ： 這會將 hello HTTP 觸發程序 tooact 設定為 hello 指定提供者的 webhook 線上發生干擾。</span><span class="sxs-lookup"><span data-stu-id="b99c1-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="b99c1-141">hello_方法_屬性不應該設定這個選擇。</span><span class="sxs-lookup"><span data-stu-id="b99c1-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="b99c1-142">請參閱[回應 toowebhooks](#hooktrigger)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="b99c1-143">hello 值可以是 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="b99c1-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="b99c1-144">_genericJson_：一般用途的 Webhook 端點，不需要特定提供者的邏輯。</span><span class="sxs-lookup"><span data-stu-id="b99c1-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="b99c1-145">_github_ : hello 函式會回應 tooGitHub webhook。</span><span class="sxs-lookup"><span data-stu-id="b99c1-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="b99c1-146">hello _authLevel_屬性不應該設定這個選擇。</span><span class="sxs-lookup"><span data-stu-id="b99c1-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="b99c1-147">_slack_ : hello 函式會回應 tooSlack webhook。</span><span class="sxs-lookup"><span data-stu-id="b99c1-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="b99c1-148">hello _authLevel_屬性不應該設定這個選擇。</span><span class="sxs-lookup"><span data-stu-id="b99c1-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="b99c1-149">從程式碼使用 HTTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="b99c1-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="b99c1-150">對於 C# 和 F # 函式，您可以是宣告您的觸發程序輸入 toobe hello 類型`HttpRequestMessage`或自訂型別。</span><span class="sxs-lookup"><span data-stu-id="b99c1-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="b99c1-151">如果您選擇`HttpRequestMessage`，就會得到完整存取 toohello 要求物件。</span><span class="sxs-lookup"><span data-stu-id="b99c1-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="b99c1-152">自訂 （例如 POCO) 類型，函式會嘗試 tooparse hello 要求主體為 JSON toopopulate hello 物件屬性。</span><span class="sxs-lookup"><span data-stu-id="b99c1-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="b99c1-153">Node.js 函式，hello 函式執行階段會提供 hello 要求本文，而不是 hello 要求物件。</span><span class="sxs-lookup"><span data-stu-id="b99c1-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="b99c1-154">請參閱 [HTTP 觸發程序範例](#httptriggersample)以取得範例使用方式。</span><span class="sxs-lookup"><span data-stu-id="b99c1-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="b99c1-155">HTTP 回應輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b99c1-155">HTTP response output binding</span></span>
<span data-ttu-id="b99c1-156">使用 hello HTTP 輸出繫結 toorespond toohello HTTP 要求寄件者。</span><span class="sxs-lookup"><span data-stu-id="b99c1-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="b99c1-157">這個繫結需要 HTTP 觸發程序，並可讓您 toocustomize hello 回應 hello 觸發程序的要求相關聯。</span><span class="sxs-lookup"><span data-stu-id="b99c1-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="b99c1-158">如果沒有提供 HTTP 輸出繫結，HTTP 觸發程序將會傳回 HTTP 200 OK 和空白主體。</span><span class="sxs-lookup"><span data-stu-id="b99c1-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="b99c1-159">設定 HTTP 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b99c1-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="b99c1-160">hello HTTP 輸出繫結定義包含下列 hello 中 JSON 的物件類似 toohello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="b99c1-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="b99c1-161">hello 繫結包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="b99c1-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="b99c1-162">**名稱**： 需要-hello 回應 hello 函式程式碼中使用的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="b99c1-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="b99c1-163">請參閱[從程式碼使用 HTTP 輸出繫結](#outputusage)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="b99c1-164">**型別**： 需要-必須設定太"http"。</span><span class="sxs-lookup"><span data-stu-id="b99c1-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="b99c1-165">**方向**： 需要-必須設定太"out"。</span><span class="sxs-lookup"><span data-stu-id="b99c1-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="b99c1-166">從程式碼使用 HTTP 輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b99c1-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="b99c1-167">您可以使用 hello 輸出參數 (例如，"res 」) toorespond toohello http 或 webhook 呼叫者。</span><span class="sxs-lookup"><span data-stu-id="b99c1-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="b99c1-168">或者，您可以使用標準`Request.CreateResponse()`(C#) 或`context.res`(Node.JS) 模式 tooreturn 您的回應。</span><span class="sxs-lookup"><span data-stu-id="b99c1-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="b99c1-169">如需如何 toouse hello 第二個方法的範例，請參閱[HTTP 觸發程序範例](#httptriggersample)和[Webhook 觸發程序範例](#hooktriggersample)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="b99c1-170">回應 toowebhooks</span><span class="sxs-lookup"><span data-stu-id="b99c1-170">Responding toowebhooks</span></span>
<span data-ttu-id="b99c1-171">HTTP 觸發程序以 hello _webHookType_屬性會設定的 toorespond 太[webhook](https://en.wikipedia.org/wiki/Webhook)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="b99c1-172">hello 基本組態會使用 hello"genericJson 」 設定。</span><span class="sxs-lookup"><span data-stu-id="b99c1-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="b99c1-173">這會限制要求 tooonly 與使用 HTTP POST 和以 hello`application/json`內容類型。</span><span class="sxs-lookup"><span data-stu-id="b99c1-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="b99c1-174">hello 觸發程序可以此外是量身訂做的 tooa webhook 特定提供者 (例如[GitHub](https://developer.github.com/webhooks/)和[Slack](https://api.slack.com/outgoing-webhooks))。</span><span class="sxs-lookup"><span data-stu-id="b99c1-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="b99c1-175">如果指定的提供者，則 hello 函式執行階段將會處理 hello 提供者的驗證邏輯為您。</span><span class="sxs-lookup"><span data-stu-id="b99c1-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="b99c1-176">將 GitHub 設定為 Webhook 提供者</span><span class="sxs-lookup"><span data-stu-id="b99c1-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="b99c1-177">toorespond tooGitHub webhook，第一次使用了 HTTP 觸發程序，建立您的函式，並設定 hello _webHookType_屬性太"github"。</span><span class="sxs-lookup"><span data-stu-id="b99c1-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="b99c1-178">接著將其 [URL](#url) 和 [API 金鑰](#keys) 複製到您 GitHub 存放庫的 [加入 webhook] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b99c1-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="b99c1-179">若要深入了解，請參閱 GitHub 的[建立 Webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) 文件。</span><span class="sxs-lookup"><span data-stu-id="b99c1-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="b99c1-180">將 Slack 設定為 Webhook 提供者</span><span class="sxs-lookup"><span data-stu-id="b99c1-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="b99c1-181">hello Slack 的 webhook 為您產生權杖，而不是讓您指定，因此您必須設定的函式特定金鑰 Slack hello 權杖。</span><span class="sxs-lookup"><span data-stu-id="b99c1-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="b99c1-182">請參閱[使用金鑰](#keys)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="b99c1-183">自訂 hello HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="b99c1-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="b99c1-184">依預設建立 HTTP 觸發程序，或 WebHook，函式時 hello 函式為可定址與 hello 表單的路由：</span><span class="sxs-lookup"><span data-stu-id="b99c1-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="b99c1-185">您可以自訂此路由使用選擇性的 hello `route` hello HTTP 觸發程序上的屬性輸入繫結。</span><span class="sxs-lookup"><span data-stu-id="b99c1-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="b99c1-186">例如，hello 遵循*function.json*檔案會定義`route`HTTP 觸發程序的屬性：</span><span class="sxs-lookup"><span data-stu-id="b99c1-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="b99c1-187">使用此組態，hello 函式現在是可定址以 hello 遵循而不是 hello 原始路由的路由。</span><span class="sxs-lookup"><span data-stu-id="b99c1-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="b99c1-188">這可讓 hello 函式程式碼在 hello 位址、 「 類別目錄 」 和 「 識別碼 」 的 toosupport 兩個參數。</span><span class="sxs-lookup"><span data-stu-id="b99c1-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="b99c1-189">您可以將任何 [Web API 路由條件約束](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints)與您的參數搭配使用。</span><span class="sxs-lookup"><span data-stu-id="b99c1-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="b99c1-190">hello 下列 C# 函式程式碼會使用這兩個參數。</span><span class="sxs-lookup"><span data-stu-id="b99c1-190">hello following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="b99c1-191">以下是相同的路由參數 Node.js 函式程式碼 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="b99c1-191">Here is Node.js function code toouse hello same route parameters.</span></span>

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

<span data-ttu-id="b99c1-192">所有函式路由預設前面都會加上 *api*。</span><span class="sxs-lookup"><span data-stu-id="b99c1-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="b99c1-193">您也可以自訂或移除使用 hello hello 首碼`http.routePrefix`屬性中的您*host.json*檔案。</span><span class="sxs-lookup"><span data-stu-id="b99c1-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="b99c1-194">hello 下列範例會移除 hello *api*路由前置字元，使用空字串 hello 前置詞在 hello *host.json*檔案。</span><span class="sxs-lookup"><span data-stu-id="b99c1-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="b99c1-195">如需詳細資訊 tooupdate hello *host.json*函式，請參閱 < 檔案[tooupdate 運作應用程式檔案的方式](functions-reference.md#fileupdate)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="b99c1-196">如需有關您可以在 *host.json* 檔案中設定之其他屬性的資訊，請參閱 [host.json 參考](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="b99c1-197">使用金鑰</span><span class="sxs-lookup"><span data-stu-id="b99c1-197">Working with keys</span></span>
<span data-ttu-id="b99c1-198">HttpTriggers 可以利用金鑰來增加安全性。</span><span class="sxs-lookup"><span data-stu-id="b99c1-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="b99c1-199">標準 HttpTrigger 可以使用這些 API 金鑰，為需要 hello 金鑰 toobe hello 要求上呈現。</span><span class="sxs-lookup"><span data-stu-id="b99c1-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="b99c1-200">Webhook 可以使用各種不同的方式，根據哪個 hello 提供者支援的索引鍵 tooauthorize 要求。</span><span class="sxs-lookup"><span data-stu-id="b99c1-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="b99c1-201">金鑰會當作您函數應用程式的一部分儲存於 Azure 中，並在加密後靜置。</span><span class="sxs-lookup"><span data-stu-id="b99c1-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="b99c1-202">tooview 您的金鑰，建立新的或復原金鑰 toonew 值、 導覽 tooone hello 入口網站中函式，並選取 「 管理 」。</span><span class="sxs-lookup"><span data-stu-id="b99c1-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="b99c1-203">金鑰類型有兩種：</span><span class="sxs-lookup"><span data-stu-id="b99c1-203">There are two types of keys:</span></span>
- <span data-ttu-id="b99c1-204">**主機金鑰**： 共用這些機碼的 hello 函式應用程式內的所有函式。</span><span class="sxs-lookup"><span data-stu-id="b99c1-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="b99c1-205">API 金鑰當做使用時，這些行為允許 hello 函式應用程式內存取 tooany 函式。</span><span class="sxs-lookup"><span data-stu-id="b99c1-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="b99c1-206">**功能鍵**： 這些金鑰套用只有 toohello 特定函式的定義。</span><span class="sxs-lookup"><span data-stu-id="b99c1-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="b99c1-207">API 金鑰當做使用時，這些只允許存取 toothat 函式。</span><span class="sxs-lookup"><span data-stu-id="b99c1-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="b99c1-208">如需參考，名為每個索引鍵，而且 hello 函式和主機層級沒有 （名為 「 預設 」） 的預設索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b99c1-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="b99c1-209">hello**主要金鑰**預設主機鍵名為"_master 」，為每個函式應用程式定義並無法撤銷。</span><span class="sxs-lookup"><span data-stu-id="b99c1-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="b99c1-210">它會提供系統管理存取權 toohello 執行階段 Api。</span><span class="sxs-lookup"><span data-stu-id="b99c1-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="b99c1-211">使用`"authLevel": "admin"`hello 中繫結 JSON hello 要求上呈現此金鑰 toobe; 任何其他金鑰會導致授權失敗。</span><span class="sxs-lookup"><span data-stu-id="b99c1-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="b99c1-212">到期 toohello 提高權限不應與協力廠商共用此機碼或原生用戶端應用程式，將它發佈以 hello 的主要金鑰，授與權限。</span><span class="sxs-lookup"><span data-stu-id="b99c1-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="b99c1-213">當您選擇 hello 管理員授權層級時，請務必謹慎。</span><span class="sxs-lookup"><span data-stu-id="b99c1-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="b99c1-214">API 金鑰授權</span><span class="sxs-lookup"><span data-stu-id="b99c1-214">API key authorization</span></span>
<span data-ttu-id="b99c1-215">根據預設，HttpTrigger 要求 hello HTTP 要求中的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b99c1-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="b99c1-216">因此您的 HTTP 要求通常看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="b99c1-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="b99c1-217">hello 金鑰可以包含在查詢字串變數，名為`code`、 與以上所述，或可以包含在`x-functions-key`HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="b99c1-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="b99c1-218">hello hello 機碼值可以是定義 hello 函式的任何函式索引鍵或所有主機金鑰。</span><span class="sxs-lookup"><span data-stu-id="b99c1-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="b99c1-219">您可以選擇 tooallow 要求沒有金鑰，或指定該 hello 主要金鑰必須使用藉由變更 hello `authLevel` hello 繫結 JSON 中的屬性 (請參閱[HTTP 觸發程序](#httptrigger))。</span><span class="sxs-lookup"><span data-stu-id="b99c1-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="b99c1-220">金鑰和 Webhook</span><span class="sxs-lookup"><span data-stu-id="b99c1-220">Keys and webhooks</span></span>
<span data-ttu-id="b99c1-221">Webhook 授權則 hello webhook 線上發生干擾元件來處理，hello HttpTrigger 和 hello 機制的一部分而異 hello webhook 型別。</span><span class="sxs-lookup"><span data-stu-id="b99c1-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="b99c1-222">不過，每個機制都依賴金鑰。</span><span class="sxs-lookup"><span data-stu-id="b99c1-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="b99c1-223">根據預設，會使用名為 「 預設 」 的 hello 函式索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b99c1-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="b99c1-224">如果您想 toouse 不同的索引鍵，您需要 tooconfigure hello webhook 提供者 toosend hello 金鑰名稱與 hello 要求 hello 下列方式之一：</span><span class="sxs-lookup"><span data-stu-id="b99c1-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="b99c1-225">**查詢字串**: hello 提供者會將 hello 索引鍵名稱傳入 hello`clientid`查詢字串參數 (例如`https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`)。</span><span class="sxs-lookup"><span data-stu-id="b99c1-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="b99c1-226">**要求標頭**: hello 提供者會將 hello 索引鍵名稱傳入 hello`x-functions-clientid`標頭。</span><span class="sxs-lookup"><span data-stu-id="b99c1-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="b99c1-227">函式金鑰的優先順序高於主機金鑰。</span><span class="sxs-lookup"><span data-stu-id="b99c1-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="b99c1-228">如果兩個索引鍵所定義的名稱相同，hello hello 將使用功能鍵。</span><span class="sxs-lookup"><span data-stu-id="b99c1-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="b99c1-229">HTTP 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b99c1-229">HTTP trigger samples</span></span>
<span data-ttu-id="b99c1-230">假設您有下列 HTTP 觸發程序在 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="b99c1-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="b99c1-231">請參閱 hello 特定語言的範例會求取`name`在 hello 查詢字串或 hello hello HTTP 要求主體中的參數。</span><span class="sxs-lookup"><span data-stu-id="b99c1-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="b99c1-232">C#</span><span class="sxs-lookup"><span data-stu-id="b99c1-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="b99c1-233">F#</span><span class="sxs-lookup"><span data-stu-id="b99c1-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="b99c1-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="b99c1-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="b99c1-235">C# 中的 HTTP 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b99c1-235">HTTP trigger sample in C#</span></span> #
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

<span data-ttu-id="b99c1-236">您也可以繫結 tooa POCO 而不是`HttpRequestMessage`。</span><span class="sxs-lookup"><span data-stu-id="b99c1-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="b99c1-237">這將 hydrated 從 hello hello 要求，剖析成 JSON 主體。</span><span class="sxs-lookup"><span data-stu-id="b99c1-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="b99c1-238">同樣地，toohello HTTP 回應輸出繫結時，可以傳遞類型，這將會傳回 200 狀態碼的 hello 回應主體。</span><span class="sxs-lookup"><span data-stu-id="b99c1-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="b99c1-239">F# 中的 HTTP 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b99c1-239">HTTP trigger sample in F#</span></span> #
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

<span data-ttu-id="b99c1-240">您需要`project.json`，並使用 NuGet tooreference hello`FSharp.Interop.Dynamic`和`Dynamitey`組件，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="b99c1-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="b99c1-241">這將會使用 NuGet toofetch 程式相依性，並將指令碼中參考。</span><span class="sxs-lookup"><span data-stu-id="b99c1-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="b99c1-242">Node.JS 中的 HTTP 觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="b99c1-242">HTTP trigger sample in Node.JS</span></span>
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
## <a name="webhook-samples"></a><span data-ttu-id="b99c1-243">Webhook 範例</span><span class="sxs-lookup"><span data-stu-id="b99c1-243">Webhook samples</span></span>
<span data-ttu-id="b99c1-244">假設您有下列 hello 中的 webhook 觸發程序的 hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="b99c1-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="b99c1-245">請參閱 GitHub 問題註解記錄檔的 hello 特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="b99c1-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="b99c1-246">C#</span><span class="sxs-lookup"><span data-stu-id="b99c1-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="b99c1-247">F#</span><span class="sxs-lookup"><span data-stu-id="b99c1-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="b99c1-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="b99c1-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="b99c1-249">C# 中的 Webhook 範例</span><span class="sxs-lookup"><span data-stu-id="b99c1-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="b99c1-250">F# 中的 Webhook 範例</span><span class="sxs-lookup"><span data-stu-id="b99c1-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="b99c1-251">Node.JS 中的 Webhook 範例</span><span class="sxs-lookup"><span data-stu-id="b99c1-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="b99c1-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b99c1-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

