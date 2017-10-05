---
title: "使用 Azure 媒體服務傳遞 DRM 授權或 AES 金鑰"
description: "本文將說明如何使用 Azure 媒體服務 (AMS) 來傳遞 PlayReady 和/或 Widevine 授權及 AES 金鑰，但使用您的內部部署伺服器完成其餘部分 (編碼、加密、串流)。"
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
ms.openlocfilehash: 263a381dc72105eea60ad9b39434599ff04a4531
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-services-to-deliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="d8b46-103">使用 Azure 媒體服務傳遞 DRM 授權或 AES 金鑰</span><span class="sxs-lookup"><span data-stu-id="d8b46-103">Use Azure Media Services to deliver DRM licenses or AES keys</span></span>
<span data-ttu-id="d8b46-104">Azure 媒體服務 (AMS) 可讓您內嵌、編碼、新增內容保護，以及串流您的內容 (如需詳細資料，請參閱 [這篇](media-services-protect-with-drm.md) 文章)。</span><span class="sxs-lookup"><span data-stu-id="d8b46-104">Azure Media Services (AMS) enables you to ingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="d8b46-105">不過，有一些客戶只想使用 AMS 來傳遞授權和/或金鑰，並使用他們的內部部署伺服器來進行編碼、加密和串流。</span><span class="sxs-lookup"><span data-stu-id="d8b46-105">However, there are customers who only want to use AMS to deliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="d8b46-106">本文章說明如何使用 AMS 來傳遞 PlayReady 和/或 Widevine 授權，但使用您的內部部署伺服器來完成其餘部分。</span><span class="sxs-lookup"><span data-stu-id="d8b46-106">This article describes how you can use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="d8b46-107">概觀</span><span class="sxs-lookup"><span data-stu-id="d8b46-107">Overview</span></span>
<span data-ttu-id="d8b46-108">媒體服務提供傳遞 PlayReady 和 Widevine DRM 授權及 AES-128 金鑰的服務。</span><span class="sxs-lookup"><span data-stu-id="d8b46-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="d8b46-109">媒體服務也提供 API，可讓您設定您要 DRM 執行階段在使用者播放受 DRM 保護內容時強制執行的權限和限制。</span><span class="sxs-lookup"><span data-stu-id="d8b46-109">Media Services also provides APIs that let you configure the rights and restrictions that you want for the DRM runtime to enforce when a user plays back the DRM protected content.</span></span> <span data-ttu-id="d8b46-110">當使用者要求受保護的內容時，播放器應用程式會向 AMS 授權服務要求授權。</span><span class="sxs-lookup"><span data-stu-id="d8b46-110">When a user requests the protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="d8b46-111">如果播放器已獲授權，則 AMS 授權服務會發出授權給播放器。</span><span class="sxs-lookup"><span data-stu-id="d8b46-111">The AMS license service will issue the license to the player (if it is authorized).</span></span> <span data-ttu-id="d8b46-112">PlayReady 和 Widevine 授權包含解密金鑰，可被用戶端播放器用來解密和串流處理內容。</span><span class="sxs-lookup"><span data-stu-id="d8b46-112">The PlayReady and Widevine licenses contain the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="d8b46-113">媒體服務支援多種方式，來授權給提出授權要求或金鑰要求的使用者。</span><span class="sxs-lookup"><span data-stu-id="d8b46-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="d8b46-114">您可以設定內容金鑰授權原則，且該原則可能會有一個或多個限制：Open 或是 Token 限制。</span><span class="sxs-lookup"><span data-stu-id="d8b46-114">You configure the content key's authorization policy and the policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="d8b46-115">權杖限制原則必須伴隨著安全權杖服務 (STS) 所發出的權杖。</span><span class="sxs-lookup"><span data-stu-id="d8b46-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="d8b46-116">媒體服務支援簡單 Web 權杖 (SWT) 格式和 JSON Web 權杖 (JWT) 格式的權杖。</span><span class="sxs-lookup"><span data-stu-id="d8b46-116">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="d8b46-117">下圖示範使用 AMS 傳遞 PlayReady 和/或 Widevine 授權，但使用您的內部部署伺服器來完成其餘部分所需採取的主要步驟。</span><span class="sxs-lookup"><span data-stu-id="d8b46-117">The following diagram shows the main steps you need to take to use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span>

