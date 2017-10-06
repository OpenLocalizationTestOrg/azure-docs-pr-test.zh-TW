---
title: "aaaCustomizing 標準媒體編碼器預設 |Microsoft 文件"
description: "本主題說明如何 tooperform 進階自訂媒體編碼器標準工作預設編碼方式。 hello 主題顯示如何 toouse Media Services.NET SDK toocreate 編碼工作與工作。 它也會顯示自訂 toosupply 預設 toohello 編碼工作的設定。"
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
ms.openlocfilehash: fa8c3bef63b0c1ecc88a6b8874ecbff3a8028a57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="71a77-105">自訂媒體編碼器標準預設</span><span class="sxs-lookup"><span data-stu-id="71a77-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="71a77-106">概觀</span><span class="sxs-lookup"><span data-stu-id="71a77-106">Overview</span></span>

<span data-ttu-id="71a77-107">本主題說明 tooperform 進階編碼的媒體編碼器標準 (MES) 使用自訂的預設值。</span><span class="sxs-lookup"><span data-stu-id="71a77-107">This topic shows how tooperform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="71a77-108">hello 主題會使用.NET toocreate，編碼的工作和作業來執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="71a77-108">hello topic uses .NET toocreate an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="71a77-109">本主題中您會看到如何 toocustomize 採取的預設 hello [H264 多重位元速率 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md)預設及減少 hello 層的數目。</span><span class="sxs-lookup"><span data-stu-id="71a77-109">In this topic you will see how toocustomize a preset by taking hello [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing hello number of layers.</span></span> <span data-ttu-id="71a77-110">hello[自訂媒體編碼器標準預設](media-services-advanced-encoding-with-mes.md)主題示範如何自訂預設值可以是使用的 tooperform 進階編碼工作。</span><span class="sxs-lookup"><span data-stu-id="71a77-110">hello [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used tooperform advanced encoding tasks.</span></span>

## <span data-ttu-id="71a77-111"><a id="customizing_presets"></a> 自訂 MES 預設值</span><span class="sxs-lookup"><span data-stu-id="71a77-111"><a id="customizing_presets"></a> Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="71a77-112">原始預設</span><span class="sxs-lookup"><span data-stu-id="71a77-112">Original preset</span></span>

<span data-ttu-id="71a77-113">儲存 hello JSON 定義中 hello [H264 多重位元速率 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md)某些.json 副檔名的檔案中的主題。</span><span class="sxs-lookup"><span data-stu-id="71a77-113">Save hello JSON defined in hello [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="71a77-114">例如，**CustomPreset_JSON.json**。</span><span class="sxs-lookup"><span data-stu-id="71a77-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="71a77-115">自訂的預設</span><span class="sxs-lookup"><span data-stu-id="71a77-115">Customized preset</span></span>

<span data-ttu-id="71a77-116">開啟 hello **CustomPreset_JSON.json**檔案，並移除從前三個層級**H264Layers**讓您的檔案，看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="71a77-116">Open hello **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
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
    

## <span data-ttu-id="71a77-117"><a id="encoding_with_dotnet"></a>使用媒體服務 .NET SDK 進行編碼</span><span class="sxs-lookup"><span data-stu-id="71a77-117"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="71a77-118">hello，下列程式碼範例會使用 Media Services.NET SDK tooperform hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="71a77-118">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="71a77-119">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="71a77-119">Create an encoding job.</span></span>
- <span data-ttu-id="71a77-120">取得參考 toohello 媒體編碼器標準編碼器。</span><span class="sxs-lookup"><span data-stu-id="71a77-120">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="71a77-121">載入自訂 JSON 預設您建立 hello 前一節中的 hello。</span><span class="sxs-lookup"><span data-stu-id="71a77-121">Load hello custom JSON preset that you created in hello previous section.</span></span> 
  
        // Load hello JSON from hello local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="71a77-122">新增編碼工作 toohello 工作。</span><span class="sxs-lookup"><span data-stu-id="71a77-122">Add an encoding task toohello job.</span></span> 
- <span data-ttu-id="71a77-123">指定 hello 輸入資產 toobe 編碼。</span><span class="sxs-lookup"><span data-stu-id="71a77-123">Specify hello input asset toobe encoded.</span></span>
- <span data-ttu-id="71a77-124">建立會包含 hello 編碼資產的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="71a77-124">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="71a77-125">加入事件處理常式 toocheck hello 工作進度。</span><span class="sxs-lookup"><span data-stu-id="71a77-125">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="71a77-126">送出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="71a77-126">Submit hello job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="71a77-127">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="71a77-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="71a77-128">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="71a77-128">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="71a77-129">範例</span><span class="sxs-lookup"><span data-stu-id="71a77-129">Example</span></span>   

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
        // Read values from hello App.config file.
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

            // Encode and generate hello output using custom presets.
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
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="71a77-130">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="71a77-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="71a77-131">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="71a77-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="71a77-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="71a77-132">See Also</span></span>
[<span data-ttu-id="71a77-133">媒體服務編碼概觀</span><span class="sxs-lookup"><span data-stu-id="71a77-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

