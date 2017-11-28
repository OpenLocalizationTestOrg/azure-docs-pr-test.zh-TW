---
title: "媒體服務作業 REST API 概觀 | Microsoft Docs"
description: "媒體服務 REST API 概觀"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: eada8f2bcd2488d5ed36b0c24aa3d1b917815517
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-operations-rest-api-overview"></a><span data-ttu-id="222ba-103">媒體服務作業 REST API 概觀</span><span class="sxs-lookup"><span data-stu-id="222ba-103">Media Services operations REST API overview</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="222ba-104">**媒體服務作業 REST** API 用於建立作業、資產、存取原則，以及媒體服務帳戶中物件上的其他作業。</span><span class="sxs-lookup"><span data-stu-id="222ba-104">The **Media Services Operations REST** API is used for creating jobs, assets, access policies, and other operations on objects in a Media Service account.</span></span> <span data-ttu-id="222ba-105">如需詳細資訊，請參閱[媒體服務作業 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="222ba-105">For more information, see [Media Services Operations REST API reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>

<span data-ttu-id="222ba-106">Microsoft Azure 媒體服務會接受以 OData 為基礎的 HTTP 要求，而且可以使用詳細資訊 JSON 或 atom+pub 回應。</span><span class="sxs-lookup"><span data-stu-id="222ba-106">Microsoft Azure Media Services is a service that accepts OData-based HTTP requests and can respond back in verbose JSON or atom+pub.</span></span> <span data-ttu-id="222ba-107">由於媒體服務符合 Azure 設計指導方針，因此在連線到媒體服務時，每個用戶端都必須使用一組必要的 HTTP 標頭，以及一組可以使用的選擇性標頭。</span><span class="sxs-lookup"><span data-stu-id="222ba-107">Because Media Services conforms to Azure design guidelines, there is a set of required HTTP headers that each client must use when connecting to Media Services, as well as a set of optional headers that can be used.</span></span> <span data-ttu-id="222ba-108">下列章節描述建立要求及接收來自媒體服務的回應時可以使用的標頭和 HTTP 指令動詞。</span><span class="sxs-lookup"><span data-stu-id="222ba-108">The following sections describe the headers and HTTP verbs you can use when creating requests and receiving responses from Media Services.</span></span>

<span data-ttu-id="222ba-109">本主題提供如何使用 REST v2 搭配媒體服務的概觀。</span><span class="sxs-lookup"><span data-stu-id="222ba-109">This topic gives an overview of how to use REST v2 with Media Services.</span></span>

## <a name="considerations"></a><span data-ttu-id="222ba-110">考量</span><span class="sxs-lookup"><span data-stu-id="222ba-110">Considerations</span></span>

<span data-ttu-id="222ba-111">使用 REST 時須考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="222ba-111">The following considerations apply when using REST.</span></span>

* <span data-ttu-id="222ba-112">查詢項目時，有一次最多傳回 1000 個實體的限制，因為公用 REST v2 有 1000 個查詢結果數目的限制。</span><span class="sxs-lookup"><span data-stu-id="222ba-112">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="222ba-113">您需要使用 **Skip** 和 **Take** (.NET)/ **top** (REST)，如[此 .NET 範例](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities)和[此 REST API 範例](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)中所述。</span><span class="sxs-lookup"><span data-stu-id="222ba-113">You need to use **Skip** and **Take** (.NET)/ **top** (REST) as described in [this .NET example](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) and [this REST API example](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities).</span></span> 
* <span data-ttu-id="222ba-114">使用 JSON 並指定在要求中使用 **__metadata** 關鍵字時 (例如，為了參考連結的物件)，您「必須」將 **Accept** 標頭設為 [JSON Verbose 格式](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (請參閱下列範例)。</span><span class="sxs-lookup"><span data-stu-id="222ba-114">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object) you MUST set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (see the following example).</span></span> <span data-ttu-id="222ba-115">Odata 並不了解要求中的 **__metadata** 屬性，除非您將它設為 verbose。</span><span class="sxs-lookup"><span data-stu-id="222ba-115">Odata does not understand the **__metadata** property in the request, unless you set it to verbose.</span></span>  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a><span data-ttu-id="222ba-116">媒體服務支援的標準 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="222ba-116">Standard HTTP request headers supported by Media Services</span></span>
<span data-ttu-id="222ba-117">您對媒體服務每次呼叫，有一組必須在要求中包含的必要標頭，以及一組可能會想要包含的選擇性標頭。</span><span class="sxs-lookup"><span data-stu-id="222ba-117">For every call you make into Media Services, there is a set of required headers you must include in your request and also a set of optional headers you may want to include.</span></span> <span data-ttu-id="222ba-118">下表列出必要標頭：</span><span class="sxs-lookup"><span data-stu-id="222ba-118">The following table lists the required headers:</span></span>

