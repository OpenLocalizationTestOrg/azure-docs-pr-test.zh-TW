---
title: "aaaOverview 與 Azure 上比較要求的媒體編碼器 |Microsoft 文件"
description: "本主題概要說明並比較 Azure 隨選媒體編碼器。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="9a68f-103">Azure 隨選媒體編碼器的概觀和比較</span><span class="sxs-lookup"><span data-stu-id="9a68f-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="9a68f-104">編碼概觀</span><span class="sxs-lookup"><span data-stu-id="9a68f-104">Encoding overview</span></span>
<span data-ttu-id="9a68f-105">Azure Media Services 提供多個 hello 編碼媒體 hello 雲端中的選項。</span><span class="sxs-lookup"><span data-stu-id="9a68f-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="9a68f-106">開始使用 Media Services，很重要的 toounderstand hello 差異轉碼器與檔案格式。</span><span class="sxs-lookup"><span data-stu-id="9a68f-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="9a68f-107">轉碼器是實作 hello 壓縮/解壓縮演算法，而檔案格式是保留 hello 壓縮視訊的容器的 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="9a68f-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="9a68f-108">Media Services 提供動態封裝可讓您 toodeliver MP4 或 Smooth Streaming 您彈性位元速率編碼格式 （MPEG DASH、 HLS、 Smooth Streaming） 的 Media Services 支援的資料流處理中的內容，而不必 toore 封裝至您串流格式。</span><span class="sxs-lookup"><span data-stu-id="9a68f-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="9a68f-109">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="9a68f-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="9a68f-110">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="9a68f-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="9a68f-111">tootake 利用[動態封裝](media-services-dynamic-packaging-overview.md)，您需要 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9a68f-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="9a68f-112">此外，編碼為一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案 （hello 編碼步驟示範稍後在本教學課程） 的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="9a68f-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="9a68f-113">Media Services 支援 hello 下列上這篇文章所述的需求編碼器：</span><span class="sxs-lookup"><span data-stu-id="9a68f-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="9a68f-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9a68f-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="9a68f-115">媒體編碼器高階工作流程</span><span class="sxs-lookup"><span data-stu-id="9a68f-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="9a68f-116">本文簡短介紹的隨選媒體編碼器，並提供連結 tooarticles，提供更詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="9a68f-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="9a68f-117">hello 主題也提供 hello 編碼器的比較。</span><span class="sxs-lookup"><span data-stu-id="9a68f-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="9a68f-118">依預設，每個媒體服務帳戶一次可以有一個進行中的編碼工作。</span><span class="sxs-lookup"><span data-stu-id="9a68f-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="9a68f-119">您可以保留編碼單元可讓您 toohave 同時執行，一個用於每個您所購買的編碼保留單元的多個編碼工作。</span><span class="sxs-lookup"><span data-stu-id="9a68f-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="9a68f-120">如需相關資訊，請參閱 [調整編碼單位](media-services-scale-media-processing-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9a68f-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="9a68f-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9a68f-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="9a68f-122">如何 toouse</span><span class="sxs-lookup"><span data-stu-id="9a68f-122">How toouse</span></span>
[<span data-ttu-id="9a68f-123">如何與媒體編碼器標準 tooencode</span><span class="sxs-lookup"><span data-stu-id="9a68f-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="9a68f-124">格式</span><span class="sxs-lookup"><span data-stu-id="9a68f-124">Formats</span></span>
[<span data-ttu-id="9a68f-125">格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="9a68f-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="9a68f-126">預設值</span><span class="sxs-lookup"><span data-stu-id="9a68f-126">Presets</span></span>
<span data-ttu-id="9a68f-127">媒體編碼器標準設定時，使用其中一個所述的 hello 編碼器預設[這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="9a68f-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="9a68f-128">輸入和輸出中繼資料</span><span class="sxs-lookup"><span data-stu-id="9a68f-128">Input and output metadata</span></span>
<span data-ttu-id="9a68f-129">hello 編碼器輸入中繼資料描述[這裡](media-services-input-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="9a68f-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="9a68f-130">hello 編碼器輸出中繼資料描述[這裡](media-services-output-metadata-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="9a68f-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="9a68f-131">產生縮圖</span><span class="sxs-lookup"><span data-stu-id="9a68f-131">Generate thumbnails</span></span>
<span data-ttu-id="9a68f-132">如需資訊，請參閱[如何使用媒體編碼器標準 toogenerate 縮圖](media-services-advanced-encoding-with-mes.md#thumbnails)。</span><span class="sxs-lookup"><span data-stu-id="9a68f-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="9a68f-133">修剪視訊 (裁剪)</span><span class="sxs-lookup"><span data-stu-id="9a68f-133">Trim videos (clipping)</span></span>
<span data-ttu-id="9a68f-134">資訊，請參閱[如何使用媒體編碼器標準 tootrim 視訊](media-services-advanced-encoding-with-mes.md#trim_video)。</span><span class="sxs-lookup"><span data-stu-id="9a68f-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="9a68f-135">建立疊加層</span><span class="sxs-lookup"><span data-stu-id="9a68f-135">Create overlays</span></span>
<span data-ttu-id="9a68f-136">資訊，請參閱[如何使用媒體編碼器標準 toocreate 覆疊](media-services-advanced-encoding-with-mes.md#overlay)。</span><span class="sxs-lookup"><span data-stu-id="9a68f-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="9a68f-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9a68f-137">See also</span></span>
[<span data-ttu-id="9a68f-138">hello 媒體服務部落格</span><span class="sxs-lookup"><span data-stu-id="9a68f-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="9a68f-139">媒體編碼器高階工作流程</span><span class="sxs-lookup"><span data-stu-id="9a68f-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="9a68f-140">Overview</span><span class="sxs-lookup"><span data-stu-id="9a68f-140">Overview</span></span>
[<span data-ttu-id="9a68f-141">介紹 Azure 媒體服務中的 Premium 編碼</span><span class="sxs-lookup"><span data-stu-id="9a68f-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="9a68f-142">如何 toouse</span><span class="sxs-lookup"><span data-stu-id="9a68f-142">How toouse</span></span>
<span data-ttu-id="9a68f-143">Media Encoder Premium Workflow 使用複雜的工作流程設定。</span><span class="sxs-lookup"><span data-stu-id="9a68f-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="9a68f-144">無法建立工作流程檔案，並使用 hello 更新[工作流程設計工具](media-services-workflow-designer.md)工具。</span><span class="sxs-lookup"><span data-stu-id="9a68f-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="9a68f-145">如何在 Azure Media Services 編碼 Premium tooUse</span><span class="sxs-lookup"><span data-stu-id="9a68f-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="9a68f-146">已知問題</span><span class="sxs-lookup"><span data-stu-id="9a68f-146">Known issues</span></span>
<span data-ttu-id="9a68f-147">如果您輸入的視訊不包含字幕，hello 輸出資產仍然會包含空白的 TTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="9a68f-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="9a68f-148">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="9a68f-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9a68f-149">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="9a68f-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="9a68f-150">相關文章</span><span class="sxs-lookup"><span data-stu-id="9a68f-150">Related articles</span></span>
* [<span data-ttu-id="9a68f-151">透過自訂 Media Encoder Standard 預設值來執行進階編碼工作</span><span class="sxs-lookup"><span data-stu-id="9a68f-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="9a68f-152">配額和限制</span><span class="sxs-lookup"><span data-stu-id="9a68f-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
