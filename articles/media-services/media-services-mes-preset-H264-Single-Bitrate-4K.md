---
title: "aaaH264 單一位元速率 4k 媒體編碼器標準預設 Azure |Microsoft 文件"
description: "hello 主題概略 hello * * H264 單一位元速率 4 K * * 工作預設值。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 8e437aea-8193-49a0-9ff2-4fd391c80972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3a88207ba89baaefddfea631aa5d4c1c74194c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4k"></a><span data-ttu-id="92bbe-103">H264 單一位元速率 4K</span><span class="sxs-lookup"><span data-stu-id="92bbe-103">H264 Single Bitrate 4K</span></span>
<span data-ttu-id="92bbe-104">`Media Encoder Standard` 定義一組編碼預設，供您在建立編碼作業時使用。</span><span class="sxs-lookup"><span data-stu-id="92bbe-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="92bbe-105">您可以使用`preset name`toospecify 成哪一種格式中，您想要 tooencode 媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="92bbe-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="92bbe-106">或者，您可以建立自己的 JSON 或 XML 型預設 (使用 UTF-8 或 UTF-16 編碼)。</span><span class="sxs-lookup"><span data-stu-id="92bbe-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="92bbe-107">然後，您會傳遞 hello 自訂預設的 toohello 編碼器。</span><span class="sxs-lookup"><span data-stu-id="92bbe-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="92bbe-108">所有的 hello hello 清單的預設名稱支援這`Media Encoder Standard`編碼器，請參閱[的媒體編碼器標準工作預設](media-services-mes-presets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92bbe-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="92bbe-109">本主題顯示 hello`H264 Single Bitrate 4K`預設 XML 和 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="92bbe-109">This topic shows hello `H264 Single Bitrate 4K` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="92bbe-110">此預設會產生位元速率為 18000 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="92bbe-110">This preset produces a single MP4 file with a bitrate of 18000 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="92bbe-111">如需設定檔的詳細資訊，位元速率，取樣率、 等等。 這個預設值，請檢查 hello XML 或 JSON 定義如下。</span><span class="sxs-lookup"><span data-stu-id="92bbe-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="92bbe-112">如需每個項目哪些這些預設值表示與 hello 有效的值中的每個項目說明，請參閱 hello[媒體編碼器標準結構描述](media-services-mes-schema.md)主題。</span><span class="sxs-lookup"><span data-stu-id="92bbe-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="92bbe-113">您應該會收到 hello Premium 保留單位類型與 4k 編碼。</span><span class="sxs-lookup"><span data-stu-id="92bbe-113">You should get hello Premium reserved unit type with 4K encodes.</span></span> <span data-ttu-id="92bbe-114">如需詳細資訊，請參閱[如何 tooScale 編碼](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units)。</span><span class="sxs-lookup"><span data-stu-id="92bbe-114">For more information, see [How tooScale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
 <span data-ttu-id="92bbe-115">XML</span><span class="sxs-lookup"><span data-stu-id="92bbe-115">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>18000</Bitrate>  
          <Width>3840</Width>  
          <Height>2160</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>18000</MaxBitrate>  
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
  
 <span data-ttu-id="92bbe-116">JSON</span><span class="sxs-lookup"><span data-stu-id="92bbe-116">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 18000,  
          "MaxBitrate": 18000,  
          "BufferWindow": "00:00:05",  
          "Width": 3840,  
          "Height": 2160,  
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
