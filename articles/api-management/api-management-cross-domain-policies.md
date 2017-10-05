---
title: "Azure API 管理跨網域原則 | Microsoft Docs"
description: "了解可在 Azure API 管理中使用的跨網域原則。"
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
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="9e319-103">API 管理跨網域原則</span><span class="sxs-lookup"><span data-stu-id="9e319-103">API Management cross domain policies</span></span>
<span data-ttu-id="9e319-104">本主題提供下列 API 管理原則的參考。</span><span class="sxs-lookup"><span data-stu-id="9e319-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="9e319-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="9e319-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="9e319-106"><a name="CrossDomainPolicies"></a>跨網域原則</span><span class="sxs-lookup"><span data-stu-id="9e319-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="9e319-107">[允許跨網域呼叫](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - 將 API 設為可供 Adobe Flash 和 Microsoft Silverlight 瀏覽器型用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="9e319-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="9e319-108">[CORS](api-management-cross-domain-policies.md#CORS) - 將跨原始來源資源分享 (CORS) 支援加入至操作或 API，以允許來自瀏覽器型用戶端的跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="9e319-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="9e319-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - 將 JSON 與補充的 (JSONP) 支援加入至操作或 API，以允許來自 JavaScript 瀏覽器型用戶端的跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="9e319-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="9e319-110"><a name="AllowCrossDomainCalls"></a>允許跨網域呼叫</span><span class="sxs-lookup"><span data-stu-id="9e319-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="9e319-111">使用 `cross-domain` 原則以將 API 設為可供 Adobe Flash 和 Microsoft Silverlight 瀏覽器型用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="9e319-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="9e319-112">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="9e319-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="9e319-113">範例</span><span class="sxs-lookup"><span data-stu-id="9e319-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="9e319-114">元素</span><span class="sxs-lookup"><span data-stu-id="9e319-114">Elements</span></span>  
  
|<span data-ttu-id="9e319-115">名稱</span><span class="sxs-lookup"><span data-stu-id="9e319-115">Name</span></span>|<span data-ttu-id="9e319-116">說明</span><span class="sxs-lookup"><span data-stu-id="9e319-116">Description</span></span>|<span data-ttu-id="9e319-117">必要</span><span class="sxs-lookup"><span data-stu-id="9e319-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="9e319-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="9e319-118">cross-domain</span></span>|<span data-ttu-id="9e319-119">根元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-119">Root element.</span></span> <span data-ttu-id="9e319-120">子元素必須符合 [Adobe 跨網域原則檔案規格](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)。</span><span class="sxs-lookup"><span data-stu-id="9e319-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="9e319-121">是</span><span class="sxs-lookup"><span data-stu-id="9e319-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="9e319-122">使用量</span><span class="sxs-lookup"><span data-stu-id="9e319-122">Usage</span></span>  
 <span data-ttu-id="9e319-123">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="9e319-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="9e319-124">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="9e319-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="9e319-125">**原則範圍︰**全域</span><span class="sxs-lookup"><span data-stu-id="9e319-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="9e319-126"><a name="CORS"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="9e319-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="9e319-127">`cors` 原則會將跨原始來源資源分享 (CORS) 支援加入至操作或 API，以允許來自瀏覽器型用戶端的跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="9e319-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="9e319-128">CORS 可讓瀏覽器和伺服器互動，以決定是否允許特定的跨原始來源要求 (例如，從網頁上的 JavaScript 對其他網域提出的 XMLHttpRequests 呼叫)。</span><span class="sxs-lookup"><span data-stu-id="9e319-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="9e319-129">這比只允許相同原始來源的要求更有彈性，也比允許所有跨原始來源的要求更安全。</span><span class="sxs-lookup"><span data-stu-id="9e319-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="9e319-130">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="9e319-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="9e319-131">範例</span><span class="sxs-lookup"><span data-stu-id="9e319-131">Example</span></span>  
 <span data-ttu-id="9e319-132">此範例示範如何支援事前要求，例如具有自訂標頭或 GET 和 POST 以外方法的要求。</span><span class="sxs-lookup"><span data-stu-id="9e319-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="9e319-133">若要支援自訂標頭和其他 HTTP 動詞命令，請使用 `allowed-methods` 和 `allowed-headers` 區段，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="9e319-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="9e319-134">元素</span><span class="sxs-lookup"><span data-stu-id="9e319-134">Elements</span></span>  
  
|<span data-ttu-id="9e319-135">名稱</span><span class="sxs-lookup"><span data-stu-id="9e319-135">Name</span></span>|<span data-ttu-id="9e319-136">說明</span><span class="sxs-lookup"><span data-stu-id="9e319-136">Description</span></span>|<span data-ttu-id="9e319-137">必要</span><span class="sxs-lookup"><span data-stu-id="9e319-137">Required</span></span>|<span data-ttu-id="9e319-138">預設值</span><span class="sxs-lookup"><span data-stu-id="9e319-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="9e319-139">cors</span><span class="sxs-lookup"><span data-stu-id="9e319-139">cors</span></span>|<span data-ttu-id="9e319-140">根元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-140">Root element.</span></span>|<span data-ttu-id="9e319-141">是</span><span class="sxs-lookup"><span data-stu-id="9e319-141">Yes</span></span>|<span data-ttu-id="9e319-142">N/A</span><span class="sxs-lookup"><span data-stu-id="9e319-142">N/A</span></span>|  
|<span data-ttu-id="9e319-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="9e319-143">allowed-origins</span></span>|<span data-ttu-id="9e319-144">包含可說明跨網域要求之允許來源的 `origin` 元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="9e319-145">`allowed-origins` 可包含指定了 `*` 以允許任何來源的單一 `origin` 元素，或一或多個包含 URI 的 `origin` 元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="9e319-146">是</span><span class="sxs-lookup"><span data-stu-id="9e319-146">Yes</span></span>|<span data-ttu-id="9e319-147">N/A</span><span class="sxs-lookup"><span data-stu-id="9e319-147">N/A</span></span>|  
|<span data-ttu-id="9e319-148">來源</span><span class="sxs-lookup"><span data-stu-id="9e319-148">origin</span></span>|<span data-ttu-id="9e319-149">值可以是 `*` 以允許所有來源，或是 URI 以指定單一來源。</span><span class="sxs-lookup"><span data-stu-id="9e319-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="9e319-150">URI 必須包含配置、主機和連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e319-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="9e319-151">是</span><span class="sxs-lookup"><span data-stu-id="9e319-151">Yes</span></span>|<span data-ttu-id="9e319-152">如果 URI 中省略了連接埠，則會將連接埠 80 用於 HTTP，將連接埠 443 用於 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="9e319-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="9e319-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="9e319-153">allowed-methods</span></span>|<span data-ttu-id="9e319-154">如果允許 GET 或 POST 以外的方法，則需要此元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="9e319-155">包含指定了所支援 HTTP 動詞命令的 `method` 元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="9e319-156">否</span><span class="sxs-lookup"><span data-stu-id="9e319-156">No</span></span>|<span data-ttu-id="9e319-157">如果這個區段不存在，則會支援 GET 和 POST。</span><span class="sxs-lookup"><span data-stu-id="9e319-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="9e319-158">method</span><span class="sxs-lookup"><span data-stu-id="9e319-158">method</span></span>|<span data-ttu-id="9e319-159">指定 HTTP 動詞命令。</span><span class="sxs-lookup"><span data-stu-id="9e319-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="9e319-160">如果 `allowed-methods` 區段存在，則需要至少一個 `method` 元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="9e319-161">N/A</span><span class="sxs-lookup"><span data-stu-id="9e319-161">N/A</span></span>|  
|<span data-ttu-id="9e319-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="9e319-162">allowed-headers</span></span>|<span data-ttu-id="9e319-163">此元素包含指定了可包含在要求中之標頭名稱的 `header` 元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="9e319-164">否</span><span class="sxs-lookup"><span data-stu-id="9e319-164">No</span></span>|<span data-ttu-id="9e319-165">N/A</span><span class="sxs-lookup"><span data-stu-id="9e319-165">N/A</span></span>|  
|<span data-ttu-id="9e319-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="9e319-166">expose-headers</span></span>|<span data-ttu-id="9e319-167">此元素包含指定了可供用戶端存取之標頭名稱的 `header` 元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="9e319-168">否</span><span class="sxs-lookup"><span data-stu-id="9e319-168">No</span></span>|<span data-ttu-id="9e319-169">N/A</span><span class="sxs-lookup"><span data-stu-id="9e319-169">N/A</span></span>|  
|<span data-ttu-id="9e319-170">頁首</span><span class="sxs-lookup"><span data-stu-id="9e319-170">header</span></span>|<span data-ttu-id="9e319-171">指定標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="9e319-171">Specifies a header name.</span></span>|<span data-ttu-id="9e319-172">如果 `allowed-headers` 或 `expose-headers` 區段存在，則該區段中需要至少一個 `header` 元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="9e319-173">N/A</span><span class="sxs-lookup"><span data-stu-id="9e319-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="9e319-174">屬性</span><span class="sxs-lookup"><span data-stu-id="9e319-174">Attributes</span></span>  
  
|<span data-ttu-id="9e319-175">名稱</span><span class="sxs-lookup"><span data-stu-id="9e319-175">Name</span></span>|<span data-ttu-id="9e319-176">說明</span><span class="sxs-lookup"><span data-stu-id="9e319-176">Description</span></span>|<span data-ttu-id="9e319-177">必要</span><span class="sxs-lookup"><span data-stu-id="9e319-177">Required</span></span>|<span data-ttu-id="9e319-178">預設值</span><span class="sxs-lookup"><span data-stu-id="9e319-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="9e319-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="9e319-179">allow-credentials</span></span>|<span data-ttu-id="9e319-180">事前回應中的 `Access-Control-Allow-Credentials` 標頭會設定為這個屬性的值，並影響用戶端是否能夠在跨網域要求中提交認證。</span><span class="sxs-lookup"><span data-stu-id="9e319-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="9e319-181">否</span><span class="sxs-lookup"><span data-stu-id="9e319-181">No</span></span>|<span data-ttu-id="9e319-182">false</span><span class="sxs-lookup"><span data-stu-id="9e319-182">false</span></span>|  
|<span data-ttu-id="9e319-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="9e319-183">preflight-result-max-age</span></span>|<span data-ttu-id="9e319-184">事前回應中的 `Access-Control-Max-Age` 標頭會設定為這個屬性的值，並影響使用者代理程式是否能夠快取事前回應。</span><span class="sxs-lookup"><span data-stu-id="9e319-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="9e319-185">否</span><span class="sxs-lookup"><span data-stu-id="9e319-185">No</span></span>|<span data-ttu-id="9e319-186">0</span><span class="sxs-lookup"><span data-stu-id="9e319-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="9e319-187">使用量</span><span class="sxs-lookup"><span data-stu-id="9e319-187">Usage</span></span>  
 <span data-ttu-id="9e319-188">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="9e319-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="9e319-189">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="9e319-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="9e319-190">**原則範圍︰**API、作業</span><span class="sxs-lookup"><span data-stu-id="9e319-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="9e319-191"><a name="JSONP"></a>JSONP</span><span class="sxs-lookup"><span data-stu-id="9e319-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="9e319-192">`jsonp` 原則會將 JSON 與補充的 (JSONP) 支援加入至作業或 API，以允許來自 JavaScript 瀏覽器型用戶端的跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="9e319-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="9e319-193">JSONP 是 JavaScript 程式中使用的方法，可從位於不同網域的伺服器要求資料。</span><span class="sxs-lookup"><span data-stu-id="9e319-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="9e319-194">JSONP 會略過大多數網頁瀏覽器中規定必須在相同網域內才能存取網頁的限制。</span><span class="sxs-lookup"><span data-stu-id="9e319-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="9e319-195">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="9e319-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="9e319-196">範例</span><span class="sxs-lookup"><span data-stu-id="9e319-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="9e319-197">如果呼叫方法時未指定回呼參數 ?cb=XXX，則會傳回一般 JSON (沒有函式呼叫包裝函式)。</span><span class="sxs-lookup"><span data-stu-id="9e319-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="9e319-198">如果加上回呼參數 `?cb=XXX`，則會傳回 JSONP 結果，在回呼函數旁邊包裝原始的 JSON 結果，例如 `XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="9e319-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="9e319-199">元素</span><span class="sxs-lookup"><span data-stu-id="9e319-199">Elements</span></span>  
  
|<span data-ttu-id="9e319-200">名稱</span><span class="sxs-lookup"><span data-stu-id="9e319-200">Name</span></span>|<span data-ttu-id="9e319-201">說明</span><span class="sxs-lookup"><span data-stu-id="9e319-201">Description</span></span>|<span data-ttu-id="9e319-202">必要</span><span class="sxs-lookup"><span data-stu-id="9e319-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="9e319-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="9e319-203">jsonp</span></span>|<span data-ttu-id="9e319-204">根元素。</span><span class="sxs-lookup"><span data-stu-id="9e319-204">Root element.</span></span>|<span data-ttu-id="9e319-205">是</span><span class="sxs-lookup"><span data-stu-id="9e319-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="9e319-206">屬性</span><span class="sxs-lookup"><span data-stu-id="9e319-206">Attributes</span></span>  
  
|<span data-ttu-id="9e319-207">名稱</span><span class="sxs-lookup"><span data-stu-id="9e319-207">Name</span></span>|<span data-ttu-id="9e319-208">說明</span><span class="sxs-lookup"><span data-stu-id="9e319-208">Description</span></span>|<span data-ttu-id="9e319-209">必要</span><span class="sxs-lookup"><span data-stu-id="9e319-209">Required</span></span>|<span data-ttu-id="9e319-210">預設值</span><span class="sxs-lookup"><span data-stu-id="9e319-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="9e319-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="9e319-211">callback-parameter-name</span></span>|<span data-ttu-id="9e319-212">跨網域 JavaScript 函數呼叫，開頭加上函數所在的完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="9e319-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="9e319-213">是</span><span class="sxs-lookup"><span data-stu-id="9e319-213">Yes</span></span>|<span data-ttu-id="9e319-214">N/A</span><span class="sxs-lookup"><span data-stu-id="9e319-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="9e319-215">使用量</span><span class="sxs-lookup"><span data-stu-id="9e319-215">Usage</span></span>  
 <span data-ttu-id="9e319-216">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="9e319-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="9e319-217">**原則區段︰**輸出</span><span class="sxs-lookup"><span data-stu-id="9e319-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="9e319-218">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="9e319-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="9e319-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e319-219">Next steps</span></span>
<span data-ttu-id="9e319-220">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="9e319-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  