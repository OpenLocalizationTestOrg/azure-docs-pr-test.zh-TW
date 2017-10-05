---
title: "使用媒體服務 REST API 設定資產傳遞原則 | Microsoft Docs"
description: "本主題說明如何使用媒體服務 REST API 設定不同的資產傳遞原則。"
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
ms.openlocfilehash: 7ffbde11b943961dd3a3b5edebd0cfd52429e845
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="a89b3-103">設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="a89b3-104">如果您打算傳遞動態加密的資產，媒體服務內容傳遞工作流程的其中一個步驟，是設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="a89b3-104">If you plan to deliver dynamically encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="a89b3-105">資產傳遞原則會告訴媒體服務您想要如何傳遞資產：您的資產應該動態封裝成哪個串流通訊協定 (如 MPEG DASH、HLS、Smooth Streaming 或所有)，您是否想要動態加密您的資產及其方式 (信封或一般加密)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-105">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="a89b3-106">本主題討論建立和設定資產傳遞原則的原因與方法。</span><span class="sxs-lookup"><span data-stu-id="a89b3-106">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="a89b3-107">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a89b3-107">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="a89b3-108">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="a89b3-108">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="a89b3-109">此外，為了能夠使用動態封裝和動態加密功能，您的資產必須包含一組調適性位元速率 MP4 或調適性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="a89b3-109">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="a89b3-110">您可以將不同的原則套用至相同的資產。</span><span class="sxs-lookup"><span data-stu-id="a89b3-110">You could apply different policies to the same asset.</span></span> <span data-ttu-id="a89b3-111">例如，您可以將 PlayReady 加密套用到 Smooth Streaming，將 AES 信封加密套用到 MPEG DASH 和 HLS。</span><span class="sxs-lookup"><span data-stu-id="a89b3-111">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="a89b3-112">傳遞原則中未定義的任何通訊協定 (例如，您加入單一原則，它只有指定 HLS 做為通訊協定) 將會遭到封鎖無法串流。</span><span class="sxs-lookup"><span data-stu-id="a89b3-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="a89b3-113">這個狀況的例外情形是您完全沒有定義資產傳遞原則之時。</span><span class="sxs-lookup"><span data-stu-id="a89b3-113">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="a89b3-114">那麼，將允許所有通訊協定，不受阻礙。</span><span class="sxs-lookup"><span data-stu-id="a89b3-114">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="a89b3-115">如果您想要傳遞儲存體加密資產，就必須設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="a89b3-115">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="a89b3-116">資產可以串流處理之前，串流伺服器會移除儲存體加密，並使用指定的傳遞原則來串流您的內容。</span><span class="sxs-lookup"><span data-stu-id="a89b3-116">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="a89b3-117">例如，若要傳遞使用進階加密標準 (AES) 信封加密金鑰加密的資產，請將原則類型設定為 **DynamicEnvelopeEncryption**。</span><span class="sxs-lookup"><span data-stu-id="a89b3-117">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="a89b3-118">如果您要移除儲存體加密，並且不受阻礙地串流資產，請將原則類型設定為 **NoDynamicEncryption**。</span><span class="sxs-lookup"><span data-stu-id="a89b3-118">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="a89b3-119">下列範例示範如何設定這些原則類型。</span><span class="sxs-lookup"><span data-stu-id="a89b3-119">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="a89b3-120">視您如何設定資產傳遞原則而定，您可以動態封裝、動態加密，以及串流下列串流通訊協定：Smooth Streaming、HLS、MPEG DASH 資料流。</span><span class="sxs-lookup"><span data-stu-id="a89b3-120">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="a89b3-121">下列清單顯示您用來串流 Smooth、HLS、DASH 的格式。</span><span class="sxs-lookup"><span data-stu-id="a89b3-121">The following list shows the formats that you use to stream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="a89b3-122">Smooth Streaming：</span><span class="sxs-lookup"><span data-stu-id="a89b3-122">Smooth Streaming:</span></span>

<span data-ttu-id="a89b3-123">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="a89b3-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="a89b3-124">HLS：</span><span class="sxs-lookup"><span data-stu-id="a89b3-124">HLS:</span></span>

<span data-ttu-id="a89b3-125">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="a89b3-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="a89b3-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="a89b3-126">MPEG DASH</span></span>

