---
title: "使用 Azure Media Services toocreate 多位元速率資料流資料流的 aaaLive |Microsoft 文件"
description: "本主題描述如何 tooset 建立通道接收單一位元速率即時資料流，從內部編碼器，並接著執行 Media services 即時編碼 tooadaptive 位元速率串流。 hello 資料流就可以傳送 tooclient 播放應用程式可以透過一個或多個資料流端點，使用其中一種 hello 遵循適應性串流通訊協定： HLS、 Smooth Streaming、 MPEG DASH。"
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>即時資料流使用 Azure Media Services toocreate 多位元速率串流
## <a name="overview"></a>概觀
在 Azure 媒體服務 (AMS) 中， **通道** 代表一個管線，負責處理即時資料流內容。 **通道** 會以兩種方式之一收到即時輸入串流：

* 在內部部署即時編碼器會傳送單一位元速率資料流是啟用的 tooperform toohello 通道即時使用其中一種 hello 下列格式的媒體服務編碼： RTP (MPEG-TS)、 RTMP、 或 Smooth Streaming (分散 MP4)。 hello 通道，然後執行即時編碼的 hello 連入單一位元速率串流 tooa 多位元速率 （自動調整） 視訊資料流。 要求時，媒體服務會傳送 hello 資料流 toocustomers。
* 在內部部署即時編碼器會傳送多位元速率**RTMP**或**Smooth Streaming** (分散 MP4) toohello 通道不啟用 tooperform 即時 AMS 編碼方式。 hello 內嵌的串流可以通過**通道**s，而不需任何進一步處理。 此方法稱為 **傳遞**。 您可以使用下列輸出多位元速率 Smooth Streaming 的即時編碼器的 hello: MediaExcel、 Ateme、 想像通訊、 Envivio、 Cisco 和元素。 hello 下列即時編碼器都會輸出 RTMP: Adobe Flash 媒體即時編碼器 (FMLE)、 Telestream wirecast 編碼、 Haivision、 Teradek 和 tricaster 轉錄編碼器。  即時編碼器也可以傳送單一位元速率串流 tooa 通道，將不會啟用即時編碼，但是不建議。 要求時，媒體服務會傳送 hello 資料流 toocustomers。
  
  > [!NOTE]
  > 使用傳遞的方法是 hello toodo 即時串流處理最經濟的方式。
  > 
  > 

Hello 媒體服務 2.10 從版本開始，當您建立的通道，您可以指定您想要用於您通道 tooreceive hello 輸入資料流和想要的 hello 通道 tooperform 的方式 live 您的資料流的編碼方式。 您有兩個選擇：

* **無**– 指定這個值，如果您計劃 toouse 在內部部署即時編碼器這樣會輸出多位元速率串流 （傳遞資料流）。 在此情況下，hello 內送資料流傳遞 toohello 輸出而不經過任何編碼。 這是通道 too2.10 先前版本的 hello 行為。  如需使用此種通道類型的詳細資訊，請參閱[使用會從建立多位元速率串流的內部部署編碼器執行即時串流](media-services-live-streaming-with-onprem-encoders.md)。
* **標準**– 選擇此值，如果您計劃 toouse Media Services tooencode 單一位元速率即時串流 toomulti 位元速率資料流。 請注意即時編碼的計費影響，而您應該記住離開 hello 「 執行 」 狀態中的即時編碼通道會產生計費費用。  建議您即時資料流事件之後立即停止您正在執行通道是完整 tooavoid 額外每小時費用。

