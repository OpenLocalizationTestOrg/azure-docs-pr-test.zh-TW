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
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a>使用 Azure Media 視訊縮圖 tooCreate 視訊摘要
## <a name="overview"></a>概觀
hello **Azure Media 視訊縮圖**媒體處理器 (MP) 可讓您 toocreate 的視訊，會很有用的 toocustomers 只想 toopreview 長的視訊摘要的摘要。 例如，客戶可能會想 toosee 簡短"摘要視訊"當他們將滑鼠停留在縮圖。 修改 hello 參數**Azure Media 視訊縮圖**透過組態預先設定，您可以使用 hello 管理組件的功能強大的次的偵測和串連技術 tooalgorithmically 產生描述性 subclip。  

hello **Azure Media 視訊縮圖**MP 目前為預覽狀態。

本主題詳細說明有關**Azure Media 視訊縮圖**，並示範如何 toouse 使用 Media Services SDK for.NET。

## <a name="limitations"></a>限制

在某些情況下，如果您的視訊不組成不同場景，hello 輸出只會單一擷取畫面。

## <a name="video-summary-example"></a>視訊摘要範例
以下是何種 hello Azure Media 視訊縮圖媒體處理器可以執行的一些範例：

### <a name="original-video"></a>原始視訊
[原始視訊](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a>視訊縮圖的結果
[視訊縮圖的結果](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a>工作設定 (預設)
以 **Azure 媒體視訊縮圖**建立視訊縮圖工作時，您必須指定設定預設值。 使用下列基本的 JSON 組態 hello 建立 hello 上述縮圖的範例：

    {"version":"1.0"}

目前，您可以變更下列參數的 hello:

| 參數 | 說明 |
| --- | --- |
| outputAudio |指定 hello 結果視訊包含任何音訊。 <br/>允許的值為 True 或 False。 預設值是 True。 |
| fadeInFadeOut |指定是否會淡出轉換之間 hello 個別影片縮圖會使用。  <br/>允許的值為 True 或 False。  預設值是 True。 |
| maxMotionThumbnailDurationInSecs |應該指定多久 hello 整個結果視訊的整數。  預設值取決於原始視訊的持續時間。 |

hello 以下表格說明 hello 預設持續時間，當**maxMotionThumbnailInSecs**未使用。

|  |  |  |
| --- | --- | --- | --- | --- |
| 視訊持續時間 |d < 3 分鐘 |3 分鐘 < d < 15 分鐘 |
| 縮圖持續時間 |15 秒 (2-3 個場景) |30 秒 (3-5 個場景) |

hello 下列 JSON 設定可用的參數。

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a>.NET 範例程式碼

hello 以下程式顯示如何：

1. 建立資產，並將媒體檔案上傳到 hello 資產。
2. 建立工作，以根據組態檔包含下列 json 的預設 hello 視訊縮圖工作。 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. 下載 hello 輸出檔案。 

#### <a name="create-and-configure-a-visual-studio-project"></a>建立和設定 Visual Studio 專案

設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。 

#### <a name="example"></a>範例

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

### <a name="video-thumbnail-output"></a>視訊縮圖的輸出
[視訊縮圖的輸出](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>相關連結
[Azure 媒體服務分析概觀](media-services-analytics-overview.md)

[Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

