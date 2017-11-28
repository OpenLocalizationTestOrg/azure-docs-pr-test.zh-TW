---
title: "使用 Microsoft Azure 儲存體資料移動程式庫傳輸資料 | Microsoft Docs"
description: "使用資料移動程式庫從 Blob 和檔案內容移動或來回複製資料。 從本機檔案複製資料到 Azure 儲存體，或在儲存體帳戶內或之間複製資料。 輕鬆地將資料移轉至 Azure 儲存體。"
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
ms.openlocfilehash: 2ba94e4dd931b6d385101c7dadccfa3583b5296e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="1c51c-105">使用 Microsoft Azure 儲存體資料移動程式庫傳輸資料</span><span class="sxs-lookup"><span data-stu-id="1c51c-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="1c51c-106">概觀</span><span class="sxs-lookup"><span data-stu-id="1c51c-106">Overview</span></span>
<span data-ttu-id="1c51c-107">Microsoft Azure 儲存體資料移動程式庫是跨平台的開放原始碼程式庫，設計用來提供 Azure 儲存體 Blob 和檔案的高效能上傳、下載及複製。</span><span class="sxs-lookup"><span data-stu-id="1c51c-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="1c51c-108">這個程式庫是支援 [AzCopy](storage-use-azcopy.md) 的核心資料移動架構。</span><span class="sxs-lookup"><span data-stu-id="1c51c-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="1c51c-109">資料移動程式庫可提供傳統的 [.NET Azure 儲存體用戶端程式庫](storage-dotnet-how-to-use-blobs.md)中並未提供的簡便方法。</span><span class="sxs-lookup"><span data-stu-id="1c51c-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="1c51c-110">這包括設定平行作業數目、追蹤傳輸進度、輕鬆繼續已取消的傳輸等等。</span><span class="sxs-lookup"><span data-stu-id="1c51c-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="1c51c-111">此程式庫也會使用 .NET Core，這表示您在建置適用於 Windows、Linux 和 macOS 的 .NET 應用程式時可以使用它。</span><span class="sxs-lookup"><span data-stu-id="1c51c-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="1c51c-112">若要深入了解 .NET Core，請參閱 [.NET Core 文件 (英文)](https://dotnet.github.io/)。</span><span class="sxs-lookup"><span data-stu-id="1c51c-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="1c51c-113">這個程式庫也適用於 Windows 的傳統 .NET 架構應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c51c-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="1c51c-114">本文件將示範如何建立可在 Windows、Linux 和 macOS 上執行的 .NET Core 主控台應用程式，並執行下列案例：</span><span class="sxs-lookup"><span data-stu-id="1c51c-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="1c51c-115">將檔案和目錄上傳至 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c51c-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="1c51c-116">定義傳輸資料時的平行作業數目。</span><span class="sxs-lookup"><span data-stu-id="1c51c-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="1c51c-117">追蹤資料傳輸進度。</span><span class="sxs-lookup"><span data-stu-id="1c51c-117">Track data transfer progress.</span></span>
- <span data-ttu-id="1c51c-118">繼續已取消的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="1c51c-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="1c51c-119">將檔案從 URL 複製到 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c51c-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="1c51c-120">從 Blob 儲存體複製到 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c51c-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="1c51c-121">**您需要的項目：**</span><span class="sxs-lookup"><span data-stu-id="1c51c-121">**What you need:**</span></span>

