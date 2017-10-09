---
title: "建立多位元速率資料流-Azure 的內部編碼器使用 live aaaStream |Microsoft 文件"
description: "本主題描述如何接收多位元速率建立通道 tooset 即時資料流，從內部部署編碼器。 hello 資料流就可以傳送 tooclient 播放應用程式可以透過一個或多個串流端點，使用其中一種 hello 遵循適應性串流通訊協定： HLS、 Smooth Streaming、 DASH。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>使用會建立多位元速率串流的內部部署編碼器執行即時串流
## <a name="overview"></a>概觀
在 Azure 媒體服務中，通道代表處理即時串流內容的管線。 通道會以兩種方式之一收到即時輸入串流：

* 在內部部署即時編碼器會傳送多位元速率 RTMP 或 Smooth Streaming (分散 MP4) 資料流 toohello 通道不啟用的 tooperform 即時使用 Media Services 編碼。 hello 內嵌資料流通過通道而不需任何進一步處理。 此方法稱為 *傳遞*。 您可以使用下列有多位元速率 Smooth Streaming 做為輸出的即時編碼器的 hello： 媒體 Excel、 Ateme、 想像通訊、 Envivio、 Cisco、 和元素。 下列即時編碼器的 hello 有做為輸出 RTMP: Adobe Flash 媒體即時編碼器、 Telestream wirecast 編碼、 Haivision、 Teradek 和 tricaster 轉錄。 即時編碼器也可以傳送即時編碼請未啟用的單一位元速率資料流 tooa 通道，但我們不建議。 媒體服務會傳遞給要求 hello 資料流 toocustomers。

  > [!NOTE]
  > 使用傳遞的方法是 hello toodo 即時串流處理最經濟的方式。


* 在內部部署即時編碼器會將傳送的單一位元速率串流 toohello 頻道時，啟用即時使用其中一種 hello 下列格式的媒體服務編碼 tooperform: RTP (MPEG-TS)、 RTMP、 或 Smooth Streaming (分散 MP4)。 hello 通道之後會執行即時 hello 連入單一位元速率串流 tooa 多位元速率 （自動調整） 視訊資料流的編碼。 媒體服務會傳遞給要求 hello 資料流 toocustomers。

Hello 媒體服務 2.10 從版本開始，當您建立的通道，您可以指定您要如何您通道 tooreceive hello 輸入資料流。 您也可以指定是否要 hello 通道 tooperform 即時將資料流的編碼方式。 您有兩個選擇：

* **Pass Through**： 指定這個值，如果您計劃 toouse 在內部部署即時編碼器，會將多位元速率串流 （傳遞資料流） 做為輸出。 在此情況下，透過 toohello 輸出而不經過任何編碼傳送 hello 內送資料流。 這是通道的 hello hello 2.10 版前行為。 本主題提供有關使用此類型通道的詳細資訊。
* **即時編碼**： 如果您計劃 toouse Media Services tooencode 單一位元速率即時串流 tooa 多位元速率串流，請選擇此值。 請注意，在**執行**狀態中離開即時編碼通道將會產生費用。 我們建議您即時資料流的事件之後立即停止執行的頻道是完整 tooavoid 額外每小時費用。 媒體服務會傳遞給要求 hello 資料流 toocustomers。

> [!NOTE]
> 本主題討論屬性未啟用的通道 tooperform 即時編碼。 如需使用通道資訊啟用 tooperform 即時編碼，請參閱 <<c0> [ 使用 Azure Media Services toocreate 多位元速率串流的即時串流](media-services-manage-live-encoder-enabled-channels.md)。
>
>

下列圖表中的 hello 表示會使用內部部署即時編碼器 toohave 多位元速率 RTMP 或分散的 MP4 (Smooth Streaming) 資料流，做為輸出的即時資料流工作流程。

![即時工作流程][live-overview]

## <a id="scenario"></a>常見即時串流案例
hello 下列步驟說明有關建立常見即時資料流的應用程式的工作。

1. 視訊攝影機 tooa 電腦連線。 啟動並設定內部部署即時編碼器，讓它以多位元速率 RTMP 或 Fragmented MP4 (Smooth Streaming) 串流做為輸出。 如需詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。

    您也可以在建立通道之後執行此步驟。
