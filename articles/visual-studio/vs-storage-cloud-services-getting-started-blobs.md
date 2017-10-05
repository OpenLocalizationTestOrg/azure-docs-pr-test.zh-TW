---
title: "開始使用 Blob 儲存體和 Visual Studio 已連接服務 (雲端服務) | Microsoft Docs"
description: "在使用 Visual Studio 已連接服務連接到儲存體帳戶之後，如何於 Visual Studio 雲端服務專案中開始使用 Azure Blob 儲存體"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: cf14880c70f90b01c5dffbfe434150581c2ec33b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="482e8-103">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (雲端服務專案)</span><span class="sxs-lookup"><span data-stu-id="482e8-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="482e8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="482e8-104">Overview</span></span>
<span data-ttu-id="482e8-105">本文描述如何在 Visual Studio 雲端服務專案中使用 [ **加入已連接服務** ] 對話方塊建立或參考 Azure 儲存體帳戶後，開始搭配使用 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="482e8-105">This article describes how to get started with Azure Blob Storage after you created or referenced an Azure Storage account by using the Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="482e8-106">我們會說明如何存取及建立 Blob 容器，以及如何執行上傳、列出和下載 Blob 等一般工作。</span><span class="sxs-lookup"><span data-stu-id="482e8-106">We'll show you how to access and create blob containers, and how to perform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="482e8-107">這些範例均以 C\# 撰寫，並使用 [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="482e8-107">The samples are written in C\# and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="482e8-108">Azure 二進位大型物件 (Microsoft Azure Blob) 儲存是一項儲存大量非結構化資料的服務，全球任何地方都可透過 HTTP 或 HTTPS 來存取這些資料。</span><span class="sxs-lookup"><span data-stu-id="482e8-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="482e8-109">單一 Blob 可以是任何大小。</span><span class="sxs-lookup"><span data-stu-id="482e8-109">A single blob can be any size.</span></span> <span data-ttu-id="482e8-110">Blob 可以是影像、音訊和視訊檔、原始資料及文件檔案。</span><span class="sxs-lookup"><span data-stu-id="482e8-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="482e8-111">就像檔案在資料夾中一樣，儲存體 Blob 位於容器中。</span><span class="sxs-lookup"><span data-stu-id="482e8-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="482e8-112">在您已建立儲存體之後，您會在儲存體中建立一個或多個容器。</span><span class="sxs-lookup"><span data-stu-id="482e8-112">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="482e8-113">例如，在稱為 "Scrapbook" 的儲存體中，您可以在儲存體中建立稱為 "images" 的容器來儲存圖片，並建立稱為 "audio" 的容器來儲存音訊檔。</span><span class="sxs-lookup"><span data-stu-id="482e8-113">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="482e8-114">建立容器之後，就可以將個別的 Blob 檔案上傳至這些容器。</span><span class="sxs-lookup"><span data-stu-id="482e8-114">After you create the containers, you can upload individual blob files to them.</span></span>

