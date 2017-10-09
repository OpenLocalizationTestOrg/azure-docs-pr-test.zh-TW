---
title: "aaaAzure Media Services 分散的 MP4 即時內嵌規格 |Microsoft 文件"
description: "此規格說明 hello 通訊協定和格式分散 MP4 基礎即時資料流擷取 Azure 媒體服務。 您可以使用 Azure Media Services toostream 即時事件，並使用 Azure 做為 hello 雲端平台廣播即時內容。 本文件也討論建置高度備援且強固之即時內嵌機制的最佳做法。"
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Azure 媒體服務的分散 MP4 即時內嵌規格
此規格說明 hello 通訊協定和格式分散 MP4 基礎即時資料流擷取 Azure 媒體服務。 Media Services 提供即時串流服務的客戶可以使用 toostream 即時事件，並使用 Azure 做為 hello 雲端平台廣播即時內容。 本文件也討論建置高度備援且強固之即時內嵌機制的最佳做法。

## <a name="1-conformance-notation"></a>1.一致性標記法
hello 關鍵字 「 必須 」 「 必須不是，」 「 要求 」 的 「"SHALL，"應該 NOT，"「 應該 」，「 應該 NOT，"「 建議 」、 「 可能 」 和此文件中的 [選擇性] 是 toobe 解譯，因為它們是在 RFC 2119 中所述。

## <a name="2-service-diagram"></a>2.服務圖表
hello 下列圖表顯示 hello 高層級架構 hello 即時串流處理媒體服務中的服務：

1. 即時編碼器將會建立及佈建的即時摘要 toochannels 推送透過 hello Azure Media Services SDK。
2. 通道、 程式及所有 hello 都即時串流功能，包括內嵌、 格式化、 媒體服務控制代碼的串流端點雲端 DVR、 安全性、 延展性和備援。
3. 客戶可以選擇 toodeploy Azure 內容傳遞網路之間的層 hello 串流端點和 hello 用戶端端點。
4. 用戶端端點的資料流從 hello 串流端點使用 HTTP 彈性資料流通訊協定。 範例包括 Microsoft Smooth Streaming、透過 HTTP 執行的動態彈性資料流 (DASH 或 MPEG-DASH)，以及 Apple HTTP 即時串流 (HLS)。

