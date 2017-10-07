---
title: "aaaMedia 編碼器高階工作流程格式和轉碼器 |Microsoft 文件"
description: "本主題提供 Media Encoder Premium Workflow 格式和轉碼器的概觀"
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="c76d4-103">媒體編碼器高階工作流程格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="c76d4-104">如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="c76d4-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="c76d4-105">本主題中討論的媒體編碼器高階工作流程媒體處理器無法在中國使用。</span><span class="sxs-lookup"><span data-stu-id="c76d4-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="c76d4-106">本文件包含一份輸入和輸出檔案格式的 hello hello 公用預覽版本所支援的轉碼器**媒體編碼器高階工作流程**編碼器。</span><span class="sxs-lookup"><span data-stu-id="c76d4-106">This document contains a list of input and output file formats and codecs that are supported by hello public preview version of hello **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="c76d4-107">Media Encoder Premium Worflow 輸入格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="c76d4-108">Media Encoder Premium Worflow 輸出格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="c76d4-109">**Media Encoder Premium Workflow** 支援 [本](#closed_captioning) 章節所述的隱藏式字幕。</span><span class="sxs-lookup"><span data-stu-id="c76d4-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="c76d4-110"><a id="input_formats"></a>Media Encoder Premium Worflow 輸入格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="c76d4-111">hello 下列區段會列出此媒體處理器支援做為輸入的 hello 轉碼器與檔案格式。</span><span class="sxs-lookup"><span data-stu-id="c76d4-111">hello following section lists hello codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="c76d4-112">輸入容器/檔案格式</span><span class="sxs-lookup"><span data-stu-id="c76d4-112">Input Container/File Formats</span></span>
* <span data-ttu-id="c76d4-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="c76d4-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="c76d4-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="c76d4-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="c76d4-115">GXF</span><span class="sxs-lookup"><span data-stu-id="c76d4-115">GXF</span></span>
* <span data-ttu-id="c76d4-116">MPEG-2 傳輸資料流</span><span class="sxs-lookup"><span data-stu-id="c76d4-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="c76d4-117">MPEG-2 程式資料流</span><span class="sxs-lookup"><span data-stu-id="c76d4-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="c76d4-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="c76d4-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="c76d4-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="c76d4-119">Windows Media/ASF</span></span>
* <span data-ttu-id="c76d4-120">AVI (未壓縮 8 位元/10 位元)</span><span class="sxs-lookup"><span data-stu-id="c76d4-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="c76d4-121">輸入視訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-121">Input Video Codecs</span></span>
* <span data-ttu-id="c76d4-122">AVC 8 位元/10 位元，向上 too4:2:2，包括 AVCIntra</span><span class="sxs-lookup"><span data-stu-id="c76d4-122">AVC 8-bit/10-bit, up too4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="c76d4-123">Avid DNxHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="c76d4-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="c76d4-124">DVCPro/DVCProHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="c76d4-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="c76d4-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="c76d4-125">JPEG2000</span></span>
* <span data-ttu-id="c76d4-126">Mpeg-2 （too422 設定檔和高的層級，包括變數，例如 XDCAM、 XDCAM HD、 XDCAM /IMX、 CableLabs® 和 D10）</span><span class="sxs-lookup"><span data-stu-id="c76d4-126">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="c76d4-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="c76d4-127">MPEG-1</span></span>
* <span data-ttu-id="c76d4-128">Windows Media 視訊/VC-1</span><span class="sxs-lookup"><span data-stu-id="c76d4-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="c76d4-129">輸入音訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-129">Input Audio Codecs</span></span>
* <span data-ttu-id="c76d4-130">AES (SMPTE 331M 和 302M，AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="c76d4-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="c76d4-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="c76d4-131">Dolby® E</span></span>
* <span data-ttu-id="c76d4-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="c76d4-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="c76d4-133">AAC (AAC-LC、 AAC 他和 AAC HEv2; up too5.1)</span><span class="sxs-lookup"><span data-stu-id="c76d4-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="c76d4-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="c76d4-134">MPEG Layer 2</span></span>
* <span data-ttu-id="c76d4-135">MP3 (MPEG-1 音訊層 3)</span><span class="sxs-lookup"><span data-stu-id="c76d4-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="c76d4-136">Windows Media 音訊</span><span class="sxs-lookup"><span data-stu-id="c76d4-136">Windows Media Audio</span></span>
* <span data-ttu-id="c76d4-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="c76d4-137">WAV/PCM</span></span>

## <span data-ttu-id="c76d4-138"><a id="output_format"></a>Media Encoder Premium Worflow 輸出格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="c76d4-139">hello 下節列出支援此媒體處理器從輸出中的 hello 轉碼器與檔案格式。</span><span class="sxs-lookup"><span data-stu-id="c76d4-139">hello following section lists hello codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="c76d4-140">輸出容器/檔案格式</span><span class="sxs-lookup"><span data-stu-id="c76d4-140">Output Container/File Formats</span></span>
* <span data-ttu-id="c76d4-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="c76d4-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="c76d4-142">MXF (OP1a、XDCAM 和 AS02)</span><span class="sxs-lookup"><span data-stu-id="c76d4-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="c76d4-143">DPP (包括 AS11)</span><span class="sxs-lookup"><span data-stu-id="c76d4-143">DPP (including AS11)</span></span>
* <span data-ttu-id="c76d4-144">GXF</span><span class="sxs-lookup"><span data-stu-id="c76d4-144">GXF</span></span>
* <span data-ttu-id="c76d4-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="c76d4-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="c76d4-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="c76d4-146">Windows Media/ASF</span></span>
* <span data-ttu-id="c76d4-147">AVI (未壓縮 8 位元/10 位元)</span><span class="sxs-lookup"><span data-stu-id="c76d4-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="c76d4-148">Smooth Streaming 檔案格式 (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="c76d4-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="c76d4-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="c76d4-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="c76d4-150">輸出視訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-150">Output Video Codecs</span></span>
* <span data-ttu-id="c76d4-151">AVC (H.264; 8 位元; 向上 tooHigh 設定檔，層級 5.2; 4k 強力 HD;AVC 內部）</span><span class="sxs-lookup"><span data-stu-id="c76d4-151">AVC (H.264; 8-bit; up tooHigh Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="c76d4-152">Avid DNxHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="c76d4-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="c76d4-153">DVCPro/DVCProHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="c76d4-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="c76d4-154">Mpeg-2 （too422 設定檔和高的層級，包括變數，例如 XDCAM、 XDCAM HD、 XDCAM /IMX、 CableLabs® 和 D10）</span><span class="sxs-lookup"><span data-stu-id="c76d4-154">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="c76d4-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="c76d4-155">MPEG-1</span></span>
* <span data-ttu-id="c76d4-156">Windows Media 視訊/VC-1</span><span class="sxs-lookup"><span data-stu-id="c76d4-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="c76d4-157">JPEG 縮圖建立</span><span class="sxs-lookup"><span data-stu-id="c76d4-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="c76d4-158">輸出音訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="c76d4-158">Output Audio Codecs</span></span>
* <span data-ttu-id="c76d4-159">AES (SMPTE 331M 和 302M，AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="c76d4-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="c76d4-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="c76d4-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="c76d4-161">Dolby® Digital Plus (E AC3) 向上 too7.1</span><span class="sxs-lookup"><span data-stu-id="c76d4-161">Dolby® Digital Plus (E-AC3) up too7.1</span></span>
* <span data-ttu-id="c76d4-162">AAC (AAC-LC、 AAC 他和 AAC HEv2; up too5.1)</span><span class="sxs-lookup"><span data-stu-id="c76d4-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="c76d4-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="c76d4-163">MPEG Layer 2</span></span>
* <span data-ttu-id="c76d4-164">MP3 (MPEG-1 音訊層 3)</span><span class="sxs-lookup"><span data-stu-id="c76d4-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="c76d4-165">Windows Media 音訊</span><span class="sxs-lookup"><span data-stu-id="c76d4-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="c76d4-166">如果編碼 tooDolby® 數位 (AC3)，hello 輸出只可以寫入的 ISO MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="c76d4-166">If you encode tooDolby® Digital (AC3), hello output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="c76d4-167"><a id="closed_captioning"></a>支援隱藏式字幕</span><span class="sxs-lookup"><span data-stu-id="c76d4-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="c76d4-168">內嵌時， **Media Encoder Premium Workflow** 支援：</span><span class="sxs-lookup"><span data-stu-id="c76d4-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="c76d4-169">SCC 檔案</span><span class="sxs-lookup"><span data-stu-id="c76d4-169">SCC files</span></span>
2. <span data-ttu-id="c76d4-170">SMPTE-TT 檔案</span><span class="sxs-lookup"><span data-stu-id="c76d4-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="c76d4-171">CEA-608/CEA-708 – 以使用者資料 (H.264 基礎資料流、ATSC/53、SCTE20 的 SEI 訊息) 的形式傳送，或以 MXF/GXF 檔案中的輔助資料形式傳送</span><span class="sxs-lookup"><span data-stu-id="c76d4-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="c76d4-172">STL 字幕檔案</span><span class="sxs-lookup"><span data-stu-id="c76d4-172">STL subtitle files</span></span>

<span data-ttu-id="c76d4-173">在輸出時，hello 下列選項可用：</span><span class="sxs-lookup"><span data-stu-id="c76d4-173">On output, hello following options are available:</span></span>

1. <span data-ttu-id="c76d4-174">CEA 608 tooCEA 708 轉譯</span><span class="sxs-lookup"><span data-stu-id="c76d4-174">CEA-608 tooCEA-708 translation</span></span>
2. <span data-ttu-id="c76d4-175">CEA-608/CEA-708 傳遞 (內嵌在 H.264 基礎資料流的 SEI 訊息，或執行為 MXF 檔案中的輔助資料)</span><span class="sxs-lookup"><span data-stu-id="c76d4-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="c76d4-176">SCC</span><span class="sxs-lookup"><span data-stu-id="c76d4-176">SCC</span></span>
4. <span data-ttu-id="c76d4-177">SMPTE 計時文字 (來自來源 CEA-608 經由 SMPTE RP2052，包括建立 DFXP 檔案)</span><span class="sxs-lookup"><span data-stu-id="c76d4-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="c76d4-178">SRT 副標題檔案</span><span class="sxs-lookup"><span data-stu-id="c76d4-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="c76d4-179">DVB 副標題資料流</span><span class="sxs-lookup"><span data-stu-id="c76d4-179">DVB subtitle streams</span></span>

<span data-ttu-id="c76d4-180">注意： 不支援所有的 hello 上面的輸出格式是透過 Azure Media Services 串流傳遞。</span><span class="sxs-lookup"><span data-stu-id="c76d4-180">Note: not all of hello above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c76d4-181">已知問題</span><span class="sxs-lookup"><span data-stu-id="c76d4-181">Known issues</span></span>
<span data-ttu-id="c76d4-182">如果您輸入的視訊不包含字幕，hello 輸出資產仍然會包含空白的 TTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="c76d4-182">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="c76d4-183">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="c76d4-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c76d4-184">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c76d4-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