| <span data-ttu-id="222ba-119">頁首</span><span class="sxs-lookup"><span data-stu-id="222ba-119">Header</span></span> | <span data-ttu-id="222ba-120">類型</span><span class="sxs-lookup"><span data-stu-id="222ba-120">Type</span></span> | <span data-ttu-id="222ba-121">值</span><span class="sxs-lookup"><span data-stu-id="222ba-121">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222ba-122">Authorization</span><span class="sxs-lookup"><span data-stu-id="222ba-122">Authorization</span></span> |<span data-ttu-id="222ba-123">Bearer</span><span class="sxs-lookup"><span data-stu-id="222ba-123">Bearer</span></span> |<span data-ttu-id="222ba-124">Bearer 是唯一接受的授權機制。</span><span class="sxs-lookup"><span data-stu-id="222ba-124">Bearer is the only accepted authorization mechanism.</span></span> <span data-ttu-id="222ba-125">此值也必須包含 ACS 所提供的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="222ba-125">The value must also include the access token provided by ACS.</span></span> |
| <span data-ttu-id="222ba-126">x-ms-version</span><span class="sxs-lookup"><span data-stu-id="222ba-126">x-ms-version</span></span> |<span data-ttu-id="222ba-127">十進位</span><span class="sxs-lookup"><span data-stu-id="222ba-127">Decimal</span></span> |<span data-ttu-id="222ba-128">2.11</span><span class="sxs-lookup"><span data-stu-id="222ba-128">2.11</span></span> |
| <span data-ttu-id="222ba-129">DataServiceVersion</span><span class="sxs-lookup"><span data-stu-id="222ba-129">DataServiceVersion</span></span> |<span data-ttu-id="222ba-130">十進位</span><span class="sxs-lookup"><span data-stu-id="222ba-130">Decimal</span></span> |<span data-ttu-id="222ba-131">3.0</span><span class="sxs-lookup"><span data-stu-id="222ba-131">3.0</span></span> |
| <span data-ttu-id="222ba-132">MaxDataServiceVersion</span><span class="sxs-lookup"><span data-stu-id="222ba-132">MaxDataServiceVersion</span></span> |<span data-ttu-id="222ba-133">十進位</span><span class="sxs-lookup"><span data-stu-id="222ba-133">Decimal</span></span> |<span data-ttu-id="222ba-134">3.0</span><span class="sxs-lookup"><span data-stu-id="222ba-134">3.0</span></span> |

> [!NOTE]
> <span data-ttu-id="222ba-135">媒體服務使用 OData 來透過 REST API 公開其基礎資產中繼資料儲存機制，因此 DataServiceVersion 和 MaxDataServiceVersion 標頭應該包含在任何要求中。不過，如果沒有，則目前媒體服務會假設使用的 DataServiceVersion 值是 3.0。</span><span class="sxs-lookup"><span data-stu-id="222ba-135">Because Media Services uses OData to expose its underlying asset metadata repository through REST APIs, the DataServiceVersion and MaxDataServiceVersion headers should be included in any request; however, if they are not, then currently Media Services assumes the DataServiceVersion value in use is 3.0.</span></span>
> 
> 

<span data-ttu-id="222ba-136">以下是一組選擇性標頭：</span><span class="sxs-lookup"><span data-stu-id="222ba-136">The following is a set of optional headers:</span></span>

