---
title: "自訂媒體編碼器標準預設 | Microsoft Docs"
description: "本主題說明如何透過自訂 Media Encoder Standard 工作預設值執行進階編碼。 本主題說明如何使用媒體服務 .NET SDK 建立編碼工作與作業。 本主題也會說明如何提供自訂預設值給編碼作業。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: b4d25f07349043da8cb745930fde3371c98f9960
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="6a28e-105">自訂媒體編碼器標準預設</span><span class="sxs-lookup"><span data-stu-id="6a28e-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="6a28e-106">概觀</span><span class="sxs-lookup"><span data-stu-id="6a28e-106">Overview</span></span>

<span data-ttu-id="6a28e-107">本主題說明如何透過使用自訂預設的媒體編碼器標準 (MES) 執行進階編碼。</span><span class="sxs-lookup"><span data-stu-id="6a28e-107">This topic shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="6a28e-108">本主題使用 .NET 建立編碼工作與執行此工作的作業。</span><span class="sxs-lookup"><span data-stu-id="6a28e-108">The topic uses .NET to create an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="6a28e-109">在本主題中，您將了解如何採取 [H264 多重位元速率 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 預設值來自訂預設，並減少圖層數目。</span><span class="sxs-lookup"><span data-stu-id="6a28e-109">In this topic you will see how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span></span> <span data-ttu-id="6a28e-110">[自訂媒體編碼器標準預設](media-services-advanced-encoding-with-mes.md)主題示範可用於執行進階編碼工作的自訂預設。</span><span class="sxs-lookup"><span data-stu-id="6a28e-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used to perform advanced encoding tasks.</span></span>

## <span data-ttu-id="6a28e-111"><a id="customizing_presets"></a> 自訂 MES 預設值</span><span class="sxs-lookup"><span data-stu-id="6a28e-111"><a id="customizing_presets"></a> Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="6a28e-112">原始預設</span><span class="sxs-lookup"><span data-stu-id="6a28e-112">Original preset</span></span>

<span data-ttu-id="6a28e-113">將 [H264 多重位元速率 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 主題中定義的 JSON 儲存於一些副檔名為 .json 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="6a28e-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="6a28e-114">例如，**CustomPreset_JSON.json**。</span><span class="sxs-lookup"><span data-stu-id="6a28e-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="6a28e-115">自訂的預設</span><span class="sxs-lookup"><span data-stu-id="6a28e-115">Customized preset</span></span>

<span data-ttu-id="6a28e-116">開啟 **CustomPreset_JSON.json** 檔案，並從 **H264Layers** 移除前三層，您的檔案看起來就會像這樣。</span><span class="sxs-lookup"><span data-stu-id="6a28e-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
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
    

## <span data-ttu-id="6a28e-117"><a id="encoding_with_dotnet"></a>使用媒體服務 .NET SDK 進行編碼</span><span class="sxs-lookup"><span data-stu-id="6a28e-117"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="6a28e-118">下列程式碼範例使用媒體服務 .NET SDK 執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="6a28e-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="6a28e-119">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="6a28e-119">Create an encoding job.</span></span>
- <span data-ttu-id="6a28e-120">取得對 Media Encoder Standard 編碼器的參考</span><span class="sxs-lookup"><span data-stu-id="6a28e-120">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="6a28e-121">載入您在上一節建立的自訂 JSON 預設。</span><span class="sxs-lookup"><span data-stu-id="6a28e-121">Load the custom JSON preset that you created in the previous section.</span></span> 
  
        // Load the JSON from the local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="6a28e-122">將編碼工作新增至作業。</span><span class="sxs-lookup"><span data-stu-id="6a28e-122">Add an encoding task to the job.</span></span> 
- <span data-ttu-id="6a28e-123">指定要編碼的輸入資產。</span><span class="sxs-lookup"><span data-stu-id="6a28e-123">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="6a28e-124">建立將包含已編碼資產的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="6a28e-124">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="6a28e-125">加入事件處理常式來檢查工作進度。</span><span class="sxs-lookup"><span data-stu-id="6a28e-125">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="6a28e-126">提交作業。</span><span class="sxs-lookup"><span data-stu-id="6a28e-126">Submit the job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6a28e-127">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="6a28e-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="6a28e-128">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="6a28e-128">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="6a28e-129">範例</span><span class="sxs-lookup"><span data-stu-id="6a28e-129">Example</span></span>   

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace CustomizeMESPresests
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
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

            // Encode and generate the output using custom presets.
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
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="6a28e-130">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="6a28e-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6a28e-131">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="6a28e-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6a28e-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6a28e-132">See Also</span></span>
[<span data-ttu-id="6a28e-133">媒體服務編碼概觀</span><span class="sxs-lookup"><span data-stu-id="6a28e-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

