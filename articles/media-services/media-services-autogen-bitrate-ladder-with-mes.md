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
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="6ea4f-105">使用 Azure 媒體編碼器標準 tooauto-產生的位元速率階梯</span><span class="sxs-lookup"><span data-stu-id="6ea4f-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="6ea4f-106">概觀</span><span class="sxs-lookup"><span data-stu-id="6ea4f-106">Overview</span></span>

<span data-ttu-id="6ea4f-107">本主題說明如何 toouse 媒體編碼器標準 (MES) tooauto-產生根據 hello 輸入的解析度和位元速率位元速率階梯 （位元速率高解析度組）。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="6ea4f-108">hello 自動產生的預設值絕對不會超過輸入 hello 解析度和位元速率。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="6ea4f-109">比方說，如果 hello 輸入是 720p 3Mbps，輸出會在最佳情況下，保持 720p 及速率低於 3Mbps 會啟動。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="6ea4f-110">只針對串流編碼</span><span class="sxs-lookup"><span data-stu-id="6ea4f-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="6ea4f-111">如果您的目的是 tooencode 您的來源視訊僅適用於資料流，則您應該使用 「 彈性資料流 」 的 hello 會預設建立編碼工作時。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="6ea4f-112">當使用 hello**彈性資料流**預設，hello MES 編碼器會以聰明的方式限制在位元速率階梯。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="6ea4f-113">不過，您將無法編碼的成本，因為 hello 服務會決定多少層 toouse 何種解析度可以 toocontrol hello。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="6ea4f-114">您可以看到的輸出層 MES 所產生的結果以 hello 編碼範例**彈性資料流**預設 hello 本主題結尾處。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="6ea4f-115">hello 輸出資產會包含 MP4 檔案，其中音訊和視訊不為交錯。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="6ea4f-116">針對串流和漸進式下載編碼</span><span class="sxs-lookup"><span data-stu-id="6ea4f-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="6ea4f-117">如果您的目的是 tooencode tooproduce MP4 檔案進行漸進式下載，以及資料流，則您應該使用 「 內容自動調整多重位元速率 MP4"hello 來源視訊會預設建立編碼工作時。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="6ea4f-118">當使用 hello**內容自動調整的多個位元速率 MP4**預設，hello MES 編碼器將會套用的 hello 相同編碼的邏輯與上面，但是 hello 輸出資產就會包含 MP4 檔案的音訊和視訊會交錯。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="6ea4f-119">您可以使用其中一個 MP4 檔案 （例如，hello 最大位元速率版） 為漸進式下載檔案。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="6ea4f-120"><a id="encoding_with_dotnet"></a>使用媒體服務 .NET SDK 進行編碼</span><span class="sxs-lookup"><span data-stu-id="6ea4f-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="6ea4f-121">hello，下列程式碼範例會使用 Media Services.NET SDK tooperform hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="6ea4f-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="6ea4f-122">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-122">Create an encoding job.</span></span>
- <span data-ttu-id="6ea4f-123">取得參考 toohello 媒體編碼器標準編碼器。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="6ea4f-124">加入的編碼工作 toohello 工作，並指定 toouse hello**彈性資料流**預設。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="6ea4f-125">建立會包含 hello 編碼資產的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="6ea4f-126">加入事件處理常式 toocheck hello 工作進度。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="6ea4f-127">送出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6ea4f-128">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="6ea4f-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="6ea4f-129">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="6ea4f-130">範例</span><span class="sxs-lookup"><span data-stu-id="6ea4f-130">Example</span></span>

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

