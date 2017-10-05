---
title: "使用 Axinom 將 Widevine 授權傳遞到 Azure 媒體服務 | Microsoft Docs"
description: "本文說明如何使用 Azure 媒體服務 (AMS) 來傳遞 AMS 使用 PlayReady 與 Widevine DRM 動態加密的資料流。 PlayReady 授權來自媒體服務 PlayReady 授權伺服器，Widevine 授權由 Axinom 授權伺服器傳遞。"
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
ms.openlocfilehash: 64e8d4a88ea78e0de065e5a2c12dba4885e08bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="using-axinom-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="446bc-104">使用 Axinom 將 Widevine 授權傳遞到 Azure 媒體服務</span><span class="sxs-lookup"><span data-stu-id="446bc-104">Using Axinom to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="446bc-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="446bc-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="446bc-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="446bc-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="446bc-107">Overview</span><span class="sxs-lookup"><span data-stu-id="446bc-107">Overview</span></span>
<span data-ttu-id="446bc-108">Azure 媒體服務 (AMS) 已新增Google Widevine 動態保護 (如需詳細資訊，請參閱 [Mingfei 的部落格](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) )。</span><span class="sxs-lookup"><span data-stu-id="446bc-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="446bc-109">此外，Azure 媒體播放器 (AMP) 也已新增 Widevine 支援 (如需詳細資訊，請參閱 [AMP 文件](http://amp.azure.net/libs/amp/latest/docs/) )。</span><span class="sxs-lookup"><span data-stu-id="446bc-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="446bc-110">談到在配備 MSE 和 EME 的現代瀏覽器上串流處理受到 CENC 與多重原生 DRM (PlayReady 和 Widevine) 保護的 DASH 內容時，這可說是一大成就。</span><span class="sxs-lookup"><span data-stu-id="446bc-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="446bc-111">從媒體服務 .NET SDK 版本 3.5.2 開始，媒體服務讓您可設定 Widevine 授權範本並取得 Widevine 授權。</span><span class="sxs-lookup"><span data-stu-id="446bc-111">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="446bc-112">您也可以使用下列 AMS 合作夥伴來協助您傳遞 Widevine 授權：[Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)、[EZDRM](http://ezdrm.com/)、[castLabs](http://castlabs.com/company/partners/azure/)。</span><span class="sxs-lookup"><span data-stu-id="446bc-112">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="446bc-113">本文說明如何整合和測試受 Axinom 管理的 Widevine 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="446bc-113">This article describes how to integrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="446bc-114">具體而言，其內容包括：</span><span class="sxs-lookup"><span data-stu-id="446bc-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="446bc-115">使用多重 DRM (PlayReady 和 Widevine) 與對應的授權取得 URL，設定動態一般加密；</span><span class="sxs-lookup"><span data-stu-id="446bc-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="446bc-116">產生 JWT 權杖以符合授權伺服器需求；</span><span class="sxs-lookup"><span data-stu-id="446bc-116">Generating a JWT token in order to meet the license server requirements;</span></span>
* <span data-ttu-id="446bc-117">開發可使用 JWT 權杖驗證處理授權取得作業的 Azure 媒體播放器應用程式；</span><span class="sxs-lookup"><span data-stu-id="446bc-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="446bc-118">完整的系統和內容金鑰、金鑰識別碼、金鑰種子、JTW 權杖及其宣告，皆可透過下圖詳盡說明。</span><span class="sxs-lookup"><span data-stu-id="446bc-118">The complete system and the flow of content key, key ID, key seed, JTW token and its claims can be best described by the following diagram.</span></span>

