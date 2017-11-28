---
title: "使用 .NET SDK 設定資產傳遞原則 | Microsoft Docs"
description: "本主題說明如何使用 Azure 媒體服務 .NET SDK 設定不同的資產傳遞原則。"
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
ms.openlocfilehash: 282fd9e24dc147e31613469926128894d48366f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="832f3-103">使用 .NET SDK 設定資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="832f3-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="832f3-104">概觀</span><span class="sxs-lookup"><span data-stu-id="832f3-104">Overview</span></span>
<span data-ttu-id="832f3-105">如果您打算傳遞加密的資產，媒體服務內容傳遞工作流程的其中一個步驟，是設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="832f3-105">If you plan to delivery encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="832f3-106">資產傳遞原則會告訴媒體服務您想要如何傳遞資產：您的資產應該動態封裝成哪個串流通訊協定 (如 MPEG DASH、HLS、Smooth Streaming 或所有)，您是否想要動態加密您的資產及其方式 (信封或一般加密)。</span><span class="sxs-lookup"><span data-stu-id="832f3-106">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="832f3-107">本主題討論建立和設定資產傳遞原則的原因與方法。</span><span class="sxs-lookup"><span data-stu-id="832f3-107">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="832f3-108">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="832f3-108">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="832f3-109">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="832f3-109">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="832f3-110">此外，為了能夠使用動態封裝和動態加密功能，您的資產必須包含一組調適性位元速率 MP4 或調適性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="832f3-110">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="832f3-111">您可以將不同的原則套用至相同的資產。</span><span class="sxs-lookup"><span data-stu-id="832f3-111">You could apply different policies to the same asset.</span></span> <span data-ttu-id="832f3-112">例如，您可以將 PlayReady 加密套用到 Smooth Streaming，將 AES 信封加密套用到 MPEG DASH 和 HLS。</span><span class="sxs-lookup"><span data-stu-id="832f3-112">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="832f3-113">傳遞原則中未定義的任何通訊協定 (例如，您加入單一原則，它只有指定 HLS 做為通訊協定) 將會遭到封鎖無法串流。</span><span class="sxs-lookup"><span data-stu-id="832f3-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="832f3-114">這個狀況的例外情形是您完全沒有定義資產傳遞原則之時。</span><span class="sxs-lookup"><span data-stu-id="832f3-114">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="832f3-115">那麼，將允許所有通訊協定，不受阻礙。</span><span class="sxs-lookup"><span data-stu-id="832f3-115">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="832f3-116">如果您想要傳遞儲存體加密資產，就必須設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="832f3-116">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="832f3-117">資產可以串流處理之前，串流伺服器會移除儲存體加密，並使用指定的傳遞原則來串流您的內容。</span><span class="sxs-lookup"><span data-stu-id="832f3-117">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="832f3-118">例如，若要傳遞使用進階加密標準 (AES) 信封加密金鑰加密的資產，請將原則類型設定為 **DynamicEnvelopeEncryption**。</span><span class="sxs-lookup"><span data-stu-id="832f3-118">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="832f3-119">如果您要移除儲存體加密，並且不受阻礙地串流資產，請將原則類型設定為 **NoDynamicEncryption**。</span><span class="sxs-lookup"><span data-stu-id="832f3-119">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="832f3-120">下列範例示範如何設定這些原則類型。</span><span class="sxs-lookup"><span data-stu-id="832f3-120">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="832f3-121">視您如何設定資產傳遞原則而定，您可以動態封裝、動態加密，以及串流下列串流通訊協定：Smooth Streaming、HLS 和 MPEG DASH 資料流。</span><span class="sxs-lookup"><span data-stu-id="832f3-121">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="832f3-122">下列清單顯示您用來串流 Smooth、HLS 和 DASH 的格式。</span><span class="sxs-lookup"><span data-stu-id="832f3-122">The following list shows the formats that you use to stream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="832f3-123">Smooth Streaming：</span><span class="sxs-lookup"><span data-stu-id="832f3-123">Smooth Streaming:</span></span>

<span data-ttu-id="832f3-124">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="832f3-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="832f3-125">HLS：</span><span class="sxs-lookup"><span data-stu-id="832f3-125">HLS:</span></span>

