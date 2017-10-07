---
title: "aaaTask 預設 MES (媒體編碼器 Standard) |Microsoft 文件"
description: "hello 主題提供和 MES （媒體編碼器標準） 的工作預設設定的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>MES 的工作預設 (媒體編碼器標準)

**媒體編碼器標準**會定義一組編碼預設，供您在建立編碼作業時使用。 建議 toouse hello 「 彈性 Streaming 」 預設，如果您想 tooencode 視訊串流處理媒體服務。 當您指定這個預設時，媒體編碼器標準將[自動產生位元速率階梯](media-services-autogen-bitrate-ladder-with-mes.md)。 

不過，如果您需要 toocustomize 編碼預設時，您應該採取 hello 編碼方式在這一節中定義為您的自訂設定的範本的預設值的其中一個。 如需每個項目哪些這些預設值表示與 hello 有效的值中的每個項目說明，請參閱 hello[媒體編碼器標準結構描述](media-services-mes-schema.md)主題。  
  
> [!NOTE]
>  當針對 4k 編碼，請使用預設值，您應該會收到 hello`S3`保留單位類型。 如需詳細資訊，請參閱[如何 tooScale 編碼](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units)。  
  
使用媒體編碼器標準時，預設會啟用旋轉。 如果您的視訊已記錄在智慧型手機或其他行動裝置在直向模式中，這些預設設定，會根據預設，將這些 tooLandscape 模式先前 tooencoding （與不同的是，當您使用 Azure 媒體編碼程式，其中視訊旋轉是手動作業，然後如中所述[這](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/)下 「 視訊旋轉 」 部落格)。  
  
可用的預設：  
  
 [H264 多重位元速率 1080p 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md)會產生一組 8 gop 之 MP4 檔案，範圍可從 6000 kbps too400 kbps 和 AAC 5.1 音訊。  
  
 [H264 多重位元速率 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md)會產生一組 8 gop 之 MP4 檔案，範圍可從 6000 kbps too400 kbps 和 AAC 立體聲音訊。  
  
 [H264 多重位元速率 16x9 ios](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md)會產生一組 8 gop 之 MP4 檔案，範圍可從 8500 kbps too200 kbps 和 AAC 立體聲音訊。  
  
 [H264 多重位元速率 16x9 SD 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md)會產生一組 5 gop 之 MP4 檔案，範圍介於 1900 kbps too400 kbps，並 AAC 5.1 音訊。  
  
 [H264 多重位元速率 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md)會產生一組 5 gop 之 MP4 檔案，範圍介於 1900 kbps too400 kbps，並 AAC 立體聲音訊。  
  
 [H264 多重位元速率 4k 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md)會產生一組 12 gop 之 MP4 檔案，範圍可從 20000 kbps too1000 kbps 和 AAC 5.1 音訊。  
  
 [H264 多重位元速率 4k](media-services-mes-preset-H264-Multiple-Bitrate-4K.md)會產生一組 12 gop 之 MP4 檔案，範圍可從 20000 kbps too1000 kbps 和 AAC 立體聲音訊。  
  
 [H264 多重位元速率 4x3 ios](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md)會產生一組 8 gop 之 MP4 檔案，範圍可從 8500 kbps too200 kbps 和 AAC 立體聲音訊。  
  
 [H264 多重位元速率 4x3 SD 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md)會產生一組 5 gop 之 MP4 檔案，範圍介於 1600 kbps too400 kbps，並 AAC 5.1 音訊。  
  
 [H264 多重位元速率 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md)會產生一組 5 gop 之 MP4 檔案，範圍介於 1600 kbps too400 kbps，並 AAC 立體聲音訊。  
  
 [H264 多重位元速率 720p 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md)會產生一組 6 gop 之 MP4 檔案，範圍從 3400 kbps too400 kbps，並 AAC 5.1 音訊。  
  
 [H264 多重位元速率 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md)會產生一組 6 gop 之 MP4 檔案，範圍從 3400 kbps too400 kbps，並 AAC 立體聲音訊。  
  
 [H264 單一位元速率 1080p 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) 會產生位元速率為 6750 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。  
  
 [H264 單一位元速率 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) 會產生位元速率為 6750 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。  
  
 [H264 單一位元速率 4K 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) 會產生位元速率為 18000 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。  
  
 [H264 單一位元速率 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) 會產生位元速率為 18000 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。  
  
 [H264 單一位元速率 4x3 SD 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) 會產生位元速率為 1800 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。  
  
 [H264 單一位元速率 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) 會產生位元速率為 1800 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。  
  
 [H264 單一位元速率 16x9 SD 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) 會產生位元速率為 2200 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。  
  
 [H264 單一位元速率 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) 會產生位元速率為 2200 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。  
  
 [H264 單一位元速率 720p 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) 會產生位元速率為 4500 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。  
  
 [H264 單一位元速率 720p (適用於 Android)](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) 預設會產生位元速率為 2000 kbps 的單一 MP4 檔案，而且是立體聲 AAC。  
  
 [H264 單一位元速率 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) 會產生位元速率為 4500 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。  
  
 [H264 單一位元速率高品質 SD (適用於 Android)](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) 會產生位元速率為 500 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。  
  
 [H264 單一位元速率低品質 SD (適用於 Android)](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) 會產生位元速率為 56 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。  
  
 如需相關的 tooMedia 服務編碼器，請參閱[編碼隨 Azure Media services](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/)。
