---
title: "跨多個儲存體帳戶管理媒體服務資產 | Microsoft Docs"
description: "此文件指引您如何管理跨多個儲存體帳戶的媒體服務資產。"
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
ms.openlocfilehash: 0b407c3b092fd2c706775154cee3164a9869315a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="55abc-103">跨多個儲存體帳戶管理媒體服務資產</span><span class="sxs-lookup"><span data-stu-id="55abc-103">Managing Media Services Assets across Multiple Storage Accounts</span></span>
<span data-ttu-id="55abc-104">從 Microsoft Azure 媒體服務 2.2 版起，您可以將多個儲存體帳戶附加至單一媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="55abc-104">Starting with Microsoft Azure Media Services 2.2, you can attach multiple storage accounts to a single Media Services account.</span></span> <span data-ttu-id="55abc-105">將多個儲存體帳戶附加到媒體服務帳戶的能力提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="55abc-105">Ability to attach multiple storage accounts to a Media Services account provides the following benefits:</span></span>

* <span data-ttu-id="55abc-106">在多個儲存體帳戶之間平衡您資產的負載。</span><span class="sxs-lookup"><span data-stu-id="55abc-106">Load balancing your assets across multiple storage accounts.</span></span>
* <span data-ttu-id="55abc-107">調整媒體服務進行大量的內容處理 (因為目前單一儲存體帳戶的最大上限為 500 TB)。</span><span class="sxs-lookup"><span data-stu-id="55abc-107">Scaling Media Services for large amounts of content processing (as currently a single storage account has a max limit of 500 TB).</span></span> 

<span data-ttu-id="55abc-108">本主題將示範如何使用 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/media/mediaservice) 和 [Powershell](/powershell/module/azurerm.media)，將多個儲存體帳戶附加到媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="55abc-108">This topic demonstrates how to attach multiple storage accounts to a Media Services account using [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media).</span></span> <span data-ttu-id="55abc-109">同時也會示範如何在使用媒體服務 SDK 建立資產時，指定不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55abc-109">It also shows how to specify different storage accounts when creating assets using the Media Services SDK.</span></span> 

## <a name="considerations"></a><span data-ttu-id="55abc-110">考量</span><span class="sxs-lookup"><span data-stu-id="55abc-110">Considerations</span></span>
<span data-ttu-id="55abc-111">當您在媒體服務帳戶中附加多個儲存體帳戶時，適用下列考量事項：</span><span class="sxs-lookup"><span data-stu-id="55abc-111">When attaching multiple storage accounts to your Media Services account, the following considerations apply:</span></span>

* <span data-ttu-id="55abc-112">所有附加到媒體服務帳戶的儲存體帳戶必須與該媒體服務帳戶位於相同的資料中心。</span><span class="sxs-lookup"><span data-stu-id="55abc-112">All storage accounts attached to a Media Services account must be in the same data center as the Media Services account.</span></span>
* <span data-ttu-id="55abc-113">目前，一旦儲存體帳戶附加到指定的媒體服務帳戶後，將無法卸離。</span><span class="sxs-lookup"><span data-stu-id="55abc-113">Currently, once a storage account is attached to the specified Media Services account, it cannot be detached.</span></span>
* <span data-ttu-id="55abc-114">在建立媒體服務帳戶時指出的儲存體帳戶，即為主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55abc-114">Primary storage account is the one indicated during Media Services account creation time.</span></span> <span data-ttu-id="55abc-115">目前您無法變更預設的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55abc-115">Currently, you cannot change the default storage account.</span></span> 
* <span data-ttu-id="55abc-116">目前，如果您要新增非經常性儲存體帳戶到 AMS 帳戶，儲存體帳戶必須是 Blob 類型，並且設定為非主要。</span><span class="sxs-lookup"><span data-stu-id="55abc-116">Currently, if you want to add a Cool Storage account to the AMS account, the storage account must be a Blob type and set to non-primary.</span></span>

<span data-ttu-id="55abc-117">其他考量：</span><span class="sxs-lookup"><span data-stu-id="55abc-117">Other considerations:</span></span>

<span data-ttu-id="55abc-118">建置串流內容的 URL (例如，http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters) 時，媒體服務會使用 **IAssetFile.Name** 屬性的值。基於這個理由，不允許 percent-encoding。</span><span class="sxs-lookup"><span data-stu-id="55abc-118">Media Services uses the value of the **IAssetFile.Name** property when building URLs for the streaming content (for example, http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="55abc-119">Name 屬性的值不能有[下列任何百分比編碼保留字元：](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters)：!*'();:@&=+$,/?%#[]"。</span><span class="sxs-lookup"><span data-stu-id="55abc-119">The value of the Name property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="55abc-120">此外，只能有一個 ‘.’</span><span class="sxs-lookup"><span data-stu-id="55abc-120">Also, there can only be one ‘.’</span></span> <span data-ttu-id="55abc-121">在檔案名稱的副檔名。</span><span class="sxs-lookup"><span data-stu-id="55abc-121">for the file name extension.</span></span>

## <a name="to-attach-storage-accounts"></a><span data-ttu-id="55abc-122">附加儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="55abc-122">To attach storage accounts</span></span>  

<span data-ttu-id="55abc-123">若要將儲存體帳戶附加到 AMS 帳戶，請使用 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/media/mediaservice) 和 [Powershell](/powershell/module/azurerm.media)，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="55abc-123">To attach storage accounts to your AMS account, use [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media), as shown in the following example.</span></span>

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

