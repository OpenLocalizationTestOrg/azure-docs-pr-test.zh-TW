---
title: "aaaUsing castLabs toodeliver Widevine 授權 tooAzure Media Services |Microsoft 文件"
description: "本文說明如何使用 Azure 媒體服務 (AMS) toodeliver 以 PlayReady 和 Widevine DRMs AMS 動態加密的資料流。 hello PlayReady 授權來自 Media Services PlayReady 授權伺服器，並 Widevine 授權傳遞 castLabs 授權伺服器。"
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>使用 castLabs toodeliver Widevine 授權 tooAzure 媒體服務
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>概觀
本文說明如何使用 Azure 媒體服務 (AMS) toodeliver 以 PlayReady 和 Widevine DRMs AMS 動態加密的資料流。 hello PlayReady 授權來自 Media Services PlayReady 授權伺服器，且傳遞 Widevine 授權**castLabs**授權伺服器。

tooplayback 串流處理受保護的內容由 CENC （PlayReady 和/或 Widevine），您可以使用[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。 如需詳細資訊，請參閱 [AMP 文件](http://amp.azure.net/libs/amp/latest/docs/) 。

下列圖表中的 hello 示範高層級的 Azure 媒體服務和 castLabs 整合架構。

![整合](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>一般系統設定
* 媒體內容儲存在 AMS 中。
* 內容金鑰的金鑰識別碼儲存在 castLabs 與 AMS 中。
* castLabs 與 AMS 皆有內建權杖驗證。 hello 下列各節討論驗證權杖。 
* 當用戶端要求 toostream hello 視訊時，hello 內容動態加密**一般加密**(CENC) 和動態 AMS tooSmooth 來封裝資料流和虛線。 我們也會針對 HLS 串流通訊協定傳遞 PlayReady M2TS 基礎資料流加密。
* PlayReady 授權擷取自 AMS 授權伺服器，Widevine 授權擷取自 castLabs 授權伺服器。 
* Media Player 會自動決定哪些授權 toofetch，根據 hello 用戶端的平台功能。 

## <a name="authentication-token-generation-for-getting-a-license"></a>產生驗證權杖以取得授權
CastLabs 和 AMS 支援 JWT （JSON Web 權杖） 使用的權杖格式 tooauthorize 授權。 

### <a name="jwt-token-in-ams"></a>AMS 中的 JWT 權杖
hello 下表描述 AMS 中的 JWT 語彙基元。 

| 簽發者 | 簽發者字串 hello 選擇安全權杖服務 (STS) |
| --- | --- |
| 對象 |使用 STS 從 hello 的對象字串。 |
| Claims |一組宣告 |
| NotBefore |啟動 hello 語彙基元的有效性 |
| Expires |Hello 語彙基元的結束有效性 |
| SigningCredentials |PlayReady 授權伺服器，授權伺服器與 STS，castLabs 之間共用的 hello 索引鍵可能是對稱或非對稱金鑰。 |

### <a name="jwt-token-in-castlabs"></a>castLabs 中的 JWT 權杖
hello 下表描述 castLabs 中的 JWT 語彙基元。 

| 名稱 | 說明 |
| --- | --- |
| optData |JSON 字串，其中包含您的相關資訊。 |
| crt |含有 hello 資產的相關資訊的 JSON 字串，它的授權資訊與播放權限。 |
| iat |epoch hello 目前日期時間。 |
| jti |有關這個語彙基元 （每個權杖可以只用一次在 hello castLabs 系統） 的唯一識別碼。 |

## <a name="sample-solution-set-up"></a>範例解決方案設定
hello[範例方案](https://github.com/AzureMediaServicesSamples/CastlabsIntegration)包含兩個專案：

* 可以是使用的 tooset DRM 的限制已經內嵌的資產，PlayReady 和 Widevine 主控台應用程式。
* Web 應用程式，用於遞出權杖，可視為「非常簡易」的 STS 版本。

toouse hello 主控台應用程式：

1. 變更 hello app.config toosetup AMS 認證、 castLabs 認證、 STS 組態和共用的金鑰。
2. 將資產上傳到 AMS。
3. 從 hello get hello UUID 上傳資產，並變更 hello Program.cs 檔案中的行 32:
   
      var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();
4. 使用命名 hello castLabs 系統 (hello Program.cs 檔案中的行 44) 中的 hello 資產的 AssetId。
   
   您必須設定為 AssetId **castLabs**; 它必須 toobe 唯一英數字串。
5. 執行 hello 程式。

toouse hello Web 應用程式 (STS):

1. 變更 hello web.config toosetup castlabs 商店識別碼、 hello STS 組態和 hello 共用的金鑰。
2. 部署 tooAzure 網站。
3. 瀏覽 toohello 網站。

## <a name="playing-back-a-video"></a>播放視訊
使用一般加密 （PlayReady 和/或 Widevine） 的 tooplayback 視訊加密，您可以使用 hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。 當執行 hello 主控台應用程式時，會回應 hello 內容金鑰識別碼和 hello 資訊清單的 URL。

1. 開啟新索引標籤，並啟動 STS：http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid]。
2. 跳過[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。
3. 在 hello 串流 URL 中貼上。
4. 按一下 hello**進階選項**核取方塊。
5. 在 hello**保護**下拉式清單中，選取 PlayReady 和/或 Widevine。
6. 貼上您向您的 STS hello 語彙基元文字方塊中的 hello 語彙基元。 
   
   hello castLab 授權伺服器不需要 hello"Bearer ="hello 權杖前面的前置詞。 因此請先移除，再送出 hello 語彙基元。
7. 更新 hello 播放程式。
8. 應該播放視訊的 hello。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

