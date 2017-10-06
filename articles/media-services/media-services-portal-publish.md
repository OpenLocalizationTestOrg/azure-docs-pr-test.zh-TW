---
title: "aaa\"發行內容以 hello Azure 入口網站 |Microsoft 文件 」"
description: "本教學課程會引導您發行您的內容以 hello Azure 入口網站的 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>發佈與 hello Azure 入口網站的內容
> [!div class="op_single_selector"]
> * [入口網站](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>概觀
> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
> 
> 

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

如需詳細資訊，請參閱 [傳遞內容概觀](media-services-deliver-content-overview.md)。

> [!NOTE]
> 如果您使用 hello 入口 toocreate 定位器 2015 年 3 月之前，會建立定位器以兩年的到期日。  
> 
> 

定位器時，使用上的到期日 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator)或[.NET](http://go.microsoft.com/fwlink/?LinkID=533259)應用程式開發介面。 請注意，當您更新的 SAS 定位器的 hello 到期日，hello URL 就會變更。

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello 入口 toopublish 資產
toouse hello 入口 toopublish 資產，請勿 hello 遵循：

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 選取 **設定** > **資產**。
3. 選取您想 toopublish hello 資產。
4. 按一下 hello**發行** 按鈕。
5. 選取 hello 定位器類型。
6. 按 [新增] 。
   
    ![發佈](./media/media-services-portal-vod-get-started/media-services-publish1.png)

hello URL 將會加入 toohello 清單**發行 Url**。

## <a name="play-content-from-hello-portal"></a>播放內容從 hello 入口網站
hello Azure 入口網站提供內容的播放程式，您可以使用 tootest 視訊。

按一下想要的 hello 視訊，然後按一下hello**播放** 按鈕。

![發佈](./media/media-services-portal-vod-get-started/media-services-play.png)

適用一些考量事項：

* 請確定已發佈視訊 hello。
* 這**Media player**播放從 hello 預設串流端點。 如果您想 tooplay 從非預設串流端點，按一下 toocopy hello URL，並使用其他播放器。 例如， [Azure 媒體服務播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。
* 必須執行 hello 串流的端點從中您串流處理。  

## <a name="next-steps"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

