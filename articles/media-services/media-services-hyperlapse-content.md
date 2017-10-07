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
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="fc45b-104">Hyperlapse Media 檔案與 Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="fc45b-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="fc45b-105">Azure Media Hyperlapse 是可以使用第一人稱視角或運動攝影機內容建立流暢縮時攝影影片的「媒體處理器 (MP)」。</span><span class="sxs-lookup"><span data-stu-id="fc45b-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="fc45b-106">太 hello 以雲端為基礎的同層級[Microsoft Research 桌面 Hyperlapse 專業版和 phone 基礎 Hyperlapse 行動](http://aka.ms/hyperlapse)，Azure Media Services 的 Microsoft Hyperlapse 利用 hello 大規模的 hello Azure 媒體服務媒體處理平台 toohorizontally 調整和平行處理大量 Hyperlapse 處理。</span><span class="sxs-lookup"><span data-stu-id="fc45b-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc45b-107">Microsoft Hyperlapse 是設計的 toowork 最佳的第一個人內容，以移動的相機。</span><span class="sxs-lookup"><span data-stu-id="fc45b-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="fc45b-108">雖然仍攝影機錄影畫面仍然可以正常運作，但是對於其他類型的內容無法保證 hello 效能和品質 hello Azure Media Hyperlapse 媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="fc45b-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="fc45b-109">深入了解 Azure Media Services 的 Microsoft Hyperlapse toolearn，請參閱部分的範例影片、 簽出 hello[簡介部落格文章](http://aka.ms/azurehyperlapseblog)從 hello 公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="fc45b-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="fc45b-110">作業會採用做為 Azure Media Hyperlapse 輸入以及組態檔，指定哪些視訊畫面應該時間屆滿和 toowhat 速度 MP4、 MOV、 或 WMV 資產檔案 （例如第一個 10000 框架在 2 倍）。</span><span class="sxs-lookup"><span data-stu-id="fc45b-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="fc45b-111">hello 輸出是 hello 輸入視訊穩定和時間屆滿轉譯。</span><span class="sxs-lookup"><span data-stu-id="fc45b-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="fc45b-112">如需最新 Azure Media Hyperlapse 更新 hello，請參閱[媒體服務部落格](https://azure.microsoft.com/blog/topics/media-services/)。</span><span class="sxs-lookup"><span data-stu-id="fc45b-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="fc45b-113">將資產進行 Hyperlapse 處理</span><span class="sxs-lookup"><span data-stu-id="fc45b-113">Hyperlapse an asset</span></span>
<span data-ttu-id="fc45b-114">首先您需要 tooupload 您所需的輸入的檔案 tooAzure Media Services。</span><span class="sxs-lookup"><span data-stu-id="fc45b-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="fc45b-115">深入了解 toolearn hello 概念上傳與管理內容，讀取 hello[內容管理的發行項](media-services-portal-vod-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fc45b-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="fc45b-116"><a id="configuration"></a>Hyperlapse 的預設組態</span><span class="sxs-lookup"><span data-stu-id="fc45b-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="fc45b-117">一旦您的內容在 Media Services 帳戶，您需要的 tooconstruct 預設您的設定。</span><span class="sxs-lookup"><span data-stu-id="fc45b-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="fc45b-118">下表中的 hello 說明 hello 使用者指定的欄位：</span><span class="sxs-lookup"><span data-stu-id="fc45b-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="fc45b-119">欄位</span><span class="sxs-lookup"><span data-stu-id="fc45b-119">Field</span></span> | <span data-ttu-id="fc45b-120">說明</span><span class="sxs-lookup"><span data-stu-id="fc45b-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fc45b-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="fc45b-121">StartFrame</span></span> |<span data-ttu-id="fc45b-122">hello 框架的 hello Microsoft Hyperlapse 時應該開始進行處理。</span><span class="sxs-lookup"><span data-stu-id="fc45b-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="fc45b-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="fc45b-123">NumFrames</span></span> |<span data-ttu-id="fc45b-124">框架 tooprocess 的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="fc45b-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="fc45b-125">速度</span><span class="sxs-lookup"><span data-stu-id="fc45b-125">Speed</span></span> |<span data-ttu-id="fc45b-126">使用哪些 toospeed 向上 hello 輸入視訊的 hello 因數。</span><span class="sxs-lookup"><span data-stu-id="fc45b-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="fc45b-127">hello 以下是符合 XML 和 JSON 組態檔的範例：</span><span class="sxs-lookup"><span data-stu-id="fc45b-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="fc45b-128">**XML 預設：**</span><span class="sxs-lookup"><span data-stu-id="fc45b-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="fc45b-129">**JSON 預設：**</span><span class="sxs-lookup"><span data-stu-id="fc45b-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="fc45b-130"><a id="sample_code"></a>Microsoft Hyperlapse 以 hello AMS.NET SDK</span><span class="sxs-lookup"><span data-stu-id="fc45b-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="fc45b-131">hello 下列方法上傳媒體檔案儲存為資產，並建立工作以 hello Azure Media Hyperlapse 媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="fc45b-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="fc45b-132">您應該已經 CloudMediaContext 此程式碼 toowork hello 名稱 [內容] 的範圍內。</span><span class="sxs-lookup"><span data-stu-id="fc45b-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="fc45b-133">深入了解此，讀取 hello toolearn[內容管理的發行項](media-services-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fc45b-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="fc45b-134">hello 字串引數"hyperConfig 」 是 JSON 或 XML，如上面所述的一致組態預先設定的預期的 toobe。</span><span class="sxs-lookup"><span data-stu-id="fc45b-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
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

### <span data-ttu-id="fc45b-135"><a id="file_types"></a>支援的檔案類型</span><span class="sxs-lookup"><span data-stu-id="fc45b-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="fc45b-136">MP4</span><span class="sxs-lookup"><span data-stu-id="fc45b-136">MP4</span></span>
* <span data-ttu-id="fc45b-137">MOV</span><span class="sxs-lookup"><span data-stu-id="fc45b-137">MOV</span></span>
* <span data-ttu-id="fc45b-138">WMV</span><span class="sxs-lookup"><span data-stu-id="fc45b-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="fc45b-139">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="fc45b-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fc45b-140">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="fc45b-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="fc45b-141">相關連結</span><span class="sxs-lookup"><span data-stu-id="fc45b-141">Related links</span></span>
[<span data-ttu-id="fc45b-142">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="fc45b-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="fc45b-143">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="fc45b-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

