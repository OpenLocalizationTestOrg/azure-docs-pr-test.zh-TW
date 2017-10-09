---
title: "aaaManaging 跨多個儲存體帳戶的媒體服務資產 |Microsoft 文件"
description: "此文章提供指引 toomanage media services 資產跨多個儲存體帳戶的方式。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4e4a9ec3-8ddb-4938-aec1-d7172d3db858
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 812f290d91f8d739be1c88db2b612767fda96220
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="93813-103">跨多個儲存體帳戶管理媒體服務資產</span><span class="sxs-lookup"><span data-stu-id="93813-103">Managing Media Services Assets across Multiple Storage Accounts</span></span>
<span data-ttu-id="93813-104">從 Microsoft Azure 媒體服務 2.2 開始，您可以附加多個儲存體帳戶 tooa 單一 Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93813-104">Starting with Microsoft Azure Media Services 2.2, you can attach multiple storage accounts tooa single Media Services account.</span></span> <span data-ttu-id="93813-105">多個儲存體帳戶 tooa Media Services 帳戶會提供下列 hello 能力 tooattach 優點：</span><span class="sxs-lookup"><span data-stu-id="93813-105">Ability tooattach multiple storage accounts tooa Media Services account provides hello following benefits:</span></span>

* <span data-ttu-id="93813-106">在多個儲存體帳戶之間平衡您資產的負載。</span><span class="sxs-lookup"><span data-stu-id="93813-106">Load balancing your assets across multiple storage accounts.</span></span>
* <span data-ttu-id="93813-107">調整媒體服務進行大量的內容處理 (因為目前單一儲存體帳戶的最大上限為 500 TB)。</span><span class="sxs-lookup"><span data-stu-id="93813-107">Scaling Media Services for large amounts of content processing (as currently a single storage account has a max limit of 500 TB).</span></span> 

