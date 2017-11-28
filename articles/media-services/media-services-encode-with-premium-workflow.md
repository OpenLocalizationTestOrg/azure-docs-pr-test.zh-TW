---
title: "媒體編碼器高階工作流程的編碼 aaaAdvanced |Microsoft 文件"
description: "深入了解如何 tooencode 與媒體編碼器高階工作流程。 程式碼範例會以 C# 所撰寫，並使用 hello Media Services SDK for.NET。"
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
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="5e6fe-104">使用 Media Encoder Premium Workflow 進行進階編碼</span><span class="sxs-lookup"><span data-stu-id="5e6fe-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="5e6fe-105">本主題中討論的媒體編碼器高階工作流程媒體處理器無法在中國使用。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="5e6fe-106">如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="5e6fe-107">概觀</span><span class="sxs-lookup"><span data-stu-id="5e6fe-107">Overview</span></span>
<span data-ttu-id="5e6fe-108">Microsoft Azure Media Services 推出 hello**媒體編碼器高階工作流程**媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-108">Microsoft Azure Media Services is introducing hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="5e6fe-109">此處理器為高階隨選工作流程提供先進的編碼功能。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="5e6fe-110">hello 下列主題簡述太相關詳細資料，**媒體編碼器高階工作流程**:</span><span class="sxs-lookup"><span data-stu-id="5e6fe-110">hello following topics outline details related too**Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="5e6fe-111">[Hello 媒體編碼器高階工作流程來格式化支援](media-services-premium-workflow-encoder-formats.md)– 討論 hello 檔案格式和轉碼器支援**媒體編碼器高階工作流程**。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-111">[Formats Supported by hello Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses hello file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="5e6fe-112">[概觀與比較 Azure 上要求的媒體編碼器](media-services-encode-asset.md)比較 hello 的編碼能力**媒體編碼器高階工作流程**和**媒體編碼器標準**。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares hello encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="5e6fe-113">本主題示範如何使用 tooencode**媒體編碼器高階工作流程**使用.NET。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-113">This topic demonstrates how tooencode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="5e6fe-114">編碼工作的 hello**媒體編碼器高階工作流程**需要不同的組態檔，稱為工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-114">Encoding tasks for hello **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="5e6fe-115">這些檔案具有.workflow 副檔名，而且會建立使用 hello[工作流程設計工具](media-services-workflow-designer.md)工具。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-115">These files have a .workflow extension and are created using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="5e6fe-116">您也可以取得 hello 預設工作流程檔案[這裡](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-116">You can also get hello default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="5e6fe-117">hello 資料夾也包含 hello 描述這些檔案。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-117">hello folder also contains hello description of these files.</span></span>

<span data-ttu-id="5e6fe-118">hello 工作流程檔案需要上傳 toobe tooyour 媒體服務帳戶為資產，，這項資產應該 toohello 編碼工作中進行傳遞。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-118">hello workflow files need toobe uploaded tooyour Media Services account as an Asset, and this Asset should be passed in toohello encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="5e6fe-119">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="5e6fe-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="5e6fe-120">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-120">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="5e6fe-121">編碼範例</span><span class="sxs-lookup"><span data-stu-id="5e6fe-121">Encoding example</span></span>

<span data-ttu-id="5e6fe-122">hello 下列範例會示範如何使用 tooencode**媒體編碼器高階工作流程**。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-122">hello following example demonstrates how tooencode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="5e6fe-123">會執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e6fe-123">hello following steps are performed:</span></span>

1. <span data-ttu-id="5e6fe-124">建立資產並上傳工作流程檔案。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="5e6fe-125">建立資產並上傳來源媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="5e6fe-126">收到 hello"媒體編碼器高階工作流程"媒體處理器。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-126">Get hello "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="5e6fe-127">建立工作 (Job) 和工作 (Task)。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-127">Create a job and a task.</span></span>

    <span data-ttu-id="5e6fe-128">在大部分情況下，hello hello 工作的組態字串是空的 （如下列範例中的 hello 中）。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-128">In most cases, hello configuration string for hello task is empty (like in hello following example).</span></span> <span data-ttu-id="5e6fe-129">有一些進階的案例 （需要的 tootooset 執行階段屬性動態地） 在此情況下，您會提供 XML 字串 toohello 編碼工作。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-129">There are some advanced scenarios (that require you tootooset runtime properties dynamically) in which case you would provide an XML string toohello encoding task.</span></span> <span data-ttu-id="5e6fe-130">這類案例的範例包括：建立疊加、平行或循序的媒體編結、顯示字幕。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="5e6fe-131">加入兩個輸入的資產 toohello 工作。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-131">Add two input assets toohello task.</span></span>

    1. <span data-ttu-id="5e6fe-132">第 1 – hello 工作流程的資產。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-132">1st – hello workflow asset.</span></span>
    2. <span data-ttu-id="5e6fe-133">第 2 – hello 視訊資產。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-133">2nd – hello video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5e6fe-134">hello 工作流程資產必須加入 toohello 工作之前 hello 媒體資產。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-134">hello workflow asset must be added toohello task before hello media asset.</span></span>
   <span data-ttu-id="5e6fe-135">這項工作中的 hello 組態字串應為空白。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-135">hello configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="5e6fe-136">送出 hello 編碼工作。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-136">Submit hello encoding job.</span></span>

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
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
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

<span data-ttu-id="5e6fe-137">如有進階編碼器的問題，請傳送電子郵件到 mepd@Microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="5e6fe-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5e6fe-138">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="5e6fe-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5e6fe-139">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5e6fe-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
