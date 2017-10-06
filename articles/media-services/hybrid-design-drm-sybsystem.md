---
title: "使用 Azure Media Services 的 DRM 子系統 aaaHybrid 設計 |Microsoft 文件"
description: "本主題討論使用 Azure 媒體服務的 DRM 子系統混合式設計。"
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a>DRM 子系統的混合式設計

本主題討論使用 Azure 媒體服務的 DRM 子系統混合式設計。

## <a name="overview"></a>概觀

Azure Media Services 提供下列三個 DRM 系統 hello 支援：

* PlayReady
* Widevine (模組)
* FairPlay

hello DRM 支援包括 DRM 加密 （動態加密） 和授權傳遞，使用 Azure Media Player 支援所有 3 DRMs 為瀏覽器播放程式 SDK。

DRM/CENC 子系統設計和實作的詳細處理方式，請參閱標題為 hello 文件[存取控制與多重 DRM CENC](media-services-cenc-with-multidrm-access-control.md)。

雖然我們提供三種 DRM 系統的完整支援，有時候客戶必須 toouse 自己基礎結構/子系統加法 tooAzure Media Services toobuild 的混合式 DRM 子系統中的各個部分。

以下是客戶常問的一些問題：

* 「我可以使用自己的 DRM 授權伺服器嗎？」 (在此例中，客戶投資了內嵌商務邏輯的 DRM 授權伺服器叢集。)
* 「我可以只使用 Azure 媒體服務的 DRM 授權傳遞，但 AMS 中不裝載內容嗎？」

## <a name="modularity-of-hello-ams-drm-platform"></a>Hello AMS DRM 平台的模組化

Azure 媒體服務 DRM 是全面雲端視訊平台的一部分，設計富彈性和模組化。 您可以使用 Azure Media Services 與任何 hello 遵循 hello 表 （遵循用於 hello 資料表中的 hello 標記法的說明） 中描述的不同組合。 

|**內容裝載與來源**|**內容加密**|**DRM 授權傳遞**|
|---|---|---|
|AMS|AMS|AMS|
|AMS|AMS|協力廠商|
|AMS|協力廠商|AMS|
|AMS|協力廠商|協力廠商|
|協力廠商|協力廠商|AMS|

### <a name="content-hosting--origin"></a>內容裝載與來源

* AMS：影片資產裝載於 AMS 中，而資料流是透過 AMS 串流端點 (但不一定是動態封裝)。
* 協力廠商：影片是在 AMS 之外的協力廠商資料流平台上裝載和傳遞。

### <a name="content-encryption"></a>內容加密

* AMS：內容加密是由 AMS 動態加密動態/隨選執行。
* 協力廠商：內容加密是使用前置處理工作流程在 AMS 之外執行。

### <a name="drm-license-delivery"></a>DRM 授權傳遞

* AMS：DRM 授權是由 AMS 授權傳遞服務傳遞。
* 協力廠商：DRM 授權是由 AMS 之外的協力廠商 DRM 授權伺服器傳遞。

## <a name="configure-based-on-your-hybrid-scenario"></a>根據混合式案例設定

### <a name="content-key"></a>內容金鑰

透過組態的內容金鑰，您可以控制下列屬性 AMS 動態加密和 AMS 授權傳遞服務的 hello:

* hello 動態 DRM 加密所使用的內容金鑰。
* 由授權傳遞服務傳送 DRM 授權內容 toobe： 權限、 內容金鑰和限制。
* **內容金鑰授權原則限制**的類型：開啟、IP 或權杖限制。
* 如果**語彙基元**類型**使用內容金鑰授權原則限制**，hello**內容金鑰授權原則限制**必須符合才能發出授權。

### <a name="asset-delivery-policy"></a>資產傳遞原則

透過設定資產遞送原則，您可以控制 hello 下列 AMS 動態封裝程式和動態加密的 AMS 串流端點所使用的屬性：

* 串流處理通訊協定和 DRM 加密的組合，例如 CENC (PlayReady 和 Widevine) 下的 DASH、PlayReady 下的 Smooth Streaming、Widevine 或 PlayReady 下的 HLS。
* 每個 hello hello 預設/內嵌授權傳遞 Url 涉及 DRMs。
* 無論 DASH MPD 或 HLS 播放清單的授權取得 URL (LA_URL) 是否分別包含 Widevine 和 FairPlay 的索引鍵識別碼 (KID) 查詢字串。

## <a name="scenarios-and-samples"></a>案例與範例

根據 hello hello 前一節中的說明，下列五個混合式案例的 hello 使用個別**內容金鑰**-**資產傳遞原則**組態的組合 (hellohello 最後一個資料行中所述的範例遵循 hello 資料表）：

|**內容裝載與來源**|**DRM 加密**|**DRM 授權傳遞**|**設定內容金鑰**|**設定資產傳遞原則**|**範例**|
|---|---|---|---|---|---|
|AMS|AMS|AMS|是|是|範例 1|
|AMS|AMS|協力廠商|是|是|範例 2|
|AMS|協力廠商|AMS|是|否|範例 3|
|AMS|協力廠商|外部|否|否|範例 4|
|協力廠商|協力廠商|AMS|是|否|    

在 hello 範例 PlayReady 保護適用於虛線和 smooth streaming。 下列 hello 視訊 Url 是 smooth streaming Url。 tooget hello 對應 DASH Url，只要附加"(格式 = mpd-時間-csf) 」。 您可以使用 hello [azure 媒體測試 player](http://aka.ms/amtest) tootest 瀏覽器中的。 它可讓您 tooconfigure 的串流處理通訊協定 toouse，底下的技術。 Windows 10 的 IE11 和 MS Edge 都透過 EME 支援 PlayReady。 如需詳細資訊，請參閱[hello 詳細測試工具](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/)。

### <a name="sample-1"></a>範例 1

* 來源 (基底) URL：https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest 
* PlayReady LA_URL (DASH & Smooth)：https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 
* Widevine LA_URL (DASH)：https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4 
* FairPlay LA_URL (HLS)：https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8 

### <a name="sample-2"></a>範例 2

* 來源 (基底) URL：http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest 
* PlayReady LA_URL (DASH & Smooth)：http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx 

### <a name="sample-3"></a>範例 3

* 來源 URL：https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest 
* PlayReady LA_URL (DASH & Smooth)：https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 

### <a name="sample-4"></a>範例 4

* 來源 URL：https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest 
* PlayReady LA_URL (DASH & Smooth)：https://willzhan12.cloudapp.net/playready/rightsmanager.asmx 

## <a name="summary"></a>摘要

總而言之，Azure 媒體服務 DRM 元件富有彈性，只要如本主題所述正確設定內容金鑰與資產傳遞原則，就可以在混合式案例中使用它們。

## <a name="next-steps"></a>後續步驟
檢視媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

