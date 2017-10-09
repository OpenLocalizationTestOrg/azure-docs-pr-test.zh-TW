---
title: "使用 Azure 媒體服務即時資料流處理的 aaaOverview |Microsoft 文件"
description: "本主題提供了使用 Azure 媒體服務之即時串流的概觀。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>使用 Azure 媒體服務之即時串流的概觀
## <a name="overview"></a>概觀
即時傳遞時透過 Azure Media Services 的事件資料流處理下列元件的 hello 經常會用到：

* 使用的 toobroadcast 事件相機。
* 將來自 tooa 傳送嗨相機 toostreams 訊號轉換的即時視訊編碼即時串流服務。

    (選擇性) 多個即時同步處理的編碼器。 針對特定重大即時事件，需要高可用性和品質使用經驗，建議您 tooemploy 主動-主動備援編碼程式，使用時間同步處理 tooachieve 無縫式容錯移轉且不遺失資料。
* 即時串流服務，可讓您遵循 toodo hello:

  * 使用各種即時串流處理通訊協定 (例如 RTMP 或 Smooth Streaming) 擷取即時內容，
  * (選擇性) 將您的串流編碼成調適性位元速率串流
  * 預覽您的即時串流，
  * 順序 toobe 中的記錄] 和 [存放區 hello 內嵌的內容資料流處理的更新版本 (Video-on-Demand)
  * 傳送嗨內容透過一般串流通訊協定 （例如，MPEG DASH、 Smooth、 HLS） 直接 tooyour 客戶或 tooa 內容傳遞網路 (CDN) 進行進一步的發佈。

**Microsoft Azure Media Services** (AMS) 中提供 hello 能力 tooingest、 編碼、 預覽、 儲存和傳遞即時串流內容。

當傳遞您內容的 toocustomers 您的目標是高品質的視訊 toovarious 裝置在不同的網路狀況下 toodeliver。 tooachieve，使用即時編碼器 tooencode 資料流 tooa 多位元速率 （彈性位元速率） 視訊資料流。  tootake care of 資料流不同的裝置上使用 Media Services[動態封裝](media-services-dynamic-packaging-overview.md)toodynamically 重新封裝您的資料流 toodifferent 通訊協定。 Media Services 支援的下列彈性位元速率串流技術的 hello 傳遞： HTTP Live Streaming (HLS)，Smooth Streaming、 MPEG DASH。

在 Azure Media Services**通道**，**程式**，和**Streamingendpoint**所有 hello 都即時串流功能，包括內嵌、 格式化、 DVR、 控制代碼安全性、 延展性和備援。

在 Azure 媒體服務中， **通道** 代表處理即時串流內容的管線。 通道可以接收即時輸入資料流中 hello 下列方法：

* 在內部部署即時編碼器會傳送多位元速率**RTMP**或**Smooth Streaming** （分散 MP4） 設定為 toohello 通道**傳遞**傳遞。 hello**傳遞**hello 內嵌的串流可以通過時傳遞**通道**s，而不需任何進一步處理。 您可以使用下列輸出多位元速率 Smooth Streaming 的即時編碼器的 hello: MediaExcel、 Ateme、 想像通訊、 Envivio、 Cisco 和元素。 hello 下列即時編碼器都會輸出 RTMP: Adobe Flash 媒體即時編碼器 (FMLE)、 Telestream wirecast 編碼、 Haivision、 Teradek 和 tricaster 轉錄器。  即時編碼器也可以傳送單一位元速率串流 tooa 通道，將不會啟用即時編碼，但是不建議。 要求時，媒體服務會傳送 hello 資料流 toocustomers。

  > [!NOTE]
  > 使用傳遞的方法是 hello toodo 即時資料流，當您在一段很長一段時間，進行多個事件，且您已經有投資在內部部署編碼器最經濟的方式。 請參閱 [價格](https://azure.microsoft.com/pricing/details/media-services/) 詳細資料。
  > 
  > 
* 在內部部署即時編碼器會傳送單一位元速率資料流是啟用的 tooperform toohello 通道即時使用其中一種 hello 下列格式的媒體服務編碼： RTMP 或 Smooth Streaming (分散 MP4)。 也支援 RTP (MPEG-TS)，假設您有專用的連接 toohello Azure 資料中心。 hello 遵循與 RTMP 的即時編碼器輸出已知這個型別的通道 toowork: Telestream wirecast 編碼、 FMLE。 hello 通道，然後執行即時編碼的 hello 連入單一位元速率串流 tooa 多位元速率 （自動調整） 視訊資料流。 要求時，媒體服務會傳送 hello 資料流 toocustomers。

Hello 媒體服務 2.10 從版本開始，當您建立的通道，您可以指定您想要用於您通道 tooreceive hello 輸入資料流和想要的 hello 通道 tooperform 的方式 live 您的資料流的編碼方式。 您有兩個選擇：

* **無**（通過） – 指定這個值，如果您計劃 toouse 在內部部署即時編碼器這樣會輸出多位元速率串流 （傳遞資料流）。 在此情況下，hello 內送資料流傳遞 toohello 輸出而不經過任何編碼。 這是通道 too2.10 先前版本的 hello 行為。  
* **標準**– 選擇此值，如果您計劃 toouse Media Services tooencode 單一位元速率即時串流 toomulti 位元速率資料流。 對於快速相應增加的非頻繁事件來說，這是較為經濟的方法。 請注意即時編碼的計費影響，而您應該記住離開 hello 「 執行 」 狀態中的即時編碼通道會產生計費費用。  建議您即時資料流事件之後立即停止您正在執行通道是完整 tooavoid 額外每小時費用。

## <a name="comparison-of-channel-types"></a>通道類型的比較
下表提供的指引 toocomparing hello 兩個通道型別在 Media Services 支援

| 功能 | 傳遞通道 | 標準通道 |
| --- | --- | --- |
| 單一位元速率輸入會編碼為多個位元 hello 雲端中 |否 |是 |
| 最大解析度、分層數目 |1080p、8 層、60+fps |720p、6 層、30 fps |
| 輸入通訊協定 |RTMP、Smooth Streaming |RTMP、Smooth Streaming 和 RTP |
| 價格 |請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/media-services/)，然後按一下 「 即時視訊 」 索引標籤 |請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/media-services/) |
| 最長執行時間 |全天候 |8 小時 |
| 插入靜態圖像支援 |否 |是 |
| 廣告訊號支援 |否 |是 |
| 傳遞 CEA 608/708 字幕 |是 |是 |
| 從比重中短暫延遲的能力 toorecover 摘要 |是 |否 (經過 6 秒以上且未有任何輸入資料時，通道便會中斷) |
| 支援未統一輸入的 GOP |是 |否 – 輸入必須為固定式 2 秒 GOP |
| 支援變動畫面播放速率輸入 |是 |否 – 輸入必須為固定畫面播放速率。<br/>輕微的差異可以接受，例如：處於高速動態場景的情況。 但編碼器無法卸除 too10 框架數/秒。 |
| 在輸入摘要遺失時自動關閉通道 |否 |經過 12 個小時，如果沒有程式仍在執行 |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>使用可從內部部署編碼器接收多位元速率即時串流的通道 (傳遞)
hello 下列圖表顯示 hello 涉及 hello AMS 平台的主要組件以 hello**傳遞**工作流程。

