---
title: "Media Encoder Standard 格式和轉碼器"
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
ms.openlocfilehash: 036c192c5f52a1943bc2799ad6c7e6db7bbffcc4
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="media-encoder-standard-formats-and-codecs"></a>Media Encoder Standard 格式和轉碼器
本文件包含您可以在 Media Encoder Standard 中使用的常見匯入和匯出檔案格式清單。

## <a name="input-containerfile-formats"></a>輸入容器/檔案格式
| 檔案格式 (副檔名) | 支援 |
| --- | --- | --- | --- |
| FLV (使用 H.264 和 AAC 轉碼器) (.flv) |是 |
| MXF    (.mxf) |是 |
| GXF    (.gxf) |是 |
| MPEG2-PS、MPEG2-TS、3GP (.ts、.ps、.3gp、.3gpp、.mpg) |是 |
| Windows Media 視訊 (WMV)/ASF (.wmv、.asf) |是 |
| AVI (未壓縮 8 位元/10 位元) (.avi) |是 |
| MP4 (.mp4、.m4a、.m4v)/ISMV (.isma、.ismv) |是 |
| [Microsoft Digital Video Recording (DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |是 |
| Matroska/WebM (.mkv) |是 |
| WAVE/WAV (.wav) |是 |
| QuickTime (.mov) |是 |

> [!NOTE]
> 以上是較常見的副檔名清單。 Media Encoder Standard 支援許多其他副檔名 (例如，.m2ts、.mpeg2video 和 .qt)。 如果您嘗試將檔案編碼，但收到格式不支援的相關錯誤訊息，請在[這裡](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/)提供意見反應。
> 
> 

### <a name="audio-formats-in-input-containers"></a>輸入容器中的音訊格式
Media Encoder Standard 支援在輸入容器中帶有下列音訊格式：

* MXF、GXF 和 QuickTime 檔案，其具有交錯立體聲或 5.1 範例的音訊音軌

或

* MXF、GXF 及 QuickTime 檔案，其中該音訊當做個別的 PCM 曲目攜帶，但可從檔案中繼資料推算通道對應 (立體聲或 5.1)

將在不久的將來提供明確/使用者提供的通道對應支援。

## <a name="input-video-codecs"></a>輸入視訊轉碼器
| 輸入視訊轉碼器 | 支援 |
| --- | --- | --- | --- |
| AVC 8 位元/10 位元，高達 4:2:2，包括 AVCIntra |8 位元 4:2:0 和 4:2:2 |
| Avid DNxHD (使用 MXF) |是 |
| DVCPro/DVCProHD (使用 MXF) |是 |
| 數位視訊 (DV) (使用 AVI 檔案) |是 |
| JPEG 2000 |是 |
| MPEG-2 (高達 422 Profile 和 High Level，包括 XDCAM、XDCAM HD、XDCAM IMX、CableLabs ® 和 D10 等變種) |最高 422 設定檔 |
| MPEG-1 |是 |
| VC-1/WMV9 |是 |
| Canopus HQ/HQX |否 |
| Mpeg-4 第 2 部分 |是 |
| [Theora](https://en.wikipedia.org/wiki/Theora) |是 |
| YUV420 未壓縮或夾層 |是 |
| Apple ProRes 422 |是 |
| Apple ProRes 422 LT |是 |
| Apple ProRes 422 HQ |是 |
| Apple ProRes Proxy |是 |
| Apple ProRes 4444 |是 |
| Apple ProRes 4444 XQ |是 |

## <a name="input-audio-codecs"></a>輸入音訊轉碼器
| 輸入音訊轉碼器 | 支援 |
| --- | --- | --- | --- |
| AAC (AAC-LC、AAC-HE 和 AAC-HEv2；高達 5.1) |是 |
| MPEG Layer 2 |是 |
| MP3 (MPEG-1 音訊層 3) |是 |
| Windows Media 音訊 |是 |
| WAV/PCM |是 |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |是 |
| [Opus](http://go.microsoft.com/fwlink/?LinkId=822667) |是 |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |是 |
| AMR (可變多速率) |是 |
| AES (SMPTE 331M 和 302M，AES3-2003) |否 |
| Dolby® E |否 |
| Dolby® Digital (AC3) |否 |
| Dolby® Digital Plus (E-AC3) |否 |

## <a name="output-formats-and-codecs"></a>輸出格式和轉碼器
下表會列出支援匯出的轉碼器和檔案格式清單。

| 檔案格式 | 視訊轉碼器 | 音訊轉碼器 |
| --- | --- | --- |
| MP4  <br/><br/>(包括多位元速率 MP4 容器) |H.264 (高、主要和基準設定檔) |AAC-LC、HE-AAC v1、HE-AAC v2 |
| MPEG2-TS |H.264 (高、主要和基準設定檔) |AAC-LC、HE-AAC v1、HE-AAC v2 |

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[透過 Azure Media Services 編碼的隨選內容](media-services-encode-asset.md)

[如何使用 Media Encoder Standard 進行編碼](media-services-dotnet-encode-with-media-encoder-standard.md)

