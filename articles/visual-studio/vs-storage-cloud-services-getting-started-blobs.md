---
title: "開始使用 blob 儲存體和 Visual Studio 已連線的服務 （雲端服務） 的 aaaGet |Microsoft 文件"
description: "Tooget 啟動連接 tooa 儲存體帳戶，使用 Visual Studio 已連接服務之後，在 Visual Studio 中的雲端服務專案中使用 Azure Blob 儲存體的方式"
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
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (雲端服務專案)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀
本文說明如何 tooget 開始使用 Azure Blob 儲存體建立，或使用 Visual Studio hello 參考 Azure 儲存體帳戶之後**加入已連接服務**對話方塊，在 Visual Studio 的雲端服務專案。 我們將為您示範如何 tooaccess 並建立 blob 容器，以及如何 tooperform 常見工作： 上傳、 列出和下載 blob。 hello 範例以 C 撰寫\#並用 hello [Microsoft Azure 儲存體用戶端程式庫適用於.NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)。

Azure Blob 儲存體是用於儲存大量非結構化資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。 單一 Blob 可以是任何大小。 Blob 可以是影像、音訊和視訊檔、原始資料及文件檔案。

就像檔案在資料夾中一樣，儲存體 Blob 位於容器中。 您已建立儲存體之後，您會建立一個或多個容器在 hello 儲存體中。 比方說，在儲存裝置，稱為 「 之前 」，您可以建立稱為 「 影像 」 toostore 圖片的 hello 儲存體中的容器和另一個名為"音訊"toostore 音訊檔案。 建立 hello 容器之後，您可以上傳個別 blob 檔案 toothem。

* 如需以程式設計方式處理 Blob 的詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。
* 如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/)。
* 如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/)。
* 如需 ASP.NET 應用程式設計的詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。

## <a name="access-blob-containers-in-code"></a>在程式碼中存取 blob 容器
tooprogrammatically 雲端服務專案中的存取 blob，您需要下列項目，如果它們不存在的 tooadd hello。

1. 新增下列程式碼命名空間宣告 toohello 頂端的任何 C# 檔案中您想在其中 tooprogrammatically 存取 Azure 儲存體的 hello。
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. 取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。 下列程式碼 tooget 使用 hello hello 您的儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態。
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. 取得**CloudBlobClient**物件 tooreference 儲存體帳戶中現有的容器。
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. 取得**CloudBlobContainer** tooreference 特定 blob 容器的物件。
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> 使用所有 hello hello hello hello 下列各節所示的程式碼前面的上一個程序所示的程式碼。
> 
> 

## <a name="create-a-container-in-code"></a>在程式碼中建立容器
> [!NOTE]
> 在 ASP.NET 中執行 tooAzure 儲存體對外呼叫，某些應用程式開發介面都是非同步的。 如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。 hello hello 下列範例中的程式碼會假設您使用非同步程式設計的方法。
> 
> 

toocreate 儲存體帳戶中的容器，您只需要 toodo 會加入呼叫太**CreateIfNotExistsAsync**如 hello 下列程式碼所示：

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


hello 容器可用 tooeveryone 內 toomake hello 檔案，您可以設定 hello 容器 toobe 公用使用下列程式碼的 hello。

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Hello 網際網路上的任何人可以看到公用容器中的 blob，但您可以修改或刪除它們，只有當您擁有 hello 適當的存取金鑰。

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
Azure 儲存體支援區塊 Blob 和頁面 Blob。 Hello 大部分的情況下，在區塊 blob 會是建議的型別 toouse hello。

tooupload 檔案 tooa 區塊 blob，取得容器的參考，並將它 tooget 區塊 blob 參考。 Blob 參考之後，您可以上傳任何資料流的資料 tooit 呼叫 hello **UploadFromStream**方法。 如果它先前不存在，會覆寫它存在的話，這項作業會建立 hello blob。 下列範例會示範如何 hello tooupload blob 容器，並假設已建立該 hello 容器。

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
toolist hello blob 容器中的第一次取得容器的參考。 然後，您可以使用 hello 容器**ListBlobs**方法 tooretrieve hello blob 及/或目錄內。 tooaccess hello 豐富的屬性和方法傳回**IListBlobItem**，您必須將它轉換 tooa **CloudBlockBlob**， **CloudPageBlob**，或**CloudBlobDirectory**物件。 如果 hello 類型都屬未知，您可以使用型別檢查 toodetermine 哪些 toocast 它。 hello 下列程式碼示範如何 tooretrieve 和輸出 hello hello 中每個項目的 URI**相片**容器：

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

Hello 上述程式碼範例所示，hello blob 服務會有 hello 概念以及容器內的目錄。 正因如此，您能夠以更像資料夾的結構組織 Blob。 例如，請考慮下列名為的容器中的區塊 blob 的整組 hello**相片**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

當您呼叫**ListBlobs** hello 容器 （hello 先前如範例所示），傳回的 hello 集合包含**CloudBlobDirectory**和**CloudBlockBlob**物件代表 hello 目錄和包含在 hello 最上層的 blob。 以下是 hello 產生的輸出：

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


您可以選擇性地設定 hello **UseFlatBlobListing**參數的 hello **ListBlobs**方法**true**。 如此會導致不論目錄為何，都將每個 Blob 當成 **CloudBlockBlob**傳回。 以下是太 hello 呼叫**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

和 hello 結果如下：

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

如需詳細資訊，請參閱 [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx)。

## <a name="download-blobs"></a>下載 Blob
toodownload blob，先擷取 blob 的參考，然後再呼叫 hello **DownloadToStream**方法。 hello 下列範例會使用 hello **DownloadToStream**方法 tootransfer hello blob 內容 tooa 資料流物件，您可以再保存 tooa 本機檔案。

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

您也可以使用 hello **DownloadToStream**方法 toodownload hello 內容為文字字串的 blob。

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>刪除 Blob
toodelete blob，先取得 blob 的參考，然後呼叫**刪除**方法。

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>以非同步方式分頁列出 Blob
如果在列示大量的 blob，或想讓您在一個清單作業中傳回的結果 toocontrol hello 數目，您可以列出結果的頁面中的 blob。 這個範例會示範如何 tooreturn 結果頁面中以非同步的方式，以便在等候 tooreturn 大型的結果集時不會封鎖執行。

此範例顯示一般 blob 清單，但您也可以執行階層式清單中，設定 hello **useFlatBlobListing** hello 參數**ListBlobsSegmentedAsync**方法太**false**。

Hello 範例方法會呼叫非同步方法，因為它前面都必須以 hello**非同步**關鍵字，而且必須傳回**工作**物件。 hello await 關鍵字指定 hello **ListBlobsSegmentedAsync**方法暫停執行 hello 取樣方法，直到 hello 清單的工作完成。

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

## <a name="next-steps"></a>後續步驟
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