![DASH 和 CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="446bc-120">內容保護</span><span class="sxs-lookup"><span data-stu-id="446bc-120">Content Protection</span></span>
<span data-ttu-id="446bc-121">若要設定動態保護和金鑰傳遞原則，請參閱 Mingfei 的部落格： [如何使用 Azure 媒體服務設定 Widevine 封裝](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)(英文)。</span><span class="sxs-lookup"><span data-stu-id="446bc-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How to configure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="446bc-122">您可以使用多重 DRM 為同時具有下列二者的 DASH 串流設定動態 CENC 保護：</span><span class="sxs-lookup"><span data-stu-id="446bc-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of the following:</span></span>

1. <span data-ttu-id="446bc-123">MS Edge 和 IE11 的 PlayReady 保護，可能有權杖授權限制。</span><span class="sxs-lookup"><span data-stu-id="446bc-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="446bc-124">權杖限制原則必須伴隨著安全權杖服務 (STS) 所發出的權杖，例如 Azure Active Directory；</span><span class="sxs-lookup"><span data-stu-id="446bc-124">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="446bc-125">Chrome 的 Widevine 保護，它可能需要對其他 STS 所發行的權杖進行權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="446bc-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="446bc-126">請參閱＜ [JWT 權杖產生](media-services-axinom-integration.md#jwt-token-generation) ＞一節，了解 Azure Active Directory 為何無法做為 Axinom Widevine 授權伺服器的 STS。</span><span class="sxs-lookup"><span data-stu-id="446bc-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="446bc-127">考量</span><span class="sxs-lookup"><span data-stu-id="446bc-127">Considerations</span></span>
1. <span data-ttu-id="446bc-128">您必須使用 Axinom 指定的金鑰種子 (8888000000000000000000000000000000000000) 和您產生或選取的金鑰識別碼，產生用以設定金鑰傳遞服務的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="446bc-128">You must use the Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID to generate the content key for configuring key delivery service.</span></span> <span data-ttu-id="446bc-129">Axinom 授權伺服器會根據相同的金鑰種子 (同時適用於測試和生產環境)，發行包含內容金鑰的所有授權。</span><span class="sxs-lookup"><span data-stu-id="446bc-129">Axinom license server will issue all licenses containing content keys based on the same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="446bc-130">測試用的 Widevine 授權取得 URL： [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense)。</span><span class="sxs-lookup"><span data-stu-id="446bc-130">The Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="446bc-131">HTTP 與 HTTS 皆可使用。</span><span class="sxs-lookup"><span data-stu-id="446bc-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="446bc-132">準備 Azure 媒體播放器</span><span class="sxs-lookup"><span data-stu-id="446bc-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="446bc-133">AMP 1.4.0 版支援同時使用 PlayReady 和 Widevine DRM 動態封裝的 AMS 內容進行播放。</span><span class="sxs-lookup"><span data-stu-id="446bc-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="446bc-134">如果 Widevine 授權伺服器不需要權杖驗證，則不需要執行任何其他動作即可測試受到 Widevine 保護的 DASH 內容。</span><span class="sxs-lookup"><span data-stu-id="446bc-134">If Widevine license server does not require token authentication, there is nothing additional you need to do to test a DASH content protected by Widevine.</span></span> <span data-ttu-id="446bc-135">例如，AMP 團隊提供簡單的 [範例](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html)，在此您可以看到在 Edge 和 IE11 中搭配 PlayReady 以及在 Chrome 中搭配 Widevine 皆順利運作。</span><span class="sxs-lookup"><span data-stu-id="446bc-135">For an example, the AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="446bc-136">Axinom 提供的 Widevine 授權伺服器需要 JWT 權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="446bc-136">The Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="446bc-137">JWT 權杖必須使用透過 HTTP 標頭 “X-AxDRM-Message” 發出的授權要求來提交。</span><span class="sxs-lookup"><span data-stu-id="446bc-137">The JWT token needs to be submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="446bc-138">為此，您必須在設定來源之前，在裝載 AMP 的網頁中新增下列 Javascript：</span><span class="sxs-lookup"><span data-stu-id="446bc-138">For this purpose, you need to add the following javascript in the web page hosting AMP before setting the source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="446bc-139">AMP 程式碼的其餘部分是標準 AMP API，如 [這裡](http://amp.azure.net/libs/amp/latest/docs/)的 AMP 文件所說明。</span><span class="sxs-lookup"><span data-stu-id="446bc-139">The rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="446bc-140">請注意，上述用來設定自訂授權標頭的 Javascript 是在 AMP 中正式發行長期方法之前所使用的短期方法。</span><span class="sxs-lookup"><span data-stu-id="446bc-140">Note that the above javascript for setting custom authorization header is still a short term approach before the official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="446bc-141">JWT 權杖產生</span><span class="sxs-lookup"><span data-stu-id="446bc-141">JWT Token Generation</span></span>
<span data-ttu-id="446bc-142">測試用的 Axinom Widevine 授權伺服器需要 JWT 權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="446bc-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="446bc-143">此外，JWT 權杖中的其中一個宣告屬於複雜物件類型，而非基本資料類型。</span><span class="sxs-lookup"><span data-stu-id="446bc-143">In addition, one of the claims in the JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="446bc-144">可惜的是，Azure AD 只能發行具有基本類型的 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="446bc-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="446bc-145">同樣地，.NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler 和 JwtPayload) 也只能讓您輸入複雜物件類型做為宣告。</span><span class="sxs-lookup"><span data-stu-id="446bc-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you to input complex object type as claims.</span></span> <span data-ttu-id="446bc-146">不過，這些宣告仍會序列化為字串。</span><span class="sxs-lookup"><span data-stu-id="446bc-146">However, the claims are still serialized as string.</span></span> <span data-ttu-id="446bc-147">因此，這兩者都無法用來產生 Widevine 授權要求的 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="446bc-147">Therefore we cannot use any of the two for generating the JWT token for Widevine license request.</span></span>

<span data-ttu-id="446bc-148">John Sheehan 的 [JWT Nuget 套件](https://www.nuget.org/packages/JWT) 符合這些需求，因此我們將使用此 Nuget 套件。</span><span class="sxs-lookup"><span data-stu-id="446bc-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets the needs so we are going to use this Nuget package.</span></span>

<span data-ttu-id="446bc-149">下列程式碼會產生 JWT 權杖，且具有 Axinom Widevine 授權伺服器進行測試時所需的必要宣告：</span><span class="sxs-lookup"><span data-stu-id="446bc-149">Below is the code for generating JWT token with the needed claims as required by Axinom Widevine license server for testing:</span></span>

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
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string to byte[] Note: Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string to byte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "The binary key cannot have an odd number of digits: {0}", hexString));
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