* <span data-ttu-id="482e8-115">如需以程式設計方式處理 Blob 的詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="482e8-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="482e8-116">如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="482e8-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="482e8-117">如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/)。</span><span class="sxs-lookup"><span data-stu-id="482e8-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="482e8-118">如需 ASP.NET 應用程式設計的詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。</span><span class="sxs-lookup"><span data-stu-id="482e8-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="482e8-119">在程式碼中存取 blob 容器</span><span class="sxs-lookup"><span data-stu-id="482e8-119">Access blob containers in code</span></span>
<span data-ttu-id="482e8-120">若要以程式設計方式存取雲端服務中的 blob，您需要加入下列項目 (如果尚未存在)。</span><span class="sxs-lookup"><span data-stu-id="482e8-120">To programmatically access blobs in cloud service projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="482e8-121">將下列程式碼命名空間宣告，新增至您想要在其中以程式設計方式存取 Azure 儲存體之任何 C# 檔案內的頂端。</span><span class="sxs-lookup"><span data-stu-id="482e8-121">Add the following code namespace declarations to the top of any C# file in which you wish to programmatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="482e8-122">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="482e8-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="482e8-123">使用下列程式碼，從 Azure 服務組態取得您的儲存體連接字串和儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="482e8-123">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="482e8-124">取得 **CloudBlobClient** 物件，來參考儲存體帳戶中的現有容器。</span><span class="sxs-lookup"><span data-stu-id="482e8-124">Get a **CloudBlobClient** object to reference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="482e8-125">取得 **CloudBlobContainer** 物件，以參考特定的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="482e8-125">Get a **CloudBlobContainer** object to reference a specific blob container.</span></span>
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="482e8-126">請將前一個程序中顯示的所有程式碼使用於後續章節中顯示的程式碼之前。</span><span class="sxs-lookup"><span data-stu-id="482e8-126">Use all of the code shown in the previous procedure in front of the code shown in the following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="482e8-127">在程式碼中建立容器</span><span class="sxs-lookup"><span data-stu-id="482e8-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="482e8-128">有些對外向 ASP.NET 中 Azure 儲存體執行呼叫的 API 是非同步的。</span><span class="sxs-lookup"><span data-stu-id="482e8-128">Some APIs that perform calls out to Azure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="482e8-129">如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="482e8-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="482e8-130">以下範例中的程式碼假設使用非同步程式設計方法。</span><span class="sxs-lookup"><span data-stu-id="482e8-130">The code in the following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="482e8-131">若要在儲存體帳戶中建立容器，您只需要新增對 **CreateIfNotExistsAsync** 的呼叫，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="482e8-131">To create a container in your storage account, all you need to do is add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="482e8-132">若要讓所有人都能使用容器中的檔案，您可以使用下列程式碼將容器設定為公用容器。</span><span class="sxs-lookup"><span data-stu-id="482e8-132">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="482e8-133">網際網路上的任何人都可以看到公用容器中的 Blob，但要有適當的存取金鑰，才能修改或刪除這些 Blob。</span><span class="sxs-lookup"><span data-stu-id="482e8-133">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="482e8-134">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="482e8-134">Upload a blob into a container</span></span>
<span data-ttu-id="482e8-135">Azure 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="482e8-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="482e8-136">在大多數情況下，建議使用區塊 Blob 的類型。</span><span class="sxs-lookup"><span data-stu-id="482e8-136">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="482e8-137">若要將檔案上傳至區塊 Blob，請取得容器參照，並使用該參照來取得區塊 Blob 參照。</span><span class="sxs-lookup"><span data-stu-id="482e8-137">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="482e8-138">擁有 Blob 參照後，即可藉由呼叫 **UploadFromStream** 方法，將任何資料流上傳至其中。</span><span class="sxs-lookup"><span data-stu-id="482e8-138">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="482e8-139">此操作會建立 Blob (如果其並不存在) 或覆寫 Blob (如果其已存在)。</span><span class="sxs-lookup"><span data-stu-id="482e8-139">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="482e8-140">下列範例顯示如何將 Blob 上傳到容器，並假設已建立該容器。</span><span class="sxs-lookup"><span data-stu-id="482e8-140">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Retrieve a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="482e8-141">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="482e8-141">List the blobs in a container</span></span>
<span data-ttu-id="482e8-142">若要列出容器中的 Blob，請先取得容器參照。</span><span class="sxs-lookup"><span data-stu-id="482e8-142">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="482e8-143">然後您即可使用容器的 **ListBlobs** 方法來擷取 Blob 和 (或) 其中的目錄。</span><span class="sxs-lookup"><span data-stu-id="482e8-143">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="482e8-144">若要針對傳回的 **IListBlobItem** 存取一組豐富的屬性與方法，您必須先將它轉換至 **CloudBlockBlob**、**CloudPageBlob** 或 **CloudBlobDirectory** 物件。</span><span class="sxs-lookup"><span data-stu-id="482e8-144">To access the rich set of properties and methods for a  returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="482e8-145">如果不清楚類型，可使用類型檢查來決定要將其轉換至何種類型。</span><span class="sxs-lookup"><span data-stu-id="482e8-145">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="482e8-146">下列程式碼示範如何擷取和輸出 **photos** 容器中每個項目的 URI：</span><span class="sxs-lookup"><span data-stu-id="482e8-146">The following code demonstrates how to retrieve and output the URI of each item in the **photos** container:</span></span>

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

