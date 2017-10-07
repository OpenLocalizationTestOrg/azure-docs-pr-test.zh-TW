---
title: "aaaFilters 和動態的資訊清單 |Microsoft 文件"
description: "本主題描述如何 toocreate 篩選讓您的用戶端能夠使用它們 toostream 特定區段的資料流。 媒體服務會建立動態資訊清單 tooarchive 這個選擇性的資料流。"
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>篩選器與動態資訊清單
從 2.11 版開始，媒體服務可讓您為您資產的 toodefine 篩選器。 這些篩選條件是伺服器端規則，可讓您的客戶 toochoose toodo 等： 播放視訊 （而不是正在播放 hello 整個視訊） 的區段，或指定的音訊和視訊多種客戶的裝置可以處理 （子集而不是所有 hello 多種與相關聯 hello 資產）。 此篩選您的資產會透過封存**動態資訊清單**視訊在您的客戶要求 toostream 時所建立根據指定的篩選器。

本主題將討論常見的案例中使用篩選條件會很有幫助 tooyour 客戶和連結 tootopics 示範 toocreate 如何以程式設計方式篩選 （目前，您可以建立篩選的 REST Api 只能）。

## <a name="overview"></a>概觀
當傳遞您內容的 toocustomers （串流即時事件或 video-on-demand） 您的目標是高品質的視訊 toovarious 裝置在不同的網路狀況下 toodeliver。 此目標沒有 hello 遵循 tooachieve:

* 編碼您的資料流 toomulti 元速率 ([彈性位元速率](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) 視訊資料流 （這會負責品質和網路狀況）， 
* 使用 Media Services[動態封裝](media-services-dynamic-packaging-overview.md)toodynamically 重新封裝您的資料流成不同的通訊協定 （這會負責的資料流不同的裝置上）。 Media Services 支援的下列彈性位元速率串流技術的 hello 傳遞： HTTP Live Streaming (HLS)、 Smooth Streaming 和 MPEG DASH。 

### <a name="manifest-files"></a>資訊清單檔案
當您編碼為彈性位元速率串流，資產**資訊清單**（播放清單） 檔案建立 （hello 檔案是以文字為基礎或以 XML 為基礎）。 hello**資訊清單**檔案包含資料流中繼資料時，例如： 追蹤名稱、 開始和結束時間、 位元速率 （品質）、 追蹤語言、 簡報視窗 （滑動視窗固定持續時間）、 視訊，追蹤類型 （音訊、 視訊或文字）轉碼器 (FourCC)。 也會提供資訊 hello 下一步 可播放視訊片段可用以及它們的位置指示 hello player tooretrieve hello 下一個片段。 片段 （或區段） 是 hello 實際 「 區塊 」 的視訊內容。

資訊清單檔案範例如下： 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>動態資訊清單
有[案例](media-services-dynamic-manifest-overview.md#scenarios)您的用戶端時需要更多的彈性比述 hello 預設資產的資訊清單檔案。 例如：

* 特定的裝置： 傳送 hello 指定多種和/或指定了 only，是使用的 tooplayback hello 裝置所支援的語言曲目 hello （「 轉譯篩選 」） 的內容。 
* 減少 hello 資訊清單 tooshow 子剪輯的即時事件 （「 子剪輯篩選 」）。
* 修剪視訊 （」 修剪視訊 」） 的 hello 開頭。
* 調整簡報視窗 (DVR) 中的順序 tooprovide 有限的 hello 播放程式 （「 調整簡報視窗 」） 中的 hello DVR 視窗長度。

tooachieve 此彈性，Media Services 提供**動態資訊清單**基礎上預先定義的[篩選](media-services-dynamic-manifest-overview.md#filters)。  一旦您定義 hello 篩選器，您的用戶端無法使用它們 toostream 特定轉譯或子剪輯的視訊。 它們會指定篩選器，在 hello 串流 URL。 篩選器可能套用的 tooadaptive 位元速率串流通訊協定支援[動態封裝](media-services-dynamic-packaging-overview.md): HLS、 MPEG-DASH 以及 Smooth Streaming。 例如：

含篩選器的 MPEG DASH URL

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

含篩選器的 Smooth Streaming URL

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


如需有關如何 toodeliver 您的內容和建置串流 Url，請參閱[傳遞內容概觀](media-services-deliver-content-overview.md)。

> [!NOTE]
> 請注意，動態資訊清單沒有不變更 hello 資產 hello 該資產的預設資訊清單。 您的用戶端可以選擇 toorequest，不論篩選的資料流。 
> 
> 

### <a id="filters"></a>篩選器
資產篩選器有兩種： 

* 全域篩選 （套用的 tooany hello Azure Media Services 帳戶中的資產，存留期為 hello 帳戶） 和 
* 本機篩選條件 （只可套用的 tooan 資產的 hello 與篩選已在建立時建立關聯，存留期為 hello 資產）。 

全域和區域的篩選類型具有剛好 hello 相同的屬性。 hello 之間 hello 兩個主要的差異是篩選的哪些案例用於哪種類型是篩選的更適合。 全域篩選通常適用的裝置設定檔 （篩選出） 其中本機篩選條件可以是使用的 tootrim 特定資產。

## <a id="scenarios"></a>常見案例
已提過之前，您也可以在不同的 toovarious 裝置時傳遞您內容的 toocustomers （串流即時事件或 video-on-demand） 您的目標是高品質的視訊 toodeliver 網路狀況。 此外，您可能會有其他對於篩選資產與使用 **動態資訊清單**相關的需求。 hello 下列各節提供不同的篩選案例的簡短概觀。

* 指定音訊和視訊 （而不是與 hello 資產相關聯的所有 hello 轉譯） 可以處理的特定裝置的多種的子集。 
* 播放視訊 （而不是播放 hello 整個視訊） 的區段。
* 調整 DVR 簡報視窗。

## <a name="rendition-filtering"></a>轉譯篩選
您可以選擇 tooencode 您資產 toomultiple 編碼設定檔 （H.264 基準、 H.264 高，AACL，AACH，Dolby Digital Plus） 和多品質個位元。 不過，並非所有的用戶端裝置都支援您所有的資產和位元速率。 例如，較舊的 Android 裝置只支援 H.264 Baseline+AACL。 傳送較高的位元 tooa 裝置無法取得 hello 優點，則會浪費頻寬及裝置的計算。 這類裝置必須解碼所有 hello 指定的資訊，請只 tooscale 它向下顯示。

您可以使用動態資訊清單中，建立裝置設定檔行動裝置，例如 HD/SD 等主控台並加入 hello 追蹤和您想要的品質 toobe 每個設定檔的一部分。

![轉譯篩選範例][renditions2]

在下列範例的 hello，編碼器會是使用的 tooencode （從 180 p too1080p) 七個 ISO mp4 視訊轉譯成的夾層資產。 hello 編碼的資產可以動態封裝到任何下列串流通訊協定的 hello: HLS、 Smooth 和 MPEG DASH。  在 hello 頂端 hello 圖表，顯示的 hello HLS hello 資產的資訊清單與任何篩選條件 （包含所有的七個轉譯）。  在 hello 左下方，會顯示的 hello HLS 資訊清單的 toowhich 名為"ott 」 篩選已套用。 hello"ott 」 篩選條件指定 tooremove 下方 1Mbps，導致 hello 下兩個指定的品質等級被去除 hello 回應中的所有位元。  在 hello 右下 hello HLS 會顯示名為 「 行動 」 篩選已套用的資訊清單 toowhich。 hello 「 行動 」 篩選條件指定 tooremove 多種其中 hello 解析度大於 720p，導致 hello 被去除兩個 1080p 轉譯中。

![轉譯篩選][renditions1]

## <a name="removing-language-tracks"></a>移除語言資料軌
您的資產可能包含多個音訊語言，例如英文、西班牙文、法文等。通常，hello Player SDK 管理員預設音訊播放軌的選取範圍，而且可用的音訊會追蹤每個使用者選取項目。 它很困難 toodevelop 這類 Player Sdk，它需要跨裝置特定的播放器架構的不同實作。 此外，在某些平台，播放器應用程式開發介面會受到限制，而且不包含使用者無法在其中選取或變更 hello 音訊播放軌的音訊的選取範圍功能。與資產的篩選器，您可以藉由建立只包含所要的音訊語言的篩選控制 hello 行為。

![語言資料軌篩選][language_filter]

## <a name="trimming-start-of-an-asset"></a>修剪資產開頭
在大多數的即時資料流事件，運算子會執行某些測試 hello 實際事件之前。 例如，它們可能包含如下 hello 開頭 hello 事件之前的候選影片:"程式將立即開始 」。 如果 hello 程式即將保存，hello 測試和平板電腦的資料也封存，並將包含在 hello 簡報中。 不過，這項資訊不應該顯示 toohello 用戶端。 與動態資訊清單中，您可以建立開始時間篩選器，並移除 hello 資訊清單中的 hello 的不必要資料。

![開始修剪][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>從即時封存中建立子剪輯 (檢視)
許多即時事件的執行時間長，且即時封存可能包括多個事件。 Hello 即時事件結束廣播者可能會想出 hello toobreak 之後即時封存到邏輯程式啟動和停止序列。 然後分別處理 hello 即時封存和不建立個別的資產 （這不會收到 hello 現有快取的片段優點 hello Cdn 中） 的 post 不發行這些虛擬程式。 這類虛擬程式 （子剪輯） 的範例是 football 或籃球遊戲、 hello innings 棒球中的 hello 季或個別的下午奧林匹亞運動會程式的事件。

與動態資訊清單中，您可以建立使用開始/結束時間篩選和建立您的即時封存的 hello 頂端虛擬檢視。 

![子剪輯篩選][subclip_filter]

已篩選的資產：

![滑動][skiing]

## <a name="adjusting-presentation-window-dvr"></a>調整簡報視窗 (DVR)
目前，Azure Media Services 提供循環的封存位置設定 hello 持續時間介於 5 分鐘-25 個小時。 資訊清單的篩選，可以使用的 toocreate 循環的 DVR 視窗是透過 hello 頂端 hello 封存，但不會刪除媒體。 有許多案例中，廣播者 tooprovide 會隨之移動 hello live 邊緣和相同的時間讓更大的封存視窗保持在 hello 有限的 DVR 視窗。 廣播者可能想 toouse hello 資料超出 hello DVR 視窗 toohighlight 剪輯，或 he\she 希望 tooprovide 不同的 DVR 視窗適用於不同的裝置。 例如，大部分的 hello 行動裝置不處理大的 DVR 視窗 （如桌面用戶端可以有 2 分鐘 DVR 視窗適用於行動裝置和 1 小時）。

![DVR 視窗][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>調整 LiveBackoff (即時位置)
資訊清單的篩選可以是使用的 tooremove 幾秒鐘的時間從 hello 即時邊緣即時計劃。 這可讓廣播者 toowatch hello 簡報 hello 預覽發行集上的點和 hello 檢視器收到 hello (通常是備份-off 30 秒) 的資料流之前，先建立公告插入點。 廣播者可以再推送這些公告 tootheir 用戶端架構中時間 tooreceived 和處理序 hello 資訊，再行 hello 公告機會。

此外 toohello 廣告支援、 LiveBackoff 可用於調整用戶端即時的下載位置，讓用戶端漂移，並叫用 hello 即時邊緣時就可以從伺服器，而非收到 404 或 412 HTTP 錯誤訊息，還是取得片段。

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>將多個規則結合成單一篩選器
您可以將多個篩選規則結合成單一篩選器。 例如，您可以定義從即時封存 tooremove 範圍規則候選影片，並也篩選 可用的位元。 篩選規則 hello end 結果是這些規則的 hello 組合 （交集只）。

![多個規則][multiple-rules]

## <a name="create-filters-programmatically"></a>以程式設計方式建立篩選器
下列主題中的 hello 討論媒體服務實體的相關的 toofilters。 hello 主題也會顯示如何 tooprogrammatically 建立篩選器。  

[使用 REST API 建立篩選器](media-services-rest-dynamic-manifest.md)。

## <a name="combining-multiple-filters-filter-composition"></a>結合多個篩選條件 (篩選器組合)
您也可以將多個篩選條件結合成單一 URL。 

hello 下列案例示範為什麼您可能會想 toocombine 篩選：

1. 您需要 toofilter 您視訊品質的 Android 或 （在順序 toolimit 視訊品質） iPAD 等行動裝置。 tooremove hello 不想要的品質，您會建立全域的篩選條件適用於裝置設定檔。 全域篩選如上面所述，可用於所有的資產在 hello 相同的媒體服務帳戶不需要任何進一步的關聯。 
2. 您也想 tootrim hello 開始和結束時間的資產。 tooachieve，您會建立本機篩選條件，並設定 hello 開始/結束時間。 
3. 您想要的這些篩選器 toocombine （組合不需要 tooadd 品質篩選 toohello 調整篩選器，它會使篩選使用情況困難）。

toocombine 篩選，您需要 tooset hello 篩選器名稱 toohello 資訊清單/播放清單 URL，並以分號分隔。 讓我們假設您有篩選，名為*MyMobileDevice*篩選品質，而且您有另一個名為*MyStartTime* tooset 特定開始時間。 您可以將它們結合如下：

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

您可以結合向上 too3 篩選器。 

如需詳細資訊，請參閱 [此](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) 部落格。

## <a name="know-issues-and-limitations"></a>已知問題與限制
* 動態資訊清單會在 GOP 界限 (主要畫面格) 中運作，因此修剪後能夠有精確的 GOP。 
* 您可以讓本機和全域篩選器使用相同的篩選器名稱。 請注意，本機篩選有較高的優先權，會覆寫全域篩選器。
* 如果您更新篩選器，就可以在資料流端點 toorefresh hello 規則 too2 分鐘。 如果 hello 內容處理使用部分的篩選器 （快取和 proxy 和 CDN 中快取），更新這些篩選器導致播放失敗。 它是在更新 hello 篩選之後，建議 tooclear hello 快取。 如果這個選項無法執行，請考慮使用不同的篩選器。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[傳遞內容 tooCustomers 概觀](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