<span data-ttu-id="446bc-150">Axinom Widevine 授權伺服器</span><span class="sxs-lookup"><span data-stu-id="446bc-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="446bc-151">考量</span><span class="sxs-lookup"><span data-stu-id="446bc-151">Considerations</span></span>
1. <span data-ttu-id="446bc-152">即使 AMS PlayReady 授權傳遞服務會要求驗證權杖之前必須有 “Bearer=”，Axinom Widevine 授權伺服器並不會加以使用。</span><span class="sxs-lookup"><span data-stu-id="446bc-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="446bc-153">Axinom 通訊金鑰會做為簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="446bc-153">The Axinom communication key is used as signing key.</span></span> <span data-ttu-id="446bc-154">請注意，此金鑰是十六進位字串，但在編碼時必須將其視為一系列的位元組，而不是字串。</span><span class="sxs-lookup"><span data-stu-id="446bc-154">Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="446bc-155">這可藉由 ConvertHexStringToByteArray 方法來達成。</span><span class="sxs-lookup"><span data-stu-id="446bc-155">This is achieved by the method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="446bc-156">擷取金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="446bc-156">Retrieving Key ID</span></span>
<span data-ttu-id="446bc-157">您可能已注意到，在產生 JWT 權杖的程式碼中，金鑰識別碼是必要項目。</span><span class="sxs-lookup"><span data-stu-id="446bc-157">You may have noticed that in the code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="446bc-158">由於 JWT 權杖必須在載入 AMP 播放程式之前備妥，因此必須要擷取金鑰識別碼，才能產生 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="446bc-158">Since the JWT token needs to be ready before loading AMP player, key ID needs to be retrieved in order to generate JWT token.</span></span>

<span data-ttu-id="446bc-159">當然，有多種方式可用來取得金鑰識別碼。</span><span class="sxs-lookup"><span data-stu-id="446bc-159">Of course there are multiple ways to get hold of key ID.</span></span> <span data-ttu-id="446bc-160">比方說，有人可能會將金鑰識別碼與內容中繼資料一起儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="446bc-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="446bc-161">或者，您可以從 DASH MPD (媒體顯示說明) 檔案擷取金鑰識別碼。</span><span class="sxs-lookup"><span data-stu-id="446bc-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="446bc-162">以下程式碼適用於後者。</span><span class="sxs-lookup"><span data-stu-id="446bc-162">The code below is for the latter.</span></span>

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

