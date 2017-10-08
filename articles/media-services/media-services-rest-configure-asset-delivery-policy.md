---
title: "使用媒體服務 REST API aaaConfiguring 資產傳遞原則 |Microsoft 文件"
description: "本主題說明如何使用媒體服務 REST API tooconfigure 不同資產傳遞原則。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="d7434-103">設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="d7434-104">如果您計劃 toodeliver 動態加密資產，hello 其中一個步驟中 hello 媒體服務內容傳遞工作流程設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="d7434-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="d7434-105">hello 資產傳遞原則會告知 Media Services 方式如您傳遞的資產 toobe： 成哪一個資料流通訊協定應在您的資產動態封裝 （適用於例如 MPEG DASH、 HLS、 Smooth Streaming 或全部），是否要 toodynamically加密您的資產和方式 （信封或一般加密）。</span><span class="sxs-lookup"><span data-stu-id="d7434-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="d7434-106">本主題討論原因以及如何 toocreate 及設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="d7434-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="d7434-107">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="d7434-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d7434-108">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="d7434-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="d7434-109">此外，toobe 無法 toouse 動態封裝和動態加密您的資產必須包含一組彈性位元速率 mp4 或彈性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="d7434-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="d7434-110">您可以套用不同的原則 toohello 相同資產。</span><span class="sxs-lookup"><span data-stu-id="d7434-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="d7434-111">例如，您可以套用 PlayReady 加密 tooSmooth 資料流與 AES 信封加密 tooMPEG DASH 和 HLS。</span><span class="sxs-lookup"><span data-stu-id="d7434-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="d7434-112">傳遞原則中未定義任何通訊協定 （例如，新增只能指定 HLS 作為 hello 通訊協定的單一原則），將無法從資料流。</span><span class="sxs-lookup"><span data-stu-id="d7434-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="d7434-113">hello 例外狀況 toothis 是如果您有未完全定義的資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="d7434-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="d7434-114">然後，將允許 hello 清除所有通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d7434-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="d7434-115">如果您想 toodeliver 儲存體加密資產時，您必須設定 hello 資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="d7434-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="d7434-116">在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="d7434-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="d7434-117">比方說，toodeliver 資產加密使用進階加密標準 (AES) 信封加密金鑰，將 hello 原則類型設定太**DynamicEnvelopeEncryption**。</span><span class="sxs-lookup"><span data-stu-id="d7434-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="d7434-118">tooremove 存放裝置加密和資料流 hello 資產中 hello 清除，設定 hello 原則類型太**NoDynamicEncryption**。</span><span class="sxs-lookup"><span data-stu-id="d7434-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="d7434-119">顯示如何 tooconfigure 這些原則類型的範例。</span><span class="sxs-lookup"><span data-stu-id="d7434-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="d7434-120">取決於您如何設定 hello 資產傳遞原則會是能 toodynamically 封裝、 動態加密和 hello 遵循串流通訊協定資料流： Smooth Streaming、 HLS、 MPEG DASH 資料流。</span><span class="sxs-lookup"><span data-stu-id="d7434-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="d7434-121">下列清單顯示 hello hello 格式化您使用 toostream Smooth、 HLS、 破折號。</span><span class="sxs-lookup"><span data-stu-id="d7434-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="d7434-122">Smooth Streaming：</span><span class="sxs-lookup"><span data-stu-id="d7434-122">Smooth Streaming:</span></span>

<span data-ttu-id="d7434-123">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="d7434-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="d7434-124">HLS：</span><span class="sxs-lookup"><span data-stu-id="d7434-124">HLS:</span></span>

<span data-ttu-id="d7434-125">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="d7434-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="d7434-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="d7434-126">MPEG DASH</span></span>

