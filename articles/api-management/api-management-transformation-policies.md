---
title: "aaaAzure API 管理轉換原則 |Microsoft 文件"
description: "深入了解 hello 轉換原則可在 Azure API 管理中使用。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="5adff-103">API 管理轉換原則</span><span class="sxs-lookup"><span data-stu-id="5adff-103">API Management transformation policies</span></span>
<span data-ttu-id="5adff-104">本主題提供下列 API 管理原則的 hello 的參考。</span><span class="sxs-lookup"><span data-stu-id="5adff-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="5adff-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="5adff-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="5adff-106"><a name="TransformationPolicies"></a> 轉換原則</span><span class="sxs-lookup"><span data-stu-id="5adff-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="5adff-107">[轉換 JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) -將要求或回應內文從 JSON tooXML。</span><span class="sxs-lookup"><span data-stu-id="5adff-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="5adff-108">[轉換 XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) -將要求或回應內文從 XML tooJSON。</span><span class="sxs-lookup"><span data-stu-id="5adff-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="5adff-109">[在內文中尋找並取代字串](api-management-transformation-policies.md#Findandreplacestringinbody) - 尋找要求或回應子字串，並將它取代為其他子字串。</span><span class="sxs-lookup"><span data-stu-id="5adff-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="5adff-110">[遮罩內容中的 Url](api-management-transformation-policies.md#MaskURLSContent) -重寫 （遮罩） 的連結，以 hello 回應內文，以便指向透過 hello 閘道 toohello 等同的連結。</span><span class="sxs-lookup"><span data-stu-id="5adff-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="5adff-111">[設定後端服務](api-management-transformation-policies.md#SetBackendService)-變更連入要求的 hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="5adff-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="5adff-112">[設定主體](api-management-transformation-policies.md#SetBody)-設定傳入和傳出要求的 hello 訊息本文。</span><span class="sxs-lookup"><span data-stu-id="5adff-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="5adff-113">[設定 HTTP 標頭](api-management-transformation-policies.md#SetHTTPheader)-指派值 tooan 現有的回應和/或要求標頭，或加入新的回應和/或要求標頭。</span><span class="sxs-lookup"><span data-stu-id="5adff-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="5adff-114">[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter) - 新增、取代值或刪除要求查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5adff-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="5adff-115">[請重寫 URL](api-management-transformation-policies.md#RewriteURL) -將要求 URL 的 hello web 服務所需要的公用格式 toohello 格式轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="5adff-116">[使用 XSLT 的 XML 轉換](api-management-transformation-policies.md#XSLTransform)層套用 XSL 轉換 tooXML，hello 要求或回應主體中的。</span><span class="sxs-lookup"><span data-stu-id="5adff-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="5adff-117"><a name="ConvertJSONtoXML"></a>轉換 JSON tooXML</span><span class="sxs-lookup"><span data-stu-id="5adff-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="5adff-118">hello`json-to-xml`原則將要求或回應內文從 JSON tooXML 中轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-119">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="5adff-120">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="5adff-121">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-121">Elements</span></span>  
  
|<span data-ttu-id="5adff-122">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-122">Name</span></span>|<span data-ttu-id="5adff-123">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-123">Description</span></span>|<span data-ttu-id="5adff-124">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="5adff-125">json-to-xml</span></span>|<span data-ttu-id="5adff-126">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-126">Root element.</span></span>|<span data-ttu-id="5adff-127">是</span><span class="sxs-lookup"><span data-stu-id="5adff-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5adff-128">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-128">Attributes</span></span>  
  
|<span data-ttu-id="5adff-129">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-129">Name</span></span>|<span data-ttu-id="5adff-130">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-130">Description</span></span>|<span data-ttu-id="5adff-131">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-131">Required</span></span>|<span data-ttu-id="5adff-132">預設值</span><span class="sxs-lookup"><span data-stu-id="5adff-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5adff-133">apply</span><span class="sxs-lookup"><span data-stu-id="5adff-133">apply</span></span>|<span data-ttu-id="5adff-134">hello 屬性必須設定下列值的 hello 的 tooone。</span><span class="sxs-lookup"><span data-stu-id="5adff-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="5adff-135">-   always - 一律套用轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="5adff-136">-   content-type-json - 只有當回應中的 Content-type 標頭指出 JSON 存在時才轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="5adff-137">是</span><span class="sxs-lookup"><span data-stu-id="5adff-137">Yes</span></span>|<span data-ttu-id="5adff-138">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-138">N/A</span></span>|  
|<span data-ttu-id="5adff-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="5adff-139">consider-accept-header</span></span>|<span data-ttu-id="5adff-140">hello 屬性必須設定下列值的 hello 的 tooone。</span><span class="sxs-lookup"><span data-stu-id="5adff-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="5adff-141">-   true - 如果在要求的 Accept 標頭中要求 JSON，才套用轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="5adff-142">-   false - 一律套用轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="5adff-143">否</span><span class="sxs-lookup"><span data-stu-id="5adff-143">No</span></span>|<span data-ttu-id="5adff-144">true</span><span class="sxs-lookup"><span data-stu-id="5adff-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5adff-145">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-145">Usage</span></span>  
 <span data-ttu-id="5adff-146">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-147">**原則區段︰**輸入、輸出、錯誤</span><span class="sxs-lookup"><span data-stu-id="5adff-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="5adff-148">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-149"><a name="ConvertXMLtoJSON"></a>轉換 XML tooJSON</span><span class="sxs-lookup"><span data-stu-id="5adff-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="5adff-150">hello`xml-to-json`原則將要求或回應內文從 XML tooJSON 中轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="5adff-151">使用的 toomodernize 僅 XML 後端 web 服務為基礎的應用程式開發介面，可將此原則。</span><span class="sxs-lookup"><span data-stu-id="5adff-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-152">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="5adff-153">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="5adff-154">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-154">Elements</span></span>  
  
|<span data-ttu-id="5adff-155">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-155">Name</span></span>|<span data-ttu-id="5adff-156">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-156">Description</span></span>|<span data-ttu-id="5adff-157">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="5adff-158">xml-to-json</span></span>|<span data-ttu-id="5adff-159">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-159">Root element.</span></span>|<span data-ttu-id="5adff-160">是</span><span class="sxs-lookup"><span data-stu-id="5adff-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5adff-161">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-161">Attributes</span></span>  
  
|<span data-ttu-id="5adff-162">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-162">Name</span></span>|<span data-ttu-id="5adff-163">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-163">Description</span></span>|<span data-ttu-id="5adff-164">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-164">Required</span></span>|<span data-ttu-id="5adff-165">預設值</span><span class="sxs-lookup"><span data-stu-id="5adff-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5adff-166">kind</span><span class="sxs-lookup"><span data-stu-id="5adff-166">kind</span></span>|<span data-ttu-id="5adff-167">hello 屬性必須設定下列值的 hello 的 tooone。</span><span class="sxs-lookup"><span data-stu-id="5adff-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="5adff-168">javascript-易記-hello 轉換的 JSON 具有表單易記 tooJavaScript 開發人員。</span><span class="sxs-lookup"><span data-stu-id="5adff-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="5adff-169">-直接-hello 轉換的 JSON 反映 hello 原始 XML 文件的結構。</span><span class="sxs-lookup"><span data-stu-id="5adff-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="5adff-170">是</span><span class="sxs-lookup"><span data-stu-id="5adff-170">Yes</span></span>|<span data-ttu-id="5adff-171">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-171">N/A</span></span>|  
|<span data-ttu-id="5adff-172">apply</span><span class="sxs-lookup"><span data-stu-id="5adff-172">apply</span></span>|<span data-ttu-id="5adff-173">hello 屬性必須設定下列值的 hello 的 tooone。</span><span class="sxs-lookup"><span data-stu-id="5adff-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="5adff-174">-   always - 一律轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-174">-   always - convert always.</span></span><br /><span data-ttu-id="5adff-175">-   content-type-xml - 只有當回應中的 Content-type 標頭指出 XML 存在時才轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="5adff-176">是</span><span class="sxs-lookup"><span data-stu-id="5adff-176">Yes</span></span>|<span data-ttu-id="5adff-177">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-177">N/A</span></span>|  
|<span data-ttu-id="5adff-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="5adff-178">consider-accept-header</span></span>|<span data-ttu-id="5adff-179">hello 屬性必須設定下列值的 hello 的 tooone。</span><span class="sxs-lookup"><span data-stu-id="5adff-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="5adff-180">-   true - 如果在要求的 Accept 標頭中要求 XML，才套用轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="5adff-181">-   false - 一律套用轉換。</span><span class="sxs-lookup"><span data-stu-id="5adff-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="5adff-182">否</span><span class="sxs-lookup"><span data-stu-id="5adff-182">No</span></span>|<span data-ttu-id="5adff-183">true</span><span class="sxs-lookup"><span data-stu-id="5adff-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5adff-184">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-184">Usage</span></span>  
 <span data-ttu-id="5adff-185">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-186">**原則區段︰**輸入、輸出、錯誤</span><span class="sxs-lookup"><span data-stu-id="5adff-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="5adff-187">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-188"><a name="Findandreplacestringinbody"></a> 在本文中尋找並取代字串</span><span class="sxs-lookup"><span data-stu-id="5adff-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="5adff-189">hello`find-and-replace`原則尋找要求或回應子字串，並以不同的子字串取代。</span><span class="sxs-lookup"><span data-stu-id="5adff-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-190">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="5adff-191">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="5adff-192">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-192">Elements</span></span>  
  
|<span data-ttu-id="5adff-193">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-193">Name</span></span>|<span data-ttu-id="5adff-194">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-194">Description</span></span>|<span data-ttu-id="5adff-195">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="5adff-196">find-and-replace</span></span>|<span data-ttu-id="5adff-197">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-197">Root element.</span></span>|<span data-ttu-id="5adff-198">是</span><span class="sxs-lookup"><span data-stu-id="5adff-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5adff-199">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-199">Attributes</span></span>  
  
|<span data-ttu-id="5adff-200">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-200">Name</span></span>|<span data-ttu-id="5adff-201">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-201">Description</span></span>|<span data-ttu-id="5adff-202">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-202">Required</span></span>|<span data-ttu-id="5adff-203">預設值</span><span class="sxs-lookup"><span data-stu-id="5adff-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5adff-204">from</span><span class="sxs-lookup"><span data-stu-id="5adff-204">from</span></span>|<span data-ttu-id="5adff-205">hello 字串 toosearch 的。</span><span class="sxs-lookup"><span data-stu-id="5adff-205">hello string toosearch for.</span></span>|<span data-ttu-id="5adff-206">是</span><span class="sxs-lookup"><span data-stu-id="5adff-206">Yes</span></span>|<span data-ttu-id="5adff-207">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-207">N/A</span></span>|  
|<span data-ttu-id="5adff-208">to</span><span class="sxs-lookup"><span data-stu-id="5adff-208">to</span></span>|<span data-ttu-id="5adff-209">hello 取代字串。</span><span class="sxs-lookup"><span data-stu-id="5adff-209">hello replacement string.</span></span> <span data-ttu-id="5adff-210">指定零長度的取代字串 tooremove hello 搜尋字串。</span><span class="sxs-lookup"><span data-stu-id="5adff-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="5adff-211">是</span><span class="sxs-lookup"><span data-stu-id="5adff-211">Yes</span></span>|<span data-ttu-id="5adff-212">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5adff-213">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-213">Usage</span></span>  
 <span data-ttu-id="5adff-214">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-215">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="5adff-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5adff-216">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-217"><a name="MaskURLSContent"></a> 遮罩內容中的 URL</span><span class="sxs-lookup"><span data-stu-id="5adff-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="5adff-218">hello`redirect-content-urls`原則重寫 （遮罩） hello 回應主體中的連結，以便指向透過 hello 閘道 toohello 等同的連結。</span><span class="sxs-lookup"><span data-stu-id="5adff-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="5adff-219">使用在 hello 輸出區段 toore 寫入回應主體連結 toomake 它們點 toohello 閘道。</span><span class="sxs-lookup"><span data-stu-id="5adff-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="5adff-220">Hello 用於輸入產生相反效果 > 一節。</span><span class="sxs-lookup"><span data-stu-id="5adff-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5adff-221">此原則不會變更任何標頭值，如 `Location` 標頭。</span><span class="sxs-lookup"><span data-stu-id="5adff-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="5adff-222">toochange 標頭值，會使用 hello[集標頭](api-management-transformation-policies.md#SetHTTPheader)原則。</span><span class="sxs-lookup"><span data-stu-id="5adff-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-223">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="5adff-224">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="5adff-225">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-225">Elements</span></span>  
  
|<span data-ttu-id="5adff-226">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-226">Name</span></span>|<span data-ttu-id="5adff-227">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-227">Description</span></span>|<span data-ttu-id="5adff-228">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="5adff-229">redirect-content-urls</span></span>|<span data-ttu-id="5adff-230">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-230">Root element.</span></span>|<span data-ttu-id="5adff-231">是</span><span class="sxs-lookup"><span data-stu-id="5adff-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5adff-232">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-232">Usage</span></span>  
 <span data-ttu-id="5adff-233">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-234">**原則區段︰**輸入、輸出</span><span class="sxs-lookup"><span data-stu-id="5adff-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="5adff-235">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-236"><a name="SetBackendService"></a> 設定後端服務</span><span class="sxs-lookup"><span data-stu-id="5adff-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="5adff-237">使用 hello`set-backend-service`原則 tooredirect 傳入要求 tooa 不同的後端，比 hello hello API 設定該作業中指定的其中一個。</span><span class="sxs-lookup"><span data-stu-id="5adff-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="5adff-238">此原則的變更 hello 連入要求 toohello hello 原則中指定的其中一個的 hello 後端服務基礎的 URL。</span><span class="sxs-lookup"><span data-stu-id="5adff-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-239">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="5adff-240">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="5adff-241">在此範例中的 hello 設定後端服務原則，將要求 hello 版本值傳入 hello 查詢字串 tooa 不同的後端服務於 hello 中所指定的一個 hello API 為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="5adff-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="5adff-242">一開始 hello 後端服務基礎 URL 被衍生自 hello API 設定。</span><span class="sxs-lookup"><span data-stu-id="5adff-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="5adff-243">因此 hello 要求 URL`https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef`變成`http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef`其中`http://contoso.com/api/10.4/`hello hello API 設定中指定的後端服務 url。</span><span class="sxs-lookup"><span data-stu-id="5adff-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="5adff-244">當 hello [< 選擇\>](api-management-advanced-policies.md#choose)套用原則陳述 hello 後端服務基礎 URL 可能再次變更太`http://contoso.com/api/8.2`或`http://contoso.com/api/9.1`，端視 hello hello 版本要求查詢參數的值。</span><span class="sxs-lookup"><span data-stu-id="5adff-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="5adff-245">例如，如果 hello 值是`"2013-15"`hello URL 會成為最後一項要求`http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`。</span><span class="sxs-lookup"><span data-stu-id="5adff-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="5adff-246">如果進一步的 hello 要求轉換為所需，其他[轉換原則](api-management-transformation-policies.md#TransformationPolicies)可用。</span><span class="sxs-lookup"><span data-stu-id="5adff-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="5adff-247">例如，tooremove hello 版本查詢參數，既然 hello 要求會被路由傳送 tooa 版本特定後端，hello[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter)原則可以是使用的 tooremove hello now 多餘版本屬性。</span><span class="sxs-lookup"><span data-stu-id="5adff-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="5adff-248">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="5adff-249">在此範例 hello 原則路由 hello 要求 tooa 服務網狀架構後端中，為 hello 資料分割索引鍵使用 hello userId 查詢字串，並使用 hello hello 磁碟分割的主要複本。</span><span class="sxs-lookup"><span data-stu-id="5adff-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="5adff-250">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-250">Elements</span></span>  
  
|<span data-ttu-id="5adff-251">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-251">Name</span></span>|<span data-ttu-id="5adff-252">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-252">Description</span></span>|<span data-ttu-id="5adff-253">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="5adff-254">set-backend-service</span></span>|<span data-ttu-id="5adff-255">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-255">Root element.</span></span>|<span data-ttu-id="5adff-256">是</span><span class="sxs-lookup"><span data-stu-id="5adff-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5adff-257">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-257">Attributes</span></span>  
  
|<span data-ttu-id="5adff-258">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-258">Name</span></span>|<span data-ttu-id="5adff-259">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-259">Description</span></span>|<span data-ttu-id="5adff-260">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-260">Required</span></span>|<span data-ttu-id="5adff-261">預設值</span><span class="sxs-lookup"><span data-stu-id="5adff-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5adff-262">base-url</span><span class="sxs-lookup"><span data-stu-id="5adff-262">base-url</span></span>|<span data-ttu-id="5adff-263">新的後端服務基底 URL。</span><span class="sxs-lookup"><span data-stu-id="5adff-263">New backend service base URL.</span></span>|<span data-ttu-id="5adff-264">否</span><span class="sxs-lookup"><span data-stu-id="5adff-264">No</span></span>|<span data-ttu-id="5adff-265">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-265">N/A</span></span>|  
|<span data-ttu-id="5adff-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="5adff-266">backend-id</span></span>|<span data-ttu-id="5adff-267">Hello 後端 tooroute 來識別項。</span><span class="sxs-lookup"><span data-stu-id="5adff-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="5adff-268">否</span><span class="sxs-lookup"><span data-stu-id="5adff-268">No</span></span>|<span data-ttu-id="5adff-269">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-269">N/A</span></span>|  
|<span data-ttu-id="5adff-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="5adff-270">sf-partition-key</span></span>|<span data-ttu-id="5adff-271">僅適用於 Service Fabric 服務 hello 後端，並指定使用 ' 後端 id'。</span><span class="sxs-lookup"><span data-stu-id="5adff-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="5adff-272">使用 tooresolve 從 hello 名稱解析服務的特定分割區。</span><span class="sxs-lookup"><span data-stu-id="5adff-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="5adff-273">否</span><span class="sxs-lookup"><span data-stu-id="5adff-273">No</span></span>|<span data-ttu-id="5adff-274">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-274">N/A</span></span>|  
|<span data-ttu-id="5adff-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="5adff-275">sf-replica-type</span></span>|<span data-ttu-id="5adff-276">僅適用於 Service Fabric 服務 hello 後端，並指定使用 ' 後端 id'。</span><span class="sxs-lookup"><span data-stu-id="5adff-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="5adff-277">控制是否 hello 要求應 toohello 主要或次要複本的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="5adff-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="5adff-278">否</span><span class="sxs-lookup"><span data-stu-id="5adff-278">No</span></span>|<span data-ttu-id="5adff-279">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-279">N/A</span></span>|    
|<span data-ttu-id="5adff-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="5adff-280">sf-resolve-condition</span></span>|<span data-ttu-id="5adff-281">僅適用於 Service Fabric 服務 hello 後端時。</span><span class="sxs-lookup"><span data-stu-id="5adff-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="5adff-282">識別條件如果 hello 呼叫 tooService 網狀架構後端有 toobe 重複使用新的解析度。</span><span class="sxs-lookup"><span data-stu-id="5adff-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="5adff-283">否</span><span class="sxs-lookup"><span data-stu-id="5adff-283">No</span></span>|<span data-ttu-id="5adff-284">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-284">N/A</span></span>|    
|<span data-ttu-id="5adff-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="5adff-285">sf-service-instance-name</span></span>|<span data-ttu-id="5adff-286">僅適用於 Service Fabric 服務 hello 後端時。</span><span class="sxs-lookup"><span data-stu-id="5adff-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="5adff-287">在執行階段允許 toochange 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="5adff-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="5adff-288">否</span><span class="sxs-lookup"><span data-stu-id="5adff-288">No</span></span>|<span data-ttu-id="5adff-289">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="5adff-290">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-290">Usage</span></span>  
 <span data-ttu-id="5adff-291">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-292">**原則區段︰**輸入、後端</span><span class="sxs-lookup"><span data-stu-id="5adff-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="5adff-293">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-294"><a name="SetBody"></a> 設定本文</span><span class="sxs-lookup"><span data-stu-id="5adff-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="5adff-295">使用 hello`set-body`原則 tooset hello 訊息內文的傳入和傳出要求。</span><span class="sxs-lookup"><span data-stu-id="5adff-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="5adff-296">tooaccess hello 訊息本文，您可以使用 hello`context.Request.Body`屬性或 hello `context.Response.Body`，端視 hello 原則是否會在 hello 中輸入或輸出區段。</span><span class="sxs-lookup"><span data-stu-id="5adff-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="5adff-297">請注意，根據預設，當您存取 hello 訊息本文會使用`context.Request.Body`或`context.Response.Body`，hello 原始訊息本文會遺失，而且必須設定藉由在 hello 運算式傳回 hello 主體。</span><span class="sxs-lookup"><span data-stu-id="5adff-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="5adff-298">toopreserve hello 本文內容，設定 hello`preserveContent`參數太`true`存取 hello 訊息時。</span><span class="sxs-lookup"><span data-stu-id="5adff-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="5adff-299">如果`preserveContent`設定得`true`和不同的主體傳回 hello 運算式 hello 主體使用。</span><span class="sxs-lookup"><span data-stu-id="5adff-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="5adff-300">請注意下列考量事項時使用 hello hello`set-body`原則。</span><span class="sxs-lookup"><span data-stu-id="5adff-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="5adff-301">如果您使用 hello`set-body`原則 tooreturn 新的或更新主體，您不需要 tooset`preserveContent`太`true`因為您可以明確地提供 hello 新本文內容。</span><span class="sxs-lookup"><span data-stu-id="5adff-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="5adff-302">保留回應的 hello 內容 hello 輸入管線中沒有意義，因為尚無回應。</span><span class="sxs-lookup"><span data-stu-id="5adff-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="5adff-303">Hello 內容要求的保留 hello 輸出管線中沒有意義因為 hello 要求已傳送 toohello 後端此時。</span><span class="sxs-lookup"><span data-stu-id="5adff-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="5adff-304">如果在沒有任何訊息本文時使用此原則，例如輸入 GET，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5adff-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="5adff-305">如需詳細資訊，請參閱 hello `context.Request.Body`， `context.Response.Body`，和 hello`IMessage`章節 hello[內容變數](api-management-policy-expressions.md#ContextVariables)資料表。</span><span class="sxs-lookup"><span data-stu-id="5adff-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-306">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="5adff-307">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="5adff-308">常值文字範例</span><span class="sxs-lookup"><span data-stu-id="5adff-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="5adff-309">存取 hello 本文為字串的範例。</span><span class="sxs-lookup"><span data-stu-id="5adff-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="5adff-310">請注意，我們會保留 hello 原始要求主體，讓我們可以稍後在 hello 管線中存取它。</span><span class="sxs-lookup"><span data-stu-id="5adff-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="5adff-311">存取 hello 本文為 JObject 的範例。</span><span class="sxs-lookup"><span data-stu-id="5adff-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="5adff-312">請注意，由於我們不會保留 hello 的原始要求本文，而稍後在 hello 管線將會導致例外狀況的存取。</span><span class="sxs-lookup"><span data-stu-id="5adff-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="5adff-313">根據產品篩選回應</span><span class="sxs-lookup"><span data-stu-id="5adff-313">Filter response based on product</span></span>  
 <span data-ttu-id="5adff-314">這個範例會示範如何 tooperform 內容篩選的資料元素，移除 hello 回應 hello 後端服務時收到使用 hello`Starter`產品。</span><span class="sxs-lookup"><span data-stu-id="5adff-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="5adff-315">如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too34:30 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="5adff-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="5adff-316">開始使用 31:50 toosee 概觀[hello 深色 Sky 預測 API](https://developer.forecast.io/)用於此示範。</span><span class="sxs-lookup"><span data-stu-id="5adff-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="5adff-317">使用 Liquid 範本搭配設定本文</span><span class="sxs-lookup"><span data-stu-id="5adff-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="5adff-318">hello`set-body`原則可以設定的 toouse hello[不固定](https://shopify.github.io/liquid/basics/introduction/)樣板化語言 tootransfom hello 主體的要求或回應。</span><span class="sxs-lookup"><span data-stu-id="5adff-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="5adff-319">這可以是訊息的非常有效，如果您需要 toocompletely 重繪 hello 格式。</span><span class="sxs-lookup"><span data-stu-id="5adff-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5adff-320">hello 實作用於 hello 液晶`set-body`原則設定為 'C# 模式'。</span><span class="sxs-lookup"><span data-stu-id="5adff-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="5adff-321">這在進行篩選之類的操作時尤其重要。</span><span class="sxs-lookup"><span data-stu-id="5adff-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="5adff-322">例如，使用日期篩選需要 hello 使用 Pascal 大小寫和 C# 的日期格式設定例如：</span><span class="sxs-lookup"><span data-stu-id="5adff-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="5adff-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="5adff-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5adff-324">順序 toocorrectly 繫結 tooan XML 主體，使用 hello 不固定的範本，在使用`set-header`原則 tooset Content-type tooeither 應用程式/xml、 text/xml （或任何型別結尾 + xml）; JSON 主體，它必須是應用程式/json、 text/json （或任何類型結束與 + json)。</span><span class="sxs-lookup"><span data-stu-id="5adff-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="5adff-325">轉換 JSON tooSOAP 使用不固定範本</span><span class="sxs-lookup"><span data-stu-id="5adff-325">Convert JSON tooSOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="5adff-326">使用 Liquid 範本來轉換 JSON</span><span class="sxs-lookup"><span data-stu-id="5adff-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="5adff-327">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-327">Elements</span></span>  
  
|<span data-ttu-id="5adff-328">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-328">Name</span></span>|<span data-ttu-id="5adff-329">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-329">Description</span></span>|<span data-ttu-id="5adff-330">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-331">set-body</span><span class="sxs-lookup"><span data-stu-id="5adff-331">set-body</span></span>|<span data-ttu-id="5adff-332">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-332">Root element.</span></span> <span data-ttu-id="5adff-333">包含 hello 本文文字或運算式傳回本文。</span><span class="sxs-lookup"><span data-stu-id="5adff-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="5adff-334">是</span><span class="sxs-lookup"><span data-stu-id="5adff-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="5adff-335">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-335">Properties</span></span>  
  
|<span data-ttu-id="5adff-336">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-336">Name</span></span>|<span data-ttu-id="5adff-337">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-337">Description</span></span>|<span data-ttu-id="5adff-338">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-338">Required</span></span>|<span data-ttu-id="5adff-339">預設值</span><span class="sxs-lookup"><span data-stu-id="5adff-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5adff-340">template</span><span class="sxs-lookup"><span data-stu-id="5adff-340">template</span></span>|<span data-ttu-id="5adff-341">Hello 設定主體原則使用的 toochange hello 樣板化模式將會執行。</span><span class="sxs-lookup"><span data-stu-id="5adff-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="5adff-342">目前僅支援 hello 值為：</span><span class="sxs-lookup"><span data-stu-id="5adff-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="5adff-343">-不固定-hello 設定主體的原則會使用 hello 不固定範本引擎</span><span class="sxs-lookup"><span data-stu-id="5adff-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="5adff-344">否</span><span class="sxs-lookup"><span data-stu-id="5adff-344">No</span></span>|<span data-ttu-id="5adff-345">liquid</span><span class="sxs-lookup"><span data-stu-id="5adff-345">liquid</span></span>|  

<span data-ttu-id="5adff-346">對於存取 hello 要求和回應的相關資訊，請 hello 不固定範本可以繫結 tooa 內容物件，以 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="5adff-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="5adff-347">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-347">Usage</span></span>  
 <span data-ttu-id="5adff-348">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-349">**原則區段︰**輸入、輸出、後端</span><span class="sxs-lookup"><span data-stu-id="5adff-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="5adff-350">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-351"><a name="SetHTTPheader"></a> 設定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="5adff-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="5adff-352">hello`set-header`原則指派值 tooan 現有的回應和/或要求標頭，或加入新的回應和/或要求標頭。</span><span class="sxs-lookup"><span data-stu-id="5adff-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="5adff-353">將 HTTP 標頭清單插入至 HTTP 訊息中。</span><span class="sxs-lookup"><span data-stu-id="5adff-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="5adff-354">輸入管線中放置時，此原則設定 hello 傳遞 toohello 目標服務的 hello 要求的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="5adff-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="5adff-355">輸出管線中放置時，此原則設定傳送 toohello 閘道用戶端 hello 回應 hello HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="5adff-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-356">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="5adff-357">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="5adff-358">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="5adff-359">轉送內容資訊 toohello 後端服務</span><span class="sxs-lookup"><span data-stu-id="5adff-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="5adff-360">這個範例會示範如何在 hello API tooapply 原則層級 toosupply 內容資訊 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="5adff-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="5adff-361">如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too10:30 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="5adff-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="5adff-362">在 12:10 沒有您可以在其中看到 hello 原則，在工作中 hello 開發人員入口網站呼叫作業的示範。</span><span class="sxs-lookup"><span data-stu-id="5adff-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="5adff-363">如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="5adff-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="5adff-364">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-364">Elements</span></span>  
  
|<span data-ttu-id="5adff-365">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-365">Name</span></span>|<span data-ttu-id="5adff-366">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-366">Description</span></span>|<span data-ttu-id="5adff-367">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-368">set-header</span><span class="sxs-lookup"><span data-stu-id="5adff-368">set-header</span></span>|<span data-ttu-id="5adff-369">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-369">Root element.</span></span>|<span data-ttu-id="5adff-370">是</span><span class="sxs-lookup"><span data-stu-id="5adff-370">Yes</span></span>|  
|<span data-ttu-id="5adff-371">value</span><span class="sxs-lookup"><span data-stu-id="5adff-371">value</span></span>|<span data-ttu-id="5adff-372">指定 hello hello 標頭 toobe 組值。</span><span class="sxs-lookup"><span data-stu-id="5adff-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="5adff-373">多個標頭以 hello 相同的名稱加入更多`value`項目。</span><span class="sxs-lookup"><span data-stu-id="5adff-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="5adff-374">是</span><span class="sxs-lookup"><span data-stu-id="5adff-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="5adff-375">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-375">Properties</span></span>  
  
|<span data-ttu-id="5adff-376">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-376">Name</span></span>|<span data-ttu-id="5adff-377">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-377">Description</span></span>|<span data-ttu-id="5adff-378">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-378">Required</span></span>|<span data-ttu-id="5adff-379">預設值</span><span class="sxs-lookup"><span data-stu-id="5adff-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5adff-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="5adff-380">exists-action</span></span>|<span data-ttu-id="5adff-381">Hello 標頭已指定時，請指定何種動作 tootake。</span><span class="sxs-lookup"><span data-stu-id="5adff-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="5adff-382">此屬性必須有 hello 下列值之一。</span><span class="sxs-lookup"><span data-stu-id="5adff-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="5adff-383">-覆寫-取代 hello hello 現有的標頭值。</span><span class="sxs-lookup"><span data-stu-id="5adff-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="5adff-384">-skip-不會取代 hello 現有標頭值。</span><span class="sxs-lookup"><span data-stu-id="5adff-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="5adff-385">-附加-附加 hello 值 toohello 現有標頭值。</span><span class="sxs-lookup"><span data-stu-id="5adff-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="5adff-386">-delete-從 hello 要求移除 hello 標頭。</span><span class="sxs-lookup"><span data-stu-id="5adff-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="5adff-387">當設定太`override`編列多個項目以 hello 相同的名稱，正在設定相應 tooall 項目 （列出多次） hello 標頭中的結果; 只有列出的值會設定在 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="5adff-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="5adff-388">否</span><span class="sxs-lookup"><span data-stu-id="5adff-388">No</span></span>|<span data-ttu-id="5adff-389">override</span><span class="sxs-lookup"><span data-stu-id="5adff-389">override</span></span>|  
|<span data-ttu-id="5adff-390">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-390">name</span></span>|<span data-ttu-id="5adff-391">指定 hello 標頭 toobe 集的名稱。</span><span class="sxs-lookup"><span data-stu-id="5adff-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="5adff-392">是</span><span class="sxs-lookup"><span data-stu-id="5adff-392">Yes</span></span>|<span data-ttu-id="5adff-393">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5adff-394">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-394">Usage</span></span>  
 <span data-ttu-id="5adff-395">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-396">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="5adff-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5adff-397">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-398"><a name="SetQueryStringParameter"></a> 設定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="5adff-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="5adff-399">hello`set-query-parameter`原則新增、 取代值，或刪除要求查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5adff-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="5adff-400">可以是使用的 toopass hello 後端服務所需要的是選擇性的或永遠不會出現在 hello 要求查詢參數。</span><span class="sxs-lookup"><span data-stu-id="5adff-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-401">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="5adff-402">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="5adff-403">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="5adff-404">轉送內容資訊 toohello 後端服務</span><span class="sxs-lookup"><span data-stu-id="5adff-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="5adff-405">這個範例會示範如何在 hello API tooapply 原則層級 toosupply 內容資訊 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="5adff-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="5adff-406">如需設定和使用此原則的示範，請參閱[雲端涵蓋的時段 177： 更 API 管理功能與 Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)和 too10:30 向前快轉。</span><span class="sxs-lookup"><span data-stu-id="5adff-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="5adff-407">在 12:10 沒有您可以在其中看到 hello 原則，在工作中 hello 開發人員入口網站呼叫作業的示範。</span><span class="sxs-lookup"><span data-stu-id="5adff-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="5adff-408">如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="5adff-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="5adff-409">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-409">Elements</span></span>  
  
|<span data-ttu-id="5adff-410">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-410">Name</span></span>|<span data-ttu-id="5adff-411">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-411">Description</span></span>|<span data-ttu-id="5adff-412">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="5adff-413">set-query-parameter</span></span>|<span data-ttu-id="5adff-414">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-414">Root element.</span></span>|<span data-ttu-id="5adff-415">是</span><span class="sxs-lookup"><span data-stu-id="5adff-415">Yes</span></span>|  
|<span data-ttu-id="5adff-416">value</span><span class="sxs-lookup"><span data-stu-id="5adff-416">value</span></span>|<span data-ttu-id="5adff-417">指定 hello hello 查詢參數 toobe 集值。</span><span class="sxs-lookup"><span data-stu-id="5adff-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="5adff-418">多個查詢參數以 hello 相同的名稱新增額外`value`項目。</span><span class="sxs-lookup"><span data-stu-id="5adff-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="5adff-419">是</span><span class="sxs-lookup"><span data-stu-id="5adff-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="5adff-420">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-420">Properties</span></span>  
  
|<span data-ttu-id="5adff-421">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-421">Name</span></span>|<span data-ttu-id="5adff-422">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-422">Description</span></span>|<span data-ttu-id="5adff-423">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-423">Required</span></span>|<span data-ttu-id="5adff-424">預設值</span><span class="sxs-lookup"><span data-stu-id="5adff-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5adff-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="5adff-425">exists-action</span></span>|<span data-ttu-id="5adff-426">已指定 hello 查詢參數時，請指定何種動作 tootake。</span><span class="sxs-lookup"><span data-stu-id="5adff-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="5adff-427">此屬性必須有 hello 下列值之一。</span><span class="sxs-lookup"><span data-stu-id="5adff-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="5adff-428">-覆寫-取代 hello hello 現有參數值。</span><span class="sxs-lookup"><span data-stu-id="5adff-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="5adff-429">-skip-不會取代 hello 現有的查詢參數值。</span><span class="sxs-lookup"><span data-stu-id="5adff-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="5adff-430">-附加-附加 hello 值 toohello 現有查詢的參數值。</span><span class="sxs-lookup"><span data-stu-id="5adff-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="5adff-431">-delete-從 hello 要求移除 hello 查詢參數。</span><span class="sxs-lookup"><span data-stu-id="5adff-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="5adff-432">當設定太`override`編列多個項目以 hello 相同的名稱，正在設定相應 tooall 項目 （列出多次） hello 查詢參數中的結果; 只有列出的值會設定在 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="5adff-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="5adff-433">否</span><span class="sxs-lookup"><span data-stu-id="5adff-433">No</span></span>|<span data-ttu-id="5adff-434">override</span><span class="sxs-lookup"><span data-stu-id="5adff-434">override</span></span>|  
|<span data-ttu-id="5adff-435">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-435">name</span></span>|<span data-ttu-id="5adff-436">指定 hello 查詢參數 toobe 集的名稱。</span><span class="sxs-lookup"><span data-stu-id="5adff-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="5adff-437">是</span><span class="sxs-lookup"><span data-stu-id="5adff-437">Yes</span></span>|<span data-ttu-id="5adff-438">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5adff-439">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-439">Usage</span></span>  
 <span data-ttu-id="5adff-440">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-441">**原則區段︰**輸入、後端</span><span class="sxs-lookup"><span data-stu-id="5adff-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="5adff-442">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-443"><a name="RewriteURL"></a> 重寫 URL</span><span class="sxs-lookup"><span data-stu-id="5adff-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="5adff-444">hello`rewrite-uri`原則將轉換要求 URL 的公用格式 toohello 格式 hello web 服務所預期 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5adff-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="5adff-445">公用 URL - `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="5adff-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="5adff-446">要求 URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="5adff-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="5adff-447">人力和 （或) 瀏覽器易記 URL 應該轉換成 hello web 服務所預期的 hello URL 格式時，可以使用此原則。</span><span class="sxs-lookup"><span data-stu-id="5adff-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="5adff-448">此原則只需要套用公開替代 URL 格式，例如潔淨 Url、 RESTful Url、 使用者易記的 Url 或不包含查詢字串而改為包含只有 hello 路徑 hello 的純粹結構化 url 的 SEO 易記 Url 時 toobe（之後 hello 配置和 hello 授權） 的資源。</span><span class="sxs-lookup"><span data-stu-id="5adff-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="5adff-449">這樣做通常是基於美觀、實用性或搜尋引擎最佳化 (SEO) 目的。</span><span class="sxs-lookup"><span data-stu-id="5adff-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5adff-450">您只能新增使用 hello 原則的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5adff-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="5adff-451">您無法加入額外的範本路徑參數，在 hello 重寫 URL。</span><span class="sxs-lookup"><span data-stu-id="5adff-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="5adff-452">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="5adff-453">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="5adff-454">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-454">Elements</span></span>  
  
|<span data-ttu-id="5adff-455">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-455">Name</span></span>|<span data-ttu-id="5adff-456">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-456">Description</span></span>|<span data-ttu-id="5adff-457">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="5adff-458">rewrite-uri</span></span>|<span data-ttu-id="5adff-459">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-459">Root element.</span></span>|<span data-ttu-id="5adff-460">是</span><span class="sxs-lookup"><span data-stu-id="5adff-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5adff-461">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-461">Attributes</span></span>  
  
|<span data-ttu-id="5adff-462">屬性</span><span class="sxs-lookup"><span data-stu-id="5adff-462">Attribute</span></span>|<span data-ttu-id="5adff-463">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-463">Description</span></span>|<span data-ttu-id="5adff-464">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-464">Required</span></span>|<span data-ttu-id="5adff-465">預設值</span><span class="sxs-lookup"><span data-stu-id="5adff-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="5adff-466">template</span><span class="sxs-lookup"><span data-stu-id="5adff-466">template</span></span>|<span data-ttu-id="5adff-467">與任何查詢字串參數的 hello 實際的 web 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="5adff-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="5adff-468">當使用運算式，hello 整個值必須是運算式。</span><span class="sxs-lookup"><span data-stu-id="5adff-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="5adff-469">是</span><span class="sxs-lookup"><span data-stu-id="5adff-469">Yes</span></span>|<span data-ttu-id="5adff-470">N/A</span><span class="sxs-lookup"><span data-stu-id="5adff-470">N/A</span></span>|  
|<span data-ttu-id="5adff-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="5adff-471">copy-unmatched-params</span></span>|<span data-ttu-id="5adff-472">指定是否在 hello 內送要求不存在於 hello 原始 URL 範本中的查詢參數會加入 toohello hello 所定義的 URL 重新撰寫範本</span><span class="sxs-lookup"><span data-stu-id="5adff-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="5adff-473">否</span><span class="sxs-lookup"><span data-stu-id="5adff-473">No</span></span>|<span data-ttu-id="5adff-474">true</span><span class="sxs-lookup"><span data-stu-id="5adff-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5adff-475">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-475">Usage</span></span>  
 <span data-ttu-id="5adff-476">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-477">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="5adff-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="5adff-478">**原則範圍︰**產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="5adff-479"><a name="XSLTransform"></a> 使用 XSLT 轉換 XML</span><span class="sxs-lookup"><span data-stu-id="5adff-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="5adff-480">hello`Transform XML using an XSLT`原則會套用 XSL 轉換 tooXML，hello 要求或回應主體中的。</span><span class="sxs-lookup"><span data-stu-id="5adff-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5adff-481">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="5adff-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="5adff-482">範例</span><span class="sxs-lookup"><span data-stu-id="5adff-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="5adff-483">元素</span><span class="sxs-lookup"><span data-stu-id="5adff-483">Elements</span></span>  
  
|<span data-ttu-id="5adff-484">名稱</span><span class="sxs-lookup"><span data-stu-id="5adff-484">Name</span></span>|<span data-ttu-id="5adff-485">說明</span><span class="sxs-lookup"><span data-stu-id="5adff-485">Description</span></span>|<span data-ttu-id="5adff-486">必要</span><span class="sxs-lookup"><span data-stu-id="5adff-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5adff-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="5adff-487">xsl-transform</span></span>|<span data-ttu-id="5adff-488">根元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-488">Root element.</span></span>|<span data-ttu-id="5adff-489">是</span><span class="sxs-lookup"><span data-stu-id="5adff-489">Yes</span></span>|  
|<span data-ttu-id="5adff-490">參數</span><span class="sxs-lookup"><span data-stu-id="5adff-490">parameter</span></span>|<span data-ttu-id="5adff-491">使用的 toodefine hello 轉換中使用的變數</span><span class="sxs-lookup"><span data-stu-id="5adff-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="5adff-492">否</span><span class="sxs-lookup"><span data-stu-id="5adff-492">No</span></span>|  
|<span data-ttu-id="5adff-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="5adff-493">xsl:stylesheet</span></span>|<span data-ttu-id="5adff-494">根樣式表元素。</span><span class="sxs-lookup"><span data-stu-id="5adff-494">Root stylesheet element.</span></span> <span data-ttu-id="5adff-495">所有的項目和屬性內定義遵循 hello 標準[XSLT 規格](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="5adff-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="5adff-496">是</span><span class="sxs-lookup"><span data-stu-id="5adff-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5adff-497">使用量</span><span class="sxs-lookup"><span data-stu-id="5adff-497">Usage</span></span>  
 <span data-ttu-id="5adff-498">此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="5adff-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5adff-499">**原則區段︰**輸入、輸出</span><span class="sxs-lookup"><span data-stu-id="5adff-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="5adff-500">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="5adff-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="5adff-501">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5adff-501">Next steps</span></span>
<span data-ttu-id="5adff-502">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="5adff-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
