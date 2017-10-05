---
title: "開發具有媒體服務的 Azure Functions"
description: "本主題說明如何使用 Azure 入口網站開始開發具有媒體服務的 Azure Functions。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a>開發具有媒體服務的 Azure Functions

本主題說明如何開始建立使用媒體服務的 Azure Functions。 本主題中定義的 Azure Function 會針對新的 MP4 檔案監視名為 **input** 的儲存體帳戶容器。 一旦將檔案拖放至儲存體容器之後，blob 觸發程序將會執行此函式。

如果您想要瀏覽及部署使用 Azure 媒體服務的現有 Azure Functions，請參閱[媒體服務 Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)。 此存放庫包含的範例會使用媒體服務來顯示與直接從 Blob 儲存體擷取內容、進行編碼，再將內容寫回 Blob 儲存體相關的工作流程。 此存放庫也包含如何透過 Webhook 和 Azure 佇列監視作業通知的範例。 您也可以根據[媒體服務 Azure Functions (英文)](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) 儲存機制中的範例來開發您的函式。 若要部署函式，請按 [部署至 Azure] 按鈕。

## <a name="prerequisites"></a>必要條件

- 您必須先具備有效的 Azure 帳戶，才可以建立第一個函式。 如果您還沒有 Azure 帳戶， [可以使用免費帳戶](https://azure.microsoft.com/free/)。
- 如果您要建立會對 Azure 媒體服務 (AMS) 帳戶執行動作或是會接聽媒體服務所傳送之事件的 Azure Functions，您應該建立 AMS 帳戶，如[這裡](media-services-portal-create-account.md)所述。
- 了解[如何使用 Azure Functions](../azure-functions/functions-overview.md)。 此外，請參閱：
    - [Azure Functions HTTP 和 Webhook 繫結](../azure-functions/functions-triggers-bindings.md)
    - [如何設定 Azure Functions 應用程式設定](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>考量

-  在 Consumption 方案下執行的 Azure Functions 有 5 分鐘的逾時限制。

## <a name="create-a-function-app"></a>建立函數應用程式

1. 移至 [Azure 入口網站](http://portal.azure.com) ，然後以您的 Azure 帳戶登入。
2. 如[這裡](../azure-functions/functions-create-function-app-portal.md)所述建立函式應用程式。

>[!NOTE]
> 您在 **StorageConnection** 環境變數中指定的儲存體帳戶 (請見上一個步驟) 應該與您的應用程式位於相同的區域。

## <a name="configure-function-app-settings"></a>設定函式應用程式設定

開發媒體服務函式時，您可以很方便地新增要在整個函式中使用的環境變數。 若要設定應用程式設定，請按一下 [設定應用程式設定] 連結。 如需詳細資訊，請參閱[如何設定 Azure Function 應用程式設定](../azure-functions/functions-how-to-use-azure-function-app-settings.md)。 

例如：

![設定](./media/media-services-azure-functions/media-services-azure-functions001.png)

本文中所定義的函式會假設您在應用程式設定中具有下列環境變數：

**AMSAccount**：AMS 帳戶名稱 (例如 testams)

**AMSKey**：AMS 帳戶金鑰 (例如 IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)

**MediaServicesStorageAccountName**：儲存體帳戶名稱 (例如 testamsstorage)

**MediaServicesStorageAccountKey**：儲存體帳戶金鑰 (例如 xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)

**StorageConnection**：儲存體連接 (例如 DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)

## <a name="create-a-function"></a>建立函式

部署函式應用程式之後，您可以在**應用程式服務** Azure Functions 中找到它。

1. 選取您的函式應用程式，然後按一下 [新增函式]。
2. 選擇 [C#] 語言和 [資料處理] 案例。
3. 選擇 [BlobTrigger] 範本。 每次將 blob 上傳到 **input** 容器時，將會觸發此函式。 **input** 名稱指定於下一個步驟的 **Path** 中。

    ![檔案](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. 一旦您選取 **BlobTrigger** 之後，頁面上將出現更多控制項。

    ![檔案](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. 按一下 [建立] 。 


## <a name="files"></a>檔案

您的 Azure 函式會與本節所述的程式碼檔案和其他檔案相關聯。 根據預設，函式會與 **function.json** 和 **run.csx** (C#) 檔案相關聯。 您必須新增 **project.json** 檔案。 本節其餘部分會說明這些檔案的定義。

![檔案](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>function.json

function.json 檔案會定義函式繫結和其他組態設定。 執行階段使用此檔案來判斷要監視的事件，以及如何傳入資料並從函式執行傳回資料。 如需詳細資訊，請參閱 [Azure Functions HTTP 和 Webhook 繫結](../azure-functions/functions-reference.md#function-code)。

>[!NOTE]
>將 **disabled** 屬性設定為 **true** 以防止函式執行。 


以下是 **function.json** 檔案的範例。

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a>project.json

project.json 檔案包含相依性。 以下是 **project.json** 檔案的範例，其中包含來自 Nuget 的必要 .NET Azure 媒體服務封裝。 請注意，版本號碼將隨著對封裝的最新更新而不同，因此您應該確認最新版本。 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a>run.csx

這是您的函式適用的 C# 程式碼。  以下定義的函式會針對新的 MP4 檔案監視名為 **input** (指定於路徑中) 的儲存體帳戶。 一旦將檔案拖放至儲存體容器之後，blob 觸發程序將會執行此函式。
    
本節中定義的範例會示範 

1. 如何將資產內嵌到媒體服務帳戶 (藉由將 blob 複製到 AMS 資產)，以及 
2. 如何提交編碼作業，該作業會使用媒體編碼器標準的「彈性資料流」預設。

在真實案例中，您很可能想要追蹤作業進度，然後發佈編碼的資產。 如需詳細資訊，請參閱[使用 Azure WebHook 監視媒體服務作業通知](media-services-dotnet-check-job-progress-with-webhooks.md)。 如需詳細資訊，請參閱[媒體服務 Azure Functions (英文)](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)。  

當您完成定義之後，按一下 [儲存並執行]。

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
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


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get the destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of the destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a>測試您的函式

若要測試您的函式，您需要將 MP4 檔案上傳到您在連接字串中指定之儲存體帳戶的 **input** 容器。  

## <a name="next-step"></a>後續步驟

現在，您可以開始開發媒體服務應用程式。 
 
如需使用 Azure Functions 和 Logic Apps 搭配 Azure 媒體服務來建立自訂內容建立工作流程的詳細資訊和完整範例/解決方案，請參閱 [GitHub 上的媒體服務 .NET 功能整合範例 (英文)](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)。

另請參閱[使用 Azure WebHook 監視 .NET 的媒體服務作業通知](media-services-dotnet-check-job-progress-with-webhooks.md)。 

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

