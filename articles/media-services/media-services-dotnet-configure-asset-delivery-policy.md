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
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>使用 .NET SDK 設定資產傳遞原則
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>概觀
如果您計劃 toodelivery 加密資產，hello 其中一個步驟中 hello 媒體服務內容傳遞工作流程設定資產的傳遞原則。 hello 資產傳遞原則會告知 Media Services 方式如您傳遞的資產 toobe： 成哪一個資料流通訊協定應在您的資產動態封裝 （適用於例如 MPEG DASH、 HLS、 Smooth Streaming 或全部），是否要 toodynamically加密您的資產和方式 （信封或一般加密）。

本主題討論原因以及如何 toocreate 及設定資產的傳遞原則。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 
>
>此外，toobe 無法 toouse 動態封裝和動態加密您的資產必須包含一組彈性位元速率 mp4 或彈性位元速率 Smooth Streaming 檔案。


您可以套用不同的原則 toohello 相同資產。 例如，您可以套用 PlayReady 加密 tooSmooth 資料流與 AES 信封加密 tooMPEG DASH 和 HLS。 傳遞原則中未定義任何通訊協定 （例如，新增只能指定 HLS 作為 hello 通訊協定的單一原則），將無法從資料流。 hello 例外狀況 toothis 是如果您有未完全定義的資產傳遞原則。 然後，將允許 hello 清除所有通訊協定。

如果您想 toodeliver 儲存體加密資產時，您必須設定 hello 資產的傳遞原則。 在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則。 比方說，toodeliver 資產加密使用進階加密標準 (AES) 信封加密金鑰，將 hello 原則類型設定太**DynamicEnvelopeEncryption**。 tooremove 存放裝置加密和資料流 hello 資產中 hello 清除，設定 hello 原則類型太**NoDynamicEncryption**。 顯示如何 tooconfigure 這些原則類型的範例。

取決於您如何設定 hello 資產傳遞原則會是能 toodynamically 封裝、 動態加密和 hello 遵循串流通訊協定資料流： Smooth Streaming、 HLS 和 MPEG DASH 資料流。

hello 下列清單顯示 hello 格式，使用 toostream Smooth、 HLS 及虛線。

Smooth Streaming：

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest

HLS：

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)


## <a name="considerations"></a>考量
* 當資產的 OnDemand (串流) 定位器仍存在時，您無法刪除與該資產關聯的 AssetDeliveryPolicy。 hello 建議是從 hello 資產 tooremove hello 原則之前刪除 hello 原則。
* 未設定資產傳遞原則時，將無法於儲存空間已加密的資產建立串流定位器。  如果 hello 資產不儲存體加密，hello 系統可讓您在 hello 清除未使用的資產傳遞原則中建立定位器和資料流的 hello 資產。
* 您可以有多個單一資產相關聯的資產傳遞原則，但您只能指定其中一種方式 toohandle 給定 AssetDeliveryProtocol。  這表示如果您嘗試 toolink 兩個傳遞指定的原則，因為 hello 系統並不知道哪一個，將會導致錯誤的 hello AssetDeliveryProtocol.SmoothStreaming 通訊協定您希望 tooapply 當用戶端要求 Smooth Streaming。
* 如果您有現有的串流定位器的資產，您無法連結新原則 toohello 資產 （您可以取消連結現有的原則從 hello 資產，或更新與 hello 資產相關聯的傳遞原則）。  第一次有 tooremove hello 串流定位器，調整 hello 原則，然後重新建立 hello 串流定位器。  您可以使用相同的 locatorId，當您重新建立 hello 串流定位器，但是您應該確定因為 hello 原點或下游 CDN 快取內容，將不會造成問題的用戶端 hello。

## <a name="clear-asset-delivery-policy"></a>清除資產傳遞原則

hello 下列**ConfigureClearAssetDeliveryPolicy**方法指定 toonot 套用動態加密和 toodeliver hello 資料流中的 hello 遵循任何通訊協定： MPEG DASH、 HLS 和 Smooth Streaming 通訊協定。 您可能想 tooapply 此原則 tooyour 儲存體加密資產。

建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>DynamicCommonEncryption 資產傳遞原則

hello 下列**CreateAssetDeliveryPolicy**方法會建立 hello **AssetDeliveryPolicy**也就是設定的 tooapply 動態一般加密 (**DynamicCommonEncryption**)tooa smooth streaming （其他通訊協定，將無法從資料流） 通訊協定。 hello 方法會採用兩個參數：**資產**(hello 資產 toowhich 想 tooapply hello 傳遞原則) 和**和 Contentkey** (hello 內容金鑰的 hello **CommonEncryption**類型，如需詳細資訊，請參閱：[建立內容金鑰](media-services-dotnet-create-contentkey.md#common_contentkey))。

建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。

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

Azure Media Services 也可讓您 tooadd Widevine 加密。 hello 下列範例示範 PlayReady 和 Widevine 加入 toohello 資產傳遞原則。

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
> 當 Widevine 使用加密，才會使用虛線無法 toodeliver。 請確定 toospecify 虛線 hello 資產傳遞通訊協定。
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>DynamicEnvelopeEncryption 資產傳遞原則
hello 下列**CreateAssetDeliveryPolicy**方法會建立 hello **AssetDeliveryPolicy**也就是設定的 tooapply 動態信封加密 (**DynamicEnvelopeEncryption**) tooSmooth Streaming、 HLS 及虛線通訊協定 （如果您決定 toonot 指定某些通訊協定，它們將會遭到封鎖而無法串流處理）。 hello 方法會採用兩個參數：**資產**(hello 資產 toowhich 想 tooapply hello 傳遞原則) 和**和 Contentkey** (hello 內容金鑰的 hello **EnvelopeEncryption**類型，如需詳細資訊，請參閱：[建立內容金鑰](media-services-dotnet-create-contentkey.md#envelope_contentkey))。

建立 AssetDeliveryPolicy 時，可以指定哪些值的詳細資訊，請參閱 hello[類型用來定義 AssetDeliveryPolicy](#types) > 一節。   

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


## <a id="types"></a>定義 AssetDeliveryPolicy 時使用的類型

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

hello 下列列舉描述您可以針對 hello 資產傳遞通訊協定設定的值。

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

hello 下列列舉描述您可以設定 hello 資產傳遞原則類型的值。  

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

hello 下列列舉描述您可以使用 hello 內容金鑰 toohello 用戶端 tooconfigure hello 傳遞方法的值。
    
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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

下列列舉 hello 描述您可以設定資產傳遞原則的 tooconfigure 用金鑰 tooget 特定組態的值。

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

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