| <span data-ttu-id="222ba-137">頁首</span><span class="sxs-lookup"><span data-stu-id="222ba-137">Header</span></span> | <span data-ttu-id="222ba-138">類型</span><span class="sxs-lookup"><span data-stu-id="222ba-138">Type</span></span> | <span data-ttu-id="222ba-139">值</span><span class="sxs-lookup"><span data-stu-id="222ba-139">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222ba-140">Date</span><span class="sxs-lookup"><span data-stu-id="222ba-140">Date</span></span> |<span data-ttu-id="222ba-141">RFC 1123 日期</span><span class="sxs-lookup"><span data-stu-id="222ba-141">RFC 1123 date</span></span> |<span data-ttu-id="222ba-142">要求的時間戳記</span><span class="sxs-lookup"><span data-stu-id="222ba-142">Timestamp of the request</span></span> |
| <span data-ttu-id="222ba-143">Accept</span><span class="sxs-lookup"><span data-stu-id="222ba-143">Accept</span></span> |<span data-ttu-id="222ba-144">內容類型</span><span class="sxs-lookup"><span data-stu-id="222ba-144">Content type</span></span> |<span data-ttu-id="222ba-145">如下所示的回應要求內容類型：</span><span class="sxs-lookup"><span data-stu-id="222ba-145">The requested content type for the response such as the following:</span></span><p> <span data-ttu-id="222ba-146">-application/json;odata=verbose</span><span class="sxs-lookup"><span data-stu-id="222ba-146">-application/json;odata=verbose</span></span><p> <span data-ttu-id="222ba-147">- application/atom+xml</span><span class="sxs-lookup"><span data-stu-id="222ba-147">- application/atom+xml</span></span><p> <span data-ttu-id="222ba-148">回應可能會有不同的內容類型，例如 Blob 擷取，成功的回應會在其中包含 Blob 資料流做為裝載。</span><span class="sxs-lookup"><span data-stu-id="222ba-148">Responses may have a different content type, such as a blob fetch, where a successful response will contain the blob stream as the payload.</span></span> |
| <span data-ttu-id="222ba-149">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="222ba-149">Accept-Encoding</span></span> |<span data-ttu-id="222ba-150">Gzip、deflate</span><span class="sxs-lookup"><span data-stu-id="222ba-150">Gzip, deflate</span></span> |<span data-ttu-id="222ba-151">GZIP 和 DEFLATE 編碼 (適用時)。</span><span class="sxs-lookup"><span data-stu-id="222ba-151">GZIP and DEFLATE encoding, when applicable.</span></span> <span data-ttu-id="222ba-152">注意：若是大型資源，媒體服務可能會忽略此標頭，並傳回未壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="222ba-152">Note: For large resources, Media Services may ignore this header and return noncompressed data.</span></span> |
| <span data-ttu-id="222ba-153">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="222ba-153">Accept-Language</span></span> |<span data-ttu-id="222ba-154">"en"、"es" 等。</span><span class="sxs-lookup"><span data-stu-id="222ba-154">"en", "es", and so on.</span></span> |<span data-ttu-id="222ba-155">指定回應的慣用語言。</span><span class="sxs-lookup"><span data-stu-id="222ba-155">Specifies the preferred language for the response.</span></span> |
| <span data-ttu-id="222ba-156">Accept-Charset</span><span class="sxs-lookup"><span data-stu-id="222ba-156">Accept-Charset</span></span> |<span data-ttu-id="222ba-157">字元集類型，如 "UTF-8"</span><span class="sxs-lookup"><span data-stu-id="222ba-157">Charset type like “UTF-8”</span></span> |<span data-ttu-id="222ba-158">預設值為 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="222ba-158">Default is UTF-8.</span></span> |
| <span data-ttu-id="222ba-159">X-HTTP-Method</span><span class="sxs-lookup"><span data-stu-id="222ba-159">X-HTTP-Method</span></span> |<span data-ttu-id="222ba-160">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="222ba-160">HTTP Method</span></span> |<span data-ttu-id="222ba-161">可讓不支援 PUT 或 DELETE 等 HTTP 方法的用戶端或防火牆，透過 GET 呼叫通道傳送使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="222ba-161">Allows clients or firewalls that do not support HTTP methods like PUT or DELETE to use these methods, tunneled via a GET call.</span></span> |
| <span data-ttu-id="222ba-162">Content-Type</span><span class="sxs-lookup"><span data-stu-id="222ba-162">Content-Type</span></span> |<span data-ttu-id="222ba-163">內容類型</span><span class="sxs-lookup"><span data-stu-id="222ba-163">Content type</span></span> |<span data-ttu-id="222ba-164">PUT 或 POST 要求中的要求主體內容類型。</span><span class="sxs-lookup"><span data-stu-id="222ba-164">Content type of the request body in PUT or POST requests.</span></span> |
| <span data-ttu-id="222ba-165">client-request-id</span><span class="sxs-lookup"><span data-stu-id="222ba-165">client-request-id</span></span> |<span data-ttu-id="222ba-166">String</span><span class="sxs-lookup"><span data-stu-id="222ba-166">String</span></span> |<span data-ttu-id="222ba-167">呼叫端定義的值，識別指定的要求。</span><span class="sxs-lookup"><span data-stu-id="222ba-167">A caller-defined value that identifies the given request.</span></span> <span data-ttu-id="222ba-168">如果指定，回應訊息中將包含此值以做為對應要求的方式。</span><span class="sxs-lookup"><span data-stu-id="222ba-168">If specified, this value will be included in the response message as a way to map the request.</span></span> <p><p><span data-ttu-id="222ba-169">**重要**</span><span class="sxs-lookup"><span data-stu-id="222ba-169">**Important**</span></span><p><span data-ttu-id="222ba-170">值的上限應該為 2096b (2k)。</span><span class="sxs-lookup"><span data-stu-id="222ba-170">Values should be capped at 2096b (2k).</span></span> |

