---
title: "以 Microsoft Azure 儲存體的資料移動程式庫 hello aaaTransfer 資料 |Microsoft 文件"
description: "使用 hello 資料移動文件庫 toomove 或複製資料 tooor 從 blob 和檔案的內容。 複製資料 tooAzure 存放裝置從本機檔案，或複製資料內或之間的儲存體帳戶。 輕鬆地將移轉您的資料 tooAzure 儲存體。"
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 5de902d132565a8eafdc672f7a1a18e1a2db3a06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>將資料傳輸以 hello Microsoft Azure 儲存體的資料移動程式庫

## <a name="overview"></a>概觀
hello Microsoft Azure 儲存體的資料移動程式庫是設計用來上傳、 下載和 Azure 儲存體 Blob 和檔案複製的高效能的開放原始碼跨平台程式庫。 此程式庫是 hello 核心資料移動架構提供[AzCopy](storage-use-azcopy.md)。 hello 資料移動程式庫提供方便的方法不提供的我們傳統[.NET Azure 儲存體用戶端程式庫](storage-dotnet-how-to-use-blobs.md)。 這包括 hello 能力 tooset hello 平行作業數目，追蹤傳輸進度，輕鬆地繼續已取消的傳輸，以及執行更多。  

此程式庫也會使用 .NET Core，這表示您在建置適用於 Windows、Linux 和 macOS 的 .NET 應用程式時可以使用它。 toolearn 有關.NET Core 的詳細資訊，請參閱 toohello [.NET Core 文件](https://dotnet.github.io/)。 這個程式庫也適用於 Windows 的傳統 .NET 架構應用程式。 

本文件將示範如何 toocreate.NET Core 主控台應用程式，在 Windows、 Linux 及 macOS 上執行，並執行下列案例的 hello:

- 上傳的檔案和目錄 tooBlob 儲存體。
- 傳送資料時，請定義 hello 平行作業數目。
- 追蹤資料傳輸進度。
- 繼續已取消的資料傳輸。 
- 從 URL tooBlob 儲存體檔案複製。 
- 從 Blob 儲存體 tooBlob 儲存體複製。

**您需要的項目：**

* [Visual Studio Code](https://code.visualstudio.com/)
* [Azure 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> 本指南假設您已熟悉 [Azure 儲存體](https://azure.microsoft.com/services/storage/)。 如果沒有，請閱讀 hello[簡介 tooAzure 儲存體](storage-introduction.md)文件會很有幫助。 最重要的是，您需要太[建立儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)toostart 使用 hello 資料移動文件庫。
> 
> 

## <a name="setup"></a>設定  

1. 請瀏覽 hello [.NET Core 的安裝指南](https://www.microsoft.com/net/core)tooinstall.NET Core。 選取您的環境，請選擇 hello 命令列選項。 
2. 從 hello 命令列中，建立您的專案的目錄。 瀏覽到這個目錄中，然後輸入`dotnet new`toocreate C# 主控台專案。
3. 在 Visual Studio Code 中開啟此目錄。 這個步驟可快速地透過 hello 命令列輸入`code .`。  
4. 安裝 hello [C# 擴充](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)從 Visual Studio 程式碼 Marketplace hello。 重新啟動 Visual Studio Code。 
5. 這時，您應該會看到兩個提示。 其中一個可讓您新增 「 必要的資產 toobuild 和偵錯 」。 按一下 [是]。 另一個提示是還原無法解析的相依性。 按一下 [還原]。
6. 您的應用程式現在應該會包含`launch.json`下 hello 檔案`.vscode`目錄。 在此檔案中，變更 hello`externalConsole`值太`true`。
7. Visual Studio 程式碼可讓您 toodebug.NET Core 應用程式。 叫用`F5`toorun 您的應用程式並確認您的安裝程式可以運作。 您應該會看到「Hello World!」 列印的 toohello 主控台。 

## <a name="add-data-movement-library-tooyour-project"></a>將資料移動程式庫 tooyour 專案

1. 新增 hello 最新版 hello 資料移動文件庫 toohello`dependencies`區段您`project.json`檔案。 這個版本會是 hello 撰寫本文時，`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. 新增`"portable-net45+win8"`toohello `imports` > 一節。 
3. 提示應該顯示 toorestore 您的專案。 按一下 [還原] 按鈕，hello。 您也可以還原 hello 命令列從您的專案，藉由輸入 hello 命令`dotnet restore`hello 根專案目錄中。

修改 `project.json`：

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>設定您的應用程式的 hello 基本架構
hello 第一件事是設定 hello 「 基本架構 」 程式碼的應用程式。 此程式碼提示我們的儲存體帳戶名稱和帳戶金鑰，並使用這些認證 toocreate`CloudStorageAccount`物件。 這個物件是使用的 toointeract 與我們在所有案例中傳送的儲存體帳戶。 hello 程式碼也會我們提示 toochoose hello 類型的傳送作業，我們都希望 tooexecute。 

修改 `Program.cs`：

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>傳輸本機檔案 tooAzure Blob
加入 hello 方法`GetSourcePath`和`GetBlob`太`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

修改 hello`TransferLocalFileToAzureBlob`方法：

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

此程式碼會提示我們 hello 路徑 tooa 本機檔案、 新的或現有的容器，hello 名稱以及 hello 的新 blob 的名稱。 hello`TransferManager.UploadAsync`方法會執行 hello 上傳使用這項資訊。 

叫用`F5`toorun 您的應用程式。 您可以確認 hello 傳發生藉由檢視儲存體帳戶以 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。

## <a name="set-number-of-parallel-operations"></a>設定平行作業的數目
很棒的功能提供 hello 資料移動程式庫是平行作業 tooincrease hello 資料傳輸輸送量的 hello 能力 tooset hello 數目。 根據預設，hello 資料移動文件庫設定 hello too8 平行作業數目 * hello 您的電腦上的核心數目。 

請記住，在低頻寬的環境中的多個平行作業可能會淹沒 hello 網路連線和實際防止作業完全完成。 您將需要使用此設定 toodetermine tooexperiment 有哪些最好根據可用的網路頻寬。 

讓我們加入一些程式碼，讓我們 tooset hello 數目平行作業。 我們也加入程式碼的 hello 傳輸 toocomplete 所花費的時間。

新增`SetNumberOfParallelOperations`方法太`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

修改 hello`ExecuteChoice`方法 toouse `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

修改 hello`TransferLocalFileToAzureBlob`方法 toouse 計時器：

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>追蹤傳輸進度
了解我們的資料 tootransfer 的所需的時間很棒。 不過，在我們傳輸無法 toosee hello 進度*期間*hello 傳送作業會更好。 tooachieve 此案例中，我們需要 toocreate`TransferContext`物件。 hello`TransferContext`物件都有兩種形式：`SingleTransferContext`和`DirectoryTransferContext`。 hello 先前傳送單一檔案 （這是我們要現在），而後者 hello 傳輸檔案 （我們稍後會加入） 的目錄。

加入 hello 方法`GetSingleTransferContext`和`GetDirectoryTransferContext`太`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

修改 hello`TransferLocalFileToAzureBlob`方法 toouse `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>繼續已取消的傳輸
Hello 資料移動程式庫所提供的另一個方便的功能是 hello 能力 tooresume 取消傳輸。 讓我們加入一些程式碼，讓我們 tootemporarily 取消 hello 傳輸輸入`c`，然後繼續傳送嗨稍後 3 秒。

修改 `TransferLocalFileToAzureBlob`：

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

至今的情況下，我們`checkpoint`值的設定一定得`null`。 現在，如果我們取消 hello 傳輸時，我們擷取 hello 的我們傳輸時，最後一個檢查點然後我們傳送的內容中使用這個新的檢查點。 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>傳送本機目錄 tooAzure Blob 目錄
將事與願違如果 hello 資料移動程式庫無法一次只能傳送一個檔案。 幸運的是，這不是 hello 案例。 hello 資料移動程式庫提供 hello 能力 tootransfer 檔案和所有子目錄的目錄。 讓我們加入一些程式碼，讓我們 toodo 寫的。

首先，新增 hello 方法`GetBlobDirectory`太`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

然後，修改 `TransferLocalDirectoryToAzureBlobDirectory`：

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

沒有此方法與上傳一個檔案的 hello 方法之間有一些差異。 我們現在使用`TransferManager.UploadDirectoryAsync`和 hello`getDirectoryTransferContext`我們稍早建立的方法。 此外，我們現在會提供`options`值 tooour 上傳作業，讓我們 tooindicate 我們在我們的上傳想 tooinclude 子目錄。 

## <a name="copy-file-from-url-tooazure-blob"></a>從 URL tooAzure Blob 複製檔案
現在，讓我們加入程式碼，讓我們 toocopy URL tooan Azure Blob 中的檔案。 

修改 `TransferUrlToAzureBlob`：

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

這項功能的一個重要的使用案例是當您需要從另一個雲端服務 (例如 AWS) tooAzure toomove 資料。 只要您有 URL，可讓您存取 toohello 資源，您可以輕鬆地將該資源到 Azure Blob 使用 hello`TransferManager.CopyAsync`方法。 這個方法也引入新的布林值參數。 將這個參數設定為太`true`表示我們想 toodo 非同步的伺服器端副本。 將這個參數設定為太`false`指出同步複本-代表 hello 資源下載的 tooour 本機電腦第一次，然後上傳 tooAzure Blob。 不過，同步複本目前只適用於從一個 Azure 儲存體資源 tooanother 複製。 

## <a name="transfer-azure-blob-tooazure-blob"></a>傳輸 Azure Blob tooAzure Blob
唯一 hello 資料移動程式庫所提供的另一個功能是從一個 Azure 儲存體資源 tooanother hello 能力 toocopy。 

修改 `TransferAzureBlobToAzureBlob`：

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

在此範例中，我們 hello 布林值參數中設定`TransferManager.CopyAsync`太`false`tooindicate 我們想要 toodo 同步複本。 這表示確認 hello 資源下載的 tooour 本機電腦第一次，然後上傳 tooAzure Blob。 hello 同步複本 選項是很好的方法 tooensure 複製作業有一致的速度。 相較之下，非同步的伺服器端副本 hello 速度會相依於 hello 可變動的 hello 伺服器上的可用網路頻寬。 不過，同步複本可能會產生額外的輸出成本比較 tooasynchronous 複製。 hello 建議的作法是在 Azure VM 中 hello toouse 同步複本與來源儲存體帳戶 tooavoid 出口成本相同的區域。

## <a name="conclusion"></a>結論
現在已經完成資料移動應用程式。 [hello 完整的程式碼範例是 github](https://github.com/azure-samples/storage-dotnet-data-movement-library-app)。 

## <a name="next-steps"></a>後續步驟
在此快速入門中，我們已建立可在 Windows、Linux 和 macOS 上執行並與 Azure 儲存體互動的應用程式。 此快速入門的重點在 Blob 儲存體。 不過，這個相同的知識可以套用的 tooFile 儲存體。 toolearn 詳細資訊，請參閱[Azure 儲存體的資料移動程式庫參考文件](https://azure.github.io/azure-storage-net-data-movement)。

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




