---
title: "使用 aaaConfiguring 內容保護原則 hello Azure 入口網站 |Microsoft 文件"
description: "本文示範如何 toouse hello Azure 入口網站 tooconfigure 內容保護原則。 hello 文章也顯示如何為您資產的 tooenable 動態加密。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>設定使用 hello Azure 入口網站的內容保護原則
> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
> 
> 

## <a name="overview"></a>概觀
Microsoft Azure 媒體服務 (AMS) 可讓您 toosecure 離開您的電腦，透過儲存體、 處理和傳遞的 hello 時間從您的媒體。 Media Services 可讓您 toodeliver 您的內容加密以動態方式使用進階加密標準 (AES) （使用 128 位元加密金鑰），使用 PlayReady 和/或 Widevine DRM 和 Apple FairPlay 一般加密 (CENC)。 

AMS 提供服務，以傳遞授權 DRM 和 AES 清除金鑰 tooauthorized 用戶端。 hello Azure 入口網站可讓您其中一個 toocreate**金鑰授權授權原則**所有類型的加密。

本文示範如何 tooconfigure 內容保護原則 hello Azure 入口網站。 hello 文章也顯示如何 tooapply 動態加密 tooyour 資產。


> [!NOTE]
> 如果您使用 hello Azure 傳統入口網站 toocreate 保護原則，hello 原則可能不會出現在 hello [Azure 入口網站](https://portal.azure.com/)。 不過，所有舊的 hello 原則仍然存在。 您可以檢查它們是否使用 Azure Media Services.NET SDK 或 hello hello [Azure 媒體服務-總管](https://github.com/Azure/Azure-Media-Services-Explorer/releases)工具 (toosee hello 原則，以滑鼠右鍵按一下 hello 資產]-> [的顯示資訊 (F4)-> 中，按一下 [內容]-> [索引標籤的索引鍵按一下 hello 索引鍵）。 
> 
> 如果您想 tooencrypt 資產使用新的原則，設定這些文件以 hello Azure 入口網站中，按一下 [儲存]，重新套用動態加密。 
> 
> 

## <a name="start-configuring-content-protection"></a>開始設定內容保護
設定內容的保護，全域 tooyour AMS 帳戶 toouse hello 入口 toostart hello 遵循：

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 選取 [設定] > [內容保護]。

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>金鑰/授權的授權原則
AMS 支援多種方式來驗證提出金鑰或授權要求的使用者。 hello 內容金鑰授權原則必須由您設定，並且符合您的用戶端 hello 金鑰/授權 toobe delived 的 toohello 用戶端的順序。 hello 內容金鑰授權原則可能會有一或多個授權限制：**開啟**或**語彙基元**限制。

hello Azure 入口網站可讓您其中一個 toocreate**金鑰授權授權原則**所有類型的加密。

### <a name="open"></a>開啟
開放限制表示 hello 系統將會傳送 hello 金鑰 tooanyone 人員提出金鑰要求。 這項限制可用於測試用途。 

### <a name="token"></a>權杖
hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。 Media Services 支援 hello 簡易 Web 權杖 (SWT) 格式和 JSON Web Token (JWT) 格式的權杖。 媒體服務不提供安全權杖服務。 您可以建立自訂的 STS，或利用 Microsoft Azure ACS tooissue 語彙基元。 hello STS 必須設定以指定的 hello 簽署權杖的 toocreate hello 權杖限制組態中指定的索引鍵和問題的宣告。 hello Media Services 金鑰傳遞服務會傳回 hello 要求金鑰 （或授權） toohello 用戶端 hello 語彙基元是否有效並 hello 宣告 hello 語彙基元在比對中所設定的 hello 金鑰 （或授權）。

在設定 hello 權杖限制的原則時，您必須指定 hello 主要驗證金鑰、 簽發者和對象的參數。 hello 主要驗證金鑰包含 hello 確認 hello 權杖簽署，而且發行者是 hello 安全權杖服務發行 hello 權杖的金鑰。 hello 對象 （有時稱為 「 範圍 」） 說明的 hello 語彙基元的 hello 意圖或 hello 資源 hello 權杖授與存取權。 hello Media Services 金鑰傳遞服務會驗證這些 hello 權杖中的值符合 hello 範本中的 hello 值。

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>PlayReady 權限範本
如需 hello PlayReady 權限範本的詳細資訊，請參閱[媒體服務 PlayReady 授權範本概觀](media-services-playready-license-template-overview.md)。

### <a name="non-persistent"></a>非持續性
如果您將授權設定為非持續性時，它是只在記憶體中時保留 hello 播放程式會使用 hello 授權。  

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>持續性
如果您將 hello 授權設定為持續性時，將它儲存在永續性儲存體 hello 用戶端上。

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Widevine 權限範本
如需 hello Widevine 權限範本的詳細資訊，請參閱[Widevine 授權範本概觀](media-services-widevine-license-template-overview.md)。

### <a name="basic"></a>基本
當您選取**基本**，hello 範本將會建立使用所有預設值。

### <a name="advanced"></a>進階
如需有關 Widevine 組態進階選項的詳細說明，請參閱 [這個](media-services-widevine-license-template-overview.md) 主題。

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>FairPlay 組態
tooenable FairPlay 加密，您需要 tooprovide hello 應用程式的憑證和應用程式密碼金鑰 （詢問） 透過 hello FairPlay 組態選項。 如需 FairPlay 組態和需求的詳細資訊，請參閱 [這個](media-services-protect-hls-with-fairplay.md) 文章。

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>套用動態加密 tooyour 資產
tootake 利用動態加密，您需要 tooencode 原始程式檔成一組彈性位元速率 MP4 檔案。

### <a name="select-an-asset-that-you-want-tooencrypt"></a>選取您想 tooencrypt 資產
所有的資產，選取 toosee**設定** > **資產**。

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>使用 AES 或 DRM 加密
一旦您在資產上按下 [加密] 後，會看到兩個選擇︰[AES] 或 [DRM]。 

#### <a name="aes"></a>AES
AES 清除金鑰加密將會在所有串流通訊協定上啟用︰Smooth Streaming、HLS 和 MPEG DASH。

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
當您選取 hello DRM 索引標籤時，您會有不同的內容保護原則的選擇 （其中，您必須設定到目前為止） + 串流處理通訊協定的一組。

* **PlayReady 和 Widevine 與 MPEG-DASH** - 會使用 PlayReady 與 Widevine DRM 動態加密您的 MPEG DASH 串流。
* **PlayReady 和 Widevine 與 MPEG-DASH + FairPlay 與 HLS** - 會使用 PlayReady 與 Widevine DRM 動態加密您的 MPEG DASH 串流。 並且會使用 FairPlay 加密您的 HLS 串流。
* **PlayReady 僅與 Smooth Streaming、HLS 和 MPEG-DASH** - 會使用 PlayReady DRM 動態加密 Smooth Streaming、HLS、MPEG-DASH 串流。
* **Widevine 僅與 MPEG-DASH** - 會使用 Widevine DRM 動態加密您的 MPEG-DASH。
* **FairPlay 僅與 HLS** - 會使用 FairPlay 動態加密您的 HLS 串流。

tooenable FairPlay 加密，您需要 tooprovide hello 應用程式的憑證和應用程式密碼金鑰 （詢問） 透過 hello hello 內容保護設定 刀鋒視窗的 FairPlay 組態選項。

![保護內容](./media/media-services-portal-content-protection/media-services-content-protection009.png)

一旦您進行 hello 加密 選項，請按**套用**。

>[!NOTE] 
>如果您計劃 tooplay AES 加密 HLS Safari 中的，請參閱[這篇部落格](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)。

## <a name="next-steps"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

