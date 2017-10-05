---
title: "Hyperlapse Media 檔案與 Azure 媒體超縮時攝影 | Microsoft Docs"
description: "Azure Media Hyperlapse 能夠利用第一人稱視角或運動攝影的內容，來建立流暢的縮時影片。 本主題說明如何使用 Media Indexer。"
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
ms.openlocfilehash: 02f634c2af04b6b372642ab0e6a17a5d29f16450
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="ddc4a-104">Hyperlapse Media 檔案與 Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="ddc4a-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="ddc4a-105">Azure Media Hyperlapse 是可以使用第一人稱視角或運動攝影機內容建立流暢縮時攝影影片的「媒體處理器 (MP)」。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="ddc4a-106">Azure 媒體服務的雲端型 Microsoft Hyperlapse 與 [Microsoft Research 的桌面 Hyperlapse Pro 和手機型 Hyperlapse Mobile](http://aka.ms/hyperlapse)相似，它運用大規模的 Azure 媒體服務媒體處理平台來水平調整，並平行化大量的 Hyperlapse 處理。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddc4a-107">Microsoft Hyperlapse 是專門使用移動中攝影機拍攝第一人稱視角內容而設計。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span></span>  <span data-ttu-id="ddc4a-108">雖然攝影機位置固定的內容也可以運作，但 Azure 媒體 Hyperlapse 媒體處理器無法保證其他類型內容的效能及品質。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="ddc4a-109">若要深入了解 Azure 媒體服務的 Microsoft Hyperlapse 並觀賞一些範例影片，請查看公開預覽的 [簡介部落格文章](http://aka.ms/azurehyperlapseblog) 。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span></span>
> 
> 

<span data-ttu-id="ddc4a-110">Azure 媒體 Hyperlapse 工作接受輸入 MP4、MOV 或 WMV 資產檔案連同組態檔，以指定影片中要縮時的畫面及其速度 (例如前 10,000 個畫面速度為 2x)。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="ddc4a-111">輸出是輸入影片經過穩定和縮時轉譯的成果。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-111">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

<span data-ttu-id="ddc4a-112">如需 Azure 媒體 Hyperlapse 的更新，請參閱 [媒體服務部落格](https://azure.microsoft.com/blog/topics/media-services/)。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="ddc4a-113">將資產進行 Hyperlapse 處理</span><span class="sxs-lookup"><span data-stu-id="ddc4a-113">Hyperlapse an asset</span></span>
<span data-ttu-id="ddc4a-114">首先您需要上傳要輸入 Azure 媒體服務的檔案。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-114">First you will need to upload your desired input file to Azure Media Services.</span></span>  <span data-ttu-id="ddc4a-115">若要深入了解上傳和管理內容的相關概念，請閱讀 [內容管理文章](media-services-portal-vod-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="ddc4a-116"><a id="configuration"></a>Hyperlapse 的預設組態</span><span class="sxs-lookup"><span data-stu-id="ddc4a-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="ddc4a-117">一旦內容在媒體服務帳戶中，您將需要建構預設組態。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span></span>  <span data-ttu-id="ddc4a-118">下表說明使用者指定的欄位：</span><span class="sxs-lookup"><span data-stu-id="ddc4a-118">The following table explains the user-specified fields:</span></span>

| <span data-ttu-id="ddc4a-119">欄位</span><span class="sxs-lookup"><span data-stu-id="ddc4a-119">Field</span></span> | <span data-ttu-id="ddc4a-120">說明</span><span class="sxs-lookup"><span data-stu-id="ddc4a-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ddc4a-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="ddc4a-121">StartFrame</span></span> |<span data-ttu-id="ddc4a-122">開始進行 Microsoft Hyperlapse 處理的畫面。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="ddc4a-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="ddc4a-123">NumFrames</span></span> |<span data-ttu-id="ddc4a-124">要處理的畫面數目。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-124">The number of frames to process</span></span> |
| <span data-ttu-id="ddc4a-125">速度</span><span class="sxs-lookup"><span data-stu-id="ddc4a-125">Speed</span></span> |<span data-ttu-id="ddc4a-126">輸入影片要加速的設定因素。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-126">The factor with which to speed up the input video.</span></span> |

<span data-ttu-id="ddc4a-127">以下是符合標準的 JSON 和 XML 格式組態檔：</span><span class="sxs-lookup"><span data-stu-id="ddc4a-127">The following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="ddc4a-128">**XML 預設：**</span><span class="sxs-lookup"><span data-stu-id="ddc4a-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="ddc4a-129">**JSON 預設：**</span><span class="sxs-lookup"><span data-stu-id="ddc4a-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="ddc4a-130"><a id="sample_code"></a> 包含 AMS .NET SDK 的 Microsoft Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="ddc4a-130"><a id="sample_code"></a> Microsoft Hyperlapse with the AMS .NET SDK</span></span>
<span data-ttu-id="ddc4a-131">下列方法會將媒體檔案上傳為資產，並使用 Azure 媒體 Hyperlapse 媒體處理器建立工作。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="ddc4a-132">為了使程式碼可以運作，您應該已經具備在名稱為「context」之範圍內的 CloudMediaContext。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span></span>  <span data-ttu-id="ddc4a-133">若要深入了解，請參閱 [內容管理文章](media-services-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="ddc4a-134">字串引數 "hyperConfig" 預期為上述符合標準的 JSON 或 XML 格式的預設組態。</span><span class="sxs-lookup"><span data-stu-id="ddc4a-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span></span>
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

            // If job state is Error, the event handling
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

### <span data-ttu-id="ddc4a-135"><a id="file_types"></a>支援的檔案類型</span><span class="sxs-lookup"><span data-stu-id="ddc4a-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="ddc4a-136">MP4</span><span class="sxs-lookup"><span data-stu-id="ddc4a-136">MP4</span></span>
* <span data-ttu-id="ddc4a-137">MOV</span><span class="sxs-lookup"><span data-stu-id="ddc4a-137">MOV</span></span>
* <span data-ttu-id="ddc4a-138">WMV</span><span class="sxs-lookup"><span data-stu-id="ddc4a-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ddc4a-139">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="ddc4a-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ddc4a-140">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ddc4a-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="ddc4a-141">相關連結</span><span class="sxs-lookup"><span data-stu-id="ddc4a-141">Related links</span></span>
[<span data-ttu-id="ddc4a-142">Azure 媒體服務分析概觀</span><span class="sxs-lookup"><span data-stu-id="ddc4a-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="ddc4a-143">Azure 媒體分析示範</span><span class="sxs-lookup"><span data-stu-id="ddc4a-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

