---
title: "使用 Azure Functions 建立無伺服器 API | Microsoft Docs"
description: "如何使用 Azure Functions 建立無伺服器 API"
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
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="18644-103">使用 Azure Functions 建立無伺服器 API</span><span class="sxs-lookup"><span data-stu-id="18644-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="18644-104">在本教學課程中，您將了解 Azure Functions 如何讓您建置可靈活調整的 API。</span><span class="sxs-lookup"><span data-stu-id="18644-104">In this tutorial you will learn how Azure Functions allows you to build highly-scalable APIs.</span></span> <span data-ttu-id="18644-105">Azure Functions 隨附一組內建的 HTTP 觸發程序和繫結，可讓您以各種語言輕鬆撰寫端點，包括 Node.JS、C# 等。</span><span class="sxs-lookup"><span data-stu-id="18644-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="18644-106">在本教學課程中，您將自訂 HTTP 觸發程序來處理 API 設計中的特定動作。</span><span class="sxs-lookup"><span data-stu-id="18644-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span></span> <span data-ttu-id="18644-107">您也會準備整合 API 與 Azure Functions Proxy，並設定模擬 API，以擴充您的 API。</span><span class="sxs-lookup"><span data-stu-id="18644-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="18644-108">這一切都在 Functions 無伺服器計算環境之上完成，因此，您不必擔心調整資源 - 只需要專注於您的 API 邏輯。</span><span class="sxs-lookup"><span data-stu-id="18644-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18644-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="18644-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="18644-110">產生的函式將用於本教學課程的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="18644-110">The resulting function will be used for the rest of this tutorial.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="18644-111">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="18644-111">Sign in to Azure</span></span>

<span data-ttu-id="18644-112">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="18644-112">Open the Azure portal.</span></span> <span data-ttu-id="18644-113">若要這麼做，請以您的 Azure 帳戶登入 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="18644-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="18644-114">自訂 HTTP 函式</span><span class="sxs-lookup"><span data-stu-id="18644-114">Customize your HTTP function</span></span>

<span data-ttu-id="18644-115">根據預設，HTTP 觸發函式會設定為接受任何 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="18644-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span></span> <span data-ttu-id="18644-116">另外還有 `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>` 格式的預設 URL。</span><span class="sxs-lookup"><span data-stu-id="18644-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="18644-117">如果您遵循快速入門，則 `<funcname>` 可能會像 "HttpTriggerJS1" 一樣。</span><span class="sxs-lookup"><span data-stu-id="18644-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="18644-118">在本節中，您會將函式修改為只回應 `/api/hello` 路由的 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="18644-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="18644-119">在 Azure 入口網站中瀏覽至您的函式。</span><span class="sxs-lookup"><span data-stu-id="18644-119">Navigate to your function in the Azure portal.</span></span> <span data-ttu-id="18644-120">在左側導覽列中，選取 [整合]。</span><span class="sxs-lookup"><span data-stu-id="18644-120">Select **Integrate** in the left navigation.</span></span>

