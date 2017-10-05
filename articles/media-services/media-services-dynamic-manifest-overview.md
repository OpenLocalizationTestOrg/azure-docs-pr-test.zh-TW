---
title: "篩選器與動態資訊清單 | Microsoft Docs"
description: "本主題說明如何建立篩選器，讓您的用戶端可以使用篩選器來串流特定的資料流區段。 媒體服務會建立動態資訊清單來封存此選擇性資料流。"
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
ms.openlocfilehash: 4034fd0aa64627c107a43208dcca766f7f44d5d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="filters-and-dynamic-manifests"></a><span data-ttu-id="979da-104">篩選器與動態資訊清單</span><span class="sxs-lookup"><span data-stu-id="979da-104">Filters and dynamic manifests</span></span>
<span data-ttu-id="979da-105">從 2.11 版開始，媒體服務可讓您為資產定義篩選器。</span><span class="sxs-lookup"><span data-stu-id="979da-105">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="979da-106">這些篩選器是伺服器端規則，可讓您的客戶選擇執行如下的動作：只播放一段視訊 (而非播放完整視訊)，或只指定您客戶裝置可以處理的一部分音訊和視訊轉譯 (而非與該資產相關的所有轉譯)。</span><span class="sxs-lookup"><span data-stu-id="979da-106">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="979da-107">透過在您客戶要求下建立的 **動態資訊清單**可達成對資訊進行這樣的篩選，藉此根據指定的篩選器來串流視訊。</span><span class="sxs-lookup"><span data-stu-id="979da-107">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="979da-108">本主題討論對您客戶很有幫助的常見篩選器使用案例，並提供主題連結以示範如何以程式設計方式建立篩選器 (目前您只能使用 REST API 建立篩選器)。</span><span class="sxs-lookup"><span data-stu-id="979da-108">This topics discusses common scenarios in which using filters would be very beneficial to your customers and links to topics that demonstrate how to create filters programmatically (currently, you can create filters with REST APIs only).</span></span>

## <a name="overview"></a><span data-ttu-id="979da-109">Overview</span><span class="sxs-lookup"><span data-stu-id="979da-109">Overview</span></span>
<span data-ttu-id="979da-110">當您將內容傳遞給客戶時 (串流即時事件或點播視訊)，您的目標是在不同的網路條件下將高品質的視訊傳遞到各種裝置。</span><span class="sxs-lookup"><span data-stu-id="979da-110">When delivering your content to customers (streaming live events or video-on-demand) your goal is to deliver a high quality video to various devices under different network conditions.</span></span> <span data-ttu-id="979da-111">若要達成此目標，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="979da-111">To achieve this goal do the following:</span></span>

