---
title: "aaaAzure API 管理原則 |Microsoft 文件"
description: "深入了解 hello 原則可在 Azure API 管理中使用。"
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
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="75dd3-103">API 管理原則</span><span class="sxs-lookup"><span data-stu-id="75dd3-103">API Management policies</span></span>
<span data-ttu-id="75dd3-104">本節提供下列 API 管理原則的 hello 參考。</span><span class="sxs-lookup"><span data-stu-id="75dd3-104">This section provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="75dd3-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="75dd3-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="75dd3-106">原則是 hello 的透過組態 API toochange hello 行為允許 hello publisher 的 hello 系統的強大功能。</span><span class="sxs-lookup"><span data-stu-id="75dd3-106">Policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="75dd3-107">原則是循序 hello 要求上執行的陳述式的集合或應用程式開發介面的回應。</span><span class="sxs-lookup"><span data-stu-id="75dd3-107">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="75dd3-108">受歡迎的陳述式包含從 XML tooJSON 格式轉換，並呼叫速率限制為開發人員的來電 toorestrict hello 數量。</span><span class="sxs-lookup"><span data-stu-id="75dd3-108">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="75dd3-109">更多原則是可用的 hello 方塊。</span><span class="sxs-lookup"><span data-stu-id="75dd3-109">Many more policies are available out of hello box.</span></span>  
  
 <span data-ttu-id="75dd3-110">除非另外指定 hello 原則，可以使用原則運算式做為屬性值或任何 hello API 管理原則中的文字值。</span><span class="sxs-lookup"><span data-stu-id="75dd3-110">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="75dd3-111">某些原則，例如 hello[控制流程](api-management-advanced-policies.md#choose)和[設定變數](api-management-advanced-policies.md#set-variable)原則為基礎的原則運算式。</span><span class="sxs-lookup"><span data-stu-id="75dd3-111">Some policies such as hello [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="75dd3-112">如需詳細資訊，請參閱[進階原則](api-management-advanced-policies.md#AdvancedPolicies)和[原則運算式](api-management-policy-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="75dd3-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="75dd3-113"><a name="ProxyPolicies"></a> 原則</span><span class="sxs-lookup"><span data-stu-id="75dd3-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="75dd3-114">存取限制原則</span><span class="sxs-lookup"><span data-stu-id="75dd3-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="75dd3-115">[檢查 HTTP 標頭](api-management-access-restriction-policies.md#CheckHTTPHeader) - 強制必須存在和/或強制採用 HTTP 標頭的值。</span><span class="sxs-lookup"><span data-stu-id="75dd3-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="75dd3-116">[依訂閱限制呼叫率](api-management-access-restriction-policies.md#LimitCallRate) - 以訂閱為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="75dd3-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="75dd3-117">[依金鑰限制呼叫率](api-management-access-restriction-policies.md#LimitCallRateByKey) - 以金鑰為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="75dd3-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="75dd3-118">[限制呼叫端 IP](api-management-access-restriction-policies.md#RestrictCallerIPs) - 篩選 (允許/拒絕) 來自特定 IP 位址和/或位址範圍的呼叫。</span><span class="sxs-lookup"><span data-stu-id="75dd3-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="75dd3-119">[訂用帳戶所設定使用量配額](api-management-access-restriction-policies.md#SetUsageQuota)-可讓您以每個訂用帳戶為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。</span><span class="sxs-lookup"><span data-stu-id="75dd3-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="75dd3-120">[設定使用量配額，依索引鍵](api-management-access-restriction-policies.md#SetUsageQuotaByKey)-可讓您以每個索引鍵為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。</span><span class="sxs-lookup"><span data-stu-id="75dd3-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="75dd3-121">[驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT) - 強制擷取自指定 HTTP 標頭或指定查詢參數的 JWT 必須存在且有效。</span><span class="sxs-lookup"><span data-stu-id="75dd3-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="75dd3-122">進階原則</span><span class="sxs-lookup"><span data-stu-id="75dd3-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="75dd3-123">[控制流程](api-management-advanced-policies.md#choose)-有條件地套用原則陳述式，根據 hello 評估布林運算式。</span><span class="sxs-lookup"><span data-stu-id="75dd3-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="75dd3-124">[要求轉寄](api-management-advanced-policies.md#ForwardRequest)-轉送 hello 要求 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="75dd3-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards hello request toohello backend service.</span></span>  
  
    -   <span data-ttu-id="75dd3-125">[記錄 tooEvent 中樞](api-management-advanced-policies.md#log-to-eventhub)-傳送 hello 指定的格式 tooa 訊息目標記錄器實體所定義的訊息。</span><span class="sxs-lookup"><span data-stu-id="75dd3-125">[Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in hello specified format tooa message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="75dd3-126">[重試](api-management-advanced-policies.md#Retry)-重試執行 hello 括住原則陳述，如果，直到符合 hello 條件為止。</span><span class="sxs-lookup"><span data-stu-id="75dd3-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="75dd3-127">執行，就會重複在 hello 指定的時間間隔向上 toohello 指定重試計數。</span><span class="sxs-lookup"><span data-stu-id="75dd3-127">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
    -   <span data-ttu-id="75dd3-128">[將回應傳回](api-management-advanced-policies.md#ReturnResponse)-中止管線執行並傳回 hello 指定回應直接 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="75dd3-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>  
  
    -   <span data-ttu-id="75dd3-129">[其中一種方式要求傳送](api-management-advanced-policies.md#SendOneWayRequest)-傳送要求 toohello 指定 URL，而不必等候回應。</span><span class="sxs-lookup"><span data-stu-id="75dd3-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="75dd3-130">[傳送要求](api-management-advanced-policies.md#SendRequest)-傳送要求 toohello 指定 URL。</span><span class="sxs-lookup"><span data-stu-id="75dd3-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request toohello specified URL.</span></span>  
  
    -   <span data-ttu-id="75dd3-131">[設定變數](api-management-advanced-policies.md#set-variable) - 將值保存在具名的 context 變數中以供日後存取。</span><span class="sxs-lookup"><span data-stu-id="75dd3-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="75dd3-132">[將要求方法設定](api-management-advanced-policies.md#SetRequestMethod)-可讓您要求的 toochange hello HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="75dd3-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="75dd3-133">[設定狀態碼](api-management-advanced-policies.md#SetStatus)-變更 hello HTTP 狀態碼 toohello 指定的值。</span><span class="sxs-lookup"><span data-stu-id="75dd3-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
    -   <span data-ttu-id="75dd3-134">[追蹤](api-management-advanced-policies.md#Trace)-將字串新增至 hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。</span><span class="sxs-lookup"><span data-stu-id="75dd3-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="75dd3-135">[等候](api-management-advanced-policies.md#Wait)-括住，等候[傳送要求](api-management-advanced-policies.md#SendRequest)，[取得值，從快取](api-management-caching-policies.md#GetFromCacheByKey)，或[控制流程](api-management-advanced-policies.md#choose)原則 toocomplete 後再繼續。</span><span class="sxs-lookup"><span data-stu-id="75dd3-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
-   [<span data-ttu-id="75dd3-136">驗證原則</span><span class="sxs-lookup"><span data-stu-id="75dd3-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="75dd3-137">[使用基本驗證進行驗證](api-management-authentication-policies.md#Basic) - 使用基本驗證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="75dd3-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="75dd3-138">[使用用戶端憑證進行驗證](api-management-authentication-policies.md#ClientCertificate) - 使用用戶端憑證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="75dd3-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="75dd3-139">快取原則</span><span class="sxs-lookup"><span data-stu-id="75dd3-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="75dd3-140">[從快取中取得](api-management-caching-policies.md#GetFromCache) - 執行快取查閱並傳回有效的快取回應 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="75dd3-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="75dd3-141">[儲存 toocache](api-management-caching-policies.md#StoreToCache) -根據 toohello 快取回應指定快取控制組態。</span><span class="sxs-lookup"><span data-stu-id="75dd3-141">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches response according toohello specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="75dd3-142">[從快取取得值](api-management-caching-policies.md#GetFromCacheByKey) - 依金鑰擷取快取的項目。</span><span class="sxs-lookup"><span data-stu-id="75dd3-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="75dd3-143">[將值儲存在快取](api-management-caching-policies.md#StoreToCacheByKey)-hello 快取中儲存的項目，依索引鍵。</span><span class="sxs-lookup"><span data-stu-id="75dd3-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="75dd3-144">[從快取中移除值](api-management-caching-policies.md#RemoveCacheByKey)-hello 快取中移除項目，依索引鍵。</span><span class="sxs-lookup"><span data-stu-id="75dd3-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
-   [<span data-ttu-id="75dd3-145">跨網域原則</span><span class="sxs-lookup"><span data-stu-id="75dd3-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="75dd3-146">[允許跨網域呼叫](api-management-cross-domain-policies.md#AllowCrossDomainCalls)-從 Adobe Flash 和 Microsoft Silverlight 的瀏覽器型用戶端，讓 hello API 存取。</span><span class="sxs-lookup"><span data-stu-id="75dd3-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="75dd3-147">[CORS](api-management-cross-domain-policies.md#CORS) -將跨原始資源共用 (CORS) 支援 tooan 作業或 API tooallow 跨網域呼叫從瀏覽器型用戶端。</span><span class="sxs-lookup"><span data-stu-id="75dd3-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="75dd3-148">[JSONP](api-management-cross-domain-policies.md#JSONP) -將 JSON padding (JSONP) 支援 tooan 作業，或從 JavaScript 瀏覽器為基礎的用戶端的應用程式開發介面 tooallow 跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="75dd3-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="75dd3-149">轉換原則</span><span class="sxs-lookup"><span data-stu-id="75dd3-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="75dd3-150">[轉換 JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) -將要求或回應內文從 JSON tooXML。</span><span class="sxs-lookup"><span data-stu-id="75dd3-150">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
    -   <span data-ttu-id="75dd3-151">[轉換 XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) -將要求或回應內文從 XML tooJSON。</span><span class="sxs-lookup"><span data-stu-id="75dd3-151">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
    -   <span data-ttu-id="75dd3-152">[在內文中尋找並取代字串](api-management-transformation-policies.md#Findandreplacestringinbody) - 尋找要求或回應子字串，並將它取代為其他子字串。</span><span class="sxs-lookup"><span data-stu-id="75dd3-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="75dd3-153">[遮罩內容中的 Url](api-management-transformation-policies.md#MaskURLSContent) -重寫 （遮罩） 的連結，以 hello 回應內文，以便指向透過 hello 閘道 toohello 等同的連結。</span><span class="sxs-lookup"><span data-stu-id="75dd3-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
    -   <span data-ttu-id="75dd3-154">[設定後端服務](api-management-transformation-policies.md#SetBackendService)-變更連入要求的 hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="75dd3-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="75dd3-155">[設定主體](api-management-transformation-policies.md#SetBody)-設定傳入和傳出要求的 hello 訊息本文。</span><span class="sxs-lookup"><span data-stu-id="75dd3-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="75dd3-156">[設定 HTTP 標頭](api-management-transformation-policies.md#SetHTTPheader)-指派值 tooan 現有的回應和/或要求標頭，或加入新的回應和/或要求標頭。</span><span class="sxs-lookup"><span data-stu-id="75dd3-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="75dd3-157">[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter) - 新增、取代值或刪除要求查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="75dd3-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="75dd3-158">[請重寫 URL](api-management-transformation-policies.md#RewriteURL) -將要求 URL 的 hello web 服務所需要的公用格式 toohello 格式轉換。</span><span class="sxs-lookup"><span data-stu-id="75dd3-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
    -   <span data-ttu-id="75dd3-159">[使用 XSLT 的 XML 轉換](api-management-transformation-policies.md#XSLTransform)層套用 XSL 轉換 tooXML，hello 要求或回應主體中的。</span><span class="sxs-lookup"><span data-stu-id="75dd3-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="75dd3-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75dd3-160">Next steps</span></span>
<span data-ttu-id="75dd3-161">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="75dd3-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
