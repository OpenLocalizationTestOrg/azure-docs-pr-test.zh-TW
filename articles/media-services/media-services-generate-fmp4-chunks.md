---
title: "Azure Media Services 編碼工作產生 fMP4 區塊 aaaCreate |Microsoft 文件"
description: "本主題說明如何 toocreate 產生 fMP4 編碼工作區塊。 媒體編碼器標準 hello 或媒體編碼器高階工作流程的編碼器搭配使用這項工作中時, hello 輸出資產包含 fMP4 區塊，而不是 ISO MP4 檔案。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b7029ac5-eadd-4a2f-8111-1fc460828981
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 388f3ccb9865b5c4e159af86d5a9ee2f4e3f6120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="create-an-encoding-task-that-generates-fmp4-chunks"></a><span data-ttu-id="e5873-104">建立會產生 fMP4 區塊的編碼工作</span><span class="sxs-lookup"><span data-stu-id="e5873-104">Create an encoding task that generates fMP4 chunks</span></span>

## <a name="overview"></a><span data-ttu-id="e5873-105">概觀</span><span class="sxs-lookup"><span data-stu-id="e5873-105">Overview</span></span>

<span data-ttu-id="e5873-106">本主題說明如何產生的編碼工作 toocreate 分散 MP4 (fMP4) 區塊，而不是 ISO MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="e5873-106">This topic shows how toocreate an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span></span> <span data-ttu-id="e5873-107">toogenerate fMP4 區塊，使用 hello**媒體編碼器標準**或**媒體編碼器高階工作流程**編碼工作，以及指定的編碼器 toocreate **AssetFormatOption.AdaptiveStreaming**選項，此程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="e5873-107">toogenerate fMP4 chunks, use hello **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder toocreate an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span></span>  
    
    task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks", 
            options: AssetCreationOptions.None, 
            formatOption: AssetFormatOption.AdaptiveStreaming);


## <span data-ttu-id="e5873-108"><a id="encoding_with_dotnet"></a>使用媒體服務 .NET SDK 進行編碼</span><span class="sxs-lookup"><span data-stu-id="e5873-108"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="e5873-109">hello，下列程式碼範例會使用 Media Services.NET SDK tooperform hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="e5873-109">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="e5873-110">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="e5873-110">Create an encoding job.</span></span>
- <span data-ttu-id="e5873-111">取得參考 toohello**媒體編碼器標準**編碼器。</span><span class="sxs-lookup"><span data-stu-id="e5873-111">Get a reference toohello **Media Encoder Standard** encoder.</span></span>
- <span data-ttu-id="e5873-112">加入的編碼工作 toohello 工作，並指定 toouse hello**彈性資料流**預設。</span><span class="sxs-lookup"><span data-stu-id="e5873-112">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="e5873-113">建立將包含 fMP4 區塊和 .ism 檔案的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="e5873-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span></span>
- <span data-ttu-id="e5873-114">加入事件處理常式 toocheck hello 工作進度。</span><span class="sxs-lookup"><span data-stu-id="e5873-114">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="e5873-115">送出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="e5873-115">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e5873-116">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="e5873-116">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e5873-117">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="e5873-117">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="e5873-118">範例</span><span class="sxs-lookup"><span data-stu-id="e5873-118">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreaming
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
            // It is also specified toouse AssetFormatOption.AdaptiveStreaming, 
            // which means hello output asset will contain fMP4 chunks.

            task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks",
            options: AssetCreationOptions.None,
            formatOption: AssetFormatOption.AdaptiveStreaming);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="e5873-119">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e5873-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e5873-120">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e5873-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="e5873-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e5873-121">See Also</span></span>
[<span data-ttu-id="e5873-122">媒體服務編碼概觀</span><span class="sxs-lookup"><span data-stu-id="e5873-122">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

