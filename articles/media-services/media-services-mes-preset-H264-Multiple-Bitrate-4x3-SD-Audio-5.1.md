---
title: "aaaH264 多重位元速率 4x3 SD 音訊 5.1 |Microsoft 文件"
description: "hello 主題概略 hello * * H264 多重位元速率 4x3 SD 音訊 5.1* * 工作預設值。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 24faec4f-a69c-4ae5-afd4-308e03046a3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 894c89067f387ae3823df77a7ae9c4e64047dd31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="h264-multiple-bitrate-4x3-sd-audio-51"></a><span data-ttu-id="7b294-103">H264 多重位元速率 4x3 SD 音訊 5.1</span><span class="sxs-lookup"><span data-stu-id="7b294-103">H264 Multiple Bitrate 4x3 SD Audio 5.1</span></span>
<span data-ttu-id="7b294-104">`Media Encoder Standard` 定義一組編碼預設，供您在建立編碼作業時使用。</span><span class="sxs-lookup"><span data-stu-id="7b294-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="7b294-105">您可以使用`preset name`toospecify 成哪一種格式中，您想要 tooencode 媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="7b294-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="7b294-106">或者，您可以建立自己的 JSON 或 XML 型預設 (使用 UTF-8 或 UTF-16 編碼)。</span><span class="sxs-lookup"><span data-stu-id="7b294-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="7b294-107">然後，您會傳遞 hello 自訂預設的 toohello 編碼器。</span><span class="sxs-lookup"><span data-stu-id="7b294-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="7b294-108">所有的 hello hello 清單的預設名稱支援這`Media Encoder Standard`編碼器，請參閱[的媒體編碼器標準工作預設](media-services-mes-presets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7b294-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="7b294-109">本主題顯示 hello`H264 Multiple Bitrate 4x3 SD Audio 5.1`預設 XML 和 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="7b294-109">This topic shows hello `H264 Multiple Bitrate 4x3 SD Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="7b294-110">此預設會產生一組 5 gop 之 MP4 檔案，範圍介於 1600 kbps too400 kbps，並 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="7b294-110">This preset produces a set of 5 GOP-aligned MP4 files, ranging from 1600 kbps too400 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="7b294-111">如需設定檔的詳細資訊，位元速率，取樣率、 等等。 這個預設值，請檢查 hello XML 或 JSON 定義如下。</span><span class="sxs-lookup"><span data-stu-id="7b294-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="7b294-112">如對於每個項目，表示每個項目，和 hello 有效值的說明，請參閱 hello[媒體編碼器標準結構描述](media-services-mes-schema.md)...</span><span class="sxs-lookup"><span data-stu-id="7b294-112">For explanations of what each element means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md)..</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7b294-113">當修改 hello`Width`和`Height`值個層面，請確定該 hello 外觀比例會保持一致。</span><span class="sxs-lookup"><span data-stu-id="7b294-113">When modifying hello `Width` and `Height` values across layers, make sure that hello aspect ratio remains consistent.</span></span> <span data-ttu-id="7b294-114">例如︰1920x1080、1280x720、1080x576、640x360。</span><span class="sxs-lookup"><span data-stu-id="7b294-114">For example: 1920x1080, 1280x720, 1080x576, 640x360.</span></span> <span data-ttu-id="7b294-115">請勿使用混合的長寬比，例如︰1280x720、720x480、640x360。</span><span class="sxs-lookup"><span data-stu-id="7b294-115">You should not use a mixture of aspect ratios, such as: 1280x720, 720x480, 640x360.</span></span>  
  
 <span data-ttu-id="7b294-116">XML</span><span class="sxs-lookup"><span data-stu-id="7b294-116">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>1600</Bitrate>  
          <Width>640</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>1600</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>1300</Bitrate>  
          <Width>640</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>1300</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>800</Bitrate>  
          <Width>480</Width>  
          <Height>360</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>800</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>600</Bitrate>  
          <Width>480</Width>  
          <Height>360</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>600</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>400</Bitrate>  
          <Width>360</Width>  
          <Height>240</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>400</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="7b294-117">JSON</span><span class="sxs-lookup"><span data-stu-id="7b294-117">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 1600,  
          "MaxBitrate": 1600,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
          "Height": 480,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        },  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 1300,  
          "MaxBitrate": 1300,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
          "Height": 480,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        },  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 800,  
          "MaxBitrate": 800,  
          "BufferWindow": "00:00:05",  
          "Width": 480,  
          "Height": 360,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        },  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 600,  
          "MaxBitrate": 600,  
          "BufferWindow": "00:00:05",  
          "Width": 480,  
          "Height": 360,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        },  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 400,  
          "MaxBitrate": 400,  
          "BufferWindow": "00:00:05",  
          "Width": 360,  
          "Height": 240,  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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
```
