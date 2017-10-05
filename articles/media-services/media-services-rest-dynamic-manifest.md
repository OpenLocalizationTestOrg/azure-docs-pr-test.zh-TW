---
title: "使用 Azure 媒體服務 REST API 建立篩選器 | Microsoft Docs"
description: "本主題說明如何建立篩選器，讓您的用戶端可以使用篩選器來串流特定的資料流區段。 媒體服務會建立動態資訊清單來完成此選擇性資料流。"
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
ms.openlocfilehash: 76d2721138668d9f0a908af3fa42840309b068ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="a7d36-104">使用 Azure 媒體服務 REST API 建立篩選器</span><span class="sxs-lookup"><span data-stu-id="a7d36-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7d36-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a7d36-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="a7d36-106">REST</span><span class="sxs-lookup"><span data-stu-id="a7d36-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="a7d36-107">從 2.11 版開始，媒體服務可讓您為資產定義篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7d36-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="a7d36-108">這些篩選器是伺服器端規則，可讓您的客戶選擇執行如下的動作：只播放一段視訊 (而非播放完整視訊)，或只指定您客戶裝置可以處理的一部分音訊和視訊轉譯 (而非與該資產相關的所有轉譯)。</span><span class="sxs-lookup"><span data-stu-id="a7d36-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="a7d36-109">透過在您客戶要求下建立的 **動態資訊清單**可達成對資訊進行這樣的篩選，藉此根據指定的篩選器來串流視訊。</span><span class="sxs-lookup"><span data-stu-id="a7d36-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="a7d36-110">如需篩選器與動態資訊清單的詳細資訊，請參閱 [動態資訊清單概觀](media-services-dynamic-manifest-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a7d36-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="a7d36-111">本主題說明如何使用 REST API 建立、更新與刪除篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7d36-111">This topic shows how to use REST APIs to create, update, and delete filters.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="a7d36-112">用於建立篩選器的類型</span><span class="sxs-lookup"><span data-stu-id="a7d36-112">Types used to create filters</span></span>
<span data-ttu-id="a7d36-113">建立篩選器時會使用下列類型：</span><span class="sxs-lookup"><span data-stu-id="a7d36-113">The following types are used when creating filters:</span></span>  

* [<span data-ttu-id="a7d36-114">Filter</span><span class="sxs-lookup"><span data-stu-id="a7d36-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="a7d36-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="a7d36-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="a7d36-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="a7d36-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="a7d36-117">FilterTrackSelect 和 FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="a7d36-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="a7d36-118">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="a7d36-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a7d36-119">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="a7d36-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="a7d36-120">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="a7d36-120">Connect to Media Services</span></span>

<span data-ttu-id="a7d36-121">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a7d36-121">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a7d36-122">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="a7d36-122">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a7d36-123">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="a7d36-123">You must make subsequent calls to the new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="a7d36-124">建立篩選器</span><span class="sxs-lookup"><span data-stu-id="a7d36-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="a7d36-125">建立全域篩選器</span><span class="sxs-lookup"><span data-stu-id="a7d36-125">Create global Filters</span></span>
<span data-ttu-id="a7d36-126">若要建立全域篩選器，請使用下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="a7d36-126">To create a global Filter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="a7d36-127">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-127">HTTP Request</span></span>
<span data-ttu-id="a7d36-128">要求標頭</span><span class="sxs-lookup"><span data-stu-id="a7d36-128">Request Headers</span></span>

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

<span data-ttu-id="a7d36-129">Request body</span><span class="sxs-lookup"><span data-stu-id="a7d36-129">Request body</span></span> 

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




#### <a name="http-response"></a><span data-ttu-id="a7d36-130">HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="a7d36-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="a7d36-131">建立區域 AssetFilter</span><span class="sxs-lookup"><span data-stu-id="a7d36-131">Create local AssetFilters</span></span>
<span data-ttu-id="a7d36-132">若要建立區域 AssetFilter，請使用下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="a7d36-132">To create a local AssetFilter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="a7d36-133">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-133">HTTP Request</span></span>
<span data-ttu-id="a7d36-134">要求標頭</span><span class="sxs-lookup"><span data-stu-id="a7d36-134">Request Headers</span></span>

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

<span data-ttu-id="a7d36-135">Request body</span><span class="sxs-lookup"><span data-stu-id="a7d36-135">Request body</span></span> 

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

#### <a name="http-response"></a><span data-ttu-id="a7d36-136">HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="a7d36-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="a7d36-137">清單篩選器</span><span class="sxs-lookup"><span data-stu-id="a7d36-137">List filters</span></span>
### <a name="get-all-global-filters-in-the-ams-account"></a><span data-ttu-id="a7d36-138">取得 AMS 帳戶中所有的全域 **篩選器**</span><span class="sxs-lookup"><span data-stu-id="a7d36-138">Get all global **Filter**s in the AMS account</span></span>
<span data-ttu-id="a7d36-139">若要列出篩選器，請使用下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="a7d36-139">To list filters, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="a7d36-140">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="a7d36-141">取得與資產相關聯的 **AssetFilter**</span><span class="sxs-lookup"><span data-stu-id="a7d36-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="a7d36-142">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="a7d36-143">根據識別碼取得 **AssetFilter**</span><span class="sxs-lookup"><span data-stu-id="a7d36-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="a7d36-144">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="a7d36-145">更新篩選器</span><span class="sxs-lookup"><span data-stu-id="a7d36-145">Update filters</span></span>
<span data-ttu-id="a7d36-146">使用 PATCH、PUT 或 MERGE 以新的屬性值更新篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7d36-146">Use PATCH, PUT or MERGE to update a filter with new property values.</span></span>  <span data-ttu-id="a7d36-147">如需這些作業的詳細資訊，請參閱 [PATCH、PUT、MERGE](http://msdn.microsoft.com/library/dd541276.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a7d36-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="a7d36-148">如果您更新篩選器，則資料流端點需要 2 分鐘的時間來重新整理規則。</span><span class="sxs-lookup"><span data-stu-id="a7d36-148">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="a7d36-149">如果內容是使用此篩選器提供的 (並快取在 Proxy 與 CDN 快取中)，則更新此篩選器會造成播放程式失敗。</span><span class="sxs-lookup"><span data-stu-id="a7d36-149">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="a7d36-150">建議在更新篩選器之後清除快取。</span><span class="sxs-lookup"><span data-stu-id="a7d36-150">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="a7d36-151">如果這個選項無法執行，請考慮使用不同的篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7d36-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="a7d36-152">更新全域篩選器</span><span class="sxs-lookup"><span data-stu-id="a7d36-152">Update global Filters</span></span>
<span data-ttu-id="a7d36-153">若要更新全域篩選器，請使用下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="a7d36-153">To update a global filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="a7d36-154">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-154">HTTP Request</span></span>
<span data-ttu-id="a7d36-155">要求標頭：</span><span class="sxs-lookup"><span data-stu-id="a7d36-155">Request headers:</span></span> 

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

<span data-ttu-id="a7d36-156">要求本文：</span><span class="sxs-lookup"><span data-stu-id="a7d36-156">Request body:</span></span> 

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

### <a name="update-local-assetfilters"></a><span data-ttu-id="a7d36-157">更新區域 AssetFilter</span><span class="sxs-lookup"><span data-stu-id="a7d36-157">Update local AssetFilters</span></span>
<span data-ttu-id="a7d36-158">若要更新區域篩選器，請使用下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="a7d36-158">To update a local filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="a7d36-159">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-159">HTTP Request</span></span>
<span data-ttu-id="a7d36-160">要求標頭：</span><span class="sxs-lookup"><span data-stu-id="a7d36-160">Request headers:</span></span> 

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

<span data-ttu-id="a7d36-161">要求本文：</span><span class="sxs-lookup"><span data-stu-id="a7d36-161">Request body:</span></span> 

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


## <a name="delete-filters"></a><span data-ttu-id="a7d36-162">刪除篩選器</span><span class="sxs-lookup"><span data-stu-id="a7d36-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="a7d36-163">刪除全域篩選器</span><span class="sxs-lookup"><span data-stu-id="a7d36-163">Delete global Filters</span></span>
<span data-ttu-id="a7d36-164">若要刪除全域篩選器，請使用下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="a7d36-164">To delete a global Filter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="a7d36-165">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="a7d36-166">刪除區域 AssetFilter</span><span class="sxs-lookup"><span data-stu-id="a7d36-166">Delete local AssetFilters</span></span>
<span data-ttu-id="a7d36-167">若要刪除區域 AssetFilter，請使用下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="a7d36-167">To delete a local AssetFilter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="a7d36-168">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="a7d36-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="a7d36-169">建置使用篩選器的資料流 URL</span><span class="sxs-lookup"><span data-stu-id="a7d36-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="a7d36-170">如需如何發佈與傳遞資產的相關資訊，請參閱 [將內容傳遞給客戶概觀](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a7d36-170">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="a7d36-171">下列範例顯示如何將篩選器新增至資料流 URL。</span><span class="sxs-lookup"><span data-stu-id="a7d36-171">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="a7d36-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="a7d36-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="a7d36-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="a7d36-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="a7d36-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="a7d36-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="a7d36-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="a7d36-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="a7d36-176">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="a7d36-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a7d36-177">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="a7d36-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a7d36-178">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a7d36-178">See Also</span></span>
[<span data-ttu-id="a7d36-179">動態資訊清單概觀</span><span class="sxs-lookup"><span data-stu-id="a7d36-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

