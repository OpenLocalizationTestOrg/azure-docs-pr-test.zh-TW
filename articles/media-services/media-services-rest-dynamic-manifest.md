---
title: "使用 Azure 媒體服務 REST API aaaCreating 篩選 |Microsoft 文件"
description: "本主題描述如何 toocreate 篩選讓您的用戶端能夠使用它們 toostream 特定區段的資料流。 媒體服務會建立動態資訊清單 tooachieve 這個選擇性的資料流。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="f4d3b-104">使用 Azure 媒體服務 REST API 建立篩選器</span><span class="sxs-lookup"><span data-stu-id="f4d3b-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4d3b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f4d3b-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="f4d3b-106">REST</span><span class="sxs-lookup"><span data-stu-id="f4d3b-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="f4d3b-107">從 2.11 版開始，媒體服務可讓您為您資產的 toodefine 篩選器。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="f4d3b-108">這些篩選條件是伺服器端規則，可讓您的客戶 toochoose toodo 等： 播放視訊 （而不是正在播放 hello 整個視訊） 的區段，或指定的音訊和視訊多種客戶的裝置可以處理 （子集而不是所有 hello 多種與相關聯 hello 資產）。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="f4d3b-109">此篩選您的資產會透過封存**動態資訊清單**視訊在您的客戶要求 toostream 時所建立根據指定的篩選器。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="f4d3b-110">如需詳細資訊相關的 toofilters 和動態資訊清單，請參閱[動態資訊清單概觀](media-services-dynamic-manifest-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="f4d3b-111">本主題說明如何 toouse REST Api toocreate、 更新和刪除篩選。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="f4d3b-112">使用 toocreate 篩選類型。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-112">Types used toocreate filters</span></span>
<span data-ttu-id="f4d3b-113">hello 下列使用類型時建立的篩選條件：</span><span class="sxs-lookup"><span data-stu-id="f4d3b-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="f4d3b-114">Filter</span><span class="sxs-lookup"><span data-stu-id="f4d3b-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="f4d3b-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="f4d3b-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="f4d3b-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="f4d3b-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="f4d3b-117">FilterTrackSelect 和 FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="f4d3b-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="f4d3b-118">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="f4d3b-119">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="f4d3b-120">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="f4d3b-120">Connect tooMedia Services</span></span>

