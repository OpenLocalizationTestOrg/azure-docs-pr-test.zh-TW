---
title: "Azure Media Services 進行資料流處理的 aaaImplement 容錯移轉 |Microsoft 文件"
description: "本主題說明如何 tooimplement 容錯移轉的串流處理案例。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fc45d849-eb0d-4739-ae91-0ff648113445
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: ade0bace57f35ab3ed855d3a98f743e08da4f324
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-failover-streaming-with-azure-media-services"></a>使用 Azure 媒體服務實作容錯移轉串流

本逐步解說示範如何從一個資產到另一個隨選串流順序 toohandle 備援 toocopy 內容 (blob)。 這個案例是如果您想透過 Azure 內容傳遞網路 toofail 向上 tooset 之間兩個資料中心，在一個資料中心中斷時很有用。 本逐步解說會使用 Azure Media Services SDK hello、 hello Azure 媒體服務 REST API 和 hello Azure 儲存體 SDK toodemonstrate hello 下列工作：

1. 在「資料中心 A」中設定媒體服務帳戶。
2. 將夾層檔上傳到來源資產。
3. Hello 資產編碼為多位元的速率 MP4 檔案。 
4. 建立唯讀的共用存取簽章定位器。 這是 hello 來源資產 toohave 讀取權限 toohello 容器 hello 與 hello 來源資產相關聯的儲存體帳戶中。
5. 收到 hello hello 先前步驟中建立的唯讀共用的存取簽章定位器 hello hello 來源資產容器名稱。 這是必要的複製 （hello 主題稍後說明）。 儲存體帳戶之間的 blob
6. 建立原始定位器以建立編碼工作的 hello hello 資產。 

然後，toohandle hello 容錯移轉：

1. 在「資料中心 B」中設定媒體服務帳戶。
2. Hello 目標 Media Services 帳戶中建立目標空白的資產。
3. 建立寫入共用存取簽章定位器。 這是 hello 目標空白資產 toohave 寫入權限 toohello 容器 hello 目標資產相關聯的 hello 目標儲存體帳戶中。
4. 使用 「 資料中心 A"中的 hello 來源儲存體帳戶與 「 資料中心 B 」 中的 hello 目標儲存體帳戶之間的 hello Azure 儲存體 SDK toocopy blob （資產檔案） 這些儲存體帳戶設定為與感興趣的 hello 資產相關聯。
5. 建立了與 hello 目標資產複製的 toohello 目標 blob 容器的 blob （資產檔案） 的關聯。 
6. 建立原始定位器以 「 資料中心 B"中的 hello 資產，並指定所產生的 「 資料中心 A 」 中的 hello 資產 hello 定位器識別碼

這讓 hello hello 相對路徑的 hello Url 所在的串流 Url hello （只有 hello 基底 Url 會不同）。 

然後，toohandle 任何中斷時，您可以建立內容傳遞網路之上這些原始定位器。 

hello 下列考量適用於：

* hello Media Services SDK 目前版本不支援以程式設計方式產生 IAssetFile 資訊會與資產檔案相關聯的資產。 請改用 hello CreateFileInfos 媒體服務 REST API toodo 這。 
* （因為 hello 加密金鑰是在這兩個媒體服務帳戶不同），儲存體加密資產 (AssetCreationOptions.StorageEncrypted) 不支援複寫。 
* 如果您想 tootake 使用動態封裝，請確定將內容串流的端點要從中 toostream hello 處於 hello**執行**狀態。

