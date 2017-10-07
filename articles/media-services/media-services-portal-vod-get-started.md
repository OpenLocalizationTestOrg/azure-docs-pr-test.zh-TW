---
title: "aaaGet 入門傳遞 VoD 使用 hello Azure 入口網站 |Microsoft 文件"
description: "本教學課程會引導您實作與使用 hello Azure 入口網站的 Azure 媒體服務 (AMS) 應用程式的基本 Video-on-Demand (VoD) 內容傳遞服務的 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>快速入門將內容傳送隨選使用 hello Azure 入口網站
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

本教學課程會引導您實作與使用 hello Azure 入口網站的 Azure 媒體服務 (AMS) 應用程式的基本 Video-on-Demand (VoD) 內容傳遞服務的 hello 步驟。

## <a name="prerequisites"></a>必要條件
hello 下面是必要的 toocomplete hello 教學課程：

* 一個 Azure 帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
* 媒體服務帳戶。 toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。

這個教學課程包括下列工作的 hello:

1. Azure 串流端點。
2. 上傳視訊檔案。
3. Hello 原始程式檔編碼為一組彈性位元速率 MP4 檔案。
4. 發佈 hello 資產和取得資料流和漸進式下載 Url。  
5. 播放您的內容。

## <a name="start-streaming-endpoints"></a>啟動串流端點 

當使用 Azure Media Services hello 最常見的案例的其中一個會將視訊透過串流處理的彈性位元速率。 Media Services 提供的動態封裝，可讓您 toodeliver 您彈性位元速率編碼的 MP4 內容串流處理媒體服務 (MPEG DASH、 HLS、 Smooth Streaming) 在 just-in-time，支援不需要您 toostore 預先封裝格式每種串流處理格式的版本。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 

toostart hello 串流端點，請執行下列 hello:

