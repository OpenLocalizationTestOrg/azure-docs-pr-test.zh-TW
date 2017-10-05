---
title: "Azure API 管理進階原則 | Microsoft Docs"
description: "了解可在 Azure API 管理中使用的進階原則。"
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
ms.openlocfilehash: 0c65ac74316421a0258f01143baa25ffecb5be3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="732fa-103">API 管理進階原則</span><span class="sxs-lookup"><span data-stu-id="732fa-103">API Management advanced policies</span></span>
<span data-ttu-id="732fa-104">本主題提供下列 API 管理原則的參考。</span><span class="sxs-lookup"><span data-stu-id="732fa-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="732fa-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="732fa-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="732fa-106"><a name="AdvancedPolicies"></a>進階原則</span><span class="sxs-lookup"><span data-stu-id="732fa-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="732fa-107">[控制流程](api-management-advanced-policies.md#choose) - 根據布林值[運算式](api-management-policy-expressions.md)的評估結果，有條件地套用原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="732fa-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="732fa-108">[轉寄要求](#ForwardRequest) - 將要求轉寄至後端服務。</span><span class="sxs-lookup"><span data-stu-id="732fa-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>

-   <span data-ttu-id="732fa-109">[限制並行](#LimitConcurrency) - 防止超過指定之要求數目同時執行括住的原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than the specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="732fa-110">[記錄至事件中樞](#log-to-eventhub) - 將指定格式的訊息傳送至記錄器實體所定義的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="732fa-110">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="732fa-111">[Mock 回應](#mock-response) - 中止管線執行，並將模擬回應直接傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="732fa-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="732fa-112">[重試](#Retry) - 重試已括住的原則陳述式執行，直到符合條件為止。</span><span class="sxs-lookup"><span data-stu-id="732fa-112">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="732fa-113">系統會在指定的時間間隔重複執行，直到指定的重試計數為止。</span><span class="sxs-lookup"><span data-stu-id="732fa-113">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="732fa-114">[傳回回應](#ReturnResponse) - 中止管線執行，並將指定的回應直接傳回呼叫者。</span><span class="sxs-lookup"><span data-stu-id="732fa-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span> 
  
-   <span data-ttu-id="732fa-115">[傳送單向要求](#SendOneWayRequest) - 將要求傳送到指定的 URL，無須等待回應。</span><span class="sxs-lookup"><span data-stu-id="732fa-115">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="732fa-116">[傳送要求](#SendRequest) - 將要求傳送到指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="732fa-116">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  

-   <span data-ttu-id="732fa-117">[設定 HTTP Proxy](#SetHttpProxy) - 可讓您透過 HTTP Proxy 路由轉送要求。</span><span class="sxs-lookup"><span data-stu-id="732fa-117">[Set HTTP proxy](#SetHttpProxy) - Allows you to route forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="732fa-118">[設定要求方法](#SetRequestMethod) - 允許您變更要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="732fa-118">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="732fa-119">[設定狀態碼](#SetStatus) - 將 HTTP 狀態碼變更為指定的值。</span><span class="sxs-lookup"><span data-stu-id="732fa-119">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="732fa-120">[設定變數](api-management-advanced-policies.md#set-variable) - 保存具名[內容](api-management-policy-expressions.md#ContextVariables)變數中的值，供日後存取使用。</span><span class="sxs-lookup"><span data-stu-id="732fa-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="732fa-121">[追蹤](#Trace) - 將字串新增至 [API 檢查器](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。</span><span class="sxs-lookup"><span data-stu-id="732fa-121">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="732fa-122">[等候](#Wait) - 等候括住的 [Send 要求](api-management-advanced-policies.md#SendRequest)、[取得快取的值](api-management-caching-policies.md#GetFromCacheByKey)或[控制流程](api-management-advanced-policies.md#choose)原則完成後再繼續。</span><span class="sxs-lookup"><span data-stu-id="732fa-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <span data-ttu-id="732fa-123"><a name="choose"></a>控制流程</span><span class="sxs-lookup"><span data-stu-id="732fa-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="732fa-124">`choose` 原則會根據布林運算式 (類似於 if-then-else 或程式語言中的參數建構) 的評估結果套用括住的原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="732fa-124">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="732fa-125"><a name="ChoosePolicyStatement"></a>原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="732fa-126">控制流程原則至少必須包含一個 `<when/>` 元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-126">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="732fa-127">`<otherwise/>` 則是選擇性元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-127">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="732fa-128">`<when/>` 元素中的條件會依其在原則內的出現順序進行評估。</span><span class="sxs-lookup"><span data-stu-id="732fa-128">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="732fa-129">系統會套用條件屬性等於 `true` 的第一個 `<when/>` 元素內所括住的原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="732fa-129">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="732fa-130">如果所有 `<when/>` 元素的條件屬性都是 `false`，則會套用 `<otherwise/>` 元素內所括住的原則 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="732fa-130">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="732fa-131">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-131">Examples</span></span>  
  
####  <span data-ttu-id="732fa-132"><a name="ChooseExample"></a>範例</span><span class="sxs-lookup"><span data-stu-id="732fa-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="732fa-133">下列範例會示範 [set-variable](api-management-advanced-policies.md#set-variable) 原則和兩個控制流程原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-133">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="732fa-134">設定變數原則位於 inbound 區段中，並且會在 `User-Agent` 要求標頭包含文字 `iPad` 或 `iPhone` 時，建立設為 true 的 `isMobile` 布林[內容](api-management-policy-expressions.md#ContextVariables)變數。</span><span class="sxs-lookup"><span data-stu-id="732fa-134">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="732fa-135">第一個控制流程原則也位於 inbound 區段中，並且會按照條件，根據 `isMobile` 內容變數的值套用兩個[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter)原則的其中一個。</span><span class="sxs-lookup"><span data-stu-id="732fa-135">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="732fa-136">第二個控制流程原則位於 outbound 區段中，並且會按照條件，在 `isMobile` 設為 `true` 時套用[將 XML 轉換為 JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) 原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-136">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="732fa-137">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-137">Example</span></span>  
 <span data-ttu-id="732fa-138">這個範例示範如何在使用 `Starter` 產品時，移除「從後端服務收到的回應」中的資料元素，藉此執行內容篩選。</span><span class="sxs-lookup"><span data-stu-id="732fa-138">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="732fa-139">如需設定和使用此原則的示範，請觀賞 [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)，快轉到 34:30。</span><span class="sxs-lookup"><span data-stu-id="732fa-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="732fa-140">從 31:50 處開始觀賞用於本示範的 [The Dark Sky Forecast API](https://developer.forecast.io/) 概觀。</span><span class="sxs-lookup"><span data-stu-id="732fa-140">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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
  
### <a name="elements"></a><span data-ttu-id="732fa-141">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-141">Elements</span></span>  
  
|<span data-ttu-id="732fa-142">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-142">Element</span></span>|<span data-ttu-id="732fa-143">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-143">Description</span></span>|<span data-ttu-id="732fa-144">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-145">choose</span><span class="sxs-lookup"><span data-stu-id="732fa-145">choose</span></span>|<span data-ttu-id="732fa-146">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-146">Root element.</span></span>|<span data-ttu-id="732fa-147">是</span><span class="sxs-lookup"><span data-stu-id="732fa-147">Yes</span></span>|  
|<span data-ttu-id="732fa-148">when</span><span class="sxs-lookup"><span data-stu-id="732fa-148">when</span></span>|<span data-ttu-id="732fa-149">要用於 `choose` 原則之 `if` 或 `ifelse` 組件的條件。</span><span class="sxs-lookup"><span data-stu-id="732fa-149">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="732fa-150">如果 `choose` 原則有多個 `when` 區段，則會依序評估這些區段。</span><span class="sxs-lookup"><span data-stu-id="732fa-150">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="732fa-151">一旦 when 元素的 `condition` 評估為 `true` 後，就不會再評估後面的 `when` 條件。</span><span class="sxs-lookup"><span data-stu-id="732fa-151">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="732fa-152">是</span><span class="sxs-lookup"><span data-stu-id="732fa-152">Yes</span></span>|  
|<span data-ttu-id="732fa-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="732fa-153">otherwise</span></span>|<span data-ttu-id="732fa-154">內含沒有任何 `when` 條件評估為 `true` 時，所要使用的原則片段。</span><span class="sxs-lookup"><span data-stu-id="732fa-154">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="732fa-155">否</span><span class="sxs-lookup"><span data-stu-id="732fa-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-156">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-156">Attributes</span></span>  
  
|<span data-ttu-id="732fa-157">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-157">Attribute</span></span>|<span data-ttu-id="732fa-158">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-158">Description</span></span>|<span data-ttu-id="732fa-159">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="732fa-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="732fa-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="732fa-161">所包含之 `when` 原則陳述式受到評估時，所要評估的布林運算式或常數。</span><span class="sxs-lookup"><span data-stu-id="732fa-161">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="732fa-162">是</span><span class="sxs-lookup"><span data-stu-id="732fa-162">Yes</span></span>|  
  
###  <span data-ttu-id="732fa-163"><a name="ChooseUsage"></a>使用方式</span><span class="sxs-lookup"><span data-stu-id="732fa-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="732fa-164">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-164">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-165">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-166">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="732fa-167"><a name="ForwardRequest"></a>轉送要求</span><span class="sxs-lookup"><span data-stu-id="732fa-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="732fa-168">`forward-request` 原則會將內送要求轉送給要求[內容](api-management-policy-expressions.md#ContextVariables)中指定的後端服務。</span><span class="sxs-lookup"><span data-stu-id="732fa-168">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="732fa-169">後端服務 URL 會指定於 API [設定](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings)中，而且可以使用[設定後端服務](api-management-transformation-policies.md)原則加以變更。</span><span class="sxs-lookup"><span data-stu-id="732fa-169">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="732fa-170">移除此原則會導致要求不會轉送到後端服務中，而且當 inbound 區段中的原則一順利完成，就會立即評估 outbound 區段中的原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-170">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-171">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="732fa-172">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="732fa-173">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-173">Example</span></span>  
 <span data-ttu-id="732fa-174">下列 API 層級原則會將所有要求轉送至後端服務，且逾時間隔為 60 秒。</span><span class="sxs-lookup"><span data-stu-id="732fa-174">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="732fa-175">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-175">Example</span></span>  
 <span data-ttu-id="732fa-176">此作業層級原則使用 `base` 元素，從父 API 層級範圍繼承後端原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-176">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="732fa-177">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-177">Example</span></span>  
 <span data-ttu-id="732fa-178">此作業層級原則會明確地將所有要求轉送至後端服務 (逾時值為 120)，且不會繼承父 API 層級的後端原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-178">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="732fa-179">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-179">Example</span></span>  
 <span data-ttu-id="732fa-180">此作業層級原則不會將要求轉送到後端服務。</span><span class="sxs-lookup"><span data-stu-id="732fa-180">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="732fa-181">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-181">Elements</span></span>  
  
|<span data-ttu-id="732fa-182">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-182">Element</span></span>|<span data-ttu-id="732fa-183">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-183">Description</span></span>|<span data-ttu-id="732fa-184">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="732fa-185">forward-request</span></span>|<span data-ttu-id="732fa-186">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-186">Root element.</span></span>|<span data-ttu-id="732fa-187">是</span><span class="sxs-lookup"><span data-stu-id="732fa-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-188">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-188">Attributes</span></span>  
  
|<span data-ttu-id="732fa-189">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-189">Attribute</span></span>|<span data-ttu-id="732fa-190">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-190">Description</span></span>|<span data-ttu-id="732fa-191">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-191">Required</span></span>|<span data-ttu-id="732fa-192">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="732fa-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="732fa-193">timeout="integer"</span></span>|<span data-ttu-id="732fa-194">以秒為單位的逾時間隔，後端服務的呼叫在經過此間隔後便會失敗。</span><span class="sxs-lookup"><span data-stu-id="732fa-194">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="732fa-195">否</span><span class="sxs-lookup"><span data-stu-id="732fa-195">No</span></span>|<span data-ttu-id="732fa-196">無逾時</span><span class="sxs-lookup"><span data-stu-id="732fa-196">No timeout</span></span>|  
|<span data-ttu-id="732fa-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="732fa-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="732fa-198">指定來自後端服務的重新導向會由閘道遵循或傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="732fa-198">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="732fa-199">否</span><span class="sxs-lookup"><span data-stu-id="732fa-199">No</span></span>|<span data-ttu-id="732fa-200">false</span><span class="sxs-lookup"><span data-stu-id="732fa-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-201">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-201">Usage</span></span>  
 <span data-ttu-id="732fa-202">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-203">**原則區段︰**後端</span><span class="sxs-lookup"><span data-stu-id="732fa-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="732fa-204">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="732fa-205"><a name="LimitConcurrency"></a> 限制並行</span><span class="sxs-lookup"><span data-stu-id="732fa-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="732fa-206">`limit-concurrency` 原則可防止超過指定之要求數目在指定的時間執行括住的原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-206">The `limit-concurrency` policy prevents enclosed policies from executing by more than the specified number of requests at a given time.</span></span> <span data-ttu-id="732fa-207">在超出閾值時，新的要求會新增至佇列，直到達到最大佇列長度為止。</span><span class="sxs-lookup"><span data-stu-id="732fa-207">Upon exceeding the threshold, new requests are added to a queue, until the maximum queue length is achieved.</span></span> <span data-ttu-id="732fa-208">在佇列耗盡時，新的要求會立即失敗。</span><span class="sxs-lookup"><span data-stu-id="732fa-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="732fa-209"><a name="LimitConcurrencyStatement"></a>原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="732fa-210">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-210">Examples</span></span>  
  
####  <span data-ttu-id="732fa-211"><a name="ChooseExample"></a>範例</span><span class="sxs-lookup"><span data-stu-id="732fa-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="732fa-212">下列範例示範如何根據內容變數的值，限制轉送至後端的要求數目。</span><span class="sxs-lookup"><span data-stu-id="732fa-212">The following example demonstrates how to limit number of requests forwarded to a backend based on the value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="732fa-213">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-213">Elements</span></span>  
  
|<span data-ttu-id="732fa-214">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-214">Element</span></span>|<span data-ttu-id="732fa-215">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-215">Description</span></span>|<span data-ttu-id="732fa-216">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="732fa-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="732fa-217">limit-concurrency</span></span>|<span data-ttu-id="732fa-218">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-218">Root element.</span></span>|<span data-ttu-id="732fa-219">是</span><span class="sxs-lookup"><span data-stu-id="732fa-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-220">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-220">Attributes</span></span>  
  
|<span data-ttu-id="732fa-221">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-221">Attribute</span></span>|<span data-ttu-id="732fa-222">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-222">Description</span></span>|<span data-ttu-id="732fa-223">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-223">Required</span></span>|<span data-ttu-id="732fa-224">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="732fa-225">key</span><span class="sxs-lookup"><span data-stu-id="732fa-225">key</span></span>|<span data-ttu-id="732fa-226">字串。</span><span class="sxs-lookup"><span data-stu-id="732fa-226">A string.</span></span> <span data-ttu-id="732fa-227">允許的運算式。</span><span class="sxs-lookup"><span data-stu-id="732fa-227">Expression allowed.</span></span> <span data-ttu-id="732fa-228">指定並行範圍。</span><span class="sxs-lookup"><span data-stu-id="732fa-228">Specifies the concurrency scope.</span></span> <span data-ttu-id="732fa-229">可由多個原則共用。</span><span class="sxs-lookup"><span data-stu-id="732fa-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="732fa-230">是</span><span class="sxs-lookup"><span data-stu-id="732fa-230">Yes</span></span>|<span data-ttu-id="732fa-231">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-231">N/A</span></span>|  
|<span data-ttu-id="732fa-232">max-count</span><span class="sxs-lookup"><span data-stu-id="732fa-232">max-count</span></span>|<span data-ttu-id="732fa-233">整數。</span><span class="sxs-lookup"><span data-stu-id="732fa-233">An integer.</span></span> <span data-ttu-id="732fa-234">指定允許輸入原則的要求數目上限。</span><span class="sxs-lookup"><span data-stu-id="732fa-234">Specifies a maximum number of requests that are allowed to enter the policy.</span></span>|<span data-ttu-id="732fa-235">是</span><span class="sxs-lookup"><span data-stu-id="732fa-235">Yes</span></span>|<span data-ttu-id="732fa-236">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-236">N/A</span></span>|  
|<span data-ttu-id="732fa-237">timeout</span><span class="sxs-lookup"><span data-stu-id="732fa-237">timeout</span></span>|<span data-ttu-id="732fa-238">整數。</span><span class="sxs-lookup"><span data-stu-id="732fa-238">An integer.</span></span> <span data-ttu-id="732fa-239">允許的運算式。</span><span class="sxs-lookup"><span data-stu-id="732fa-239">Expression allowed.</span></span> <span data-ttu-id="732fa-240">指定要求因為「403 太多要求」而失敗之前，應等候進入某個範圍的秒數</span><span class="sxs-lookup"><span data-stu-id="732fa-240">Specifies the number of seconds a request should wait to enter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="732fa-241">否</span><span class="sxs-lookup"><span data-stu-id="732fa-241">No</span></span>|<span data-ttu-id="732fa-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="732fa-242">Infinity</span></span>|  
|<span data-ttu-id="732fa-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="732fa-243">max-queue-length</span></span>|<span data-ttu-id="732fa-244">整數。</span><span class="sxs-lookup"><span data-stu-id="732fa-244">An integer.</span></span> <span data-ttu-id="732fa-245">允許的運算式。</span><span class="sxs-lookup"><span data-stu-id="732fa-245">Expression allowed.</span></span> <span data-ttu-id="732fa-246">指定最大佇列長度。</span><span class="sxs-lookup"><span data-stu-id="732fa-246">Specifies the maximum queue length.</span></span> <span data-ttu-id="732fa-247">嘗試輸入此原則的內送要求將會終止，因為佇列耗盡時立即出現「403 太多要求」。</span><span class="sxs-lookup"><span data-stu-id="732fa-247">Incoming requests trying to enter this policy will be terminated with “403 Too Many Requests” immediately when the queue is exhausted.</span></span>|<span data-ttu-id="732fa-248">否</span><span class="sxs-lookup"><span data-stu-id="732fa-248">No</span></span>|<span data-ttu-id="732fa-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="732fa-249">Infinity</span></span>|  
  
###  <span data-ttu-id="732fa-250"><a name="ChooseUsage"></a>使用方式</span><span class="sxs-lookup"><span data-stu-id="732fa-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="732fa-251">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-251">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-252">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-253">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="732fa-254"><a name="log-to-eventhub"></a>記錄到事件中樞</span><span class="sxs-lookup"><span data-stu-id="732fa-254"><a name="log-to-eventhub"></a> Log to Event Hub</span></span>  
 <span data-ttu-id="732fa-255">`log-to-eventhub` 原則會將指定格式的訊息傳送至記錄器實體所定義的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="732fa-255">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="732fa-256">此原則正如其名，可用來儲存選取的要求或回應內容資訊，以進行線上或離線分析。</span><span class="sxs-lookup"><span data-stu-id="732fa-256">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="732fa-257">如需如何設定事件中樞和記錄事件的逐步指南，請參閱[如何使用 Azure 事件中樞記錄 API 管理事件](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="732fa-257">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-258">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="732fa-259">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-259">Example</span></span>  
 <span data-ttu-id="732fa-260">任何字串皆可做為值來記錄到事件中樞內。</span><span class="sxs-lookup"><span data-stu-id="732fa-260">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="732fa-261">在此範例中，所有傳入呼叫的日期和時間、部署服務名稱、要求識別碼、IP 位址和作業名稱，都會記錄到以 `contoso-logger` 識別碼所註冊的事件中樞記錄器內。</span><span class="sxs-lookup"><span data-stu-id="732fa-261">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="732fa-262">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-262">Elements</span></span>  
  
|<span data-ttu-id="732fa-263">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-263">Element</span></span>|<span data-ttu-id="732fa-264">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-264">Description</span></span>|<span data-ttu-id="732fa-265">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="732fa-266">log-to-eventhub</span></span>|<span data-ttu-id="732fa-267">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-267">Root element.</span></span> <span data-ttu-id="732fa-268">此元素的值是要記錄至事件中樞的字串。</span><span class="sxs-lookup"><span data-stu-id="732fa-268">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="732fa-269">是</span><span class="sxs-lookup"><span data-stu-id="732fa-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-270">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-270">Attributes</span></span>  
  
|<span data-ttu-id="732fa-271">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-271">Attribute</span></span>|<span data-ttu-id="732fa-272">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-272">Description</span></span>|<span data-ttu-id="732fa-273">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="732fa-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="732fa-274">logger-id</span></span>|<span data-ttu-id="732fa-275">向 API 管理服務註冊之記錄器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="732fa-275">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="732fa-276">是</span><span class="sxs-lookup"><span data-stu-id="732fa-276">Yes</span></span>|  
|<span data-ttu-id="732fa-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="732fa-277">partition-id</span></span>|<span data-ttu-id="732fa-278">指定訊息傳送目的地的資料分割索引。</span><span class="sxs-lookup"><span data-stu-id="732fa-278">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="732fa-279">選用。</span><span class="sxs-lookup"><span data-stu-id="732fa-279">Optional.</span></span> <span data-ttu-id="732fa-280">如果使用 `partition-key`，就不能使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="732fa-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="732fa-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="732fa-281">partition-key</span></span>|<span data-ttu-id="732fa-282">指定在傳送訊息時，用來指派資料分割的值。</span><span class="sxs-lookup"><span data-stu-id="732fa-282">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="732fa-283">選用。</span><span class="sxs-lookup"><span data-stu-id="732fa-283">Optional.</span></span> <span data-ttu-id="732fa-284">如果使用 `partition-id`，就不能使用這個屬性。</span><span class="sxs-lookup"><span data-stu-id="732fa-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-285">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-285">Usage</span></span>  
 <span data-ttu-id="732fa-286">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-286">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-287">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-288">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="732fa-289"><a name="mock-response"></a> Mock 回應</span><span class="sxs-lookup"><span data-stu-id="732fa-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="732fa-290">如名稱所示，`mock-response` 是用來模擬 API 和作業。</span><span class="sxs-lookup"><span data-stu-id="732fa-290">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="732fa-291">它會中止正常的管線執行，並將模擬回應傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="732fa-291">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="732fa-292">原則一律會嘗試傳回最高精確度的回應。</span><span class="sxs-lookup"><span data-stu-id="732fa-292">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="732fa-293">它偏好使用回應內容範例 (若可使用)。</span><span class="sxs-lookup"><span data-stu-id="732fa-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="732fa-294">當提供結構描述而無提供範例時，它會從結構描述產生範例回應。</span><span class="sxs-lookup"><span data-stu-id="732fa-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="732fa-295">如果沒有找到範例或結構描述，則會傳回沒有內容的回應。</span><span class="sxs-lookup"><span data-stu-id="732fa-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-296">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="732fa-297">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="732fa-298">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-298">Elements</span></span>  
  
|<span data-ttu-id="732fa-299">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-299">Element</span></span>|<span data-ttu-id="732fa-300">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-300">Description</span></span>|<span data-ttu-id="732fa-301">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="732fa-302">mock-response</span></span>|<span data-ttu-id="732fa-303">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-303">Root element.</span></span>|<span data-ttu-id="732fa-304">是</span><span class="sxs-lookup"><span data-stu-id="732fa-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-305">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-305">Attributes</span></span>  
  
|<span data-ttu-id="732fa-306">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-306">Attribute</span></span>|<span data-ttu-id="732fa-307">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-307">Description</span></span>|<span data-ttu-id="732fa-308">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-308">Required</span></span>|<span data-ttu-id="732fa-309">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="732fa-310">status-code</span><span class="sxs-lookup"><span data-stu-id="732fa-310">status-code</span></span>|<span data-ttu-id="732fa-311">指定回應狀態碼，且用來選取對應範例或結構描述。</span><span class="sxs-lookup"><span data-stu-id="732fa-311">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="732fa-312">否</span><span class="sxs-lookup"><span data-stu-id="732fa-312">No</span></span>|<span data-ttu-id="732fa-313">200</span><span class="sxs-lookup"><span data-stu-id="732fa-313">200</span></span>|  
|<span data-ttu-id="732fa-314">Content-Type</span><span class="sxs-lookup"><span data-stu-id="732fa-314">content-type</span></span>|<span data-ttu-id="732fa-315">指定 `Content-Type` 回應標頭值，且用來選取對應範例或結構描述。</span><span class="sxs-lookup"><span data-stu-id="732fa-315">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="732fa-316">否</span><span class="sxs-lookup"><span data-stu-id="732fa-316">No</span></span>|<span data-ttu-id="732fa-317">None</span><span class="sxs-lookup"><span data-stu-id="732fa-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-318">使用方式</span><span class="sxs-lookup"><span data-stu-id="732fa-318">Usage</span></span>  
 <span data-ttu-id="732fa-319">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-319">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-320">**原則區段︰**輸入、輸出、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="732fa-321">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="732fa-322"><a name="Retry"></a>重試</span><span class="sxs-lookup"><span data-stu-id="732fa-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="732fa-323">`retry` 原則會執行其子原則一次，然後重試子原則的執行，直到重試 `condition` 變成 `false` 或重試 `count` 用盡。</span><span class="sxs-lookup"><span data-stu-id="732fa-323">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-324">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="732fa-325">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-325">Example</span></span>  
 <span data-ttu-id="732fa-326">下列範例會使用指數重試演算法重試要求轉送達十次之多。</span><span class="sxs-lookup"><span data-stu-id="732fa-326">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="732fa-327">由於 `first-fast-retry` 設為 false，所有重試嘗試都會使用指數重試演算法。</span><span class="sxs-lookup"><span data-stu-id="732fa-327">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="732fa-328">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-328">Elements</span></span>  
  
|<span data-ttu-id="732fa-329">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-329">Element</span></span>|<span data-ttu-id="732fa-330">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-330">Description</span></span>|<span data-ttu-id="732fa-331">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-332">retry</span><span class="sxs-lookup"><span data-stu-id="732fa-332">retry</span></span>|<span data-ttu-id="732fa-333">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-333">Root element.</span></span> <span data-ttu-id="732fa-334">可包含其他任何原則來做為其子元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="732fa-335">是</span><span class="sxs-lookup"><span data-stu-id="732fa-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-336">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-336">Attributes</span></span>  
  
|<span data-ttu-id="732fa-337">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-337">Attribute</span></span>|<span data-ttu-id="732fa-338">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-338">Description</span></span>|<span data-ttu-id="732fa-339">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-339">Required</span></span>|<span data-ttu-id="732fa-340">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="732fa-341">condition</span><span class="sxs-lookup"><span data-stu-id="732fa-341">condition</span></span>|<span data-ttu-id="732fa-342">布林常值或[運算式](api-management-policy-expressions.md)，指定應停止 (`false`) 還是繼續 (`true`) 重試。</span><span class="sxs-lookup"><span data-stu-id="732fa-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="732fa-343">是</span><span class="sxs-lookup"><span data-stu-id="732fa-343">Yes</span></span>|<span data-ttu-id="732fa-344">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-344">N/A</span></span>|  
|<span data-ttu-id="732fa-345">計數</span><span class="sxs-lookup"><span data-stu-id="732fa-345">count</span></span>|<span data-ttu-id="732fa-346">正數，指定要嘗試的重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="732fa-346">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="732fa-347">是</span><span class="sxs-lookup"><span data-stu-id="732fa-347">Yes</span></span>|<span data-ttu-id="732fa-348">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-348">N/A</span></span>|  
|<span data-ttu-id="732fa-349">interval</span><span class="sxs-lookup"><span data-stu-id="732fa-349">interval</span></span>|<span data-ttu-id="732fa-350">以秒為單位的正數，指定重試嘗試之間的等待間隔。</span><span class="sxs-lookup"><span data-stu-id="732fa-350">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="732fa-351">是</span><span class="sxs-lookup"><span data-stu-id="732fa-351">Yes</span></span>|<span data-ttu-id="732fa-352">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-352">N/A</span></span>|  
|<span data-ttu-id="732fa-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="732fa-353">max-interval</span></span>|<span data-ttu-id="732fa-354">以秒為單位的正數，指定重試嘗試之間的最大等待間隔。</span><span class="sxs-lookup"><span data-stu-id="732fa-354">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="732fa-355">此屬性可用來實作指數重試演算法。</span><span class="sxs-lookup"><span data-stu-id="732fa-355">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="732fa-356">否</span><span class="sxs-lookup"><span data-stu-id="732fa-356">No</span></span>|<span data-ttu-id="732fa-357">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-357">N/A</span></span>|  
|<span data-ttu-id="732fa-358">delta</span><span class="sxs-lookup"><span data-stu-id="732fa-358">delta</span></span>|<span data-ttu-id="732fa-359">以秒為單位的正數，指定等待間隔的增量。</span><span class="sxs-lookup"><span data-stu-id="732fa-359">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="732fa-360">此屬性可用來實作線性和指數的重試演算法。</span><span class="sxs-lookup"><span data-stu-id="732fa-360">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="732fa-361">否</span><span class="sxs-lookup"><span data-stu-id="732fa-361">No</span></span>|<span data-ttu-id="732fa-362">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-362">N/A</span></span>|  
|<span data-ttu-id="732fa-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="732fa-363">first-fast-retry</span></span>|<span data-ttu-id="732fa-364">如果設為 `true`，則會立即執行第一次的重試嘗試。</span><span class="sxs-lookup"><span data-stu-id="732fa-364">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="732fa-365">否</span><span class="sxs-lookup"><span data-stu-id="732fa-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="732fa-366">當只有指定 `interval` 時，會執行**固定**間隔的重試。</span><span class="sxs-lookup"><span data-stu-id="732fa-366">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="732fa-367">當只有指定 `interval` 和 `delta` 時，會使用**線性**的間隔重試演算法，其中，重試之間的等待時間會根據下列公式來進行計算：`interval + (count - 1)*delta`。</span><span class="sxs-lookup"><span data-stu-id="732fa-367">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="732fa-368">當指定了 `interval`、`max-interval` 和 `delta` 時，則會套用**指數**的間隔重試演算法，其中，重試之間的等待時間會根據下列公式，以指數方式從 `interval` 的值增加到 `max-interval` 的值：`min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`。</span><span class="sxs-lookup"><span data-stu-id="732fa-368">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="732fa-369">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-369">Usage</span></span>  
 <span data-ttu-id="732fa-370">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-370">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="732fa-371">請注意，此原則會繼承子原則的使用方式限制。</span><span class="sxs-lookup"><span data-stu-id="732fa-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="732fa-372">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-373">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="732fa-374"><a name="ReturnResponse"></a>傳回回應</span><span class="sxs-lookup"><span data-stu-id="732fa-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="732fa-375">`return-response` 原則會中止管線的執行，並將預設或自訂的回應傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="732fa-375">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="732fa-376">預設回應是 `200 OK`，且沒有本文。</span><span class="sxs-lookup"><span data-stu-id="732fa-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="732fa-377">透過內容變數或原則陳述式即可指定自訂回應。</span><span class="sxs-lookup"><span data-stu-id="732fa-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="732fa-378">若同時提供兩者，原則陳述式會先修改內容變數中包含的回應，再傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="732fa-378">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-379">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="732fa-380">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="732fa-381">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-381">Elements</span></span>  
  
|<span data-ttu-id="732fa-382">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-382">Element</span></span>|<span data-ttu-id="732fa-383">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-383">Description</span></span>|<span data-ttu-id="732fa-384">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-385">return-response</span><span class="sxs-lookup"><span data-stu-id="732fa-385">return-response</span></span>|<span data-ttu-id="732fa-386">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-386">Root element.</span></span>|<span data-ttu-id="732fa-387">是</span><span class="sxs-lookup"><span data-stu-id="732fa-387">Yes</span></span>|  
|<span data-ttu-id="732fa-388">set-header</span><span class="sxs-lookup"><span data-stu-id="732fa-388">set-header</span></span>|<span data-ttu-id="732fa-389">[set-header](api-management-transformation-policies.md#SetHTTPheader) 原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="732fa-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="732fa-390">否</span><span class="sxs-lookup"><span data-stu-id="732fa-390">No</span></span>|  
|<span data-ttu-id="732fa-391">set-body</span><span class="sxs-lookup"><span data-stu-id="732fa-391">set-body</span></span>|<span data-ttu-id="732fa-392">[set-body](api-management-transformation-policies.md#SetBody) 原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="732fa-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="732fa-393">否</span><span class="sxs-lookup"><span data-stu-id="732fa-393">No</span></span>|  
|<span data-ttu-id="732fa-394">set-status</span><span class="sxs-lookup"><span data-stu-id="732fa-394">set-status</span></span>|<span data-ttu-id="732fa-395">[set-status](api-management-advanced-policies.md#SetStatus) 原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="732fa-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="732fa-396">否</span><span class="sxs-lookup"><span data-stu-id="732fa-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-397">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-397">Attributes</span></span>  
  
|<span data-ttu-id="732fa-398">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-398">Attribute</span></span>|<span data-ttu-id="732fa-399">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-399">Description</span></span>|<span data-ttu-id="732fa-400">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="732fa-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="732fa-401">response-variable-name</span></span>|<span data-ttu-id="732fa-402">所參考的內容變數名稱，其參考來源為 (舉例來說) 上游 [send-request](api-management-advanced-policies.md#SendRequest) 原則，且包含 `Response` 物件</span><span class="sxs-lookup"><span data-stu-id="732fa-402">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="732fa-403">選用。</span><span class="sxs-lookup"><span data-stu-id="732fa-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-404">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-404">Usage</span></span>  
 <span data-ttu-id="732fa-405">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-405">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-406">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-407">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="732fa-408"><a name="SendOneWayRequest"></a>傳送單向要求</span><span class="sxs-lookup"><span data-stu-id="732fa-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="732fa-409">`send-one-way-request` 原則會將所提供的要求傳送到指定的 URL，無須等待回應。</span><span class="sxs-lookup"><span data-stu-id="732fa-409">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-410">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="732fa-411">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-411">Example</span></span>  
 <span data-ttu-id="732fa-412">此一相同原則會舉例說明如何使用 `send-one-way-request` 原則，以在 HTTP 回應碼大於或等於 500 時，將訊息傳送至 Slack 聊天室。</span><span class="sxs-lookup"><span data-stu-id="732fa-412">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="732fa-413">如需此範例的詳細資訊，請參閱[使用來自 Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。</span><span class="sxs-lookup"><span data-stu-id="732fa-413">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="732fa-414">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-414">Elements</span></span>  
  
|<span data-ttu-id="732fa-415">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-415">Element</span></span>|<span data-ttu-id="732fa-416">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-416">Description</span></span>|<span data-ttu-id="732fa-417">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="732fa-418">send-one-way-request</span></span>|<span data-ttu-id="732fa-419">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-419">Root element.</span></span>|<span data-ttu-id="732fa-420">是</span><span class="sxs-lookup"><span data-stu-id="732fa-420">Yes</span></span>|  
|<span data-ttu-id="732fa-421">url</span><span class="sxs-lookup"><span data-stu-id="732fa-421">url</span></span>|<span data-ttu-id="732fa-422">要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="732fa-422">The URL of the request.</span></span>|<span data-ttu-id="732fa-423">mode=copy 時為 [否]；否則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="732fa-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="732fa-424">method</span><span class="sxs-lookup"><span data-stu-id="732fa-424">method</span></span>|<span data-ttu-id="732fa-425">要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="732fa-425">The HTTP method for the request.</span></span>|<span data-ttu-id="732fa-426">mode=copy 時為 [否]；否則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="732fa-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="732fa-427">頁首</span><span class="sxs-lookup"><span data-stu-id="732fa-427">header</span></span>|<span data-ttu-id="732fa-428">要求標頭。</span><span class="sxs-lookup"><span data-stu-id="732fa-428">Request header.</span></span> <span data-ttu-id="732fa-429">若有多個要求標頭，請使用多個 header 元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="732fa-430">否</span><span class="sxs-lookup"><span data-stu-id="732fa-430">No</span></span>|  
|<span data-ttu-id="732fa-431">body</span><span class="sxs-lookup"><span data-stu-id="732fa-431">body</span></span>|<span data-ttu-id="732fa-432">要求本文。</span><span class="sxs-lookup"><span data-stu-id="732fa-432">The request body.</span></span>|<span data-ttu-id="732fa-433">否</span><span class="sxs-lookup"><span data-stu-id="732fa-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-434">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-434">Attributes</span></span>  
  
|<span data-ttu-id="732fa-435">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-435">Attribute</span></span>|<span data-ttu-id="732fa-436">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-436">Description</span></span>|<span data-ttu-id="732fa-437">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-437">Required</span></span>|<span data-ttu-id="732fa-438">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="732fa-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="732fa-439">mode="string"</span></span>|<span data-ttu-id="732fa-440">判斷這是新要求還是現行要求的複本。</span><span class="sxs-lookup"><span data-stu-id="732fa-440">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="732fa-441">在輸出模式中，mode=copy 不會初始化要求本文。</span><span class="sxs-lookup"><span data-stu-id="732fa-441">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="732fa-442">否</span><span class="sxs-lookup"><span data-stu-id="732fa-442">No</span></span>|<span data-ttu-id="732fa-443">新增</span><span class="sxs-lookup"><span data-stu-id="732fa-443">New</span></span>|  
|<span data-ttu-id="732fa-444">名稱</span><span class="sxs-lookup"><span data-stu-id="732fa-444">name</span></span>|<span data-ttu-id="732fa-445">指定要設定之標頭的名稱。</span><span class="sxs-lookup"><span data-stu-id="732fa-445">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="732fa-446">是</span><span class="sxs-lookup"><span data-stu-id="732fa-446">Yes</span></span>|<span data-ttu-id="732fa-447">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-447">N/A</span></span>|  
|<span data-ttu-id="732fa-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="732fa-448">exists-action</span></span>|<span data-ttu-id="732fa-449">指定當已指定標頭時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="732fa-449">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="732fa-450">此屬性必須具有下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="732fa-450">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="732fa-451">-   override - 取代現有標頭的值。</span><span class="sxs-lookup"><span data-stu-id="732fa-451">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="732fa-452">-   skip - 不取代現有的標頭值。</span><span class="sxs-lookup"><span data-stu-id="732fa-452">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="732fa-453">-   append - 將值附加至現有標頭值之後。</span><span class="sxs-lookup"><span data-stu-id="732fa-453">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="732fa-454">-   delete - 移除要求中的標頭。</span><span class="sxs-lookup"><span data-stu-id="732fa-454">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="732fa-455">設為 `override` 時，編列多個相同名稱的項目會導致根據所有項目來設定標頭 (列出多次)；只有列出的值才會設定在結果中。</span><span class="sxs-lookup"><span data-stu-id="732fa-455">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="732fa-456">否</span><span class="sxs-lookup"><span data-stu-id="732fa-456">No</span></span>|<span data-ttu-id="732fa-457">override</span><span class="sxs-lookup"><span data-stu-id="732fa-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-458">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-458">Usage</span></span>  
 <span data-ttu-id="732fa-459">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-459">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-460">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-461">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="732fa-462"><a name="SendRequest"></a>傳送要求</span><span class="sxs-lookup"><span data-stu-id="732fa-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="732fa-463">`send-request` 原則會將所提供的要求傳送至指定的 URL，等候時間不會超過所設定的逾時值。</span><span class="sxs-lookup"><span data-stu-id="732fa-463">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-464">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="732fa-465">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-465">Example</span></span>  
 <span data-ttu-id="732fa-466">此範例會顯示向授權伺服器確認參考權杖的方法。</span><span class="sxs-lookup"><span data-stu-id="732fa-466">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="732fa-467">如需此範例的詳細資訊，請參閱[使用來自 Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。</span><span class="sxs-lookup"><span data-stu-id="732fa-467">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
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
  
### <a name="elements"></a><span data-ttu-id="732fa-468">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-468">Elements</span></span>  
  
|<span data-ttu-id="732fa-469">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-469">Element</span></span>|<span data-ttu-id="732fa-470">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-470">Description</span></span>|<span data-ttu-id="732fa-471">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-472">send-request</span><span class="sxs-lookup"><span data-stu-id="732fa-472">send-request</span></span>|<span data-ttu-id="732fa-473">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-473">Root element.</span></span>|<span data-ttu-id="732fa-474">是</span><span class="sxs-lookup"><span data-stu-id="732fa-474">Yes</span></span>|  
|<span data-ttu-id="732fa-475">url</span><span class="sxs-lookup"><span data-stu-id="732fa-475">url</span></span>|<span data-ttu-id="732fa-476">要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="732fa-476">The URL of the request.</span></span>|<span data-ttu-id="732fa-477">mode=copy 時為 [否]；否則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="732fa-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="732fa-478">method</span><span class="sxs-lookup"><span data-stu-id="732fa-478">method</span></span>|<span data-ttu-id="732fa-479">要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="732fa-479">The HTTP method for the request.</span></span>|<span data-ttu-id="732fa-480">mode=copy 時為 [否]；否則為 [是]。</span><span class="sxs-lookup"><span data-stu-id="732fa-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="732fa-481">頁首</span><span class="sxs-lookup"><span data-stu-id="732fa-481">header</span></span>|<span data-ttu-id="732fa-482">要求標頭。</span><span class="sxs-lookup"><span data-stu-id="732fa-482">Request header.</span></span> <span data-ttu-id="732fa-483">若有多個要求標頭，請使用多個 header 元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="732fa-484">否</span><span class="sxs-lookup"><span data-stu-id="732fa-484">No</span></span>|  
|<span data-ttu-id="732fa-485">body</span><span class="sxs-lookup"><span data-stu-id="732fa-485">body</span></span>|<span data-ttu-id="732fa-486">要求本文。</span><span class="sxs-lookup"><span data-stu-id="732fa-486">The request body.</span></span>|<span data-ttu-id="732fa-487">否</span><span class="sxs-lookup"><span data-stu-id="732fa-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-488">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-488">Attributes</span></span>  
  
|<span data-ttu-id="732fa-489">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-489">Attribute</span></span>|<span data-ttu-id="732fa-490">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-490">Description</span></span>|<span data-ttu-id="732fa-491">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-491">Required</span></span>|<span data-ttu-id="732fa-492">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="732fa-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="732fa-493">mode="string"</span></span>|<span data-ttu-id="732fa-494">判斷這是新要求還是現行要求的複本。</span><span class="sxs-lookup"><span data-stu-id="732fa-494">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="732fa-495">在輸出模式中，mode=copy 不會初始化要求本文。</span><span class="sxs-lookup"><span data-stu-id="732fa-495">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="732fa-496">否</span><span class="sxs-lookup"><span data-stu-id="732fa-496">No</span></span>|<span data-ttu-id="732fa-497">新增</span><span class="sxs-lookup"><span data-stu-id="732fa-497">New</span></span>|  
|<span data-ttu-id="732fa-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="732fa-498">response-variable-name="string"</span></span>|<span data-ttu-id="732fa-499">如果不存在，則會使用 `context.Response`。</span><span class="sxs-lookup"><span data-stu-id="732fa-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="732fa-500">否</span><span class="sxs-lookup"><span data-stu-id="732fa-500">No</span></span>|<span data-ttu-id="732fa-501">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-501">N/A</span></span>|  
|<span data-ttu-id="732fa-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="732fa-502">timeout="integer"</span></span>|<span data-ttu-id="732fa-503">以秒為單位的逾時間隔，URL 的呼叫在經過此間隔後便會失敗。</span><span class="sxs-lookup"><span data-stu-id="732fa-503">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="732fa-504">否</span><span class="sxs-lookup"><span data-stu-id="732fa-504">No</span></span>|<span data-ttu-id="732fa-505">60</span><span class="sxs-lookup"><span data-stu-id="732fa-505">60</span></span>|  
|<span data-ttu-id="732fa-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="732fa-506">ignore-error</span></span>|<span data-ttu-id="732fa-507">如果為 true，則要求會導致錯誤︰</span><span class="sxs-lookup"><span data-stu-id="732fa-507">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="732fa-508">-   如果已指定 response-variable-name，它會包含 null 值。</span><span class="sxs-lookup"><span data-stu-id="732fa-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="732fa-509">-   如果未指定 response-variable-name，則不會更新 context.Request。</span><span class="sxs-lookup"><span data-stu-id="732fa-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="732fa-510">否</span><span class="sxs-lookup"><span data-stu-id="732fa-510">No</span></span>|<span data-ttu-id="732fa-511">false</span><span class="sxs-lookup"><span data-stu-id="732fa-511">false</span></span>|  
|<span data-ttu-id="732fa-512">名稱</span><span class="sxs-lookup"><span data-stu-id="732fa-512">name</span></span>|<span data-ttu-id="732fa-513">指定要設定之標頭的名稱。</span><span class="sxs-lookup"><span data-stu-id="732fa-513">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="732fa-514">是</span><span class="sxs-lookup"><span data-stu-id="732fa-514">Yes</span></span>|<span data-ttu-id="732fa-515">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-515">N/A</span></span>|  
|<span data-ttu-id="732fa-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="732fa-516">exists-action</span></span>|<span data-ttu-id="732fa-517">指定當已指定標頭時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="732fa-517">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="732fa-518">此屬性必須具有下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="732fa-518">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="732fa-519">-   override - 取代現有標頭的值。</span><span class="sxs-lookup"><span data-stu-id="732fa-519">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="732fa-520">-   skip - 不取代現有的標頭值。</span><span class="sxs-lookup"><span data-stu-id="732fa-520">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="732fa-521">-   append - 將值附加至現有標頭值之後。</span><span class="sxs-lookup"><span data-stu-id="732fa-521">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="732fa-522">-   delete - 移除要求中的標頭。</span><span class="sxs-lookup"><span data-stu-id="732fa-522">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="732fa-523">設為 `override` 時，編列多個相同名稱的項目會導致根據所有項目來設定標頭 (列出多次)；只有列出的值才會設定在結果中。</span><span class="sxs-lookup"><span data-stu-id="732fa-523">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="732fa-524">否</span><span class="sxs-lookup"><span data-stu-id="732fa-524">No</span></span>|<span data-ttu-id="732fa-525">override</span><span class="sxs-lookup"><span data-stu-id="732fa-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-526">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-526">Usage</span></span>  
 <span data-ttu-id="732fa-527">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-527">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-528">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-529">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="732fa-530"><a name="SetHttpProxy"></a> 設定 HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="732fa-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="732fa-531">`proxy` 原則可讓您透過 HTTP Proxy 將要求路由轉送至後端。</span><span class="sxs-lookup"><span data-stu-id="732fa-531">The `proxy` policy allows you to route requests forwarded to backends via an HTTP proxy.</span></span> <span data-ttu-id="732fa-532">在閘道與 Proxy 之間僅支援 HTTP (不是 HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="732fa-532">Only HTTP (not HTTPS) is supported between the gateway and the proxy.</span></span> <span data-ttu-id="732fa-533">僅限基本和 NTLM 驗證。</span><span class="sxs-lookup"><span data-stu-id="732fa-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-534">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="732fa-535">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-535">Example</span></span>  
<span data-ttu-id="732fa-536">請注意，其中使用[屬性](api-management-howto-properties.md)作為 username 和 password 的值，以避免將機密資訊儲存在原則文件中。</span><span class="sxs-lookup"><span data-stu-id="732fa-536">Note the use of [properties](api-management-howto-properties.md) as values of the username and password to avoid storing sensitive information in the policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="732fa-537">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-537">Elements</span></span>  
  
|<span data-ttu-id="732fa-538">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-538">Element</span></span>|<span data-ttu-id="732fa-539">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-539">Description</span></span>|<span data-ttu-id="732fa-540">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-541">proxy</span><span class="sxs-lookup"><span data-stu-id="732fa-541">proxy</span></span>|<span data-ttu-id="732fa-542">根元素</span><span class="sxs-lookup"><span data-stu-id="732fa-542">Root element</span></span>|<span data-ttu-id="732fa-543">是</span><span class="sxs-lookup"><span data-stu-id="732fa-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="732fa-544">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-544">Attributes</span></span>  
  
|<span data-ttu-id="732fa-545">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-545">Attribute</span></span>|<span data-ttu-id="732fa-546">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-546">Description</span></span>|<span data-ttu-id="732fa-547">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-547">Required</span></span>|<span data-ttu-id="732fa-548">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="732fa-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="732fa-549">url="string"</span></span>|<span data-ttu-id="732fa-550">http://host:port 形式的 Proxy URL。</span><span class="sxs-lookup"><span data-stu-id="732fa-550">Proxy URL in the form of http://host:port.</span></span>|<span data-ttu-id="732fa-551">是</span><span class="sxs-lookup"><span data-stu-id="732fa-551">Yes</span></span>|<span data-ttu-id="732fa-552">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-552">N/A</span></span>|  
|<span data-ttu-id="732fa-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="732fa-553">username="string"</span></span>|<span data-ttu-id="732fa-554">用於向 Proxy 驗證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="732fa-554">Username to be used for authentication with the proxy.</span></span>|<span data-ttu-id="732fa-555">否</span><span class="sxs-lookup"><span data-stu-id="732fa-555">No</span></span>|<span data-ttu-id="732fa-556">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-556">N/A</span></span>|  
|<span data-ttu-id="732fa-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="732fa-557">password="string"</span></span>|<span data-ttu-id="732fa-558">用於向 Proxy 驗證的密碼。</span><span class="sxs-lookup"><span data-stu-id="732fa-558">Password to be used for authentication with the proxy.</span></span>|<span data-ttu-id="732fa-559">否</span><span class="sxs-lookup"><span data-stu-id="732fa-559">No</span></span>|<span data-ttu-id="732fa-560">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="732fa-561">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-561">Usage</span></span>  
 <span data-ttu-id="732fa-562">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-562">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-563">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="732fa-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="732fa-564">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="732fa-565"><a name="SetRequestMethod"></a>設定要求方法</span><span class="sxs-lookup"><span data-stu-id="732fa-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="732fa-566">`set-method` 原則允許您變更要求的 HTTP 要求方法。</span><span class="sxs-lookup"><span data-stu-id="732fa-566">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-567">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="732fa-568">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-568">Example</span></span>  
 <span data-ttu-id="732fa-569">這個使用 `set-method` 原則的相同原則會舉例說明如何在 HTTP 回應碼大於或等於 500 時，將訊息傳送至 Slack 聊天室。</span><span class="sxs-lookup"><span data-stu-id="732fa-569">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="732fa-570">如需此範例的詳細資訊，請參閱[使用來自 Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)。</span><span class="sxs-lookup"><span data-stu-id="732fa-570">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="732fa-571">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-571">Elements</span></span>  
  
|<span data-ttu-id="732fa-572">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-572">Element</span></span>|<span data-ttu-id="732fa-573">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-573">Description</span></span>|<span data-ttu-id="732fa-574">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-575">set-method</span><span class="sxs-lookup"><span data-stu-id="732fa-575">set-method</span></span>|<span data-ttu-id="732fa-576">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-576">Root element.</span></span> <span data-ttu-id="732fa-577">元素的值會指定 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="732fa-577">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="732fa-578">是</span><span class="sxs-lookup"><span data-stu-id="732fa-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-579">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-579">Usage</span></span>  
 <span data-ttu-id="732fa-580">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-580">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-581">**原則區段︰**輸入、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="732fa-582">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="732fa-583"><a name="SetStatus"></a>設定狀態碼</span><span class="sxs-lookup"><span data-stu-id="732fa-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="732fa-584">`set-status` 原則會將 HTTP 狀態碼設為指定值。</span><span class="sxs-lookup"><span data-stu-id="732fa-584">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-585">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="732fa-586">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-586">Example</span></span>  
 <span data-ttu-id="732fa-587">此範例會說明如何在授權權杖無效時傳回 401 回應。</span><span class="sxs-lookup"><span data-stu-id="732fa-587">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="732fa-588">如需詳細資訊，請參閱[使用來自 Azure API 管理服務的外部服務](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="732fa-588">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="732fa-589">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-589">Elements</span></span>  
  
|<span data-ttu-id="732fa-590">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-590">Element</span></span>|<span data-ttu-id="732fa-591">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-591">Description</span></span>|<span data-ttu-id="732fa-592">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-593">set-status</span><span class="sxs-lookup"><span data-stu-id="732fa-593">set-status</span></span>|<span data-ttu-id="732fa-594">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-594">Root element.</span></span>|<span data-ttu-id="732fa-595">是</span><span class="sxs-lookup"><span data-stu-id="732fa-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-596">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-596">Attributes</span></span>  
  
|<span data-ttu-id="732fa-597">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-597">Attribute</span></span>|<span data-ttu-id="732fa-598">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-598">Description</span></span>|<span data-ttu-id="732fa-599">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-599">Required</span></span>|<span data-ttu-id="732fa-600">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="732fa-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="732fa-601">code="integer"</span></span>|<span data-ttu-id="732fa-602">要傳回的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="732fa-602">The HTTP status code to return.</span></span>|<span data-ttu-id="732fa-603">是</span><span class="sxs-lookup"><span data-stu-id="732fa-603">Yes</span></span>|<span data-ttu-id="732fa-604">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-604">N/A</span></span>|  
|<span data-ttu-id="732fa-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="732fa-605">reason="string"</span></span>|<span data-ttu-id="732fa-606">狀態碼傳回原因的描述。</span><span class="sxs-lookup"><span data-stu-id="732fa-606">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="732fa-607">是</span><span class="sxs-lookup"><span data-stu-id="732fa-607">Yes</span></span>|<span data-ttu-id="732fa-608">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-609">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-609">Usage</span></span>  
 <span data-ttu-id="732fa-610">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-610">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-611">**原則區段︰**輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-612">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="732fa-613"><a name="set-variable"></a>設定變數</span><span class="sxs-lookup"><span data-stu-id="732fa-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="732fa-614">`set-variable` 原則會宣告[內容](api-management-policy-expressions.md#ContextVariables)變數，並對其指派透過[運算式](api-management-policy-expressions.md)或字串常值指定的值。</span><span class="sxs-lookup"><span data-stu-id="732fa-614">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="732fa-615">包含常值的運算式會轉換成字串，且值的類型為 `System.String`。</span><span class="sxs-lookup"><span data-stu-id="732fa-615">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="732fa-616"><a name="set-variablePolicyStatement"></a>原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="732fa-617"><a name="set-variableExample"></a>範例</span><span class="sxs-lookup"><span data-stu-id="732fa-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="732fa-618">下列範例會示範 inbound 區段中的設定變數原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-618">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="732fa-619">此設定變數原則會在 `User-Agent` 要求標頭包含文字 `iPad` 或 `iPhone` 時，建立設為 true 的 `isMobile` 布林[內容](api-management-policy-expressions.md#ContextVariables)變數。</span><span class="sxs-lookup"><span data-stu-id="732fa-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="732fa-620">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-620">Elements</span></span>  
  
|<span data-ttu-id="732fa-621">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-621">Element</span></span>|<span data-ttu-id="732fa-622">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-622">Description</span></span>|<span data-ttu-id="732fa-623">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="732fa-624">set-variable</span></span>|<span data-ttu-id="732fa-625">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-625">Root element.</span></span>|<span data-ttu-id="732fa-626">是</span><span class="sxs-lookup"><span data-stu-id="732fa-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-627">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-627">Attributes</span></span>  
  
|<span data-ttu-id="732fa-628">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-628">Attribute</span></span>|<span data-ttu-id="732fa-629">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-629">Description</span></span>|<span data-ttu-id="732fa-630">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="732fa-631">名稱</span><span class="sxs-lookup"><span data-stu-id="732fa-631">name</span></span>|<span data-ttu-id="732fa-632">變數的名稱。</span><span class="sxs-lookup"><span data-stu-id="732fa-632">The name of the variable.</span></span>|<span data-ttu-id="732fa-633">是</span><span class="sxs-lookup"><span data-stu-id="732fa-633">Yes</span></span>|  
|<span data-ttu-id="732fa-634">value</span><span class="sxs-lookup"><span data-stu-id="732fa-634">value</span></span>|<span data-ttu-id="732fa-635">變數的值。</span><span class="sxs-lookup"><span data-stu-id="732fa-635">The value of the variable.</span></span> <span data-ttu-id="732fa-636">此值可為運算式或常值。</span><span class="sxs-lookup"><span data-stu-id="732fa-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="732fa-637">是</span><span class="sxs-lookup"><span data-stu-id="732fa-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-638">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-638">Usage</span></span>  
 <span data-ttu-id="732fa-639">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-639">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-640">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-641">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="732fa-642"><a name="set-variableAllowedTypes"></a>允許的類型</span><span class="sxs-lookup"><span data-stu-id="732fa-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="732fa-643">`set-variable` 原則中使用的運算式必須傳回下列其中一個基本類型。</span><span class="sxs-lookup"><span data-stu-id="732fa-643">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="732fa-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="732fa-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="732fa-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="732fa-645">System.SByte</span></span>  
  
-   <span data-ttu-id="732fa-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="732fa-646">System.Byte</span></span>  
  
-   <span data-ttu-id="732fa-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="732fa-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="732fa-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="732fa-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="732fa-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="732fa-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="732fa-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="732fa-650">System.Int16</span></span>  
  
-   <span data-ttu-id="732fa-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="732fa-651">System.Int32</span></span>  
  
-   <span data-ttu-id="732fa-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="732fa-652">System.Int64</span></span>  
  
-   <span data-ttu-id="732fa-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="732fa-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="732fa-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="732fa-654">System.Single</span></span>  
  
-   <span data-ttu-id="732fa-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="732fa-655">System.Double</span></span>  
  
-   <span data-ttu-id="732fa-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="732fa-656">System.Guid</span></span>  
  
-   <span data-ttu-id="732fa-657">System.String</span><span class="sxs-lookup"><span data-stu-id="732fa-657">System.String</span></span>  
  
-   <span data-ttu-id="732fa-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="732fa-658">System.Char</span></span>  
  
-   <span data-ttu-id="732fa-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="732fa-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="732fa-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="732fa-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="732fa-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="732fa-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="732fa-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="732fa-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="732fa-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="732fa-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="732fa-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="732fa-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="732fa-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="732fa-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="732fa-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="732fa-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="732fa-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="732fa-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="732fa-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="732fa-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="732fa-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="732fa-669">System.Single?</span></span>  
  
-   <span data-ttu-id="732fa-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="732fa-670">System.Double?</span></span>  
  
-   <span data-ttu-id="732fa-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="732fa-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="732fa-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="732fa-672">System.String?</span></span>  
  
-   <span data-ttu-id="732fa-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="732fa-673">System.Char?</span></span>  
  
-   <span data-ttu-id="732fa-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="732fa-674">System.DateTime?</span></span>  

##  <span data-ttu-id="732fa-675"><a name="Trace"></a>追蹤</span><span class="sxs-lookup"><span data-stu-id="732fa-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="732fa-676">`trace` 原則會將字串新增至 [API 檢查器](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/)輸出。</span><span class="sxs-lookup"><span data-stu-id="732fa-676">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="732fa-677">此原則只會在觸發追蹤時執行，也就是 `Ocp-Apim-Trace` 要求標頭存在且設為 `true` 以及 `Ocp-Apim-Subscription-Key` 要求標頭存在且含有與管理帳戶相關聯的有效金鑰時。</span><span class="sxs-lookup"><span data-stu-id="732fa-677">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-678">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="732fa-679">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-679">Elements</span></span>  
  
|<span data-ttu-id="732fa-680">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-680">Element</span></span>|<span data-ttu-id="732fa-681">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-681">Description</span></span>|<span data-ttu-id="732fa-682">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-683">trace</span><span class="sxs-lookup"><span data-stu-id="732fa-683">trace</span></span>|<span data-ttu-id="732fa-684">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-684">Root element.</span></span>|<span data-ttu-id="732fa-685">是</span><span class="sxs-lookup"><span data-stu-id="732fa-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-686">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-686">Attributes</span></span>  
  
|<span data-ttu-id="732fa-687">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-687">Attribute</span></span>|<span data-ttu-id="732fa-688">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-688">Description</span></span>|<span data-ttu-id="732fa-689">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-689">Required</span></span>|<span data-ttu-id="732fa-690">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="732fa-691">來源</span><span class="sxs-lookup"><span data-stu-id="732fa-691">source</span></span>|<span data-ttu-id="732fa-692">對追蹤檢視器有意義，並指定了訊息來源的字串常值。</span><span class="sxs-lookup"><span data-stu-id="732fa-692">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="732fa-693">是</span><span class="sxs-lookup"><span data-stu-id="732fa-693">Yes</span></span>|<span data-ttu-id="732fa-694">N/A</span><span class="sxs-lookup"><span data-stu-id="732fa-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-695">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-695">Usage</span></span>  
 <span data-ttu-id="732fa-696">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-696">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="732fa-697">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="732fa-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="732fa-698">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="732fa-699"><a name="Wait"></a>等候</span><span class="sxs-lookup"><span data-stu-id="732fa-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="732fa-700">`wait` 原則會以平行方式執行其直屬子原則，並等候其所有或其中一個直屬子原則完成後再完成。</span><span class="sxs-lookup"><span data-stu-id="732fa-700">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="732fa-701">等候原則可擁有做為其直屬子原則[傳送要求](api-management-advanced-policies.md#SendRequest)、[從快取取得值](api-management-caching-policies.md#GetFromCacheByKey)和[控制流程](api-management-advanced-policies.md#choose)原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-701">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="732fa-702">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="732fa-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="732fa-703">範例</span><span class="sxs-lookup"><span data-stu-id="732fa-703">Example</span></span>  
 <span data-ttu-id="732fa-704">在下列範例中，有兩個 `choose` 原則做為 `wait` 原則的直屬子原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-704">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="732fa-705">在這些 `choose` 原則中，每一個都會以平行方式執行。</span><span class="sxs-lookup"><span data-stu-id="732fa-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="732fa-706">每個 `choose` 原則都會嘗試擷取快取的值。</span><span class="sxs-lookup"><span data-stu-id="732fa-706">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="732fa-707">如果有快取遺漏，便會呼叫後端服務以提供值。</span><span class="sxs-lookup"><span data-stu-id="732fa-707">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="732fa-708">在此範例中，因為 `for` 屬性設為 `all`，所以要等到其所有直屬子原則完成後，`wait` 原則才會完成。</span><span class="sxs-lookup"><span data-stu-id="732fa-708">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="732fa-709">在此範例中，內容變數 (`execute-branch-one`、`value-one`、`execute-branch-two` 和 `value-two`) 會在此範例原則的範圍之外進行宣告。</span><span class="sxs-lookup"><span data-stu-id="732fa-709">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="732fa-710">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-710">Elements</span></span>  
  
|<span data-ttu-id="732fa-711">元素</span><span class="sxs-lookup"><span data-stu-id="732fa-711">Element</span></span>|<span data-ttu-id="732fa-712">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-712">Description</span></span>|<span data-ttu-id="732fa-713">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="732fa-714">wait</span><span class="sxs-lookup"><span data-stu-id="732fa-714">wait</span></span>|<span data-ttu-id="732fa-715">根元素。</span><span class="sxs-lookup"><span data-stu-id="732fa-715">Root element.</span></span> <span data-ttu-id="732fa-716">只能包含做為子元素 `send-request`、`cache-lookup-value` 和 `choose` 原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="732fa-717">是</span><span class="sxs-lookup"><span data-stu-id="732fa-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="732fa-718">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-718">Attributes</span></span>  
  
|<span data-ttu-id="732fa-719">屬性</span><span class="sxs-lookup"><span data-stu-id="732fa-719">Attribute</span></span>|<span data-ttu-id="732fa-720">說明</span><span class="sxs-lookup"><span data-stu-id="732fa-720">Description</span></span>|<span data-ttu-id="732fa-721">必要</span><span class="sxs-lookup"><span data-stu-id="732fa-721">Required</span></span>|<span data-ttu-id="732fa-722">預設值</span><span class="sxs-lookup"><span data-stu-id="732fa-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="732fa-723">for</span><span class="sxs-lookup"><span data-stu-id="732fa-723">for</span></span>|<span data-ttu-id="732fa-724">決定 `wait` 原則是要等候所有直屬子原則完成或只等候一個完成。</span><span class="sxs-lookup"><span data-stu-id="732fa-724">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="732fa-725">允許的值包括：</span><span class="sxs-lookup"><span data-stu-id="732fa-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="732fa-726">-   `all` - 等候所有直屬子原則完成</span><span class="sxs-lookup"><span data-stu-id="732fa-726">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="732fa-727">-   any - 等候任一直屬子原則完成。</span><span class="sxs-lookup"><span data-stu-id="732fa-727">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="732fa-728">第一個直屬子原則完成後，`wait` 原則便會完成，並終止執行任何其他直屬子原則。</span><span class="sxs-lookup"><span data-stu-id="732fa-728">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="732fa-729">否</span><span class="sxs-lookup"><span data-stu-id="732fa-729">No</span></span>|<span data-ttu-id="732fa-730">所有</span><span class="sxs-lookup"><span data-stu-id="732fa-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="732fa-731">使用量</span><span class="sxs-lookup"><span data-stu-id="732fa-731">Usage</span></span>  
 <span data-ttu-id="732fa-732">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="732fa-732">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="732fa-733">**原則區段︰**輸入、輸出、後端</span><span class="sxs-lookup"><span data-stu-id="732fa-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="732fa-734">**原則範圍：**所有範圍</span><span class="sxs-lookup"><span data-stu-id="732fa-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="732fa-735">後續步驟</span><span class="sxs-lookup"><span data-stu-id="732fa-735">Next steps</span></span>
<span data-ttu-id="732fa-736">如需使用原則的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="732fa-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="732fa-737">API 管理中的原則</span><span class="sxs-lookup"><span data-stu-id="732fa-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="732fa-738">原則運算式</span><span class="sxs-lookup"><span data-stu-id="732fa-738">Policy expressions</span></span>](api-management-policy-expressions.md)
