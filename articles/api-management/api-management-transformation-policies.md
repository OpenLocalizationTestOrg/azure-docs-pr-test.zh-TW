---
title: "aaaAzure API 管理轉換原則 |Microsoft 文件"
description: "深入了解 hello 轉換原則可在 Azure API 管理中使用。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a>API 管理轉換原則
本主題提供下列 API 管理原則的 hello 的參考。 如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。  
  
##  <a name="TransformationPolicies"></a> 轉換原則  
  
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
  
##  <a name="ConvertJSONtoXML"></a>轉換 JSON tooXML  
 hello`json-to-xml`原則將要求或回應內文從 JSON tooXML 中轉換。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|json-to-xml|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|apply|hello 屬性必須設定下列值的 hello 的 tooone。<br /><br /> -   always - 一律套用轉換。<br />-   content-type-json - 只有當回應中的 Content-type 標頭指出 JSON 存在時才轉換。|是|N/A|  
|consider-accept-header|hello 屬性必須設定下列值的 hello 的 tooone。<br /><br /> -   true - 如果在要求的 Accept 標頭中要求 JSON，才套用轉換。<br />-   false - 一律套用轉換。|否|true|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、錯誤  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="ConvertXMLtoJSON"></a>轉換 XML tooJSON  
 hello`xml-to-json`原則將要求或回應內文從 XML tooJSON 中轉換。 使用的 toomodernize 僅 XML 後端 web 服務為基礎的應用程式開發介面，可將此原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|xml-to-json|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|kind|hello 屬性必須設定下列值的 hello 的 tooone。<br /><br /> javascript-易記-hello 轉換的 JSON 具有表單易記 tooJavaScript 開發人員。<br />-直接-hello 轉換的 JSON 反映 hello 原始 XML 文件的結構。|是|N/A|  
|apply|hello 屬性必須設定下列值的 hello 的 tooone。<br /><br /> -   always - 一律轉換。<br />-   content-type-xml - 只有當回應中的 Content-type 標頭指出 XML 存在時才轉換。|是|N/A|  
|consider-accept-header|hello 屬性必須設定下列值的 hello 的 tooone。<br /><br /> -   true - 如果在要求的 Accept 標頭中要求 XML，才套用轉換。<br />-   false - 一律套用轉換。|否|true|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、錯誤  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="Findandreplacestringinbody"></a> 在本文中尋找並取代字串  
 hello`find-and-replace`原則尋找要求或回應子字串，並以不同的子字串取代。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>範例  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|find-and-replace|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|from|hello 字串 toosearch 的。|是|N/A|  
|to|hello 取代字串。 指定零長度的取代字串 tooremove hello 搜尋字串。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="MaskURLSContent"></a> 遮罩內容中的 URL  
 hello`redirect-content-urls`原則重寫 （遮罩） hello 回應主體中的連結，以便指向透過 hello 閘道 toohello 等同的連結。 使用在 hello 輸出區段 toore 寫入回應主體連結 toomake 它們點 toohello 閘道。 Hello 用於輸入產生相反效果 > 一節。  
  