<span data-ttu-id="a89b3-127">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="a89b3-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="a89b3-128">如需有關如何發佈資產，並建置串流 URL 的指示，請參閱 [建置串流 URL](media-services-deliver-streaming-content.md)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-128">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="a89b3-129">考量</span><span class="sxs-lookup"><span data-stu-id="a89b3-129">Considerations</span></span>
* <span data-ttu-id="a89b3-130">當資產的 OnDemand (串流) 定位器仍存在時，您無法刪除與該資產關聯的 AssetDeliveryPolicy。</span><span class="sxs-lookup"><span data-stu-id="a89b3-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="a89b3-131">建議刪除原則之前，先將該原則從資產移除。</span><span class="sxs-lookup"><span data-stu-id="a89b3-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="a89b3-132">未設定資產傳遞原則時，將無法於儲存空間已加密的資產建立串流定位器。</span><span class="sxs-lookup"><span data-stu-id="a89b3-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="a89b3-133">如果資產的儲存空間未加密，系統會讓您建立定位器，並直接串流資產而不使用資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="a89b3-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="a89b3-134">您可以有多個資產傳遞原則與一個資產關聯，但只能指定一種方法處理特定的 AssetDeliveryProtocol。</span><span class="sxs-lookup"><span data-stu-id="a89b3-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="a89b3-135">這表示如果您嘗試連結二個指定 AssetDeliveryProtocol.SmoothStreaming 通訊協定的傳遞原則時將會導致錯誤，因為當用戶端發出 Smooth Streaming 要求時，系統會不知道要套用哪一個原則。</span><span class="sxs-lookup"><span data-stu-id="a89b3-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="a89b3-136">如果您有包含現有串流定位器的資產，則您無法將新原則連接到該資產，請解除現有原則與資產的連結，或更新與資產關聯的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="a89b3-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset, unlink an existing policy from the asset, or update a delivery policy associated with the asset.</span></span>  <span data-ttu-id="a89b3-137">您必須先移除串流定位器，調整原則，然後重新建立串流定位器。</span><span class="sxs-lookup"><span data-stu-id="a89b3-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="a89b3-138">重新建立串流定位器時，您可以使用同一個 locatorId，但必須確定不會對用戶端造成問題，因為原始或下游 CDN 可能會快取內容。</span><span class="sxs-lookup"><span data-stu-id="a89b3-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="a89b3-139">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="a89b3-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a89b3-140">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="a89b3-141">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="a89b3-141">Connect to Media Services</span></span>

