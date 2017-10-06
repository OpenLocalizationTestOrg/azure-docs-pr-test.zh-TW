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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>使用 Axinom toodeliver Widevine 授權 tooAzure 媒體服務
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Overview
Azure 媒體服務 (AMS) 已新增Google Widevine 動態保護 (如需詳細資訊，請參閱 [Mingfei 的部落格](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) )。 此外，Azure 媒體播放器 (AMP) 也已新增 Widevine 支援 (如需詳細資訊，請參閱 [AMP 文件](http://amp.azure.net/libs/amp/latest/docs/) )。 談到在配備 MSE 和 EME 的現代瀏覽器上串流處理受到 CENC 與多重原生 DRM (PlayReady 和 Widevine) 保護的 DASH 內容時，這可說是一大成就。

從開始 hello Media Services.NET SDK 版本 3.5.2，Media Services 可讓您 tooconfigure Widevine 授權範本，並取得 Widevine 授權。 您也可以使用下列 AMS 夥伴 toohelp 傳遞 Widevine 授權 hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)， [EZDRM](http://ezdrm.com/)， [castLabs](http://castlabs.com/company/partners/azure/)。

本文說明如何 toointegrate 和測試 Widevine 授權 Axinom 受管理伺服器。 具體而言，其內容包括：  

* 使用多重 DRM (PlayReady 和 Widevine) 與對應的授權取得 URL，設定動態一般加密；
* 順序 toomeet hello 授權伺服器的需求; 在產生的 JWT 語彙基元
* 開發可使用 JWT 權杖驗證處理授權取得作業的 Azure 媒體播放器應用程式；

hello 完整的系統和 hello 傳送的金鑰、 金鑰識別碼、 金鑰種子 JTW 語彙基元，其宣告可以最 hello 下列圖表所描述的內容。

![DASH 和 CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>內容保護
如需設定動態保護和金鑰傳遞原則，請參閱 Mingfei 的部落格：[如何透過 Azure Media Services tooconfigure Widevine 封裝](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)。

您可以使用多重 DRM 為 DASH 串流處理具有兩個 hello 下列設定動態 CENC 保護：

1. MS Edge 和 IE11 的 PlayReady 保護，可能有權杖授權限制。 hello 權杖限制的原則必須伴隨著權杖核發的權杖服務 (STS)，例如 Azure Active Directory;
2. Chrome 的 Widevine 保護，它可能需要對其他 STS 所發行的權杖進行權杖驗證。 

請參閱＜ [JWT 權杖產生](media-services-axinom-integration.md#jwt-token-generation) ＞一節，了解 Azure Active Directory 為何無法做為 Axinom Widevine 授權伺服器的 STS。

### <a name="considerations"></a>考量
1. 您必須使用的 hello Axinom 指定金鑰種子 (8888000000000000000000000000000000000000)，以及您產生的或選取索引鍵識別碼 toogenerate hello 的內容金鑰設定金鑰傳遞服務。 Axinom 授權伺服器會發出包含基礎的內容金鑰的所有授權 hello 上相同金鑰種子，僅適用於測試及生產環境。
2. hello Widevine 授權取得 URL 進行測試： [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense)。 HTTP 與 HTTS 皆可使用。

## <a name="azure-media-player-preparation"></a>準備 Azure 媒體播放器
AMP 1.4.0 版支援同時使用 PlayReady 和 Widevine DRM 動態封裝的 AMS 內容進行播放。
Widevine 授權伺服器不需要權杖驗證，如果沒有進行任何額外需要 toodo tootest 保護虛線-內容由 Widevine。 如需範例，hello AMP 團隊提供一個簡單[範例](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html)，其中您可以檢視它在邊緣和 IE11 使用 PlayReady 和 Chrome Widevine 使用中工作。
提供 Axinom hello Widevine 授權伺服器需要 JWT 權杖驗證。 hello JWT 權杖需要 toobe 提交透過 HTTP 標頭 「 X-AxDRM-訊息 」 的授權要求。 基於此目的，您需要遵循之前設定 hello 來源裝載 AMP hello 網頁中的 javascript tooadd hello:

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

hello AMP 程式碼其餘部分是 AMP 文件的標準 AMP API[這裡](http://amp.azure.net/libs/amp/latest/docs/)。

請注意該 hello javascript 設定自訂的授權標頭仍是 hello 官方長期 AMP 的方法，發行前的短期方法上方。

## <a name="jwt-token-generation"></a>JWT 權杖產生
測試用的 Axinom Widevine 授權伺服器需要 JWT 權杖驗證。 此外，hello JWT 權杖中的 hello 宣告的其中一個是複雜的物件類型，而不是基本資料類型。

可惜的是，Azure AD 只能發行具有基本類型的 JWT 權杖。 同樣地，.NET Framework 應用程式開發介面 （System.IdentityModel.Tokens.SecurityTokenHandler 和 JwtPayload） 只允許您 tooinput 複雜的物件類型做為宣告。 不過，hello 宣告仍會序列化為字串。 因此我們無法用於任何兩個 hello 產生 Widevine 授權要求的 hello JWT 語彙基元。

John Sheehan [JWT Nuget 封裝](https://www.nuget.org/packages/JWT)符合 hello 需求，因此我們 toouse 此 Nuget 封裝。

以下是產生以 hello JWT 權杖中的 hello 程式碼測試所需視 Axinom Widevine 授權伺服器所需要的宣告：

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

Axinom Widevine 授權伺服器

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>考量
1. 即使 AMS PlayReady 授權傳遞服務會要求驗證權杖之前必須有 “Bearer=”，Axinom Widevine 授權伺服器並不會加以使用。
2. hello Axinom 通訊金鑰做為簽署金鑰。 請注意該 hello 金鑰是十六進位的字串，不過必須將它視為一系列的位元組不是字串編碼時也一樣。 Hello 方法 ConvertHexStringToByteArray 達到此目的。

## <a name="retrieving-key-id"></a>擷取金鑰識別碼
您可能已注意到在 hello 程式碼來產生 JWT 權杖的金鑰識別碼是必要。 因為 hello JWT 權杖需要 toobe 準備載入 AMP 播放程式之前，toobe 擷取中的金鑰 ID 必須訂購 toogenerate JWT 權杖中。

課程有多種方式可以 tooget 保存索引鍵的識別碼。 比方說，有人可能會將金鑰識別碼與內容中繼資料一起儲存在資料庫中。 或者，您可以從 DASH MPD (媒體顯示說明) 檔案擷取金鑰識別碼。 下列的 hello 程式碼是後者的 hello。

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

## <a name="summary"></a>摘要
使用最新的 Azure 媒體服務內容保護和 Azure Media Player 中 Widevine 支援加法，我們能夠就近 tooimplement 串流的虛線 + 多 native DRM （PlayReady + Widevine） 與 AMS 和 Widevine 授權中這兩個 PlayReady 授權服務hello 遵循新式瀏覽器從 Axinom 伺服器：

* Chrome
* Windows 10 上的 Microsoft Edge
* Windows 8.1 和 Windows 10 上的 IE 11
* (Desktop) Firefox 和 Safari Mac (不限 iOS) 上的也支援透過 Silverlight 和 hello 相同的 URL，使用 Azure Media Player

hello 下列參數需要 hello 迷你解決方案運用 Axinom Widevine 授權伺服器。 除了索引鍵識別碼 hello 其餘的參數所提供的 Axinom 根據其 Widevine server 安裝程式。

| 參數 | 使用方式 |
| --- | --- |
| 通訊金鑰識別碼 |必須是包含為 hello 宣告"com_key_id 「 JWT 權杖中的值 (請參閱[這](media-services-axinom-integration.md#jwt-token-generation)> 一節)。 |
| 通訊金鑰 |您必須使用因為 hello 的 JWT 權杖簽署金鑰 (請參閱[這](media-services-axinom-integration.md#jwt-token-generation)> 一節)。 |
| 金鑰種子 |必須與任何使用的 toogenerate 內容金鑰指定為內容金鑰識別碼 (請參閱[這](media-services-axinom-integration.md#content-protection)> 一節)。 |
| Widevine 授權取得 URL |必須用於設定 DASH 串流資產傳遞原則 (請參閱 [本節](media-services-axinom-integration.md#content-protection))。 |
| 內容金鑰識別碼 |必須是 hello 的 JWT 權杖中的權限訊息宣告值的一部分 (請參閱[這](media-services-axinom-integration.md#jwt-token-generation)> 一節)。 |

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>通知
我們想要遵循造成建立這份文件的人 tooacknowledge hello: Kristjan Jõgi 的 Axinom、 Mingfei Yan 和 Amit Rajput。

