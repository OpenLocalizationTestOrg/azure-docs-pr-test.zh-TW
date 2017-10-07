---
title: "aaaLive 資料流，與在內部部署編碼器使用 hello Azure 入口網站 |Microsoft 文件"
description: "本教學課程會引導您建立設定為傳遞的傳遞通道的 hello 步驟。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>如何 tooperform 即時資料流與內部部署編碼器使用 hello Azure 入口網站
> [!div class="op_single_selector"]
> * [入口網站](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

本教學課程中引導您使用 Azure 入口網站 toocreate hello 的 hello 步驟**通道**針對傳遞的傳遞設定。 

## <a name="prerequisites"></a>必要條件
hello 下面是必要的 toocomplete hello 教學課程：

* 一個 Azure 帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
* 媒體服務帳戶。 toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。
* 網路攝影機。 例如， [Telestream Wirecast 編碼器](http://www.telestream.net/wirecast/overview.htm)。

強烈建議 tooreview hello 下列文章：

* [Azure 媒體服務 RTMP 支援和即時編碼器](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [使用 Azure 媒體服務之即時串流的概觀](media-services-manage-channels-overview.md)
* [使用會建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>常見即時串流案例
hello 下列步驟說明建立常見即時資料流使用的應用程式所設定的通道傳遞傳遞所涉及的工作。 本教學課程示範如何 toocreate 及管理通過通道和即時事件。

>[!NOTE]
>請確定 hello 串流的端點要從中 toostream 內容處於 hello**執行**狀態。 
    
1. 視訊攝影機 tooa 電腦連線。 啟動並設定內部部署即時編碼器，讓它輸出多位元速率 RTMP 或 Fragmented MP4 串流。 如需詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。
   
    此步驟也可以在您建立通道之後執行。
2. 建立並啟動即時通行通道。
3. 擷取 hello 通道的內嵌 URL。 
   
    hello 內嵌 URL 由 hello 即時編碼器 toosend hello 資料流 toohello 通道。
4. 擷取 hello 通道預覽 URL。 
   
    使用您的通道可正常接收即時資料流 hello 這個 URL tooverify。
5. 建立即時事件/程式。 
   
    當使用 hello Azure 入口網站時，建立即時事件也會建立資產。 

6. 當您準備好 toostart 串流和封存時啟動 hello 事件/程式。
7. （選擇性） hello 即時編碼器可以信號的 toostart 公告。 hello 公告 hello 輸出資料流中插入。
8. 每當您想 toostop 串流並封存 hello 事件時，請停止 hello 事件/程式。
9. 刪除 hello 事件/程式，並選擇性地刪除 hello 資產。     

> [!IMPORTANT]
> 請檢閱[建立多位元速率串流的內部編碼器進行即時資料流處理](media-services-live-streaming-with-onprem-encoders.md)toolearn 概念和考量相關 toolive 內部編碼器和傳遞通道進行資料流處理。
> 
> 

## <a name="tooview-notifications-and-errors"></a>tooview 通知和錯誤
如果您希望 tooview 通知錯誤所產生的 hello Azure 入口網站，請按一下 hello 通知圖示。

![通知](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>建立並啟動即時通行通道和事件
通道是 toocontrol hello 發行和即時串流片段的儲存體可讓您的事件/程式相關聯。 通道會管理事件。 

您可以指定您想要 tooretain hello 記錄內容 hello 程式設定 hello 的 hello 數**封存時間長度**長度。 這個值可以設定為 5 分鐘 tooa 最多 25 個小時的最小值。 封存時間長度也會規定 hello 最大用戶端可以從 hello 目前即時位置搜尋的時間量。 事件可以透過 hello 指定時間內，執行但落後 hello 時間長度的內容會持續遭到捨棄。 這個屬性的值也會決定資訊清單所能成長的時間長度 hello 用戶端。

每個事件都是與資產相關聯。 toopublish hello 事件，您必須建立 OnDemand 定位器 hello 相關聯的資產。 擁有這個定位器，可讓您 toobuild 您可以提供 tooyour 用戶端的串流 URL。

一個通道可支援同時執行的事件，因此您可以建立多個封存 hello toothree 註冊相同的傳入資料流。 這可讓您 toopublish 和封存的事件所需的不同部分。 例如，您的商務需求是 tooarchive 6 小時的程式，但 toobroadcast 最後的 10 分鐘。 tooaccomplish，您需要 toocreate 兩個同時執行的程式。 一個程式設 tooarchive 6 小時的 hello 事件，但 hello 程式不會發行。 hello 其他程式的組 tooarchive 為 10 分鐘並發佈此程式。

您不應該重複使用現有的即時事件。 而是針對每個事件建立並啟動新事件。

啟動 hello 事件，當您準備好 toostart 串流和封存時。 每當您想 toostop 串流並封存 hello 事件時，請停止 hello 程式。 

toodelete 封存內容時，會停止和刪除 hello 事件，然後再刪除 hello 相關聯的資產。 無法刪除資產，如果它由事件。必須先刪除 hello 事件。 

即使您停止並刪除 hello 事件之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。

若要封存的 tooretain hello 內容，而不是需要它提供給串流，刪除 hello 串流定位器。

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse hello 入口 toocreate 通道
此區段會顯示如何 toouse hello**快速建立**選項 toocreate 通過通道。

如需傳遞通道的詳細資訊，請參閱[使用會從建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)。

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 在 hello**設定**視窗中，按一下 **即時資料流**。 
   
    ![開始使用](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    hello**即時資料流** 視窗隨即出現。
3. 按一下**快速建立**toocreate 通過通道以 hello RTMP 內嵌通訊協定。
   
    hello**建立新的通道** 視窗隨即出現。
4. 提供 hello 新通道名稱，然後按一下 **建立**。 
   
    這會建立 hello 通過通道 RTMP 內嵌通訊協定。

## <a name="create-events"></a>建立事件
1. 選取您想要 tooadd 事件通道 toowhich。
2. 按下 [即時事件]  按鈕。

![Event](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>取得內嵌 URL
一旦建立 hello 通道之後，您可以取得內嵌您將會提供 toohello 即時編碼器的 Url。 hello 編碼器使用這些 Url tooinput 即時資料流。

![建立時間](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>監看式 hello 事件
toowatch hello 事件中，按一下 **監看式**在 hello Azure 入口網站 或 複製 hello 串流 URL，並使用您選擇的播放程式。 

![建立時間](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

實況事件時會自動取得轉換的 tooon 要求內容時停止。

## <a name="clean-up"></a>清除
如需傳遞通道的詳細資訊，請參閱[使用會從建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)。

* 所有事件/程式 hello 通道上都已都停止時，才可都停止通道。  一旦停止 hello 通道時，它不會不會產生任何費用。 當您需要 toostart 同樣地，它會有 hello 相同內嵌 URL，您不需要 tooreconfigure 您的編碼器。
* 已刪除 hello 通道上的所有即時事件時，才可以刪除通道。

## <a name="view-archived-content"></a>檢視封存的內容
即使您停止並刪除 hello 事件之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。 無法刪除資產，如果它由事件。必須先刪除 hello 事件。 

您的資產，選取 toomanage**設定**按一下**資產**。

![Assets](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

