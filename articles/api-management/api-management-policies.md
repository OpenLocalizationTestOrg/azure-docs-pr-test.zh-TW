---
title: "Azure API 管理原則 | Microsoft Docs"
description: "了解可在「Azure API 管理」中使用的原則。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="f6c78-103">API 管理原則</span><span class="sxs-lookup"><span data-stu-id="f6c78-103">API Management policies</span></span>
<span data-ttu-id="f6c78-104">本節提供下列「API 管理」原則的參考。</span><span class="sxs-lookup"><span data-stu-id="f6c78-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="f6c78-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="f6c78-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="f6c78-106">原則是系統的強大功能，可讓發行者透過組態來變更 API 的行為。</span><span class="sxs-lookup"><span data-stu-id="f6c78-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="f6c78-107">原則是「陳述式」的集合，會在 API 的要求或回應上循序執行。</span><span class="sxs-lookup"><span data-stu-id="f6c78-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="f6c78-108">常見的「陳述式」包括從 XML 至 JSON 的格式轉換，以及利用呼叫速率限制來限制開發人員傳入的呼叫數量。</span><span class="sxs-lookup"><span data-stu-id="f6c78-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="f6c78-109">還有許多現成的原則可用。</span><span class="sxs-lookup"><span data-stu-id="f6c78-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="f6c78-110">如果原則不另行指定，則可以在任何 API 管理原則中，使用原則運算式做為屬性值或文字值。</span><span class="sxs-lookup"><span data-stu-id="f6c78-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="f6c78-111">某些原則是以原則運算式為基礎，例如[控制流程](api-management-advanced-policies.md#choose)和[設定變數](api-management-advanced-policies.md#set-variable)原則。</span><span class="sxs-lookup"><span data-stu-id="f6c78-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="f6c78-112">如需詳細資訊，請參閱[進階原則](api-management-advanced-policies.md#AdvancedPolicies)和[原則運算式](api-management-policy-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="f6c78-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="f6c78-113"><a name="ProxyPolicies"></a> 原則</span><span class="sxs-lookup"><span data-stu-id="f6c78-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="f6c78-114">存取限制原則</span><span class="sxs-lookup"><span data-stu-id="f6c78-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="f6c78-115">[檢查 HTTP 標頭](api-management-access-restriction-policies.md#CheckHTTPHeader) - 強制必須存在和/或強制採用 HTTP 標頭的值。</span><span class="sxs-lookup"><span data-stu-id="f6c78-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="f6c78-116">[依訂閱限制呼叫率](api-management-access-restriction-policies.md#LimitCallRate) - 以訂閱為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="f6c78-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="f6c78-117">[依金鑰限制呼叫率](api-management-access-restriction-policies.md#LimitCallRateByKey) - 以金鑰為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="f6c78-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="f6c78-118">[限制呼叫端 IP](api-management-access-restriction-policies.md#RestrictCallerIPs) - 篩選 (允許/拒絕) 來自特定 IP 位址和/或位址範圍的呼叫。</span><span class="sxs-lookup"><span data-stu-id="f6c78-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="f6c78-119">[依訂閱設定使用量配額](api-management-access-restriction-policies.md#SetUsageQuota) - 以訂閱為單位，讓您可以強制採用可續訂或有存留期呼叫量與 (或) 頻寬配額。</span><span class="sxs-lookup"><span data-stu-id="f6c78-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="f6c78-120">[依金鑰設定使用量配額](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - 以金鑰為單位，讓您可以強制採用可續訂或有存留期呼叫量與 (或) 頻寬配額。</span><span class="sxs-lookup"><span data-stu-id="f6c78-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="f6c78-121">[驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT) - 強制擷取自指定 HTTP 標頭或指定查詢參數的 JWT 必須存在且有效。</span><span class="sxs-lookup"><span data-stu-id="f6c78-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="f6c78-122">進階原則</span><span class="sxs-lookup"><span data-stu-id="f6c78-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="f6c78-123">[控制流程](api-management-advanced-policies.md#choose) - 根據布林值運算式的評估，有條件地套用原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="f6c78-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="f6c78-124">[轉寄要求](api-management-advanced-policies.md#ForwardRequest) - 將要求轉寄至後端服務。</span><span class="sxs-lookup"><span data-stu-id="f6c78-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="f6c78-125">[記錄至事件中樞](api-management-advanced-policies.md#log-to-eventhub) - 將訊息以指定的格式傳送至「記錄器」實體所定義的訊息目標。</span><span class="sxs-lookup"><span data-stu-id="f6c78-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="f6c78-126">[重試](api-management-advanced-policies.md#Retry) - 重試已括住的原則陳述式執行，直到符合條件為止。</span><span class="sxs-lookup"><span data-stu-id="f6c78-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="f6c78-127">系統會在指定的時間間隔重複執行，直到指定的重試計數為止。</span><span class="sxs-lookup"><span data-stu-id="f6c78-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="f6c78-128">[傳回回應](api-management-advanced-policies.md#ReturnResponse) - 中止管線執行，並將指定的回應直接傳回呼叫者。</span><span class="sxs-lookup"><span data-stu-id="f6c78-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="f6c78-129">[傳送單向要求](api-management-advanced-policies.md#SendOneWayRequest) - 將要求傳送到指定的 URL，無須等待回應。</span><span class="sxs-lookup"><span data-stu-id="f6c78-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="f6c78-130">[傳送要求](api-management-advanced-policies.md#SendRequest) - 將要求傳送到指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="f6c78-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="f6c78-131">[設定變數](api-management-advanced-policies.md#set-variable) - 將值保存在具名的 context 變數中以供日後存取。</span><span class="sxs-lookup"><span data-stu-id="f6c78-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="f6c78-132">[設定要求方法](api-management-advanced-policies.md#SetRequestMethod) - 允許您變更要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f6c78-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="f6c78-133">[設定狀態碼](api-management-advanced-policies.md#SetStatus) - 將 HTTP 狀態碼變更為指定的值。</span><span class="sxs-lookup"><span data-stu-id="f6c78-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="f6c78-134">[追蹤](api-management-advanced-policies.md#Trace) - 將字串新增至 [API 檢查器](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。</span><span class="sxs-lookup"><span data-stu-id="f6c78-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="f6c78-135">[等候](api-management-advanced-policies.md#Wait) - 等候括住的 [Send 要求](api-management-advanced-policies.md#SendRequest)、[從快取取得值](api-management-caching-policies.md#GetFromCacheByKey)或[控制流程](api-management-advanced-policies.md#choose)原則完成後再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="f6c78-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="f6c78-136">驗證原則</span><span class="sxs-lookup"><span data-stu-id="f6c78-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="f6c78-137">[使用基本驗證進行驗證](api-management-authentication-policies.md#Basic) - 使用基本驗證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="f6c78-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="f6c78-138">[使用用戶端憑證進行驗證](api-management-authentication-policies.md#ClientCertificate) - 使用用戶端憑證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="f6c78-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="f6c78-139">快取原則</span><span class="sxs-lookup"><span data-stu-id="f6c78-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="f6c78-140">[從快取中取得](api-management-caching-policies.md#GetFromCache) - 執行快取查閱並傳回有效的快取回應 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="f6c78-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="f6c78-141">[儲存至快取](api-management-caching-policies.md#StoreToCache) - 根據指定的快取控制組態來快取回應。</span><span class="sxs-lookup"><span data-stu-id="f6c78-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="f6c78-142">[從快取取得值](api-management-caching-policies.md#GetFromCacheByKey) - 依金鑰擷取快取的項目。</span><span class="sxs-lookup"><span data-stu-id="f6c78-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="f6c78-143">[儲存快取中的值](api-management-caching-policies.md#StoreToCacheByKey) -依金鑰儲存快取中的項目。</span><span class="sxs-lookup"><span data-stu-id="f6c78-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="f6c78-144">[移除快取中的值](api-management-caching-policies.md#RemoveCacheByKey) - 依金鑰移除快取中的項目。</span><span class="sxs-lookup"><span data-stu-id="f6c78-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="f6c78-145">跨網域原則</span><span class="sxs-lookup"><span data-stu-id="f6c78-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="f6c78-146">[允許跨網域呼叫](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - 將 API 設為可供 Adobe Flash 和 Microsoft Silverlight 瀏覽器型用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="f6c78-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="f6c78-147">[CORS](api-management-cross-domain-policies.md#CORS) - 將跨原始來源資源分享 (CORS) 支援加入至操作或 API，以允許來自瀏覽器型用戶端的跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="f6c78-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="f6c78-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - 將 JSON 與補充的 (JSONP) 支援加入至操作或 API，以允許來自 JavaScript 瀏覽器型用戶端的跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="f6c78-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="f6c78-149">轉換原則</span><span class="sxs-lookup"><span data-stu-id="f6c78-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="f6c78-150">[將 JSON 轉換成 XML](api-management-transformation-policies.md#ConvertJSONtoXML) - 將要求或回應內文從 JSON 轉換成 XML。</span><span class="sxs-lookup"><span data-stu-id="f6c78-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="f6c78-151">[將 XML 轉換成 JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - 將要求或回應內文從 XML 轉換成 JSON。</span><span class="sxs-lookup"><span data-stu-id="f6c78-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="f6c78-152">[在內文中尋找並取代字串](api-management-transformation-policies.md#Findandreplacestringinbody) - 尋找要求或回應子字串，並將它取代為其他子字串。</span><span class="sxs-lookup"><span data-stu-id="f6c78-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="f6c78-153">[遮罩內容中的 URL](api-management-transformation-policies.md#MaskURLSContent) - 重寫 (遮罩) 回應內文的連結，使其經由閘道器指向同等的連結。</span><span class="sxs-lookup"><span data-stu-id="f6c78-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="f6c78-154">[設定後端服務](api-management-transformation-policies.md#SetBackendService) - 變更傳入要求的後端服務。</span><span class="sxs-lookup"><span data-stu-id="f6c78-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="f6c78-155">[設定本文](api-management-transformation-policies.md#SetBody) - 設定傳入和傳出要求的訊息本文。</span><span class="sxs-lookup"><span data-stu-id="f6c78-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="f6c78-156">[設定 HTTP 標頭](api-management-transformation-policies.md#SetHTTPheader) - 指派值給現有的回應及/或要求標頭，或加入新的回應及/或要求標頭。</span><span class="sxs-lookup"><span data-stu-id="f6c78-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="f6c78-157">[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter) - 新增、取代值或刪除要求查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="f6c78-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="f6c78-158">[重寫 URL](api-management-transformation-policies.md#RewriteURL) - 將要求 URL 從公用格式轉換成 Web 服務所需的格式。</span><span class="sxs-lookup"><span data-stu-id="f6c78-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="f6c78-159">[使用 XSLT 轉換 XML](api-management-transformation-policies.md#XSLTransform) - 將 XSL 轉換套用至要求或回應主體中的 XML。</span><span class="sxs-lookup"><span data-stu-id="f6c78-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="f6c78-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6c78-160">Next steps</span></span>
<span data-ttu-id="f6c78-161">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="f6c78-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
