---
title: "aaaAzure API 管理存取限制原則 |Microsoft 文件"
description: "深入了解 hello 存取限制原則可在 Azure API 管理中使用。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>API 管理存取限制原則
本主題提供下列 API 管理原則的 hello 的參考。 如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。  
  
##  <a name="AccessRestrictionPolicies"></a>存取限制原則  
  
-   [檢查 HTTP 標頭](api-management-access-restriction-policies.md#CheckHTTPHeader) - 強制必須存在和/或強制採用 HTTP 標頭的值。  
  
-   [依訂閱限制呼叫率](api-management-access-restriction-policies.md#LimitCallRate) - 以訂閱為單位，限制呼叫率以避免 API 使用量暴增。  
  
-   [依金鑰限制呼叫率](#LimitCallRateByKey) - 以金鑰為單位，限制呼叫率以避免 API 使用量暴增。  
  
-   [限制呼叫端 IP](api-management-access-restriction-policies.md#RestrictCallerIPs) - 篩選 (允許/拒絕) 來自特定 IP 位址和/或位址範圍的呼叫。  
  
-   [訂用帳戶所設定使用量配額](api-management-access-restriction-policies.md#SetUsageQuota)-可讓您以每個訂用帳戶為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。  
  
-   [設定使用量配額，依索引鍵](#SetUsageQuotaByKey)-可讓您以每個索引鍵為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。  
  
-   [驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT) - 強制擷取自指定 HTTP 標頭或指定查詢參數的 JWT 必須存在且有效。  
  
##  <a name="CheckHTTPHeader"></a>檢查 HTTP 標頭  
 使用 hello`check-header`原則 tooenforce 要求必須指定的 HTTP 標頭。 您可以選擇性地檢查 toosee，如果 hello 標頭所擁有的特定值或允許的值範圍的檢查。 如果 hello 檢查失敗，hello 原則終止要求處理，並傳回 hello HTTP 狀態碼和錯誤訊息 hello 原則所指定。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>範例  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|check-header|根元素。|是|  
|value|允許的 HTTP 標頭值。 當指定多個值的項目時，hello 則視為檢查成功 hello 值的任何一個是否符合項目。|否|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|failed-check-error-message|錯誤訊息 tooreturn hello 標頭不存在，或有無效的值如果 hello HTTP 回應主體中。 此訊息必須正確逸出任何特殊字元。|是|N/A|  
|failed-check-httpcode|HTTP 狀態碼 tooreturn 如果 hello 標頭不存在，或有無效的值。|是|N/A|  
|header-name|hello hello toocheck HTTP 標頭名稱。|是|N/A|  
|ignore-case|可以設定 tooTrue 或 False。 如果會比對可接受值的 hello 組 hello 標頭值時，會忽略 set tooTrue 案例。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="LimitCallRate"></a>依訂用帳戶限制呼叫頻率  
 hello`rate-limit`原則防止 API 使用量暴增的每個訂用帳戶為基礎，藉由限制 hello 呼叫速率 tooa 指定數字，每個指定的時間期間。 觸發此原則時 hello 呼叫端會收到`429 Too Many Requests`回應狀態碼。  
  
> [!IMPORTANT]
>  每份原則文件只能使用此原則一次。  
>   
>  [原則運算式](api-management-policy-expressions.md)不能在任何 hello 原則屬性的這個原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|set-limit|根元素。|是|  
|api|應用程式開發介面中新增一或多個這些項目 tooimpose 呼叫率限制 hello 產品中。 產品和 API 呼叫頻率限制會獨立套用。|否|  
|operation|加入一或多個這些項目 tooimpose 呼叫率限制對 API 內的作業。 產品、API 和作業呼叫頻率限制會獨立套用。|否|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|名稱|hello 名稱 hello API tooapply hello 速率限制。|是|N/A|  
|calls|hello 的 hello hello 中指定的時間間隔內允許的呼叫總數上限`renewal-period`。|是|N/A|  
|renewal-period|hello 時間期間 （秒） 之後 hello 重設配額。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**產品  
  
##  <a name="LimitCallRateByKey"></a>依金鑰限制呼叫頻率  
 hello`rate-limit-by-key`原則防止 API 使用量暴增的每個索引鍵為基礎，藉由限制 hello 呼叫速率 tooa 指定數字，每個指定的時間期間。 hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。 選擇性的遞條件可以加入的 toospecify 哪些要求應該計入 hello 限制。 觸發此原則時 hello 呼叫端會收到`429 Too Many Requests`回應狀態碼。  
  
 如需此原則範例的詳細資訊，請參閱[以 Azure API 管理進行進階要求節流](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)。  
  
> [!IMPORTANT]
>  每份原則文件只能使用此原則一次。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>範例  
 在下列範例的 hello，hello 速率限制是以 hello 呼叫端的 IP 位址做為索引。  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|set-limit|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|calls|hello 的 hello hello 中指定的時間間隔內允許的呼叫總數上限`renewal-period`。|是|N/A|  
|counter-key|hello 金鑰 toouse hello 速率限制原則。|是|N/A|  
|increment-condition|指定是否 hello 要求應該計數算入 hello 配額的 hello 布林運算式 (`true`)。|否|N/A|  
|renewal-period|hello 時間期間 （秒） 之後 hello 重設配額。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="RestrictCallerIPs"></a>限制呼叫端 IP  
 hello`ip-filter`原則會篩選 （允許/拒絕） 來自特定 IP 位址和/或位址範圍的呼叫。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>範例  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|ip-filter|根元素。|是|  
|位址|哪些 toofilter 上指定單一 IP 位址。|至少需要一個 `address` 或 `address-range` 元素。|  
|address-range from="位址" to="位址"|哪些 toofilter 上指定的 IP 位址範圍。|至少需要一個 `address` 或 `address-range` 元素。|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|address-range from="位址" to="位址"|範圍的 IP 位址 tooallow 或拒絕存取。|需要： 當 hello`address-range`使用項目。|N/A|  
|ip-filter action="allow &#124; forbid"|指定呼叫應允許還是不會針對 hello 指定 IP 位址和範圍。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="SetUsageQuota"></a>依訂用帳戶設定使用量配額  
 hello`quota`原則會強制執行的可更新的或存留期呼叫量和/或頻寬配額限制時，每個訂用帳戶為基礎。  
  
> [!IMPORTANT]
>  每份原則文件只能使用此原則一次。  
>   
>  [原則運算式](api-management-policy-expressions.md)不能在任何 hello 原則屬性的這個原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|quota|根元素。|是|  
|api|應用程式開發介面中新增一或多個這些項目 tooimpose 配額 hello 產品中。 產品和 API 配額會獨立套用。|否|  
|operation|加入一或多個這些項目 tooimpose 配額對 API 內的作業。 產品、API 和作業配額會獨立套用。|否|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|名稱|hello 的 hello API 或操作的 hello 套用配額的名稱。|是|N/A|  
|bandwidth|hello 的 hello hello 中指定的時間間隔內允許的 kb 總數上限`renewal-period`。|必須指定 `calls`、`bandwidth`，或同時指定兩者。|N/A|  
|calls|hello 的 hello hello 中指定的時間間隔內允許的呼叫總數上限`renewal-period`。|必須指定 `calls`、`bandwidth`，或同時指定兩者。|N/A|  
|renewal-period|hello 時間期間 （秒） 之後 hello 重設配額。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**產品  
  
##  <a name="SetUsageQuotaByKey"></a>依金鑰設定使用量配額  
 hello`quota-by-key`原則會強制執行的可更新的或存留期呼叫量和/或頻寬配額限制時，每個索引鍵為基礎。 hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。 選擇性的遞條件可以加入的 toospecify 哪些要求應該計入 hello 配額。  
  
 如需此原則範例的詳細資訊，請參閱[以 Azure API 管理進行進階要求節流](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)。  
  
> [!IMPORTANT]
>  每份原則文件只能使用此原則一次。  
>   
>  [原則運算式](api-management-policy-expressions.md)不能在任何 hello 原則屬性的這個原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>範例  
 在下列範例的 hello，hello 配額是做為索引鍵使用 hello 呼叫端的 IP 位址。  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|quota|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|bandwidth|hello 的 hello hello 中指定的時間間隔內允許的 kb 總數上限`renewal-period`。|必須指定 `calls`、`bandwidth`，或同時指定兩者。|N/A|  
|calls|hello 的 hello hello 中指定的時間間隔內允許的呼叫總數上限`renewal-period`。|必須指定 `calls`、`bandwidth`，或同時指定兩者。|N/A|  
|counter-key|hello 金鑰 toouse hello 配額原則。|是|N/A|  
|increment-condition|指定是否 hello 要求應該計數算入 hello 配額的 hello 布林運算式 (`true`)|否|N/A|  
|renewal-period|hello 時間期間 （秒） 之後 hello 重設配額。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="ValidateJWT"></a>驗證 JWT  
 hello`validate-jwt`原則會強制執行是否存在，並從任一指定 HTTP 標頭或指定的查詢參數擷取的 JWT 的有效性。  
  
> [!IMPORTANT]
>  hello`validate-jwt`原則需要該 hello`exp`已註冊的宣告是在 hello JWT 權杖中，所含，除非`require-expiration-time`屬性會指定並設定得`false`。  
> hello`validate-jwt`原則支援 HS256 和 RS256 簽章演算法。 HS256 hello 金鑰還必須提供內嵌 hello base64 編碼格式的 hello 原則內。 如 RS256 hello 金鑰都有 toobe 提供透過 Open ID 組態端點。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>範例  
  
#### <a name="azure-mobile-services-token-validation"></a>Azure 行動服務權杖驗證  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Azure Active Directory 權杖驗證  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Azure Active Directory B2C 權杖驗證  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>授權權杖的宣告為基礎的存取 toooperations  
 這個範例會示範如何 toouse hello[驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT)原則 toopre-授權存取 toooperations 權杖宣告為基礎。 如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too13:50 向前快轉。 向前快轉 too15:00 toosee hello 原則在 hello 原則編輯器中設定，然後示範從 hello 開發人員入口網站及 hello 未呼叫作業的 too18:50 所需授權權杖。  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|validate-jwt|根元素。|是|  
|audiences|包含可存在於 hello 語彙基元的可接受的對象宣告的清單。 如果存在多個受眾值，則會嘗試每個值，直到全部試完 (即表示驗證失敗) 或其中一個值成功為止。 必須指定至少一個受眾。|否|  
|issuer-signing-keys|一份 base-64 編碼安全性金鑰使用 toovalidate 簽署權杖。 如果存在多個安全性金鑰，則會嘗試每個金鑰，直到全部試完 (即表示驗證失敗) 或其中一個金鑰成功 (很適合用於權杖變換) 為止。 索引鍵項目有選用`id`針對屬性使用 toomatch`kid`宣告。|否|  
|issuers|可接受的主體發出 hello 權杖清單。 如果存在多個簽發者值，則會嘗試每個值，直到全部試完 (即表示驗證失敗) 或其中一個值成功為止。|否|  
|openid-config|用來指定要從中簽署金鑰和簽發者可以取得相容 Open ID 組態端點的 hello 項目。|否|  
|required-claims|包含一份存在於它的 hello 語彙基元上宣告 toobe toobe 視為有效。 當 hello`match`屬性設定太`all`hello 原則中的每個宣告值必須位於為驗證 toosucceed hello 語彙基元。 當 hello`match`屬性設定太`any`至少一個宣告中必須要有 hello 語彙基元的驗證 toosucceed。|否|  
|zumo-master-key|Azure 行動服務所簽發之權杖的主要金鑰|否|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|clock-skew|時間範圍。 提供些許 hello 權杖的逾期宣告存在於 hello 語彙基元，而且已超出 hello 目前日期 / 時間。|否|0 秒|  
|failed-validation-error-message|如果 hello JWT 未通過驗證的 hello HTTP 回應主體中的錯誤訊息 tooreturn。 此訊息必須正確逸出任何特殊字元。|否|預設錯誤訊息視驗證問題而定，例如「JWT 不存在」。|  
|failed-validation-httpcode|HTTP 狀態碼 tooreturn 如果 hello JWT 未通過驗證。|否|401|  
|header-name|hello 持有 hello 語彙基元的 hello HTTP 標頭名稱。|必須指定 `header-name` 或 `query-paremeter-name`；但不能同時指定。|N/A|  
|id|hello`id`屬性 hello`key`元素可讓您將會比對的 toospecify hello 字串`kid`hello 出 hello 適當索引鍵的 toouse 簽章驗證的語彙基元 （如果有的話） toofind 中宣告。|否|N/A|  
|match|hello`match`屬性 hello`claim`項目會指定是否必須存在於 hello 語彙基元的驗證 toosucceed hello 原則中的每個宣告值。 可能的值包括：<br /><br /> -                          `all`-hello 原則中的每個宣告值必須位於為驗證 toosucceed hello 語彙基元。<br /><br /> -                          `any`-至少一個宣告值必須位於為驗證 toosucceed hello 語彙基元。|否|所有|  
|query-paremeter-name|hello hello hello 查詢參數可保留 hello 語彙基元名稱。|必須指定 `header-name` 或 `query-paremeter-name`；但不能同時指定。|N/A|  
|require-expiration-time|布林值。 指定是否 hello 語彙基元必須有逾期宣告。|否|true|
|require-scheme|hello 配置的名稱 hello 語彙基元，例如："Bearer"。 當設定這個屬性時，可確保 hello 原則，指定之結構描述存在於 hello 授權標頭值。|否|N/A|
|require-signed-tokens|布林值。 指定權杖是否需要的 toobe 簽署。|否|true|  
|url|可從中取得 Open ID 設定中繼資料的 Open ID 設定端點 URL。 Azure Active Directory，請使用下列 URL 的 hello:`https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration`以取代您目錄租用戶的名稱，例如`contoso.onmicrosoft.com`。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**全域、產品、API、作業  
  
## <a name="next-steps"></a>後續步驟
如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。  
