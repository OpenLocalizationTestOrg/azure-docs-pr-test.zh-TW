---
title: "使用.NET SDK aaaConfigure 資產傳遞原則 |Microsoft 文件"
description: "本主題說明如何使用 Azure Media Services.NET SDK tooconfigure 不同資產傳遞原則。"
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="8aaad-103">使用 .NET SDK 設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="8aaad-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="8aaad-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8aaad-104">Overview</span></span>
<span data-ttu-id="8aaad-105">如果您計劃 toodelivery 加密資產，hello 其中一個步驟中 hello 媒體服務內容傳遞工作流程設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="8aaad-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="8aaad-106">hello 資產傳遞原則會告知 Media Services 方式如您傳遞的資產 toobe： 成哪一個資料流通訊協定應在您的資產動態封裝 （適用於例如 MPEG DASH、 HLS、 Smooth Streaming 或全部），是否要 toodynamically加密您的資產和方式 （信封或一般加密）。</span><span class="sxs-lookup"><span data-stu-id="8aaad-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="8aaad-107">本主題討論原因以及如何 toocreate 及設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="8aaad-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="8aaad-108">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="8aaad-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="8aaad-109">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="8aaad-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="8aaad-110">此外，toobe 無法 toouse 動態封裝和動態加密您的資產必須包含一組彈性位元速率 mp4 或彈性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="8aaad-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="8aaad-111">您可以套用不同的原則 toohello 相同資產。</span><span class="sxs-lookup"><span data-stu-id="8aaad-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="8aaad-112">例如，您可以套用 PlayReady 加密 tooSmooth 資料流與 AES 信封加密 tooMPEG DASH 和 HLS。</span><span class="sxs-lookup"><span data-stu-id="8aaad-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="8aaad-113">傳遞原則中未定義任何通訊協定 （例如，新增只能指定 HLS 作為 hello 通訊協定的單一原則），將無法從資料流。</span><span class="sxs-lookup"><span data-stu-id="8aaad-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="8aaad-114">hello 例外狀況 toothis 是如果您有未完全定義的資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="8aaad-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="8aaad-115">然後，將允許 hello 清除所有通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8aaad-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="8aaad-116">如果您想 toodeliver 儲存體加密資產時，您必須設定 hello 資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="8aaad-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="8aaad-117">在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="8aaad-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="8aaad-118">比方說，toodeliver 資產加密使用進階加密標準 (AES) 信封加密金鑰，將 hello 原則類型設定太**DynamicEnvelopeEncryption**。</span><span class="sxs-lookup"><span data-stu-id="8aaad-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="8aaad-119">tooremove 存放裝置加密和資料流 hello 資產中 hello 清除，設定 hello 原則類型太**NoDynamicEncryption**。</span><span class="sxs-lookup"><span data-stu-id="8aaad-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="8aaad-120">顯示如何 tooconfigure 這些原則類型的範例。</span><span class="sxs-lookup"><span data-stu-id="8aaad-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="8aaad-121">取決於您如何設定 hello 資產傳遞原則會是能 toodynamically 封裝、 動態加密和 hello 遵循串流通訊協定資料流： Smooth Streaming、 HLS 和 MPEG DASH 資料流。</span><span class="sxs-lookup"><span data-stu-id="8aaad-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="8aaad-122">hello 下列清單顯示 hello 格式，使用 toostream Smooth、 HLS 及虛線。</span><span class="sxs-lookup"><span data-stu-id="8aaad-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="8aaad-123">Smooth Streaming：</span><span class="sxs-lookup"><span data-stu-id="8aaad-123">Smooth Streaming:</span></span>

<span data-ttu-id="8aaad-124">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="8aaad-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="8aaad-125">HLS：</span><span class="sxs-lookup"><span data-stu-id="8aaad-125">HLS:</span></span>

<span data-ttu-id="8aaad-126">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="8aaad-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="8aaad-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="8aaad-127">MPEG DASH</span></span>

<span data-ttu-id="8aaad-128">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="8aaad-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="8aaad-129">考量</span><span class="sxs-lookup"><span data-stu-id="8aaad-129">Considerations</span></span>
* <span data-ttu-id="8aaad-130">當資產的 OnDemand (串流) 定位器仍存在時，您無法刪除與該資產關聯的 AssetDeliveryPolicy。</span><span class="sxs-lookup"><span data-stu-id="8aaad-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="8aaad-131">hello 建議是從 hello 資產 tooremove hello 原則之前刪除 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="8aaad-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="8aaad-132">未設定資產傳遞原則時，將無法於儲存空間已加密的資產建立串流定位器。</span><span class="sxs-lookup"><span data-stu-id="8aaad-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="8aaad-133">如果 hello 資產不儲存體加密，hello 系統可讓您在 hello 清除未使用的資產傳遞原則中建立定位器和資料流的 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="8aaad-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="8aaad-134">您可以有多個單一資產相關聯的資產傳遞原則，但您只能指定其中一種方式 toohandle 給定 AssetDeliveryProtocol。</span><span class="sxs-lookup"><span data-stu-id="8aaad-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="8aaad-135">這表示如果您嘗試 toolink 兩個傳遞指定的原則，因為 hello 系統並不知道哪一個，將會導致錯誤的 hello AssetDeliveryProtocol.SmoothStreaming 通訊協定您希望 tooapply 當用戶端要求 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="8aaad-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="8aaad-136">如果您有現有的串流定位器的資產，您無法連結新原則 toohello 資產 （您可以取消連結現有的原則從 hello 資產，或更新與 hello 資產相關聯的傳遞原則）。</span><span class="sxs-lookup"><span data-stu-id="8aaad-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="8aaad-137">第一次有 tooremove hello 串流定位器，調整 hello 原則，然後重新建立 hello 串流定位器。</span><span class="sxs-lookup"><span data-stu-id="8aaad-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="8aaad-138">您可以使用相同的 locatorId，當您重新建立 hello 串流定位器，但是您應該確定因為 hello 原點或下游 CDN 快取內容，將不會造成問題的用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="8aaad-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="8aaad-139">清除資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="8aaad-139">Clear asset delivery policy</span></span>

