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
ms.openlocfilehash: 9aec6cb171f794cc6ca432938ce499079e7dfdec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="0fe70-105">將資料傳輸以 hello Microsoft Azure 儲存體的資料移動程式庫</span><span class="sxs-lookup"><span data-stu-id="0fe70-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="0fe70-106">概觀</span><span class="sxs-lookup"><span data-stu-id="0fe70-106">Overview</span></span>
<span data-ttu-id="0fe70-107">hello Microsoft Azure 儲存體的資料移動程式庫是設計用來上傳、 下載和 Azure 儲存體 Blob 和檔案複製的高效能的開放原始碼跨平台程式庫。</span><span class="sxs-lookup"><span data-stu-id="0fe70-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="0fe70-108">此程式庫是 hello 核心資料移動架構提供[AzCopy](../storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="0fe70-108">This library is hello core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="0fe70-109">hello 資料移動程式庫提供方便的方法不提供的我們傳統[.NET Azure 儲存體用戶端程式庫](../blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="0fe70-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="0fe70-110">這包括 hello 能力 tooset hello 平行作業數目，追蹤傳輸進度，輕鬆地繼續已取消的傳輸，以及執行更多。</span><span class="sxs-lookup"><span data-stu-id="0fe70-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="0fe70-111">此程式庫也會使用 .NET Core，這表示您在建置適用於 Windows、Linux 和 macOS 的 .NET 應用程式時可以使用它。</span><span class="sxs-lookup"><span data-stu-id="0fe70-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="0fe70-112">toolearn 有關.NET Core 的詳細資訊，請參閱 toohello [.NET Core 文件](https://dotnet.github.io/)。</span><span class="sxs-lookup"><span data-stu-id="0fe70-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="0fe70-113">這個程式庫也適用於 Windows 的傳統 .NET 架構應用程式。</span><span class="sxs-lookup"><span data-stu-id="0fe70-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="0fe70-114">本文件將示範如何 toocreate.NET Core 主控台應用程式，在 Windows、 Linux 及 macOS 上執行，並執行下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="0fe70-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="0fe70-115">上傳的檔案和目錄 tooBlob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0fe70-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="0fe70-116">傳送資料時，請定義 hello 平行作業數目。</span><span class="sxs-lookup"><span data-stu-id="0fe70-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="0fe70-117">追蹤資料傳輸進度。</span><span class="sxs-lookup"><span data-stu-id="0fe70-117">Track data transfer progress.</span></span>
- <span data-ttu-id="0fe70-118">繼續已取消的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="0fe70-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="0fe70-119">從 URL tooBlob 儲存體檔案複製。</span><span class="sxs-lookup"><span data-stu-id="0fe70-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="0fe70-120">從 Blob 儲存體 tooBlob 儲存體複製。</span><span class="sxs-lookup"><span data-stu-id="0fe70-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="0fe70-121">**您需要的項目：**</span><span class="sxs-lookup"><span data-stu-id="0fe70-121">**What you need:**</span></span>

* [<span data-ttu-id="0fe70-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0fe70-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="0fe70-123">[Azure 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="0fe70-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="0fe70-124">本指南假設您已熟悉 [Azure 儲存體](https://azure.microsoft.com/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="0fe70-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="0fe70-125">如果沒有，請閱讀 hello[簡介 tooAzure 儲存體](storage-introduction.md)文件會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="0fe70-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="0fe70-126">最重要的是，您需要太[建立儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)toostart 使用 hello 資料移動文件庫。</span><span class="sxs-lookup"><span data-stu-id="0fe70-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="0fe70-127">設定</span><span class="sxs-lookup"><span data-stu-id="0fe70-127">Setup</span></span>  

1. <span data-ttu-id="0fe70-128">請瀏覽 hello [.NET Core 的安裝指南](https://www.microsoft.com/net/core)tooinstall.NET Core。</span><span class="sxs-lookup"><span data-stu-id="0fe70-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="0fe70-129">選取您的環境，請選擇 hello 命令列選項。</span><span class="sxs-lookup"><span data-stu-id="0fe70-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="0fe70-130">從 hello 命令列中，建立您的專案的目錄。</span><span class="sxs-lookup"><span data-stu-id="0fe70-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="0fe70-131">瀏覽到這個目錄中，然後輸入`dotnet new`toocreate C# 主控台專案。</span><span class="sxs-lookup"><span data-stu-id="0fe70-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="0fe70-132">在 Visual Studio Code 中開啟此目錄。</span><span class="sxs-lookup"><span data-stu-id="0fe70-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="0fe70-133">這個步驟可快速地透過 hello 命令列輸入`code .`。</span><span class="sxs-lookup"><span data-stu-id="0fe70-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="0fe70-134">安裝 hello [C# 擴充](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)從 Visual Studio 程式碼 Marketplace hello。</span><span class="sxs-lookup"><span data-stu-id="0fe70-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="0fe70-135">重新啟動 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="0fe70-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="0fe70-136">這時，您應該會看到兩個提示。</span><span class="sxs-lookup"><span data-stu-id="0fe70-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="0fe70-137">其中一個可讓您新增 「 必要的資產 toobuild 和偵錯 」。</span><span class="sxs-lookup"><span data-stu-id="0fe70-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="0fe70-138">按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="0fe70-138">Click "yes."</span></span> <span data-ttu-id="0fe70-139">另一個提示是還原無法解析的相依性。</span><span class="sxs-lookup"><span data-stu-id="0fe70-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="0fe70-140">按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="0fe70-140">Click "restore."</span></span>
6. <span data-ttu-id="0fe70-141">您的應用程式現在應該會包含`launch.json`下 hello 檔案`.vscode`目錄。</span><span class="sxs-lookup"><span data-stu-id="0fe70-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="0fe70-142">在此檔案中，變更 hello`externalConsole`值太`true`。</span><span class="sxs-lookup"><span data-stu-id="0fe70-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="0fe70-143">Visual Studio 程式碼可讓您 toodebug.NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0fe70-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="0fe70-144">叫用`F5`toorun 您的應用程式並確認您的安裝程式可以運作。</span><span class="sxs-lookup"><span data-stu-id="0fe70-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="0fe70-145">您應該會看到「Hello World!」</span><span class="sxs-lookup"><span data-stu-id="0fe70-145">You should see "Hello World!"</span></span> <span data-ttu-id="0fe70-146">列印的 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="0fe70-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="0fe70-147">將資料移動程式庫 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="0fe70-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="0fe70-148">新增 hello 最新版 hello 資料移動文件庫 toohello`dependencies`區段您`project.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="0fe70-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="0fe70-149">這個版本會是 hello 撰寫本文時，`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="0fe70-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="0fe70-150">新增`"portable-net45+win8"`toohello `imports` > 一節。</span><span class="sxs-lookup"><span data-stu-id="0fe70-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="0fe70-151">提示應該顯示 toorestore 您的專案。</span><span class="sxs-lookup"><span data-stu-id="0fe70-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="0fe70-152">按一下 [還原] 按鈕，hello。</span><span class="sxs-lookup"><span data-stu-id="0fe70-152">Click hello "restore" button.</span></span> <span data-ttu-id="0fe70-153">您也可以還原 hello 命令列從您的專案，藉由輸入 hello 命令`dotnet restore`hello 根專案目錄中。</span><span class="sxs-lookup"><span data-stu-id="0fe70-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="0fe70-154">修改 `project.json`：</span><span class="sxs-lookup"><span data-stu-id="0fe70-154">Modify `project.json`:</span></span>

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

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="0fe70-155">設定您的應用程式的 hello 基本架構</span><span class="sxs-lookup"><span data-stu-id="0fe70-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="0fe70-156">hello 第一件事是設定 hello 「 基本架構 」 程式碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0fe70-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="0fe70-157">此程式碼提示我們的儲存體帳戶名稱和帳戶金鑰，並使用這些認證 toocreate`CloudStorageAccount`物件。</span><span class="sxs-lookup"><span data-stu-id="0fe70-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="0fe70-158">這個物件是使用的 toointeract 與我們在所有案例中傳送的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fe70-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="0fe70-159">hello 程式碼也會我們提示 toochoose hello 類型的傳送作業，我們都希望 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="0fe70-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="0fe70-160">修改 `Program.cs`：</span><span class="sxs-lookup"><span data-stu-id="0fe70-160">Modify `Program.cs`:</span></span>

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

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="0fe70-161">傳輸本機檔案 tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="0fe70-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="0fe70-162">加入 hello 方法`GetSourcePath`和`GetBlob`太`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="0fe70-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

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

<span data-ttu-id="0fe70-163">修改 hello`TransferLocalFileToAzureBlob`方法：</span><span class="sxs-lookup"><span data-stu-id="0fe70-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="0fe70-164">此程式碼會提示我們 hello 路徑 tooa 本機檔案、 新的或現有的容器，hello 名稱以及 hello 的新 blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fe70-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="0fe70-165">hello`TransferManager.UploadAsync`方法會執行 hello 上傳使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="0fe70-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="0fe70-166">叫用`F5`toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0fe70-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="0fe70-167">您可以確認 hello 傳發生藉由檢視儲存體帳戶以 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="0fe70-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="0fe70-168">設定平行作業的數目</span><span class="sxs-lookup"><span data-stu-id="0fe70-168">Set number of parallel operations</span></span>
<span data-ttu-id="0fe70-169">很棒的功能提供 hello 資料移動程式庫是平行作業 tooincrease hello 資料傳輸輸送量的 hello 能力 tooset hello 數目。</span><span class="sxs-lookup"><span data-stu-id="0fe70-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="0fe70-170">根據預設，hello 資料移動文件庫設定 hello too8 平行作業數目 * hello 您的電腦上的核心數目。</span><span class="sxs-lookup"><span data-stu-id="0fe70-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="0fe70-171">請記住，在低頻寬的環境中的多個平行作業可能會淹沒 hello 網路連線和實際防止作業完全完成。</span><span class="sxs-lookup"><span data-stu-id="0fe70-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="0fe70-172">您將需要使用此設定 toodetermine tooexperiment 有哪些最好根據可用的網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="0fe70-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="0fe70-173">讓我們加入一些程式碼，讓我們 tooset hello 數目平行作業。</span><span class="sxs-lookup"><span data-stu-id="0fe70-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="0fe70-174">我們也加入程式碼的 hello 傳輸 toocomplete 所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="0fe70-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="0fe70-175">新增`SetNumberOfParallelOperations`方法太`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="0fe70-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="0fe70-176">修改 hello`ExecuteChoice`方法 toouse `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="0fe70-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

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

<span data-ttu-id="0fe70-177">修改 hello`TransferLocalFileToAzureBlob`方法 toouse 計時器：</span><span class="sxs-lookup"><span data-stu-id="0fe70-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="0fe70-178">追蹤傳輸進度</span><span class="sxs-lookup"><span data-stu-id="0fe70-178">Track transfer progress</span></span>
<span data-ttu-id="0fe70-179">了解我們的資料 tootransfer 的所需的時間很棒。</span><span class="sxs-lookup"><span data-stu-id="0fe70-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="0fe70-180">不過，在我們傳輸無法 toosee hello 進度*期間*hello 傳送作業會更好。</span><span class="sxs-lookup"><span data-stu-id="0fe70-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="0fe70-181">tooachieve 此案例中，我們需要 toocreate`TransferContext`物件。</span><span class="sxs-lookup"><span data-stu-id="0fe70-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="0fe70-182">hello`TransferContext`物件都有兩種形式：`SingleTransferContext`和`DirectoryTransferContext`。</span><span class="sxs-lookup"><span data-stu-id="0fe70-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="0fe70-183">hello 先前傳送單一檔案 （這是我們要現在），而後者 hello 傳輸檔案 （我們稍後會加入） 的目錄。</span><span class="sxs-lookup"><span data-stu-id="0fe70-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="0fe70-184">加入 hello 方法`GetSingleTransferContext`和`GetDirectoryTransferContext`太`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="0fe70-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

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

<span data-ttu-id="0fe70-185">修改 hello`TransferLocalFileToAzureBlob`方法 toouse `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="0fe70-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="0fe70-186">繼續已取消的傳輸</span><span class="sxs-lookup"><span data-stu-id="0fe70-186">Resume a canceled transfer</span></span>
<span data-ttu-id="0fe70-187">Hello 資料移動程式庫所提供的另一個方便的功能是 hello 能力 tooresume 取消傳輸。</span><span class="sxs-lookup"><span data-stu-id="0fe70-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="0fe70-188">讓我們加入一些程式碼，讓我們 tootemporarily 取消 hello 傳輸輸入`c`，然後繼續傳送嗨稍後 3 秒。</span><span class="sxs-lookup"><span data-stu-id="0fe70-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="0fe70-189">修改 `TransferLocalFileToAzureBlob`：</span><span class="sxs-lookup"><span data-stu-id="0fe70-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

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

<span data-ttu-id="0fe70-190">至今的情況下，我們`checkpoint`值的設定一定得`null`。</span><span class="sxs-lookup"><span data-stu-id="0fe70-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="0fe70-191">現在，如果我們取消 hello 傳輸時，我們擷取 hello 的我們傳輸時，最後一個檢查點然後我們傳送的內容中使用這個新的檢查點。</span><span class="sxs-lookup"><span data-stu-id="0fe70-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="0fe70-192">傳送本機目錄 tooAzure Blob 目錄</span><span class="sxs-lookup"><span data-stu-id="0fe70-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="0fe70-193">將事與願違如果 hello 資料移動程式庫無法一次只能傳送一個檔案。</span><span class="sxs-lookup"><span data-stu-id="0fe70-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="0fe70-194">幸運的是，這不是 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="0fe70-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="0fe70-195">hello 資料移動程式庫提供 hello 能力 tootransfer 檔案和所有子目錄的目錄。</span><span class="sxs-lookup"><span data-stu-id="0fe70-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="0fe70-196">讓我們加入一些程式碼，讓我們 toodo 寫的。</span><span class="sxs-lookup"><span data-stu-id="0fe70-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="0fe70-197">首先，新增 hello 方法`GetBlobDirectory`太`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="0fe70-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

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

<span data-ttu-id="0fe70-198">然後，修改 `TransferLocalDirectoryToAzureBlobDirectory`：</span><span class="sxs-lookup"><span data-stu-id="0fe70-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

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

<span data-ttu-id="0fe70-199">沒有此方法與上傳一個檔案的 hello 方法之間有一些差異。</span><span class="sxs-lookup"><span data-stu-id="0fe70-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="0fe70-200">我們現在使用`TransferManager.UploadDirectoryAsync`和 hello`getDirectoryTransferContext`我們稍早建立的方法。</span><span class="sxs-lookup"><span data-stu-id="0fe70-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="0fe70-201">此外，我們現在會提供`options`值 tooour 上傳作業，讓我們 tooindicate 我們在我們的上傳想 tooinclude 子目錄。</span><span class="sxs-lookup"><span data-stu-id="0fe70-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="0fe70-202">從 URL tooAzure Blob 複製檔案</span><span class="sxs-lookup"><span data-stu-id="0fe70-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="0fe70-203">現在，讓我們加入程式碼，讓我們 toocopy URL tooan Azure Blob 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="0fe70-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="0fe70-204">修改 `TransferUrlToAzureBlob`：</span><span class="sxs-lookup"><span data-stu-id="0fe70-204">Modify `TransferUrlToAzureBlob`:</span></span>

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

<span data-ttu-id="0fe70-205">這項功能的一個重要的使用案例是當您需要從另一個雲端服務 (例如 AWS) tooAzure toomove 資料。</span><span class="sxs-lookup"><span data-stu-id="0fe70-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="0fe70-206">只要您有 URL，可讓您存取 toohello 資源，您可以輕鬆地將該資源到 Azure Blob 使用 hello`TransferManager.CopyAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="0fe70-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="0fe70-207">這個方法也引入新的布林值參數。</span><span class="sxs-lookup"><span data-stu-id="0fe70-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="0fe70-208">將這個參數設定為太`true`表示我們想 toodo 非同步的伺服器端副本。</span><span class="sxs-lookup"><span data-stu-id="0fe70-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="0fe70-209">將這個參數設定為太`false`指出同步複本-代表 hello 資源下載的 tooour 本機電腦第一次，然後上傳 tooAzure Blob。</span><span class="sxs-lookup"><span data-stu-id="0fe70-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="0fe70-210">不過，同步複本目前只適用於從一個 Azure 儲存體資源 tooanother 複製。</span><span class="sxs-lookup"><span data-stu-id="0fe70-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="0fe70-211">傳輸 Azure Blob tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="0fe70-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="0fe70-212">唯一 hello 資料移動程式庫所提供的另一個功能是從一個 Azure 儲存體資源 tooanother hello 能力 toocopy。</span><span class="sxs-lookup"><span data-stu-id="0fe70-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="0fe70-213">修改 `TransferAzureBlobToAzureBlob`：</span><span class="sxs-lookup"><span data-stu-id="0fe70-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

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

<span data-ttu-id="0fe70-214">在此範例中，我們 hello 布林值參數中設定`TransferManager.CopyAsync`太`false`tooindicate 我們想要 toodo 同步複本。</span><span class="sxs-lookup"><span data-stu-id="0fe70-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="0fe70-215">這表示確認 hello 資源下載的 tooour 本機電腦第一次，然後上傳 tooAzure Blob。</span><span class="sxs-lookup"><span data-stu-id="0fe70-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="0fe70-216">hello 同步複本 選項是很好的方法 tooensure 複製作業有一致的速度。</span><span class="sxs-lookup"><span data-stu-id="0fe70-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="0fe70-217">相較之下，非同步的伺服器端副本 hello 速度會相依於 hello 可變動的 hello 伺服器上的可用網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="0fe70-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="0fe70-218">不過，同步複本可能會產生額外的輸出成本比較 tooasynchronous 複製。</span><span class="sxs-lookup"><span data-stu-id="0fe70-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="0fe70-219">hello 建議的作法是在 Azure VM 中 hello toouse 同步複本與來源儲存體帳戶 tooavoid 出口成本相同的區域。</span><span class="sxs-lookup"><span data-stu-id="0fe70-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="0fe70-220">結論</span><span class="sxs-lookup"><span data-stu-id="0fe70-220">Conclusion</span></span>
<span data-ttu-id="0fe70-221">現在已經完成資料移動應用程式。</span><span class="sxs-lookup"><span data-stu-id="0fe70-221">Our data movement application is now complete.</span></span> <span data-ttu-id="0fe70-222">[hello 完整的程式碼範例是 github](https://github.com/azure-samples/storage-dotnet-data-movement-library-app)。</span><span class="sxs-lookup"><span data-stu-id="0fe70-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0fe70-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fe70-223">Next steps</span></span>
<span data-ttu-id="0fe70-224">在此快速入門中，我們已建立可在 Windows、Linux 和 macOS 上執行並與 Azure 儲存體互動的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0fe70-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="0fe70-225">此快速入門的重點在 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0fe70-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="0fe70-226">不過，這個相同的知識可以套用的 tooFile 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0fe70-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="0fe70-227">toolearn 詳細資訊，請參閱[Azure 儲存體的資料移動程式庫參考文件](https://azure.github.io/azure-storage-net-data-movement)。</span><span class="sxs-lookup"><span data-stu-id="0fe70-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