![自訂 HTTP 函式](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="18644-122">使用表格中指定的 HTTP 觸發程序設定。</span><span class="sxs-lookup"><span data-stu-id="18644-122">Use the HTTP trigger settings as specified in the table.</span></span>

| <span data-ttu-id="18644-123">欄位</span><span class="sxs-lookup"><span data-stu-id="18644-123">Field</span></span> | <span data-ttu-id="18644-124">範例值</span><span class="sxs-lookup"><span data-stu-id="18644-124">Sample value</span></span> | <span data-ttu-id="18644-125">說明</span><span class="sxs-lookup"><span data-stu-id="18644-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="18644-126">允許的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="18644-126">Allowed HTTP methods</span></span> | <span data-ttu-id="18644-127">選取的方法</span><span class="sxs-lookup"><span data-stu-id="18644-127">Selected methods</span></span> | <span data-ttu-id="18644-128">決定哪些 HTTP 方法可用來叫用此函式</span><span class="sxs-lookup"><span data-stu-id="18644-128">Determines what HTTP methods may be used to invoke this function</span></span> |
| <span data-ttu-id="18644-129">選取的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="18644-129">Selected HTTP methods</span></span> | <span data-ttu-id="18644-130">GET</span><span class="sxs-lookup"><span data-stu-id="18644-130">GET</span></span> | <span data-ttu-id="18644-131">只允許使用選取的 HTTP 方法來叫用此函式</span><span class="sxs-lookup"><span data-stu-id="18644-131">Allows only selected HTTP methods to be used to invoke this function</span></span> |
| <span data-ttu-id="18644-132">路由範本</span><span class="sxs-lookup"><span data-stu-id="18644-132">Route template</span></span> | <span data-ttu-id="18644-133">/hello</span><span class="sxs-lookup"><span data-stu-id="18644-133">/hello</span></span> | <span data-ttu-id="18644-134">決定使用什麼路由來叫用此函式</span><span class="sxs-lookup"><span data-stu-id="18644-134">Determines what route is used to invoke this function</span></span> |

<span data-ttu-id="18644-135">請注意，您並未在路由範本中包含 `/api` 基底路徑前置詞，因為這是由全域設定來處理。</span><span class="sxs-lookup"><span data-stu-id="18644-135">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="18644-136">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="18644-136">Click **Save**.</span></span>

<span data-ttu-id="18644-137">您可以在 [Azure Functions HTTP 和 webhook 繫結](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint)中，進一步了解自訂 HTTP 函式。</span><span class="sxs-lookup"><span data-stu-id="18644-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="18644-138">測試您的 API</span><span class="sxs-lookup"><span data-stu-id="18644-138">Test your API</span></span>

<span data-ttu-id="18644-139">接下來，測試您的函式，確定可以搭配新的 API 介面一起使用。</span><span class="sxs-lookup"><span data-stu-id="18644-139">Next, test your function to see it working with the new API surface.</span></span>

<span data-ttu-id="18644-140">在左側導覽中按一下函式的名稱，返回開發頁面。</span><span class="sxs-lookup"><span data-stu-id="18644-140">Navigate back to the development page by clicking on the function's name in the left navigation.</span></span>

<span data-ttu-id="18644-141">按一下 [取得函式 URL] 並複製 URL。</span><span class="sxs-lookup"><span data-stu-id="18644-141">Click **Get function URL** and copy the URL.</span></span> <span data-ttu-id="18644-142">您應該會看到它現在使用 `/api/hello` 路由。</span><span class="sxs-lookup"><span data-stu-id="18644-142">You should see that it uses the `/api/hello` route now.</span></span>

<span data-ttu-id="18644-143">將 URL 複製到新的瀏覽器索引標籤或您慣用的 REST 用戶端。</span><span class="sxs-lookup"><span data-stu-id="18644-143">Copy the URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="18644-144">根據預設，瀏覽器會使用 GET。</span><span class="sxs-lookup"><span data-stu-id="18644-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="18644-145">執行函式，確認它可以運作。</span><span class="sxs-lookup"><span data-stu-id="18644-145">Run the function and confirm that it is working.</span></span> <span data-ttu-id="18644-146">您可能需要提供 "name" 參數作為查詢字串，以滿足快速入門程式碼。</span><span class="sxs-lookup"><span data-stu-id="18644-146">You may need to provide the "name" parameter as a query string to satisfy the quickstart code.</span></span>

<span data-ttu-id="18644-147">您也可以嘗試使用另一個 HTTP 方法呼叫端點，以確認不會執行此函式。</span><span class="sxs-lookup"><span data-stu-id="18644-147">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span></span> <span data-ttu-id="18644-148">為此，您必須使用 REST 用戶端，例如 cURL、Postman 或 Fiddler。</span><span class="sxs-lookup"><span data-stu-id="18644-148">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="18644-149">Proxy 概觀</span><span class="sxs-lookup"><span data-stu-id="18644-149">Proxies overview</span></span>

<span data-ttu-id="18644-150">在下一節，您將透過 Proxy 公開您的 API。</span><span class="sxs-lookup"><span data-stu-id="18644-150">In the next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="18644-151">Azure Functions Proxy 是預覽功能，可讓您將要求轉送至其他資源。</span><span class="sxs-lookup"><span data-stu-id="18644-151">Azure Functions Proxies is a preview feature that allows you to forward requests to other resources.</span></span> <span data-ttu-id="18644-152">定義 HTTP 端點就像定義 HTTP 觸發程序一樣，但並不撰寫呼叫該端點時要執行的程式碼，而是提供遠端實作的 URL。</span><span class="sxs-lookup"><span data-stu-id="18644-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span></span> <span data-ttu-id="18644-153">這可讓您將多個 API 來源組成單一 API 介面，讓用戶端輕鬆取用。</span><span class="sxs-lookup"><span data-stu-id="18644-153">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span></span> <span data-ttu-id="18644-154">如果您想要將 API 建置成微服務，這特別有用。</span><span class="sxs-lookup"><span data-stu-id="18644-154">This is particularly useful if you wish to build your API as microservices.</span></span>

<span data-ttu-id="18644-155">Proxy 可以指向任何 HTTP 資源，例如︰</span><span class="sxs-lookup"><span data-stu-id="18644-155">A proxy can point to any HTTP resource, such as:</span></span>
- <span data-ttu-id="18644-156">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="18644-156">Azure Functions</span></span> 
- <span data-ttu-id="18644-157">[Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) 中的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="18644-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="18644-158">[Linux 上的 App Service](https://docs.microsoft.com/azure/app-service/app-service-linux-readme) 中的 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="18644-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="18644-159">其他任何裝載 API</span><span class="sxs-lookup"><span data-stu-id="18644-159">Any other hosted API</span></span>

<span data-ttu-id="18644-160">若要深入了解 Proxy，請參閱[使用 Azure Functions Proxy (預覽)]。</span><span class="sxs-lookup"><span data-stu-id="18644-160">To learn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="18644-161">建立您的第一個 Proxy</span><span class="sxs-lookup"><span data-stu-id="18644-161">Create your first proxy</span></span>

<span data-ttu-id="18644-162">在本節中，您將建立新的 Proxy 作為整個 API 的前端。</span><span class="sxs-lookup"><span data-stu-id="18644-162">In this section, you will create a new proxy which serves as a frontend to your overall API.</span></span> 

### <a name="setting-up-the-frontend-environment"></a><span data-ttu-id="18644-163">設定前端環境</span><span class="sxs-lookup"><span data-stu-id="18644-163">Setting up the frontend environment</span></span>

<span data-ttu-id="18644-164">重複[建立函式應用程式](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app)的步驟建立新的函式應用程式，您將在其中建立您的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="18644-164">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span></span> <span data-ttu-id="18644-165">這個新的應用程式將作為我們 API 的前端，而您先前編輯的函式應用程式將作為後端。</span><span class="sxs-lookup"><span data-stu-id="18644-165">This new app will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="18644-166">在入口網站中瀏覽至新的前端函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="18644-166">Navigate to your new frontend function app in the portal.</span></span>

<span data-ttu-id="18644-167">選取 [Settings] \(設定) 。</span><span class="sxs-lookup"><span data-stu-id="18644-167">Select **Settings**.</span></span> <span data-ttu-id="18644-168">然後，將 [啟用 Azure Functions Proxy (預覽)] 切換為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="18644-168">Then toggle **Enable Azure Functions Proxies (preview)** to "On".</span></span>

<span data-ttu-id="18644-169">選取 [平台設定]，然後選擇 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="18644-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="18644-170">向下捲動至 [應用程式設定]，並使用金鑰 "HELLO_HOST" 建立新的設定。</span><span class="sxs-lookup"><span data-stu-id="18644-170">Scroll down to **App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="18644-171">將值設定為後端函式應用程式的主機，例如 `<YourApp>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="18644-171">Set its value to the host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="18644-172">這是您先前測試 HTTP 函式時複製之 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="18644-172">This is part of the URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="18644-173">稍後，您將在設定中參考這項設定。</span><span class="sxs-lookup"><span data-stu-id="18644-173">You'll reference this setting in the configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="18644-174">建議使用應用程式設定作為主機設定，以避免 Proxy 依賴硬式編碼的環境。</span><span class="sxs-lookup"><span data-stu-id="18644-174">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span></span> <span data-ttu-id="18644-175">使用應用程式設定表示您可以在不同環境之間移動 Proxy 設定，將會套用環境特定的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="18644-175">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span></span>

<span data-ttu-id="18644-176">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="18644-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-the-frontend"></a><span data-ttu-id="18644-177">在前端建立 Proxy</span><span class="sxs-lookup"><span data-stu-id="18644-177">Creating a proxy on the frontend</span></span>

<span data-ttu-id="18644-178">在入口網站中瀏覽回到前端函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="18644-178">Navigate back to your frontend function app in the portal.</span></span>

<span data-ttu-id="18644-179">在左側導覽中，按一下 [Proxy (預覽)] 旁邊的加號 '+'。</span><span class="sxs-lookup"><span data-stu-id="18644-179">In the left-hand navigation, click the plus sign '+' next to "Proxies (preview)".</span></span>

![建立 Proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="18644-181">使用表格中指定的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="18644-181">Use proxy settings as specified in the table.</span></span>

| <span data-ttu-id="18644-182">欄位</span><span class="sxs-lookup"><span data-stu-id="18644-182">Field</span></span> | <span data-ttu-id="18644-183">範例值</span><span class="sxs-lookup"><span data-stu-id="18644-183">Sample value</span></span> | <span data-ttu-id="18644-184">說明</span><span class="sxs-lookup"><span data-stu-id="18644-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="18644-185">名稱</span><span class="sxs-lookup"><span data-stu-id="18644-185">Name</span></span> | <span data-ttu-id="18644-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="18644-186">HelloProxy</span></span> | <span data-ttu-id="18644-187">僅用於管理的易記名稱</span><span class="sxs-lookup"><span data-stu-id="18644-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="18644-188">路由範本</span><span class="sxs-lookup"><span data-stu-id="18644-188">Route template</span></span> | <span data-ttu-id="18644-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="18644-189">/api/hello</span></span> | <span data-ttu-id="18644-190">決定使用什麼路由來叫用此 Proxy</span><span class="sxs-lookup"><span data-stu-id="18644-190">Determines what route is used to invoke this proxy</span></span> |
| <span data-ttu-id="18644-191">後端 URL</span><span class="sxs-lookup"><span data-stu-id="18644-191">Backend URL</span></span> | <span data-ttu-id="18644-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="18644-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="18644-193">指定端點，而其要求應該透過代理</span><span class="sxs-lookup"><span data-stu-id="18644-193">Specifies the endpoint to which the request should be proxied</span></span> |

<span data-ttu-id="18644-194">請注意，Proxy 不提供 `/api` 基底路徑前置詞，這必須加入路由範本中。</span><span class="sxs-lookup"><span data-stu-id="18644-194">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span></span>

<span data-ttu-id="18644-195">`%HELLO_HOST%` 語法會參考您稍早建立的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="18644-195">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span></span> <span data-ttu-id="18644-196">解析後的 URL 會指向您的原始函式。</span><span class="sxs-lookup"><span data-stu-id="18644-196">The resolved URL will point to your original function.</span></span>

<span data-ttu-id="18644-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="18644-197">Click **Create**.</span></span>

<span data-ttu-id="18644-198">您可以複製 Proxy URL，然後在瀏覽器或您最愛的 HTTP 用戶端測試，以試驗新的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="18644-198">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="18644-199">建立模擬 API</span><span class="sxs-lookup"><span data-stu-id="18644-199">Create a mock API</span></span>

<span data-ttu-id="18644-200">接下來，您將使用 Proxy 為您的方案建立模擬 API。</span><span class="sxs-lookup"><span data-stu-id="18644-200">Next, you will use a proxy to create a mock API for your solution.</span></span> <span data-ttu-id="18644-201">這樣可以開始進行用戶端開發，而不需完全實作後端。</span><span class="sxs-lookup"><span data-stu-id="18644-201">This allows client development to progress, without needing the backend fully implemented.</span></span> <span data-ttu-id="18644-202">在開發過程中，稍後您可以建立新的函式應用程式來支援此邏輯，並將您的 Proxy 重新導向此應用程式。</span><span class="sxs-lookup"><span data-stu-id="18644-202">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span></span>

<span data-ttu-id="18644-203">為了建立這個模擬 API，我們將建立新的 proxy，這次會使用 [App Service 編輯器](https://github.com/projectkudu/kudu/wiki/App-Service-Editor)。</span><span class="sxs-lookup"><span data-stu-id="18644-203">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="18644-204">若要開始，請在入口網站中瀏覽至您的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="18644-204">To get started, navigate to your function app in the portal.</span></span> <span data-ttu-id="18644-205">選取 [平台功能]，找出 [App Service 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="18644-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="18644-206">按一下此選項會在新的索引標籤中開啟 App Service 編輯器。</span><span class="sxs-lookup"><span data-stu-id="18644-206">Clicking this will open the App Service Editor in a new tab.</span></span>

<span data-ttu-id="18644-207">在左側導覽中，選取 `proxies.json`。</span><span class="sxs-lookup"><span data-stu-id="18644-207">Select `proxies.json` in the left navigation.</span></span> <span data-ttu-id="18644-208">此檔案儲存您的所有 Proxy 的設定。</span><span class="sxs-lookup"><span data-stu-id="18644-208">This is the file which stores the configuration for all of your proxies.</span></span> <span data-ttu-id="18644-209">如果您使用其中一個 [Functions 部署方法](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)，則這是您在原始檔控制中維護的檔案。</span><span class="sxs-lookup"><span data-stu-id="18644-209">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span></span> <span data-ttu-id="18644-210">若要深入了解此檔案，請參閱 [Proxy 進階組態](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration)。</span><span class="sxs-lookup"><span data-stu-id="18644-210">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="18644-211">如果您到目前為止一直遵循指示操作，則 proxies.json 應該如下所示︰</span><span class="sxs-lookup"><span data-stu-id="18644-211">If you've followed along so far, your proxies.json should look like the following:</span></span>

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

<span data-ttu-id="18644-212">接下來，您將新增模擬 API。</span><span class="sxs-lookup"><span data-stu-id="18644-212">Next you'll add your mock API.</span></span> <span data-ttu-id="18644-213">用下列內容取代 proxies.json 檔案︰</span><span class="sxs-lookup"><span data-stu-id="18644-213">Replace your proxies.json file with the following:</span></span>

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

<span data-ttu-id="18644-214">這會新增 Proxy "GetUserByName"，但不含 backendUri 屬性。</span><span class="sxs-lookup"><span data-stu-id="18644-214">This adds a new proxy, "GetUserByName", without the backendUri property.</span></span> <span data-ttu-id="18644-215">它會使用回應覆寫修改 Proxy 的預設回應，而不是呼叫另一個資源。</span><span class="sxs-lookup"><span data-stu-id="18644-215">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span></span> <span data-ttu-id="18644-216">要求和回應覆寫也可以搭配後端 URL 一起使用。</span><span class="sxs-lookup"><span data-stu-id="18644-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="18644-217">當代理至舊版系統時 (您可能需要修改標頭、查詢參數等)，這特別有用。若要深入了解要求和回應覆寫，請參閱[在 Proxy 中修改要求和回應](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses)。</span><span class="sxs-lookup"><span data-stu-id="18644-217">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="18644-218">使用瀏覽器或您最愛的 REST 用戶端呼叫 `/api/users/{username}` 端點，以測試您的模擬 API。</span><span class="sxs-lookup"><span data-stu-id="18644-218">Test your mock API by calling the `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="18644-219">請務必以代表使用者名稱的字串值取代 _{username}_。</span><span class="sxs-lookup"><span data-stu-id="18644-219">Be sure to replace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18644-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18644-220">Next steps</span></span>

<span data-ttu-id="18644-221">在本教學課程中，您學到如何在 Azure Functions 上建置和自訂 API。</span><span class="sxs-lookup"><span data-stu-id="18644-221">In this tutorial, you learned how to build and customize an API on Azure Functions.</span></span> <span data-ttu-id="18644-222">您也學到如何將多個 API (包括模擬) 組合成統一的 API 介面。</span><span class="sxs-lookup"><span data-stu-id="18644-222">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="18644-223">不論多麼複雜的 API 都可以使用這些技術來建置，而且都在 Azure Functions 提供的無伺服器計算模型上執行。</span><span class="sxs-lookup"><span data-stu-id="18644-223">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="18644-224">進一步開發您的 API 時，下列參考可能很有幫助︰</span><span class="sxs-lookup"><span data-stu-id="18644-224">The following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="18644-225">Azure Functions HTTP 和 webhook 繫結</span><span class="sxs-lookup"><span data-stu-id="18644-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="18644-226">[使用 Azure Functions Proxy (預覽)]</span><span class="sxs-lookup"><span data-stu-id="18644-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="18644-227">定義 Azure Functions API (預覽)</span><span class="sxs-lookup"><span data-stu-id="18644-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[使用 Azure Functions Proxy (預覽)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
