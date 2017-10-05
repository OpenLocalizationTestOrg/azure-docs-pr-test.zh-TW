---
title: "Azure API 管理快取原則 | Microsoft Docs"
description: "了解可在 Azure API 管理中使用的快取原則。"
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
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="68b54-103">API 管理快取原則</span><span class="sxs-lookup"><span data-stu-id="68b54-103">API Management caching policies</span></span>
<span data-ttu-id="68b54-104">本主題提供下列 API 管理原則的參考。</span><span class="sxs-lookup"><span data-stu-id="68b54-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="68b54-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="68b54-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="68b54-106"><a name="CachingPolicies"></a>快取原則</span><span class="sxs-lookup"><span data-stu-id="68b54-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="68b54-107">回應快取原則</span><span class="sxs-lookup"><span data-stu-id="68b54-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="68b54-108">[從快取中取得](api-management-caching-policies.md#GetFromCache) - 執行快取查閱並傳回有效的快取回應 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="68b54-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="68b54-109">[儲存至快取](api-management-caching-policies.md#StoreToCache) - 根據指定的快取控制組態來快取回應。</span><span class="sxs-lookup"><span data-stu-id="68b54-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="68b54-110">值快取原則</span><span class="sxs-lookup"><span data-stu-id="68b54-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="68b54-111">[從快取取得值](#GetFromCacheByKey) - 依金鑰擷取快取的項目。</span><span class="sxs-lookup"><span data-stu-id="68b54-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="68b54-112">[儲存快取中的值](#StoreToCacheByKey) -依金鑰儲存快取中的項目。</span><span class="sxs-lookup"><span data-stu-id="68b54-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="68b54-113">[移除快取中的值](#RemoveCacheByKey) - 依金鑰移除快取中的項目。</span><span class="sxs-lookup"><span data-stu-id="68b54-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="68b54-114"><a name="GetFromCache"></a>從快取中取得</span><span class="sxs-lookup"><span data-stu-id="68b54-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="68b54-115">使用 `cache-lookup` 原則來執行快取查閱並傳回有效的快取回應 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="68b54-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="68b54-116">此原則可於回應內容在一段期間維持靜態時套用。</span><span class="sxs-lookup"><span data-stu-id="68b54-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="68b54-117">回應快取可降低加諸於後端 Web 伺服器的頻寬和處理需求，並縮短 API 取用者所感受的延遲時間。</span><span class="sxs-lookup"><span data-stu-id="68b54-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="68b54-118">此原則必須有對應的[儲存至快取](api-management-caching-policies.md#StoreToCache)原則。</span><span class="sxs-lookup"><span data-stu-id="68b54-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="68b54-119">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="68b54-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="68b54-120">範例</span><span class="sxs-lookup"><span data-stu-id="68b54-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="68b54-121">範例</span><span class="sxs-lookup"><span data-stu-id="68b54-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="68b54-122">使用原則運算式的範例</span><span class="sxs-lookup"><span data-stu-id="68b54-122">Example using policy expressions</span></span>  
 <span data-ttu-id="68b54-123">此範例說明如何設定 API 管理回應快取持續時間，使其符合備用服務之 `Cache-Control` 指示詞所指定的後端服務回應快取。</span><span class="sxs-lookup"><span data-stu-id="68b54-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="68b54-124">如需設定和使用此原則的示範，請觀賞 [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)，快轉到 25:25。</span><span class="sxs-lookup"><span data-stu-id="68b54-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="68b54-125">如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="68b54-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="68b54-126">元素</span><span class="sxs-lookup"><span data-stu-id="68b54-126">Elements</span></span>  
  
|<span data-ttu-id="68b54-127">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-127">Name</span></span>|<span data-ttu-id="68b54-128">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-128">Description</span></span>|<span data-ttu-id="68b54-129">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="68b54-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="68b54-130">cache-lookup</span></span>|<span data-ttu-id="68b54-131">根元素。</span><span class="sxs-lookup"><span data-stu-id="68b54-131">Root element.</span></span>|<span data-ttu-id="68b54-132">是</span><span class="sxs-lookup"><span data-stu-id="68b54-132">Yes</span></span>|  
|<span data-ttu-id="68b54-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="68b54-133">vary-by-header</span></span>|<span data-ttu-id="68b54-134">根據指定標頭 (例如 Accept、Accept-Charset、Accept-Encoding、Accept-Language、Authorization、Expect、From、Host、If-Match) 的值開始快取回應。</span><span class="sxs-lookup"><span data-stu-id="68b54-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="68b54-135">否</span><span class="sxs-lookup"><span data-stu-id="68b54-135">No</span></span>|  
|<span data-ttu-id="68b54-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="68b54-136">vary-by-query-parameter</span></span>|<span data-ttu-id="68b54-137">根據指定查詢參數的值開始快取回應。</span><span class="sxs-lookup"><span data-stu-id="68b54-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="68b54-138">輸入單一或多個參數。</span><span class="sxs-lookup"><span data-stu-id="68b54-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="68b54-139">使用分號作為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="68b54-139">Use semicolon as a separator.</span></span> <span data-ttu-id="68b54-140">如果未指定任何參數，則會使用所有查詢參數。</span><span class="sxs-lookup"><span data-stu-id="68b54-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="68b54-141">否</span><span class="sxs-lookup"><span data-stu-id="68b54-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="68b54-142">屬性</span><span class="sxs-lookup"><span data-stu-id="68b54-142">Attributes</span></span>  
  
|<span data-ttu-id="68b54-143">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-143">Name</span></span>|<span data-ttu-id="68b54-144">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-144">Description</span></span>|<span data-ttu-id="68b54-145">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-145">Required</span></span>|<span data-ttu-id="68b54-146">預設值</span><span class="sxs-lookup"><span data-stu-id="68b54-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="68b54-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="68b54-147">allow-private-response-caching</span></span>|<span data-ttu-id="68b54-148">當設定為 `true` 時，可快取包含 Authorization 標頭的要求。</span><span class="sxs-lookup"><span data-stu-id="68b54-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="68b54-149">否</span><span class="sxs-lookup"><span data-stu-id="68b54-149">No</span></span>|<span data-ttu-id="68b54-150">false</span><span class="sxs-lookup"><span data-stu-id="68b54-150">false</span></span>|  
|<span data-ttu-id="68b54-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="68b54-151">downstream-caching-type</span></span>|<span data-ttu-id="68b54-152">此屬性必須設為下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="68b54-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="68b54-153">-   none - 不允許下游快取。</span><span class="sxs-lookup"><span data-stu-id="68b54-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="68b54-154">-   private - 允許下游私人快取。</span><span class="sxs-lookup"><span data-stu-id="68b54-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="68b54-155">-   public - 允許私人和共用下游快取。</span><span class="sxs-lookup"><span data-stu-id="68b54-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="68b54-156">否</span><span class="sxs-lookup"><span data-stu-id="68b54-156">No</span></span>|<span data-ttu-id="68b54-157">無</span><span class="sxs-lookup"><span data-stu-id="68b54-157">none</span></span>|  
|<span data-ttu-id="68b54-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="68b54-158">must-revalidate</span></span>|<span data-ttu-id="68b54-159">當下游快取啟用時，此屬性會開啟或關閉閘道回應中的 `must-revalidate` 快取控制指示詞。</span><span class="sxs-lookup"><span data-stu-id="68b54-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="68b54-160">否</span><span class="sxs-lookup"><span data-stu-id="68b54-160">No</span></span>|<span data-ttu-id="68b54-161">true</span><span class="sxs-lookup"><span data-stu-id="68b54-161">true</span></span>|  
|<span data-ttu-id="68b54-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="68b54-162">vary-by-developer</span></span>|<span data-ttu-id="68b54-163">設定為 `true` 可按照開發人員索引鍵來快取回應。</span><span class="sxs-lookup"><span data-stu-id="68b54-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="68b54-164">否</span><span class="sxs-lookup"><span data-stu-id="68b54-164">No</span></span>|<span data-ttu-id="68b54-165">false</span><span class="sxs-lookup"><span data-stu-id="68b54-165">false</span></span>|  
|<span data-ttu-id="68b54-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="68b54-166">vary-by-developer-groups</span></span>|<span data-ttu-id="68b54-167">設定為 `true` 可按照使用者角色來快取回應。</span><span class="sxs-lookup"><span data-stu-id="68b54-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="68b54-168">否</span><span class="sxs-lookup"><span data-stu-id="68b54-168">No</span></span>|<span data-ttu-id="68b54-169">false</span><span class="sxs-lookup"><span data-stu-id="68b54-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="68b54-170">使用量</span><span class="sxs-lookup"><span data-stu-id="68b54-170">Usage</span></span>  
 <span data-ttu-id="68b54-171">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="68b54-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="68b54-172">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="68b54-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="68b54-173">**原則範圍︰**API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="68b54-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="68b54-174"><a name="StoreToCache"></a>儲存至快取</span><span class="sxs-lookup"><span data-stu-id="68b54-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="68b54-175">`cache-store` 原則會根據指定的快取設定來快取回應。</span><span class="sxs-lookup"><span data-stu-id="68b54-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="68b54-176">此原則可於回應內容在一段期間維持靜態時套用。</span><span class="sxs-lookup"><span data-stu-id="68b54-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="68b54-177">回應快取可降低加諸於後端 Web 伺服器的頻寬和處理需求，並縮短 API 取用者所感受的延遲時間。</span><span class="sxs-lookup"><span data-stu-id="68b54-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="68b54-178">此原則必須有對應的[從快取中取得](api-management-caching-policies.md#GetFromCache)原則。</span><span class="sxs-lookup"><span data-stu-id="68b54-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="68b54-179">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="68b54-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="68b54-180">範例</span><span class="sxs-lookup"><span data-stu-id="68b54-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="68b54-181">範例</span><span class="sxs-lookup"><span data-stu-id="68b54-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="68b54-182">使用原則運算式的範例</span><span class="sxs-lookup"><span data-stu-id="68b54-182">Example using policy expressions</span></span>  
 <span data-ttu-id="68b54-183">此範例說明如何設定 API 管理回應快取持續時間，使其符合備用服務之 `Cache-Control` 指示詞所指定的後端服務回應快取。</span><span class="sxs-lookup"><span data-stu-id="68b54-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="68b54-184">如需設定和使用此原則的示範，請觀賞 [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)，快轉到 25:25。</span><span class="sxs-lookup"><span data-stu-id="68b54-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="68b54-185">如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="68b54-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="68b54-186">元素</span><span class="sxs-lookup"><span data-stu-id="68b54-186">Elements</span></span>  
  
|<span data-ttu-id="68b54-187">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-187">Name</span></span>|<span data-ttu-id="68b54-188">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-188">Description</span></span>|<span data-ttu-id="68b54-189">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="68b54-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="68b54-190">cache-store</span></span>|<span data-ttu-id="68b54-191">根元素。</span><span class="sxs-lookup"><span data-stu-id="68b54-191">Root element.</span></span>|<span data-ttu-id="68b54-192">是</span><span class="sxs-lookup"><span data-stu-id="68b54-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="68b54-193">屬性</span><span class="sxs-lookup"><span data-stu-id="68b54-193">Attributes</span></span>  
  
|<span data-ttu-id="68b54-194">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-194">Name</span></span>|<span data-ttu-id="68b54-195">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-195">Description</span></span>|<span data-ttu-id="68b54-196">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-196">Required</span></span>|<span data-ttu-id="68b54-197">預設值</span><span class="sxs-lookup"><span data-stu-id="68b54-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="68b54-198">duration</span><span class="sxs-lookup"><span data-stu-id="68b54-198">duration</span></span>|<span data-ttu-id="68b54-199">快取項目的存留時間，以秒為單位進行指定。</span><span class="sxs-lookup"><span data-stu-id="68b54-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="68b54-200">是</span><span class="sxs-lookup"><span data-stu-id="68b54-200">Yes</span></span>|<span data-ttu-id="68b54-201">N/A</span><span class="sxs-lookup"><span data-stu-id="68b54-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="68b54-202">使用量</span><span class="sxs-lookup"><span data-stu-id="68b54-202">Usage</span></span>  
 <span data-ttu-id="68b54-203">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="68b54-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="68b54-204">**原則區段︰**輸出</span><span class="sxs-lookup"><span data-stu-id="68b54-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="68b54-205">**原則範圍︰**API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="68b54-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="68b54-206"><a name="GetFromCacheByKey"></a>從快取取得值</span><span class="sxs-lookup"><span data-stu-id="68b54-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="68b54-207">使用 `cache-lookup-value` 原則以執行依索引鍵的快取查閱，並傳回快取的值。</span><span class="sxs-lookup"><span data-stu-id="68b54-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="68b54-208">金鑰可以具有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="68b54-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="68b54-209">此原則必須有對應的[儲存快取中的值](#StoreToCacheByKey)原則。</span><span class="sxs-lookup"><span data-stu-id="68b54-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="68b54-210">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="68b54-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="68b54-211">範例</span><span class="sxs-lookup"><span data-stu-id="68b54-211">Example</span></span>  
 <span data-ttu-id="68b54-212">如需此原則的詳細資訊和範例，請參閱[在 Azure API 管理中自訂快取](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)。</span><span class="sxs-lookup"><span data-stu-id="68b54-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="68b54-213">元素</span><span class="sxs-lookup"><span data-stu-id="68b54-213">Elements</span></span>  
  
|<span data-ttu-id="68b54-214">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-214">Name</span></span>|<span data-ttu-id="68b54-215">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-215">Description</span></span>|<span data-ttu-id="68b54-216">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="68b54-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="68b54-217">cache-lookup-value</span></span>|<span data-ttu-id="68b54-218">根元素。</span><span class="sxs-lookup"><span data-stu-id="68b54-218">Root element.</span></span>|<span data-ttu-id="68b54-219">是</span><span class="sxs-lookup"><span data-stu-id="68b54-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="68b54-220">屬性</span><span class="sxs-lookup"><span data-stu-id="68b54-220">Attributes</span></span>  
  
|<span data-ttu-id="68b54-221">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-221">Name</span></span>|<span data-ttu-id="68b54-222">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-222">Description</span></span>|<span data-ttu-id="68b54-223">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-223">Required</span></span>|<span data-ttu-id="68b54-224">預設值</span><span class="sxs-lookup"><span data-stu-id="68b54-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="68b54-225">default-value</span><span class="sxs-lookup"><span data-stu-id="68b54-225">default-value</span></span>|<span data-ttu-id="68b54-226">當快取索引鍵查閱沒有結果時，要指派給變數的值。</span><span class="sxs-lookup"><span data-stu-id="68b54-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="68b54-227">如果未指定此屬性，則會指派 `null`。</span><span class="sxs-lookup"><span data-stu-id="68b54-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="68b54-228">否</span><span class="sxs-lookup"><span data-stu-id="68b54-228">No</span></span>|`null`|  
|<span data-ttu-id="68b54-229">索引鍵</span><span class="sxs-lookup"><span data-stu-id="68b54-229">key</span></span>|<span data-ttu-id="68b54-230">要在查閱中使用的快取索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="68b54-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="68b54-231">是</span><span class="sxs-lookup"><span data-stu-id="68b54-231">Yes</span></span>|<span data-ttu-id="68b54-232">N/A</span><span class="sxs-lookup"><span data-stu-id="68b54-232">N/A</span></span>|  
|<span data-ttu-id="68b54-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="68b54-233">variable-name</span></span>|<span data-ttu-id="68b54-234">查閱成功時，要將查閱到的值指派到之[內容變數](api-management-policy-expressions.md#ContextVariables)的名稱。</span><span class="sxs-lookup"><span data-stu-id="68b54-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="68b54-235">如果查閱沒有結果，會對變數指派 `default-value` 屬性的值，如果省略 `default-value` 屬性，則會指派 `null`。</span><span class="sxs-lookup"><span data-stu-id="68b54-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="68b54-236">是</span><span class="sxs-lookup"><span data-stu-id="68b54-236">Yes</span></span>|<span data-ttu-id="68b54-237">N/A</span><span class="sxs-lookup"><span data-stu-id="68b54-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="68b54-238">使用量</span><span class="sxs-lookup"><span data-stu-id="68b54-238">Usage</span></span>  
 <span data-ttu-id="68b54-239">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="68b54-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="68b54-240">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="68b54-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="68b54-241">**原則範圍︰**全域、API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="68b54-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="68b54-242"><a name="StoreToCacheByKey"></a>儲存快取中的值</span><span class="sxs-lookup"><span data-stu-id="68b54-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="68b54-243">`cache-store-value` 會依索引鍵執行快取儲存。</span><span class="sxs-lookup"><span data-stu-id="68b54-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="68b54-244">金鑰可以具有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="68b54-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="68b54-245">此原則必須有對應的[從快取取得值](#GetFromCacheByKey)原則。</span><span class="sxs-lookup"><span data-stu-id="68b54-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="68b54-246">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="68b54-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="68b54-247">範例</span><span class="sxs-lookup"><span data-stu-id="68b54-247">Example</span></span>  
 <span data-ttu-id="68b54-248">如需此原則的詳細資訊和範例，請參閱[在 Azure API 管理中自訂快取](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)。</span><span class="sxs-lookup"><span data-stu-id="68b54-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="68b54-249">元素</span><span class="sxs-lookup"><span data-stu-id="68b54-249">Elements</span></span>  
  
|<span data-ttu-id="68b54-250">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-250">Name</span></span>|<span data-ttu-id="68b54-251">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-251">Description</span></span>|<span data-ttu-id="68b54-252">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="68b54-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="68b54-253">cache-store-value</span></span>|<span data-ttu-id="68b54-254">根元素。</span><span class="sxs-lookup"><span data-stu-id="68b54-254">Root element.</span></span>|<span data-ttu-id="68b54-255">是</span><span class="sxs-lookup"><span data-stu-id="68b54-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="68b54-256">屬性</span><span class="sxs-lookup"><span data-stu-id="68b54-256">Attributes</span></span>  
  
|<span data-ttu-id="68b54-257">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-257">Name</span></span>|<span data-ttu-id="68b54-258">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-258">Description</span></span>|<span data-ttu-id="68b54-259">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-259">Required</span></span>|<span data-ttu-id="68b54-260">預設值</span><span class="sxs-lookup"><span data-stu-id="68b54-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="68b54-261">duration</span><span class="sxs-lookup"><span data-stu-id="68b54-261">duration</span></span>|<span data-ttu-id="68b54-262">會針對所提供的持續時間值來快取值，以秒為單位進行指定。</span><span class="sxs-lookup"><span data-stu-id="68b54-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="68b54-263">是</span><span class="sxs-lookup"><span data-stu-id="68b54-263">Yes</span></span>|<span data-ttu-id="68b54-264">N/A</span><span class="sxs-lookup"><span data-stu-id="68b54-264">N/A</span></span>|  
|<span data-ttu-id="68b54-265">索引鍵</span><span class="sxs-lookup"><span data-stu-id="68b54-265">key</span></span>|<span data-ttu-id="68b54-266">用來做為值儲存依據的快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="68b54-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="68b54-267">是</span><span class="sxs-lookup"><span data-stu-id="68b54-267">Yes</span></span>|<span data-ttu-id="68b54-268">N/A</span><span class="sxs-lookup"><span data-stu-id="68b54-268">N/A</span></span>|  
|<span data-ttu-id="68b54-269">value</span><span class="sxs-lookup"><span data-stu-id="68b54-269">value</span></span>|<span data-ttu-id="68b54-270">要快取的值。</span><span class="sxs-lookup"><span data-stu-id="68b54-270">The value to be cached.</span></span>|<span data-ttu-id="68b54-271">是</span><span class="sxs-lookup"><span data-stu-id="68b54-271">Yes</span></span>|<span data-ttu-id="68b54-272">N/A</span><span class="sxs-lookup"><span data-stu-id="68b54-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="68b54-273">使用量</span><span class="sxs-lookup"><span data-stu-id="68b54-273">Usage</span></span>  
 <span data-ttu-id="68b54-274">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="68b54-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="68b54-275">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="68b54-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="68b54-276">**原則範圍︰**全域、API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="68b54-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="68b54-277"><a name="RemoveCacheByKey"></a>移除快取中的值</span><span class="sxs-lookup"><span data-stu-id="68b54-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="68b54-278">`cache-remove-value` 會刪除依其索引鍵所識別的快取項目。</span><span class="sxs-lookup"><span data-stu-id="68b54-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="68b54-279">金鑰可以具有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="68b54-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="68b54-280">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="68b54-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="68b54-281">範例</span><span class="sxs-lookup"><span data-stu-id="68b54-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="68b54-282">元素</span><span class="sxs-lookup"><span data-stu-id="68b54-282">Elements</span></span>  
  
|<span data-ttu-id="68b54-283">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-283">Name</span></span>|<span data-ttu-id="68b54-284">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-284">Description</span></span>|<span data-ttu-id="68b54-285">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="68b54-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="68b54-286">cache-remove-value</span></span>|<span data-ttu-id="68b54-287">根元素。</span><span class="sxs-lookup"><span data-stu-id="68b54-287">Root element.</span></span>|<span data-ttu-id="68b54-288">是</span><span class="sxs-lookup"><span data-stu-id="68b54-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="68b54-289">屬性</span><span class="sxs-lookup"><span data-stu-id="68b54-289">Attributes</span></span>  
  
|<span data-ttu-id="68b54-290">名稱</span><span class="sxs-lookup"><span data-stu-id="68b54-290">Name</span></span>|<span data-ttu-id="68b54-291">說明</span><span class="sxs-lookup"><span data-stu-id="68b54-291">Description</span></span>|<span data-ttu-id="68b54-292">必要</span><span class="sxs-lookup"><span data-stu-id="68b54-292">Required</span></span>|<span data-ttu-id="68b54-293">預設值</span><span class="sxs-lookup"><span data-stu-id="68b54-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="68b54-294">索引鍵</span><span class="sxs-lookup"><span data-stu-id="68b54-294">key</span></span>|<span data-ttu-id="68b54-295">要從快取中移除之先前快取值的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="68b54-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="68b54-296">是</span><span class="sxs-lookup"><span data-stu-id="68b54-296">Yes</span></span>|<span data-ttu-id="68b54-297">N/A</span><span class="sxs-lookup"><span data-stu-id="68b54-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="68b54-298">使用量</span><span class="sxs-lookup"><span data-stu-id="68b54-298">Usage</span></span>  
 <span data-ttu-id="68b54-299">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="68b54-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="68b54-300">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="68b54-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="68b54-301">**原則範圍︰**全域、API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="68b54-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="68b54-302">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68b54-302">Next steps</span></span>
<span data-ttu-id="68b54-303">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="68b54-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  