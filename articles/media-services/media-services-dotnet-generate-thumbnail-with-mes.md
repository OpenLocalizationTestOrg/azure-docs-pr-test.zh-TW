---
title: "如何搭配 .NET 使用 Media Encoder Standard 產生縮圖"
description: "本主題說明如何使用 .NET 編碼資產，並同時使用媒體編碼器標準產生縮圖。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 89d15cbdf71a140e78f34e07ff208776b7d4cab3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="170b4-103">如何搭配 .NET 使用 Media Encoder Standard 產生縮圖</span><span class="sxs-lookup"><span data-stu-id="170b4-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="170b4-104">您可以使用媒體編碼器標準，以 [JPEG](https://en.wikipedia.org/wiki/JPEG)、[PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) 或 [BMP](https://en.wikipedia.org/wiki/BMP_file_format) 影像檔案格式，從您的輸入視訊中產生一或多個縮圖。</span><span class="sxs-lookup"><span data-stu-id="170b4-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="170b4-105">您可以送出只產生影像的工作，或是結合縮圖產生與編碼。</span><span class="sxs-lookup"><span data-stu-id="170b4-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="170b4-106">本主題會提供幾個對於這類情況的範例 XML 和 JSON 縮圖預設。</span><span class="sxs-lookup"><span data-stu-id="170b4-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="170b4-107">在主題的結尾有[範例程式碼](#code_sample)，示範如何使用 Media Services .NET SDK，以完成編碼工作。</span><span class="sxs-lookup"><span data-stu-id="170b4-107">At the end of the topic, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="170b4-108">如需用於範例預設中項目的詳細資料，您應該檢閱 [Media Encoder Standard 結構描述](media-services-mes-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="170b4-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="170b4-109">請務必閱讀 [考量](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) 一節。</span><span class="sxs-lookup"><span data-stu-id="170b4-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="170b4-110">範例 – 單一 PNG 檔案</span><span class="sxs-lookup"><span data-stu-id="170b4-110">Example – single PNG file</span></span>

<span data-ttu-id="170b4-111">下列 JSON 和 XML 預設可以用來從輸入視訊的前幾秒產生單一輸出 PNG 檔，在這前幾秒，編碼器會進行最佳嘗試，尋找「有趣」的畫面。</span><span class="sxs-lookup"><span data-stu-id="170b4-111">The following JSON and XML preset can be used to produce a single output PNG file out of the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="170b4-112">請注意，輸出影像大小已設定為 100%，表示這些會符合輸入視訊的大小。</span><span class="sxs-lookup"><span data-stu-id="170b4-112">Note that the output image dimensions have been set to 100%, meaning these will match the dimensions of the input video.</span></span> <span data-ttu-id="170b4-113">另外也請注意，“Outputs” 中的 “Format” 設定必須如何符合 “Codecs” 區段中的 “PngLayers” 使用。</span><span class="sxs-lookup"><span data-stu-id="170b4-113">Note also how the “Format” setting in “Outputs” is required to match the use of “PngLayers” in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="170b4-114">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="170b4-114">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="170b4-115">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="170b4-115">XML preset</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="170b4-116">範例 – 一系列的 JPEG 影像</span><span class="sxs-lookup"><span data-stu-id="170b4-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="170b4-117">下列 JSON 和 XML 預設可以用來產生一組 10 個影像，分別是在輸入時間軸的時間戳記 5%、15%、...、95% 等等，其中影像大小指定為輸入視訊影像大小的四分之一。</span><span class="sxs-lookup"><span data-stu-id="170b4-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="170b4-118">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="170b4-118">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="170b4-119">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="170b4-119">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="170b4-120">範例 – 在特定時間戳記的一個影像</span><span class="sxs-lookup"><span data-stu-id="170b4-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="170b4-121">下列 JSON 和 XML 預設可以用來在輸入視訊的 30 秒標記處產生單一 JPEG 影像。</span><span class="sxs-lookup"><span data-stu-id="170b4-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30 second mark of the input video.</span></span> <span data-ttu-id="170b4-122">此預設會預期輸入的持續時間為 30 秒以上 (否則作業將會失敗)。</span><span class="sxs-lookup"><span data-stu-id="170b4-122">This preset expects the input to be more than 30 seconds in duration (else the job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="170b4-123">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="170b4-123">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="170b4-124">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="170b4-124">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="170b4-125"><a id="code_sample"></a>範例 – 編碼視訊，並產生縮圖</span><span class="sxs-lookup"><span data-stu-id="170b4-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="170b4-126">下列程式碼範例使用媒體服務 .NET SDK 執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="170b4-126">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="170b4-127">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="170b4-127">Create an encoding job.</span></span>
* <span data-ttu-id="170b4-128">取得對 Media Encoder Standard 編碼器的參考</span><span class="sxs-lookup"><span data-stu-id="170b4-128">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="170b4-129">載入預設 [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) 或 [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)，其包含產生縮圖所需的編碼預設以及資訊。</span><span class="sxs-lookup"><span data-stu-id="170b4-129">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="170b4-130">您可以在檔案中儲存此 [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) 或 [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)，並使用下列程式碼載入檔案。</span><span class="sxs-lookup"><span data-stu-id="170b4-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="170b4-131">將單一編碼工作加入工作。</span><span class="sxs-lookup"><span data-stu-id="170b4-131">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="170b4-132">指定要編碼的輸入資產。</span><span class="sxs-lookup"><span data-stu-id="170b4-132">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="170b4-133">建立將包含已編碼資產的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="170b4-133">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="170b4-134">加入事件處理常式來檢查工作進度。</span><span class="sxs-lookup"><span data-stu-id="170b4-134">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="170b4-135">提交作業。</span><span class="sxs-lookup"><span data-stu-id="170b4-135">Submit the job.</span></span>

<span data-ttu-id="170b4-136">請參閱[使用 .NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)主題，以取得如何設定開發環境的指示。</span><span class="sxs-lookup"><span data-stu-id="170b4-136">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how to set up your dev environment.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
            }

            private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
            {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
                case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
                case JobState.Canceled:
                case JobState.Error:

                // Cast sender as a job.
                IJob job = (IJob)sender;

                // Display or log error details as needed.
                break;
                default:
                break;
            }
            }

            private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
            }
        }
        }

