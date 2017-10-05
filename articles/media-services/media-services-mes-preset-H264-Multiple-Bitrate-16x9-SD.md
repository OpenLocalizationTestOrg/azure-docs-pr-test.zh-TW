---
title: "H264 多重位元速率 16x9 SD | Microsoft Docs"
description: "本主題提供「H264 多重位元速率 16x9 SD」工作預設的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 8b16385a-9a3d-4939-aef3-ca6ac82f455f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: d5836589932e27e7439fb89fca7be63f0856681e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="h264-multiple-bitrate-16x9-sd"></a><span data-ttu-id="92b40-103">H264 多重位元速率 16x9 SD</span><span class="sxs-lookup"><span data-stu-id="92b40-103">H264 Multiple Bitrate 16x9 SD</span></span>
<span data-ttu-id="92b40-104">`Media Encoder Standard` 定義一組編碼預設，供您在建立編碼作業時使用。</span><span class="sxs-lookup"><span data-stu-id="92b40-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="92b40-105">您可以使用 `preset name` 來指定您想要將媒體檔案編碼成哪一種格式。</span><span class="sxs-lookup"><span data-stu-id="92b40-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="92b40-106">或者，您可以建立自己的 JSON 或 XML 型預設 (使用 UTF-8 或 UTF-16 編碼)。</span><span class="sxs-lookup"><span data-stu-id="92b40-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="92b40-107">然後，您要將自訂預設傳遞給編碼器。</span><span class="sxs-lookup"><span data-stu-id="92b40-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="92b40-108">如需這個 `Media Encoder Standard` 編碼器支援的所有預設名稱清單，請參閱[媒體編碼器標準的工作預設](media-services-mes-presets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92b40-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="92b40-109">本主題說明 XML 和 JSON 格式的 `H264 Multiple Bitrate 16x9 SD` 預設。</span><span class="sxs-lookup"><span data-stu-id="92b40-109">This topic shows the `H264 Multiple Bitrate 16x9 SD` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="92b40-110">此預設會產生一組 5 個對齊 GOP 的 MP4 檔案 (範圍從 1900 kbps 到 400 kbps) 和立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="92b40-110">This preset produces a set of 5 GOP-aligned MP4 files, ranging from 1900 kbps to 400 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="92b40-111">如需此預設的設定檔、位元速率、取樣率等的詳細資訊，請檢查以下定義的 XML 或 JSON。</span><span class="sxs-lookup"><span data-stu-id="92b40-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="92b40-112">如需這些預設中每個元素的意義說明，請參閱[媒體編碼器標準結構描述](media-services-mes-schema.md)主題。</span><span class="sxs-lookup"><span data-stu-id="92b40-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="92b40-113">跨層修改 `Width` 和 `Height` 值時，請確定長寬比保持一致。</span><span class="sxs-lookup"><span data-stu-id="92b40-113">When modifying the `Width` and `Height` values across layers, make sure that the aspect ratio remains consistent.</span></span> <span data-ttu-id="92b40-114">例如︰1920x1080、1280x720、1080x576、640x360。</span><span class="sxs-lookup"><span data-stu-id="92b40-114">For example: 1920x1080, 1280x720, 1080x576, 640x360.</span></span> <span data-ttu-id="92b40-115">請勿使用混合的長寬比，例如︰1280x720、720x480、640x360。</span><span class="sxs-lookup"><span data-stu-id="92b40-115">You should not use a mixture of aspect ratios, such as: 1280x720, 720x480, 640x360.</span></span>  
  
 <span data-ttu-id="92b40-116">XML</span><span class="sxs-lookup"><span data-stu-id="92b40-116">XML</span></span>  
  
```  
  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>1900</Bitrate>  
          <Width>848</Width>  
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
          <MaxBitrate>1900</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>1300</Bitrate>  
          <Width>848</Width>  
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
          <Bitrate>900</Bitrate>  
          <Width>640</Width>  
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
          <MaxBitrate>900</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>650</Bitrate>  
          <Width>640</Width>  
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
          <MaxBitrate>650</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>400</Bitrate>  
          <Width>432</Width>  
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
      <Channels>2</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>128</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="92b40-117">JSON</span><span class="sxs-lookup"><span data-stu-id="92b40-117">JSON</span></span>  
  
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
          "Bitrate": 1900,  
          "MaxBitrate": 1900,  
          "BufferWindow": "00:00:05",  
          "Width": 848,  
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
          "Width": 848,  
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
          "Bitrate": 900,  
          "MaxBitrate": 900,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
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
          "Bitrate": 650,  
          "MaxBitrate": 650,  
          "BufferWindow": "00:00:05",  
          "Width": 640,  
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
          "Width": 432,  
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
```
