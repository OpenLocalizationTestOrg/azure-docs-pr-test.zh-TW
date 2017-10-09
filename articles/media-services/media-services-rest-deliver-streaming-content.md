---
title: "使用 REST aaaPublish Azure 媒體服務內容"
description: "深入了解如何 toocreate 是使用的 toobuild 串流 URL 定位器。 hello 程式碼使用 REST API。"
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
ms.openlocfilehash: f849e21b3103b9b33bc652e886b2016ea495b19a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="c004e-104">使用 REST 發佈 Azure 媒體服務內容</span><span class="sxs-lookup"><span data-stu-id="c004e-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c004e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c004e-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="c004e-106">REST</span><span class="sxs-lookup"><span data-stu-id="c004e-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="c004e-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="c004e-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c004e-108">Overview</span><span class="sxs-lookup"><span data-stu-id="c004e-108">Overview</span></span>
<span data-ttu-id="c004e-109">您可以建立隨選串流定位器及建置串流 URL，串流處理調適性位元速率 MP4 集。</span><span class="sxs-lookup"><span data-stu-id="c004e-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="c004e-110">hello[編碼資產](media-services-rest-encode-asset.md)主題說明如何設定 tooencode 成彈性位元速率 MP4。</span><span class="sxs-lookup"><span data-stu-id="c004e-110">hello [encoding an asset](media-services-rest-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="c004e-111">如果您的內容已加密，請在建立定位器之前設定資產傳遞原則 (如 [這個](media-services-rest-configure-asset-delivery-policy.md) 主題中所述)。</span><span class="sxs-lookup"><span data-stu-id="c004e-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="c004e-112">您也可以使用串流定位器 toobuild Url 可以漸進式下載該點 tooMP4 檔案 OnDemand。</span><span class="sxs-lookup"><span data-stu-id="c004e-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="c004e-113">本主題說明如何 toocreate OnDemand 串流定位器中的排序 toopublish 資產並建置 Smooth、 MPEG DASH 和 HLS 資料流 Url。</span><span class="sxs-lookup"><span data-stu-id="c004e-113">This topic shows how toocreate an OnDemand streaming locator in order toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="c004e-114">它也會示範熱 toobuild 漸進式下載 Url。</span><span class="sxs-lookup"><span data-stu-id="c004e-114">It also shows hot toobuild progressive download URLs.</span></span>

<span data-ttu-id="c004e-115">hello[下列](#types)區段會顯示 hello 列舉型別會使用其值在 hello REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="c004e-115">hello [following](#types) section shows hello enum types whose values are used in hello REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="c004e-116">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="c004e-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="c004e-117">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="c004e-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="c004e-118">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="c004e-118">Connect tooMedia Services</span></span>

<span data-ttu-id="c004e-119">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="c004e-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="c004e-120">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="c004e-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="c004e-121">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="c004e-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="c004e-122">建立隨選串流定位器</span><span class="sxs-lookup"><span data-stu-id="c004e-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="c004e-123">toocreate hello OnDemand 串流定位器，並取得您需要遵循 toodo hello 的 Url:</span><span class="sxs-lookup"><span data-stu-id="c004e-123">toocreate hello OnDemand streaming locator and get URLs you need toodo hello following:</span></span>

1. <span data-ttu-id="c004e-124">如果 hello 內容會經過加密，定義存取原則。</span><span class="sxs-lookup"><span data-stu-id="c004e-124">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="c004e-125">建立隨選串流定位器。</span><span class="sxs-lookup"><span data-stu-id="c004e-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="c004e-126">如果您計劃 toostream，取得資料流 hello 資產中的資訊清單檔案 (.ism) 的 hello。</span><span class="sxs-lookup"><span data-stu-id="c004e-126">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="c004e-127">如果您計劃 tooprogressively 下載，會收到 hello hello 資產中的 MP4 檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="c004e-127">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span> 
4. <span data-ttu-id="c004e-128">建置 Url toohello 資訊清單檔或 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="c004e-128">Build URLs toohello manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="c004e-129">請注意，您無法使用包含寫入或刪除權限的 AccessPolicy 建立串流訂位器。</span><span class="sxs-lookup"><span data-stu-id="c004e-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="c004e-130">建立存取原則</span><span class="sxs-lookup"><span data-stu-id="c004e-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="c004e-131">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="c004e-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="c004e-132">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="c004e-132">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="c004e-133">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="c004e-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="c004e-134">要求：</span><span class="sxs-lookup"><span data-stu-id="c004e-134">Request:</span></span>

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

<span data-ttu-id="c004e-135">回應：</span><span class="sxs-lookup"><span data-stu-id="c004e-135">Response:</span></span>

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

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="c004e-136">建立隨選串流定位器</span><span class="sxs-lookup"><span data-stu-id="c004e-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="c004e-137">建立 hello 定位器 hello 指定的資產和資產的原則。</span><span class="sxs-lookup"><span data-stu-id="c004e-137">Create hello locator for hello specified asset and asset policy.</span></span>

<span data-ttu-id="c004e-138">要求：</span><span class="sxs-lookup"><span data-stu-id="c004e-138">Request:</span></span>

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

<span data-ttu-id="c004e-139">回應：</span><span class="sxs-lookup"><span data-stu-id="c004e-139">Response:</span></span>

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

### <a name="build-streaming-urls"></a><span data-ttu-id="c004e-140">建置串流 URL</span><span class="sxs-lookup"><span data-stu-id="c004e-140">Build streaming URLs</span></span>
<span data-ttu-id="c004e-141">使用 hello**路徑**hello 定位器 toobuild hello hello 建立之後 Smooth、 HLS 及 MPEG DASH Url 傳回的值。</span><span class="sxs-lookup"><span data-stu-id="c004e-141">Use hello **Path** value returned after hello creation of hello locator toobuild hello Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="c004e-142">Smooth Streaming： **Path** + 資訊清單檔案名稱 + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="c004e-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="c004e-143">例如：</span><span class="sxs-lookup"><span data-stu-id="c004e-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="c004e-144">HLS： **Path** + 資訊清單檔案名稱 + "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="c004e-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="c004e-145">例如：</span><span class="sxs-lookup"><span data-stu-id="c004e-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="c004e-146">DASH： **Path** + 資訊清單檔案名稱 + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="c004e-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="c004e-147">例如：</span><span class="sxs-lookup"><span data-stu-id="c004e-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="c004e-148">建置漸進式下載 URL</span><span class="sxs-lookup"><span data-stu-id="c004e-148">Build progressive download URLs</span></span>
<span data-ttu-id="c004e-149">使用 hello**路徑**hello 建立 hello 定位器 toobuild hello 漸進式下載 URL 之後，傳回值。</span><span class="sxs-lookup"><span data-stu-id="c004e-149">Use hello **Path** value returned after hello creation of hello locator toobuild hello progressive download URL.</span></span>   

<span data-ttu-id="c004e-150">URL： **Path** + 資產檔案 MP4 名稱</span><span class="sxs-lookup"><span data-stu-id="c004e-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="c004e-151">例如：</span><span class="sxs-lookup"><span data-stu-id="c004e-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="c004e-152"><a id="types"></a>列舉類型</span><span class="sxs-lookup"><span data-stu-id="c004e-152"><a id="types"></a>Enum types</span></span>
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="c004e-153">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="c004e-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c004e-154">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c004e-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c004e-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c004e-155">See also</span></span>
[<span data-ttu-id="c004e-156">媒體服務作業 REST API 概觀</span><span class="sxs-lookup"><span data-stu-id="c004e-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="c004e-157">設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="c004e-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

