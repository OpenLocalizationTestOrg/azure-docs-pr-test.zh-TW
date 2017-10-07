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
# <a name="filters-and-dynamic-manifests"></a><span data-ttu-id="a7e7f-104">篩選器與動態資訊清單</span><span class="sxs-lookup"><span data-stu-id="a7e7f-104">Filters and dynamic manifests</span></span>
<span data-ttu-id="a7e7f-105">從 2.11 版開始，媒體服務可讓您為您資產的 toodefine 篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-105">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="a7e7f-106">這些篩選條件是伺服器端規則，可讓您的客戶 toochoose toodo 等： 播放視訊 （而不是正在播放 hello 整個視訊） 的區段，或指定的音訊和視訊多種客戶的裝置可以處理 （子集而不是所有 hello 多種與相關聯 hello 資產）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-106">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="a7e7f-107">此篩選您的資產會透過封存**動態資訊清單**視訊在您的客戶要求 toostream 時所建立根據指定的篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-107">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="a7e7f-108">本主題將討論常見的案例中使用篩選條件會很有幫助 tooyour 客戶和連結 tootopics 示範 toocreate 如何以程式設計方式篩選 （目前，您可以建立篩選的 REST Api 只能）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-108">This topics discusses common scenarios in which using filters would be very beneficial tooyour customers and links tootopics that demonstrate how toocreate filters programmatically (currently, you can create filters with REST APIs only).</span></span>

## <a name="overview"></a><span data-ttu-id="a7e7f-109">概觀</span><span class="sxs-lookup"><span data-stu-id="a7e7f-109">Overview</span></span>
<span data-ttu-id="a7e7f-110">當傳遞您內容的 toocustomers （串流即時事件或 video-on-demand） 您的目標是高品質的視訊 toovarious 裝置在不同的網路狀況下 toodeliver。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-110">When delivering your content toocustomers (streaming live events or video-on-demand) your goal is toodeliver a high quality video toovarious devices under different network conditions.</span></span> <span data-ttu-id="a7e7f-111">此目標沒有 hello 遵循 tooachieve:</span><span class="sxs-lookup"><span data-stu-id="a7e7f-111">tooachieve this goal do hello following:</span></span>

