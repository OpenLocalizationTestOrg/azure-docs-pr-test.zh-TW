---
title: "MES 的工作預設 (媒體編碼器標準) | Microsoft Docs"
description: "本主題提供 MES 的工作預設 (媒體編碼器標準) 概觀。"
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
ms.openlocfilehash: 6fcdd361b7725b1a5136828cede24cdaac5dacc1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a><span data-ttu-id="b3160-103">MES 的工作預設 (媒體編碼器標準)</span><span class="sxs-lookup"><span data-stu-id="b3160-103">Task Presets for MES (Media Encoder Standard)</span></span>

<span data-ttu-id="b3160-104">**媒體編碼器標準**會定義一組編碼預設，供您在建立編碼作業時使用。</span><span class="sxs-lookup"><span data-stu-id="b3160-104">**Media Encoder Standard** defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="b3160-105">如果您想要將視訊編碼以使用媒體服務進行串流處理，建議使用「彈性資料流」預設。</span><span class="sxs-lookup"><span data-stu-id="b3160-105">It is recommended to use the "Adaptive Streaming" preset if you want to encode a video for streaming with Media Services.</span></span> <span data-ttu-id="b3160-106">當您指定這個預設時，媒體編碼器標準將[自動產生位元速率階梯](media-services-autogen-bitrate-ladder-with-mes.md)。</span><span class="sxs-lookup"><span data-stu-id="b3160-106">When you specify this preset, Media Encoder Standard will [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md).</span></span> 

