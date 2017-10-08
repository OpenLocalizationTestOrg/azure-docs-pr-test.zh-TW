---
title: "使用 Azure 函式的無伺服器 API aaaCreate |Microsoft 文件"
description: "如何 toocreate 無伺服器應用程式開發介面使用 Azure 函式"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="a5744-103">使用 Azure Functions 建立無伺服器 API</span><span class="sxs-lookup"><span data-stu-id="a5744-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="a5744-104">在本教學課程中您將學習如何 Azure 函式可讓您 toobuild 高擴充性 Api。</span><span class="sxs-lookup"><span data-stu-id="a5744-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="a5744-105">Azure 功能中各種不同的語言，包括 Node.JS、 C# 中，以及更多的端點隨附內建 HTTP 觸發程序和更容易 tooauthor 繫結的集合。</span><span class="sxs-lookup"><span data-stu-id="a5744-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="a5744-106">在本教學課程中，您將在您的應用程式開發介面設計自訂 HTTP 觸發程序 toohandle 特定動作。</span><span class="sxs-lookup"><span data-stu-id="a5744-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="a5744-107">您也會準備整合 API 與 Azure Functions Proxy，並設定模擬 API，以擴充您的 API。</span><span class="sxs-lookup"><span data-stu-id="a5744-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="a5744-108">這些全部都被完成之上 hello 函式無伺服器計算環境中，因此您不需要調整規模資源 tooworry-您可只著重於您應用程式開發介面的邏輯。</span><span class="sxs-lookup"><span data-stu-id="a5744-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5744-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="a5744-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="a5744-110">hello 產生函式將用於本教學課程的 hello rest。</span><span class="sxs-lookup"><span data-stu-id="a5744-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="a5744-111">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a5744-111">Sign in tooAzure</span></span>

<span data-ttu-id="a5744-112">開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a5744-112">Open hello Azure portal.</span></span> <span data-ttu-id="a5744-113">toodo，登入太[https://portal.azure.com](https://portal.azure.com)與 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a5744-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="a5744-114">自訂 HTTP 函式</span><span class="sxs-lookup"><span data-stu-id="a5744-114">Customize your HTTP function</span></span>

<span data-ttu-id="a5744-115">根據預設，您 HTTP 觸發的函式是設定的 tooaccept 任何 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="a5744-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="a5744-116">另外還有 hello 表單的預設 URL `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`。</span><span class="sxs-lookup"><span data-stu-id="a5744-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="a5744-117">如果您遵循 hello 快速入門中，然後`<funcname>`可能類似 「 HttpTriggerJS1"。</span><span class="sxs-lookup"><span data-stu-id="a5744-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="a5744-118">在本節中，您將修改對 hello 函式 toorespond 只有 tooGET 要求`/api/hello`改為路由。</span><span class="sxs-lookup"><span data-stu-id="a5744-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="a5744-119">瀏覽 tooyour hello Azure 入口網站中的函式。</span><span class="sxs-lookup"><span data-stu-id="a5744-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="a5744-120">選取**整合**在 hello 左瀏覽。</span><span class="sxs-lookup"><span data-stu-id="a5744-120">Select **Integrate** in hello left navigation.</span></span>

