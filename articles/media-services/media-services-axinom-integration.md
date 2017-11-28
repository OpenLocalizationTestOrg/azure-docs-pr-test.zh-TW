---
title: "aaaUsing Axinom toodeliver Widevine 授權 tooAzure Media Services |Microsoft 文件"
description: "本文說明如何使用 Azure 媒體服務 (AMS) toodeliver 以 PlayReady 和 Widevine DRMs AMS 動態加密的資料流。 hello PlayReady 授權來自 Media Services PlayReady 授權伺服器，並 Widevine 授權傳遞 Axinom 授權伺服器。"
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="e0201-104">使用 Axinom toodeliver Widevine 授權 tooAzure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="e0201-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0201-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="e0201-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="e0201-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="e0201-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e0201-107">Overview</span><span class="sxs-lookup"><span data-stu-id="e0201-107">Overview</span></span>
<span data-ttu-id="e0201-108">Azure 媒體服務 (AMS) 已新增Google Widevine 動態保護 (如需詳細資訊，請參閱 [Mingfei 的部落格](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) )。</span><span class="sxs-lookup"><span data-stu-id="e0201-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="e0201-109">此外，Azure 媒體播放器 (AMP) 也已新增 Widevine 支援 (如需詳細資訊，請參閱 [AMP 文件](http://amp.azure.net/libs/amp/latest/docs/) )。</span><span class="sxs-lookup"><span data-stu-id="e0201-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="e0201-110">談到在配備 MSE 和 EME 的現代瀏覽器上串流處理受到 CENC 與多重原生 DRM (PlayReady 和 Widevine) 保護的 DASH 內容時，這可說是一大成就。</span><span class="sxs-lookup"><span data-stu-id="e0201-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="e0201-111">從開始 hello Media Services.NET SDK 版本 3.5.2，Media Services 可讓您 tooconfigure Widevine 授權範本，並取得 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="e0201-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="e0201-112">您也可以使用下列 AMS 夥伴 toohelp 傳遞 Widevine 授權 hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)， [EZDRM](http://ezdrm.com/)， [castLabs](http://castlabs.com/company/partners/azure/)。</span><span class="sxs-lookup"><span data-stu-id="e0201-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="e0201-113">本文說明如何 toointegrate 和測試 Widevine 授權 Axinom 受管理伺服器。</span><span class="sxs-lookup"><span data-stu-id="e0201-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="e0201-114">具體而言，其內容包括：</span><span class="sxs-lookup"><span data-stu-id="e0201-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="e0201-115">使用多重 DRM (PlayReady 和 Widevine) 與對應的授權取得 URL，設定動態一般加密；</span><span class="sxs-lookup"><span data-stu-id="e0201-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="e0201-116">順序 toomeet hello 授權伺服器的需求; 在產生的 JWT 語彙基元</span><span class="sxs-lookup"><span data-stu-id="e0201-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="e0201-117">開發可使用 JWT 權杖驗證處理授權取得作業的 Azure 媒體播放器應用程式；</span><span class="sxs-lookup"><span data-stu-id="e0201-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="e0201-118">hello 完整的系統和 hello 傳送的金鑰、 金鑰識別碼、 金鑰種子 JTW 語彙基元，其宣告可以最 hello 下列圖表所描述的內容。</span><span class="sxs-lookup"><span data-stu-id="e0201-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![DASH 和 CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="e0201-120">內容保護</span><span class="sxs-lookup"><span data-stu-id="e0201-120">Content Protection</span></span>
<span data-ttu-id="e0201-121">如需設定動態保護和金鑰傳遞原則，請參閱 Mingfei 的部落格：[如何透過 Azure Media Services tooconfigure Widevine 封裝](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)。</span><span class="sxs-lookup"><span data-stu-id="e0201-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="e0201-122">您可以使用多重 DRM 為 DASH 串流處理具有兩個 hello 下列設定動態 CENC 保護：</span><span class="sxs-lookup"><span data-stu-id="e0201-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="e0201-123">MS Edge 和 IE11 的 PlayReady 保護，可能有權杖授權限制。</span><span class="sxs-lookup"><span data-stu-id="e0201-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="e0201-124">hello 權杖限制的原則必須伴隨著權杖核發的權杖服務 (STS)，例如 Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="e0201-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="e0201-125">Chrome 的 Widevine 保護，它可能需要對其他 STS 所發行的權杖進行權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="e0201-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="e0201-126">請參閱＜ [JWT 權杖產生](media-services-axinom-integration.md#jwt-token-generation) ＞一節，了解 Azure Active Directory 為何無法做為 Axinom Widevine 授權伺服器的 STS。</span><span class="sxs-lookup"><span data-stu-id="e0201-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="e0201-127">考量</span><span class="sxs-lookup"><span data-stu-id="e0201-127">Considerations</span></span>
1. <span data-ttu-id="e0201-128">您必須使用的 hello Axinom 指定金鑰種子 (8888000000000000000000000000000000000000)，以及您產生的或選取索引鍵識別碼 toogenerate hello 的內容金鑰設定金鑰傳遞服務。</span><span class="sxs-lookup"><span data-stu-id="e0201-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="e0201-129">Axinom 授權伺服器會發出包含基礎的內容金鑰的所有授權 hello 上相同金鑰種子，僅適用於測試及生產環境。</span><span class="sxs-lookup"><span data-stu-id="e0201-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="e0201-130">hello Widevine 授權取得 URL 進行測試： [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense)。</span><span class="sxs-lookup"><span data-stu-id="e0201-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="e0201-131">HTTP 與 HTTS 皆可使用。</span><span class="sxs-lookup"><span data-stu-id="e0201-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="e0201-132">準備 Azure 媒體播放器</span><span class="sxs-lookup"><span data-stu-id="e0201-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="e0201-133">AMP 1.4.0 版支援同時使用 PlayReady 和 Widevine DRM 動態封裝的 AMS 內容進行播放。</span><span class="sxs-lookup"><span data-stu-id="e0201-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="e0201-134">Widevine 授權伺服器不需要權杖驗證，如果沒有進行任何額外需要 toodo tootest 保護虛線-內容由 Widevine。</span><span class="sxs-lookup"><span data-stu-id="e0201-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="e0201-135">如需範例，hello AMP 團隊提供一個簡單[範例](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html)，其中您可以檢視它在邊緣和 IE11 使用 PlayReady 和 Chrome Widevine 使用中工作。</span><span class="sxs-lookup"><span data-stu-id="e0201-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="e0201-136">提供 Axinom hello Widevine 授權伺服器需要 JWT 權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="e0201-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="e0201-137">hello JWT 權杖需要 toobe 提交透過 HTTP 標頭 「 X-AxDRM-訊息 」 的授權要求。</span><span class="sxs-lookup"><span data-stu-id="e0201-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="e0201-138">基於此目的，您需要遵循之前設定 hello 來源裝載 AMP hello 網頁中的 javascript tooadd hello:</span><span class="sxs-lookup"><span data-stu-id="e0201-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="e0201-139">hello AMP 程式碼其餘部分是 AMP 文件的標準 AMP API[這裡](http://amp.azure.net/libs/amp/latest/docs/)。</span><span class="sxs-lookup"><span data-stu-id="e0201-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="e0201-140">請注意該 hello javascript 設定自訂的授權標頭仍是 hello 官方長期 AMP 的方法，發行前的短期方法上方。</span><span class="sxs-lookup"><span data-stu-id="e0201-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="e0201-141">JWT 權杖產生</span><span class="sxs-lookup"><span data-stu-id="e0201-141">JWT Token Generation</span></span>
<span data-ttu-id="e0201-142">測試用的 Axinom Widevine 授權伺服器需要 JWT 權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="e0201-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="e0201-143">此外，hello JWT 權杖中的 hello 宣告的其中一個是複雜的物件類型，而不是基本資料類型。</span><span class="sxs-lookup"><span data-stu-id="e0201-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="e0201-144">可惜的是，Azure AD 只能發行具有基本類型的 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="e0201-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="e0201-145">同樣地，.NET Framework 應用程式開發介面 （System.IdentityModel.Tokens.SecurityTokenHandler 和 JwtPayload） 只允許您 tooinput 複雜的物件類型做為宣告。</span><span class="sxs-lookup"><span data-stu-id="e0201-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="e0201-146">不過，hello 宣告仍會序列化為字串。</span><span class="sxs-lookup"><span data-stu-id="e0201-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="e0201-147">因此我們無法用於任何兩個 hello 產生 Widevine 授權要求的 hello JWT 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="e0201-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="e0201-148">John Sheehan [JWT Nuget 封裝](https://www.nuget.org/packages/JWT)符合 hello 需求，因此我們 toouse 此 Nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="e0201-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="e0201-149">以下是產生以 hello JWT 權杖中的 hello 程式碼測試所需視 Axinom Widevine 授權伺服器所需要的宣告：</span><span class="sxs-lookup"><span data-stu-id="e0201-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

<span data-ttu-id="e0201-150">Axinom Widevine 授權伺服器</span><span class="sxs-lookup"><span data-stu-id="e0201-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="e0201-151">考量</span><span class="sxs-lookup"><span data-stu-id="e0201-151">Considerations</span></span>
1. <span data-ttu-id="e0201-152">即使 AMS PlayReady 授權傳遞服務會要求驗證權杖之前必須有 “Bearer=”，Axinom Widevine 授權伺服器並不會加以使用。</span><span class="sxs-lookup"><span data-stu-id="e0201-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="e0201-153">hello Axinom 通訊金鑰做為簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="e0201-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="e0201-154">請注意該 hello 金鑰是十六進位的字串，不過必須將它視為一系列的位元組不是字串編碼時也一樣。</span><span class="sxs-lookup"><span data-stu-id="e0201-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="e0201-155">Hello 方法 ConvertHexStringToByteArray 達到此目的。</span><span class="sxs-lookup"><span data-stu-id="e0201-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="e0201-156">擷取金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="e0201-156">Retrieving Key ID</span></span>
<span data-ttu-id="e0201-157">您可能已注意到在 hello 程式碼來產生 JWT 權杖的金鑰識別碼是必要。</span><span class="sxs-lookup"><span data-stu-id="e0201-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="e0201-158">因為 hello JWT 權杖需要 toobe 準備載入 AMP 播放程式之前，toobe 擷取中的金鑰 ID 必須訂購 toogenerate JWT 權杖中。</span><span class="sxs-lookup"><span data-stu-id="e0201-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="e0201-159">課程有多種方式可以 tooget 保存索引鍵的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e0201-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="e0201-160">比方說，有人可能會將金鑰識別碼與內容中繼資料一起儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e0201-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="e0201-161">或者，您可以從 DASH MPD (媒體顯示說明) 檔案擷取金鑰識別碼。</span><span class="sxs-lookup"><span data-stu-id="e0201-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="e0201-162">下列的 hello 程式碼是後者的 hello。</span><span class="sxs-lookup"><span data-stu-id="e0201-162">hello code below is for hello latter.</span></span>

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a><span data-ttu-id="e0201-163">摘要</span><span class="sxs-lookup"><span data-stu-id="e0201-163">Summary</span></span>
<span data-ttu-id="e0201-164">使用最新的 Azure 媒體服務內容保護和 Azure Media Player 中 Widevine 支援加法，我們能夠就近 tooimplement 串流的虛線 + 多 native DRM （PlayReady + Widevine） 與 AMS 和 Widevine 授權中這兩個 PlayReady 授權服務hello 遵循新式瀏覽器從 Axinom 伺服器：</span><span class="sxs-lookup"><span data-stu-id="e0201-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="e0201-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="e0201-165">Chrome</span></span>
* <span data-ttu-id="e0201-166">Windows 10 上的 Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="e0201-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="e0201-167">Windows 8.1 和 Windows 10 上的 IE 11</span><span class="sxs-lookup"><span data-stu-id="e0201-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="e0201-168">(Desktop) Firefox 和 Safari Mac (不限 iOS) 上的也支援透過 Silverlight 和 hello 相同的 URL，使用 Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="e0201-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="e0201-169">hello 下列參數需要 hello 迷你解決方案運用 Axinom Widevine 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="e0201-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="e0201-170">除了索引鍵識別碼 hello 其餘的參數所提供的 Axinom 根據其 Widevine server 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="e0201-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="e0201-171">參數</span><span class="sxs-lookup"><span data-stu-id="e0201-171">Parameter</span></span> | <span data-ttu-id="e0201-172">使用方式</span><span class="sxs-lookup"><span data-stu-id="e0201-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="e0201-173">通訊金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="e0201-173">Communication key ID</span></span> |<span data-ttu-id="e0201-174">必須是包含為 hello 宣告"com_key_id 「 JWT 權杖中的值 (請參閱[這](media-services-axinom-integration.md#jwt-token-generation)> 一節)。</span><span class="sxs-lookup"><span data-stu-id="e0201-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="e0201-175">通訊金鑰</span><span class="sxs-lookup"><span data-stu-id="e0201-175">Communication key</span></span> |<span data-ttu-id="e0201-176">您必須使用因為 hello 的 JWT 權杖簽署金鑰 (請參閱[這](media-services-axinom-integration.md#jwt-token-generation)> 一節)。</span><span class="sxs-lookup"><span data-stu-id="e0201-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="e0201-177">金鑰種子</span><span class="sxs-lookup"><span data-stu-id="e0201-177">Key seed</span></span> |<span data-ttu-id="e0201-178">必須與任何使用的 toogenerate 內容金鑰指定為內容金鑰識別碼 (請參閱[這](media-services-axinom-integration.md#content-protection)> 一節)。</span><span class="sxs-lookup"><span data-stu-id="e0201-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="e0201-179">Widevine 授權取得 URL</span><span class="sxs-lookup"><span data-stu-id="e0201-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="e0201-180">必須用於設定 DASH 串流資產傳遞原則 (請參閱 [本節](media-services-axinom-integration.md#content-protection))。</span><span class="sxs-lookup"><span data-stu-id="e0201-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="e0201-181">內容金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="e0201-181">Content Key ID</span></span> |<span data-ttu-id="e0201-182">必須是 hello 的 JWT 權杖中的權限訊息宣告值的一部分 (請參閱[這](media-services-axinom-integration.md#jwt-token-generation)> 一節)。</span><span class="sxs-lookup"><span data-stu-id="e0201-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="e0201-183">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e0201-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e0201-184">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e0201-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="e0201-185">通知</span><span class="sxs-lookup"><span data-stu-id="e0201-185">Acknowledgments</span></span>
<span data-ttu-id="e0201-186">我們想要遵循造成建立這份文件的人 tooacknowledge hello: Kristjan Jõgi 的 Axinom、 Mingfei Yan 和 Amit Rajput。</span><span class="sxs-lookup"><span data-stu-id="e0201-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

