---
title: "aaaPerform 進階自訂 MES 預設編碼方式 |Microsoft 文件"
description: "本主題說明如何 tooperform 進階自訂媒體編碼器標準工作預設編碼方式。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="d05b0-103">自訂 MES 預設值來執行進階編碼</span><span class="sxs-lookup"><span data-stu-id="d05b0-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="d05b0-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d05b0-104">Overview</span></span>

<span data-ttu-id="d05b0-105">本主題說明 toocustomize 媒體編碼器標準的預設設定。</span><span class="sxs-lookup"><span data-stu-id="d05b0-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="d05b0-106">hello[媒體編碼器標準使用自訂的預設編碼方式](media-services-custom-mes-presets-with-dotnet.md)主題會說明如何 toouse.NET toocreate 編碼工作以及的作業來執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="d05b0-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="d05b0-107">一旦您自訂的預設供應 hello 自訂預設 toohello 編碼工作。</span><span class="sxs-lookup"><span data-stu-id="d05b0-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="d05b0-108">如果使用 XML 預設，請確定 toopreserve hello 項目的順序，如下列 XML 範例所示 （例如，KeyFrameInterval 之前 SceneChangeDetection）。</span><span class="sxs-lookup"><span data-stu-id="d05b0-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="d05b0-109">本主題會示範 hello 執行 hello 下列編碼工作的自訂預設。</span><span class="sxs-lookup"><span data-stu-id="d05b0-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="d05b0-110">支援相對大小</span><span class="sxs-lookup"><span data-stu-id="d05b0-110">Support for relative sizes</span></span>