<span data-ttu-id="832f3-126">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="832f3-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="832f3-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="832f3-127">MPEG DASH</span></span>

<span data-ttu-id="832f3-128">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="832f3-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="832f3-129">考量</span><span class="sxs-lookup"><span data-stu-id="832f3-129">Considerations</span></span>
* <span data-ttu-id="832f3-130">當資產的 OnDemand (串流) 定位器仍存在時，您無法刪除與該資產關聯的 AssetDeliveryPolicy。</span><span class="sxs-lookup"><span data-stu-id="832f3-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="832f3-131">建議刪除原則之前，先將該原則從資產移除。</span><span class="sxs-lookup"><span data-stu-id="832f3-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="832f3-132">未設定資產傳遞原則時，將無法於儲存空間已加密的資產建立串流定位器。</span><span class="sxs-lookup"><span data-stu-id="832f3-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="832f3-133">如果資產的儲存空間未加密，系統會讓您建立定位器，並直接串流資產而不使用資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="832f3-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="832f3-134">您可以有多個資產傳遞原則與一個資產關聯，但只能指定一種方法處理特定的 AssetDeliveryProtocol。</span><span class="sxs-lookup"><span data-stu-id="832f3-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="832f3-135">這表示如果您嘗試連結二個指定 AssetDeliveryProtocol.SmoothStreaming 通訊協定的傳遞原則時將會導致錯誤，因為當用戶端發出 Smooth Streaming 要求時，系統會不知道要套用哪一個原則。</span><span class="sxs-lookup"><span data-stu-id="832f3-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="832f3-136">如果您有包含現有串流定位器的資產，則您無法將新原則連接到該資產 (您可以解除現有原則與資產的連結，或更新與資產關聯的傳遞原則)。</span><span class="sxs-lookup"><span data-stu-id="832f3-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset (you can either unlink an existing policy from the asset, or update a delivery policy associated with the asset).</span></span>  <span data-ttu-id="832f3-137">您必須先移除串流定位器，調整原則，然後重新建立串流定位器。</span><span class="sxs-lookup"><span data-stu-id="832f3-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="832f3-138">重新建立串流定位器時，您可以使用同一個 locatorId，但必須確定不會對用戶端造成問題，因為原始或下游 CDN 可能會快取內容。</span><span class="sxs-lookup"><span data-stu-id="832f3-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="832f3-139">清除資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="832f3-139">Clear asset delivery policy</span></span>

<span data-ttu-id="832f3-140">下列 **ConfigureClearAssetDeliveryPolicy** 方法指定不套用動態加密，以及使用下列任何通訊協定來傳遞資料流：MPEG DASH、HLS 和 Smooth Streaming 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="832f3-140">The following **ConfigureClearAssetDeliveryPolicy** method specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="832f3-141">您可能想要將此原則套用到您的儲存體加密資產。</span><span class="sxs-lookup"><span data-stu-id="832f3-141">You might want to apply this policy to your storage encrypted assets.</span></span>

