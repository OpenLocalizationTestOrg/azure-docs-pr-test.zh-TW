---
title: "使用 Azure 媒體分析 aaaDetect 動作 |Microsoft 文件"
description: "hello Azure 媒體動作偵測器媒體處理器 (MP) 可讓您 tooefficiently 識別有興趣，否則冗長且較為簡單的視訊中的章節。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>使用 Azure 媒體分析偵測動作
## <a name="overview"></a>概觀
hello **Azure 媒體動作偵測器**媒體處理器 (MP) 可讓您 tooefficiently 識別有興趣，否則冗長且較為簡單的視訊中的章節。 影片偵測可用靜態攝影機錄影畫面 tooidentify 部分的 hello 視訊動作發生的位置。 它會產生包含時間戳記與 hello 週框 hello 事件發生的位置 （地區） 的中繼資料的 JSON 檔案。

針對安全性視訊摘要，此技術是無法 toocategorize 移動到相關的事件，例如陰影和光源處理變更的誤判。 可以讓您從相機摘要 toogenerate 安全性警示，沒有與無止盡不相關的事件，同時會無法 tooextract 分鐘的時間很長的監視視訊從感興趣的垃圾信件。

hello **Azure 媒體動作偵測器**MP 目前為預覽狀態。

本主題詳細說明有關**Azure 媒體動作偵測器**，並示範如何 toouse 使用 Media Services SDK for.NET

## <a name="motion-detector-input-files"></a>動作偵測器輸入檔案
影片檔案。 目前支援下列格式的 hello: MP4、 MOV、 和 WMV。

## <a name="task-configuration-preset"></a>工作組態 (預設)
以 **Azure 媒體動作偵測器**建立工作時，您必須指定設定預設值。 

### <a name="parameters"></a>參數
您可以使用下列參數的 hello:

| 名稱 | 選項 | 說明 | 預設值 |
| --- | --- | --- | --- |
| sensitivityLevel |字串：'low'、'medium'、'high' |在哪些動作會報告設定 hello 敏感度層級。 調整這個 tooadjust 數量誤判。 |'medium' |
| frameSamplingValue |正整數 |在哪些演算法回合設定 hello 頻率。 1 等於每個畫面，2 表示每 2 個畫面，依此類推。 |1 |
| detectLightChange |布林值：'true'、'false' |設定是否 hello 結果中會報告淺的變更 |'False' |
| mergeTimeThreshold |Xs-time: Hh:mm:ss<br/>範例：00:00:03 |指定 hello 影片事件結合並回報為 1 2 個事件之間的時間間隔。 |00:00:00 |
| detectionZones |偵測區域的陣列︰<br/>- 偵測區域是 3 個或更多個點的陣列<br/>點是 x 和 y 座標，從 0 too1。 |描述使用多邊形偵測區域 toobe hello 清單。<br/>會使用 hello 區域報告結果，做為識別碼，以第一個是 'id' hello: 0 |其中涵蓋了 hello 整個框架的單一區域。 |

### <a name="json-example"></a>JSON 範例
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>動作偵測器輸出檔案
影片偵測作業會傳回 JSON 檔案中會描述 hello 影片警示和其類別，在 hello 視訊 hello 輸出資產。 hello 檔案會包含有關 hello 時間和持續時間的移動 hello 視訊中偵測到的資訊。

hello 影片偵測器 API 提供指標，當物件在影片中有固定的背景影像 （例如監視視訊）。 hello 動作偵測器是定型的 tooreduce false 警示，例如光源和陰影變更。 目前限制的 hello 演算法包括晚上願景影片、 半透明效果的物件和小型物件。

### <a id="output_elements"></a>Hello 輸出 JSON 檔案的項目
> [!NOTE]
> 在 hello 最新版本中，hello 輸出 JSON 格式已變更，可能會對某些客戶代表是重大變更。
> 
> 

hello 下表說明 hello 輸出 JSON 檔案的項目。

| 元素 | 說明 |
| --- | --- |
| 版本 |這是指 toohello 版的 hello 視訊應用程式開發介面。 hello 目前版本為 2。 |
| 時幅 |「 滴答 」 每秒的 hello 視訊。 |
| Offset |hello 「 滴答 」 中的時間戳記的時間位移。 在版本 1.0 的影片 API 中，這永遠會是 0。 在我們於未來將支援的案例中，此值可能會變更。 |
| 畫面播放速率 |每秒的 hello 視訊畫面。 |
| 寬度，高度 |是指 toohello 寬度和高度 hello 視訊像素為單位。 |
| Start |hello 開始 「 滴答 」 中的時間戳記。 |
| Duration |hello 事件，請在 「 滴答 」 hello 長度。 |
| 間隔 |hello 間隔 hello 事件，請在 「 滴答 」 中的每個項目。 |
| 事件 |每個事件片段包含該持續時間內偵測到的 hello 影片。 |
| 類型 |在 hello 目前版本中，這一律是 '2' 的泛型影片。 此標籤會提供在未來版本中視訊 Api hello 彈性 toocategorize 影片。 |
| RegionID |如前文所述，這在此版本中將永遠會是 0。 此標籤可讓視訊 API hello 彈性 toofind 動作的未來版本中的各個區域。 |
| 區域 |是指 toohello 區域在視訊中的關心影片。 <br/><br/>-「 識別碼 」 代表 hello 區 – 在此版本中都只有一個，識別碼為 0。 <br/>-「 類型 」 代表 hello 圖形的 hello 關心影片的區域。 目前支援「矩形」和「多邊形」。<br/> 如果您指定 「 矩形 」，hello 區具有維度的 x、 Y、 寬度和高度。 hello X 和 Y 座標代表 hello 左上 XY 座標的正規化的小數位數為 0.0 too1.0 中的 hello 區域。 hello 寬度和高度代表 hello 正規化的小數位數為 0.0 too1.0 中的 hello 區域大小。 在 hello 目前版本中，X、 Y、 寬度和高度都一律固定為 0，0，1，1。 <br/>如果您指定 「 多邊形 」，hello 地區會有維度以點為單位。 <br/> |
| 片段 |到不同的區段，稱為片段 hello 中繼資料區塊上處理。 每個片段皆包含開始、持續時間、間隔數字及事件。 沒有事件的片段，代表在該片段的開始時間和持續時間之間沒有偵測到任何動作。 |
| 括號 [] |每個括號表示 hello 事件中的一個時間間隔。 如果間隔顯示空白括號，便代表沒有偵測到動作。 |
| 位置 |這個新的項目，[事件] 底下列出 hello hello 動作發生所在的位置。 這是比 hello 偵測區域更明確。 |

hello 以下是 JSON 輸出範例

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>限制
* 支援的 hello 輸入視訊格式包括 MP4、 MOV、 和 WMV。
* 動作偵測已針對固定背景的影片最佳化。 hello 演算法著重於減少錯誤的警示，例如光源變更和陰影。
* 某些影片可能無法偵測 tootechnical 挑戰; 到期例如晚上願景影片、 半透明效果的物件和小型物件。

## <a name="net-sample-code"></a>.NET 範例程式碼

hello 以下程式顯示如何：

1. 建立資產，並將媒體檔案上傳到 hello 資產。
2. 建立具有工作影片的影片偵測工作，根據包含 hello 下列 json 的預設組態檔。 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
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

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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
[Azure 媒體服務動作偵測器部落格](https://azure.microsoft.com/blog/motion-detector-update/)

[Azure 媒體服務分析概觀](media-services-analytics-overview.md)

[Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

