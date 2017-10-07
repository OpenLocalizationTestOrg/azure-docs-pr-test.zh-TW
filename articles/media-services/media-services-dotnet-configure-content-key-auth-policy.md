---
title: "使用 Media Services.NET SDK aaaConfigure 內容金鑰授權原則 |Microsoft 文件"
description: "深入了解如何 tooconfigure 使用 Media Services.NET SDK 的內容金鑰授權原則。"
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a>動態加密：設定內容金鑰授權原則
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>概觀
Microsoft Azure Media Services 可讓您 toodeliver MPEG DASH、 Smooth Streaming 和受保護的進階加密標準 (AES) （使用 128 位元加密金鑰） 的 HTTP Live Streaming (HLS) 資料流或[Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS 也可讓您 toodeliver DASH 串流加密使用 Widevine DRM。 PlayReady 和 Widevine 加密 hello 一般加密 (ISO/IEC 23001-7 CENC) 規格。

Media Services 也提供**金鑰/授權傳遞服務**從用戶端可以取得 AES 金鑰或 PlayReady/Widevine 授權 tooplay hello 加密的內容。

如果想要讓 Media Services tooencrypt 資產，您需要 tooassociate 加密金鑰 (**CommonEncryption**或**EnvelopeEncryption**) 與 hello 資產 (如所述[這裡](media-services-dotnet-create-contentkey.md))此外，也可以設定授權原則 hello 索引鍵 （如本文所述）。

Media Services 時，播放程式要求串流時，使用指定的 hello 金鑰 toodynamically 加密使用 AES 或 DRM 加密的內容。 toodecrypt hello 資料流，hello 播放程式會要求 hello 金鑰從 hello 金鑰傳遞服務。 toodecide hello 使用者獲授權 tooget hello 索引鍵，hello 服務會評估您指定 hello 索引鍵的 hello 授權原則。

媒體服務支援多種方式來驗證提出金鑰要求的使用者。 hello 內容金鑰授權原則可能會有一或多個授權限制：**開啟**或**語彙基元**限制。 hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。 Media Services 支援語彙基元中 hello**簡單 Web 權杖**([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) 格式和**JSON Web 權杖**([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) 格式。

媒體服務不提供安全權杖服務。 您可以建立自訂的 STS，或利用 Microsoft Azure ACS tooissue 語彙基元。 hello STS 必須設定的 toocreate hello 指定金鑰簽署權杖和宣告 （如本文所述），指定在 hello 權杖限制組態中的發行。 hello Media Services 金鑰傳遞服務會傳回 hello 加密金鑰 toohello 用戶端 hello 語彙基元有效且 hello hello 權杖中的宣告符合為 hello 內容金鑰設定。

如需詳細資訊，請參閱

[JWT 權杖驗證](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[整合 Azure 媒體服務 OWIN MVC 型應用程式與 Azure Active Directory 並根據 JWT 宣告限制內容金鑰傳遞](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)。

[使用 Azure ACS tooissue 語彙基元](http://mingfeiy.com/acs-with-key-services)。

### <a name="some-considerations-apply"></a>適用一些考量事項：
* AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，您的串流端點 toostart hello 中有 toobe**執行**狀態。 
* 您的資產必須包含一組調適性位元速率 MP4 或調適性位元速率 Smooth Streaming 檔案。 如需詳細資訊，請參閱 [為資產編碼](media-services-encode-asset.md)。
* 使用 **AssetCreationOptions.StorageEncrypted** 選項，上傳資產並為其編碼。
* 如果您計劃 toohave 需要的多個內容金鑰 hello 相同原則設定，強烈建議 toocreate 單一授權原則和其重複使用於多個內容的索引鍵。
* hello 金鑰傳遞服務會在快取 ContentKeyAuthorizationPolicy 及其相關的物件 （原則選項和限制） 15 分鐘。  如果您建立 ContentKeyAuthorizationPolicy toouse 「 Token 」 限制，則加以測試，並指定然後 hello 原則更新太 「 開啟 」 限制，需要大約 15 分鐘的時間之前 hello 原則參數 toohello 「 開放 」 版本的 hello 原則。
* 如果您加入或更新您的資產傳遞原則，您必須刪除現有的定位程式 (如果有的話)，並建立新的定位器。
* 您目前無法加密漸進式下載。

## <a name="aes-128-dynamic-encryption"></a>AES-128 動態加密
### <a name="open-restriction"></a>Open 限制
開放限制表示 hello 系統將會傳送 hello 金鑰 tooanyone 人員提出金鑰要求。 這項限制可用於測試用途。

hello 下列範例會建立開放授權原則，並將它加入 toohello 內容金鑰。

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a>Token 限制
本章節描述如何 toocreate 內容金鑰授權原則及關聯 hello 內容金鑰。 hello 授權原則說明哪些授權需求必須符合的 toodetermine，如果 hello 使用者是授權的 tooreceive hello 索引鍵 (hello 「 驗證金鑰 」 清單，例如包含 hello 金鑰簽署該 hello 語彙基元)。

tooconfigure hello 權杖限制選項，就需要 toouse XML toodescribe hello 權杖的授權需求。 hello 權杖限制組態 XML 必須符合 toohello 下列 XML 結構描述。

#### <a id="schema"></a>Token 限制結構描述
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

當設定 hello**語彙基元**限制原則，您必須指定 hello 主要 * * 驗證金鑰 * *，**簽發者**和**觀眾**參數。 hello * * 主要驗證金鑰 * * 包含 hello 語彙基元的 hello 金鑰簽署，**簽發者**是 hello 安全權杖服務的問題 hello 語彙基元。 hello**觀眾**(有時稱為**範圍**) 描述 hello 意圖 hello token 或 hello 資源的 hello 權杖授與存取權。 hello Media Services 金鑰傳遞服務會驗證這些 hello 權杖中的值符合 hello 範本中的 hello 值。 

當使用**Media Services SDK for.NET**，您可以使用 hello **TokenRestrictionTemplate**類別 toogenerate hello 限制語彙基元。
hello 下列範例會建立包含權杖限制授權原則。 在此範例中，hello 用戶端必須 toopresent 包含的語彙基元： 簽署金鑰 (VerificationKey)、 權杖簽發者和必要的宣告。

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <a id="test"></a>測試權杖
tooget 測試語彙基元的 hello 用於 hello 金鑰授權原則的權杖限制，請不要遵循 hello。

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a>PlayReady 動態加密
Media Services 可讓您 tooconfigure hello 權限和限制您想要 hello PlayReady DRM 執行階段 tooenforce 當使用者想 tooplay 回受保護的內容。 

當保護使用 PlayReady，其中一項 hello 您需要在您的授權原則 toospecify 是 XML 字串，定義 hello [PlayReady 授權範本](media-services-playready-license-template-overview.md)。 在 Media Services SDK for.NET，hello **PlayReadyLicenseResponseTemplate**和**PlayReadyLicenseTemplate**類別可協助您定義 hello PlayReady 授權範本。

[本主題](media-services-protect-with-drm.md)示範如何 tooencrypt 內容**PlayReady**和**Widevine**。

### <a name="open-restriction"></a>Open 限制
開放限制表示 hello 系統將會傳送 hello 金鑰 tooanyone 人員提出金鑰要求。 這項限制可用於測試用途。

hello 下列範例會建立開放授權原則，並將它加入 toohello 內容金鑰。

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a>Token 限制
tooconfigure hello 權杖限制選項，就需要 toouse XML toodescribe hello 權杖的授權需求。 hello 權杖限制組態 XML 必須符合 toohello XML 結構描述所示[這](#schema)> 一節。

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


測試語彙基元根據 hello 權杖限制用於 hello 金鑰授權原則，請參閱 tooget[這](#test)> 一節。 

## <a id="types"></a>定義 ContentKeyAuthorizationPolicy 時使用的類型
### <a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <a id="TokenType"></a>TokenType
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>後續步驟
既然您已設定內容金鑰授權原則，請移 toohello[如何 tooconfigure 資產傳遞原則](media-services-dotnet-configure-asset-delivery-policy.md)主題。

