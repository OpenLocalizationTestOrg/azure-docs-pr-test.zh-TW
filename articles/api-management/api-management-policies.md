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
# <a name="api-management-policies"></a>API 管理原則
本節提供下列 API 管理原則的 hello 參考。 如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。  
  
 原則是 hello 的透過組態 API toochange hello 行為允許 hello publisher 的 hello 系統的強大功能。 原則是循序 hello 要求上執行的陳述式的集合或應用程式開發介面的回應。 受歡迎的陳述式包含從 XML tooJSON 格式轉換，並呼叫速率限制為開發人員的來電 toorestrict hello 數量。 更多原則是可用的 hello 方塊。  
  
 除非另外指定 hello 原則，可以使用原則運算式做為屬性值或任何 hello API 管理原則中的文字值。 某些原則，例如 hello[控制流程](api-management-advanced-policies.md#choose)和[設定變數](api-management-advanced-policies.md#set-variable)原則為基礎的原則運算式。 如需詳細資訊，請參閱[進階原則](api-management-advanced-policies.md#AdvancedPolicies)和[原則運算式](api-management-policy-expressions.md)。  
  
##  <a name="ProxyPolicies"></a> 原則  
  
-   [存取限制原則](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [檢查 HTTP 標頭](api-management-access-restriction-policies.md#CheckHTTPHeader) - 強制必須存在和/或強制採用 HTTP 標頭的值。  
  
    -   [依訂閱限制呼叫率](api-management-access-restriction-policies.md#LimitCallRate) - 以訂閱為單位，限制呼叫率以避免 API 使用量暴增。  
  
    -   [依金鑰限制呼叫率](api-management-access-restriction-policies.md#LimitCallRateByKey) - 以金鑰為單位，限制呼叫率以避免 API 使用量暴增。  
  
    -   [限制呼叫端 IP](api-management-access-restriction-policies.md#RestrictCallerIPs) - 篩選 (允許/拒絕) 來自特定 IP 位址和/或位址範圍的呼叫。  
  
    -   [訂用帳戶所設定使用量配額](api-management-access-restriction-policies.md#SetUsageQuota)-可讓您以每個訂用帳戶為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。  
  
    -   [設定使用量配額，依索引鍵](api-management-access-restriction-policies.md#SetUsageQuotaByKey)-可讓您以每個索引鍵為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。  
  
    -   [驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT) - 強制擷取自指定 HTTP 標頭或指定查詢參數的 JWT 必須存在且有效。  
  
-   [進階原則](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [控制流程](api-management-advanced-policies.md#choose)-有條件地套用原則陳述式，根據 hello 評估布林運算式。  
  
    -   [要求轉寄](api-management-advanced-policies.md#ForwardRequest)-轉送 hello 要求 toohello 後端服務。  
  
    -   [記錄 tooEvent 中樞](api-management-advanced-policies.md#log-to-eventhub)-傳送 hello 指定的格式 tooa 訊息目標記錄器實體所定義的訊息。  
  
    -   [重試](api-management-advanced-policies.md#Retry)-重試執行 hello 括住原則陳述，如果，直到符合 hello 條件為止。 執行，就會重複在 hello 指定的時間間隔向上 toohello 指定重試計數。  
  
    -   [將回應傳回](api-management-advanced-policies.md#ReturnResponse)-中止管線執行並傳回 hello 指定回應直接 toohello 呼叫端。  
  
    -   [其中一種方式要求傳送](api-management-advanced-policies.md#SendOneWayRequest)-傳送要求 toohello 指定 URL，而不必等候回應。  
  
    -   [傳送要求](api-management-advanced-policies.md#SendRequest)-傳送要求 toohello 指定 URL。  
  
    -   [設定變數](api-management-advanced-policies.md#set-variable) - 將值保存在具名的 context 變數中以供日後存取。  
  
    -   [將要求方法設定](api-management-advanced-policies.md#SetRequestMethod)-可讓您要求的 toochange hello HTTP 方法。  
  
    -   [設定狀態碼](api-management-advanced-policies.md#SetStatus)-變更 hello HTTP 狀態碼 toohello 指定的值。  
  
    -   [追蹤](api-management-advanced-policies.md#Trace)-將字串新增至 hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。  
  
    -   [等候](api-management-advanced-policies.md#Wait)-括住，等候[傳送要求](api-management-advanced-policies.md#SendRequest)，[取得值，從快取](api-management-caching-policies.md#GetFromCacheByKey)，或[控制流程](api-management-advanced-policies.md#choose)原則 toocomplete 後再繼續。  
  
-   [驗證原則](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [使用基本驗證進行驗證](api-management-authentication-policies.md#Basic) - 使用基本驗證來驗證後端服務。  
  
    -   [使用用戶端憑證進行驗證](api-management-authentication-policies.md#ClientCertificate) - 使用用戶端憑證來驗證後端服務。  
  
-   [快取原則](api-management-caching-policies.md#CachingPolicies)  
  
    -   [從快取中取得](api-management-caching-policies.md#GetFromCache) - 執行快取查閱並傳回有效的快取回應 (如果有的話)。  
  
    -   [儲存 toocache](api-management-caching-policies.md#StoreToCache) -根據 toohello 快取回應指定快取控制組態。  
  
    -   [從快取取得值](api-management-caching-policies.md#GetFromCacheByKey) - 依金鑰擷取快取的項目。  
  
    -   [將值儲存在快取](api-management-caching-policies.md#StoreToCacheByKey)-hello 快取中儲存的項目，依索引鍵。  
  
    -   [從快取中移除值](api-management-caching-policies.md#RemoveCacheByKey)-hello 快取中移除項目，依索引鍵。  
  
-   [跨網域原則](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [允許跨網域呼叫](api-management-cross-domain-policies.md#AllowCrossDomainCalls)-從 Adobe Flash 和 Microsoft Silverlight 的瀏覽器型用戶端，讓 hello API 存取。  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -將跨原始資源共用 (CORS) 支援 tooan 作業或 API tooallow 跨網域呼叫從瀏覽器型用戶端。  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) -將 JSON padding (JSONP) 支援 tooan 作業，或從 JavaScript 瀏覽器為基礎的用戶端的應用程式開發介面 tooallow 跨網域呼叫。  
  
-   [轉換原則](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [轉換 JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) -將要求或回應內文從 JSON tooXML。  
  
    -   [轉換 XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) -將要求或回應內文從 XML tooJSON。  
  
    -   [在內文中尋找並取代字串](api-management-transformation-policies.md#Findandreplacestringinbody) - 尋找要求或回應子字串，並將它取代為其他子字串。  
  
    -   [遮罩內容中的 Url](api-management-transformation-policies.md#MaskURLSContent) -重寫 （遮罩） 的連結，以 hello 回應內文，以便指向透過 hello 閘道 toohello 等同的連結。  
  
    -   [設定後端服務](api-management-transformation-policies.md#SetBackendService)-變更連入要求的 hello 後端服務。  
  
    -   [設定主體](api-management-transformation-policies.md#SetBody)-設定傳入和傳出要求的 hello 訊息本文。  
  
    -   [設定 HTTP 標頭](api-management-transformation-policies.md#SetHTTPheader)-指派值 tooan 現有的回應和/或要求標頭，或加入新的回應和/或要求標頭。  
  
    -   [設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter) - 新增、取代值或刪除要求查詢字串參數。  
  
    -   [請重寫 URL](api-management-transformation-policies.md#RewriteURL) -將要求 URL 的 hello web 服務所需要的公用格式 toohello 格式轉換。  
  
    -   [使用 XSLT 的 XML 轉換](api-management-transformation-policies.md#XSLTransform)層套用 XSL 轉換 tooXML，hello 要求或回應主體中的。  
  
## <a name="next-steps"></a>後續步驟
如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。  