## <span data-ttu-id="170b4-137"><a id="json"></a>縮圖 JSON 預設</span><span class="sxs-lookup"><span data-stu-id="170b4-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="170b4-138">如需結構描述的資訊，請參閱 [這個主題](https://msdn.microsoft.com/library/mt269962.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="170b4-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
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
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="170b4-139"><a id="xml"></a>縮圖 XML 預設</span><span class="sxs-lookup"><span data-stu-id="170b4-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="170b4-140">如需結構描述的資訊，請參閱 [這個主題](https://msdn.microsoft.com/library/mt269962.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="170b4-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a><span data-ttu-id="170b4-141">考量</span><span class="sxs-lookup"><span data-stu-id="170b4-141">Considerations</span></span>
<span data-ttu-id="170b4-142">您必須考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="170b4-142">The following considerations apply:</span></span>

* <span data-ttu-id="170b4-143">為 Start/Step/Range 使用明確的時間戳記會假設輸入來源至少為 1 分鐘的長度。</span><span class="sxs-lookup"><span data-stu-id="170b4-143">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="170b4-144">具有 Start、Step 和 Range 字串屬性的 Jpg/Png/BmpImage 項目 – 這些可以解譯為：</span><span class="sxs-lookup"><span data-stu-id="170b4-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="170b4-145">畫面格數目 (如果是非負整數)，例如：</span><span class="sxs-lookup"><span data-stu-id="170b4-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="170b4-146">"Start"："120"，</span><span class="sxs-lookup"><span data-stu-id="170b4-146">"Start": "120",</span></span>
  * <span data-ttu-id="170b4-147">相對於持續時間 (如果以  % 尾碼表示)，例如：</span><span class="sxs-lookup"><span data-stu-id="170b4-147">Relative to source duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="170b4-148">"Start"："15%" 或</span><span class="sxs-lookup"><span data-stu-id="170b4-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="170b4-149">時間戳記 (如果以 HH:MM:SS...</span><span class="sxs-lookup"><span data-stu-id="170b4-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="170b4-150">format。</span><span class="sxs-lookup"><span data-stu-id="170b4-150">format.</span></span> <span data-ttu-id="170b4-151">例如</span><span class="sxs-lookup"><span data-stu-id="170b4-151">Eg.</span></span> <span data-ttu-id="170b4-152">"Start"："00:01:00"</span><span class="sxs-lookup"><span data-stu-id="170b4-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="170b4-153">您可以隨意混合使用標記法。</span><span class="sxs-lookup"><span data-stu-id="170b4-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="170b4-154">此外， Start 也支援特殊的巨集 (即 {Best})，它會嘗試判斷第一個「 有趣 」的內容畫面。附註：(Start 設為 {Best} 時，會忽略 Step 與 Range)</span><span class="sxs-lookup"><span data-stu-id="170b4-154">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="170b4-155">預設值：Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="170b4-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="170b4-156">必須明確地提供每個影像格式的輸出格式：Jpg/Png/BmpFormat。</span><span class="sxs-lookup"><span data-stu-id="170b4-156">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="170b4-157">顯示時，AMS 會讓 JpgVideo 與 JpgFormat 相符，依此類推。</span><span class="sxs-lookup"><span data-stu-id="170b4-157">When present, MES will match JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="170b4-158">OutputFormat 引進了新的影像轉碼器特定巨集 (即 {Index})，必須針對影像輸出格式提供一次 (只需一次)。</span><span class="sxs-lookup"><span data-stu-id="170b4-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="170b4-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="170b4-159">Next steps</span></span>

<span data-ttu-id="170b4-160">您可以在編碼工作擱置時檢查[作業進度](media-services-check-job-progress.md)。</span><span class="sxs-lookup"><span data-stu-id="170b4-160">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="170b4-161">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="170b4-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="170b4-162">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="170b4-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="170b4-163">另請參閱</span><span class="sxs-lookup"><span data-stu-id="170b4-163">See Also</span></span>
[<span data-ttu-id="170b4-164">媒體服務編碼概觀</span><span class="sxs-lookup"><span data-stu-id="170b4-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

