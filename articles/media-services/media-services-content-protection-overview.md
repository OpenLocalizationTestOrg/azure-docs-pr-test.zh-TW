---
title: "aaaProtect 您的內容與 Azure Media Services |Microsoft 文件"
description: "此文章簡介如何利用 Media Services 保護內容。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>保護內容概觀
Microsoft Azure Media Services 可讓您 toosecure 離開您的電腦，透過儲存體、 處理和傳遞的 hello 時間從您的媒體。 Media Services 可讓您使用動態加密您的實況和點播內容 toodeliver 進階加密標準 (AES) （使用 128 位元加密金鑰），或任何 hello 主要 DRMs: Microsoft PlayReady、 Google Widevine 和 Apple FairPlay。 Media Services 也提供傳遞 AES 金鑰的服務並 DRM （PlayReady、 Widevine 和 FairPlay） 授權 tooauthorized 用戶端。 

下列映像的 hello 示範 hello AMS 支援的內容保護工作流程。 

![利用 PlayReady 保護](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 

本主題說明[概念與術語](media-services-content-protection-overview.md)相關 toounderstanding AMS 與內容的保護。 hello 主題也包含[連結](media-services-content-protection-overview.md#common-scenarios)tootopics 顯示 tooachieve 內容保護工作的方式。 

## <a name="dynamic-encryption"></a>動態加密
Microsoft Azure Media Services 可讓您的內容動態加密使用 AES 清除金鑰或 DRM 加密 toodeliver: Microsoft PlayReady、 Google Widevine 和 Apple FairPlay。

目前，您可以加密 hello 下列資料流的格式： HLS、 MPEG DASH 和 Smooth Streaming。 您無法加密漸進式下載。

如果想要讓 Media Services tooencrypt 資產，您需要與您的 asset tooassociate 加密金鑰 （「 CommonEncryption 」 或 「 EnvelopeEncryption 」），並也可以設定 hello 金鑰授權原則。

您也需要 tooconfigure hello 資產的傳遞原則。 如果您想 toostream 儲存體加密資產，請確定您想要的 toospecify toodeliver 它藉由設定資產遞送原則。

Media Services 時，播放程式要求串流時，使用指定的 hello 金鑰 toodynamically 加密您的內容使用 AES 清除金鑰或 DRM 加密。 toodecrypt hello 資料流，hello 播放程式會要求 hello 金鑰從 hello 金鑰傳遞服務。 toodecide hello 使用者獲授權 tooget hello 索引鍵，hello 服務會評估您指定 hello 索引鍵的 hello 授權原則。


## <a name="storage-encryption"></a>儲存體加密
使用儲存體加密 tooencrypt 您清除的內容，在本機使用 AES 256 位元加密，然後將它上傳 tooAzure 儲存體的方式予以儲存加密在靜止。 使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。 儲存體加密的 hello 主要使用案例是當您想的 toosecure 強式加密您高品質的輸入的媒體檔案放在磁碟。

在順序 toodeliver 儲存體加密資產，您必須設定 hello 資產的傳遞原則，讓媒體服務知道要如何 toodeliver 您的內容。 在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則 （例如 AES、 一般加密或不加密）。

## <a name="common-encryption-cenc"></a>一般加密 (CENC)
當使用 PlayReady 或/及 Widewine 加密您的內容時會使用一般加密。

## <a name="using-cbcs-aapl-encryption"></a>使用 cbcs-aapl 加密
使用 FairPlay 加密您的內容時會使用 Cbcs-aapl。

## <a name="envelope-encryption"></a>信封加密
如果您想要 tooprotect 您的內容與 AES 128 清除金鑰，請使用此選項。 若要更安全的選項，請選擇其中一個 hello DRMs 本主題中列出。 

## <a name="licenses-and-keys-delivery-service"></a>授權和金鑰傳遞服務
Media Services 提供傳遞 PlayReady、 Widevine (FairPlay） DRM 授權的服務和 AES 清除金鑰 tooauthorized 用戶端。 您可以使用[hello Azure 入口網站](media-services-portal-protect-content.md)，REST API 或 Media Services SDK for.NET tooconfigure 授權和驗證原則的授權和金鑰。

## <a name="token-restriction"></a>權杖限制
hello 內容金鑰授權原則可能會有一或多個授權限制： 開啟或語彙基元限制。 hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。 Media Services 支援 hello 簡易 Web 權杖 (SWT) 格式和 JSON Web Token (JWT) 格式的權杖。 媒體服務不提供安全權杖服務。 您可以建立自訂的 STS，或利用 Microsoft Azure ACS tooissue 語彙基元。 hello STS 必須設定以指定的 hello 簽署權杖的 toocreate hello 權杖限制組態中指定的索引鍵和問題的宣告。 hello Media Services 金鑰傳遞服務會傳回 hello 要求金鑰 （或授權） toohello 用戶端 hello 語彙基元是否有效並 hello 宣告 hello 語彙基元在比對中所設定的 hello 金鑰 （或授權）。

在設定 hello 權杖限制的原則時，您必須指定 hello 主要驗證金鑰、 簽發者和對象的參數。 hello 主要驗證金鑰包含 hello 確認 hello 權杖簽署，而且發行者是 hello 安全權杖服務發行 hello 權杖的金鑰。 hello 對象 （有時稱為 「 範圍 」） 說明的 hello 語彙基元的 hello 意圖或 hello 資源 hello 權杖授與存取權。 hello Media Services 金鑰傳遞服務會驗證這些 hello 權杖中的值符合 hello 範本中的 hello 值。

## <a name="streaming-urls"></a>串流 URL
如果您的資產使用一個以上的 DRM 加密，您應該使用的加密標記 hello 串流 URL: (格式 ='m3u8-aapl' 加密 = 'xxx')。

hello 下列考量適用於：

* 僅可指定零個或一個加密類型。
* 加密類型沒有 toobe hello url 中指定，如果只有一個加密已套用的 toohello 資產。
* 加密類型不區分大小寫。
* 您可以指定下列加密類型的 hello:  
  * **cenc**︰一般加密 (Playready 或 Widevine)
  * **cbcs-aapl**：Fairplay
  * **cbc**：AES 信封加密。

## <a name="common-scenarios"></a>常見案例
hello 下列主題示範如何在儲存體，tooprotect 內容傳遞動態加密進行媒體串流處理，使用 AMS 金鑰/授權傳遞服務

* [以 AES 保護](media-services-protect-with-aes128.md) 
* [以 PlayReady 及/或 Widevine 保護 ](media-services-protect-with-drm.md)
* [串流以 Apple FairPlay 及/或 PlayReady 保護的 HLS 內容](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>其他案例
* [如何 toointegrate Azure PlayReady 授權服務與您自己的加密程式/串流伺服器](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server)。
* [使用 castLabs toodeliver DRM 授權 tooAzure 媒體服務](media-services-castlabs-integration.md)

>[!NOTE]
>目前不支援使用外部 DRM 伺服器 (技術) 並從 AMS 進行串流處理的案例。


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>相關連結
[利用 Azure 媒體服務宣告 PlayReady 是一個服務和 AES 動態加密](http://mingfeiy.com/playready)

[Azure 媒體服務 PlayReady 授權傳遞定價說明](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Toodebug aes 加密 Azure 媒體服務中的資料流的方式](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[JWT 權杖驗證](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[整合 Azure 媒體服務 OWIN MVC 型應用程式與 Azure Active Directory 並根據 JWT 宣告限制內容金鑰傳遞](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)。

[使用 Azure ACS tooissue 語彙基元](http://mingfeiy.com/acs-with-key-services)。

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
