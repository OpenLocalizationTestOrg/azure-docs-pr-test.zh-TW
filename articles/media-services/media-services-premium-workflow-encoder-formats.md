---
title: "媒體編碼器高階工作流程格式和轉碼器 | Microsoft Docs"
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
ms.openlocfilehash: e18de2adc9aac585d6890dd7b43a54f1a0ca177e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="7e41e-103">媒體編碼器高階工作流程格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="7e41e-104">如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="7e41e-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="7e41e-105">本主題中討論的媒體編碼器高階工作流程媒體處理器無法在中國使用。</span><span class="sxs-lookup"><span data-stu-id="7e41e-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="7e41e-106">本文包含 **Media Encoder Premium Workflow** 編碼器公開預覽版本支援的輸入與輸出檔案格式以及轉碼器清單。</span><span class="sxs-lookup"><span data-stu-id="7e41e-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="7e41e-107">Media Encoder Premium Worflow 輸入格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="7e41e-108">Media Encoder Premium Worflow 輸出格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="7e41e-109">**Media Encoder Premium Workflow** 支援 [本](#closed_captioning) 章節所述的隱藏式字幕。</span><span class="sxs-lookup"><span data-stu-id="7e41e-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="7e41e-110"><a id="input_formats"></a>Media Encoder Premium Worflow 輸入格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="7e41e-111">下節列出此媒體處理器支援做為輸入的轉碼器和檔案格式。</span><span class="sxs-lookup"><span data-stu-id="7e41e-111">The following section lists the codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="7e41e-112">輸入容器/檔案格式</span><span class="sxs-lookup"><span data-stu-id="7e41e-112">Input Container/File Formats</span></span>
* <span data-ttu-id="7e41e-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="7e41e-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="7e41e-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="7e41e-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="7e41e-115">GXF</span><span class="sxs-lookup"><span data-stu-id="7e41e-115">GXF</span></span>
* <span data-ttu-id="7e41e-116">MPEG-2 傳輸資料流</span><span class="sxs-lookup"><span data-stu-id="7e41e-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="7e41e-117">MPEG-2 程式資料流</span><span class="sxs-lookup"><span data-stu-id="7e41e-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="7e41e-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="7e41e-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="7e41e-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="7e41e-119">Windows Media/ASF</span></span>
* <span data-ttu-id="7e41e-120">AVI (未壓縮 8 位元/10 位元)</span><span class="sxs-lookup"><span data-stu-id="7e41e-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="7e41e-121">輸入視訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-121">Input Video Codecs</span></span>
* <span data-ttu-id="7e41e-122">AVC 8 位元/10 位元，高達 4:2:2，包括 AVCIntra</span><span class="sxs-lookup"><span data-stu-id="7e41e-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="7e41e-123">Avid DNxHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="7e41e-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="7e41e-124">DVCPro/DVCProHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="7e41e-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="7e41e-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="7e41e-125">JPEG2000</span></span>
* <span data-ttu-id="7e41e-126">MPEG-2 (高達 422 Profile 和 High Level，包括 XDCAM、XDCAM HD、XDCAM IMX、CableLabs ® 和 D10 等變種)</span><span class="sxs-lookup"><span data-stu-id="7e41e-126">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="7e41e-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="7e41e-127">MPEG-1</span></span>
* <span data-ttu-id="7e41e-128">Windows Media 視訊/VC-1</span><span class="sxs-lookup"><span data-stu-id="7e41e-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="7e41e-129">輸入音訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-129">Input Audio Codecs</span></span>
* <span data-ttu-id="7e41e-130">AES (SMPTE 331M 和 302M，AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="7e41e-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="7e41e-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="7e41e-131">Dolby® E</span></span>
* <span data-ttu-id="7e41e-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="7e41e-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="7e41e-133">AAC (AAC-LC、AAC-HE 和 AAC-HEv2；高達 5.1)</span><span class="sxs-lookup"><span data-stu-id="7e41e-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="7e41e-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="7e41e-134">MPEG Layer 2</span></span>
* <span data-ttu-id="7e41e-135">MP3 (MPEG-1 音訊層 3)</span><span class="sxs-lookup"><span data-stu-id="7e41e-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="7e41e-136">Windows Media 音訊</span><span class="sxs-lookup"><span data-stu-id="7e41e-136">Windows Media Audio</span></span>
* <span data-ttu-id="7e41e-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="7e41e-137">WAV/PCM</span></span>

## <span data-ttu-id="7e41e-138"><a id="output_format"></a>Media Encoder Premium Worflow 輸出格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="7e41e-139">下節列出此媒體處理器支援做為輸出的轉碼器和檔案格式。</span><span class="sxs-lookup"><span data-stu-id="7e41e-139">The following section lists the codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="7e41e-140">輸出容器/檔案格式</span><span class="sxs-lookup"><span data-stu-id="7e41e-140">Output Container/File Formats</span></span>
* <span data-ttu-id="7e41e-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="7e41e-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="7e41e-142">MXF (OP1a、XDCAM 和 AS02)</span><span class="sxs-lookup"><span data-stu-id="7e41e-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="7e41e-143">DPP (包括 AS11)</span><span class="sxs-lookup"><span data-stu-id="7e41e-143">DPP (including AS11)</span></span>
* <span data-ttu-id="7e41e-144">GXF</span><span class="sxs-lookup"><span data-stu-id="7e41e-144">GXF</span></span>
* <span data-ttu-id="7e41e-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="7e41e-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="7e41e-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="7e41e-146">Windows Media/ASF</span></span>
* <span data-ttu-id="7e41e-147">AVI (未壓縮 8 位元/10 位元)</span><span class="sxs-lookup"><span data-stu-id="7e41e-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="7e41e-148">Smooth Streaming 檔案格式 (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="7e41e-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="7e41e-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="7e41e-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="7e41e-150">輸出視訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-150">Output Video Codecs</span></span>
* <span data-ttu-id="7e41e-151">AVC (H.264；8 位元；高達 High Profile、Level 5.2；4K Ultra HD；AVC Intra)</span><span class="sxs-lookup"><span data-stu-id="7e41e-151">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="7e41e-152">Avid DNxHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="7e41e-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="7e41e-153">DVCPro/DVCProHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="7e41e-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="7e41e-154">MPEG-2 (高達 422 Profile 和 High Level，包括 XDCAM、XDCAM HD、XDCAM IMX、CableLabs ® 和 D10 等變種)</span><span class="sxs-lookup"><span data-stu-id="7e41e-154">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="7e41e-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="7e41e-155">MPEG-1</span></span>
* <span data-ttu-id="7e41e-156">Windows Media 視訊/VC-1</span><span class="sxs-lookup"><span data-stu-id="7e41e-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="7e41e-157">JPEG 縮圖建立</span><span class="sxs-lookup"><span data-stu-id="7e41e-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="7e41e-158">輸出音訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="7e41e-158">Output Audio Codecs</span></span>
* <span data-ttu-id="7e41e-159">AES (SMPTE 331M 和 302M，AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="7e41e-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="7e41e-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="7e41e-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="7e41e-161">Dolby® Digital Plus (E-AC3) 高達 7.1</span><span class="sxs-lookup"><span data-stu-id="7e41e-161">Dolby® Digital Plus (E-AC3) up to 7.1</span></span>
* <span data-ttu-id="7e41e-162">AAC (AAC-LC、AAC-HE 和 AAC-HEv2；高達 5.1)</span><span class="sxs-lookup"><span data-stu-id="7e41e-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="7e41e-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="7e41e-163">MPEG Layer 2</span></span>
* <span data-ttu-id="7e41e-164">MP3 (MPEG-1 音訊層 3)</span><span class="sxs-lookup"><span data-stu-id="7e41e-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="7e41e-165">Windows Media 音訊</span><span class="sxs-lookup"><span data-stu-id="7e41e-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="7e41e-166">如果編碼成 Dolby® Digital (AC3)，則輸出只能寫入到 ISO MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="7e41e-166">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="7e41e-167"><a id="closed_captioning"></a>支援隱藏式字幕</span><span class="sxs-lookup"><span data-stu-id="7e41e-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="7e41e-168">內嵌時， **Media Encoder Premium Workflow** 支援：</span><span class="sxs-lookup"><span data-stu-id="7e41e-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="7e41e-169">SCC 檔案</span><span class="sxs-lookup"><span data-stu-id="7e41e-169">SCC files</span></span>
2. <span data-ttu-id="7e41e-170">SMPTE-TT 檔案</span><span class="sxs-lookup"><span data-stu-id="7e41e-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="7e41e-171">CEA-608/CEA-708 – 以使用者資料 (H.264 基礎資料流、ATSC/53、SCTE20 的 SEI 訊息) 的形式傳送，或以 MXF/GXF 檔案中的輔助資料形式傳送</span><span class="sxs-lookup"><span data-stu-id="7e41e-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="7e41e-172">STL 字幕檔案</span><span class="sxs-lookup"><span data-stu-id="7e41e-172">STL subtitle files</span></span>

<span data-ttu-id="7e41e-173">輸出時，可以使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="7e41e-173">On output, the following options are available:</span></span>

1. <span data-ttu-id="7e41e-174">CEA-608 至 CEA-708 翻譯</span><span class="sxs-lookup"><span data-stu-id="7e41e-174">CEA-608 to CEA-708 translation</span></span>
2. <span data-ttu-id="7e41e-175">CEA-608/CEA-708 傳遞 (內嵌在 H.264 基礎資料流的 SEI 訊息，或執行為 MXF 檔案中的輔助資料)</span><span class="sxs-lookup"><span data-stu-id="7e41e-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="7e41e-176">SCC</span><span class="sxs-lookup"><span data-stu-id="7e41e-176">SCC</span></span>
4. <span data-ttu-id="7e41e-177">SMPTE 計時文字 (來自來源 CEA-608 經由 SMPTE RP2052，包括建立 DFXP 檔案)</span><span class="sxs-lookup"><span data-stu-id="7e41e-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="7e41e-178">SRT 副標題檔案</span><span class="sxs-lookup"><span data-stu-id="7e41e-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="7e41e-179">DVB 副標題資料流</span><span class="sxs-lookup"><span data-stu-id="7e41e-179">DVB subtitle streams</span></span>

<span data-ttu-id="7e41e-180">注意：Azure 媒體服務並不支援透過串流傳遞上述所有的輸出格式。</span><span class="sxs-lookup"><span data-stu-id="7e41e-180">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7e41e-181">已知問題</span><span class="sxs-lookup"><span data-stu-id="7e41e-181">Known issues</span></span>
<span data-ttu-id="7e41e-182">如果您的輸入視訊不包含隱藏式字幕，輸出資產仍然會包含空白 TTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="7e41e-182">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="7e41e-183">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="7e41e-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7e41e-184">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="7e41e-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

