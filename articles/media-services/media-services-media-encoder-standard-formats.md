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
# <a name="media-encoder-standard-formats-and-codecs"></a>Media Encoder Standard 格式和轉碼器
本文件包含一份 hello 最常見匯入和匯出檔案格式，您可以使用標準的媒體編碼器。

## <a name="input-containerfile-formats"></a>輸入容器/檔案格式
| 檔案格式 (副檔名) | 支援 |
| --- | --- | --- | --- |
| FLV (使用 H.264 和 AAC 轉碼器) (.flv) |yes |
| MXF    (.mxf) |yes |
| GXF    (.gxf) |yes |
| MPEG2-PS、MPEG2-TS、3GP (.ts、.ps、.3gp、.3gpp、.mpg) |是 |
| Windows Media 視訊 (WMV)/ASF (.wmv、.asf) |是 |
| AVI (未壓縮 8 位元/10 位元) (.avi) |是 |
| MP4 (.mp4、.m4a、.m4v)/ISMV (.isma、.ismv) |是 |
| [Microsoft Digital Video Recording (DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |是 |
| Matroska/WebM (.mkv) |是 |
| WAVE/WAV (.wav) |是 |
| QuickTime (.mov) |是 |

> [!NOTE]
> 上方是一個 hello 更常見的副檔名清單。 Media Encoder Standard 支援許多其他副檔名 (例如，.m2ts、.mpeg2video 和 .qt)。 如果 tooencode 檔案再試一次，並且收到不支援的 hello 格式的相關錯誤訊息，請提供意見反應[這裡](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/)。
> 
> 

### <a name="audio-formats-in-input-containers"></a>輸入容器中的音訊格式
媒體編碼器標準支援下列輸入容器中的音訊格式攜帶 hello:

* MXF、GXF 和 QuickTime 檔案，其具有交錯立體聲或 5.1 範例的音訊音軌

或

* 而為個別的 PCM 曲目，但 hello 通道對應來運送 hello 音訊 MXF、 GXF 及 QuickTime 檔案 （toostereo 或 5.1） 可以推算 hello 檔案中繼資料

請注意 hello 附近未來將提供明確/使用者提供的通道對應支援。

## <a name="input-video-codecs"></a>輸入視訊轉碼器
| 輸入視訊轉碼器 | 支援 |
| --- | --- | --- | --- |
| AVC 8 位元/10 位元，向上 too4:2:2，包括 AVCIntra |8 位元 4:2:0 和 4:2:2 |
| Avid DNxHD (使用 MXF) |是 |
| DVCPro/DVCProHD (使用 MXF) |是 |
| 數位視訊 (DV) (使用 AVI 檔案) |是 |
| JPEG 2000 |是 |
| Mpeg-2 （too422 設定檔和高的層級，包括變數，例如 XDCAM、 XDCAM HD、 XDCAM /IMX、 CableLabs® 和 D10） |Too422 設定檔 |
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
| AAC (AAC-LC、 AAC 他和 AAC HEv2; up too5.1) |是 |
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
hello 下表列出支援匯出的 hello 轉碼器與檔案格式。

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

[如何與媒體編碼器標準 tooencode](media-services-dotnet-encode-with-media-encoder-standard.md)

