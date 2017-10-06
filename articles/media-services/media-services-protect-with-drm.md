---
title: "aaaUsing PlayReady 和/或 Widevine 動態一般加密 |Microsoft 文件"
description: "Microsoft Azure Media Services 可讓您 toodeliver MPEG DASH、 Smooth Streaming 和 Http Live Streaming (HLS) 資料流以 Microsoft PlayReady DRM 保護。 它也可讓您 toodelivery Widevine DRM 使用加密的 DASH。 本主題說明如何 toodynamically 加密以 PlayReady 和 Widevine DRM。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>使用 PlayReady 和/或 Widevine 動態一般加密

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Microsoft Azure Media Services 可讓您 toodeliver MPEG DASH、 Smooth Streaming 和受保護的 HTTP Live Streaming (HLS) 資料流[Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/)。 它也可讓您加密 toodeliver DASH 資料流 Widevine DRM 授權。 PlayReady 和 Widevine 加密 hello 一般加密 (ISO/IEC 23001-7 CENC) 規格。 您可以使用[AMS.NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) （起 hello 版本 3.5.1） 或 REST API tooconfigure 您 AssetDeliveryConfiguration toouse Widevine。

媒體服務提供傳遞 PlayReady 和 Widevine DRM 授權的服務。 Media Services 也提供應用程式開發介面可讓您設定 hello 權限和限制您想要 hello PlayReady 或 Widevine DRM 執行階段 tooenforce 當使用者播放受保護的內容。 當使用者要求受 DRM 保護內容時，hello 播放器應用程式將會從 hello AMS 授權服務要求的授權。 如果已獲得授權，hello AMS 授權服務將會發出授權 toohello 播放程式。 PlayReady 或 Widevine 執照包含可供 hello 的用戶端播放程式 toodecrypt 和資料流 hello 內容的 hello 解密金鑰。

