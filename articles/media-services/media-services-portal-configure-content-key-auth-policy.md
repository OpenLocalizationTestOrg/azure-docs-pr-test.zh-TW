---
title: "aaaConfigure 內容金鑰授權原則使用 hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 tooconfigure 內容金鑰授權原則。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>設定內容金鑰授權原則
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>概觀
Microsoft Azure Media Services 可讓您 toodeliver MPEG DASH、 Smooth Streaming 和受保護的進階加密標準 (AES) （使用 128 位元加密金鑰） 的 HTTP Live Streaming (HLS) 資料流或[Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS 也可讓您 toodeliver DASH 串流加密使用 Widevine DRM。 PlayReady 和 Widevine 加密 hello 一般加密 (ISO/IEC 23001-7 CENC) 規格。

Media Services 也提供**金鑰/授權傳遞服務**從用戶端可以取得 AES 金鑰或 PlayReady/Widevine 授權 tooplay hello 加密的內容。

本主題說明如何 toouse hello Azure 入口網站 tooconfigure hello 內容金鑰授權原則。 稍後可以使用 hello 金鑰 toodynamically 加密的內容。 請注意，目前您可以加密 hello 下列資料流的格式： HLS、 MPEG DASH 和 Smooth Streaming。 您無法加密漸進式下載。

當播放程式要求設定 toobe 動態加密的資料流時，Media Services 會使用設定的 hello 金鑰 toodynamically 加密使用 AES 或 DRM 加密的內容。 toodecrypt hello 資料流，hello 播放程式會要求 hello 金鑰從 hello 金鑰傳遞服務。 toodecide hello 使用者獲授權 tooget hello 索引鍵，hello 服務會評估您指定 hello 索引鍵的 hello 授權原則。

如果您計劃 toohave 多個內容的索引鍵，或想 toospecify**金鑰/授權傳遞服務**以外 hello Media Services 金鑰傳遞服務，URL 使用 Media Services.NET SDK 或 REST Api。

[使用媒體服務 .NET SDK 設定內容金鑰授權原則](media-services-dotnet-configure-content-key-auth-policy.md)

[使用媒體服務 REST API 設定內容金鑰授權原則](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>適用一些考量事項：
* AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，您的串流端點 toostart hello 中有 toobe**執行**狀態。 
* 您的資產必須包含一組調適性位元速率 MP4 或調適性位元速率 Smooth Streaming 檔案。 如需詳細資訊，請參閱 [為資產編碼](media-services-encode-asset.md)。
* hello 金鑰傳遞服務會在快取 ContentKeyAuthorizationPolicy 及其相關的物件 （原則選項和限制） 15 分鐘。  如果您建立 ContentKeyAuthorizationPolicy toouse 「 Token 」 限制，則加以測試，並指定然後 hello 原則更新太 「 開啟 」 限制，需要大約 15 分鐘的時間之前 hello 原則參數 toohello 「 開放 」 版本的 hello 原則。

## <a name="how-to-configure-hello-key-authorization-policy"></a>如何： 設定 hello 金鑰授權原則
tooconfigure hello 金鑰授權原則，選取 hello**內容保護**頁面。

媒體服務支援多種方式來驗證提出金鑰要求的使用者。 hello 內容金鑰授權原則中可能有**開啟**，**語彙基元**，或**IP**授權限制 (**IP**可以使用設定REST 或.NET SDK）。

### <a name="open-restriction"></a>Open 限制
hello**開啟**限制表示，hello 系統將會傳送 hello 金鑰 tooanyone 人員提出金鑰要求。 這項限制可用於測試用途。

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>權杖限制
toochoose hello 權杖限制原則，請按 hello**語彙基元** 按鈕。

hello**語彙基元**限制的原則必須伴隨著所發出的權杖**Secure Token Service** (STS)。 Media Services 支援語彙基元中 hello**簡單 Web 權杖**([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) 格式和**JSON Web 權杖**(JWT) 格式。 如需資訊，請參閱 [JWT 權杖驗證](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)。

媒體服務不提供 **安全權杖服務**。 您可以建立自訂的 STS，或利用 Microsoft Azure ACS tooissue 語彙基元。 hello STS 必須設定以指定的 hello 簽署權杖的 toocreate hello 權杖限制組態中指定的索引鍵和問題的宣告。 hello Media Services 金鑰傳遞服務會傳回 hello 加密金鑰 toohello 用戶端 hello 語彙基元有效且 hello hello 權杖中的宣告符合為 hello 內容金鑰設定。 如需詳細資訊，請參閱[使用 Azure ACS tooissue 語彙基元](http://mingfeiy.com/acs-with-key-services)。

當設定 hello**語彙基元**限制的原則，您必須設定的值**驗證金鑰**，**簽發者**和**觀眾**。 hello 主要驗證金鑰包含 hello 確認 hello 權杖簽署，而且發行者是 hello 安全權杖服務發行 hello 權杖的金鑰。 hello 對象 （有時稱為 「 範圍 」） 說明的 hello 語彙基元的 hello 意圖或 hello 資源 hello 權杖授與存取權。 hello Media Services 金鑰傳遞服務會驗證這些 hello 權杖中的值符合 hello 範本中的 hello 值。

### <a name="playready"></a>PlayReady
保護內容時**PlayReady**，下列其中一個，您需要的 hello 事情 toospecify 在您的授權原則是定義 hello PlayReady 授權範本的 XML 字串。 根據預設，設定下列原則 hello:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"> <LicenseTemplates> <PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>非持續性</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>允許</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates> </PlayReadyLicenseResponseTemplate>

您可以按一下 hello**匯入原則的 xml**按鈕，並提供符合 toohello 定義 XML 結構描述的不同 XML[這裡](media-services-playready-license-template-overview.md)。

## <a name="next-step"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

