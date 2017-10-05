---
title: "使用 REST 發佈 Azure 媒體服務內容"
description: "了解如何建立定位器，用來建置串流 URL。 程式碼使用 REST API。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d1e0a112040f6aa4cfa9e8c323507b1c0a223f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="8b572-104">使用 REST 發佈 Azure 媒體服務內容</span><span class="sxs-lookup"><span data-stu-id="8b572-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b572-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8b572-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="8b572-106">REST</span><span class="sxs-lookup"><span data-stu-id="8b572-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="8b572-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="8b572-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="8b572-108">Overview</span><span class="sxs-lookup"><span data-stu-id="8b572-108">Overview</span></span>
<span data-ttu-id="8b572-109">您可以建立隨選串流定位器及建置串流 URL，串流處理調適性位元速率 MP4 集。</span><span class="sxs-lookup"><span data-stu-id="8b572-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="8b572-110">[為資產編碼](media-services-rest-encode-asset.md) 主題說明如何編碼為調適性位元速率 MP4 集。</span><span class="sxs-lookup"><span data-stu-id="8b572-110">The [encoding an asset](media-services-rest-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="8b572-111">如果您的內容已加密，請在建立定位器之前設定資產傳遞原則 (如 [這個](media-services-rest-configure-asset-delivery-policy.md) 主題中所述)。</span><span class="sxs-lookup"><span data-stu-id="8b572-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="8b572-112">您也可以使用隨選串流定位器來建置指向可漸進式下載之 MP4 檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="8b572-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="8b572-113">本主題說明如何建立隨選串流定位器以發佈資產及建置 Smooth、MPEG DASH 和 HLS 串流 URL。</span><span class="sxs-lookup"><span data-stu-id="8b572-113">This topic shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="8b572-114">它也會示範如何建置漸進式下載 URL。</span><span class="sxs-lookup"><span data-stu-id="8b572-114">It also shows hot to build progressive download URLs.</span></span>

<span data-ttu-id="8b572-115">[下列章節](#types) 說明列舉類型，REST 呼叫中會使用這些類型的值。</span><span class="sxs-lookup"><span data-stu-id="8b572-115">The [following](#types) section shows the enum types whose values are used in the REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="8b572-116">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="8b572-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="8b572-117">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="8b572-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="8b572-118">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="8b572-118">Connect to Media Services</span></span>

<span data-ttu-id="8b572-119">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="8b572-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="8b572-120">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="8b572-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="8b572-121">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="8b572-121">You must make subsequent calls to the new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="8b572-122">建立隨選串流定位器</span><span class="sxs-lookup"><span data-stu-id="8b572-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="8b572-123">若要建立隨選串流定位器並取得 URL，您需要執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="8b572-123">To create the OnDemand streaming locator and get URLs you need to do the following:</span></span>

1. <span data-ttu-id="8b572-124">如果內容已加密，請定義存取原則。</span><span class="sxs-lookup"><span data-stu-id="8b572-124">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="8b572-125">建立隨選串流定位器。</span><span class="sxs-lookup"><span data-stu-id="8b572-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="8b572-126">如果您想要串流處理，請取得資產內的串流資訊清單檔案 (.ism)。</span><span class="sxs-lookup"><span data-stu-id="8b572-126">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="8b572-127">如果您想要漸進式地下載，請取得資產中的 MP4 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="8b572-127">If you plan to progressively download, get the names of MP4 files in the asset.</span></span> 
4. <span data-ttu-id="8b572-128">建置資訊清單檔或 MP4 檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="8b572-128">Build URLs to the manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="8b572-129">請注意，您無法使用包含寫入或刪除權限的 AccessPolicy 建立串流訂位器。</span><span class="sxs-lookup"><span data-stu-id="8b572-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="8b572-130">建立存取原則</span><span class="sxs-lookup"><span data-stu-id="8b572-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="8b572-131">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="8b572-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="8b572-132">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="8b572-132">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="8b572-133">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="8b572-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="8b572-134">要求：</span><span class="sxs-lookup"><span data-stu-id="8b572-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="8b572-135">回應：</span><span class="sxs-lookup"><span data-stu-id="8b572-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="8b572-136">建立隨選串流定位器</span><span class="sxs-lookup"><span data-stu-id="8b572-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="8b572-137">建立指定資產和資產原則的定位器。</span><span class="sxs-lookup"><span data-stu-id="8b572-137">Create the locator for the specified asset and asset policy.</span></span>

<span data-ttu-id="8b572-138">要求：</span><span class="sxs-lookup"><span data-stu-id="8b572-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="8b572-139">回應：</span><span class="sxs-lookup"><span data-stu-id="8b572-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="8b572-140">建置串流 URL</span><span class="sxs-lookup"><span data-stu-id="8b572-140">Build streaming URLs</span></span>
<span data-ttu-id="8b572-141">建立定位器之後，使用傳回的 **Path** 值建置 Smooth、HLS 和 MPEG DASH URL。</span><span class="sxs-lookup"><span data-stu-id="8b572-141">Use the **Path** value returned after the creation of the locator to build the Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="8b572-142">Smooth Streaming： **Path** + 資訊清單檔案名稱 + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="8b572-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="8b572-143">例如：</span><span class="sxs-lookup"><span data-stu-id="8b572-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="8b572-144">HLS： **Path** + 資訊清單檔案名稱 + "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="8b572-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="8b572-145">例如：</span><span class="sxs-lookup"><span data-stu-id="8b572-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="8b572-146">DASH： **Path** + 資訊清單檔案名稱 + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="8b572-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="8b572-147">例如：</span><span class="sxs-lookup"><span data-stu-id="8b572-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="8b572-148">建置漸進式下載 URL</span><span class="sxs-lookup"><span data-stu-id="8b572-148">Build progressive download URLs</span></span>
<span data-ttu-id="8b572-149">建立定位器之後，使用傳回的 **Path** 值建置漸進式下載 URL。</span><span class="sxs-lookup"><span data-stu-id="8b572-149">Use the **Path** value returned after the creation of the locator to build the progressive download URL.</span></span>   

<span data-ttu-id="8b572-150">URL： **Path** + 資產檔案 MP4 名稱</span><span class="sxs-lookup"><span data-stu-id="8b572-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="8b572-151">例如：</span><span class="sxs-lookup"><span data-stu-id="8b572-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="8b572-152"><a id="types"></a>列舉類型</span><span class="sxs-lookup"><span data-stu-id="8b572-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="8b572-153">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="8b572-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8b572-154">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="8b572-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="8b572-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8b572-155">See also</span></span>
[<span data-ttu-id="8b572-156">媒體服務作業 REST API 概觀</span><span class="sxs-lookup"><span data-stu-id="8b572-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="8b572-157">設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="8b572-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