<span data-ttu-id="832f3-142">如需建立 AssetDeliveryPolicy 時可以指定之值的相關資訊，請參閱 [定義 AssetDeliveryPolicy 時使用的類型](#types) 一節。</span><span class="sxs-lookup"><span data-stu-id="832f3-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="832f3-143">DynamicCommonEncryption 資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="832f3-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="832f3-144">下列 **CreateAssetDeliveryPolicy** 方法會建立 **AssetDeliveryPolicy**，而後者設定成將動態一般加密 (**DynamicCommonEncryption**) 套用至 Smooth Streaming 通訊協定 (將會封鎖其他通訊協定進行串流處理)。</span><span class="sxs-lookup"><span data-stu-id="832f3-144">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to a smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="832f3-145">此方法會採用兩個參數：**Asset** (您要套用傳遞原則的資產) 和 **IContentKey** (**CommonEncryption** 類型的內容金鑰，如需詳細資訊，請參閱：[建立內容金鑰](media-services-dotnet-create-contentkey.md#common_contentkey))。</span><span class="sxs-lookup"><span data-stu-id="832f3-145">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="832f3-146">如需建立 AssetDeliveryPolicy 時可以指定之值的相關資訊，請參閱 [定義 AssetDeliveryPolicy 時使用的類型](#types) 一節。</span><span class="sxs-lookup"><span data-stu-id="832f3-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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
    
            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="832f3-147">Azure 媒體服務也可讓您加入 Widevine 加密。</span><span class="sxs-lookup"><span data-stu-id="832f3-147">Azure Media Services also enables you to add Widevine encryption.</span></span> <span data-ttu-id="832f3-148">下列範例會示範 PlayReady 和 Widevine 如何新增到資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="832f3-148">The following example demonstrates both PlayReady and Widevine being added to the asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get the PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // to append /? KID =< keyId > to the end of the url when creating the manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

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


        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="832f3-149">以 Widevine 加密時，就只能使用 DASH 來傳遞。</span><span class="sxs-lookup"><span data-stu-id="832f3-149">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="832f3-150">請務必在資產傳遞通訊協定中指定 DASH。</span><span class="sxs-lookup"><span data-stu-id="832f3-150">Make sure to specify DASH in the asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="832f3-151">DynamicEnvelopeEncryption 資產傳遞原則</span><span class="sxs-lookup"><span data-stu-id="832f3-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="832f3-152">下列 **CreateAssetDeliveryPolicy** 方法會建立 **AssetDeliveryPolicy**，而後者設定成將動態信封加密 (**DynamicEnvelopeEncryption**) 套用至 Smooth Streaming、HLS 及 DASH 通訊協定 (若您決定不指定某些通訊協定，系統將會封鎖它們進行串流處理)。</span><span class="sxs-lookup"><span data-stu-id="832f3-152">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to Smooth Streaming, HLS, and DASH protocols (if you decide to not specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="832f3-153">此方法會採用兩個參數：**Asset** (您要套用傳遞原則的資產) 和 **IContentKey** (**EnvelopeEncryption** 類型的內容金鑰，如需詳細資訊，請參閱：[建立內容金鑰](media-services-dotnet-create-contentkey.md#envelope_contentkey))。</span><span class="sxs-lookup"><span data-stu-id="832f3-153">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="832f3-154">如需建立 AssetDeliveryPolicy 時可以指定之值的相關資訊，請參閱 [定義 AssetDeliveryPolicy 時使用的類型](#types) 一節。</span><span class="sxs-lookup"><span data-stu-id="832f3-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get the Key Delivery Base Url by removing the Query parameter.  The Dynamic Encryption service will
        //  automatically add the correct key identifier to the url when it generates the Envelope encrypted content
        //  manifest.  Omitting the IV will also cause the Dynamice Encryption service to generate a deterministic
        //  IV for the content automatically.  By using the EnvelopeBaseKeyAcquisitionUrl and omitting the IV, this
        //  allows the AssetDelivery policy to be reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // The following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended to the envelope and
        //   the Initialization Vector (IV) to use for the envelope encryption.
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

        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="832f3-155"><a id="types"></a>定義 AssetDeliveryPolicy 時使用的類型</span><span class="sxs-lookup"><span data-stu-id="832f3-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="832f3-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="832f3-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="832f3-157">下列列舉描述您可以針對資產傳遞通訊協定設定的值。</span><span class="sxs-lookup"><span data-stu-id="832f3-157">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <span data-ttu-id="832f3-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="832f3-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="832f3-159">下列列舉描述您可以針對資產傳遞原則類型設定的值。</span><span class="sxs-lookup"><span data-stu-id="832f3-159">The following enum describes values you can set for the asset delivery policy type.</span></span>  

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

### <span data-ttu-id="832f3-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="832f3-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="832f3-161">下列列舉描述您可用來設定將內容金鑰傳遞給用戶端之方法的值。</span><span class="sxs-lookup"><span data-stu-id="832f3-161">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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

### <span data-ttu-id="832f3-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="832f3-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="832f3-163">下列列舉描述您可以設定的值，以便設定用來取得資產傳遞原則特定設定的金鑰。</span><span class="sxs-lookup"><span data-stu-id="832f3-163">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="832f3-164">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="832f3-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="832f3-165">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="832f3-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

