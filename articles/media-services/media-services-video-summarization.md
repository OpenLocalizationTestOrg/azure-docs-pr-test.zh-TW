---
title: "aaaUse Azure Media 視訊縮圖 tooCreate 視訊摘要 |Microsoft 文件"
description: "視訊摘要可以協助您建立的較長的視訊摘要會自動從 hello 來源視訊中選取感興趣的程式碼片段。 當您想 tooprovide 哪些 tooexpect 長的視訊中的快速概觀，這非常有用。"
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
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="c21c2-104">使用 Azure Media 視訊縮圖 tooCreate 視訊摘要</span><span class="sxs-lookup"><span data-stu-id="c21c2-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="c21c2-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c21c2-105">Overview</span></span>
<span data-ttu-id="c21c2-106">hello **Azure Media 視訊縮圖**媒體處理器 (MP) 可讓您 toocreate 的視訊，會很有用的 toocustomers 只想 toopreview 長的視訊摘要的摘要。</span><span class="sxs-lookup"><span data-stu-id="c21c2-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="c21c2-107">例如，客戶可能會想 toosee 簡短"摘要視訊"當他們將滑鼠停留在縮圖。</span><span class="sxs-lookup"><span data-stu-id="c21c2-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="c21c2-108">修改 hello 參數**Azure Media 視訊縮圖**透過組態預先設定，您可以使用 hello 管理組件的功能強大的次的偵測和串連技術 tooalgorithmically 產生描述性 subclip。</span><span class="sxs-lookup"><span data-stu-id="c21c2-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="c21c2-109">hello **Azure Media 視訊縮圖**MP 目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="c21c2-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="c21c2-110">本主題詳細說明有關**Azure Media 視訊縮圖**，並示範如何 toouse 使用 Media Services SDK for.NET。</span><span class="sxs-lookup"><span data-stu-id="c21c2-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="c21c2-111">限制</span><span class="sxs-lookup"><span data-stu-id="c21c2-111">Limitations</span></span>