* <span data-ttu-id="979da-112">將您的資料流編碼成多位元速率 ([彈性位元速率](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) 視訊串流 (這會處理品質與網路條件)，並</span><span class="sxs-lookup"><span data-stu-id="979da-112">encode your stream to multi-bitrate ([adaptive bitrate](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) video stream (this will take care of quality and network conditions) and</span></span> 
* <span data-ttu-id="979da-113">使用媒體服務 [動態封裝](media-services-dynamic-packaging-overview.md) 將資料流動態地重新封裝至不同的通訊協定 (這會處理不同裝置上的資料流)。</span><span class="sxs-lookup"><span data-stu-id="979da-113">use Media Services [Dynamic Packaging](media-services-dynamic-packaging-overview.md) to dynamically re-package your stream into different protocols (this will take care of streaming on different devices).</span></span> <span data-ttu-id="979da-114">媒體服務支援傳遞下列自適性串流技術：HTTP 即時串流 (HLS)、Smooth Streaming 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="979da-114">Media Services supports delivery of the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span> 

### <a name="manifest-files"></a><span data-ttu-id="979da-115">資訊清單檔案</span><span class="sxs-lookup"><span data-stu-id="979da-115">Manifest files</span></span>
<span data-ttu-id="979da-116">當您將資產編碼以進行彈性位元速率資料流時，會建立 **資訊清單** (播放清單) 檔案 (此檔案是以文字或 XML 為基礎)。</span><span class="sxs-lookup"><span data-stu-id="979da-116">When you encode an asset for adaptive bitrate streaming, a **manifest** (playlist) file is created (the file is text-based or XML-based).</span></span> <span data-ttu-id="979da-117">**資訊清單** 檔案包含資料流中繼資料，例如：資料軌類型 (音訊、視訊或文字)、資料軌名稱、開始和結束時間、位元速率 (品質)、資料軌語言、簡報視窗 (持續時間固定的滑動視窗)，視訊轉碼器 (FourCC)。</span><span class="sxs-lookup"><span data-stu-id="979da-117">The **manifest** file includes streaming metadata such as: track type (audio, video, or text), track name, start and end time, bitrate (qualities), track languages, presentation window (sliding window of fixed duration), video codec (FourCC).</span></span> <span data-ttu-id="979da-118">此檔案也會透過提供下一個可播放視訊片段及其位置的相關資訊，來指示播放程式擷取下一個片段。</span><span class="sxs-lookup"><span data-stu-id="979da-118">It also instructs the player to retrieve the next fragment by providing information about the next playable video fragments available and their location.</span></span> <span data-ttu-id="979da-119">片段 (或區段) 實際上是視訊內容的「區塊」。</span><span class="sxs-lookup"><span data-stu-id="979da-119">Fragments (or segments) are the actual “chunks” of a video content.</span></span>

<span data-ttu-id="979da-120">資訊清單檔案範例如下：</span><span class="sxs-lookup"><span data-stu-id="979da-120">Here is an example of a manifest file:</span></span> 

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

### <a name="dynamic-manifests"></a><span data-ttu-id="979da-121">動態資訊清單</span><span class="sxs-lookup"><span data-stu-id="979da-121">Dynamic manifests</span></span>
<span data-ttu-id="979da-122">提供許多當您的用戶端需要比預設資產資訊清單檔更多彈性的 [案例](media-services-dynamic-manifest-overview.md#scenarios) 。</span><span class="sxs-lookup"><span data-stu-id="979da-122">There are [scenarios](media-services-dynamic-manifest-overview.md#scenarios) when your client needs more flexibility than what's described in the default asset's manifest file.</span></span> <span data-ttu-id="979da-123">例如：</span><span class="sxs-lookup"><span data-stu-id="979da-123">For example:</span></span>

* <span data-ttu-id="979da-124">裝置特有：只傳遞用來播放內容的裝置所支援的指定轉譯和/或指定的語言資料軌 (「轉譯篩選」)。</span><span class="sxs-lookup"><span data-stu-id="979da-124">Device specific: deliver only the specified renditions and\or specified language tracks that are supported by the device that is used to playback the content ("rendition filtering").</span></span> 
* <span data-ttu-id="979da-125">縮小資訊清單以顯示即時事件的子剪輯 (「子剪輯篩選」)。</span><span class="sxs-lookup"><span data-stu-id="979da-125">Reduce the manifest to show a sub-clip of a live event ("sub-clip filtering").</span></span>
* <span data-ttu-id="979da-126">修剪視訊開頭 (「修剪視訊」)。</span><span class="sxs-lookup"><span data-stu-id="979da-126">Trim the start of a video ("trimming a video").</span></span>
* <span data-ttu-id="979da-127">調整 簡報視窗 (DVR)，以便在播放程式中提供長度有限的 DVR 視窗 (「調整簡報視窗」)。</span><span class="sxs-lookup"><span data-stu-id="979da-127">Adjust Presentation Window (DVR) in order to provide a limited length of the DVR window in the player ("adjusting presentation window") .</span></span>

<span data-ttu-id="979da-128">為達到這種彈性，媒體服務會根據預先定義的 **篩選器** 提供 [動態資訊清單](media-services-dynamic-manifest-overview.md#filters)。</span><span class="sxs-lookup"><span data-stu-id="979da-128">To achieve this flexibility, Media Services offers **Dynamic Manifests** based on pre-defined [filters](media-services-dynamic-manifest-overview.md#filters).</span></span>  <span data-ttu-id="979da-129">一旦您定義了篩選器，您的用戶端便會使用篩選器來串流視訊的特定轉譯或子剪輯。</span><span class="sxs-lookup"><span data-stu-id="979da-129">Once you define the filters, your clients could use them to stream a specific rendition or sub-clips of your video.</span></span> <span data-ttu-id="979da-130">用戶端會在資料流 URL 中指定篩選器。</span><span class="sxs-lookup"><span data-stu-id="979da-130">They would specify filter(s) in the streaming URL.</span></span> <span data-ttu-id="979da-131">篩選器可以套用到下列 [動態封裝](media-services-dynamic-packaging-overview.md)支援的自適性串流通訊協定：HLS、MPEG-DASH 和 Smooth Streaming。</span><span class="sxs-lookup"><span data-stu-id="979da-131">Filters could be applied to adaptive bitrate streaming protocols supported by [Dynamic Packaging](media-services-dynamic-packaging-overview.md): HLS, MPEG-DASH, and Smooth Streaming.</span></span> <span data-ttu-id="979da-132">例如：</span><span class="sxs-lookup"><span data-stu-id="979da-132">For example:</span></span>

<span data-ttu-id="979da-133">含篩選器的 MPEG DASH URL</span><span class="sxs-lookup"><span data-stu-id="979da-133">MPEG DASH URL with filter</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

<span data-ttu-id="979da-134">含篩選器的 Smooth Streaming URL</span><span class="sxs-lookup"><span data-stu-id="979da-134">Smooth Streaming URL with filter</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


<span data-ttu-id="979da-135">如需如何傳遞內容和建置資料流 URL 的詳細資訊，請參閱 [傳遞內容概觀](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="979da-135">For more information about how to deliver your content and build streaming URLs, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="979da-136">請注意，動態資訊清單不會變更資產和該資產的預設資訊清單。</span><span class="sxs-lookup"><span data-stu-id="979da-136">Note that Dynamic Manifests do not change the asset and the default manifest for that asset.</span></span> <span data-ttu-id="979da-137">您的用戶端可以選擇要求包含或不含篩選器的資料流。</span><span class="sxs-lookup"><span data-stu-id="979da-137">Your client can choose to request a stream with or without filters.</span></span> 
> 
> 

### <span data-ttu-id="979da-138"><a id="filters"></a>篩選器</span><span class="sxs-lookup"><span data-stu-id="979da-138"><a id="filters"></a>Filters</span></span>
<span data-ttu-id="979da-139">資產篩選器有兩種：</span><span class="sxs-lookup"><span data-stu-id="979da-139">There are two types of asset filters:</span></span> 

* <span data-ttu-id="979da-140">全域篩選器 (可以套用到 Azure 媒體服務帳戶中所有的資產，擁有帳戶的存留期間) 和</span><span class="sxs-lookup"><span data-stu-id="979da-140">Global filters (can be applied to any asset in the Azure Media Services account, have a lifetime of the account) and</span></span> 
* <span data-ttu-id="979da-141">本機篩選器 (只能套用篩選器建立時與其相關聯的資產，擁有資產的存留期間)。</span><span class="sxs-lookup"><span data-stu-id="979da-141">Local filters (can only be applied to an asset with which the filter was associated upon creation, have a lifetime of the asset).</span></span> 

<span data-ttu-id="979da-142">全域和本機篩選器類型有完全相同的屬性。</span><span class="sxs-lookup"><span data-stu-id="979da-142">Global and local filter types have exactly the same properties.</span></span> <span data-ttu-id="979da-143">這兩個的主要差異在於案例較適合哪一種篩選器。</span><span class="sxs-lookup"><span data-stu-id="979da-143">The main difference between the two is for which scenarios what type of a filer is more suitable.</span></span> <span data-ttu-id="979da-144">全域篩選器通常適用於裝置設定檔 (轉譯篩選)，而本機篩選器可用於修剪特定的資產。</span><span class="sxs-lookup"><span data-stu-id="979da-144">Global filters are generally suitable for device profiles (rendition filtering) where local filters could be used to trim a specific asset.</span></span>

## <span data-ttu-id="979da-145"><a id="scenarios"></a>常見案例</span><span class="sxs-lookup"><span data-stu-id="979da-145"><a id="scenarios"></a>Common scenarios</span></span>
<span data-ttu-id="979da-146">先前提過，將內容傳遞給客戶時 (串流即時事件或點播視訊)，您的目標是在不同的網路條件下將高品質的視訊傳遞到各種裝置。</span><span class="sxs-lookup"><span data-stu-id="979da-146">As was mentioned before, when delivering your content to customers (streaming live events or video-on-demand) your goal is to deliver a high quality video to various devices under different network conditions.</span></span> <span data-ttu-id="979da-147">此外，您可能會有其他對於篩選資產與使用 **動態資訊清單**相關的需求。</span><span class="sxs-lookup"><span data-stu-id="979da-147">In addition, your might have other requirements that involve filtering your assets and using of **Dynamic Manifest**s.</span></span> <span data-ttu-id="979da-148">以下幾節提供不同篩選案例的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="979da-148">The following sections give a short overview of different filtering scenarios.</span></span>

* <span data-ttu-id="979da-149">僅指定某些裝置可以處理的音訊和視訊轉譯子集 (而非與該資產相關聯的所有轉譯)。</span><span class="sxs-lookup"><span data-stu-id="979da-149">Specify only a subset of audio and video renditions that certain devices can handle (instead of all the renditions that are associated with the asset).</span></span> 
* <span data-ttu-id="979da-150">僅播放視訊的某個區段 (而非播放整個視訊)。</span><span class="sxs-lookup"><span data-stu-id="979da-150">Playing back only a section of a video (instead of playing the whole video).</span></span>
* <span data-ttu-id="979da-151">調整 DVR 簡報視窗。</span><span class="sxs-lookup"><span data-stu-id="979da-151">Adjust DVR presentation window.</span></span>

## <a name="rendition-filtering"></a><span data-ttu-id="979da-152">轉譯篩選</span><span class="sxs-lookup"><span data-stu-id="979da-152">Rendition filtering</span></span>
<span data-ttu-id="979da-153">您可以選擇將資產編碼成多個編碼設定檔 (H.264 Baseline、H.264 High、AACL、AACH、Dolby Digital Plus)，及多個高品質位元速率。</span><span class="sxs-lookup"><span data-stu-id="979da-153">You may choose to encode your asset to multiple encoding profiles (H.264 Baseline, H.264 High, AACL, AACH, Dolby Digital Plus) and multiple quality bitrates.</span></span> <span data-ttu-id="979da-154">不過，並非所有的用戶端裝置都支援您所有的資產和位元速率。</span><span class="sxs-lookup"><span data-stu-id="979da-154">However, not all client devices will support all your asset's profiles and bitrates.</span></span> <span data-ttu-id="979da-155">例如，較舊的 Android 裝置只支援 H.264 Baseline+AACL。</span><span class="sxs-lookup"><span data-stu-id="979da-155">For example, older Android devices only supports H.264 Baseline+AACL.</span></span> <span data-ttu-id="979da-156">將較高的位元速率傳送到無法獲益的裝置，將會浪費頻寬及裝置計算。</span><span class="sxs-lookup"><span data-stu-id="979da-156">Sending higher bitrates to a device which cannot get the benefits, wastes bandwidth and device computation.</span></span> <span data-ttu-id="979da-157">這類裝置必須將所有指定的資訊解碼，才能縮小以顯示。</span><span class="sxs-lookup"><span data-stu-id="979da-157">Such device must decode all the given information, only to scale it down for display.</span></span>

<span data-ttu-id="979da-158">有了動態資訊清單，您可以建立裝置設定檔，例如行動、主控台、HD/SD 等，並包括您想要納入設定檔中的特質與品質。</span><span class="sxs-lookup"><span data-stu-id="979da-158">With Dynamic Manifest, you can create device profiles such as mobile, console, HD/SD, etc. and include the tracks and qualities which you want to be a part of each profile.</span></span>

![轉譯篩選範例][renditions2]

<span data-ttu-id="979da-160">下列範例使用編碼器將夾層資產編碼成七個 ISO MP4 視訊轉譯 (從 180p 到 1080p)。</span><span class="sxs-lookup"><span data-stu-id="979da-160">In the following example, an encoder was used to encode a mezzanine asset into seven ISO MP4s video renditions (from 180p to 1080p).</span></span> <span data-ttu-id="979da-161">編碼的資產可以動態地封裝至下列任何一個資料流通訊協定：HLS、Smooth 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="979da-161">The encoded asset can be dynamically packaged into any of the following streaming protocols: HLS, Smooth, and MPEG DASH.</span></span>  <span data-ttu-id="979da-162">圖表頂端顯示不含篩選器的資產其 HLS 資訊清單 (包含全部七個轉譯)。</span><span class="sxs-lookup"><span data-stu-id="979da-162">At the top of the diagram, the HLS manifest for the asset with no filters is shown (it contains all seven renditions).</span></span>  <span data-ttu-id="979da-163">左下角顯示名為 "ott" 的篩選器已套用到 HLS 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="979da-163">In the bottom left, the HLS manifest to which a filter named "ott" was applied is shown.</span></span> <span data-ttu-id="979da-164">"ott" 篩選器指定要移除所有不到 1Mbps 的位元速率，因此將最差的兩個品質等級從回應中去除。</span><span class="sxs-lookup"><span data-stu-id="979da-164">The "ott" filter specifies to remove all bitrates below 1Mbps, which resulted in the bottom two quality levels being stripped off in the response.</span></span>  <span data-ttu-id="979da-165">右下角顯示名為 "mobile" 的篩選器已套用到 HLS 資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="979da-165">In the bottom right,   the HLS manifest to which a filter named "mobile" was applied is shown.</span></span> <span data-ttu-id="979da-166">"mobile" 篩選器指定要移除的解析度大於 720p 的轉譯，因此去除兩個 1080p 的轉譯。</span><span class="sxs-lookup"><span data-stu-id="979da-166">The "mobile" filter specifies to remove renditions where the resolution is larger than 720p, which resulted in the two 1080p renditions being stripped off.</span></span>

![轉譯篩選][renditions1]

## <a name="removing-language-tracks"></a><span data-ttu-id="979da-168">移除語言資料軌</span><span class="sxs-lookup"><span data-stu-id="979da-168">Removing language tracks</span></span>
<span data-ttu-id="979da-169">您的資產可能包含多個音訊語言，例如英文、西班牙文、法文等。通常，播放程式 SDK 管理員會預設音訊資料軌選取範圍，以及每個使用者可選擇的可用音訊資料軌。</span><span class="sxs-lookup"><span data-stu-id="979da-169">Your assets might include multiple audio languages such as English, Spanish, French, etc. Usually, the Player SDK managers default audio track selection and available audio tracks per user selection.</span></span> <span data-ttu-id="979da-170">開發這類的播放程式 SDK 相當有挑戰性，因為在各個裝置特有的播放程式架構之間有不同的實作方式。</span><span class="sxs-lookup"><span data-stu-id="979da-170">It is challenging to develop such Player SDKs, it requires different implementations across device-specific player-frameworks.</span></span> <span data-ttu-id="979da-171">此外播放程式 API 在某些平台上受到限制，且不包含音訊選擇功能，因此使用者無法選取或變更預設的音訊資料軌。有了資產篩選器，您可以藉由建立只包含所需音訊語言的篩選器來控制行為。</span><span class="sxs-lookup"><span data-stu-id="979da-171">Also, on some platforms, Player APIs are limited and do not include audio selection feature where users cannot select or change the default audio track. With asset filters, you can control the behavior by creating filters that only include desired audio languages.</span></span>

![語言資料軌篩選][language_filter]

## <a name="trimming-start-of-an-asset"></a><span data-ttu-id="979da-173">修剪資產開頭</span><span class="sxs-lookup"><span data-stu-id="979da-173">Trimming start of an asset</span></span>
<span data-ttu-id="979da-174">在大部分的即時資料流事件中，操作人員必須在實際的事件前先進行測試。</span><span class="sxs-lookup"><span data-stu-id="979da-174">In most live streaming events, operators run some tests before the actual event.</span></span> <span data-ttu-id="979da-175">例如，他們可以在事件開始前包含如下 slate 訊息：「程式將立刻開始」。</span><span class="sxs-lookup"><span data-stu-id="979da-175">For example, they might include a slate like this before the start of the event: "Program will begin momentarily".</span></span> <span data-ttu-id="979da-176">如果程式正在進行封存，則測試和 slate 資料也會一併封存並包含在簡報中。</span><span class="sxs-lookup"><span data-stu-id="979da-176">If the program is archiving, the test and slate data are also archived and will be included in the presentation.</span></span> <span data-ttu-id="979da-177">但是此資訊不會對用戶端顯示。</span><span class="sxs-lookup"><span data-stu-id="979da-177">However, this information should not be shown to the clients.</span></span> <span data-ttu-id="979da-178">透過動態資訊清單，您可以建立開始時間篩選器，並從資訊清單中移除不必要的資料。</span><span class="sxs-lookup"><span data-stu-id="979da-178">With Dynamic Manifest, you can create a start time filter and remove the unwanted data from the manifest.</span></span>

![開始修剪][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a><span data-ttu-id="979da-180">從即時封存中建立子剪輯 (檢視)</span><span class="sxs-lookup"><span data-stu-id="979da-180">Creating sub-clips (views) from a live archive</span></span>
<span data-ttu-id="979da-181">許多即時事件的執行時間長，且即時封存可能包括多個事件。</span><span class="sxs-lookup"><span data-stu-id="979da-181">Many live events are long running and live archive might include multiple events.</span></span> <span data-ttu-id="979da-182">即時事件結束後，廣播者可能想要將即時封存分解成邏輯程式的啟動和停止序列。</span><span class="sxs-lookup"><span data-stu-id="979da-182">After the live event ends broadcasters may want to break up the live archive into logical program start and stop sequences.</span></span> <span data-ttu-id="979da-183">然後個別發佈這些虛擬程式，但不後續處理即時封存，亦不建立個別的資產 (這將無法運用 CDN 中現有快取片段的優點)。</span><span class="sxs-lookup"><span data-stu-id="979da-183">Then, publish these virtual programs separately without post processing the live archive and not creating separate assets (which will not get benefit of the existing cached fragments in the CDNs).</span></span> <span data-ttu-id="979da-184">例如足球或籃球比賽的球季、棒球賽局，或是奧運下午賽程的個別事件，都是此類虛擬程式 (子剪輯) 的範例。</span><span class="sxs-lookup"><span data-stu-id="979da-184">Examples of such virtual programs (sub-clips) are the quarters of a football or basketball game, the innings in baseball, or individual events of an afternoon of Olympics program.</span></span>

<span data-ttu-id="979da-185">使用動態資訊清單，您便可以使用開始/結束時間建立篩選器，並在即時封存頂端建立虛擬檢視。</span><span class="sxs-lookup"><span data-stu-id="979da-185">With Dynamic Manifest, you can create filters using start/end times and create virtual views over the top of your live archive.</span></span> 

![子剪輯篩選][subclip_filter]

<span data-ttu-id="979da-187">已篩選的資產：</span><span class="sxs-lookup"><span data-stu-id="979da-187">Filtered Asset:</span></span>

![滑動][skiing]

## <a name="adjusting-presentation-window-dvr"></a><span data-ttu-id="979da-189">調整簡報視窗 (DVR)</span><span class="sxs-lookup"><span data-stu-id="979da-189">Adjusting Presentation Window (DVR)</span></span>
<span data-ttu-id="979da-190">目前，Azure 媒體服務提供持續時間可設為 5 分鐘到 25 小時的循環封存。</span><span class="sxs-lookup"><span data-stu-id="979da-190">Currently, Azure Media Services offers circular archive where the duration can be configured between 5 minutes - 25 hours.</span></span> <span data-ttu-id="979da-191">資訊清單篩選可以在封存頂端建立循環 DVR 視窗封存，而不會刪除媒體。</span><span class="sxs-lookup"><span data-stu-id="979da-191">Manifest filtering can be used to create a rolling DVR window over the top of the archive, without deleting media.</span></span> <span data-ttu-id="979da-192">在許多情況下，廣播者想要提供受限制的 DVR 視窗，此視窗可隨著即時邊緣移動，並同時保留更大的封存視窗。</span><span class="sxs-lookup"><span data-stu-id="979da-192">There are many scenarios where broadcasters want to provide a limited DVR window which moves with the live edge and at the same time keep a bigger archiving window.</span></span> <span data-ttu-id="979da-193">廣播者可能會想要使用超出 DVR 視窗的資料來反白顯示剪輯，或者想要為不同的裝置提供不同的 DVR 視窗。</span><span class="sxs-lookup"><span data-stu-id="979da-193">A broadcaster may want to use the data that is out of the DVR window to highlight clips, or he\she may want to provide different DVR windows for different devices.</span></span> <span data-ttu-id="979da-194">例如，大多數的行動裝置不處理大 DVR 視窗 (您可以讓行動裝置有 2 分鐘的 DVR 視窗，桌上型用戶端有 1 小時的 DVR 視窗)。</span><span class="sxs-lookup"><span data-stu-id="979da-194">For example, most of the mobile devices don’t handle big DVR windows (you can have a 2 minute DVR window for mobile devices and 1 hour for desktop clients).</span></span>

![DVR 視窗][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a><span data-ttu-id="979da-196">調整 LiveBackoff (即時位置)</span><span class="sxs-lookup"><span data-stu-id="979da-196">Adjusting LiveBackoff (live position)</span></span>
<span data-ttu-id="979da-197">資訊清單篩選可用來移除即時程式其即時邊緣幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="979da-197">Manifest filtering can be used to remove several seconds from the live edge of a live program.</span></span> <span data-ttu-id="979da-198">這可讓廣播者在檢視者收到資料流前 (通常倒退 30 秒) 先觀賞預覽發佈點的簡報，並建立廣告插入點。</span><span class="sxs-lookup"><span data-stu-id="979da-198">This allows broadcasters to watch the presentation on the preview publication point and create advertisement insertion points before the viewers receive the stream (usually backed-off by 30 seconds).</span></span> <span data-ttu-id="979da-199">廣播者接著可將這些廣告及時推送到其用戶端架構，讓廣播者能夠收到與處理資訊，才有機會播放廣告。</span><span class="sxs-lookup"><span data-stu-id="979da-199">Broadcasters can then push these advertisements to their client frameworks in time for them to received and process the information before the advertisement opportunity.</span></span>

<span data-ttu-id="979da-200">除了廣告支援外，LiveBackoff 可用於調整用戶端即時下載位置，讓用戶端移動並命中即時邊緣時，仍然可以從伺服器取得片段，而非得到 404 或 412 HTTP 錯誤。</span><span class="sxs-lookup"><span data-stu-id="979da-200">In addition to the advertisement support, LiveBackoff can be used for adjusting client live download position so that when clients drift and hit the live edge they can still get fragments from server instead of getting 404 or 412 HTTP errors.</span></span>

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a><span data-ttu-id="979da-202">將多個規則結合成單一篩選器</span><span class="sxs-lookup"><span data-stu-id="979da-202">Combining multiple rules in a single filter</span></span>
<span data-ttu-id="979da-203">您可以將多個篩選規則結合成單一篩選器。</span><span class="sxs-lookup"><span data-stu-id="979da-203">You can combine multiple filtering rules in a single filter.</span></span> <span data-ttu-id="979da-204">例如，您可以定義一個範圍規則，藉此將 slate 從即時封存中移除，並篩選可用的位元速率。</span><span class="sxs-lookup"><span data-stu-id="979da-204">As an example you can define a range rule to remove slate from a live archive and also filter available bitrates.</span></span> <span data-ttu-id="979da-205">對於多個篩選規則而言，最終結果會是這些規則的合成 (僅交集)。</span><span class="sxs-lookup"><span data-stu-id="979da-205">For multiple filtering rules the end result is the composition (intersection only) of these rules.</span></span>

![多個規則][multiple-rules]

## <a name="create-filters-programmatically"></a><span data-ttu-id="979da-207">以程式設計方式建立篩選器</span><span class="sxs-lookup"><span data-stu-id="979da-207">Create filters programmatically</span></span>
<span data-ttu-id="979da-208">下列主題討論與篩選器相關的媒體服務實體。</span><span class="sxs-lookup"><span data-stu-id="979da-208">The following topic discusses Media Services entities that are related to filters.</span></span> <span data-ttu-id="979da-209">此主題也會示範如何以程式設計方式建立篩選器。</span><span class="sxs-lookup"><span data-stu-id="979da-209">The topic also shows how to programmatically create filters.</span></span>  

<span data-ttu-id="979da-210">[使用 REST API 建立篩選器](media-services-rest-dynamic-manifest.md)。</span><span class="sxs-lookup"><span data-stu-id="979da-210">[Create filters with REST APIs](media-services-rest-dynamic-manifest.md).</span></span>

## <a name="combining-multiple-filters-filter-composition"></a><span data-ttu-id="979da-211">結合多個篩選條件 (篩選器組合)</span><span class="sxs-lookup"><span data-stu-id="979da-211">Combining multiple filters (filter composition)</span></span>
<span data-ttu-id="979da-212">您也可以將多個篩選條件結合成單一 URL。</span><span class="sxs-lookup"><span data-stu-id="979da-212">You can also combine multiple filters in a single URL.</span></span> 

<span data-ttu-id="979da-213">下列案例示範您可能會想結合篩選條件的理由：</span><span class="sxs-lookup"><span data-stu-id="979da-213">The following scenario demonstrates why you might want to combine filters:</span></span>

1. <span data-ttu-id="979da-214">您要篩選例如 Android 或 iPAD 等行動裝置的視訊品質 (以限制視訊品質)。</span><span class="sxs-lookup"><span data-stu-id="979da-214">You need to filter your video qualities for mobile devices such as Android or iPAD (in order to limit video qualities).</span></span> <span data-ttu-id="979da-215">若要移除不必要的品質，您或可建立適用於裝置設定檔的全域篩選條件。</span><span class="sxs-lookup"><span data-stu-id="979da-215">To remove the unwanted qualities, you would create a global filter which is suitable for device profiles.</span></span> <span data-ttu-id="979da-216">如上所述，全域篩選條件可以用於相同媒體服務帳戶下所有的資產，而不需進一步的關聯。</span><span class="sxs-lookup"><span data-stu-id="979da-216">As mentioned above, global filters can be used for all your assets under the same media services account without any further association.</span></span> 
2. <span data-ttu-id="979da-217">您也想要修剪資產的開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="979da-217">You also want to trim the start and end time of an asset.</span></span> <span data-ttu-id="979da-218">若要達到此目的，您可建立本機篩選條件，並設定開始/結束時間。</span><span class="sxs-lookup"><span data-stu-id="979da-218">To achieve this, you would create a local filter and set the start/end time.</span></span> 
3. <span data-ttu-id="979da-219">您想要結合這兩個篩選條件 (不含您需要加入品質篩選到修剪篩選條件的組合，這會讓使用篩選條件更為困難)。</span><span class="sxs-lookup"><span data-stu-id="979da-219">You want to combine both of these filters (without combination you would need to add quality filtering to the trimming filter which will make filter usage difficult).</span></span>

<span data-ttu-id="979da-220">若要結合篩選條件，您必須設定資訊清單/播放清單 URL 的篩選條件名稱，並以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="979da-220">To combine filters, you need to set the filter names to the manifest/playlist URL with semicolon delimited.</span></span> <span data-ttu-id="979da-221">假設您擁有名為 *MyMobileDevice* 的篩選條件，可篩選品質，且您有另一個名為 *MyStartTime* 的篩選條件，用來設定特定的開始時間。</span><span class="sxs-lookup"><span data-stu-id="979da-221">Let’s assume you have a filter named *MyMobileDevice* that filters qualities and you have another named *MyStartTime* to set a specific start time.</span></span> <span data-ttu-id="979da-222">您可以將它們結合如下：</span><span class="sxs-lookup"><span data-stu-id="979da-222">You can combine them like this:</span></span>

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

<span data-ttu-id="979da-223">您可以結合最多 3 個篩選條件。</span><span class="sxs-lookup"><span data-stu-id="979da-223">You can combine up to 3 filters.</span></span> 

<span data-ttu-id="979da-224">如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) 。</span><span class="sxs-lookup"><span data-stu-id="979da-224">For more information see [this](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.</span></span>

## <a name="know-issues-and-limitations"></a><span data-ttu-id="979da-225">已知問題與限制</span><span class="sxs-lookup"><span data-stu-id="979da-225">Know issues and limitations</span></span>
* <span data-ttu-id="979da-226">動態資訊清單會在 GOP 界限 (主要畫面格) 中運作，因此修剪後能夠有精確的 GOP。</span><span class="sxs-lookup"><span data-stu-id="979da-226">Dynamic manifest operates in GOP boundaries (Key Frames) hence trimming has GOP accuracy.</span></span> 
* <span data-ttu-id="979da-227">您可以讓本機和全域篩選器使用相同的篩選器名稱。</span><span class="sxs-lookup"><span data-stu-id="979da-227">You can use same filter name for local and global filters.</span></span> <span data-ttu-id="979da-228">請注意，本機篩選有較高的優先權，會覆寫全域篩選器。</span><span class="sxs-lookup"><span data-stu-id="979da-228">Note that local filter have higher precedence and will override global filters.</span></span>
* <span data-ttu-id="979da-229">如果您更新篩選器，則資料流端點需要 2 分鐘的時間來重新整理規則。</span><span class="sxs-lookup"><span data-stu-id="979da-229">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="979da-230">如果內容是透過使用某些篩選器提供的 (並在 Proxy 和 CDN 快取中快取)，則更新這些篩選器會導致播放程式失敗。</span><span class="sxs-lookup"><span data-stu-id="979da-230">If the content was served using some filters (and cached in proxies and CDN caches), updating these filters can result in player failures.</span></span> <span data-ttu-id="979da-231">建議在更新篩選器之後清除快取。</span><span class="sxs-lookup"><span data-stu-id="979da-231">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="979da-232">如果這個選項無法執行，請考慮使用不同的篩選器。</span><span class="sxs-lookup"><span data-stu-id="979da-232">If this option is not possible, consider using a different filter.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="979da-233">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="979da-233">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="979da-234">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="979da-234">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="979da-235">另請參閱</span><span class="sxs-lookup"><span data-stu-id="979da-235">See Also</span></span>
[<span data-ttu-id="979da-236">將內容傳遞給客戶概觀</span><span class="sxs-lookup"><span data-stu-id="979da-236">Delivering Content to Customers Overview</span></span>](media-services-deliver-content-overview.md)

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
