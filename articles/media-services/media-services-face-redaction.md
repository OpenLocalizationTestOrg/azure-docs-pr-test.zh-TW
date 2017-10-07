---
title: "使用 Azure 媒體分析 aaaRedact 字體 |Microsoft 文件"
description: "本主題示範使用 Azure media analytics tooredact 面臨的方式。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>使用 Azure 媒體分析修訂臉部
## <a name="overview"></a>概觀
**Azure 媒體 Redactor**是[Azure 媒體分析](media-services-analytics-overview.md)提供可擴充的字體 redaction hello 雲端中的媒體處理器 (MP)。 字體 redaction 可讓您 toomodify 順序 tooblur 表面選取個人視訊。 您可以在公用的安全性和新聞媒體案例 toouse hello 朝 redaction 服務。 幾分鐘的影片，其中包含多個字型都會小時 tooredact 以手動方式，但具有此服務的 hello 圖示 redaction 程序將需要幾個簡單的步驟。 如需詳細資訊，請參閱[此](https://azure.microsoft.com/blog/azure-media-redactor/)部落格。

本主題詳細說明有關**Azure 媒體 Redactor** ，並示範如何 toouse 使用 Media Services SDK for.NET。

hello **Azure 媒體 Redactor** MP 目前為預覽狀態。 在所有公開的 Azure 區域及美國政府和中國的數據中心皆有提供。 此預覽版本目前以免費方式提供。 

## <a name="face-redaction-modes"></a>臉部修訂模式
臉部 redaction 運作方式是在每個畫面格的視訊中偵測到字體及追蹤 hello 朝物件，兩者向前及向後的時間，使 hello 相同的個人可以模糊從以及其他角度。 hello 自動化的 redaction 程序是很複雜的並不一定會產生 100%的所需的輸出，因此媒體分析提供讓您透過數種方式 toomodify hello 最終輸出。

加法 tooa 完全自動模式中，在沒有兩段式工作流程可讓 hello 選取項目/還原-selection 的找到表面透過 Id 的清單。 此外，toomake 任意每框架調整 hello 管理組件會使用 JSON 格式的中繼資料檔案。 此工作流程分割成**分析**和**修訂**模式。 您可以結合在單一行程中一個作業，執行這兩項工作中的 hello 兩種模式這個模式稱為**組合**。

### <a name="combined-mode"></a>結合模式
這會自動產生修訂的 mp4，而不需要手動輸入。

| 階段 | 檔案名稱 | 注意事項 |
| --- | --- | --- |
| 輸入資產 |foo.bar |WMV、MOV 或 MP4 格式的視訊 |
| 輸入組態 |作業組態預設值 |{'version':'1.0', 'options': {'mode':'combined'}} |
| 輸出資產 |foo_redacted.mp4 |已套用模糊處理的視訊 |

#### <a name="input-example"></a>輸入範例︰
[請觀看這個影片](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>輸出範例：
[請觀看這個影片](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>分析模式
hello**分析**hello 兩段式工作流程的階段接受視訊輸入，並且會產生正面的位置，請在 JSON 檔案和 jpg 影像，每個偵測到的字體。

| 階段 | 檔案名稱 | 注意事項 |
| --- | --- | --- |
| 輸入資產 |foo.bar |WMV、MPV 或 MP4 格式的視訊 |
| 輸入組態 |作業組態預設值 |{'version':'1.0', 'options': {'mode':'analyze'}} |
| 輸出資產 |foo_annotations.json |JSON 格式的臉部位置註解資料。 這可以編輯 hello 使用者 toomodify hello 模糊週框方塊。 請參閱以下範例。 |
| 輸出資產 |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |每個裁剪的 jpg 偵測到的表面，其中 hello 數字表示 hello 面臨的 hello labelId |

#### <a name="output-example"></a>輸出範例：

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>修訂模式
hello hello 工作流程的第二個階段會較大的輸入必須結合成單一資產的數目。

這包括識別碼 tooblur、 hello 原始視訊，以及 hello 註解 JSON 的清單。 這個模式會使用 hello 註釋上 hello 輸入視訊模糊的 tooapply。

hello hello 分析階段的輸出不包括 hello 原始視訊。 hello 視訊需要 toobe 上傳到 hello hello Redact 模式工作的輸入資產，並選取為 hello 主要檔案。

| 階段 | 檔案名稱 | 注意事項 |
| --- | --- | --- |
| 輸入資產 |foo.bar |WMV、MPV 或 MP4 格式的視訊。 和步驟 1 相同的視訊。 |
| 輸入資產 |foo_annotations.json |來自第一個階段的註解中繼資料檔案，並帶有選擇性的修改。 |
| 輸入資產 |foo_IDList.txt (選擇性) |選擇性的新行分隔識別碼 tooredact 朝的清單。 如果保持空白，則會模糊所有臉部。 |
| 輸入組態 |作業組態預設值 |{'version':'1.0', 'options': {'mode':'redact'}} |
| 輸出資產 |foo_redacted.mp4 |已根據註解套用模糊處理的視訊 |

#### <a name="example-output"></a>範例輸出
這是一個識別碼為選取 IDList hello 輸出。

[請觀看這個影片](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

Example foo_IDList.txt
 
     1
     2
     3

## <a name="blur-types"></a>模糊類型

在 hello**組合**或**Redact**模式中，有 5 不同模糊模式，您可以選擇透過 hello JSON 輸入組態：**低**， **Med**，**高**，**偵錯**，和**黑色**。 預設會使用 [中]。

您可以尋找範例的 hello 模糊下列型別。

### <a name="example-json"></a>範例 JSON：

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>低

![低](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>中

![中](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>高

![高](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>偵錯

![偵錯](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>黑色

![黑色](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Hello 輸出 JSON 檔案的項目

hello Redaction 管理組件提供高精確度朝位置偵測和追蹤可以偵測出 too64 人力字體視訊畫面中。 人臉正面提供 hello 獲得最佳結果，同時端字體和小型的字體 (小於或等於 too24x24 像素為單位) 一大挑戰。

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>.NET 範例程式碼

hello 以下程式顯示如何：

1. 建立資產，並將媒體檔案上傳到 hello 資產。
2. 建立工作，以根據組態檔包含下列 json 的預設 hello 朝 redaction 工作。 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>後續步驟

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>相關連結
[Azure 媒體服務分析概觀](media-services-analytics-overview.md)

[Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

