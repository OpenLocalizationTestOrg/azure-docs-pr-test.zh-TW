---
title: "媒體檔案，使用 Azure Media Indexer 2 預覽 aaaIndexing |Microsoft 文件"
description: "Azure Media Indexer 可讓您的媒體檔案可搜尋的 toomake 內容和 toogenerate 全文檢索文字記錄的關閉字幕和關鍵字。 本主題顯示如何 toouse Media Indexer 2 預覽。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>使用 Azure Media Indexer 2 Preview 編製媒體檔案索引
## <a name="overview"></a>概觀
hello **Azure Media Indexer 2 預覽**媒體處理器 (MP) 可讓您 toomake 媒體檔案和內容可搜尋，以及產生已關閉隱藏式輔助字幕追蹤。 比較的 toohello 舊版[Azure Media Indexer](media-services-index-content.md)， **Azure Media Indexer 2 預覽**執行更快索引，並提供更廣泛的語言支援。 支援的語言包括英文、西班牙文、法文、德文、義大利文、中文 (國語、簡體)、葡萄牙文、阿拉伯文和日文。

hello **Azure Media Indexer 2 預覽**MP 目前為預覽狀態。

本主題說明如何 toocreate 編製索引作業與**Azure Media Indexer 2 預覽**。

> [!NOTE]
> hello 下列考量適用於：
> 
> Azure China 和 Azure Government 不支援 Indexer 2。
> 
> 建立索引時的內容，請確定 toouse （沒有背景音樂、 噪音、 效果或麥克風雜音） 語音非常清楚的媒體檔案。 適當內容的一些範例有：錄製的會議、演講或簡報。 hello 下列內容可能不適合編製索引： 電影、 電視節目，任何具有混音效果與音效，錄製不佳的內容有背景噪音 （雜音））。
> 
> 

本主題詳細說明有關**Azure Media Indexer 2 預覽**，並示範如何 toouse 使用 Media Services SDK for.NET

## <a name="input-and-output-files"></a>輸入和輸出檔案
### <a name="input-files"></a>輸入檔案
音訊或視訊檔案

### <a name="output-files"></a>輸出檔案
索引作業可以產生隱藏式的字幕檔案在 hello 下列格式：  

* **SAMI**
* **TTML**
* **WebVTT**

已關閉的字幕 (CC) 檔案，這些格式可以是使用的 toomake 音訊和視訊檔案存取 toopeople 聽覺時。

## <a name="task-configuration-preset"></a>工作組態 (預設)
以 **Azure 媒體索引器 2 預覽**建立索引工作時，您必須指定設定預設值。

hello 下列 JSON 設定可用的參數。

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>支援的語言
Azure Media Indexer 2 預覽支援語音轉文字 hello （時在 hello 工作組態中，使用 4 個字元的程式碼以括號指定 hello 語言名稱，如下所示），下列語言：

* 英文 [EnUs]
* 西班牙文 [EsEs]
* 中文 (國語、簡體) [ZhCn]
* 法文 [FrFr]
* 德文 [DeDe]
* 義大利文 [ItIt]
* 葡萄牙文 [PtBr]
* 阿拉伯文 (埃及) [ArEg]
* 日文 [JaJp]
* 俄文 [RuRu]
* 英式英文 [EnGb]
* 墨西哥西班牙文 [EsMx] 

## <a name="supported-file-types"></a>支援的檔案類型

如需支援的檔案類型的資訊，請參閱 hello[支援的轉碼器/格式](media-services-media-encoder-standard-formats.md#input-containerfile-formats)> 一節。

## <a name="net-sample-code"></a>.NET 範例程式碼

hello 以下程式顯示如何：

1. 建立資產，並將媒體檔案上傳到 hello 資產。
2. 使用包含 hello 下列 json 的預設組態檔為基礎的索引工作建立工作。
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
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

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>相關連結
[Azure 媒體服務分析概觀](media-services-analytics-overview.md)

[Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