<span data-ttu-id="b3160-107">不過，如果您需要自訂編碼預設，則應採用本節中定義的其中一個編碼預設做為您自訂組態的範本。</span><span class="sxs-lookup"><span data-stu-id="b3160-107">However, if you need to customize an encoding preset, you should take one of the encoding presets defined in this section as a template for your custom configuration.</span></span> <span data-ttu-id="b3160-108">如需這些預設中每個元素的意義說明及每個元素的有效值，請參閱[媒體編碼器標準結構描述](media-services-mes-schema.md)主題。</span><span class="sxs-lookup"><span data-stu-id="b3160-108">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b3160-109">使用 4k 編碼的預設值時，您應該取得 `S3` 保留單元類型。</span><span class="sxs-lookup"><span data-stu-id="b3160-109">When using a preset for 4k encodes, you should get the `S3` reserved unit type.</span></span> <span data-ttu-id="b3160-110">如需詳細資訊，請參閱 [如何調整編碼](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units)。</span><span class="sxs-lookup"><span data-stu-id="b3160-110">For more information, see [How to Scale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
<span data-ttu-id="b3160-111">使用媒體編碼器標準時，預設會啟用旋轉。</span><span class="sxs-lookup"><span data-stu-id="b3160-111">When working with Media Encoder Standard, rotation is enabled by default.</span></span> <span data-ttu-id="b3160-112">如果您的視訊是在智慧型手機或其他行動裝置上以直向模式錄製，根據預設，這些預設會將它們旋轉成橫向模式後再編譯 (有別於使用 Azure 媒體編碼器時，視訊旋轉為手動操作，如[此部落格](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/)中的＜視訊旋轉＞所述)。</span><span class="sxs-lookup"><span data-stu-id="b3160-112">If your video has been recorded on a smartphone or other mobile device in Portrait mode, then these presets will, by default, rotate them to Landscape mode prior to encoding (unlike, when you work with Azure Media Encoder, where video rotation is a manual operation, as documented in [this](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog, under “Video Rotation”).</span></span>  
  
<span data-ttu-id="b3160-113">可用的預設：</span><span class="sxs-lookup"><span data-stu-id="b3160-113">Available presets:</span></span>  
  
 <span data-ttu-id="b3160-114">[H264 多重位元速率 1080p 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) 會產生一組 8 個對齊 GOP 的 MP4 檔案 (範圍從 6000 kbps 到 400 kbps) 和 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-114">[H264 Multiple Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) produces a set of 8 GOP-aligned MP4 files, ranging from 6000 kbps to 400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-115">[H264 多重位元速率 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) 會產生一組 8 個對齊 GOP 的 MP4 檔案 (範圍從 6000 kbps 到 400 kbps) 和立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-115">[H264 Multiple Bitrate 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) produces a set of 8 GOP-aligned MP4 files, ranging from 6000 kbps to 400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-116">[H264 多重位元速率 16x9 (適用於 iOS)](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) 會產生一組 8 個對齊 GOP 的 MP4 檔案 (範圍從 8500 kbps 到 200 kbps) 和立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-116">[H264 Multiple Bitrate 16x9 for iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) produces a set of 8 GOP-aligned MP4 files, ranging from 8500 kbps to 200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-117">[H264 多重位元速率 16x9 SD 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) 會產生一組 5 個對齊 GOP 的 MP4 檔案 (範圍從 1900 kbps 到 400 kbps) 和 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-117">[H264 Multiple Bitrate 16x9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1900 kbps to 400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-118">[H264 多重位元速率 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) 會產生一組 5 個對齊 GOP 的 MP4 檔案 (範圍從 1900 kbps 到 400 kbps) 和立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-118">[H264 Multiple Bitrate 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1900 kbps to 400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-119">[H264 多重位元速率 4K 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) 會產生一組 12 個對齊 GOP 的 MP4 檔案 (範圍從 20000 kbps 到 1000 kbps) 和 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-119">[H264 Multiple Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) produces a set of 12 GOP-aligned MP4 files, ranging from 20000 kbps to 1000 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-120">[H264 多重位元速率 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) 會產生一組 12 個對齊 GOP 的 MP4 檔案 (範圍從 20000 kbps 到 1000 kbps) 和立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-120">[H264 Multiple Bitrate 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) produces a set of 12 GOP-aligned MP4 files, ranging from 20000 kbps to 1000 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-121">[H264 多重位元速率 4x3 (適用於 iOS)](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) 會產生一組 8 個對齊 GOP 的 MP4 檔案 (範圍從 8500 kbps 到 200 kbps) 和立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-121">[H264 Multiple Bitrate 4x3 for iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) produces a set of 8 GOP-aligned MP4 files, ranging from 8500 kbps to 200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-122">[H264 多重位元速率 4x3 SD 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) 會產生一組 5 個對齊 GOP 的 MP4 檔案 (範圍從 1600 kbps 到 400 kbps) 和 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-122">[H264 Multiple Bitrate 4x3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1600 kbps to 400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-123">[H264 多重位元速率 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) 會產生一組 5 個對齊 GOP 的 MP4 檔案 (範圍從 1600 kbps 到 400 kbps) 和立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-123">[H264 Multiple Bitrate 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1600 kbps to 400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-124">[H264 多重位元速率 720p 音訊 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) 會產生一組 6 個對齊 GOP 的 MP4 檔案 (範圍從 3400 kbps 到 400 kbps) 和 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-124">[H264 Multiple Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) produces a set of 6 GOP-aligned MP4 files, ranging from 3400 kbps to 400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-125">[H264 多重位元速率 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 會產生一組 6 個對齊 GOP 的 MP4 檔案 (範圍從 3400 kbps 到 400 kbps) 和立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-125">[H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) produces a set of 6 GOP-aligned MP4 files, ranging from 3400 kbps to 400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-126">[H264 單一位元速率 1080p 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) 會產生位元速率為 6750 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-126">[H264 Single Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) produces a single MP4 file with a bitrate of 6750 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-127">[H264 單一位元速率 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) 會產生位元速率為 6750 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-127">[H264 Single Bitrate 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) produces a single MP4 file with a bitrate of 6750 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-128">[H264 單一位元速率 4K 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) 會產生位元速率為 18000 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-128">[H264 Single Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) produces a single MP4 file with a bitrate of 18000 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-129">[H264 單一位元速率 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) 會產生位元速率為 18000 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-129">[H264 Single Bitrate 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) produces a single MP4 file with a bitrate of 18000 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-130">[H264 單一位元速率 4x3 SD 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) 會產生位元速率為 1800 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-130">[H264 Single Bitrate 4x3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) produces a single MP4 file with a bitrate of 1800 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-131">[H264 單一位元速率 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) 會產生位元速率為 1800 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-131">[H264 Single Bitrate 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) produces a single MP4 file with a bitrate of 1800 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-132">[H264 單一位元速率 16x9 SD 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) 會產生位元速率為 2200 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-132">[H264 Single Bitrate 16x9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) produces a single MP4 file with a bitrate of 2200 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-133">[H264 單一位元速率 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) 會產生位元速率為 2200 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-133">[H264 Single Bitrate 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) produces a single MP4 file with a bitrate of 2200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-134">[H264 單一位元速率 720p 音訊 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) 會產生位元速率為 4500 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-134">[H264 Single Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) produces a single MP4 file with a bitrate of 4500 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="b3160-135">[H264 單一位元速率 720p (適用於 Android)](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) 預設會產生位元速率為 2000 kbps 的單一 MP4 檔案，而且是立體聲 AAC。</span><span class="sxs-lookup"><span data-stu-id="b3160-135">[H264 Single Bitrate 720p for Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) preset produces a single MP4 file with a bitrate of 2000 kbps, and stereo AAC.</span></span>  
  
 <span data-ttu-id="b3160-136">[H264 單一位元速率 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) 會產生位元速率為 4500 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-136">[H264 Single Bitrate 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) produces a single MP4 file with a bitrate of 4500 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-137">[H264 單一位元速率高品質 SD (適用於 Android)](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) 會產生位元速率為 500 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-137">[H264 Single Bitrate High Quality SD for Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) produces a single MP4 file with a bitrate of 500 kbps, and stereo AAC audio..</span></span>  
  
 <span data-ttu-id="b3160-138">[H264 單一位元速率低品質 SD (適用於 Android)](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) 會產生位元速率為 56 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="b3160-138">[H264 Single Bitrate Low Quality SD for Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) produces a single MP4 file with a bitrate of 56 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="b3160-139">如需與媒體服務編碼器相關的詳細資訊，請參閱[使用 Azure 媒體服務隨選編碼](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/)。</span><span class="sxs-lookup"><span data-stu-id="b3160-139">For more information related to Media Services encoders, see [Encoding On-Demand with Azure Media Services](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).</span></span>
