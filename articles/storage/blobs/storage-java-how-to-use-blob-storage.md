---
title: "aaaHow toouse 來自 Java 的 Azure Blob 儲存體 （物件儲存體） |Microsoft 文件"
description: "使用 Azure Blob 儲存體 （物件儲存體） 的 hello 雲端中儲存非結構化的資料。"
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: a905d318abdaa7538ec3f6b53b5186b965b8b86e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>如何從 Java 的 Blob 儲存體 toouse
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>概觀
Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。 Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 Blob 儲存體也是參考的 tooas 物件儲存體。

本文將告訴您如何使用 tooperform 常見案例 hello Microsoft Azure Blob 儲存體。 hello 範例以 Java 撰寫，並使用 hello [for Java 的 Azure 儲存體 SDK][Azure Storage SDK for Java]。 hello 涵蓋案例包括**上載**，**列出**，**下載**，和**刪除**blob。 如需有關 blob 的詳細資訊，請參閱 hello[接下來的步驟](#Next-Steps)> 一節。

> [!NOTE]
> 有一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。 如需詳細資訊，請參閱 hello[適用於 Android 的 Azure 儲存體 SDK][Azure Storage SDK for Android]。
>
>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>建立 Java 應用程式
在本文中，您將使用儲存體功能，這些功能可執行於本機的 Java 應用程式內，也可執行於在 Azure 中之 Web 角色或背景工作角色內執行的程式碼中。

toodo 因此，您將需要 tooinstall hello Java Development Kit (JDK)，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。 一旦您這樣做，您必須開發系統符合 hello 最低需求和相依性的 hello 中所列的 tooverify [for Java 的 Azure 儲存體 SDK] [ Azure Storage SDK for Java] GitHub 上的儲存機制。 如果您的系統符合這些需求，您可以遵循下載並安裝在您從該儲存機制的系統上的 hello Azure 儲存體 Libraries for Java 的 hello 指示。 當您完成這些工作時，您就會無法 toocreate hello 範例會使用這份文件中的 Java 應用程式。

## <a name="configure-your-application-tooaccess-blob-storage"></a>設定您的應用程式 tooaccess Blob 儲存體
新增下列匯入陳述式 toohello 想 toouse hello Azure 儲存體 Api tooaccess blob hello Java 檔案頂端的 hello。

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。 用戶端應用程式中執行時，您必須提供 hello 遵循格式，請使用 hello 您的儲存體帳戶名稱中的 hello 儲存體連接字串和 hello hello hello 中所列的儲存體帳戶的主要存取金鑰[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。 hello 下列範例示範如何宣告靜態欄位 toohold hello 連接字串。

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

在應用程式中執行 Microsoft Azure 中的角色，這個字串可以儲存在 hello 服務組態檔， *ServiceConfiguration.cscfg*，而且可以存取與呼叫 toohello **RoleEnvironment.getConfigurationSettings**方法。 hello 下列範例會取得連接字串 hello**設定**名*StorageConnectionString* hello 服務組態檔中。

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。

## <a name="create-a-container"></a>建立容器
**CloudBlobClient** 物件可讓您取得容器和 Blob 的參考物件。 hello 下列程式碼會建立**CloudBlobClient**物件。

> [!NOTE]
> 有其他方式 toocreate **CloudStorageAccount**物件; 如需詳細資訊，請參閱**CloudStorageAccount**在 hello [Azure 儲存體用戶端 SDK 參考]。
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

使用 hello **CloudBlobClient** tooget 想 toouse 參考 toohello 容器的物件。 如果以 hello 不存在，您可以建立 hello 容器**createIfNotExists**方法，否則會傳回 hello 現有容器。 根據預設，hello 新容器是私人的所以您必須指定儲存體存取金鑰 （如先前般） toodownload 從這個容器的 blob。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>選擇性步驟：設定公用存取的容器
根據預設，容器的權限設定為私用存取，但您可以輕鬆地在 hello 網際網路上設定容器的權限 tooallow 公用、 僅限讀取所有使用者的存取：

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
tooupload 檔案 tooa blob 取得容器的參考，並將它 tooget blob 參考。 Blob 參考之後，您可以藉由呼叫 hello blob 參考上的上傳來上傳任何資料流。 如果它不存在，或覆寫它，如果是的話，這項作業將會建立 hello blob。 hello，下列程式碼範例顯示，並假設已建立該 hello 容器。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
toolist hello blob 容器中的第一次取得容器的參考，像 tooupload blob。 您可以使用 hello 容器**listBlobs**方法**如**迴圈。 hello 下列程式碼輸出 hello 容器 toohello 主控台中每個 blob 的 Uri。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

請注意，為 Blob 命名時，您可以在其名稱中包含路徑資訊。 這會建立虛擬目錄結構，讓您能夠組織及周遊，就像使用傳統檔案系統一樣。 請注意，只是虛擬 hello 目錄結構-hello 只可用的資源在 Blob 儲存體不容器和 blob。 不過，hello 用戶端程式庫提供**CloudBlobDirectory**物件 toorefer tooa 虛擬目錄，並簡化 hello 程序會以這種方式組織的 blob 使用。

例如，您可能有名為 "photos" 的容器，當中您可能上傳名為 "rootphoto1"、"2010/photo1"、"2010/photo2" 和 "2011/photo1" 的 Blob。 這樣會建立 hello"2010"和"2011"hello"相片 」 容器內的虛擬目錄。 當您呼叫**listBlobs** hello 「 相片 」 容器，將會包含傳回 hello 集合**CloudBlobDirectory**和**CloudBlob**代表 hello 物件目錄和包含在 hello 最上層的 blob。 在此情況下，系統會傳回目錄 "2010" 和 "2011"，以及照片 "rootphoto1"。 您可以使用 hello **instanceof**運算子 toodistinguish 這些物件。

（選擇性） 您可以傳入參數 toohello **listBlobs**方法以 hello **useFlatBlobListing**參數設定 tootrue。 如此會導致不論目錄為何，都會傳回每個 Blob。 如需詳細資訊，請參閱**CloudBlobContainer.listBlobs**在 hello [Azure 儲存體用戶端 SDK 參考]。

## <a name="download-a-blob"></a>下載 Blob
toodownload blob，請遵循相同步驟與您上傳 blob 中的 blob 參考的順序 tooget hello。 在上傳範例 hello，您會在 hello blob 物件上呼叫上傳。 在下列範例的 hello，呼叫下載 tootransfer hello blob 內容 tooa 資料流物件，例如**FileOutputStream**您可以使用 toopersist hello blob tooa 本機檔案。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>刪除 Blob
toodelete blob、 取得 blob 參考，並呼叫**deleteIfExists**。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>刪除 Blob 容器
最後，toodelete blob 容器、 取得 blob 容器的參考，並呼叫**deleteIfExists**。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>後續步驟
現在，您學到的 Blob 儲存體的 hello 基本概念，請遵循這些連結 toolearn，更複雜的存放工作相關。

* [Azure Storage SDK for Java][Azure Storage SDK for Java]
* [Azure 儲存體用戶端 SDK 參考][Azure 儲存體用戶端 SDK 參考]
* [Azure 儲存體 REST API][Azure Storage REST API]
* [Azure 儲存體團隊部落格][Azure Storage Team Blog]

如需詳細資訊，另請參閱[適用於 Java 開發人員的 Azure](/java/azure)。

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 儲存體用戶端 SDK 參考]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