![內嵌流程][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3.位元資料流格式 – ISO 14496-12 分散 MP4
hello 電傳格式的即時資料流擷取中討論這份文件根據 [14496-12]。 如需分散 MP4 格式、點播視訊檔案及即時串流內嵌的詳細說明，請參閱 [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx)。

### <a name="live-ingest-format-definitions"></a>即時內嵌格式定義
hello 下列清單說明適用於 toolive 定義內嵌到 Azure Media Services 的特殊格式：

1. hello **ftyp**，**即時伺服器資訊清單方塊**，和**moov**方塊必須傳送每個要求 (HTTP POST)。 兩個方塊必須傳送 hello 資料流的 hello 開頭，並的隨時 hello 編碼器必須重新連接 tooresume 資料流擷取。 如需詳細資訊，請參閱 [1] 的第 6 節。
2. [1] 的第 3.3.2 節為即時內嵌定義名為 **StreamManifestBox** 的選用方塊。 Toohello hello Azure 負載平衡器的路由邏輯，因為使用此方塊已被取代。 hello 方塊不能有時擷取到 Media Services。 如果有此方塊，則媒體服務會以無訊息方式將其忽略。
3. hello **TrackFragmentExtendedHeaderBox**必須存在的每個片段中 3.2.3.2 [1] 中定義的方塊。
4. 第 2 版的 hello **TrackFragmentExtendedHeaderBox**方塊應使用的 toogenerate 媒體區段在多個資料中心中具有相同的 Url。 hello 片段索引欄位為 REQUIRED 跨資料中心容錯移轉的索引式例如 Apple HLS 的串流格式，以索引為基礎的 MPEG DASH。 tooenable 跨資料中心容錯移轉，hello 片段索引必須跨多個編碼器會進行同步處理，並會加 1 的每個後續媒體片段，甚至可跨編碼器重新啟動或失敗。
5. 在 [1] 的區段 3.3.6 會定義方塊稱為**MovieFragmentRandomAccessBox** (**mfra**)，可能會傳送 hello 即時擷取 tooindicate 結束資料流 (EOS) toohello 通道一端。 到期 toohello 內嵌 Media Services 的邏輯，使用 EOS 已經過時，而且 hello **mfra**方塊不會傳送即時擷取的。 如果已傳送，媒體服務會以無訊息方式將其忽略。 hello tooreset hello 狀態擷取點，我們建議您改用[重設通道](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels)。 我們也建議您改用[程式停止](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs)tooend 簡報和資料流。
6. hello MP4 片段持續時間應為常數，tooreduce hello 大小 hello 用戶端資訊清單。 常數的 MP4 片段持續時間也會改善用戶端下載啟發學習法透過 hello 使用重複的標記。 hello 持續時間可能會變動 toocompensate 的非整數的畫面播放速率。
7. hello MP4 片段期間應該大約 2 和 6 秒之間。
8. 「應該」以遞增順序送達 MP4 片段時間戳記和索引 (**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` 和 `fragment_index`)。 雖然媒體服務具有恢復功能 tooduplicate 片段，但是它具有有限能力 tooreorder 片段根據 toohello 媒體時間軸。

## <a name="4-protocol-format--http"></a>4.通訊協定格式 – HTTP
ISO 分散 MP4 基礎即時內嵌的 Media Services 會使用標準長時間執行 HTTP POST 要求 tootransmit 編碼媒體資料封裝在分散 MP4 格式 toohello 服務。 每個 HTTP POST 傳送完整的分散 MP4 bitstream （「 資料流 」），從標頭方塊的 hello 開頭開始 (**ftyp**，**即時伺服器資訊清單方塊**，和**moov**方塊），並繼續進行一連串的片段 (**moof**和**mdat**方塊)。 如需 hello HTTP POST 要求的 URL 語法，請參閱節 9.2 [1]。 舉例來說，hello POST URL 是： 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>需求
以下是 hello 詳細的需求：

1. hello 編碼器應該啟動廣播傳送 HTTP POST 要求為空白的 hello"body"（內容長度為零） 使用 hello 擷取相同的 URL。 這可協助 hello 編碼器快速偵測 hello 即時擷取端點是否有效，並且如果有任何驗證或其他所需的條件。 每個 HTTP 通訊協定，hello 伺服器無法傳送回 HTTP 回應 hello 整個收到要求之前，包括 hello 張貼的內容。 即時事件，而此步驟中，hello 編碼器不 hello 長時間執行，因此可能不是能 toodetect 任何錯誤直到完成傳送嗨的所有資料為止。
2. hello 編碼器必須處理的任何錯誤或驗證挑戰，因為 (1)。 如果 (1) 後續的回應為 200，則繼續進行。
3. hello 編碼器必須啟動新的 HTTP POST 要求與 hello 分散 MP4 資料流。 hello 承載必須以 hello [標題] 方塊中，後面接著片段開頭。 請注意該 hello **ftyp**，**即時伺服器資訊清單方塊**，和**moov**必須與每個要求，傳送 （依此順序） 的方塊，即使因為必須重新連接 hello 編碼器 hello前一個要求已終止前一個 toohello hello 資料流結尾。 
4. hello 編碼器必須使用區塊的傳輸編碼用於上傳，因為它是不可能 toopredict hello 整個內容長度 hello 即時事件。
5. Hello 事件時，透過傳送嗨最後一個片段之後, hello 編碼器必須依正常程序會結束 hello 區塊傳輸編碼方式 （大部分的 HTTP 用戶端堆疊就會自動處理） 的訊息序列。 hello 編碼器必須等候 hello 服務 tooreturn hello 最終回應程式碼，並再結束 hello 的連接。 
6. hello 編碼器不得使用 hello`Events()`名詞中所述 9.2 中 [1] 到 Media Services 即時擷取的。
7. 如果 hello HTTP POST 要求終止或時間出 TCP 錯誤先前 toohello hello 資料流的結尾，與 hello 編碼器必須發出新的 POST 要求使用新的連接，並遵循 hello 上述需求。 此外，hello 編碼器必須重新傳送嗨先前的兩個 MP4 片段，針對每個追蹤中 hello 資料流，並繼續而不會引進 hello 媒體時間軸中的不一致。 重新傳送嗨最後兩個 MP4 片段，針對每個追蹤，可確保不會遺失任何資料。 換句話說，如果資料流包含音訊和視訊播放軌，hello 目前 POST 要求失敗，hello 編碼器必須重新連接並重新傳送 hello hello 音訊播放軌，如先前傳送成功時，最後兩個片段和 hello 最後兩個片段的hello 視訊音軌，先前已成功傳送，不會遺失任何資料的 tooensure。 hello 編碼器必須維護它重新連線時重新傳送的媒體片段的 「 轉送 」 緩衝區。

## <a name="5-timescale"></a>5.時幅
[[MS SSTR]](https://msdn.microsoft.com/library/ff469518.aspx)說明 hello 用法的時幅**SmoothStreamingMedia** （區段 2.2.2.1）、 **StreamElement** （區段 2.2.2.3）、 **StreamFragmentElement**（區段 2.2.2.6） 和**LiveSMIL** （區段 2.2.7.3.1）。 如果 hello 的時幅值不存在，hello 所使用的預設值為 10,000,000 (10 MHz)。 Hello Smooth Streaming 格式規格不會封鎖其他時間單位值的使用方式，雖然大部分的編碼器實作都會使用此預設值的值 (10 MHz) toogenerate Smooth Streaming 內嵌資料。 到期 toohello [Azure 媒體動態封裝](media-services-dynamic-packaging-overview.md)功能，我們建議您使用 90 KHz 時幅視訊資料流和 44.1 KHz 或 48.1 KHz 音訊資料流。 如果不同的資料流使用不同的時間單位值時，必須先傳送 hello 資料流層級時幅。 如需詳細資訊，請參閱 [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx)。     

## <a name="6-definition-of-stream"></a>6.「資料流」的定義
資料流是 hello 的基本單位中組合實況簡報，即時擷取作業處理資料流的容錯移轉與備援性案例。 「資料流」定義為一個唯一的分散 MP4 位元資料流，其中可能包含單一資料軌或多個資料軌。 完整即時展示檔可能包含一或多個資料流，依據 hello hello 即時編碼器設定。 hello 遵循範例說明使用資料流 toocompose 的各種選項完整實況簡報。

**範例：** 

客戶想 toocreate 即時資料流展示檔包含下列音訊/視訊位元的 hello:

視訊 - 3000 kbps、1500 kbps、750 kbps

音訊 - 128 kbps

### <a name="option-1-all-tracks-in-one-stream"></a>選項 1：一個資料流中所有的資料軌
在此選項中，單一編碼器會產生所有音訊/視訊資料軌，然後將其組合成一個分散的 MP4 位元資料流。 hello 分散的 MP4 bitstream 會透過單一的 HTTP POST 連線傳送。 此範例中有此即時簡報的唯一資料流。

![資料流 - 一個資料軌][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>選項 2：每個資料軌分在不同的資料流中
在此選項，hello 編碼器一首曲目放入每個 MP4 片段 bitstream，，然後再將所有 hello 資料流透過個別 HTTP 連線。 這可透過一或多個編碼器完成。 hello 即時擷取可看到此實況簡報四個資料流所組成。

![資料流 - 分開的資料軌][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>選項 3： 組合成一個資料流與 hello 最低位元速率視訊音軌的音訊播放軌
此選項，在 hello 客戶會選擇 toobundle hello 音訊播放軌與 hello 最低位元速率視訊播放軌中一個片段 MP4 bitstream 和保持 hello 其他兩個視訊音軌，為不同資料流。 

![資料流 - 音訊與視訊資料軌][image4]

### <a name="summary"></a>摘要
此並非詳盡清單，僅列出此範例中部分可用的內嵌選項。 事實上，即時內嵌支援將資料軌以任何組合分組到資料流。 客戶和編碼器廠商可以根據工程的複雜性、編碼器的能力，以及備援與容錯移轉考量，來選擇自己的實作。 不過，在大部分情況下，沒有 hello 整個即時展示檔只有一個音訊播放軌。 因此，它的重要 tooensure hello healthiness hello 的內嵌資料流，包含 hello 音訊播放軌。這項考量通常會導致將 hello 音訊播放軌放在它自己的資料流 （如同選項 2) 或組合與 hello 最低位元速率視訊音軌 （如同選項 3)。 此外，較佳的備援和容錯功能，如傳送 hello 相同的音訊播放軌中兩個不同的資料流 (選項 2 與備援的音訊播放軌) 或使用至少兩部 hello 最低位元速率視訊音軌的音訊在組合在一起 (選項 3 將 hello 音訊播放軌至少兩個視訊資料流） 強烈建議在即時內嵌到 Media Services。

## <a name="7-service-failover"></a>7.服務容錯移轉
指定的即時資料流的 hello 本質，很好的容錯移轉支援是關鍵確保 hello hello 服務可用性。 Media Services 是設計的 toohandle 各種類型的失敗，包括網路錯誤，伺服器錯誤，以及儲存體問題。 中適當的容錯移轉邏輯從 hello 即時編碼器端搭配使用時，客戶就可以達到從 hello 雲端可靠的即時串流服務。

在本節中，我們將討論服務容錯移轉的案例。 在此情況下，hello 失敗發生 hello 服務內的某處，它就會出現網路錯誤。 以下是一些 hello 編碼器的實作來處理服務容錯移轉的建議：

1. 建立 hello TCP 連接使用 10 秒逾時。 如果嘗試 tooestablish hello 連接費時超過 10 秒，中止 hello 作業，並再試一次。 
2. 使用簡短的逾時，傳送嗨 HTTP 要求訊息區塊 （chunk）。 如果 hello 目標 MP4 片段持續時間 N 秒，請使用 N 之間 2 N 秒; 傳送逾時例如，如果 hello MP4 片段持續時間是 6 秒，使用 6 too12 秒的逾時。 如果發生逾時，重設 hello 連線、 開啟新的連接，以及繼續資料流將內嵌 hello 新的連接。 
3. 維護具有 hello 最後兩個片段的每個追蹤記錄已成功且完全地傳送 toohello 服務的循環緩衝區。  如果 hello 資料流的 HTTP POST 要求已終止，或逾時之前的 toohello hello 資料流結尾，開啟新的連接和開始另一個 HTTP POST 要求，重新傳送嗨資料流標頭、 重新傳送嗨最後兩個片段，針對每個追蹤，並繼續 hello 資料流，而不導入 hello 媒體時間軸中的不一致。 這會減少 hello 可能發生資料遺失。
4. 我們建議的 hello 編碼器不會限制 hello 重試 tooestablish 連線的數目或繼續之後就會發生 TCP 錯誤資料流。
5. 發生 TCP 錯誤後：
  
    a. 必須先關閉 hello 目前的連接，並為新的 HTTP POST 要求，必須建立新的連接。

    b. 新 HTTP POST URL 必須是的 hello hello 與 hello 初始 POST URL 相同。
  
    c. hello 新 HTTP POST 必須包含資料流標頭 (**ftyp**，**即時伺服器資訊清單方塊**，和**moov**方塊)，會在 hello 相同 toohello 資料流標頭初始 POST。
  
    d. 必須重新傳送 hello 傳送每個追蹤記錄的最後兩個片段，以及資料流必須繼續而不會引進 hello 媒體時間軸中的不一致。 hello MP4 片段時間戳記必須持續增加，甚至可跨 HTTP POST 要求。
6. 如果資料不會傳送 hello MP4 片段持續時間與 parallel 速率 hello 編碼器應該結束 hello HTTP POST 要求。  不會傳送資料的 HTTP POST 要求可以防止媒體服務快速地中斷連線的服務更新的 hello 事件中的 hello 編碼器。 基於這個理由，hello 的 HTTP POST 疏鬆 （在廣告訊號） 追蹤記錄應存留較短，傳送嗨疏鬆片段時，立即終止。

## <a name="8-encoder-failover"></a>8.編碼器容錯移轉
編碼器的容錯移轉是 hello toobe 定址所需要的端對端的即時資料流傳送的容錯移轉案例的第二個型別。 在此案例中，在 hello 編碼器端發生 hello 錯誤狀況。 

![編碼器容錯移轉][image5]

當編碼器的容錯移轉發生時從 hello 即時擷取端點適用於下列期望的 hello:

1. 新的編碼程式執行個體應該建立 toocontinue 串流，hello 圖表 （資料流 3000 k 視訊虛線） 中所示。
2. hello hello 的形式使用必須 hello 相同 URL 為 HTTP POST 要求新的編碼器失敗執行個體。
3. hello 新的編碼器 POST 要求都必須包含 hello 相同分散 MP4 標題方塊為 hello 失敗的執行個體。
4. hello 相同實況簡報 toogenerate 同步處理音訊/視訊樣本對齊的片段界限，hello 新的編碼器，必須正確地同步與所有其他執行的編碼器。
5. hello 新的資料流必須在語意上與使用 hello 先前的資料流，並且可交換 hello 標頭或片段層級。
6. hello 新的編碼器應該嘗試 toominimize 資料遺失。 hello`fragment_absolute_time`和`fragment_index`的媒體片段應增加從上次停止 hello 編碼器 hello 點。 hello`fragment_absolute_time`和`fragment_index`應增加持續的方式，但它是允許 toointroduce 不一致，如有必要。 Media Services 會忽略它已收到並處理片段，因此它是較佳 tooerr 重送片段比 toointroduce 中斷點 hello 媒體時間軸中的 hello 端。 

## <a name="9-encoder-redundancy"></a>9.編碼器備援
針對特定重大即時事件，視需要更高可用性和品質使用經驗，我們建議您使用主動-主動備援編碼程式 tooachieve 無縫式容錯移轉，且不遺失資料。

![編碼器備援][image6]

此圖所示，兩個群組的編碼器推送每個資料流的兩個的複本同時 hello 即時服務。 此設定之所以受到支援，是因為媒體服務能夠根據資料流 ID 與片段時間戳記篩選出重複的片段。 hello 產生即時資料流，並封存不是 hello 最佳可能彙總來自 hello 兩個來源的單一複本 hello 的所有資料流。 比方說，假設極端案例中，只要一個編碼器 （不需要 toobe hello 同一個） 執行在任何給定時間點的時間，每個資料流 hello 產生 hello 服務即時資料流是連續不會遺失資料。 

此案例中的 hello 需求幾乎相同 hello 當做 hello 需求 hello 「 編碼器的容錯移轉 」 案例中，與 hello 例外狀況在 hello 執行編碼器的 hello 第二個集合的相同的時間 hello 主要編碼器。

## <a name="10-service-redundancy"></a>10.服務備援
備援性高的通用散發，有時候您必須要能夠跨地區備份 toohandle 地區災害。 展開 hello 「 編碼器備援 」 拓樸，客戶可以選擇 toohave 備援服務部署的編碼器 hello 第二個集合會連接到不同區域中。 客戶也可以使用內容傳遞網路提供者 toodeploy 前面 hello 兩個服務部署 tooseamlessly 路由用戶端流量全域流量管理員使用。 hello 編碼器的 hello 需求是 hello 與 hello 「 編碼器備援 」 案例相同。 hello 只例外狀況是編碼器需求 toobe hello 第二組指向不同 tooa 即時內嵌端點。 hello 下圖顯示此安裝程式：

![服務備援][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11.特殊類型的內嵌格式
本章節將討論設計的 toohandle 特定案例的即時擷取格式的特殊類型。

### <a name="sparse-track"></a>疏鬆資料軌
忘即時資料流與豐富型用戶端體驗，通常是必要 tootransmit 時間同步處理的事件或訊號頻外 hello 主要媒體資料。 動態即時廣告插入是其中一個例子。 此類型的事件訊號不同於一般音訊/視訊資料流，因為其疏鬆的本質之故。 換句話說，hello 資料通常不會持續，而且 hello 間隔可以是永久 toopredict 信號。 疏鬆播放軌的 hello 概念是設計的 tooingest 信號廣播頻外的資料。

hello 下列步驟會擷取疏鬆播放軌的建議的實作：

1. 建立個別的分散 MP4 位元資料流，其只包含疏鬆資料軌，但不包含音訊/視訊資料軌。
2. 在 hello**即時伺服器資訊清單中**如第 6 節定義 [1] 中，使用 hello *parentTrackName* hello 父曲目參數 toospecify hello 名稱。如需詳細資訊，請參閱 [1] 的第 4.2.1.2.1.2 節。
3. 在 hello**即時伺服器資訊清單方塊**， **manifestOutput**必須設定得**true**。
4. 指定 hello 疏鬆性質 hello 信號事件，我們建議使用 hello 下列：
   
    a. 在 hello 即時事件 hello 開頭，hello 編碼器會傳送 hello 初始的標題方塊 toohello 服務，可讓 hello 用戶端資訊清單中的 hello 服務 tooregister hello 疏鬆播放軌。
   
    b. 未傳送資料時，hello 編碼器應該結束 hello HTTP POST 要求。 不會傳送資料的長時間執行 HTTP POST 可以防止媒體服務快速地中斷連線的服務更新或伺服器重新開機的 hello 事件中的 hello 編碼器。 在這些情況下，已暫時封鎖 hello 媒體伺服器 hello 通訊端上接收作業中。
   
    c. 在當信號資料不是可用的 hello 期間，hello 編碼器應該關閉 hello HTTP POST 要求。 Hello POST 要求使用中時，應該將資料傳送 hello 編碼器。

    d. 當傳送疏鬆的片段，hello 編碼器可以設定明確的內容長度標頭，如果有的話。

    e. 傳送時具有新的連接疏鬆片段，hello 編碼器應該開始傳送 hello [標題] 方塊中，後面接著 hello 新片段。 這是在容錯移轉會發生介於，案例和 hello 新疏鬆連線正在建立的 tooa 見過 hello 之前疏鬆播放軌的新伺服器。

    f. hello 疏鬆播放軌片段 hello 對應父曲目片段具有相等或更大的時間戳記值進行可用 toohello 用戶端時，會變成可用 toohello 用戶端。 例如，如果 hello 疏鬆片段都有 t 的時間戳記 = 1000，預期的 hello 用戶端觀察 「 視訊 」 （假設 hello 追蹤懷疑 「 視訊 」） 片段時間戳記 1000年或更新版本，才能下載之後 hello 疏鬆片段 t = 1000年。 請注意，hello 實際訊號無法用於 hello 簡報時間軸中的不同位置，為其指定的目的。 在此範例中，它的可能在 hello 疏鬆片段 t = 1000年具有 XML 裝載，也就是將廣告插入的位置時，在幾秒鐘內更新版本。

    g. hello 裝載的疏鬆播放軌片段可以是以不同格式 （例如 XML、 文字或二進位），視 hello 案例而定。

### <a name="redundant-audio-track"></a>備援音訊資料軌
在一般 HTTP 彈性串流處理案例 （例如，Smooth Streaming 或虛線），通常會在 hello 整個簡報中的只有一個音訊播放軌。 不同視訊音軌，有多個的品質等級的 hello 用戶端 toochoose 從錯誤狀況中，如果 hello 擷取包含 hello 音訊播放軌的 hello 資料流已損毀 hello 音訊播放軌時，可以有單一失敗點。 

這個問題，Media Services 支援的 toosolve 即時備援音訊音軌的擷取。 hello 概念是相同的音訊播放軌可以多次傳送不同的資料流中的 hello。 雖然 hello 服務只會註冊 hello 音訊播放軌一次 hello 用戶端資訊清單中，它可作為備援音訊音軌備份擷取音訊的片段，如果 hello 主要音訊音軌有問題。 tooingest 多餘的音訊播放軌 hello 編碼器必須：

1. 建立多個片段 MP4 bitstreams hello 相同的音訊播放軌。 hello 備援音訊音軌必須在語意上與、 以 hello 相同片段時間戳記，並可以互換 hello 標頭和片段層級。
2. 請確定該 hello 「 聲音 」 項目在 hello 即時伺服器資訊清單 (第 6 節中 [1]) 是 hello 相同所有多餘的音訊音軌。

hello 下列實作是多餘的音訊音軌的建議：

1. 讓資料流獨自傳送每個唯一的音訊資料軌。 此外，每個音訊播放軌資料流，其中第二個資料流 hello 只有不同於 hello 先 hello HTTP POST URL 中的 hello 識別碼傳送重複的資料流: {通訊協定}:// {伺服器位址} / {發佈點 path}/Streams({identifier})。
2. 使用個別的資料流 toosend hello 兩個最低視訊位元。 這些資料流皆「應該」包含每個唯一音訊資料軌的複本。例如，當支援多國語言時，這些資料流「應該」包含每種語言的音訊資料軌。
3. 使用不同的伺服器 （編碼器） 執行個體 tooencode 以及傳送 hello 多餘資料流中所述 （1） 和 (2)。 

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
