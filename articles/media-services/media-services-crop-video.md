---
title: "媒體編碼器標準-Azure aaaHow toocrop 視訊 |Microsoft 文件"
description: "本文將說明如何與媒體編碼器標準 toocrop 視訊。"
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="36319-103">以 Media Encoder Standard 裁剪影片</span><span class="sxs-lookup"><span data-stu-id="36319-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="36319-104">您可以使用您輸入視訊 toocrop 媒體編碼器標準 (MES)。</span><span class="sxs-lookup"><span data-stu-id="36319-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="36319-105">裁剪就是選取矩形視窗內 hello 視訊畫面格，並編碼只在該視窗中的 hello 像素 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="36319-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="36319-106">下列圖表中的 hello 可協助說明 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="36319-106">hello following diagram helps illustrate hello process.</span></span>

![裁剪影片](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="36319-108">假設您有做為輸入的解析度 1920 x 1080 像素 （16:9 外觀比例），但有黑色列 （pillar 方塊） 在 hello 左邊和右邊，使只有 4:3 視窗或 1440 x 1080 像素包含作用中的視訊的視訊。</span><span class="sxs-lookup"><span data-stu-id="36319-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="36319-109">您可以使用 MES toocrop 或刪 hello 黑色列，並編碼 hello 1440 x 1080 區域。</span><span class="sxs-lookup"><span data-stu-id="36319-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="36319-110">裁剪 MES 中就是前置處理階段中，以便在 hello 編碼預設 hello 裁剪參數套用 toohello 原始輸入的視訊。</span><span class="sxs-lookup"><span data-stu-id="36319-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="36319-111">編碼是後續階段中，與 hello 寬度/高度設定會套用 toohello*預先處理*視訊及不 toohello 原始視訊。</span><span class="sxs-lookup"><span data-stu-id="36319-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="36319-112">設計您的預設設定時您需要 toodo hello 下列: （a），請選取 hello 裁剪參數根據原始輸入視訊 hello，和 （b） 選取您編碼基礎 hello 裁剪視訊設定。</span><span class="sxs-lookup"><span data-stu-id="36319-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="36319-113">如果不符合您將編碼設定 toohello 裁剪視訊、 hello 輸出不會如預期般。</span><span class="sxs-lookup"><span data-stu-id="36319-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="36319-114">hello[下列](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet)主題說明如何 toocreate 編碼工作與 MES 和 toospecify 自訂方式為預設 hello 編碼工作。</span><span class="sxs-lookup"><span data-stu-id="36319-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="36319-115">建立自訂預設值</span><span class="sxs-lookup"><span data-stu-id="36319-115">Creating a custom preset</span></span>
<span data-ttu-id="36319-116">在 hello 範例 hello 圖所示：</span><span class="sxs-lookup"><span data-stu-id="36319-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="36319-117">原始輸入為 1920x1080</span><span class="sxs-lookup"><span data-stu-id="36319-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="36319-118">它需要 toobe 裁剪 tooan 1440 x 1080、 置中於 hello 輸入畫面格的輸出</span><span class="sxs-lookup"><span data-stu-id="36319-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="36319-119">這表示 X 位移為 (1920 – 1440)/2 = 240，Y 位移為零</span><span class="sxs-lookup"><span data-stu-id="36319-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="36319-120">hello 寬度與 hello 裁剪矩形的高度，分別為 1440年和 1080，</span><span class="sxs-lookup"><span data-stu-id="36319-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="36319-121">在 hello 編碼階段中，hello 要求是 tooproduce 三個層級，分別為解決方案 1440 x 1080、 960 x 720 和 480 x 360，</span><span class="sxs-lookup"><span data-stu-id="36319-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="36319-122">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="36319-122">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


## <a name="restrictions-on-cropping"></a><span data-ttu-id="36319-123">裁剪的限制</span><span class="sxs-lookup"><span data-stu-id="36319-123">Restrictions on cropping</span></span>
<span data-ttu-id="36319-124">hello 裁剪功能的目的在於 toobe 手冊。</span><span class="sxs-lookup"><span data-stu-id="36319-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="36319-125">您需要 tooload 輸入視訊到適當的編輯工具，可讓您選取感興趣的框架，定位 hello hello 裁剪矩形的資料指標 toodetermine 位移，toodetermine hello 會調整為適用於該特定視訊等的編碼預設。這項功能不是 tooenable 等： 自動偵測和移除您的輸入視訊中的黑色的 letterbox pillarbox 框線。</span><span class="sxs-lookup"><span data-stu-id="36319-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="36319-126">下列條件約束套用 toohello 裁剪功能。</span><span class="sxs-lookup"><span data-stu-id="36319-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="36319-127">如果不符合這些，hello 編碼工作可能失敗，或是產生非預期的輸出。</span><span class="sxs-lookup"><span data-stu-id="36319-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="36319-128">hello 座標和 hello 裁剪矩形的大小有 toofit 內 hello 輸入視訊</span><span class="sxs-lookup"><span data-stu-id="36319-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="36319-129">如上面所述，hello 寬度和高度以 hello 編碼設定有 toocorrespond toohello 裁剪視訊</span><span class="sxs-lookup"><span data-stu-id="36319-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="36319-130">裁剪套用 toovideos 擷取以橫向模式 (也就是不適用 toovideos 記錄搭配以垂直方式保留在智慧型手機或縱向模式)</span><span class="sxs-lookup"><span data-stu-id="36319-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="36319-131">最適合用於以方形像素擷取的漸進式影片</span><span class="sxs-lookup"><span data-stu-id="36319-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="36319-132">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="36319-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="36319-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="36319-133">Next step</span></span>
<span data-ttu-id="36319-134">請參閱 Azure Media Services 學習路徑 toohelp 您了解 AMS 所提供的強大功能。</span><span class="sxs-lookup"><span data-stu-id="36319-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