* [<span data-ttu-id="1c51c-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1c51c-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="1c51c-123">[Azure 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="1c51c-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="1c51c-124">本指南假設您已熟悉 [Azure 儲存體](https://azure.microsoft.com/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="1c51c-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="1c51c-125">如果不熟悉，閱讀 [Azure 儲存體簡介](storage-introduction.md)說明文件會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="1c51c-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="1c51c-126">最重要的是，您需要[建立儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)才能開始使用資料移動程式庫。</span><span class="sxs-lookup"><span data-stu-id="1c51c-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="1c51c-127">設定</span><span class="sxs-lookup"><span data-stu-id="1c51c-127">Setup</span></span>  

1. <span data-ttu-id="1c51c-128">瀏覽 [.NET Core 安裝指南](https://www.microsoft.com/net/core)以安裝 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="1c51c-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="1c51c-129">選取環境時，請選擇命令列選項。</span><span class="sxs-lookup"><span data-stu-id="1c51c-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="1c51c-130">從命令列為專案建立目錄。</span><span class="sxs-lookup"><span data-stu-id="1c51c-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="1c51c-131">瀏覽到此目錄中，然後輸入 `dotnet new` 以建立 C# 主控台專案。</span><span class="sxs-lookup"><span data-stu-id="1c51c-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="1c51c-132">在 Visual Studio Code 中開啟此目錄。</span><span class="sxs-lookup"><span data-stu-id="1c51c-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="1c51c-133">您可以透過在命令列中輸入 `code .` 來快速完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="1c51c-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="1c51c-134">從 Visual Studio Code Marketplace 安裝 [C# 擴充 (英文)](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)。</span><span class="sxs-lookup"><span data-stu-id="1c51c-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="1c51c-135">重新啟動 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="1c51c-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="1c51c-136">這時，您應該會看到兩個提示。</span><span class="sxs-lookup"><span data-stu-id="1c51c-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="1c51c-137">其中一個是新增「建置和偵錯的必要資產。」</span><span class="sxs-lookup"><span data-stu-id="1c51c-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="1c51c-138">按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="1c51c-138">Click "yes."</span></span> <span data-ttu-id="1c51c-139">另一個提示是還原無法解析的相依性。</span><span class="sxs-lookup"><span data-stu-id="1c51c-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="1c51c-140">按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="1c51c-140">Click "restore."</span></span>
6. <span data-ttu-id="1c51c-141">您的應用程式現在應該會包含 `launch.json` 檔案 (位於 `.vscode` 目錄之下)。</span><span class="sxs-lookup"><span data-stu-id="1c51c-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="1c51c-142">將此檔案中的 `externalConsole` 值變更為 `true`。</span><span class="sxs-lookup"><span data-stu-id="1c51c-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="1c51c-143">Visual Studio Code 可讓您偵錯 .NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c51c-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="1c51c-144">按 `F5` 以執行應用程式，並確定您的設定運作正常。</span><span class="sxs-lookup"><span data-stu-id="1c51c-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="1c51c-145">您應該會看到「Hello World!」</span><span class="sxs-lookup"><span data-stu-id="1c51c-145">You should see "Hello World!"</span></span> <span data-ttu-id="1c51c-146">印出到主控台。</span><span class="sxs-lookup"><span data-stu-id="1c51c-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="1c51c-147">將資料移動程式庫加入至專案</span><span class="sxs-lookup"><span data-stu-id="1c51c-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="1c51c-148">將最新版本的資料移動程式庫加入到 `project.json` 檔案的 `dependencies` 區段。</span><span class="sxs-lookup"><span data-stu-id="1c51c-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="1c51c-149">撰寫本文時，此版本為 `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="1c51c-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="1c51c-150">將 `"portable-net45+win8"` 加入到 `imports` 區段。</span><span class="sxs-lookup"><span data-stu-id="1c51c-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="1c51c-151">您應該會看到提示顯示以還原專案。</span><span class="sxs-lookup"><span data-stu-id="1c51c-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="1c51c-152">按一下 [還原] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c51c-152">Click the "restore" button.</span></span> <span data-ttu-id="1c51c-153">您也可以在專案目錄的根目錄中輸入命令 `dotnet restore`，來從命令列還原專案。</span><span class="sxs-lookup"><span data-stu-id="1c51c-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="1c51c-154">修改 `project.json`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="1c51c-155">設定應用程式的基本架構</span><span class="sxs-lookup"><span data-stu-id="1c51c-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="1c51c-156">我們要做的第一件事是設定應用程式的「基本架構」程式碼。</span><span class="sxs-lookup"><span data-stu-id="1c51c-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="1c51c-157">此程式碼會提示我們輸入儲存體帳戶的名稱及帳戶金鑰，並使用該認證來建立 `CloudStorageAccount` 物件。</span><span class="sxs-lookup"><span data-stu-id="1c51c-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="1c51c-158">這個物件是用來在所有的傳輸案例中與儲存體帳戶互動。</span><span class="sxs-lookup"><span data-stu-id="1c51c-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="1c51c-159">該程式碼也會提示我們選擇要執行的傳輸作業類型。</span><span class="sxs-lookup"><span data-stu-id="1c51c-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="1c51c-160">修改 `Program.cs`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="1c51c-161">將本機檔案傳輸至 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1c51c-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="1c51c-162">將方法 `GetSourcePath` 和 `GetBlob` 加入到 `Program.cs`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="1c51c-163">修改 `TransferLocalFileToAzureBlob` 方法：</span><span class="sxs-lookup"><span data-stu-id="1c51c-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="1c51c-164">此程式碼會提示我們輸入本機檔案的路徑、新的或現有容器的名稱，和新的 Blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1c51c-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="1c51c-165">`TransferManager.UploadAsync` 方法會利用此資訊執行上傳。</span><span class="sxs-lookup"><span data-stu-id="1c51c-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="1c51c-166">按 `F5` 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c51c-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="1c51c-167">您可以使用 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)檢視儲存體帳戶，確認是否有上傳。</span><span class="sxs-lookup"><span data-stu-id="1c51c-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="1c51c-168">設定平行作業的數目</span><span class="sxs-lookup"><span data-stu-id="1c51c-168">Set number of parallel operations</span></span>
<span data-ttu-id="1c51c-169">資料移動程式庫提供的一項絕佳功能是設定平行作業的數目，以增加資料傳輸輸送量。</span><span class="sxs-lookup"><span data-stu-id="1c51c-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="1c51c-170">根據預設，資料移動程式庫會將平行作業的數目設為 8 * 您電腦的核心數目。</span><span class="sxs-lookup"><span data-stu-id="1c51c-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="1c51c-171">請留意，在低頻寬環境執行大量的平行作業可能會拖垮網路連線，並造成作業無法完成。</span><span class="sxs-lookup"><span data-stu-id="1c51c-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="1c51c-172">您必須針對此設定進行實驗，以根據您的可用網路頻寬決定最佳的運作方式。</span><span class="sxs-lookup"><span data-stu-id="1c51c-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="1c51c-173">讓我們加入一些程式碼，以便設定平行作業數目。</span><span class="sxs-lookup"><span data-stu-id="1c51c-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="1c51c-174">另外，也加入可用來計算傳輸完成所需時間的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1c51c-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="1c51c-175">將 `SetNumberOfParallelOperations` 方法加入到 `Program.cs`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="1c51c-176">修改 `ExecuteChoice` 方法以使用 `SetNumberOfParallelOperations`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="1c51c-177">修改 `TransferLocalFileToAzureBlob` 方法以使用計時器：</span><span class="sxs-lookup"><span data-stu-id="1c51c-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="1c51c-178">追蹤傳輸進度</span><span class="sxs-lookup"><span data-stu-id="1c51c-178">Track transfer progress</span></span>
<span data-ttu-id="1c51c-179">能知道資料完成傳輸需要多少時間，是一件很不錯的事。</span><span class="sxs-lookup"><span data-stu-id="1c51c-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="1c51c-180">不過，能夠在傳輸作業期間看到傳輸的進度會更好。</span><span class="sxs-lookup"><span data-stu-id="1c51c-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="1c51c-181">為了達成此案例，我們需要建立 `TransferContext` 物件。</span><span class="sxs-lookup"><span data-stu-id="1c51c-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="1c51c-182">`TransferContext` 物件有兩種形式：`SingleTransferContext` 和 `DirectoryTransferContext`。</span><span class="sxs-lookup"><span data-stu-id="1c51c-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="1c51c-183">前者用於傳輸單一檔案 (也就是我們現在要做的)，而後者用於傳輸檔案的目錄 (我們將在稍後進行)。</span><span class="sxs-lookup"><span data-stu-id="1c51c-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="1c51c-184">將方法 `GetSingleTransferContext` 和 `GetDirectoryTransferContext` 加入到 `Program.cs`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="1c51c-185">修改 `TransferLocalFileToAzureBlob` 方法以使用 `GetSingleTransferContext`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="1c51c-186">繼續已取消的傳輸</span><span class="sxs-lookup"><span data-stu-id="1c51c-186">Resume a canceled transfer</span></span>
<span data-ttu-id="1c51c-187">資料移動程式庫提供的另一項方便功能，是能夠繼續已取消的傳輸。</span><span class="sxs-lookup"><span data-stu-id="1c51c-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="1c51c-188">讓我們加入一些程式碼，使我們能夠輸入 `c` 來暫時取消傳輸，然後在 3 秒之後繼續傳輸。</span><span class="sxs-lookup"><span data-stu-id="1c51c-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="1c51c-189">修改 `TransferLocalFileToAzureBlob`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="1c51c-190">目前為止，`checkpoint` 的值一律是設為 `null`。</span><span class="sxs-lookup"><span data-stu-id="1c51c-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="1c51c-191">現在，如果我們取消傳輸，我們會擷取傳輸的最後一個檢查點，然後在新的傳輸內容中使用這個新的檢查點。</span><span class="sxs-lookup"><span data-stu-id="1c51c-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="1c51c-192">將本機目錄傳輸到 Azure Blob 目錄</span><span class="sxs-lookup"><span data-stu-id="1c51c-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="1c51c-193">如果資料移動程式庫一次只能傳輸一個檔案，不免令人有些失望。</span><span class="sxs-lookup"><span data-stu-id="1c51c-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="1c51c-194">所幸，事實並非如此。</span><span class="sxs-lookup"><span data-stu-id="1c51c-194">Luckily, this is not the case.</span></span> <span data-ttu-id="1c51c-195">資料移動程式庫可以傳輸檔案目錄及其子目錄的所有內容。</span><span class="sxs-lookup"><span data-stu-id="1c51c-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="1c51c-196">讓我們加入一些程式碼來這麼做。</span><span class="sxs-lookup"><span data-stu-id="1c51c-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="1c51c-197">首先，將方法 `GetBlobDirectory` 加入 `Program.cs`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="1c51c-198">然後，修改 `TransferLocalDirectoryToAzureBlobDirectory`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="1c51c-199">這個方法與上傳單一檔案的方法有一些差異。</span><span class="sxs-lookup"><span data-stu-id="1c51c-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="1c51c-200">我們現在使用 `TransferManager.UploadDirectoryAsync` 和稍早建立的 `getDirectoryTransferContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="1c51c-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="1c51c-201">此外，我們現在會提供 `options` 值給上傳作業，這可讓我們指出要在上傳中包含的子目錄。</span><span class="sxs-lookup"><span data-stu-id="1c51c-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="1c51c-202">將檔案從 URL 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1c51c-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="1c51c-203">現在，讓我們加入程式碼，以從 URL 將檔案複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="1c51c-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="1c51c-204">修改 `TransferUrlToAzureBlob`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="1c51c-205">這項功能的一個重要使用案例，是當您必須從另一個雲端服務 (例如 AWS) 將資料移動到 Azure 時。</span><span class="sxs-lookup"><span data-stu-id="1c51c-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="1c51c-206">只要您有可以存取資源的 URL，您就可以使用 `TransferManager.CopyAsync` 方法，輕鬆地將資源移動至 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="1c51c-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="1c51c-207">這個方法也引入新的布林值參數。</span><span class="sxs-lookup"><span data-stu-id="1c51c-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="1c51c-208">將此參數設定為 `true`，表示我們要執行非同步伺服器端複製。</span><span class="sxs-lookup"><span data-stu-id="1c51c-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="1c51c-209">將此參數設定為 `false` 表示同步複製，這代表資源會先下載到本機電腦，然後再上傳至 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="1c51c-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="1c51c-210">不過，同步複製目前僅適用於從某個 Azure 儲存體資源複製到另一個 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c51c-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="1c51c-211">將 Azure Blob 傳輸至 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1c51c-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="1c51c-212">資料移動程式庫提供的另一項獨特功能，是可從某個 Azure 儲存體資源複製到另一個。</span><span class="sxs-lookup"><span data-stu-id="1c51c-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="1c51c-213">修改 `TransferAzureBlobToAzureBlob`：</span><span class="sxs-lookup"><span data-stu-id="1c51c-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="1c51c-214">在此範例中，我們將 `TransferManager.CopyAsync` 中的布林值參數設為 `false`，指出我們要執行同步複製。</span><span class="sxs-lookup"><span data-stu-id="1c51c-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="1c51c-215">這表示資源會先下載到本機電腦，然後再上傳至 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="1c51c-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="1c51c-216">同步複製選項是確保複製作業有一致速度的絕佳方式。</span><span class="sxs-lookup"><span data-stu-id="1c51c-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="1c51c-217">相較之下，非同步伺服器端複製取決於伺服器的可用網路頻寬，速度可能會有所變動。</span><span class="sxs-lookup"><span data-stu-id="1c51c-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="1c51c-218">不過，相較於非同步複製，同步複製可能會產生額外的輸出成本。</span><span class="sxs-lookup"><span data-stu-id="1c51c-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="1c51c-219">建議的方法是在與您來源儲存體帳戶位於同一區域的 Azure VM 中使用同步複製，以避免產生輸出成本。</span><span class="sxs-lookup"><span data-stu-id="1c51c-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1c51c-220">結論</span><span class="sxs-lookup"><span data-stu-id="1c51c-220">Conclusion</span></span>
<span data-ttu-id="1c51c-221">現在已經完成資料移動應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c51c-221">Our data movement application is now complete.</span></span> <span data-ttu-id="1c51c-222">[您可在 GitHub 上取得完整的程式碼範例](https://github.com/azure-samples/storage-dotnet-data-movement-library-app)。</span><span class="sxs-lookup"><span data-stu-id="1c51c-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1c51c-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c51c-223">Next steps</span></span>
<span data-ttu-id="1c51c-224">在此快速入門中，我們已建立可在 Windows、Linux 和 macOS 上執行並與 Azure 儲存體互動的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c51c-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="1c51c-225">此快速入門的重點在 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c51c-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="1c51c-226">不過，同樣的知識可套用至檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="1c51c-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="1c51c-227">若要深入了解，請參閱 [Azure 儲存體資料移動程式庫參考文件 (英文)](https://azure.github.io/azure-storage-net-data-movement)。</span><span class="sxs-lookup"><span data-stu-id="1c51c-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




