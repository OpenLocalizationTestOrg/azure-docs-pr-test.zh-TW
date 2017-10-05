---
title: "在 Azure Functions 中使用 Proxy | Microsoft Docs"
description: "如何使用 Azure Functions Proxy 的概觀"
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
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="8a566-103">使用 Azure Functions Proxy (預覽)</span><span class="sxs-lookup"><span data-stu-id="8a566-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="8a566-104">Azure Functions Proxy 目前為預覽版。</span><span class="sxs-lookup"><span data-stu-id="8a566-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="8a566-105">預覽版是免費的，但是標準 Functions 計費會套用至 Proxy 執行。</span><span class="sxs-lookup"><span data-stu-id="8a566-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="8a566-106">如需詳細資訊，請參閱 [Azure Functions 價格](https://azure.microsoft.com/pricing/details/functions/)。</span><span class="sxs-lookup"><span data-stu-id="8a566-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="8a566-107">這篇文章說明如何設定與使用 Azure Functions Proxy。</span><span class="sxs-lookup"><span data-stu-id="8a566-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="8a566-108">這項功能可讓您在函式應用程式上指定由其他資源所實作的端點。</span><span class="sxs-lookup"><span data-stu-id="8a566-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="8a566-109">您可以使用這些 Proxy 將大型 API 細分為多個函式應用程式 (如同在微服務架構中)，同時仍為用戶端呈現單一的 API 介面。</span><span class="sxs-lookup"><span data-stu-id="8a566-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="8a566-110"><a name="enable"></a>啟用 Azure Functions Proxy</span><span class="sxs-lookup"><span data-stu-id="8a566-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="8a566-111">預設不會啟用 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8a566-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="8a566-112">功能停用時您可以建立 Proxy，但是它們不會執行。</span><span class="sxs-lookup"><span data-stu-id="8a566-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="8a566-113">若要啟用 Proxy，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="8a566-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="8a566-114">開啟 [Azure 入口網站]，然後移至您的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a566-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="8a566-115">選取 [函式應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="8a566-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="8a566-116">將 [啟用 Azure Functions Proxy (預覽)] 切換為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="8a566-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="8a566-117">您也可以在新功能可供使用時，返回這裡以更新 Proxy 執行階段。</span><span class="sxs-lookup"><span data-stu-id="8a566-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="8a566-118"><a name="create"></a>建立 Proxy</span><span class="sxs-lookup"><span data-stu-id="8a566-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="8a566-119">本節將示範如何在 Functions 入口網站中建立 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8a566-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="8a566-120">開啟 [Azure 入口網站]，然後移至您的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a566-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="8a566-121">在左側窗格中，選取 [新增 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="8a566-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="8a566-122">為您的 Proxy 提供名稱。</span><span class="sxs-lookup"><span data-stu-id="8a566-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="8a566-123">指定 [路由範本] 和 [HTTP 方法]，以設定此函式應用程式上公開的端點。</span><span class="sxs-lookup"><span data-stu-id="8a566-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="8a566-124">這些參數的行為會根據 [HTTP 觸發程序]的規則。</span><span class="sxs-lookup"><span data-stu-id="8a566-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="8a566-125">將**後端 URL** 設定為其他端點。</span><span class="sxs-lookup"><span data-stu-id="8a566-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="8a566-126">此端點可能是另一個函式應用程式中的函式，也可能是任何其他 API。</span><span class="sxs-lookup"><span data-stu-id="8a566-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="8a566-127">值不需要是靜態，且可以參考[應用程式設定]和[來自原始用戶端要求的參數]。</span><span class="sxs-lookup"><span data-stu-id="8a566-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="8a566-128">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8a566-128">Click **Create**.</span></span>

<span data-ttu-id="8a566-129">您的 Proxy 現在會存在做為函式應用程式上的新端點。</span><span class="sxs-lookup"><span data-stu-id="8a566-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="8a566-130">從用戶端的觀點而言，它相當於 Azure Functions 中的 HttpTrigger。</span><span class="sxs-lookup"><span data-stu-id="8a566-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="8a566-131">您可以藉由複製 Proxy URL 並使用最愛的 HTTP 用戶端來測試它，以嘗試您的新 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8a566-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="8a566-132"><a name="modify-requests-responses"></a>修改要求和回應</span><span class="sxs-lookup"><span data-stu-id="8a566-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="8a566-133">Azure Functions Proxy 可讓您修改針對後端的要求及來自後端的回應。</span><span class="sxs-lookup"><span data-stu-id="8a566-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="8a566-134">這些轉換可以利用[使用變數]中所定義的變數。</span><span class="sxs-lookup"><span data-stu-id="8a566-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="8a566-135"><a name="modify-backend-request"></a>修改後端要求</span><span class="sxs-lookup"><span data-stu-id="8a566-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="8a566-136">根據預設，後端要求會初始化為原始要求的複本。</span><span class="sxs-lookup"><span data-stu-id="8a566-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="8a566-137">除了設定後端 URL 之外，您也可以變更 HTTP 方法、標頭及查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="8a566-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="8a566-138">修改過的值可以參考[應用程式設定]和[來自原始用戶端要求的參數]。</span><span class="sxs-lookup"><span data-stu-id="8a566-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="8a566-139">目前，尚無修改後端要求的入口網站體驗。</span><span class="sxs-lookup"><span data-stu-id="8a566-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="8a566-140">若要了解如何從 proxies.json 套用此功能，請參閱[定義 requestOverrides 物件]。</span><span class="sxs-lookup"><span data-stu-id="8a566-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="8a566-141"><a name="modify-response"></a>修改回應</span><span class="sxs-lookup"><span data-stu-id="8a566-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="8a566-142">根據預設，用戶端回應會初始化為後端回應的複本。</span><span class="sxs-lookup"><span data-stu-id="8a566-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="8a566-143">您可以對回應的狀態碼、原因說明、標頭及本文做出變更。</span><span class="sxs-lookup"><span data-stu-id="8a566-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="8a566-144">修改過的值可以參考[應用程式設定]、[來自原始用戶端要求的參數]，以及[來自後端回應的參數]。</span><span class="sxs-lookup"><span data-stu-id="8a566-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="8a566-145">目前，尚無修改回應的入口網站體驗。</span><span class="sxs-lookup"><span data-stu-id="8a566-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="8a566-146">若要了解如何從 proxies.json 套用此功能，請參閱[定義 responseOverrides 物件]。</span><span class="sxs-lookup"><span data-stu-id="8a566-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="8a566-147"><a name="using-variables"></a>使用變數</span><span class="sxs-lookup"><span data-stu-id="8a566-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="8a566-148">Proxy 的設定不需要是靜態。</span><span class="sxs-lookup"><span data-stu-id="8a566-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="8a566-149">您可以將它設定為使用來自原始要求、後端回應或應用程式設定的變數。</span><span class="sxs-lookup"><span data-stu-id="8a566-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="8a566-150"><a name="request-parameters"></a>參考要求參數</span><span class="sxs-lookup"><span data-stu-id="8a566-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="8a566-151">您可以使用要求參數作為後端 URL 屬性的輸入，或在修改要求和回應時使用。</span><span class="sxs-lookup"><span data-stu-id="8a566-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="8a566-152">某些參數可能繫結自基底 Proxy 設定中指定的路由範本，而其他參數可能來自連入要求的屬性。</span><span class="sxs-lookup"><span data-stu-id="8a566-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="8a566-153">路由範本參數</span><span class="sxs-lookup"><span data-stu-id="8a566-153">Route template parameters</span></span>
<span data-ttu-id="8a566-154">路由範本中使用的參數可依名稱參考。</span><span class="sxs-lookup"><span data-stu-id="8a566-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="8a566-155">參數名稱以大括號 ("{}") 括住。</span><span class="sxs-lookup"><span data-stu-id="8a566-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="8a566-156">例如，如果 Proxy 的路由範本是 `/pets/{petId}`，則後端 URL 可以包含 `{petId}` 的值，如 `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}` 中所示。</span><span class="sxs-lookup"><span data-stu-id="8a566-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="8a566-157">如果路由範本的結尾是萬用字元，例如 `/api/{*restOfPath}`，則值 `{restOfPath}` 是連入要求之其餘路徑區段的字串表示。</span><span class="sxs-lookup"><span data-stu-id="8a566-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="8a566-158">其他要求參數</span><span class="sxs-lookup"><span data-stu-id="8a566-158">Additional request parameters</span></span>
<span data-ttu-id="8a566-159">除了路由範本參數之外，設定值中也可以使用下列值：</span><span class="sxs-lookup"><span data-stu-id="8a566-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="8a566-160">**{request.method}**：用於原始要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="8a566-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="8a566-161">**{request.headers.\<HeaderName\>}**：可以從原始要求讀取的標頭。</span><span class="sxs-lookup"><span data-stu-id="8a566-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="8a566-162">以您想要讀取之標頭的名稱取代 *\<HeaderName\>*。</span><span class="sxs-lookup"><span data-stu-id="8a566-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="8a566-163">如果標頭沒有包含在要求之上，值將會是空字串。</span><span class="sxs-lookup"><span data-stu-id="8a566-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="8a566-164">**{request.querystring.\<ParameterName\>}**：可以從原始要求讀取的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="8a566-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="8a566-165">以您想要讀取之參數的名稱取代 *\<ParameterName\>*。</span><span class="sxs-lookup"><span data-stu-id="8a566-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="8a566-166">如果參數沒有包含在要求之上，值將會是空字串。</span><span class="sxs-lookup"><span data-stu-id="8a566-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="8a566-167"><a name="response-parameters"></a>參考後端回應參數</span><span class="sxs-lookup"><span data-stu-id="8a566-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="8a566-168">修改對用戶端的回應時可以使用回應參數。</span><span class="sxs-lookup"><span data-stu-id="8a566-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="8a566-169">設定值中可以使用下列值：</span><span class="sxs-lookup"><span data-stu-id="8a566-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="8a566-170">**{backend.response.statusCode}**：後端回應上所傳回的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="8a566-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="8a566-171">**{backend.response.statusReason}**：後端回應上所傳回的 HTTP 原因說明。</span><span class="sxs-lookup"><span data-stu-id="8a566-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="8a566-172">**{backend.response.headers.\<HeaderName\>}**：可以從後端回應讀取的標頭。</span><span class="sxs-lookup"><span data-stu-id="8a566-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="8a566-173">以您想要讀取之標頭的名稱取代 *\<HeaderName\>*。</span><span class="sxs-lookup"><span data-stu-id="8a566-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="8a566-174">如果標頭沒有包含在要求之上，值將會是空字串。</span><span class="sxs-lookup"><span data-stu-id="8a566-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="8a566-175"><a name="use-appsettings"></a>參考應用程式設定</span><span class="sxs-lookup"><span data-stu-id="8a566-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="8a566-176">您也可以參考[針對函式應用程式定義的應用程式設定](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop)，只要以百分比符號 (%) 括住設定名稱即可。</span><span class="sxs-lookup"><span data-stu-id="8a566-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="8a566-177">例如，後端 URL *https://%ORDER_PROCESSING_HOST%/api/orders* 中會以 ORDER_PROCESSING_HOST 設定的值取代 "%ORDER_PROCESSING_HOST%"。</span><span class="sxs-lookup"><span data-stu-id="8a566-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="8a566-178">當您有多個部署或測試環境時，請使用後端主機的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="8a566-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="8a566-179">這樣一來，您可以確保永遠與該環境的正確後端通訊。</span><span class="sxs-lookup"><span data-stu-id="8a566-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="8a566-180">進階組態</span><span class="sxs-lookup"><span data-stu-id="8a566-180">Advanced configuration</span></span>

<span data-ttu-id="8a566-181">您設定的 Proxy 會儲存在 proxies.json 檔案中 (位於函式應用程式目錄的根目錄中)。</span><span class="sxs-lookup"><span data-stu-id="8a566-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="8a566-182">當您使用Functions 支援的任何[部署方法](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)時，您可以手動編輯此檔案，並部署為應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="8a566-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="8a566-183">對於要處理的檔案，必須[啟用](#enable)此功能。</span><span class="sxs-lookup"><span data-stu-id="8a566-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="8a566-184">如果您尚未設定其中一個部署方法，您也可以使用入口網站中的 proxies.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="8a566-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="8a566-185">移至您的函式應用程式，選取 [平台功能]，然後選取 [App Service 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="8a566-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="8a566-186">如此一來，您可以查看函式應用程式的整個檔案結構，然後做出變更。</span><span class="sxs-lookup"><span data-stu-id="8a566-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="8a566-187">Proxies.json 是由 Proxy 物件定義，該物件包含具名 Proxy 及其定義。</span><span class="sxs-lookup"><span data-stu-id="8a566-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="8a566-188">您可以選擇性地參考 [JSON 結構描述](http://json.schemastore.org/proxies)，以啟用程式碼自動完成 (如果編輯器支援的話)。</span><span class="sxs-lookup"><span data-stu-id="8a566-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="8a566-189">範例檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a566-189">An example file might look like the following:</span></span>

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

<span data-ttu-id="8a566-190">在上述範例中，每個 Proxy 都有好記的名稱，例如 *proxy1*。</span><span class="sxs-lookup"><span data-stu-id="8a566-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="8a566-191">對應的 Proxy 定義物件是由下列屬性定義︰</span><span class="sxs-lookup"><span data-stu-id="8a566-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="8a566-192">**matchCondition**︰必要 -- 此物件定義要求以觸發執行此 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8a566-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="8a566-193">它包含與 [HTTP 觸發程序]共用的兩個屬性：</span><span class="sxs-lookup"><span data-stu-id="8a566-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="8a566-194">_method_：Proxy 回應的 HTTP 方法陣列。</span><span class="sxs-lookup"><span data-stu-id="8a566-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="8a566-195">如果未指定，Proxy 會回應路由上的所有 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="8a566-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="8a566-196">_route_：必要 - 定義路由範本，控制 Proxy 回應哪些要求 URL。</span><span class="sxs-lookup"><span data-stu-id="8a566-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="8a566-197">不同於 HTTP 觸發程序，這個項目沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="8a566-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="8a566-198">**backendUri**︰後端資源的 URL，而其要求應該透過代理。</span><span class="sxs-lookup"><span data-stu-id="8a566-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="8a566-199">此值可以參考應用程式設定和來自原始用戶端要求的參數。</span><span class="sxs-lookup"><span data-stu-id="8a566-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="8a566-200">如果不包含這個屬性，Azure Functions 會回應 HTTP 200 OK。</span><span class="sxs-lookup"><span data-stu-id="8a566-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="8a566-201">**requestOverrides**：此物件定義後端要求的轉換。</span><span class="sxs-lookup"><span data-stu-id="8a566-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="8a566-202">請參閱[定義 requestOverrides 物件]。</span><span class="sxs-lookup"><span data-stu-id="8a566-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="8a566-203">**responseOverrides**：此物件定義用戶端回應的轉換。</span><span class="sxs-lookup"><span data-stu-id="8a566-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="8a566-204">請參閱[定義 responseOverrides 物件]。</span><span class="sxs-lookup"><span data-stu-id="8a566-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="8a566-205">route 屬性 Azure Functions Proxy 不採納 Functions 主機組態的 routePrefix 屬性。</span><span class="sxs-lookup"><span data-stu-id="8a566-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="8a566-206">如果您想要包含前置詞，例如 /api，則必須加入 route 屬性中。</span><span class="sxs-lookup"><span data-stu-id="8a566-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="8a566-207"><a name="requestOverrides"></a>定義 requestOverrides 物件</span><span class="sxs-lookup"><span data-stu-id="8a566-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="8a566-208">requestOverrides 物件定義呼叫後端資源時針對要求所做的變更。</span><span class="sxs-lookup"><span data-stu-id="8a566-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="8a566-209">該物件是由下列屬性所定義：</span><span class="sxs-lookup"><span data-stu-id="8a566-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="8a566-210">**backend.request.method**：用來呼叫後端的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="8a566-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="8a566-211">**backend.request.querystring.\<ParameterName\>**：呼叫後端時可以設定的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="8a566-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="8a566-212">以您想要設定之參數的名稱取代 *\<ParameterName\>*。</span><span class="sxs-lookup"><span data-stu-id="8a566-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="8a566-213">若提供空字串，則後端要求不會包含該參數。</span><span class="sxs-lookup"><span data-stu-id="8a566-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="8a566-214">**backend.request.headers.\<HeaderName\>**：呼叫後端時可以設定的標頭。</span><span class="sxs-lookup"><span data-stu-id="8a566-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="8a566-215">以您想要設定之標頭的名稱取代 *\<HeaderName\>*。</span><span class="sxs-lookup"><span data-stu-id="8a566-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="8a566-216">如果您提供空字串，則後端要求不會包含該標頭。</span><span class="sxs-lookup"><span data-stu-id="8a566-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="8a566-217">值可以參考應用程式設定和來自原始用戶端要求的參數。</span><span class="sxs-lookup"><span data-stu-id="8a566-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="8a566-218">範例設定看起來可能如下：</span><span class="sxs-lookup"><span data-stu-id="8a566-218">An example configuration might look like the following:</span></span>

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

### <span data-ttu-id="8a566-219"><a name="responseOverrides"></a>定義 responseOverrides 物件</span><span class="sxs-lookup"><span data-stu-id="8a566-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="8a566-220">requestOverrides 物件定義針對傳回給用戶端之回應所做的變更。</span><span class="sxs-lookup"><span data-stu-id="8a566-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="8a566-221">該物件是由下列屬性所定義：</span><span class="sxs-lookup"><span data-stu-id="8a566-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="8a566-222">**response.statusCode**：要傳回給用戶端的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="8a566-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="8a566-223">**response.statusReason**：要傳回給用戶端的 HTTP 原因說明。</span><span class="sxs-lookup"><span data-stu-id="8a566-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="8a566-224">**response.body**：要傳回給用戶端之本文的字串表示。</span><span class="sxs-lookup"><span data-stu-id="8a566-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="8a566-225">**response.headers.\<HeaderName\>**：在回應用戶端時可以設定的標頭。</span><span class="sxs-lookup"><span data-stu-id="8a566-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="8a566-226">以您想要設定之標頭的名稱取代 *\<HeaderName\>*。</span><span class="sxs-lookup"><span data-stu-id="8a566-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="8a566-227">如果您提供空字串，則回應不會包含該標頭。</span><span class="sxs-lookup"><span data-stu-id="8a566-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="8a566-228">值可以參考應用程式設定、來自原始用戶端要求的參數，以及來自後端回應的參數。</span><span class="sxs-lookup"><span data-stu-id="8a566-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="8a566-229">範例設定看起來可能如下：</span><span class="sxs-lookup"><span data-stu-id="8a566-229">An example configuration might look like the following:</span></span>

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
> <span data-ttu-id="8a566-230">此範例會直接設定本文，因此不需要 `backendUri` 屬性。</span><span class="sxs-lookup"><span data-stu-id="8a566-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="8a566-231">此範例示範如何使用 Azure Functions Proxy 來模擬 API。</span><span class="sxs-lookup"><span data-stu-id="8a566-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="8a566-232">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="8a566-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="8a566-233">[HTTP 觸發程序]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="8a566-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="8a566-234">[定義 requestOverrides 物件]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="8a566-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="8a566-235">[定義 responseOverrides 物件]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="8a566-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="8a566-236">[應用程式設定]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="8a566-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="8a566-237">[使用變數]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="8a566-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="8a566-238">[來自原始用戶端要求的參數]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="8a566-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="8a566-239">[來自後端回應的參數]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="8a566-239">[parameters from the back-end response]: #response-parameters</span></span>
