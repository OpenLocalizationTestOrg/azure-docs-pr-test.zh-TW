---
title: "使用 blob 儲存體和 Visual Studio 啟動 aaaGet 已連線的服務 (ASP.NET Core) |Microsoft 文件"
description: "Tooget 如何啟動建立儲存體帳戶，使用 Visual Studio 之後，Visual Studio ASP.NET Core 專案中使用 Azure Blob 儲存體已連接服務"
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
ms.openlocfilehash: a4c31c08c38d99eb9c66fe2af72ca42fa3804688
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="95e56-103">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="95e56-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="95e56-104">概觀</span><span class="sxs-lookup"><span data-stu-id="95e56-104">Overview</span></span>
<span data-ttu-id="95e56-105">本文章說明如何 tooget 啟動 Visual Studio 中使用 Azure Blob 儲存體之後您建立或使用 hello Visual Studio 加入已連接服務對話方塊參考 Azure 儲存體帳戶中的 ASP.NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="95e56-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="95e56-106">Azure Blob 儲存體是用於儲存大量非結構化資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="95e56-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="95e56-107">單一 Blob 可以是任何大小。</span><span class="sxs-lookup"><span data-stu-id="95e56-107">A single blob can be any size.</span></span> <span data-ttu-id="95e56-108">Blob 可以是影像、音訊和視訊檔、原始資料及文件檔案。</span><span class="sxs-lookup"><span data-stu-id="95e56-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="95e56-109">本文說明如何 tooget 開始使用 blob 儲存體使用 hello Visual Studio 建立 Azure 儲存體帳戶之後**加入已連接服務**ASP.NET Core 專案中的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="95e56-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="95e56-110">就像檔案在資料夾中一樣，儲存體 Blob 位於容器中。</span><span class="sxs-lookup"><span data-stu-id="95e56-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="95e56-111">您已建立儲存體之後，您會建立一個或多個容器在 hello 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="95e56-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="95e56-112">比方說，在儲存裝置，稱為 「 之前 」，您可以建立稱為 「 影像 」 toostore 圖片的 hello 儲存體中的容器和另一個名為"音訊"toostore 音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="95e56-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="95e56-113">建立 hello 容器之後，您可以上傳個別 blob 檔案 toothem。</span><span class="sxs-lookup"><span data-stu-id="95e56-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="95e56-114">如需以程式設計方式處理 Blob 的詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md) 。</span><span class="sxs-lookup"><span data-stu-id="95e56-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="95e56-115">在程式碼中存取 blob 容器</span><span class="sxs-lookup"><span data-stu-id="95e56-115">Access blob containers in code</span></span>
<span data-ttu-id="95e56-116">tooprogrammatically ASP.NET Core 專案中的存取 blob，您需要下列項目，tooadd hello，如果它們不存在。</span><span class="sxs-lookup"><span data-stu-id="95e56-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="95e56-117">新增下列程式碼命名空間宣告 toohello 任何 C# 檔案頂端想 tooprogrammatically 存取 Azure 儲存體的 hello。</span><span class="sxs-lookup"><span data-stu-id="95e56-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="95e56-118">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="95e56-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="95e56-119">您的儲存體連接字串和 hello Azure 服務組態的儲存體帳戶資訊，請使用下列程式碼 tooget hello。</span><span class="sxs-lookup"><span data-stu-id="95e56-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="95e56-120">**注意：** hello 下列各節中使用所有的 hello hello 程式碼前面的程式碼上方。</span><span class="sxs-lookup"><span data-stu-id="95e56-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="95e56-121">使用**CloudBlobClient**物件 tooget **CloudBlobContainer**參考 tooan 現有容器儲存體帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="95e56-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="95e56-122">在程式碼中建立容器</span><span class="sxs-lookup"><span data-stu-id="95e56-122">Create a container in code</span></span>
<span data-ttu-id="95e56-123">您也可以使用 hello **CloudBlobClient** toocreate 儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="95e56-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="95e56-124">您只需要 toodo 太 tooadd 呼叫**CreateIfNotExistsAsync**如 hello 下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="95e56-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="95e56-125">**注意：** hello 執行呼叫 tooAzure 儲存體中 ASP.NET Core Api 是非同步。</span><span class="sxs-lookup"><span data-stu-id="95e56-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="95e56-126">如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="95e56-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="95e56-127">下列程式碼 hello 假設正在使用非同步程式設計的方法。</span><span class="sxs-lookup"><span data-stu-id="95e56-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="95e56-128">hello 容器可用 tooeveryone 內 toomake hello 檔案，您可以設定 hello 容器 toobe 公用使用下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="95e56-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="95e56-129">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="95e56-129">Upload a blob into a container</span></span>
<span data-ttu-id="95e56-130">tooupload blob 檔案至容器，來取得容器的參考，並將它 tooget blob 參考。</span><span class="sxs-lookup"><span data-stu-id="95e56-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="95e56-131">Blob 參考之後，您可以上傳任何資料流的資料 tooit 呼叫 hello **UploadFromStreamAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="95e56-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="95e56-132">如果它不存在，會覆寫它存在的話，這項作業會建立 hello blob。</span><span class="sxs-lookup"><span data-stu-id="95e56-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="95e56-133">下列範例會示範如何 hello tooupload blob 容器，並假設已建立該 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="95e56-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="95e56-134">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="95e56-134">List hello blobs in a container</span></span>
<span data-ttu-id="95e56-135">toolist hello blob 容器中的第一次取得容器的參考。</span><span class="sxs-lookup"><span data-stu-id="95e56-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="95e56-136">接著，您可以呼叫 hello 容器**ListBlobsSegmentedAsync**方法 tooretrieve hello blob 及/或目錄內。</span><span class="sxs-lookup"><span data-stu-id="95e56-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="95e56-137">tooaccess hello 豐富的屬性和方法傳回**IListBlobItem**，您必須將它轉換 tooa **CloudBlockBlob**， **CloudPageBlob**，或**CloudBlobDirectory**物件。</span><span class="sxs-lookup"><span data-stu-id="95e56-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="95e56-138">如果您不知道輸入 hello blob，您可以使用型別檢查 toodetermine 哪些 toocast 它。</span><span class="sxs-lookup"><span data-stu-id="95e56-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="95e56-139">下列程式碼的 hello 示範 tooretrieve 和輸出 hello URI 的容器中的每個項目。</span><span class="sxs-lookup"><span data-stu-id="95e56-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

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

<span data-ttu-id="95e56-140">還有其他方式 toolist hello blob 容器的內容。</span><span class="sxs-lookup"><span data-stu-id="95e56-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="95e56-141">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) 。</span><span class="sxs-lookup"><span data-stu-id="95e56-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="95e56-142">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="95e56-142">Download a blob</span></span>
<span data-ttu-id="95e56-143">toodownload blob，第一次取得參考 toohello blob，然後再呼叫 hello **DownloadToStreamAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="95e56-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="95e56-144">hello 下列範例會使用 hello **DownloadToStreamAsync**方法 tootransfer hello blob 內容 tooa 資料流物件，您可以再將儲存為本機檔案。</span><span class="sxs-lookup"><span data-stu-id="95e56-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="95e56-145">還有其他方式 toosave blob 檔案。</span><span class="sxs-lookup"><span data-stu-id="95e56-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="95e56-146">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md#download-blobs) 。</span><span class="sxs-lookup"><span data-stu-id="95e56-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="95e56-147">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="95e56-147">Delete a blob</span></span>
<span data-ttu-id="95e56-148">toodelete blob，第一次取得參考 toohello blob，然後再呼叫 hello **DeleteAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="95e56-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="95e56-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95e56-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

