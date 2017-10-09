---
title: "aaaDetect 表面和使用 Azure 媒體分析情緒 |Microsoft 文件"
description: "本主題示範如何 toodetect 正面會面對和情緒使用 Azure 媒體分析。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a>使用 Azure 媒體分析偵測臉部和情緒
## <a name="overview"></a>概觀
hello **Azure 媒體正面偵測器**媒體處理器 (MP) 可讓您 toocount、 軌跡的移動，即使量測計的對象參與以及透過臉部表情的反應。 此服務包含兩個功能： 

* **臉部偵測**
  
    臉部偵測能夠找出並追蹤影片中的臉部。 多個字型可以偵測到且後續追蹤與 hello 時間和位置傳回中繼資料中的 JSON 檔案中，移動。 在追蹤時，它就會嘗試 toogive 一致的識別碼 toohello 相同面臨 hello 人員四處移動在畫面上，即使它們受到阻擋或簡短保留 hello 框架時。
  
  > [!NOTE]
  > 此服務並不會執行臉部辨識。 個人離開 hello 框架，或會變成受到阻擋的時間太長時，會指定新的識別碼，就會傳回。
  > 
  > 
* **情緒偵測**
  
    情緒偵測作業屬於選擇性元件的 hello 分析多個情感屬性傳回 hello 字體偵測到，包括快樂、 sadness、 擔心、 anger，以及更多的臉偵測媒體處理器。 

hello **Azure 媒體正面偵測器**MP 目前為預覽狀態。

本主題詳細說明有關**Azure 媒體正面偵測器**，並示範如何 toouse 使用 Media Services SDK for.NET。

## <a name="face-detector-input-files"></a>臉部偵測器輸入檔案
影片檔案。 目前支援下列格式的 hello: MP4、 MOV、 和 WMV。

## <a name="face-detector-output-files"></a>臉部偵測器輸出檔案
hello 朝偵測和追蹤 API 可提供高精確度朝位置偵測和追蹤可以偵測向上 too64 人力字體視訊中。 人臉正面提供 hello 獲得最佳結果，同時端字體和小型的字體 (小於或等於 too24x24 像素為單位) 可能不準確。

hello 偵測和追蹤字體傳回座標為 （左側、 頂端、 寬度和高度） 指出 hello 的表面，以像素的 hello 映像中的位置，以及一個朝識別碼數字，指出 hello 的個別的追蹤。 字體識別碼時情況下的很容易出錯 tooreset hello 人臉正面遺失或重疊在 hello 框架內，導致指派多個識別碼的某些個人。

## <a id="output_elements"></a>Hello 輸出 JSON 檔案的項目

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

正面偵測器會使用的片段 （hello 中繼資料可以會中斷以時間為基礎的區塊，而您可以下載只配備），以及分割技術 （其中 hello 事件會分解以防它們得太大）。 一些簡單的計算，可協助您將 hello 資料轉換。 例如，如果事件是從 6300 (刻度) 開始，並擁有 2997 (刻度/每秒) 的時幅，以及 29.97 (畫面/每秒) 的畫面播放速率，則：

* 開始/時幅 = 2.1 秒
* 秒數 x 畫面播放速率 = 63 格畫面

## <a name="face-detection-input-and-output-example"></a>臉部偵測輸入和輸出範例
### <a name="input-video"></a>輸入影片
[輸入影片](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>工作設定 (預設)
以 **Azure 媒體臉部偵測器**建立工作時，您必須指定設定預設值。 下列組態的預設 hello 只適用於臉偵測。

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a>屬性描述
| 屬性名稱 | 說明 |
| --- | --- |
| Mode |Fast：較快的處理速度，但較不精確 (預設)。|

### <a name="json-output"></a>JSON 輸出
下列範例的 JSON 輸出的 hello 已遭截斷。

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a>情緒偵測輸入和輸出範例
### <a name="input-video"></a>輸入影片
[輸入影片](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>工作設定 (預設)
以 **Azure 媒體臉部偵測器**建立工作時，您必須指定設定預設值。 下列組態的預設 hello 指定的 toocreate JSON 根據 hello 情緒偵測。

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a>屬性描述
| 屬性名稱 | 說明 |
| --- | --- |
| 模式 |Faces：僅臉部偵測。<br/>PerFaceEmotion：將每個臉部偵測的情緒單獨傳回。<br/>AggregateEmotion：傳回該畫面中所有臉部的平均情緒值。 |
| AggregateEmotionWindowMs |在已選取 AggregateEmotion 模式時使用。 指定每個彙總的結果視訊使用 tooproduce hello 長度，以毫秒為單位。 |
| AggregateEmotionIntervalMs |在已選取 AggregateEmotion 模式時使用。 指定哪些頻率 tooproduce 彙總結果。 |

#### <a name="aggregate-defaults"></a>彙總預設值
以下被建議的 hello 彙總視窗和間隔設定的值。 AggregateEmotionWindowMs 應該超過 AggregateEmotionIntervalMs。

|| 預設 | 最小 | 最大 |
|--- | --- | --- | --- |
| AggregateEmotionWindowMs |0.5 |2 |0.25|
| AggregateEmotionIntervalMs |0.5 |1 |0.25|

### <a name="json-output"></a>JSON 輸出
彙總情緒的 JSON 輸出 (已截斷)：

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a>限制
* 支援的 hello 輸入視訊格式包括 MP4、 MOV、 和 WMV。
* hello 偵測臉大小範圍為 24 x 24 too2048x2048 像素。 將不會偵測 hello 字體超出此範圍。
* 每個視訊，hello 字體傳回的數目上限為 64。
* 因為 tootechnical 挑戰; 可能無法偵測某些字體例如非常大的正面角度 （h e a d-碰到） 和大型阻擋。 人臉和正面附近的字體有 hello 最佳的結果。

## <a name="net-sample-code"></a>.NET 範例程式碼

hello 以下程式顯示如何：

1. 建立資產，並將媒體檔案上傳到 hello 資產。
2. 建立具有工作臉偵測工作，根據包含 hello 下列 json 的預設組態檔。 
   
        {
            "version": "1.0"
        }
3. 下載 hello 輸出 JSON 檔案。 

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

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

[Azure 媒體分析示範](http://amslabs.azurewebsites.net/demos/Analytics.html)