## <span data-ttu-id="6ea4f-131"><a id="output"></a>輸出</span><span class="sxs-lookup"><span data-stu-id="6ea4f-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="6ea4f-132">此區段會顯示三個範例的輸出層 MES 所產生的結果以 hello 編碼**彈性資料流**預設。</span><span class="sxs-lookup"><span data-stu-id="6ea4f-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="6ea4f-133">範例 1</span><span class="sxs-lookup"><span data-stu-id="6ea4f-133">Example 1</span></span>
<span data-ttu-id="6ea4f-134">高度 "1080" 和畫面播放速率 "29.970" 的來源會產生 6 個視訊層︰</span><span class="sxs-lookup"><span data-stu-id="6ea4f-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="6ea4f-135">層次</span><span class="sxs-lookup"><span data-stu-id="6ea4f-135">Layer</span></span>|<span data-ttu-id="6ea4f-136">高度</span><span class="sxs-lookup"><span data-stu-id="6ea4f-136">Height</span></span>|<span data-ttu-id="6ea4f-137">寬度</span><span class="sxs-lookup"><span data-stu-id="6ea4f-137">Width</span></span>|<span data-ttu-id="6ea4f-138">位元速率 (kbps)</span><span class="sxs-lookup"><span data-stu-id="6ea4f-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="6ea4f-139">1</span><span class="sxs-lookup"><span data-stu-id="6ea4f-139">1</span></span>|<span data-ttu-id="6ea4f-140">1080</span><span class="sxs-lookup"><span data-stu-id="6ea4f-140">1080</span></span>|<span data-ttu-id="6ea4f-141">1920</span><span class="sxs-lookup"><span data-stu-id="6ea4f-141">1920</span></span>|<span data-ttu-id="6ea4f-142">6780</span><span class="sxs-lookup"><span data-stu-id="6ea4f-142">6780</span></span>|
|<span data-ttu-id="6ea4f-143">2</span><span class="sxs-lookup"><span data-stu-id="6ea4f-143">2</span></span>|<span data-ttu-id="6ea4f-144">720</span><span class="sxs-lookup"><span data-stu-id="6ea4f-144">720</span></span>|<span data-ttu-id="6ea4f-145">1280</span><span class="sxs-lookup"><span data-stu-id="6ea4f-145">1280</span></span>|<span data-ttu-id="6ea4f-146">3520</span><span class="sxs-lookup"><span data-stu-id="6ea4f-146">3520</span></span>|
|<span data-ttu-id="6ea4f-147">3</span><span class="sxs-lookup"><span data-stu-id="6ea4f-147">3</span></span>|<span data-ttu-id="6ea4f-148">540</span><span class="sxs-lookup"><span data-stu-id="6ea4f-148">540</span></span>|<span data-ttu-id="6ea4f-149">960</span><span class="sxs-lookup"><span data-stu-id="6ea4f-149">960</span></span>|<span data-ttu-id="6ea4f-150">2210</span><span class="sxs-lookup"><span data-stu-id="6ea4f-150">2210</span></span>|
|<span data-ttu-id="6ea4f-151">4</span><span class="sxs-lookup"><span data-stu-id="6ea4f-151">4</span></span>|<span data-ttu-id="6ea4f-152">360</span><span class="sxs-lookup"><span data-stu-id="6ea4f-152">360</span></span>|<span data-ttu-id="6ea4f-153">640</span><span class="sxs-lookup"><span data-stu-id="6ea4f-153">640</span></span>|<span data-ttu-id="6ea4f-154">1150</span><span class="sxs-lookup"><span data-stu-id="6ea4f-154">1150</span></span>|
|<span data-ttu-id="6ea4f-155">5</span><span class="sxs-lookup"><span data-stu-id="6ea4f-155">5</span></span>|<span data-ttu-id="6ea4f-156">270</span><span class="sxs-lookup"><span data-stu-id="6ea4f-156">270</span></span>|<span data-ttu-id="6ea4f-157">480</span><span class="sxs-lookup"><span data-stu-id="6ea4f-157">480</span></span>|<span data-ttu-id="6ea4f-158">720</span><span class="sxs-lookup"><span data-stu-id="6ea4f-158">720</span></span>|
|<span data-ttu-id="6ea4f-159">6</span><span class="sxs-lookup"><span data-stu-id="6ea4f-159">6</span></span>|<span data-ttu-id="6ea4f-160">180</span><span class="sxs-lookup"><span data-stu-id="6ea4f-160">180</span></span>|<span data-ttu-id="6ea4f-161">320</span><span class="sxs-lookup"><span data-stu-id="6ea4f-161">320</span></span>|<span data-ttu-id="6ea4f-162">380</span><span class="sxs-lookup"><span data-stu-id="6ea4f-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="6ea4f-163">範例 2</span><span class="sxs-lookup"><span data-stu-id="6ea4f-163">Example 2</span></span>
<span data-ttu-id="6ea4f-164">高度 "720" 和畫面播放速率 "23.970" 的來源會產生 5 個視訊層︰</span><span class="sxs-lookup"><span data-stu-id="6ea4f-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="6ea4f-165">層次</span><span class="sxs-lookup"><span data-stu-id="6ea4f-165">Layer</span></span>|<span data-ttu-id="6ea4f-166">高度</span><span class="sxs-lookup"><span data-stu-id="6ea4f-166">Height</span></span>|<span data-ttu-id="6ea4f-167">寬度</span><span class="sxs-lookup"><span data-stu-id="6ea4f-167">Width</span></span>|<span data-ttu-id="6ea4f-168">位元速率 (kbps)</span><span class="sxs-lookup"><span data-stu-id="6ea4f-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="6ea4f-169">1</span><span class="sxs-lookup"><span data-stu-id="6ea4f-169">1</span></span>|<span data-ttu-id="6ea4f-170">720</span><span class="sxs-lookup"><span data-stu-id="6ea4f-170">720</span></span>|<span data-ttu-id="6ea4f-171">1280</span><span class="sxs-lookup"><span data-stu-id="6ea4f-171">1280</span></span>|<span data-ttu-id="6ea4f-172">2940</span><span class="sxs-lookup"><span data-stu-id="6ea4f-172">2940</span></span>|
|<span data-ttu-id="6ea4f-173">2</span><span class="sxs-lookup"><span data-stu-id="6ea4f-173">2</span></span>|<span data-ttu-id="6ea4f-174">540</span><span class="sxs-lookup"><span data-stu-id="6ea4f-174">540</span></span>|<span data-ttu-id="6ea4f-175">960</span><span class="sxs-lookup"><span data-stu-id="6ea4f-175">960</span></span>|<span data-ttu-id="6ea4f-176">1850</span><span class="sxs-lookup"><span data-stu-id="6ea4f-176">1850</span></span>|
|<span data-ttu-id="6ea4f-177">3</span><span class="sxs-lookup"><span data-stu-id="6ea4f-177">3</span></span>|<span data-ttu-id="6ea4f-178">360</span><span class="sxs-lookup"><span data-stu-id="6ea4f-178">360</span></span>|<span data-ttu-id="6ea4f-179">640</span><span class="sxs-lookup"><span data-stu-id="6ea4f-179">640</span></span>|<span data-ttu-id="6ea4f-180">960</span><span class="sxs-lookup"><span data-stu-id="6ea4f-180">960</span></span>|
|<span data-ttu-id="6ea4f-181">4</span><span class="sxs-lookup"><span data-stu-id="6ea4f-181">4</span></span>|<span data-ttu-id="6ea4f-182">270</span><span class="sxs-lookup"><span data-stu-id="6ea4f-182">270</span></span>|<span data-ttu-id="6ea4f-183">480</span><span class="sxs-lookup"><span data-stu-id="6ea4f-183">480</span></span>|<span data-ttu-id="6ea4f-184">600</span><span class="sxs-lookup"><span data-stu-id="6ea4f-184">600</span></span>|
|<span data-ttu-id="6ea4f-185">5</span><span class="sxs-lookup"><span data-stu-id="6ea4f-185">5</span></span>|<span data-ttu-id="6ea4f-186">180</span><span class="sxs-lookup"><span data-stu-id="6ea4f-186">180</span></span>|<span data-ttu-id="6ea4f-187">320</span><span class="sxs-lookup"><span data-stu-id="6ea4f-187">320</span></span>|<span data-ttu-id="6ea4f-188">320</span><span class="sxs-lookup"><span data-stu-id="6ea4f-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="6ea4f-189">範例 3</span><span class="sxs-lookup"><span data-stu-id="6ea4f-189">Example 3</span></span>
<span data-ttu-id="6ea4f-190">高度 "360" 和畫面播放速率 "29.970" 的來源會產生 3 個視訊層︰</span><span class="sxs-lookup"><span data-stu-id="6ea4f-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="6ea4f-191">層次</span><span class="sxs-lookup"><span data-stu-id="6ea4f-191">Layer</span></span>|<span data-ttu-id="6ea4f-192">高度</span><span class="sxs-lookup"><span data-stu-id="6ea4f-192">Height</span></span>|<span data-ttu-id="6ea4f-193">寬度</span><span class="sxs-lookup"><span data-stu-id="6ea4f-193">Width</span></span>|<span data-ttu-id="6ea4f-194">位元速率 (kbps)</span><span class="sxs-lookup"><span data-stu-id="6ea4f-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="6ea4f-195">1</span><span class="sxs-lookup"><span data-stu-id="6ea4f-195">1</span></span>|<span data-ttu-id="6ea4f-196">360</span><span class="sxs-lookup"><span data-stu-id="6ea4f-196">360</span></span>|<span data-ttu-id="6ea4f-197">640</span><span class="sxs-lookup"><span data-stu-id="6ea4f-197">640</span></span>|<span data-ttu-id="6ea4f-198">700</span><span class="sxs-lookup"><span data-stu-id="6ea4f-198">700</span></span>|
|<span data-ttu-id="6ea4f-199">2</span><span class="sxs-lookup"><span data-stu-id="6ea4f-199">2</span></span>|<span data-ttu-id="6ea4f-200">270</span><span class="sxs-lookup"><span data-stu-id="6ea4f-200">270</span></span>|<span data-ttu-id="6ea4f-201">480</span><span class="sxs-lookup"><span data-stu-id="6ea4f-201">480</span></span>|<span data-ttu-id="6ea4f-202">440</span><span class="sxs-lookup"><span data-stu-id="6ea4f-202">440</span></span>|
|<span data-ttu-id="6ea4f-203">3</span><span class="sxs-lookup"><span data-stu-id="6ea4f-203">3</span></span>|<span data-ttu-id="6ea4f-204">180</span><span class="sxs-lookup"><span data-stu-id="6ea4f-204">180</span></span>|<span data-ttu-id="6ea4f-205">320</span><span class="sxs-lookup"><span data-stu-id="6ea4f-205">320</span></span>|<span data-ttu-id="6ea4f-206">230</span><span class="sxs-lookup"><span data-stu-id="6ea4f-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="6ea4f-207">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="6ea4f-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6ea4f-208">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="6ea4f-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6ea4f-209">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6ea4f-209">See Also</span></span>
[<span data-ttu-id="6ea4f-210">媒體服務編碼概觀</span><span class="sxs-lookup"><span data-stu-id="6ea4f-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

