---
title: "Azure 隨選媒體編碼器的概觀和比較 | Microsoft Docs"
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
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="c980c-103">Azure 隨選媒體編碼器的概觀和比較</span><span class="sxs-lookup"><span data-stu-id="c980c-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="c980c-104">編碼概觀</span><span class="sxs-lookup"><span data-stu-id="c980c-104">Encoding overview</span></span>
<span data-ttu-id="c980c-105">Azure 媒體服務提供多個用於將雲端中之媒體編碼的選項。</span><span class="sxs-lookup"><span data-stu-id="c980c-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="c980c-106">開始使用媒體服務時，請務必了解轉碼器和檔案格式之間的差異。</span><span class="sxs-lookup"><span data-stu-id="c980c-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="c980c-107">轉碼器是實作壓縮/解壓縮演算法的軟體，而檔案格式是保存已壓縮視訊的容器。</span><span class="sxs-lookup"><span data-stu-id="c980c-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="c980c-108">「媒體服務」提供動態封裝，這可讓您以「媒體服務」支援的串流格式 (MPEG DASH、HLS、Smooth Streaming) 提供調適性位元速率 MP4 或 Smooth Streaming 編碼內容，而不必重新封裝成這些串流格式。</span><span class="sxs-lookup"><span data-stu-id="c980c-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="c980c-109">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c980c-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="c980c-110">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="c980c-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="c980c-111">若要利用 [動態封裝](media-services-dynamic-packaging-overview.md)，您需要執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c980c-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="c980c-112">此外，請將您的來源檔案編碼成一組調適性位元速率 MP4 檔案或調適性位元速率 Smooth Streaming 檔案 (本教學課程稍後會示範編碼步驟)。</span><span class="sxs-lookup"><span data-stu-id="c980c-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="c980c-113">媒體服務支援本文中所描述的下列隨選編碼器：</span><span class="sxs-lookup"><span data-stu-id="c980c-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="c980c-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="c980c-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="c980c-115">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="c980c-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="c980c-116">本文概略敘述隨選媒體編碼器，並提供文章連結以提供更詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c980c-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="c980c-117">本主題也提供各種編碼器的比較。</span><span class="sxs-lookup"><span data-stu-id="c980c-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="c980c-118">依預設，每個媒體服務帳戶一次可以有一個進行中的編碼工作。</span><span class="sxs-lookup"><span data-stu-id="c980c-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="c980c-119">您可以保留編碼單位，這樣就可以同時執行多個編碼工作，其中一個用於您購買的每一個編碼保留單位。</span><span class="sxs-lookup"><span data-stu-id="c980c-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="c980c-120">如需相關資訊，請參閱 [調整編碼單位](media-services-scale-media-processing-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c980c-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="c980c-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="c980c-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="c980c-122">使用方式</span><span class="sxs-lookup"><span data-stu-id="c980c-122">How to use</span></span>
[<span data-ttu-id="c980c-123">如何使用 Media Encoder Standard 進行編碼</span><span class="sxs-lookup"><span data-stu-id="c980c-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="c980c-124">格式</span><span class="sxs-lookup"><span data-stu-id="c980c-124">Formats</span></span>
[<span data-ttu-id="c980c-125">格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="c980c-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="c980c-126">預設值</span><span class="sxs-lookup"><span data-stu-id="c980c-126">Presets</span></span>
<span data-ttu-id="c980c-127">Media Encoder Standard 使用 [這裡](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)描述的其中一個編碼器預設值進行設定。</span><span class="sxs-lookup"><span data-stu-id="c980c-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="c980c-128">輸入和輸出中繼資料</span><span class="sxs-lookup"><span data-stu-id="c980c-128">Input and output metadata</span></span>
<span data-ttu-id="c980c-129">[這裡](media-services-input-metadata-schema.md)說明編碼器輸入中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c980c-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="c980c-130">[這裡](media-services-output-metadata-schema.md)說明編碼器輸出中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c980c-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="c980c-131">產生縮圖</span><span class="sxs-lookup"><span data-stu-id="c980c-131">Generate thumbnails</span></span>
<span data-ttu-id="c980c-132">如需相關資訊，請參閱 [如何使用媒體編碼器標準產生縮圖](media-services-advanced-encoding-with-mes.md#thumbnails)。</span><span class="sxs-lookup"><span data-stu-id="c980c-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="c980c-133">修剪視訊 (裁剪)</span><span class="sxs-lookup"><span data-stu-id="c980c-133">Trim videos (clipping)</span></span>
<span data-ttu-id="c980c-134">如需相關資訊，請參閱 [如何使用媒體編碼器標準修剪視訊](media-services-advanced-encoding-with-mes.md#trim_video)。</span><span class="sxs-lookup"><span data-stu-id="c980c-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="c980c-135">建立疊加層</span><span class="sxs-lookup"><span data-stu-id="c980c-135">Create overlays</span></span>
<span data-ttu-id="c980c-136">如需相關資訊，請參閱 [如何使用媒體編碼器標準建立覆疊](media-services-advanced-encoding-with-mes.md#overlay)。</span><span class="sxs-lookup"><span data-stu-id="c980c-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="c980c-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c980c-137">See also</span></span>
[<span data-ttu-id="c980c-138">媒體服務部落格</span><span class="sxs-lookup"><span data-stu-id="c980c-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="c980c-139">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="c980c-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="c980c-140">Overview</span><span class="sxs-lookup"><span data-stu-id="c980c-140">Overview</span></span>
[<span data-ttu-id="c980c-141">介紹 Azure 媒體服務中的 Premium 編碼</span><span class="sxs-lookup"><span data-stu-id="c980c-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="c980c-142">使用方式</span><span class="sxs-lookup"><span data-stu-id="c980c-142">How to use</span></span>
<span data-ttu-id="c980c-143">Media Encoder Premium Workflow 使用複雜的工作流程設定。</span><span class="sxs-lookup"><span data-stu-id="c980c-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="c980c-144">您可以使用 [工作流程設計工具](media-services-workflow-designer.md) 建立和更新工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="c980c-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="c980c-145">如何使用 Azure 媒體服務中的 Premium 編碼</span><span class="sxs-lookup"><span data-stu-id="c980c-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="c980c-146">已知問題</span><span class="sxs-lookup"><span data-stu-id="c980c-146">Known issues</span></span>
<span data-ttu-id="c980c-147">如果您的輸入視訊不包含隱藏式字幕，輸出資產仍然會包含空白 TTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="c980c-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="c980c-148">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="c980c-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c980c-149">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c980c-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="c980c-150">相關文章</span><span class="sxs-lookup"><span data-stu-id="c980c-150">Related articles</span></span>
* [<span data-ttu-id="c980c-151">透過自訂 Media Encoder Standard 預設值來執行進階編碼工作</span><span class="sxs-lookup"><span data-stu-id="c980c-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="c980c-152">配額和限制</span><span class="sxs-lookup"><span data-stu-id="c980c-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
