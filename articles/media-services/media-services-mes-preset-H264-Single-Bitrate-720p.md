---
title: "H264 單一位元率 720p 媒體編碼器標準預設值 - Azure | Microsoft Docs"
description: "本主題提供「H264 單一位元速率 720p」工作預設的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f66da66c-9f21-441d-8038-51e3094e9307
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5ca683db654a5adda6e15e1761579c7e81438417
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-720p"></a><span data-ttu-id="95ddd-103">H264 單一位元速率 720p</span><span class="sxs-lookup"><span data-stu-id="95ddd-103">H264 Single Bitrate 720p</span></span>
<span data-ttu-id="95ddd-104">`Media Encoder Standard` 定義一組編碼預設，供您在建立編碼作業時使用。</span><span class="sxs-lookup"><span data-stu-id="95ddd-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="95ddd-105">您可以使用 `preset name` 來指定您想要將媒體檔案編碼成哪一種格式。</span><span class="sxs-lookup"><span data-stu-id="95ddd-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="95ddd-106">或者，您可以建立自己的 JSON 或 XML 型預設 (使用 UTF-8 或 UTF-16 編碼)。</span><span class="sxs-lookup"><span data-stu-id="95ddd-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="95ddd-107">然後，您要將自訂預設傳遞給編碼器。</span><span class="sxs-lookup"><span data-stu-id="95ddd-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="95ddd-108">如需這個 `Media Encoder Standard` 編碼器支援的所有預設名稱清單，請參閱[媒體編碼器標準的工作預設](media-services-mes-presets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="95ddd-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="95ddd-109">本主題說明 XML 和 JSON 格式的 `H264 Single Bitrate 720p` 預設。</span><span class="sxs-lookup"><span data-stu-id="95ddd-109">This topic shows the `H264 Single Bitrate 720p` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="95ddd-110">此預設會產生位元速率為 4500 kbps 的單一 MP4 檔案，而且是立體聲 AAC 音訊。</span><span class="sxs-lookup"><span data-stu-id="95ddd-110">This preset produces a single MP4 file with a bitrate of 4500 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="95ddd-111">如需此預設的設定檔、位元速率、取樣率等的詳細資訊，請檢查以下定義的 XML 或 JSON。</span><span class="sxs-lookup"><span data-stu-id="95ddd-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="95ddd-112">如需這些預設中每個元素的意義說明及每個元素的有效值，請參閱[媒體編碼器標準結構描述](media-services-mes-schema.md)主題。</span><span class="sxs-lookup"><span data-stu-id="95ddd-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="95ddd-113">XML</span><span class="sxs-lookup"><span data-stu-id="95ddd-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>4500</Bitrate>  
          <Width>1280</Width>  
          <Height>720</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>4500</MaxBitrate>  
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
  
 <span data-ttu-id="95ddd-114">JSON</span><span class="sxs-lookup"><span data-stu-id="95ddd-114">JSON</span></span>  
  
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
          "Bitrate": 4500,  
          "MaxBitrate": 4500,  
          "BufferWindow": "00:00:05",  
          "Width": 1280,  
          "Height": 720,  
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
