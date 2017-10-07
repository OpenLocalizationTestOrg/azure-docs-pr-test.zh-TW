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
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="e7dd7-103">API 管理存取限制原則</span><span class="sxs-lookup"><span data-stu-id="e7dd7-103">API Management access restriction policies</span></span>
<span data-ttu-id="e7dd7-104">本主題提供下列 API 管理原則的 hello 的參考。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="e7dd7-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="e7dd7-106"><a name="AccessRestrictionPolicies"></a>存取限制原則</span><span class="sxs-lookup"><span data-stu-id="e7dd7-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="e7dd7-107">[檢查 HTTP 標頭](api-management-access-restriction-policies.md#CheckHTTPHeader) - 強制必須存在和/或強制採用 HTTP 標頭的值。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="e7dd7-108">[依訂閱限制呼叫率](api-management-access-restriction-policies.md#LimitCallRate) - 以訂閱為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="e7dd7-109">[依金鑰限制呼叫率](#LimitCallRateByKey) - 以金鑰為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="e7dd7-110">[限制呼叫端 IP](api-management-access-restriction-policies.md#RestrictCallerIPs) - 篩選 (允許/拒絕) 來自特定 IP 位址和/或位址範圍的呼叫。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="e7dd7-111">[訂用帳戶所設定使用量配額](api-management-access-restriction-policies.md#SetUsageQuota)-可讓您以每個訂用帳戶為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="e7dd7-112">[設定使用量配額，依索引鍵](#SetUsageQuotaByKey)-可讓您以每個索引鍵為基礎的可更新的或存留期呼叫量和/或頻寬配額限制時，tooenforce。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="e7dd7-113">[驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT) - 強制擷取自指定 HTTP 標頭或指定查詢參數的 JWT 必須存在且有效。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="e7dd7-114"><a name="CheckHTTPHeader"></a>檢查 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="e7dd7-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="e7dd7-115">使用 hello`check-header`原則 tooenforce 要求必須指定的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="e7dd7-116">您可以選擇性地檢查 toosee，如果 hello 標頭所擁有的特定值或允許的值範圍的檢查。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="e7dd7-117">如果 hello 檢查失敗，hello 原則終止要求處理，並傳回 hello HTTP 狀態碼和錯誤訊息 hello 原則所指定。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7dd7-118">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="e7dd7-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="e7dd7-119">範例</span><span class="sxs-lookup"><span data-stu-id="e7dd7-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="e7dd7-120">元素</span><span class="sxs-lookup"><span data-stu-id="e7dd7-120">Elements</span></span>  
  
|<span data-ttu-id="e7dd7-121">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-121">Name</span></span>|<span data-ttu-id="e7dd7-122">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-122">Description</span></span>|<span data-ttu-id="e7dd7-123">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7dd7-124">check-header</span><span class="sxs-lookup"><span data-stu-id="e7dd7-124">check-header</span></span>|<span data-ttu-id="e7dd7-125">根元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-125">Root element.</span></span>|<span data-ttu-id="e7dd7-126">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-126">Yes</span></span>|  
|<span data-ttu-id="e7dd7-127">value</span><span class="sxs-lookup"><span data-stu-id="e7dd7-127">value</span></span>|<span data-ttu-id="e7dd7-128">允許的 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-128">Allowed HTTP header value.</span></span> <span data-ttu-id="e7dd7-129">當指定多個值的項目時，hello 則視為檢查成功 hello 值的任何一個是否符合項目。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="e7dd7-130">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7dd7-131">屬性</span><span class="sxs-lookup"><span data-stu-id="e7dd7-131">Attributes</span></span>  
  
|<span data-ttu-id="e7dd7-132">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-132">Name</span></span>|<span data-ttu-id="e7dd7-133">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-133">Description</span></span>|<span data-ttu-id="e7dd7-134">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-134">Required</span></span>|<span data-ttu-id="e7dd7-135">預設值</span><span class="sxs-lookup"><span data-stu-id="e7dd7-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7dd7-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="e7dd7-136">failed-check-error-message</span></span>|<span data-ttu-id="e7dd7-137">錯誤訊息 tooreturn hello 標頭不存在，或有無效的值如果 hello HTTP 回應主體中。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="e7dd7-138">此訊息必須正確逸出任何特殊字元。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="e7dd7-139">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-139">Yes</span></span>|<span data-ttu-id="e7dd7-140">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-140">N/A</span></span>|  
|<span data-ttu-id="e7dd7-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="e7dd7-141">failed-check-httpcode</span></span>|<span data-ttu-id="e7dd7-142">HTTP 狀態碼 tooreturn 如果 hello 標頭不存在，或有無效的值。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="e7dd7-143">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-143">Yes</span></span>|<span data-ttu-id="e7dd7-144">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-144">N/A</span></span>|  
|<span data-ttu-id="e7dd7-145">header-name</span><span class="sxs-lookup"><span data-stu-id="e7dd7-145">header-name</span></span>|<span data-ttu-id="e7dd7-146">hello hello toocheck HTTP 標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="e7dd7-147">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-147">Yes</span></span>|<span data-ttu-id="e7dd7-148">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-148">N/A</span></span>|  
|<span data-ttu-id="e7dd7-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="e7dd7-149">ignore-case</span></span>|<span data-ttu-id="e7dd7-150">可以設定 tooTrue 或 False。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="e7dd7-151">如果會比對可接受值的 hello 組 hello 標頭值時，會忽略 set tooTrue 案例。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="e7dd7-152">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-152">Yes</span></span>|<span data-ttu-id="e7dd7-153">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7dd7-154">使用量</span><span class="sxs-lookup"><span data-stu-id="e7dd7-154">Usage</span></span>  
 <span data-ttu-id="e7dd7-155">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7dd7-156">**原則區段︰**輸入、輸出</span><span class="sxs-lookup"><span data-stu-id="e7dd7-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="e7dd7-157">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="e7dd7-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e7dd7-158"><a name="LimitCallRate"></a>依訂用帳戶限制呼叫頻率</span><span class="sxs-lookup"><span data-stu-id="e7dd7-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="e7dd7-159">hello`rate-limit`原則防止 API 使用量暴增的每個訂用帳戶為基礎，藉由限制 hello 呼叫速率 tooa 指定數字，每個指定的時間期間。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="e7dd7-160">觸發此原則時 hello 呼叫端會收到`429 Too Many Requests`回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e7dd7-161">每份原則文件只能使用此原則一次。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e7dd7-162">[原則運算式](api-management-policy-expressions.md)不能在任何 hello 原則屬性的這個原則。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7dd7-163">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="e7dd7-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="e7dd7-164">範例</span><span class="sxs-lookup"><span data-stu-id="e7dd7-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e7dd7-165">元素</span><span class="sxs-lookup"><span data-stu-id="e7dd7-165">Elements</span></span>  
  
|<span data-ttu-id="e7dd7-166">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-166">Name</span></span>|<span data-ttu-id="e7dd7-167">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-167">Description</span></span>|<span data-ttu-id="e7dd7-168">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7dd7-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="e7dd7-169">set-limit</span></span>|<span data-ttu-id="e7dd7-170">根元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-170">Root element.</span></span>|<span data-ttu-id="e7dd7-171">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-171">Yes</span></span>|  
|<span data-ttu-id="e7dd7-172">api</span><span class="sxs-lookup"><span data-stu-id="e7dd7-172">api</span></span>|<span data-ttu-id="e7dd7-173">應用程式開發介面中新增一或多個這些項目 tooimpose 呼叫率限制 hello 產品中。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="e7dd7-174">產品和 API 呼叫頻率限制會獨立套用。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="e7dd7-175">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-175">No</span></span>|  
|<span data-ttu-id="e7dd7-176">operation</span><span class="sxs-lookup"><span data-stu-id="e7dd7-176">operation</span></span>|<span data-ttu-id="e7dd7-177">加入一或多個這些項目 tooimpose 呼叫率限制對 API 內的作業。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="e7dd7-178">產品、API 和作業呼叫頻率限制會獨立套用。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="e7dd7-179">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7dd7-180">屬性</span><span class="sxs-lookup"><span data-stu-id="e7dd7-180">Attributes</span></span>  
  
|<span data-ttu-id="e7dd7-181">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-181">Name</span></span>|<span data-ttu-id="e7dd7-182">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-182">Description</span></span>|<span data-ttu-id="e7dd7-183">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-183">Required</span></span>|<span data-ttu-id="e7dd7-184">預設值</span><span class="sxs-lookup"><span data-stu-id="e7dd7-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7dd7-185">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-185">name</span></span>|<span data-ttu-id="e7dd7-186">hello 名稱 hello API tooapply hello 速率限制。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="e7dd7-187">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-187">Yes</span></span>|<span data-ttu-id="e7dd7-188">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-188">N/A</span></span>|  
|<span data-ttu-id="e7dd7-189">calls</span><span class="sxs-lookup"><span data-stu-id="e7dd7-189">calls</span></span>|<span data-ttu-id="e7dd7-190">hello 的 hello hello 中指定的時間間隔內允許的呼叫總數上限`renewal-period`。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e7dd7-191">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-191">Yes</span></span>|<span data-ttu-id="e7dd7-192">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-192">N/A</span></span>|  
|<span data-ttu-id="e7dd7-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="e7dd7-193">renewal-period</span></span>|<span data-ttu-id="e7dd7-194">hello 時間期間 （秒） 之後 hello 重設配額。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="e7dd7-195">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-195">Yes</span></span>|<span data-ttu-id="e7dd7-196">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7dd7-197">使用量</span><span class="sxs-lookup"><span data-stu-id="e7dd7-197">Usage</span></span>  
 <span data-ttu-id="e7dd7-198">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7dd7-199">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="e7dd7-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e7dd7-200">**原則範圍︰**產品</span><span class="sxs-lookup"><span data-stu-id="e7dd7-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="e7dd7-201"><a name="LimitCallRateByKey"></a>依金鑰限制呼叫頻率</span><span class="sxs-lookup"><span data-stu-id="e7dd7-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="e7dd7-202">hello`rate-limit-by-key`原則防止 API 使用量暴增的每個索引鍵為基礎，藉由限制 hello 呼叫速率 tooa 指定數字，每個指定的時間期間。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="e7dd7-203">hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="e7dd7-204">選擇性的遞條件可以加入的 toospecify 哪些要求應該計入 hello 限制。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="e7dd7-205">觸發此原則時 hello 呼叫端會收到`429 Too Many Requests`回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="e7dd7-206">如需此原則範例的詳細資訊，請參閱[以 Azure API 管理進行進階要求節流](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e7dd7-207">每份原則文件只能使用此原則一次。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7dd7-208">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="e7dd7-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="e7dd7-209">範例</span><span class="sxs-lookup"><span data-stu-id="e7dd7-209">Example</span></span>  
 <span data-ttu-id="e7dd7-210">在下列範例的 hello，hello 速率限制是以 hello 呼叫端的 IP 位址做為索引。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e7dd7-211">元素</span><span class="sxs-lookup"><span data-stu-id="e7dd7-211">Elements</span></span>  
  
|<span data-ttu-id="e7dd7-212">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-212">Name</span></span>|<span data-ttu-id="e7dd7-213">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-213">Description</span></span>|<span data-ttu-id="e7dd7-214">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7dd7-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="e7dd7-215">set-limit</span></span>|<span data-ttu-id="e7dd7-216">根元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-216">Root element.</span></span>|<span data-ttu-id="e7dd7-217">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7dd7-218">屬性</span><span class="sxs-lookup"><span data-stu-id="e7dd7-218">Attributes</span></span>  
  
|<span data-ttu-id="e7dd7-219">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-219">Name</span></span>|<span data-ttu-id="e7dd7-220">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-220">Description</span></span>|<span data-ttu-id="e7dd7-221">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-221">Required</span></span>|<span data-ttu-id="e7dd7-222">預設值</span><span class="sxs-lookup"><span data-stu-id="e7dd7-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7dd7-223">calls</span><span class="sxs-lookup"><span data-stu-id="e7dd7-223">calls</span></span>|<span data-ttu-id="e7dd7-224">hello 的 hello hello 中指定的時間間隔內允許的呼叫總數上限`renewal-period`。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e7dd7-225">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-225">Yes</span></span>|<span data-ttu-id="e7dd7-226">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-226">N/A</span></span>|  
|<span data-ttu-id="e7dd7-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="e7dd7-227">counter-key</span></span>|<span data-ttu-id="e7dd7-228">hello 金鑰 toouse hello 速率限制原則。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="e7dd7-229">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-229">Yes</span></span>|<span data-ttu-id="e7dd7-230">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-230">N/A</span></span>|  
|<span data-ttu-id="e7dd7-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="e7dd7-231">increment-condition</span></span>|<span data-ttu-id="e7dd7-232">指定是否 hello 要求應該計數算入 hello 配額的 hello 布林運算式 (`true`)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="e7dd7-233">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-233">No</span></span>|<span data-ttu-id="e7dd7-234">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-234">N/A</span></span>|  
|<span data-ttu-id="e7dd7-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="e7dd7-235">renewal-period</span></span>|<span data-ttu-id="e7dd7-236">hello 時間期間 （秒） 之後 hello 重設配額。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="e7dd7-237">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-237">Yes</span></span>|<span data-ttu-id="e7dd7-238">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7dd7-239">使用量</span><span class="sxs-lookup"><span data-stu-id="e7dd7-239">Usage</span></span>  
 <span data-ttu-id="e7dd7-240">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7dd7-241">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="e7dd7-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e7dd7-242">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="e7dd7-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e7dd7-243"><a name="RestrictCallerIPs"></a>限制呼叫端 IP</span><span class="sxs-lookup"><span data-stu-id="e7dd7-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="e7dd7-244">hello`ip-filter`原則會篩選 （允許/拒絕） 來自特定 IP 位址和/或位址範圍的呼叫。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7dd7-245">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="e7dd7-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="e7dd7-246">範例</span><span class="sxs-lookup"><span data-stu-id="e7dd7-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="e7dd7-247">元素</span><span class="sxs-lookup"><span data-stu-id="e7dd7-247">Elements</span></span>  
  
|<span data-ttu-id="e7dd7-248">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-248">Name</span></span>|<span data-ttu-id="e7dd7-249">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-249">Description</span></span>|<span data-ttu-id="e7dd7-250">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7dd7-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="e7dd7-251">ip-filter</span></span>|<span data-ttu-id="e7dd7-252">根元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-252">Root element.</span></span>|<span data-ttu-id="e7dd7-253">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-253">Yes</span></span>|  
|<span data-ttu-id="e7dd7-254">位址</span><span class="sxs-lookup"><span data-stu-id="e7dd7-254">address</span></span>|<span data-ttu-id="e7dd7-255">哪些 toofilter 上指定單一 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="e7dd7-256">至少需要一個 `address` 或 `address-range` 元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="e7dd7-257">address-range from="位址" to="位址"</span><span class="sxs-lookup"><span data-stu-id="e7dd7-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="e7dd7-258">哪些 toofilter 上指定的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="e7dd7-259">至少需要一個 `address` 或 `address-range` 元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7dd7-260">屬性</span><span class="sxs-lookup"><span data-stu-id="e7dd7-260">Attributes</span></span>  
  
|<span data-ttu-id="e7dd7-261">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-261">Name</span></span>|<span data-ttu-id="e7dd7-262">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-262">Description</span></span>|<span data-ttu-id="e7dd7-263">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-263">Required</span></span>|<span data-ttu-id="e7dd7-264">預設值</span><span class="sxs-lookup"><span data-stu-id="e7dd7-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7dd7-265">address-range from="位址" to="位址"</span><span class="sxs-lookup"><span data-stu-id="e7dd7-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="e7dd7-266">範圍的 IP 位址 tooallow 或拒絕存取。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="e7dd7-267">需要： 當 hello`address-range`使用項目。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="e7dd7-268">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-268">N/A</span></span>|  
|<span data-ttu-id="e7dd7-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="e7dd7-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="e7dd7-270">指定呼叫應允許還是不會針對 hello 指定 IP 位址和範圍。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="e7dd7-271">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-271">Yes</span></span>|<span data-ttu-id="e7dd7-272">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7dd7-273">使用量</span><span class="sxs-lookup"><span data-stu-id="e7dd7-273">Usage</span></span>  
 <span data-ttu-id="e7dd7-274">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7dd7-275">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="e7dd7-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e7dd7-276">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="e7dd7-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e7dd7-277"><a name="SetUsageQuota"></a>依訂用帳戶設定使用量配額</span><span class="sxs-lookup"><span data-stu-id="e7dd7-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="e7dd7-278">hello`quota`原則會強制執行的可更新的或存留期呼叫量和/或頻寬配額限制時，每個訂用帳戶為基礎。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e7dd7-279">每份原則文件只能使用此原則一次。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e7dd7-280">[原則運算式](api-management-policy-expressions.md)不能在任何 hello 原則屬性的這個原則。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7dd7-281">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="e7dd7-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="e7dd7-282">範例</span><span class="sxs-lookup"><span data-stu-id="e7dd7-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e7dd7-283">元素</span><span class="sxs-lookup"><span data-stu-id="e7dd7-283">Elements</span></span>  
  
|<span data-ttu-id="e7dd7-284">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-284">Name</span></span>|<span data-ttu-id="e7dd7-285">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-285">Description</span></span>|<span data-ttu-id="e7dd7-286">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7dd7-287">quota</span><span class="sxs-lookup"><span data-stu-id="e7dd7-287">quota</span></span>|<span data-ttu-id="e7dd7-288">根元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-288">Root element.</span></span>|<span data-ttu-id="e7dd7-289">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-289">Yes</span></span>|  
|<span data-ttu-id="e7dd7-290">api</span><span class="sxs-lookup"><span data-stu-id="e7dd7-290">api</span></span>|<span data-ttu-id="e7dd7-291">應用程式開發介面中新增一或多個這些項目 tooimpose 配額 hello 產品中。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="e7dd7-292">產品和 API 配額會獨立套用。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="e7dd7-293">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-293">No</span></span>|  
|<span data-ttu-id="e7dd7-294">operation</span><span class="sxs-lookup"><span data-stu-id="e7dd7-294">operation</span></span>|<span data-ttu-id="e7dd7-295">加入一或多個這些項目 tooimpose 配額對 API 內的作業。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="e7dd7-296">產品、API 和作業配額會獨立套用。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="e7dd7-297">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7dd7-298">屬性</span><span class="sxs-lookup"><span data-stu-id="e7dd7-298">Attributes</span></span>  
  
|<span data-ttu-id="e7dd7-299">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-299">Name</span></span>|<span data-ttu-id="e7dd7-300">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-300">Description</span></span>|<span data-ttu-id="e7dd7-301">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-301">Required</span></span>|<span data-ttu-id="e7dd7-302">預設值</span><span class="sxs-lookup"><span data-stu-id="e7dd7-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7dd7-303">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-303">name</span></span>|<span data-ttu-id="e7dd7-304">hello 的 hello API 或操作的 hello 套用配額的名稱。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="e7dd7-305">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-305">Yes</span></span>|<span data-ttu-id="e7dd7-306">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-306">N/A</span></span>|  
|<span data-ttu-id="e7dd7-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="e7dd7-307">bandwidth</span></span>|<span data-ttu-id="e7dd7-308">hello 的 hello hello 中指定的時間間隔內允許的 kb 總數上限`renewal-period`。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e7dd7-309">必須指定 `calls`、`bandwidth`，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e7dd7-310">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-310">N/A</span></span>|  
|<span data-ttu-id="e7dd7-311">calls</span><span class="sxs-lookup"><span data-stu-id="e7dd7-311">calls</span></span>|<span data-ttu-id="e7dd7-312">hello 的 hello hello 中指定的時間間隔內允許的呼叫總數上限`renewal-period`。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e7dd7-313">必須指定 `calls`、`bandwidth`，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e7dd7-314">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-314">N/A</span></span>|  
|<span data-ttu-id="e7dd7-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="e7dd7-315">renewal-period</span></span>|<span data-ttu-id="e7dd7-316">hello 時間期間 （秒） 之後 hello 重設配額。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="e7dd7-317">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-317">Yes</span></span>|<span data-ttu-id="e7dd7-318">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7dd7-319">使用量</span><span class="sxs-lookup"><span data-stu-id="e7dd7-319">Usage</span></span>  
 <span data-ttu-id="e7dd7-320">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7dd7-321">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="e7dd7-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e7dd7-322">**原則範圍︰**產品</span><span class="sxs-lookup"><span data-stu-id="e7dd7-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="e7dd7-323"><a name="SetUsageQuotaByKey"></a>依金鑰設定使用量配額</span><span class="sxs-lookup"><span data-stu-id="e7dd7-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="e7dd7-324">hello`quota-by-key`原則會強制執行的可更新的或存留期呼叫量和/或頻寬配額限制時，每個索引鍵為基礎。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="e7dd7-325">hello 金鑰可以有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="e7dd7-326">選擇性的遞條件可以加入的 toospecify 哪些要求應該計入 hello 配額。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="e7dd7-327">如需此原則範例的詳細資訊，請參閱[以 Azure API 管理進行進階要求節流](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e7dd7-328">每份原則文件只能使用此原則一次。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e7dd7-329">[原則運算式](api-management-policy-expressions.md)不能在任何 hello 原則屬性的這個原則。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7dd7-330">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="e7dd7-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="e7dd7-331">範例</span><span class="sxs-lookup"><span data-stu-id="e7dd7-331">Example</span></span>  
 <span data-ttu-id="e7dd7-332">在下列範例的 hello，hello 配額是做為索引鍵使用 hello 呼叫端的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e7dd7-333">元素</span><span class="sxs-lookup"><span data-stu-id="e7dd7-333">Elements</span></span>  
  
|<span data-ttu-id="e7dd7-334">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-334">Name</span></span>|<span data-ttu-id="e7dd7-335">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-335">Description</span></span>|<span data-ttu-id="e7dd7-336">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7dd7-337">quota</span><span class="sxs-lookup"><span data-stu-id="e7dd7-337">quota</span></span>|<span data-ttu-id="e7dd7-338">根元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-338">Root element.</span></span>|<span data-ttu-id="e7dd7-339">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7dd7-340">屬性</span><span class="sxs-lookup"><span data-stu-id="e7dd7-340">Attributes</span></span>  
  
|<span data-ttu-id="e7dd7-341">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-341">Name</span></span>|<span data-ttu-id="e7dd7-342">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-342">Description</span></span>|<span data-ttu-id="e7dd7-343">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-343">Required</span></span>|<span data-ttu-id="e7dd7-344">預設值</span><span class="sxs-lookup"><span data-stu-id="e7dd7-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7dd7-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="e7dd7-345">bandwidth</span></span>|<span data-ttu-id="e7dd7-346">hello 的 hello hello 中指定的時間間隔內允許的 kb 總數上限`renewal-period`。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e7dd7-347">必須指定 `calls`、`bandwidth`，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e7dd7-348">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-348">N/A</span></span>|  
|<span data-ttu-id="e7dd7-349">calls</span><span class="sxs-lookup"><span data-stu-id="e7dd7-349">calls</span></span>|<span data-ttu-id="e7dd7-350">hello 的 hello hello 中指定的時間間隔內允許的呼叫總數上限`renewal-period`。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e7dd7-351">必須指定 `calls`、`bandwidth`，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e7dd7-352">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-352">N/A</span></span>|  
|<span data-ttu-id="e7dd7-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="e7dd7-353">counter-key</span></span>|<span data-ttu-id="e7dd7-354">hello 金鑰 toouse hello 配額原則。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="e7dd7-355">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-355">Yes</span></span>|<span data-ttu-id="e7dd7-356">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-356">N/A</span></span>|  
|<span data-ttu-id="e7dd7-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="e7dd7-357">increment-condition</span></span>|<span data-ttu-id="e7dd7-358">指定是否 hello 要求應該計數算入 hello 配額的 hello 布林運算式 (`true`)</span><span class="sxs-lookup"><span data-stu-id="e7dd7-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="e7dd7-359">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-359">No</span></span>|<span data-ttu-id="e7dd7-360">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-360">N/A</span></span>|  
|<span data-ttu-id="e7dd7-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="e7dd7-361">renewal-period</span></span>|<span data-ttu-id="e7dd7-362">hello 時間期間 （秒） 之後 hello 重設配額。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="e7dd7-363">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-363">Yes</span></span>|<span data-ttu-id="e7dd7-364">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7dd7-365">使用量</span><span class="sxs-lookup"><span data-stu-id="e7dd7-365">Usage</span></span>  
 <span data-ttu-id="e7dd7-366">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7dd7-367">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="e7dd7-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e7dd7-368">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="e7dd7-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e7dd7-369"><a name="ValidateJWT"></a>驗證 JWT</span><span class="sxs-lookup"><span data-stu-id="e7dd7-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="e7dd7-370">hello`validate-jwt`原則會強制執行是否存在，並從任一指定 HTTP 標頭或指定的查詢參數擷取的 JWT 的有效性。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e7dd7-371">hello`validate-jwt`原則需要該 hello`exp`已註冊的宣告是在 hello JWT 權杖中，所含，除非`require-expiration-time`屬性會指定並設定得`false`。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="e7dd7-372">hello`validate-jwt`原則支援 HS256 和 RS256 簽章演算法。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="e7dd7-373">HS256 hello 金鑰還必須提供內嵌 hello base64 編碼格式的 hello 原則內。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="e7dd7-374">如 RS256 hello 金鑰都有 toobe 提供透過 Open ID 組態端點。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7dd7-375">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="e7dd7-375">Policy statement</span></span>  
  
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
  
### <a name="examples"></a><span data-ttu-id="e7dd7-376">範例</span><span class="sxs-lookup"><span data-stu-id="e7dd7-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="e7dd7-377">Azure 行動服務權杖驗證</span><span class="sxs-lookup"><span data-stu-id="e7dd7-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="e7dd7-378">Azure Active Directory 權杖驗證</span><span class="sxs-lookup"><span data-stu-id="e7dd7-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="e7dd7-379">Azure Active Directory B2C 權杖驗證</span><span class="sxs-lookup"><span data-stu-id="e7dd7-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="e7dd7-380">授權權杖的宣告為基礎的存取 toooperations</span><span class="sxs-lookup"><span data-stu-id="e7dd7-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="e7dd7-381">這個範例會示範如何 toouse hello[驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT)原則 toopre-授權存取 toooperations 權杖宣告為基礎。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="e7dd7-382">如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too13:50 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="e7dd7-383">向前快轉 too15:00 toosee hello 原則在 hello 原則編輯器中設定，然後示範從 hello 開發人員入口網站及 hello 未呼叫作業的 too18:50 所需授權權杖。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e7dd7-384">元素</span><span class="sxs-lookup"><span data-stu-id="e7dd7-384">Elements</span></span>  
  
|<span data-ttu-id="e7dd7-385">元素</span><span class="sxs-lookup"><span data-stu-id="e7dd7-385">Element</span></span>|<span data-ttu-id="e7dd7-386">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-386">Description</span></span>|<span data-ttu-id="e7dd7-387">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="e7dd7-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="e7dd7-388">validate-jwt</span></span>|<span data-ttu-id="e7dd7-389">根元素。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-389">Root element.</span></span>|<span data-ttu-id="e7dd7-390">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-390">Yes</span></span>|  
|<span data-ttu-id="e7dd7-391">audiences</span><span class="sxs-lookup"><span data-stu-id="e7dd7-391">audiences</span></span>|<span data-ttu-id="e7dd7-392">包含可存在於 hello 語彙基元的可接受的對象宣告的清單。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="e7dd7-393">如果存在多個受眾值，則會嘗試每個值，直到全部試完 (即表示驗證失敗) 或其中一個值成功為止。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="e7dd7-394">必須指定至少一個受眾。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-394">At least one audience must be specified.</span></span>|<span data-ttu-id="e7dd7-395">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-395">No</span></span>|  
|<span data-ttu-id="e7dd7-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="e7dd7-396">issuer-signing-keys</span></span>|<span data-ttu-id="e7dd7-397">一份 base-64 編碼安全性金鑰使用 toovalidate 簽署權杖。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="e7dd7-398">如果存在多個安全性金鑰，則會嘗試每個金鑰，直到全部試完 (即表示驗證失敗) 或其中一個金鑰成功 (很適合用於權杖變換) 為止。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="e7dd7-399">索引鍵項目有選用`id`針對屬性使用 toomatch`kid`宣告。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="e7dd7-400">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-400">No</span></span>|  
|<span data-ttu-id="e7dd7-401">issuers</span><span class="sxs-lookup"><span data-stu-id="e7dd7-401">issuers</span></span>|<span data-ttu-id="e7dd7-402">可接受的主體發出 hello 權杖清單。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="e7dd7-403">如果存在多個簽發者值，則會嘗試每個值，直到全部試完 (即表示驗證失敗) 或其中一個值成功為止。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="e7dd7-404">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-404">No</span></span>|  
|<span data-ttu-id="e7dd7-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="e7dd7-405">openid-config</span></span>|<span data-ttu-id="e7dd7-406">用來指定要從中簽署金鑰和簽發者可以取得相容 Open ID 組態端點的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="e7dd7-407">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-407">No</span></span>|  
|<span data-ttu-id="e7dd7-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="e7dd7-408">required-claims</span></span>|<span data-ttu-id="e7dd7-409">包含一份存在於它的 hello 語彙基元上宣告 toobe toobe 視為有效。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="e7dd7-410">當 hello`match`屬性設定太`all`hello 原則中的每個宣告值必須位於為驗證 toosucceed hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="e7dd7-411">當 hello`match`屬性設定太`any`至少一個宣告中必須要有 hello 語彙基元的驗證 toosucceed。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="e7dd7-412">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-412">No</span></span>|  
|<span data-ttu-id="e7dd7-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="e7dd7-413">zumo-master-key</span></span>|<span data-ttu-id="e7dd7-414">Azure 行動服務所簽發之權杖的主要金鑰</span><span class="sxs-lookup"><span data-stu-id="e7dd7-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="e7dd7-415">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7dd7-416">屬性</span><span class="sxs-lookup"><span data-stu-id="e7dd7-416">Attributes</span></span>  
  
|<span data-ttu-id="e7dd7-417">名稱</span><span class="sxs-lookup"><span data-stu-id="e7dd7-417">Name</span></span>|<span data-ttu-id="e7dd7-418">說明</span><span class="sxs-lookup"><span data-stu-id="e7dd7-418">Description</span></span>|<span data-ttu-id="e7dd7-419">必要</span><span class="sxs-lookup"><span data-stu-id="e7dd7-419">Required</span></span>|<span data-ttu-id="e7dd7-420">預設值</span><span class="sxs-lookup"><span data-stu-id="e7dd7-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7dd7-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="e7dd7-421">clock-skew</span></span>|<span data-ttu-id="e7dd7-422">時間範圍。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-422">Timespan.</span></span> <span data-ttu-id="e7dd7-423">提供些許 hello 權杖的逾期宣告存在於 hello 語彙基元，而且已超出 hello 目前日期 / 時間。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="e7dd7-424">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-424">No</span></span>|<span data-ttu-id="e7dd7-425">0 秒</span><span class="sxs-lookup"><span data-stu-id="e7dd7-425">0 seconds</span></span>|  
|<span data-ttu-id="e7dd7-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="e7dd7-426">failed-validation-error-message</span></span>|<span data-ttu-id="e7dd7-427">如果 hello JWT 未通過驗證的 hello HTTP 回應主體中的錯誤訊息 tooreturn。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="e7dd7-428">此訊息必須正確逸出任何特殊字元。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="e7dd7-429">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-429">No</span></span>|<span data-ttu-id="e7dd7-430">預設錯誤訊息視驗證問題而定，例如「JWT 不存在」。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="e7dd7-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="e7dd7-431">failed-validation-httpcode</span></span>|<span data-ttu-id="e7dd7-432">HTTP 狀態碼 tooreturn 如果 hello JWT 未通過驗證。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="e7dd7-433">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-433">No</span></span>|<span data-ttu-id="e7dd7-434">401</span><span class="sxs-lookup"><span data-stu-id="e7dd7-434">401</span></span>|  
|<span data-ttu-id="e7dd7-435">header-name</span><span class="sxs-lookup"><span data-stu-id="e7dd7-435">header-name</span></span>|<span data-ttu-id="e7dd7-436">hello 持有 hello 語彙基元的 hello HTTP 標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="e7dd7-437">必須指定 `header-name` 或 `query-paremeter-name`；但不能同時指定。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="e7dd7-438">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-438">N/A</span></span>|  
|<span data-ttu-id="e7dd7-439">id</span><span class="sxs-lookup"><span data-stu-id="e7dd7-439">id</span></span>|<span data-ttu-id="e7dd7-440">hello`id`屬性 hello`key`元素可讓您將會比對的 toospecify hello 字串`kid`hello 出 hello 適當索引鍵的 toouse 簽章驗證的語彙基元 （如果有的話） toofind 中宣告。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="e7dd7-441">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-441">No</span></span>|<span data-ttu-id="e7dd7-442">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-442">N/A</span></span>|  
|<span data-ttu-id="e7dd7-443">match</span><span class="sxs-lookup"><span data-stu-id="e7dd7-443">match</span></span>|<span data-ttu-id="e7dd7-444">hello`match`屬性 hello`claim`項目會指定是否必須存在於 hello 語彙基元的驗證 toosucceed hello 原則中的每個宣告值。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="e7dd7-445">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="e7dd7-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="e7dd7-446">-                          `all`-hello 原則中的每個宣告值必須位於為驗證 toosucceed hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="e7dd7-447">-                          `any`-至少一個宣告值必須位於為驗證 toosucceed hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="e7dd7-448">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-448">No</span></span>|<span data-ttu-id="e7dd7-449">所有</span><span class="sxs-lookup"><span data-stu-id="e7dd7-449">all</span></span>|  
|<span data-ttu-id="e7dd7-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="e7dd7-450">query-paremeter-name</span></span>|<span data-ttu-id="e7dd7-451">hello hello hello 查詢參數可保留 hello 語彙基元名稱。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="e7dd7-452">必須指定 `header-name` 或 `query-paremeter-name`；但不能同時指定。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="e7dd7-453">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-453">N/A</span></span>|  
|<span data-ttu-id="e7dd7-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="e7dd7-454">require-expiration-time</span></span>|<span data-ttu-id="e7dd7-455">布林值。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-455">Boolean.</span></span> <span data-ttu-id="e7dd7-456">指定是否 hello 語彙基元必須有逾期宣告。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="e7dd7-457">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-457">No</span></span>|<span data-ttu-id="e7dd7-458">true</span><span class="sxs-lookup"><span data-stu-id="e7dd7-458">true</span></span>|
|<span data-ttu-id="e7dd7-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="e7dd7-459">require-scheme</span></span>|<span data-ttu-id="e7dd7-460">hello 配置的名稱 hello 語彙基元，例如："Bearer"。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="e7dd7-461">當設定這個屬性時，可確保 hello 原則，指定之結構描述存在於 hello 授權標頭值。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="e7dd7-462">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-462">No</span></span>|<span data-ttu-id="e7dd7-463">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-463">N/A</span></span>|
|<span data-ttu-id="e7dd7-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="e7dd7-464">require-signed-tokens</span></span>|<span data-ttu-id="e7dd7-465">布林值。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-465">Boolean.</span></span> <span data-ttu-id="e7dd7-466">指定權杖是否需要的 toobe 簽署。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="e7dd7-467">否</span><span class="sxs-lookup"><span data-stu-id="e7dd7-467">No</span></span>|<span data-ttu-id="e7dd7-468">true</span><span class="sxs-lookup"><span data-stu-id="e7dd7-468">true</span></span>|  
|<span data-ttu-id="e7dd7-469">url</span><span class="sxs-lookup"><span data-stu-id="e7dd7-469">url</span></span>|<span data-ttu-id="e7dd7-470">可從中取得 Open ID 設定中繼資料的 Open ID 設定端點 URL。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="e7dd7-471">Azure Active Directory，請使用下列 URL 的 hello:`https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration`以取代您目錄租用戶的名稱，例如`contoso.onmicrosoft.com`。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="e7dd7-472">是</span><span class="sxs-lookup"><span data-stu-id="e7dd7-472">Yes</span></span>|<span data-ttu-id="e7dd7-473">N/A</span><span class="sxs-lookup"><span data-stu-id="e7dd7-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7dd7-474">使用量</span><span class="sxs-lookup"><span data-stu-id="e7dd7-474">Usage</span></span>  
 <span data-ttu-id="e7dd7-475">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7dd7-476">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="e7dd7-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e7dd7-477">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="e7dd7-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="e7dd7-478">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7dd7-478">Next steps</span></span>
<span data-ttu-id="e7dd7-479">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="e7dd7-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
