---
title: "aaaTutorial-使用 hello Azure 批次用戶端程式庫適用於.NET |Microsoft 文件"
description: "深入了解 hello Azure Batch 基本概念，並建立使用適用於.NET 的簡易解決方案。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>開始建置適用於.NET 的解決方案與 hello 批次的用戶端程式庫

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

了解 hello 基本概念的[Azure Batch] [ azure_batch]和 hello[批次.NET] [ net_api]本文章中的程式庫我們討論 C# 範例應用程式步驟的步驟。 我們會審視如何 hello 範例應用程式會利用 hello 批次服務 tooprocess 平行的工作負載中 hello 雲端，以及它如何與互動[Azure 儲存體](../storage/common/storage-introduction.md)檔案暫存和擷取。 您將了解常見的批次應用程式工作流程和基底的 hello 主要元件批次的工作、 工作、 集區，例如了解計算節點。

![Batch 方案工作流程 (基本)][11]<br/>

## <a name="prerequisites"></a>必要條件
本文假設您已具備 C# 和 Visual Studio 的使用知識。 它也假設您使用的是可以 toosatisfy hello 帳戶建立所指定需求的下面針對 Azure hello 批次和儲存體服務。

### <a name="accounts"></a>帳戶
* **Azure 帳戶**：如果您沒有 Azure 訂用帳戶，請[建立免費的 Azure 帳戶][azure_free_account]。
* **Batch 帳戶**：擁有 Azure 訂用帳戶後，請 [建立 Azure Batch 帳戶](batch-account-create-portal.md)。
* **儲存體帳戶**：請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。

> [!IMPORTANT]
> 目前批次支援*只*hello**一般用途**儲存體帳戶類型，如步驟 5 中所述[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)中[關於 Azure儲存體帳戶](../storage/common/storage-create-storage-account.md)。
>
>

### <a name="visual-studio"></a>Visual Studio
您必須擁有**2015年或更新版本的 Visual Studio** toobuild hello 範例專案。 您可以在 hello 找到免費及試用版本的 Visual Studio[的 Visual Studio 產品概觀][visual_studio]。

### <a name="dotnettutorial-code-sample"></a> 程式碼範例
hello [DotNetTutorial] [ github_dotnettutorial]範例是一個在 hello 中找到多個批次的程式碼範例的 hello [azure 批次範例][ github_samples]上的儲存機制GitHub。 您可以按一下 下載所有 hello 範例**複製或都下載 > 都下載 ZIP** hello 儲存機制首頁上，或按一下 hello [azure 批次範例-master.zip] [ github_samples_zip]直接下載連結。 一旦您已擷取 hello hello ZIP 檔案的內容，您可以找到下列資料夾的 hello hello 方案：

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Azure Batch 總管 (選用)
hello [Azure 批次總管][ github_batchexplorer]是免費的公用程式隨附的 hello [azure 批次範例][ github_samples] GitHub 上的儲存機制。 時不需要 toocomplete 本教學課程中，它可以時很實用開發及偵錯您批次的解決方案。

## <a name="dotnettutorial-sample-project-overview"></a>DotNetTutorial 範例專案概觀
hello *DotNetTutorial*程式碼範例是包含兩個專案的 Visual Studio 方案： **DotNetTutorial**和**TaskApplication**。

* **DotNetTutorial**是平行計算節點 （虛擬機器） 上的工作負載之互動 hello 批次和儲存體服務 tooexecute hello 用戶端應用程式。 DotNetTutorial 會在本機工作站上執行。
* **TaskApplication**是 hello Azure tooperform hello 實際工作中的計算節點執行的程式。 在 hello 範例`TaskApplication.exe`剖析 hello 下載自 Azure 儲存體 （hello 輸入檔） 的檔案中的文字。 然後它會產生文字檔案 （hello 輸出檔），其中包含出現在 hello 輸入檔中的 hello 前三個單字的清單。 它會建立 hello 輸出檔後，TaskApplication 會上傳 hello 檔案 tooAzure 儲存體。 這使得可用 toohello 下載的用戶端應用程式。 Hello 批次服務中的多個計算節點上，以平行方式執行 TaskApplication。

