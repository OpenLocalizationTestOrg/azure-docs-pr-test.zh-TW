---
title: "Azure API 管理驗證原則 | Microsoft Docs"
description: "了解「Azure API 管理」中可用的驗證原則。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="9153a-103">API 管理驗證原則</span><span class="sxs-lookup"><span data-stu-id="9153a-103">API Management authentication policies</span></span>
<span data-ttu-id="9153a-104">本主題提供下列「API 管理」原則的參考。</span><span class="sxs-lookup"><span data-stu-id="9153a-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="9153a-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="9153a-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="9153a-106"><a name="AuthenticationPolicies"></a> 驗證原則</span><span class="sxs-lookup"><span data-stu-id="9153a-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="9153a-107">[使用基本驗證進行驗證](api-management-authentication-policies.md#Basic) - 使用基本驗證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="9153a-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="9153a-108">[使用用戶端憑證進行驗證](api-management-authentication-policies.md#ClientCertificate) - 使用用戶端憑證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="9153a-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="9153a-109"><a name="Basic"></a> 使用基本驗證進行驗證</span><span class="sxs-lookup"><span data-stu-id="9153a-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="9153a-110">使用 `authentication-basic` 原則以利用「基本」驗證向後端服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9153a-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="9153a-111">此原則會將「HTTP 授權」標頭有效地設定為與此原則中所提供認證對應的值。</span><span class="sxs-lookup"><span data-stu-id="9153a-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="9153a-112">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="9153a-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="9153a-113">範例</span><span class="sxs-lookup"><span data-stu-id="9153a-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="9153a-114">元素</span><span class="sxs-lookup"><span data-stu-id="9153a-114">Elements</span></span>  
  
|<span data-ttu-id="9153a-115">名稱</span><span class="sxs-lookup"><span data-stu-id="9153a-115">Name</span></span>|<span data-ttu-id="9153a-116">說明</span><span class="sxs-lookup"><span data-stu-id="9153a-116">Description</span></span>|<span data-ttu-id="9153a-117">必要</span><span class="sxs-lookup"><span data-stu-id="9153a-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="9153a-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="9153a-118">authentication-basic</span></span>|<span data-ttu-id="9153a-119">根元素。</span><span class="sxs-lookup"><span data-stu-id="9153a-119">Root element.</span></span>|<span data-ttu-id="9153a-120">是</span><span class="sxs-lookup"><span data-stu-id="9153a-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="9153a-121">屬性</span><span class="sxs-lookup"><span data-stu-id="9153a-121">Attributes</span></span>  
  
|<span data-ttu-id="9153a-122">名稱</span><span class="sxs-lookup"><span data-stu-id="9153a-122">Name</span></span>|<span data-ttu-id="9153a-123">說明</span><span class="sxs-lookup"><span data-stu-id="9153a-123">Description</span></span>|<span data-ttu-id="9153a-124">必要</span><span class="sxs-lookup"><span data-stu-id="9153a-124">Required</span></span>|<span data-ttu-id="9153a-125">預設值</span><span class="sxs-lookup"><span data-stu-id="9153a-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="9153a-126">username</span><span class="sxs-lookup"><span data-stu-id="9153a-126">username</span></span>|<span data-ttu-id="9153a-127">指定「基本驗證」認證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="9153a-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="9153a-128">是</span><span class="sxs-lookup"><span data-stu-id="9153a-128">Yes</span></span>|<span data-ttu-id="9153a-129">N/A</span><span class="sxs-lookup"><span data-stu-id="9153a-129">N/A</span></span>|  
|<span data-ttu-id="9153a-130">password</span><span class="sxs-lookup"><span data-stu-id="9153a-130">password</span></span>|<span data-ttu-id="9153a-131">指定「基本驗證」認證的密碼。</span><span class="sxs-lookup"><span data-stu-id="9153a-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="9153a-132">是</span><span class="sxs-lookup"><span data-stu-id="9153a-132">Yes</span></span>|<span data-ttu-id="9153a-133">N/A</span><span class="sxs-lookup"><span data-stu-id="9153a-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="9153a-134">使用量</span><span class="sxs-lookup"><span data-stu-id="9153a-134">Usage</span></span>  
 <span data-ttu-id="9153a-135">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="9153a-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="9153a-136">**原則區段︰**inbound</span><span class="sxs-lookup"><span data-stu-id="9153a-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="9153a-137">**原則範圍︰**API</span><span class="sxs-lookup"><span data-stu-id="9153a-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="9153a-138"><a name="ClientCertificate"></a> 使用用戶端憑證進行驗證</span><span class="sxs-lookup"><span data-stu-id="9153a-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="9153a-139">使用 `authentication-certificate` 原則以利用用戶端憑證向後端服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9153a-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="9153a-140">憑證必須先[安裝到 API 管理中](http://go.microsoft.com/fwlink/?LinkID=511599)且會以其指紋作為識別。</span><span class="sxs-lookup"><span data-stu-id="9153a-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="9153a-141">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="9153a-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="9153a-142">範例</span><span class="sxs-lookup"><span data-stu-id="9153a-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="9153a-143">元素</span><span class="sxs-lookup"><span data-stu-id="9153a-143">Elements</span></span>  
  
|<span data-ttu-id="9153a-144">名稱</span><span class="sxs-lookup"><span data-stu-id="9153a-144">Name</span></span>|<span data-ttu-id="9153a-145">說明</span><span class="sxs-lookup"><span data-stu-id="9153a-145">Description</span></span>|<span data-ttu-id="9153a-146">必要</span><span class="sxs-lookup"><span data-stu-id="9153a-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="9153a-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="9153a-147">authentication-certificate</span></span>|<span data-ttu-id="9153a-148">根元素。</span><span class="sxs-lookup"><span data-stu-id="9153a-148">Root element.</span></span>|<span data-ttu-id="9153a-149">是</span><span class="sxs-lookup"><span data-stu-id="9153a-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="9153a-150">屬性</span><span class="sxs-lookup"><span data-stu-id="9153a-150">Attributes</span></span>  
  
|<span data-ttu-id="9153a-151">名稱</span><span class="sxs-lookup"><span data-stu-id="9153a-151">Name</span></span>|<span data-ttu-id="9153a-152">說明</span><span class="sxs-lookup"><span data-stu-id="9153a-152">Description</span></span>|<span data-ttu-id="9153a-153">必要</span><span class="sxs-lookup"><span data-stu-id="9153a-153">Required</span></span>|<span data-ttu-id="9153a-154">預設值</span><span class="sxs-lookup"><span data-stu-id="9153a-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="9153a-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="9153a-155">thumbprint</span></span>|<span data-ttu-id="9153a-156">用戶端憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="9153a-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="9153a-157">是</span><span class="sxs-lookup"><span data-stu-id="9153a-157">Yes</span></span>|<span data-ttu-id="9153a-158">N/A</span><span class="sxs-lookup"><span data-stu-id="9153a-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="9153a-159">使用量</span><span class="sxs-lookup"><span data-stu-id="9153a-159">Usage</span></span>  
 <span data-ttu-id="9153a-160">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="9153a-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="9153a-161">**原則區段︰**inbound</span><span class="sxs-lookup"><span data-stu-id="9153a-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="9153a-162">**原則範圍︰**API</span><span class="sxs-lookup"><span data-stu-id="9153a-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="9153a-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9153a-163">Next steps</span></span>
<span data-ttu-id="9153a-164">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="9153a-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  