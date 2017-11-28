---
title: "開始使用 blob 儲存體和 Visual Studio 已連線的服務 （雲端服務） 的 aaaGet |Microsoft 文件"
description: "Tooget 啟動連接 tooa 儲存體帳戶，使用 Visual Studio 已連接服務之後，在 Visual Studio 中的雲端服務專案中使用 Azure Blob 儲存體的方式"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="4a8f8-103">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (雲端服務專案)</span><span class="sxs-lookup"><span data-stu-id="4a8f8-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="4a8f8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4a8f8-104">Overview</span></span>
<span data-ttu-id="4a8f8-105">本文說明如何 tooget 開始使用 Azure Blob 儲存體建立，或使用 Visual Studio hello 參考 Azure 儲存體帳戶之後**加入已連接服務**對話方塊，在 Visual Studio 的雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="4a8f8-106">我們將為您示範如何 tooaccess 並建立 blob 容器，以及如何 tooperform 常見工作： 上傳、 列出和下載 blob。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="4a8f8-107">hello 範例以 C 撰寫\#並用 hello [Microsoft Azure 儲存體用戶端程式庫適用於.NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="4a8f8-108">Azure Blob 儲存體是用於儲存大量非結構化資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="4a8f8-109">單一 Blob 可以是任何大小。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-109">A single blob can be any size.</span></span> <span data-ttu-id="4a8f8-110">Blob 可以是影像、音訊和視訊檔、原始資料及文件檔案。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="4a8f8-111">就像檔案在資料夾中一樣，儲存體 Blob 位於容器中。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="4a8f8-112">您已建立儲存體之後，您會建立一個或多個容器在 hello 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="4a8f8-113">比方說，在儲存裝置，稱為 「 之前 」，您可以建立稱為 「 影像 」 toostore 圖片的 hello 儲存體中的容器和另一個名為"音訊"toostore 音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="4a8f8-114">建立 hello 容器之後，您可以上傳個別 blob 檔案 toothem。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="4a8f8-115">如需以程式設計方式處理 Blob 的詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="4a8f8-116">如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="4a8f8-117">如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/)。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="4a8f8-118">如需 ASP.NET 應用程式設計的詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="4a8f8-119">在程式碼中存取 blob 容器</span><span class="sxs-lookup"><span data-stu-id="4a8f8-119">Access blob containers in code</span></span>
<span data-ttu-id="4a8f8-120">tooprogrammatically 雲端服務專案中的存取 blob，您需要下列項目，如果它們不存在的 tooadd hello。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="4a8f8-121">新增下列程式碼命名空間宣告 toohello 頂端的任何 C# 檔案中您想在其中 tooprogrammatically 存取 Azure 儲存體的 hello。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="4a8f8-122">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="4a8f8-123">下列程式碼 tooget 使用 hello hello 您的儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="4a8f8-124">取得**CloudBlobClient**物件 tooreference 儲存體帳戶中現有的容器。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="4a8f8-125">取得**CloudBlobContainer** tooreference 特定 blob 容器的物件。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="4a8f8-126">使用所有 hello hello hello hello 下列各節所示的程式碼前面的上一個程序所示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="4a8f8-127">在程式碼中建立容器</span><span class="sxs-lookup"><span data-stu-id="4a8f8-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="4a8f8-128">在 ASP.NET 中執行 tooAzure 儲存體對外呼叫，某些應用程式開發介面都是非同步的。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="4a8f8-129">如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="4a8f8-130">hello hello 下列範例中的程式碼會假設您使用非同步程式設計的方法。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="4a8f8-131">toocreate 儲存體帳戶中的容器，您只需要 toodo 會加入呼叫太**CreateIfNotExistsAsync**如 hello 下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="4a8f8-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="4a8f8-132">hello 容器可用 tooeveryone 內 toomake hello 檔案，您可以設定 hello 容器 toobe 公用使用下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="4a8f8-133">Hello 網際網路上的任何人可以看到公用容器中的 blob，但您可以修改或刪除它們，只有當您擁有 hello 適當的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="4a8f8-134">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="4a8f8-134">Upload a blob into a container</span></span>
<span data-ttu-id="4a8f8-135">Azure 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="4a8f8-136">Hello 大部分的情況下，在區塊 blob 會是建議的型別 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="4a8f8-137">tooupload 檔案 tooa 區塊 blob，取得容器的參考，並將它 tooget 區塊 blob 參考。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="4a8f8-138">Blob 參考之後，您可以上傳任何資料流的資料 tooit 呼叫 hello **UploadFromStream**方法。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="4a8f8-139">如果它先前不存在，會覆寫它存在的話，這項作業會建立 hello blob。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="4a8f8-140">下列範例會示範如何 hello tooupload blob 容器，並假設已建立該 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="4a8f8-141">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="4a8f8-141">List hello blobs in a container</span></span>
<span data-ttu-id="4a8f8-142">toolist hello blob 容器中的第一次取得容器的參考。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="4a8f8-143">然後，您可以使用 hello 容器**ListBlobs**方法 tooretrieve hello blob 及/或目錄內。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="4a8f8-144">tooaccess hello 豐富的屬性和方法傳回**IListBlobItem**，您必須將它轉換 tooa **CloudBlockBlob**， **CloudPageBlob**，或**CloudBlobDirectory**物件。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="4a8f8-145">如果 hello 類型都屬未知，您可以使用型別檢查 toodetermine 哪些 toocast 它。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="4a8f8-146">hello 下列程式碼示範如何 tooretrieve 和輸出 hello hello 中每個項目的 URI**相片**容器：</span><span class="sxs-lookup"><span data-stu-id="4a8f8-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

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