<span data-ttu-id="d7434-127">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="d7434-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="d7434-128">如需有關如何 toopublish 資產和建置串流 URL，請參閱指示[建置串流 URL](media-services-deliver-streaming-content.md)。</span><span class="sxs-lookup"><span data-stu-id="d7434-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="d7434-129">考量</span><span class="sxs-lookup"><span data-stu-id="d7434-129">Considerations</span></span>
* <span data-ttu-id="d7434-130">當資產的 OnDemand (串流) 定位器仍存在時，您無法刪除與該資產關聯的 AssetDeliveryPolicy。</span><span class="sxs-lookup"><span data-stu-id="d7434-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="d7434-131">hello 建議是從 hello 資產 tooremove hello 原則之前刪除 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="d7434-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="d7434-132">未設定資產傳遞原則時，將無法於儲存空間已加密的資產建立串流定位器。</span><span class="sxs-lookup"><span data-stu-id="d7434-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="d7434-133">如果 hello 資產不儲存體加密，hello 系統可讓您在 hello 清除未使用的資產傳遞原則中建立定位器和資料流的 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="d7434-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="d7434-134">您可以有多個單一資產相關聯的資產傳遞原則，但您只能指定其中一種方式 toohandle 給定 AssetDeliveryProtocol。</span><span class="sxs-lookup"><span data-stu-id="d7434-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="d7434-135">這表示如果您嘗試 toolink 兩個傳遞指定的原則，因為 hello 系統並不知道哪一個，將會導致錯誤的 hello AssetDeliveryProtocol.SmoothStreaming 通訊協定您希望 tooapply 當用戶端要求 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="d7434-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="d7434-136">如果您有現有的串流定位器的資產，您無法連結新的原則 toohello 資產、 取消連結現有的原則從 hello 資產，或更新與 hello 資產相關聯的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="d7434-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="d7434-137">第一次有 tooremove hello 串流定位器，調整 hello 原則，然後重新建立 hello 串流定位器。</span><span class="sxs-lookup"><span data-stu-id="d7434-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="d7434-138">您可以使用相同的 locatorId，當您重新建立 hello 串流定位器，但是您應該確定因為 hello 原點或下游 CDN 快取內容，將不會造成問題的用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="d7434-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="d7434-139">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="d7434-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d7434-140">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="d7434-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="d7434-141">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="d7434-141">Connect tooMedia Services</span></span>

<span data-ttu-id="d7434-142">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d7434-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d7434-143">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="d7434-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d7434-144">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="d7434-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="d7434-145">清除資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="d7434-146"><a id="create_asset_delivery_policy"></a>建立資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="d7434-147">hello 下列 HTTP 要求建立資產傳遞原則，指定 toonot 套用動態加密和 toodeliver hello 資料流中的 hello 遵循任何通訊協定： MPEG DASH、 HLS 和 Smooth Streaming 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d7434-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="d7434-148">建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。</span><span class="sxs-lookup"><span data-stu-id="d7434-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d7434-149">要求：</span><span class="sxs-lookup"><span data-stu-id="d7434-149">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

<span data-ttu-id="d7434-150">回應：</span><span class="sxs-lookup"><span data-stu-id="d7434-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <span data-ttu-id="d7434-151"><a id="link_asset_with_asset_delivery_policy"></a>連結資產與資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="d7434-152">下列 HTTP 要求的連結 hello hello 指定資產 toohello 資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="d7434-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="d7434-153">要求：</span><span class="sxs-lookup"><span data-stu-id="d7434-153">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

<span data-ttu-id="d7434-154">回應：</span><span class="sxs-lookup"><span data-stu-id="d7434-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="d7434-155">DynamicEnvelopeEncryption 資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="d7434-156">建立 hello EnvelopeEncryption 類型內容金鑰，並將它連結 toohello 資產</span><span class="sxs-lookup"><span data-stu-id="d7434-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="d7434-157">當指定 DynamicEnvelopeEncryption 傳遞原則，您需要 toomake 確定 toolink hello EnvelopeEncryption 類型將資產 tooa 內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="d7434-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="d7434-158">如需詳細資訊，請參閱 [建立內容金鑰](media-services-rest-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="d7434-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="d7434-159"><a id="get_delivery_url"></a>取得傳遞 URL</span><span class="sxs-lookup"><span data-stu-id="d7434-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="d7434-160">指定傳遞方法的 hello hello 先前步驟中建立的內容金鑰的 hello get hello 傳遞 URL。</span><span class="sxs-lookup"><span data-stu-id="d7434-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="d7434-161">用戶端會使用傳回 URL toorequest hello AES 金鑰或 PlayReady 授權順序 tooplayback hello 中的受保護的內容。</span><span class="sxs-lookup"><span data-stu-id="d7434-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="d7434-162">指定 hello hello HTTP 要求主體中的 hello URL tooget hello 類型。</span><span class="sxs-lookup"><span data-stu-id="d7434-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="d7434-163">如果您要保護使用 PlayReady，要求媒體服務 PlayReady 授權取得 URL，使用 1 hello keyDeliveryType: {"keyDeliveryType": 1}。</span><span class="sxs-lookup"><span data-stu-id="d7434-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="d7434-164">如果您要保護您的內容與 hello 信封加密，來要求金鑰取得 URL 指定 keyDeliveryType 的 2: {"keyDeliveryType": 2}。</span><span class="sxs-lookup"><span data-stu-id="d7434-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="d7434-165">要求：</span><span class="sxs-lookup"><span data-stu-id="d7434-165">Request:</span></span>

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

<span data-ttu-id="d7434-166">回應：</span><span class="sxs-lookup"><span data-stu-id="d7434-166">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="d7434-167">建立資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-167">Create asset delivery policy</span></span>
<span data-ttu-id="d7434-168">hello 下列 HTTP 要求建立 hello **AssetDeliveryPolicy**也就是設定的 tooapply 動態信封加密 (**DynamicEnvelopeEncryption**) toohello **HLS**通訊協定 （在此範例中，其他通訊協定將會遭到封鎖而無法串流處理）。</span><span class="sxs-lookup"><span data-stu-id="d7434-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="d7434-169">建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。</span><span class="sxs-lookup"><span data-stu-id="d7434-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d7434-170">要求：</span><span class="sxs-lookup"><span data-stu-id="d7434-170">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


