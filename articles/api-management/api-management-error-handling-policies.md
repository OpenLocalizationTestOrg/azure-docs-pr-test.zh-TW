---
title: "在 Azure API 管理原則中處理 aaaError |Microsoft 文件"
description: "了解如何 toorespond tooerror 條件期間可能發生的 hello Azure API 管理中的要求處理。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>API 管理原則中的錯誤處理
Azure API 管理可讓 「 發行者 」 所提供的要求 toohello proxy hello 處理期間可能發生的 toorespond tooerror 條件`ProxyError`物件。 hello`ProxyError`物件經由 hello[內容。LastError](api-management-policy-expressions.md#ContextVariables)屬性和可供在 hello 原則`on-error`原則 > 一節。 本主題提供的參考 hello 錯誤處理功能，在 Azure API 管理。  
  
## <a name="error-handling-in-api-management"></a>API 管理中的錯誤處理  
 在 Azure API 管理原則可分為`inbound`， `backend`， `outbound`，和`on-error`區段 hello 下列範例所示。  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Hello 在處理期間的要求，以及在 hello 要求的範圍內的任何原則執行內建的步驟。 如果發生錯誤時，會立即處理跳 toohello`on-error`原則 > 一節。 hello`on-error`原則 區段中可用在任何範圍，而且應用程式開發介面的 「 發行者 」 可以設定自訂的行為，例如記錄 hello 錯誤 tooevent 集線器或建立新的回應 tooreturn toohello 呼叫端。  
  
> [!NOTE]
>  hello`on-error`區段不存在預設原則中。 tooadd hello`on-error`區段 tooa 原則，瀏覽 hello 原則編輯器 中的預期 toohello 原則並將它加入。 如需如何設定原則的詳細資訊，請參閱 [API 管理中的原則](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/)。  
>   
>  如果沒有 `on-error` 區段，在發生錯誤狀況時，呼叫端將會收到 400 或 500 HTTP 回應訊息。  
  
### <a name="policies-allowed-in-on-error"></a>on-error 中允許的原則  
 hello 下列原則可用於 hello`on-error`原則 > 一節。  
  
-   [choose](api-management-advanced-policies.md#choose)  
  
-   [set-variable](api-management-advanced-policies.md#set-variable)  
  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [return-response](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set-method](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [set-status](api-management-advanced-policies.md#SetStatus)  
  
-   [send-request](api-management-advanced-policies.md#SendRequest)  
  
-   [send-one-way-request](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [log-to-eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 當發生錯誤，並控制跳躍 toohello `on-error` hello 錯誤會儲存原則 區段中，在[內容。LastError](api-management-policy-expressions.md#ContextVariables)屬性可存取的原則中 hello`on-error`區段，並具有下列屬性的 hello。  
  
|名稱|類型|說明|必要|  
|----------|----------|-----------------|--------------|  
|來源|字串|發生錯誤 hello 名稱 hello 項目。 可能是原則或內建的管線步驟名稱。|是|  
|原因|字串|方便電腦理解的錯誤碼，可用於處理錯誤。|否|  
|訊息|字串|人類可以看懂的錯誤描述。|是|  
|Scope|字串|Hello 領域其中 hello，發生錯誤可能是其中一個 「 全域 」、 「 產品 」、 「 api 」 或 「 作業 」 的名稱|否|  
|區段|字串|發生錯誤的區段名稱，此名稱可為「輸入」、「後端」、「輸出」或「錯誤」其中之一。|否|  
|Path|字串|指定巢狀原則，例如「choose[3]/when[2]」。|否|  
|PolicyId|字串|值為 hello`id`屬性，如果指定 hello 客戶，hello 原則時發生錯誤|否|  
  
> [!NOTE]
>  所有的原則有選用`id`hello 原則 toohello 根項目可加入的屬性。 如果這個屬性在原則中的錯誤狀況發生時，則可以使用 hello 擷取 hello hello 屬性值`context.LastError.PolicyId`屬性。  
  
## <a name="predefined-errors-for-built-in-steps"></a>內建步驟的預先定義錯誤  
 hello 下列錯誤已預先定義的內建的處理步驟的 hello 評估期間可能發生的錯誤狀況。  
  
|來源|條件|原因|訊息|  
|------------|---------------|------------|-------------|  
|組態|Uri 不符合 tooany 應用程式開發介面或作業|OperationNotFound|內送要求 tooan 作業無法 toomatch。|  
|授權|未提供訂用帳戶金鑰|SubscriptionKeyNotFound|存取被拒，因為 toomissing 訂閱金鑰。 進行要求 toothis API 時，請確定 tooinclude 訂閱金鑰。|  
|授權|訂用帳戶金鑰值無效|SubscriptionKeyInvalid|存取被拒，因為 tooinvalid 訂閱金鑰。 請確定 tooprovide 有效的訂用帳戶的有效索引鍵。|  
  
## <a name="predefined-errors-for-policies"></a>原則的預先定義錯誤  
 hello 下列錯誤會預先定義的原則評估期間可能發生的錯誤狀況。  
  
|來源|條件|原因|訊息|  
|------------|---------------|------------|-------------|  
|rate-limit|超過了速率限制|RateLimitExceeded|超過速率限制|  
|quota|超過配額|QuotaExceeded|呼叫量配額不足。 會在 xx:xx:xx 中補充配額。 -或- 頻寬配額不足。 會在 xx:xx:xx 中補充配額。|  
|jsonp|回呼參數值無效 (包含錯誤的字元)|CallbackParameterInvalid|回呼參數 {callback-parameter-name} 的值不是有效的 JavaScript 識別碼。|  
|ip-filter|從要求失敗的 tooparse 呼叫端 IP|FailedToParseCallerIP|無法 tooestablish hello 呼叫端的 IP 位址。 拒絕存取。|  
|ip-filter|呼叫端 IP 不在允許清單中|CallerIpNotAllowed|不允許呼叫端 IP 位址 {ip-address}。 拒絕存取。|  
|ip-filter|呼叫端 IP 位於封鎖清單中|CallerIpBlocked|呼叫端 IP 位址遭到封鎖。 拒絕存取。|  
|check-header|所需標頭不存在或找不到值|HeaderNotFound|Hello 要求中找不到標頭 {標頭-名稱}。 拒絕存取。|  
|check-header|所需標頭不存在或找不到值|HeaderValueNotAllowed|不允許標頭 {header-name} 值 {header-value}。 拒絕存取。|  
|validate-jwt|要求中沒有 Jwt 權杖|TokenNotFound|JWT hello 要求中找不到。 拒絕存取。|  
|validate-jwt|簽章驗證失敗|TokenSignatureInvalid|<來自 jwt 程式庫的訊息\>。 拒絕存取。|  
|validate-jwt|無效的對象|TokenAudienceNotAllowed|<來自 jwt 程式庫的訊息\>。 拒絕存取。|  
|validate-jwt|無效的簽發者|TokenIssuerNotAllowed|<來自 jwt 程式庫的訊息\>。 拒絕存取。|  
|validate-jwt|權杖過期|TokenExpired|<來自 jwt 程式庫的訊息\>。 拒絕存取。|  
|validate-jwt|識別碼未解析簽章金鑰|TokenSignatureKeyNotFound|<來自 jwt 程式庫的訊息\>。 拒絕存取。|  
|validate-jwt|權杖中沒有必要的宣告|TokenClaimNotFound|JWT 權杖中遺漏 hello 下列宣告： < c1\>，< c2\>，... 拒絕存取。|  
|validate-jwt|宣告值不相符|TokenClaimValueNotAllowed|不允許宣告 {claim-name} 值 {claim-value}。 拒絕存取。|  
|validate-jwt|其他驗證失敗|JwtInvalid|<來自 jwt 程式庫的訊息\>|

## <a name="next-steps"></a>後續步驟
如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。  