![利用 PlayReady 保護](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="d8b46-119">下載範例</span><span class="sxs-lookup"><span data-stu-id="d8b46-119">Download sample</span></span>
<span data-ttu-id="d8b46-120">您可以從 [這裡](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses)下載本文所述的範例。</span><span class="sxs-lookup"><span data-stu-id="d8b46-120">You can download the sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d8b46-121">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="d8b46-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d8b46-122">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="d8b46-122">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d8b46-123">將下列項目新增至 app.config 檔案中定義的 **appSettings**：</span><span class="sxs-lookup"><span data-stu-id="d8b46-123">Add the following elements to **appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="d8b46-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="d8b46-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="d8b46-125">.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="d8b46-125">.NET code example</span></span>

<span data-ttu-id="d8b46-126">下列程式碼範例示範如何建立通用內容金鑰，並取得 PlayReady 或 Widevine 授權取得 URL。</span><span class="sxs-lookup"><span data-stu-id="d8b46-126">The following code example shows how to create a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="d8b46-127">您需要從 AMS 取得下列資訊項目，並設定您的內部部署伺服器：**內容金鑰**、**金鑰識別碼**、**授權取得 URL**。</span><span class="sxs-lookup"><span data-stu-id="d8b46-127">You need to get the following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="d8b46-128">一旦設定內部部署伺服器之後，就可以從您的串流伺服器串流處理。</span><span class="sxs-lookup"><span data-stu-id="d8b46-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="d8b46-129">由於加密的串流指向 AMS 授權伺服器，您的播放器將會從 AMS 要求授權。</span><span class="sxs-lookup"><span data-stu-id="d8b46-129">Since the encrypted stream points to AMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="d8b46-130">如果您選擇權杖驗證，AMS 授權伺服器將會驗證您透過 HTTPS 所傳送的權杖，然後 (如果有效) 將授權傳遞回您的播放器。</span><span class="sxs-lookup"><span data-stu-id="d8b46-130">If you choose token authentication, the AMS license server will validate the token you sent through HTTPS and (if valid) will deliver the license back to your player.</span></span> <span data-ttu-id="d8b46-131">(此程式碼範例只示範如何建立通用內容金鑰，並取得 PlayReady 或 Widevine 授權取得 URL。</span><span class="sxs-lookup"><span data-stu-id="d8b46-131">(The code example only shows how to create a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="d8b46-132">如果您想要傳遞 AES-128 金鑰，您必須建立信封內容金鑰，並取得金鑰取得 URL，而 [這篇](media-services-protect-with-aes128.md) 文章將說明做法)。</span><span class="sxs-lookup"><span data-stu-id="d8b46-132">If you want to delivery AES-128 keys, you need to create an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how to do it).</span></span>

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
            // Read values from the App.config file.
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

                // Print out the key ID and Key in base64 string format
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
                // Associate the content key authorization policy with the content key.
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

                // Associate the content key authorization policy with the content key
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
                // The following code configures PlayReady License Template using .NET classes
                // and returns the XML string.

                //The PlayReadyLicenseResponseTemplate class represents the template 
                //for the response sent back to the end user. 
                //It contains a field for a custom data string between the license server 
                //and the application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // The PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // to be returned to the end users. 
                // It contains the data on the content key in the license 
                // and any rights or restrictions to be 
                // enforced by the PlayReady DRM runtime when using the content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether the license is persistent 
                // (saved in persistent storage on the client) 
                // or non-persistent (only held in memory while the player is using the license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use the license or not.  
                // If true, the MinimumSecurityLevel property of the license
                // is set to 150.  If false (the default), 
                // the MinimumSecurityLevel property of the license is set to 2000.
                licenseTemplate.AllowTestDevices = true;

                // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
                // It grants the user the ability to playback the content subject to the zero or more restrictions 
                // configured in the license and on the PlayRight itself (for playback specific policy). 
                // Much of the policy on the PlayRight has to do with output restrictions 
                // which control the types of outputs that the content can be played over and 
                // any restrictions that must be put in place when using a given output.
                // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
                //then the DRM runtime will only allow the video to be displayed over digital outputs 
                //(analog video outputs won’t be allowed to pass the content).

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect the consumer experience. 
                // If the output protections are configured too restrictive, 
                // the content might be unplayable on some clients. 
                // For more information, see the PlayReady Compliance Rules document.

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="d8b46-133">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="d8b46-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8b46-134">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d8b46-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d8b46-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d8b46-135">See also</span></span>
[<span data-ttu-id="d8b46-136">使用 PlayReady 和/或 Widevine 動態 Common Encryption</span><span class="sxs-lookup"><span data-stu-id="d8b46-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="d8b46-137">使用 AES-128 動態加密和金鑰傳遞服務</span><span class="sxs-lookup"><span data-stu-id="d8b46-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="d8b46-138">使用合作夥伴將 Widevine 授權傳遞到 Azure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="d8b46-138">Using partners to deliver Widevine licenses to Azure Media Services</span></span>](media-services-licenses-partner-integration.md)