1. 在 [hello 登入[Azure 入口網站](https://portal.azure.com/)。
2. 在 [hello 設定視窗中，按一下 [串流端點。 
3. 按一下 hello 預設串流端點。 

    hello 預設串流端點詳細資料] 視窗隨即出現。

4. 按一下 hello 入門圖示。
5. 按一下 hello 儲存按鈕 toosave 您的變更。

## <a name="upload-files"></a>上傳檔案
toostream 使用 Azure Media Services 的視訊，您需要 tooupload hello 來源視訊編碼多個位元，並發行 hello 結果。 本章節涵蓋 hello 第一個步驟。 

1. 在 [hello**設定**視窗中，按一下 [**資產**。
   
    ![上傳檔案](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. 按一下 hello**上傳**] 按鈕。
   
    hello**上載視訊資產**] 視窗隨即出現。
   
   > [!NOTE]
   > 檔案大小不受限。
   > 
   > 
3. 瀏覽您的電腦上的預期 toohello 視訊、 加以選取，並點擊 [確定]。  
   
    hello 上載啟動，而且您可以看見 hello 進度 hello 檔名底下。  

Hello 上傳完成之後，您會看到 hello hello 中所列的新資產**資產**視窗。 

## <a name="encode-assets"></a>為資產編碼

當使用 Azure Media Services hello 最常見的案例之一傳遞彈性位元速率串流 tooyour 用戶端。 Media Services 支援下列彈性位元速率串流技術的 hello: HTTP Live Streaming (HLS)，Smooth Streaming、 MPEG DASH。 tooprepare 視訊彈性位元速率串流，您需要 tooencode 您的來源視訊多位元速率檔案。 您應該使用 hello**媒體編碼器標準**編碼器 tooencode 視訊。  

Media Services 也提供動態封裝，可讓您 toodeliver 中遵循的串流格式 hello 您多位元速率 mp4 集： MPEG DASH、 HLS、 Smooth Streaming，不需要您 toorepackage 到這些資料流的格式。 使用動態封裝，您只需要 toostore 及支付一種儲存格式，以及 Media Services 中的 hello 檔案建置，並提供服務 hello 適當的回應，根據用戶端的要求。

tootake 利用動態封裝，您需要 tooencode 原始程式檔成一組多位元速率 MP4 檔案 （hello 編碼步驟會示範稍後這一節）。

### <a name="toouse-hello-portal-tooencode"></a>toouse hello 入口 tooencode
本章節描述 hello 步驟可讓您 tooencode 媒體編碼器標準內容。

1. 在 [hello**設定**視窗中，選取**資產**。  
2. 在 [hello**資產**視窗中，您想要 tooencode 選取 hello 資產。
3. 按 hello**編碼**] 按鈕。
4. 在 [hello**編碼資產**視窗中選取 hello 「 媒體編碼器標準 」 的處理器，並預先設定。 如需預設值的相關資訊，請參閱[自動產生的位元速率排行榜](media-services-autogen-bitrate-ladder-with-mes.md)和 [MES 的工作預設值](media-services-mes-presets-overview.md)。 如果您打算使用的編碼預設 toocontrol，記住這： 請務必 tooselect hello 預先設定的最適合您輸入的視訊。 比方說，如果您知道輸入的視訊具有 1920 x 1080 像素的解析度，然後您可以使用 hello"H264 多重位元速率 1080p 」 預設。 如果您有低解析度 (640x360) 視訊，則不應該使用 [H264 多重位元速率 1080p] 預設值。
   
   為了方便管理，您必須編輯 hello 名稱 hello 輸出資產，以及 hello hello 作業名稱的選項。
   
   ![為資產編碼](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. 按下 [建立] 。

### <a name="monitor-encoding-job-progress"></a>監視編碼作業進度
toomonitor hello 進度 hello 編碼作業中，按一下**設定**（hello 頁面頂端的 hello），然後選取 [**作業**。

![工作](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>發佈內容
tooprovide 您一個 url，也可以使用的 toostream 或下載您的內容的使用者，您首先需要太 「 發行 」 您的資產建立定位器。 定位器提供存取 toofiles hello 資產中所包含。 媒體服務支援兩種類型的定位器： 

* 資料流 (OnDemandOrigin) 定位器，用於彈性資料流 （例如，toostream MPEG DASH、 HLS 或 Smooth Streaming）。 toocreate 串流定位器資產必須包含.ism 檔案。 
* 漸進式 (SAS) 定位器，用於透過漸進式下載傳遞視訊。

串流 URL 具有下列格式的 hello，您可以使用它 tooplay Smooth Streaming 資產。

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

附加 toobuild 的 HLS 資料流 URL (格式 = m3u8 aapl) toohello URL。

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

附加 toobuild 的 MPEG DASH 串流 URL (格式 = mpd-時間-csf) toohello URL。

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


SAS URL 具有下列格式的 hello。

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> 如果您使用 hello 入口 toocreate 定位器 2015 年 3 月之前，會建立定位器以兩年到期日。  
> 
> 

定位器時，使用上的到期日 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator)或[.NET](http://go.microsoft.com/fwlink/?LinkID=533259)應用程式開發介面。 當您更新的 SAS 定位器的 hello 到期日時，hello URL 將會變更。

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello 入口 toopublish 資產
toouse hello 入口 toopublish 資產，請勿 hello 遵循：

1. 選取 **設定** > **資產**。
2. 選取您想 toopublish hello 資產。
3. 按一下 hello**發行**] 按鈕。
4. 選取 hello 定位器類型。
5. 按 [新增] 。
   
    ![發佈](./media/media-services-portal-vod-get-started/media-services-publish1.png)

hello URL 加入 toohello 清單**發行 Url**。

## <a name="play-content-from-hello-portal"></a>播放內容從 hello 入口網站
hello Azure 入口網站提供內容的播放程式，您可以使用 tootest 視訊。

按一下想要的 hello 視訊，然後按一下 [hello**播放**] 按鈕。

![發佈](./media/media-services-portal-vod-get-started/media-services-play.png)

適用一些考量事項：

* 資料流，toobegin 開始執行 hello**預設**串流端點。
* 請確定已發佈視訊 hello。
* 這**Media player**播放從 hello 預設串流端點。 如果您想 tooplay 從非預設串流端點，按一下 [toocopy hello URL，並使用其他播放器。 例如， [Azure 媒體服務播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。

## <a name="next-steps"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

