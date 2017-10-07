---
title: "aaaAzure API 管理跨網域原則 |Microsoft 文件"
description: "深入了解 hello 跨網域原則可在 Azure API 管理中使用。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="0499f-103">API 管理跨網域原則</span><span class="sxs-lookup"><span data-stu-id="0499f-103">API Management cross domain policies</span></span>
<span data-ttu-id="0499f-104">本主題提供下列 API 管理原則的 hello 的參考。</span><span class="sxs-lookup"><span data-stu-id="0499f-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="0499f-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="0499f-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="0499f-106"><a name="CrossDomainPolicies"></a>跨網域原則</span><span class="sxs-lookup"><span data-stu-id="0499f-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="0499f-107">[允許跨網域呼叫](api-management-cross-domain-policies.md#AllowCrossDomainCalls)-從 Adobe Flash 和 Microsoft Silverlight 的瀏覽器型用戶端，讓 hello API 存取。</span><span class="sxs-lookup"><span data-stu-id="0499f-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="0499f-108">[CORS](api-management-cross-domain-policies.md#CORS) -將跨原始資源共用 (CORS) 支援 tooan 作業或 API tooallow 跨網域呼叫從瀏覽器型用戶端。</span><span class="sxs-lookup"><span data-stu-id="0499f-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="0499f-109">[JSONP](api-management-cross-domain-policies.md#JSONP) -將 JSON padding (JSONP) 支援 tooan 作業，或從 JavaScript 瀏覽器為基礎的用戶端的應用程式開發介面 tooallow 跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="0499f-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="0499f-110"><a name="AllowCrossDomainCalls"></a>允許跨網域呼叫</span><span class="sxs-lookup"><span data-stu-id="0499f-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="0499f-111">使用 hello`cross-domain`原則 toomake hello 從 Adobe Flash 和 Microsoft Silverlight 的瀏覽器型用戶端可存取的 API。</span><span class="sxs-lookup"><span data-stu-id="0499f-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0499f-112">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0499f-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="0499f-113">範例</span><span class="sxs-lookup"><span data-stu-id="0499f-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="0499f-114">元素</span><span class="sxs-lookup"><span data-stu-id="0499f-114">Elements</span></span>  
  
|<span data-ttu-id="0499f-115">名稱</span><span class="sxs-lookup"><span data-stu-id="0499f-115">Name</span></span>|<span data-ttu-id="0499f-116">說明</span><span class="sxs-lookup"><span data-stu-id="0499f-116">Description</span></span>|<span data-ttu-id="0499f-117">必要</span><span class="sxs-lookup"><span data-stu-id="0499f-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0499f-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="0499f-118">cross-domain</span></span>|<span data-ttu-id="0499f-119">根元素。</span><span class="sxs-lookup"><span data-stu-id="0499f-119">Root element.</span></span> <span data-ttu-id="0499f-120">子元素必須符合 toohello [Adobe 跨網域原則檔案規格](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)。</span><span class="sxs-lookup"><span data-stu-id="0499f-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="0499f-121">是</span><span class="sxs-lookup"><span data-stu-id="0499f-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0499f-122">使用量</span><span class="sxs-lookup"><span data-stu-id="0499f-122">Usage</span></span>  
 <span data-ttu-id="0499f-123">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0499f-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0499f-124">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="0499f-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0499f-125">**原則範圍︰**全域</span><span class="sxs-lookup"><span data-stu-id="0499f-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="0499f-126"><a name="CORS"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="0499f-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="0499f-127">hello`cors`原則新增跨原始資源共用 (CORS) 支援 tooan 作業或 API tooallow 跨網域呼叫從瀏覽器型用戶端。</span><span class="sxs-lookup"><span data-stu-id="0499f-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="0499f-128">CORS 允許瀏覽器和伺服器 toointeract，並判斷 tooallow 特定的跨原始要求 （亦即 XMLHttpRequests 呼叫從網頁 tooother 網域上的 JavaScript 進行）。</span><span class="sxs-lookup"><span data-stu-id="0499f-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="0499f-129">這比只允許相同原始來源的要求更有彈性，也比允許所有跨原始來源的要求更安全。</span><span class="sxs-lookup"><span data-stu-id="0499f-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0499f-130">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0499f-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="0499f-131">範例</span><span class="sxs-lookup"><span data-stu-id="0499f-131">Example</span></span>  
 <span data-ttu-id="0499f-132">此範例示範如何 toosupport 事前要求，例如含有自訂標頭或 GET 和 POST 以外的方法。</span><span class="sxs-lookup"><span data-stu-id="0499f-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="0499f-133">toosupport 自訂標頭和其他 HTTP 動詞命令，使用 hello`allowed-methods`和`allowed-headers`區段 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="0499f-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="0499f-134">元素</span><span class="sxs-lookup"><span data-stu-id="0499f-134">Elements</span></span>  
  
|<span data-ttu-id="0499f-135">名稱</span><span class="sxs-lookup"><span data-stu-id="0499f-135">Name</span></span>|<span data-ttu-id="0499f-136">說明</span><span class="sxs-lookup"><span data-stu-id="0499f-136">Description</span></span>|<span data-ttu-id="0499f-137">必要</span><span class="sxs-lookup"><span data-stu-id="0499f-137">Required</span></span>|<span data-ttu-id="0499f-138">預設值</span><span class="sxs-lookup"><span data-stu-id="0499f-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0499f-139">cors</span><span class="sxs-lookup"><span data-stu-id="0499f-139">cors</span></span>|<span data-ttu-id="0499f-140">根元素。</span><span class="sxs-lookup"><span data-stu-id="0499f-140">Root element.</span></span>|<span data-ttu-id="0499f-141">是</span><span class="sxs-lookup"><span data-stu-id="0499f-141">Yes</span></span>|<span data-ttu-id="0499f-142">N/A</span><span class="sxs-lookup"><span data-stu-id="0499f-142">N/A</span></span>|  
|<span data-ttu-id="0499f-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="0499f-143">allowed-origins</span></span>|<span data-ttu-id="0499f-144">包含`origin`描述 hello 允許出處跨網域要求的項目。</span><span class="sxs-lookup"><span data-stu-id="0499f-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="0499f-145">`allowed-origins`可以包含單一`origin`項目，指定`*`tooallow 任何來源，或者一個或多個`origin`包含 URI 的項目。</span><span class="sxs-lookup"><span data-stu-id="0499f-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="0499f-146">是</span><span class="sxs-lookup"><span data-stu-id="0499f-146">Yes</span></span>|<span data-ttu-id="0499f-147">N/A</span><span class="sxs-lookup"><span data-stu-id="0499f-147">N/A</span></span>|  
|<span data-ttu-id="0499f-148">來源</span><span class="sxs-lookup"><span data-stu-id="0499f-148">origin</span></span>|<span data-ttu-id="0499f-149">hello 值可以是`*`tooallow 所有來源或指定單一來源的 URI。</span><span class="sxs-lookup"><span data-stu-id="0499f-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="0499f-150">hello URI 必須包含配置、 主機和連接埠。</span><span class="sxs-lookup"><span data-stu-id="0499f-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="0499f-151">是</span><span class="sxs-lookup"><span data-stu-id="0499f-151">Yes</span></span>|<span data-ttu-id="0499f-152">如果 URI 中省略 hello 連接埠，則連接埠 80 用於 HTTP 和 HTTPS 使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="0499f-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="0499f-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="0499f-153">allowed-methods</span></span>|<span data-ttu-id="0499f-154">如果允許 GET 或 POST 以外的方法，則需要此元素。</span><span class="sxs-lookup"><span data-stu-id="0499f-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="0499f-155">包含`method`指定 hello 支援 HTTP 指令動詞的項目。</span><span class="sxs-lookup"><span data-stu-id="0499f-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="0499f-156">否</span><span class="sxs-lookup"><span data-stu-id="0499f-156">No</span></span>|<span data-ttu-id="0499f-157">如果這個區段不存在，則會支援 GET 和 POST。</span><span class="sxs-lookup"><span data-stu-id="0499f-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="0499f-158">method</span><span class="sxs-lookup"><span data-stu-id="0499f-158">method</span></span>|<span data-ttu-id="0499f-159">指定 HTTP 動詞命令。</span><span class="sxs-lookup"><span data-stu-id="0499f-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="0499f-160">至少一個`method`項目是必要的如果 hello`allowed-methods`區段已存在。</span><span class="sxs-lookup"><span data-stu-id="0499f-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="0499f-161">N/A</span><span class="sxs-lookup"><span data-stu-id="0499f-161">N/A</span></span>|  
|<span data-ttu-id="0499f-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="0499f-162">allowed-headers</span></span>|<span data-ttu-id="0499f-163">這個項目包含`header`元素，指定可以在 hello 要求中包含的 hello 標頭的名稱。</span><span class="sxs-lookup"><span data-stu-id="0499f-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="0499f-164">否</span><span class="sxs-lookup"><span data-stu-id="0499f-164">No</span></span>|<span data-ttu-id="0499f-165">N/A</span><span class="sxs-lookup"><span data-stu-id="0499f-165">N/A</span></span>|  
|<span data-ttu-id="0499f-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="0499f-166">expose-headers</span></span>|<span data-ttu-id="0499f-167">這個項目包含`header`元素，指定可供存取 hello 用戶端 hello 標頭的名稱。</span><span class="sxs-lookup"><span data-stu-id="0499f-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="0499f-168">否</span><span class="sxs-lookup"><span data-stu-id="0499f-168">No</span></span>|<span data-ttu-id="0499f-169">N/A</span><span class="sxs-lookup"><span data-stu-id="0499f-169">N/A</span></span>|  
|<span data-ttu-id="0499f-170">頁首</span><span class="sxs-lookup"><span data-stu-id="0499f-170">header</span></span>|<span data-ttu-id="0499f-171">指定標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="0499f-171">Specifies a header name.</span></span>|<span data-ttu-id="0499f-172">至少一個`header`項目所需要的是`allowed-headers`或`expose-headers`如果 hello 區段存在。</span><span class="sxs-lookup"><span data-stu-id="0499f-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="0499f-173">N/A</span><span class="sxs-lookup"><span data-stu-id="0499f-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0499f-174">屬性</span><span class="sxs-lookup"><span data-stu-id="0499f-174">Attributes</span></span>  
  
|<span data-ttu-id="0499f-175">名稱</span><span class="sxs-lookup"><span data-stu-id="0499f-175">Name</span></span>|<span data-ttu-id="0499f-176">說明</span><span class="sxs-lookup"><span data-stu-id="0499f-176">Description</span></span>|<span data-ttu-id="0499f-177">必要</span><span class="sxs-lookup"><span data-stu-id="0499f-177">Required</span></span>|<span data-ttu-id="0499f-178">預設值</span><span class="sxs-lookup"><span data-stu-id="0499f-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0499f-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="0499f-179">allow-credentials</span></span>|<span data-ttu-id="0499f-180">hello `Access-Control-Allow-Credentials` hello 預檢回應的標頭會設定 toohello 值，這個屬性，並影響中跨網域要求的用戶端 hello 能力 toosubmit 認證。</span><span class="sxs-lookup"><span data-stu-id="0499f-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="0499f-181">否</span><span class="sxs-lookup"><span data-stu-id="0499f-181">No</span></span>|<span data-ttu-id="0499f-182">false</span><span class="sxs-lookup"><span data-stu-id="0499f-182">false</span></span>|  
|<span data-ttu-id="0499f-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="0499f-183">preflight-result-max-age</span></span>|<span data-ttu-id="0499f-184">hello `Access-Control-Max-Age` hello 預檢回應的標頭會設定 toohello 值，這個屬性，並會影響 hello 使用者代理程式的能力 toocache 事前回應。</span><span class="sxs-lookup"><span data-stu-id="0499f-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="0499f-185">否</span><span class="sxs-lookup"><span data-stu-id="0499f-185">No</span></span>|<span data-ttu-id="0499f-186">0</span><span class="sxs-lookup"><span data-stu-id="0499f-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0499f-187">使用量</span><span class="sxs-lookup"><span data-stu-id="0499f-187">Usage</span></span>  
 <span data-ttu-id="0499f-188">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0499f-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0499f-189">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="0499f-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0499f-190">**原則範圍︰**API、作業</span><span class="sxs-lookup"><span data-stu-id="0499f-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="0499f-191"><a name="JSONP"></a>JSONP</span><span class="sxs-lookup"><span data-stu-id="0499f-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="0499f-192">hello`jsonp`原則新增 JSON 搭配填補 (JSONP) 支援 tooan 操作或從 JavaScript 瀏覽器為基礎的用戶端應用程式開發介面 tooallow 跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="0499f-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="0499f-193">JSONP 是 JavaScript 程式 toorequest 資料位於不同的網域中，從伺服器中使用的方法。</span><span class="sxs-lookup"><span data-stu-id="0499f-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="0499f-194">JSONP 不強制執行大部分的網頁瀏覽器位置存取 tooweb 網頁必須在 hello hello 限制相同的網域。</span><span class="sxs-lookup"><span data-stu-id="0499f-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0499f-195">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="0499f-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="0499f-196">範例</span><span class="sxs-lookup"><span data-stu-id="0499f-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="0499f-197">如果您呼叫 hello 方法沒有 hello 回呼參數？ cb = XXX，則會傳回單純 JSON （無函數呼叫包裝函式）。</span><span class="sxs-lookup"><span data-stu-id="0499f-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="0499f-198">如果您將加入 hello 回呼參數`?cb=XXX`則會傳回 JSONP 結果，包裝 hello 原始 JSON 結果周圍像 hello 回呼函式`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="0499f-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="0499f-199">元素</span><span class="sxs-lookup"><span data-stu-id="0499f-199">Elements</span></span>  
  
|<span data-ttu-id="0499f-200">名稱</span><span class="sxs-lookup"><span data-stu-id="0499f-200">Name</span></span>|<span data-ttu-id="0499f-201">說明</span><span class="sxs-lookup"><span data-stu-id="0499f-201">Description</span></span>|<span data-ttu-id="0499f-202">必要</span><span class="sxs-lookup"><span data-stu-id="0499f-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0499f-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="0499f-203">jsonp</span></span>|<span data-ttu-id="0499f-204">根元素。</span><span class="sxs-lookup"><span data-stu-id="0499f-204">Root element.</span></span>|<span data-ttu-id="0499f-205">是</span><span class="sxs-lookup"><span data-stu-id="0499f-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0499f-206">屬性</span><span class="sxs-lookup"><span data-stu-id="0499f-206">Attributes</span></span>  
  
|<span data-ttu-id="0499f-207">名稱</span><span class="sxs-lookup"><span data-stu-id="0499f-207">Name</span></span>|<span data-ttu-id="0499f-208">說明</span><span class="sxs-lookup"><span data-stu-id="0499f-208">Description</span></span>|<span data-ttu-id="0499f-209">必要</span><span class="sxs-lookup"><span data-stu-id="0499f-209">Required</span></span>|<span data-ttu-id="0499f-210">預設值</span><span class="sxs-lookup"><span data-stu-id="0499f-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0499f-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="0499f-211">callback-parameter-name</span></span>|<span data-ttu-id="0499f-212">hello 跨網域 JavaScript 函式呼叫前面加上 hello hello 函式所在位置的完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="0499f-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="0499f-213">是</span><span class="sxs-lookup"><span data-stu-id="0499f-213">Yes</span></span>|<span data-ttu-id="0499f-214">N/A</span><span class="sxs-lookup"><span data-stu-id="0499f-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0499f-215">使用量</span><span class="sxs-lookup"><span data-stu-id="0499f-215">Usage</span></span>  
 <span data-ttu-id="0499f-216">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="0499f-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0499f-217">**原則區段︰**輸出</span><span class="sxs-lookup"><span data-stu-id="0499f-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="0499f-218">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="0499f-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="0499f-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0499f-219">Next steps</span></span>
<span data-ttu-id="0499f-220">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="0499f-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  