> [!NOTE]
> 本主題討論的已啟用的通道屬性 tooperform 即時編碼 (**標準**編碼類型)。 通道不使用的相關資訊啟用 tooperform 即時編碼，請參閱[建立多位元速率串流的內部編碼器進行即時資料流處理](media-services-live-streaming-with-onprem-encoders.md)。
> 
> 請確定 tooreview hello[考量](media-services-manage-live-encoder-enabled-channels.md#Considerations)> 一節。
> 
> 

## <a name="billing-implications"></a>計費影響
即時編碼的通道開始計費，只要它的狀態轉換太 「 執行 」 透過 hello 應用程式開發介面。   Hello Azure 媒體服務總管工具 (http://aka.ms/amse) 或 hello Azure 入口網站中，您也可以檢視 hello 狀態。

hello 下表顯示 hello API 中的 toobilling 狀態和 Azure 入口網站通道狀態對應的方式。 請注意，hello 狀態 hello API 和入口網站 UX 之間稍有不同 一旦通道處於 hello 「 執行 」 透過 hello 應用程式開發介面，或在 hello 「 就緒 」 或 「 串流處理 」 狀態中 hello Azure 入口網站，計費將會啟用。
從計費您進一步 toostop hello 通道，您必須 tooStop hello 通道透過 hello 應用程式開發介面或在 hello Azure 入口網站中。
您必須負責停止您的通道，當您完成 hello 即時編碼通道時。  失敗 toostop 編碼的頻道會導致繼續計費。

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

### <a name="automatic-shut-off-for-unused-channels"></a>自動關閉未使用的通道
自 2016 年 1 月 25 日開始，媒體服務推出的更新會在 (啟用即時編碼的) 通道已長時間處於未使用的狀態時，自動停止該通道。 這適用於的 tooChannels 具有任何作用中的程式，以及哪些沒有接收到的一段時間的摘要輸入的比重。

hello 臨界值，在未使用的期間內受到名義 12 小時，但是主體 toochange。

## <a name="live-encoding-workflow"></a>即時編碼工作流程
hello 圖代表通道其中其中一種 hello 下列通訊協定接收單一位元速率串流的即時串流工作流程： RTMP、 Smooth Streaming 或 RTP (MPEG-TS);然後，它將編碼 hello 資料流 tooa 多位元速率串流。 

![即時工作流程][live-overview]

## <a id="scenario"></a>常見即時串流案例
hello 以下是建立通用的即時串流應用程式所需的一般步驟。

> [!NOTE]
> 目前，最大的 hello 建議即時事件的持續時間是 8 小時。 請如果您需要 toorun 通道的時間較長的時間，連絡 amslived microsoft.com。請注意即時編碼的計費影響，而您應該記住離開 hello 「 執行 」 狀態中的即時編碼通道會致使其每小時的計費費用。  建議您即時資料流事件之後立即停止您正在執行通道是完整 tooavoid 額外每小時費用。 
> 
> 

1. 視訊攝影機 tooa 電腦連線。 啟動及設定內部部署即時編碼器可以輸出**單一**位元速率串流，其中一種 hello 下列通訊協定： RTMP、 Smooth Streaming 或 RTP (MPEG-TS)。 
   
    此步驟也可以在您建立通道之後執行。
2. 建立並啟動通道。 
3. 擷取 hello 通道的內嵌 URL。 
   
    hello 內嵌 URL 由 hello 即時編碼器 toosend hello 資料流 toohello 通道。
4. 擷取 hello 通道預覽 URL。 
   
    使用您的通道可正常接收即時資料流 hello 這個 URL tooverify。
5. 建立程式。 
   
    當使用 hello Azure 入口網站時，建立程式也會建立資產。 
   
    使用.NET SDK 或 REST 時您需要 toocreate 資產，並指定 toouse 此資產時建立程式。 
6. 發佈 hello 與 hello 程式相關聯的資產。   
   
    >[!NOTE]
    >AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 hello 串流的端點要從中 toostream 內容已經在 hello toobe**執行**狀態。 
    
7. 當您準備好 toostart 串流和封存時，請啟動 hello 程式。
8. （選擇性） hello 即時編碼器可以信號的 toostart 公告。 hello 公告 hello 輸出資料流中插入。
9. 每當您想 toostop 串流並封存 hello 事件時，請停止 hello 程式。
10. 刪除 hello 程式 （並選擇性地刪除 hello 資產）。   

> [!NOTE]
> 您一定不 tooforget tooStop 即時編碼通道。 請注意，每小時計費即時編碼的影響，而您應該記住離開 hello 「 執行 」 狀態中的即時編碼通道會產生計費費用。  建議您即時資料流事件之後立即停止您正在執行通道是完整 tooavoid 額外每小時費用。 
> 
> 

## <a id="channel"></a>通道的輸入 (嵌入) 組態
### <a id="Ingest_Protocols"></a>嵌入串流通訊協定
如果 hello**編碼器類型**設定得**標準**，有效的選項為：

* **RTP** (MPEG-TS)：透過 RTP 的 MPEG-2 傳輸串流。  
* 單一位元速率 **RTMP**
* 單一位元速率 **分散的 MP4** (Smooth Streaming)

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG-TS) - 透過 RTP 的 MPEG-2 傳輸串流。
典型的使用案例： 

專業廣播者通常使用的高階在內部部署即時編碼器像元素的技術、 易利信行動、 Ateme、 Imagine 或 Envivio toosend 廠商資料流。 通常會和 IT 部門和私人網路一起使用。

考量：

* 強烈建議使用單一程式傳輸串流 (SPTS) 輸入 hello。 
* 您可以設定使用透過 RTP 的 mpeg-2 TS too8 音訊資料流輸入。 
* 應有低於 15 Mbps 的平均位元速率 hello 視訊資料流。
* hello 彙總平均位元速率的 hello 音訊資料流應少於 1 Mbps
* 下列是 hello 支援的轉碼器：
  
  * Mpeg-2 / H.262 視訊 
    
    * 主要設定檔 (4:2:0)
    * 高設定檔 (4:2:0, 4:2:2)
    * 422 設定檔 (4:2:0, 4:2:2)
  * MPEG-4 AVC / H.264 視訊  
    
    * 基準、主要、高設定檔 (8-bit 4:2:0)
    * 高 10 設定檔 (10 位元 4:2:0)
    * 高 422 設定檔 (10 位元 4:2:2)
  * Mpeg-2 AAC-LC 音訊 
    
    * 單聲道、立體聲、環繞 (5.1、7.1)
    * MPEG-2 樣式 ADTS 封裝
  * Dolby Digital (AC-3) 音訊 
    
    * 單聲道、立體聲、環繞 (5.1、7.1)
  * MPEG 音訊 (Layer II 和 III) 
    
    * 單聲道、立體聲
* 建議的廣播編碼器包含：
  
  * Imagine Communications Selenio ENC 1
  * Imagine Communications Selenio ENC 2
  * Elemental Live

#### <a id="single_bitrate_RTMP"></a>單一位元速率 RTMP
考量：

* hello 內送資料流不能包含多位元速率視訊
* 應有低於 15 Mbps 的平均位元速率 hello 視訊資料流。
* 應有低於 1 Mbps 的平均位元速率 hello 音訊資料流。
* 下列是 hello 支援的轉碼器：
* MPEG-4 AVC / H.264 視訊
* 基準、主要、高設定檔 (8-bit 4:2:0)
* 高 10 設定檔 (10 位元 4:2:0)
* 高 422 設定檔 (10 位元 4:2:2)
* Mpeg-2 AAC-LC 音訊
* 單聲道、立體聲、環繞 (5.1、7.1)
* 44.1 kHz 範例速率
* MPEG-2 樣式 ADTS 封裝
* 建議的編碼器包括：
* Telestream Wirecast
* Flash Media Live Encoder

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>單一位元速率的分散 MP4 (Smooth Streaming)
典型的使用案例：

使用內部部署即時編碼器像元素的技術、 易利信行動、 Ateme，Envivio toosend hello 輸入資料流透過 hello 開啟網際網路 tooa 附近的 Azure 資料中心的廠商。

考量：

對於 [單一位元速率 RTMP](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP)也一樣。

#### <a name="other-considerations"></a>其他考量
* 您無法變更 hello hello 通道時的輸入通訊協定，或其相關聯的程式正在執行。 如果您需要不同的通訊協定，則應該為每個輸入通訊協定建立個別的通道。
* Hello 連入的視訊資料流的最大解析度 1920 x 1080，和最多 60 欄位/秒交錯式，如果或 30 框架/秒如果漸進式。

### <a name="ingest-urls-endpoints"></a>內嵌 URL (端點)
通道所提供的輸入的端點 （內嵌 URL） 您指定在 hello 即時編碼程式，讓可以推送 hello 編碼器串流 tooyour 通道。

您可以取得 hello 內嵌 Url，一旦您建立的通道。 tooget 這些 Url，hello 通道中並沒有 toobe hello**執行**狀態。 當您準備好 toostart 將資料推送至 hello 通道時，它必須位於 hello**執行**狀態。 一旦 hello 通道開始擷取資料，您可以預覽您的資料流透過 hello 預覽 URL。

您可以透過 SSL 連線選擇內嵌的分散 MP4 (Smooth Streaming) 即時串流。 tooingest over SSL，請確定 tooupdate hello 內嵌 URL tooHTTPS。 請注意，目前 AMS 不支援使用 SSL 搭配自訂網域。  

### <a name="allowed-ip-addresses"></a>允許的 IP 位址
您可以定義可允許 toopublish 視訊 toothis 通道的 hello IP 位址。 允許的 IP 位址可以指定為單一 IP 位址 (例如'10.0.0.1')、使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如'10.0.0.1/22’)，或使用 IP 位址和以點分隔十進位子網路遮罩的 IP 範圍 (例如'10.0.0.1(255.255.252.0)')。

如果未指定 IP 位址，而且沒有任何規則定義，則不允許任何 IP 位址。 tooallow 任何 IP 位址，建立一個規則，並設定 0.0.0.0/0。

## <a name="channel-preview"></a>通道預覽
### <a name="preview-urls"></a>預覽 URL
通道提供預覽端點 (預覽 URL) toopreview 並驗證您的資料流，然後再進一步處理和傳遞。

當您建立 hello 通道時，您可以取得 hello 預覽 URL。 tooget hello URL，hello 通道中並沒有 toobe hello**執行**狀態。

一旦 hello 通道開始擷取資料，您可以預覽您的資料流。

> [!NOTE]
> 目前只有來傳送 hello 預覽資料流中分散 MP4 (Smooth Streaming) 格式 hello 不論指定的輸入的類型。 您可以使用 hello [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) player tootest hello Smooth Stream。 您也可以使用播放程式裝載在 Azure 入口網站 tooview hello 您的資料流。
> 
> 

### <a name="allowed-ip-addresses"></a>允許的 IP 位址
您可以定義可允許 tooconnect toohello 預覽端點的 hello IP 位址。 如果沒有指定 IP 位址，將會允許任何 IP 位址。 允許的 IP 位址可以指定為單一 IP 位址 (例如'10.0.0.1')、使用 IP 位址和 CIDR 子網路遮罩的 IP 範圍 (例如'10.0.0.1/22’)，或使用 IP 位址和以點分隔十進位子網路遮罩的 IP 範圍 (例如‘10.0.0.1(255.255.252.0)’)。

## <a name="live-encoding-settings"></a>即時編碼設定
本節說明如何 hello hello hello 通道內的即時編碼器設定，調整當 hello**編碼類型**通道設定太**標準**。

> [!NOTE]
> 使用 Azure 輸入多個語言資料軌及執行即時編碼時，多語言輸入僅支援 RTP。 您可以使用透過 RTP 的 mpeg-2 TS too8 音訊資料流上定義。 目前不支援使用 RTMP 或 Smooth Streaming 內嵌多個音軌。 在執行動作時即時編碼與[在內部部署即時編碼](media-services-live-streaming-with-onprem-encoders.md)，不會有這類限制因為任何傳送 tooAMS 通過通道而不需任何進一步處理。
> 
> 

### <a name="ad-marker-source"></a>Ad 標記來源
您可以指定 ad 標記信號的 hello 來源。 預設值是**Api**，表示該 hello 通道內的 hello 即時編碼器應接聽非同步 tooan **Ad 標記 API**。

hello 其他有效的選項是**Scte35** （才允許 hello 內嵌串流通訊協定設定 tooRTP (MPEG-TS)。 指定 Scte35 時，hello 即時編碼器會剖析從輸入 RTP (MPEG-TS) 資料流 hello scte-35 訊號。

### <a name="cea-708-closed-captions"></a>CEA 708 隱藏式輔助字幕
選擇性的旗標，告知 hello 即時編碼器 tooignore 任何 CEA 708 標題資料內嵌在 hello 連入的視訊。 當 hello 旗標設定 toofalse （預設值） 時，hello 編碼器會偵測並重新將 CEA 708 資料插入 hello 輸出視訊串流。

### <a name="video-stream"></a>視訊串流
選用。 描述 hello 輸入視訊串流。 如果未指定此欄位，則會使用 hello 預設值。 Hello 輸入資料流通訊協定設定 tooRTP (MPEG-TS) 時，才允許這項設定。

#### <a name="index"></a>索引
指定 hello hello 通道內的即時編碼器應該處理哪一個輸入視訊串流的以零為起始索引。 只有當內嵌串流通訊協定是 RTP (MPEG-TS) 時才適用此設定。

預設值為零。 建議 toosend 單一程式傳輸串流 (SPTS) 中。 如果 hello 輸入資料流包含多個程式，hello 即時編碼器會剖析 hello 輸入中的 hello 程式對應資料表 (PMT)、 識別具有串流類型名稱的 mpeg-2 視訊或 H.264，hello 輸入並排列 hello hello PMT 中指定的順序 hello 以零為起始的索引可隨即用 toopick hello 在排列中的第 n 個項目。

### <a name="audio-stream"></a>音訊串流
選用。 描述 hello 輸入音訊串流。 如果未指定此欄位，適用於指定 hello 預設值。 Hello 輸入資料流通訊協定設定 tooRTP (MPEG-TS) 時，才允許這項設定。

#### <a name="index"></a>索引
建議 toosend 單一程式傳輸串流 (SPTS) 中。 如果 hello 輸入資料流包含多個程式，hello hello 通道內的即時編碼器會剖析 hello 輸入中的 hello 程式對應資料表 (PMT)、 識別具有串流類型名稱 mpeg-2 AAC ADTS 或 ac-3 系統 A 或 ac-3 系統 B 或 mpeg-2 私用的 hello 輸入PES 或 mpeg-1 音訊或 mpeg-2 音訊並 hello hello PMT 中指定的順序排列 hello 以零為起始的索引可隨即用 toopick hello 在排列中的第 n 個項目。

#### <a name="language"></a>語言
hello hello 音訊資料流，符合 tooISO 639-2 例如 ENG 語言識別碼 如果不存在，hello 預設為 UND （未定義）。

有最長可能會設定指定是否 hello 輸入 toohello 通道是透過 RTP mpeg-2 TS too8 音訊資料流。 不過，有可能會以 hello 沒有兩個項目相同的索引值。

### <a id="preset"></a>系統預設
指定 hello 預設 toobe hello 這個通道內的即時編碼器所使用。 目前，hello 只允許值是**Default720p** （預設值）。

請注意如果您需要自訂的預設設定，您應該在 Microsoft.com 上連絡 amslived。

**Default720p** hello 視訊會編碼至下列 7 層 hello。

#### <a name="output-video-stream"></a>輸出視訊串流
| 位元速率 | 寬度 | 高度 | MaxFPS | 設定檔 | 輸出串流名稱 |
| --- | --- | --- | --- | --- | --- |
| 3500 |1280 |720 |30 |高 |Video_1280x720_3500kbps |
| 2200 |960 |540 |30 |主要區段 |Video_960x540_2200kbps |
| 1350 |704 |396 |30 |主要區段 |Video_704x396_1350kbps |
| 850 |512 |288 |30 |主要區段 |Video_512x288_850kbps |
| 550 |384 |216 |30 |主要區段 |Video_384x216_550kbps |
| 350 |340 |192 |30 |基準 |Video_340x192_350kbps |
| 200 |340 |192 |30 |基準 |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>輸出音訊串流
音訊已編碼的 toostereo AAC-LC 64 kbps，取樣率的 44.1 kHz。

## <a name="signaling-advertisements"></a>發出信號的廣告
當您的通道啟用即時編碼時，您會在處理視訊的管線中具有元件，並可加以操作。 您可以發出信號的 hello 通道 tooinsert 情況及/或廣告插入 hello 傳出彈性位元速率資料流。 情況仍可用總 hello 輸入即時摘要 toocover 在某些情況下 （例如在廣告插播） 的映像。 廣告訊號是時間同步處理的訊號，您內嵌到 hello 傳出資料流 tootell hello 影片播放器 tootake 特殊的動作 – 例如 tooswitch tooan 公告在 hello 適當的時間。 請參閱此[部落格](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/)hello scte-35 訊號機制為此用途的概觀。 以下是您可以在即時事件中實作的典型案例。

1. 具有您取得預先事件映像之前 hello 事件開始的檢視者。
2. 具有您的檢視者 hello 事件結束之後，取得事件後的映像。
3. 具有您的檢視者取得的錯誤事件映像，如果在 hello 事件 （例如，hello 場地中的電源中斷） 期間的問題。
4. 傳送廣告插播映像 toohide hello 即時事件摘要廣告插播期間。

hello 以下是 hello 信號廣告時，您可以設定的內容。 

### <a name="duration"></a>Duration
hello 持續時間，以秒為單位 hello 廣告插播。 這有 toobe 非零的正整數值中順序 toostart hello 廣告插播。 當廣告插播處於進度與 hello 持續時間組 toozero 以 hello CueId 符合 hello 在廣告插播，則會取消該插播。

### <a name="cueid"></a>CueId
Hello 廣告插播，toobe tootake 適當動作時，下游應用程式所使用的唯一識別碼。 需要 toobe 的正整數。 您可以設定此值 tooany 隨機正整數或上游系統 tootrack hello 提示識別碼。 透過 hello API 送出之前請特定 toonormalize 任何識別碼 toopositive 整數。

### <a name="show-slate"></a>顯示 slate
選用。 表示 hello 即時編碼器 tooswitch toohello[預設 slate](media-services-manage-live-encoder-enabled-channels.md#default_slate)廣告插播期間的映像，隱藏 hello 連入的視訊摘要。 在 slate 期間也要使音訊靜音。 預設值為 **false**。 

hello hello 預設 slate 資產識別碼屬性透過指定 hello hello 通道建立時的其中一個可以使用 hello 映像。 hello 候選影片會伸展 toofit hello 顯示映像大小。 

## <a name="insert-slate--images"></a>插入靜態圖像映像
hello hello 通道內的即時編碼器可以信號的 tooswitch tooa slate 映像。 它也可以收到信號的 tooend 進行中的 slate。 

hello 即時編碼器可以設定的 tooswitch tooa slate 映像和隱藏 hello 連入的視訊訊號在某些情況下 – 例如，在廣告插播期間。 如果未設定此 slate，就不會在廣告插播期間遮罩處理輸入視訊。

### <a name="duration"></a>Duration
hello 的持續時間 hello 候選影片以秒為單位。 這有 toobe 非零的正整數值順序 toostart hello 候選影片中。 如果沒有進行中的 slate，就會指定玲為持續時間，進行中的 slate 就會終止。

### <a name="insert-slate-on-ad-marker"></a>插入 ad 標記上的 slate
當組 tootrue，這項設定會設定在廣告插播期間 hello 即時編碼器 tooinsert slate 映像。 hello 預設值為 true。 

### <a id="default_slate"></a>預設靜態圖像資產識別碼

選用。 指定 hello hello 包含 hello slate 映像的媒體服務資產的資產識別碼。 預設值為 null。 


>[!NOTE] 
>建立 hello 通道之前, hello slate 映像以 hello 遵循條件約束應上傳做為專用的資產 （此資產應該沒有其他檔案）。 只有當 hello 即時編碼器正在插入 slate tooan 廣告插播，到期或已明確發出信號 tooinsert 平板式，會使用此映像。 hello 即時編碼器可以也進入平板電腦模式在某些錯誤情況 – 例如 hello 輸入的訊號就會遺失。 目前沒有選項 toouse 自訂映像時 hello 即時編碼器會進入這類 '輸入的訊號遺失' 的狀態。 您可以在[這裡](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel)投此功能一票。


* 最多 1920 x 1080 的解析度。
* 最多 3 Mb 的大小。
* hello 檔案名稱副檔名必須是 *.jpg。
* hello 映像必須當做 hello 該資產中的唯一 AssetFile 和此 AssetFile 應該標示為 hello 主要檔案上傳到資產之用。 hello 資產不能儲存體加密。

如果 hello**預設平板電腦資產識別碼**未指定，和**ad 標記上插入平板電腦**設定得**true**，預設的 Azure 媒體服務映像將會使用的 toohide hello 輸入視訊資料流。 在 slate 期間也要使音訊靜音。 

## <a name="channels-programs"></a>通道的程式
通道是 toocontrol hello 發行和即時串流片段的儲存體可讓您的程式相關聯。 通道會管理程式。 hello 通道和程式的關聯性是內容的非常類似 tootraditional 媒體其中通道具有常數資料流，而程式是內容的該頻道上的已設定領域的 toosome 逾時事件。

您可以指定您想要 tooretain hello 記錄內容 hello 程式設定 hello 的 hello 數**封存時間長度**長度。 這個值可以設定為 5 分鐘 tooa 最多 25 個小時的最小值。 封存時間長度也會規定 hello 最大用戶端可以從 hello 目前即時位置搜尋的時間量。 程式可以透過 hello 指定時間內，執行但落後 hello 時間長度的內容會持續遭到捨棄。 這個屬性的值也會決定資訊清單所能成長的時間長度 hello 用戶端。

每個程式都與可儲存 hello 串流處理內容的資產。 資產是 hello Azure 儲存體帳戶中的對應的 tooa 區塊 blob 容器和 hello 資產中的 hello 檔案會儲存成該容器中的 blob。 toopublish hello 程式讓您的客戶可以檢視您必須建立 OnDemand 定位器 hello 資料流相關聯的資產。 擁有這個定位器，可讓您 toobuild 您可以提供 tooyour 用戶端的串流 URL。

一個通道可支援同時執行的程式，因此您可以建立多個封存 hello toothree 註冊相同的傳入資料流。 這可讓您 toopublish 和封存的事件所需的不同部分。 例如，您的商務需求是 tooarchive 6 小時的程式，但 toobroadcast 最後的 10 分鐘。 tooaccomplish，您需要 toocreate 兩個同時執行的程式。 一個程式設 tooarchive 6 小時的 hello 事件，但 hello 程式不會發行。 hello 其他程式的組 tooarchive 為 10 分鐘並發佈此程式。

您不應該將現有程式重複用於新的事件。 相反地，建立並啟動新的程式，針對每個事件 hello 程式設計即時串流應用程式 > 一節中所述。

當您準備好 toostart 串流和封存時，請啟動 hello 程式。 每當您想 toostop 串流並封存 hello 事件時，請停止 hello 程式。 

toodelete 封存內容時，會停止和刪除 hello 程式，然後再刪除 hello 相關聯的資產。 無法刪除資產，如果它由程式;必須先刪除 hello 程式。 

即使您停止並刪除 hello 程式之後，hello 使用者是無法 toostream 封存的內容，視視訊，只要您不要刪除 hello 資產。

若要封存的 tooretain hello 內容，而不是需要它提供給串流，刪除 hello 串流定位器。

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>取得即時摘要的縮圖預覽
啟用即時編碼時，您現在可以取得 hello 即時摘要的預覽到達 hello 通道。 這可以是有用的工具 toocheck 是否即時摘要確實抵達通道 hello。 

## <a id="states"></a>通道狀態和狀態如何對應 toohello 計費模式
hello 的目前狀態的通道。 可能的值包括：

* **已停止**。 這是在建立之後的 hello hello 通道初始狀態。 處於此狀態，可以更新 hello 通道內容，但不是允許串流。
* **啟動中**。 正在啟動 hello 通道。 在此狀態期間允許任何更新或串流。 如果發生錯誤，hello 通道就會傳回 toohello 已停止 」 狀態。
* **執行中**。 hello 通道都能夠處理即時串流。
* **停止中**。 hello 通道正在停止。 在此狀態期間允許任何更新或串流。
* **刪除中**。 正在刪除 hello 通道。 在此狀態期間允許任何更新或串流。

hello 下表顯示如何通道狀態地圖 toohello 計費模式。 

| 通道狀態 | 入口網站 UI 指標 | 是否計費？ |
| --- | --- | --- |
| 啟動中 |啟動中 |無 (暫時性狀態) |
| 執行中 |就緒 (沒有執行中的程式)<br/>或<br/>串流 (至少一個執行中的程式) |是 |
| 停止中 |停止中 |無 (暫時性狀態) |
| 已停止 |已停止 |否 |

> [!NOTE]
> 目前 hello 通道開始平均約為 2 分鐘，但有些時候可能會佔用 too20 + 分鐘。 通道重設可能佔用 too5 分鐘。
> 
> 

## <a id="Considerations"></a>考量
* 當通道**標準**編碼類型發生的輸入的來源/比重摘要遺失時，它取代成錯誤 slate，無回應 hello 來源視訊/音訊補償它。 hello 通道將會繼續 tooemit 平板式，直到 hello 輸入/比重摘要的履歷表。 我們建議不要讓即時通道停留在此狀態超過 2 個小時。 超過該時間點，不保證 hello 行為的 hello 通道輸入重新連線時，都不是在回應 tooa 重設命令及其行為。 您將有 toostop hello 通道、 將它刪除，並建立一個新。
* 您無法變更 hello hello 通道時的輸入通訊協定，或其相關聯的程式正在執行。 如果您需要不同的通訊協定，則應該為每個輸入通訊協定建立個別的通道。
* 每次您重新設定 hello 即時編碼器，呼叫 hello**重設**hello 通道上的方法。 您重設 hello 通道之前，您會有 toostop hello 程式。 在重設 hello 通道之後，重新啟動 hello 程式。
* 只有當它是在 hello 執行狀態，而且 hello 通道上的所有程式都已都停止時，可能會都停止通道。
* 根據預設，您可以只加入 5 通道 tooyour Media Services 帳戶。 這是所有新帳戶的彈性配額。 如需詳細資訊，請參閱 [配額和限制](media-services-quotas-and-limitations.md)。
* 您無法變更 hello hello 通道時的輸入通訊協定，或其相關聯的程式正在執行。 如果您需要不同的通訊協定，則應該為每個輸入通訊協定建立個別的通道。
* 您會在通道處於 hello 時才需要付費**執行**狀態。 如需詳細資訊，請參閱太[這](media-services-manage-live-encoder-enabled-channels.md#states)> 一節。
* 目前，最大的 hello 建議即時事件的持續時間是 8 小時。 請如果您需要 toorun 通道的時間較長的時間，連絡 amslived microsoft.com。
* 請確定 toohave hello 您要在 hello toostream 內容的串流端點**執行**狀態。
* 使用 Azure 輸入多個語言資料軌及執行即時編碼時，多語言輸入僅支援 RTP。 您可以使用透過 RTP 的 mpeg-2 TS too8 音訊資料流上定義。 目前不支援使用 RTMP 或 Smooth Streaming 內嵌多個音軌。 在執行動作時即時編碼與[在內部部署即時編碼](media-services-live-streaming-with-onprem-encoders.md)，不會有這類限制因為任何傳送 tooAMS 通過通道而不需任何進一步處理。
* hello 編碼預設會使用 hello 的 「 最大的畫面播放速率"30fps 的概念。 因此，如果 hello 輸入就 60 fps / 59.97i，hello 輸入的框架會卸除/還原-interlaced too30/29.97 fps。 如果 hello 輸入 50 fps/50i，hello 輸入畫面格就會卸除/還原-interlaced too25 fps。 如果 25 fps hello 輸入，輸出會保持為 25 的 fps。
* 別忘了 tooSTOP 您通道時完成。 如果您忘記，計費會繼續。

## <a name="known-issues"></a>已知問題
* 通道啟動時間已經過改良 tooan 平均 2 分鐘，但有時候日益增加的需求可能仍然需要 too20 + 分鐘。
* 為專業的廣播者建立 RTP 支援。 請檢閱 RTP 中的 hello 注意事項[這](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/)部落格。
* 平板電腦影像應該符合所述的 toorestrictions[這裡](media-services-manage-live-encoder-enabled-channels.md#default_slate)。 如果您嘗試建立通道時的預設平板電腦大於 1920 x 1080、 hello 要求最後將會錯誤。
* 再次...忘 tooSTOP 您通道，當您在資料流。 如果您忘記，計費會繼續。

## <a name="next-step"></a>後續步驟
檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>相關主題
[使用 Azure 媒體服務傳遞即時串流事件](media-services-overview.md)

[建立執行即時編碼，從入口網站的單一位元速率 tooadaptive 位元速率資料流的通道](media-services-portal-creating-live-encoder-enabled-channel.md)

[建立執行使用.NET SDK 單一位元速率 tooadaptive 位元速率串流的即時編碼的頻道](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[使用 REST API 管理通道 (英文)](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[媒體服務概念](media-services-concepts.md)

[Azure 媒體服務的分散 MP4 即時內嵌規格](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