2. 建立並啟動通道。

3. 擷取 hello 通道的內嵌 URL。

    hello 即時編碼器會使用 hello 內嵌 URL toosend hello 資料流 toohello 通道。
4. 擷取 hello 通道預覽 URL。

    使用您的通道可正常接收即時資料流 hello 這個 URL tooverify。
5. 建立程式。

    當您使用 hello Azure 入口網站時，建立程式也會建立資產。

    當您使用 hello.NET SDK 或 REST 時，您需要 toocreate 資產，並指定 toouse 此資產時建立程式。
6. 發佈與 hello 程式相關聯的 hello 資產。   

    >[!NOTE]
    >建立 Azure Media Services 帳戶時，**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 hello 串流的端點要從中 toostream 內容已經在 hello toobe**執行**狀態。

7. 當您準備好 toostart 串流並封存，請啟動 hello 程式。

8. （選擇性） hello 即時編碼器可以信號的 toostart 公告。 hello 公告 hello 輸出資料流中插入。

9. 每當您想 toostop 串流並封存 hello 事件時，請停止 hello 程式。

10. 刪除 hello 程式 （並選擇性地刪除 hello 資產）。     

## <a id="channel"></a>通道和其相關元件的說明
### <a id="channel_input"></a>頻道輸入 (內嵌) 組態
#### <a id="ingest_protocols"></a>嵌入串流通訊協定
媒體服務會使用多位元速率分散 MP4 和多位元速率 RTMP 做為串流通訊協定來支援內嵌即時摘要。 當 hello RTMP 內嵌串流通訊協定已選取時，兩個內嵌 （輸入） 端點會建立 hello 通道：

* **主要 URL**： 指定 hello 完整的 URL 的 hello 通道主要 RTMP 內嵌端點。
* **次要 URL** （選擇性）： 指定 hello 完整的 URL 的 hello 通道次要 RTMP 內嵌端點。

Hello 次要 URL 適用於您想 tooimprove hello 持久性與容錯您內嵌資料流 （以及編碼器容錯移轉及容錯功能），特別是針對下列案例的 hello:

- 單一雙推送 tooboth 主要及次要 Url 的編碼器：

    hello 這個案例的主要用途是 tooprovide 復原 toonetwork 波動越來越 jitters。 部分 RTMP 編碼器無法妥善處理網路中斷連線。 網路中斷連接發生失敗時，可能會停止編碼編碼器，與然後不會傳送 hello 緩衝處理資料時重新連線。 這會導致不連續和資料遺失。 網路中斷連線可能因為網路錯誤或維護 hello Azure 端上。 主要/次要 Url 減少 hello 網路問題，並提供受控制的升級程序。 每次發生排程的網路中斷連接，Media Services 會管理 hello 主要和次要資料庫中斷連接，以及提供延遲 hello 兩者之間中斷連線。 編碼器有時間 tookeep 傳送資料，然後重新連接一次。 hello hello 順序中斷連線可以是隨機的但永遠之間會有延遲主要/次要資料庫或次要/主要資料庫的 Url。 在此案例中，hello 編碼器仍是 hello 單一失敗點。

- 多個編碼器，以每個編碼器發送 tooa 專用點：

    這種情況下會提供兩個編碼器和擷取備援。 在此案例中，encoder1 推播通知 toohello 主要 URL，並 encoder2 將推送 toohello 次要 URL。 當編碼器失敗時，hello 其他編碼器可以保留傳送資料。 可以維護資料冗餘，因為媒體服務不會中斷 hello 在主要和次要 Url 相同的時間。 此案例假設編碼器會進行同步處理的時間，並完全提供 hello 相同的資料。  

- 雙推送 tooboth 主要及次要 Url 的多個編碼器：

    在此案例中，這兩個編碼器發送資料 tooboth 主要及次要 Url。 這提供 hello 最佳可靠性和容錯功能，以及資料重複。 此案例可容許兩個編碼器皆失敗並且中斷連線，即使一個編碼器停止運作。 假設編碼器會進行同步處理的時間，並且提供完全 hello 相同的資料。  

