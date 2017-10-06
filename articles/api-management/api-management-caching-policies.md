---
title: "aaaAzure API 管理快取原則 |Microsoft 文件"
description: "深入了解快取原則可供使用，在 Azure API 管理中的 hello。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>API 管理快取原則
本主題提供下列 API 管理原則的 hello 的參考。 如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。  
  
##  <a name="CachingPolicies"></a>快取原則  
  
-   回應快取原則  
  
    -   [從快取中取得](api-management-caching-policies.md#GetFromCache) - 執行快取查閱並傳回有效的快取回應 (如果有的話)。  
  
    -   [儲存 toocache](api-management-caching-policies.md#StoreToCache) -根據 toohello 指定快取控制組態快取回應。  
  
-   值快取原則  
  
    -   [從快取取得值](#GetFromCacheByKey) - 依金鑰擷取快取的項目。  
  
    -   [將值儲存在快取](#StoreToCacheByKey)-hello 快取中儲存的項目，依索引鍵。  
  
    -   [從快取中移除值](#RemoveCacheByKey)-hello 快取中移除項目，依索引鍵。  
  
##  <a name="GetFromCache"></a>從快取中取得  
 使用 hello`cache-lookup`原則 tooperform 快取查閱，並傳回有效的快取回的應的話。 此原則可於回應內容在一段期間維持靜態時套用。 回應快取可減少頻寬和處理需求加諸於 hello 後端 web 伺服器，並降低延遲 API 取用者看得見。  
  
> [!NOTE]
>  此原則必須有對應[存放區 toocache](api-management-caching-policies.md#StoreToCache)原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>範例  
  
#### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>使用原則運算式的範例  
 這個範例會示範如何 tootooconfigure API 管理回應快取持續時間比對 hello 回應 hello hello 所指定的後端服務快取備份服務的`Cache-Control`指示詞。 如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too25:25 向前快轉。  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|cache-lookup|根元素。|是|  
|vary-by-header|根據指定標頭 (例如 Accept、Accept-Charset、Accept-Encoding、Accept-Language、Authorization、Expect、From、Host、If-Match) 的值開始快取回應。|否|  
|vary-by-query-parameter|根據指定查詢參數的值開始快取回應。 輸入單一或多個參數。 使用分號作為分隔符號。 如果未指定任何參數，則會使用所有查詢參數。|否|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|allow-private-response-caching|當設定太`true`，好讓快取的要求包含授權標頭。|否|false|  
|downstream-caching-type|這個屬性必須設定下列值的 hello 的 tooone。<br /><br /> -   none - 不允許下游快取。<br />-   private - 允許下游私人快取。<br />-   public - 允許私人和共用下游快取。|否|無|  
|must-revalidate|這個屬性下游快取啟用時開啟或關閉 hello`must-revalidate`閘道回應中的快取控制指示詞。|否|true|  
|vary-by-developer|設定得`true`toocache 回應每個開發人員索引鍵。|否|false|  
|vary-by-developer-groups|設定得`true`toocache 回應每個使用者角色。|否|false|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**API、作業、產品  
  
##  <a name="StoreToCache"></a>存放區 toocache  
 hello`cache-store`根據 toohello 原則快取的回應指定快取設定。 此原則可於回應內容在一段期間維持靜態時套用。 回應快取可減少頻寬和處理需求加諸於 hello 後端 web 伺服器，並降低延遲 API 取用者看得見。  
  
> [!NOTE]
>  此原則必須有對應的[從快取中取得](api-management-caching-policies.md#GetFromCache)原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>範例  
  
#### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>使用原則運算式的範例  
 這個範例會示範如何 tootooconfigure API 管理回應快取持續時間比對 hello 回應 hello hello 所指定的後端服務快取備份服務的`Cache-Control`指示詞。 如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too25:25 向前快轉。  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|cache-store|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|duration|存留時間的 hello 快取項目，以秒為單位指定。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸出  
  
-   **原則範圍︰**API、作業、產品  
  
##  <a name="GetFromCacheByKey"></a>從快取取得值  
 使用 hello`cache-lookup-value`原則 tooperform 查閱快取索引鍵，並傳回快取的值。 hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。  
  
> [!NOTE]
>  此原則必須有對應的[儲存快取中的值](#StoreToCacheByKey)原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>範例  
 如需此原則的詳細資訊和範例，請參閱[在 Azure API 管理中自訂快取](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)。  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|cache-lookup-value|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|default-value|將會指派 toohello 變數，如果 hello 快取索引鍵查閱產生遺漏值。 如果未指定此屬性，則會指派 `null`。|否|`null`|  
|key|快取索引鍵值 toouse hello 查閱中。|是|N/A|  
|variable-name|名稱的 hello[內容變數](api-management-policy-expressions.md#ContextVariables)hello 查閱值會指派給，如果查閱成功。 如果查詢結果中遺漏，hello 變數將值指派給 hello hello`default-value`屬性或`null`，如果 hello`default-value`省略屬性。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍︰**全域、API、作業、產品  
  
##  <a name="StoreToCacheByKey"></a>儲存快取中的值  
 hello`cache-store-value`執行快取存放區索引鍵。 hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。  
  
> [!NOTE]
>  此原則必須有對應的[從快取取得值](#GetFromCacheByKey)原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>範例  
 如需此原則的詳細資訊和範例，請參閱[在 Azure API 管理中自訂快取](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)。  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|cache-store-value|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|duration|將快取 hello 提供持續時間值，指定以秒為單位的值。|是|N/A|  
|key|快取索引鍵的 hello 值將會儲存在下。|是|N/A|  
|value|hello 值 toobe 快取。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍︰**全域、API、作業、產品  
  
###  <a name="RemoveCacheByKey"></a>移除快取中的值  
 hello`cache-remove-value`刪除快取項目由其索引鍵識別。 hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。  
  
#### <a name="policy-statement"></a>原則陳述式  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>範例  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|cache-remove-value|根元素。|是|  
  
#### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|key|hello 索引鍵的 hello 先前快取值 toobe 從 hello 快取中移除。|是|N/A|  
  
#### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍︰**全域、API、作業、產品  
  

## <a name="next-steps"></a>後續步驟
如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。  