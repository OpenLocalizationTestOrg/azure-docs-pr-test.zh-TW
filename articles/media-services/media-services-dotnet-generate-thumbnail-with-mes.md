---
title: "搭配.NET 使用媒體編碼器標準 aaaHow toogenerate 縮圖"
description: "本主題說明如何 toouse.NET tooencode 資產，並產生縮圖在 hello 同時使用媒體編碼程式標準。"
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
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="987ba-103">如何搭配.NET 使用媒體編碼器標準 toogenerate 縮圖</span><span class="sxs-lookup"><span data-stu-id="987ba-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="987ba-104">您可以使用標準的媒體編碼器 toogenerate 一或多個縮圖從視訊在您輸入[JPEG](https://en.wikipedia.org/wiki/JPEG)， [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics)，或[BMP](https://en.wikipedia.org/wiki/BMP_file_format)影像檔案格式。</span><span class="sxs-lookup"><span data-stu-id="987ba-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="987ba-105">您可以送出只產生影像的工作，或是結合縮圖產生與編碼。</span><span class="sxs-lookup"><span data-stu-id="987ba-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="987ba-106">本主題會提供幾個對於這類情況的範例 XML 和 JSON 縮圖預設。</span><span class="sxs-lookup"><span data-stu-id="987ba-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="987ba-107">在 hello hello 主題結尾，沒有[範例程式碼](#code_sample)toouse hello Media Services.NET SDK tooaccomplish hello 編碼工作的方式，它會顯示。</span><span class="sxs-lookup"><span data-stu-id="987ba-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="987ba-108">如需有關範例的預設設定中所使用的 hello 元素的詳細資訊，您應該檢閱[媒體編碼器標準結構描述](media-services-mes-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="987ba-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="987ba-109">請確定 tooreview hello[考量](media-services-dotnet-generate-thumbnail-with-mes.md#considerations)> 一節。</span><span class="sxs-lookup"><span data-stu-id="987ba-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="987ba-110">範例 – 單一 PNG 檔案</span><span class="sxs-lookup"><span data-stu-id="987ba-110">Example – single PNG file</span></span>

<span data-ttu-id="987ba-111">hello 下列 JSON 和 XML 預設可以是單一輸出 PNG 檔案超出 hello 前幾個使用的 tooproduce hello 輸入視訊，其中 hello 編碼器會進行全力嘗試在尋找 「 有趣 」 的框架秒數。</span><span class="sxs-lookup"><span data-stu-id="987ba-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="987ba-112">請注意 hello 輸出影像尺寸，已設定 too100%，表示這些設定將會符合 hello 輸入視訊的 hello 維度。</span><span class="sxs-lookup"><span data-stu-id="987ba-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="987ba-113">也請注意 「 輸出 」 中的 hello 「 格式 」 設定的必要方式 toomatch hello"PngLayers"hello"轉碼器 」 一節中使用。</span><span class="sxs-lookup"><span data-stu-id="987ba-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="987ba-114">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="987ba-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="987ba-115">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="987ba-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="987ba-116">範例 – 一系列的 JPEG 影像</span><span class="sxs-lookup"><span data-stu-id="987ba-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="987ba-117">hello 下列 JSON 和 XML 預設可以使用的 tooproduce 一組在 5%的時間戳記的 10 個映像的 15%，95%的 hello 輸入時間軸，其中 hello 映像大小會是指定的 toobe 輸入視訊的 hello 一季。</span><span class="sxs-lookup"><span data-stu-id="987ba-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="987ba-118">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="987ba-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="987ba-119">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="987ba-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="987ba-120">範例 – 在特定時間戳記的一個影像</span><span class="sxs-lookup"><span data-stu-id="987ba-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="987ba-121">hello 下列 JSON 和 XML 預設可以使用的 tooproduce hello 輸入視訊的標記的單一 JPEG 影像 hello 在 30 秒。</span><span class="sxs-lookup"><span data-stu-id="987ba-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="987ba-122">此預設預期 hello 輸入的 toobe 的持續時間超過 30 秒 （其他 hello 作業將會失敗）。</span><span class="sxs-lookup"><span data-stu-id="987ba-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="987ba-123">JSON 預設值</span><span class="sxs-lookup"><span data-stu-id="987ba-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="987ba-124">XML 預設值</span><span class="sxs-lookup"><span data-stu-id="987ba-124">XML preset</span></span>
    
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

## <span data-ttu-id="987ba-125"><a id="code_sample"></a>範例 – 編碼視訊，並產生縮圖</span><span class="sxs-lookup"><span data-stu-id="987ba-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="987ba-126">hello，下列程式碼範例會使用 Media Services.NET SDK tooperform hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="987ba-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="987ba-127">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="987ba-127">Create an encoding job.</span></span>
* <span data-ttu-id="987ba-128">取得參考 toohello 媒體編碼器標準編碼器。</span><span class="sxs-lookup"><span data-stu-id="987ba-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="987ba-129">預設負載 hello [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml)或[JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)包含 hello 編碼預設值，以及所需的資訊 toogenerate 縮圖。</span><span class="sxs-lookup"><span data-stu-id="987ba-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="987ba-130">您可以儲存此[XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml)或[JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)檔，並使用 hello，下列程式碼 tooload hello 檔中。</span><span class="sxs-lookup"><span data-stu-id="987ba-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="987ba-131">加入單一編碼工作 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="987ba-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="987ba-132">指定 hello 輸入資產 toobe 編碼。</span><span class="sxs-lookup"><span data-stu-id="987ba-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="987ba-133">建立會包含 hello 編碼資產的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="987ba-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="987ba-134">加入事件處理常式 toocheck hello 工作進度。</span><span class="sxs-lookup"><span data-stu-id="987ba-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="987ba-135">送出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="987ba-135">Submit hello job.</span></span>

<span data-ttu-id="987ba-136">請參閱 hello[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)directions on 如何主題 tooset 開發環境。</span><span class="sxs-lookup"><span data-stu-id="987ba-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

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
            // Read values from hello App.config file.
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

            // Encode and generate hello thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
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

## <span data-ttu-id="987ba-137"><a id="json"></a>縮圖 JSON 預設</span><span class="sxs-lookup"><span data-stu-id="987ba-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="987ba-138">如需結構描述的資訊，請參閱 [這個主題](https://msdn.microsoft.com/library/mt269962.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="987ba-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="987ba-139"><a id="xml"></a>縮圖 XML 預設</span><span class="sxs-lookup"><span data-stu-id="987ba-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="987ba-140">如需結構描述的資訊，請參閱 [這個主題](https://msdn.microsoft.com/library/mt269962.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="987ba-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="987ba-141">考量</span><span class="sxs-lookup"><span data-stu-id="987ba-141">Considerations</span></span>
<span data-ttu-id="987ba-142">hello 下列考量適用於：</span><span class="sxs-lookup"><span data-stu-id="987ba-142">hello following considerations apply:</span></span>

* <span data-ttu-id="987ba-143">hello 使用明確的時間戳記的開始/步驟/範圍假設該 hello 輸入的來源是在至少 1 分鐘長。</span><span class="sxs-lookup"><span data-stu-id="987ba-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="987ba-144">具有 Start、Step 和 Range 字串屬性的 Jpg/Png/BmpImage 項目 – 這些可以解譯為：</span><span class="sxs-lookup"><span data-stu-id="987ba-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="987ba-145">畫面格數目 (如果是非負整數)，例如：</span><span class="sxs-lookup"><span data-stu-id="987ba-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="987ba-146">"Start"："120"，</span><span class="sxs-lookup"><span data-stu-id="987ba-146">"Start": "120",</span></span>
  * <span data-ttu-id="987ba-147">如果以 %-後置字元，例如表示相對 toosource 持續時間。</span><span class="sxs-lookup"><span data-stu-id="987ba-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="987ba-148">"Start"："15%" 或</span><span class="sxs-lookup"><span data-stu-id="987ba-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="987ba-149">時間戳記 (如果以 HH:MM:SS...</span><span class="sxs-lookup"><span data-stu-id="987ba-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="987ba-150">format。</span><span class="sxs-lookup"><span data-stu-id="987ba-150">format.</span></span> <span data-ttu-id="987ba-151">例如</span><span class="sxs-lookup"><span data-stu-id="987ba-151">Eg.</span></span> <span data-ttu-id="987ba-152">"Start"："00:01:00"</span><span class="sxs-lookup"><span data-stu-id="987ba-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="987ba-153">您可以隨意混合使用標記法。</span><span class="sxs-lookup"><span data-stu-id="987ba-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="987ba-154">此外，開始也支援特殊的巨集: {最佳}，其中嘗試 toodetermine hello 第一個 「 有趣 」 畫面格的 hello 內容附註: (步驟和範圍時開始設定得忽略 {最佳})</span><span class="sxs-lookup"><span data-stu-id="987ba-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="987ba-155">預設值：Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="987ba-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="987ba-156">輸出格式需要明確地提供每個影像格式 toobe: Jpg/Png/BmpFormat。</span><span class="sxs-lookup"><span data-stu-id="987ba-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="987ba-157">如果有，MES 會比對 JpgVideo tooJpgFormat，依此類推。</span><span class="sxs-lookup"><span data-stu-id="987ba-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="987ba-158">OutputFormat 導入了新的影像轉碼器特定巨集: {}，而且需要 toobe 存在 （一次，一次） 用於索引的影像輸出格式。</span><span class="sxs-lookup"><span data-stu-id="987ba-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="987ba-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="987ba-159">Next steps</span></span>

<span data-ttu-id="987ba-160">您可以檢查 hello[作業進度](media-services-check-job-progress.md)時 hello 編碼工作已暫止。</span><span class="sxs-lookup"><span data-stu-id="987ba-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="987ba-161">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="987ba-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="987ba-162">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="987ba-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="987ba-163">另請參閱</span><span class="sxs-lookup"><span data-stu-id="987ba-163">See Also</span></span>
[<span data-ttu-id="987ba-164">媒體服務編碼概觀</span><span class="sxs-lookup"><span data-stu-id="987ba-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

