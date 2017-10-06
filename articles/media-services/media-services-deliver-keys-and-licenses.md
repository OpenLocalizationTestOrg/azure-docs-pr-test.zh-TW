---
title: "aaaUse Azure Media Services toodeliver DRM 授權或 AES 金鑰"
description: "本文說明如何可以使用 Azure 媒體服務 (AMS) toodeliver PlayReady 和/或 Widevine 授權和 AES 金鑰，但不要 hello （編碼、 加密、 資料流處理） 的其餘部分使用內部部署伺服器。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 8546c2c1-430b-4254-a88d-4436a83f9192
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: a81da2973c79e5182ae58aeca7a0f14f3fc7c9ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-services-toodeliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="f1359-103">使用 Azure Media Services toodeliver DRM 授權或 AES 金鑰</span><span class="sxs-lookup"><span data-stu-id="f1359-103">Use Azure Media Services toodeliver DRM licenses or AES keys</span></span>
<span data-ttu-id="f1359-104">Azure 媒體服務 (AMS) 可讓您 tooingest、 編碼、 加入內容的保護和串流處理內容 (請參閱[這](media-services-protect-with-drm.md)文件以取得詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="f1359-104">Azure Media Services (AMS) enables you tooingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="f1359-105">不過，有一些客戶只想 toouse AMS toodeliver 授權及/或金鑰，並進行編碼、 加密和串流處理使用其內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1359-105">However, there are customers who only want toouse AMS toodeliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="f1359-106">本文說明如何 AMS toodeliver PlayReady 和/或 Widevine 授權可以使用，但不要 hello rest 與您在內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1359-106">This article describes how you can use AMS toodeliver PlayReady and/or Widevine licenses but do hello rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="f1359-107">概觀</span><span class="sxs-lookup"><span data-stu-id="f1359-107">Overview</span></span>
<span data-ttu-id="f1359-108">媒體服務提供傳遞 PlayReady 和 Widevine DRM 授權及 AES-128 金鑰的服務。</span><span class="sxs-lookup"><span data-stu-id="f1359-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="f1359-109">Media Services 也提供應用程式開發介面可讓您設定 hello 權限和限制您想要在使用者 hello DRM 執行階段 tooenforce 播放 hello DRM 受保護的內容。</span><span class="sxs-lookup"><span data-stu-id="f1359-109">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello DRM runtime tooenforce when a user plays back hello DRM protected content.</span></span> <span data-ttu-id="f1359-110">當使用者要求 hello 受保護的內容時，hello 播放器應用程式將會從 hello AMS 授權服務要求的授權。</span><span class="sxs-lookup"><span data-stu-id="f1359-110">When a user requests hello protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="f1359-111">hello AMS 授權服務 （如果它已獲授權），會發出 hello 授權 toohello 播放程式。</span><span class="sxs-lookup"><span data-stu-id="f1359-111">hello AMS license service will issue hello license toohello player (if it is authorized).</span></span> <span data-ttu-id="f1359-112">hello PlayReady 和 Widevine 授權包含可供 hello 的用戶端播放程式 toodecrypt 和資料流 hello 內容的 hello 解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f1359-112">hello PlayReady and Widevine licenses contain hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="f1359-113">媒體服務支援多種方式，來授權給提出授權要求或金鑰要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="f1359-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="f1359-114">設定 hello 內容金鑰授權原則，且 hello 原則可能有一或多個的限制： 開啟或語彙基元限制。</span><span class="sxs-lookup"><span data-stu-id="f1359-114">You configure hello content key's authorization policy and hello policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="f1359-115">hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。</span><span class="sxs-lookup"><span data-stu-id="f1359-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="f1359-116">Media Services 支援 hello 簡易 Web 權杖 (SWT) 格式和 JSON Web Token (JWT) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="f1359-116">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="f1359-117">hello 下列圖表顯示 hello 主要步驟需要 tootake toouse AMS toodeliver PlayReady 和/或 Widevine 授權，但沒有與您在內部部署伺服器 hello rest。</span><span class="sxs-lookup"><span data-stu-id="f1359-117">hello following diagram shows hello main steps you need tootake toouse AMS toodeliver PlayReady and/or Widevine licenses but do hello rest with your on-premises servers.</span></span>

![利用 PlayReady 保護](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="f1359-119">下載範例</span><span class="sxs-lookup"><span data-stu-id="f1359-119">Download sample</span></span>
<span data-ttu-id="f1359-120">您可以下載從本文中所述的 hello 範例[這裡](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses)。</span><span class="sxs-lookup"><span data-stu-id="f1359-120">You can download hello sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="f1359-121">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="f1359-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="f1359-122">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="f1359-122">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="f1359-123">新增下列項目太 hello**appSettings** app.config 檔案中所定義：</span><span class="sxs-lookup"><span data-stu-id="f1359-123">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="f1359-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="f1359-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="f1359-125">.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="f1359-125">.NET code example</span></span>

<span data-ttu-id="f1359-126">hello，下列程式碼範例將說明如何 toocreate 通用內容金鑰，並取得 PlayReady 或 Widevine 授權取得 Url。</span><span class="sxs-lookup"><span data-stu-id="f1359-126">hello following code example shows how toocreate a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="f1359-127">您需要 tooget hello 下列資訊從 AMS 並設定內部部署伺服器：**內容金鑰**，**索引鍵識別碼**，**授權取得 URL**。</span><span class="sxs-lookup"><span data-stu-id="f1359-127">You need tooget hello following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="f1359-128">一旦設定內部部署伺服器之後，就可以從您的串流伺服器串流處理。</span><span class="sxs-lookup"><span data-stu-id="f1359-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="f1359-129">Hello 加密的資料流點 tooAMS 授權伺服器，因為您的播放程式會從 AMS 要求的授權。</span><span class="sxs-lookup"><span data-stu-id="f1359-129">Since hello encrypted stream points tooAMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="f1359-130">如果您選擇權杖驗證，hello AMS 授權伺服器會驗證您透過 HTTPS 傳送嗨語彙基元和 （若有效） 會傳送 hello 授權後 tooyour 播放程式。</span><span class="sxs-lookup"><span data-stu-id="f1359-130">If you choose token authentication, hello AMS license server will validate hello token you sent through HTTPS and (if valid) will deliver hello license back tooyour player.</span></span> <span data-ttu-id="f1359-131">（hello 程式碼範例只會顯示如何 toocreate 通用內容索引鍵，並取得 PlayReady 或 Widevine 授權取得 Url。</span><span class="sxs-lookup"><span data-stu-id="f1359-131">(hello code example only shows how toocreate a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="f1359-132">如果您想 toodelivery AES 128 金鑰時，您需要 toocreate 信封內容金鑰，並取得金鑰取得 URL 和[這](media-services-protect-with-aes128.md)文章顯示如何 toodo 它)。</span><span class="sxs-lookup"><span data-stu-id="f1359-132">If you want toodelivery AES-128 keys, you need toocreate an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how toodo it).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DeliverDRMLicenses
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static readonly Uri _sampleIssuer =
                new Uri(ConfigurationManager.AppSettings["Issuer"]);
            private static readonly Uri _sampleAudience =
                new Uri(ConfigurationManager.AppSettings["Audience"]);

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                bool tokenRestriction = true;
                string tokenTemplateString = null;


                IContentKey key = CreateCommonTypeContentKey();

                // Print out hello key ID and Key in base64 string format
                Console.WriteLine("Created key {0} with key value {1} ",
                    key.Id, System.Convert.ToBase64String(key.GetClearKeyValue()));

                Console.WriteLine("PlayReady License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));

                Console.WriteLine("Widevine License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine));

                if (tokenRestriction)
                    tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                else
                    AddOpenAuthorizationPolicy(key);

                Console.WriteLine("Added authorization policy: {0}",
                    key.AuthorizationPolicyId);
                Console.WriteLine();
                Console.ReadLine();
            }

            static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
            {

                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Open",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                            Requirements = null
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.Widevine,
                        restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
            {
                string tokenTemplateString = GenerateTokenRequirements();

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Token Authorization Policy",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                            Requirements = tokenTemplateString,
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.Widevine,
                            restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with token restrictions").
                            Result;

                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

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

                //hello PlayReadyLicenseResponseTemplate class represents hello template 
                //for hello response sent back toohello end user. 
                //It contains a field for a custom data string between hello license server 
                //and hello application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // hello PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // toobe returned toohello end users. 
                // It contains hello data on hello content key in hello license 
                // and any rights or restrictions toobe 
                // enforced by hello PlayReady DRM runtime when using hello content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether hello license is persistent 
                // (saved in persistent storage on hello client) 
                // or non-persistent (only held in memory while hello player is using hello license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use hello license or not.  
                // If true, hello MinimumSecurityLevel property of hello license
                // is set too150.  If false (hello default), 
                // hello MinimumSecurityLevel property of hello license is set too2000.
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

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect hello consumer experience. 
                // If hello output protections are configured too restrictive, 
                // hello content might be unplayable on some clients. 
                // For more information, see hello PlayReady Compliance Rules document.

                // For example:
                //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }


            private static string ConfigureWidevineLicenseTemplate()
            {
                var template = new WidevineMessage
                {
                    allowed_track_types = AllowedTrackTypes.SD_HD,
                    content_key_specs = new[]
                    {
                            new ContentKeySpecs
                            {
                                required_output_protection =
                                    new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                                security_level = 1,
                                track_type = "SD"
                            }
                        },
                    policy_overrides = new
                    {
                        can_play = true,
                        can_persist = true,
                        can_renew = false
                    }
                };

                string configuration = JsonConvert.SerializeObject(template);
                return configuration;
            }


            static public IContentKey CreateCommonTypeContentKey()
            {
                // Create envelope encryption content key
                Guid keyId = Guid.NewGuid();
                byte[] contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="f1359-133">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="f1359-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f1359-134">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="f1359-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f1359-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f1359-135">See also</span></span>
[<span data-ttu-id="f1359-136">使用 PlayReady 和/或 Widevine 動態 Common Encryption</span><span class="sxs-lookup"><span data-stu-id="f1359-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="f1359-137">使用 AES-128 動態加密和金鑰傳遞服務</span><span class="sxs-lookup"><span data-stu-id="f1359-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="f1359-138">使用協力廠商 toodeliver Widevine 授權 tooAzure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="f1359-138">Using partners toodeliver Widevine licenses tooAzure Media Services</span></span>](media-services-licenses-partner-integration.md)