<span data-ttu-id="482e8-147">如先前程式碼範例所示，Blob 服務也具備容器中之目錄的概念。</span><span class="sxs-lookup"><span data-stu-id="482e8-147">As shown in the previous code sample, the blob service has the concept of directories within containers, as well.</span></span> <span data-ttu-id="482e8-148">正因如此，您能夠以更像資料夾的結構組織 Blob。</span><span class="sxs-lookup"><span data-stu-id="482e8-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="482e8-149">例如，假設名為 **photos**的容器中有下列一組區塊 Blob：</span><span class="sxs-lookup"><span data-stu-id="482e8-149">For example, consider the following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="482e8-150">當您在容器上呼叫 **ListBlobs** (如上一個範例所示) 時，傳回的集合將包含 **CloudBlobDirectory** 和 **CloudBlockBlob** 物件，其分別代表最上層所包含的目錄和 Blob。</span><span class="sxs-lookup"><span data-stu-id="482e8-150">When you call **ListBlobs** on the container (as in the previous sample), the collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="482e8-151">以下是輸出結果：</span><span class="sxs-lookup"><span data-stu-id="482e8-151">Here is the resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="482e8-152">此外，您可以選擇將 **ListBlobs** 方法的 **UseFlatBlobListing** 參數設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="482e8-152">Optionally, you can set the **UseFlatBlobListing** parameter of of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="482e8-153">如此會導致不論目錄為何，都將每個 Blob 當成 **CloudBlockBlob**傳回。</span><span class="sxs-lookup"><span data-stu-id="482e8-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="482e8-154">以下是對 **ListBlobs**的呼叫︰</span><span class="sxs-lookup"><span data-stu-id="482e8-154">Here is the call to **ListBlobs**:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="482e8-155">其結果如下：</span><span class="sxs-lookup"><span data-stu-id="482e8-155">and here are the results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="482e8-156">如需詳細資訊，請參閱 [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx)。</span><span class="sxs-lookup"><span data-stu-id="482e8-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="482e8-157">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="482e8-157">Download blobs</span></span>
<span data-ttu-id="482e8-158">若要下載 Blob，請先擷取 Blob 參照，然後呼叫 **DownloadToStream** 方法。</span><span class="sxs-lookup"><span data-stu-id="482e8-158">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="482e8-159">下列範例使用 **DownloadToStream** 方法將 Blob 內容傳送給資料流物件，您接著可將該物件永久儲存成本機檔案。</span><span class="sxs-lookup"><span data-stu-id="482e8-159">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents to a file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="482e8-160">您也可以使用 **DownloadToStream** 方法，將 Blob 的內容當成文字字串下載。</span><span class="sxs-lookup"><span data-stu-id="482e8-160">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

    // Get a reference to a blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="482e8-161">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="482e8-161">Delete blobs</span></span>
<span data-ttu-id="482e8-162">若要刪除 Blob，請先取得 Blob 參考，然後呼叫 **Delete** 方法。</span><span class="sxs-lookup"><span data-stu-id="482e8-162">To delete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="482e8-163">以非同步方式分頁列出 Blob</span><span class="sxs-lookup"><span data-stu-id="482e8-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="482e8-164">如果您要列出大量的 Blob，或是要控制在單一列出作業中傳回的結果數，您可以在結果頁面中列出 Blob。</span><span class="sxs-lookup"><span data-stu-id="482e8-164">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="482e8-165">此範例說明如何以非同步方式分頁傳回結果，使執行不會因為等待大型結果集傳回而中斷。</span><span class="sxs-lookup"><span data-stu-id="482e8-165">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="482e8-166">此範例說明一般 Blob 列出方式，但您也可以執行階層式清單，方法是將 **ListBlobsSegmentedAsync** 方法的 **useFlatBlobListing** 參數設為 **false**。</span><span class="sxs-lookup"><span data-stu-id="482e8-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the **useFlatBlobListing** parameter of the **ListBlobsSegmentedAsync** method to **false**.</span></span>

<span data-ttu-id="482e8-167">範例方法會呼叫非同步方法，因此前面必須加上 **async** 關鍵字，且必須傳回 **Task** 物件。</span><span class="sxs-lookup"><span data-stu-id="482e8-167">Because the sample method calls an asynchronous method, it must be prefaced with the **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="482e8-168">為 **ListBlobsSegmentedAsync** 方法指定的 await 關鍵字會擱置範例方法的執行，直到列出工作完成為止。</span><span class="sxs-lookup"><span data-stu-id="482e8-168">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs to the console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
        // When the continuation token is null, the last page has been returned and execution can exit the loop.
        do
        {
            // This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="482e8-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="482e8-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