## <a name="summary"></a><span data-ttu-id="446bc-163">摘要</span><span class="sxs-lookup"><span data-stu-id="446bc-163">Summary</span></span>
<span data-ttu-id="446bc-164">透過 Azure 媒體服務內容保護和 Azure 媒體播放器中最新版的 Widevine 支援，我們得以同時使用 AMS 中的 PlayReady 授權服務和 Axinom 的 Widevine 授權伺服器，為下列現代瀏覽器實作 DASH + 多重原生 DRM (PlayReady + Widevine) 的串流：</span><span class="sxs-lookup"><span data-stu-id="446bc-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able to implement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for the following modern browsers:</span></span>

* <span data-ttu-id="446bc-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="446bc-165">Chrome</span></span>
* <span data-ttu-id="446bc-166">Windows 10 上的 Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="446bc-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="446bc-167">Windows 8.1 和 Windows 10 上的 IE 11</span><span class="sxs-lookup"><span data-stu-id="446bc-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="446bc-168">Firefox (桌面) 和 Mac (非 iOS) 上的 Safari 也都可透過 Silverlight 和與 Azure 媒體播放器相同的 URL 受到支援</span><span class="sxs-lookup"><span data-stu-id="446bc-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and the same URL with Azure Media Player</span></span>

<span data-ttu-id="446bc-169">以下是運用 Axinom Widevine 授權伺服器的迷你解決方案所需的參數。</span><span class="sxs-lookup"><span data-stu-id="446bc-169">The following parameters are required in the mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="446bc-170">除了金鑰識別碼以外，Axinom 會根據 Widevine 伺服器安裝來提供其餘參數。</span><span class="sxs-lookup"><span data-stu-id="446bc-170">Except for key ID, the rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="446bc-171">參數</span><span class="sxs-lookup"><span data-stu-id="446bc-171">Parameter</span></span> | <span data-ttu-id="446bc-172">使用方式</span><span class="sxs-lookup"><span data-stu-id="446bc-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="446bc-173">通訊金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="446bc-173">Communication key ID</span></span> |<span data-ttu-id="446bc-174">必須包含在 JWT 權杖中作為宣告 "com_key_id" 的值 (請參閱 [本節](media-services-axinom-integration.md#jwt-token-generation))。</span><span class="sxs-lookup"><span data-stu-id="446bc-174">Must be included as value of the claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="446bc-175">通訊金鑰</span><span class="sxs-lookup"><span data-stu-id="446bc-175">Communication key</span></span> |<span data-ttu-id="446bc-176">必須做為 JWT 權杖的簽署金鑰 (請參閱 [本節](media-services-axinom-integration.md#jwt-token-generation) )。</span><span class="sxs-lookup"><span data-stu-id="446bc-176">Must be used as the signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="446bc-177">金鑰種子</span><span class="sxs-lookup"><span data-stu-id="446bc-177">Key seed</span></span> |<span data-ttu-id="446bc-178">必須用來使用任何指定的內容金鑰識別碼來產生內容金鑰 (請參閱 [本節](media-services-axinom-integration.md#content-protection))。</span><span class="sxs-lookup"><span data-stu-id="446bc-178">Must be used to generate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="446bc-179">Widevine 授權取得 URL</span><span class="sxs-lookup"><span data-stu-id="446bc-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="446bc-180">必須用於設定 DASH 串流資產傳遞原則 (請參閱 [本節](media-services-axinom-integration.md#content-protection))。</span><span class="sxs-lookup"><span data-stu-id="446bc-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="446bc-181">內容金鑰識別碼</span><span class="sxs-lookup"><span data-stu-id="446bc-181">Content Key ID</span></span> |<span data-ttu-id="446bc-182">必須包含其中作為 JWT 權杖之權利訊息宣告值的一部分 (請參閱 [本節](media-services-axinom-integration.md#jwt-token-generation) )。</span><span class="sxs-lookup"><span data-stu-id="446bc-182">Must be included as part of the value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="446bc-183">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="446bc-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="446bc-184">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="446bc-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="446bc-185">通知</span><span class="sxs-lookup"><span data-stu-id="446bc-185">Acknowledgments</span></span>
<span data-ttu-id="446bc-186">我們想要向下列為建立此文件貢獻心力的人員致謝：Kristjan Jõgi of Axinom、Mingfei Yan 及 Amit Rajput。</span><span class="sxs-lookup"><span data-stu-id="446bc-186">We would like to acknowledge the following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

