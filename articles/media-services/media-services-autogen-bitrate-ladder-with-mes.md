---
title: "使用 Azure 媒體編碼器標準自動產生位元速率階梯 | Microsoft Docs"
description: "本主題說明如何使用媒體編碼器標準 (MES) 根據輸入解析度和位元速率自動產生位元速率階梯。 永遠不會超過輸入解析度和位元速率。 例如，如果輸入是 720p 3Mbps，則輸出會維持在最多 720p，且速率啟動低於 3Mbps。"
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
ms.openlocfilehash: b5616aa9f8b15ab576d914fbae89a56f64c27f4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a><span data-ttu-id="3f8ae-105">使用 Azure 媒體編碼器標準自動產生位元速率階梯</span><span class="sxs-lookup"><span data-stu-id="3f8ae-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="3f8ae-106">概觀</span><span class="sxs-lookup"><span data-stu-id="3f8ae-106">Overview</span></span>

<span data-ttu-id="3f8ae-107">本主題說明如何使用媒體編碼器標準 (MES) 根據解析度和位元速率自動產生輸入位元速率階梯 (位元速率解析組)。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-107">This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="3f8ae-108">自動產生的預設值絕對不會超過輸入解析度和位元速率。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-108">The auto-generated preset will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="3f8ae-109">例如，如果輸入是 720p 3Mbps，則輸出會維持在最多 720p，且速率啟動低於 3Mbps。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-109">For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="3f8ae-110">只針對串流編碼</span><span class="sxs-lookup"><span data-stu-id="3f8ae-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="3f8ae-111">如果您打算只針對串流編碼來源視訊，則您在建立編碼工作時，應該使用 "Adaptive Streaming" (彈性資料流) 預設值。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-111">If your intent is to encode your source video only for streaming, then you shoud use the "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="3f8ae-112">當使用 **Adaptive Streaming** (彈性資料流) 預設值時，MES 編碼器會智慧地覆蓋位元速率階梯。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-112">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="3f8ae-113">不過，您將無法控制編碼成本，因為服務會決定要使用多少層以及哪種解析度。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-113">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span></span> <span data-ttu-id="3f8ae-114">由於本主題結尾使用 **Adaptive Streaming** (彈性資料流) 進行編碼的結果，您可以看到 MES 產生的輸出層範例。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-114">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the end of this topic.</span></span> <span data-ttu-id="3f8ae-115">輸出資產將包含 MP4 檔案，其中的音訊和視訊為非交錯格式。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-115">The output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="3f8ae-116">針對串流和漸進式下載編碼</span><span class="sxs-lookup"><span data-stu-id="3f8ae-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="3f8ae-117">如果您打算針對串流以及漸進式下載要產生的 MP4 檔案編碼，則您在建立編碼工作時，應該使用 "Content Adaptive Multiple Bitrate MP4" (內容自適性多位元速率 MP4) 預設值。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-117">If your intent is to encode your source video for streaming as well as to produce MP4 files for progressive download, then you shoud use the "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="3f8ae-118">使用 **Content Adaptive Multiple Bitrate MP4** (內容自適性多位元速率 MP4) 預設值時，MES 編碼器將會套用與先前相同的編碼邏輯，但現在輸出資產會包含 MP4 檔案，其中的音訊和視訊為交錯格式。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-118">When using the **Content Adaptive Multiple Bitrate MP4** preset, the MES encoder will apply the same encoding logic as above, but now the output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="3f8ae-119">您可以使用這些 MP4 檔案的其中一個 (例如最高位元速率的版本) 作為漸進式下載檔案。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-119">You can use one of these MP4 files (for example, the highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="3f8ae-120"><a id="encoding_with_dotnet"></a>使用媒體服務 .NET SDK 進行編碼</span><span class="sxs-lookup"><span data-stu-id="3f8ae-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="3f8ae-121">下列程式碼範例使用媒體服務 .NET SDK 執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="3f8ae-121">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="3f8ae-122">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-122">Create an encoding job.</span></span>
- <span data-ttu-id="3f8ae-123">取得對 Media Encoder Standard 編碼器的參考</span><span class="sxs-lookup"><span data-stu-id="3f8ae-123">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="3f8ae-124">將編碼工作新增至作業，並指定使用**彈性資料流**預設值。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-124">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="3f8ae-125">建立將包含已編碼資產的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-125">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="3f8ae-126">加入事件處理常式來檢查工作進度。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-126">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="3f8ae-127">提交作業。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-127">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3f8ae-128">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="3f8ae-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="3f8ae-129">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-129">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="3f8ae-130">範例</span><span class="sxs-lookup"><span data-stu-id="3f8ae-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
    {
        class Program
        {
        // Read values from the App.config file.
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

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <span data-ttu-id="3f8ae-131"><a id="output"></a>輸出</span><span class="sxs-lookup"><span data-stu-id="3f8ae-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="3f8ae-132">由於編碼與**彈性資料流**預設值，本區段會顯示 MES 所產生的輸出層範例。</span><span class="sxs-lookup"><span data-stu-id="3f8ae-132">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="3f8ae-133">範例 1</span><span class="sxs-lookup"><span data-stu-id="3f8ae-133">Example 1</span></span>
<span data-ttu-id="3f8ae-134">高度 "1080" 和畫面播放速率 "29.970" 的來源會產生 6 個視訊層︰</span><span class="sxs-lookup"><span data-stu-id="3f8ae-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="3f8ae-135">層次</span><span class="sxs-lookup"><span data-stu-id="3f8ae-135">Layer</span></span>|<span data-ttu-id="3f8ae-136">高度</span><span class="sxs-lookup"><span data-stu-id="3f8ae-136">Height</span></span>|<span data-ttu-id="3f8ae-137">寬度</span><span class="sxs-lookup"><span data-stu-id="3f8ae-137">Width</span></span>|<span data-ttu-id="3f8ae-138">位元速率 (kbps)</span><span class="sxs-lookup"><span data-stu-id="3f8ae-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="3f8ae-139">1</span><span class="sxs-lookup"><span data-stu-id="3f8ae-139">1</span></span>|<span data-ttu-id="3f8ae-140">1080</span><span class="sxs-lookup"><span data-stu-id="3f8ae-140">1080</span></span>|<span data-ttu-id="3f8ae-141">1920</span><span class="sxs-lookup"><span data-stu-id="3f8ae-141">1920</span></span>|<span data-ttu-id="3f8ae-142">6780</span><span class="sxs-lookup"><span data-stu-id="3f8ae-142">6780</span></span>|
|<span data-ttu-id="3f8ae-143">2</span><span class="sxs-lookup"><span data-stu-id="3f8ae-143">2</span></span>|<span data-ttu-id="3f8ae-144">720</span><span class="sxs-lookup"><span data-stu-id="3f8ae-144">720</span></span>|<span data-ttu-id="3f8ae-145">1280</span><span class="sxs-lookup"><span data-stu-id="3f8ae-145">1280</span></span>|<span data-ttu-id="3f8ae-146">3520</span><span class="sxs-lookup"><span data-stu-id="3f8ae-146">3520</span></span>|
|<span data-ttu-id="3f8ae-147">3</span><span class="sxs-lookup"><span data-stu-id="3f8ae-147">3</span></span>|<span data-ttu-id="3f8ae-148">540</span><span class="sxs-lookup"><span data-stu-id="3f8ae-148">540</span></span>|<span data-ttu-id="3f8ae-149">960</span><span class="sxs-lookup"><span data-stu-id="3f8ae-149">960</span></span>|<span data-ttu-id="3f8ae-150">2210</span><span class="sxs-lookup"><span data-stu-id="3f8ae-150">2210</span></span>|
|<span data-ttu-id="3f8ae-151">4</span><span class="sxs-lookup"><span data-stu-id="3f8ae-151">4</span></span>|<span data-ttu-id="3f8ae-152">360</span><span class="sxs-lookup"><span data-stu-id="3f8ae-152">360</span></span>|<span data-ttu-id="3f8ae-153">640</span><span class="sxs-lookup"><span data-stu-id="3f8ae-153">640</span></span>|<span data-ttu-id="3f8ae-154">1150</span><span class="sxs-lookup"><span data-stu-id="3f8ae-154">1150</span></span>|
|<span data-ttu-id="3f8ae-155">5</span><span class="sxs-lookup"><span data-stu-id="3f8ae-155">5</span></span>|<span data-ttu-id="3f8ae-156">270</span><span class="sxs-lookup"><span data-stu-id="3f8ae-156">270</span></span>|<span data-ttu-id="3f8ae-157">480</span><span class="sxs-lookup"><span data-stu-id="3f8ae-157">480</span></span>|<span data-ttu-id="3f8ae-158">720</span><span class="sxs-lookup"><span data-stu-id="3f8ae-158">720</span></span>|
|<span data-ttu-id="3f8ae-159">6</span><span class="sxs-lookup"><span data-stu-id="3f8ae-159">6</span></span>|<span data-ttu-id="3f8ae-160">180</span><span class="sxs-lookup"><span data-stu-id="3f8ae-160">180</span></span>|<span data-ttu-id="3f8ae-161">320</span><span class="sxs-lookup"><span data-stu-id="3f8ae-161">320</span></span>|<span data-ttu-id="3f8ae-162">380</span><span class="sxs-lookup"><span data-stu-id="3f8ae-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="3f8ae-163">範例 2</span><span class="sxs-lookup"><span data-stu-id="3f8ae-163">Example 2</span></span>
<span data-ttu-id="3f8ae-164">高度 "720" 和畫面播放速率 "23.970" 的來源會產生 5 個視訊層︰</span><span class="sxs-lookup"><span data-stu-id="3f8ae-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="3f8ae-165">層次</span><span class="sxs-lookup"><span data-stu-id="3f8ae-165">Layer</span></span>|<span data-ttu-id="3f8ae-166">高度</span><span class="sxs-lookup"><span data-stu-id="3f8ae-166">Height</span></span>|<span data-ttu-id="3f8ae-167">寬度</span><span class="sxs-lookup"><span data-stu-id="3f8ae-167">Width</span></span>|<span data-ttu-id="3f8ae-168">位元速率 (kbps)</span><span class="sxs-lookup"><span data-stu-id="3f8ae-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="3f8ae-169">1</span><span class="sxs-lookup"><span data-stu-id="3f8ae-169">1</span></span>|<span data-ttu-id="3f8ae-170">720</span><span class="sxs-lookup"><span data-stu-id="3f8ae-170">720</span></span>|<span data-ttu-id="3f8ae-171">1280</span><span class="sxs-lookup"><span data-stu-id="3f8ae-171">1280</span></span>|<span data-ttu-id="3f8ae-172">2940</span><span class="sxs-lookup"><span data-stu-id="3f8ae-172">2940</span></span>|
|<span data-ttu-id="3f8ae-173">2</span><span class="sxs-lookup"><span data-stu-id="3f8ae-173">2</span></span>|<span data-ttu-id="3f8ae-174">540</span><span class="sxs-lookup"><span data-stu-id="3f8ae-174">540</span></span>|<span data-ttu-id="3f8ae-175">960</span><span class="sxs-lookup"><span data-stu-id="3f8ae-175">960</span></span>|<span data-ttu-id="3f8ae-176">1850</span><span class="sxs-lookup"><span data-stu-id="3f8ae-176">1850</span></span>|
|<span data-ttu-id="3f8ae-177">3</span><span class="sxs-lookup"><span data-stu-id="3f8ae-177">3</span></span>|<span data-ttu-id="3f8ae-178">360</span><span class="sxs-lookup"><span data-stu-id="3f8ae-178">360</span></span>|<span data-ttu-id="3f8ae-179">640</span><span class="sxs-lookup"><span data-stu-id="3f8ae-179">640</span></span>|<span data-ttu-id="3f8ae-180">960</span><span class="sxs-lookup"><span data-stu-id="3f8ae-180">960</span></span>|
|<span data-ttu-id="3f8ae-181">4</span><span class="sxs-lookup"><span data-stu-id="3f8ae-181">4</span></span>|<span data-ttu-id="3f8ae-182">270</span><span class="sxs-lookup"><span data-stu-id="3f8ae-182">270</span></span>|<span data-ttu-id="3f8ae-183">480</span><span class="sxs-lookup"><span data-stu-id="3f8ae-183">480</span></span>|<span data-ttu-id="3f8ae-184">600</span><span class="sxs-lookup"><span data-stu-id="3f8ae-184">600</span></span>|
|<span data-ttu-id="3f8ae-185">5</span><span class="sxs-lookup"><span data-stu-id="3f8ae-185">5</span></span>|<span data-ttu-id="3f8ae-186">180</span><span class="sxs-lookup"><span data-stu-id="3f8ae-186">180</span></span>|<span data-ttu-id="3f8ae-187">320</span><span class="sxs-lookup"><span data-stu-id="3f8ae-187">320</span></span>|<span data-ttu-id="3f8ae-188">320</span><span class="sxs-lookup"><span data-stu-id="3f8ae-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="3f8ae-189">範例 3</span><span class="sxs-lookup"><span data-stu-id="3f8ae-189">Example 3</span></span>
<span data-ttu-id="3f8ae-190">高度 "360" 和畫面播放速率 "29.970" 的來源會產生 3 個視訊層︰</span><span class="sxs-lookup"><span data-stu-id="3f8ae-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="3f8ae-191">層次</span><span class="sxs-lookup"><span data-stu-id="3f8ae-191">Layer</span></span>|<span data-ttu-id="3f8ae-192">高度</span><span class="sxs-lookup"><span data-stu-id="3f8ae-192">Height</span></span>|<span data-ttu-id="3f8ae-193">寬度</span><span class="sxs-lookup"><span data-stu-id="3f8ae-193">Width</span></span>|<span data-ttu-id="3f8ae-194">位元速率 (kbps)</span><span class="sxs-lookup"><span data-stu-id="3f8ae-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="3f8ae-195">1</span><span class="sxs-lookup"><span data-stu-id="3f8ae-195">1</span></span>|<span data-ttu-id="3f8ae-196">360</span><span class="sxs-lookup"><span data-stu-id="3f8ae-196">360</span></span>|<span data-ttu-id="3f8ae-197">640</span><span class="sxs-lookup"><span data-stu-id="3f8ae-197">640</span></span>|<span data-ttu-id="3f8ae-198">700</span><span class="sxs-lookup"><span data-stu-id="3f8ae-198">700</span></span>|
|<span data-ttu-id="3f8ae-199">2</span><span class="sxs-lookup"><span data-stu-id="3f8ae-199">2</span></span>|<span data-ttu-id="3f8ae-200">270</span><span class="sxs-lookup"><span data-stu-id="3f8ae-200">270</span></span>|<span data-ttu-id="3f8ae-201">480</span><span class="sxs-lookup"><span data-stu-id="3f8ae-201">480</span></span>|<span data-ttu-id="3f8ae-202">440</span><span class="sxs-lookup"><span data-stu-id="3f8ae-202">440</span></span>|
|<span data-ttu-id="3f8ae-203">3</span><span class="sxs-lookup"><span data-stu-id="3f8ae-203">3</span></span>|<span data-ttu-id="3f8ae-204">180</span><span class="sxs-lookup"><span data-stu-id="3f8ae-204">180</span></span>|<span data-ttu-id="3f8ae-205">320</span><span class="sxs-lookup"><span data-stu-id="3f8ae-205">320</span></span>|<span data-ttu-id="3f8ae-206">230</span><span class="sxs-lookup"><span data-stu-id="3f8ae-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="3f8ae-207">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="3f8ae-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3f8ae-208">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="3f8ae-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="3f8ae-209">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3f8ae-209">See Also</span></span>
[<span data-ttu-id="3f8ae-210">媒體服務編碼概觀</span><span class="sxs-lookup"><span data-stu-id="3f8ae-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

