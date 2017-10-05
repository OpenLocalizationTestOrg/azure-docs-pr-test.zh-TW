---
title: "使用 Azure 媒體影片縮圖建立視訊摘要 | Microsoft Docs"
description: "視訊摘要可自動選取來源視訊的有趣片段，協助您建立較長視訊的摘要。 針對片長較長的視訊，如果您想要提供精彩內容的快速概觀，這非常有用。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 5d5afdaf22ffea8f3b77a154acb5d0a8dda74405
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-video-thumbnails-to-create-a-video-summarization"></a><span data-ttu-id="0ef45-104">使用 Azure 媒體視訊縮圖建立視訊摘要</span><span class="sxs-lookup"><span data-stu-id="0ef45-104">Use Azure Media Video Thumbnails to Create a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="0ef45-105">Overview</span><span class="sxs-lookup"><span data-stu-id="0ef45-105">Overview</span></span>
<span data-ttu-id="0ef45-106">**Azure 媒體視訊縮圖** 媒體處理器 (MP) 可讓您建立視訊的摘要；當視訊較長而客戶只想預覽摘要時，就非常實用。</span><span class="sxs-lookup"><span data-stu-id="0ef45-106">The **Azure Media Video Thumbnails** media processor (MP) enables you to create a summary of a video that is useful to customers who just want to preview a summary of a long video.</span></span> <span data-ttu-id="0ef45-107">例如，客戶可能會想在將滑鼠移至縮圖上時，查看簡短的「視訊摘要」。</span><span class="sxs-lookup"><span data-stu-id="0ef45-107">For example, customers might want to see a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="0ef45-108">透過設定預設值，調整 **Azure 媒體視訊縮圖** 的參數，您即可使用 MP 強大的拍攝偵測和串連技術，以演算法來產生描述性的子剪輯。</span><span class="sxs-lookup"><span data-stu-id="0ef45-108">By tweaking the parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use the MP's powerful shot detection and concatenation technology to algorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="0ef45-109">**Azure 媒體視訊縮圖** MP 目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="0ef45-109">The **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="0ef45-110">本主題提供有關 **Azure 媒體視訊縮圖**的詳細資訊，並示範如何搭配適用於 .NET 的媒體服務 SDK 來使用它。</span><span class="sxs-lookup"><span data-stu-id="0ef45-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="0ef45-111">限制</span><span class="sxs-lookup"><span data-stu-id="0ef45-111">Limitations</span></span>