<span data-ttu-id="c21c2-112">在某些情況下，如果您的視訊不組成不同場景，hello 輸出只會單一擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="c21c2-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="c21c2-113">視訊摘要範例</span><span class="sxs-lookup"><span data-stu-id="c21c2-113">Video summary example</span></span>
<span data-ttu-id="c21c2-114">以下是何種 hello Azure Media 視訊縮圖媒體處理器可以執行的一些範例：</span><span class="sxs-lookup"><span data-stu-id="c21c2-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="c21c2-115">原始視訊</span><span class="sxs-lookup"><span data-stu-id="c21c2-115">Original video</span></span>
[<span data-ttu-id="c21c2-116">原始視訊</span><span class="sxs-lookup"><span data-stu-id="c21c2-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="c21c2-117">視訊縮圖的結果</span><span class="sxs-lookup"><span data-stu-id="c21c2-117">Video thumbnail result</span></span>
[<span data-ttu-id="c21c2-118">視訊縮圖的結果</span><span class="sxs-lookup"><span data-stu-id="c21c2-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="c21c2-119">工作設定 (預設)</span><span class="sxs-lookup"><span data-stu-id="c21c2-119">Task configuration (preset)</span></span>
<span data-ttu-id="c21c2-120">以 **Azure 媒體視訊縮圖**建立視訊縮圖工作時，您必須指定設定預設值。</span><span class="sxs-lookup"><span data-stu-id="c21c2-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="c21c2-121">使用下列基本的 JSON 組態 hello 建立 hello 上述縮圖的範例：</span><span class="sxs-lookup"><span data-stu-id="c21c2-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="c21c2-122">目前，您可以變更下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="c21c2-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="c21c2-123">參數</span><span class="sxs-lookup"><span data-stu-id="c21c2-123">Param</span></span> | <span data-ttu-id="c21c2-124">說明</span><span class="sxs-lookup"><span data-stu-id="c21c2-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c21c2-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="c21c2-125">outputAudio</span></span> |<span data-ttu-id="c21c2-126">指定 hello 結果視訊包含任何音訊。</span><span class="sxs-lookup"><span data-stu-id="c21c2-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="c21c2-127">允許的值為 True 或 False。</span><span class="sxs-lookup"><span data-stu-id="c21c2-127">Allowed values are: True or False.</span></span> <span data-ttu-id="c21c2-128">預設值是 True。</span><span class="sxs-lookup"><span data-stu-id="c21c2-128">Default is True.</span></span> |
| <span data-ttu-id="c21c2-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="c21c2-129">fadeInFadeOut</span></span> |<span data-ttu-id="c21c2-130">指定是否會淡出轉換之間 hello 個別影片縮圖會使用。</span><span class="sxs-lookup"><span data-stu-id="c21c2-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="c21c2-131">允許的值為 True 或 False。</span><span class="sxs-lookup"><span data-stu-id="c21c2-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="c21c2-132">預設值是 True。</span><span class="sxs-lookup"><span data-stu-id="c21c2-132">Default is True.</span></span> |
| <span data-ttu-id="c21c2-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="c21c2-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="c21c2-134">應該指定多久 hello 整個結果視訊的整數。</span><span class="sxs-lookup"><span data-stu-id="c21c2-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="c21c2-135">預設值取決於原始視訊的持續時間。</span><span class="sxs-lookup"><span data-stu-id="c21c2-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="c21c2-136">hello 以下表格說明 hello 預設持續時間，當**maxMotionThumbnailInSecs**未使用。</span><span class="sxs-lookup"><span data-stu-id="c21c2-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c21c2-137">視訊持續時間</span><span class="sxs-lookup"><span data-stu-id="c21c2-137">Video duration</span></span> |<span data-ttu-id="c21c2-138">d < 3 分鐘</span><span class="sxs-lookup"><span data-stu-id="c21c2-138">d < 3 min</span></span> |<span data-ttu-id="c21c2-139">3 分鐘 < d < 15 分鐘</span><span class="sxs-lookup"><span data-stu-id="c21c2-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="c21c2-140">縮圖持續時間</span><span class="sxs-lookup"><span data-stu-id="c21c2-140">Thumbnail duration</span></span> |<span data-ttu-id="c21c2-141">15 秒 (2-3 個場景)</span><span class="sxs-lookup"><span data-stu-id="c21c2-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="c21c2-142">30 秒 (3-5 個場景)</span><span class="sxs-lookup"><span data-stu-id="c21c2-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="c21c2-143">hello 下列 JSON 設定可用的參數。</span><span class="sxs-lookup"><span data-stu-id="c21c2-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="c21c2-144">.NET 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="c21c2-144">.NET sample code</span></span>

<span data-ttu-id="c21c2-145">hello 以下程式顯示如何：</span><span class="sxs-lookup"><span data-stu-id="c21c2-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="c21c2-146">建立資產，並將媒體檔案上傳到 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="c21c2-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="c21c2-147">建立工作，以根據組態檔包含下列 json 的預設 hello 視訊縮圖工作。</span><span class="sxs-lookup"><span data-stu-id="c21c2-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="c21c2-148">下載 hello 輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="c21c2-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c21c2-149">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="c21c2-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c21c2-150">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="c21c2-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="c21c2-151">範例</span><span class="sxs-lookup"><span data-stu-id="c21c2-151">Example</span></span>

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
            // Read values from hello App.config file.
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


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
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

### <a name="video-thumbnail-output"></a><span data-ttu-id="c21c2-152">視訊縮圖的輸出</span><span class="sxs-lookup"><span data-stu-id="c21c2-152">Video thumbnail output</span></span>
[<span data-ttu-id="c21c2-153">視訊縮圖的輸出</span><span class="sxs-lookup"><span data-stu-id="c21c2-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="c21c2-154">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="c21c2-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c21c2-155">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c21c2-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c21c2-156">相關連結</span><span class="sxs-lookup"><span data-stu-id="c21c2-156">Related links</span></span>
[<span data-ttu-id="c21c2-157">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="c21c2-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c21c2-158">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="c21c2-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

