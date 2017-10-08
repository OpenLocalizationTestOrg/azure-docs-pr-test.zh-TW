---
title: "aaaAzure API 管理驗證原則 |Microsoft 文件"
description: "深入了解 hello 可在 Azure API 管理中使用的驗證原則。"
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
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="b98d2-103">API 管理驗證原則</span><span class="sxs-lookup"><span data-stu-id="b98d2-103">API Management authentication policies</span></span>
<span data-ttu-id="b98d2-104">本主題提供下列 API 管理原則的 hello 的參考。</span><span class="sxs-lookup"><span data-stu-id="b98d2-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="b98d2-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="b98d2-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="b98d2-106"><a name="AuthenticationPolicies"></a> 驗證原則</span><span class="sxs-lookup"><span data-stu-id="b98d2-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="b98d2-107">[使用基本驗證進行驗證](api-management-authentication-policies.md#Basic) - 使用基本驗證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="b98d2-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="b98d2-108">[使用用戶端憑證進行驗證](api-management-authentication-policies.md#ClientCertificate) - 使用用戶端憑證來驗證後端服務。</span><span class="sxs-lookup"><span data-stu-id="b98d2-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="b98d2-109"><a name="Basic"></a> 使用基本驗證進行驗證</span><span class="sxs-lookup"><span data-stu-id="b98d2-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="b98d2-110">使用 hello`authentication-basic`原則 tooauthenticate 使用基本驗證的後端服務。</span><span class="sxs-lookup"><span data-stu-id="b98d2-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="b98d2-111">此原則實際上是設定 hello HTTP 授權標頭 toohello 值 hello 原則中提供對應 toohello 認證。</span><span class="sxs-lookup"><span data-stu-id="b98d2-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b98d2-112">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="b98d2-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="b98d2-113">範例</span><span class="sxs-lookup"><span data-stu-id="b98d2-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="b98d2-114">元素</span><span class="sxs-lookup"><span data-stu-id="b98d2-114">Elements</span></span>  
  
|<span data-ttu-id="b98d2-115">名稱</span><span class="sxs-lookup"><span data-stu-id="b98d2-115">Name</span></span>|<span data-ttu-id="b98d2-116">說明</span><span class="sxs-lookup"><span data-stu-id="b98d2-116">Description</span></span>|<span data-ttu-id="b98d2-117">必要</span><span class="sxs-lookup"><span data-stu-id="b98d2-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b98d2-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="b98d2-118">authentication-basic</span></span>|<span data-ttu-id="b98d2-119">根元素。</span><span class="sxs-lookup"><span data-stu-id="b98d2-119">Root element.</span></span>|<span data-ttu-id="b98d2-120">是</span><span class="sxs-lookup"><span data-stu-id="b98d2-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b98d2-121">屬性</span><span class="sxs-lookup"><span data-stu-id="b98d2-121">Attributes</span></span>  
  
|<span data-ttu-id="b98d2-122">名稱</span><span class="sxs-lookup"><span data-stu-id="b98d2-122">Name</span></span>|<span data-ttu-id="b98d2-123">說明</span><span class="sxs-lookup"><span data-stu-id="b98d2-123">Description</span></span>|<span data-ttu-id="b98d2-124">必要</span><span class="sxs-lookup"><span data-stu-id="b98d2-124">Required</span></span>|<span data-ttu-id="b98d2-125">預設值</span><span class="sxs-lookup"><span data-stu-id="b98d2-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b98d2-126">username</span><span class="sxs-lookup"><span data-stu-id="b98d2-126">username</span></span>|<span data-ttu-id="b98d2-127">指定 hello 的 hello 基本認證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b98d2-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="b98d2-128">是</span><span class="sxs-lookup"><span data-stu-id="b98d2-128">Yes</span></span>|<span data-ttu-id="b98d2-129">N/A</span><span class="sxs-lookup"><span data-stu-id="b98d2-129">N/A</span></span>|  
|<span data-ttu-id="b98d2-130">password</span><span class="sxs-lookup"><span data-stu-id="b98d2-130">password</span></span>|<span data-ttu-id="b98d2-131">指定 hello 的 hello 基本認證的密碼。</span><span class="sxs-lookup"><span data-stu-id="b98d2-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="b98d2-132">是</span><span class="sxs-lookup"><span data-stu-id="b98d2-132">Yes</span></span>|<span data-ttu-id="b98d2-133">N/A</span><span class="sxs-lookup"><span data-stu-id="b98d2-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b98d2-134">使用量</span><span class="sxs-lookup"><span data-stu-id="b98d2-134">Usage</span></span>  
 <span data-ttu-id="b98d2-135">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="b98d2-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b98d2-136">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="b98d2-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b98d2-137">**原則範圍︰**API</span><span class="sxs-lookup"><span data-stu-id="b98d2-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="b98d2-138"><a name="ClientCertificate"></a> 使用用戶端憑證進行驗證</span><span class="sxs-lookup"><span data-stu-id="b98d2-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="b98d2-139">使用 hello`authentication-certificate`原則 tooauthenticate 與後端服務使用用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="b98d2-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="b98d2-140">hello 憑證必須 toobe[安裝到 API 管理](http://go.microsoft.com/fwlink/?LinkID=511599)第一次，並由其指紋識別。</span><span class="sxs-lookup"><span data-stu-id="b98d2-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b98d2-141">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="b98d2-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="b98d2-142">範例</span><span class="sxs-lookup"><span data-stu-id="b98d2-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="b98d2-143">元素</span><span class="sxs-lookup"><span data-stu-id="b98d2-143">Elements</span></span>  
  
|<span data-ttu-id="b98d2-144">名稱</span><span class="sxs-lookup"><span data-stu-id="b98d2-144">Name</span></span>|<span data-ttu-id="b98d2-145">說明</span><span class="sxs-lookup"><span data-stu-id="b98d2-145">Description</span></span>|<span data-ttu-id="b98d2-146">必要</span><span class="sxs-lookup"><span data-stu-id="b98d2-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b98d2-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="b98d2-147">authentication-certificate</span></span>|<span data-ttu-id="b98d2-148">根元素。</span><span class="sxs-lookup"><span data-stu-id="b98d2-148">Root element.</span></span>|<span data-ttu-id="b98d2-149">是</span><span class="sxs-lookup"><span data-stu-id="b98d2-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b98d2-150">屬性</span><span class="sxs-lookup"><span data-stu-id="b98d2-150">Attributes</span></span>  
  
|<span data-ttu-id="b98d2-151">名稱</span><span class="sxs-lookup"><span data-stu-id="b98d2-151">Name</span></span>|<span data-ttu-id="b98d2-152">說明</span><span class="sxs-lookup"><span data-stu-id="b98d2-152">Description</span></span>|<span data-ttu-id="b98d2-153">必要</span><span class="sxs-lookup"><span data-stu-id="b98d2-153">Required</span></span>|<span data-ttu-id="b98d2-154">預設值</span><span class="sxs-lookup"><span data-stu-id="b98d2-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b98d2-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="b98d2-155">thumbprint</span></span>|<span data-ttu-id="b98d2-156">hello hello 用戶端憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="b98d2-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="b98d2-157">是</span><span class="sxs-lookup"><span data-stu-id="b98d2-157">Yes</span></span>|<span data-ttu-id="b98d2-158">N/A</span><span class="sxs-lookup"><span data-stu-id="b98d2-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b98d2-159">使用量</span><span class="sxs-lookup"><span data-stu-id="b98d2-159">Usage</span></span>  
 <span data-ttu-id="b98d2-160">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="b98d2-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b98d2-161">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="b98d2-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b98d2-162">**原則範圍︰**API</span><span class="sxs-lookup"><span data-stu-id="b98d2-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="b98d2-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b98d2-163">Next steps</span></span>
<span data-ttu-id="b98d2-164">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="b98d2-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  