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
# <a name="get-started-with-azure-blob-storage-using-net"></a>以 .NET 開始使用 Azure Blob 儲存體

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。 Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 Blob 儲存體也是參考的 tooas 物件儲存體。

### <a name="about-this-tutorial"></a>關於本教學課程
本教學課程會示範如何 toowrite.NET 程式碼為使用 Azure Blob 儲存體的一些常見案例。 所涵蓋的案例包括上傳、列出、下載及刪除 Blob。

**必要條件：**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [適用於 .NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [適用於.NET 的 Azure 設定管理員](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>更多範例
如需使用 Blob 儲存體的其他範例，請參閱 [在 .NET 中開始使用 Azure Blob 儲存體](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)。 您可以下載 hello 範例應用程式並執行它，或瀏覽 hello GitHub 上的程式碼。

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>新增 using 指示詞
新增下列 hello**使用**指示詞 toohello 頂端 hello`Program.cs`檔案：

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>剖析 hello 連接字串
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>建立 hello Blob 服務用戶端
hello **CloudBlobClient**類別可讓您 tooretrieve 容器和 Blob 儲存體中的 blob。 以下是其中一種方式 toocreate hello 服務用戶端：

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
現在您已準備好 toowrite 讀取和寫入資料 tooBlob 儲存的程式碼。

## <a name="create-a-container"></a>建立容器
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

這個範例會示範如何 toocreate 如果不存在的容器：

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

根據預設，hello 新容器是私人的也就是說，您必須指定您的儲存體存取金鑰 toodownload blob，從這個容器。 如果您想在 hello 容器可用 tooeveryone toomake hello 檔案時，您可以設定 hello 容器 toobe 公用使用下列程式碼的 hello:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Hello 網際網路上的任何人可以看到公用容器中的 blob。 不過，您可以修改或刪除它們，只有當您擁有 hello 適當的帳戶存取金鑰或共用的存取簽章。

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。  在大部分情況下，區塊 blob 是建議的型別 toouse hello。

tooupload 檔案 tooa 區塊 blob，取得容器的參考，並將它 tooget 區塊 blob 參考。 Blob 參考之後，您可以上傳任何資料流的資料 tooit 呼叫 hello **UploadFromStream**方法。 如果它先前不存在，會覆寫它存在的話，這項作業會建立 hello blob。

下列範例會示範如何 hello tooupload blob 容器，並假設已建立該 hello 容器。

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

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
toolist hello blob 容器中的第一次取得容器的參考。 然後，您可以使用 hello 容器**ListBlobs**方法 tooretrieve hello blob 及/或目錄內。 tooaccess hello 豐富的屬性和方法傳回**IListBlobItem**，您必須將它轉換 tooa **CloudBlockBlob**， **CloudPageBlob**，或**CloudBlobDirectory**物件。 如果 hello 類型都屬未知，您可以使用型別檢查 toodetermine 哪些 toocast 它。 hello 下列程式碼示範如何 tooretrieve 和輸出 hello hello 中每個項目的 URI_相片_容器：

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

在 Blob 名稱中包含路徑資訊，您可以建立虛擬目錄結構，讓您能夠組織及周遊，就像使用傳統檔案系統一樣。 hello 目錄結構是虛擬只-hello 只可用在 Blob 儲存體資源是容器和 blob。 不過，hello 儲存體用戶端程式庫提供**CloudBlobDirectory**物件 toorefer tooa 虛擬目錄，並簡化 hello 程序會以這種方式組織的 blob 使用。

例如，請考慮下列名為的容器中的區塊 blob 的整組 hello*相片*:

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

當您呼叫**ListBlobs**上 hello*相片*容器 （例如 hello 前面程式碼片段)，則會傳回階層式清單。 它同時包含**CloudBlobDirectory**和**CloudBlockBlob**分別代表 hello 目錄和 hello 容器中的 blob 的物件。 hello 產生的輸出看起來像：

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

您可以選擇性地設定 hello **UseFlatBlobListing** hello 參數**ListBlobs**方法**true**。 在此情況下，hello 容器中的每個 blob 會當做傳回**CloudBlockBlob**物件。 太 hello 呼叫**ListBlobs** tooreturn 一般清單看起來像這樣：

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

和 hello 結果看起來像這樣：

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

## <a name="download-blobs"></a>下載 Blob
toodownload blob，先擷取 blob 的參考，然後再呼叫 hello **DownloadToStream**方法。 hello 下列範例會使用 hello **DownloadToStream**方法 tootransfer hello blob 內容 tooa 資料流物件，您可以再保存 tooa 本機檔案。

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

您也可以使用 hello **DownloadToStream**方法 toodownload hello 內容為文字字串的 blob。

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

## <a name="delete-blobs"></a>刪除 Blob
toodelete blob，先取得 blob 的參考，然後呼叫**刪除**方法。

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

## <a name="list-blobs-in-pages-asynchronously"></a>以非同步方式分頁列出 Blob
如果在列示大量的 blob，或想讓您在一個清單作業中傳回的結果 toocontrol hello 數目，您可以列出結果的頁面中的 blob。 這個範例會示範如何 tooreturn 結果頁面中以非同步的方式，以便在等候 tooreturn 大型的結果集時不會封鎖執行。

此範例顯示一般 blob 清單，但您也可以執行階層式清單中，設定 hello _useFlatBlobListing_ hello 參數**ListBlobsSegmentedAsync**方法 too_false_。

Hello 範例方法會呼叫非同步方法，因為它前面都必須以 hello_非同步_關鍵字，而且必須傳回**工作**物件。 hello await 關鍵字指定 hello **ListBlobsSegmentedAsync**方法暫停執行 hello 取樣方法，直到 hello 清單的工作完成。

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

## <a name="writing-tooan-append-blob"></a>寫入 tooan 附加 blob
附加 Blob 已針對附加作業 (例如紀錄) 最佳化。 為區塊 blob，例如附加 blob 區塊組成，但當您新增新的區塊 tooan 附加 blob 時，它一律是附加的 toohello hello blob 結尾。 您無法更新或刪除附加 Blob 中的現有區塊。 因為它們是區塊 blob，不會公開附加 blob 的 hello 區塊識別碼。

每個區塊中附加 blob 可以是不同的大小，tooa 最大值為 4 MB，總而且附加 blob 不可包括最多 50,000 個區塊。 hello 附加 blob 的大小上限，因此是稍微大於 195 GB （4 MB X 50000 區塊）。

hello 下面範例會建立新的附加 blob，並將附加一些資料 tooit，模擬簡單的記錄作業。

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

請參閱[了解區塊 Blob、 分頁 Blob，並附加 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)如需有關 hello hello 三種 blob 之間的差異。

## <a name="managing-security-for-blobs"></a>管理 Blob 安全性
根據預設，Azure 儲存體會保留您的資料安全，方法是限制存取 toohello 帳戶擁有者，並且擁有 hello 帳戶存取金鑰。 當您需要 tooshare blob 資料儲存體帳戶中時，很重要的 toodo 因此不會危及您的帳戶存取金鑰的 hello 安全性。 此外，您可以加密安全移 hello 網路與 Azure 儲存體中的 blob 資料 tooensure。

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>控制存取 tooblob 資料
根據預設，儲存體帳戶中的 hello blob 資料會是可存取的只有 toostorage 帳戶擁有者。 根據預設，驗證要求，針對 Blob 儲存體需要 hello 帳戶存取金鑰。 不過，您可能希望 toomake 特定 blob 資料可用 tooother 使用者。 您有兩個選擇：

* **匿名存取︰** 您可讓容器或其 blob 公開供匿名存取。 請參閱[管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)如需詳細資訊。
* **共用存取簽章：**提供共用的存取簽章 (SAS)，以您指定的權限，並在您指定的間隔上，提供儲存體帳戶中，委派的存取 tooa 資源的用戶端。 如需詳細資訊，請參閱 [使用共用存取簽章 (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 。

### <a name="encrypting-blob-data"></a>加密 blob 資料
Azure 儲存體支援 blob 資料在 hello 用戶端和伺服器 hello 上加密：

* **用戶端加密：** hello.NET tooAzure 存放裝置，將上傳和下載 toohello 用戶端時解密資料之前可支援用戶端應用程式中的加密資料的儲存體用戶端程式庫。 hello 程式庫也支援儲存體帳戶金鑰管理與 Azure 金鑰保存庫的整合。 如需詳細資訊，請參閱 [Microsoft Azure 儲存體的用戶端 .NET 加密](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 。 另請參閱 [教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob](storage-encrypt-decrypt-blobs-key-vault.md)。
* **伺服器端加密**：Azure 儲存體現在支援伺服器端加密。 請參閱 [待用資料的 Azure 儲存體服務加密 (預覽)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。

## <a name="next-steps"></a>後續步驟
現在，您學到的 Blob 儲存體的 hello 基本概念，請遵循這些連結 toolearn 更多。

### <a name="microsoft-azure-storage-explorer"></a>Microsoft Azure 儲存體總管
* [Microsoft Azure 儲存體總管 (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。

### <a name="blob-storage-samples"></a>Blob 儲存體範例
* [在 .NET 中開始使用 Azure Blob 儲存體](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Blob 儲存體參考
* [Storage Client Library for .NET 參考資料](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [REST API 參考資料](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>概念性指南
* [使用 hello AzCopy 命令列公用程式傳輸資料](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [開始使用適用於 .NET 的檔案儲存體](../files/storage-dotnet-how-to-use-files.md)
* [如何 toouse Azure blob 儲存體與 hello WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
