---
title: "Azure API 管理存取限制原則 | Microsoft Docs"
description: "了解可用於 Azure API 管理中的存取限制原則。"
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
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="0d7cd-103">API 管理存取限制原則</span><span class="sxs-lookup"><span data-stu-id="0d7cd-103">API Management access restriction policies</span></span>
<span data-ttu-id="0d7cd-104">本主題提供下列 API 管理原則的參考。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="0d7cd-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="0d7cd-106"><a name="AccessRestrictionPolicies"></a>存取限制原則</span><span class="sxs-lookup"><span data-stu-id="0d7cd-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="0d7cd-107">[檢查 HTTP 標頭](api-management-access-restriction-policies.md#CheckHTTPHeader) - 強制必須存在和/或強制採用 HTTP 標頭的值。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="0d7cd-108">[依訂閱限制呼叫率](api-management-access-restriction-policies.md#LimitCallRate) - 以訂閱為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="0d7cd-109">[依金鑰限制呼叫率](#LimitCallRateByKey) - 以金鑰為單位，限制呼叫率以避免 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="0d7cd-110">[限制呼叫端 IP](api-management-access-restriction-policies.md#RestrictCallerIPs) - 篩選 (允許/拒絕) 來自特定 IP 位址和/或位址範圍的呼叫。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="0d7cd-111">[依訂閱設定使用量配額](api-management-access-restriction-policies.md#SetUsageQuota) - 以訂閱為單位，讓您可以強制採用可續訂或有存留期呼叫量與 (或) 頻寬配額。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="0d7cd-112">[依金鑰設定使用量配額](#SetUsageQuotaByKey) - 以金鑰為單位，讓您可以強制採用可續訂或有存留期呼叫量與 (或) 頻寬配額。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="0d7cd-113">[驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT) - 強制擷取自指定 HTTP 標頭或指定查詢參數的 JWT 必須存在且有效。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="0d7cd-114"><a name="CheckHTTPHeader"></a>檢查 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="0d7cd-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="0d7cd-115">使用 `check-header` 原則來強制各要求均需具有指定的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="0d7cd-116">您可以選擇性地查看標頭是否具有特定值，或檢查允許的值範圍。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="0d7cd-117">如果檢查失敗，原則就會終止要求處理，並傳回原則所指定的 HTTP 狀態碼和錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0d7cd-118">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0d7cd-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="0d7cd-119">範例</span><span class="sxs-lookup"><span data-stu-id="0d7cd-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="0d7cd-120">元素</span><span class="sxs-lookup"><span data-stu-id="0d7cd-120">Elements</span></span>  
  
|<span data-ttu-id="0d7cd-121">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-121">Name</span></span>|<span data-ttu-id="0d7cd-122">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-122">Description</span></span>|<span data-ttu-id="0d7cd-123">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0d7cd-124">check-header</span><span class="sxs-lookup"><span data-stu-id="0d7cd-124">check-header</span></span>|<span data-ttu-id="0d7cd-125">根元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-125">Root element.</span></span>|<span data-ttu-id="0d7cd-126">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-126">Yes</span></span>|  
|<span data-ttu-id="0d7cd-127">value</span><span class="sxs-lookup"><span data-stu-id="0d7cd-127">value</span></span>|<span data-ttu-id="0d7cd-128">允許的 HTTP 標頭值。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-128">Allowed HTTP header value.</span></span> <span data-ttu-id="0d7cd-129">指定多個值元素時，如果其中任何一個值相符，則會將檢查視為成功。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="0d7cd-130">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0d7cd-131">屬性</span><span class="sxs-lookup"><span data-stu-id="0d7cd-131">Attributes</span></span>  
  
|<span data-ttu-id="0d7cd-132">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-132">Name</span></span>|<span data-ttu-id="0d7cd-133">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-133">Description</span></span>|<span data-ttu-id="0d7cd-134">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-134">Required</span></span>|<span data-ttu-id="0d7cd-135">預設值</span><span class="sxs-lookup"><span data-stu-id="0d7cd-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0d7cd-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="0d7cd-136">failed-check-error-message</span></span>|<span data-ttu-id="0d7cd-137">如果標頭不存在或具有無效值，要在 HTTP 回應本文中傳回的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="0d7cd-138">此訊息必須正確逸出任何特殊字元。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="0d7cd-139">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-139">Yes</span></span>|<span data-ttu-id="0d7cd-140">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-140">N/A</span></span>|  
|<span data-ttu-id="0d7cd-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="0d7cd-141">failed-check-httpcode</span></span>|<span data-ttu-id="0d7cd-142">標頭不存在或具有無效值時所要傳回的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="0d7cd-143">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-143">Yes</span></span>|<span data-ttu-id="0d7cd-144">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-144">N/A</span></span>|  
|<span data-ttu-id="0d7cd-145">header-name</span><span class="sxs-lookup"><span data-stu-id="0d7cd-145">header-name</span></span>|<span data-ttu-id="0d7cd-146">要檢查的 HTTP 標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="0d7cd-147">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-147">Yes</span></span>|<span data-ttu-id="0d7cd-148">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-148">N/A</span></span>|  
|<span data-ttu-id="0d7cd-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="0d7cd-149">ignore-case</span></span>|<span data-ttu-id="0d7cd-150">可以設定為 True 或 False。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-150">Can be set to True or False.</span></span> <span data-ttu-id="0d7cd-151">如果設定為 True，則會在標頭值與一組可接受的值進行比較時，忽略大小寫。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="0d7cd-152">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-152">Yes</span></span>|<span data-ttu-id="0d7cd-153">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0d7cd-154">使用量</span><span class="sxs-lookup"><span data-stu-id="0d7cd-154">Usage</span></span>  
 <span data-ttu-id="0d7cd-155">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0d7cd-156">**原則區段︰**輸入、輸出</span><span class="sxs-lookup"><span data-stu-id="0d7cd-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="0d7cd-157">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="0d7cd-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="0d7cd-158"><a name="LimitCallRate"></a>依訂用帳戶限制呼叫頻率</span><span class="sxs-lookup"><span data-stu-id="0d7cd-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="0d7cd-159">`rate-limit` 原則藉由將指定時間週期內的呼叫頻率限制為指定次數，以防止每個訂用帳戶的 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="0d7cd-160">觸發此原則時，呼叫者會收到 `429 Too Many Requests` 回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="0d7cd-161">每份原則文件只能使用此原則一次。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="0d7cd-162">[原則運算式](api-management-policy-expressions.md)無法使用於此原則的任何原則屬性。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0d7cd-163">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0d7cd-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="0d7cd-164">範例</span><span class="sxs-lookup"><span data-stu-id="0d7cd-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="0d7cd-165">元素</span><span class="sxs-lookup"><span data-stu-id="0d7cd-165">Elements</span></span>  
  
|<span data-ttu-id="0d7cd-166">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-166">Name</span></span>|<span data-ttu-id="0d7cd-167">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-167">Description</span></span>|<span data-ttu-id="0d7cd-168">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0d7cd-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="0d7cd-169">set-limit</span></span>|<span data-ttu-id="0d7cd-170">根元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-170">Root element.</span></span>|<span data-ttu-id="0d7cd-171">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-171">Yes</span></span>|  
|<span data-ttu-id="0d7cd-172">api</span><span class="sxs-lookup"><span data-stu-id="0d7cd-172">api</span></span>|<span data-ttu-id="0d7cd-173">新增一或多個這些元素，以對產品內的 API 強加呼叫頻率限制。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="0d7cd-174">產品和 API 呼叫頻率限制會獨立套用。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="0d7cd-175">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-175">No</span></span>|  
|<span data-ttu-id="0d7cd-176">operation</span><span class="sxs-lookup"><span data-stu-id="0d7cd-176">operation</span></span>|<span data-ttu-id="0d7cd-177">新增一或多個這些元素，以對 API 內的作業強加呼叫頻率限制。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="0d7cd-178">產品、API 和作業呼叫頻率限制會獨立套用。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="0d7cd-179">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0d7cd-180">屬性</span><span class="sxs-lookup"><span data-stu-id="0d7cd-180">Attributes</span></span>  
  
|<span data-ttu-id="0d7cd-181">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-181">Name</span></span>|<span data-ttu-id="0d7cd-182">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-182">Description</span></span>|<span data-ttu-id="0d7cd-183">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-183">Required</span></span>|<span data-ttu-id="0d7cd-184">預設值</span><span class="sxs-lookup"><span data-stu-id="0d7cd-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0d7cd-185">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-185">name</span></span>|<span data-ttu-id="0d7cd-186">要套用速率限制的 API 名稱。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="0d7cd-187">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-187">Yes</span></span>|<span data-ttu-id="0d7cd-188">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-188">N/A</span></span>|  
|<span data-ttu-id="0d7cd-189">calls</span><span class="sxs-lookup"><span data-stu-id="0d7cd-189">calls</span></span>|<span data-ttu-id="0d7cd-190">在 `renewal-period` 中指定的時間週期內允許的呼叫總數上限。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="0d7cd-191">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-191">Yes</span></span>|<span data-ttu-id="0d7cd-192">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-192">N/A</span></span>|  
|<span data-ttu-id="0d7cd-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="0d7cd-193">renewal-period</span></span>|<span data-ttu-id="0d7cd-194">重設配額的時間週期 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="0d7cd-195">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-195">Yes</span></span>|<span data-ttu-id="0d7cd-196">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0d7cd-197">使用量</span><span class="sxs-lookup"><span data-stu-id="0d7cd-197">Usage</span></span>  
 <span data-ttu-id="0d7cd-198">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0d7cd-199">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="0d7cd-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0d7cd-200">**原則範圍︰**產品</span><span class="sxs-lookup"><span data-stu-id="0d7cd-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="0d7cd-201"><a name="LimitCallRateByKey"></a>依金鑰限制呼叫頻率</span><span class="sxs-lookup"><span data-stu-id="0d7cd-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="0d7cd-202">`rate-limit-by-key` 原則藉由將指定時間週期內的呼叫頻率限制為指定次數，以防止每個金鑰的 API 使用量暴增。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="0d7cd-203">金鑰可以具有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="0d7cd-204">可以新增選擇性增量條件，以指定哪些要求應該計入限制。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="0d7cd-205">觸發此原則時，呼叫者會收到 `429 Too Many Requests` 回應狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="0d7cd-206">如需此原則範例的詳細資訊，請參閱[以 Azure API 管理進行進階要求節流](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="0d7cd-207">每份原則文件只能使用此原則一次。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0d7cd-208">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0d7cd-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="0d7cd-209">範例</span><span class="sxs-lookup"><span data-stu-id="0d7cd-209">Example</span></span>  
 <span data-ttu-id="0d7cd-210">在下列範例中，頻率限制是依呼叫端 IP 位址鍵入。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="0d7cd-211">元素</span><span class="sxs-lookup"><span data-stu-id="0d7cd-211">Elements</span></span>  
  
|<span data-ttu-id="0d7cd-212">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-212">Name</span></span>|<span data-ttu-id="0d7cd-213">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-213">Description</span></span>|<span data-ttu-id="0d7cd-214">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0d7cd-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="0d7cd-215">set-limit</span></span>|<span data-ttu-id="0d7cd-216">根元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-216">Root element.</span></span>|<span data-ttu-id="0d7cd-217">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0d7cd-218">屬性</span><span class="sxs-lookup"><span data-stu-id="0d7cd-218">Attributes</span></span>  
  
|<span data-ttu-id="0d7cd-219">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-219">Name</span></span>|<span data-ttu-id="0d7cd-220">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-220">Description</span></span>|<span data-ttu-id="0d7cd-221">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-221">Required</span></span>|<span data-ttu-id="0d7cd-222">預設值</span><span class="sxs-lookup"><span data-stu-id="0d7cd-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0d7cd-223">calls</span><span class="sxs-lookup"><span data-stu-id="0d7cd-223">calls</span></span>|<span data-ttu-id="0d7cd-224">在 `renewal-period` 中指定的時間週期內允許的呼叫總數上限。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="0d7cd-225">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-225">Yes</span></span>|<span data-ttu-id="0d7cd-226">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-226">N/A</span></span>|  
|<span data-ttu-id="0d7cd-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="0d7cd-227">counter-key</span></span>|<span data-ttu-id="0d7cd-228">用於頻率限制原則的金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="0d7cd-229">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-229">Yes</span></span>|<span data-ttu-id="0d7cd-230">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-230">N/A</span></span>|  
|<span data-ttu-id="0d7cd-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="0d7cd-231">increment-condition</span></span>|<span data-ttu-id="0d7cd-232">此布林運算式指定要求是否應該計入配額 (`true`)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="0d7cd-233">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-233">No</span></span>|<span data-ttu-id="0d7cd-234">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-234">N/A</span></span>|  
|<span data-ttu-id="0d7cd-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="0d7cd-235">renewal-period</span></span>|<span data-ttu-id="0d7cd-236">重設配額的時間週期 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="0d7cd-237">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-237">Yes</span></span>|<span data-ttu-id="0d7cd-238">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0d7cd-239">使用量</span><span class="sxs-lookup"><span data-stu-id="0d7cd-239">Usage</span></span>  
 <span data-ttu-id="0d7cd-240">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0d7cd-241">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="0d7cd-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0d7cd-242">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="0d7cd-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="0d7cd-243"><a name="RestrictCallerIPs"></a>限制呼叫端 IP</span><span class="sxs-lookup"><span data-stu-id="0d7cd-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="0d7cd-244">`ip-filter` 原則可篩選 (允許/拒絕) 來自特定 IP 位址及/或位址範圍的呼叫。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0d7cd-245">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0d7cd-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="0d7cd-246">範例</span><span class="sxs-lookup"><span data-stu-id="0d7cd-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="0d7cd-247">元素</span><span class="sxs-lookup"><span data-stu-id="0d7cd-247">Elements</span></span>  
  
|<span data-ttu-id="0d7cd-248">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-248">Name</span></span>|<span data-ttu-id="0d7cd-249">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-249">Description</span></span>|<span data-ttu-id="0d7cd-250">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0d7cd-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="0d7cd-251">ip-filter</span></span>|<span data-ttu-id="0d7cd-252">根元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-252">Root element.</span></span>|<span data-ttu-id="0d7cd-253">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-253">Yes</span></span>|  
|<span data-ttu-id="0d7cd-254">位址</span><span class="sxs-lookup"><span data-stu-id="0d7cd-254">address</span></span>|<span data-ttu-id="0d7cd-255">指定要篩選的單一 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="0d7cd-256">至少需要一個 `address` 或 `address-range` 元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="0d7cd-257">address-range from="位址" to="位址"</span><span class="sxs-lookup"><span data-stu-id="0d7cd-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="0d7cd-258">指定要篩選的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="0d7cd-259">至少需要一個 `address` 或 `address-range` 元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0d7cd-260">屬性</span><span class="sxs-lookup"><span data-stu-id="0d7cd-260">Attributes</span></span>  
  
|<span data-ttu-id="0d7cd-261">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-261">Name</span></span>|<span data-ttu-id="0d7cd-262">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-262">Description</span></span>|<span data-ttu-id="0d7cd-263">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-263">Required</span></span>|<span data-ttu-id="0d7cd-264">預設值</span><span class="sxs-lookup"><span data-stu-id="0d7cd-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0d7cd-265">address-range from="位址" to="位址"</span><span class="sxs-lookup"><span data-stu-id="0d7cd-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="0d7cd-266">允許或拒絕存取的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="0d7cd-267">使用 `address-range` 元素時必要。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="0d7cd-268">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-268">N/A</span></span>|  
|<span data-ttu-id="0d7cd-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="0d7cd-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="0d7cd-270">指定允許或不允許指定的 IP 位址和範圍進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="0d7cd-271">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-271">Yes</span></span>|<span data-ttu-id="0d7cd-272">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0d7cd-273">使用量</span><span class="sxs-lookup"><span data-stu-id="0d7cd-273">Usage</span></span>  
 <span data-ttu-id="0d7cd-274">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0d7cd-275">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="0d7cd-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0d7cd-276">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="0d7cd-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="0d7cd-277"><a name="SetUsageQuota"></a>依訂用帳戶設定使用量配額</span><span class="sxs-lookup"><span data-stu-id="0d7cd-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="0d7cd-278">`quota` 原則會以訂用帳戶為單位，強制採用可續訂或有存留期呼叫量與 (或) 頻寬配額。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="0d7cd-279">每份原則文件只能使用此原則一次。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="0d7cd-280">[原則運算式](api-management-policy-expressions.md)無法使用於此原則的任何原則屬性。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0d7cd-281">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0d7cd-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="0d7cd-282">範例</span><span class="sxs-lookup"><span data-stu-id="0d7cd-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="0d7cd-283">元素</span><span class="sxs-lookup"><span data-stu-id="0d7cd-283">Elements</span></span>  
  
|<span data-ttu-id="0d7cd-284">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-284">Name</span></span>|<span data-ttu-id="0d7cd-285">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-285">Description</span></span>|<span data-ttu-id="0d7cd-286">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0d7cd-287">quota</span><span class="sxs-lookup"><span data-stu-id="0d7cd-287">quota</span></span>|<span data-ttu-id="0d7cd-288">根元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-288">Root element.</span></span>|<span data-ttu-id="0d7cd-289">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-289">Yes</span></span>|  
|<span data-ttu-id="0d7cd-290">api</span><span class="sxs-lookup"><span data-stu-id="0d7cd-290">api</span></span>|<span data-ttu-id="0d7cd-291">新增一或多個這些元素，以對產品內的 API 強加配額。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="0d7cd-292">產品和 API 配額會獨立套用。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="0d7cd-293">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-293">No</span></span>|  
|<span data-ttu-id="0d7cd-294">operation</span><span class="sxs-lookup"><span data-stu-id="0d7cd-294">operation</span></span>|<span data-ttu-id="0d7cd-295">新增一或多個這些元素，以對 API 內的作業強加配額。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="0d7cd-296">產品、API 和作業配額會獨立套用。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="0d7cd-297">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0d7cd-298">屬性</span><span class="sxs-lookup"><span data-stu-id="0d7cd-298">Attributes</span></span>  
  
|<span data-ttu-id="0d7cd-299">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-299">Name</span></span>|<span data-ttu-id="0d7cd-300">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-300">Description</span></span>|<span data-ttu-id="0d7cd-301">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-301">Required</span></span>|<span data-ttu-id="0d7cd-302">預設值</span><span class="sxs-lookup"><span data-stu-id="0d7cd-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0d7cd-303">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-303">name</span></span>|<span data-ttu-id="0d7cd-304">套用配額的 API 或作業名稱。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="0d7cd-305">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-305">Yes</span></span>|<span data-ttu-id="0d7cd-306">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-306">N/A</span></span>|  
|<span data-ttu-id="0d7cd-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="0d7cd-307">bandwidth</span></span>|<span data-ttu-id="0d7cd-308">在 `renewal-period` 中指定的時間週期內允許的 KB 總數上限。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="0d7cd-309">必須指定 `calls`、`bandwidth`，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="0d7cd-310">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-310">N/A</span></span>|  
|<span data-ttu-id="0d7cd-311">calls</span><span class="sxs-lookup"><span data-stu-id="0d7cd-311">calls</span></span>|<span data-ttu-id="0d7cd-312">在 `renewal-period` 中指定的時間週期內允許的呼叫總數上限。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="0d7cd-313">必須指定 `calls`、`bandwidth`，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="0d7cd-314">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-314">N/A</span></span>|  
|<span data-ttu-id="0d7cd-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="0d7cd-315">renewal-period</span></span>|<span data-ttu-id="0d7cd-316">重設配額的時間週期 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="0d7cd-317">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-317">Yes</span></span>|<span data-ttu-id="0d7cd-318">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0d7cd-319">使用量</span><span class="sxs-lookup"><span data-stu-id="0d7cd-319">Usage</span></span>  
 <span data-ttu-id="0d7cd-320">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0d7cd-321">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="0d7cd-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0d7cd-322">**原則範圍︰**產品</span><span class="sxs-lookup"><span data-stu-id="0d7cd-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="0d7cd-323"><a name="SetUsageQuotaByKey"></a>依金鑰設定使用量配額</span><span class="sxs-lookup"><span data-stu-id="0d7cd-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="0d7cd-324">`quota-by-key` 原則會以金鑰為單位，強制採用可續訂或有存留期呼叫量與 (或) 頻寬配額。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="0d7cd-325">金鑰可以具有任意字串值，而且通常會使用原則運算式來提供。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="0d7cd-326">可以新增選擇性增量條件，以指定哪些要求應該計入配額。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="0d7cd-327">如需此原則範例的詳細資訊，請參閱[以 Azure API 管理進行進階要求節流](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="0d7cd-328">每份原則文件只能使用此原則一次。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="0d7cd-329">[原則運算式](api-management-policy-expressions.md)無法使用於此原則的任何原則屬性。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0d7cd-330">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0d7cd-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="0d7cd-331">範例</span><span class="sxs-lookup"><span data-stu-id="0d7cd-331">Example</span></span>  
 <span data-ttu-id="0d7cd-332">在下列範例中，配額是依呼叫端 IP 位址鍵入。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="0d7cd-333">元素</span><span class="sxs-lookup"><span data-stu-id="0d7cd-333">Elements</span></span>  
  
|<span data-ttu-id="0d7cd-334">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-334">Name</span></span>|<span data-ttu-id="0d7cd-335">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-335">Description</span></span>|<span data-ttu-id="0d7cd-336">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0d7cd-337">quota</span><span class="sxs-lookup"><span data-stu-id="0d7cd-337">quota</span></span>|<span data-ttu-id="0d7cd-338">根元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-338">Root element.</span></span>|<span data-ttu-id="0d7cd-339">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0d7cd-340">屬性</span><span class="sxs-lookup"><span data-stu-id="0d7cd-340">Attributes</span></span>  
  
|<span data-ttu-id="0d7cd-341">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-341">Name</span></span>|<span data-ttu-id="0d7cd-342">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-342">Description</span></span>|<span data-ttu-id="0d7cd-343">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-343">Required</span></span>|<span data-ttu-id="0d7cd-344">預設值</span><span class="sxs-lookup"><span data-stu-id="0d7cd-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0d7cd-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="0d7cd-345">bandwidth</span></span>|<span data-ttu-id="0d7cd-346">在 `renewal-period` 中指定的時間週期內允許的 KB 總數上限。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="0d7cd-347">必須指定 `calls`、`bandwidth`，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="0d7cd-348">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-348">N/A</span></span>|  
|<span data-ttu-id="0d7cd-349">calls</span><span class="sxs-lookup"><span data-stu-id="0d7cd-349">calls</span></span>|<span data-ttu-id="0d7cd-350">在 `renewal-period` 中指定的時間週期內允許的呼叫總數上限。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="0d7cd-351">必須指定 `calls`、`bandwidth`，或同時指定兩者。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="0d7cd-352">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-352">N/A</span></span>|  
|<span data-ttu-id="0d7cd-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="0d7cd-353">counter-key</span></span>|<span data-ttu-id="0d7cd-354">用於配額原則的金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="0d7cd-355">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-355">Yes</span></span>|<span data-ttu-id="0d7cd-356">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-356">N/A</span></span>|  
|<span data-ttu-id="0d7cd-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="0d7cd-357">increment-condition</span></span>|<span data-ttu-id="0d7cd-358">此布林運算式指定要求是否應該計入配額 (`true`)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="0d7cd-359">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-359">No</span></span>|<span data-ttu-id="0d7cd-360">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-360">N/A</span></span>|  
|<span data-ttu-id="0d7cd-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="0d7cd-361">renewal-period</span></span>|<span data-ttu-id="0d7cd-362">重設配額的時間週期 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="0d7cd-363">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-363">Yes</span></span>|<span data-ttu-id="0d7cd-364">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0d7cd-365">使用量</span><span class="sxs-lookup"><span data-stu-id="0d7cd-365">Usage</span></span>  
 <span data-ttu-id="0d7cd-366">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0d7cd-367">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="0d7cd-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0d7cd-368">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="0d7cd-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="0d7cd-369"><a name="ValidateJWT"></a>驗證 JWT</span><span class="sxs-lookup"><span data-stu-id="0d7cd-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="0d7cd-370">`validate-jwt` 原則會強制擷取自指定 HTTP 標頭或指定查詢參數的 JWT 必須存在且有效。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="0d7cd-371">`validate-jwt` 原則會要求 `exp` 註冊的宣告包含在 JWT 權杖中 (除非已指定 `require-expiration-time` 屬性並設定為 `false`)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="0d7cd-372">`validate-jwt` 原則支援 HS256 和 RS256 簽署演算法。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="0d7cd-373">若為 HS256，必須以 base64 編碼形式內嵌於原則內的方式提供金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="0d7cd-374">若為 RS256，必須透過 Open ID 設定端點提供金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0d7cd-375">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0d7cd-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
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
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="0d7cd-376">範例</span><span class="sxs-lookup"><span data-stu-id="0d7cd-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="0d7cd-377">Azure 行動服務權杖驗證</span><span class="sxs-lookup"><span data-stu-id="0d7cd-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="0d7cd-378">Azure Active Directory 權杖驗證</span><span class="sxs-lookup"><span data-stu-id="0d7cd-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="0d7cd-379">Azure Active Directory B2C 權杖驗證</span><span class="sxs-lookup"><span data-stu-id="0d7cd-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="0d7cd-380">根據權杖宣告授與作業的存取權</span><span class="sxs-lookup"><span data-stu-id="0d7cd-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="0d7cd-381">此範例示範如何使用 [驗證 JWT](api-management-access-restriction-policies.md#ValidateJWT) 原則來根據權杖宣告預先授與作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="0d7cd-382">如需設定和使用此原則的示範，請觀賞 [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)，快轉到 13:50。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="0d7cd-383">向前快轉到 15:00 可看到在原則編輯器中設定的原則，再到 18:50 可以看到一個示範，從開發人員入口網站 (使用和不使用必要的授權權杖) 呼叫運算。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="0d7cd-384">元素</span><span class="sxs-lookup"><span data-stu-id="0d7cd-384">Elements</span></span>  
  
|<span data-ttu-id="0d7cd-385">元素</span><span class="sxs-lookup"><span data-stu-id="0d7cd-385">Element</span></span>|<span data-ttu-id="0d7cd-386">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-386">Description</span></span>|<span data-ttu-id="0d7cd-387">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="0d7cd-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="0d7cd-388">validate-jwt</span></span>|<span data-ttu-id="0d7cd-389">根元素。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-389">Root element.</span></span>|<span data-ttu-id="0d7cd-390">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-390">Yes</span></span>|  
|<span data-ttu-id="0d7cd-391">audiences</span><span class="sxs-lookup"><span data-stu-id="0d7cd-391">audiences</span></span>|<span data-ttu-id="0d7cd-392">包含可呈現在權杖上之可接受的受眾宣告清單。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="0d7cd-393">如果存在多個受眾值，則會嘗試每個值，直到全部試完 (即表示驗證失敗) 或其中一個值成功為止。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="0d7cd-394">必須指定至少一個受眾。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-394">At least one audience must be specified.</span></span>|<span data-ttu-id="0d7cd-395">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-395">No</span></span>|  
|<span data-ttu-id="0d7cd-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="0d7cd-396">issuer-signing-keys</span></span>|<span data-ttu-id="0d7cd-397">用來驗證已簽署權杖的 Base64 編碼安全性金鑰清單。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="0d7cd-398">如果存在多個安全性金鑰，則會嘗試每個金鑰，直到全部試完 (即表示驗證失敗) 或其中一個金鑰成功 (很適合用於權杖變換) 為止。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="0d7cd-399">金鑰元素具有用來與 `kid` 宣告進行比對的選擇性 `id` 屬性。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="0d7cd-400">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-400">No</span></span>|  
|<span data-ttu-id="0d7cd-401">issuers</span><span class="sxs-lookup"><span data-stu-id="0d7cd-401">issuers</span></span>|<span data-ttu-id="0d7cd-402">可接受之簽發權杖的主體清單。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="0d7cd-403">如果存在多個簽發者值，則會嘗試每個值，直到全部試完 (即表示驗證失敗) 或其中一個值成功為止。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="0d7cd-404">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-404">No</span></span>|  
|<span data-ttu-id="0d7cd-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="0d7cd-405">openid-config</span></span>|<span data-ttu-id="0d7cd-406">此元素用於指定可從中取得簽署金鑰和簽發者之符合規範的 Open ID 設定端點。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="0d7cd-407">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-407">No</span></span>|  
|<span data-ttu-id="0d7cd-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="0d7cd-408">required-claims</span></span>|<span data-ttu-id="0d7cd-409">包含應存在於權杖上才會被視為有效的宣告清單。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="0d7cd-410">當 `match` 屬性設定為 `all` 時，原則中的每個宣告值都必須存在於權杖，才能驗證成功。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="0d7cd-411">當 `match` 屬性設定為 `any` 時，至少一個宣告必須存在於權杖，才能驗證成功。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="0d7cd-412">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-412">No</span></span>|  
|<span data-ttu-id="0d7cd-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="0d7cd-413">zumo-master-key</span></span>|<span data-ttu-id="0d7cd-414">Azure 行動服務所簽發之權杖的主要金鑰</span><span class="sxs-lookup"><span data-stu-id="0d7cd-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="0d7cd-415">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0d7cd-416">屬性</span><span class="sxs-lookup"><span data-stu-id="0d7cd-416">Attributes</span></span>  
  
|<span data-ttu-id="0d7cd-417">名稱</span><span class="sxs-lookup"><span data-stu-id="0d7cd-417">Name</span></span>|<span data-ttu-id="0d7cd-418">說明</span><span class="sxs-lookup"><span data-stu-id="0d7cd-418">Description</span></span>|<span data-ttu-id="0d7cd-419">必要</span><span class="sxs-lookup"><span data-stu-id="0d7cd-419">Required</span></span>|<span data-ttu-id="0d7cd-420">預設值</span><span class="sxs-lookup"><span data-stu-id="0d7cd-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0d7cd-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="0d7cd-421">clock-skew</span></span>|<span data-ttu-id="0d7cd-422">時間範圍。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-422">Timespan.</span></span> <span data-ttu-id="0d7cd-423">如果權杖的到期宣告出現於權杖且超過目前日期 / 時間，則提供些許時間。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="0d7cd-424">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-424">No</span></span>|<span data-ttu-id="0d7cd-425">0 秒</span><span class="sxs-lookup"><span data-stu-id="0d7cd-425">0 seconds</span></span>|  
|<span data-ttu-id="0d7cd-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="0d7cd-426">failed-validation-error-message</span></span>|<span data-ttu-id="0d7cd-427">如果 JWT 未通過驗證，在 HTTP 回應主體中傳回的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="0d7cd-428">此訊息必須正確逸出任何特殊字元。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="0d7cd-429">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-429">No</span></span>|<span data-ttu-id="0d7cd-430">預設錯誤訊息視驗證問題而定，例如「JWT 不存在」。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="0d7cd-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="0d7cd-431">failed-validation-httpcode</span></span>|<span data-ttu-id="0d7cd-432">JWT 未通過驗證時所要傳回的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="0d7cd-433">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-433">No</span></span>|<span data-ttu-id="0d7cd-434">401</span><span class="sxs-lookup"><span data-stu-id="0d7cd-434">401</span></span>|  
|<span data-ttu-id="0d7cd-435">header-name</span><span class="sxs-lookup"><span data-stu-id="0d7cd-435">header-name</span></span>|<span data-ttu-id="0d7cd-436">保留權杖的 HTTP 標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="0d7cd-437">必須指定 `header-name` 或 `query-paremeter-name`；但不能同時指定。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="0d7cd-438">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-438">N/A</span></span>|  
|<span data-ttu-id="0d7cd-439">id</span><span class="sxs-lookup"><span data-stu-id="0d7cd-439">id</span></span>|<span data-ttu-id="0d7cd-440">`key` 元素的 `id` 屬性可讓您指定要與權杖中的 `kid` 宣告 (如果存在) 進行比對的字串，以找出適合用於簽章驗證的金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="0d7cd-441">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-441">No</span></span>|<span data-ttu-id="0d7cd-442">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-442">N/A</span></span>|  
|<span data-ttu-id="0d7cd-443">match</span><span class="sxs-lookup"><span data-stu-id="0d7cd-443">match</span></span>|<span data-ttu-id="0d7cd-444">`claim` 元素的 `match` 屬性可指定原則中的每個宣告值是否都必須存在於權杖，才能驗證成功。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="0d7cd-445">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="0d7cd-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="0d7cd-446">-                          `all` - 原則中的每個宣告值都必須存在於權杖，才能驗證成功。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="0d7cd-447">-                          `any` - 至少一個宣告必須存在於權杖，才能驗證成功。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="0d7cd-448">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-448">No</span></span>|<span data-ttu-id="0d7cd-449">所有</span><span class="sxs-lookup"><span data-stu-id="0d7cd-449">all</span></span>|  
|<span data-ttu-id="0d7cd-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="0d7cd-450">query-paremeter-name</span></span>|<span data-ttu-id="0d7cd-451">保留權杖的查詢參數名稱。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="0d7cd-452">必須指定 `header-name` 或 `query-paremeter-name`；但不能同時指定。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="0d7cd-453">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-453">N/A</span></span>|  
|<span data-ttu-id="0d7cd-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="0d7cd-454">require-expiration-time</span></span>|<span data-ttu-id="0d7cd-455">布林值。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-455">Boolean.</span></span> <span data-ttu-id="0d7cd-456">指定權杖中是否需有逾期宣告。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="0d7cd-457">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-457">No</span></span>|<span data-ttu-id="0d7cd-458">true</span><span class="sxs-lookup"><span data-stu-id="0d7cd-458">true</span></span>|
|<span data-ttu-id="0d7cd-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="0d7cd-459">require-scheme</span></span>|<span data-ttu-id="0d7cd-460">權杖結構描述的名稱，例如"Bearer"。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="0d7cd-461">當已設定此屬性時，原則將會確定指定的結構描述存在於授權標頭值中。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="0d7cd-462">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-462">No</span></span>|<span data-ttu-id="0d7cd-463">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-463">N/A</span></span>|
|<span data-ttu-id="0d7cd-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="0d7cd-464">require-signed-tokens</span></span>|<span data-ttu-id="0d7cd-465">布林值。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-465">Boolean.</span></span> <span data-ttu-id="0d7cd-466">指定是否需要簽署權杖。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="0d7cd-467">否</span><span class="sxs-lookup"><span data-stu-id="0d7cd-467">No</span></span>|<span data-ttu-id="0d7cd-468">true</span><span class="sxs-lookup"><span data-stu-id="0d7cd-468">true</span></span>|  
|<span data-ttu-id="0d7cd-469">url</span><span class="sxs-lookup"><span data-stu-id="0d7cd-469">url</span></span>|<span data-ttu-id="0d7cd-470">可從中取得 Open ID 設定中繼資料的 Open ID 設定端點 URL。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="0d7cd-471">對於 Azure Active Directory，使用下列 URL：`https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` 代替您的目錄租用戶名稱，例如 `contoso.onmicrosoft.com`。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="0d7cd-472">是</span><span class="sxs-lookup"><span data-stu-id="0d7cd-472">Yes</span></span>|<span data-ttu-id="0d7cd-473">N/A</span><span class="sxs-lookup"><span data-stu-id="0d7cd-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0d7cd-474">使用量</span><span class="sxs-lookup"><span data-stu-id="0d7cd-474">Usage</span></span>  
 <span data-ttu-id="0d7cd-475">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0d7cd-476">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="0d7cd-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0d7cd-477">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="0d7cd-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="0d7cd-478">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d7cd-478">Next steps</span></span>
<span data-ttu-id="0d7cd-479">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="0d7cd-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
