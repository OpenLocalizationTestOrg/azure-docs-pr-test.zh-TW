---
title: "aaaUse Azure 媒體編碼器標準 tooauto-產生的位元速率階梯 |Microsoft 文件"
description: "本主題說明如何 toouse 媒體編碼器標準 (MES) tooauto-產生的位元速率階梯根據 hello 輸入的解析度和位元速率。 永遠不會超過 hello 輸入的解析度和位元速率。 比方說，如果 hello 輸入是 720p 3Mbps，輸出會在最佳情況下，保持 720p 及速率低於 3Mbps 會啟動。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>使用 Azure 媒體編碼器標準 tooauto-產生的位元速率階梯

## <a name="overview"></a>概觀

本主題說明如何 toouse 媒體編碼器標準 (MES) tooauto-產生根據 hello 輸入的解析度和位元速率位元速率階梯 （位元速率高解析度組）。 hello 自動產生的預設值絕對不會超過輸入 hello 解析度和位元速率。 比方說，如果 hello 輸入是 720p 3Mbps，輸出會在最佳情況下，保持 720p 及速率低於 3Mbps 會啟動。

### <a name="encoding-for-streaming-only"></a>只針對串流編碼

如果您的目的是 tooencode 您的來源視訊僅適用於資料流，則您應該使用 「 彈性資料流 」 的 hello 會預設建立編碼工作時。 當使用 hello**彈性資料流**預設，hello MES 編碼器會以聰明的方式限制在位元速率階梯。 不過，您將無法編碼的成本，因為 hello 服務會決定多少層 toouse 何種解析度可以 toocontrol hello。 您可以看到的輸出層 MES 所產生的結果以 hello 編碼範例**彈性資料流**預設 hello 本主題結尾處。 hello 輸出資產會包含 MP4 檔案，其中音訊和視訊不為交錯。

### <a name="encoding-for-streaming-and-progressive-download"></a>針對串流和漸進式下載編碼

如果您的目的是 tooencode tooproduce MP4 檔案進行漸進式下載，以及資料流，則您應該使用 「 內容自動調整多重位元速率 MP4"hello 來源視訊會預設建立編碼工作時。 當使用 hello**內容自動調整的多個位元速率 MP4**預設，hello MES 編碼器將會套用的 hello 相同編碼的邏輯與上面，但是 hello 輸出資產就會包含 MP4 檔案的音訊和視訊會交錯。 您可以使用其中一個 MP4 檔案 （例如，hello 最大位元速率版） 為漸進式下載檔案。

## <a id="encoding_with_dotnet"></a>使用媒體服務 .NET SDK 進行編碼

hello，下列程式碼範例會使用 Media Services.NET SDK tooperform hello 下列工作：

- 建立編碼工作。
- 取得參考 toohello 媒體編碼器標準編碼器。
- 加入的編碼工作 toohello 工作，並指定 toouse hello**彈性資料流**預設。 
- 建立會包含 hello 編碼資產的輸出資產。
- 加入事件處理常式 toocheck hello 工作進度。
- 送出 hello 作業。

#### <a name="create-and-configure-a-visual-studio-project"></a>建立和設定 Visual Studio 專案

設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。 

#### <a name="example"></a>範例

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
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

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
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

## <a id="output"></a>輸出

此區段會顯示三個範例的輸出層 MES 所產生的結果以 hello 編碼**彈性資料流**預設。 

### <a name="example-1"></a>範例 1
高度 "1080" 和畫面播放速率 "29.970" 的來源會產生 6 個視訊層︰

|層次|高度|寬度|位元速率 (kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>範例 2
高度 "720" 和畫面播放速率 "23.970" 的來源會產生 5 個視訊層︰

|層次|高度|寬度|位元速率 (kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>範例 3
高度 "360" 和畫面播放速率 "29.970" 的來源會產生 3 個視訊層︰

|層次|高度|寬度|位元速率 (kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[媒體服務編碼概觀](media-services-encode-asset.md)