<span data-ttu-id="93813-108">本主題示範如何 tooattach 多個儲存體帳戶的 tooa 媒體服務帳戶使用[Azure 資源管理員 Api](https://docs.microsoft.com/rest/api/media/mediaservice)和[Powershell](/powershell/module/azurerm.media)。</span><span class="sxs-lookup"><span data-stu-id="93813-108">This topic demonstrates how tooattach multiple storage accounts tooa Media Services account using [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media).</span></span> <span data-ttu-id="93813-109">它也會示範如何 toospecify 不同的儲存體帳戶時建立使用 hello Media Services SDK 的資產。</span><span class="sxs-lookup"><span data-stu-id="93813-109">It also shows how toospecify different storage accounts when creating assets using hello Media Services SDK.</span></span> 

## <a name="considerations"></a><span data-ttu-id="93813-110">考量</span><span class="sxs-lookup"><span data-stu-id="93813-110">Considerations</span></span>
<span data-ttu-id="93813-111">當附加多個儲存體帳戶 tooyour Media Services 帳戶，hello 適用下列考量：</span><span class="sxs-lookup"><span data-stu-id="93813-111">When attaching multiple storage accounts tooyour Media Services account, hello following considerations apply:</span></span>

* <span data-ttu-id="93813-112">所有儲存體帳戶附加的 tooa 媒體服務帳戶必須在 hello 與 hello Media Services 帳戶的相同資料中心。</span><span class="sxs-lookup"><span data-stu-id="93813-112">All storage accounts attached tooa Media Services account must be in hello same data center as hello Media Services account.</span></span>
* <span data-ttu-id="93813-113">目前，一旦儲存體帳戶附加 toohello 指定 Media Services 帳戶，無法卸離。</span><span class="sxs-lookup"><span data-stu-id="93813-113">Currently, once a storage account is attached toohello specified Media Services account, it cannot be detached.</span></span>
* <span data-ttu-id="93813-114">一個 Media Services 帳戶建立期間指定的 hello 主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="93813-114">Primary storage account is hello one indicated during Media Services account creation time.</span></span> <span data-ttu-id="93813-115">目前，您無法變更 hello 預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="93813-115">Currently, you cannot change hello default storage account.</span></span> 
* <span data-ttu-id="93813-116">目前，如果您想 tooadd 酷炫的儲存體帳戶 toohello AMS 帳戶，hello 儲存體帳戶必須是 Blob 類型，並將 toonon 主要。</span><span class="sxs-lookup"><span data-stu-id="93813-116">Currently, if you want tooadd a Cool Storage account toohello AMS account, hello storage account must be a Blob type and set toonon-primary.</span></span>

<span data-ttu-id="93813-117">其他考量：</span><span class="sxs-lookup"><span data-stu-id="93813-117">Other considerations:</span></span>

<span data-ttu-id="93813-118">Media Services 會使用 hello hello 值**IAssetFile.Name**屬性時建置串流處理內容 (例如，http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/ hello 的 UrlstreamingParameters。)基於這個理由，不允許 percent-encoding。</span><span class="sxs-lookup"><span data-stu-id="93813-118">Media Services uses hello value of hello **IAssetFile.Name** property when building URLs for hello streaming content (for example, http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="93813-119">hello hello 名稱屬性的值不能有 hello 下列任何一項[百分比編碼的保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ！ *' （);: @& = + $，/？ %# []"。</span><span class="sxs-lookup"><span data-stu-id="93813-119">hello value of hello Name property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="93813-120">此外，只能有一個 ‘.’</span><span class="sxs-lookup"><span data-stu-id="93813-120">Also, there can only be one ‘.’</span></span> <span data-ttu-id="93813-121">hello 檔案名稱副檔名。</span><span class="sxs-lookup"><span data-stu-id="93813-121">for hello file name extension.</span></span>

## <a name="tooattach-storage-accounts"></a><span data-ttu-id="93813-122">tooattach 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="93813-122">tooattach storage accounts</span></span>  

<span data-ttu-id="93813-123">tooattach 儲存體帳戶 tooyour AMS 帳戶，使用[Azure 資源管理員 Api](https://docs.microsoft.com/rest/api/media/mediaservice)和[Powershell](/powershell/module/azurerm.media)hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="93813-123">tooattach storage accounts tooyour AMS account, use [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media), as shown in hello following example.</span></span>

    $regionName = "West US"
    $subscriptionId = " xxxxxxxx-xxxx-xxxx-xxxx- xxxxxxxxxxxx "
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccount1Name = "skystorage1"
    $storageAccount2Name = "skystorage2"
    $storageAccount1Id = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccount1Name"
    $storageAccount2Id = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccount2Name"
    $storageAccount1 = New-AzureRmMediaServiceStorageConfig -StorageAccountId $storageAccount1Id -IsPrimary
    $storageAccount2 = New-AzureRmMediaServiceStorageConfig -StorageAccountId $storageAccount2Id
    $storageAccounts = @($storageAccount1, $storageAccount2)
    
    Set-AzureRmMediaService -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccounts $storageAccounts

### <a name="support-for-cool-storage"></a><span data-ttu-id="93813-124">非經常性儲存空間的支援</span><span class="sxs-lookup"><span data-stu-id="93813-124">Support for Cool Storage</span></span>

<span data-ttu-id="93813-125">目前，如果您想 tooadd 酷炫的儲存體帳戶 toohello AMS 帳戶，hello 儲存體帳戶必須是 Blob 類型，並將 toonon 主要。</span><span class="sxs-lookup"><span data-stu-id="93813-125">Currently, if you want tooadd a Cool Storage account toohello AMS account, hello storage account must be a Blob type and set toonon-primary.</span></span>

## <a name="toomanage-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="93813-126">跨多個儲存體帳戶的 toomanage Media Services 資產</span><span class="sxs-lookup"><span data-stu-id="93813-126">toomanage Media Services assets across multiple Storage Accounts</span></span>
<span data-ttu-id="93813-127">下列程式碼的 hello 使用 hello 最新 Media Services SDK tooperform hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="93813-127">hello following code uses hello latest Media Services SDK tooperform hello following tasks:</span></span>

1. <span data-ttu-id="93813-128">顯示所有 hello 儲存體帳戶相關都聯 hello 指定 Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93813-128">Display all hello storage accounts associated with hello specified Media Services account.</span></span>
2. <span data-ttu-id="93813-129">擷取 hello hello 預設儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="93813-129">Retrieve hello name of hello default storage account.</span></span>
3. <span data-ttu-id="93813-130">Hello 預設儲存體帳戶中建立新資產。</span><span class="sxs-lookup"><span data-stu-id="93813-130">Create a new asset in hello default storage account.</span></span>
4. <span data-ttu-id="93813-131">建立 hello 編碼的輸出資產中 hello 工作指定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="93813-131">Create an output asset of hello encoding job in hello specified storage account.</span></span>
   
```
using Microsoft.WindowsAzure.MediaServices.Client;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace MultipleStorageAccounts
{
    class Program
    {
        // Location of hello media file that you want tooencode. 
        private static readonly string _singleInputFilePath =
            Path.GetFullPath(@"../..\supportFiles\multifile\interview2.wmv");

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Display hello storage accounts associated with 
            // hello specified Media Services account:
            foreach (var sa in _context.StorageAccounts)
                Console.WriteLine(sa.Name);

            // Retrieve hello name of hello default storage account.
            var defaultStorageName = _context.StorageAccounts.Where(s => s.IsDefault == true).FirstOrDefault();
            Console.WriteLine("Name: {0}", defaultStorageName.Name);
            Console.WriteLine("IsDefault: {0}", defaultStorageName.IsDefault);

            // Retrieve hello name of a storage account that is not hello default one.
            var notDefaultStroageName = _context.StorageAccounts.Where(s => s.IsDefault == false).FirstOrDefault();
            Console.WriteLine("Name: {0}", notDefaultStroageName.Name);
            Console.WriteLine("IsDefault: {0}", notDefaultStroageName.IsDefault);

            // Create hello original asset in hello default storage account.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.None,
                defaultStorageName.Name, _singleInputFilePath);
            Console.WriteLine("Created hello asset in hello {0} storage account", asset.StorageAccountName);

            // Create an output asset of hello encoding job in hello other storage account.
            IAsset outputAsset = CreateEncodingJob(asset, notDefaultStroageName.Name, _singleInputFilePath);
            if (outputAsset != null)
                Console.WriteLine("Created hello output asset in hello {0} storage account", outputAsset.StorageAccountName);

        }

        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string storageName, string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();

            // If you are creating an asset in hello default storage account, you can omit hello StorageName parameter.
            var asset = _context.Assets.Create(assetName, storageName, assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);

            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return asset;
        }

        static IAsset CreateEncodingJob(IAsset asset, string storageName, string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My encoding job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.ProtectedConfiguration);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset", storageName,
                AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();

            // Get an updated job reference.
            job = GetJob(job.Id);

            // If job state is Error hello event handling 
            // method for job progress should log errors.  Here we check 
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                Console.WriteLine("\nExiting method due toojob error.");
                return null;
            }

            // Get a reference toohello output asset from hello job.
            IAsset outputAsset = job.OutputMediaAssets[0];

            return outputAsset;
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        private static void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("********************");
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine("Please wait while local tasks or downloads complete...");
                    Console.WriteLine("********************");
                    Console.WriteLine();
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
                    Console.WriteLine("An error occurred in {0}", job.Id);
                    break;
                default:
                    break;
            }
        }

        static IJob GetJob(string jobId)
        {
            // Use a Linq select query tooget an updated 
            // reference by Id. 
            var jobInstance =
                from j in _context.Jobs
                where j.Id == jobId
                select j;
            // Return hello job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }
    }
}
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="93813-132">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="93813-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="93813-133">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="93813-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

