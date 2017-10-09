---
title: "開始使用 Azure Blob 儲存體 （物件儲存體） 使用適用於.NET 的 aaaGet |Microsoft 文件"
description: "使用 Azure Blob 儲存體 （物件儲存體） 的 hello 雲端中儲存非結構化的資料。"
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 3df0cf14b69d85cdc2f62cc3c8b901be102fa026
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="6e366-103">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="6e366-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="6e366-104">Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。</span><span class="sxs-lookup"><span data-stu-id="6e366-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="6e366-105">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="6e366-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="6e366-106">Blob 儲存體也是參考的 tooas 物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="6e366-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="6e366-107">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="6e366-107">About this tutorial</span></span>
<span data-ttu-id="6e366-108">本教學課程會示範如何 toowrite.NET 程式碼為使用 Azure Blob 儲存體的一些常見案例。</span><span class="sxs-lookup"><span data-stu-id="6e366-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="6e366-109">所涵蓋的案例包括上傳、列出、下載及刪除 Blob。</span><span class="sxs-lookup"><span data-stu-id="6e366-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="6e366-110">**必要條件：**</span><span class="sxs-lookup"><span data-stu-id="6e366-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="6e366-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e366-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="6e366-112">適用於 .NET 的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="6e366-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="6e366-113">適用於.NET 的 Azure 設定管理員</span><span class="sxs-lookup"><span data-stu-id="6e366-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="6e366-114">[Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="6e366-114">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="6e366-115">更多範例</span><span class="sxs-lookup"><span data-stu-id="6e366-115">More samples</span></span>
<span data-ttu-id="6e366-116">如需使用 Blob 儲存體的其他範例，請參閱 [在 .NET 中開始使用 Azure Blob 儲存體](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="6e366-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="6e366-117">您可以下載 hello 範例應用程式並執行它，或瀏覽 hello GitHub 上的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6e366-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="6e366-118">新增 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="6e366-118">Add using directives</span></span>
<span data-ttu-id="6e366-119">新增下列 hello**使用**指示詞 toohello 頂端 hello`Program.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="6e366-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="6e366-120">剖析 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="6e366-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="6e366-121">建立 hello Blob 服務用戶端</span><span class="sxs-lookup"><span data-stu-id="6e366-121">Create hello Blob service client</span></span>
<span data-ttu-id="6e366-122">hello **CloudBlobClient**類別可讓您 tooretrieve 容器和 Blob 儲存體中的 blob。</span><span class="sxs-lookup"><span data-stu-id="6e366-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="6e366-123">以下是其中一種方式 toocreate hello 服務用戶端：</span><span class="sxs-lookup"><span data-stu-id="6e366-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="6e366-124">現在您已準備好 toowrite 讀取和寫入資料 tooBlob 儲存的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6e366-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="6e366-125">建立容器</span><span class="sxs-lookup"><span data-stu-id="6e366-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="6e366-126">這個範例會示範如何 toocreate 如果不存在的容器：</span><span class="sxs-lookup"><span data-stu-id="6e366-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="6e366-127">根據預設，hello 新容器是私人的也就是說，您必須指定您的儲存體存取金鑰 toodownload blob，從這個容器。</span><span class="sxs-lookup"><span data-stu-id="6e366-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="6e366-128">如果您想在 hello 容器可用 tooeveryone toomake hello 檔案時，您可以設定 hello 容器 toobe 公用使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6e366-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="6e366-129">Hello 網際網路上的任何人可以看到公用容器中的 blob。</span><span class="sxs-lookup"><span data-stu-id="6e366-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="6e366-130">不過，您可以修改或刪除它們，只有當您擁有 hello 適當的帳戶存取金鑰或共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="6e366-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6e366-131">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="6e366-131">Upload a blob into a container</span></span>
<span data-ttu-id="6e366-132">Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="6e366-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="6e366-133">在大部分情況下，區塊 blob 是建議的型別 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="6e366-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="6e366-134">tooupload 檔案 tooa 區塊 blob，取得容器的參考，並將它 tooget 區塊 blob 參考。</span><span class="sxs-lookup"><span data-stu-id="6e366-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="6e366-135">Blob 參考之後，您可以上傳任何資料流的資料 tooit 呼叫 hello **UploadFromStream**方法。</span><span class="sxs-lookup"><span data-stu-id="6e366-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="6e366-136">如果它先前不存在，會覆寫它存在的話，這項作業會建立 hello blob。</span><span class="sxs-lookup"><span data-stu-id="6e366-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="6e366-137">下列範例會示範如何 hello tooupload blob 容器，並假設已建立該 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="6e366-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="6e366-138">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="6e366-138">List hello blobs in a container</span></span>
<span data-ttu-id="6e366-139">toolist hello blob 容器中的第一次取得容器的參考。</span><span class="sxs-lookup"><span data-stu-id="6e366-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="6e366-140">然後，您可以使用 hello 容器**ListBlobs**方法 tooretrieve hello blob 及/或目錄內。</span><span class="sxs-lookup"><span data-stu-id="6e366-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="6e366-141">tooaccess hello 豐富的屬性和方法傳回**IListBlobItem**，您必須將它轉換 tooa **CloudBlockBlob**， **CloudPageBlob**，或**CloudBlobDirectory**物件。</span><span class="sxs-lookup"><span data-stu-id="6e366-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="6e366-142">如果 hello 類型都屬未知，您可以使用型別檢查 toodetermine 哪些 toocast 它。</span><span class="sxs-lookup"><span data-stu-id="6e366-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="6e366-143">hello 下列程式碼示範如何 tooretrieve 和輸出 hello hello 中每個項目的 URI_相片_容器：</span><span class="sxs-lookup"><span data-stu-id="6e366-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

<span data-ttu-id="6e366-144">在 Blob 名稱中包含路徑資訊，您可以建立虛擬目錄結構，讓您能夠組織及周遊，就像使用傳統檔案系統一樣。</span><span class="sxs-lookup"><span data-stu-id="6e366-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="6e366-145">hello 目錄結構是虛擬只-hello 只可用在 Blob 儲存體資源是容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="6e366-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="6e366-146">不過，hello 儲存體用戶端程式庫提供**CloudBlobDirectory**物件 toorefer tooa 虛擬目錄，並簡化 hello 程序會以這種方式組織的 blob 使用。</span><span class="sxs-lookup"><span data-stu-id="6e366-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="6e366-147">例如，請考慮下列名為的容器中的區塊 blob 的整組 hello*相片*:</span><span class="sxs-lookup"><span data-stu-id="6e366-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="6e366-148">當您呼叫**ListBlobs**上 hello*相片*容器 （例如 hello 前面程式碼片段)，則會傳回階層式清單。</span><span class="sxs-lookup"><span data-stu-id="6e366-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="6e366-149">它同時包含**CloudBlobDirectory**和**CloudBlockBlob**分別代表 hello 目錄和 hello 容器中的 blob 的物件。</span><span class="sxs-lookup"><span data-stu-id="6e366-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="6e366-150">hello 產生的輸出看起來像：</span><span class="sxs-lookup"><span data-stu-id="6e366-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="6e366-151">您可以選擇性地設定 hello **UseFlatBlobListing** hello 參數**ListBlobs**方法**true**。</span><span class="sxs-lookup"><span data-stu-id="6e366-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="6e366-152">在此情況下，hello 容器中的每個 blob 會當做傳回**CloudBlockBlob**物件。</span><span class="sxs-lookup"><span data-stu-id="6e366-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="6e366-153">太 hello 呼叫**ListBlobs** tooreturn 一般清單看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="6e366-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="6e366-154">和 hello 結果看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="6e366-154">and hello results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="6e366-155">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="6e366-155">Download blobs</span></span>
<span data-ttu-id="6e366-156">toodownload blob，先擷取 blob 的參考，然後再呼叫 hello **DownloadToStream**方法。</span><span class="sxs-lookup"><span data-stu-id="6e366-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="6e366-157">hello 下列範例會使用 hello **DownloadToStream**方法 tootransfer hello blob 內容 tooa 資料流物件，您可以再保存 tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="6e366-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="6e366-158">您也可以使用 hello **DownloadToStream**方法 toodownload hello 內容為文字字串的 blob。</span><span class="sxs-lookup"><span data-stu-id="6e366-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="6e366-159">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="6e366-159">Delete blobs</span></span>
<span data-ttu-id="6e366-160">toodelete blob，先取得 blob 的參考，然後呼叫**刪除**方法。</span><span class="sxs-lookup"><span data-stu-id="6e366-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="6e366-161">以非同步方式分頁列出 Blob</span><span class="sxs-lookup"><span data-stu-id="6e366-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="6e366-162">如果在列示大量的 blob，或想讓您在一個清單作業中傳回的結果 toocontrol hello 數目，您可以列出結果的頁面中的 blob。</span><span class="sxs-lookup"><span data-stu-id="6e366-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="6e366-163">這個範例會示範如何 tooreturn 結果頁面中以非同步的方式，以便在等候 tooreturn 大型的結果集時不會封鎖執行。</span><span class="sxs-lookup"><span data-stu-id="6e366-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="6e366-164">此範例顯示一般 blob 清單，但您也可以執行階層式清單中，設定 hello _useFlatBlobListing_ hello 參數**ListBlobsSegmentedAsync**方法 too_false_。</span><span class="sxs-lookup"><span data-stu-id="6e366-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="6e366-165">Hello 範例方法會呼叫非同步方法，因為它前面都必須以 hello_非同步_關鍵字，而且必須傳回**工作**物件。</span><span class="sxs-lookup"><span data-stu-id="6e366-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="6e366-166">hello await 關鍵字指定 hello **ListBlobsSegmentedAsync**方法暫停執行 hello 取樣方法，直到 hello 清單的工作完成。</span><span class="sxs-lookup"><span data-stu-id="6e366-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="6e366-167">寫入 tooan 附加 blob</span><span class="sxs-lookup"><span data-stu-id="6e366-167">Writing tooan append blob</span></span>
<span data-ttu-id="6e366-168">附加 Blob 已針對附加作業 (例如紀錄) 最佳化。</span><span class="sxs-lookup"><span data-stu-id="6e366-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="6e366-169">為區塊 blob，例如附加 blob 區塊組成，但當您新增新的區塊 tooan 附加 blob 時，它一律是附加的 toohello hello blob 結尾。</span><span class="sxs-lookup"><span data-stu-id="6e366-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="6e366-170">您無法更新或刪除附加 Blob 中的現有區塊。</span><span class="sxs-lookup"><span data-stu-id="6e366-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="6e366-171">因為它們是區塊 blob，不會公開附加 blob 的 hello 區塊識別碼。</span><span class="sxs-lookup"><span data-stu-id="6e366-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="6e366-172">每個區塊中附加 blob 可以是不同的大小，tooa 最大值為 4 MB，總而且附加 blob 不可包括最多 50,000 個區塊。</span><span class="sxs-lookup"><span data-stu-id="6e366-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="6e366-173">hello 附加 blob 的大小上限，因此是稍微大於 195 GB （4 MB X 50000 區塊）。</span><span class="sxs-lookup"><span data-stu-id="6e366-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="6e366-174">hello 下面範例會建立新的附加 blob，並將附加一些資料 tooit，模擬簡單的記錄作業。</span><span class="sxs-lookup"><span data-stu-id="6e366-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="6e366-175">請參閱[了解區塊 Blob、 分頁 Blob，並附加 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)如需有關 hello hello 三種 blob 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="6e366-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="6e366-176">管理 Blob 安全性</span><span class="sxs-lookup"><span data-stu-id="6e366-176">Managing security for blobs</span></span>
<span data-ttu-id="6e366-177">根據預設，Azure 儲存體會保留您的資料安全，方法是限制存取 toohello 帳戶擁有者，並且擁有 hello 帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e366-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="6e366-178">當您需要 tooshare blob 資料儲存體帳戶中時，很重要的 toodo 因此不會危及您的帳戶存取金鑰的 hello 安全性。</span><span class="sxs-lookup"><span data-stu-id="6e366-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="6e366-179">此外，您可以加密安全移 hello 網路與 Azure 儲存體中的 blob 資料 tooensure。</span><span class="sxs-lookup"><span data-stu-id="6e366-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="6e366-180">控制存取 tooblob 資料</span><span class="sxs-lookup"><span data-stu-id="6e366-180">Controlling access tooblob data</span></span>
<span data-ttu-id="6e366-181">根據預設，儲存體帳戶中的 hello blob 資料會是可存取的只有 toostorage 帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="6e366-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="6e366-182">根據預設，驗證要求，針對 Blob 儲存體需要 hello 帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e366-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="6e366-183">不過，您可能希望 toomake 特定 blob 資料可用 tooother 使用者。</span><span class="sxs-lookup"><span data-stu-id="6e366-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="6e366-184">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="6e366-184">You have two options:</span></span>

* <span data-ttu-id="6e366-185">**匿名存取︰** 您可讓容器或其 blob 公開供匿名存取。</span><span class="sxs-lookup"><span data-stu-id="6e366-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="6e366-186">請參閱[管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6e366-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="6e366-187">**共用存取簽章：**提供共用的存取簽章 (SAS)，以您指定的權限，並在您指定的間隔上，提供儲存體帳戶中，委派的存取 tooa 資源的用戶端。</span><span class="sxs-lookup"><span data-stu-id="6e366-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="6e366-188">如需詳細資訊，請參閱 [使用共用存取簽章 (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 。</span><span class="sxs-lookup"><span data-stu-id="6e366-188">See [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="6e366-189">加密 blob 資料</span><span class="sxs-lookup"><span data-stu-id="6e366-189">Encrypting blob data</span></span>
<span data-ttu-id="6e366-190">Azure 儲存體支援 blob 資料在 hello 用戶端和伺服器 hello 上加密：</span><span class="sxs-lookup"><span data-stu-id="6e366-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="6e366-191">**用戶端加密：** hello.NET tooAzure 存放裝置，將上傳和下載 toohello 用戶端時解密資料之前可支援用戶端應用程式中的加密資料的儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="6e366-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="6e366-192">hello 程式庫也支援儲存體帳戶金鑰管理與 Azure 金鑰保存庫的整合。</span><span class="sxs-lookup"><span data-stu-id="6e366-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="6e366-193">如需詳細資訊，請參閱 [Microsoft Azure 儲存體的用戶端 .NET 加密](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 。</span><span class="sxs-lookup"><span data-stu-id="6e366-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span> <span data-ttu-id="6e366-194">另請參閱 [教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob](storage-encrypt-decrypt-blobs-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="6e366-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="6e366-195">**伺服器端加密**：Azure 儲存體現在支援伺服器端加密。</span><span class="sxs-lookup"><span data-stu-id="6e366-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="6e366-196">請參閱 [待用資料的 Azure 儲存體服務加密 (預覽)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6e366-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e366-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e366-197">Next steps</span></span>
<span data-ttu-id="6e366-198">現在，您學到的 Blob 儲存體的 hello 基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="6e366-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="6e366-199">Microsoft Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="6e366-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="6e366-200">[Microsoft Azure 儲存體總管 (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。</span><span class="sxs-lookup"><span data-stu-id="6e366-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="6e366-201">Blob 儲存體範例</span><span class="sxs-lookup"><span data-stu-id="6e366-201">Blob storage samples</span></span>
* [<span data-ttu-id="6e366-202">在 .NET 中開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="6e366-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="6e366-203">Blob 儲存體參考</span><span class="sxs-lookup"><span data-stu-id="6e366-203">Blob storage reference</span></span>
* [<span data-ttu-id="6e366-204">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="6e366-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="6e366-205">REST API 參考資料</span><span class="sxs-lookup"><span data-stu-id="6e366-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="6e366-206">概念性指南</span><span class="sxs-lookup"><span data-stu-id="6e366-206">Conceptual guides</span></span>
* [<span data-ttu-id="6e366-207">使用 hello AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="6e366-207">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="6e366-208">開始使用適用於 .NET 的檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="6e366-208">Get started with File storage for .NET</span></span>](../files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="6e366-209">如何 toouse Azure blob 儲存體與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="6e366-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