## <a name="standard-http-response-headers-supported-by-media-services"></a><span data-ttu-id="222ba-171">媒體服務支援的標準 HTTP 回應標頭</span><span class="sxs-lookup"><span data-stu-id="222ba-171">Standard HTTP response headers supported by Media Services</span></span>
<span data-ttu-id="222ba-172">以下是一組可能會根據您所要求的資源，以及您要執行的動作而傳回給您的標頭。</span><span class="sxs-lookup"><span data-stu-id="222ba-172">The following is a set of headers that may be returned to you depending on the resource you were requesting and the action you intended to perform.</span></span>

| <span data-ttu-id="222ba-173">頁首</span><span class="sxs-lookup"><span data-stu-id="222ba-173">Header</span></span> | <span data-ttu-id="222ba-174">類型</span><span class="sxs-lookup"><span data-stu-id="222ba-174">Type</span></span> | <span data-ttu-id="222ba-175">值</span><span class="sxs-lookup"><span data-stu-id="222ba-175">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222ba-176">request-id</span><span class="sxs-lookup"><span data-stu-id="222ba-176">request-id</span></span> |<span data-ttu-id="222ba-177">String</span><span class="sxs-lookup"><span data-stu-id="222ba-177">String</span></span> |<span data-ttu-id="222ba-178">目前作業的唯一識別碼，由服務產生。</span><span class="sxs-lookup"><span data-stu-id="222ba-178">A unique identifier for the current operation, service generated.</span></span> |
| <span data-ttu-id="222ba-179">client-request-id</span><span class="sxs-lookup"><span data-stu-id="222ba-179">client-request-id</span></span> |<span data-ttu-id="222ba-180">String</span><span class="sxs-lookup"><span data-stu-id="222ba-180">String</span></span> |<span data-ttu-id="222ba-181">在原始要求中，呼叫者所指定的識別碼 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="222ba-181">An identifier specified by the caller in the original request, if present.</span></span> |
| <span data-ttu-id="222ba-182">Date</span><span class="sxs-lookup"><span data-stu-id="222ba-182">Date</span></span> |<span data-ttu-id="222ba-183">RFC 1123 日期</span><span class="sxs-lookup"><span data-stu-id="222ba-183">RFC 1123 date</span></span> |<span data-ttu-id="222ba-184">處理要求的日期。</span><span class="sxs-lookup"><span data-stu-id="222ba-184">The date that the request was processed.</span></span> |
| <span data-ttu-id="222ba-185">Content-Type</span><span class="sxs-lookup"><span data-stu-id="222ba-185">Content-Type</span></span> |<span data-ttu-id="222ba-186">視情況而異</span><span class="sxs-lookup"><span data-stu-id="222ba-186">Varies</span></span> |<span data-ttu-id="222ba-187">回應主體的內容類型。</span><span class="sxs-lookup"><span data-stu-id="222ba-187">The content type of the response body.</span></span> |
| <span data-ttu-id="222ba-188">Content-Encoding</span><span class="sxs-lookup"><span data-stu-id="222ba-188">Content-Encoding</span></span> |<span data-ttu-id="222ba-189">視情況而異</span><span class="sxs-lookup"><span data-stu-id="222ba-189">Varies</span></span> |<span data-ttu-id="222ba-190">Gzip 或 deflate (視情況)。</span><span class="sxs-lookup"><span data-stu-id="222ba-190">Gzip or deflate, as appropriate.</span></span> |

## <a name="standard-http-verbs-supported-by-media-services"></a><span data-ttu-id="222ba-191">媒體服務支援的標準 HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="222ba-191">Standard HTTP verbs supported by Media Services</span></span>
<span data-ttu-id="222ba-192">以下是進行 HTTP 要求時，可以使用的 HTTP 指令動詞完整清單：</span><span class="sxs-lookup"><span data-stu-id="222ba-192">The following is a complete list of HTTP verbs that can be used when making HTTP requests:</span></span>