![自訂 HTTP 函式](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="a5744-122">使用 HTTP 觸發程序設定 hello 資料表中所指定。</span><span class="sxs-lookup"><span data-stu-id="a5744-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="a5744-123">欄位</span><span class="sxs-lookup"><span data-stu-id="a5744-123">Field</span></span> | <span data-ttu-id="a5744-124">範例值</span><span class="sxs-lookup"><span data-stu-id="a5744-124">Sample value</span></span> | <span data-ttu-id="a5744-125">說明</span><span class="sxs-lookup"><span data-stu-id="a5744-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="a5744-126">允許的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="a5744-126">Allowed HTTP methods</span></span> | <span data-ttu-id="a5744-127">選取的方法</span><span class="sxs-lookup"><span data-stu-id="a5744-127">Selected methods</span></span> | <span data-ttu-id="a5744-128">判斷哪些 HTTP 方法可能使用的 tooinvoke 此函式</span><span class="sxs-lookup"><span data-stu-id="a5744-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="a5744-129">選取的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="a5744-129">Selected HTTP methods</span></span> | <span data-ttu-id="a5744-130">GET</span><span class="sxs-lookup"><span data-stu-id="a5744-130">GET</span></span> | <span data-ttu-id="a5744-131">可讓您只選取的 HTTP 方法 toobe 用 tooinvoke 此函式</span><span class="sxs-lookup"><span data-stu-id="a5744-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="a5744-132">路由範本</span><span class="sxs-lookup"><span data-stu-id="a5744-132">Route template</span></span> | <span data-ttu-id="a5744-133">/hello</span><span class="sxs-lookup"><span data-stu-id="a5744-133">/hello</span></span> | <span data-ttu-id="a5744-134">決定哪些路由會使用的 tooinvoke 此函式</span><span class="sxs-lookup"><span data-stu-id="a5744-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="a5744-135">請注意您未包含 hello`/api`基底路徑前置詞在 hello 路由範本中，因為這由全域設定。</span><span class="sxs-lookup"><span data-stu-id="a5744-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="a5744-136">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a5744-136">Click **Save**.</span></span>

<span data-ttu-id="a5744-137">您可以在 [Azure Functions HTTP 和 webhook 繫結](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint)中，進一步了解自訂 HTTP 函式。</span><span class="sxs-lookup"><span data-stu-id="a5744-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="a5744-138">測試您的 API</span><span class="sxs-lookup"><span data-stu-id="a5744-138">Test your API</span></span>

<span data-ttu-id="a5744-139">接著，測試函式 toosee hello 新 API 介面使用它。</span><span class="sxs-lookup"><span data-stu-id="a5744-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="a5744-140">在左瀏覽的 hello 的 hello 函式的名稱上按一下瀏覽後 toohello 開發頁面。</span><span class="sxs-lookup"><span data-stu-id="a5744-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="a5744-141">按一下**取得函式 URL**和複製 hello URL。</span><span class="sxs-lookup"><span data-stu-id="a5744-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="a5744-142">您應該會看到它會使用 hello`/api/hello`現在路由。</span><span class="sxs-lookup"><span data-stu-id="a5744-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="a5744-143">Hello URL 複製到新的瀏覽器索引標籤或您慣用的 REST 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a5744-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="a5744-144">根據預設，瀏覽器會使用 GET。</span><span class="sxs-lookup"><span data-stu-id="a5744-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="a5744-145">執行 hello 函式並確認它可運作。</span><span class="sxs-lookup"><span data-stu-id="a5744-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="a5744-146">您可能需要 tooprovide hello 「 名稱 」 參數查詢字串 toosatisfy hello 快速入門的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a5744-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="a5744-147">您也可以嘗試呼叫 hello 與另一個 HTTP 方法 tooconfirm hello 函式不會執行的端點。</span><span class="sxs-lookup"><span data-stu-id="a5744-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="a5744-148">這麼做，您將需要 toouse REST 用戶端，例如 cURL、 郵差或 Fiddler。</span><span class="sxs-lookup"><span data-stu-id="a5744-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="a5744-149">Proxy 概觀</span><span class="sxs-lookup"><span data-stu-id="a5744-149">Proxies overview</span></span>

<span data-ttu-id="a5744-150">在 hello 下一步 區段中，您就會出現您透過 proxy 的 API。</span><span class="sxs-lookup"><span data-stu-id="a5744-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="a5744-151">Azure 的函式 Proxy 是預覽功能，可讓您 tooforward 要求 tooother 資源。</span><span class="sxs-lookup"><span data-stu-id="a5744-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="a5744-152">您定義的 HTTP 端點類似 HTTP 觸發程序，但不需要撰寫程式碼 tooexecute，呼叫該端點時，您可以提供 URL tooa 遠端實作。</span><span class="sxs-lookup"><span data-stu-id="a5744-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="a5744-153">這可讓您 toocompose 成單一的 API 介面，如用戶端 tooconsume 輕鬆來源的多個應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a5744-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="a5744-154">這是特別有用，如果您想 toobuild microservices 為您的 API。</span><span class="sxs-lookup"><span data-stu-id="a5744-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="a5744-155">Proxy 可以指向 tooany HTTP 資源，例如：</span><span class="sxs-lookup"><span data-stu-id="a5744-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="a5744-156">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a5744-156">Azure Functions</span></span> 
- <span data-ttu-id="a5744-157">[Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) 中的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="a5744-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="a5744-158">[Linux 上的 App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme) 中的 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="a5744-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="a5744-159">其他任何裝載 API</span><span class="sxs-lookup"><span data-stu-id="a5744-159">Any other hosted API</span></span>

<span data-ttu-id="a5744-160">toolearn 深入了解 proxy，請參閱[使用 Azure （預覽） 的函式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="a5744-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="a5744-161">建立您的第一個 Proxy</span><span class="sxs-lookup"><span data-stu-id="a5744-161">Create your first proxy</span></span>

<span data-ttu-id="a5744-162">在本節中，您將建立新的 proxy 哪些可做為前端 tooyour 整體應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a5744-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="a5744-163">設定 hello 前端環境</span><span class="sxs-lookup"><span data-stu-id="a5744-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="a5744-164">重覆步驟 hello[建立函式的應用程式](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app)toocreate 新的函式應用程式在您將建立您的 proxy。</span><span class="sxs-lookup"><span data-stu-id="a5744-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="a5744-165">這個新的應用程式時，將做為 hello 前端上，我們的 api，以及您先前已編輯的 hello 函式應用程式將做為後端。</span><span class="sxs-lookup"><span data-stu-id="a5744-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="a5744-166">瀏覽 tooyour 新前端函式的應用程式在 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a5744-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="a5744-167">選取 [Settings] \(設定) 。</span><span class="sxs-lookup"><span data-stu-id="a5744-167">Select **Settings**.</span></span> <span data-ttu-id="a5744-168">然後切換**啟用 Azure 函式 Proxy （預覽）**太 「 On 」。</span><span class="sxs-lookup"><span data-stu-id="a5744-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="a5744-169">選取 [平台設定]，然後選擇 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="a5744-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="a5744-170">向下捲動太**應用程式設定**並建立新的設定與索引鍵 」 HELLO_HOST"。</span><span class="sxs-lookup"><span data-stu-id="a5744-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="a5744-171">設定函式應用程式後端，其值 toohello 主機例如`<YourApp>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="a5744-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="a5744-172">這是您之前複製測試您的 HTTP 函式時的 hello URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="a5744-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="a5744-173">您將參考此設定在 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a5744-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="a5744-174">應用程式設定被建議 hello 主機組態 tooprevent hello proxy 的硬式編碼環境相依性。</span><span class="sxs-lookup"><span data-stu-id="a5744-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="a5744-175">使用應用程式設定時，表示您可以在不同環境間移動 hello proxy 組態，而且 hello 環境專屬的應用程式設定會套用。</span><span class="sxs-lookup"><span data-stu-id="a5744-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="a5744-176">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a5744-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="a5744-177">建立 hello 前端上的 proxy</span><span class="sxs-lookup"><span data-stu-id="a5744-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="a5744-178">瀏覽 hello 入口網站中的上一頁 tooyour 前端函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5744-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="a5744-179">在 [hello 左側導覽中，按一下 hello '+' 下一步] 再加上正負號太"Proxy （預覽） 」。</span><span class="sxs-lookup"><span data-stu-id="a5744-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![建立 Proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="a5744-181">使用 hello 資料表中所指定的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a5744-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="a5744-182">欄位</span><span class="sxs-lookup"><span data-stu-id="a5744-182">Field</span></span> | <span data-ttu-id="a5744-183">範例值</span><span class="sxs-lookup"><span data-stu-id="a5744-183">Sample value</span></span> | <span data-ttu-id="a5744-184">說明</span><span class="sxs-lookup"><span data-stu-id="a5744-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="a5744-185">名稱</span><span class="sxs-lookup"><span data-stu-id="a5744-185">Name</span></span> | <span data-ttu-id="a5744-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="a5744-186">HelloProxy</span></span> | <span data-ttu-id="a5744-187">僅用於管理的易記名稱</span><span class="sxs-lookup"><span data-stu-id="a5744-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="a5744-188">路由範本</span><span class="sxs-lookup"><span data-stu-id="a5744-188">Route template</span></span> | <span data-ttu-id="a5744-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="a5744-189">/api/hello</span></span> | <span data-ttu-id="a5744-190">決定哪些路由會使用的 tooinvoke 這個 proxy</span><span class="sxs-lookup"><span data-stu-id="a5744-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="a5744-191">後端 URL</span><span class="sxs-lookup"><span data-stu-id="a5744-191">Backend URL</span></span> | <span data-ttu-id="a5744-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="a5744-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="a5744-193">指定應該代理 hello 端點 toowhich hello 要求</span><span class="sxs-lookup"><span data-stu-id="a5744-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="a5744-194">請注意，Proxy 不提供 hello`/api`基底路徑前置詞，而且此包含在 hello 路由範本。</span><span class="sxs-lookup"><span data-stu-id="a5744-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="a5744-195">hello`%HELLO_HOST%`語法會參考您稍早建立的 hello 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="a5744-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="a5744-196">hello 解析 URL 將會為 tooyour 原始函式。</span><span class="sxs-lookup"><span data-stu-id="a5744-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="a5744-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a5744-197">Click **Create**.</span></span>

<span data-ttu-id="a5744-198">藉由複製 hello Proxy URL 並測試它 hello 瀏覽器中，或使用您最愛的 HTTP 用戶端，您可以試用新的 proxy。</span><span class="sxs-lookup"><span data-stu-id="a5744-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="a5744-199">建立模擬 API</span><span class="sxs-lookup"><span data-stu-id="a5744-199">Create a mock API</span></span>

<span data-ttu-id="a5744-200">接下來，您將使用 proxy toocreate 模擬的 API，為您的方案。</span><span class="sxs-lookup"><span data-stu-id="a5744-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="a5744-201">這可讓用戶端開發 tooprogress，而不需完全實作的 hello 後端。</span><span class="sxs-lookup"><span data-stu-id="a5744-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="a5744-202">稍後在開發中，您無法建立新的函式應用程式可支援此邏輯，並重新導向 proxy tooit。</span><span class="sxs-lookup"><span data-stu-id="a5744-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="a5744-203">toocreate 這模擬應用程式開發介面中，我們將建立新的 proxy，這次使用 hello[應用程式服務編輯器](https://github.com/projectkudu/kudu/wiki/App-Service-Editor)。</span><span class="sxs-lookup"><span data-stu-id="a5744-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="a5744-204">tooget 啟動，瀏覽 tooyour hello 入口網站中的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5744-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="a5744-205">選取 [平台功能]，找出 [App Service 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="a5744-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="a5744-206">按一下此按鈕會在新的索引標籤中開啟 hello 應用程式服務的編輯器。</span><span class="sxs-lookup"><span data-stu-id="a5744-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="a5744-207">選取`proxies.json`在 hello 左瀏覽。</span><span class="sxs-lookup"><span data-stu-id="a5744-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="a5744-208">這是用於儲存所有您的 proxy hello 組態 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5744-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="a5744-209">如果您使用其中一個 hello[函式的部署方法](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)，這是您將會維護原始檔控制中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5744-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="a5744-210">toolearn 進一步了解此檔案，請參閱[Proxy 進階組態](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration)。</span><span class="sxs-lookup"><span data-stu-id="a5744-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="a5744-211">如果您有跟著到目前為止，您 proxies.json 看起來應該類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a5744-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="a5744-212">接下來，您將新增模擬 API。</span><span class="sxs-lookup"><span data-stu-id="a5744-212">Next you'll add your mock API.</span></span> <span data-ttu-id="a5744-213">取代 hello 下列 proxies.json 檔案：</span><span class="sxs-lookup"><span data-stu-id="a5744-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="a5744-214">這會將新的 proxy，"GetUserByName"，沒有 hello backendUri 內容。</span><span class="sxs-lookup"><span data-stu-id="a5744-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="a5744-215">而不是呼叫另一個資源，它會修改 hello Proxy 使用的回應覆寫預設回應。</span><span class="sxs-lookup"><span data-stu-id="a5744-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="a5744-216">要求和回應覆寫也可以搭配後端 URL 一起使用。</span><span class="sxs-lookup"><span data-stu-id="a5744-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="a5744-217">這是特別有用，當 proxy 處理 tooa 舊有系統，其中，您可能需要 toomodify 標頭、 查詢參數等 toolearn 深入了解要求和回應的覆寫，請參閱[修改要求和回應 Proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses)。</span><span class="sxs-lookup"><span data-stu-id="a5744-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="a5744-218">測試您模擬的 API 呼叫 hello`/api/users/{username}`使用瀏覽器或您最愛的 REST 用戶端端點。</span><span class="sxs-lookup"><span data-stu-id="a5744-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="a5744-219">要確定 tooreplace _{username}_與字串值，表示使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a5744-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5744-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5744-220">Next steps</span></span>

<span data-ttu-id="a5744-221">在本教學課程中，您學到如何 toobuild 和自訂 Azure 函式上的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a5744-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="a5744-222">您也學到如何 toobring 多個 Api，包括 mocks，同時以統一的 API 介面的形式。</span><span class="sxs-lookup"><span data-stu-id="a5744-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="a5744-223">您可以使用這些技術 toobuild，任何複雜度的 Api 時，所有 hello 無伺服器上執行時計算模型提供的 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="a5744-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="a5744-224">hello 下列參考可能會很有用，因為您在開發您的 API，進一步：</span><span class="sxs-lookup"><span data-stu-id="a5744-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="a5744-225">Azure Functions HTTP 和 webhook 繫結</span><span class="sxs-lookup"><span data-stu-id="a5744-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="a5744-226">[使用 Azure （預覽） 的函式 Proxy]</span><span class="sxs-lookup"><span data-stu-id="a5744-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="a5744-227">定義 Azure Functions API (預覽)</span><span class="sxs-lookup"><span data-stu-id="a5744-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[使用 Azure （預覽） 的函式 Proxy]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
