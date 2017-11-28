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
# <a name="api-management-caching-policies"></a><span data-ttu-id="37c1f-103">API 管理快取原則</span><span class="sxs-lookup"><span data-stu-id="37c1f-103">API Management caching policies</span></span>
<span data-ttu-id="37c1f-104">本主題提供下列 API 管理原則的 hello 的參考。</span><span class="sxs-lookup"><span data-stu-id="37c1f-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="37c1f-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="37c1f-106"><a name="CachingPolicies"></a>快取原則</span><span class="sxs-lookup"><span data-stu-id="37c1f-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="37c1f-107">回應快取原則</span><span class="sxs-lookup"><span data-stu-id="37c1f-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="37c1f-108">[從快取中取得](api-management-caching-policies.md#GetFromCache) - 執行快取查閱並傳回有效的快取回應 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="37c1f-109">[儲存 toocache](api-management-caching-policies.md#StoreToCache) -根據 toohello 指定快取控制組態快取回應。</span><span class="sxs-lookup"><span data-stu-id="37c1f-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="37c1f-110">值快取原則</span><span class="sxs-lookup"><span data-stu-id="37c1f-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="37c1f-111">[從快取取得值](#GetFromCacheByKey) - 依金鑰擷取快取的項目。</span><span class="sxs-lookup"><span data-stu-id="37c1f-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="37c1f-112">[將值儲存在快取](#StoreToCacheByKey)-hello 快取中儲存的項目，依索引鍵。</span><span class="sxs-lookup"><span data-stu-id="37c1f-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="37c1f-113">[從快取中移除值](#RemoveCacheByKey)-hello 快取中移除項目，依索引鍵。</span><span class="sxs-lookup"><span data-stu-id="37c1f-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="37c1f-114"><a name="GetFromCache"></a>從快取中取得</span><span class="sxs-lookup"><span data-stu-id="37c1f-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="37c1f-115">使用 hello`cache-lookup`原則 tooperform 快取查閱，並傳回有效的快取回的應的話。</span><span class="sxs-lookup"><span data-stu-id="37c1f-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="37c1f-116">此原則可於回應內容在一段期間維持靜態時套用。</span><span class="sxs-lookup"><span data-stu-id="37c1f-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="37c1f-117">回應快取可減少頻寬和處理需求加諸於 hello 後端 web 伺服器，並降低延遲 API 取用者看得見。</span><span class="sxs-lookup"><span data-stu-id="37c1f-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="37c1f-118">此原則必須有對應[存放區 toocache](api-management-caching-policies.md#StoreToCache)原則。</span><span class="sxs-lookup"><span data-stu-id="37c1f-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="37c1f-119">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="37c1f-119">Policy statement</span></span>  
  
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
  
### <a name="examples"></a><span data-ttu-id="37c1f-120">範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="37c1f-121">範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="37c1f-122">使用原則運算式的範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-122">Example using policy expressions</span></span>  
 <span data-ttu-id="37c1f-123">這個範例會示範如何 tootooconfigure API 管理回應快取持續時間比對 hello 回應 hello hello 所指定的後端服務快取備份服務的`Cache-Control`指示詞。</span><span class="sxs-lookup"><span data-stu-id="37c1f-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="37c1f-124">如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too25:25 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="37c1f-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
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
  
 <span data-ttu-id="37c1f-125">如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="37c1f-126">元素</span><span class="sxs-lookup"><span data-stu-id="37c1f-126">Elements</span></span>  
  
|<span data-ttu-id="37c1f-127">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-127">Name</span></span>|<span data-ttu-id="37c1f-128">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-128">Description</span></span>|<span data-ttu-id="37c1f-129">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="37c1f-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="37c1f-130">cache-lookup</span></span>|<span data-ttu-id="37c1f-131">根元素。</span><span class="sxs-lookup"><span data-stu-id="37c1f-131">Root element.</span></span>|<span data-ttu-id="37c1f-132">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-132">Yes</span></span>|  
|<span data-ttu-id="37c1f-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="37c1f-133">vary-by-header</span></span>|<span data-ttu-id="37c1f-134">根據指定標頭 (例如 Accept、Accept-Charset、Accept-Encoding、Accept-Language、Authorization、Expect、From、Host、If-Match) 的值開始快取回應。</span><span class="sxs-lookup"><span data-stu-id="37c1f-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="37c1f-135">否</span><span class="sxs-lookup"><span data-stu-id="37c1f-135">No</span></span>|  
|<span data-ttu-id="37c1f-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="37c1f-136">vary-by-query-parameter</span></span>|<span data-ttu-id="37c1f-137">根據指定查詢參數的值開始快取回應。</span><span class="sxs-lookup"><span data-stu-id="37c1f-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="37c1f-138">輸入單一或多個參數。</span><span class="sxs-lookup"><span data-stu-id="37c1f-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="37c1f-139">使用分號作為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="37c1f-139">Use semicolon as a separator.</span></span> <span data-ttu-id="37c1f-140">如果未指定任何參數，則會使用所有查詢參數。</span><span class="sxs-lookup"><span data-stu-id="37c1f-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="37c1f-141">否</span><span class="sxs-lookup"><span data-stu-id="37c1f-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="37c1f-142">屬性</span><span class="sxs-lookup"><span data-stu-id="37c1f-142">Attributes</span></span>  
  
|<span data-ttu-id="37c1f-143">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-143">Name</span></span>|<span data-ttu-id="37c1f-144">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-144">Description</span></span>|<span data-ttu-id="37c1f-145">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-145">Required</span></span>|<span data-ttu-id="37c1f-146">預設值</span><span class="sxs-lookup"><span data-stu-id="37c1f-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="37c1f-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="37c1f-147">allow-private-response-caching</span></span>|<span data-ttu-id="37c1f-148">當設定太`true`，好讓快取的要求包含授權標頭。</span><span class="sxs-lookup"><span data-stu-id="37c1f-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="37c1f-149">否</span><span class="sxs-lookup"><span data-stu-id="37c1f-149">No</span></span>|<span data-ttu-id="37c1f-150">false</span><span class="sxs-lookup"><span data-stu-id="37c1f-150">false</span></span>|  
|<span data-ttu-id="37c1f-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="37c1f-151">downstream-caching-type</span></span>|<span data-ttu-id="37c1f-152">這個屬性必須設定下列值的 hello 的 tooone。</span><span class="sxs-lookup"><span data-stu-id="37c1f-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="37c1f-153">-   none - 不允許下游快取。</span><span class="sxs-lookup"><span data-stu-id="37c1f-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="37c1f-154">-   private - 允許下游私人快取。</span><span class="sxs-lookup"><span data-stu-id="37c1f-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="37c1f-155">-   public - 允許私人和共用下游快取。</span><span class="sxs-lookup"><span data-stu-id="37c1f-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="37c1f-156">否</span><span class="sxs-lookup"><span data-stu-id="37c1f-156">No</span></span>|<span data-ttu-id="37c1f-157">無</span><span class="sxs-lookup"><span data-stu-id="37c1f-157">none</span></span>|  
|<span data-ttu-id="37c1f-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="37c1f-158">must-revalidate</span></span>|<span data-ttu-id="37c1f-159">這個屬性下游快取啟用時開啟或關閉 hello`must-revalidate`閘道回應中的快取控制指示詞。</span><span class="sxs-lookup"><span data-stu-id="37c1f-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="37c1f-160">否</span><span class="sxs-lookup"><span data-stu-id="37c1f-160">No</span></span>|<span data-ttu-id="37c1f-161">true</span><span class="sxs-lookup"><span data-stu-id="37c1f-161">true</span></span>|  
|<span data-ttu-id="37c1f-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="37c1f-162">vary-by-developer</span></span>|<span data-ttu-id="37c1f-163">設定得`true`toocache 回應每個開發人員索引鍵。</span><span class="sxs-lookup"><span data-stu-id="37c1f-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="37c1f-164">否</span><span class="sxs-lookup"><span data-stu-id="37c1f-164">No</span></span>|<span data-ttu-id="37c1f-165">false</span><span class="sxs-lookup"><span data-stu-id="37c1f-165">false</span></span>|  
|<span data-ttu-id="37c1f-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="37c1f-166">vary-by-developer-groups</span></span>|<span data-ttu-id="37c1f-167">設定得`true`toocache 回應每個使用者角色。</span><span class="sxs-lookup"><span data-stu-id="37c1f-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="37c1f-168">否</span><span class="sxs-lookup"><span data-stu-id="37c1f-168">No</span></span>|<span data-ttu-id="37c1f-169">false</span><span class="sxs-lookup"><span data-stu-id="37c1f-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="37c1f-170">使用量</span><span class="sxs-lookup"><span data-stu-id="37c1f-170">Usage</span></span>  
 <span data-ttu-id="37c1f-171">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="37c1f-172">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="37c1f-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="37c1f-173">**原則範圍︰**API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="37c1f-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="37c1f-174"><a name="StoreToCache"></a>存放區 toocache</span><span class="sxs-lookup"><span data-stu-id="37c1f-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="37c1f-175">hello`cache-store`根據 toohello 原則快取的回應指定快取設定。</span><span class="sxs-lookup"><span data-stu-id="37c1f-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="37c1f-176">此原則可於回應內容在一段期間維持靜態時套用。</span><span class="sxs-lookup"><span data-stu-id="37c1f-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="37c1f-177">回應快取可減少頻寬和處理需求加諸於 hello 後端 web 伺服器，並降低延遲 API 取用者看得見。</span><span class="sxs-lookup"><span data-stu-id="37c1f-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="37c1f-178">此原則必須有對應的[從快取中取得](api-management-caching-policies.md#GetFromCache)原則。</span><span class="sxs-lookup"><span data-stu-id="37c1f-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="37c1f-179">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="37c1f-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="37c1f-180">範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="37c1f-181">範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="37c1f-182">使用原則運算式的範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-182">Example using policy expressions</span></span>  
 <span data-ttu-id="37c1f-183">這個範例會示範如何 tootooconfigure API 管理回應快取持續時間比對 hello 回應 hello hello 所指定的後端服務快取備份服務的`Cache-Control`指示詞。</span><span class="sxs-lookup"><span data-stu-id="37c1f-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="37c1f-184">如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too25:25 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="37c1f-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
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
  
 <span data-ttu-id="37c1f-185">如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="37c1f-186">元素</span><span class="sxs-lookup"><span data-stu-id="37c1f-186">Elements</span></span>  
  
|<span data-ttu-id="37c1f-187">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-187">Name</span></span>|<span data-ttu-id="37c1f-188">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-188">Description</span></span>|<span data-ttu-id="37c1f-189">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="37c1f-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="37c1f-190">cache-store</span></span>|<span data-ttu-id="37c1f-191">根元素。</span><span class="sxs-lookup"><span data-stu-id="37c1f-191">Root element.</span></span>|<span data-ttu-id="37c1f-192">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="37c1f-193">屬性</span><span class="sxs-lookup"><span data-stu-id="37c1f-193">Attributes</span></span>  
  
|<span data-ttu-id="37c1f-194">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-194">Name</span></span>|<span data-ttu-id="37c1f-195">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-195">Description</span></span>|<span data-ttu-id="37c1f-196">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-196">Required</span></span>|<span data-ttu-id="37c1f-197">預設值</span><span class="sxs-lookup"><span data-stu-id="37c1f-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="37c1f-198">duration</span><span class="sxs-lookup"><span data-stu-id="37c1f-198">duration</span></span>|<span data-ttu-id="37c1f-199">存留時間的 hello 快取項目，以秒為單位指定。</span><span class="sxs-lookup"><span data-stu-id="37c1f-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="37c1f-200">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-200">Yes</span></span>|<span data-ttu-id="37c1f-201">N/A</span><span class="sxs-lookup"><span data-stu-id="37c1f-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="37c1f-202">使用量</span><span class="sxs-lookup"><span data-stu-id="37c1f-202">Usage</span></span>  
 <span data-ttu-id="37c1f-203">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="37c1f-204">**原則區段︰**輸出</span><span class="sxs-lookup"><span data-stu-id="37c1f-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="37c1f-205">**原則範圍︰**API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="37c1f-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="37c1f-206"><a name="GetFromCacheByKey"></a>從快取取得值</span><span class="sxs-lookup"><span data-stu-id="37c1f-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="37c1f-207">使用 hello`cache-lookup-value`原則 tooperform 查閱快取索引鍵，並傳回快取的值。</span><span class="sxs-lookup"><span data-stu-id="37c1f-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="37c1f-208">hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="37c1f-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="37c1f-209">此原則必須有對應的[儲存快取中的值](#StoreToCacheByKey)原則。</span><span class="sxs-lookup"><span data-stu-id="37c1f-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="37c1f-210">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="37c1f-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="37c1f-211">範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-211">Example</span></span>  
 <span data-ttu-id="37c1f-212">如需此原則的詳細資訊和範例，請參閱[在 Azure API 管理中自訂快取](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="37c1f-213">元素</span><span class="sxs-lookup"><span data-stu-id="37c1f-213">Elements</span></span>  
  
|<span data-ttu-id="37c1f-214">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-214">Name</span></span>|<span data-ttu-id="37c1f-215">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-215">Description</span></span>|<span data-ttu-id="37c1f-216">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="37c1f-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="37c1f-217">cache-lookup-value</span></span>|<span data-ttu-id="37c1f-218">根元素。</span><span class="sxs-lookup"><span data-stu-id="37c1f-218">Root element.</span></span>|<span data-ttu-id="37c1f-219">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="37c1f-220">屬性</span><span class="sxs-lookup"><span data-stu-id="37c1f-220">Attributes</span></span>  
  
|<span data-ttu-id="37c1f-221">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-221">Name</span></span>|<span data-ttu-id="37c1f-222">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-222">Description</span></span>|<span data-ttu-id="37c1f-223">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-223">Required</span></span>|<span data-ttu-id="37c1f-224">預設值</span><span class="sxs-lookup"><span data-stu-id="37c1f-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="37c1f-225">default-value</span><span class="sxs-lookup"><span data-stu-id="37c1f-225">default-value</span></span>|<span data-ttu-id="37c1f-226">將會指派 toohello 變數，如果 hello 快取索引鍵查閱產生遺漏值。</span><span class="sxs-lookup"><span data-stu-id="37c1f-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="37c1f-227">如果未指定此屬性，則會指派 `null`。</span><span class="sxs-lookup"><span data-stu-id="37c1f-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="37c1f-228">否</span><span class="sxs-lookup"><span data-stu-id="37c1f-228">No</span></span>|`null`|  
|<span data-ttu-id="37c1f-229">key</span><span class="sxs-lookup"><span data-stu-id="37c1f-229">key</span></span>|<span data-ttu-id="37c1f-230">快取索引鍵值 toouse hello 查閱中。</span><span class="sxs-lookup"><span data-stu-id="37c1f-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="37c1f-231">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-231">Yes</span></span>|<span data-ttu-id="37c1f-232">N/A</span><span class="sxs-lookup"><span data-stu-id="37c1f-232">N/A</span></span>|  
|<span data-ttu-id="37c1f-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="37c1f-233">variable-name</span></span>|<span data-ttu-id="37c1f-234">名稱的 hello[內容變數](api-management-policy-expressions.md#ContextVariables)hello 查閱值會指派給，如果查閱成功。</span><span class="sxs-lookup"><span data-stu-id="37c1f-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="37c1f-235">如果查詢結果中遺漏，hello 變數將值指派給 hello hello`default-value`屬性或`null`，如果 hello`default-value`省略屬性。</span><span class="sxs-lookup"><span data-stu-id="37c1f-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="37c1f-236">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-236">Yes</span></span>|<span data-ttu-id="37c1f-237">N/A</span><span class="sxs-lookup"><span data-stu-id="37c1f-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="37c1f-238">使用量</span><span class="sxs-lookup"><span data-stu-id="37c1f-238">Usage</span></span>  
 <span data-ttu-id="37c1f-239">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="37c1f-240">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="37c1f-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="37c1f-241">**原則範圍︰**全域、API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="37c1f-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="37c1f-242"><a name="StoreToCacheByKey"></a>儲存快取中的值</span><span class="sxs-lookup"><span data-stu-id="37c1f-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="37c1f-243">hello`cache-store-value`執行快取存放區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="37c1f-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="37c1f-244">hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="37c1f-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="37c1f-245">此原則必須有對應的[從快取取得值](#GetFromCacheByKey)原則。</span><span class="sxs-lookup"><span data-stu-id="37c1f-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="37c1f-246">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="37c1f-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="37c1f-247">範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-247">Example</span></span>  
 <span data-ttu-id="37c1f-248">如需此原則的詳細資訊和範例，請參閱[在 Azure API 管理中自訂快取](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="37c1f-249">元素</span><span class="sxs-lookup"><span data-stu-id="37c1f-249">Elements</span></span>  
  
|<span data-ttu-id="37c1f-250">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-250">Name</span></span>|<span data-ttu-id="37c1f-251">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-251">Description</span></span>|<span data-ttu-id="37c1f-252">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="37c1f-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="37c1f-253">cache-store-value</span></span>|<span data-ttu-id="37c1f-254">根元素。</span><span class="sxs-lookup"><span data-stu-id="37c1f-254">Root element.</span></span>|<span data-ttu-id="37c1f-255">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="37c1f-256">屬性</span><span class="sxs-lookup"><span data-stu-id="37c1f-256">Attributes</span></span>  
  
|<span data-ttu-id="37c1f-257">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-257">Name</span></span>|<span data-ttu-id="37c1f-258">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-258">Description</span></span>|<span data-ttu-id="37c1f-259">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-259">Required</span></span>|<span data-ttu-id="37c1f-260">預設值</span><span class="sxs-lookup"><span data-stu-id="37c1f-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="37c1f-261">duration</span><span class="sxs-lookup"><span data-stu-id="37c1f-261">duration</span></span>|<span data-ttu-id="37c1f-262">將快取 hello 提供持續時間值，指定以秒為單位的值。</span><span class="sxs-lookup"><span data-stu-id="37c1f-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="37c1f-263">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-263">Yes</span></span>|<span data-ttu-id="37c1f-264">N/A</span><span class="sxs-lookup"><span data-stu-id="37c1f-264">N/A</span></span>|  
|<span data-ttu-id="37c1f-265">key</span><span class="sxs-lookup"><span data-stu-id="37c1f-265">key</span></span>|<span data-ttu-id="37c1f-266">快取索引鍵的 hello 值將會儲存在下。</span><span class="sxs-lookup"><span data-stu-id="37c1f-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="37c1f-267">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-267">Yes</span></span>|<span data-ttu-id="37c1f-268">N/A</span><span class="sxs-lookup"><span data-stu-id="37c1f-268">N/A</span></span>|  
|<span data-ttu-id="37c1f-269">value</span><span class="sxs-lookup"><span data-stu-id="37c1f-269">value</span></span>|<span data-ttu-id="37c1f-270">hello 值 toobe 快取。</span><span class="sxs-lookup"><span data-stu-id="37c1f-270">hello value toobe cached.</span></span>|<span data-ttu-id="37c1f-271">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-271">Yes</span></span>|<span data-ttu-id="37c1f-272">N/A</span><span class="sxs-lookup"><span data-stu-id="37c1f-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="37c1f-273">使用量</span><span class="sxs-lookup"><span data-stu-id="37c1f-273">Usage</span></span>  
 <span data-ttu-id="37c1f-274">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="37c1f-275">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="37c1f-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="37c1f-276">**原則範圍︰**全域、API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="37c1f-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="37c1f-277"><a name="RemoveCacheByKey"></a>移除快取中的值</span><span class="sxs-lookup"><span data-stu-id="37c1f-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="37c1f-278">hello`cache-remove-value`刪除快取項目由其索引鍵識別。</span><span class="sxs-lookup"><span data-stu-id="37c1f-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="37c1f-279">hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="37c1f-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="37c1f-280">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="37c1f-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="37c1f-281">範例</span><span class="sxs-lookup"><span data-stu-id="37c1f-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="37c1f-282">元素</span><span class="sxs-lookup"><span data-stu-id="37c1f-282">Elements</span></span>  
  
|<span data-ttu-id="37c1f-283">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-283">Name</span></span>|<span data-ttu-id="37c1f-284">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-284">Description</span></span>|<span data-ttu-id="37c1f-285">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="37c1f-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="37c1f-286">cache-remove-value</span></span>|<span data-ttu-id="37c1f-287">根元素。</span><span class="sxs-lookup"><span data-stu-id="37c1f-287">Root element.</span></span>|<span data-ttu-id="37c1f-288">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="37c1f-289">屬性</span><span class="sxs-lookup"><span data-stu-id="37c1f-289">Attributes</span></span>  
  
|<span data-ttu-id="37c1f-290">名稱</span><span class="sxs-lookup"><span data-stu-id="37c1f-290">Name</span></span>|<span data-ttu-id="37c1f-291">說明</span><span class="sxs-lookup"><span data-stu-id="37c1f-291">Description</span></span>|<span data-ttu-id="37c1f-292">必要</span><span class="sxs-lookup"><span data-stu-id="37c1f-292">Required</span></span>|<span data-ttu-id="37c1f-293">預設值</span><span class="sxs-lookup"><span data-stu-id="37c1f-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="37c1f-294">key</span><span class="sxs-lookup"><span data-stu-id="37c1f-294">key</span></span>|<span data-ttu-id="37c1f-295">hello 索引鍵的 hello 先前快取值 toobe 從 hello 快取中移除。</span><span class="sxs-lookup"><span data-stu-id="37c1f-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="37c1f-296">是</span><span class="sxs-lookup"><span data-stu-id="37c1f-296">Yes</span></span>|<span data-ttu-id="37c1f-297">N/A</span><span class="sxs-lookup"><span data-stu-id="37c1f-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="37c1f-298">使用量</span><span class="sxs-lookup"><span data-stu-id="37c1f-298">Usage</span></span>  
 <span data-ttu-id="37c1f-299">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="37c1f-300">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="37c1f-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="37c1f-301">**原則範圍︰**全域、API、作業、產品</span><span class="sxs-lookup"><span data-stu-id="37c1f-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="37c1f-302">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37c1f-302">Next steps</span></span>
<span data-ttu-id="37c1f-303">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="37c1f-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  