<span data-ttu-id="0ef45-112">在某些情況下，如果您的視訊並未包含不同場景，則輸出將只是單一擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="0ef45-112">In some cases, if your video is not comprised of different scenes, the output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="0ef45-113">視訊摘要範例</span><span class="sxs-lookup"><span data-stu-id="0ef45-113">Video summary example</span></span>
<span data-ttu-id="0ef45-114">以下是 Azure 媒體視訊縮圖媒體處理器可以執行的一些範例：</span><span class="sxs-lookup"><span data-stu-id="0ef45-114">Here are some examples of what the Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="0ef45-115">原始視訊</span><span class="sxs-lookup"><span data-stu-id="0ef45-115">Original video</span></span>
[<span data-ttu-id="0ef45-116">原始視訊</span><span class="sxs-lookup"><span data-stu-id="0ef45-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="0ef45-117">視訊縮圖的結果</span><span class="sxs-lookup"><span data-stu-id="0ef45-117">Video thumbnail result</span></span>
[<span data-ttu-id="0ef45-118">視訊縮圖的結果</span><span class="sxs-lookup"><span data-stu-id="0ef45-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="0ef45-119">工作設定 (預設)</span><span class="sxs-lookup"><span data-stu-id="0ef45-119">Task configuration (preset)</span></span>
<span data-ttu-id="0ef45-120">以 **Azure 媒體視訊縮圖**建立視訊縮圖工作時，您必須指定設定預設值。</span><span class="sxs-lookup"><span data-stu-id="0ef45-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="0ef45-121">上述縮圖是使用下列基本 JSON 組態建立的範例︰</span><span class="sxs-lookup"><span data-stu-id="0ef45-121">The above thumbnail sample was created with the following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="0ef45-122">目前，您可以變更下列參數：</span><span class="sxs-lookup"><span data-stu-id="0ef45-122">Currently, you can change the following parameters:</span></span>

| <span data-ttu-id="0ef45-123">參數</span><span class="sxs-lookup"><span data-stu-id="0ef45-123">Param</span></span> | <span data-ttu-id="0ef45-124">說明</span><span class="sxs-lookup"><span data-stu-id="0ef45-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0ef45-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="0ef45-125">outputAudio</span></span> |<span data-ttu-id="0ef45-126">指定結果視訊是否要包含任何音訊。</span><span class="sxs-lookup"><span data-stu-id="0ef45-126">Specifies whether or not the resultant video contains any audio.</span></span> <br/><span data-ttu-id="0ef45-127">允許的值為 True 或 False。</span><span class="sxs-lookup"><span data-stu-id="0ef45-127">Allowed values are: True or False.</span></span> <span data-ttu-id="0ef45-128">預設值是 True。</span><span class="sxs-lookup"><span data-stu-id="0ef45-128">Default is True.</span></span> |
| <span data-ttu-id="0ef45-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="0ef45-129">fadeInFadeOut</span></span> |<span data-ttu-id="0ef45-130">指定不同的動作縮圖之間是否要使用淡化轉換。</span><span class="sxs-lookup"><span data-stu-id="0ef45-130">Specifies whether or not fade transitions are used between the separate motion thumbnails.</span></span>  <br/><span data-ttu-id="0ef45-131">允許的值為 True 或 False。</span><span class="sxs-lookup"><span data-stu-id="0ef45-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="0ef45-132">預設值是 True。</span><span class="sxs-lookup"><span data-stu-id="0ef45-132">Default is True.</span></span> |
| <span data-ttu-id="0ef45-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="0ef45-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="0ef45-134">整數，指定整個結果視訊的片長。</span><span class="sxs-lookup"><span data-stu-id="0ef45-134">Integer that specifies how long the entire resultant video shall be.</span></span>  <span data-ttu-id="0ef45-135">預設值取決於原始視訊的持續時間。</span><span class="sxs-lookup"><span data-stu-id="0ef45-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="0ef45-136">下表說明未使用 **maxMotionThumbnailInSecs** 時的預設持續時間。</span><span class="sxs-lookup"><span data-stu-id="0ef45-136">The following table describes the default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0ef45-137">視訊持續時間</span><span class="sxs-lookup"><span data-stu-id="0ef45-137">Video duration</span></span> |<span data-ttu-id="0ef45-138">d < 3 分鐘</span><span class="sxs-lookup"><span data-stu-id="0ef45-138">d < 3 min</span></span> |<span data-ttu-id="0ef45-139">3 分鐘 < d < 15 分鐘</span><span class="sxs-lookup"><span data-stu-id="0ef45-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="0ef45-140">縮圖持續時間</span><span class="sxs-lookup"><span data-stu-id="0ef45-140">Thumbnail duration</span></span> |<span data-ttu-id="0ef45-141">15 秒 (2-3 個場景)</span><span class="sxs-lookup"><span data-stu-id="0ef45-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="0ef45-142">30 秒 (3-5 個場景)</span><span class="sxs-lookup"><span data-stu-id="0ef45-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="0ef45-143">下列 JSON 會設定可用的參數。</span><span class="sxs-lookup"><span data-stu-id="0ef45-143">The following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="0ef45-144">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="0ef45-144">.NET sample code</span></span>

<span data-ttu-id="0ef45-145">下列程式將示範如何：</span><span class="sxs-lookup"><span data-stu-id="0ef45-145">The following program shows how to:</span></span>

1. <span data-ttu-id="0ef45-146">建立資產並將媒體檔案上傳到資產。</span><span class="sxs-lookup"><span data-stu-id="0ef45-146">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="0ef45-147">根據包含下列 JSON 預設值的組態檔案，建立執行視訊縮圖工作的工作。</span><span class="sxs-lookup"><span data-stu-id="0ef45-147">Creates a job with a video thumbnail task based on a configuration file that contains the following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="0ef45-148">下載輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="0ef45-148">Downloads the output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0ef45-149">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="0ef45-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0ef45-150">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="0ef45-150">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="0ef45-151">範例</span><span class="sxs-lookup"><span data-stu-id="0ef45-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
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

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


                // Run the thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference to Azure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
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
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="0ef45-152">視訊縮圖的輸出</span><span class="sxs-lookup"><span data-stu-id="0ef45-152">Video thumbnail output</span></span>
[<span data-ttu-id="0ef45-153">視訊縮圖的輸出</span><span class="sxs-lookup"><span data-stu-id="0ef45-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="0ef45-154">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="0ef45-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0ef45-155">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="0ef45-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="0ef45-156">相關連結</span><span class="sxs-lookup"><span data-stu-id="0ef45-156">Related links</span></span>
[<span data-ttu-id="0ef45-157">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="0ef45-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="0ef45-158">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="0ef45-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

