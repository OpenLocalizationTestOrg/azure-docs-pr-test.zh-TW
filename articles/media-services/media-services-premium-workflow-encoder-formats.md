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
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a>媒體編碼器高階工作流程格式和轉碼器
> [!NOTE]
> 如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。
> 
> 本主題中討論的媒體編碼器高階工作流程媒體處理器無法在中國使用。 
> 
> 

本文件包含一份輸入和輸出檔案格式的 hello hello 公用預覽版本所支援的轉碼器**媒體編碼器高階工作流程**編碼器。

[Media Encoder Premium Worflow 輸入格式和轉碼器](#input_formats)

[Media Encoder Premium Worflow 輸出格式和轉碼器](#output_formats)

**Media Encoder Premium Workflow** 支援 [本](#closed_captioning) 章節所述的隱藏式字幕。 

## <a id="input_formats"></a>Media Encoder Premium Worflow 輸入格式和轉碼器
hello 下列區段會列出此媒體處理器支援做為輸入的 hello 轉碼器與檔案格式。

### <a name="input-containerfile-formats"></a>輸入容器/檔案格式
* Adobe® Flash® F4V
* MXF/SMPTE 377M
* GXF
* MPEG-2 傳輸資料流
* MPEG-2 程式資料流
* MPEG-4/MP4
* Windows Media/ASF
* AVI (未壓縮 8 位元/10 位元)

### <a name="input-video-codecs"></a>輸入視訊轉碼器
* AVC 8 位元/10 位元，向上 too4:2:2，包括 AVCIntra
* Avid DNxHD (使用 MXF)
* DVCPro/DVCProHD (使用 MXF)
* JPEG2000
* Mpeg-2 （too422 設定檔和高的層級，包括變數，例如 XDCAM、 XDCAM HD、 XDCAM /IMX、 CableLabs® 和 D10）
* MPEG-1
* Windows Media 視訊/VC-1

### <a name="input-audio-codecs"></a>輸入音訊轉碼器
* AES (SMPTE 331M 和 302M，AES3-2003)
* Dolby® E
* Dolby® Digital (AC3)
* AAC (AAC-LC、 AAC 他和 AAC HEv2; up too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 音訊層 3)
* Windows Media 音訊
* WAV/PCM

## <a id="output_format"></a>Media Encoder Premium Worflow 輸出格式和轉碼器
hello 下節列出支援此媒體處理器從輸出中的 hello 轉碼器與檔案格式。

### <a name="output-containerfile-formats"></a>輸出容器/檔案格式
* Adobe® Flash® F4V
* MXF (OP1a、XDCAM 和 AS02)
* DPP (包括 AS11)
* GXF
* MPEG-4/MP4
* Windows Media/ASF
* AVI (未壓縮 8 位元/10 位元)
* Smooth Streaming 檔案格式 (PIFF 1.3)
* MPEG-TS 

### <a name="output-video-codecs"></a>輸出視訊轉碼器
* AVC (H.264; 8 位元; 向上 tooHigh 設定檔，層級 5.2; 4k 強力 HD;AVC 內部）
* Avid DNxHD (使用 MXF)
* DVCPro/DVCProHD (使用 MXF)
* Mpeg-2 （too422 設定檔和高的層級，包括變數，例如 XDCAM、 XDCAM HD、 XDCAM /IMX、 CableLabs® 和 D10）
* MPEG-1
* Windows Media 視訊/VC-1
* JPEG 縮圖建立

### <a name="output-audio-codecs"></a>輸出音訊轉碼器
* AES (SMPTE 331M 和 302M，AES3-2003)
* Dolby® Digital (AC3)
* Dolby® Digital Plus (E AC3) 向上 too7.1
* AAC (AAC-LC、 AAC 他和 AAC HEv2; up too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 音訊層 3)
* Windows Media 音訊

>[!NOTE]
>如果編碼 tooDolby® 數位 (AC3)，hello 輸出只可以寫入的 ISO MP4 檔案。

## <a id="closed_captioning"></a>支援隱藏式字幕
內嵌時， **Media Encoder Premium Workflow** 支援：

1. SCC 檔案
2. SMPTE-TT 檔案
3. CEA-608/CEA-708 – 以使用者資料 (H.264 基礎資料流、ATSC/53、SCTE20 的 SEI 訊息) 的形式傳送，或以 MXF/GXF 檔案中的輔助資料形式傳送
4. STL 字幕檔案

在輸出時，hello 下列選項可用：

1. CEA 608 tooCEA 708 轉譯
2. CEA-608/CEA-708 傳遞 (內嵌在 H.264 基礎資料流的 SEI 訊息，或執行為 MXF 檔案中的輔助資料)
3. SCC
4. SMPTE 計時文字 (來自來源 CEA-608 經由 SMPTE RP2052，包括建立 DFXP 檔案)
5. SRT 副標題檔案
6. DVB 副標題資料流

注意： 不支援所有的 hello 上面的輸出格式是透過 Azure Media Services 串流傳遞。

## <a name="known-issues"></a>已知問題
如果您輸入的視訊不包含字幕，hello 輸出資產仍然會包含空白的 TTML 檔案。 

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