如需 RTMP 即時編碼器的詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](http://go.microsoft.com/fwlink/?LinkId=532824)。

#### <a name="ingest-urls-endpoints"></a>內嵌 URL (端點)
通道所提供的輸入的端點 （內嵌 URL） 您指定在 hello 即時編碼程式，讓可以推送 hello 編碼器串流 tooyour 通道。   

您可以取得 hello 內嵌 Url，當您建立 hello 通道。 針對您 tooget 這些 Url，hello 通道中並沒有 toobe hello**執行**狀態。 當您準備好 toostart 推送資料 toohello 通道時，必須在 hello hello 通道**執行**狀態。 Hello 通道開始擷取資料之後，您可以預覽您的資料流透過 hello 預覽 URL。

您可以選擇透過 SSL 連線來內嵌 Fragmented MP4 (Smooth Streaming) 即時資料流。 tooingest over SSL，請確定 tooupdate hello 內嵌 URL tooHTTPS。 目前，您無法內嵌 RTMP over SSL。

#### <a id="keyframe_interval"></a>主要畫面格間隔
當您使用內部部署即時編碼器 toogenerate 多位元速率串流時，hello 主要畫面格間隔可指定所使用的外部編碼器的 hello 的 hello 圖片群組 (GOP) 的持續時間。 Hello 通道收到此連入的資料流之後，您可以提供您的即時串流 tooclient 播放應用程式中任何 hello 下列格式： Smooth Streaming、 HTTP （虛線） 和 HTTP Live Streaming (HLS) 透過動態彈性資料流。 在執行即時資料流時，會一律動態封裝 HLS。 根據預設，媒體服務會自動計算 hello HLS 區段封裝比率 （每個區段的片段） 接收來自即時編碼程式 hello hello 主要畫面格間隔為基礎。

下表中的 hello 顯示 hello 區段持續時間的計算方式：

| 主要畫面格間隔 | HLS 區段封裝比例 (FragmentsPerSegment) | 範例 |
| --- | --- | --- |
| 小於或等於 too3 秒 |3:1 |如果 KeyFrameInterval （或 GOP） 是 2 秒，hello 預設 HLS 區段封裝比率會是 3 too1。 這會建立 6 秒 HLS 區段。 |
| 3 too5 秒 |2:1 |如果 KeyFrameInterval （或 GOP） 是 4 秒，hello 預設 HLS 區段封裝比率會是 2 too1。 這會建立 8 秒 HLS 區段。 |
| 大於 5 秒 |1:1 |如果 KeyFrameInterval （或 GOP） 6 秒，hello 預設 HLS 區段封裝比率會是 1 too1。 這會建立 6 秒 HLS 區段。 |

您可以變更設定 hello 通道的輸出和設定上 ChannelOutputHls FragmentsPerSegment hello 每個區段的片段比率。

您也可以設定上 ChanneInput hello KeyFrameInterval 屬性，以變更 hello 主要畫面格間隔值。 如果您明確設定 KeyFrameInterval，hello FragmentsPerSegment 透過先前所述的 hello 規則計算 HLS 區段封裝比率。  

如果您明確設定 KeyFrameInterval 和 FragmentsPerSegment，Media Services 會使用您設定的 hello 值。

#### <a name="allowed-ip-addresses"></a>允許的 IP 位址
您可以定義可允許 toopublish 視訊 toothis 通道的 hello IP 位址。 允許的 IP 位址可以指定為 hello 下列其中一種：

* 單一 IP 位址 (例如 10.0.0.1)
* 使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如 10.0.0.1/22)
* 使用 IP 位址和小數點十進位子網路遮罩的 IP 範圍 (例如 10.0.0.1(255.255.252.0))

如果未指定 IP 位址而且也未定義規則，則任何 IP 位址都不允許。 tooallow 任何 IP 位址，建立一個規則，並設定 0.0.0.0/0。

### <a name="channel-preview"></a>通道預覽
#### <a name="preview-urls"></a>預覽 URL
通道提供預覽端點 (預覽 URL) toopreview 並驗證您的資料流，然後再進一步處理和傳遞。

當您建立 hello 通道時，您可以取得 hello 預覽 URL。 對於您 tooget hello URL，hello 通道中並沒有 toobe hello**執行**狀態。 Hello 通道開始擷取資料之後，您可以預覽您的資料流。

