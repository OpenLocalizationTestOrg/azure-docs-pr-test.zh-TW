---
title: "使用 Azure Media Hyperlapse 的媒體檔案 aaaHyperlapse |Microsoft 文件"
description: "Azure Media Hyperlapse 能夠利用第一人稱視角或運動攝影的內容，來建立流暢的縮時影片。 本主題說明如何 toouse Media Indexer。"
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Hyperlapse Media 檔案與 Azure Media Hyperlapse
Azure Media Hyperlapse 是可以使用第一人稱視角或運動攝影機內容建立流暢縮時攝影影片的「媒體處理器 (MP)」。  太 hello 以雲端為基礎的同層級[Microsoft Research 桌面 Hyperlapse 專業版和 phone 基礎 Hyperlapse 行動](http://aka.ms/hyperlapse)，Azure Media Services 的 Microsoft Hyperlapse 利用 hello 大規模的 hello Azure 媒體服務媒體處理平台 toohorizontally 調整和平行處理大量 Hyperlapse 處理。

> [!IMPORTANT]
> Microsoft Hyperlapse 是設計的 toowork 最佳的第一個人內容，以移動的相機。  雖然仍攝影機錄影畫面仍然可以正常運作，但是對於其他類型的內容無法保證 hello 效能和品質 hello Azure Media Hyperlapse 媒體處理器。  深入了解 Azure Media Services 的 Microsoft Hyperlapse toolearn，請參閱部分的範例影片、 簽出 hello[簡介部落格文章](http://aka.ms/azurehyperlapseblog)從 hello 公開預覽狀態。
> 
> 

作業會採用做為 Azure Media Hyperlapse 輸入以及組態檔，指定哪些視訊畫面應該時間屆滿和 toowhat 速度 MP4、 MOV、 或 WMV 資產檔案 （例如第一個 10000 框架在 2 倍）。  hello 輸出是 hello 輸入視訊穩定和時間屆滿轉譯。

如需最新 Azure Media Hyperlapse 更新 hello，請參閱[媒體服務部落格](https://azure.microsoft.com/blog/topics/media-services/)。

## <a name="hyperlapse-an-asset"></a>將資產進行 Hyperlapse 處理
首先您需要 tooupload 您所需的輸入的檔案 tooAzure Media Services。  深入了解 toolearn hello 概念上傳與管理內容，讀取 hello[內容管理的發行項](media-services-portal-vod-get-started.md)。

### <a id="configuration"></a>Hyperlapse 的預設組態
一旦您的內容在 Media Services 帳戶，您需要的 tooconstruct 預設您的設定。  下表中的 hello 說明 hello 使用者指定的欄位：

| 欄位 | 說明 |
| --- | --- |
| StartFrame |hello 框架的 hello Microsoft Hyperlapse 時應該開始進行處理。 |
| NumFrames |框架 tooprocess 的 hello 數目 |
| 速度 |使用哪些 toospeed 向上 hello 輸入視訊的 hello 因數。 |

hello 以下是符合 XML 和 JSON 組態檔的範例：

**XML 預設：**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**JSON 預設：**

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <a id="sample_code"></a>Microsoft Hyperlapse 以 hello AMS.NET SDK
hello 下列方法上傳媒體檔案儲存為資產，並建立工作以 hello Azure Media Hyperlapse 媒體處理器。

> [!NOTE]
> 您應該已經 CloudMediaContext 此程式碼 toowork hello 名稱 [內容] 的範圍內。  深入了解此，讀取 hello toolearn[內容管理的發行項](media-services-dotnet-get-started.md)。
> 
> [!NOTE]
> hello 字串引數"hyperConfig 」 是 JSON 或 XML，如上面所述的一致組態預先設定的預期的 toobe。
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
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
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <a id="file_types"></a>支援的檔案類型
* MP4
* MOV
* WMV

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>相關連結
[Azure 媒體服務分析概觀](media-services-analytics-overview.md)

[Azure 媒體分析示範](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

