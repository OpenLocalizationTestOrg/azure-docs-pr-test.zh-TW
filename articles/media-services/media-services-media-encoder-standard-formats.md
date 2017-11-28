---
title: "aaaMedia 編碼器標準格式和轉碼器"
description: "本主題提供媒體編碼器標準格式和轉碼器的概觀。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 51a67f372dff579383ffcfa988e8f4d38ad44a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-formats-and-codecs"></a><span data-ttu-id="5c771-103">Media Encoder Standard 格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="5c771-103">Media Encoder Standard Formats and Codecs</span></span>
<span data-ttu-id="5c771-104">本文件包含一份 hello 最常見匯入和匯出檔案格式，您可以使用標準的媒體編碼器。</span><span class="sxs-lookup"><span data-stu-id="5c771-104">This document contains a list of hello most common import and export file formats that you can use with Media Encoder Standard.</span></span>

## <a name="input-containerfile-formats"></a><span data-ttu-id="5c771-105">輸入容器/檔案格式</span><span class="sxs-lookup"><span data-stu-id="5c771-105">Input Container/File Formats</span></span>
| <span data-ttu-id="5c771-106">檔案格式 (副檔名)</span><span class="sxs-lookup"><span data-stu-id="5c771-106">File formats (file extensions)</span></span> | <span data-ttu-id="5c771-107">支援</span><span class="sxs-lookup"><span data-stu-id="5c771-107">Supported</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5c771-108">FLV (使用 H.264 和 AAC 轉碼器) (.flv)</span><span class="sxs-lookup"><span data-stu-id="5c771-108">FLV (with H.264 and AAC codecs) (.flv)</span></span> |<span data-ttu-id="5c771-109">yes</span><span class="sxs-lookup"><span data-stu-id="5c771-109">Yes</span></span> |
| <span data-ttu-id="5c771-110">MXF    (.mxf)</span><span class="sxs-lookup"><span data-stu-id="5c771-110">MXF    (.mxf)</span></span> |<span data-ttu-id="5c771-111">yes</span><span class="sxs-lookup"><span data-stu-id="5c771-111">Yes</span></span> |
| <span data-ttu-id="5c771-112">GXF    (.gxf)</span><span class="sxs-lookup"><span data-stu-id="5c771-112">GXF    (.gxf)</span></span> |<span data-ttu-id="5c771-113">yes</span><span class="sxs-lookup"><span data-stu-id="5c771-113">Yes</span></span> |
| <span data-ttu-id="5c771-114">MPEG2-PS、MPEG2-TS、3GP (.ts、.ps、.3gp、.3gpp、.mpg)</span><span class="sxs-lookup"><span data-stu-id="5c771-114">MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg)</span></span> |<span data-ttu-id="5c771-115">是</span><span class="sxs-lookup"><span data-stu-id="5c771-115">Yes</span></span> |
| <span data-ttu-id="5c771-116">Windows Media 視訊 (WMV)/ASF (.wmv、.asf)</span><span class="sxs-lookup"><span data-stu-id="5c771-116">Windows Media Video (WMV)/ASF (.wmv, .asf)</span></span> |<span data-ttu-id="5c771-117">是</span><span class="sxs-lookup"><span data-stu-id="5c771-117">Yes</span></span> |
| <span data-ttu-id="5c771-118">AVI (未壓縮 8 位元/10 位元) (.avi)</span><span class="sxs-lookup"><span data-stu-id="5c771-118">AVI (Uncompressed 8bit/10bit) (.avi)</span></span> |<span data-ttu-id="5c771-119">是</span><span class="sxs-lookup"><span data-stu-id="5c771-119">Yes</span></span> |
| <span data-ttu-id="5c771-120">MP4 (.mp4、.m4a、.m4v)/ISMV (.isma、.ismv)</span><span class="sxs-lookup"><span data-stu-id="5c771-120">MP4 (.mp4, .m4a, .m4v)/ISMV (.isma, .ismv)</span></span> |<span data-ttu-id="5c771-121">是</span><span class="sxs-lookup"><span data-stu-id="5c771-121">Yes</span></span> |
| <span data-ttu-id="5c771-122">[Microsoft Digital Video Recording (DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms)</span><span class="sxs-lookup"><span data-stu-id="5c771-122">[Microsoft Digital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms)</span></span> |<span data-ttu-id="5c771-123">是</span><span class="sxs-lookup"><span data-stu-id="5c771-123">Yes</span></span> |
| <span data-ttu-id="5c771-124">Matroska/WebM (.mkv)</span><span class="sxs-lookup"><span data-stu-id="5c771-124">Matroska/WebM (.mkv)</span></span> |<span data-ttu-id="5c771-125">是</span><span class="sxs-lookup"><span data-stu-id="5c771-125">Yes</span></span> |
| <span data-ttu-id="5c771-126">WAVE/WAV (.wav)</span><span class="sxs-lookup"><span data-stu-id="5c771-126">WAVE/WAV (.wav)</span></span> |<span data-ttu-id="5c771-127">是</span><span class="sxs-lookup"><span data-stu-id="5c771-127">Yes</span></span> |
| <span data-ttu-id="5c771-128">QuickTime (.mov)</span><span class="sxs-lookup"><span data-stu-id="5c771-128">QuickTime (.mov)</span></span> |<span data-ttu-id="5c771-129">是</span><span class="sxs-lookup"><span data-stu-id="5c771-129">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="5c771-130">上方是一個 hello 更常見的副檔名清單。</span><span class="sxs-lookup"><span data-stu-id="5c771-130">Above is a list of hello more commonly encountered file extensions.</span></span> <span data-ttu-id="5c771-131">Media Encoder Standard 支援許多其他副檔名 (例如，.m2ts、.mpeg2video 和 .qt)。</span><span class="sxs-lookup"><span data-stu-id="5c771-131">Media Encoder Standard does support many others (for example: .m2ts, .mpeg2video, .qt).</span></span> <span data-ttu-id="5c771-132">如果 tooencode 檔案再試一次，並且收到不支援的 hello 格式的相關錯誤訊息，請提供意見反應[這裡](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/)。</span><span class="sxs-lookup"><span data-stu-id="5c771-132">If you try tooencode a file and you get an error message about hello format not being supported, please provide a feedback [here](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).</span></span>
> 
> 

### <a name="audio-formats-in-input-containers"></a><span data-ttu-id="5c771-133">輸入容器中的音訊格式</span><span class="sxs-lookup"><span data-stu-id="5c771-133">Audio formats in input containers</span></span>
<span data-ttu-id="5c771-134">媒體編碼器標準支援下列輸入容器中的音訊格式攜帶 hello:</span><span class="sxs-lookup"><span data-stu-id="5c771-134">Media Encoder Standard supports carrying hello following audio formats in input containers:</span></span>

* <span data-ttu-id="5c771-135">MXF、GXF 和 QuickTime 檔案，其具有交錯立體聲或 5.1 範例的音訊音軌</span><span class="sxs-lookup"><span data-stu-id="5c771-135">MXF, GXF and QuickTime files which have audio tracks with interleaved stereo or 5.1 samples</span></span>

<span data-ttu-id="5c771-136">或</span><span class="sxs-lookup"><span data-stu-id="5c771-136">or</span></span>

* <span data-ttu-id="5c771-137">而為個別的 PCM 曲目，但 hello 通道對應來運送 hello 音訊 MXF、 GXF 及 QuickTime 檔案 （toostereo 或 5.1） 可以推算 hello 檔案中繼資料</span><span class="sxs-lookup"><span data-stu-id="5c771-137">MXF, GXF and QuickTime files where hello audio is carried as separate PCM tracks but hello channel mapping (toostereo or 5.1) can be deduced from hello file metadata</span></span>

<span data-ttu-id="5c771-138">請注意 hello 附近未來將提供明確/使用者提供的通道對應支援。</span><span class="sxs-lookup"><span data-stu-id="5c771-138">Note that support for explicit/user-supplied channel mapping will be provided in hello near future.</span></span>

## <a name="input-video-codecs"></a><span data-ttu-id="5c771-139">輸入視訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="5c771-139">Input Video Codecs</span></span>
| <span data-ttu-id="5c771-140">輸入視訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="5c771-140">Input Video Codecs</span></span> | <span data-ttu-id="5c771-141">支援</span><span class="sxs-lookup"><span data-stu-id="5c771-141">Supported</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5c771-142">AVC 8 位元/10 位元，向上 too4:2:2，包括 AVCIntra</span><span class="sxs-lookup"><span data-stu-id="5c771-142">AVC 8-bit/10-bit, up too4:2:2, including AVCIntra</span></span> |<span data-ttu-id="5c771-143">8 位元 4:2:0 和 4:2:2</span><span class="sxs-lookup"><span data-stu-id="5c771-143">8 bit 4:2:0 and 4:2:2</span></span> |
| <span data-ttu-id="5c771-144">Avid DNxHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="5c771-144">Avid DNxHD (in MXF)</span></span> |<span data-ttu-id="5c771-145">是</span><span class="sxs-lookup"><span data-stu-id="5c771-145">Yes</span></span> |
| <span data-ttu-id="5c771-146">DVCPro/DVCProHD (使用 MXF)</span><span class="sxs-lookup"><span data-stu-id="5c771-146">DVCPro/DVCProHD (in MXF)</span></span> |<span data-ttu-id="5c771-147">是</span><span class="sxs-lookup"><span data-stu-id="5c771-147">Yes</span></span> |
| <span data-ttu-id="5c771-148">數位視訊 (DV) (使用 AVI 檔案)</span><span class="sxs-lookup"><span data-stu-id="5c771-148">Digital video (DV) (in AVI files)</span></span> |<span data-ttu-id="5c771-149">是</span><span class="sxs-lookup"><span data-stu-id="5c771-149">Yes</span></span> |
| <span data-ttu-id="5c771-150">JPEG 2000</span><span class="sxs-lookup"><span data-stu-id="5c771-150">JPEG 2000</span></span> |<span data-ttu-id="5c771-151">是</span><span class="sxs-lookup"><span data-stu-id="5c771-151">Yes</span></span> |
| <span data-ttu-id="5c771-152">Mpeg-2 （too422 設定檔和高的層級，包括變數，例如 XDCAM、 XDCAM HD、 XDCAM /IMX、 CableLabs® 和 D10）</span><span class="sxs-lookup"><span data-stu-id="5c771-152">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span> |<span data-ttu-id="5c771-153">Too422 設定檔</span><span class="sxs-lookup"><span data-stu-id="5c771-153">Up too422 Profile</span></span> |
| <span data-ttu-id="5c771-154">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="5c771-154">MPEG-1</span></span> |<span data-ttu-id="5c771-155">是</span><span class="sxs-lookup"><span data-stu-id="5c771-155">Yes</span></span> |
| <span data-ttu-id="5c771-156">VC-1/WMV9</span><span class="sxs-lookup"><span data-stu-id="5c771-156">VC-1/WMV9</span></span> |<span data-ttu-id="5c771-157">是</span><span class="sxs-lookup"><span data-stu-id="5c771-157">Yes</span></span> |
| <span data-ttu-id="5c771-158">Canopus HQ/HQX</span><span class="sxs-lookup"><span data-stu-id="5c771-158">Canopus HQ/HQX</span></span> |<span data-ttu-id="5c771-159">否</span><span class="sxs-lookup"><span data-stu-id="5c771-159">No</span></span> |
| <span data-ttu-id="5c771-160">Mpeg-4 第 2 部分</span><span class="sxs-lookup"><span data-stu-id="5c771-160">MPEG-4 Part 2</span></span> |<span data-ttu-id="5c771-161">是</span><span class="sxs-lookup"><span data-stu-id="5c771-161">Yes</span></span> |
| [<span data-ttu-id="5c771-162">Theora</span><span class="sxs-lookup"><span data-stu-id="5c771-162">Theora</span></span>](https://en.wikipedia.org/wiki/Theora) |<span data-ttu-id="5c771-163">是</span><span class="sxs-lookup"><span data-stu-id="5c771-163">Yes</span></span> |
| <span data-ttu-id="5c771-164">YUV420 未壓縮或夾層</span><span class="sxs-lookup"><span data-stu-id="5c771-164">YUV420 uncompressed, or mezzanine</span></span> |<span data-ttu-id="5c771-165">是</span><span class="sxs-lookup"><span data-stu-id="5c771-165">Yes</span></span> |
| <span data-ttu-id="5c771-166">Apple ProRes 422</span><span class="sxs-lookup"><span data-stu-id="5c771-166">Apple ProRes 422</span></span> |<span data-ttu-id="5c771-167">是</span><span class="sxs-lookup"><span data-stu-id="5c771-167">Yes</span></span> |
| <span data-ttu-id="5c771-168">Apple ProRes 422 LT</span><span class="sxs-lookup"><span data-stu-id="5c771-168">Apple ProRes 422 LT</span></span> |<span data-ttu-id="5c771-169">是</span><span class="sxs-lookup"><span data-stu-id="5c771-169">Yes</span></span> |
| <span data-ttu-id="5c771-170">Apple ProRes 422 HQ</span><span class="sxs-lookup"><span data-stu-id="5c771-170">Apple ProRes 422 HQ</span></span> |<span data-ttu-id="5c771-171">是</span><span class="sxs-lookup"><span data-stu-id="5c771-171">Yes</span></span> |
| <span data-ttu-id="5c771-172">Apple ProRes Proxy</span><span class="sxs-lookup"><span data-stu-id="5c771-172">Apple ProRes Proxy</span></span> |<span data-ttu-id="5c771-173">是</span><span class="sxs-lookup"><span data-stu-id="5c771-173">Yes</span></span> |
| <span data-ttu-id="5c771-174">Apple ProRes 4444</span><span class="sxs-lookup"><span data-stu-id="5c771-174">Apple ProRes 4444</span></span> |<span data-ttu-id="5c771-175">是</span><span class="sxs-lookup"><span data-stu-id="5c771-175">Yes</span></span> |
| <span data-ttu-id="5c771-176">Apple ProRes 4444 XQ</span><span class="sxs-lookup"><span data-stu-id="5c771-176">Apple ProRes 4444 XQ</span></span> |<span data-ttu-id="5c771-177">是</span><span class="sxs-lookup"><span data-stu-id="5c771-177">Yes</span></span> |

## <a name="input-audio-codecs"></a><span data-ttu-id="5c771-178">輸入音訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="5c771-178">Input Audio Codecs</span></span>
| <span data-ttu-id="5c771-179">輸入音訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="5c771-179">Input Audio Codecs</span></span> | <span data-ttu-id="5c771-180">支援</span><span class="sxs-lookup"><span data-stu-id="5c771-180">Supported</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5c771-181">AAC (AAC-LC、 AAC 他和 AAC HEv2; up too5.1)</span><span class="sxs-lookup"><span data-stu-id="5c771-181">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span> |<span data-ttu-id="5c771-182">是</span><span class="sxs-lookup"><span data-stu-id="5c771-182">Yes</span></span> |
| <span data-ttu-id="5c771-183">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="5c771-183">MPEG Layer 2</span></span> |<span data-ttu-id="5c771-184">是</span><span class="sxs-lookup"><span data-stu-id="5c771-184">Yes</span></span> |
| <span data-ttu-id="5c771-185">MP3 (MPEG-1 音訊層 3)</span><span class="sxs-lookup"><span data-stu-id="5c771-185">MP3 (MPEG-1 Audio Layer 3)</span></span> |<span data-ttu-id="5c771-186">是</span><span class="sxs-lookup"><span data-stu-id="5c771-186">Yes</span></span> |
| <span data-ttu-id="5c771-187">Windows Media 音訊</span><span class="sxs-lookup"><span data-stu-id="5c771-187">Windows Media Audio</span></span> |<span data-ttu-id="5c771-188">是</span><span class="sxs-lookup"><span data-stu-id="5c771-188">Yes</span></span> |
| <span data-ttu-id="5c771-189">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="5c771-189">WAV/PCM</span></span> |<span data-ttu-id="5c771-190">是</span><span class="sxs-lookup"><span data-stu-id="5c771-190">Yes</span></span> |
| <span data-ttu-id="5c771-191">[FLAC](https://en.wikipedia.org/wiki/FLAC)</a></span><span class="sxs-lookup"><span data-stu-id="5c771-191">[FLAC](https://en.wikipedia.org/wiki/FLAC)</a></span></span> |<span data-ttu-id="5c771-192">是</span><span class="sxs-lookup"><span data-stu-id="5c771-192">Yes</span></span> |
| [<span data-ttu-id="5c771-193">Opus</span><span class="sxs-lookup"><span data-stu-id="5c771-193">Opus</span></span>](http://go.microsoft.com/fwlink/?LinkId=822667) |<span data-ttu-id="5c771-194">是</span><span class="sxs-lookup"><span data-stu-id="5c771-194">Yes</span></span> |
| <span data-ttu-id="5c771-195">[Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a></span><span class="sxs-lookup"><span data-stu-id="5c771-195">[Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a></span></span> |<span data-ttu-id="5c771-196">是</span><span class="sxs-lookup"><span data-stu-id="5c771-196">Yes</span></span> |
| <span data-ttu-id="5c771-197">AMR (可變多速率)</span><span class="sxs-lookup"><span data-stu-id="5c771-197">AMR (adaptive multi-rate)</span></span> |<span data-ttu-id="5c771-198">是</span><span class="sxs-lookup"><span data-stu-id="5c771-198">Yes</span></span> |
| <span data-ttu-id="5c771-199">AES (SMPTE 331M 和 302M，AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="5c771-199">AES (SMPTE 331M and 302M, AES3-2003)</span></span> |<span data-ttu-id="5c771-200">否</span><span class="sxs-lookup"><span data-stu-id="5c771-200">No</span></span> |
| <span data-ttu-id="5c771-201">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="5c771-201">Dolby® E</span></span> |<span data-ttu-id="5c771-202">否</span><span class="sxs-lookup"><span data-stu-id="5c771-202">No</span></span> |
| <span data-ttu-id="5c771-203">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="5c771-203">Dolby® Digital (AC3)</span></span> |<span data-ttu-id="5c771-204">否</span><span class="sxs-lookup"><span data-stu-id="5c771-204">No</span></span> |
| <span data-ttu-id="5c771-205">Dolby® Digital Plus (E-AC3)</span><span class="sxs-lookup"><span data-stu-id="5c771-205">Dolby® Digital Plus (E-AC3)</span></span> |<span data-ttu-id="5c771-206">否</span><span class="sxs-lookup"><span data-stu-id="5c771-206">No</span></span> |

## <a name="output-formats-and-codecs"></a><span data-ttu-id="5c771-207">輸出格式和轉碼器</span><span class="sxs-lookup"><span data-stu-id="5c771-207">Output Formats and codecs</span></span>
<span data-ttu-id="5c771-208">hello 下表列出支援匯出的 hello 轉碼器與檔案格式。</span><span class="sxs-lookup"><span data-stu-id="5c771-208">hello following table lists hello codecs and file formats that are supported for export.</span></span>

| <span data-ttu-id="5c771-209">檔案格式</span><span class="sxs-lookup"><span data-stu-id="5c771-209">File Format</span></span> | <span data-ttu-id="5c771-210">視訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="5c771-210">Video Codec</span></span> | <span data-ttu-id="5c771-211">音訊轉碼器</span><span class="sxs-lookup"><span data-stu-id="5c771-211">Audio Codec</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c771-212">MP4 </span><span class="sxs-lookup"><span data-stu-id="5c771-212">MP4</span></span> <br/><br/><span data-ttu-id="5c771-213">(包括多位元速率 MP4 容器)</span><span class="sxs-lookup"><span data-stu-id="5c771-213">(including multi-bitrate MP4 containers)</span></span> |<span data-ttu-id="5c771-214">H.264 (高、主要和基準設定檔)</span><span class="sxs-lookup"><span data-stu-id="5c771-214">H.264 (High, Main, and Baseline Profiles)</span></span> |<span data-ttu-id="5c771-215">AAC-LC、HE-AAC v1、HE-AAC v2</span><span class="sxs-lookup"><span data-stu-id="5c771-215">AAC-LC, HE-AAC v1, HE-AAC v2</span></span> |
| <span data-ttu-id="5c771-216">MPEG2-TS</span><span class="sxs-lookup"><span data-stu-id="5c771-216">MPEG2-TS</span></span> |<span data-ttu-id="5c771-217">H.264 (高、主要和基準設定檔)</span><span class="sxs-lookup"><span data-stu-id="5c771-217">H.264 (High, Main, and Baseline Profiles)</span></span> |<span data-ttu-id="5c771-218">AAC-LC、HE-AAC v1、HE-AAC v2</span><span class="sxs-lookup"><span data-stu-id="5c771-218">AAC-LC, HE-AAC v1, HE-AAC v2</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="5c771-219">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="5c771-219">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5c771-220">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5c771-220">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="5c771-221">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5c771-221">See also</span></span>
[<span data-ttu-id="5c771-222">透過 Azure Media Services 編碼的隨選內容</span><span class="sxs-lookup"><span data-stu-id="5c771-222">Encoding On-Demand Content with Azure Media Services</span></span>](media-services-encode-asset.md)

[<span data-ttu-id="5c771-223">如何與媒體編碼器標準 tooencode</span><span class="sxs-lookup"><span data-stu-id="5c771-223">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