<span data-ttu-id="8aaad-140">hello 下列**ConfigureClearAssetDeliveryPolicy**方法指定 toonot 套用動態加密和 toodeliver hello 資料流中的 hello 遵循任何通訊協定： MPEG DASH、 HLS 和 Smooth Streaming 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8aaad-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="8aaad-141">您可能想 tooapply 此原則 tooyour 儲存體加密資產。</span><span class="sxs-lookup"><span data-stu-id="8aaad-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="8aaad-142">建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。</span><span class="sxs-lookup"><span data-stu-id="8aaad-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="8aaad-143">DynamicCommonEncryption 資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="8aaad-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="8aaad-144">hello 下列**CreateAssetDeliveryPolicy**方法會建立 hello **AssetDeliveryPolicy**也就是設定的 tooapply 動態一般加密 (**DynamicCommonEncryption**)tooa smooth streaming （其他通訊協定，將無法從資料流） 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8aaad-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="8aaad-145">hello 方法會採用兩個參數：**資產**(hello 資產 toowhich 想 tooapply hello 傳遞原則) 和**和 Contentkey** (hello 內容金鑰的 hello **CommonEncryption**類型，如需詳細資訊，請參閱：[建立內容金鑰](media-services-dotnet-create-contentkey.md#common_contentkey))。</span><span class="sxs-lookup"><span data-stu-id="8aaad-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="8aaad-146">建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。</span><span class="sxs-lookup"><span data-stu-id="8aaad-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="8aaad-147">Azure Media Services 也可讓您 tooadd Widevine 加密。</span><span class="sxs-lookup"><span data-stu-id="8aaad-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="8aaad-148">hello 下列範例示範 PlayReady 和 Widevine 加入 toohello 資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="8aaad-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="8aaad-149">當 Widevine 使用加密，才會使用虛線無法 toodeliver。</span><span class="sxs-lookup"><span data-stu-id="8aaad-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="8aaad-150">請確定 toospecify 虛線 hello 資產傳遞通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8aaad-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="8aaad-151">DynamicEnvelopeEncryption 資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="8aaad-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="8aaad-152">hello 下列**CreateAssetDeliveryPolicy**方法會建立 hello **AssetDeliveryPolicy**也就是設定的 tooapply 動態信封加密 (**DynamicEnvelopeEncryption**) tooSmooth Streaming、 HLS 及虛線通訊協定 （如果您決定 toonot 指定某些通訊協定，它們將會遭到封鎖而無法串流處理）。</span><span class="sxs-lookup"><span data-stu-id="8aaad-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="8aaad-153">hello 方法會採用兩個參數：**資產**(hello 資產 toowhich 想 tooapply hello 傳遞原則) 和**和 Contentkey** (hello 內容金鑰的 hello **EnvelopeEncryption**類型，如需詳細資訊，請參閱：[建立內容金鑰](media-services-dotnet-create-contentkey.md#envelope_contentkey))。</span><span class="sxs-lookup"><span data-stu-id="8aaad-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="8aaad-154">建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。</span><span class="sxs-lookup"><span data-stu-id="8aaad-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="8aaad-155"><a id="types"></a>定義 AssetDeliveryPolicy 時使用的類型</span><span class="sxs-lookup"><span data-stu-id="8aaad-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="8aaad-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="8aaad-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="8aaad-157">hello 下列列舉描述您可以針對 hello 資產傳遞通訊協定設定的值。</span><span class="sxs-lookup"><span data-stu-id="8aaad-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="8aaad-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="8aaad-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="8aaad-159">hello 下列列舉描述您可以設定 hello 資產傳遞原則類型的值。</span><span class="sxs-lookup"><span data-stu-id="8aaad-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="8aaad-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="8aaad-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="8aaad-161">hello 下列列舉描述您可以使用 hello 內容金鑰 toohello 用戶端 tooconfigure hello 傳遞方法的值。</span><span class="sxs-lookup"><span data-stu-id="8aaad-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="8aaad-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="8aaad-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="8aaad-163">下列列舉 hello 描述您可以設定資產傳遞原則的 tooconfigure 用金鑰 tooget 特定組態的值。</span><span class="sxs-lookup"><span data-stu-id="8aaad-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="8aaad-164">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="8aaad-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8aaad-165">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="8aaad-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

