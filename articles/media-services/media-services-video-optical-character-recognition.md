---
title: "Azure 媒體分析 ocr aaaDigitize 文字 |Microsoft 文件"
description: "Azure 媒體分析 OCR （光學字元辨識） 可讓您 tooconvert 文字內容中的視訊檔案為可編輯，搜尋數位文字。  這可讓您 tooautomate hello 擷取有意義的中繼資料從您的媒體 hello 視訊訊號。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>視訊檔案中，使用 Azure 媒體分析 tooconvert 文字內容，到數位的文字
## <a name="overview"></a>概觀
如果您需要從視訊檔案的內容 tooextract 文字，並產生可編輯的可搜尋數位文字，您應該使用 Azure 媒體分析 OCR （光學字元辨識）。 此 Azure 媒體處理器會偵測視訊檔案的文字內容並產生文字檔案，以供您使用。 OCR 可讓您 tooautomate hello 的有意義的中繼資料中擷取媒體的 hello 視訊訊號。

搭配使用搜尋引擎，您可以輕鬆地索引時您的媒體依文字、 與增強 hello 發現您的內容。 這在具有大量文字的視訊 (例如視訊錄製或投影片簡報的螢幕擷取) 中非常實用。 hello Azure OCR 媒體處理器最適合用於數位文字。

hello **Azure 媒體 OCR**媒體處理器目前為預覽狀態。

本主題詳細說明有關**Azure 媒體 OCR** ，並示範如何 toouse 使用 Media Services SDK for.NET。 如需詳細資訊和範例，請參閱 [這篇部落格](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/)。

## <a name="ocr-input-files"></a>OCR 輸入檔案
影片檔案。 目前支援下列格式的 hello: MP4、 MOV、 和 WMV。

## <a name="task-configuration"></a>工作組態
工作組態 (預設)。 使用 **Azure 媒體 OCR** 建立工作時，您必須使用 JSON 或 XML 來指定組態預設。 

>[!NOTE]
>hello OCR 引擎才會與最小 40 像素 toomaximum 32000 像素的影像區域，做為有效的輸入，在這兩個高度/寬度。
>

### <a name="attribute-descriptions"></a>屬性描述
| 屬性名稱 | 說明 |
| --- | --- |
|AdvancedOutput| 如果您設定 AdvancedOutput tootrue，hello JSON 輸出會包含位置資料的每個單字 （在加法 toophrases 和區域）。 如果您不想 toosee 這些詳細資料，設定 hello 旗標 toofalse。 hello 預設值為 false。 如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/)。|
| 語言 |（選擇性） 描述文字的哪些 toolook hello 語言。 Hello 下列其中一種： 自動偵測 （預設值）、 阿拉伯文、 ChineseSimplified、 ChineseTraditional、 捷克文丹麥文、 荷蘭文、 英文、 芬蘭文、 法文、 德文、 希臘文、 匈牙利文、 義大利文、 日文、 韓文、 挪威文、 波蘭文、 葡萄牙文、 羅馬尼亞文、 俄文SerbianCyrillic、 SerbianLatin、 斯洛伐克文、 西班牙文、 瑞典文、 土耳其文。 |
| TextOrientation |（選擇性） 描述 hello 哪些 toolook 文字方向。  「 左 」 表示 hello 的所有字母上方所指朝向 hello 左邊。  預設文字 (像是可在書本中找到的文字) 的方向為 "Up"。  Hello 下列其中一種： 自動偵測 （預設值），最多、 右邊、 向下、 左。 |
| TimeInterval |（選擇性） 描述 hello 取樣率。  預設值為每 1/2 秒。<br/>JSON 格式 – HH:mm:ss.SSS (預設值 00:00:00.500)<br/>XML 格式 – W3C XSD 持續時間基本型別 (預設值 PT0.5) |
| DetectRegions |（選擇性）指定區域內 hello 視訊畫面格 toodetect 文字 DetectRegion 物件的陣列。<br/>DetectRegion 物件是由下列四個整數值的 hello:<br/>左 – 從 hello 左邊界的像素為單位<br/>Top – 從 hello 的上邊界的像素為單位<br/>寬度-像素為單位的 hello 區域的寬度<br/>高度-像素為單位的 hello 區域的高度 |

#### <a name="json-preset-example"></a>JSON 預設範例

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>XML 預設範例
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>OCR 輸出檔案
hello OCR 媒體處理器的 hello 輸出是 JSON 檔案。

### <a name="elements-of-hello-output-json-file"></a>Hello 輸出 JSON 檔案的項目
hello 視訊 OCR 輸出提供在視訊中找到的 hello 字元時間分割資料。  您可以使用的語言或 toohone 中方向等屬性完全 hello 字，您有興趣分析。 

hello 輸出內容包含下列屬性的 hello:

| 元素 | 說明 |
| --- | --- |
| 時幅 |hello 視訊的每秒 「 滴答 」 |
| Offset |時間戳記的時間位移。 在版本 1.0 的影片 API 中，這永遠會是 0。 |
| 畫面播放速率 |每秒的 hello 視訊畫面格 |
| width |hello 視訊像素為單位的寬度 |
| height |hello 視訊像素為單位的高度 |
| 片段 |以時間為基礎的中繼資料被截斷成哪一個 hello 視訊的區塊的陣列 |
| start |片段的開始時間 (以「刻度」為單位) |
| duration |片段的長度 (以「刻度」為單位) |
| interval |每個事件內 hello 給定片段的間隔 |
| 活動 |包含區域的陣列 |
| region |物件，代表偵測到的單字或片語 |
| 語言 |區域內偵測到的 hello 文字的語言 |
| orientation |區域內偵測到的 hello 文字方向 |
| lines |區域內偵測到的文字行陣列 |
| 文字 |實際的 hello 文字 |

### <a name="json-output-example"></a>JSON 輸出範例
hello 下列輸出範例包含 hello 一般視訊資訊和數個視訊片段。 在每個視訊片段中，它會包含每個偵測到的 OCR 管理組件以 hello 語言和其文字方向的區域。 hello 區域也包含 hello 一行文字、 與 hello 行的位置，這行中的每個 word 資訊 （word 內容、 位置和信心） 這個區域中的每個字行。 hello 以下是範例，並使某些註解內嵌。

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>.NET 範例程式碼

hello 以下程式顯示如何：

1. 建立資產，並將媒體檔案上傳到 hello 資產。
2. 使用 OCR 設定/預設檔案建立作業。
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

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

