---
title: "aaaHow tooperform 即時資料流使用 Azure Media Services toocreate 多位元速率串流以 hello Azure 入口網站 |Microsoft 文件"
description: "此教學課程會逐步引導您完成建立通道的 hello 步驟接收單一位元速率即時串流，並將其編碼使用 hello Azure 入口網站的 toomulti 位元速率資料流。"
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>如何 tooperform 即時資料流使用 Azure Media Services toocreate 多位元速率串流以 hello Azure 入口網站
> [!div class="op_single_selector"]
> * [入口網站](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [REST API](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

本教學課程將引導您完成 hello 步驟建立的**通道**，接收單一位元速率即時串流，並將其編碼 toomulti 位元速率串流。

> [!NOTE]
> 如需詳細的概念性資訊相關的 tooChannels 啟用即時編碼，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。
> 
> 

## <a name="common-live-streaming-scenario"></a>常見即時串流案例
hello 以下是建立通用的即時串流應用程式所需的一般步驟。

> [!NOTE]
> 目前，最大的 hello 建議即時事件的持續時間是 8 小時。 請如果您需要 toorun 通道的時間較長的時間，連絡 amslived microsoft.com。
> 
> 

1. 視訊攝影機 tooa 電腦連線。 啟動及設定內部部署即時編碼器可以輸出的其中一種 hello 下列通訊協定的單一位元速率資料流： RTMP、 Smooth Streaming 或 RTP (MPEG-TS)。 如需詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。
   
    此步驟也可以在您建立通道之後執行。
2. 建立並啟動通道。 
3. 擷取 hello 通道的內嵌 URL。 
   
    hello 內嵌 URL 由 hello 即時編碼器 toosend hello 資料流 toohello 通道。
4. 擷取 hello 通道預覽 URL。 
   
    使用您的通道可正常接收即時資料流 hello 這個 URL tooverify。
5. 建立事件/程式，此程式也會建立資產。 
6. 發行 hello 事件 （會建立 OnDemand 定位器 hello 相關聯的資產）。    
7. 啟動 hello 事件，當您準備好 toostart 串流和封存時。
8. （選擇性） hello 即時編碼器可以信號的 toostart 公告。 hello 公告 hello 輸出資料流中插入。
9. 停止 hello 事件時，您隨時 toostop 串流並封存 hello 事件。
10. 刪除 hello 事件 （並選擇性地刪除 hello 資產）。   

## <a name="in-this-tutorial"></a>本教學課程內容
在本教學課程，hello Azure 入口網站是使用的 tooaccomplish hello 下列工作： 

1. 建立通道也就啟用的 tooperform 即時編碼。
2. 取得在順序 toosupply hello 內嵌 URL 它 toolive 編碼器。 hello 即時編碼器會使用這個 URL tooingest hello 資料流到 hello 通道。
3. 建立事件/程式 (和資產)。
4. 發行 hello 資產，並取得串流 Url。  
5. 播放您的內容。
6. 清除。

## <a name="prerequisites"></a>必要條件
hello 下面是必要的 toocomplete hello 教學課程。

* toocomplete 本教學課程中，您需要 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 
  如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* 媒體服務帳戶。 toocreate Media Services 帳戶，請參閱[建立帳戶](media-services-portal-create-account.md)。
* 網路攝影機以及可以傳送單一位元速率即時串流的編碼器。

## <a name="create-a-channel"></a>建立通道
1. 在 hello [Azure 入口網站](https://portal.azure.com/)選取 Media Services，然後按一下您的 Media Services 帳戶名稱。
2. 選取 [即時串流] 。
3. 選取 [自訂建立] 。 此選項可讓您建立通道，而啟用通道即可進行即時編碼。
   
    ![建立通道](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. 按一下 [設定] 。
   
   1. 選擇 hello**即時編碼**通道類型。 此類型指定您想要啟用通道 toocreate 即時編碼。 表示 hello 連入的單一位元速率串流會傳送 toohello 通道，並編碼為多位元速率串流，使用指定的即時編碼器設定。 如需詳細資訊，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。 按一下 [確定]。
   2. 指定通道的名稱。
   3. 按一下 [確定] 在 hello 囉 」 畫面底部。
5. 選取 hello**內嵌** 索引標籤。
   
   1. 在這個頁面上，您可以選取串流通訊協定。 Hello**即時編碼**通道類型，有效的通訊協定選項為：
      
      * 單一位元速率的分散 MP4 (Smooth Streaming)
      * 單一位元速率 RTMP
      * RTP (MPEG-TS)：透過 RTP 的 MPEG-2 傳輸串流。
        
        如需有關每個通訊協定的詳細說明，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。
        
        您無法變更 hello hello 通道時的通訊協定選項，或其相關聯的事件/程式正在執行。 如果您需要不同的通訊協定，則應該為每個串流通訊協定建立個別的通道。  
   2. 您可以在 hello 套用 IP 限制內嵌。 
      
       您可以定義 hello IP 位址允許 tooingest 視訊 toothis 通道。 允許的 IP 位址可以指定為單一 IP 位址 (例如'10.0.0.1')、使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如'10.0.0.1/22’)，或使用 IP 位址和以點分隔十進位子網路遮罩的 IP 範圍 (例如'10.0.0.1(255.255.252.0)')。
      
       如果未指定 IP 位址，而且沒有任何規則定義，則不允許任何 IP 位址。 tooallow 任何 IP 位址，建立一個規則，並設定 0.0.0.0/0。
6. 在 hello**預覽**索引標籤上，套用 hello preview 上的 IP 限制。
7. 在 hello**編碼**索引標籤上，指定 hello 編碼預設。 
   
    目前，hello 只有系統是的預設您可以選取**預設 720p**。 toospecify 自訂預設值，請開啟 Microsoft 支援票證。 然後，輸入 hello hello 名稱為您建立的預設值。 

> [!NOTE]
> 目前，hello 通道開始可能會佔用 too30 分鐘。 重設通道可能會佔用 too5 分鐘。
> 
> 

一旦您建立 hello 通道時，您可以按一下 hello 通道，然後選取**設定**，您可以在其中檢視通道組態。 

如需詳細資訊，請參閱[使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。

## <a name="get-ingest-urls"></a>取得內嵌 URL
一旦建立 hello 通道之後，您可以取得內嵌您將會提供 toohello 即時編碼器的 Url。 hello 編碼器使用這些 Url tooinput 即時資料流。

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>建立和管理事件
### <a name="overview"></a>概觀
通道是 toocontrol hello 發行和即時串流片段的儲存體可讓您的事件/程式相關聯。 通道會管理事件/程式。 hello 通道和程式的關聯性是內容的非常類似 tootraditional 媒體其中通道具有常數資料流，而程式是內容的該頻道上的已設定領域的 toosome 逾時事件。

您可以指定您想要 tooretain hello 記錄內容 hello 事件設定 hello 的 hello 數**封存時間長度**長度。 這個值可以設定為 5 分鐘 tooa 最多 25 個小時的最小值。 封存時間長度也會規定 hello 最大用戶端可以從 hello 目前即時位置搜尋的時間量。 事件可以透過 hello 指定時間內，執行但落後 hello 時間長度的內容會持續遭到捨棄。 這個屬性的值也會決定資訊清單所能成長的時間長度 hello 用戶端。

每個事件都是與資產相關聯。 您必須建立 OnDemand 定位器 hello toopublish hello 事件相關聯的資產。 擁有這個定位器，可讓您 toobuild 您可以提供 tooyour 用戶端的串流 URL。

一個通道可支援同時執行的事件，因此您可以建立多個封存 hello toothree 註冊相同的傳入資料流。 這可讓您 toopublish 和封存的事件所需的不同部分。 例如，您的商務需求是 tooarchive 6 小時的事件，但是 toobroadcast 最後的 10 分鐘。 tooaccomplish，您需要 toocreate 兩個同時執行事件。 一個事件設定 tooarchive 6 小時的 hello 事件但 hello 程式不會發行。 hello 其他事件的集合 tooarchive 為 10 分鐘並發佈此程式。

您不應該將現有程式重複用於新的事件。 而是針對每個事件建立並啟動新的程式。

當您準備好 toostart 串流和封存時啟動事件/程式。 停止 hello 事件時，您隨時 toostop 串流並封存 hello 事件。 

toodelete 封存內容時，會停止和刪除 hello 事件，然後再刪除 hello 相關聯的資產。 無法刪除資產，如果它由 hello 事件。必須先刪除 hello 事件。 

即使您停止並刪除 hello 事件之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。

若要封存的 tooretain hello 內容，而不是需要它提供給串流，刪除 hello 串流定位器。

### <a name="createstartstop-events"></a>建立/啟動/停止事件
一旦您擁有 hello 資料流流入 hello 通道就可以開始建立資產、 程式和串流定位器串流處理事件的 hello。 這將會封存 hello 資料流，並讓它使用 tooviewers 透過 hello 串流端點。 

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 

有兩種方式 toostart 事件： 

1. 從 hello**通道**頁面上，按**即時事件**tooadd 新的事件。
   
    指定：事件名稱、資產名稱、封存時間範圍和加密選項。
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    如果您保留**立即發行這個即時事件**核取，hello 事件 hello 發行 Url 將會建立。
   
    您可以按**啟動**，當您準備好 toostream hello 事件。
   
    一旦您開始 hello 事件時，您可以按**監看式**toostart 播放 hello 內容。
2. 或者，您可以使用捷徑，並按**Go Live**按鈕 hello**通道**頁面。 這樣會建立預設「資產」、「程式」和「串流定位器」。
   
    hello 事件命名為**預設**而且 hello 封存時間長度會設定 too8 小時。

您可以觀看 hello 已發行的事件從 hello**即時事件**頁面。 

如果您按一下 [停止播放] ，則會停止所有的即時事件。 

## <a name="watch-hello-event"></a>監看式 hello 事件
toowatch hello 事件中，按一下 **監看式**在 hello Azure 入口網站 或 複製 hello 串流 URL，並使用您選擇的播放程式。 

![建立時間](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

實況事件會自動將事件 tooon 要求內容時停止。

## <a name="clean-up"></a>清除
如果您完成資料流的事件，而且想 tooclean hello 資源佈建之前，請依照下列程序的 hello。

* 停止從 hello 編碼器發送 hello 資料流。
* 停止 hello 通道。 一旦停止 hello 通道時，它將不會產生任何費用。 當您需要 toostart 同樣地，它會有 hello 相同內嵌 URL，您不需要 tooreconfigure 您的編碼器。
* 您可以停止串流端點，除非您想為點播串流即時事件的 toocontinue tooprovide hello 封存。 如果 hello 通道處於停止狀態，它將不會產生任何費用。

## <a name="view-archived-content"></a>檢視封存的內容
即使您停止並刪除 hello 事件之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。 無法刪除資產，如果它由事件。必須先刪除 hello 事件。 

您的資產，選取 toomanage**設定**按一下**資產**。

![Assets](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>考量
* 目前，最大的 hello 建議即時事件的持續時間是 8 小時。 請如果您需要 toorun 通道的時間較長的時間，連絡 amslived microsoft.com。
* 請確定將內容串流的端點要從中 toostream hello 處於 hello**執行**狀態。

## <a name="next-step"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

