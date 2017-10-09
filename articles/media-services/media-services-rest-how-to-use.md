---
title: "aaaMedia 服務作業的 REST API 概觀 |Microsoft 文件"
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
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a><span data-ttu-id="ca5b4-103">媒體服務作業 REST API 概觀</span><span class="sxs-lookup"><span data-stu-id="ca5b4-103">Media Services operations REST API overview</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="ca5b4-104">hello**媒體服務作業的 REST** API 用於建立媒體服務帳戶中的工作、 資產、 存取原則和其他物件上的作業。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-104">hello **Media Services Operations REST** API is used for creating jobs, assets, access policies, and other operations on objects in a Media Service account.</span></span> <span data-ttu-id="ca5b4-105">如需詳細資訊，請參閱[媒體服務作業 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-105">For more information, see [Media Services Operations REST API reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>

<span data-ttu-id="ca5b4-106">Microsoft Azure 媒體服務會接受以 OData 為基礎的 HTTP 要求，而且可以使用詳細資訊 JSON 或 atom+pub 回應。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-106">Microsoft Azure Media Services is a service that accepts OData-based HTTP requests and can respond back in verbose JSON or atom+pub.</span></span> <span data-ttu-id="ca5b4-107">Media Services 符合 tooAzure 設計指導方針，因為沒有一組連接 tooMedia 服務時，必須使用每個用戶端的必要 HTTP 標頭，以及一組可用的選擇性標頭。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-107">Because Media Services conforms tooAzure design guidelines, there is a set of required HTTP headers that each client must use when connecting tooMedia Services, as well as a set of optional headers that can be used.</span></span> <span data-ttu-id="ca5b4-108">hello 下列各節說明 hello 標頭和建立要求時使用的 HTTP 動詞命令，以及從媒體服務接收回應。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-108">hello following sections describe hello headers and HTTP verbs you can use when creating requests and receiving responses from Media Services.</span></span>

<span data-ttu-id="ca5b4-109">本主題概要說明如何使用 Media Services toouse REST v2。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-109">This topic gives an overview of how toouse REST v2 with Media Services.</span></span>

## <a name="considerations"></a><span data-ttu-id="ca5b4-110">考量</span><span class="sxs-lookup"><span data-stu-id="ca5b4-110">Considerations</span></span>

<span data-ttu-id="ca5b4-111">使用 REST 時，適用下列考量 hello。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-111">hello following considerations apply when using REST.</span></span>

* <span data-ttu-id="ca5b4-112">當查詢實體，就會限制為 1000年因為公用 REST v2 限制查詢結果 too1000 結果一次傳回的實體。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-112">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="ca5b4-113">您需要 toouse**略過**和**採取**(.NET) /**頂端**(REST) 中所述[.NET 本例](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities)和[這個 REST API範例](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-113">You need toouse **Skip** and **Take** (.NET)/ **top** (REST) as described in [this .NET example](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) and [this REST API example](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities).</span></span> 
* <span data-ttu-id="ca5b4-114">當使用 JSON，並指定 toouse hello **__metadata**關鍵字 hello 要求 (例如，tooreferences 連結物件)，您必須設定 hello**接受**標頭太[詳細資訊 JSON 格式](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) （請參閱下列範例中的 hello）。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-114">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object) you MUST set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (see hello following example).</span></span> <span data-ttu-id="ca5b4-115">Odata 不了解 hello **__metadata** hello 屬性要求，除非 tooverbose 設定。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-115">Odata does not understand hello **__metadata** property in hello request, unless you set it tooverbose.</span></span>  
  
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

## <a name="standard-http-request-headers-supported-by-media-services"></a><span data-ttu-id="ca5b4-116">媒體服務支援的標準 HTTP 要求標頭</span><span class="sxs-lookup"><span data-stu-id="ca5b4-116">Standard HTTP request headers supported by Media Services</span></span>
<span data-ttu-id="ca5b4-117">您對 Media Services 的每個呼叫沒有必要的標頭，您必須在要求中包含一組與另一組選擇性標頭可能會想 tooinclude。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-117">For every call you make into Media Services, there is a set of required headers you must include in your request and also a set of optional headers you may want tooinclude.</span></span> <span data-ttu-id="ca5b4-118">下列表格列出 hello hello 必要標頭：</span><span class="sxs-lookup"><span data-stu-id="ca5b4-118">hello following table lists hello required headers:</span></span>

| <span data-ttu-id="ca5b4-119">標頭</span><span class="sxs-lookup"><span data-stu-id="ca5b4-119">Header</span></span> | <span data-ttu-id="ca5b4-120">類型</span><span class="sxs-lookup"><span data-stu-id="ca5b4-120">Type</span></span> | <span data-ttu-id="ca5b4-121">值</span><span class="sxs-lookup"><span data-stu-id="ca5b4-121">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca5b4-122">Authorization</span><span class="sxs-lookup"><span data-stu-id="ca5b4-122">Authorization</span></span> |<span data-ttu-id="ca5b4-123">Bearer</span><span class="sxs-lookup"><span data-stu-id="ca5b4-123">Bearer</span></span> |<span data-ttu-id="ca5b4-124">Bearer 是 hello 只接受的授權機制。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-124">Bearer is hello only accepted authorization mechanism.</span></span> <span data-ttu-id="ca5b4-125">hello 值也必須包含 ACS 提供的 hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-125">hello value must also include hello access token provided by ACS.</span></span> |
| <span data-ttu-id="ca5b4-126">x-ms-version</span><span class="sxs-lookup"><span data-stu-id="ca5b4-126">x-ms-version</span></span> |<span data-ttu-id="ca5b4-127">十進位</span><span class="sxs-lookup"><span data-stu-id="ca5b4-127">Decimal</span></span> |<span data-ttu-id="ca5b4-128">2.11</span><span class="sxs-lookup"><span data-stu-id="ca5b4-128">2.11</span></span> |
| <span data-ttu-id="ca5b4-129">DataServiceVersion</span><span class="sxs-lookup"><span data-stu-id="ca5b4-129">DataServiceVersion</span></span> |<span data-ttu-id="ca5b4-130">十進位</span><span class="sxs-lookup"><span data-stu-id="ca5b4-130">Decimal</span></span> |<span data-ttu-id="ca5b4-131">3.0</span><span class="sxs-lookup"><span data-stu-id="ca5b4-131">3.0</span></span> |
| <span data-ttu-id="ca5b4-132">MaxDataServiceVersion</span><span class="sxs-lookup"><span data-stu-id="ca5b4-132">MaxDataServiceVersion</span></span> |<span data-ttu-id="ca5b4-133">十進位</span><span class="sxs-lookup"><span data-stu-id="ca5b4-133">Decimal</span></span> |<span data-ttu-id="ca5b4-134">3.0</span><span class="sxs-lookup"><span data-stu-id="ca5b4-134">3.0</span></span> |

> [!NOTE]
> <span data-ttu-id="ca5b4-135">因為媒體服務會使用 OData tooexpose 其基礎資產中繼資料儲存機制透過 REST Api，hello DataServiceVersion 與 MaxDataServiceVersion 標頭應該包含在任何要求。不過，如果沒有，然後目前 Media Services 假設使用中的 hello DataServiceVersion 值為 3.0。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-135">Because Media Services uses OData tooexpose its underlying asset metadata repository through REST APIs, hello DataServiceVersion and MaxDataServiceVersion headers should be included in any request; however, if they are not, then currently Media Services assumes hello DataServiceVersion value in use is 3.0.</span></span>
> 
> 

<span data-ttu-id="ca5b4-136">hello 以下是一組選擇性標頭：</span><span class="sxs-lookup"><span data-stu-id="ca5b4-136">hello following is a set of optional headers:</span></span>

| <span data-ttu-id="ca5b4-137">標頭</span><span class="sxs-lookup"><span data-stu-id="ca5b4-137">Header</span></span> | <span data-ttu-id="ca5b4-138">類型</span><span class="sxs-lookup"><span data-stu-id="ca5b4-138">Type</span></span> | <span data-ttu-id="ca5b4-139">值</span><span class="sxs-lookup"><span data-stu-id="ca5b4-139">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca5b4-140">Date</span><span class="sxs-lookup"><span data-stu-id="ca5b4-140">Date</span></span> |<span data-ttu-id="ca5b4-141">RFC 1123 日期</span><span class="sxs-lookup"><span data-stu-id="ca5b4-141">RFC 1123 date</span></span> |<span data-ttu-id="ca5b4-142">Hello 要求的時間戳記</span><span class="sxs-lookup"><span data-stu-id="ca5b4-142">Timestamp of hello request</span></span> |
| <span data-ttu-id="ca5b4-143">Accept</span><span class="sxs-lookup"><span data-stu-id="ca5b4-143">Accept</span></span> |<span data-ttu-id="ca5b4-144">內容類型</span><span class="sxs-lookup"><span data-stu-id="ca5b4-144">Content type</span></span> |<span data-ttu-id="ca5b4-145">hello 要求的內容類型 hello 回應 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="ca5b4-145">hello requested content type for hello response such as hello following:</span></span><p> <span data-ttu-id="ca5b4-146">-application/json;odata=verbose</span><span class="sxs-lookup"><span data-stu-id="ca5b4-146">-application/json;odata=verbose</span></span><p> <span data-ttu-id="ca5b4-147">- application/atom+xml</span><span class="sxs-lookup"><span data-stu-id="ca5b4-147">- application/atom+xml</span></span><p> <span data-ttu-id="ca5b4-148">回應可能會有不同的內容類型，如 blob 擷取，其中成功的回應將包含做為 hello 裝載 hello blob 資料流。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-148">Responses may have a different content type, such as a blob fetch, where a successful response will contain hello blob stream as hello payload.</span></span> |
| <span data-ttu-id="ca5b4-149">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="ca5b4-149">Accept-Encoding</span></span> |<span data-ttu-id="ca5b4-150">Gzip、deflate</span><span class="sxs-lookup"><span data-stu-id="ca5b4-150">Gzip, deflate</span></span> |<span data-ttu-id="ca5b4-151">GZIP 和 DEFLATE 編碼 (適用時)。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-151">GZIP and DEFLATE encoding, when applicable.</span></span> <span data-ttu-id="ca5b4-152">注意：若是大型資源，媒體服務可能會忽略此標頭，並傳回未壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-152">Note: For large resources, Media Services may ignore this header and return noncompressed data.</span></span> |
| <span data-ttu-id="ca5b4-153">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="ca5b4-153">Accept-Language</span></span> |<span data-ttu-id="ca5b4-154">"en"、"es" 等。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-154">"en", "es", and so on.</span></span> |<span data-ttu-id="ca5b4-155">指定 hello 回應 hello 慣用語言。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-155">Specifies hello preferred language for hello response.</span></span> |
| <span data-ttu-id="ca5b4-156">Accept-Charset</span><span class="sxs-lookup"><span data-stu-id="ca5b4-156">Accept-Charset</span></span> |<span data-ttu-id="ca5b4-157">字元集類型，如 "UTF-8"</span><span class="sxs-lookup"><span data-stu-id="ca5b4-157">Charset type like “UTF-8”</span></span> |<span data-ttu-id="ca5b4-158">預設值為 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-158">Default is UTF-8.</span></span> |
| <span data-ttu-id="ca5b4-159">X-HTTP-Method</span><span class="sxs-lookup"><span data-stu-id="ca5b4-159">X-HTTP-Method</span></span> |<span data-ttu-id="ca5b4-160">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="ca5b4-160">HTTP Method</span></span> |<span data-ttu-id="ca5b4-161">可讓用戶端或不支援 HTTP 方法，例如 PUT 或 DELETE toouse 防火牆這些方法，透過 GET 呼叫通道。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-161">Allows clients or firewalls that do not support HTTP methods like PUT or DELETE toouse these methods, tunneled via a GET call.</span></span> |
| <span data-ttu-id="ca5b4-162">Content-Type</span><span class="sxs-lookup"><span data-stu-id="ca5b4-162">Content-Type</span></span> |<span data-ttu-id="ca5b4-163">內容類型</span><span class="sxs-lookup"><span data-stu-id="ca5b4-163">Content type</span></span> |<span data-ttu-id="ca5b4-164">內容的 PUT 或 POST 要求中的 hello 要求主體的類型。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-164">Content type of hello request body in PUT or POST requests.</span></span> |
| <span data-ttu-id="ca5b4-165">client-request-id</span><span class="sxs-lookup"><span data-stu-id="ca5b4-165">client-request-id</span></span> |<span data-ttu-id="ca5b4-166">String</span><span class="sxs-lookup"><span data-stu-id="ca5b4-166">String</span></span> |<span data-ttu-id="ca5b4-167">呼叫端定義的值，識別 hello 給定要求。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-167">A caller-defined value that identifies hello given request.</span></span> <span data-ttu-id="ca5b4-168">如果指定，將 hello 回應訊息中包含此值，做為方法 toomap hello 要求。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-168">If specified, this value will be included in hello response message as a way toomap hello request.</span></span> <p><p><span data-ttu-id="ca5b4-169">**重要**</span><span class="sxs-lookup"><span data-stu-id="ca5b4-169">**Important**</span></span><p><span data-ttu-id="ca5b4-170">值的上限應該為 2096b (2k)。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-170">Values should be capped at 2096b (2k).</span></span> |

## <a name="standard-http-response-headers-supported-by-media-services"></a><span data-ttu-id="ca5b4-171">媒體服務支援的標準 HTTP 回應標頭</span><span class="sxs-lookup"><span data-stu-id="ca5b4-171">Standard HTTP response headers supported by Media Services</span></span>
<span data-ttu-id="ca5b4-172">hello 以下是一組可能會傳回根據您所要求的 hello 資源 tooyou 和 hello 適合 tooperform 的動作標頭。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-172">hello following is a set of headers that may be returned tooyou depending on hello resource you were requesting and hello action you intended tooperform.</span></span>

| <span data-ttu-id="ca5b4-173">標頭</span><span class="sxs-lookup"><span data-stu-id="ca5b4-173">Header</span></span> | <span data-ttu-id="ca5b4-174">類型</span><span class="sxs-lookup"><span data-stu-id="ca5b4-174">Type</span></span> | <span data-ttu-id="ca5b4-175">值</span><span class="sxs-lookup"><span data-stu-id="ca5b4-175">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca5b4-176">request-id</span><span class="sxs-lookup"><span data-stu-id="ca5b4-176">request-id</span></span> |<span data-ttu-id="ca5b4-177">String</span><span class="sxs-lookup"><span data-stu-id="ca5b4-177">String</span></span> |<span data-ttu-id="ca5b4-178">Hello 目前的作業，服務產生的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-178">A unique identifier for hello current operation, service generated.</span></span> |
| <span data-ttu-id="ca5b4-179">client-request-id</span><span class="sxs-lookup"><span data-stu-id="ca5b4-179">client-request-id</span></span> |<span data-ttu-id="ca5b4-180">String</span><span class="sxs-lookup"><span data-stu-id="ca5b4-180">String</span></span> |<span data-ttu-id="ca5b4-181">如果有的話，hello 呼叫端，在 hello 原始要求中，指定識別項。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-181">An identifier specified by hello caller in hello original request, if present.</span></span> |
| <span data-ttu-id="ca5b4-182">Date</span><span class="sxs-lookup"><span data-stu-id="ca5b4-182">Date</span></span> |<span data-ttu-id="ca5b4-183">RFC 1123 日期</span><span class="sxs-lookup"><span data-stu-id="ca5b4-183">RFC 1123 date</span></span> |<span data-ttu-id="ca5b4-184">hello 日期該 hello 要求處理。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-184">hello date that hello request was processed.</span></span> |
| <span data-ttu-id="ca5b4-185">Content-Type</span><span class="sxs-lookup"><span data-stu-id="ca5b4-185">Content-Type</span></span> |<span data-ttu-id="ca5b4-186">視情況而異</span><span class="sxs-lookup"><span data-stu-id="ca5b4-186">Varies</span></span> |<span data-ttu-id="ca5b4-187">hello hello 回應主體的內容類型。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-187">hello content type of hello response body.</span></span> |
| <span data-ttu-id="ca5b4-188">Content-Encoding</span><span class="sxs-lookup"><span data-stu-id="ca5b4-188">Content-Encoding</span></span> |<span data-ttu-id="ca5b4-189">視情況而異</span><span class="sxs-lookup"><span data-stu-id="ca5b4-189">Varies</span></span> |<span data-ttu-id="ca5b4-190">Gzip 或 deflate (視情況)。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-190">Gzip or deflate, as appropriate.</span></span> |

## <a name="standard-http-verbs-supported-by-media-services"></a><span data-ttu-id="ca5b4-191">媒體服務支援的標準 HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="ca5b4-191">Standard HTTP verbs supported by Media Services</span></span>
<span data-ttu-id="ca5b4-192">hello 下列是可以在提出 HTTP 要求時使用的 HTTP 動詞命令的完整清單：</span><span class="sxs-lookup"><span data-stu-id="ca5b4-192">hello following is a complete list of HTTP verbs that can be used when making HTTP requests:</span></span>

| <span data-ttu-id="ca5b4-193">指令動詞</span><span class="sxs-lookup"><span data-stu-id="ca5b4-193">Verb</span></span> | <span data-ttu-id="ca5b4-194">說明</span><span class="sxs-lookup"><span data-stu-id="ca5b4-194">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ca5b4-195">GET</span><span class="sxs-lookup"><span data-stu-id="ca5b4-195">GET</span></span> |<span data-ttu-id="ca5b4-196">傳回 hello 物件的目前值。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-196">Returns hello current value of an object.</span></span> |
| <span data-ttu-id="ca5b4-197">POST</span><span class="sxs-lookup"><span data-stu-id="ca5b4-197">POST</span></span> |<span data-ttu-id="ca5b4-198">建立基礎提供，hello 資料的物件，或提交的命令。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-198">Creates an object based on hello data provided, or submits a command.</span></span> |
| <span data-ttu-id="ca5b4-199">PUT</span><span class="sxs-lookup"><span data-stu-id="ca5b4-199">PUT</span></span> |<span data-ttu-id="ca5b4-200">取代物件，或建立具名的物件 (如果適用的話)。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-200">Replaces an object, or creates a named object (when applicable).</span></span> |
| <span data-ttu-id="ca5b4-201">刪除</span><span class="sxs-lookup"><span data-stu-id="ca5b4-201">DELETE</span></span> |<span data-ttu-id="ca5b4-202">刪除物件。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-202">Deletes an object.</span></span> |
| <span data-ttu-id="ca5b4-203">MERGE</span><span class="sxs-lookup"><span data-stu-id="ca5b4-203">MERGE</span></span> |<span data-ttu-id="ca5b4-204">以具名屬性變更來更新現有的物件。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-204">Updates an existing object with named property changes.</span></span> |
| <span data-ttu-id="ca5b4-205">HEAD</span><span class="sxs-lookup"><span data-stu-id="ca5b4-205">HEAD</span></span> |<span data-ttu-id="ca5b4-206">傳回 GET 回應的物件中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-206">Returns metadata of an object for a GET response.</span></span> |

## <a name="discover-media-services-model"></a><span data-ttu-id="ca5b4-207">探索媒體服務模型</span><span class="sxs-lookup"><span data-stu-id="ca5b4-207">Discover Media Services model</span></span>
<span data-ttu-id="ca5b4-208">可以使用 toomake 媒體服務實體更容易找到 hello $metadata 作業。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-208">toomake Media Services entities more discoverable, hello $metadata operation can be used.</span></span> <span data-ttu-id="ca5b4-209">它可讓您 tooretrieve 所有有效的實體類型、 實體屬性、 關聯、 函數、 動作和等等。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-209">It allows you tooretrieve all valid entity types, entity properties, associations, functions, actions, and so on.</span></span> <span data-ttu-id="ca5b4-210">hello 下列範例示範如何 tooconstruct hello URI: https://media.windows.net/API/$ 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-210">hello following example shows how tooconstruct hello URI: https://media.windows.net/API/$metadata.</span></span>

<span data-ttu-id="ca5b4-211">您應該附加"？ api version=2.x"toohello 結尾 hello URI，如果您想要在瀏覽器，tooview hello 中繼資料或不在要求中包含 hello x ms 版本標頭。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-211">You should append "?api-version=2.x" toohello end of hello URI if you want tooview hello metadata in a browser, or do not include hello x-ms-version header in your request.</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="ca5b4-212">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="ca5b4-212">Connect tooMedia Services</span></span>

<span data-ttu-id="ca5b4-213">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-213">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="ca5b4-214">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-214">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ca5b4-215">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-215">You must make subsequent calls toohello new URI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca5b4-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca5b4-216">Next steps</span></span>

<span data-ttu-id="ca5b4-217">tooaccess AMS 應用程式開發介面與其他部分，請參閱[使用 Azure AD 驗證 tooaccess hello Azure 媒體服務 API 與其餘](media-services-rest-connect-with-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="ca5b4-217">tooaccess AMS APIs with REST, see [Use Azure AD authentication tooaccess hello Azure Media Services API with REST](media-services-rest-connect-with-aad.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ca5b4-218">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="ca5b4-218">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ca5b4-219">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ca5b4-219">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