<span data-ttu-id="d05b0-111">當產生縮圖，您不需要 tooalways 指定輸出寬度和高度 （像素）。</span><span class="sxs-lookup"><span data-stu-id="d05b0-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="d05b0-112">您可以在 hello 範圍 [1%，100%] 中的百分比，來指定它們。</span><span class="sxs-lookup"><span data-stu-id="d05b0-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="d05b0-113">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="d05b0-114">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="d05b0-115"><a id="thumbnails"></a>產生縮圖</span><span class="sxs-lookup"><span data-stu-id="d05b0-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="d05b0-116">此區段會顯示如何 toocustomize 產生縮圖的預設值。</span><span class="sxs-lookup"><span data-stu-id="d05b0-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="d05b0-117">hello 底下定義的預設包含有關要 tooencode 如何您的檔案，以及所需的資訊 toogenerate 縮圖。</span><span class="sxs-lookup"><span data-stu-id="d05b0-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="d05b0-118">您可以接受任何內記載的 hello MES 預設[這](media-services-mes-presets-overview.md)區段，並將產生縮圖的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d05b0-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="d05b0-119">hello **SceneChangeDetection**中 hello 下列預設設定才會設定 tootrue 編碼 tooa 單一位元速率視訊。</span><span class="sxs-lookup"><span data-stu-id="d05b0-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="d05b0-120">如果您的編碼 tooa 多位元速率視訊及設定**SceneChangeDetection** tootrue，hello 編碼器會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="d05b0-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="d05b0-121">如需結構描述的資訊，請參閱 [這個主題](media-services-mes-schema.md) 。</span><span class="sxs-lookup"><span data-stu-id="d05b0-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="d05b0-122">請確定 tooreview hello[考量](#considerations)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d05b0-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="d05b0-123"><a id="json"></a>JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-123"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="d05b0-124"><a id="xml"></a>XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-124"><a id="xml"></a>XML preset</span></span>
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
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="d05b0-125">考量</span><span class="sxs-lookup"><span data-stu-id="d05b0-125">Considerations</span></span>

<span data-ttu-id="d05b0-126">hello 下列考量適用於：</span><span class="sxs-lookup"><span data-stu-id="d05b0-126">hello following considerations apply:</span></span>

* <span data-ttu-id="d05b0-127">hello 使用明確的時間戳記的開始/步驟/範圍假設該 hello 輸入的來源是在至少 1 分鐘長。</span><span class="sxs-lookup"><span data-stu-id="d05b0-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="d05b0-128">具有 Start、Step 和 Range 字串屬性的 Jpg/Png/BmpImage 項目 - 這些可以解譯為：</span><span class="sxs-lookup"><span data-stu-id="d05b0-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="d05b0-129">畫面格數目 (如果是非負整數)，例如 "Start": "120"、</span><span class="sxs-lookup"><span data-stu-id="d05b0-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="d05b0-130">如果表示為 %加相對 toosource 會持續時間。 例如"Start":"15%」，或</span><span class="sxs-lookup"><span data-stu-id="d05b0-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="d05b0-131">時間戳記 (如果以 HH:MM:SS...</span><span class="sxs-lookup"><span data-stu-id="d05b0-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="d05b0-132">格式表示)，例如 "Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="d05b0-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="d05b0-133">您可以隨意混合使用標記法。</span><span class="sxs-lookup"><span data-stu-id="d05b0-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="d05b0-134">此外，開始也支援特殊的巨集: {最佳}，其中嘗試 toodetermine hello 第一個 「 有趣 」 畫面格的 hello 內容附註: (步驟和範圍時開始設定得忽略 {最佳})</span><span class="sxs-lookup"><span data-stu-id="d05b0-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="d05b0-135">預設值：Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="d05b0-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="d05b0-136">輸出格式需要明確地提供每個影像格式 toobe: Jpg/Png/BmpFormat。</span><span class="sxs-lookup"><span data-stu-id="d05b0-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="d05b0-137">存在時，MES 符合 JpgVideo tooJpgFormat，依此類推。</span><span class="sxs-lookup"><span data-stu-id="d05b0-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="d05b0-138">OutputFormat 導入了新的影像轉碼器特定巨集: {}，而且需要 toobe 存在 （一次，一次） 用於索引的影像輸出格式。</span><span class="sxs-lookup"><span data-stu-id="d05b0-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="d05b0-139"><a id="trim_video"></a>修剪視訊 (裁剪)</span><span class="sxs-lookup"><span data-stu-id="d05b0-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="d05b0-140">此章節討論修改 hello 編碼器預設 tooclip 或修剪 hello 輸入的視訊 hello 輸入其中是所謂的夾層檔或點播檔案。</span><span class="sxs-lookup"><span data-stu-id="d05b0-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="d05b0-141">– hello 編碼器也可以使用的 tooclip 或修剪資產，擷取或封存的即時資料流中的 hello 詳細資料，這可用[這篇部落格](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/)。</span><span class="sxs-lookup"><span data-stu-id="d05b0-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="d05b0-142">tootrim 視訊，您可以接受任何內記載的 hello MES 預設[這](media-services-mes-presets-overview.md)區段，並修改 hello**來源**項目 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="d05b0-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="d05b0-143">hello StartTime 值必須 toomatch hello 絕對時間戳記的 hello 輸入視訊。</span><span class="sxs-lookup"><span data-stu-id="d05b0-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="d05b0-144">例如，如果 hello hello 輸入視訊的第一個畫面格具有時間戳記的 12:00:10.000，則 StartTime 應該至少 12:00:10.000 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="d05b0-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="d05b0-145">在 [hello 下列範例中，我們假設 hello 輸入視訊的開始時間戳記為零。</span><span class="sxs-lookup"><span data-stu-id="d05b0-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="d05b0-146">**來源**應放在 hello 預設 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="d05b0-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="d05b0-147"><a id="json"></a>JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
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
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
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
              "Width": 320,
              "Height": 180,
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

### <a name="xml-preset"></a><span data-ttu-id="d05b0-148">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-148">XML preset</span></span>
<span data-ttu-id="d05b0-149">tootrim 視訊，您可以接受任何內記載的 hello MES 預設[這裡](media-services-mes-presets-overview.md)和修改 hello**來源**項目 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="d05b0-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
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
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
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
              <MaxBitrate>1000</MaxBitrate>
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
              <Width>320</Width>
              <Height>180</Height>
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

## <span data-ttu-id="d05b0-150"><a id="overlay"></a>建立疊加層</span><span class="sxs-lookup"><span data-stu-id="d05b0-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="d05b0-151">媒體編碼器標準 hello 可讓您 toooverlay 到現有的視訊映像。</span><span class="sxs-lookup"><span data-stu-id="d05b0-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="d05b0-152">目前支援下列格式的 hello: png、 jpg、 gif、 bmp 及。</span><span class="sxs-lookup"><span data-stu-id="d05b0-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="d05b0-153">hello 底下定義的預設值是視訊重疊的基本範例。</span><span class="sxs-lookup"><span data-stu-id="d05b0-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="d05b0-154">此外 toodefining 了預設檔案，您也可以 toolet 媒體服務知道 hello 資產中的檔案，而且 hello 覆疊影像的檔案，在想 toooverlay hello 映像的 hello 來源視訊。</span><span class="sxs-lookup"><span data-stu-id="d05b0-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="d05b0-155">hello 視訊檔具有 toobe hello**主要**檔案。</span><span class="sxs-lookup"><span data-stu-id="d05b0-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="d05b0-156">如果您使用.NET，新增下列 toohello.NET 範例中所定義的兩個函式的 hello[這](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet)主題。</span><span class="sxs-lookup"><span data-stu-id="d05b0-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="d05b0-157">hello **UploadMediaFilesFromFolder**函式將從資料夾 （例如，BigBuckBunny.mp4 和 Image001.png） 檔案上傳和設定 hello mp4 檔案 toobe hello 主要檔案 hello 資產中的。</span><span class="sxs-lookup"><span data-stu-id="d05b0-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="d05b0-158">hello **EncodeWithOverlay**函式會使用 hello 自訂預設的檔案傳遞 tooit （例如，「 hello 」 預設，如下所示） toocreate hello 編碼工作。</span><span class="sxs-lookup"><span data-stu-id="d05b0-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="d05b0-159">目前限制：</span><span class="sxs-lookup"><span data-stu-id="d05b0-159">Current limitations:</span></span>
>
> <span data-ttu-id="d05b0-160">不支援 hello 重疊的不透明度設定。</span><span class="sxs-lookup"><span data-stu-id="d05b0-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="d05b0-161">將來源視訊檔案和 hello 覆疊影像檔案有 toobe 在 hello 相同資產，並為此資產中的 hello 主要檔案 hello 視訊檔案的需求 toobe 組。</span><span class="sxs-lookup"><span data-stu-id="d05b0-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="d05b0-162">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
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
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="d05b0-163">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="d05b0-164"><a id="silent_audio"></a>在輸入不含音訊時插入靜音曲目</span><span class="sxs-lookup"><span data-stu-id="d05b0-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="d05b0-165">根據預設，如果您傳送僅包含視訊、 且沒有音訊輸入的 toohello 編碼器然後 hello 輸出資產包含檔案，其中包含只視訊資料。</span><span class="sxs-lookup"><span data-stu-id="d05b0-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="d05b0-166">某些播放程式可能無法再 toohandle 這類輸出資料流。</span><span class="sxs-lookup"><span data-stu-id="d05b0-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="d05b0-167">在這個案例中，您可以使用此設定 tooforce hello 編碼器 tooadd 無訊息的音訊播放軌 toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="d05b0-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="d05b0-168">tooforce hello 編碼器 tooproduce 包含無訊息的音訊播放軌時輸入有沒有音訊的資產指定 hello"InsertSilenceIfNoAudio"值。</span><span class="sxs-lookup"><span data-stu-id="d05b0-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="d05b0-169">您可以採取任何 hello MES 預設記載於[這](media-services-mes-presets-overview.md)區段，然後進行下列修改的 hello:</span><span class="sxs-lookup"><span data-stu-id="d05b0-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="d05b0-170">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="d05b0-171">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="d05b0-172"><a id="deinterlacing"></a>停用自動去交錯</span><span class="sxs-lookup"><span data-stu-id="d05b0-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="d05b0-173">客戶不需要 toodo 任何項目如果它們像 hello 交錯內容 toobe 自動取消交錯式。</span><span class="sxs-lookup"><span data-stu-id="d05b0-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="d05b0-174">Hello 去交錯自動開啟時 （預設值） hello hello MES 沒有自動偵測的交錯式框架和只能取消 interlaces 框架標示為交錯式。</span><span class="sxs-lookup"><span data-stu-id="d05b0-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="d05b0-175">您可以關閉 hello 自動去交錯。</span><span class="sxs-lookup"><span data-stu-id="d05b0-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="d05b0-176">但不建議您這樣做。</span><span class="sxs-lookup"><span data-stu-id="d05b0-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="d05b0-177">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="d05b0-178">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="d05b0-179"><a id="audio_only"></a>純音訊預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="d05b0-180">本節示範兩個純音訊的 MES 預設值︰AAC 音訊和 AAC 好品質音訊。</span><span class="sxs-lookup"><span data-stu-id="d05b0-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="d05b0-181">AAC 音訊</span><span class="sxs-lookup"><span data-stu-id="d05b0-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
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
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="d05b0-182">AAC 好品質音訊</span><span class="sxs-lookup"><span data-stu-id="d05b0-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="d05b0-183"><a id="concatenate"></a>串連兩個以上的視訊檔案</span><span class="sxs-lookup"><span data-stu-id="d05b0-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="d05b0-184">hello 下列範例說明如何產生預設的 tooconcatenate 兩個或多個視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="d05b0-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="d05b0-185">hello 最常見的案例是當您想 tooadd 標頭或結尾 toohello 主要影片。</span><span class="sxs-lookup"><span data-stu-id="d05b0-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="d05b0-186">hello 為了 hello 視訊檔案一起正在編輯共用內容 （視訊解析度，畫面播放速率、 音訊播放軌計數等等） 時使用。</span><span class="sxs-lookup"><span data-stu-id="d05b0-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="d05b0-187">您應該要特別注意不 toomix 的不同的畫面格速率或視訊與音訊音軌的數目不同。</span><span class="sxs-lookup"><span data-stu-id="d05b0-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="d05b0-188">hello hello 串連 」 功能的目前設計必須要有該 hello 輸入視訊剪輯會一致方面的解析度，畫面播放速率等等。</span><span class="sxs-lookup"><span data-stu-id="d05b0-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="d05b0-189">需求和考量</span><span class="sxs-lookup"><span data-stu-id="d05b0-189">Requirements and considerations</span></span>

* <span data-ttu-id="d05b0-190">輸入視訊應該只有一個曲目。</span><span class="sxs-lookup"><span data-stu-id="d05b0-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="d05b0-191">輸入影片都應該具備 hello 相同的畫面播放速率。</span><span class="sxs-lookup"><span data-stu-id="d05b0-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="d05b0-192">您必須將視訊上載到個別的資產，並將 hello 視訊設為每個資產中的 hello 主要檔案。</span><span class="sxs-lookup"><span data-stu-id="d05b0-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="d05b0-193">您需要視訊 tooknow hello 持續的時間。</span><span class="sxs-lookup"><span data-stu-id="d05b0-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="d05b0-194">hello 以下的範例預設會假設所有 hello 輸入的視訊都開始時間戳記為零。</span><span class="sxs-lookup"><span data-stu-id="d05b0-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="d05b0-195">您需要 toomodify hello StartTime 值 hello 視訊有不同的開始時間戳記，通常是與即時封存 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="d05b0-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="d05b0-196">hello JSON 的預設可明確參考 toohello 的 hello 輸入資產的 AssetID 值。</span><span class="sxs-lookup"><span data-stu-id="d05b0-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="d05b0-197">hello 範例程式碼假設已儲存 JSON 預設該 hello tooa 本機檔案，例如"C:\supportFiles\preset.json"。</span><span class="sxs-lookup"><span data-stu-id="d05b0-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="d05b0-198">它也假設兩個資產都由上傳兩個視訊檔案，而且您知道 hello 結果的 AssetID 值。</span><span class="sxs-lookup"><span data-stu-id="d05b0-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="d05b0-199">hello 程式碼片段和 JSON 的預設顯示串連兩個視訊檔案的範例。</span><span class="sxs-lookup"><span data-stu-id="d05b0-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="d05b0-200">您可以擴充 toomore 比由兩個視訊：</span><span class="sxs-lookup"><span data-stu-id="d05b0-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="d05b0-201">呼叫工作。InputAssets.Add() 重複 tooadd 順序中的多個視訊。</span><span class="sxs-lookup"><span data-stu-id="d05b0-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="d05b0-202">使對應 hello 中加入更多的項目編輯 toohello 「 來源 」 項目 hello JSON，在相同的順序。</span><span class="sxs-lookup"><span data-stu-id="d05b0-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="d05b0-203">.NET 程式碼</span><span class="sxs-lookup"><span data-stu-id="d05b0-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="d05b0-204">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-204">JSON preset</span></span>

<span data-ttu-id="d05b0-205">更新您的自訂預設的 tooconcatenate，hello 資產識別碼與 hello 適當的時間區段的每個視訊。</span><span class="sxs-lookup"><span data-stu-id="d05b0-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
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

## <span data-ttu-id="d05b0-206"><a id="crop"></a>以 Media Encoder Standard 裁剪影片</span><span class="sxs-lookup"><span data-stu-id="d05b0-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="d05b0-207">請參閱 hello[裁剪視訊媒體編碼器標準](media-services-crop-video.md)主題。</span><span class="sxs-lookup"><span data-stu-id="d05b0-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="d05b0-208"><a id="no_video"></a>在輸入不含視訊時插入視訊播放軌</span><span class="sxs-lookup"><span data-stu-id="d05b0-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="d05b0-209">根據預設，如果您傳送輸入的 toohello 編碼器只包含音訊和沒有影像，然後 hello 輸出資產包含檔案包含只音訊資料。</span><span class="sxs-lookup"><span data-stu-id="d05b0-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="d05b0-210">某些播放程式，包括 Azure Media Player (請參閱[這](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) 可能不是能 toohandle 這類資料流。</span><span class="sxs-lookup"><span data-stu-id="d05b0-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="d05b0-211">您可以在這個案例中使用此設定 tooforce hello 編碼器 tooadd 單色視訊播放軌 toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="d05b0-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="d05b0-212">強制 hello 編碼器 tooinsert hello 輸出視訊播放軌增加 hello 大小輸出資產，並藉此 hello hello 編碼工作的相關成本。</span><span class="sxs-lookup"><span data-stu-id="d05b0-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="d05b0-213">您應該會執行測試 tooverify 結果增加對每月費用適度造成影響。</span><span class="sxs-lookup"><span data-stu-id="d05b0-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="d05b0-214">只有 hello 最低位元速率將視訊</span><span class="sxs-lookup"><span data-stu-id="d05b0-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="d05b0-215">假設您使用多重位元速率編碼預設例如["H264 多重位元速率 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode 整個輸入資料流，其中包含混合的視訊檔及純音訊檔案類別目錄。</span><span class="sxs-lookup"><span data-stu-id="d05b0-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="d05b0-216">在此案例中，當 hello 輸入有視訊，您可能想 tooforce hello 編碼器 tooinsert 視訊單色追蹤只 hello 最低位元速率，但不要 tooinserting 每一個輸出位元速率視訊。</span><span class="sxs-lookup"><span data-stu-id="d05b0-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="d05b0-217">tooachieve，您需要 toouse hello **InsertBlackIfNoVideoBottomLayerOnly**旗標。</span><span class="sxs-lookup"><span data-stu-id="d05b0-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="d05b0-218">您可以採取任何 hello MES 預設記載於[這](media-services-mes-presets-overview.md)區段，然後進行下列修改的 hello:</span><span class="sxs-lookup"><span data-stu-id="d05b0-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="d05b0-219">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="d05b0-220">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-220">XML preset</span></span>

<span data-ttu-id="d05b0-221">當您使用 XML，使用條件 ="InsertBlackIfNoVideoBottomLayerOnly"做為屬性 toohello **H264Video**項目及條件太 ="InsertSilenceIfNoAudio"做為屬性**AACAudio**。</span><span class="sxs-lookup"><span data-stu-id="d05b0-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="d05b0-222">以所有輸出位元速率插入視訊</span><span class="sxs-lookup"><span data-stu-id="d05b0-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="d05b0-223">假設您使用多重位元速率編碼預設例如["H264 多重位元速率 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode 整個輸入資料流，其中包含混合的視訊檔及純音訊檔案類別目錄。</span><span class="sxs-lookup"><span data-stu-id="d05b0-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="d05b0-224">在此案例中，當 hello 輸入有視訊，您可能想 tooforce hello 編碼器 tooinsert 單色視訊播放軌所有 hello 輸出種位元速率。</span><span class="sxs-lookup"><span data-stu-id="d05b0-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="d05b0-225">如此可確保您的輸出資產是與視訊音軌的音訊音軌尊重 toonumber 所有同質性。</span><span class="sxs-lookup"><span data-stu-id="d05b0-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="d05b0-226">tooachieve，您需要 toospecify hello"InsertBlackIfNoVideo 」 旗標。</span><span class="sxs-lookup"><span data-stu-id="d05b0-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="d05b0-227">您可以採取任何 hello MES 預設記載於[這](media-services-mes-presets-overview.md)區段，然後進行下列修改的 hello:</span><span class="sxs-lookup"><span data-stu-id="d05b0-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="d05b0-228">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="d05b0-229">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-229">XML preset</span></span>

<span data-ttu-id="d05b0-230">當您使用 XML，使用條件 ="InsertBlackIfNoVideo"做為屬性 toohello **H264Video**項目及條件太 ="InsertSilenceIfNoAudio"做為屬性**AACAudio**。</span><span class="sxs-lookup"><span data-stu-id="d05b0-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="d05b0-231"><a id="rotate_video"></a>旋轉視訊</span><span class="sxs-lookup"><span data-stu-id="d05b0-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="d05b0-232">hello[媒體編碼器標準](media-services-dotnet-encode-with-media-encoder-standard.md)支援旋轉 0/90/180/270 角度。</span><span class="sxs-lookup"><span data-stu-id="d05b0-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="d05b0-233">hello 預設行為是 「 自動 」，它會嘗試在 hello 連入的視訊檔 toodetect hello 旋轉中繼資料和補償它。</span><span class="sxs-lookup"><span data-stu-id="d05b0-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="d05b0-234">Hello 如下**來源**hello 預設設定中定義的項目 tooone[這](media-services-mes-presets-overview.md)> 一節：</span><span class="sxs-lookup"><span data-stu-id="d05b0-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="d05b0-235">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="d05b0-236">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="d05b0-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="d05b0-237">此外，請參閱[這](media-services-mes-schema.md#PreserveResolutionAfterRotation)需 hello 編碼器如何解譯在 [hello hello 寬度和高度設定的詳細資訊的主題預設觸發旋轉補償時。</span><span class="sxs-lookup"><span data-stu-id="d05b0-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="d05b0-238">如果有的話，在 hello 輸入段影片中，您可以使用 hello 值"0"tooindicate toohello 編碼器 tooignore 旋轉中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d05b0-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d05b0-239">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="d05b0-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d05b0-240">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d05b0-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d05b0-241">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d05b0-241">See Also</span></span>
[<span data-ttu-id="d05b0-242">媒體服務編碼概觀</span><span class="sxs-lookup"><span data-stu-id="d05b0-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