> [!NOTE]
> 請考慮使用 hello Media Services[複寫器工具](http://replicator.codeplex.com/)做為資料流案例時，手動容錯移轉的替代 tooimplementing。 此工具可讓您 tooreplicate 資產跨兩個 Media Services 帳戶。
> 
> 

## <a name="prerequisites"></a>必要條件
* 在新的或現有的 Azure 訂用帳戶中有兩個媒體服務帳戶。 請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。
* 作業系統：Windows 7、Windows 2008 R2 或 Windows 8。
* .NET Framework 4.5 或 .NET Framework 4。
* Visual Studio 2010 SP1 或更新版本 (Professional, Premium、Ultimate 或 Express)。

## <a name="set-up-your-project"></a>設定專案
在本節中，您會建立 C# Console Application 專案。

1. 使用 Visual Studio toocreate 包含 hello C# 主控台應用程式專案的新方案。 輸入**HandleRedundancyForOnDemandStreaming**的 hello 名稱，然後按一下**確定**。
2. 建立 hello **SupportFiles**上 hello 資料夾相同層級為 hello **HandleRedundancyForOnDemandStreaming.csproj**專案檔。 在 hello **SupportFiles**資料夾中，建立 hello **OutputFiles**和**MP4Files**資料夾。 將.mp4 檔案複製到 hello **MP4Files**資料夾。 (在此範例中，hello **BigBuckBunny.mp4**檔案使用。) 
3. 使用**Nuget** tooadd 參考 tooDLLs 相關 tooMedia 服務。 在 **Visual Studio 主要功能表**中，選取 [工具] > [Library Package Manager] > [Package Manager Console]。 在 [hello] 主控台視窗中，輸入**Install-package windowsazure.mediaservices**，然後按 Enter。
4. 新增此專案所需的其他參考：System.Configuration、System.Runtime.Serialization 和 System.Web。
5. 取代**使用**陳述式所加入 toohello **Programs.cs**檔案，根據預設，使用下列的 hello:
   
        using System;
        using System.Configuration;
        using System.Globalization;
        using System.IO;
        using System.Net;
        using System.Runtime.Serialization.Json;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using System.Web;
        using System.Xml;
        using System.Linq;
        using Microsoft.WindowsAzure;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using Microsoft.WindowsAzure.Storage.Auth;
6. 新增 hello **appSettings**區段 toohello **.config**檔案，並更新 hello 值根據您的媒體服務和儲存體金鑰和名稱值。 
   
        <appSettings>
          <add key="MediaServicesAccountNameSource" value="Media-Services-Account-Name-Source"/>
          <add key="MediaServicesAccountKeySource" value="Media-Services-Account-Key-Source"/>
          <add key="MediaServicesStorageAccountNameSource" value="Media-Services-Storage-Account-Name-Source"/>
          <add key="MediaServicesStorageAccountKeySource" value="Media-Services-Storage-Account-Key-Source"/>
          <add key="MediaServicesAccountNameTarget" value="Media-Services-Account-Name-Target" />
          <add key="MediaServicesAccountKeyTarget" value=" Media-Services-Account-Key-Target" />
          <add key="MediaServicesStorageAccountNameTarget" value=" Media-Services-Storage-Account-Name-Target" />
          <add key="MediaServicesStorageAccountKeyTarget" value=" Media-Services-Storage-Account-Key-Target" />
        </appSettings>

## <a name="add-code-that-handles-redundancy-for-on-demand-streaming"></a>新增可為隨選資料流處理備援的程式碼
在本節中，您可以建立 hello 能力 toohandle 備援。

1. 新增下列類別層級欄位 toohello Program 類別的 hello。
       
        // Read values from hello App.config file.
        private static readonly string MediaServicesAccountNameSource = ConfigurationManager.AppSettings["MediaServicesAccountNameSource"];
        private static readonly string MediaServicesAccountKeySource = ConfigurationManager.AppSettings["MediaServicesAccountKeySource"];
        private static readonly string StorageNameSource = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameSource"];
        private static readonly string StorageKeySource = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeySource"];
        
        private static readonly string MediaServicesAccountNameTarget = ConfigurationManager.AppSettings["MediaServicesAccountNameTarget"];
        private static readonly string MediaServicesAccountKeyTarget = ConfigurationManager.AppSettings["MediaServicesAccountKeyTarget"];
        private static readonly string StorageNameTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountNameTarget"];
        private static readonly string StorageKeyTarget = ConfigurationManager.AppSettings["MediaServicesStorageAccountKeyTarget"];
        
        // Base support files path.  Update this field toopoint toohello base path  
        // for hello local support files folder that you create. 
        private static readonly string SupportFiles = Path.GetFullPath(@"../..\SupportFiles");
        
        // Paths toosupport files (within hello above base path). 
        private static readonly string SingleInputMp4Path = Path.GetFullPath(SupportFiles + @"\MP4Files\BigBuckBunny.mp4");
        private static readonly string OutputFilesFolder = Path.GetFullPath(SupportFiles + @"\OutputFiles");
        
        // Class-level field used tookeep a reference toohello service context.
        static private CloudMediaContext _contextSource = null;
        static private CloudMediaContext _contextTarget = null;
        static private MediaServicesCredentials _cachedCredentialsSource = null;
        static private MediaServicesCredentials _cachedCredentialsTarget = null;

2. 取代下列其中一個 hello hello 預設 Main 方法定義。 從 Main 呼叫的方法定義會定義如下。
        
        static void Main(string[] args)
        {
            _cachedCredentialsSource = new MediaServicesCredentials(
                            MediaServicesAccountNameSource,
                            MediaServicesAccountKeySource);
        
            _cachedCredentialsTarget = new MediaServicesCredentials(
                            MediaServicesAccountNameTarget,
                            MediaServicesAccountKeyTarget);
        
            // Get server context.    
            _contextSource = new CloudMediaContext(_cachedCredentialsSource);
            _contextTarget = new CloudMediaContext(_cachedCredentialsTarget);
        
            IAsset assetSingleFile = CreateAssetAndUploadSingleFile(_contextSource,
                                        AssetCreationOptions.None,
                                        SingleInputMp4Path);
        
            IJob job = CreateEncodingJob(_contextSource, assetSingleFile);
        
            if (job.State != JobState.Error)
            {
                IAsset sourceOutputAsset = job.OutputMediaAssets[0];
                // Get hello locator for Smooth Streaming
                var sourceOriginLocator = GetStreamingOriginLocator(_contextSource, sourceOutputAsset);
        
                Console.WriteLine("Locator Id: {0}", sourceOriginLocator.Id);
                
                // 1.Create a read-only SAS locator for hello source asset toohave read access toohello container in hello source Storage account (associated with hello source Media Services account)
                var readSasLocator = GetSasReadLocator(_contextSource, sourceOutputAsset);
        
                // 2.Get hello container name of hello source asset from hello read-only SAS locator created in hello previous step
                string containerName = (new Uri(readSasLocator.Path)).Segments[1];
        
                // 3.Create a target empty asset in hello target Media Services account
                var targetAsset = CreateTargetEmptyAsset(_contextTarget, containerName);
        
                // 4.Create a write SAS locator for hello target empty asset toohave write access toohello container in hello target Storage account (associated with hello target Media Services account)
                ILocator writeSasLocator = CreateSasWriteLocator(_contextTarget, targetAsset);
        
                // Get asset container name.
                string targetContainerName = (new Uri(writeSasLocator.Path)).Segments[1];
        
                // 5.Copy hello blobs in hello source container (source asset) toohello target container (target empty asset)
                CopyBlobsFromDifferentStorage(containerName, targetContainerName, StorageNameSource, StorageKeySource, StorageNameTarget, StorageKeyTarget);
        
                // 6.Use hello CreateFileInfos Media Services REST API tooautomatically generate all hello IAssetFile’s for hello target asset. 
                //      This API call is not supported in hello current Media Services SDK for .NET. 
                CreateFileInfosForAssetWithRest(_contextTarget, targetAsset, MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget);
        
                // Check if hello AssetFiles are now  associated with hello asset.
                Console.WriteLine("Asset files assocated with hello {0} asset:", targetAsset.Name);
                foreach (var af in targetAsset.AssetFiles)
                {
                    Console.WriteLine(af.Name);
                }
        
                // 7.Copy hello Origin locator of hello source asset toohello target asset by using hello same Id
                var replicatedLocatorPath = CreateOriginLocatorWithRest(_contextTarget,
                            MediaServicesAccountNameTarget, MediaServicesAccountKeyTarget,
                            sourceOriginLocator.Id, targetAsset.Id);
        
                // Create a full URL toohello manifest file. Use this for playback
                // in streaming media clients. 
                string originalUrlForClientStreaming = sourceOriginLocator.Path + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Original Locator Path: {0}\n", originalUrlForClientStreaming);
        
                string replicatedUrlForClientStreaming = replicatedLocatorPath + GetPrimaryFile(sourceOutputAsset).Name + "/manifest";
        
                Console.WriteLine("Replicated Locator Path: {0}", replicatedUrlForClientStreaming);
        
                readSasLocator.Delete();
                writeSasLocator.Delete();
        }

3. 從 Main 呼叫下列方法定義的 hello。

    >[!NOTE]
    >對於不同的媒體服務原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。 您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同的日期和存取權限。 就地預定的 tooremain 對於較長的時間 （非上載原則） 的定位器原則，例如使用相同識別碼的 hello。 如需詳細資訊，請參閱[這個主題](media-services-dotnet-manage-entities.md#limit-access-policies)。

        public static IAsset CreateAssetAndUploadSingleFile(CloudMediaContext context,
                                                        AssetCreationOptions assetCreationOptions,
                                                        string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
   
            var asset = context.Assets.Create(assetName, assetCreationOptions);
   
            Console.WriteLine("Asset name: " + asset.Name);
   
            var fileName = Path.GetFileName(singleFilePath);
   
            var assetFile = asset.AssetFiles.Create(fileName);
   
            Console.WriteLine("Created assetFile {0}", assetFile.Name);
   
            Console.WriteLine("Upload {0}", assetFile.Name);
   
            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);
   
            return asset;
        }
   
        public static IJob CreateEncodingJob(CloudMediaContext context, IAsset asset)
        {
            // Declare a new job.
            IJob job = context.Jobs.Create("My encoding job");
   
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName(context,
                                                    "Media Encoder Standard");
   
            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.ProtectedConfiguration);
   
            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
   
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is in hello clear (unencrypted). 
            var outputAssetName = "OutputAsset_" + Guid.NewGuid();
            task.OutputAssets.AddNew(outputAssetName,
                AssetCreationOptions.None);
   
            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);
   
            // Launch hello job.
            job.Submit();
   
            // Optionally log job details. This displays basic job details
            // toohello console and saves them tooa JobDetails-{JobId}.txt file 
            // in your output folder.
            LogJobDetails(context, job.Id);
   
            // Check job execution and wait for job toofinish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();
   
            // Get an updated job reference.
            job = GetJob(context, job.Id);
   
            // Since we hello output asset contains a set of Smooth Streaming files,
            // set hello .ism file toobe hello primary file
            if (job.State != JobState.Error)
                SetPrimaryFile(job.OutputMediaAssets[0]);
   
            return job;
        }
   
        public static ILocator GetStreamingOriginLocator(CloudMediaContext context, IAsset assetToStream)
        {
            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 
            IAssetFile manifestFile = GetPrimaryFile(assetToStream);
   
            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
   
            IAccessPolicy policy = context.AccessPolicies.Create("Streaming policy",
                TimeSpan.FromDays(30),
                AccessPermissions.Read);
   
            // Create a locator toohello streaming content on an origin. 
            ILocator originLocator = context.Locators.CreateLocator(LocatorType.OnDemandOrigin,
                assetToStream,
                policy,
                DateTime.UtcNow.AddMinutes(-5));
   
            // Return hello locator. 
            return originLocator;
        }
   
        public static ILocator GetSasReadLocator(CloudMediaContext context, IAsset asset)
        {
            IAccessPolicy accessPolicy = context.AccessPolicies.Create("File Download Policy",
                TimeSpan.FromDays(30), AccessPermissions.Read);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, accessPolicy);
   
            return sasLocator;
        }
   
        public static ILocator CreateSasWriteLocator(CloudMediaContext context, IAsset asset)
        {
   
            IAccessPolicy writePolicy = context.AccessPolicies.Create("Write Policy",
                TimeSpan.FromDays(30), AccessPermissions.Write);
   
            ILocator sasLocator = context.Locators.CreateLocator(LocatorType.Sas,
                asset, writePolicy);
   
            return sasLocator;
        }
   
        public static IAsset CreateTargetEmptyAsset(CloudMediaContext context, string containerName)
        {
            // Create a new asset.
            IAsset assetToBeProcessed = context.Assets.Create(containerName,
                AssetCreationOptions.None);
   
            return assetToBeProcessed;
        }
   
        public static void CreateFileInfosForAssetWithRest(CloudMediaContext context, IAsset asset, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget)
        {
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                CreateFileInfos(apiServer, acsToken, asset.Id);
            }
        }
   
        public static string CreateOriginLocatorWithRest(CloudMediaContext context, string mediaServicesAccountNameTarget,
            string mediaServicesAccountKeyTarget, string locatorIdToReplicate, string targetAssetId)
        {
            //Make sure we are not asking for a duplicate:
            var locator = context.Locators.Where(l => l.Id == locatorIdToReplicate).FirstOrDefault();
            if (locator != null)
                return "";
   
            string locatorNewPath = "";
            string apiServer = "";
            string scope = "";
            string acsBaseAddress = "";
   
            string acsToken = GetAcsBearerToken(mediaServicesAccountNameTarget,
                                    mediaServicesAccountKeyTarget, scope, acsBaseAddress);
   
            if (!string.IsNullOrEmpty(acsToken))
            {
                var asset = context.Assets.Where(a => a.Id == targetAssetId).FirstOrDefault();
   
                // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
                var accessPolicy = context.AccessPolicies.Create("RestTest", TimeSpan.FromDays(100),
                                                                    AccessPermissions.Read);
                if (asset != null)
                {
                    string redirectedServiceUri = null;
   
                    var xmlResponse = CreateLocator(apiServer, out redirectedServiceUri, acsToken,
                                                                asset.Id, accessPolicy.Id,
                                                                (int)LocatorType.OnDemandOrigin,
                                                                DateTime.UtcNow.AddMinutes(-10), locatorIdToReplicate);
   
                    Console.WriteLine("Redirected to: " + redirectedServiceUri);
                    if (xmlResponse != null)
                    {
                        Console.WriteLine(String.Format("Locator Id: {0}",
                                                        xmlResponse.GetElementsByTagName("Id")[0].InnerText));
                        Console.WriteLine(String.Format("Locator Path: {0}",
                                xmlResponse.GetElementsByTagName("Path")[0].InnerText));

                        locatorNewPath = xmlResponse.GetElementsByTagName("Path")[0].InnerText;
                    }
                }
            }

            return locatorNewPath;
        }

        public static void SetPrimaryFile(IAsset asset)
        {

            var ismAssetFiles = asset.AssetFiles.ToList().
                        Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase))
                        .ToArray();

            if (ismAssetFiles.Count() != 1)
                throw new ArgumentException("hello asset should have only one, .ism file");

            ismAssetFiles.First().IsPrimary = true;
            ismAssetFiles.First().Update();
        }

        public static IAssetFile GetPrimaryFile(IAsset asset)
        {
            var theManifest =
                    from f in asset.AssetFiles
                    where f.Name.EndsWith(".ism")
                    select f;

            // Cast hello reference tooa true IAssetFile type. 
            IAssetFile manifestFile = theManifest.First();

            return manifestFile;
        }

        public static IAsset RefreshAsset(CloudMediaContext context, IAsset asset)
        {
            asset = context.Assets.Where(a => a.Id == asset.Id).FirstOrDefault();
            return asset;
        }

        public static void CopyBlobsFromDifferentStorage(string sourceContainerName, string targetContainerName,
                                            string srcAccountName, string srcAccountKey,
                                            string destAccountName, string destAccountKey)
        {
            var srcAccount = new CloudStorageAccount(new StorageCredentials(srcAccountName, srcAccountKey), true);
            var destAccount = new CloudStorageAccount(new StorageCredentials(destAccountName, destAccountKey), true);

            var cloudBlobClient = srcAccount.CreateCloudBlobClient();
            var targetBlobClient = destAccount.CreateCloudBlobClient();

            var sourceContainer = cloudBlobClient.GetContainerReference(sourceContainerName);
            var targetContainer = targetBlobClient.GetContainerReference(targetContainerName);
            targetContainer.CreateIfNotExists();

            string blobToken = sourceContainer.GetSharedAccessSignature(new SharedAccessBlobPolicy()
            {
                // Specify hello expiration time for hello signature.
                SharedAccessExpiryTime = DateTime.Now.AddDays(1),
                // Specify hello permissions granted by hello signature.
                Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read
            });

            foreach (var sourceBlob in sourceContainer.ListBlobs())
            {
                string fileName = (sourceBlob as ICloudBlob).Name;
                var sourceCloudBlob = sourceContainer.GetBlockBlobReference(fileName);
                sourceCloudBlob.FetchAttributes();

                if (sourceCloudBlob.Properties.Length > 0)
                {
                    // In Azure Media Services, hello files are stored as block blobs. 
                    // Page blobs are not supported by Azure Media Services.  
                    var destinationBlob = targetContainer.GetBlockBlobReference(fileName);
                    destinationBlob.StartCopyFromBlob(new Uri(sourceBlob.Uri.AbsoluteUri + blobToken));

                    while (true)
                    {
                        // hello StartCopyFromBlob is an async operation, 
                        // so we want toocheck if hello copy operation is completed before proceeding. 
                        // toodo that, we call FetchAttributes on hello blob and check hello CopyStatus. 
                        destinationBlob.FetchAttributes();
                        if (destinationBlob.CopyState.Status != CopyStatus.Pending)
                        {
                            break;
                        }
                        //It's still not completed. So wait for some time.
                        System.Threading.Thread.Sleep(1000);
                    }
                }

                Console.WriteLine(fileName);
            }

            Console.WriteLine("Done copying.");
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(CloudMediaContext context, string mediaProcessorName)
        {

            var processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        // This method is a handler for events that track job progress.   
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
                    LogJobStop(null, job.Id);
                    break;
                default:
                    break;
            }
        }

        private static void LogJobStop(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nThe job stopped due toocancellation or an error.");
            builder.AppendLine("***************************");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job State: " + job.State.ToString());
            builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
            // Log job errors if they exist.  
            if (job.State == JobState.Error)
            {
                builder.Append("Error Details: \n");
                foreach (ITask task in job.Tasks)
                {
                    foreach (ErrorDetail detail in task.ErrorDetails)
                    {
                        builder.AppendLine("  Task Id: " + task.Id);
                        builder.AppendLine("    Error Code: " + detail.Code);
                        builder.AppendLine("    Error Message: " + detail.Message + "\n");
                    }
                }
            }
            builder.AppendLine("***************************\n");
            // Write hello output tooa local file and toohello console. hello template 
            // for an error output file is:  JobStop-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        private static void LogJobDetails(CloudMediaContext context, string jobId)
        {
            StringBuilder builder = new StringBuilder();
            IJob job = GetJob(context, jobId);

            builder.AppendLine("\nJob ID: " + job.Id);
            builder.AppendLine("Job Name: " + job.Name);
            builder.AppendLine("Job submitted (client UTC time): " + DateTime.UtcNow.ToString());

            // Write hello output tooa local file and toohello console. hello template 
            // for an error output file is:  JobDetails-{JobId}.txt
            string outputFile = OutputFilesFolder + @"\JobDetails-" + JobIdAsFileName(job.Id) + ".txt";
            WriteToFile(outputFile, builder.ToString());
            Console.Write(builder.ToString());
        }

        // Replace ":" with "_" in Job id values so they can 
        // be used as log file names.  
        private static string JobIdAsFileName(string jobID)
        {
            return jobID.Replace(":", "_");
        }

        // Write method output toohello output files folder.
        private static void WriteToFile(string outFilePath, string fileContent)
        {
            StreamWriter sr = File.CreateText(outFilePath);
            sr.WriteLine(fileContent);
            sr.Close();
        }

        private static IJob GetJob(CloudMediaContext context, string jobId)
        {
            // Use a Linq select query tooget an updated 
            // reference by Id. 
            var jobInstance =
                from j in context.Jobs
                where j.Id == jobId
                select j;

            // Return hello job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }

        private static IAsset GetAsset(CloudMediaContext context, string assetId)
        {
            // Use a LINQ Select query tooget an asset.
            var assetInstance =
                from a in context.Assets
                where a.Id == assetId
                select a;

            // Reference hello asset as an IAsset.
            IAsset asset = assetInstance.FirstOrDefault();

            return asset;
        }

        public static void DeleteAllAssets(CloudMediaContext context)
        {
            // Loop through and delete all assets.
            foreach (IAsset asset in context.Assets)
            {
                DeleteLocatorsForAsset(context, asset);

                asset.Delete();
            }
        }

        public static void DeleteLocatorsForAsset(CloudMediaContext context, IAsset asset)
        {
            string assetId = asset.Id;
            var locators = from a in context.Locators
                            where a.AssetId == assetId
                            select a;
            foreach (var locator in locators)
            {
                Console.WriteLine("Deleting locator {0} for asset {1}", locator.Path, assetId);

                locator.Delete();
            }
        }

        public static void DeleteAccessPolicy(CloudMediaContext context, string existingPolicyId)
        {
            // toodelete a specific access policy, get a reference toohello policy.  
            // based on hello policy Id passed toohello method.
            var policyInstance =
                    from p in context.AccessPolicies
                    where p.Id == existingPolicyId
                    select p;

            IAccessPolicy policy = policyInstance.FirstOrDefault();

            policy.Delete();

        }

        //////////////////////////////////////////////////////
        /// hello following methods use REST calls.
        //////////////////////////////////////////////////////

        public static string GetAcsBearerToken(string clientId, string clientSecret, string scope, string accessControlServiceUri)
        {
            if (string.IsNullOrEmpty(clientId))
                throw new ArgumentNullException("clientId");

            if (string.IsNullOrEmpty(clientSecret))
                throw new ArgumentNullException("clientSecret");

            if (string.IsNullOrEmpty(scope))
            {
                scope = "urn:WindowsAzureMediaServices";
            }
            else if (!scope.ToLower().StartsWith("urn:"))
            {
                scope = "urn:" + scope;
            }

            if (string.IsNullOrEmpty(accessControlServiceUri))
            {
                accessControlServiceUri = "https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13";
            }
            else if (!accessControlServiceUri.ToLower().EndsWith("/v2/oauth2-13"))
            {
                accessControlServiceUri = accessControlServiceUri.TrimEnd('/') + "/v2/OAuth2-13";
            }

            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(accessControlServiceUri);
            request.Method = "POST";
            request.ContentType = "application/x-www-form-urlencoded";
            request.KeepAlive = true;
            string acsBearerToken = null;

            var requestBytes = Encoding.ASCII.GetBytes("grant_type=client_credentials&client_id=" +
                clientId + "&client_secret=" + HttpUtility.UrlEncode(clientSecret) +
                "&scope=" + HttpUtility.UrlEncode(scope));
            request.ContentLength = requestBytes.Length;

            var requestStream = request.GetRequestStream();
            requestStream.Write(requestBytes, 0, requestBytes.Length);
            requestStream.Close();

            var response = (HttpWebResponse)request.GetResponse();

            if (response.StatusCode == HttpStatusCode.OK)
            {
                using (Stream responseStream = response.GetResponseStream())
                {
                    using (StreamReader stream = new StreamReader(responseStream))
                    {
                        string responseString = stream.ReadToEnd();
                        var reader = JsonReaderWriterFactory.CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                            new XmlDictionaryReaderQuotas());

                        while (reader.Read())
                        {
                            if ((reader.Name == "access_token") && (reader.NodeType == XmlNodeType.Element))
                            {
                                if (reader.Read())
                                {
                                    acsBearerToken = reader.Value;
                                    break;
                                }
                            }
                        }
                    }
                }
            }

            return acsBearerToken;
        }

        public static XmlDocument CreateLocator(string mediaServicesApiServerUri,
                                                out string redirectedMediaServicesApiServerUri,
                                                string acsBearerToken, string assetId,
                                                string accessPolicyId, int locatorType,
                                                DateTime startTime, string locatorIdToReplicate = null,
                                                bool autoRedirect = true)
        {
            if (string.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (string.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (string.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");
            if (string.IsNullOrEmpty(accessPolicyId)) throw new ArgumentNullException("accessPolicyId");

            redirectedMediaServicesApiServerUri = null;
            XmlDocument xmlResponse = null;

            StringBuilder sb = new StringBuilder();
            sb.Append("{ \"AssetId\" : \"" + assetId + "\"");
            sb.Append(", \"AccessPolicyId\" : \"" + accessPolicyId + "\"");
            sb.Append(", \"Type\" : \"" + locatorType + "\"");
            if (startTime != DateTime.MinValue)
                sb.Append(", \"StartTime\" : \"" + startTime.ToString("G", CultureInfo.CreateSpecificCulture("en-us")) + "\"");
            if (!string.IsNullOrEmpty(locatorIdToReplicate))
                sb.Append(", \"Id\" : \"" + locatorIdToReplicate + "\"");
            sb.Append("}");

            string requestbody = sb.ToString();

            try
            {
                var request = GenerateRequest("POST", mediaServicesApiServerUri, "Locators",
                    null, acsBearerToken, requestbody);
                var response = (HttpWebResponse)request.GetResponse();

                switch (response.StatusCode)
                {
                    case HttpStatusCode.MovedPermanently:
                        //Recurse once with hello mediaServicesApiServerUri redirect Location:
                        if (autoRedirect)
                        {
                            redirectedMediaServicesApiServerUri = response.Headers["Location"];
                            string secondRedirection = null;
                            xmlResponse = CreateLocator(redirectedMediaServicesApiServerUri,
                                                        out secondRedirection, acsBearerToken,
                                                        assetId, accessPolicyId, locatorType,
                                                        startTime, locatorIdToReplicate, false);
                        }
                        else
                        {
                            Console.WriteLine("Redirection too{0} failed.",
                                mediaServicesApiServerUri);
                            return null;
                        }
                        break;
                    case HttpStatusCode.Created:
                        using (Stream responseStream = response.GetResponseStream())
                        {
                            using (StreamReader stream = new StreamReader(responseStream))
                            {
                                string responseString = stream.ReadToEnd();
                                var reader = JsonReaderWriterFactory.
                                    CreateJsonReader(Encoding.UTF8.GetBytes(responseString),
                                        new XmlDictionaryReaderQuotas());

                                xmlResponse = new XmlDocument();
                                reader.Read();
                                xmlResponse.LoadXml(reader.ReadInnerXml());
                            }
                        }
                        break;

                    default:
                        Console.WriteLine(response.StatusDescription);
                        break;
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }

            return xmlResponse;
        }

        public static void CreateFileInfos(string mediaServicesApiServerUri,
                                    string acsBearerToken,
                                    string assetId
                                    )
        {
            if (String.IsNullOrEmpty(mediaServicesApiServerUri))
            {
                mediaServicesApiServerUri = "https://media.windows.net/api/";
            }
            if (!mediaServicesApiServerUri.EndsWith("/"))
                mediaServicesApiServerUri = mediaServicesApiServerUri + "/";

            if (String.IsNullOrEmpty(acsBearerToken)) throw new ArgumentNullException("acsBearerToken");
            if (String.IsNullOrEmpty(assetId)) throw new ArgumentNullException("assetId");


            string id = assetId.Replace(":", "%");

            UriBuilder builder = new UriBuilder(mediaServicesApiServerUri);
            builder.Path = Path.Combine(builder.Path, "CreateFileInfos");
            builder.Query = String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId);

            try
            {
                var request = GenerateRequest("GET", mediaServicesApiServerUri, "CreateFileInfos",
                    String.Format(CultureInfo.InvariantCulture, "assetid='{0}'", assetId), acsBearerToken, null);

                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    if (response.StatusCode == HttpStatusCode.MovedPermanently)
                    {
                        string redirectedMediaServicesApiUrl = response.Headers["Location"];

                        CreateFileInfos(redirectedMediaServicesApiUrl, acsBearerToken, assetId);
                    }
                    else if ((response.StatusCode != HttpStatusCode.OK) &&
                        (response.StatusCode != HttpStatusCode.Accepted) &&
                        (response.StatusCode != HttpStatusCode.Created) &&
                        (response.StatusCode != HttpStatusCode.NoContent))
                    {
                        // TODO: Throw a more specific exception.
                        throw new Exception("Invalid response received ");
                    }
                }
            }
            catch (WebException ex)
            {
                Console.WriteLine(ex.Message);
            }
        }

        private static HttpWebRequest GenerateRequest(string verb,
                                                        string mediaServicesApiServerUri,
                                                        string resourcePath, string query,
                                                        string acsBearerToken, string requestbody)
        {
            var uriBuilder = new UriBuilder(mediaServicesApiServerUri);
            uriBuilder.Path += resourcePath;
            if (query != null)
            {
                uriBuilder.Query = query;
            }
            HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(uriBuilder.Uri);
            request.AllowAutoRedirect = false; //We manage our own redirects.
            request.Method = verb;

            if (resourcePath == "$metadata")
                request.MediaType = "application/xml";
            else
            {
                request.ContentType = "application/json;odata=verbose";
                request.Accept = "application/json;odata=verbose";
            }

            request.Headers.Add("DataServiceVersion", "3.0");
            request.Headers.Add("MaxDataServiceVersion", "3.0");
            request.Headers.Add("x-ms-version", "2.1");
            request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + acsBearerToken);

            if (requestbody != null)
            {
                var requestBytes = Encoding.ASCII.GetBytes(requestbody);
                request.ContentLength = requestBytes.Length;

                var requestStream = request.GetRequestStream();
                requestStream.Write(requestBytes, 0, requestBytes.Length);
                requestStream.Close();
            }
            else
            {
                request.ContentLength = 0;
            }
            return request;
        }

## <a name="next-steps"></a>後續步驟
您可以立即使用 hello 兩個資料中心之間的流量管理員 tooroute 要求，並因此任何中斷發生容錯移轉。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