<span data-ttu-id="d7434-171">回應：</span><span class="sxs-lookup"><span data-stu-id="d7434-171">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="d7434-172">連結資產與資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="d7434-173">請參閱 [連結資產與資產傳遞原則](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="d7434-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="d7434-174">DynamicCommonEncryption 資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="d7434-175">建立 hello CommonEncryption 類型內容金鑰，並將它連結 toohello 資產</span><span class="sxs-lookup"><span data-stu-id="d7434-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="d7434-176">當指定 DynamicCommonEncryption 傳遞原則，您需要 toomake 確定 toolink hello CommonEncryption 類型將資產 tooa 內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="d7434-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="d7434-177">如需詳細資訊，請參閱 [建立內容金鑰](media-services-rest-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="d7434-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="d7434-178">取得傳遞 URL</span><span class="sxs-lookup"><span data-stu-id="d7434-178">Get Delivery URL</span></span>
<span data-ttu-id="d7434-179">取得 hello PlayReady 傳遞方法的 hello hello 先前步驟中建立的內容金鑰 hello 傳遞 URL。</span><span class="sxs-lookup"><span data-stu-id="d7434-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="d7434-180">用戶端會使用 hello 傳回 URL toorequest PlayReady 授權順序 tooplayback hello 中的受保護的內容。</span><span class="sxs-lookup"><span data-stu-id="d7434-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="d7434-181">如需詳細資訊，請參閱 [取得傳遞 URL](#get_delivery_url)。</span><span class="sxs-lookup"><span data-stu-id="d7434-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="d7434-182">建立資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-182">Create asset delivery policy</span></span>
<span data-ttu-id="d7434-183">hello 下列 HTTP 要求建立 hello **AssetDeliveryPolicy**也就是設定的 tooapply 動態一般加密 (**DynamicCommonEncryption**) toohello **Smooth Streaming**通訊協定 （在此範例中，其他通訊協定將會遭到封鎖而無法串流處理）。</span><span class="sxs-lookup"><span data-stu-id="d7434-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="d7434-184">建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。</span><span class="sxs-lookup"><span data-stu-id="d7434-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="d7434-185">要求：</span><span class="sxs-lookup"><span data-stu-id="d7434-185">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


<span data-ttu-id="d7434-186">如果您想 tooprotect 您使用 Widevine DRM 的內容時，更新 hello AssetDeliveryConfiguration 值 toouse WidevineLicenseAcquisitionUrl （其 hello 值為 7），並指定 hello 授權傳遞服務 URL。</span><span class="sxs-lookup"><span data-stu-id="d7434-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="d7434-187">您可以使用下列 AMS 夥伴 toohelp 傳遞 Widevine 授權 hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)， [EZDRM](http://ezdrm.com/)， [castLabs](http://castlabs.com/company/partners/azure/)。</span><span class="sxs-lookup"><span data-stu-id="d7434-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="d7434-188">例如：</span><span class="sxs-lookup"><span data-stu-id="d7434-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="d7434-189">當 Widevine 使用加密，才會使用虛線無法 toodeliver。</span><span class="sxs-lookup"><span data-stu-id="d7434-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="d7434-190">請確定 toospecify 虛線 (2) 中的 hello 資產傳遞通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d7434-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="d7434-191">連結資產與資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="d7434-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="d7434-192">請參閱 [連結資產與資產傳遞原則](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="d7434-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="d7434-193"><a id="types"></a>定義 AssetDeliveryPolicy 時使用的類型</span><span class="sxs-lookup"><span data-stu-id="d7434-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="d7434-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="d7434-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="d7434-195">hello 下列列舉描述您可以針對 hello 資產傳遞通訊協定設定的值。</span><span class="sxs-lookup"><span data-stu-id="d7434-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="d7434-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="d7434-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="d7434-197">hello 下列列舉描述您可以設定 hello 資產傳遞原則類型的值。</span><span class="sxs-lookup"><span data-stu-id="d7434-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a><span data-ttu-id="d7434-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="d7434-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="d7434-199">hello 下列列舉描述您可以使用 hello 內容金鑰 toohello 用戶端 tooconfigure hello 傳遞方法的值。</span><span class="sxs-lookup"><span data-stu-id="d7434-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="d7434-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="d7434-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="d7434-201">下列列舉 hello 描述您可以設定資產傳遞原則的 tooconfigure 用金鑰 tooget 特定組態的值。</span><span class="sxs-lookup"><span data-stu-id="d7434-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="d7434-202">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="d7434-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d7434-203">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d7434-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

