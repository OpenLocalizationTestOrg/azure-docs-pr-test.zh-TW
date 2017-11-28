---
title: "使用 Azure 功能中的 proxy aaaWork |Microsoft 文件"
description: "概觀 toouse Azure 函式的 Proxy"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="f1efd-103">使用 Azure Functions Proxy (預覽)</span><span class="sxs-lookup"><span data-stu-id="f1efd-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="f1efd-104">Azure Functions Proxy 目前為預覽版。</span><span class="sxs-lookup"><span data-stu-id="f1efd-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="f1efd-105">雖然在預覽中，但是標準函式計費適用於 tooproxy 執行，它是免費的。</span><span class="sxs-lookup"><span data-stu-id="f1efd-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="f1efd-106">如需詳細資訊，請參閱 [Azure Functions 價格](https://azure.microsoft.com/pricing/details/functions/)。</span><span class="sxs-lookup"><span data-stu-id="f1efd-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="f1efd-107">這篇文章說明如何 tooconfigure 地使用 Azure 函式的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="f1efd-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="f1efd-108">這項功能可讓您在函式應用程式上指定由其他資源所實作的端點。</span><span class="sxs-lookup"><span data-stu-id="f1efd-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="f1efd-109">您可以使用到多個函式應用程式 （如所示的微服務架構），這些 proxy toobreak 大型的應用程式開發介面時，仍單一的 API 介面的用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1efd-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="f1efd-110"><a name="enable"></a>啟用 Azure Functions Proxy</span><span class="sxs-lookup"><span data-stu-id="f1efd-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="f1efd-111">預設不會啟用 Proxy。</span><span class="sxs-lookup"><span data-stu-id="f1efd-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="f1efd-112">Hello 功能已停用，但是它們不會執行，您可以建立 proxy。</span><span class="sxs-lookup"><span data-stu-id="f1efd-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="f1efd-113">tooenable proxy hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="f1efd-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="f1efd-114">開啟 hello [Azure 入口網站]，並前往 tooyour 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1efd-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="f1efd-115">選取 [函式應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="f1efd-116">交換器**啟用 Azure 函式 Proxy （預覽）**太**上**。</span><span class="sxs-lookup"><span data-stu-id="f1efd-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="f1efd-117">您也可以傳回以下 tooupdate hello proxy 執行階段可用時的新功能。</span><span class="sxs-lookup"><span data-stu-id="f1efd-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="f1efd-118"><a name="create"></a>建立 Proxy</span><span class="sxs-lookup"><span data-stu-id="f1efd-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="f1efd-119">本節說明如何 toocreate proxy 中的 hello 函式的入口網站。</span><span class="sxs-lookup"><span data-stu-id="f1efd-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="f1efd-120">開啟 hello [Azure 入口網站]，並前往 tooyour 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1efd-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="f1efd-121">Hello 左窗格中，選取**新 proxy**。</span><span class="sxs-lookup"><span data-stu-id="f1efd-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="f1efd-122">為您的 Proxy 提供名稱。</span><span class="sxs-lookup"><span data-stu-id="f1efd-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="f1efd-123">此函式應用程式上設定 hello 端點所公開，藉由指定 hello**路由範本**和**HTTP 方法**。</span><span class="sxs-lookup"><span data-stu-id="f1efd-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="f1efd-124">這些參數的運作方式的相應 toohello 規則[HTTP 觸發程序]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="f1efd-125">設定 hello**後端 URL** tooanother 端點。</span><span class="sxs-lookup"><span data-stu-id="f1efd-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="f1efd-126">此端點可能是另一個函式應用程式中的函式，也可能是任何其他 API。</span><span class="sxs-lookup"><span data-stu-id="f1efd-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="f1efd-127">hello 值不需要 toobe 靜態，而且可以參考[應用程式設定]和[來自原始用戶端要求 hello 參數]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="f1efd-128">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f1efd-128">Click **Create**.</span></span>

<span data-ttu-id="f1efd-129">您的 Proxy 現在會存在做為函式應用程式上的新端點。</span><span class="sxs-lookup"><span data-stu-id="f1efd-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="f1efd-130">用戶端的觀點而言，它是對等 tooan HttpTrigger Azure 函式中。</span><span class="sxs-lookup"><span data-stu-id="f1efd-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="f1efd-131">藉由複製 hello Proxy URL，並使用您最愛的 HTTP 用戶端來測試它，您可以試用新的 proxy。</span><span class="sxs-lookup"><span data-stu-id="f1efd-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="f1efd-132"><a name="modify-requests-responses"></a>修改要求和回應</span><span class="sxs-lookup"><span data-stu-id="f1efd-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="f1efd-133">使用 Azure 函式的 Proxy，您可以修改要求 tooand 回應 hello 後端。</span><span class="sxs-lookup"><span data-stu-id="f1efd-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="f1efd-134">這些轉換可以利用[使用變數]中所定義的變數。</span><span class="sxs-lookup"><span data-stu-id="f1efd-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="f1efd-135"><a name="modify-backend-request"></a>修改 hello 後端要求</span><span class="sxs-lookup"><span data-stu-id="f1efd-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="f1efd-136">根據預設，hello 後端要求會初始化為 hello 原始要求的複本。</span><span class="sxs-lookup"><span data-stu-id="f1efd-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="f1efd-137">此外 toosetting hello 後端 URL，您可以進行變更 toohello HTTP 方法、 標頭和查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="f1efd-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="f1efd-138">hello 修改的值可以參考[應用程式設定]和[來自原始用戶端要求 hello 參數]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="f1efd-139">目前，尚無修改後端要求的入口網站體驗。</span><span class="sxs-lookup"><span data-stu-id="f1efd-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="f1efd-140">toolearn 如何 tooapply 這項功能，從 proxies.json，請參閱[定義 requestOverrides 物件]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="f1efd-141"><a name="modify-response"></a>修改 hello 回應</span><span class="sxs-lookup"><span data-stu-id="f1efd-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="f1efd-142">根據預設，hello 用戶端的回應會初始化為 hello 後端回應的複本。</span><span class="sxs-lookup"><span data-stu-id="f1efd-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="f1efd-143">您可以進行變更 toohello 回應的狀態碼、 原因片語、 標頭和主體。</span><span class="sxs-lookup"><span data-stu-id="f1efd-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="f1efd-144">hello 修改的值可以參考[應用程式設定]，[來自原始用戶端要求 hello 參數]，和[hello 後端回應來自參數]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="f1efd-145">目前，尚無修改回應的入口網站體驗。</span><span class="sxs-lookup"><span data-stu-id="f1efd-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="f1efd-146">toolearn 如何 tooapply 這項功能，從 proxies.json，請參閱[定義 responseOverrides 物件]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="f1efd-147"><a name="using-variables"></a>使用變數</span><span class="sxs-lookup"><span data-stu-id="f1efd-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="f1efd-148">hello 組態 proxy 不需要 toobe 靜態。</span><span class="sxs-lookup"><span data-stu-id="f1efd-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="f1efd-149">您可以條件 toouse 變數從 hello 原始要求、 hello 後端回應或應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="f1efd-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="f1efd-150"><a name="request-parameters"></a>參考要求參數</span><span class="sxs-lookup"><span data-stu-id="f1efd-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="f1efd-151">輸入 toohello 後端 URL 屬性或修改要求和回應的一部分，您可以使用要求參數。</span><span class="sxs-lookup"><span data-stu-id="f1efd-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="f1efd-152">某些參數可以從 hello 路由範本中 hello 基底的 proxy 設定，指定繫結和其他人可以來自 hello 連入要求的屬性。</span><span class="sxs-lookup"><span data-stu-id="f1efd-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="f1efd-153">路由範本參數</span><span class="sxs-lookup"><span data-stu-id="f1efd-153">Route template parameters</span></span>
<span data-ttu-id="f1efd-154">Hello 路由範本中使用的參數都是由名稱所參考的可用 toobe。</span><span class="sxs-lookup"><span data-stu-id="f1efd-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="f1efd-155">hello 參數名稱會放在大括號 （{}）。</span><span class="sxs-lookup"><span data-stu-id="f1efd-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="f1efd-156">例如，如果 proxy 有路由範本，例如`/pets/{petId}`，hello 後端 URL 可以包含 hello 值`{petId}`，如同在`https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`。</span><span class="sxs-lookup"><span data-stu-id="f1efd-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="f1efd-157">如果 hello 路由範本就會終止中使用萬用字元，例如`/api/{*restOfPath}`，hello 值`{restOfPath}`是 hello 剩餘 hello 連入要求來自路徑片段的字串表示法。</span><span class="sxs-lookup"><span data-stu-id="f1efd-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="f1efd-158">其他要求參數</span><span class="sxs-lookup"><span data-stu-id="f1efd-158">Additional request parameters</span></span>
<span data-ttu-id="f1efd-159">此外 toohello 路由範本參數，hello 值可用於組態值：</span><span class="sxs-lookup"><span data-stu-id="f1efd-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="f1efd-160">**{request.method}**: hello hello 原始要求使用的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f1efd-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="f1efd-161">**{request.headers。\<HeaderName\>}**： 可讀取 hello 原始要求的標頭。</span><span class="sxs-lookup"><span data-stu-id="f1efd-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="f1efd-162">取代 *\<HeaderName\>*  hello 想 tooread hello 標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="f1efd-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="f1efd-163">如果 hello 標頭未包含在 hello 要求，hello 值會是 hello 空字串。</span><span class="sxs-lookup"><span data-stu-id="f1efd-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="f1efd-164">**{request.querystring。\<ParameterName\>}**： 可讀取 hello 原始要求的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="f1efd-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="f1efd-165">取代 *\<ParameterName\>*  hello 想 tooread hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="f1efd-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="f1efd-166">如果在 hello 要求不包含 hello 參數，hello 值會是 hello 空字串。</span><span class="sxs-lookup"><span data-stu-id="f1efd-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="f1efd-167"><a name="response-parameters"></a>參考後端回應參數</span><span class="sxs-lookup"><span data-stu-id="f1efd-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="f1efd-168">回應參數可修改 hello 回應 toohello 用戶端的一部分。</span><span class="sxs-lookup"><span data-stu-id="f1efd-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="f1efd-169">hello 值可以用於組態值：</span><span class="sxs-lookup"><span data-stu-id="f1efd-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="f1efd-170">**{backend.response.statusCode}**: hello 傳回 hello 後端回應的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="f1efd-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="f1efd-171">**{backend.response.statusReason}**: hello HTTP 原因片語 hello 後端回應傳回。</span><span class="sxs-lookup"><span data-stu-id="f1efd-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="f1efd-172">**{backend.response.headers。\<HeaderName\>}**： 可讀取 hello 後端回應標頭。</span><span class="sxs-lookup"><span data-stu-id="f1efd-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="f1efd-173">取代 *\<HeaderName\>* 想 tooread hello hello 標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="f1efd-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="f1efd-174">如果 hello 標頭未包含在 hello 要求，hello 值會是 hello 空字串。</span><span class="sxs-lookup"><span data-stu-id="f1efd-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="f1efd-175"><a name="use-appsettings"></a>參考應用程式設定</span><span class="sxs-lookup"><span data-stu-id="f1efd-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="f1efd-176">您也可以參考[hello 函式應用程式定義的應用程式設定](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop)住 hello 設定名稱，加上百分比符號 （%）。</span><span class="sxs-lookup"><span data-stu-id="f1efd-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="f1efd-177">例如後, 端的 URL *https://%ORDER_PROCESSING_HOST%/api/orders*會有"%order_processing_host%"hello ORDER_PROCESSING_HOST 設定 hello 值取代。</span><span class="sxs-lookup"><span data-stu-id="f1efd-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="f1efd-178">當您有多個部署或測試環境時，請使用後端主機的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="f1efd-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="f1efd-179">這樣一來，您可以確保您永遠與對話 toohello 帶回結束該環境。</span><span class="sxs-lookup"><span data-stu-id="f1efd-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="f1efd-180">進階組態</span><span class="sxs-lookup"><span data-stu-id="f1efd-180">Advanced configuration</span></span>

<span data-ttu-id="f1efd-181">您所設定的 hello proxy 會儲存在 proxies.json 檔案，位於 hello 的函式應用程式目錄的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="f1efd-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="f1efd-182">您可以手動編輯此檔案並將其部署為應用程式的一部分，當您使用任何 hello[部署方法](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)支援的函式。</span><span class="sxs-lookup"><span data-stu-id="f1efd-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="f1efd-183">hello 功能必須為[啟用](#enable)的 hello 檔案 toobe 處理。</span><span class="sxs-lookup"><span data-stu-id="f1efd-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="f1efd-184">如果您還沒有將設定 hello 部署方法之一，您也可以使用 hello 入口網站中的 hello proxies.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="f1efd-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="f1efd-185">移 tooyour 函式應用程式中，選取**平台功能**，然後選取**應用程式服務編輯器**。</span><span class="sxs-lookup"><span data-stu-id="f1efd-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="f1efd-186">如此一來，您可以檢視應用程式函式的 hello 整個檔案結構，並再進行變更。</span><span class="sxs-lookup"><span data-stu-id="f1efd-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="f1efd-187">Proxies.json 是由 Proxy 物件定義，該物件包含具名 Proxy 及其定義。</span><span class="sxs-lookup"><span data-stu-id="f1efd-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="f1efd-188">您可以選擇性地參考 [JSON 結構描述](http://json.schemastore.org/proxies)，以啟用程式碼自動完成 (如果編輯器支援的話)。</span><span class="sxs-lookup"><span data-stu-id="f1efd-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="f1efd-189">範例檔案可能看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="f1efd-189">An example file might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="f1efd-190">每個 proxy 都具有好記的名稱，例如*proxy1* hello 前面範例中。</span><span class="sxs-lookup"><span data-stu-id="f1efd-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="f1efd-191">hello 對應的 proxy 定義物件是由下列屬性的 hello 定義：</span><span class="sxs-lookup"><span data-stu-id="f1efd-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="f1efd-192">**matchCondition**： 需要-定義這個 proxy hello 執行觸發程序的 hello 要求的物件。</span><span class="sxs-lookup"><span data-stu-id="f1efd-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="f1efd-193">它包含與 [HTTP 觸發程序]共用的兩個屬性：</span><span class="sxs-lookup"><span data-stu-id="f1efd-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="f1efd-194">_方法_： 回應 hello proxy 的 hello HTTP 方法的陣列。</span><span class="sxs-lookup"><span data-stu-id="f1efd-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="f1efd-195">如果未指定，hello proxy 會回應 tooall hello 路由上的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f1efd-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="f1efd-196">_路由_： 需要-定義 hello 路由範本，控制其要求您的 proxy Url 回應。</span><span class="sxs-lookup"><span data-stu-id="f1efd-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="f1efd-197">不同於 HTTP 觸發程序，這個項目沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="f1efd-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="f1efd-198">**backendUri**: hello hello 後端資源 toowhich hello 要求 URL 應該代理。</span><span class="sxs-lookup"><span data-stu-id="f1efd-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="f1efd-199">這個值可以從原始用戶端要求 hello 參考應用程式設定和參數。</span><span class="sxs-lookup"><span data-stu-id="f1efd-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="f1efd-200">如果不包含這個屬性，Azure Functions 會回應 HTTP 200 OK。</span><span class="sxs-lookup"><span data-stu-id="f1efd-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="f1efd-201">**requestOverrides**： 定義轉換 toohello 後端要求的物件。</span><span class="sxs-lookup"><span data-stu-id="f1efd-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="f1efd-202">請參閱[定義 requestOverrides 物件]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="f1efd-203">**responseOverrides**： 定義轉換 toohello 用戶端回應的物件。</span><span class="sxs-lookup"><span data-stu-id="f1efd-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="f1efd-204">請參閱[定義 responseOverrides 物件]。</span><span class="sxs-lookup"><span data-stu-id="f1efd-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="f1efd-205">hello 路由屬性 Azure 函式的 Proxy 不接受 hello routePrefix hello 函式主機組態屬性。</span><span class="sxs-lookup"><span data-stu-id="f1efd-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="f1efd-206">如果您想 tooinclude /api 例如前置詞，則它必須包含在 hello 路由屬性。</span><span class="sxs-lookup"><span data-stu-id="f1efd-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="f1efd-207"><a name="requestOverrides"></a>定義 requestOverrides 物件</span><span class="sxs-lookup"><span data-stu-id="f1efd-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="f1efd-208">hello requestOverrides 物件會定義呼叫 hello 後端資源時提出 toohello 要求的變更。</span><span class="sxs-lookup"><span data-stu-id="f1efd-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="f1efd-209">hello 物件是由下列屬性的 hello 定義：</span><span class="sxs-lookup"><span data-stu-id="f1efd-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="f1efd-210">**backend.request.method**: hello toocall hello 後端使用的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f1efd-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="f1efd-211">**backend.request.querystring。\<ParameterName\>**： 您可以將 hello 呼叫 toohello 後端的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="f1efd-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="f1efd-212">取代 *\<ParameterName\>*  hello 想 tooset hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="f1efd-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="f1efd-213">如果提供 hello 空字串，則 hello 參數不會包含在 hello 後端要求。</span><span class="sxs-lookup"><span data-stu-id="f1efd-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="f1efd-214">**backend.request.headers。\<HeaderName\>**： 您可以將 hello 呼叫 toohello 後端的標頭。</span><span class="sxs-lookup"><span data-stu-id="f1efd-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="f1efd-215">取代 *\<HeaderName\>*  hello 想 tooset hello 標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="f1efd-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="f1efd-216">如果您提供 hello 空字串，hello 標頭未包含在 hello 後端要求。</span><span class="sxs-lookup"><span data-stu-id="f1efd-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="f1efd-217">值可以從原始用戶端要求 hello 參考應用程式設定和參數。</span><span class="sxs-lookup"><span data-stu-id="f1efd-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="f1efd-218">設定範例看起來可能類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="f1efd-218">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="f1efd-219"><a name="responseOverrides"></a>定義 responseOverrides 物件</span><span class="sxs-lookup"><span data-stu-id="f1efd-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="f1efd-220">hello requestOverrides 物件定義進行 toohello 回應已通過後 toohello 用戶端的變更。</span><span class="sxs-lookup"><span data-stu-id="f1efd-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="f1efd-221">hello 物件是由下列屬性的 hello 定義：</span><span class="sxs-lookup"><span data-stu-id="f1efd-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="f1efd-222">**response.statusCode**: hello HTTP 狀態碼 toobe 傳回 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1efd-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="f1efd-223">**response.statusReason**: hello HTTP 原因片語 toobe 傳回 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1efd-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="f1efd-224">**response.body**: hello 主體 toobe hello 字串表示法傳回 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f1efd-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="f1efd-225">**response.headers。\<HeaderName\>**: hello 回應 toohello 用戶端可設定的標頭。</span><span class="sxs-lookup"><span data-stu-id="f1efd-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="f1efd-226">取代 *\<HeaderName\>*  hello 想 tooset hello 標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="f1efd-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="f1efd-227">如果您提供 hello 空字串，hello 回應不包含 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="f1efd-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="f1efd-228">值可以參考 hello 後端回應應用程式設定、 從原始用戶端要求 hello、 參數和參數。</span><span class="sxs-lookup"><span data-stu-id="f1efd-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="f1efd-229">設定範例看起來可能類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="f1efd-229">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="f1efd-230">在此範例中，hello 主體被設定直接等等`backendUri`需要屬性。</span><span class="sxs-lookup"><span data-stu-id="f1efd-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="f1efd-231">hello 範例示範如何使用 Azure 函式 Proxy 的模擬應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f1efd-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[Azure 入口網站]: https://portal.azure.com
[HTTP 觸發程序]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[定義 requestOverrides 物件]: #requestOverrides
[定義 responseOverrides 物件]: #responseOverrides
[應用程式設定]: #use-appsettings
[使用變數]: #using-variables
[來自原始用戶端要求 hello 參數]: #request-parameters
[hello 後端回應來自參數]: #response-parameters
