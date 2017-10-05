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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀
本文說明如何在您使用 Visual Studio 的 [新增已連接服務] 對話方塊建立或參考了 ASP.NET Core 專案中的 Azure 儲存體帳戶之後，開始在 Visual Studio 使用 Azure Blob 儲存體。

Azure 二進位大型物件 (Microsoft Azure Blob) 儲存是一項儲存大量非結構化資料的服務，全球任何地方都可透過 HTTP 或 HTTPS 來存取這些資料。 單一 Blob 可以是任何大小。 Blob 可以是影像、音訊和視訊檔、原始資料及文件檔案。 本文描述如何在您於 ASP.NET Core 專案中使用 Visual Studio 的 [新增已連接服務] 對話方塊建立 Azure 儲存體帳戶之後，開始使用 Blob 儲存體。

就像檔案在資料夾中一樣，儲存體 Blob 位於容器中。 在您已建立儲存體之後，您會在儲存體中建立一個或多個容器。 例如，在稱為 "Scrapbook" 的儲存體中，您可以在儲存體中建立稱為 "images" 的容器來儲存圖片，並建立稱為 "audio" 的容器來儲存音訊檔。 建立容器之後，就可以將個別的 Blob 檔案上傳至這些容器。 如需以程式設計方式處理 Blob 的詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md) 。

## <a name="access-blob-containers-in-code"></a>在程式碼中存取 blob 容器
若要以程式設計方式存取 ASP.NET Core 專案中的 Blob，您需要加入下列項目 (如果它們尚不存在)。

1. 將下列程式碼命名空間宣告，新增至您想要在其中以程式設計方式存取 Azure 儲存體之任何 C# 檔案內的頂端。
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. 取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。 使用下列程式碼，從 Azure 服務組態取得您的儲存體連接字串和儲存體帳戶資訊。
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **注意：** 請在後續小節中的程式碼前面使用上述所有程式碼。
3. 使用 **CloudBlobClient** 物件，以取得儲存體帳戶中現有容器的 **CloudBlobContainer** 參考。
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>在程式碼中建立容器
您也可以使用 **CloudBlobClient** ，在儲存體帳戶中建立容器。 您只需加入 **CreateIfNotExistsAsync** 的呼叫即可，如下列程式碼所示：

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**注意：**對 ASP.NET Core 中的 Azure 儲存體執行呼叫的 API 是非同步的。 如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。 以下程式碼假設使用非同步程式設計方法。

若要讓所有人都能使用容器中的檔案，您可以使用下列程式碼將容器設定為公用容器。

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
若要將 Blob 檔案上傳至容器，請取得容器參考，並使用該參考來取得 Blob 參考。 擁有 Blob 參考後，即可藉由呼叫 **UploadFromStreamAsync** 方法，將任何資料流上傳至其中。 此作業會在 Blob 不存在的情況下建立 Blob，並在存在的情況下予以覆寫。 下列範例顯示如何將 Blob 上傳到容器，並假設已建立該容器。

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a>列出容器中的 Blob
若要列出容器中的 Blob，請先取得容器參照。 然後您即可呼叫容器的 **ListBlobsSegmentedAsync** 方法來擷取其中的 Blob 和/或目錄。 若要針對傳回的 **IListBlobItem** 存取一組豐富的屬性與方法，您必須先將它轉換至 **CloudBlockBlob**、**CloudPageBlob** 或 **CloudBlobDirectory** 物件。 如果不知道 Blob 類型，可使用類型檢查來決定要將它轉換成何種類型。 下列程式碼示範如何擷取和輸出容器中每個項目的 URI。

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

還有其他方法可列出 Blob 容器的內容。 如需詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) 。

## <a name="download-a-blob"></a>下載 Blob
若要下載 Blob，請先取得 Blob 的參考，然後呼叫 **DownloadToStreamAsync** 方法。 下列範例會使用 **DownloadToStreamAsync** 方法，將 Blob 內容傳送給資料流物件，您接著可將該物件儲存為本機檔案。

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

還有其他方法可將 Blob 儲存為檔案。 如需詳細資訊，請參閱 [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md#download-blobs) 。

## <a name="delete-a-blob"></a>刪除 Blob
若要刪除 Blob，請先取得 Blob 的參考，然後對其呼叫 **DeleteAsync** 方法。

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>後續步驟
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

