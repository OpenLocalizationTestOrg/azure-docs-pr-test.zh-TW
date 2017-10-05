---
title: "以 .NET 開始使用 Azure Blob 儲存體 (物件儲存體) | Microsoft Docs"
description: "使用 Azure Blob 儲存體 (物件儲存體) 在雲端中儲存非結構化資料。"
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
ms.openlocfilehash: 8393b2dc32f01cac301c713c2ae9f0ab7226ea37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="a8b5f-103">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a8b5f-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="a8b5f-104">Azure Blob 儲存體是可將非結構化的資料儲存在雲端作為物件/blob 的服務。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-104">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="a8b5f-105">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="a8b5f-106">Blob 儲存體也稱為物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-106">Blob storage is also referred to as object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="a8b5f-107">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="a8b5f-107">About this tutorial</span></span>
<span data-ttu-id="a8b5f-108">本教學課程說明如何使用 Azure Blob 儲存體撰寫一些常見案例的 .NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-108">This tutorial shows how to write .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="a8b5f-109">所涵蓋的案例包括上傳、列出、下載及刪除 Blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="a8b5f-110">**必要條件：**</span><span class="sxs-lookup"><span data-stu-id="a8b5f-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="a8b5f-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8b5f-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="a8b5f-112">適用於 .NET 的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="a8b5f-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="a8b5f-113">適用於.NET 的 Azure 設定管理員</span><span class="sxs-lookup"><span data-stu-id="a8b5f-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="a8b5f-114">[Azure 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="a8b5f-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="a8b5f-115">更多範例</span><span class="sxs-lookup"><span data-stu-id="a8b5f-115">More samples</span></span>
<span data-ttu-id="a8b5f-116">如需使用 Blob 儲存體的其他範例，請參閱 [在 .NET 中開始使用 Azure Blob 儲存體](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="a8b5f-117">您可以下載範例應用程式並加以執行，或瀏覽 GitHub 上的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-117">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="a8b5f-118">新增 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="a8b5f-118">Add using directives</span></span>
<span data-ttu-id="a8b5f-119">將下列 using 指示詞新增至 `Program.cs` 檔案的開頭處：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-119">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="a8b5f-120">解析連接字串</span><span class="sxs-lookup"><span data-stu-id="a8b5f-120">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-blob-service-client"></a><span data-ttu-id="a8b5f-121">建立 Blob 服務用戶端</span><span class="sxs-lookup"><span data-stu-id="a8b5f-121">Create the Blob service client</span></span>
<span data-ttu-id="a8b5f-122">**CloudBlobClient** 類別可讓您擷取 Blob 儲存體中儲存的容器和 Blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-122">The **CloudBlobClient** class enables you to retrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="a8b5f-123">以下是建立服務用戶端的其中一種方式：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-123">Here's one way to create the service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="a8b5f-124">您現在可以開始撰寫程式碼，以讀取 Blob 儲存體的資料並將資料寫入其中。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-124">Now you are ready to write code that reads data from and writes data to Blob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="a8b5f-125">建立容器</span><span class="sxs-lookup"><span data-stu-id="a8b5f-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="a8b5f-126">此範例說明如何建立尚不存在的容器：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-126">This example shows how to create a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="a8b5f-127">根據預設，新容器屬私人性質，這表示您必須指定儲存體存取金鑰才能從此容器下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-127">By default, the new container is private, meaning that you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="a8b5f-128">若要讓所有人都能使用容器中的檔案，您可以使用下列程式碼將容器設定為公用容器：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-128">If you want to make the files within the container available to everyone, you can set the container to be public using the following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="a8b5f-129">網際網路上的任何人都可以看到公用容器中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-129">Anyone on the Internet can see blobs in a public container.</span></span> <span data-ttu-id="a8b5f-130">不過，要有適當的帳戶存取金鑰或共用存取簽章，才能修改或刪除這些 Blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-130">However, you can modify or delete them only if you have the appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="a8b5f-131">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="a8b5f-131">Upload a blob into a container</span></span>
<span data-ttu-id="a8b5f-132">Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="a8b5f-133">在大部分情況下，建議使用區塊 Blob 的類型。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-133">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="a8b5f-134">若要將檔案上傳至區塊 Blob，請取得容器參照，並使用該參照來取得區塊 Blob 參照。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-134">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="a8b5f-135">擁有 Blob 參照後，即可藉由呼叫 **UploadFromStream** 方法，將任何資料流上傳至其中。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-135">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="a8b5f-136">此操作會建立 Blob (如果其並不存在) 或覆寫 Blob (如果其已存在)。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-136">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="a8b5f-137">下列範例顯示如何將 Blob 上傳到容器，並假設已建立該容器。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-137">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite the "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="a8b5f-138">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="a8b5f-138">List the blobs in a container</span></span>
<span data-ttu-id="a8b5f-139">若要列出容器中的 Blob，請先取得容器參照。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-139">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="a8b5f-140">然後您即可使用容器的 **ListBlobs** 方法來擷取 Blob 和 (或) 其中的目錄。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-140">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="a8b5f-141">若要針對傳回的 **IListBlobItem** 存取一組豐富的屬性與方法，您必須先將它轉換至 **CloudBlockBlob**、**CloudPageBlob** 或 **CloudBlobDirectory** 物件。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-141">To access the  rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="a8b5f-142">如果不清楚類型，可使用類型檢查來決定要將其轉換至何種類型。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-142">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="a8b5f-143">下列程式碼示範如何擷取和輸出 _photos_ 容器中每個項目的 URI：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-143">The following code demonstrates how to retrieve and output the URI of each item in the _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within the container and output the length and URI.
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

<span data-ttu-id="a8b5f-144">在 Blob 名稱中包含路徑資訊，您可以建立虛擬目錄結構，讓您能夠組織及周遊，就像使用傳統檔案系統一樣。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="a8b5f-145">目錄結構僅限虛擬目錄結構--Blob 儲存體中唯一可用的資源為容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-145">The directory structure is virtual only--the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="a8b5f-146">但是，儲存體用戶端程式庫提供 **CloudBlobDirectory** 物件來參照虛擬目錄，以及簡化透過此方式組織之 blob 的使用程序。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-146">However, the storage client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="a8b5f-147">例如，假設名為 *photos* 的容器中有下列一組區塊 Blob：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-147">For example, consider the following set of block blobs in a container named *photos*:</span></span>

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

<span data-ttu-id="a8b5f-148">當您在 *photos* 容器上呼叫 **ListBlobs** (如上面程式碼片段所示) 時，會傳回階層式清單。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-148">When you call **ListBlobs** on the *photos* container (as in the preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="a8b5f-149">它包含 **CloudBlobDirectory** 和 **CloudBlockBlob** 物件，分別代表容器中的目錄與 blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing the directories and blobs in the container, respectively.</span></span> <span data-ttu-id="a8b5f-150">輸出結果看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-150">The resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="a8b5f-151">此外，您可以選擇將 **ListBlobs** 方法的 **UseFlatBlobListing** 參數設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-151">Optionally, you can set the **UseFlatBlobListing** parameter of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="a8b5f-152">在此案例中，容器中的每個 blob 都是以 **CloudBlockBlob** 物件的方式傳回。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-152">In this case, every blob in the container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="a8b5f-153">呼叫 **ListBlobs** 會傳回簡單列表，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-153">The call to **ListBlobs** to return a flat listing looks like this:</span></span>

```csharp
// Loop over items within the container and output the length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="a8b5f-154">而且結果看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-154">and the results look like this:</span></span>

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

## <a name="download-blobs"></a><span data-ttu-id="a8b5f-155">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="a8b5f-155">Download blobs</span></span>
<span data-ttu-id="a8b5f-156">若要下載 Blob，請先擷取 Blob 參照，然後呼叫 **DownloadToStream** 方法。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-156">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="a8b5f-157">下列範例使用 **DownloadToStream** 方法將 Blob 內容傳送給資料流物件，您接著可將該物件永久儲存成本機檔案。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-157">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents to a file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="a8b5f-158">您也可以使用 **DownloadToStream** 方法，將 Blob 的內容當成文字字串下載。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-158">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="a8b5f-159">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="a8b5f-159">Delete blobs</span></span>
<span data-ttu-id="a8b5f-160">若要刪除 Blob，請先取得 Blob 參照，然後在該參照上呼叫 **Delete** 方法。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-160">To delete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete the blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="a8b5f-161">以非同步方式分頁列出 Blob</span><span class="sxs-lookup"><span data-stu-id="a8b5f-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="a8b5f-162">如果您要列出大量的 Blob，或是要控制在單一列出作業中傳回的結果數，您可以在結果頁面中列出 Blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-162">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="a8b5f-163">此範例說明如何以非同步方式分頁傳回結果，使執行不會因為等待大型結果集傳回而中斷。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-163">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="a8b5f-164">此範例說明一般 Blob 列出方式，但您也可以執行階層式清單，方法是將 **ListBlobsSegmentedAsync** 方法的 _useFlatBlobListing_ 參數設為 _false_。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the _useFlatBlobListing_ parameter of the **ListBlobsSegmentedAsync** method to _false_.</span></span>

<span data-ttu-id="a8b5f-165">範例方法會呼叫非同步方法，因此前面必須加上 _async_ 關鍵字，且必須傳回 **Task** 物件。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-165">Because the sample method calls an asynchronous method, it must be prefaced with the _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="a8b5f-166">為 **ListBlobsSegmentedAsync** 方法指定的 await 關鍵字會擱置範例方法的執行，直到列出工作完成為止。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-166">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs to the console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
    //When the continuation token is null, the last page has been returned and execution can exit the loop.
    do
    {
        //This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get the continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="a8b5f-167">寫入附加 Blob</span><span class="sxs-lookup"><span data-stu-id="a8b5f-167">Writing to an append blob</span></span>
<span data-ttu-id="a8b5f-168">附加 Blob 已針對附加作業 (例如紀錄) 最佳化。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="a8b5f-169">如同區塊 Blob，附加 Blob 亦由區塊組成，但當您將新區塊加入附加 Blob 時，它一律會附加到 Blob 結尾。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="a8b5f-170">您無法更新或刪除附加 Blob 中的現有區塊。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="a8b5f-171">附加 Blob 的區塊識別碼不會公開顯示，因為該識別碼適用於區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-171">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="a8b5f-172">附加 Blob 中的每個區塊大小都不同，最大為 4 MB，而附加 Blob 可包含高達 50,000 個區塊。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-172">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="a8b5f-173">因此，附加 Blob 的大小上限稍高於 195 GB (4 MB X 50,000 個區塊)。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-173">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="a8b5f-174">下列範例中建立了新的附加 Blob，並附加一些資料，以模擬簡單的記錄作業。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-174">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```csharp
//Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create the container if it does not already exist.
container.CreateIfNotExists();

//Get a reference to an append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create the append blob. Note that if the blob already exists, the CreateOrReplace() method will overwrite it.
//You can check whether the blob exists to avoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data to the end of the append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read the append blob to the console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="a8b5f-175">如需了解有關 Blob 的三種類型間差異的資訊，請參閱 [了解區塊 Blob、分頁 Blob 和附加 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) 。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about the differences between the three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="a8b5f-176">管理 Blob 安全性</span><span class="sxs-lookup"><span data-stu-id="a8b5f-176">Managing security for blobs</span></span>
<span data-ttu-id="a8b5f-177">根據預設，Azure 儲存體會限制擁有帳戶存取金鑰的帳戶擁有者的存取權來保持資料安全。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-177">By default, Azure Storage keeps your data secure by limiting access to the account owner, who is in possession of the account access keys.</span></span> <span data-ttu-id="a8b5f-178">當您需要共用儲存體帳戶中的 Blob 資料時，請注意不可危及您帳戶存取金鑰的安全性。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-178">When you need to share blob data in your storage account, it is important to do so without compromising the security of your account access keys.</span></span> <span data-ttu-id="a8b5f-179">此外，您可以加密 blob 資料以確保透過網路與 Azure 儲存體中的安全。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-179">Additionally, you can encrypt blob data to ensure that it is secure going over the wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-to-blob-data"></a><span data-ttu-id="a8b5f-180">控制對 blob 資料的存取</span><span class="sxs-lookup"><span data-stu-id="a8b5f-180">Controlling access to blob data</span></span>
<span data-ttu-id="a8b5f-181">根據預設，您儲存體帳戶中的 blob 資料僅供儲存體帳戶擁有者使用。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-181">By default, the blob data in your storage account is accessible only to storage account owner.</span></span> <span data-ttu-id="a8b5f-182">依預設，驗證對 Blob 儲存體的要求需要帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-182">Authenticating requests against Blob storage requires the account access key by default.</span></span> <span data-ttu-id="a8b5f-183">不過，您可能想要讓特定的 blob 資料可供其他使用者使用。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-183">However, you may wish to make certain blob data available to other users.</span></span> <span data-ttu-id="a8b5f-184">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="a8b5f-184">You have two options:</span></span>

* <span data-ttu-id="a8b5f-185">**匿名存取︰** 您可讓容器或其 blob 公開供匿名存取。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="a8b5f-186">如需詳細資訊，請參閱 [管理對容器和 Blob 的匿名讀取權限](storage-manage-access-to-resources.md) 。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-186">See [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="a8b5f-187">**共用存取簽章︰** 您可為用戶端提供共用存取簽章 (SAS)，可利用您指定的權限以及透過您指定的間隔，在儲存體帳戶中提供資源的委派存取。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access to a resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="a8b5f-188">如需詳細資訊，請參閱 [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="a8b5f-189">加密 blob 資料</span><span class="sxs-lookup"><span data-stu-id="a8b5f-189">Encrypting blob data</span></span>
<span data-ttu-id="a8b5f-190">Azure 儲存體支援在用戶端和伺服器上加密 blob 資料︰</span><span class="sxs-lookup"><span data-stu-id="a8b5f-190">Azure Storage supports encrypting blob data both at the client and on the server:</span></span>

* <span data-ttu-id="a8b5f-191">**用戶端加密：** 支援在上傳至 Azure 儲存體之前將用戶端應用程式內的資料加密，並在下載至用戶端時解密資料。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-191">**Client-side encryption:** The Storage Client Library for .NET supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="a8b5f-192">程式庫也支援與 Azure 金鑰保存庫整合，以進行儲存體帳戶金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-192">The library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="a8b5f-193">如需詳細資訊，請參閱 [Microsoft Azure 儲存體的用戶端 .NET 加密](storage-client-side-encryption.md) 。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="a8b5f-194">另請參閱 [教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob](storage-encrypt-decrypt-blobs-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="a8b5f-195">**伺服器端加密**：Azure 儲存體現在支援伺服器端加密。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="a8b5f-196">請參閱 [待用資料的 Azure 儲存體服務加密 (預覽)](storage-service-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8b5f-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8b5f-197">Next steps</span></span>
<span data-ttu-id="a8b5f-198">了解 Blob 儲存體的基礎概念之後，請使用下列連結深入了解。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-198">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="a8b5f-199">Microsoft Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="a8b5f-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="a8b5f-200">[Microsoft Azure 儲存體總管 (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="a8b5f-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="a8b5f-201">Blob 儲存體範例</span><span class="sxs-lookup"><span data-stu-id="a8b5f-201">Blob storage samples</span></span>
* [<span data-ttu-id="a8b5f-202">在 .NET 中開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="a8b5f-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="a8b5f-203">Blob 儲存體參考</span><span class="sxs-lookup"><span data-stu-id="a8b5f-203">Blob storage reference</span></span>
* [<span data-ttu-id="a8b5f-204">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="a8b5f-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="a8b5f-205">REST API 參考資料</span><span class="sxs-lookup"><span data-stu-id="a8b5f-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="a8b5f-206">概念性指南</span><span class="sxs-lookup"><span data-stu-id="a8b5f-206">Conceptual guides</span></span>
* [<span data-ttu-id="a8b5f-207">使用 AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="a8b5f-207">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="a8b5f-208">開始使用適用於 .NET 的檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="a8b5f-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="a8b5f-209">如何透過 WebJob SDK 使用 Azure Blob 儲存體 (英文)</span><span class="sxs-lookup"><span data-stu-id="a8b5f-209">How to use Azure blob storage with the WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