<span data-ttu-id="a89b3-142">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-142">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a89b3-143">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="a89b3-143">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a89b3-144">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="a89b3-144">You must make subsequent calls to the new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="a89b3-145">清除資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="a89b3-146"><a id="create_asset_delivery_policy"></a>建立資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="a89b3-147">下列 HTTP 要求會建立資產傳遞原則，指定不要套用動態加密，並以下列任何通訊協定傳遞資料流：MPEG DASH、HLS 和 Smooth Streaming 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a89b3-147">The following HTTP request creates an asset delivery policy that specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="a89b3-148">如需建立 AssetDeliveryPolicy 時可以指定之值的相關資訊，請參閱[定義 AssetDeliveryPolicy 時使用的類型](#types) 一節。</span><span class="sxs-lookup"><span data-stu-id="a89b3-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="a89b3-149">要求：</span><span class="sxs-lookup"><span data-stu-id="a89b3-149">Request:</span></span>

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

<span data-ttu-id="a89b3-150">回應：</span><span class="sxs-lookup"><span data-stu-id="a89b3-150">Response:</span></span>

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

### <span data-ttu-id="a89b3-151"><a id="link_asset_with_asset_delivery_policy"></a>連結資產與資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="a89b3-152">下列 HTTP 要求會將指定的資產連結至資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="a89b3-152">The following HTTP request links the specified asset to the asset delivery policy to.</span></span>

<span data-ttu-id="a89b3-153">要求：</span><span class="sxs-lookup"><span data-stu-id="a89b3-153">Request:</span></span>

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

<span data-ttu-id="a89b3-154">回應：</span><span class="sxs-lookup"><span data-stu-id="a89b3-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="a89b3-155">DynamicEnvelopeEncryption 資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-envelopeencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="a89b3-156">建立 EnvelopeEncryption 類型的內容金鑰，並將它連結到資產</span><span class="sxs-lookup"><span data-stu-id="a89b3-156">Create content key of the EnvelopeEncryption type and link it to the asset</span></span>
<span data-ttu-id="a89b3-157">當指定 DynamicEnvelopeEncryption 傳遞原則時，您必須將資產連結到 EnvelopeEncryption 類型的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="a89b3-157">When specifying DynamicEnvelopeEncryption delivery policy, you need to make sure to link your asset to a content key of the EnvelopeEncryption type.</span></span> <span data-ttu-id="a89b3-158">如需詳細資訊，請參閱 [建立內容金鑰](media-services-rest-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="a89b3-159"><a id="get_delivery_url"></a>取得傳遞 URL</span><span class="sxs-lookup"><span data-stu-id="a89b3-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="a89b3-160">針對前一個步驟中建立的內容金鑰的指定傳遞方法，取得傳遞 URL。</span><span class="sxs-lookup"><span data-stu-id="a89b3-160">Get the delivery URL for the specified delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="a89b3-161">用戶端會使用傳回的 URL 要求 AES 金鑰或 PlayReady 授權，以便播放受保護的內容。</span><span class="sxs-lookup"><span data-stu-id="a89b3-161">A client uses the returned URL to request an AES key or a PlayReady license in order to playback the protected content.</span></span>

<span data-ttu-id="a89b3-162">指定要在 HTTP 要求主體中取得的 URL 類型。</span><span class="sxs-lookup"><span data-stu-id="a89b3-162">Specify the type of the URL to get in the body of the HTTP request.</span></span> <span data-ttu-id="a89b3-163">如果您要使用 PlayReady 保護您的內容，請要求媒體服務 PlayReady 授權取得 URL，並針對 keyDeliveryType 使用 1：{"keyDeliveryType":1}。</span><span class="sxs-lookup"><span data-stu-id="a89b3-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for the keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="a89b3-164">如果您要使用信封加密保護您的內容，請針對 keyDeliveryType 指定 2，來要求金鑰取得 URL：{"keyDeliveryType":2}。</span><span class="sxs-lookup"><span data-stu-id="a89b3-164">If you are protecting your content with the envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="a89b3-165">要求：</span><span class="sxs-lookup"><span data-stu-id="a89b3-165">Request:</span></span>

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

<span data-ttu-id="a89b3-166">回應：</span><span class="sxs-lookup"><span data-stu-id="a89b3-166">Response:</span></span>

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


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="a89b3-167">建立資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-167">Create asset delivery policy</span></span>
<span data-ttu-id="a89b3-168">下列 HTTP 要求會建立 **AssetDeliveryPolicy**，它會設定為將動態信封加密 (**DynamicEnvelopeEncryption**) 套用到 **HLS** 通訊協定 (在此範例中，其他通訊協定將會被封鎖，無法串流)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-168">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to the **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="a89b3-169">如需建立 AssetDeliveryPolicy 時可以指定之值的相關資訊，請參閱 [定義 AssetDeliveryPolicy 時使用的類型](#types) 一節。</span><span class="sxs-lookup"><span data-stu-id="a89b3-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="a89b3-170">要求：</span><span class="sxs-lookup"><span data-stu-id="a89b3-170">Request:</span></span>

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


<span data-ttu-id="a89b3-171">回應：</span><span class="sxs-lookup"><span data-stu-id="a89b3-171">Response:</span></span>

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


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="a89b3-172">連結資產與資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="a89b3-173">請參閱 [連結資產與資產傳遞原則](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="a89b3-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="a89b3-174">DynamicCommonEncryption 資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-commonencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="a89b3-175">建立 CommonEncryption 類型的內容金鑰，並將它連結到資產</span><span class="sxs-lookup"><span data-stu-id="a89b3-175">Create content key of the CommonEncryption type and link it to the asset</span></span>
<span data-ttu-id="a89b3-176">當指定 DynamicCommonEncryption 傳遞原則時，您必須將資產連結到 CommonEncryption 類型的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="a89b3-176">When specifying DynamicCommonEncryption delivery policy, you need to make sure to link your asset to a content key of the CommonEncryption type.</span></span> <span data-ttu-id="a89b3-177">如需詳細資訊，請參閱 [建立內容金鑰](media-services-rest-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="a89b3-178">取得傳遞 URL</span><span class="sxs-lookup"><span data-stu-id="a89b3-178">Get Delivery URL</span></span>
<span data-ttu-id="a89b3-179">針對前一個步驟中建立的內容金鑰的 PlayReady 傳遞方法，取得傳遞 URL。</span><span class="sxs-lookup"><span data-stu-id="a89b3-179">Get the delivery URL for the PlayReady delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="a89b3-180">用戶端會使用傳回的 URL 要求 PlayReady 授權，以便播放受保護的內容。</span><span class="sxs-lookup"><span data-stu-id="a89b3-180">A client uses the returned URL to request a PlayReady license in order to playback the protected content.</span></span> <span data-ttu-id="a89b3-181">如需詳細資訊，請參閱 [取得傳遞 URL](#get_delivery_url)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="a89b3-182">建立資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-182">Create asset delivery policy</span></span>
<span data-ttu-id="a89b3-183">下列 HTTP 要求會建立 **AssetDeliveryPolicy**，它會設定為將動態一般加密 (**DynamicCommonEncryption**) 套用到 **Smooth Streaming** 通訊協定 (在此範例中，其他通訊協定將會被封鎖，無法串流)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-183">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to the **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="a89b3-184">如需建立 AssetDeliveryPolicy 時可以指定之值的相關資訊，請參閱 [定義 AssetDeliveryPolicy 時使用的類型](#types) 一節。</span><span class="sxs-lookup"><span data-stu-id="a89b3-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="a89b3-185">要求：</span><span class="sxs-lookup"><span data-stu-id="a89b3-185">Request:</span></span>

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


<span data-ttu-id="a89b3-186">如果您想要使用 Widevine DRM 保護內容，請將 AssetDeliveryConfiguration 值更新為使用 WidevineLicenseAcquisitionUrl (其值為 7) 和指定授權傳遞服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="a89b3-186">If you want to protect your content using Widevine DRM, update the AssetDeliveryConfiguration values to use WidevineLicenseAcquisitionUrl (which has the value of 7) and specify the URL of a license delivery service.</span></span> <span data-ttu-id="a89b3-187">您可以使用下列 AMS 合作夥伴來助您傳遞 Widevine 授權：[Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)、[EZDRM](http://ezdrm.com/)、[castLabs](http://castlabs.com/company/partners/azure/)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-187">You can use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="a89b3-188">例如：</span><span class="sxs-lookup"><span data-stu-id="a89b3-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="a89b3-189">以 Widevine 加密時，就只能使用 DASH 來傳遞。</span><span class="sxs-lookup"><span data-stu-id="a89b3-189">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="a89b3-190">請務必在資產傳遞通訊協定中指定 DASH (2)。</span><span class="sxs-lookup"><span data-stu-id="a89b3-190">Make sure to specify DASH (2) in the asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="a89b3-191">連結資產與資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="a89b3-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="a89b3-192">請參閱 [連結資產與資產傳遞原則](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="a89b3-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="a89b3-193"><a id="types"></a>定義 AssetDeliveryPolicy 時使用的類型</span><span class="sxs-lookup"><span data-stu-id="a89b3-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="a89b3-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="a89b3-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="a89b3-195">下列列舉描述您可以針對資產傳遞通訊協定設定的值。</span><span class="sxs-lookup"><span data-stu-id="a89b3-195">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="a89b3-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="a89b3-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="a89b3-197">下列列舉描述您可以針對資產傳遞原則類型設定的值。</span><span class="sxs-lookup"><span data-stu-id="a89b3-197">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <a name="contentkeydeliverytype"></a><span data-ttu-id="a89b3-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="a89b3-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="a89b3-199">下列列舉描述您可用來設定將內容金鑰傳遞給用戶端之方法的值。</span><span class="sxs-lookup"><span data-stu-id="a89b3-199">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="a89b3-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="a89b3-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="a89b3-201">下列列舉描述您可以設定的值，以便設定用來取得資產傳遞原則特定設定的金鑰。</span><span class="sxs-lookup"><span data-stu-id="a89b3-201">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="a89b3-202">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="a89b3-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a89b3-203">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="a89b3-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