hello 下列圖表說明 hello hello 用戶端應用程式，所執行的主要作業*DotNetTutorial*，和 hello 應用程式所執行的 hello 工作*TaskApplication*. 此基本工作流程通常由使用 Batch 建立的許多計算方案所組成。 雖然它不會示範 hello 批次服務中可用的每一項功能，幾乎每個批次案例包含此工作流程的部分。

![Batch 範例工作流程][8]<br/>

[**步驟 1.**](#step-1-create-storage-containers) 在 Azure Blob 儲存體中建立**容器**。<br/>
[**步驟 2.**](#step-2-upload-task-application-and-data-files) 上傳工作應用程式檔案和 toocontainers 輸入的檔。<br/>
[**步驟 3.**](#step-3-create-batch-pool) 建立 Batch **集區**。<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** hello 集區**StartTask**下載 hello 工作二進位檔案 (TaskApplication) toonodes，因為它們加入 hello 集區。<br/>
[**步驟 4.**](#step-4-create-batch-job) 建立 Batch **作業**。<br/>
[**步驟 5.**](#step-5-add-tasks-to-job) 新增**工作**toohello 作業。<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** hello 工作是排定的 tooexecute 節點上。<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** 每項工作會從 Azure 儲存體下載其輸入資料，然後開始執行。<br/>
[**步驟 6.**](#step-6-monitor-tasks) 監視工作。<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** 工作完成後，它們上傳其輸出資料 tooAzure 儲存體。<br/>
[**步驟 7.**](#step-7-download-task-output) 從儲存體下載工作輸出。

如所述，並非每個批次解決方案會執行這些確切步驟，並可能包含更多，但 hello *DotNetTutorial*範例應用程式示範一般程序，在批次方案中找到。

## <a name="build-hello-dotnettutorial-sample-project"></a>建置 hello *DotNetTutorial*範例專案
您可以順利執行 hello 範例之前，您必須指定批次和儲存體帳戶認證在 hello *DotNetTutorial*專案的`Program.cs`檔案。 如果您尚未執行此動作 hello 方案在 Visual Studio 中按兩下開啟 hello`DotNetTutorial.sln`方案檔。 或從 Visual Studio 內使用開啟 hello**檔案 > 開啟 > 專案/方案**功能表。

開啟`Program.cs`內 hello *DotNetTutorial*專案。 指定 hello hello 檔案的頂端附近，然後加入您的認證：

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> 如上面所述，您目前必須指定 hello 認證**一般用途**Azure 儲存體中的儲存體帳戶。 批次應用程式使用 blob 儲存體中 hello**一般用途**儲存體帳戶。 未指定儲存體帳戶所建立的選取 hello hello 認證*Blob 儲存體*帳戶類型。
>
>

您可以找到您的批次和儲存體帳戶認證中的每個服務的 hello 帳戶 刀鋒視窗中 hello [Azure 入口網站][azure_portal]:

![批次 hello 入口網站中的認證][9]
![hello 入口網站中的儲存體認證][10]<br/>

既然您已使用您的認證更新 hello 專案，以滑鼠右鍵按一下方案總管 中的 hello 方案，然後按一下**建置方案**。 如果系統提示您，確認 hello 任何的 NuGet 封裝還原。

> [!TIP]
> 如果 hello NuGet 封裝不會自動還原，或如果您看到失敗 toorestore hello 封裝相關的錯誤，請確定您擁有 hello [NuGet 套件管理員][ nuget_packagemgr]安裝。 再啟用 hello 下載遺漏的套件。 請參閱[啟用封裝還原建置期間][ nuget_restore] tooenable 套件下載。
>
>

在下列各節的 hello，我們可分為 hello 範例應用程式，它會執行 tooprocess hello 步驟 hello 批次服務中的工作負載，並討論這些步驟，在詳細資料。 我們鼓勵您 toorefer toohello 開啟的方案在 Visual Studio 工作透過 hello 本文其餘部分，因為討論 hello 範例中的程式碼不是每個列時。

瀏覽 toohello 頂端 hello`MainAsync`方法在 hello *DotNetTutorial*專案的`Program.cs`檔案 toostart 與步驟 1。 然後大致如下所示 hello 進展方法的呼叫中的每個步驟下方`MainAsync`。

## <a name="step-1-create-storage-containers"></a>步驟 1：建立儲存體容器
![在 Azure 儲存體中建立容器][1]
<br/>

Batch 包含與 Azure 儲存體進行互動的內建支援。 在儲存體帳戶的容器會提供在您的 Batch 帳戶中執行的 hello 工作所需的 hello 檔案。 hello 容器也會提供 hello 工作產生的地方 toostore hello 輸出資料。 首先 hello hello *DotNetTutorial*用戶端應用程式會建立三個容器在[Azure Blob 儲存體](../storage/common/storage-introduction.md):

* **應用程式**： 此容器會儲存 hello hello 工作，以及任何相依性，例如 Dll 所執行的應用程式。
* **輸入**： 工作會從 hello 下載 hello 資料檔案 tooprocess*輸入*容器。
* **輸出**： 當工作完成時輸入的檔案處理時，他們會將上傳 hello 結果 toohello*輸出*容器。

在順序 toointeract 與儲存體帳戶，並建立容器，我們使用 hello[適用於.NET 的 Azure 儲存體用戶端程式庫][net_api_storage]。 我們建立了具有參考 toohello 帳戶[CloudStorageAccount][net_cloudstorageaccount]，並從該建立[CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

我們使用 hello`blobClient`參考整個 hello 應用程式並將它傳遞為參數 tooseveral 方法。 舉例來說，這是在 hello 緊接 hello 以上版本，在呼叫的程式碼區塊`CreateContainerIfNotExistAsync`tooactually 建立 hello 容器。

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

一旦已建立 hello 容器，hello 應用程式現在可以將 hello 工作所使用的 hello 檔案上傳。

> [!TIP]
> [如何從.NET 的 Blob 儲存體 toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md)提供使用 Azure 儲存體容器和 blob 的良好概觀。 當您使用批次開始使用，它應該是 hello 讀取清單頂端附近。
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>步驟 2：上傳工作應用程式和資料檔案
![上傳工作應用程式，並輸入 （資料） 檔 toocontainers][2]
<br/>

Hello 檔案中上傳作業， *DotNetTutorial*的集合會先定義**應用程式**和**輸入**存在於 hello 本機電腦上檔案路徑。 然後它上傳您在 hello 上一個步驟中建立這些檔案 toohello 容器。

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

有兩種方法在`Program.cs`hello 上傳程序涉及：

* `UploadFilesToContainerAsync`： 這個方法傳回的集合[ResourceFile] [ net_resourcefile] （討論如下） 的物件，並在內部呼叫`UploadFileToContainerAsync`tooupload 每個檔案，傳入 hello *filePaths*參數。
* `UploadFileToContainerAsync`： 這是實際執行 hello 檔案上傳，並建立 hello hello 方法[ResourceFile] [ net_resourcefile]物件。 上傳之後 hello 檔案，它會取得 hello 檔案的共用的存取簽章 (SAS)，並傳回 ResourceFile 物件，表示它。 下面也會討論共用存取簽章。

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ net_resourcefile]提供批次中的工作會下載的 tooa 的 Azure 儲存體中的 hello URL tooa 檔案與計算節點，才能執行該工作。 hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource]存在於 Azure 儲存體中，屬性會指定 hello 的 hello 檔案的完整 URL。 hello URL 也可能包括提供安全的 access toohello 檔案的共用的存取簽章 (SAS)。 Batch .NET 中的大部分工作類型都包含 ResourceFiles  屬性，包括：

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

hello DotNetTutorial 範例應用程式不會使用 hello JobPreparationTask 或 JobReleaseTask 工作類型，但您可以深入資訊，請在[執行作業準備與完成工作上 Azure Batch 計算節點](batch-job-prep-release.md)。

### <a name="shared-access-signature-sas"></a>共用存取簽章 (SAS)
共用的存取簽章字串的 — 包含為 URL 的一部分時，提供安全地存取 toocontainers 和 Azure 儲存體中的 blob。 hello DotNetTutorial 應用程式會使用這兩個 blob 和容器共用存取簽章 Url，並示範如何 tooobtain 這些共用存取簽章字串 hello 儲存體服務。

* **Blob 共用的存取簽章**: hello 集區 StartTask DotNetTutorial 中的從儲存體下載 hello 應用程式二進位檔和輸入的資料檔時，請使用 blob 共用存取簽章 （請參閱下面步驟 #3）。 hello`UploadFileToContainerAsync`方法中 DotNetTutorial 的`Program.cs`包含 hello 程式碼會取得每個 blob 的共用的存取簽章。 呼叫 [CloudBlob.GetSharedAccessSignature][net_sas_blob] 即可完成。
* **容器共用存取簽章**： 為每項工作完成其工作 hello 計算節點上的上, 傳其輸出檔 toohello*輸出*Azure 儲存體容器中的。 toodo TaskApplication 因此，使用容器的共用的存取簽章時，會提供寫入存取 toohello 容器 hello 路徑 hello 檔案上傳。 取得 hello 容器共用的存取簽章是以類似的方式做為當取得 hello blob 共用存取簽章。 在 DotNetTutorial，您會發現該 hello `GetContainerSasUrl` helper 方法會呼叫[CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo 如此。 您會先深入 TaskApplication 如何使用 hello 容器共用存取簽章中的 「 步驟 6： 監視工作。 」

> [!TIP]
> 簽出 hello 兩段式序列上的共用的存取簽章，[第 1 部分： 了解 hello 共用存取簽章 (SAS) 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)和[第 2 部分： 建立和使用共用的存取簽章 (SAS) 使用 Blob 儲存體](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)，深入了解提供儲存體帳戶中的安全存取 toodata toolearn。
>
>

## <a name="step-3-create-batch-pool"></a>步驟 3：建立 Batch 集區
![建立 Batch 集區][3]
<br/>

Batch **集區** 是 Batch 執行作業工作所在的計算節點 (虛擬機器) 集合。

上傳 hello 應用程式及資料檔案 toohello 與 Azure 儲存體 Api，儲存體帳戶之後*DotNetTutorial*開始進行呼叫 toohello 批次服務的 hello 批次.NET 程式庫所提供的 Api。 hello 程式碼會先建立[BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

接下來，hello 範例建立集區的運算節點 hello 批次帳戶的呼叫中太`CreatePoolIfNotExistsAsync`。 `CreatePoolIfNotExistsAsync`使用 hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create]方法 toocreate hello 批次服務中的新集區：

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

當您建立的集區[CreatePool][net_pool_create]，您指定數個參數 hello 的運算節點數目，例如 hello [hello 節點大小](../cloud-services/cloud-services-sizes-specs.md)，和 hello 節點的作業系統系統。 在*DotNetTutorial*，我們使用[CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 從[雲端服務](../cloud-services/cloud-services-guestos-update-matrix.md)。 

您也可以建立 Azure 虛擬機器 (Vm) 的計算節點的集區，藉由指定 hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration]集區。 您可以從 Windows 或 [Linux 映像](batch-linux-nodes.md)建立 VM 計算節點的集區。 您的 VM 映像的 hello 來源可以是：

- hello [Azure 虛擬機器 Marketplace][vm_marketplace]，這樣會提供已備妥要使用的 Windows 和 Linux 映像。 
- 您準備和提供的自訂映像。 如需自訂映像的詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#pool)。

> [!IMPORTANT]
> 您需對 Batch 中的計算資源付費。 您可以降低 toominimize 成本`targetDedicatedComputeNodes`too1 之前執行 hello 範例。
>
>

這些實體節點的屬性，以及您也可以指定[StartTask] [ net_pool_starttask] hello 集區。 hello StartTask 執行每個節點上，該節點加入 hello 集區，以及每次重新啟動節點。 hello StartTask 為計算節點 toohello 先前執行的工作上安裝應用程式特別有用。 例如，如果您的工作會使用 Python 指令碼來處理資料，您可以使用 StartTask tooinstall Python hello 計算節點上。

在此範例應用程式，hello StartTask 會複製它會從儲存體下載的 hello 檔案 (其指定使用 hello [StartTask][net_starttask]。[ResourceFiles] [ net_starttask_resourcefiles]屬性) 從 hello StartTask 工作目錄 toohello 共用目錄的*所有*hello 節點上執行的工作可以存取。 基本上，這會將複製`TaskApplication.exe`和其相依性 toohello 共用目錄，每個節點上的為 hello 節點加入 hello 集區，以便在 hello 節點執行任何工作可以存取它。

> [!TIP]
> hello**應用程式封裝**Azure Batch 功能提供其他方式 tooget 到集區中的 hello 計算節點上的應用程式。 請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)如需詳細資訊。
>
>

也在 hello 上述程式碼片段的值得注意的是兩個環境中的變數 hello hello 使用*CommandLine* hello StartTask 屬性：`%AZ_BATCH_TASK_WORKING_DIR%`和`%AZ_BATCH_NODE_SHARED_DIR%`。 批次集區中每個運算節點會自動設定成有特定 tooBatch 的數個環境變數中。 任何處理程序所執行的工作有存取 toothese 環境變數。

> [!TIP]
> toofind 深入了解 hello 環境變數所提供的計算節點的批次集區和工作的工作目錄的詳細資訊，請參閱 「 hello[工作的環境設定](batch-api-basics.md#environment-settings-for-tasks)和[檔案和目錄](batch-api-basics.md#files-and-directories)章節 hello[批次功能概觀，讓開發人員](batch-api-basics.md)。
>
>

## <a name="step-4-create-batch-job"></a>步驟 4：建立 Batch 作業
![建立 Batch 作業][4]<br/>

Batch **作業** 是與計算節點集區相關聯的工作集合。 作業中的 hello 工作執行相關聯的 hello 集區的計算節點上。

您可以使用工作，不只對組織及追蹤相關的工作負載中的工作，也在 hello 批次中的關聯性 tooother 作業中的工作優先順序以及諸特定條件約束-例如 hello 最大 runtime hello 作業 （和延伸模組，其工作）帳戶。 在此範例中，不過，hello 作業是只能搭配步驟 #3 中建立的 hello 集區相關聯。 不會設定任何其他屬性。

所有 Batch 作業都會與特定集區相關聯。 這項關聯指示 hello 作業 」 工作，也會執行哪些節點。 指定此使用 hello [CloudJob.PoolInformation] [ net_job_poolinfo]屬性 hello 下列程式碼片段所示。

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

已建立工作，工作會新增 tooperform hello 工作。

## <a name="step-5-add-tasks-toojob"></a>步驟 5： 加入工作 toojob
![新增工作 toojob][5]<br/>
*（1） 工作已加入 toohello 作業、 （2) hello 工作是排定的 toorun 節點上，以及 （3) hello 工作下載 hello 資料檔案 tooprocess*

批次**工作**是 hello 個別的工作單位 hello 上所執行的計算節點。 工作已命令列，並執行 hello 指令碼或您在該命令列中指定的可執行檔。

tooactually 執行工作、 工作必須加入 tooa 作業。 每個[CloudTask] [ net_task]使用命令列屬性來設定和[ResourceFiles] [ net_task_resourcefiles] （如同 hello 集區 StartTask），hello 工作會在其命令列會自動在執行之前下載 toohello 節點。 在 hello *DotNetTutorial*範例專案，每項工作會處理一個檔案。 因此其 ResourceFiles 集合只包含單一元素。

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> 當他們存取環境變數例如`%AZ_BATCH_NODE_SHARED_DIR%`或執行應用程式中的 hello 節點找不到`PATH`，工作的命令列必須在前面加上`cmd /c`。 明確地將執行 hello 命令直譯器，並指示它 tooterminate 之後執行您的命令。 這項需求是不必要，如果您的工作執行應用程式中的 hello 節點`PATH`(例如*robocopy.exe*或*powershell.exe*)，而且不可用任何環境變數。
>
>

在 hello `foreach` hello 上述程式碼片段中的迴圈，您可以看到建構 hello hello 工作的命令列時，三個命令列引數會傳遞太*TaskApplication.exe*:

1. hello**第一個引數**是 hello 檔案 tooprocess hello 路徑。 這是 hello 本機路徑 toohello 檔案存在於 hello 節點。 當 hello 中的 ResourceFile 物件`UploadFileToContainerAsync`初次建立上述中 hello 檔案名稱已用於此屬性 （做為參數 toohello ResourceFile 建構函式）。 這表示該 hello 檔案位於 hello 相同目錄做為*TaskApplication.exe*。
2. hello**第二個引數**指定該 hello 頂端*N*字詞應該寫 toohello 輸出檔。 在 hello 範例中，這是硬式編碼，讓 hello 前三個單字都會寫入 toohello 輸出檔。
3. hello**第三個引數**hello 共用的存取簽章 (SAS) 提供寫入存取 toohello**輸出**Azure 儲存體容器中的。 *TaskApplication.exe*當它上傳 hello 輸出檔案 tooAzure 儲存體時，會使用此共用存取簽章 URL。 您可以在 hello 這個尋找 hello 程式碼`UploadFileToContainer`方法在 hello TaskApplication 專案的`Program.cs`檔案：

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>步驟 6：監視工作
![監視工作][6]<br/>
*hello 用戶端應用程式 （1） 監視 hello 完成及成功狀態的工作和 （2) hello 工作上傳結果資料 tooAzure 儲存體*

當工作區加入 tooa 工作時，他們會自動排入佇列，排定在 hello 與 hello 工作相關聯的集區的計算節點上執行。 根據您指定的 hello 設定，批次工作的所有佇列、 排程、 重試和其他工作的系統管理工作會為您處理。

有多種方法 toomonitoring 工作執行。 DotNetTutorial 顯示了一個只報告完成和工作失敗或成功狀態的簡單範例。 在 hello`MonitorTasks`中 DotNetTutorial 的方法`Program.cs`，有三個批次.NET 概念保證討論。 底下依其出現的順序列出：

1. **ODATADetailLevel**：一定要在清單作業 (例如取得作業的工作清單) 中指定 [ODATADetailLevel][net_odatadetaillevel]，以確保 Batch 應用程式效能。 新增[有效率地查詢 hello Azure Batch 服務](batch-efficient-list-queries.md)tooyour 讀取清單，如果您計劃執行任何類型的批次應用程式中監視狀態。
2. **TaskStateMonitor**：[TaskStateMonitor][net_taskstatemonitor] 提供給 Batch .NET 應用程可用來監視工作狀態的協助公用程式。 在`MonitorTasks`， *DotNetTutorial*等候所有工作 tooreach [TaskState.Completed] [ net_taskstate]時間限制內。 然後它會終止 hello 作業。
3. **TerminateJobAsync**： 終止與作業[JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] （或 hello 封鎖 JobOperations.TerminateJob） 將工作標示為已完成。 它是不可或缺的 toodo 因此如果您的批次方案使用[JobReleaseTask][net_jobreltask]。 如 [作業準備和完成工作](batch-job-prep-release.md)中所述，這是一種特殊的工作類型。

hello`MonitorTasks`方法從*DotNetTutorial*的`Program.cs`下方會出現：

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>步驟 7：下載工作輸出
![從儲存體下載工作輸出][7]<br/>

既然 hello 作業已完成，您可以從 Azure 儲存體下載 hello hello 工作輸出。 這是透過呼叫太`DownloadBlobsFromContainerAsync`中*DotNetTutorial*的`Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> 太 hello 呼叫`DownloadBlobsFromContainerAsync`在 hello *DotNetTutorial*應用程式指定 hello 檔案應該下載的 tooyour`%TEMP%`資料夾。 感覺可用 toomodify 這輸出位置。
>
>

## <a name="step-8-delete-containers"></a>步驟 8：刪除容器
因為您必須支付位於 Azure 儲存體中的資料，永遠是個不錯的主意 tooremove blob 不再需要的批次作業。 在 DotNetTutorial 的`Program.cs`，做法是使用三個呼叫 toohello helper 方法`DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

hello 方法本身只會取得參考 toohello 容器，然後再呼叫[CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>步驟 9： 刪除 hello 作業和 hello 集區
在 hello 最後一個步驟中，您提示的 toodelete hello 作業和 hello 集區所建立的 hello DotNetTutorial 應用程式。 雖然您不需支付作業和工作的費用，但您「需」支付計算節點的費用。 因此，我們建議您只在必要時配置節點。 刪除未使用的集區可成為您維護程序的一部分。

hello BatchClient 的[JobOperations] [ net_joboperations]和[PoolOperations] [ net_pooloperations]兩者都有對應的刪除動作方法，如果呼叫hello 使用者確認刪除項目：

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> 請記住，您需支付計算資源的費用，而刪除未使用的集區會將成本降到最低。 此外，請注意，刪除集區會刪除所有的運算節點區內，而且之後刪除 hello 集區 hello 節點上的任何資料將無法復原。
>
>

## <a name="run-hello-dotnettutorial-sample"></a>執行 hello *DotNetTutorial*範例
當您執行 hello 範例應用程式時，hello 主控台輸出會是類似 toohello 下列。 在執行期間，就會發生在暫停`Awaiting task completion, timeout in 00:30:00...`時 hello 集區的計算節點都已啟動。 使用 hello [Azure 入口網站][ azure_portal] toomonitor 集區、 計算節點、 工作和工作期間和之後執行。 使用 hello [Azure 入口網站][ azure_portal]或 hello [Azure 儲存體總管][ storage_explorers] tooview hello 存放資源 （容器和 blob） 的hello 應用程式所建立。

一般的執行時間是**大約 5 分鐘**當您執行 hello 應用程式在其預設組態。

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>後續步驟
太覺得可用 toomake 變更*DotNetTutorial*和*TaskApplication*不同 tooexperiment 計算案例。 例如，再次嘗試新增執行延遲太*TaskApplication*，例如如同[Thread.Sleep][net_thread_sleep]，toosimulate 長時間執行工作，並在 hello 入口網站中監視它們。 再試一次新增更多工作，或調整 hello 的運算節點數目。 新增的邏輯 toocheck 並允許 hello 使用現有的集區 toospeed 執行時間 (*提示*： 簽出`ArticleHelpers.cs`在 hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common]專案中[azure 批次範例][github_samples])。

既然您已熟悉 hello 批次解決方案的基本工作流程，它是 hello 的時間 toodig 中 toohello 批次服務的額外功能。

* 檢閱 hello [Azure Batch 概觀功能](batch-api-basics.md)發行項，我們建議您是否新增 toohello 服務。
* 開始在 hello 底下其他批次開發文件**深入開發**在 hello[批次學習路徑][batch_learning_path]。
* 簽出使用批次中 hello 處理 hello 「 前 n 個單字"工作負載的不同實作[TopNWords] [ github_topnwords]範例。
* 檢閱 hello 批次.NET[版本資訊](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes)hello hello 文件庫中的最新變更。

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "在 Azure 儲存體中建立容器"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "上傳工作應用程式，並輸入 （資料） 檔 toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "建立 Batch 集區"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "建立 Batch 作業"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "新增工作 toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "監視工作"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "從儲存體下載工作輸出"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Batch 方案工作流程 (完整圖表)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "入口網站中的 Batch 認證"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "入口網站中的儲存體認證"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch 方案工作流程 (最小圖表)"
