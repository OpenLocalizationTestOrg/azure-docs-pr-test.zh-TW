---
title: "Azure API 管理中的轉換原則 | Microsoft Docs"
description: "了解 Azure API 管理中可使用的轉換原則。"
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
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="f43e1-103">API 管理轉換原則</span><span class="sxs-lookup"><span data-stu-id="f43e1-103">API Management transformation policies</span></span>
<span data-ttu-id="f43e1-104">本主題提供下列 API 管理原則的參考。</span><span class="sxs-lookup"><span data-stu-id="f43e1-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="f43e1-105">如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="f43e1-106"><a name="TransformationPolicies"></a> 轉換原則</span><span class="sxs-lookup"><span data-stu-id="f43e1-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="f43e1-107">[將 JSON 轉換成 XML](api-management-transformation-policies.md#ConvertJSONtoXML) - 將要求或回應內文從 JSON 轉換成 XML。</span><span class="sxs-lookup"><span data-stu-id="f43e1-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="f43e1-108">[將 XML 轉換成 JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - 將要求或回應內文從 XML 轉換成 JSON。</span><span class="sxs-lookup"><span data-stu-id="f43e1-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="f43e1-109">[在內文中尋找並取代字串](api-management-transformation-policies.md#Findandreplacestringinbody) - 尋找要求或回應子字串，並將它取代為其他子字串。</span><span class="sxs-lookup"><span data-stu-id="f43e1-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="f43e1-110">[遮罩內容中的 URL](api-management-transformation-policies.md#MaskURLSContent) - 重寫 (遮罩) 回應內文的連結，使其經由閘道器指向同等的連結。</span><span class="sxs-lookup"><span data-stu-id="f43e1-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="f43e1-111">[設定後端服務](api-management-transformation-policies.md#SetBackendService) - 變更傳入要求的後端服務。</span><span class="sxs-lookup"><span data-stu-id="f43e1-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="f43e1-112">[設定本文](api-management-transformation-policies.md#SetBody) - 設定傳入和傳出要求的訊息本文。</span><span class="sxs-lookup"><span data-stu-id="f43e1-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="f43e1-113">[設定 HTTP 標頭](api-management-transformation-policies.md#SetHTTPheader) - 指派值給現有的回應及/或要求標頭，或加入新的回應及/或要求標頭。</span><span class="sxs-lookup"><span data-stu-id="f43e1-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="f43e1-114">[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter) - 新增、取代值或刪除要求查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="f43e1-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="f43e1-115">[重寫 URL](api-management-transformation-policies.md#RewriteURL) - 將要求 URL 從公用格式轉換成 Web 服務所需的格式。</span><span class="sxs-lookup"><span data-stu-id="f43e1-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="f43e1-116">[使用 XSLT 轉換 XML](api-management-transformation-policies.md#XSLTransform) - 將 XSL 轉換套用至要求或回應本文中的 XML。</span><span class="sxs-lookup"><span data-stu-id="f43e1-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="f43e1-117"><a name="ConvertJSONtoXML"></a> 將 JSON 轉換成 XML</span><span class="sxs-lookup"><span data-stu-id="f43e1-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="f43e1-118">`json-to-xml` 原則將要求或回應本文從 JSON 轉換成 XML。</span><span class="sxs-lookup"><span data-stu-id="f43e1-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-119">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="f43e1-120">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="f43e1-121">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-121">Elements</span></span>  
  
|<span data-ttu-id="f43e1-122">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-122">Name</span></span>|<span data-ttu-id="f43e1-123">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-123">Description</span></span>|<span data-ttu-id="f43e1-124">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="f43e1-125">json-to-xml</span></span>|<span data-ttu-id="f43e1-126">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-126">Root element.</span></span>|<span data-ttu-id="f43e1-127">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f43e1-128">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-128">Attributes</span></span>  
  
|<span data-ttu-id="f43e1-129">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-129">Name</span></span>|<span data-ttu-id="f43e1-130">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-130">Description</span></span>|<span data-ttu-id="f43e1-131">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-131">Required</span></span>|<span data-ttu-id="f43e1-132">預設值</span><span class="sxs-lookup"><span data-stu-id="f43e1-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f43e1-133">apply</span><span class="sxs-lookup"><span data-stu-id="f43e1-133">apply</span></span>|<span data-ttu-id="f43e1-134">此屬性必須設為下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="f43e1-135">-   always - 一律套用轉換。</span><span class="sxs-lookup"><span data-stu-id="f43e1-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="f43e1-136">-   content-type-json - 只有當回應中的 Content-type 標頭指出 JSON 存在時才轉換。</span><span class="sxs-lookup"><span data-stu-id="f43e1-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="f43e1-137">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-137">Yes</span></span>|<span data-ttu-id="f43e1-138">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-138">N/A</span></span>|  
|<span data-ttu-id="f43e1-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="f43e1-139">consider-accept-header</span></span>|<span data-ttu-id="f43e1-140">此屬性必須設為下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="f43e1-141">-   true - 如果在要求的 Accept 標頭中要求 JSON，才套用轉換。</span><span class="sxs-lookup"><span data-stu-id="f43e1-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="f43e1-142">-   false - 一律套用轉換。</span><span class="sxs-lookup"><span data-stu-id="f43e1-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="f43e1-143">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-143">No</span></span>|<span data-ttu-id="f43e1-144">true</span><span class="sxs-lookup"><span data-stu-id="f43e1-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f43e1-145">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-145">Usage</span></span>  
 <span data-ttu-id="f43e1-146">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-147">**原則區段︰**輸入、輸出、錯誤</span><span class="sxs-lookup"><span data-stu-id="f43e1-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="f43e1-148">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-149"><a name="ConvertXMLtoJSON"></a> 將 XML 轉換成 JSON</span><span class="sxs-lookup"><span data-stu-id="f43e1-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="f43e1-150">`xml-to-json` 原則將要求或回應本文從 XML 轉換成 JSON。</span><span class="sxs-lookup"><span data-stu-id="f43e1-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="f43e1-151">此原則可用於將架構在「僅使用 XML 的後端 Web 服務」上的 API 現代化。</span><span class="sxs-lookup"><span data-stu-id="f43e1-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-152">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="f43e1-153">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="f43e1-154">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-154">Elements</span></span>  
  
|<span data-ttu-id="f43e1-155">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-155">Name</span></span>|<span data-ttu-id="f43e1-156">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-156">Description</span></span>|<span data-ttu-id="f43e1-157">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="f43e1-158">xml-to-json</span></span>|<span data-ttu-id="f43e1-159">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-159">Root element.</span></span>|<span data-ttu-id="f43e1-160">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f43e1-161">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-161">Attributes</span></span>  
  
|<span data-ttu-id="f43e1-162">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-162">Name</span></span>|<span data-ttu-id="f43e1-163">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-163">Description</span></span>|<span data-ttu-id="f43e1-164">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-164">Required</span></span>|<span data-ttu-id="f43e1-165">預設值</span><span class="sxs-lookup"><span data-stu-id="f43e1-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f43e1-166">kind</span><span class="sxs-lookup"><span data-stu-id="f43e1-166">kind</span></span>|<span data-ttu-id="f43e1-167">此屬性必須設為下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="f43e1-168">-   javascript-friendly - 轉換後的 JSON 有 JavaScript 開發人員熟悉的格式。</span><span class="sxs-lookup"><span data-stu-id="f43e1-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="f43e1-169">-   direct -  | 轉換後的 JSON 可反映原始 XML 文件的結構。</span><span class="sxs-lookup"><span data-stu-id="f43e1-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="f43e1-170">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-170">Yes</span></span>|<span data-ttu-id="f43e1-171">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-171">N/A</span></span>|  
|<span data-ttu-id="f43e1-172">apply</span><span class="sxs-lookup"><span data-stu-id="f43e1-172">apply</span></span>|<span data-ttu-id="f43e1-173">此屬性必須設為下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="f43e1-174">-   always - 一律轉換。</span><span class="sxs-lookup"><span data-stu-id="f43e1-174">-   always - convert always.</span></span><br /><span data-ttu-id="f43e1-175">-   content-type-xml - 只有當回應中的 Content-type 標頭指出 XML 存在時才轉換。</span><span class="sxs-lookup"><span data-stu-id="f43e1-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="f43e1-176">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-176">Yes</span></span>|<span data-ttu-id="f43e1-177">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-177">N/A</span></span>|  
|<span data-ttu-id="f43e1-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="f43e1-178">consider-accept-header</span></span>|<span data-ttu-id="f43e1-179">此屬性必須設為下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="f43e1-180">-   true - 如果在要求的 Accept 標頭中要求 XML，才套用轉換。</span><span class="sxs-lookup"><span data-stu-id="f43e1-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="f43e1-181">-   false - 一律套用轉換。</span><span class="sxs-lookup"><span data-stu-id="f43e1-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="f43e1-182">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-182">No</span></span>|<span data-ttu-id="f43e1-183">true</span><span class="sxs-lookup"><span data-stu-id="f43e1-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f43e1-184">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-184">Usage</span></span>  
 <span data-ttu-id="f43e1-185">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-186">**原則區段︰**輸入、輸出、錯誤</span><span class="sxs-lookup"><span data-stu-id="f43e1-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="f43e1-187">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-188"><a name="Findandreplacestringinbody"></a> 在本文中尋找並取代字串</span><span class="sxs-lookup"><span data-stu-id="f43e1-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="f43e1-189">`find-and-replace` 原則會尋找要求或回應子字串，並取代為不同的子字串。</span><span class="sxs-lookup"><span data-stu-id="f43e1-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-190">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="f43e1-191">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="f43e1-192">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-192">Elements</span></span>  
  
|<span data-ttu-id="f43e1-193">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-193">Name</span></span>|<span data-ttu-id="f43e1-194">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-194">Description</span></span>|<span data-ttu-id="f43e1-195">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="f43e1-196">find-and-replace</span></span>|<span data-ttu-id="f43e1-197">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-197">Root element.</span></span>|<span data-ttu-id="f43e1-198">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f43e1-199">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-199">Attributes</span></span>  
  
|<span data-ttu-id="f43e1-200">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-200">Name</span></span>|<span data-ttu-id="f43e1-201">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-201">Description</span></span>|<span data-ttu-id="f43e1-202">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-202">Required</span></span>|<span data-ttu-id="f43e1-203">預設值</span><span class="sxs-lookup"><span data-stu-id="f43e1-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f43e1-204">from</span><span class="sxs-lookup"><span data-stu-id="f43e1-204">from</span></span>|<span data-ttu-id="f43e1-205">要搜尋的字串。</span><span class="sxs-lookup"><span data-stu-id="f43e1-205">The string to search for.</span></span>|<span data-ttu-id="f43e1-206">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-206">Yes</span></span>|<span data-ttu-id="f43e1-207">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-207">N/A</span></span>|  
|<span data-ttu-id="f43e1-208">to</span><span class="sxs-lookup"><span data-stu-id="f43e1-208">to</span></span>|<span data-ttu-id="f43e1-209">取代字串。</span><span class="sxs-lookup"><span data-stu-id="f43e1-209">The replacement string.</span></span> <span data-ttu-id="f43e1-210">指定零長度的取代字串可移除搜尋字串。</span><span class="sxs-lookup"><span data-stu-id="f43e1-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="f43e1-211">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-211">Yes</span></span>|<span data-ttu-id="f43e1-212">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f43e1-213">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-213">Usage</span></span>  
 <span data-ttu-id="f43e1-214">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-215">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="f43e1-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="f43e1-216">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-217"><a name="MaskURLSContent"></a> 遮罩內容中的 URL</span><span class="sxs-lookup"><span data-stu-id="f43e1-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="f43e1-218">`redirect-content-urls` 原則會重寫 (遮罩) 回應本文中的連結，使其經由閘道器指向同等的連結。</span><span class="sxs-lookup"><span data-stu-id="f43e1-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="f43e1-219">使用在輸出區段中，用以重新撰寫回應本文連結，使其指向閘道。</span><span class="sxs-lookup"><span data-stu-id="f43e1-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="f43e1-220">使用在輸入區段中則效果相反。</span><span class="sxs-lookup"><span data-stu-id="f43e1-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f43e1-221">此原則不會變更任何標頭值，如 `Location` 標頭。</span><span class="sxs-lookup"><span data-stu-id="f43e1-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="f43e1-222">若要變更標頭值，請使用 [set-header](api-management-transformation-policies.md#SetHTTPheader) 原則。</span><span class="sxs-lookup"><span data-stu-id="f43e1-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-223">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="f43e1-224">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="f43e1-225">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-225">Elements</span></span>  
  
|<span data-ttu-id="f43e1-226">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-226">Name</span></span>|<span data-ttu-id="f43e1-227">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-227">Description</span></span>|<span data-ttu-id="f43e1-228">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="f43e1-229">redirect-content-urls</span></span>|<span data-ttu-id="f43e1-230">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-230">Root element.</span></span>|<span data-ttu-id="f43e1-231">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f43e1-232">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-232">Usage</span></span>  
 <span data-ttu-id="f43e1-233">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-234">**原則區段︰**輸入、輸出</span><span class="sxs-lookup"><span data-stu-id="f43e1-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="f43e1-235">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-236"><a name="SetBackendService"></a> 設定後端服務</span><span class="sxs-lookup"><span data-stu-id="f43e1-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="f43e1-237">使用 `set-backend-service` 原則將傳入要求重新導向至不同的後端，而不是 API 設定中為該作業指定的後端。</span><span class="sxs-lookup"><span data-stu-id="f43e1-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="f43e1-238">此原則會將傳入要求中的後端服務基底 URL 變更為原則中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="f43e1-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-239">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="f43e1-240">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-240">Example</span></span>  
  
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
<span data-ttu-id="f43e1-241">在這個範例中，設定後端服務原則會根據查詢字串中傳遞的版本值，將要求路由傳送至不同於 API 指定的後端服務。</span><span class="sxs-lookup"><span data-stu-id="f43e1-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="f43e1-242">一開始的後端服務基底 URL 是來自 API 設定。</span><span class="sxs-lookup"><span data-stu-id="f43e1-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="f43e1-243">因此要求 URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` 變成 `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef`，其中 `http://contoso.com/api/10.4/` 是 API 設定中指定的後端服務 URL。</span><span class="sxs-lookup"><span data-stu-id="f43e1-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="f43e1-244">套用 [<choose\>](api-management-advanced-policies.md#choose) 原則陳述式後，後端服務基底 URL 可能再次變更，根據版本要求查詢參數的值變為 `http://contoso.com/api/8.2` 或 `http://contoso.com/api/9.1`。</span><span class="sxs-lookup"><span data-stu-id="f43e1-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="f43e1-245">例如，如果其值為 `"2013-15"`，最終的要求 URL 會變成 `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`。</span><span class="sxs-lookup"><span data-stu-id="f43e1-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="f43e1-246">如果需要進一步轉換要求，可使用其他[轉換原則](api-management-transformation-policies.md#TransformationPolicies)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="f43e1-247">例如，將要求路由傳送到版本特定後端之後要移除版本查詢參數，可使用[設定查詢字串參數](api-management-transformation-policies.md#SetQueryStringParameter)原則移除現在變得多餘的版本屬性。</span><span class="sxs-lookup"><span data-stu-id="f43e1-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="f43e1-248">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-248">Example</span></span>  
  
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
<span data-ttu-id="f43e1-249">在此範例中，原則會將要求傳送至 Service Fabric 後端，使用 userId 查詢字串作為資料分割索引鍵，以及使用資料分割的主要複本。</span><span class="sxs-lookup"><span data-stu-id="f43e1-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="f43e1-250">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-250">Elements</span></span>  
  
|<span data-ttu-id="f43e1-251">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-251">Name</span></span>|<span data-ttu-id="f43e1-252">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-252">Description</span></span>|<span data-ttu-id="f43e1-253">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="f43e1-254">set-backend-service</span></span>|<span data-ttu-id="f43e1-255">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-255">Root element.</span></span>|<span data-ttu-id="f43e1-256">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f43e1-257">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-257">Attributes</span></span>  
  
|<span data-ttu-id="f43e1-258">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-258">Name</span></span>|<span data-ttu-id="f43e1-259">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-259">Description</span></span>|<span data-ttu-id="f43e1-260">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-260">Required</span></span>|<span data-ttu-id="f43e1-261">預設值</span><span class="sxs-lookup"><span data-stu-id="f43e1-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f43e1-262">base-url</span><span class="sxs-lookup"><span data-stu-id="f43e1-262">base-url</span></span>|<span data-ttu-id="f43e1-263">新的後端服務基底 URL。</span><span class="sxs-lookup"><span data-stu-id="f43e1-263">New backend service base URL.</span></span>|<span data-ttu-id="f43e1-264">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-264">No</span></span>|<span data-ttu-id="f43e1-265">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-265">N/A</span></span>|  
|<span data-ttu-id="f43e1-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="f43e1-266">backend-id</span></span>|<span data-ttu-id="f43e1-267">要傳送至的後端識別碼。</span><span class="sxs-lookup"><span data-stu-id="f43e1-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="f43e1-268">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-268">No</span></span>|<span data-ttu-id="f43e1-269">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-269">N/A</span></span>|  
|<span data-ttu-id="f43e1-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="f43e1-270">sf-partition-key</span></span>|<span data-ttu-id="f43e1-271">僅適用於後端為 Service Fabric 服務並使用 'backend-id' 指定時。</span><span class="sxs-lookup"><span data-stu-id="f43e1-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="f43e1-272">用於從名稱解析服務解析特定資料分割。</span><span class="sxs-lookup"><span data-stu-id="f43e1-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="f43e1-273">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-273">No</span></span>|<span data-ttu-id="f43e1-274">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-274">N/A</span></span>|  
|<span data-ttu-id="f43e1-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="f43e1-275">sf-replica-type</span></span>|<span data-ttu-id="f43e1-276">僅適用於後端為 Service Fabric 服務並使用 'backend-id' 指定時。</span><span class="sxs-lookup"><span data-stu-id="f43e1-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="f43e1-277">控制要求應移至資料分割的主要或次要複本。</span><span class="sxs-lookup"><span data-stu-id="f43e1-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="f43e1-278">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-278">No</span></span>|<span data-ttu-id="f43e1-279">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-279">N/A</span></span>|    
|<span data-ttu-id="f43e1-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="f43e1-280">sf-resolve-condition</span></span>|<span data-ttu-id="f43e1-281">僅適用於後端為 Service Fabric 服務時。</span><span class="sxs-lookup"><span data-stu-id="f43e1-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="f43e1-282">識別新的解析是否必須重複呼叫 Service Fabric 後端的條件。</span><span class="sxs-lookup"><span data-stu-id="f43e1-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="f43e1-283">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-283">No</span></span>|<span data-ttu-id="f43e1-284">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-284">N/A</span></span>|    
|<span data-ttu-id="f43e1-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="f43e1-285">sf-service-instance-name</span></span>|<span data-ttu-id="f43e1-286">僅適用於後端為 Service Fabric 服務時。</span><span class="sxs-lookup"><span data-stu-id="f43e1-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="f43e1-287">允許在執行階段變更服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="f43e1-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="f43e1-288">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-288">No</span></span>|<span data-ttu-id="f43e1-289">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="f43e1-290">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-290">Usage</span></span>  
 <span data-ttu-id="f43e1-291">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-292">**原則區段︰**輸入、後端</span><span class="sxs-lookup"><span data-stu-id="f43e1-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="f43e1-293">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-294"><a name="SetBody"></a> 設定本文</span><span class="sxs-lookup"><span data-stu-id="f43e1-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="f43e1-295">使用 `set-body` 原則來設定傳入和傳出要求的訊息本文。</span><span class="sxs-lookup"><span data-stu-id="f43e1-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="f43e1-296">若要存取訊息本文，您可以使用 `context.Request.Body` 屬性或 `context.Response.Body`，取決於原則是在輸入或輸出區段中。</span><span class="sxs-lookup"><span data-stu-id="f43e1-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="f43e1-297">請注意，根據預設，當您使用 `context.Request.Body` 或 `context.Response.Body` 存取訊息本文，原始訊息本文會遺失，且必須在運算式中傳回本文加以設置。</span><span class="sxs-lookup"><span data-stu-id="f43e1-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="f43e1-298">若要保留本文內容，存取訊息時將 `preserveContent` 參數設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="f43e1-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="f43e1-299">如果 `preserveContent` 設為 `true`，且運算式傳回不同的本文，則會使用傳回的本文。</span><span class="sxs-lookup"><span data-stu-id="f43e1-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="f43e1-300">使用 `set-body` 原則時請注意下列事項。</span><span class="sxs-lookup"><span data-stu-id="f43e1-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="f43e1-301">如果您使用 `set-body` 原則來傳回新的或更新的本文，您不需要將 `preserveContent` 設為 `true`，因為您已明確地提供新的本文內容。</span><span class="sxs-lookup"><span data-stu-id="f43e1-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="f43e1-302">在輸入管線中保留回應的內容沒有意義，因為尚無回應。</span><span class="sxs-lookup"><span data-stu-id="f43e1-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="f43e1-303">在輸出管線中保留要求的內容沒有意義，因為此時要求已傳送至後端。</span><span class="sxs-lookup"><span data-stu-id="f43e1-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="f43e1-304">如果在沒有任何訊息本文時使用此原則，例如輸入 GET，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f43e1-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="f43e1-305">如需詳細資訊，請參閱[內容變數](api-management-policy-expressions.md#ContextVariables)表中 `context.Request.Body`、`context.Response.Body`、`IMessage` 的部分。</span><span class="sxs-lookup"><span data-stu-id="f43e1-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-306">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="f43e1-307">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="f43e1-308">常值文字範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="f43e1-309">以字串存取本文的範例。</span><span class="sxs-lookup"><span data-stu-id="f43e1-309">Example accessing the body as a string.</span></span> <span data-ttu-id="f43e1-310">請注意，我們會保留原始要求本文，以在稍後於管線中存取它。</span><span class="sxs-lookup"><span data-stu-id="f43e1-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
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
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="f43e1-311">以 JObject 存取本文的範例。</span><span class="sxs-lookup"><span data-stu-id="f43e1-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="f43e1-312">請注意，由於我們不會保留原始要求本文，若在稍後於管線中存取它，將會導致例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f43e1-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="f43e1-313">根據產品篩選回應</span><span class="sxs-lookup"><span data-stu-id="f43e1-313">Filter response based on product</span></span>  
 <span data-ttu-id="f43e1-314">這個範例示範如何在使用 `Starter` 產品時，移除「從後端服務收到的回應」中的資料元素，藉此執行內容篩選。</span><span class="sxs-lookup"><span data-stu-id="f43e1-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="f43e1-315">如需設定和使用此原則的示範，請觀賞 [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)，快轉到 34:30。</span><span class="sxs-lookup"><span data-stu-id="f43e1-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="f43e1-316">從 31:50 處開始觀賞用於本示範的 [The Dark Sky Forecast API](https://developer.forecast.io/) 概觀。</span><span class="sxs-lookup"><span data-stu-id="f43e1-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="f43e1-317">使用 Liquid 範本搭配設定本文</span><span class="sxs-lookup"><span data-stu-id="f43e1-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="f43e1-318">您可以設定讓 `set-body` 原則使用 [Liquid](https://shopify.github.io/liquid/basics/introduction/) 範本化語言來轉換要求或回應的本文。</span><span class="sxs-lookup"><span data-stu-id="f43e1-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="f43e1-319">如果您需要完全重設訊息的格式，這會非常有效。</span><span class="sxs-lookup"><span data-stu-id="f43e1-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f43e1-320">`set-body` 原則中使用的 Liquid 實作是在「 C# 模式」下設定。</span><span class="sxs-lookup"><span data-stu-id="f43e1-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="f43e1-321">這在進行篩選之類的操作時尤其重要。</span><span class="sxs-lookup"><span data-stu-id="f43e1-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="f43e1-322">舉例來說，使用日期篩選需要使用 Pascal 大小寫慣例和 C# 日期格是，例如：</span><span class="sxs-lookup"><span data-stu-id="f43e1-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="f43e1-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="f43e1-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f43e1-324">為了使用 Liquid 範本來正確地繫結至 XML 主體，請使用 `set-header` 原則將 Content-Type 設定為 application/xml、text/xml (或任何結尾為 +xml 的類型)；如果是 JSON 主體，則必須是 application/json、text/json (或任何結尾為 +json 的類型)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="f43e1-325">使用 Liquid 範本將 JSON 轉換成 SOAP</span><span class="sxs-lookup"><span data-stu-id="f43e1-325">Convert JSON to SOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="f43e1-326">使用 Liquid 範本來轉換 JSON</span><span class="sxs-lookup"><span data-stu-id="f43e1-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="f43e1-327">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-327">Elements</span></span>  
  
|<span data-ttu-id="f43e1-328">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-328">Name</span></span>|<span data-ttu-id="f43e1-329">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-329">Description</span></span>|<span data-ttu-id="f43e1-330">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-331">set-body</span><span class="sxs-lookup"><span data-stu-id="f43e1-331">set-body</span></span>|<span data-ttu-id="f43e1-332">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-332">Root element.</span></span> <span data-ttu-id="f43e1-333">包含本文文字或會傳回本文的運算式。</span><span class="sxs-lookup"><span data-stu-id="f43e1-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="f43e1-334">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="f43e1-335">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-335">Properties</span></span>  
  
|<span data-ttu-id="f43e1-336">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-336">Name</span></span>|<span data-ttu-id="f43e1-337">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-337">Description</span></span>|<span data-ttu-id="f43e1-338">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-338">Required</span></span>|<span data-ttu-id="f43e1-339">預設值</span><span class="sxs-lookup"><span data-stu-id="f43e1-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f43e1-340">template</span><span class="sxs-lookup"><span data-stu-id="f43e1-340">template</span></span>|<span data-ttu-id="f43e1-341">用來變更設定本文原則將在其中執行的範本化模式。</span><span class="sxs-lookup"><span data-stu-id="f43e1-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="f43e1-342">目前唯一支援的值為：</span><span class="sxs-lookup"><span data-stu-id="f43e1-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="f43e1-343">- liquid - 設定本文原則將會使用 Liquid 範本化引擎</span><span class="sxs-lookup"><span data-stu-id="f43e1-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="f43e1-344">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-344">No</span></span>|<span data-ttu-id="f43e1-345">liquid</span><span class="sxs-lookup"><span data-stu-id="f43e1-345">liquid</span></span>|  

<span data-ttu-id="f43e1-346">為了存取要求與回應的相關資訊，Liquid 範本可以繫結至具有下列屬性的內容物件：</span><span class="sxs-lookup"><span data-stu-id="f43e1-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="f43e1-347">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-347">Usage</span></span>  
 <span data-ttu-id="f43e1-348">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-349">**原則區段︰**輸入、輸出、後端</span><span class="sxs-lookup"><span data-stu-id="f43e1-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="f43e1-350">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-351"><a name="SetHTTPheader"></a> 設定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="f43e1-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="f43e1-352">`set-header` 原則會指派值給現有的回應及/或要求標頭，或加入新的回應及/或要求標頭。</span><span class="sxs-lookup"><span data-stu-id="f43e1-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="f43e1-353">將 HTTP 標頭清單插入至 HTTP 訊息中。</span><span class="sxs-lookup"><span data-stu-id="f43e1-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="f43e1-354">放在輸入管線中時，此原則會為傳遞至目標服務的要求設定 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="f43e1-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="f43e1-355">放在輸出管線中時，此原則會為傳送至閘道器用戶端的回應設定 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="f43e1-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-356">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="f43e1-357">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="f43e1-358">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="f43e1-359">將內容資訊轉寄到後端服務</span><span class="sxs-lookup"><span data-stu-id="f43e1-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="f43e1-360">這個範例示範如何在 API 層級套用，以提供後端服務的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="f43e1-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="f43e1-361">如需設定和使用此原則的示範，請觀賞 [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)，快轉到 10:30。</span><span class="sxs-lookup"><span data-stu-id="f43e1-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="f43e1-362">12:10 處是在開發人員入口網站中呼叫作業的示範，您可以看到「原則」的運作。</span><span class="sxs-lookup"><span data-stu-id="f43e1-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="f43e1-363">如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="f43e1-364">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-364">Elements</span></span>  
  
|<span data-ttu-id="f43e1-365">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-365">Name</span></span>|<span data-ttu-id="f43e1-366">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-366">Description</span></span>|<span data-ttu-id="f43e1-367">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-368">set-header</span><span class="sxs-lookup"><span data-stu-id="f43e1-368">set-header</span></span>|<span data-ttu-id="f43e1-369">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-369">Root element.</span></span>|<span data-ttu-id="f43e1-370">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-370">Yes</span></span>|  
|<span data-ttu-id="f43e1-371">value</span><span class="sxs-lookup"><span data-stu-id="f43e1-371">value</span></span>|<span data-ttu-id="f43e1-372">指定要設定之標頭的值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="f43e1-373">若多個標頭有相同名稱，請額外加入 `value` 元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="f43e1-374">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="f43e1-375">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-375">Properties</span></span>  
  
|<span data-ttu-id="f43e1-376">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-376">Name</span></span>|<span data-ttu-id="f43e1-377">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-377">Description</span></span>|<span data-ttu-id="f43e1-378">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-378">Required</span></span>|<span data-ttu-id="f43e1-379">預設值</span><span class="sxs-lookup"><span data-stu-id="f43e1-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f43e1-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="f43e1-380">exists-action</span></span>|<span data-ttu-id="f43e1-381">指定當已指定標頭時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="f43e1-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="f43e1-382">此屬性必須具有下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="f43e1-383">-   override - 取代現有標頭的值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="f43e1-384">-   skip - 不取代現有的標頭值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="f43e1-385">-   append - 將值附加至現有標頭值之後。</span><span class="sxs-lookup"><span data-stu-id="f43e1-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="f43e1-386">-   delete - 移除要求中的標頭。</span><span class="sxs-lookup"><span data-stu-id="f43e1-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="f43e1-387">設為 `override` 時，編列多個相同名稱的項目會導致根據所有項目來設定標頭 (列出多次)；只有列出的值才會設定在結果中。</span><span class="sxs-lookup"><span data-stu-id="f43e1-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="f43e1-388">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-388">No</span></span>|<span data-ttu-id="f43e1-389">override</span><span class="sxs-lookup"><span data-stu-id="f43e1-389">override</span></span>|  
|<span data-ttu-id="f43e1-390">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-390">name</span></span>|<span data-ttu-id="f43e1-391">指定要設定之標頭的名稱。</span><span class="sxs-lookup"><span data-stu-id="f43e1-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="f43e1-392">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-392">Yes</span></span>|<span data-ttu-id="f43e1-393">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f43e1-394">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-394">Usage</span></span>  
 <span data-ttu-id="f43e1-395">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-396">**原則區段︰**輸入、輸出、後端、錯誤</span><span class="sxs-lookup"><span data-stu-id="f43e1-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="f43e1-397">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-398"><a name="SetQueryStringParameter"></a> 設定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="f43e1-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="f43e1-399">`set-query-parameter` 原則會新增、取代值或刪除要求查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="f43e1-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="f43e1-400">可用來傳遞後端服務所需的查詢參數，為選擇性或從未存在於要求中。</span><span class="sxs-lookup"><span data-stu-id="f43e1-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-401">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="f43e1-402">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="f43e1-403">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="f43e1-404">將內容資訊轉寄到後端服務</span><span class="sxs-lookup"><span data-stu-id="f43e1-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="f43e1-405">這個範例示範如何在 API 層級套用，以提供後端服務的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="f43e1-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="f43e1-406">如需設定和使用此原則的示範，請觀賞 [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)，快轉到 10:30。</span><span class="sxs-lookup"><span data-stu-id="f43e1-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="f43e1-407">12:10 處是在開發人員入口網站中呼叫作業的示範，您可以看到「原則」的運作。</span><span class="sxs-lookup"><span data-stu-id="f43e1-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="f43e1-408">如需詳細資訊，請參閱[原則運算式](api-management-policy-expressions.md)和[內容變數](api-management-policy-expressions.md#ContextVariables)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="f43e1-409">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-409">Elements</span></span>  
  
|<span data-ttu-id="f43e1-410">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-410">Name</span></span>|<span data-ttu-id="f43e1-411">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-411">Description</span></span>|<span data-ttu-id="f43e1-412">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="f43e1-413">set-query-parameter</span></span>|<span data-ttu-id="f43e1-414">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-414">Root element.</span></span>|<span data-ttu-id="f43e1-415">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-415">Yes</span></span>|  
|<span data-ttu-id="f43e1-416">value</span><span class="sxs-lookup"><span data-stu-id="f43e1-416">value</span></span>|<span data-ttu-id="f43e1-417">指定要設定之查詢參數的值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="f43e1-418">若多個查詢參數有相同名稱，請額外加入 `value` 元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="f43e1-419">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="f43e1-420">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-420">Properties</span></span>  
  
|<span data-ttu-id="f43e1-421">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-421">Name</span></span>|<span data-ttu-id="f43e1-422">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-422">Description</span></span>|<span data-ttu-id="f43e1-423">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-423">Required</span></span>|<span data-ttu-id="f43e1-424">預設值</span><span class="sxs-lookup"><span data-stu-id="f43e1-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f43e1-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="f43e1-425">exists-action</span></span>|<span data-ttu-id="f43e1-426">指定當已指定查詢參數時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="f43e1-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="f43e1-427">此屬性必須具有下列其中一個值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="f43e1-428">-   override - 取代現有參數的值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="f43e1-429">-   skip - 不取代現有的查詢參數值。</span><span class="sxs-lookup"><span data-stu-id="f43e1-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="f43e1-430">-   append - 將值附加至現有查詢參數值之後。</span><span class="sxs-lookup"><span data-stu-id="f43e1-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="f43e1-431">-   delete - 移除要求中的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="f43e1-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="f43e1-432">設為 `override` 時，編列多個相同名稱的項目會導致根據所有項目來設定查詢參數 (列出多次)；只有列出的值才會設定在結果中。</span><span class="sxs-lookup"><span data-stu-id="f43e1-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="f43e1-433">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-433">No</span></span>|<span data-ttu-id="f43e1-434">override</span><span class="sxs-lookup"><span data-stu-id="f43e1-434">override</span></span>|  
|<span data-ttu-id="f43e1-435">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-435">name</span></span>|<span data-ttu-id="f43e1-436">指定要設定之查詢參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="f43e1-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="f43e1-437">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-437">Yes</span></span>|<span data-ttu-id="f43e1-438">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f43e1-439">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-439">Usage</span></span>  
 <span data-ttu-id="f43e1-440">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-441">**原則區段︰**輸入、後端</span><span class="sxs-lookup"><span data-stu-id="f43e1-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="f43e1-442">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-443"><a name="RewriteURL"></a> 重寫 URL</span><span class="sxs-lookup"><span data-stu-id="f43e1-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="f43e1-444">`rewrite-uri` 原則會將要求 URL 從公用格式轉換成 Web 服務所需的格式，如以下範例中所示。</span><span class="sxs-lookup"><span data-stu-id="f43e1-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="f43e1-445">公用 URL - `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="f43e1-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="f43e1-446">要求 URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="f43e1-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="f43e1-447">應該將一般人及/或瀏覽器可理解的 URL 轉換成 Web 服務所需的 URL 格式時，可使用此原則。</span><span class="sxs-lookup"><span data-stu-id="f43e1-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="f43e1-448">只有在公開替代 URL 格式時需要套用此原則；例如，簡潔 URL、RESTful URL、使用者易記 URL 或符合 SEO 的 URL 等單純的結構式 URL 格式，不含查詢字串，只包含資源的路徑 (在配置和授權後面)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="f43e1-449">這樣做通常是基於美觀、實用性或搜尋引擎最佳化 (SEO) 目的。</span><span class="sxs-lookup"><span data-stu-id="f43e1-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f43e1-450">使用此原則只能加入查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="f43e1-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="f43e1-451">無法在重寫 URL 中加入額外的範本路徑參數。</span><span class="sxs-lookup"><span data-stu-id="f43e1-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="f43e1-452">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="f43e1-453">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="f43e1-454">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-454">Elements</span></span>  
  
|<span data-ttu-id="f43e1-455">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-455">Name</span></span>|<span data-ttu-id="f43e1-456">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-456">Description</span></span>|<span data-ttu-id="f43e1-457">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="f43e1-458">rewrite-uri</span></span>|<span data-ttu-id="f43e1-459">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-459">Root element.</span></span>|<span data-ttu-id="f43e1-460">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f43e1-461">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-461">Attributes</span></span>  
  
|<span data-ttu-id="f43e1-462">屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-462">Attribute</span></span>|<span data-ttu-id="f43e1-463">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-463">Description</span></span>|<span data-ttu-id="f43e1-464">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-464">Required</span></span>|<span data-ttu-id="f43e1-465">預設值</span><span class="sxs-lookup"><span data-stu-id="f43e1-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="f43e1-466">template</span><span class="sxs-lookup"><span data-stu-id="f43e1-466">template</span></span>|<span data-ttu-id="f43e1-467">含有任何查詢字串參數的實際 Web 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="f43e1-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="f43e1-468">使用運算式時，整個值必須是運算式。</span><span class="sxs-lookup"><span data-stu-id="f43e1-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="f43e1-469">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-469">Yes</span></span>|<span data-ttu-id="f43e1-470">N/A</span><span class="sxs-lookup"><span data-stu-id="f43e1-470">N/A</span></span>|  
|<span data-ttu-id="f43e1-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="f43e1-471">copy-unmatched-params</span></span>|<span data-ttu-id="f43e1-472">指定當連入要求中查詢參數不存在於原始 URL 範本時，是否要將它新增到由重寫範本所定義的 URL</span><span class="sxs-lookup"><span data-stu-id="f43e1-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="f43e1-473">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-473">No</span></span>|<span data-ttu-id="f43e1-474">true</span><span class="sxs-lookup"><span data-stu-id="f43e1-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f43e1-475">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-475">Usage</span></span>  
 <span data-ttu-id="f43e1-476">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-477">**原則區段︰**輸入</span><span class="sxs-lookup"><span data-stu-id="f43e1-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f43e1-478">**原則範圍︰**產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="f43e1-479"><a name="XSLTransform"></a> 使用 XSLT 轉換 XML</span><span class="sxs-lookup"><span data-stu-id="f43e1-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="f43e1-480">`Transform XML using an XSLT` 原則會將 XSL 轉換套用至要求或回應本文中的 XML。</span><span class="sxs-lookup"><span data-stu-id="f43e1-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f43e1-481">原則陳述式</span><span class="sxs-lookup"><span data-stu-id="f43e1-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="f43e1-482">範例</span><span class="sxs-lookup"><span data-stu-id="f43e1-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="f43e1-483">元素</span><span class="sxs-lookup"><span data-stu-id="f43e1-483">Elements</span></span>  
  
|<span data-ttu-id="f43e1-484">名稱</span><span class="sxs-lookup"><span data-stu-id="f43e1-484">Name</span></span>|<span data-ttu-id="f43e1-485">說明</span><span class="sxs-lookup"><span data-stu-id="f43e1-485">Description</span></span>|<span data-ttu-id="f43e1-486">必要</span><span class="sxs-lookup"><span data-stu-id="f43e1-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f43e1-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="f43e1-487">xsl-transform</span></span>|<span data-ttu-id="f43e1-488">根元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-488">Root element.</span></span>|<span data-ttu-id="f43e1-489">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-489">Yes</span></span>|  
|<span data-ttu-id="f43e1-490">參數</span><span class="sxs-lookup"><span data-stu-id="f43e1-490">parameter</span></span>|<span data-ttu-id="f43e1-491">用於定義轉換中使用的變數</span><span class="sxs-lookup"><span data-stu-id="f43e1-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="f43e1-492">否</span><span class="sxs-lookup"><span data-stu-id="f43e1-492">No</span></span>|  
|<span data-ttu-id="f43e1-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="f43e1-493">xsl:stylesheet</span></span>|<span data-ttu-id="f43e1-494">根樣式表元素。</span><span class="sxs-lookup"><span data-stu-id="f43e1-494">Root stylesheet element.</span></span> <span data-ttu-id="f43e1-495">遵循 [XSLT 規格](http://www.w3.org/TR/xslt)標準定義的所有的元素和屬性</span><span class="sxs-lookup"><span data-stu-id="f43e1-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="f43e1-496">是</span><span class="sxs-lookup"><span data-stu-id="f43e1-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f43e1-497">使用量</span><span class="sxs-lookup"><span data-stu-id="f43e1-497">Usage</span></span>  
 <span data-ttu-id="f43e1-498">此原則可用於下列原則[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f43e1-499">**原則區段︰**輸入、輸出</span><span class="sxs-lookup"><span data-stu-id="f43e1-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="f43e1-500">**原則範圍︰**全域、產品、API、作業</span><span class="sxs-lookup"><span data-stu-id="f43e1-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="f43e1-501">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f43e1-501">Next steps</span></span>
<span data-ttu-id="f43e1-502">如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="f43e1-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