<span data-ttu-id="f4d3b-121">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="f4d3b-122">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="f4d3b-123">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="f4d3b-124">建立篩選器</span><span class="sxs-lookup"><span data-stu-id="f4d3b-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="f4d3b-125">建立全域篩選器</span><span class="sxs-lookup"><span data-stu-id="f4d3b-125">Create global Filters</span></span>
<span data-ttu-id="f4d3b-126">toocreate 全域的篩選器，請使用下列 HTTP 要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4d3b-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="f4d3b-127">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-127">HTTP Request</span></span>
<span data-ttu-id="f4d3b-128">要求標頭</span><span class="sxs-lookup"><span data-stu-id="f4d3b-128">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="f4d3b-129">Request body</span><span class="sxs-lookup"><span data-stu-id="f4d3b-129">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="f4d3b-130">HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="f4d3b-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="f4d3b-131">建立區域 AssetFilter</span><span class="sxs-lookup"><span data-stu-id="f4d3b-131">Create local AssetFilters</span></span>
<span data-ttu-id="f4d3b-132">toocreate 本機 AssetFilter，使用下列 HTTP 要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4d3b-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="f4d3b-133">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-133">HTTP Request</span></span>
<span data-ttu-id="f4d3b-134">要求標頭</span><span class="sxs-lookup"><span data-stu-id="f4d3b-134">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="f4d3b-135">Request body</span><span class="sxs-lookup"><span data-stu-id="f4d3b-135">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="f4d3b-136">HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="f4d3b-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="f4d3b-137">清單篩選器</span><span class="sxs-lookup"><span data-stu-id="f4d3b-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="f4d3b-138">取得所有全域**篩選**hello AMS 帳戶中的 s</span><span class="sxs-lookup"><span data-stu-id="f4d3b-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="f4d3b-139">toolist 篩選，請使用下列 HTTP 要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4d3b-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="f4d3b-140">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="f4d3b-141">取得與資產相關聯的 **AssetFilter**</span><span class="sxs-lookup"><span data-stu-id="f4d3b-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="f4d3b-142">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="f4d3b-143">根據識別碼取得 **AssetFilter**</span><span class="sxs-lookup"><span data-stu-id="f4d3b-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="f4d3b-144">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="f4d3b-145">更新篩選器</span><span class="sxs-lookup"><span data-stu-id="f4d3b-145">Update filters</span></span>
<span data-ttu-id="f4d3b-146">使用 PATCH、 PUT 或合併 tooupdate 與新的屬性值篩選器。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="f4d3b-147">如需這些作業的詳細資訊，請參閱 [PATCH、PUT、MERGE](http://msdn.microsoft.com/library/dd541276.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="f4d3b-148">如果您更新篩選器，就可以在資料流端點 toorefresh hello 規則 too2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="f4d3b-149">如果 hello 內容處理使用此篩選器 （快取和 proxy 和 CDN 中快取），更新此篩選器導致播放失敗。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="f4d3b-150">它是在更新 hello 篩選之後，建議 tooclear hello 快取。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="f4d3b-151">如果這個選項無法執行，請考慮使用不同的篩選器。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="f4d3b-152">更新全域篩選器</span><span class="sxs-lookup"><span data-stu-id="f4d3b-152">Update global Filters</span></span>
<span data-ttu-id="f4d3b-153">tooupdate 全域的篩選器，請使用下列 HTTP 要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4d3b-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="f4d3b-154">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-154">HTTP Request</span></span>
<span data-ttu-id="f4d3b-155">要求標頭：</span><span class="sxs-lookup"><span data-stu-id="f4d3b-155">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="f4d3b-156">要求本文：</span><span class="sxs-lookup"><span data-stu-id="f4d3b-156">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="f4d3b-157">更新區域 AssetFilter</span><span class="sxs-lookup"><span data-stu-id="f4d3b-157">Update local AssetFilters</span></span>
<span data-ttu-id="f4d3b-158">tooupdate 本機篩選條件，請使用下列 HTTP 要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4d3b-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="f4d3b-159">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-159">HTTP Request</span></span>
<span data-ttu-id="f4d3b-160">要求標頭：</span><span class="sxs-lookup"><span data-stu-id="f4d3b-160">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="f4d3b-161">要求本文：</span><span class="sxs-lookup"><span data-stu-id="f4d3b-161">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="f4d3b-162">刪除篩選器</span><span class="sxs-lookup"><span data-stu-id="f4d3b-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="f4d3b-163">刪除全域篩選器</span><span class="sxs-lookup"><span data-stu-id="f4d3b-163">Delete global Filters</span></span>
<span data-ttu-id="f4d3b-164">toodelete 全域的篩選器，請使用下列 HTTP 要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4d3b-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="f4d3b-165">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="f4d3b-166">刪除區域 AssetFilter</span><span class="sxs-lookup"><span data-stu-id="f4d3b-166">Delete local AssetFilters</span></span>
<span data-ttu-id="f4d3b-167">toodelete 本機 AssetFilter，使用下列 HTTP 要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4d3b-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="f4d3b-168">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="f4d3b-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="f4d3b-169">建置使用篩選器的資料流 URL</span><span class="sxs-lookup"><span data-stu-id="f4d3b-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="f4d3b-170">如需有關如何 toopublish 及傳遞資產，請參閱詳細[傳遞內容 tooCustomers 概觀](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="f4d3b-171">hello 下列範例顯示如何 tooadd 篩選 tooyour 串流 Url。</span><span class="sxs-lookup"><span data-stu-id="f4d3b-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="f4d3b-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="f4d3b-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="f4d3b-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="f4d3b-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="f4d3b-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="f4d3b-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="f4d3b-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="f4d3b-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="f4d3b-176">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="f4d3b-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f4d3b-177">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="f4d3b-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f4d3b-178">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f4d3b-178">See Also</span></span>
[<span data-ttu-id="f4d3b-179">動態資訊清單概觀</span><span class="sxs-lookup"><span data-stu-id="f4d3b-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