您也可以使用下列 AMS 夥伴 toohelp 傳遞 Widevine 授權 hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)， [EZDRM](http://ezdrm.com/)， [castLabs](http://castlabs.com/company/partners/azure/)。 如需詳細資訊，請參閱整合 [Axinom](media-services-axinom-integration.md) 和 [castLabs](media-services-castlabs-integration.md)。

媒體服務支援多種方式來授權提出金鑰要求的使用者。 hello 內容金鑰授權原則可能會有一或多個授權限制： 開啟或語彙基元限制。 hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。 Media Services 支援語彙基元中 hello[簡單 Web 權杖](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)(SWT) 格式和[JSON Web 權杖](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)(JWT) 格式。 如需詳細資訊，請參閱設定 hello 內容金鑰授權原則。

tootake 利用動態加密，您需要 toohave 包含一組多位元速率 MP4 檔案或多位元速率 Smooth Streaming 來源檔案的資產。 您也需要 tooconfigure hello 傳遞原則 （在本主題稍後所述） 的 hello 資產。 然後，根據 hello hello 串流 URL 中指定的格式，hello 隨選串流伺服器可確保您已選擇 hello 通訊協定傳遞該 hello 資料流。 如此一來，您只需要 toostore 及支付一種儲存格式以及 Media Services 中的 hello 檔案將會建立及傳遞 hello 根據每個要求從用戶端適當 HTTP 回應。

本主題會在應用程式，以便將多個 DRMs，例如 PlayReady 和 Widevine 受保護的媒體運作的有用 toodevelopers。 hello 主題將說明如何 tooconfigure hello 與授權原則的 PlayReady 授權傳遞服務，讓只有獲得授權的用戶端無法接收 PlayReady 或 Widevine 授權。 它也會示範如何使用 PlayReady 或透過虛線 Widevine DRM toouse 動態加密加密。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 

## <a name="download-sample"></a>下載範例
您可以下載從本文中所述的 hello 範例[這裡](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm)。

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>設定動態 Common Encryption 和 DRM 授權傳遞服務

hello 下面是保護您以 PlayReady 使用 hello Media Services 授權傳遞服務，並且使用動態加密的資產時，您會需要 tooperform 的一般步驟。

1. 建立資產，並將檔案上傳到 hello 資產。
2. 編碼 hello 資產包含 hello 檔案 toohello 彈性位元速率 MP4 集。
3. 建立內容金鑰，並將它與 hello 編碼資產產生關聯。 在 Media Services hello 內容金鑰包含 hello 資產的加密金鑰。
4. 設定 hello 內容金鑰授權原則。 hello 內容金鑰授權原則必須由您設定並符合 hello 為了讓 hello 內容金鑰 toobe 傳遞的 toohello 用戶端的用戶端。

    當建立 hello 內容金鑰授權原則，您需要 toospecify hello 下列： 傳遞方法 （PlayReady 或 Widevine），限制 （開啟或權杖），以及定義 hello 金鑰如何傳遞的資訊特定 toohello 金鑰傳遞類型toohello 用戶端 ([PlayReady](media-services-playready-license-template-overview.md)或[Widevine](media-services-widevine-license-template-overview.md)授權範本)。

5. 設定 hello 資產的傳遞原則。 hello 傳遞原則設定包括： 傳送通訊協定 （例如，MPEG DASH、 HLS、 Smooth Streaming 或全部），hello 動態加密 （例如，一般加密）、 PlayReady 或 Widevine 授權取得 URL 類型。

    您可以套用不同的原則 tooeach 通訊協定 hello 上相同的資產。 例如，您可以套用 PlayReady 加密 tooSmooth/DASH 和 AES 信封 tooHLS。 傳遞原則中未定義任何通訊協定 （例如，新增只能指定 HLS 作為 hello 通訊協定的單一原則），將無法從資料流。 hello 例外狀況 toothis 是如果您有未完全定義的資產傳遞原則。 然後，將允許 hello 清除所有通訊協定。

6. 建立 OnDemand 定位器順序 tooget 串流 URL 中。

您可以找到完整的.NET 範例在 hello hello 主題的結尾。

hello 下列影像示範上述的 hello 工作流程。 本文 hello 語彙基元用來進行驗證。

![利用 PlayReady 保護](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

本主題的 hello 其餘提供詳細的說明、 程式碼範例，以及連結 tootopics 可為您示範如何 tooachieve hello 上面所述的工作。

## <a name="current-limitations"></a>目前的限制
如果您加入或更新資產傳遞原則，您必須刪除相關聯的 hello 定位器 （若有的話），並建立新的定位器。

使用 Widevine 搭配 Azure 媒體服務加密時的限制：目前不支援多個內容索引鍵。

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>建立資產，並將檔案上傳到資產 hello
順序 toomanage 中編碼和串流您的視訊，您必須先將內容上傳到 Microsoft Azure Media Services。 上傳之後，您的內容會安全地儲存在 hello 雲端進行進一步處理和串流。

如需詳細資訊，請參閱 [上傳檔案到媒體服務帳戶](media-services-dotnet-upload-files.md)。

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>編碼 hello 資產包含 hello 檔案 toohello 彈性位元速率 MP4 集
使用動態加密您只需要為 toocreate 包含一組多位元速率 MP4 檔案或多位元速率 Smooth Streaming 來源檔案的資產。 然後，根據 hello hello 資訊清單中指定的格式和片段的要求，hello 隨選串流伺服器可確保您已選擇 hello 通訊協定接收 hello 資料流。 如此一來，您只需要 toostore 及支付一種儲存格式和 Media Services 服務中的 hello 檔案將會建立及傳遞 hello 適當的回應，根據用戶端的要求。 如需詳細資訊，請參閱 hello[動態封裝概觀](media-services-dynamic-packaging-overview.md)主題。

如需有關指示 tooencode，請參閱[如何 tooencode 資產使用媒體編碼器標準](media-services-dotnet-encode-with-media-encoder-standard.md)。

## <a id="create_contentkey"></a>建立內容金鑰，並將它與 hello 編碼資產產生關聯
在 Media Services hello 內容金鑰包含您想 tooencrypt 資產的 hello 索引鍵使用。

如需詳細資訊，請參閱 [建立內容金鑰](media-services-dotnet-create-contentkey.md)。

## <a id="configure_key_auth_policy"></a>設定 hello 內容金鑰授權原則
媒體服務支援多種方式來驗證提出金鑰要求的使用者。 hello 內容金鑰授權原則必須由您設定，並且符合 hello 用戶端 （播放器），才能傳遞 toohello 用戶端 hello 金鑰 toobe。 hello 內容金鑰授權原則可能會有一或多個授權限制： 開啟或語彙基元限制。

如需詳細資訊，請參閱 [設定內容金鑰授權原則](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption)。

## <a id="configure_asset_delivery_policy"></a>設定資產傳遞原則
設定 hello 您資產的傳遞原則。 Hello 資產傳遞原則設定的一些事項包括：

* hello DRM 授權取得 URL。
* hello 資產傳遞通訊協定 (例如，MPEG DASH、 HLS、 Smooth Streaming 或全部）。
* hello （在此情況下，一般加密） 的動態加密類型。

如需詳細資訊，請參閱 [設定資產傳遞原則 ](media-services-rest-configure-asset-delivery-policy.md)。

## <a id="create_locator"></a>建立資料流中順序 tooget 串流 URL 定位器 OnDemand
您將需要 tooprovide 您的使用者，以 hello URL Smooth、 DASH 或 HLS 資料流。

> [!NOTE]
> 如果您加入或更新您的資產傳遞原則，您必須刪除現有的定位程式 (如果有的話)，並建立新的定位器。
>
>

如需有關如何 toopublish 資產和建置串流 URL，請參閱指示[建置串流 URL](media-services-deliver-streaming-content.md)。

## <a name="get-a-test-token"></a>取得測試權杖
取得測試權杖根據 hello 用於 hello 金鑰授權原則的權杖限制。

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


您可以使用 hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest 您的資料流。

## <a name="create-and-configure-a-visual-studio-project"></a>建立和設定 Visual Studio 專案

1. 設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。 
2. 新增下列項目太 hello**appSettings** app.config 檔案中所定義：

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>範例

hello 下列範例示範的功能中推出的 Azure Media Services SDK for.Net-版本 3.5.2 （具體而言，可授權範本並從 Azure Media Services 要求 Widevine 授權 hello 能力 toodefine Widevine）。

Hello 本節中所顯示的程式碼來覆寫您 Program.cs 檔案中的 hello 程式碼。

>[!NOTE]
>對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。 您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。 如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。

請確定 tooupdate 變數 toopoint toofolders 輸入的檔案的所在位置。

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
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

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
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
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
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


## <a name="next-step"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[具有多重 DRM 及存取控制的 CENC](media-services-cenc-with-multidrm-access-control.md)

[使用 AMS 設定 Widevine 封裝](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[宣布在 Azure 媒體服務中推出 Google Widevine 授權傳遞服務](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