目前，傳送 hello 預覽資料流，只能在分散 MP4 (Smooth Streaming) 格式，不論 hello 指定的輸入的類型。 您可以使用 hello [Smooth Streaming 的健全狀況監視器](http://smf.cloudapp.net/healthmonitor)player tootest hello smooth streaming。 您也可以使用播放程式裝載在 Azure 入口網站 tooview hello 您的資料流。

#### <a name="allowed-ip-addresses"></a>允許的 IP 位址
您可以定義可允許 tooconnect toohello 預覽端點的 hello IP 位址。 如果沒有指定 IP 位址，將會允許任何 IP 位址。 允許的 IP 位址可以指定為 hello 下列其中一種：

* 單一 IP 位址 (例如 10.0.0.1)
* 使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如 10.0.0.1/22)
* 使用 IP 位址和小數點十進位子網路遮罩的 IP 範圍 (例如 10.0.0.1(255.255.252.0))

### <a name="channel-output"></a>通道輸出
通道輸出的相關資訊，請參閱 hello[主要畫面格間隔](#keyframe_interval)> 一節。

### <a name="channel-managed-programs"></a>通道管理程式
通道是與程式，您可以使用 toocontrol hello 發佈和儲存區段中的即時資料流相關聯。 通道會管理程式。 hello 通道和程式的關聯性是內容的非常類似 tootraditional 媒體，其中通道具有常數資料流，而程式是內容的該頻道上的已設定領域的 toosome 逾時事件。

您可以指定您想要 tooretain hello 記錄內容 hello 程式設定 hello 的 hello 數**封存時間長度**長度。 這個值可以設定為 5 分鐘 tooa 最多 25 個小時的最小值。 封存時間長度也會規定 hello 最大用戶端可以從 hello 目前即時位置搜尋的時間量。 程式可以透過 hello 指定時間內，執行但落後 hello 時間長度的內容會持續遭到捨棄。 這個屬性的值也會決定資訊清單所能成長的時間長度 hello 用戶端。

每個程式都與儲存 hello 串流處理內容的資產。 資產是 hello Azure 儲存體帳戶中，對應的 tooa 區塊 blob 容器和 hello 資產中的 hello 檔案會儲存成該容器中的 blob。 toopublish hello 程式讓您的客戶可以檢視 hello 資料流中，您必須建立 OnDemand 定位器 hello 相關聯的資產。 您可以使用這個定位器 toobuild 您可以提供 tooyour 用戶端的串流 URL。

一個通道可支援同時執行的程式，因此您可以建立多個封存 hello toothree 註冊相同的傳入資料流。 您可以視需要發行和封存事件的不同部分。 例如，假設您的商務需求是 tooarchive 6 小時的程式，但 toobroadcast 只有 hello 過去 10 分鐘。 tooaccomplish，您需要 toocreate 兩個同時執行的程式。 一個程式設 tooarchive 6 小時的 hello 事件，但 hello 程式不會發行。 hello 其他程式的組 tooarchive 為 10 分鐘，並發佈此程式。

您不應該將現有程式重複用於新的事件。 而是針對每個事件建立新的程式。 當您準備好 toostart 串流並封存，請啟動 hello 程式。 每當您想 toostop 串流並封存 hello 事件時，請停止 hello 程式。

toodelete 封存內容時，會停止和刪除 hello 程式，然後再刪除 hello 相關聯的資產。 如果程式使用資產，則無法刪除它。 必須先刪除 hello 程式。

即使您停止並刪除 hello 程式之後，則使用者可以在直到您刪除 hello 資產串流處理將封存的內容，視視訊。 如果您想 tooretain hello 封存的內容，但沒有可供串流處理它，請刪除串流定位器 hello。

## <a id="states"></a>通道狀態和計費
Hello 之通道的目前狀態的可能值包括：

* **停止**： 這是在建立之後的 hello 通道 hello 初始狀態。 處於此狀態，可以更新 hello 通道內容，但不是允許串流。
* **啟動**: hello 通道正在啟動。 在此狀態期間允許任何更新或串流。 Hello 通道發生錯誤時，傳回 toohello**已停止**狀態。
* **執行**: hello 通道能夠處理即時資料流。
* **停止**: hello 通道正在停止。 在此狀態期間允許任何更新或串流。
* **刪除**： 正在刪除 hello 通道。 在此狀態期間允許任何更新或串流。

hello 下表顯示如何通道狀態地圖 toohello 計費模式。

| 通道狀態 | 入口網站 UI 指標 | 是否計費？ |
| --- | --- | --- | --- |
| **啟動中** |**啟動中** |無 (暫時性狀態) |
| **執行中** |**就緒** (沒有執行中的程式)<p><p>或<p>**串流** (至少一個執行中的程式) |是 |
| **停止中** |**停止中** |無 (暫時性狀態) |
| **已停止** |**已停止** |否 |

## <a id="cc_and_ads"></a>隱藏式字幕和廣告插入
下表中的 hello 示範字幕和廣告插入支援的標準。

| 標準 | 注意事項 |
| --- | --- |
| CEA-708 和 EIA-608 (708/608) |Cea-708 和 eia-608 是字幕 hello 美國和加拿大地區的標準。<p><p>目前，字幕功能才會支援傳送嗨編碼的輸入資料流中。 您需要 toouse 即時媒體編碼程式可以將 608 或 708 字幕插入傳送 tooMedia 服務的 hello 編碼資料流中。 Media Services 來提供 hello 與插入的字幕 tooyour 檢視器的內容。 |
| .ismt 裡面附帶字幕 (Smooth Streaming 文字播放軌) |Media Services 動態封裝可讓您的用戶端 toostream 內容中任何 hello 下列格式： DASH、 HLS 或 Smooth Streaming。 不過，如果您所擷取的分散 MP4 (Smooth Streaming) 含有.ismt （Smooth Streaming 文字播放軌） 內的標題，您可以傳送 hello 資料流 tooonly Smooth Streaming 用戶端。 |
| SCTE-35 |Scte-35 是已使用 toocue 廣告插入的數位訊號系統。 下游接收器會使用 hello 訊號 toosplice 廣告插入 hello 資料流 hello 分配的時間。 Scte-35 必須以疏鬆播放軌 hello 輸入資料流中傳送。<p><p>分散帶有廣告訊號的 hello 只支援輸入資料流格式的目前 MP4 (Smooth Streaming)。 hello，才支援輸出格式也是 Smooth Streaming。 |

## <a id="considerations"></a>考量
當您使用內部部署即時編碼器 toosend 多位元速率串流 tooa 通道時，適用於下列條件約束的 hello:

* 請確定您有足夠可用網際網路連線 toosend 資料 toohello 內嵌點。
* 使用次要內嵌 URL 時會佔用額外的頻寬。
* hello 傳入多位元速率串流可以有 10 個視訊的品質等級 （層級） 的最大值和最多 5 個音訊音軌。
* hello 最高平均位元速率 hello 視訊品質等級的其中之一應少於 10 Mbps。
* hello hello 平均彈性位元速率所有 hello 視訊和音訊資料流的彙總應少於 25 Mbps。
* 您無法變更 hello hello 通道時的輸入通訊協定，或其相關聯的程式正在執行。 如果您需要不同的通訊協定，則應該為每個輸入通訊協定建立個別的通道。
* 您可以在通道中內嵌單一位元速率。 但因為 hello 通道不會處理 hello 資料流，hello 用戶端應用程式也會收到單一位元速率資料流。 (不建議這個選項。)

以下是其他考量相關的 tooworking 與通道和相關的元件：

* 每次您重新設定 hello 即時編碼器，呼叫 hello**重設**hello 通道上的方法。 您重設 hello 通道之前，您會有 toostop hello 程式。 在重設 hello 通道之後，重新啟動 hello 程式。
* 只有當它在 hello 時才能停止通道**執行**狀態和 hello 通道上的所有程式都已停止。
* 根據預設，您可以加入只有 5 個通道 tooyour Media Services 帳戶。 如需詳細資訊，請參閱 [配額和限制](media-services-quotas-and-limitations.md)。
* 您會在通道處於 hello 時，才需要付費**執行**狀態。 如需詳細資訊，請參閱 toohello[通道狀態和計費](media-services-live-streaming-with-onprem-encoders.md#states)> 一節。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>相關主題
[Azure 媒體服務的分散 MP4 即時內嵌規格](media-services-fmp4-live-ingest-overview.md)

[Azure 媒體服務概觀和常見案例](media-services-overview.md)

[媒體服務概念](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