<span data-ttu-id="4a8f8-147">Hello 上述程式碼範例所示，hello blob 服務會有 hello 概念以及容器內的目錄。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="4a8f8-148">正因如此，您能夠以更像資料夾的結構組織 Blob。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="4a8f8-149">例如，請考慮下列名為的容器中的區塊 blob 的整組 hello**相片**:</span><span class="sxs-lookup"><span data-stu-id="4a8f8-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="4a8f8-150">當您呼叫**ListBlobs** hello 容器 （hello 先前如範例所示），傳回的 hello 集合包含**CloudBlobDirectory**和**CloudBlockBlob**物件代表 hello 目錄和包含在 hello 最上層的 blob。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="4a8f8-151">以下是 hello 產生的輸出：</span><span class="sxs-lookup"><span data-stu-id="4a8f8-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="4a8f8-152">您可以選擇性地設定 hello **UseFlatBlobListing**參數的 hello **ListBlobs**方法**true**。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="4a8f8-153">如此會導致不論目錄為何，都將每個 Blob 當成 **CloudBlockBlob**傳回。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="4a8f8-154">以下是太 hello 呼叫**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="4a8f8-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="4a8f8-155">和 hello 結果如下：</span><span class="sxs-lookup"><span data-stu-id="4a8f8-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="4a8f8-156">如需詳細資訊，請參閱 [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="4a8f8-157">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="4a8f8-157">Download blobs</span></span>
<span data-ttu-id="4a8f8-158">toodownload blob，先擷取 blob 的參考，然後再呼叫 hello **DownloadToStream**方法。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="4a8f8-159">hello 下列範例會使用 hello **DownloadToStream**方法 tootransfer hello blob 內容 tooa 資料流物件，您可以再保存 tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="4a8f8-160">您也可以使用 hello **DownloadToStream**方法 toodownload hello 內容為文字字串的 blob。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="4a8f8-161">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="4a8f8-161">Delete blobs</span></span>
<span data-ttu-id="4a8f8-162">toodelete blob，先取得 blob 的參考，然後呼叫**刪除**方法。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="4a8f8-163">以非同步方式分頁列出 Blob</span><span class="sxs-lookup"><span data-stu-id="4a8f8-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="4a8f8-164">如果在列示大量的 blob，或想讓您在一個清單作業中傳回的結果 toocontrol hello 數目，您可以列出結果的頁面中的 blob。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="4a8f8-165">這個範例會示範如何 tooreturn 結果頁面中以非同步的方式，以便在等候 tooreturn 大型的結果集時不會封鎖執行。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="4a8f8-166">此範例顯示一般 blob 清單，但您也可以執行階層式清單中，設定 hello **useFlatBlobListing** hello 參數**ListBlobsSegmentedAsync**方法太**false**。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="4a8f8-167">Hello 範例方法會呼叫非同步方法，因為它前面都必須以 hello**非同步**關鍵字，而且必須傳回**工作**物件。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="4a8f8-168">hello await 關鍵字指定 hello **ListBlobsSegmentedAsync**方法暫停執行 hello 取樣方法，直到 hello 清單的工作完成。</span><span class="sxs-lookup"><span data-stu-id="4a8f8-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="4a8f8-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a8f8-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

