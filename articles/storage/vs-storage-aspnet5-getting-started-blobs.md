---
title: "開始使用 Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET Core) | Microsoft Docs"
description: "在使用 Visual Studio 已連接服務建立儲存體帳戶之後，如何在 Visual Studio ASP.NET Core 專案中開始使用 Azure Blob 儲存體"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e725015c8be7ecfa908f0ae75986b73f218fa3ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="ba5bc-103">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="ba5bc-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="ba5bc-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ba5bc-104">Overview</span></span>
<span data-ttu-id="ba5bc-105">本文說明如何在您使用 Visual Studio 的 [新增已連接服務] 對話方塊建立或參考了 ASP.NET Core 專案中的 Azure 儲存體帳戶之後，開始在 Visual Studio 使用 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="ba5bc-106">Azure 二進位大型物件 (Microsoft Azure Blob) 儲存是一項儲存大量非結構化資料的服務，全球任何地方都可透過 HTTP 或 HTTPS 來存取這些資料。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="ba5bc-107">單一 Blob 可以是任何大小。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-107">A single blob can be any size.</span></span> <span data-ttu-id="ba5bc-108">Blob 可以是影像、音訊和視訊檔、原始資料及文件檔案。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="ba5bc-109">本文描述如何在您於 ASP.NET Core 專案中使用 Visual Studio 的 [新增已連接服務] 對話方塊建立 Azure 儲存體帳戶之後，開始使用 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="ba5bc-110">就像檔案在資料夾中一樣，儲存體 Blob 位於容器中。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="ba5bc-111">在您已建立儲存體之後，您會在儲存體中建立一個或多個容器。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="ba5bc-112">例如，在稱為 "Scrapbook" 的儲存體中，您可以在儲存體中建立稱為 "images" 的容器來儲存圖片，並建立稱為 "audio" 的容器來儲存音訊檔。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="ba5bc-113">建立容器之後，就可以將個別的 Blob 檔案上傳至這些容器。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="ba5bc-114">如需以程式設計方式處理 Blob 的詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md) 。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="ba5bc-115">在程式碼中存取 blob 容器</span><span class="sxs-lookup"><span data-stu-id="ba5bc-115">Access blob containers in code</span></span>
<span data-ttu-id="ba5bc-116">若要以程式設計方式存取 ASP.NET Core 專案中的 Blob，您需要加入下列項目 (如果它們尚不存在)。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="ba5bc-117">將下列程式碼命名空間宣告，新增至您想要在其中以程式設計方式存取 Azure 儲存體之任何 C# 檔案內的頂端。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="ba5bc-118">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ba5bc-119">使用下列程式碼，從 Azure 服務組態取得您的儲存體連接字串和儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="ba5bc-120">**注意：** 請在後續小節中的程式碼前面使用上述所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="ba5bc-121">使用 **CloudBlobClient** 物件，以取得儲存體帳戶中現有容器的 **CloudBlobContainer** 參考。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="ba5bc-122">在程式碼中建立容器</span><span class="sxs-lookup"><span data-stu-id="ba5bc-122">Create a container in code</span></span>
<span data-ttu-id="ba5bc-123">您也可以使用 **CloudBlobClient** ，在儲存體帳戶中建立容器。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="ba5bc-124">您只需加入 **CreateIfNotExistsAsync** 的呼叫即可，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="ba5bc-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="ba5bc-125">**注意：**對 ASP.NET Core 中的 Azure 儲存體執行呼叫的 API 是非同步的。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="ba5bc-126">如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="ba5bc-127">以下程式碼假設使用非同步程式設計方法。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="ba5bc-128">若要讓所有人都能使用容器中的檔案，您可以使用下列程式碼將容器設定為公用容器。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ba5bc-129">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="ba5bc-129">Upload a blob into a container</span></span>
<span data-ttu-id="ba5bc-130">若要將 Blob 檔案上傳至容器，請取得容器參考，並使用該參考來取得 Blob 參考。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="ba5bc-131">擁有 Blob 參考後，即可藉由呼叫 **UploadFromStreamAsync** 方法，將任何資料流上傳至其中。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="ba5bc-132">此作業會在 Blob 不存在的情況下建立 Blob，並在存在的情況下予以覆寫。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="ba5bc-133">下列範例顯示如何將 Blob 上傳到容器，並假設已建立該容器。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="ba5bc-134">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="ba5bc-134">List the blobs in a container</span></span>
<span data-ttu-id="ba5bc-135">若要列出容器中的 Blob，請先取得容器參照。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="ba5bc-136">然後您即可呼叫容器的 **ListBlobsSegmentedAsync** 方法來擷取其中的 Blob 和/或目錄。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="ba5bc-137">若要針對傳回的 **IListBlobItem** 存取一組豐富的屬性與方法，您必須先將它轉換至 **CloudBlockBlob**、**CloudPageBlob** 或 **CloudBlobDirectory** 物件。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="ba5bc-138">如果不知道 Blob 類型，可使用類型檢查來決定要將它轉換成何種類型。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="ba5bc-139">下列程式碼示範如何擷取和輸出容器中每個項目的 URI。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

<span data-ttu-id="ba5bc-140">還有其他方法可列出 Blob 容器的內容。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="ba5bc-141">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) 。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="ba5bc-142">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="ba5bc-142">Download a blob</span></span>
<span data-ttu-id="ba5bc-143">若要下載 Blob，請先取得 Blob 的參考，然後呼叫 **DownloadToStreamAsync** 方法。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="ba5bc-144">下列範例會使用 **DownloadToStreamAsync** 方法，將 Blob 內容傳送給資料流物件，您接著可將該物件儲存為本機檔案。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="ba5bc-145">還有其他方法可將 Blob 儲存為檔案。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="ba5bc-146">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md#download-blobs) 。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="ba5bc-147">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="ba5bc-147">Delete a blob</span></span>
<span data-ttu-id="ba5bc-148">若要刪除 Blob，請先取得 Blob 的參考，然後對其呼叫 **DeleteAsync** 方法。</span><span class="sxs-lookup"><span data-stu-id="ba5bc-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="ba5bc-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba5bc-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

