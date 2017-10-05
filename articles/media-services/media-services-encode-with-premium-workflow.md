---
title: "利用 Media Encoder Premium Workflow 進行進階編碼 | Microsoft Docs"
description: "了解如何使用 Media Encoder Premium Workflow 進行編碼。 程式碼範例以 C# 撰寫，並使用 Media Services SDK for .NET。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 2b03853bf07e05c07fd730d5e8a8563963887921
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="09961-104">使用 Media Encoder Premium Workflow 進行進階編碼</span><span class="sxs-lookup"><span data-stu-id="09961-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="09961-105">本主題中討論的媒體編碼器高階工作流程媒體處理器無法在中國使用。</span><span class="sxs-lookup"><span data-stu-id="09961-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="09961-106">如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="09961-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="09961-107">Overview</span><span class="sxs-lookup"><span data-stu-id="09961-107">Overview</span></span>
<span data-ttu-id="09961-108">Microsoft Azure 媒體服務推出 **Media Encoder Premium Workflow** 媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="09961-108">Microsoft Azure Media Services is introducing the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="09961-109">此處理器為高階隨選工作流程提供先進的編碼功能。</span><span class="sxs-lookup"><span data-stu-id="09961-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="09961-110">以下主題說明 **Media Encoder Premium Workflow**的相關詳細資料：</span><span class="sxs-lookup"><span data-stu-id="09961-110">The following topics outline details related to **Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="09961-111">[Media Encoder Premium Workflow 支援的格式](media-services-premium-workflow-encoder-formats.md) – 討論 **Media Encoder Premium Workflow**支援的檔案格式和轉碼器。</span><span class="sxs-lookup"><span data-stu-id="09961-111">[Formats Supported by the Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses the file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="09961-112">[Azure 隨選媒體編碼器的概觀和比較](media-services-encode-asset.md)比較 **Media Encoder Premium Workflow** 和**媒體編碼器標準**的編碼功能。</span><span class="sxs-lookup"><span data-stu-id="09961-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares the encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="09961-113">本主題示範如何使用 .NET 以 **Media Encoder Premium Workflow** 進行編碼。</span><span class="sxs-lookup"><span data-stu-id="09961-113">This topic demonstrates how to encode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="09961-114">**Media Encoder Premium Workflow** 的編碼工作需要個別的組態檔，這稱為工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="09961-114">Encoding tasks for the **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="09961-115">這些檔案具有 .workflow 副檔名，並且使用 [工作流程設計工具](media-services-workflow-designer.md) 工具建立。</span><span class="sxs-lookup"><span data-stu-id="09961-115">These files have a .workflow extension and are created using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="09961-116">您也可以在 [這裡](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)取得預設的工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="09961-116">You can also get the default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="09961-117">資料夾也包含這些檔案的說明。</span><span class="sxs-lookup"><span data-stu-id="09961-117">The folder also contains the description of these files.</span></span>

<span data-ttu-id="09961-118">工作流程檔案必須上傳至媒體服務帳戶做為資產，而且應將此資產傳遞給編碼工作。</span><span class="sxs-lookup"><span data-stu-id="09961-118">The workflow files need to be uploaded to your Media Services account as an Asset, and this Asset should be passed in to the encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="09961-119">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="09961-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="09961-120">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="09961-120">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="09961-121">編碼範例</span><span class="sxs-lookup"><span data-stu-id="09961-121">Encoding example</span></span>

<span data-ttu-id="09961-122">下列範例示範如何使用 **Media Encoder Premium Workflow**進行編碼。</span><span class="sxs-lookup"><span data-stu-id="09961-122">The following example demonstrates how to encode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="09961-123">會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="09961-123">The following steps are performed:</span></span>

1. <span data-ttu-id="09961-124">建立資產並上傳工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="09961-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="09961-125">建立資產並上傳來源媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="09961-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="09961-126">取得 “Media Encoder Premium Workflow” 媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="09961-126">Get the "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="09961-127">建立工作 (Job) 和工作 (Task)。</span><span class="sxs-lookup"><span data-stu-id="09961-127">Create a job and a task.</span></span>

    <span data-ttu-id="09961-128">在大部分情況下，工作的組態字串是空的 (如下列範例)。</span><span class="sxs-lookup"><span data-stu-id="09961-128">In most cases, the configuration string for the task is empty (like in the following example).</span></span> <span data-ttu-id="09961-129">在一些進階的案例 (會要求您動態設定執行階段屬性) 情況下，您可以提供 XML 字串給編碼工作。</span><span class="sxs-lookup"><span data-stu-id="09961-129">There are some advanced scenarios (that require you to to set runtime properties dynamically) in which case you would provide an XML string to the encoding task.</span></span> <span data-ttu-id="09961-130">這類案例的範例包括：建立疊加、平行或循序的媒體編結、顯示字幕。</span><span class="sxs-lookup"><span data-stu-id="09961-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="09961-131">將兩個輸入資產加入工作 (Task)。</span><span class="sxs-lookup"><span data-stu-id="09961-131">Add two input assets to the task.</span></span>

    1. <span data-ttu-id="09961-132">第一個 – 工作流程資產。</span><span class="sxs-lookup"><span data-stu-id="09961-132">1st – the workflow asset.</span></span>
    2. <span data-ttu-id="09961-133">第二個 – 視訊資產。</span><span class="sxs-lookup"><span data-stu-id="09961-133">2nd – the video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="09961-134">新增媒體資產前，必須先將工作流程資產新增至工作 (Task)。</span><span class="sxs-lookup"><span data-stu-id="09961-134">The workflow asset must be added to the task before the media asset.</span></span>
   <span data-ttu-id="09961-135">這項工作 (Task) 的組態字串應該是空的。</span><span class="sxs-lookup"><span data-stu-id="09961-135">The configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="09961-136">提交編碼工作 (Job)。</span><span class="sxs-lookup"><span data-stu-id="09961-136">Submit the encoding job.</span></span>

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass to it the name of the
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset to contain the results of the job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means the output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use the following event handler to check job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch the job.
                    job.Submit();

                    // Check job execution and wait for job to finish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error the event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due to job error.");
                    }

                    return job.OutputMediaAssets[0];
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

<span data-ttu-id="09961-137">如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="09961-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="09961-138">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="09961-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="09961-139">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="09961-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