* <span data-ttu-id="a7e7f-112">編碼您的資料流 toomulti 元速率 ([彈性位元速率](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) 視訊資料流 （這會負責品質和網路狀況），</span><span class="sxs-lookup"><span data-stu-id="a7e7f-112">encode your stream toomulti-bitrate ([adaptive bitrate](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) video stream (this will take care of quality and network conditions) and</span></span> 
* <span data-ttu-id="a7e7f-113">使用 Media Services[動態封裝](media-services-dynamic-packaging-overview.md)toodynamically 重新封裝您的資料流成不同的通訊協定 （這會負責的資料流不同的裝置上）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-113">use Media Services [Dynamic Packaging](media-services-dynamic-packaging-overview.md) toodynamically re-package your stream into different protocols (this will take care of streaming on different devices).</span></span> <span data-ttu-id="a7e7f-114">Media Services 支援的下列彈性位元速率串流技術的 hello 傳遞： HTTP Live Streaming (HLS)、 Smooth Streaming 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-114">Media Services supports delivery of hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span> 

### <a name="manifest-files"></a><span data-ttu-id="a7e7f-115">資訊清單檔案</span><span class="sxs-lookup"><span data-stu-id="a7e7f-115">Manifest files</span></span>
<span data-ttu-id="a7e7f-116">當您編碼為彈性位元速率串流，資產**資訊清單**（播放清單） 檔案建立 （hello 檔案是以文字為基礎或以 XML 為基礎）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-116">When you encode an asset for adaptive bitrate streaming, a **manifest** (playlist) file is created (hello file is text-based or XML-based).</span></span> <span data-ttu-id="a7e7f-117">hello**資訊清單**檔案包含資料流中繼資料時，例如： 追蹤名稱、 開始和結束時間、 位元速率 （品質）、 追蹤語言、 簡報視窗 （滑動視窗固定持續時間）、 視訊，追蹤類型 （音訊、 視訊或文字）轉碼器 (FourCC)。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-117">hello **manifest** file includes streaming metadata such as: track type (audio, video, or text), track name, start and end time, bitrate (qualities), track languages, presentation window (sliding window of fixed duration), video codec (FourCC).</span></span> <span data-ttu-id="a7e7f-118">也會提供資訊 hello 下一步 可播放視訊片段可用以及它們的位置指示 hello player tooretrieve hello 下一個片段。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-118">It also instructs hello player tooretrieve hello next fragment by providing information about hello next playable video fragments available and their location.</span></span> <span data-ttu-id="a7e7f-119">片段 （或區段） 是 hello 實際 「 區塊 」 的視訊內容。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-119">Fragments (or segments) are hello actual “chunks” of a video content.</span></span>

<span data-ttu-id="a7e7f-120">資訊清單檔案範例如下：</span><span class="sxs-lookup"><span data-stu-id="a7e7f-120">Here is an example of a manifest file:</span></span> 

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

### <a name="dynamic-manifests"></a><span data-ttu-id="a7e7f-121">動態資訊清單</span><span class="sxs-lookup"><span data-stu-id="a7e7f-121">Dynamic manifests</span></span>
<span data-ttu-id="a7e7f-122">有[案例](media-services-dynamic-manifest-overview.md#scenarios)您的用戶端時需要更多的彈性比述 hello 預設資產的資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-122">There are [scenarios](media-services-dynamic-manifest-overview.md#scenarios) when your client needs more flexibility than what's described in hello default asset's manifest file.</span></span> <span data-ttu-id="a7e7f-123">例如：</span><span class="sxs-lookup"><span data-stu-id="a7e7f-123">For example:</span></span>

* <span data-ttu-id="a7e7f-124">特定的裝置： 傳送 hello 指定多種和/或指定了 only，是使用的 tooplayback hello 裝置所支援的語言曲目 hello （「 轉譯篩選 」） 的內容。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-124">Device specific: deliver only hello specified renditions and\or specified language tracks that are supported by hello device that is used tooplayback hello content ("rendition filtering").</span></span> 
* <span data-ttu-id="a7e7f-125">減少 hello 資訊清單 tooshow 子剪輯的即時事件 （「 子剪輯篩選 」）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-125">Reduce hello manifest tooshow a sub-clip of a live event ("sub-clip filtering").</span></span>
* <span data-ttu-id="a7e7f-126">修剪視訊 （」 修剪視訊 」） 的 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-126">Trim hello start of a video ("trimming a video").</span></span>
* <span data-ttu-id="a7e7f-127">調整簡報視窗 (DVR) 中的順序 tooprovide 有限的 hello 播放程式 （「 調整簡報視窗 」） 中的 hello DVR 視窗長度。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-127">Adjust Presentation Window (DVR) in order tooprovide a limited length of hello DVR window in hello player ("adjusting presentation window") .</span></span>

<span data-ttu-id="a7e7f-128">tooachieve 此彈性，Media Services 提供**動態資訊清單**基礎上預先定義的[篩選](media-services-dynamic-manifest-overview.md#filters)。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-128">tooachieve this flexibility, Media Services offers **Dynamic Manifests** based on pre-defined [filters](media-services-dynamic-manifest-overview.md#filters).</span></span>  <span data-ttu-id="a7e7f-129">一旦您定義 hello 篩選器，您的用戶端無法使用它們 toostream 特定轉譯或子剪輯的視訊。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-129">Once you define hello filters, your clients could use them toostream a specific rendition or sub-clips of your video.</span></span> <span data-ttu-id="a7e7f-130">它們會指定篩選器，在 hello 串流 URL。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-130">They would specify filter(s) in hello streaming URL.</span></span> <span data-ttu-id="a7e7f-131">篩選器可能套用的 tooadaptive 位元速率串流通訊協定支援[動態封裝](media-services-dynamic-packaging-overview.md): HLS、 MPEG-DASH 以及 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-131">Filters could be applied tooadaptive bitrate streaming protocols supported by [Dynamic Packaging](media-services-dynamic-packaging-overview.md): HLS, MPEG-DASH, and Smooth Streaming.</span></span> <span data-ttu-id="a7e7f-132">例如：</span><span class="sxs-lookup"><span data-stu-id="a7e7f-132">For example:</span></span>

<span data-ttu-id="a7e7f-133">含篩選器的 MPEG DASH URL</span><span class="sxs-lookup"><span data-stu-id="a7e7f-133">MPEG DASH URL with filter</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

<span data-ttu-id="a7e7f-134">含篩選器的 Smooth Streaming URL</span><span class="sxs-lookup"><span data-stu-id="a7e7f-134">Smooth Streaming URL with filter</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


<span data-ttu-id="a7e7f-135">如需有關如何 toodeliver 您的內容和建置串流 Url，請參閱[傳遞內容概觀](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-135">For more information about how toodeliver your content and build streaming URLs, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a7e7f-136">請注意，動態資訊清單沒有不變更 hello 資產 hello 該資產的預設資訊清單。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-136">Note that Dynamic Manifests do not change hello asset and hello default manifest for that asset.</span></span> <span data-ttu-id="a7e7f-137">您的用戶端可以選擇 toorequest，不論篩選的資料流。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-137">Your client can choose toorequest a stream with or without filters.</span></span> 
> 
> 

### <span data-ttu-id="a7e7f-138"><a id="filters"></a>篩選器</span><span class="sxs-lookup"><span data-stu-id="a7e7f-138"><a id="filters"></a>Filters</span></span>
<span data-ttu-id="a7e7f-139">資產篩選器有兩種：</span><span class="sxs-lookup"><span data-stu-id="a7e7f-139">There are two types of asset filters:</span></span> 

* <span data-ttu-id="a7e7f-140">全域篩選 （套用的 tooany hello Azure Media Services 帳戶中的資產，存留期為 hello 帳戶） 和</span><span class="sxs-lookup"><span data-stu-id="a7e7f-140">Global filters (can be applied tooany asset in hello Azure Media Services account, have a lifetime of hello account) and</span></span> 
* <span data-ttu-id="a7e7f-141">本機篩選條件 （只可套用的 tooan 資產的 hello 與篩選已在建立時建立關聯，存留期為 hello 資產）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-141">Local filters (can only be applied tooan asset with which hello filter was associated upon creation, have a lifetime of hello asset).</span></span> 

<span data-ttu-id="a7e7f-142">全域和區域的篩選類型具有剛好 hello 相同的屬性。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-142">Global and local filter types have exactly hello same properties.</span></span> <span data-ttu-id="a7e7f-143">hello 之間 hello 兩個主要的差異是篩選的哪些案例用於哪種類型是篩選的更適合。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-143">hello main difference between hello two is for which scenarios what type of a filer is more suitable.</span></span> <span data-ttu-id="a7e7f-144">全域篩選通常適用的裝置設定檔 （篩選出） 其中本機篩選條件可以是使用的 tootrim 特定資產。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-144">Global filters are generally suitable for device profiles (rendition filtering) where local filters could be used tootrim a specific asset.</span></span>

## <span data-ttu-id="a7e7f-145"><a id="scenarios"></a>常見案例</span><span class="sxs-lookup"><span data-stu-id="a7e7f-145"><a id="scenarios"></a>Common scenarios</span></span>
<span data-ttu-id="a7e7f-146">已提過之前，您也可以在不同的 toovarious 裝置時傳遞您內容的 toocustomers （串流即時事件或 video-on-demand） 您的目標是高品質的視訊 toodeliver 網路狀況。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-146">As was mentioned before, when delivering your content toocustomers (streaming live events or video-on-demand) your goal is toodeliver a high quality video toovarious devices under different network conditions.</span></span> <span data-ttu-id="a7e7f-147">此外，您可能會有其他對於篩選資產與使用 **動態資訊清單**相關的需求。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-147">In addition, your might have other requirements that involve filtering your assets and using of **Dynamic Manifest**s.</span></span> <span data-ttu-id="a7e7f-148">hello 下列各節提供不同的篩選案例的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-148">hello following sections give a short overview of different filtering scenarios.</span></span>

* <span data-ttu-id="a7e7f-149">指定音訊和視訊 （而不是與 hello 資產相關聯的所有 hello 轉譯） 可以處理的特定裝置的多種的子集。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-149">Specify only a subset of audio and video renditions that certain devices can handle (instead of all hello renditions that are associated with hello asset).</span></span> 
* <span data-ttu-id="a7e7f-150">播放視訊 （而不是播放 hello 整個視訊） 的區段。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-150">Playing back only a section of a video (instead of playing hello whole video).</span></span>
* <span data-ttu-id="a7e7f-151">調整 DVR 簡報視窗。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-151">Adjust DVR presentation window.</span></span>

## <a name="rendition-filtering"></a><span data-ttu-id="a7e7f-152">轉譯篩選</span><span class="sxs-lookup"><span data-stu-id="a7e7f-152">Rendition filtering</span></span>
<span data-ttu-id="a7e7f-153">您可以選擇 tooencode 您資產 toomultiple 編碼設定檔 （H.264 基準、 H.264 高，AACL，AACH，Dolby Digital Plus） 和多品質個位元。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-153">You may choose tooencode your asset toomultiple encoding profiles (H.264 Baseline, H.264 High, AACL, AACH, Dolby Digital Plus) and multiple quality bitrates.</span></span> <span data-ttu-id="a7e7f-154">不過，並非所有的用戶端裝置都支援您所有的資產和位元速率。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-154">However, not all client devices will support all your asset's profiles and bitrates.</span></span> <span data-ttu-id="a7e7f-155">例如，較舊的 Android 裝置只支援 H.264 Baseline+AACL。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-155">For example, older Android devices only supports H.264 Baseline+AACL.</span></span> <span data-ttu-id="a7e7f-156">傳送較高的位元 tooa 裝置無法取得 hello 優點，則會浪費頻寬及裝置的計算。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-156">Sending higher bitrates tooa device which cannot get hello benefits, wastes bandwidth and device computation.</span></span> <span data-ttu-id="a7e7f-157">這類裝置必須解碼所有 hello 指定的資訊，請只 tooscale 它向下顯示。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-157">Such device must decode all hello given information, only tooscale it down for display.</span></span>

<span data-ttu-id="a7e7f-158">您可以使用動態資訊清單中，建立裝置設定檔行動裝置，例如 HD/SD 等主控台並加入 hello 追蹤和您想要的品質 toobe 每個設定檔的一部分。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-158">With Dynamic Manifest, you can create device profiles such as mobile, console, HD/SD, etc. and include hello tracks and qualities which you want toobe a part of each profile.</span></span>

![轉譯篩選範例][renditions2]

<span data-ttu-id="a7e7f-160">在下列範例的 hello，編碼器會是使用的 tooencode （從 180 p too1080p) 七個 ISO mp4 視訊轉譯成的夾層資產。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-160">In hello following example, an encoder was used tooencode a mezzanine asset into seven ISO MP4s video renditions (from 180p too1080p).</span></span> <span data-ttu-id="a7e7f-161">hello 編碼的資產可以動態封裝到任何下列串流通訊協定的 hello: HLS、 Smooth 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-161">hello encoded asset can be dynamically packaged into any of hello following streaming protocols: HLS, Smooth, and MPEG DASH.</span></span>  <span data-ttu-id="a7e7f-162">在 hello 頂端 hello 圖表，顯示的 hello HLS hello 資產的資訊清單與任何篩選條件 （包含所有的七個轉譯）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-162">At hello top of hello diagram, hello HLS manifest for hello asset with no filters is shown (it contains all seven renditions).</span></span>  <span data-ttu-id="a7e7f-163">在 hello 左下方，會顯示的 hello HLS 資訊清單的 toowhich 名為"ott 」 篩選已套用。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-163">In hello bottom left, hello HLS manifest toowhich a filter named "ott" was applied is shown.</span></span> <span data-ttu-id="a7e7f-164">hello"ott 」 篩選條件指定 tooremove 下方 1Mbps，導致 hello 下兩個指定的品質等級被去除 hello 回應中的所有位元。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-164">hello "ott" filter specifies tooremove all bitrates below 1Mbps, which resulted in hello bottom two quality levels being stripped off in hello response.</span></span>  <span data-ttu-id="a7e7f-165">在 hello 右下 hello HLS 會顯示名為 「 行動 」 篩選已套用的資訊清單 toowhich。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-165">In hello bottom right,   hello HLS manifest toowhich a filter named "mobile" was applied is shown.</span></span> <span data-ttu-id="a7e7f-166">hello 「 行動 」 篩選條件指定 tooremove 多種其中 hello 解析度大於 720p，導致 hello 被去除兩個 1080p 轉譯中。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-166">hello "mobile" filter specifies tooremove renditions where hello resolution is larger than 720p, which resulted in hello two 1080p renditions being stripped off.</span></span>

![轉譯篩選][renditions1]

## <a name="removing-language-tracks"></a><span data-ttu-id="a7e7f-168">移除語言資料軌</span><span class="sxs-lookup"><span data-stu-id="a7e7f-168">Removing language tracks</span></span>
<span data-ttu-id="a7e7f-169">您的資產可能包含多個音訊語言，例如英文、西班牙文、法文等。通常，hello Player SDK 管理員預設音訊播放軌的選取範圍，而且可用的音訊會追蹤每個使用者選取項目。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-169">Your assets might include multiple audio languages such as English, Spanish, French, etc. Usually, hello Player SDK managers default audio track selection and available audio tracks per user selection.</span></span> <span data-ttu-id="a7e7f-170">它很困難 toodevelop 這類 Player Sdk，它需要跨裝置特定的播放器架構的不同實作。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-170">It is challenging toodevelop such Player SDKs, it requires different implementations across device-specific player-frameworks.</span></span> <span data-ttu-id="a7e7f-171">此外，在某些平台，播放器應用程式開發介面會受到限制，而且不包含使用者無法在其中選取或變更 hello 音訊播放軌的音訊的選取範圍功能。與資產的篩選器，您可以藉由建立只包含所要的音訊語言的篩選控制 hello 行為。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-171">Also, on some platforms, Player APIs are limited and do not include audio selection feature where users cannot select or change hello default audio track. With asset filters, you can control hello behavior by creating filters that only include desired audio languages.</span></span>

![語言資料軌篩選][language_filter]

## <a name="trimming-start-of-an-asset"></a><span data-ttu-id="a7e7f-173">修剪資產開頭</span><span class="sxs-lookup"><span data-stu-id="a7e7f-173">Trimming start of an asset</span></span>
<span data-ttu-id="a7e7f-174">在大多數的即時資料流事件，運算子會執行某些測試 hello 實際事件之前。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-174">In most live streaming events, operators run some tests before hello actual event.</span></span> <span data-ttu-id="a7e7f-175">例如，它們可能包含如下 hello 開頭 hello 事件之前的候選影片:"程式將立即開始 」。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-175">For example, they might include a slate like this before hello start of hello event: "Program will begin momentarily".</span></span> <span data-ttu-id="a7e7f-176">如果 hello 程式即將保存，hello 測試和平板電腦的資料也封存，並將包含在 hello 簡報中。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-176">If hello program is archiving, hello test and slate data are also archived and will be included in hello presentation.</span></span> <span data-ttu-id="a7e7f-177">不過，這項資訊不應該顯示 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-177">However, this information should not be shown toohello clients.</span></span> <span data-ttu-id="a7e7f-178">與動態資訊清單中，您可以建立開始時間篩選器，並移除 hello 資訊清單中的 hello 的不必要資料。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-178">With Dynamic Manifest, you can create a start time filter and remove hello unwanted data from hello manifest.</span></span>

![開始修剪][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a><span data-ttu-id="a7e7f-180">從即時封存中建立子剪輯 (檢視)</span><span class="sxs-lookup"><span data-stu-id="a7e7f-180">Creating sub-clips (views) from a live archive</span></span>
<span data-ttu-id="a7e7f-181">許多即時事件的執行時間長，且即時封存可能包括多個事件。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-181">Many live events are long running and live archive might include multiple events.</span></span> <span data-ttu-id="a7e7f-182">Hello 即時事件結束廣播者可能會想出 hello toobreak 之後即時封存到邏輯程式啟動和停止序列。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-182">After hello live event ends broadcasters may want toobreak up hello live archive into logical program start and stop sequences.</span></span> <span data-ttu-id="a7e7f-183">然後分別處理 hello 即時封存和不建立個別的資產 （這不會收到 hello 現有快取的片段優點 hello Cdn 中） 的 post 不發行這些虛擬程式。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-183">Then, publish these virtual programs separately without post processing hello live archive and not creating separate assets (which will not get benefit of hello existing cached fragments in hello CDNs).</span></span> <span data-ttu-id="a7e7f-184">這類虛擬程式 （子剪輯） 的範例是 football 或籃球遊戲、 hello innings 棒球中的 hello 季或個別的下午奧林匹亞運動會程式的事件。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-184">Examples of such virtual programs (sub-clips) are hello quarters of a football or basketball game, hello innings in baseball, or individual events of an afternoon of Olympics program.</span></span>

<span data-ttu-id="a7e7f-185">與動態資訊清單中，您可以建立使用開始/結束時間篩選和建立您的即時封存的 hello 頂端虛擬檢視。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-185">With Dynamic Manifest, you can create filters using start/end times and create virtual views over hello top of your live archive.</span></span> 

![子剪輯篩選][subclip_filter]

<span data-ttu-id="a7e7f-187">已篩選的資產：</span><span class="sxs-lookup"><span data-stu-id="a7e7f-187">Filtered Asset:</span></span>

![滑動][skiing]

## <a name="adjusting-presentation-window-dvr"></a><span data-ttu-id="a7e7f-189">調整簡報視窗 (DVR)</span><span class="sxs-lookup"><span data-stu-id="a7e7f-189">Adjusting Presentation Window (DVR)</span></span>
<span data-ttu-id="a7e7f-190">目前，Azure Media Services 提供循環的封存位置設定 hello 持續時間介於 5 分鐘-25 個小時。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-190">Currently, Azure Media Services offers circular archive where hello duration can be configured between 5 minutes - 25 hours.</span></span> <span data-ttu-id="a7e7f-191">資訊清單的篩選，可以使用的 toocreate 循環的 DVR 視窗是透過 hello 頂端 hello 封存，但不會刪除媒體。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-191">Manifest filtering can be used toocreate a rolling DVR window over hello top of hello archive, without deleting media.</span></span> <span data-ttu-id="a7e7f-192">有許多案例中，廣播者 tooprovide 會隨之移動 hello live 邊緣和相同的時間讓更大的封存視窗保持在 hello 有限的 DVR 視窗。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-192">There are many scenarios where broadcasters want tooprovide a limited DVR window which moves with hello live edge and at hello same time keep a bigger archiving window.</span></span> <span data-ttu-id="a7e7f-193">廣播者可能想 toouse hello 資料超出 hello DVR 視窗 toohighlight 剪輯，或 he\she 希望 tooprovide 不同的 DVR 視窗適用於不同的裝置。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-193">A broadcaster may want toouse hello data that is out of hello DVR window toohighlight clips, or he\she may want tooprovide different DVR windows for different devices.</span></span> <span data-ttu-id="a7e7f-194">例如，大部分的 hello 行動裝置不處理大的 DVR 視窗 （如桌面用戶端可以有 2 分鐘 DVR 視窗適用於行動裝置和 1 小時）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-194">For example, most of hello mobile devices don’t handle big DVR windows (you can have a 2 minute DVR window for mobile devices and 1 hour for desktop clients).</span></span>

![DVR 視窗][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a><span data-ttu-id="a7e7f-196">調整 LiveBackoff (即時位置)</span><span class="sxs-lookup"><span data-stu-id="a7e7f-196">Adjusting LiveBackoff (live position)</span></span>
<span data-ttu-id="a7e7f-197">資訊清單的篩選可以是使用的 tooremove 幾秒鐘的時間從 hello 即時邊緣即時計劃。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-197">Manifest filtering can be used tooremove several seconds from hello live edge of a live program.</span></span> <span data-ttu-id="a7e7f-198">這可讓廣播者 toowatch hello 簡報 hello 預覽發行集上的點和 hello 檢視器收到 hello (通常是備份-off 30 秒) 的資料流之前，先建立公告插入點。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-198">This allows broadcasters toowatch hello presentation on hello preview publication point and create advertisement insertion points before hello viewers receive hello stream (usually backed-off by 30 seconds).</span></span> <span data-ttu-id="a7e7f-199">廣播者可以再推送這些公告 tootheir 用戶端架構中時間 tooreceived 和處理序 hello 資訊，再行 hello 公告機會。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-199">Broadcasters can then push these advertisements tootheir client frameworks in time for them tooreceived and process hello information before hello advertisement opportunity.</span></span>

<span data-ttu-id="a7e7f-200">此外 toohello 廣告支援、 LiveBackoff 可用於調整用戶端即時的下載位置，讓用戶端漂移，並叫用 hello 即時邊緣時就可以從伺服器，而非收到 404 或 412 HTTP 錯誤訊息，還是取得片段。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-200">In addition toohello advertisement support, LiveBackoff can be used for adjusting client live download position so that when clients drift and hit hello live edge they can still get fragments from server instead of getting 404 or 412 HTTP errors.</span></span>

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a><span data-ttu-id="a7e7f-202">將多個規則結合成單一篩選器</span><span class="sxs-lookup"><span data-stu-id="a7e7f-202">Combining multiple rules in a single filter</span></span>
<span data-ttu-id="a7e7f-203">您可以將多個篩選規則結合成單一篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-203">You can combine multiple filtering rules in a single filter.</span></span> <span data-ttu-id="a7e7f-204">例如，您可以定義從即時封存 tooremove 範圍規則候選影片，並也篩選 可用的位元。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-204">As an example you can define a range rule tooremove slate from a live archive and also filter available bitrates.</span></span> <span data-ttu-id="a7e7f-205">篩選規則 hello end 結果是這些規則的 hello 組合 （交集只）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-205">For multiple filtering rules hello end result is hello composition (intersection only) of these rules.</span></span>

![多個規則][multiple-rules]

## <a name="create-filters-programmatically"></a><span data-ttu-id="a7e7f-207">以程式設計方式建立篩選器</span><span class="sxs-lookup"><span data-stu-id="a7e7f-207">Create filters programmatically</span></span>
<span data-ttu-id="a7e7f-208">下列主題中的 hello 討論媒體服務實體的相關的 toofilters。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-208">hello following topic discusses Media Services entities that are related toofilters.</span></span> <span data-ttu-id="a7e7f-209">hello 主題也會顯示如何 tooprogrammatically 建立篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-209">hello topic also shows how tooprogrammatically create filters.</span></span>  

<span data-ttu-id="a7e7f-210">[使用 REST API 建立篩選器](media-services-rest-dynamic-manifest.md)。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-210">[Create filters with REST APIs](media-services-rest-dynamic-manifest.md).</span></span>

## <a name="combining-multiple-filters-filter-composition"></a><span data-ttu-id="a7e7f-211">結合多個篩選條件 (篩選器組合)</span><span class="sxs-lookup"><span data-stu-id="a7e7f-211">Combining multiple filters (filter composition)</span></span>
<span data-ttu-id="a7e7f-212">您也可以將多個篩選條件結合成單一 URL。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-212">You can also combine multiple filters in a single URL.</span></span> 

<span data-ttu-id="a7e7f-213">hello 下列案例示範為什麼您可能會想 toocombine 篩選：</span><span class="sxs-lookup"><span data-stu-id="a7e7f-213">hello following scenario demonstrates why you might want toocombine filters:</span></span>

1. <span data-ttu-id="a7e7f-214">您需要 toofilter 您視訊品質的 Android 或 （在順序 toolimit 視訊品質） iPAD 等行動裝置。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-214">You need toofilter your video qualities for mobile devices such as Android or iPAD (in order toolimit video qualities).</span></span> <span data-ttu-id="a7e7f-215">tooremove hello 不想要的品質，您會建立全域的篩選條件適用於裝置設定檔。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-215">tooremove hello unwanted qualities, you would create a global filter which is suitable for device profiles.</span></span> <span data-ttu-id="a7e7f-216">全域篩選如上面所述，可用於所有的資產在 hello 相同的媒體服務帳戶不需要任何進一步的關聯。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-216">As mentioned above, global filters can be used for all your assets under hello same media services account without any further association.</span></span> 
2. <span data-ttu-id="a7e7f-217">您也想 tootrim hello 開始和結束時間的資產。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-217">You also want tootrim hello start and end time of an asset.</span></span> <span data-ttu-id="a7e7f-218">tooachieve，您會建立本機篩選條件，並設定 hello 開始/結束時間。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-218">tooachieve this, you would create a local filter and set hello start/end time.</span></span> 
3. <span data-ttu-id="a7e7f-219">您想要的這些篩選器 toocombine （組合不需要 tooadd 品質篩選 toohello 調整篩選器，它會使篩選使用情況困難）。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-219">You want toocombine both of these filters (without combination you would need tooadd quality filtering toohello trimming filter which will make filter usage difficult).</span></span>

<span data-ttu-id="a7e7f-220">toocombine 篩選，您需要 tooset hello 篩選器名稱 toohello 資訊清單/播放清單 URL，並以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-220">toocombine filters, you need tooset hello filter names toohello manifest/playlist URL with semicolon delimited.</span></span> <span data-ttu-id="a7e7f-221">讓我們假設您有篩選，名為*MyMobileDevice*篩選品質，而且您有另一個名為*MyStartTime* tooset 特定開始時間。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-221">Let’s assume you have a filter named *MyMobileDevice* that filters qualities and you have another named *MyStartTime* tooset a specific start time.</span></span> <span data-ttu-id="a7e7f-222">您可以將它們結合如下：</span><span class="sxs-lookup"><span data-stu-id="a7e7f-222">You can combine them like this:</span></span>

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

<span data-ttu-id="a7e7f-223">您可以結合向上 too3 篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-223">You can combine up too3 filters.</span></span> 

<span data-ttu-id="a7e7f-224">如需詳細資訊，請參閱 [此](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) 部落格。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-224">For more information see [this](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.</span></span>

## <a name="know-issues-and-limitations"></a><span data-ttu-id="a7e7f-225">已知問題與限制</span><span class="sxs-lookup"><span data-stu-id="a7e7f-225">Know issues and limitations</span></span>
* <span data-ttu-id="a7e7f-226">動態資訊清單會在 GOP 界限 (主要畫面格) 中運作，因此修剪後能夠有精確的 GOP。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-226">Dynamic manifest operates in GOP boundaries (Key Frames) hence trimming has GOP accuracy.</span></span> 
* <span data-ttu-id="a7e7f-227">您可以讓本機和全域篩選器使用相同的篩選器名稱。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-227">You can use same filter name for local and global filters.</span></span> <span data-ttu-id="a7e7f-228">請注意，本機篩選有較高的優先權，會覆寫全域篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-228">Note that local filter have higher precedence and will override global filters.</span></span>
* <span data-ttu-id="a7e7f-229">如果您更新篩選器，就可以在資料流端點 toorefresh hello 規則 too2 分鐘。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-229">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="a7e7f-230">如果 hello 內容處理使用部分的篩選器 （快取和 proxy 和 CDN 中快取），更新這些篩選器導致播放失敗。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-230">If hello content was served using some filters (and cached in proxies and CDN caches), updating these filters can result in player failures.</span></span> <span data-ttu-id="a7e7f-231">它是在更新 hello 篩選之後，建議 tooclear hello 快取。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-231">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="a7e7f-232">如果這個選項無法執行，請考慮使用不同的篩選器。</span><span class="sxs-lookup"><span data-stu-id="a7e7f-232">If this option is not possible, consider using a different filter.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a7e7f-233">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="a7e7f-233">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a7e7f-234">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="a7e7f-234">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a7e7f-235">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a7e7f-235">See Also</span></span>
[<span data-ttu-id="a7e7f-236">傳遞內容 tooCustomers 概觀</span><span class="sxs-lookup"><span data-stu-id="a7e7f-236">Delivering Content tooCustomers Overview</span></span>](media-services-deliver-content-overview.md)

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
