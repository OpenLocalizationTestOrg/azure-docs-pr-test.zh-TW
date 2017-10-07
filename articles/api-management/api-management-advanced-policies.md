---
title: "aaaAzure API 管理進階原則 |Microsoft 文件"
description: "深入了解 hello 進階原則可在 Azure API 管理中使用。"
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a>API 管理進階原則
本主題提供下列 API 管理原則的 hello 的參考。 如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。  
  
##  <a name="AdvancedPolicies"></a>進階原則  
  
-   [控制流程](api-management-advanced-policies.md#choose)-有條件地套用原則陳述式，根據 hello hello 評估的布林值結果[運算式](api-management-policy-expressions.md)。  
  
-   [要求轉寄](#ForwardRequest)-轉送 hello 要求 toohello 後端服務。

-   [限制並行](#LimitConcurrency)-防止括住執行超過一次 hello 指定的數目之要求的原則。
  
-   [記錄 tooEvent 中樞](#log-to-eventhub)-將訊息傳送嗨中的指定的格式 tooan 記錄器實體所定義的事件中樞。 

-   [模擬回應](#mock-response)-中止管線執行，並傳回模擬的回應直接 toohello 呼叫端。
  
-   [重試](#Retry)-重試執行 hello 括住原則陳述，如果，直到符合 hello 條件為止。 執行，就會重複在 hello 指定的時間間隔向上 toohello 指定重試計數。  
  
-   [將回應傳回](#ReturnResponse)-中止管線執行並傳回 hello 指定回應直接 toohello 呼叫端。 
  
-   [其中一種方式要求傳送](#SendOneWayRequest)-傳送要求 toohello 指定 URL，而不必等候回應。  
  
-   [傳送要求](#SendRequest)-傳送要求 toohello 指定 URL。  

-   [設定 HTTP proxy](#SetHttpProxy) -可讓您透過 HTTP proxy 的 tooroute 轉寄要求。  

-   [將要求方法設定](#SetRequestMethod)-可讓您要求的 toochange hello HTTP 方法。  
  
-   [設定狀態碼](#SetStatus)-變更 hello HTTP 狀態碼 toohello 指定的值。  
  
-   [設定變數](api-management-advanced-policies.md#set-variable) - 保存具名[內容](api-management-policy-expressions.md#ContextVariables)變數中的值，供日後存取使用。  

-   [追蹤](#Trace)-將字串新增至 hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。  
  
-   [等候](#Wait)-括住，等候[傳送要求](api-management-advanced-policies.md#SendRequest)，[取得值，從快取](api-management-caching-policies.md#GetFromCacheByKey)，或[控制流程](api-management-advanced-policies.md#choose)原則 toocomplete 後再繼續。  
  
##  <a name="choose"></a>控制流程  
 hello`choose`原則適用於 hello 布林運算式，類似 tooan if-then-其他或參數的評估結果為基礎的陳述式會建構的程式語言中括住的原則。  
  
###  <a name="ChoosePolicyStatement"></a>原則陳述式  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 hello 控制流程原則必須包含至少一個`<when/>`項目。 hello`<otherwise/>`是選擇性項目。 中的條件`<when/>`hello 原則內其出現的順序進行評估的項目。 原則陳述式先住 hello`<when/>`元素條件屬性等於`true`將會套用。 Hello 括住的原則`<otherwise/>`會套用項目，如果有的話，如果要將所有的 hello`<when/>`元素條件屬性都是`false`。  
  
### <a name="examples"></a>範例  
  
####  <a name="ChooseExample"></a>範例  
 hello 下列範例會示範[-set-variable-](api-management-advanced-policies.md#set-variable)原則和兩個控制流程原則。  
  
 hello 設定變數原則位於 hello 輸入的區段，並建立`isMobile`布林[內容](api-management-policy-expressions.md#ContextVariables)變數時 hello 設定 tootrue`User-Agent`要求標頭包含的 hello 文字`iPad`或`iPhone`。  
  
 hello 第一個控制流程原則位於也 hello 輸入的區段，並有條件地套用兩個的其中一個[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter)hello 的值而定 hello 原則`isMobile`內容變數。  
  
 第二個控制流程原則 hello hello 輸出區段中，有條件地套用 hello[轉換 XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON)原則時`isMobile`設定得`true`。  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a>範例  
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
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|choose|根元素。|是|  
|when|hello hello 的條件 toouse`if`或`ifelse`部分 hello`choose`原則。 如果 hello`choose`原則有多個`when`章節中，依序評估。 一次 hello`condition`時的項目評估太`true`，沒有其他進一步`when`評估條件。|是|  
|otherwise|包含使用 如果沒有 hello hello 原則程式碼片段 toobe`when`條件的評估太`true`。|否|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|  
|---------------|-----------------|--------------|  
|condition="Boolean expression &#124; Boolean constant"|hello 布林運算式或常數 tooevaluated 當 hello 包含`when`會評估原則陳述式。|是|  
  
###  <a name="ChooseUsage"></a>使用方式  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  
  
##  <a name="ForwardRequest"></a>轉送要求  
 hello`forward-request`原則轉送 hello 連入要求 toohello 後端服務 hello 要求中指定[內容](api-management-policy-expressions.md#ContextVariables)。 hello 後端服務 URL 中指定 hello API[設定](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings)，而且可以使用 hello 變更[設定後端服務](api-management-transformation-policies.md)原則。  
  
> [!NOTE]
>  移除不會轉送 toohello 後端服務和 hello 原則 hello 輸出區段中的 hello 要求此原則會產生 hello hello 中的 hello 原則成功完成時立即評估輸入 > 一節。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>範例  
  
#### <a name="example"></a>範例  
 hello 下列應用程式開發介面層級的原則會轉送所有要求 toohello 後端服務的逾時間隔為 60 秒。  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>範例  
 這個作業層級原則使用 hello `base` hello 父應用程式開發介面層級範圍的項目 tooinherit hello 後端原則。  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>範例  
 此作業層級原則明確會轉送所有要求 toohello 後端服務逾時值為 120，而且沒有繼承 hello 父應用程式開發介面層級的後端原則。  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>範例  
 此作業層級原則不會轉送要求 toohello 後端服務。  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|forward-request|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|timeout="integer"|hello 逾時間隔，以秒為單位 hello 呼叫 toohello 後端服務之前就會失敗。|否|無逾時|  
|follow-redirects="true &#124; false"|指定從 hello 後端服務的重新導向是後面接著 hello 閘道或傳回 toohello 呼叫端。|否|false|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**後端  
  
-   **原則範圍：**所有範圍  
  
##  <a name="LimitConcurrency"></a> 限制並行  
 hello`limit-concurrency`原則防止括住的原則執行的多個 hello 指定的數目之要求在指定的時間。 當超出 hello 臨界值，新的要求都會加入 tooa 佇列，直到 hello 最大佇列長度為止。 在佇列耗盡時，新的要求會立即失敗。
  
###  <a name="LimitConcurrencyStatement"></a>原則陳述式  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>範例  
  
####  <a name="ChooseExample"></a>範例  
 hello 下列範例示範如何要求 toolimit 數目轉寄 tooa hello 的內容變數的值為基礎的後端。
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|    
|limit-concurrency|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|--------------|  
|key|字串。 允許的運算式。 指定 hello 並行存取範圍。 可由多個原則共用。|是|N/A|  
|max-count|整數。 指定允許 tooenter hello 原則的要求的數目上限。|是|N/A|  
|timeout|整數。 允許的運算式。 指定的要求應該等候 tooenter 範圍而失敗之前的秒 hello 數 「 403 太多要求 」|否|Infinity|  
|max-queue-length|整數。 允許的運算式。 指定 hello 最大佇列長度。 嘗試 tooenter 的連入要求此原則將會終止並 「 403 太多要求 」 立即耗盡 hello 佇列時。|否|Infinity|  
  
###  <a name="ChooseUsage"></a>使用方式  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  

##  <a name="log-to-eventhub"></a>記錄 tooEvent 中樞  
 hello`log-to-eventhub`原則會傳送 hello 訊息指定格式 tooan 記錄器實體所定義的事件中樞。 正如其名，hello 原則用來儲存所選的要求或回應的內容資訊線上或離線分析。  
  
> [!NOTE]
>  如需設定事件中樞與記錄事件的逐步指南，請參閱[如何為 Azure 事件中心 toolog API 管理事件](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/)。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>範例  
 任何字串可以當做 hello 值 toobe 記錄在事件中心。 在此範例中 hello 日期和時間，部署服務名稱、 要求識別碼、 ip 位址和所有的傳入呼叫的作業名稱會以 hello 註冊的記錄器記錄的 toohello 事件中心`contoso-logger`識別碼。  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|log-to-eventhub|根元素。 這個項目 hello 值為 hello 字串 toolog tooyour 事件中心。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|  
|---------------|-----------------|--------------|  
|logger-id|hello 識別碼 hello 記錄器註冊您的 API 管理服務。|是|  
|partition-id|指定 hello hello 訊息傳送的分割區索引。|選用。 如果使用 `partition-key`，就不能使用這個屬性。|  
|partition-key|指定 hello 訊息傳送時用於資料分割指派的值。|選用。 如果使用 `partition-id`，就不能使用這個屬性。|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  

##  <a name="mock-response"></a> Mock 回應  
hello `mock-response`，做為 hello 名稱表示，是使用 toomock 應用程式開發介面和作業。 它會中止正常管線執行，並傳回模擬的回應 toohello 呼叫端。 hello 原則一律會嘗試最高逼真度 tooreturn 的回應。 它偏好使用回應內容範例 (若可使用)。 當提供結構描述而無提供範例時，它會從結構描述產生範例回應。 如果沒有找到範例或結構描述，則會傳回沒有內容的回應。
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>範例  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|mock-response|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|--------------|  
|status-code|指定回應狀態碼，並使用的 tooselect 對應的範例或結構描述。|否|200|  
|Content-Type|指定`Content-Type`回應標頭值，而且是使用的 tooselect 對應的範例或結構描述。|否|None|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、錯誤  
  
-   **原則範圍：**所有範圍

##  <a name="Retry"></a>重試  
 hello`retry`原則執行它的子原則一次，然後重試 hello 重試之前執行`condition`變成`false`或重試`count`已用盡。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a>範例  
 Hello 在下列範例要求 forewarding 會重試總 tooten 時間使用指數重試演算法。 因為`first-fast-retry`設定 toofalse，所有的重試次數是主體 toohello exponsntial 重試演算法。  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|retry|根元素。 可包含其他任何原則來做為其子元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|condition|布林常值或[運算式](api-management-policy-expressions.md)，指定應停止 (`false`) 還是繼續 (`true`) 重試。|是|N/A|  
|計數|指定的重試 tooattempt hello 最大數目的正數。|是|N/A|  
|interval|以秒為單位指定 hello hello 重試嘗試之間的等待間隔正數。|是|N/A|  
|max-interval|以秒為單位指定 hello hello 重試嘗試之間的最長等待間隔正數。 它是使用的 tooimplement 指數重試演算法。|否|N/A|  
|delta|以秒為單位指定 hello 等待間隔遞增正數。 它是使用的 tooimplement hello 線性和指數重試演算法。|否|N/A|  
|first-fast-retry|如果設定太`true`，hello 第一次重試嘗試會立即執行。|否|`false`|  
  
> [!NOTE]
>  當只有 hello`interval`指定，則**固定**間隔重試執行。  
>  當只有 hello`interval`和`delta`都有指定，**線性**使用間隔重試演算法，其中的重試之間的等待時間是導出的相應 hello 下列公式- `interval + (count - 1)*delta`。  
>  當 hello `interval`，`max-interval`和`delta`都有指定，**指數**間隔重試演算法會套用 hello hello 重試之間的等待時間出現指數型成長hello值`interval`toohello 值`max-interval`根據 toohello 下列 forumula- `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`。  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。 請注意，此原則會繼承子原則的使用方式限制。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  
  
##  <a name="ReturnResponse"></a>傳回回應  
 hello`return-response`中止管線執行原則，並傳回預設或自訂回應 toohello 呼叫端。 預設回應是 `200 OK`，且沒有本文。 透過內容變數或原則陳述式即可指定自訂回應。 當同時提供時，hello 回應 hello 內容變數中包含以 hello 原則陳述式前會先修改傳回 toohello 呼叫端。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>範例  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|return-response|根元素。|是|  
|set-header|[set-header](api-management-transformation-policies.md#SetHTTPheader) 原則陳述式。|否|  
|set-body|[set-body](api-management-transformation-policies.md#SetBody) 原則陳述式。|否|  
|set-status|[set-status](api-management-advanced-policies.md#SetStatus) 原則陳述式。|否|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|  
|---------------|-----------------|--------------|  
|response-variable-name|hello hello 內容變數的參考名稱，例如，上游[傳送要求](api-management-advanced-policies.md#SendRequest)原則，並包含`Response`物件|選用。|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  
  
##  <a name="SendOneWayRequest"></a>傳送單向要求  
 hello`send-one-way-request`原則傳送嗨提供要求 toohello 指定 URL，而不必等候回應。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>範例  
 此原則的範例示範使用 hello`send-one-way-request`原則 toosend 訊息 tooa Slack 聊天室如果 hello HTTP 回應碼大於或等於 too500。 如需有關此範例的詳細資訊，請參閱[使用來自 hello Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|send-one-way-request|根元素。|是|  
|url|hello hello 要求 URL。|mode=copy 時為 [否]；否則為 [是]。|  
|method|hello hello 要求的 HTTP 方法。|mode=copy 時為 [否]；否則為 [是]。|  
|頁首|要求標頭。 若有多個要求標頭，請使用多個 header 元素。|否|  
|body|hello 要求主體。|否|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|判斷這是否為新的要求或是 hello 目前要求的複本。 在輸出模式中，模式 = 複本不會初始化 hello 要求主體。|否|新增|  
|名稱|指定 hello hello 標頭 toobe 集名稱。|是|N/A|  
|exists-action|Hello 標頭已指定時，請指定何種動作 tootake。 此屬性必須有 hello 下列值之一。<br /><br /> -覆寫-取代 hello hello 現有的標頭值。<br />-skip-不會取代 hello 現有標頭值。<br />-附加-附加 hello 值 toohello 現有標頭值。<br />-delete-從 hello 要求移除 hello 標頭。<br /><br /> 當設定太`override`編列多個項目以 hello 相同的名稱，正在設定相應 tooall 項目 （列出多次） hello 標頭中的結果; 只有列出的值會設定在 hello 結果。|否|override|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  
  
##  <a name="SendRequest"></a>傳送要求  
 hello`send-request`原則傳送 hello 提供要求 toohello 指定 URL，不會再等候非 hello 設定逾時值。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>範例  
 這個範例會示範其中一種方式 tooverify 參考權杖，向授權伺服器。 如需有關此範例的詳細資訊，請參閱[使用來自 hello Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|send-request|根元素。|是|  
|url|hello hello 要求 URL。|mode=copy 時為 [否]；否則為 [是]。|  
|method|hello hello 要求的 HTTP 方法。|mode=copy 時為 [否]；否則為 [是]。|  
|頁首|要求標頭。 若有多個要求標頭，請使用多個 header 元素。|否|  
|body|hello 要求主體。|否|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|判斷這是否為新的要求或是 hello 目前要求的複本。 在輸出模式中，模式 = 複本不會初始化 hello 要求主體。|否|新增|  
|response-variable-name="string"|如果不存在，則會使用 `context.Response`。|否|N/A|  
|timeout="integer"|hello 逾時間隔，以秒為單位 hello 呼叫之前 toohello URL 將會失敗。|否|60|  
|ignore-error|如果為 true，而且 hello 要求會導致錯誤：<br /><br /> -   如果已指定 response-variable-name，它會包含 null 值。<br />-   如果未指定 response-variable-name，則不會更新 context.Request。|否|false|  
|名稱|指定 hello hello 標頭 toobe 集名稱。|是|N/A|  
|exists-action|Hello 標頭已指定時，請指定何種動作 tootake。 此屬性必須有 hello 下列值之一。<br /><br /> -覆寫-取代 hello hello 現有的標頭值。<br />-skip-不會取代 hello 現有標頭值。<br />-附加-附加 hello 值 toohello 現有標頭值。<br />-delete-從 hello 要求移除 hello 標頭。<br /><br /> 當設定太`override`編列多個項目以 hello 相同的名稱，正在設定相應 tooall 項目 （列出多次） hello 標頭中的結果; 只有列出的值會設定在 hello 結果。|否|override|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  
  
##  <a name="SetHttpProxy"></a> 設定 HTTP Proxy  
 hello`proxy`原則可讓您將要求轉送 toobackends tooroute 透過 HTTP proxy。 HTTP (不是 HTTPS) 支援 hello 閘道與 hello proxy 之間。 僅限基本和 NTLM 驗證。
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>範例  
請注意 hello 使用[屬性](api-management-howto-properties.md)為 hello 使用者名稱和密碼 tooavoid hello 原則文件中儲存機密資訊的值。  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|proxy|根元素|是|  

### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|url="string"|Http://host:port hello 形式的 proxy URL。|是|N/A|  
|username="string"|用來與 hello proxy 進行驗證的使用者名稱 toobe。|否|N/A|  
|password="string"|密碼 toobe 用於 hello proxy 驗證。|否|N/A|  

### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍：**所有範圍  

##  <a name="SetRequestMethod"></a>設定要求方法  
 hello`set-method`原則可讓您要求 toochange hello HTTP 要求方法。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>範例  
 此範例原則使用 hello`set-method`原則會顯示傳送訊息 tooa Slack 聊天室的案例，如果 hello HTTP 回應碼大於或等於 too500 的範例。 如需有關此範例的詳細資訊，請參閱[使用來自 hello Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|set-method|根元素。 hello hello 項目的值指定 hello HTTP 方法。|是|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、錯誤  
  
-   **原則範圍：**所有範圍  
  
##  <a name="SetStatus"></a>設定狀態碼  
 hello`set-status`原則集 hello HTTP 狀態碼 toohello 指定的值。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>範例  
 這個範例會示範如何 tooreturn 401 回應 hello 授權權杖是否無效。 如需詳細資訊，請參閱[使用來自 hello Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|set-status|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|code="integer"|hello HTTP 狀態碼 tooreturn。|是|N/A|  
|reason="string"|傳回狀態碼為 hello hello 原因的描述。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  

##  <a name="set-variable"></a>設定變數  
 hello`set-variable`原則宣告[內容](api-management-policy-expressions.md#ContextVariables)變數並將其指派值，指定透過[運算式](api-management-policy-expressions.md)或字串常值。 如果 hello 運算式包含常值會轉換 tooa 字串和 hello hello 值類型會是`System.String`。  
  
###  <a name="set-variablePolicyStatement"></a>原則陳述式  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a>範例  
 hello 下列範例會示範設定變數原則在 hello 輸入 > 一節。 此設定變數原則建立`isMobile`布林[內容](api-management-policy-expressions.md#ContextVariables)變數時 hello 設定 tootrue`User-Agent`要求標頭包含的 hello 文字`iPad`或`iPhone`。  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|set-variable|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|  
|---------------|-----------------|--------------|  
|名稱|hello hello 變數名稱。|是|  
|value|hello hello 變數值。 此值可為運算式或常值。|是|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  
  
###  <a name="set-variableAllowedTypes"></a>允許的類型  
 Hello 中使用的運算式`set-variable`原則必須傳回 hello 下列基本類型的其中一個。  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a>追蹤  
 hello`trace`原則會將字串新增到 hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。 hello 原則將會執行只追蹤會觸發時，也就是`Ocp-Apim-Trace`要求標頭是否存在並設定太`true`和`Ocp-Apim-Subscription-Key`要求標頭存在，並保留 hello 系統管理員帳戶相關聯的有效索引鍵。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|trace|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|來源|字串常值有意義的 toohello 追蹤檢視器與指定的 hello 來源的 hello 訊息。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端、錯誤  
  
-   **原則範圍：**所有範圍  
  
##  <a name="Wait"></a>等候  
 hello`wait`原則以平行方式，執行其直屬子原則，並完成之前，等待所有或其中一個其直屬子原則 toocomplete。 hello 等候原則可以有為其直屬子原則[傳送要求](api-management-advanced-policies.md#SendRequest)，[取得值，從快取](api-management-caching-policies.md#GetFromCacheByKey)，和[控制流程](api-management-advanced-policies.md#choose)原則。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>範例  
 下列範例中的 hello 中有兩個`choose`直屬子原則的 hello 原則`wait`原則。 在這些 `choose` 原則中，每一個都會以平行方式執行。 每個`choose`原則嘗試 tooretrieve 快取的值。 如果沒有快取遺漏後, 端服務稱為 tooprovide hello 值。 在此範例 hello`wait`原則才會完成所有其直屬子原則完成，因為 hello`for`屬性設定太`all`。   在此範例 hello 內容變數 (`execute-branch-one`， `value-one`， `execute-branch-two`，和`value-two`) 宣告此範例原則 hello 範圍之外。  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a>元素  
  
|元素|說明|必要|  
|-------------|-----------------|--------------|  
|wait|根元素。 只能包含做為子元素 `send-request`、`cache-lookup-value` 和 `choose` 原則。|是|  
  
### <a name="attributes"></a>屬性  
  
|屬性|說明|必要|預設值|  
|---------------|-----------------|--------------|-------------|  
|for|決定是否 hello`wait`原則等候完成的所有直接子原則 toobe 或只有一個。 允許的值包括：<br /><br /> -   `all`-等候所有直接子原則 toocomplete<br />-任何-等候任何直接子原則 toocomplete。 第一個直屬子原則 hello 完成後，請 hello`wait`原則完成，並終止執行的其他直屬子原則。|否|所有|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入、輸出、後端  
  
-   **原則範圍：**所有範圍  
  
## <a name="next-steps"></a>後續步驟
如需使用原則的詳細資訊，請參閱︰
-   [API 管理中的原則](api-management-howto-policies.md) 
-   [原則運算式](api-management-policy-expressions.md)