### <a name="support-for-cool-storage"></a><span data-ttu-id="55abc-124">非經常性儲存空間的支援</span><span class="sxs-lookup"><span data-stu-id="55abc-124">Support for Cool Storage</span></span>

<span data-ttu-id="55abc-125">目前，如果您要新增非經常性儲存體帳戶到 AMS 帳戶，儲存體帳戶必須是 Blob 類型，並且設定為非主要。</span><span class="sxs-lookup"><span data-stu-id="55abc-125">Currently, if you want to add a Cool Storage account to the AMS account, the storage account must be a Blob type and set to non-primary.</span></span>

## <a name="to-manage-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="55abc-126">管理跨多個儲存體帳戶的媒體服務資產</span><span class="sxs-lookup"><span data-stu-id="55abc-126">To manage Media Services assets across multiple Storage Accounts</span></span>
<span data-ttu-id="55abc-127">下列程式碼會使用最新的媒體服務 SDK，執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="55abc-127">The following code uses the latest Media Services SDK to perform the following tasks:</span></span>

1. <span data-ttu-id="55abc-128">顯示所有與指定媒體服務帳戶相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55abc-128">Display all the storage accounts associated with the specified Media Services account.</span></span>
2. <span data-ttu-id="55abc-129">擷取預設儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="55abc-129">Retrieve the name of the default storage account.</span></span>
3. <span data-ttu-id="55abc-130">在預設儲存體帳戶中建立新資產。</span><span class="sxs-lookup"><span data-stu-id="55abc-130">Create a new asset in the default storage account.</span></span>
4. <span data-ttu-id="55abc-131">在指定的儲存體帳戶內建立編碼工作的輸出資產。</span><span class="sxs-lookup"><span data-stu-id="55abc-131">Create an output asset of the encoding job in the specified storage account.</span></span>
   
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
        // Location of the media file that you want to encode. 
        private static readonly string _singleInputFilePath =
            Path.GetFullPath(@"../..\supportFiles\multifile\interview2.wmv");

        // Read values from the App.config file.
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

            // Display the storage accounts associated with 
            // the specified Media Services account:
            foreach (var sa in _context.StorageAccounts)
                Console.WriteLine(sa.Name);

            // Retrieve the name of the default storage account.
            var defaultStorageName = _context.StorageAccounts.Where(s => s.IsDefault == true).FirstOrDefault();
            Console.WriteLine("Name: {0}", defaultStorageName.Name);
            Console.WriteLine("IsDefault: {0}", defaultStorageName.IsDefault);

            // Retrieve the name of a storage account that is not the default one.
            var notDefaultStroageName = _context.StorageAccounts.Where(s => s.IsDefault == false).FirstOrDefault();
            Console.WriteLine("Name: {0}", notDefaultStroageName.Name);
            Console.WriteLine("IsDefault: {0}", notDefaultStroageName.IsDefault);

            // Create the original asset in the default storage account.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.None,
                defaultStorageName.Name, _singleInputFilePath);
            Console.WriteLine("Created the asset in the {0} storage account", asset.StorageAccountName);

            // Create an output asset of the encoding job in the other storage account.
            IAsset outputAsset = CreateEncodingJob(asset, notDefaultStroageName.Name, _singleInputFilePath);
            if (outputAsset != null)
                Console.WriteLine("Created the output asset in the {0} storage account", outputAsset.StorageAccountName);

        }

        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string storageName, string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();

            // If you are creating an asset in the default storage account, you can omit the StorageName parameter.
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
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.ProtectedConfiguration);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset", storageName,
                AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();

            // Get an updated job reference.
            job = GetJob(job.Id);

            // If job state is Error the event handling 
            // method for job progress should log errors.  Here we check 
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                Console.WriteLine("\nExiting method due to job error.");
                return null;
            }

            // Get a reference to the output asset from the job.
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
            // Use a Linq select query to get an updated 
            // reference by Id. 
            var jobInstance =
                from j in _context.Jobs
                where j.Id == jobId
                select j;
            // Return the job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }
    }
}
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="55abc-132">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="55abc-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="55abc-133">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="55abc-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

