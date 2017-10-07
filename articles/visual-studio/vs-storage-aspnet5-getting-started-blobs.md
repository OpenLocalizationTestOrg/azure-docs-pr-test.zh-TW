---
title: "使用 blob 儲存體和 Visual Studio 啟動 aaaGet 已連線的服務 (ASP.NET Core) |Microsoft 文件"
description: "Tooget 如何啟動建立儲存體帳戶，使用 Visual Studio 之後，Visual Studio ASP.NET Core 專案中使用 Azure Blob 儲存體已連接服務"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀
本文章說明如何 tooget 啟動 Visual Studio 中使用 Azure Blob 儲存體之後您建立或使用 hello Visual Studio 加入已連接服務對話方塊參考 Azure 儲存體帳戶中的 ASP.NET Core 專案。

Azure Blob 儲存體是用於儲存大量非結構化資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。 單一 Blob 可以是任何大小。 Blob 可以是影像、音訊和視訊檔、原始資料及文件檔案。 本文說明如何 tooget 開始使用 blob 儲存體使用 hello Visual Studio 建立 Azure 儲存體帳戶之後**加入已連接服務**ASP.NET Core 專案中的對話方塊。

就像檔案在資料夾中一樣，儲存體 Blob 位於容器中。 您已建立儲存體之後，您會建立一個或多個容器在 hello 儲存體中。 比方說，在儲存裝置，稱為 「 之前 」，您可以建立稱為 「 影像 」 toostore 圖片的 hello 儲存體中的容器和另一個名為"音訊"toostore 音訊檔案。 建立 hello 容器之後，您可以上傳個別 blob 檔案 toothem。 如需以程式設計方式處理 Blob 的詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 。

## <a name="access-blob-containers-in-code"></a>在程式碼中存取 blob 容器
tooprogrammatically ASP.NET Core 專案中的存取 blob，您需要下列項目，tooadd hello，如果它們不存在。

1. 新增下列程式碼命名空間宣告 toohello 任何 C# 檔案頂端想 tooprogrammatically 存取 Azure 儲存體的 hello。
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. 取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。 您的儲存體連接字串和 hello Azure 服務組態的儲存體帳戶資訊，請使用下列程式碼 tooget hello。
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **注意：** hello 下列各節中使用所有的 hello hello 程式碼前面的程式碼上方。
3. 使用**CloudBlobClient**物件 tooget **CloudBlobContainer**參考 tooan 現有容器儲存體帳戶中的。
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>在程式碼中建立容器
您也可以使用 hello **CloudBlobClient** toocreate 儲存體帳戶中的容器。 您只需要 toodo 太 tooadd 呼叫**CreateIfNotExistsAsync**如 hello 下列程式碼所示：

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**注意：** hello 執行呼叫 tooAzure 儲存體中 ASP.NET Core Api 是非同步。 如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。 下列程式碼 hello 假設正在使用非同步程式設計的方法。

hello 容器可用 tooeveryone 內 toomake hello 檔案，您可以設定 hello 容器 toobe 公用使用下列程式碼的 hello。

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
tooupload blob 檔案至容器，來取得容器的參考，並將它 tooget blob 參考。 Blob 參考之後，您可以上傳任何資料流的資料 tooit 呼叫 hello **UploadFromStreamAsync**方法。 如果它不存在，會覆寫它存在的話，這項作業會建立 hello blob。 下列範例會示範如何 hello tooupload blob 容器，並假設已建立該 hello 容器。

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
toolist hello blob 容器中的第一次取得容器的參考。 接著，您可以呼叫 hello 容器**ListBlobsSegmentedAsync**方法 tooretrieve hello blob 及/或目錄內。 tooaccess hello 豐富的屬性和方法傳回**IListBlobItem**，您必須將它轉換 tooa **CloudBlockBlob**， **CloudPageBlob**，或**CloudBlobDirectory**物件。 如果您不知道輸入 hello blob，您可以使用型別檢查 toodetermine 哪些 toocast 它。 下列程式碼的 hello 示範 tooretrieve 和輸出 hello URI 的容器中的每個項目。

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

還有其他方式 toolist hello blob 容器的內容。 如需詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) 。

## <a name="download-a-blob"></a>下載 Blob
toodownload blob，第一次取得參考 toohello blob，然後再呼叫 hello **DownloadToStreamAsync**方法。 hello 下列範例會使用 hello **DownloadToStreamAsync**方法 tootransfer hello blob 內容 tooa 資料流物件，您可以再將儲存為本機檔案。

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

還有其他方式 toosave blob 檔案。 如需詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) 。

## <a name="delete-a-blob"></a>刪除 Blob
toodelete blob，第一次取得參考 toohello blob，然後再呼叫 hello **DeleteAsync**方法。

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>後續步驟
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