![即時工作流程](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

如需詳細資訊，請參閱 [使用通道，從內部部署編碼器接收多位元速率即時串流](media-services-live-streaming-with-onprem-encoders.md)。

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>使用通道啟用 tooperform 即時使用 Azure 媒體服務編碼
hello 下列圖表顯示 hello 主要一部分 hello AMS 平台的即時串流工作流程中所涉及其中通道是啟用 tooperform 即時使用媒體服務編碼。

![即時工作流程](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

如需詳細資訊，請參閱[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)。

## <a name="description-of-a-channel-and-its-related-components"></a>通道和其相關元件的說明
### <a name="channel"></a>通道
在媒體服務中， [通道](https://docs.microsoft.com/rest/api/media/operations/channel)負責處理即時資料流內容。 通道所提供的輸入的端點 （內嵌 URL），然後提供 tooa 即時轉碼程式。 hello 通道會從 hello 即時轉碼程式接收即時輸入的串流，並使其可用於透過一或多個 Streamingendpoint 進行串流。 頻道也提供預覽端點 (預覽 URL) toopreview 並驗證您的資料流，然後再進一步處理和傳遞。

您可以取得 hello 內嵌 URL 和 hello 預覽 URL，當您建立 hello 通道。 tooget 這些 Url，hello 通道中並沒有 toobe hello 啟動狀態。 當您準備好 toostart 將資料從即時轉碼程式推送至 hello 通道時，必須先啟動 hello 通道。 一旦 hello 即時轉碼程式開始擷取資料，您可以預覽您的資料流。

每個媒體服務帳戶可以包含多個通道、多個程式和多個 StreamingEndpoints。 根據 hello 頻寬和安全性需求，StreamingEndpoint 服務可以是專用的 tooone 或多個通道。 任何 StreamingEndpoint 可以從任何通道中提取。

### <a name="program"></a>程式
A[程式](https://docs.microsoft.com/rest/api/media/operations/program)可讓您 toocontrol hello 發行和即時串流片段的儲存體。 通道會管理程式。 hello 通道和程式的關聯性是內容的非常類似 tootraditional 媒體其中通道具有常數資料流，而程式是內容的該頻道上的已設定領域的 toosome 逾時事件。
您可以指定您想要 tooretain hello 記錄內容 hello 程式設定 hello 的 hello 數**ArchiveWindowLength**屬性。 這個值可以設定為 5 分鐘 tooa 最多 25 個小時的最小值。

ArchiveWindowLength 也規定 hello 最大用戶端可以從 hello 目前即時位置搜尋的時間量。 程式可以透過 hello 指定時間內，執行但落後 hello 時間長度的內容會持續遭到捨棄。 這個屬性的值也會決定資訊清單所能成長的時間長度 hello 用戶端。

每個程式都是與「資產」相關聯。 您必須建立 hello 定位器 toopublish hello 程式相關聯的資產。 擁有這個定位器，可讓您 toobuild 您可以提供 tooyour 用戶端的串流 URL。

一個通道可支援同時執行的程式，因此您可以建立多個封存 hello toothree 註冊相同的傳入資料流。 這可讓您 toopublish 和封存的事件所需的不同部分。 例如，您的商務需求是 tooarchive 6 小時的程式，但 toobroadcast 最後的 10 分鐘。 tooaccomplish，您需要 toocreate 兩個同時執行的程式。 一個程式設 tooarchive 6 小時的 hello 事件，但 hello 程式不會發行。 hello 其他程式的組 tooarchive 為 10 分鐘並發佈此程式。

## <a name="billing-implications"></a>計費影響
通道會開始計費，只要它的狀態轉換太 「 執行 」 透過 hello 應用程式開發介面。  

hello 下表顯示 hello API 中的 toobilling 狀態和 Azure 入口網站通道狀態對應的方式。 請注意，hello 狀態 hello API 和入口網站 UX 之間稍有不同 一旦通道處於 hello 「 執行 」 透過 hello 應用程式開發介面，或在 hello 「 就緒 」 或 「 串流處理 」 狀態中 hello Azure 入口網站，計費將會啟用。

從計費您進一步 toostop hello 通道，您必須 tooStop hello 通道透過 hello 應用程式開發介面或在 hello Azure 入口網站中。
您必須負責停止您的通道，當您在與 hello 通道。 失敗 toostop hello 通道將會導致繼續計費。

> [!NOTE]
> 當使用標準頻道，AMS 就會自動關閉器仍然處於 「 執行 」 狀態 hello 輸入的摘要遺失，且不沒有執行任何程式後的 12 小時任何通道。 不過，您將仍然要支付 hello 時間 hello 通道處於 「 執行 」 狀態。
>
>

### <a id="states"></a>通道狀態和它們如何對應 toohello 計費模式
hello 的目前狀態的通道。 可能的值包括：

* **已停止**。 這是 hello 的 hello 初始狀態通道在建立之後 （除非自動啟動已選取 hello 入口網站中）。此狀態中不會計費。 處於此狀態，可以更新 hello 通道內容，但不是允許串流。
* **啟動中**。 正在啟動 hello 通道。 此狀態中不會計費。 在此狀態期間允許任何更新或串流。 如果發生錯誤，hello 通道就會傳回 toohello 已停止 」 狀態。
* **執行中**。 hello 通道都能夠處理即時串流。 現在針對使用量計費。 您必須停止 hello 通道 tooprevent 進一步計費。
* **停止中**。 hello 通道正在停止。 此暫時性狀態中不會計費。 在此狀態期間允許任何更新或串流。
* **刪除中**。 正在刪除 hello 通道。 此暫時性狀態中不會計費。 在此狀態期間允許任何更新或串流。

hello 下表顯示如何通道狀態地圖 toohello 計費模式。

| 通道狀態 | 入口網站 UI 指標 | 會計費嗎？ |
| --- | --- | --- |
| 啟動中 |啟動中 |無 (暫時性狀態) |
| 執行中 |就緒 (沒有執行中的程式)<br/>或<br/>串流 (至少一個執行中的程式) |是 |
| 停止中 |停止中 |無 (暫時性狀態) |
| 已停止 |已停止 |否 |

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>相關主題
[Azure 媒體服務的分散 MP4 即時內嵌規格](media-services-fmp4-live-ingest-overview.md)

[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)

[使用通道，從內部部署編碼器接收多位元速率即時串流](media-services-live-streaming-with-onprem-encoders.md)

[配額和限制](media-services-quotas-and-limitations.md)。  

[媒體服務概念](media-services-concepts.md)
