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
# <a name="api-management-advanced-policies"></a><span data-ttu-id="ff361-103">API 管理進階原則</span><span class="sxs-lookup"><span data-stu-id="ff361-103">API Management advanced policies</span></span>
<span data-ttu-id="ff361-104">本主題提供下列 API 管理原則的 hello 的參考。</span><span class="sxs-lookup"><span data-stu-id="ff361-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="ff361-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="ff361-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="ff361-106"><a name="AdvancedPolicies"></a>進階原則</span><span class="sxs-lookup"><span data-stu-id="ff361-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="ff361-107">[控制流程](api-management-advanced-policies.md#choose)-有條件地套用原則陳述式，根據 hello hello 評估的布林值結果[運算式](api-management-policy-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="ff361-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="ff361-108">[要求轉寄](#ForwardRequest)-轉送 hello 要求 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="ff361-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="ff361-109">[限制並行](#LimitConcurrency)-防止括住執行超過一次 hello 指定的數目之要求的原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="ff361-110">[記錄 tooEvent 中樞](#log-to-eventhub)-將訊息傳送嗨中的指定的格式 tooan 記錄器實體所定義的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ff361-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="ff361-111">[模擬回應](#mock-response)-中止管線執行，並傳回模擬的回應直接 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="ff361-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="ff361-112">[重試](#Retry)-重試執行 hello 括住原則陳述，如果，直到符合 hello 條件為止。</span><span class="sxs-lookup"><span data-stu-id="ff361-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="ff361-113">執行，就會重複在 hello 指定的時間間隔向上 toohello 指定重試計數。</span><span class="sxs-lookup"><span data-stu-id="ff361-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="ff361-114">[將回應傳回](#ReturnResponse)-中止管線執行並傳回 hello 指定回應直接 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="ff361-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="ff361-115">[其中一種方式要求傳送](#SendOneWayRequest)-傳送要求 toohello 指定 URL，而不必等候回應。</span><span class="sxs-lookup"><span data-stu-id="ff361-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="ff361-116">[傳送要求](#SendRequest)-傳送要求 toohello 指定 URL。</span><span class="sxs-lookup"><span data-stu-id="ff361-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="ff361-117">[設定 HTTP proxy](#SetHttpProxy) -可讓您透過 HTTP proxy 的 tooroute 轉寄要求。</span><span class="sxs-lookup"><span data-stu-id="ff361-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="ff361-118">[將要求方法設定](#SetRequestMethod)-可讓您要求的 toochange hello HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="ff361-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="ff361-119">[設定狀態碼](#SetStatus)-變更 hello HTTP 狀態碼 toohello 指定的值。</span><span class="sxs-lookup"><span data-stu-id="ff361-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="ff361-120">[設定變數](api-management-advanced-policies.md#set-variable) - 保存具名[內容](api-management-policy-expressions.md#ContextVariables)變數中的值，供日後存取使用。</span><span class="sxs-lookup"><span data-stu-id="ff361-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="ff361-121">[追蹤](#Trace)-將字串新增至 hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。</span><span class="sxs-lookup"><span data-stu-id="ff361-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="ff361-122">[等候](#Wait)-括住，等候[傳送要求](api-management-advanced-policies.md#SendRequest)，[取得值，從快取](api-management-caching-policies.md#GetFromCacheByKey)，或[控制流程](api-management-advanced-policies.md#choose)原則 toocomplete 後再繼續。</span><span class="sxs-lookup"><span data-stu-id="ff361-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="ff361-123"><a name="choose"></a>控制流程</span><span class="sxs-lookup"><span data-stu-id="ff361-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="ff361-124">hello`choose`原則適用於 hello 布林運算式，類似 tooan if-then-其他或參數的評估結果為基礎的陳述式會建構的程式語言中括住的原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="ff361-125"><a name="ChoosePolicyStatement"></a>原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
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
  
 <span data-ttu-id="ff361-126">hello 控制流程原則必須包含至少一個`<when/>`項目。</span><span class="sxs-lookup"><span data-stu-id="ff361-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="ff361-127">hello`<otherwise/>`是選擇性項目。</span><span class="sxs-lookup"><span data-stu-id="ff361-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="ff361-128">中的條件`<when/>`hello 原則內其出現的順序進行評估的項目。</span><span class="sxs-lookup"><span data-stu-id="ff361-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="ff361-129">原則陳述式先住 hello`<when/>`元素條件屬性等於`true`將會套用。</span><span class="sxs-lookup"><span data-stu-id="ff361-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="ff361-130">Hello 括住的原則`<otherwise/>`會套用項目，如果有的話，如果要將所有的 hello`<when/>`元素條件屬性都是`false`。</span><span class="sxs-lookup"><span data-stu-id="ff361-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="ff361-131">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-131">Examples</span></span>  
  
####  <span data-ttu-id="ff361-132"><a name="ChooseExample"></a>範例</span><span class="sxs-lookup"><span data-stu-id="ff361-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="ff361-133">hello 下列範例會示範[-set-variable-](api-management-advanced-policies.md#set-variable)原則和兩個控制流程原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="ff361-134">hello 設定變數原則位於 hello 輸入的區段，並建立`isMobile`布林[內容](api-management-policy-expressions.md#ContextVariables)變數時 hello 設定 tootrue`User-Agent`要求標頭包含的 hello 文字`iPad`或`iPhone`。</span><span class="sxs-lookup"><span data-stu-id="ff361-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="ff361-135">hello 第一個控制流程原則位於也 hello 輸入的區段，並有條件地套用兩個的其中一個[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter)hello 的值而定 hello 原則`isMobile`內容變數。</span><span class="sxs-lookup"><span data-stu-id="ff361-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="ff361-136">第二個控制流程原則 hello hello 輸出區段中，有條件地套用 hello[轉換 XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON)原則時`isMobile`設定得`true`。</span><span class="sxs-lookup"><span data-stu-id="ff361-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="ff361-137">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-137">Example</span></span>  
 <span data-ttu-id="ff361-138">這個範例會示範如何 tooperform 內容篩選的資料元素，移除 hello 回應 hello 後端服務時收到使用 hello`Starter`產品。</span><span class="sxs-lookup"><span data-stu-id="ff361-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="ff361-139">如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too34:30 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="ff361-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="ff361-140">開始使用 31:50 toosee 概觀[hello 深色 Sky 預測 API](https://developer.forecast.io/)用於此示範。</span><span class="sxs-lookup"><span data-stu-id="ff361-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-141">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-141">Elements</span></span>  
  
|<span data-ttu-id="ff361-142">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-142">Element</span></span>|<span data-ttu-id="ff361-143">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-143">Description</span></span>|<span data-ttu-id="ff361-144">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-145">choose</span><span class="sxs-lookup"><span data-stu-id="ff361-145">choose</span></span>|<span data-ttu-id="ff361-146">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-146">Root element.</span></span>|<span data-ttu-id="ff361-147">是</span><span class="sxs-lookup"><span data-stu-id="ff361-147">Yes</span></span>|  
|<span data-ttu-id="ff361-148">when</span><span class="sxs-lookup"><span data-stu-id="ff361-148">when</span></span>|<span data-ttu-id="ff361-149">hello hello 的條件 toouse`if`或`ifelse`部分 hello`choose`原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="ff361-150">如果 hello`choose`原則有多個`when`章節中，依序評估。</span><span class="sxs-lookup"><span data-stu-id="ff361-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="ff361-151">一次 hello`condition`時的項目評估太`true`，沒有其他進一步`when`評估條件。</span><span class="sxs-lookup"><span data-stu-id="ff361-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="ff361-152">是</span><span class="sxs-lookup"><span data-stu-id="ff361-152">Yes</span></span>|  
|<span data-ttu-id="ff361-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="ff361-153">otherwise</span></span>|<span data-ttu-id="ff361-154">包含使用 如果沒有 hello hello 原則程式碼片段 toobe`when`條件的評估太`true`。</span><span class="sxs-lookup"><span data-stu-id="ff361-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="ff361-155">否</span><span class="sxs-lookup"><span data-stu-id="ff361-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-156">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-156">Attributes</span></span>  
  
|<span data-ttu-id="ff361-157">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-157">Attribute</span></span>|<span data-ttu-id="ff361-158">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-158">Description</span></span>|<span data-ttu-id="ff361-159">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="ff361-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="ff361-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="ff361-161">hello 布林運算式或常數 tooevaluated 當 hello 包含`when`會評估原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="ff361-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="ff361-162">是</span><span class="sxs-lookup"><span data-stu-id="ff361-162">Yes</span></span>|  
  
###  <span data-ttu-id="ff361-163"><a name="ChooseUsage"></a>使用方式</span><span class="sxs-lookup"><span data-stu-id="ff361-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="ff361-164">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-165">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-166">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ff361-167"><a name="ForwardRequest"></a>轉送要求</span><span class="sxs-lookup"><span data-stu-id="ff361-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="ff361-168">hello`forward-request`原則轉送 hello 連入要求 toohello 後端服務 hello 要求中指定[內容](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="ff361-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="ff361-169">hello 後端服務 URL 中指定 hello API[設定](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings)，而且可以使用 hello 變更[設定後端服務](api-management-transformation-policies.md)原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ff361-170">移除不會轉送 toohello 後端服務和 hello 原則 hello 輸出區段中的 hello 要求此原則會產生 hello hello 中的 hello 原則成功完成時立即評估輸入 > 一節。</span><span class="sxs-lookup"><span data-stu-id="ff361-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-171">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="ff361-172">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="ff361-173">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-173">Example</span></span>  
 <span data-ttu-id="ff361-174">hello 下列應用程式開發介面層級的原則會轉送所有要求 toohello 後端服務的逾時間隔為 60 秒。</span><span class="sxs-lookup"><span data-stu-id="ff361-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="ff361-175">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-175">Example</span></span>  
 <span data-ttu-id="ff361-176">這個作業層級原則使用 hello `base` hello 父應用程式開發介面層級範圍的項目 tooinherit hello 後端原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="ff361-177">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-177">Example</span></span>  
 <span data-ttu-id="ff361-178">此作業層級原則明確會轉送所有要求 toohello 後端服務逾時值為 120，而且沒有繼承 hello 父應用程式開發介面層級的後端原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="ff361-179">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-179">Example</span></span>  
 <span data-ttu-id="ff361-180">此作業層級原則不會轉送要求 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="ff361-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-181">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-181">Elements</span></span>  
  
|<span data-ttu-id="ff361-182">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-182">Element</span></span>|<span data-ttu-id="ff361-183">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-183">Description</span></span>|<span data-ttu-id="ff361-184">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="ff361-185">forward-request</span></span>|<span data-ttu-id="ff361-186">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-186">Root element.</span></span>|<span data-ttu-id="ff361-187">是</span><span class="sxs-lookup"><span data-stu-id="ff361-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-188">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-188">Attributes</span></span>  
  
|<span data-ttu-id="ff361-189">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-189">Attribute</span></span>|<span data-ttu-id="ff361-190">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-190">Description</span></span>|<span data-ttu-id="ff361-191">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-191">Required</span></span>|<span data-ttu-id="ff361-192">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ff361-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="ff361-193">timeout="integer"</span></span>|<span data-ttu-id="ff361-194">hello 逾時間隔，以秒為單位 hello 呼叫 toohello 後端服務之前就會失敗。</span><span class="sxs-lookup"><span data-stu-id="ff361-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="ff361-195">否</span><span class="sxs-lookup"><span data-stu-id="ff361-195">No</span></span>|<span data-ttu-id="ff361-196">無逾時</span><span class="sxs-lookup"><span data-stu-id="ff361-196">No timeout</span></span>|  
|<span data-ttu-id="ff361-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="ff361-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="ff361-198">指定從 hello 後端服務的重新導向是後面接著 hello 閘道或傳回 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="ff361-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="ff361-199">否</span><span class="sxs-lookup"><span data-stu-id="ff361-199">No</span></span>|<span data-ttu-id="ff361-200">false</span><span class="sxs-lookup"><span data-stu-id="ff361-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-201">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-201">Usage</span></span>  
 <span data-ttu-id="ff361-202">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-203">**原則區段︰**後端</span><span class="sxs-lookup"><span data-stu-id="ff361-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="ff361-204">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ff361-205"><a name="LimitConcurrency"></a> 限制並行</span><span class="sxs-lookup"><span data-stu-id="ff361-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="ff361-206">hello`limit-concurrency`原則防止括住的原則執行的多個 hello 指定的數目之要求在指定的時間。</span><span class="sxs-lookup"><span data-stu-id="ff361-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="ff361-207">當超出 hello 臨界值，新的要求都會加入 tooa 佇列，直到 hello 最大佇列長度為止。</span><span class="sxs-lookup"><span data-stu-id="ff361-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="ff361-208">在佇列耗盡時，新的要求會立即失敗。</span><span class="sxs-lookup"><span data-stu-id="ff361-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="ff361-209"><a name="LimitConcurrencyStatement"></a>原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="ff361-210">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-210">Examples</span></span>  
  
####  <span data-ttu-id="ff361-211"><a name="ChooseExample"></a>範例</span><span class="sxs-lookup"><span data-stu-id="ff361-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="ff361-212">hello 下列範例示範如何要求 toolimit 數目轉寄 tooa hello 的內容變數的值為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="ff361-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="ff361-213">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-213">Elements</span></span>  
  
|<span data-ttu-id="ff361-214">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-214">Element</span></span>|<span data-ttu-id="ff361-215">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-215">Description</span></span>|<span data-ttu-id="ff361-216">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="ff361-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="ff361-217">limit-concurrency</span></span>|<span data-ttu-id="ff361-218">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-218">Root element.</span></span>|<span data-ttu-id="ff361-219">是</span><span class="sxs-lookup"><span data-stu-id="ff361-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-220">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-220">Attributes</span></span>  
  
|<span data-ttu-id="ff361-221">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-221">Attribute</span></span>|<span data-ttu-id="ff361-222">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-222">Description</span></span>|<span data-ttu-id="ff361-223">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-223">Required</span></span>|<span data-ttu-id="ff361-224">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="ff361-225">key</span><span class="sxs-lookup"><span data-stu-id="ff361-225">key</span></span>|<span data-ttu-id="ff361-226">字串。</span><span class="sxs-lookup"><span data-stu-id="ff361-226">A string.</span></span> <span data-ttu-id="ff361-227">允許的運算式。</span><span class="sxs-lookup"><span data-stu-id="ff361-227">Expression allowed.</span></span> <span data-ttu-id="ff361-228">指定 hello 並行存取範圍。</span><span class="sxs-lookup"><span data-stu-id="ff361-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="ff361-229">可由多個原則共用。</span><span class="sxs-lookup"><span data-stu-id="ff361-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="ff361-230">是</span><span class="sxs-lookup"><span data-stu-id="ff361-230">Yes</span></span>|<span data-ttu-id="ff361-231">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-231">N/A</span></span>|  
|<span data-ttu-id="ff361-232">max-count</span><span class="sxs-lookup"><span data-stu-id="ff361-232">max-count</span></span>|<span data-ttu-id="ff361-233">整數。</span><span class="sxs-lookup"><span data-stu-id="ff361-233">An integer.</span></span> <span data-ttu-id="ff361-234">指定允許 tooenter hello 原則的要求的數目上限。</span><span class="sxs-lookup"><span data-stu-id="ff361-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="ff361-235">是</span><span class="sxs-lookup"><span data-stu-id="ff361-235">Yes</span></span>|<span data-ttu-id="ff361-236">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-236">N/A</span></span>|  
|<span data-ttu-id="ff361-237">timeout</span><span class="sxs-lookup"><span data-stu-id="ff361-237">timeout</span></span>|<span data-ttu-id="ff361-238">整數。</span><span class="sxs-lookup"><span data-stu-id="ff361-238">An integer.</span></span> <span data-ttu-id="ff361-239">允許的運算式。</span><span class="sxs-lookup"><span data-stu-id="ff361-239">Expression allowed.</span></span> <span data-ttu-id="ff361-240">指定的要求應該等候 tooenter 範圍而失敗之前的秒 hello 數 「 403 太多要求 」</span><span class="sxs-lookup"><span data-stu-id="ff361-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="ff361-241">否</span><span class="sxs-lookup"><span data-stu-id="ff361-241">No</span></span>|<span data-ttu-id="ff361-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="ff361-242">Infinity</span></span>|  
|<span data-ttu-id="ff361-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="ff361-243">max-queue-length</span></span>|<span data-ttu-id="ff361-244">整數。</span><span class="sxs-lookup"><span data-stu-id="ff361-244">An integer.</span></span> <span data-ttu-id="ff361-245">允許的運算式。</span><span class="sxs-lookup"><span data-stu-id="ff361-245">Expression allowed.</span></span> <span data-ttu-id="ff361-246">指定 hello 最大佇列長度。</span><span class="sxs-lookup"><span data-stu-id="ff361-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="ff361-247">嘗試 tooenter 的連入要求此原則將會終止並 「 403 太多要求 」 立即耗盡 hello 佇列時。</span><span class="sxs-lookup"><span data-stu-id="ff361-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="ff361-248">否</span><span class="sxs-lookup"><span data-stu-id="ff361-248">No</span></span>|<span data-ttu-id="ff361-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="ff361-249">Infinity</span></span>|  
  
###  <span data-ttu-id="ff361-250"><a name="ChooseUsage"></a>使用方式</span><span class="sxs-lookup"><span data-stu-id="ff361-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="ff361-251">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-252">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-253">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="ff361-254"><a name="log-to-eventhub"></a>記錄 tooEvent 中樞</span><span class="sxs-lookup"><span data-stu-id="ff361-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="ff361-255">hello`log-to-eventhub`原則會傳送 hello 訊息指定格式 tooan 記錄器實體所定義的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ff361-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="ff361-256">正如其名，hello 原則用來儲存所選的要求或回應的內容資訊線上或離線分析。</span><span class="sxs-lookup"><span data-stu-id="ff361-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ff361-257">如需設定事件中樞與記錄事件的逐步指南，請參閱[如何為 Azure 事件中心 toolog API 管理事件](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="ff361-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-258">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ff361-259">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-259">Example</span></span>  
 <span data-ttu-id="ff361-260">任何字串可以當做 hello 值 toobe 記錄在事件中心。</span><span class="sxs-lookup"><span data-stu-id="ff361-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="ff361-261">在此範例中 hello 日期和時間，部署服務名稱、 要求識別碼、 ip 位址和所有的傳入呼叫的作業名稱會以 hello 註冊的記錄器記錄的 toohello 事件中心`contoso-logger`識別碼。</span><span class="sxs-lookup"><span data-stu-id="ff361-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-262">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-262">Elements</span></span>  
  
|<span data-ttu-id="ff361-263">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-263">Element</span></span>|<span data-ttu-id="ff361-264">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-264">Description</span></span>|<span data-ttu-id="ff361-265">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="ff361-266">log-to-eventhub</span></span>|<span data-ttu-id="ff361-267">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-267">Root element.</span></span> <span data-ttu-id="ff361-268">這個項目 hello 值為 hello 字串 toolog tooyour 事件中心。</span><span class="sxs-lookup"><span data-stu-id="ff361-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="ff361-269">是</span><span class="sxs-lookup"><span data-stu-id="ff361-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-270">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-270">Attributes</span></span>  
  
|<span data-ttu-id="ff361-271">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-271">Attribute</span></span>|<span data-ttu-id="ff361-272">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-272">Description</span></span>|<span data-ttu-id="ff361-273">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="ff361-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="ff361-274">logger-id</span></span>|<span data-ttu-id="ff361-275">hello 識別碼 hello 記錄器註冊您的 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="ff361-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="ff361-276">是</span><span class="sxs-lookup"><span data-stu-id="ff361-276">Yes</span></span>|  
|<span data-ttu-id="ff361-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="ff361-277">partition-id</span></span>|<span data-ttu-id="ff361-278">指定 hello hello 訊息傳送的分割區索引。</span><span class="sxs-lookup"><span data-stu-id="ff361-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="ff361-279">選用。</span><span class="sxs-lookup"><span data-stu-id="ff361-279">Optional.</span></span> <span data-ttu-id="ff361-280">如果使用 `partition-key`，就不能使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="ff361-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="ff361-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="ff361-281">partition-key</span></span>|<span data-ttu-id="ff361-282">指定 hello 訊息傳送時用於資料分割指派的值。</span><span class="sxs-lookup"><span data-stu-id="ff361-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="ff361-283">選用。</span><span class="sxs-lookup"><span data-stu-id="ff361-283">Optional.</span></span> <span data-ttu-id="ff361-284">如果使用 `partition-id`，就不能使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="ff361-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-285">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-285">Usage</span></span>  
 <span data-ttu-id="ff361-286">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-287">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-288">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="ff361-289"><a name="mock-response"></a> Mock 回應</span><span class="sxs-lookup"><span data-stu-id="ff361-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="ff361-290">hello `mock-response`，做為 hello 名稱表示，是使用 toomock 應用程式開發介面和作業。</span><span class="sxs-lookup"><span data-stu-id="ff361-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="ff361-291">它會中止正常管線執行，並傳回模擬的回應 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="ff361-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="ff361-292">hello 原則一律會嘗試最高逼真度 tooreturn 的回應。</span><span class="sxs-lookup"><span data-stu-id="ff361-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="ff361-293">它偏好使用回應內容範例 (若可使用)。</span><span class="sxs-lookup"><span data-stu-id="ff361-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="ff361-294">當提供結構描述而無提供範例時，它會從結構描述產生範例回應。</span><span class="sxs-lookup"><span data-stu-id="ff361-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="ff361-295">如果沒有找到範例或結構描述，則會傳回沒有內容的回應。</span><span class="sxs-lookup"><span data-stu-id="ff361-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-296">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="ff361-297">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="ff361-298">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-298">Elements</span></span>  
  
|<span data-ttu-id="ff361-299">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-299">Element</span></span>|<span data-ttu-id="ff361-300">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-300">Description</span></span>|<span data-ttu-id="ff361-301">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="ff361-302">mock-response</span></span>|<span data-ttu-id="ff361-303">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-303">Root element.</span></span>|<span data-ttu-id="ff361-304">是</span><span class="sxs-lookup"><span data-stu-id="ff361-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-305">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-305">Attributes</span></span>  
  
|<span data-ttu-id="ff361-306">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-306">Attribute</span></span>|<span data-ttu-id="ff361-307">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-307">Description</span></span>|<span data-ttu-id="ff361-308">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-308">Required</span></span>|<span data-ttu-id="ff361-309">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="ff361-310">status-code</span><span class="sxs-lookup"><span data-stu-id="ff361-310">status-code</span></span>|<span data-ttu-id="ff361-311">指定回應狀態碼，並使用的 tooselect 對應的範例或結構描述。</span><span class="sxs-lookup"><span data-stu-id="ff361-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="ff361-312">否</span><span class="sxs-lookup"><span data-stu-id="ff361-312">No</span></span>|<span data-ttu-id="ff361-313">200</span><span class="sxs-lookup"><span data-stu-id="ff361-313">200</span></span>|  
|<span data-ttu-id="ff361-314">Content-Type</span><span class="sxs-lookup"><span data-stu-id="ff361-314">content-type</span></span>|<span data-ttu-id="ff361-315">指定`Content-Type`回應標頭值，而且是使用的 tooselect 對應的範例或結構描述。</span><span class="sxs-lookup"><span data-stu-id="ff361-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="ff361-316">否</span><span class="sxs-lookup"><span data-stu-id="ff361-316">No</span></span>|<span data-ttu-id="ff361-317">None</span><span class="sxs-lookup"><span data-stu-id="ff361-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-318">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-318">Usage</span></span>  
 <span data-ttu-id="ff361-319">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-320">**原則區段︰**輸入、輸出、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="ff361-321">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="ff361-322"><a name="Retry"></a>重試</span><span class="sxs-lookup"><span data-stu-id="ff361-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="ff361-323">hello`retry`原則執行它的子原則一次，然後重試 hello 重試之前執行`condition`變成`false`或重試`count`已用盡。</span><span class="sxs-lookup"><span data-stu-id="ff361-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-324">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="ff361-325">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-325">Example</span></span>  
 <span data-ttu-id="ff361-326">Hello 在下列範例要求 forewarding 會重試總 tooten 時間使用指數重試演算法。</span><span class="sxs-lookup"><span data-stu-id="ff361-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="ff361-327">因為`first-fast-retry`設定 toofalse，所有的重試次數是主體 toohello exponsntial 重試演算法。</span><span class="sxs-lookup"><span data-stu-id="ff361-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-328">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-328">Elements</span></span>  
  
|<span data-ttu-id="ff361-329">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-329">Element</span></span>|<span data-ttu-id="ff361-330">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-330">Description</span></span>|<span data-ttu-id="ff361-331">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-332">retry</span><span class="sxs-lookup"><span data-stu-id="ff361-332">retry</span></span>|<span data-ttu-id="ff361-333">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-333">Root element.</span></span> <span data-ttu-id="ff361-334">可包含其他任何原則來做為其子元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="ff361-335">是</span><span class="sxs-lookup"><span data-stu-id="ff361-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-336">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-336">Attributes</span></span>  
  
|<span data-ttu-id="ff361-337">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-337">Attribute</span></span>|<span data-ttu-id="ff361-338">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-338">Description</span></span>|<span data-ttu-id="ff361-339">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-339">Required</span></span>|<span data-ttu-id="ff361-340">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ff361-341">condition</span><span class="sxs-lookup"><span data-stu-id="ff361-341">condition</span></span>|<span data-ttu-id="ff361-342">布林常值或[運算式](api-management-policy-expressions.md)，指定應停止 (`false`) 還是繼續 (`true`) 重試。</span><span class="sxs-lookup"><span data-stu-id="ff361-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="ff361-343">是</span><span class="sxs-lookup"><span data-stu-id="ff361-343">Yes</span></span>|<span data-ttu-id="ff361-344">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-344">N/A</span></span>|  
|<span data-ttu-id="ff361-345">計數</span><span class="sxs-lookup"><span data-stu-id="ff361-345">count</span></span>|<span data-ttu-id="ff361-346">指定的重試 tooattempt hello 最大數目的正數。</span><span class="sxs-lookup"><span data-stu-id="ff361-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="ff361-347">是</span><span class="sxs-lookup"><span data-stu-id="ff361-347">Yes</span></span>|<span data-ttu-id="ff361-348">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-348">N/A</span></span>|  
|<span data-ttu-id="ff361-349">interval</span><span class="sxs-lookup"><span data-stu-id="ff361-349">interval</span></span>|<span data-ttu-id="ff361-350">以秒為單位指定 hello hello 重試嘗試之間的等待間隔正數。</span><span class="sxs-lookup"><span data-stu-id="ff361-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="ff361-351">是</span><span class="sxs-lookup"><span data-stu-id="ff361-351">Yes</span></span>|<span data-ttu-id="ff361-352">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-352">N/A</span></span>|  
|<span data-ttu-id="ff361-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="ff361-353">max-interval</span></span>|<span data-ttu-id="ff361-354">以秒為單位指定 hello hello 重試嘗試之間的最長等待間隔正數。</span><span class="sxs-lookup"><span data-stu-id="ff361-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="ff361-355">它是使用的 tooimplement 指數重試演算法。</span><span class="sxs-lookup"><span data-stu-id="ff361-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="ff361-356">否</span><span class="sxs-lookup"><span data-stu-id="ff361-356">No</span></span>|<span data-ttu-id="ff361-357">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-357">N/A</span></span>|  
|<span data-ttu-id="ff361-358">delta</span><span class="sxs-lookup"><span data-stu-id="ff361-358">delta</span></span>|<span data-ttu-id="ff361-359">以秒為單位指定 hello 等待間隔遞增正數。</span><span class="sxs-lookup"><span data-stu-id="ff361-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="ff361-360">它是使用的 tooimplement hello 線性和指數重試演算法。</span><span class="sxs-lookup"><span data-stu-id="ff361-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="ff361-361">否</span><span class="sxs-lookup"><span data-stu-id="ff361-361">No</span></span>|<span data-ttu-id="ff361-362">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-362">N/A</span></span>|  
|<span data-ttu-id="ff361-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="ff361-363">first-fast-retry</span></span>|<span data-ttu-id="ff361-364">如果設定太`true`，hello 第一次重試嘗試會立即執行。</span><span class="sxs-lookup"><span data-stu-id="ff361-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="ff361-365">否</span><span class="sxs-lookup"><span data-stu-id="ff361-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="ff361-366">當只有 hello`interval`指定，則**固定**間隔重試執行。</span><span class="sxs-lookup"><span data-stu-id="ff361-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="ff361-367">當只有 hello`interval`和`delta`都有指定，**線性**使用間隔重試演算法，其中的重試之間的等待時間是導出的相應 hello 下列公式- `interval + (count - 1)*delta`。</span><span class="sxs-lookup"><span data-stu-id="ff361-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="ff361-368">當 hello `interval`，`max-interval`和`delta`都有指定，**指數**間隔重試演算法會套用 hello hello 重試之間的等待時間出現指數型成長hello值`interval`toohello 值`max-interval`根據 toohello 下列 forumula- `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`。</span><span class="sxs-lookup"><span data-stu-id="ff361-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="ff361-369">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-369">Usage</span></span>  
 <span data-ttu-id="ff361-370">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="ff361-371">請注意，此原則會繼承子原則的使用方式限制。</span><span class="sxs-lookup"><span data-stu-id="ff361-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="ff361-372">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-373">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ff361-374"><a name="ReturnResponse"></a>傳回回應</span><span class="sxs-lookup"><span data-stu-id="ff361-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="ff361-375">hello`return-response`中止管線執行原則，並傳回預設或自訂回應 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="ff361-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="ff361-376">預設回應是 `200 OK`，且沒有本文。</span><span class="sxs-lookup"><span data-stu-id="ff361-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="ff361-377">透過內容變數或原則陳述式即可指定自訂回應。</span><span class="sxs-lookup"><span data-stu-id="ff361-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="ff361-378">當同時提供時，hello 回應 hello 內容變數中包含以 hello 原則陳述式前會先修改傳回 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="ff361-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-379">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ff361-380">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ff361-381">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-381">Elements</span></span>  
  
|<span data-ttu-id="ff361-382">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-382">Element</span></span>|<span data-ttu-id="ff361-383">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-383">Description</span></span>|<span data-ttu-id="ff361-384">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-385">return-response</span><span class="sxs-lookup"><span data-stu-id="ff361-385">return-response</span></span>|<span data-ttu-id="ff361-386">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-386">Root element.</span></span>|<span data-ttu-id="ff361-387">是</span><span class="sxs-lookup"><span data-stu-id="ff361-387">Yes</span></span>|  
|<span data-ttu-id="ff361-388">set-header</span><span class="sxs-lookup"><span data-stu-id="ff361-388">set-header</span></span>|<span data-ttu-id="ff361-389">[set-header](api-management-transformation-policies.md#SetHTTPheader) 原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="ff361-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="ff361-390">否</span><span class="sxs-lookup"><span data-stu-id="ff361-390">No</span></span>|  
|<span data-ttu-id="ff361-391">set-body</span><span class="sxs-lookup"><span data-stu-id="ff361-391">set-body</span></span>|<span data-ttu-id="ff361-392">[set-body](api-management-transformation-policies.md#SetBody) 原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="ff361-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="ff361-393">否</span><span class="sxs-lookup"><span data-stu-id="ff361-393">No</span></span>|  
|<span data-ttu-id="ff361-394">set-status</span><span class="sxs-lookup"><span data-stu-id="ff361-394">set-status</span></span>|<span data-ttu-id="ff361-395">[set-status](api-management-advanced-policies.md#SetStatus) 原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="ff361-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="ff361-396">否</span><span class="sxs-lookup"><span data-stu-id="ff361-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-397">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-397">Attributes</span></span>  
  
|<span data-ttu-id="ff361-398">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-398">Attribute</span></span>|<span data-ttu-id="ff361-399">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-399">Description</span></span>|<span data-ttu-id="ff361-400">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="ff361-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="ff361-401">response-variable-name</span></span>|<span data-ttu-id="ff361-402">hello hello 內容變數的參考名稱，例如，上游[傳送要求](api-management-advanced-policies.md#SendRequest)原則，並包含`Response`物件</span><span class="sxs-lookup"><span data-stu-id="ff361-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="ff361-403">選用。</span><span class="sxs-lookup"><span data-stu-id="ff361-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-404">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-404">Usage</span></span>  
 <span data-ttu-id="ff361-405">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-406">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-407">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ff361-408"><a name="SendOneWayRequest"></a>傳送單向要求</span><span class="sxs-lookup"><span data-stu-id="ff361-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="ff361-409">hello`send-one-way-request`原則傳送嗨提供要求 toohello 指定 URL，而不必等候回應。</span><span class="sxs-lookup"><span data-stu-id="ff361-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-410">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ff361-411">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-411">Example</span></span>  
 <span data-ttu-id="ff361-412">此原則的範例示範使用 hello`send-one-way-request`原則 toosend 訊息 tooa Slack 聊天室如果 hello HTTP 回應碼大於或等於 too500。</span><span class="sxs-lookup"><span data-stu-id="ff361-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="ff361-413">如需有關此範例的詳細資訊，請參閱[使用來自 hello Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。</span><span class="sxs-lookup"><span data-stu-id="ff361-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-414">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-414">Elements</span></span>  
  
|<span data-ttu-id="ff361-415">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-415">Element</span></span>|<span data-ttu-id="ff361-416">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-416">Description</span></span>|<span data-ttu-id="ff361-417">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="ff361-418">send-one-way-request</span></span>|<span data-ttu-id="ff361-419">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-419">Root element.</span></span>|<span data-ttu-id="ff361-420">是</span><span class="sxs-lookup"><span data-stu-id="ff361-420">Yes</span></span>|  
|<span data-ttu-id="ff361-421">url</span><span class="sxs-lookup"><span data-stu-id="ff361-421">url</span></span>|<span data-ttu-id="ff361-422">hello hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="ff361-422">hello URL of hello request.</span></span>|<span data-ttu-id="ff361-423">mode=copy 時為 [否]；否則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="ff361-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="ff361-424">method</span><span class="sxs-lookup"><span data-stu-id="ff361-424">method</span></span>|<span data-ttu-id="ff361-425">hello hello 要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="ff361-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="ff361-426">mode=copy 時為 [否]；否則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="ff361-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="ff361-427">頁首</span><span class="sxs-lookup"><span data-stu-id="ff361-427">header</span></span>|<span data-ttu-id="ff361-428">要求標頭。</span><span class="sxs-lookup"><span data-stu-id="ff361-428">Request header.</span></span> <span data-ttu-id="ff361-429">若有多個要求標頭，請使用多個 header 元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="ff361-430">否</span><span class="sxs-lookup"><span data-stu-id="ff361-430">No</span></span>|  
|<span data-ttu-id="ff361-431">body</span><span class="sxs-lookup"><span data-stu-id="ff361-431">body</span></span>|<span data-ttu-id="ff361-432">hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="ff361-432">hello request body.</span></span>|<span data-ttu-id="ff361-433">否</span><span class="sxs-lookup"><span data-stu-id="ff361-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-434">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-434">Attributes</span></span>  
  
|<span data-ttu-id="ff361-435">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-435">Attribute</span></span>|<span data-ttu-id="ff361-436">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-436">Description</span></span>|<span data-ttu-id="ff361-437">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-437">Required</span></span>|<span data-ttu-id="ff361-438">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ff361-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="ff361-439">mode="string"</span></span>|<span data-ttu-id="ff361-440">判斷這是否為新的要求或是 hello 目前要求的複本。</span><span class="sxs-lookup"><span data-stu-id="ff361-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="ff361-441">在輸出模式中，模式 = 複本不會初始化 hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="ff361-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="ff361-442">否</span><span class="sxs-lookup"><span data-stu-id="ff361-442">No</span></span>|<span data-ttu-id="ff361-443">新增</span><span class="sxs-lookup"><span data-stu-id="ff361-443">New</span></span>|  
|<span data-ttu-id="ff361-444">名稱</span><span class="sxs-lookup"><span data-stu-id="ff361-444">name</span></span>|<span data-ttu-id="ff361-445">指定 hello hello 標頭 toobe 集名稱。</span><span class="sxs-lookup"><span data-stu-id="ff361-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="ff361-446">是</span><span class="sxs-lookup"><span data-stu-id="ff361-446">Yes</span></span>|<span data-ttu-id="ff361-447">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-447">N/A</span></span>|  
|<span data-ttu-id="ff361-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="ff361-448">exists-action</span></span>|<span data-ttu-id="ff361-449">Hello 標頭已指定時，請指定何種動作 tootake。</span><span class="sxs-lookup"><span data-stu-id="ff361-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="ff361-450">此屬性必須有 hello 下列值之一。</span><span class="sxs-lookup"><span data-stu-id="ff361-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="ff361-451">-覆寫-取代 hello hello 現有的標頭值。</span><span class="sxs-lookup"><span data-stu-id="ff361-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="ff361-452">-skip-不會取代 hello 現有標頭值。</span><span class="sxs-lookup"><span data-stu-id="ff361-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="ff361-453">-附加-附加 hello 值 toohello 現有標頭值。</span><span class="sxs-lookup"><span data-stu-id="ff361-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="ff361-454">-delete-從 hello 要求移除 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="ff361-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="ff361-455">當設定太`override`編列多個項目以 hello 相同的名稱，正在設定相應 tooall 項目 （列出多次） hello 標頭中的結果; 只有列出的值會設定在 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ff361-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="ff361-456">否</span><span class="sxs-lookup"><span data-stu-id="ff361-456">No</span></span>|<span data-ttu-id="ff361-457">override</span><span class="sxs-lookup"><span data-stu-id="ff361-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-458">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-458">Usage</span></span>  
 <span data-ttu-id="ff361-459">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-460">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-461">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ff361-462"><a name="SendRequest"></a>傳送要求</span><span class="sxs-lookup"><span data-stu-id="ff361-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="ff361-463">hello`send-request`原則傳送 hello 提供要求 toohello 指定 URL，不會再等候非 hello 設定逾時值。</span><span class="sxs-lookup"><span data-stu-id="ff361-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-464">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ff361-465">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-465">Example</span></span>  
 <span data-ttu-id="ff361-466">這個範例會示範其中一種方式 tooverify 參考權杖，向授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff361-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="ff361-467">如需有關此範例的詳細資訊，請參閱[使用來自 hello Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。</span><span class="sxs-lookup"><span data-stu-id="ff361-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-468">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-468">Elements</span></span>  
  
|<span data-ttu-id="ff361-469">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-469">Element</span></span>|<span data-ttu-id="ff361-470">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-470">Description</span></span>|<span data-ttu-id="ff361-471">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-472">send-request</span><span class="sxs-lookup"><span data-stu-id="ff361-472">send-request</span></span>|<span data-ttu-id="ff361-473">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-473">Root element.</span></span>|<span data-ttu-id="ff361-474">是</span><span class="sxs-lookup"><span data-stu-id="ff361-474">Yes</span></span>|  
|<span data-ttu-id="ff361-475">url</span><span class="sxs-lookup"><span data-stu-id="ff361-475">url</span></span>|<span data-ttu-id="ff361-476">hello hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="ff361-476">hello URL of hello request.</span></span>|<span data-ttu-id="ff361-477">mode=copy 時為 [否]；否則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="ff361-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="ff361-478">method</span><span class="sxs-lookup"><span data-stu-id="ff361-478">method</span></span>|<span data-ttu-id="ff361-479">hello hello 要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="ff361-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="ff361-480">mode=copy 時為 [否]；否則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="ff361-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="ff361-481">頁首</span><span class="sxs-lookup"><span data-stu-id="ff361-481">header</span></span>|<span data-ttu-id="ff361-482">要求標頭。</span><span class="sxs-lookup"><span data-stu-id="ff361-482">Request header.</span></span> <span data-ttu-id="ff361-483">若有多個要求標頭，請使用多個 header 元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="ff361-484">否</span><span class="sxs-lookup"><span data-stu-id="ff361-484">No</span></span>|  
|<span data-ttu-id="ff361-485">body</span><span class="sxs-lookup"><span data-stu-id="ff361-485">body</span></span>|<span data-ttu-id="ff361-486">hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="ff361-486">hello request body.</span></span>|<span data-ttu-id="ff361-487">否</span><span class="sxs-lookup"><span data-stu-id="ff361-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-488">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-488">Attributes</span></span>  
  
|<span data-ttu-id="ff361-489">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-489">Attribute</span></span>|<span data-ttu-id="ff361-490">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-490">Description</span></span>|<span data-ttu-id="ff361-491">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-491">Required</span></span>|<span data-ttu-id="ff361-492">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ff361-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="ff361-493">mode="string"</span></span>|<span data-ttu-id="ff361-494">判斷這是否為新的要求或是 hello 目前要求的複本。</span><span class="sxs-lookup"><span data-stu-id="ff361-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="ff361-495">在輸出模式中，模式 = 複本不會初始化 hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="ff361-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="ff361-496">否</span><span class="sxs-lookup"><span data-stu-id="ff361-496">No</span></span>|<span data-ttu-id="ff361-497">新增</span><span class="sxs-lookup"><span data-stu-id="ff361-497">New</span></span>|  
|<span data-ttu-id="ff361-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="ff361-498">response-variable-name="string"</span></span>|<span data-ttu-id="ff361-499">如果不存在，則會使用 `context.Response`。</span><span class="sxs-lookup"><span data-stu-id="ff361-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="ff361-500">否</span><span class="sxs-lookup"><span data-stu-id="ff361-500">No</span></span>|<span data-ttu-id="ff361-501">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-501">N/A</span></span>|  
|<span data-ttu-id="ff361-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="ff361-502">timeout="integer"</span></span>|<span data-ttu-id="ff361-503">hello 逾時間隔，以秒為單位 hello 呼叫之前 toohello URL 將會失敗。</span><span class="sxs-lookup"><span data-stu-id="ff361-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="ff361-504">否</span><span class="sxs-lookup"><span data-stu-id="ff361-504">No</span></span>|<span data-ttu-id="ff361-505">60</span><span class="sxs-lookup"><span data-stu-id="ff361-505">60</span></span>|  
|<span data-ttu-id="ff361-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="ff361-506">ignore-error</span></span>|<span data-ttu-id="ff361-507">如果為 true，而且 hello 要求會導致錯誤：</span><span class="sxs-lookup"><span data-stu-id="ff361-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="ff361-508">-   如果已指定 response-variable-name，它會包含 null 值。</span><span class="sxs-lookup"><span data-stu-id="ff361-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="ff361-509">-   如果未指定 response-variable-name，則不會更新 context.Request。</span><span class="sxs-lookup"><span data-stu-id="ff361-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="ff361-510">否</span><span class="sxs-lookup"><span data-stu-id="ff361-510">No</span></span>|<span data-ttu-id="ff361-511">false</span><span class="sxs-lookup"><span data-stu-id="ff361-511">false</span></span>|  
|<span data-ttu-id="ff361-512">名稱</span><span class="sxs-lookup"><span data-stu-id="ff361-512">name</span></span>|<span data-ttu-id="ff361-513">指定 hello hello 標頭 toobe 集名稱。</span><span class="sxs-lookup"><span data-stu-id="ff361-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="ff361-514">是</span><span class="sxs-lookup"><span data-stu-id="ff361-514">Yes</span></span>|<span data-ttu-id="ff361-515">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-515">N/A</span></span>|  
|<span data-ttu-id="ff361-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="ff361-516">exists-action</span></span>|<span data-ttu-id="ff361-517">Hello 標頭已指定時，請指定何種動作 tootake。</span><span class="sxs-lookup"><span data-stu-id="ff361-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="ff361-518">此屬性必須有 hello 下列值之一。</span><span class="sxs-lookup"><span data-stu-id="ff361-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="ff361-519">-覆寫-取代 hello hello 現有的標頭值。</span><span class="sxs-lookup"><span data-stu-id="ff361-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="ff361-520">-skip-不會取代 hello 現有標頭值。</span><span class="sxs-lookup"><span data-stu-id="ff361-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="ff361-521">-附加-附加 hello 值 toohello 現有標頭值。</span><span class="sxs-lookup"><span data-stu-id="ff361-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="ff361-522">-delete-從 hello 要求移除 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="ff361-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="ff361-523">當設定太`override`編列多個項目以 hello 相同的名稱，正在設定相應 tooall 項目 （列出多次） hello 標頭中的結果; 只有列出的值會設定在 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ff361-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="ff361-524">否</span><span class="sxs-lookup"><span data-stu-id="ff361-524">No</span></span>|<span data-ttu-id="ff361-525">override</span><span class="sxs-lookup"><span data-stu-id="ff361-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-526">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-526">Usage</span></span>  
 <span data-ttu-id="ff361-527">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-528">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-529">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ff361-530"><a name="SetHttpProxy"></a> 設定 HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="ff361-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="ff361-531">hello`proxy`原則可讓您將要求轉送 toobackends tooroute 透過 HTTP proxy。</span><span class="sxs-lookup"><span data-stu-id="ff361-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="ff361-532">HTTP (不是 HTTPS) 支援 hello 閘道與 hello proxy 之間。</span><span class="sxs-lookup"><span data-stu-id="ff361-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="ff361-533">僅限基本和 NTLM 驗證。</span><span class="sxs-lookup"><span data-stu-id="ff361-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-534">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="ff361-535">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-535">Example</span></span>  
<span data-ttu-id="ff361-536">請注意 hello 使用[屬性](api-management-howto-properties.md)為 hello 使用者名稱和密碼 tooavoid hello 原則文件中儲存機密資訊的值。</span><span class="sxs-lookup"><span data-stu-id="ff361-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="ff361-537">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-537">Elements</span></span>  
  
|<span data-ttu-id="ff361-538">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-538">Element</span></span>|<span data-ttu-id="ff361-539">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-539">Description</span></span>|<span data-ttu-id="ff361-540">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-541">proxy</span><span class="sxs-lookup"><span data-stu-id="ff361-541">proxy</span></span>|<span data-ttu-id="ff361-542">根元素</span><span class="sxs-lookup"><span data-stu-id="ff361-542">Root element</span></span>|<span data-ttu-id="ff361-543">是</span><span class="sxs-lookup"><span data-stu-id="ff361-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="ff361-544">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-544">Attributes</span></span>  
  
|<span data-ttu-id="ff361-545">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-545">Attribute</span></span>|<span data-ttu-id="ff361-546">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-546">Description</span></span>|<span data-ttu-id="ff361-547">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-547">Required</span></span>|<span data-ttu-id="ff361-548">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ff361-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="ff361-549">url="string"</span></span>|<span data-ttu-id="ff361-550">Http://host:port hello 形式的 proxy URL。</span><span class="sxs-lookup"><span data-stu-id="ff361-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="ff361-551">是</span><span class="sxs-lookup"><span data-stu-id="ff361-551">Yes</span></span>|<span data-ttu-id="ff361-552">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-552">N/A</span></span>|  
|<span data-ttu-id="ff361-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="ff361-553">username="string"</span></span>|<span data-ttu-id="ff361-554">用來與 hello proxy 進行驗證的使用者名稱 toobe。</span><span class="sxs-lookup"><span data-stu-id="ff361-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="ff361-555">否</span><span class="sxs-lookup"><span data-stu-id="ff361-555">No</span></span>|<span data-ttu-id="ff361-556">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-556">N/A</span></span>|  
|<span data-ttu-id="ff361-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="ff361-557">password="string"</span></span>|<span data-ttu-id="ff361-558">密碼 toobe 用於 hello proxy 驗證。</span><span class="sxs-lookup"><span data-stu-id="ff361-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="ff361-559">否</span><span class="sxs-lookup"><span data-stu-id="ff361-559">No</span></span>|<span data-ttu-id="ff361-560">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="ff361-561">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-561">Usage</span></span>  
 <span data-ttu-id="ff361-562">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-563">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="ff361-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ff361-564">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="ff361-565"><a name="SetRequestMethod"></a>設定要求方法</span><span class="sxs-lookup"><span data-stu-id="ff361-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="ff361-566">hello`set-method`原則可讓您要求 toochange hello HTTP 要求方法。</span><span class="sxs-lookup"><span data-stu-id="ff361-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-567">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ff361-568">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-568">Example</span></span>  
 <span data-ttu-id="ff361-569">此範例原則使用 hello`set-method`原則會顯示傳送訊息 tooa Slack 聊天室的案例，如果 hello HTTP 回應碼大於或等於 too500 的範例。</span><span class="sxs-lookup"><span data-stu-id="ff361-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="ff361-570">如需有關此範例的詳細資訊，請參閱[使用來自 hello Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。</span><span class="sxs-lookup"><span data-stu-id="ff361-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-571">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-571">Elements</span></span>  
  
|<span data-ttu-id="ff361-572">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-572">Element</span></span>|<span data-ttu-id="ff361-573">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-573">Description</span></span>|<span data-ttu-id="ff361-574">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-575">set-method</span><span class="sxs-lookup"><span data-stu-id="ff361-575">set-method</span></span>|<span data-ttu-id="ff361-576">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-576">Root element.</span></span> <span data-ttu-id="ff361-577">hello hello 項目的值指定 hello HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="ff361-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="ff361-578">是</span><span class="sxs-lookup"><span data-stu-id="ff361-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-579">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-579">Usage</span></span>  
 <span data-ttu-id="ff361-580">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-581">**原則區段︰**輸入、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="ff361-582">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ff361-583"><a name="SetStatus"></a>設定狀態碼</span><span class="sxs-lookup"><span data-stu-id="ff361-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="ff361-584">hello`set-status`原則集 hello HTTP 狀態碼 toohello 指定的值。</span><span class="sxs-lookup"><span data-stu-id="ff361-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-585">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ff361-586">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-586">Example</span></span>  
 <span data-ttu-id="ff361-587">這個範例會示範如何 tooreturn 401 回應 hello 授權權杖是否無效。</span><span class="sxs-lookup"><span data-stu-id="ff361-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="ff361-588">如需詳細資訊，請參閱[使用來自 hello Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="ff361-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-589">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-589">Elements</span></span>  
  
|<span data-ttu-id="ff361-590">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-590">Element</span></span>|<span data-ttu-id="ff361-591">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-591">Description</span></span>|<span data-ttu-id="ff361-592">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-593">set-status</span><span class="sxs-lookup"><span data-stu-id="ff361-593">set-status</span></span>|<span data-ttu-id="ff361-594">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-594">Root element.</span></span>|<span data-ttu-id="ff361-595">是</span><span class="sxs-lookup"><span data-stu-id="ff361-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-596">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-596">Attributes</span></span>  
  
|<span data-ttu-id="ff361-597">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-597">Attribute</span></span>|<span data-ttu-id="ff361-598">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-598">Description</span></span>|<span data-ttu-id="ff361-599">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-599">Required</span></span>|<span data-ttu-id="ff361-600">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ff361-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="ff361-601">code="integer"</span></span>|<span data-ttu-id="ff361-602">hello HTTP 狀態碼 tooreturn。</span><span class="sxs-lookup"><span data-stu-id="ff361-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="ff361-603">是</span><span class="sxs-lookup"><span data-stu-id="ff361-603">Yes</span></span>|<span data-ttu-id="ff361-604">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-604">N/A</span></span>|  
|<span data-ttu-id="ff361-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="ff361-605">reason="string"</span></span>|<span data-ttu-id="ff361-606">傳回狀態碼為 hello hello 原因的描述。</span><span class="sxs-lookup"><span data-stu-id="ff361-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="ff361-607">是</span><span class="sxs-lookup"><span data-stu-id="ff361-607">Yes</span></span>|<span data-ttu-id="ff361-608">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-609">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-609">Usage</span></span>  
 <span data-ttu-id="ff361-610">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-611">**原則區段︰**輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-612">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="ff361-613"><a name="set-variable"></a>設定變數</span><span class="sxs-lookup"><span data-stu-id="ff361-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="ff361-614">hello`set-variable`原則宣告[內容](api-management-policy-expressions.md#ContextVariables)變數並將其指派值，指定透過[運算式](api-management-policy-expressions.md)或字串常值。</span><span class="sxs-lookup"><span data-stu-id="ff361-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="ff361-615">如果 hello 運算式包含常值會轉換 tooa 字串和 hello hello 值類型會是`System.String`。</span><span class="sxs-lookup"><span data-stu-id="ff361-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="ff361-616"><a name="set-variablePolicyStatement"></a>原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="ff361-617"><a name="set-variableExample"></a>範例</span><span class="sxs-lookup"><span data-stu-id="ff361-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="ff361-618">hello 下列範例會示範設定變數原則在 hello 輸入 > 一節。</span><span class="sxs-lookup"><span data-stu-id="ff361-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="ff361-619">此設定變數原則建立`isMobile`布林[內容](api-management-policy-expressions.md#ContextVariables)變數時 hello 設定 tootrue`User-Agent`要求標頭包含的 hello 文字`iPad`或`iPhone`。</span><span class="sxs-lookup"><span data-stu-id="ff361-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="ff361-620">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-620">Elements</span></span>  
  
|<span data-ttu-id="ff361-621">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-621">Element</span></span>|<span data-ttu-id="ff361-622">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-622">Description</span></span>|<span data-ttu-id="ff361-623">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="ff361-624">set-variable</span></span>|<span data-ttu-id="ff361-625">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-625">Root element.</span></span>|<span data-ttu-id="ff361-626">是</span><span class="sxs-lookup"><span data-stu-id="ff361-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-627">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-627">Attributes</span></span>  
  
|<span data-ttu-id="ff361-628">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-628">Attribute</span></span>|<span data-ttu-id="ff361-629">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-629">Description</span></span>|<span data-ttu-id="ff361-630">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="ff361-631">名稱</span><span class="sxs-lookup"><span data-stu-id="ff361-631">name</span></span>|<span data-ttu-id="ff361-632">hello hello 變數名稱。</span><span class="sxs-lookup"><span data-stu-id="ff361-632">hello name of hello variable.</span></span>|<span data-ttu-id="ff361-633">是</span><span class="sxs-lookup"><span data-stu-id="ff361-633">Yes</span></span>|  
|<span data-ttu-id="ff361-634">value</span><span class="sxs-lookup"><span data-stu-id="ff361-634">value</span></span>|<span data-ttu-id="ff361-635">hello hello 變數值。</span><span class="sxs-lookup"><span data-stu-id="ff361-635">hello value of hello variable.</span></span> <span data-ttu-id="ff361-636">此值可為運算式或常值。</span><span class="sxs-lookup"><span data-stu-id="ff361-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="ff361-637">是</span><span class="sxs-lookup"><span data-stu-id="ff361-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-638">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-638">Usage</span></span>  
 <span data-ttu-id="ff361-639">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-640">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-641">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="ff361-642"><a name="set-variableAllowedTypes"></a>允許的類型</span><span class="sxs-lookup"><span data-stu-id="ff361-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="ff361-643">Hello 中使用的運算式`set-variable`原則必須傳回 hello 下列基本類型的其中一個。</span><span class="sxs-lookup"><span data-stu-id="ff361-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="ff361-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="ff361-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="ff361-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="ff361-645">System.SByte</span></span>  
  
-   <span data-ttu-id="ff361-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="ff361-646">System.Byte</span></span>  
  
-   <span data-ttu-id="ff361-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="ff361-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="ff361-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="ff361-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="ff361-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="ff361-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="ff361-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="ff361-650">System.Int16</span></span>  
  
-   <span data-ttu-id="ff361-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="ff361-651">System.Int32</span></span>  
  
-   <span data-ttu-id="ff361-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="ff361-652">System.Int64</span></span>  
  
-   <span data-ttu-id="ff361-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="ff361-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="ff361-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="ff361-654">System.Single</span></span>  
  
-   <span data-ttu-id="ff361-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="ff361-655">System.Double</span></span>  
  
-   <span data-ttu-id="ff361-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="ff361-656">System.Guid</span></span>  
  
-   <span data-ttu-id="ff361-657">System.String</span><span class="sxs-lookup"><span data-stu-id="ff361-657">System.String</span></span>  
  
-   <span data-ttu-id="ff361-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="ff361-658">System.Char</span></span>  
  
-   <span data-ttu-id="ff361-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="ff361-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="ff361-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ff361-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="ff361-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="ff361-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="ff361-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="ff361-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="ff361-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="ff361-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="ff361-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="ff361-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="ff361-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="ff361-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="ff361-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="ff361-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="ff361-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="ff361-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="ff361-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="ff361-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="ff361-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="ff361-669">System.Single?</span></span>  
  
-   <span data-ttu-id="ff361-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="ff361-670">System.Double?</span></span>  
  
-   <span data-ttu-id="ff361-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="ff361-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="ff361-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="ff361-672">System.String?</span></span>  
  
-   <span data-ttu-id="ff361-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="ff361-673">System.Char?</span></span>  
  
-   <span data-ttu-id="ff361-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="ff361-674">System.DateTime?</span></span>  

##  <span data-ttu-id="ff361-675"><a name="Trace"></a>追蹤</span><span class="sxs-lookup"><span data-stu-id="ff361-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="ff361-676">hello`trace`原則會將字串新增到 hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。</span><span class="sxs-lookup"><span data-stu-id="ff361-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="ff361-677">hello 原則將會執行只追蹤會觸發時，也就是`Ocp-Apim-Trace`要求標頭是否存在並設定太`true`和`Ocp-Apim-Subscription-Key`要求標頭存在，並保留 hello 系統管理員帳戶相關聯的有效索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ff361-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-678">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ff361-679">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-679">Elements</span></span>  
  
|<span data-ttu-id="ff361-680">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-680">Element</span></span>|<span data-ttu-id="ff361-681">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-681">Description</span></span>|<span data-ttu-id="ff361-682">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-683">trace</span><span class="sxs-lookup"><span data-stu-id="ff361-683">trace</span></span>|<span data-ttu-id="ff361-684">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-684">Root element.</span></span>|<span data-ttu-id="ff361-685">是</span><span class="sxs-lookup"><span data-stu-id="ff361-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-686">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-686">Attributes</span></span>  
  
|<span data-ttu-id="ff361-687">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-687">Attribute</span></span>|<span data-ttu-id="ff361-688">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-688">Description</span></span>|<span data-ttu-id="ff361-689">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-689">Required</span></span>|<span data-ttu-id="ff361-690">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ff361-691">來源</span><span class="sxs-lookup"><span data-stu-id="ff361-691">source</span></span>|<span data-ttu-id="ff361-692">字串常值有意義的 toohello 追蹤檢視器與指定的 hello 來源的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="ff361-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="ff361-693">是</span><span class="sxs-lookup"><span data-stu-id="ff361-693">Yes</span></span>|<span data-ttu-id="ff361-694">N/A</span><span class="sxs-lookup"><span data-stu-id="ff361-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-695">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-695">Usage</span></span>  
 <span data-ttu-id="ff361-696">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="ff361-697">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="ff361-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ff361-698">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ff361-699"><a name="Wait"></a>等候</span><span class="sxs-lookup"><span data-stu-id="ff361-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="ff361-700">hello`wait`原則以平行方式，執行其直屬子原則，並完成之前，等待所有或其中一個其直屬子原則 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="ff361-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="ff361-701">hello 等候原則可以有為其直屬子原則[傳送要求](api-management-advanced-policies.md#SendRequest)，[取得值，從快取](api-management-caching-policies.md#GetFromCacheByKey)，和[控制流程](api-management-advanced-policies.md#choose)原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ff361-702">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="ff361-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ff361-703">範例</span><span class="sxs-lookup"><span data-stu-id="ff361-703">Example</span></span>  
 <span data-ttu-id="ff361-704">下列範例中的 hello 中有兩個`choose`直屬子原則的 hello 原則`wait`原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="ff361-705">在這些 `choose` 原則中，每一個都會以平行方式執行。</span><span class="sxs-lookup"><span data-stu-id="ff361-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="ff361-706">每個`choose`原則嘗試 tooretrieve 快取的值。</span><span class="sxs-lookup"><span data-stu-id="ff361-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="ff361-707">如果沒有快取遺漏後, 端服務稱為 tooprovide hello 值。</span><span class="sxs-lookup"><span data-stu-id="ff361-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="ff361-708">在此範例 hello`wait`原則才會完成所有其直屬子原則完成，因為 hello`for`屬性設定太`all`。</span><span class="sxs-lookup"><span data-stu-id="ff361-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="ff361-709">在此範例 hello 內容變數 (`execute-branch-one`， `value-one`， `execute-branch-two`，和`value-two`) 宣告此範例原則 hello 範圍之外。</span><span class="sxs-lookup"><span data-stu-id="ff361-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="ff361-710">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-710">Elements</span></span>  
  
|<span data-ttu-id="ff361-711">元素</span><span class="sxs-lookup"><span data-stu-id="ff361-711">Element</span></span>|<span data-ttu-id="ff361-712">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-712">Description</span></span>|<span data-ttu-id="ff361-713">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ff361-714">wait</span><span class="sxs-lookup"><span data-stu-id="ff361-714">wait</span></span>|<span data-ttu-id="ff361-715">根元素。</span><span class="sxs-lookup"><span data-stu-id="ff361-715">Root element.</span></span> <span data-ttu-id="ff361-716">只能包含做為子元素 `send-request`、`cache-lookup-value` 和 `choose` 原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="ff361-717">是</span><span class="sxs-lookup"><span data-stu-id="ff361-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ff361-718">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-718">Attributes</span></span>  
  
|<span data-ttu-id="ff361-719">屬性</span><span class="sxs-lookup"><span data-stu-id="ff361-719">Attribute</span></span>|<span data-ttu-id="ff361-720">說明</span><span class="sxs-lookup"><span data-stu-id="ff361-720">Description</span></span>|<span data-ttu-id="ff361-721">必要</span><span class="sxs-lookup"><span data-stu-id="ff361-721">Required</span></span>|<span data-ttu-id="ff361-722">預設值</span><span class="sxs-lookup"><span data-stu-id="ff361-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ff361-723">for</span><span class="sxs-lookup"><span data-stu-id="ff361-723">for</span></span>|<span data-ttu-id="ff361-724">決定是否 hello`wait`原則等候完成的所有直接子原則 toobe 或只有一個。</span><span class="sxs-lookup"><span data-stu-id="ff361-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="ff361-725">允許的值包括：</span><span class="sxs-lookup"><span data-stu-id="ff361-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="ff361-726">-   `all`-等候所有直接子原則 toocomplete</span><span class="sxs-lookup"><span data-stu-id="ff361-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="ff361-727">-任何-等候任何直接子原則 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="ff361-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="ff361-728">第一個直屬子原則 hello 完成後，請 hello`wait`原則完成，並終止執行的其他直屬子原則。</span><span class="sxs-lookup"><span data-stu-id="ff361-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="ff361-729">否</span><span class="sxs-lookup"><span data-stu-id="ff361-729">No</span></span>|<span data-ttu-id="ff361-730">所有</span><span class="sxs-lookup"><span data-stu-id="ff361-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ff361-731">使用量</span><span class="sxs-lookup"><span data-stu-id="ff361-731">Usage</span></span>  
 <span data-ttu-id="ff361-732">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="ff361-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ff361-733">**原則區段︰**輸入、輸出、後端</span><span class="sxs-lookup"><span data-stu-id="ff361-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="ff361-734">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="ff361-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ff361-735">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff361-735">Next steps</span></span>
<span data-ttu-id="ff361-736">如需使用原則的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="ff361-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="ff361-737">API 管理中的原則</span><span class="sxs-lookup"><span data-stu-id="ff361-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="ff361-738">原則運算式</span><span class="sxs-lookup"><span data-stu-id="ff361-738">Policy expressions</span></span>](api-management-policy-expressions.md)
