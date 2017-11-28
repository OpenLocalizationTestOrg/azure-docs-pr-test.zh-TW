---
title: "aaaAzure API 管理原則參考"
description: "深入了解 hello 原則可用 tooconfigure API 管理。"
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="2a9ec-103">Azure API 管理原則參考文件</span><span class="sxs-lookup"><span data-stu-id="2a9ec-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="2a9ec-104">本節提供在 hello hello 原則索引[API 管理原則參考][API Management policy reference]。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="2a9ec-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則][Policies in API Management]。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="2a9ec-106">除非另外指定 hello 原則，可以使用原則運算式做為屬性值或任何 hello API 管理原則中的文字值。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="2a9ec-107">某些原則，例如 hello[控制流程][ Control flow]和[設定變數][ Set variable]原則為基礎的原則運算式。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="2a9ec-108">如需詳細資訊，請參閱[進階原則][Advanced policies]和[原則運算式][Policy expressions]</span><span class="sxs-lookup"><span data-stu-id="2a9ec-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="2a9ec-109">原則參考索引</span><span class="sxs-lookup"><span data-stu-id="2a9ec-109">Policy reference index</span></span>
* <span data-ttu-id="2a9ec-110">[存取限制原則][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="2a9ec-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="2a9ec-111">[檢查 HTTP 標頭][Check HTTP header] - 強制必須存在和/或強制採用 HTTP 標頭的值。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="2a9ec-112">[依訂用帳戶限制呼叫率][Limit call rate by subscription] - 以訂用帳戶為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="2a9ec-113">[依金鑰限制呼叫率](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - 以金鑰為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="2a9ec-114">[限制呼叫端 IP][Restrict caller IPs] - 篩選 (允許/拒絕) 來自特定 IP 位址和/或位址範圍的呼叫。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="2a9ec-115">[訂用帳戶所設定使用量配額][ Set usage quota by subscription] -可讓您以每個訂用帳戶為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="2a9ec-116">[設定使用量配額，依索引鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey)-可讓您以每個索引鍵為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="2a9ec-117">[驗證 JWT][Validate JWT] - 強制擷取自指定 HTTP 標頭或指定查詢參數的 JWT 必須存在且有效。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="2a9ec-118">[進階原則][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="2a9ec-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="2a9ec-119">[控制流程][ Control flow] -有條件地套用原則陳述式，根據 hello hello 評估的布林值結果[運算式][expressions]。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="2a9ec-120">[要求轉寄][ Forward request] -轉送 hello 要求 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="2a9ec-121">[記錄 tooEvent 中樞][ Log tooEvent Hub] -傳送訊息中所定義的 hello 指定的格式 tooa 訊息目標[記錄器](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger)實體。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="2a9ec-122">[重試](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry)-重試執行 hello 括住原則陳述，如果，直到符合 hello 條件為止。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="2a9ec-123">執行，就會重複在 hello 指定的時間間隔向上 toohello 指定重試計數。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="2a9ec-124">[將回應傳回](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse)-中止管線執行並傳回 hello 指定回應直接 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="2a9ec-125">[其中一種方式要求傳送](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest)-傳送要求 toohello 指定 URL，而不必等候回應。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="2a9ec-126">[傳送要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest)-傳送要求 toohello 指定 URL。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="2a9ec-127">[將要求方法設定](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod)-可讓您要求的 toochange hello HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="2a9ec-128">[設定狀態](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus)-變更 hello HTTP 狀態碼 toohello 指定的值。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="2a9ec-129">[設定變數][Set variable] - 保存具名 [context][context] 變數中的值，供日後存取使用。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="2a9ec-130">[追蹤](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace)-將字串新增至 hello [API Inspector](api-management-howto-api-inspector.md)輸出。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="2a9ec-131">[等候](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait)-等候括住傳送的要求，從快取中，取得值，或控制流程原則 toocomplete 後再繼續。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="2a9ec-132">[驗證原則][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="2a9ec-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="2a9ec-133">[使用基本驗證進行驗證][Authenticate with Basic] - 使用基本驗證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="2a9ec-134">[使用用戶端憑證進行驗證][Authenticate with client certificate] - 使用用戶端憑證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="2a9ec-135">[快取原則][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="2a9ec-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="2a9ec-136">[從快取中取得][Get from cache] - 執行快取查閱並傳回有效的快取回應 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="2a9ec-137">[儲存 toocache] [ Store toocache] -根據 toohello 快取回應指定快取控制組態。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="2a9ec-138">[從快取取得值](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - 依金鑰擷取快取的項目。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="2a9ec-139">[將值儲存在快取](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey)-hello 快取中儲存的項目，依索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="2a9ec-140">[從快取中移除值](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey)-hello 快取中移除項目，依索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="2a9ec-141">[跨網域原則][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="2a9ec-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="2a9ec-142">[允許跨網域呼叫][ Allow cross-domain calls] -從 Adobe Flash 和 Microsoft Silverlight 的瀏覽器型用戶端，讓 hello API 存取。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="2a9ec-143">[CORS] [ CORS] -將跨原始資源共用 (CORS) 支援 tooan 作業或 API tooallow 跨網域呼叫從瀏覽器型用戶端。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="2a9ec-144">[JSONP] [ JSONP] -將 JSON padding (JSONP) 支援 tooan 作業，或從 JavaScript 瀏覽器為基礎的用戶端的應用程式開發介面 tooallow 跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="2a9ec-145">[轉換原則][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="2a9ec-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="2a9ec-146">[轉換 JSON tooXML] [ Convert JSON tooXML] -將要求或回應內文從 JSON tooXML。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="2a9ec-147">[轉換 XML tooJSON] [ Convert XML tooJSON] -將要求或回應內文從 XML tooJSON。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="2a9ec-148">[在內文中尋找並取代字串][Find and replace string in body] - 尋找要求或回應子字串，並替換為其他子字串。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="2a9ec-149">[遮罩內容中的 Url] [ Mask URLs in content] -重寫 （遮罩） 的連結，以 hello 回應內文，以便指向透過 hello 閘道 toohello 等同的連結。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="2a9ec-150">[設定後端服務][ Set backend service] -變更連入要求的 hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="2a9ec-151">[設定主體][ Set body] -設定傳入和傳出要求的 hello 訊息本文。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="2a9ec-152">[設定 HTTP 標頭][ Set HTTP header] -指派值 tooan 現有的回應和/或要求標頭，或加入新的回應和/或要求標頭。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="2a9ec-153">[設定查詢字串參數][Set query string parameter] - 新增、取代值或刪除要求查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="2a9ec-154">[請重寫 URL] [ Rewrite URL] -將要求 URL 的 hello web 服務所需要的公用格式 toohello 格式轉換。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a9ec-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a9ec-155">Next steps</span></span>
<span data-ttu-id="2a9ec-156">如需有關原則運算式的詳細資訊，請參閱下列視訊 hello。</span><span class="sxs-lookup"><span data-stu-id="2a9ec-156">For more information on policy expressions, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


