---
title: "H264 單一位元速率 720p 音訊 5.1 | Microsoft Docs"
description: "本主題提供「H264 單一位元速率 720p 音訊 5.1」工作預設的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ba2bfa57-3c87-4b1b-b91b-58f9108f4e85
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 629ef7690f25dc6de1773a83cf967544cdf16682
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-720p-audio-51"></a><span data-ttu-id="8c215-103">H264 單一位元速率 720p 音訊 5.1</span><span class="sxs-lookup"><span data-stu-id="8c215-103">H264 Single Bitrate 720p Audio 5.1</span></span>
<span data-ttu-id="8c215-104">`Media Encoder Standard` 定義一組編碼預設，供您在建立編碼作業時使用。</span><span class="sxs-lookup"><span data-stu-id="8c215-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="8c215-105">您可以使用 `preset name` 來指定您想要將媒體檔案編碼成哪一種格式。</span><span class="sxs-lookup"><span data-stu-id="8c215-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="8c215-106">或者，您可以建立自己的 JSON 或 XML 型預設 (使用 UTF-8 或 UTF-16 編碼)。</span><span class="sxs-lookup"><span data-stu-id="8c215-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="8c215-107">然後，您要將自訂預設傳遞給編碼器。</span><span class="sxs-lookup"><span data-stu-id="8c215-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="8c215-108">如需這個 `Media Encoder Standard` 編碼器支援的所有預設名稱清單，請參閱[媒體編碼器標準的工作預設](media-services-mes-presets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8c215-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="8c215-109">本主題說明 XML 和 JSON 格式的 `H264 Single Bitrate 720p Audio 5.1` 預設。</span><span class="sxs-lookup"><span data-stu-id="8c215-109">This topic shows the `H264 Single Bitrate 720p Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="8c215-110">此預設會產生位元速率為 4500 kbps 的單一 MP4 檔案，而且是 AAC 5.1 音訊。</span><span class="sxs-lookup"><span data-stu-id="8c215-110">This preset produces a single MP4 file with a bitrate of 4500 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="8c215-111">如需此預設的設定檔、位元速率、取樣率等的詳細資訊，請檢查以下定義的 XML 或 JSON。</span><span class="sxs-lookup"><span data-stu-id="8c215-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="8c215-112">如需每個元素的意義說明，以及每個元素的有效值，請參閱[媒體編碼器標準結構描述](media-services-mes-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="8c215-112">For explanations of what each element means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
 <span data-ttu-id="8c215-113">XML</span><span class="sxs-lookup"><span data-stu-id="8c215-113">XML</span></span>  
  
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
  
 <span data-ttu-id="8c215-114">JSON</span><span class="sxs-lookup"><span data-stu-id="8c215-114">JSON</span></span>  
  
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