> [!NOTE]
>  此原則不會變更任何標頭值，如 `Location` 標頭。 toochange 標頭值，會使用 hello[集標頭](api-management-transformation-policies.md#SetHTTPheader)原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>範例  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|redirect-content-urls|根元素。|是|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="SetBackendService"></a> 設定後端服務  
 使用 hello`set-backend-service`原則 tooredirect 傳入要求 tooa 不同的後端，比 hello hello API 設定該作業中指定的其中一個。 此原則的變更 hello 連入要求 toohello hello 原則中指定的其中一個的 hello 後端服務基礎的 URL。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
在此範例中的 hello 設定後端服務原則，將要求 hello 版本值傳入 hello 查詢字串 tooa 不同的後端服務於 hello 中所指定的一個 hello API 為基礎的路由。
  
一開始 hello 後端服務基礎 URL 被衍生自 hello API 設定。 因此 hello 要求 URL`https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef`變成`http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef`其中`http://contoso.com/api/10.4/`hello hello API 設定中指定的後端服務 url。  
  
當 hello [< 選擇\>](api-management-advanced-policies.md#choose)套用原則陳述 hello 後端服務基礎 URL 可能再次變更太`http://contoso.com/api/8.2`或`http://contoso.com/api/9.1`，端視 hello hello 版本要求查詢參數的值。 例如，如果 hello 值是`"2013-15"`hello URL 會成為最後一項要求`http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`。  
  
如果進一步的 hello 要求轉換為所需，其他[轉換原則](api-management-transformation-policies.md#TransformationPolicies)可用。 例如，tooremove hello 版本查詢參數，既然 hello 要求會被路由傳送 tooa 版本特定後端，hello[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter)原則可以是使用的 tooremove hello now 多餘版本屬性。  
  
### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
在此範例 hello 原則路由 hello 要求 tooa 服務網狀架構後端中，為 hello 資料分割索引鍵使用 hello userId 查詢字串，並使用 hello hello 磁碟分割的主要複本。  

### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|set-backend-service|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|base-url|新的後端服務基底 URL。|否|N/A|  
|backend-id|Hello 後端 tooroute 來識別項。|否|N/A|  
|sf-partition-key|僅適用於 Service Fabric 服務 hello 後端，並指定使用 ' 後端 id'。 使用 tooresolve 從 hello 名稱解析服務的特定分割區。|否|N/A|  
|sf-replica-type|僅適用於 Service Fabric 服務 hello 後端，並指定使用 ' 後端 id'。 控制是否 hello 要求應 toohello 主要或次要複本的磁碟分割。 |否|N/A|    
|sf-resolve-condition|僅適用於 Service Fabric 服務 hello 後端時。 識別條件如果 hello 呼叫 tooService 網狀架構後端有 toobe 重複使用新的解析度。|否|N/A|    
|sf-service-instance-name|僅適用於 Service Fabric 服務 hello 後端時。 在執行階段允許 toochange 服務執行個體。 |否|N/A|    

### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、後端  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="SetBody"></a> 設定本文  
 使用 hello`set-body`原則 tooset hello 訊息內文的傳入和傳出要求。 tooaccess hello 訊息本文，您可以使用 hello`context.Request.Body`屬性或 hello `context.Response.Body`，端視 hello 原則是否會在 hello 中輸入或輸出區段。  
  
> [!IMPORTANT]
>  請注意，根據預設，當您存取 hello 訊息本文會使用`context.Request.Body`或`context.Response.Body`，hello 原始訊息本文會遺失，而且必須設定藉由在 hello 運算式傳回 hello 主體。 toopreserve hello 本文內容，設定 hello`preserveContent`參數太`true`存取 hello 訊息時。 如果`preserveContent`設定得`true`和不同的主體傳回 hello 運算式 hello 主體使用。  
>   
>  請注意下列考量事項時使用 hello hello`set-body`原則。  
>   
>  -   如果您使用 hello`set-body`原則 tooreturn 新的或更新主體，您不需要 tooset`preserveContent`太`true`因為您可以明確地提供 hello 新本文內容。  
> -   保留回應的 hello 內容 hello 輸入管線中沒有意義，因為尚無回應。  
> -   Hello 內容要求的保留 hello 輸出管線中沒有意義因為 hello 要求已傳送 toohello 後端此時。  
> -   如果在沒有任何訊息本文時使用此原則，例如輸入 GET，會擲回例外狀況。  
  
 如需詳細資訊，請參閱 hello `context.Request.Body`， `context.Response.Body`，和 hello`IMessage`章節 hello[內容變數](api-management-policy-expressions.md#ContextVariables)資料表。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>範例  
  
#### <a name="literal-text-example"></a>常值文字範例  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>存取 hello 本文為字串的範例。 請注意，我們會保留 hello 原始要求主體，讓我們可以稍後在 hello 管線中存取它。
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>存取 hello 本文為 JObject 的範例。 請注意，由於我們不會保留 hello 的原始要求本文，而稍後在 hello 管線將會導致例外狀況的存取。  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a>根據產品篩選回應  
 這個範例會示範如何 tooperform 內容篩選的資料元素，移除 hello 回應 hello 後端服務時收到使用 hello`Starter`產品。 如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too34:30 向前快轉。 開始使用 31:50 toosee 概觀[hello 深色 Sky 預測 API](https://developer.forecast.io/)用於此示範。  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a>使用 Liquid 範本搭配設定本文 
hello`set-body`原則可以設定的 toouse hello[不固定](https://shopify.github.io/liquid/basics/introduction/)樣板化語言 tootransfom hello 主體的要求或回應。 這可以是訊息的非常有效，如果您需要 toocompletely 重繪 hello 格式。

> [!IMPORTANT]
> hello 實作用於 hello 液晶`set-body`原則設定為 'C# 模式'。 這在進行篩選之類的操作時尤其重要。 例如，使用日期篩選需要 hello 使用 Pascal 大小寫和 C# 的日期格式設定例如：
>
> {{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> 順序 toocorrectly 繫結 tooan XML 主體，使用 hello 不固定的範本，在使用`set-header`原則 tooset Content-type tooeither 應用程式/xml、 text/xml （或任何型別結尾 + xml）; JSON 主體，它必須是應用程式/json、 text/json （或任何類型結束與 + json)。

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>轉換 JSON tooSOAP 使用不固定範本
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a>使用 Liquid 範本來轉換 JSON
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|set-body|根元素。 包含 hello 本文文字或運算式傳回本文。|是|  

### <a name="properties"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|template|Hello 設定主體原則使用的 toochange hello 樣板化模式將會執行。 目前僅支援 hello 值為：<br /><br />-不固定-hello 設定主體的原則會使用 hello 不固定範本引擎 |否|liquid|  

對於存取 hello 要求和回應的相關資訊，請 hello 不固定範本可以繫結 tooa 內容物件，以 hello 下列屬性： <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="SetHTTPheader"></a> 設定 HTTP 標頭  
 hello`set-header`原則指派值 tooan 現有的回應和/或要求標頭，或加入新的回應和/或要求標頭。  
  
 將 HTTP 標頭清單插入至 HTTP 訊息中。 輸入管線中放置時，此原則設定 hello 傳遞 toohello 目標服務的 hello 要求的 HTTP 標頭。 輸出管線中放置時，此原則設定傳送 toohello 閘道用戶端 hello 回應 hello HTTP 標頭。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>範例  
  
#### <a name="example"></a>範例  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>轉送內容資訊 toohello 後端服務  
 這個範例會示範如何在 hello API tooapply 原則層級 toosupply 內容資訊 toohello 後端服務。 如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too10:30 向前快轉。 在 12:10 沒有您可以在其中看到 hello 原則，在工作中 hello 開發人員入口網站呼叫作業的示範。  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|set-header|根元素。|是|  
|value|指定 hello hello 標頭 toobe 組值。 多個標頭以 hello 相同的名稱加入更多`value`項目。|是|  
  
### <a name="properties"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|exists-action|Hello 標頭已指定時，請指定何種動作 tootake。 此屬性必須有 hello 下列值之一。<br /><br /> -覆寫-取代 hello hello 現有的標頭值。<br />-skip-不會取代 hello 現有標頭值。<br />-附加-附加 hello 值 toohello 現有標頭值。<br />-delete-從 hello 要求移除 hello 標頭。<br /><br /> 當設定太`override`編列多個項目以 hello 相同的名稱，正在設定相應 tooall 項目 （列出多次） hello 標頭中的結果; 只有列出的值會設定在 hello 結果。|否|override|  
|名稱|指定 hello 標頭 toobe 集的名稱。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="SetQueryStringParameter"></a> 設定查詢字串參數  
 hello`set-query-parameter`原則新增、 取代值，或刪除要求查詢字串參數。 可以是使用的 toopass hello 後端服務所需要的是選擇性的或永遠不會出現在 hello 要求查詢參數。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>範例  
  
#### <a name="example"></a>範例  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>轉送內容資訊 toohello 後端服務  
 這個範例會示範如何在 hello API tooapply 原則層級 toosupply 內容資訊 toohello 後端服務。 如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too10:30 向前快轉。 在 12:10 沒有您可以在其中看到 hello 原則，在工作中 hello 開發人員入口網站呼叫作業的示範。  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|set-query-parameter|根元素。|是|  
|value|指定 hello hello 查詢參數 toobe 集值。 多個查詢參數以 hello 相同的名稱新增額外`value`項目。|是|  
  
### <a name="properties"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|exists-action|已指定 hello 查詢參數時，請指定何種動作 tootake。 此屬性必須有 hello 下列值之一。<br /><br /> -覆寫-取代 hello hello 現有參數值。<br />-skip-不會取代 hello 現有的查詢參數值。<br />-附加-附加 hello 值 toohello 現有查詢的參數值。<br />-delete-從 hello 要求移除 hello 查詢參數。<br /><br /> 當設定太`override`編列多個項目以 hello 相同的名稱，正在設定相應 tooall 項目 （列出多次） hello 查詢參數中的結果; 只有列出的值會設定在 hello 結果。|否|override|  
|名稱|指定 hello 查詢參數 toobe 集的名稱。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、後端  
  
-   **原則範圍︰**全域、產品、API、作業  
  
##  <a name="RewriteURL"></a> 重寫 URL  
 hello`rewrite-uri`原則將轉換要求 URL 的公用格式 toohello 格式 hello web 服務所預期 hello 下列範例所示。  
  
-   公用 URL - `http://api.example.com/storenumber/ordernumber`  
  
-   要求 URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 人力和 （或) 瀏覽器易記 URL 應該轉換成 hello web 服務所預期的 hello URL 格式時，可以使用此原則。 此原則只需要套用公開替代 URL 格式，例如潔淨 Url、 RESTful Url、 使用者易記的 Url 或不包含查詢字串而改為包含只有 hello 路徑 hello 的純粹結構化 url 的 SEO 易記 Url 時 toobe（之後 hello 配置和 hello 授權） 的資源。 這樣做通常是基於美觀、實用性或搜尋引擎最佳化 (SEO) 目的。  
  
> [!NOTE]
>  您只能新增使用 hello 原則的查詢字串參數。 您無法加入額外的範本路徑參數，在 hello 重寫 URL。  

### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>範例  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|rewrite-uri|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|template|與任何查詢字串參數的 hello 實際的 web 服務 URL。 當使用運算式，hello 整個值必須是運算式。|是|N/A|  
|copy-unmatched-params|指定是否在 hello 內送要求不存在於 hello 原始 URL 範本中的查詢參數會加入 toohello hello 所定義的 URL 重新撰寫範本|否|true|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**產品、API、作業  
  
##  <a name="XSLTransform"></a> 使用 XSLT 轉換 XML  
 hello`Transform XML using an XSLT`原則會套用 XSL 轉換 tooXML，hello 要求或回應主體中的。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a>範例  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|xsl-transform|根元素。|是|  
|參數|使用的 toodefine hello 轉換中使用的變數|否|  
|xsl:stylesheet|根樣式表元素。 所有的項目和屬性內定義遵循 hello 標準[XSLT 規格](http://www.w3.org/TR/xslt)|是|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出  
  
-   **原則範圍︰**全域、產品、API、作業  
  
## <a name="next-steps"></a>後續步驟
如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。  