| <span data-ttu-id="222ba-193">指令動詞</span><span class="sxs-lookup"><span data-stu-id="222ba-193">Verb</span></span> | <span data-ttu-id="222ba-194">說明</span><span class="sxs-lookup"><span data-stu-id="222ba-194">Description</span></span> |
| --- | --- |
| <span data-ttu-id="222ba-195">GET</span><span class="sxs-lookup"><span data-stu-id="222ba-195">GET</span></span> |<span data-ttu-id="222ba-196">傳回物件的目前值。</span><span class="sxs-lookup"><span data-stu-id="222ba-196">Returns the current value of an object.</span></span> |
| <span data-ttu-id="222ba-197">POST</span><span class="sxs-lookup"><span data-stu-id="222ba-197">POST</span></span> |<span data-ttu-id="222ba-198">根據提供的資料建立物件或提交命令。</span><span class="sxs-lookup"><span data-stu-id="222ba-198">Creates an object based on the data provided, or submits a command.</span></span> |
| <span data-ttu-id="222ba-199">PUT</span><span class="sxs-lookup"><span data-stu-id="222ba-199">PUT</span></span> |<span data-ttu-id="222ba-200">取代物件，或建立具名的物件 (如果適用的話)。</span><span class="sxs-lookup"><span data-stu-id="222ba-200">Replaces an object, or creates a named object (when applicable).</span></span> |
| <span data-ttu-id="222ba-201">刪除</span><span class="sxs-lookup"><span data-stu-id="222ba-201">DELETE</span></span> |<span data-ttu-id="222ba-202">刪除物件。</span><span class="sxs-lookup"><span data-stu-id="222ba-202">Deletes an object.</span></span> |
| <span data-ttu-id="222ba-203">MERGE</span><span class="sxs-lookup"><span data-stu-id="222ba-203">MERGE</span></span> |<span data-ttu-id="222ba-204">以具名屬性變更來更新現有的物件。</span><span class="sxs-lookup"><span data-stu-id="222ba-204">Updates an existing object with named property changes.</span></span> |
| <span data-ttu-id="222ba-205">HEAD</span><span class="sxs-lookup"><span data-stu-id="222ba-205">HEAD</span></span> |<span data-ttu-id="222ba-206">傳回 GET 回應的物件中繼資料。</span><span class="sxs-lookup"><span data-stu-id="222ba-206">Returns metadata of an object for a GET response.</span></span> |

## <a name="discover-media-services-model"></a><span data-ttu-id="222ba-207">探索媒體服務模型</span><span class="sxs-lookup"><span data-stu-id="222ba-207">Discover Media Services model</span></span>
<span data-ttu-id="222ba-208">若要讓使用者更容易找到媒體服務實體，可以使用 $metadata 作業。</span><span class="sxs-lookup"><span data-stu-id="222ba-208">To make Media Services entities more discoverable, the $metadata operation can be used.</span></span> <span data-ttu-id="222ba-209">它可讓您擷取所有有效的實體類型、實體屬性、關聯、函式、動作等等。</span><span class="sxs-lookup"><span data-stu-id="222ba-209">It allows you to retrieve all valid entity types, entity properties, associations, functions, actions, and so on.</span></span> <span data-ttu-id="222ba-210">下列範例示範如何建構 URI：https://media.windows.net/API/$metadata。</span><span class="sxs-lookup"><span data-stu-id="222ba-210">The following example shows how to construct the URI: https://media.windows.net/API/$metadata.</span></span>

<span data-ttu-id="222ba-211">如果您想要在瀏覽器檢視中繼資料，或是未在要求中包含 x-ms-version 標頭，您應該將 "?api-version=2.x" 附加到 URI 的結尾。</span><span class="sxs-lookup"><span data-stu-id="222ba-211">You should append "?api-version=2.x" to the end of the URI if you want to view the metadata in a browser, or do not include the x-ms-version header in your request.</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="222ba-212">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="222ba-212">Connect to Media Services</span></span>

<span data-ttu-id="222ba-213">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="222ba-213">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="222ba-214">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="222ba-214">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="222ba-215">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="222ba-215">You must make subsequent calls to the new URI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="222ba-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="222ba-216">Next steps</span></span>

<span data-ttu-id="222ba-217">若要使用 REST 存取 AMS API，請參閱[使用 Azure AD 驗證搭配 REST 存取 Azure 媒體服務 API](media-services-rest-connect-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="222ba-217">To access AMS APIs with REST, see [Use Azure AD authentication to access the Azure Media Services API with REST](media-services-rest-connect-with-aad.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="222ba-218">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="222ba-218">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="222ba-219">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="222ba-219">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

