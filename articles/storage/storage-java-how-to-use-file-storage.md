---
title: "使用 Java 的 Azure 檔案儲存的 aaaDevelop |Microsoft 文件"
description: "了解 toodevelop Java 應用程式和服務使用 Azure 檔案儲存體 toostore 檔案資料。"
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>使用 Java 開發 Azure 檔案儲存體
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>關於本教學課程
本教學課程將示範 hello 使用 Java toodevelop 應用程式或服務使用 Azure 檔案儲存體 toostore 檔案資料的基本概念。 在本教學課程中，我們將建立簡單的主控台應用程式，並顯示如何使用 Java 和 Azure 檔案儲存體 tooperform 基本動作：

* 建立及刪除 Azure 檔案共用
* 建立及刪除目錄
* 列舉 Azure 檔案共用的檔案和目錄
* 上傳、下載及刪除檔案

> [!Note]  
> 因為可能透過 SMB 存取 Azure 檔案儲存體，所以可能 toowrite 簡單的應用程式存取 hello Azure 檔案共用使用 hello 標準的 Java I/O 類別。 本文將說明如何使用 toowrite 應用程式 hello Azure 儲存體 Java SDK，它會使用 hello [Azure 檔案儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 檔案存放裝置。

## <a name="create-a-java-application"></a>建立 Java 應用程式
toobuild hello 範例，您將需要 hello Java Development Kit (JDK) 和 hello [Azure 儲存體 SDK for Java] []。 您也應該建立 Azure 儲存體帳戶。

## <a name="setup-your-application-toouse-azure-file-storage"></a>設定您的應用程式 toouse Azure 檔案儲存體
toouse hello Azure 儲存體應用程式開發介面，加入下列陳述式 toohello 頂端 hello Java 檔案，但您想從 tooaccess hello 儲存體服務的 hello。

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
toouse Azure 檔案儲存體，您需要 tooconnect tooyour Azure 儲存體帳戶。 hello 第一個步驟就是，我們將使用的連接字串 tooconfigure tooconnect tooyour 儲存體帳戶。 讓我們來定義靜態變數 toodo 的。

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Your_storage_account_name 和 your_storage_account_key 取代 hello 的儲存體帳戶的實際值。
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>連接 tooan Azure 儲存體帳戶
tooconnect tooyour 儲存體帳戶，您需要 toouse hello **CloudStorageAccount**物件，傳遞連接字串 tooits**剖析**方法。

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse**擲回 InvalidKeyException，因此您需要 tooput 內部 try/catch 區塊。

## <a name="create-an-azure-file-share"></a>建立 Azure 檔案共用
Azure 檔案儲存體中的所有檔案和目錄都位於名為 [共用] 的容器中。 您的儲存體帳戶可以有帳戶容量允許數量的共用。 tooobtain 存取 tooa 共用和其內容，您會需要 toouse Azure 檔案儲存體用戶端。

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

使用 hello Azure 檔案儲存體用戶端，您可以再取得參考 tooa 共用。

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually 建立 hello 共用，請使用 hello **createIfNotExists** hello CloudFileShare 物件的方法。

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

此時，**共用**保存參考 tooa 共用名為**sampleshare**。

## <a name="delete-an-azure-file-share"></a>刪除 Azure 檔案共用
刪除共用由呼叫 hello **deleteIfExists** CloudFileShare 物件上的方法。 以下是執行該作業的範例程式碼。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a>建立目錄
您也可以管理儲存體放而不需要全部都在 hello 根目錄的子目錄中的檔案。 Azure 檔案儲存體可讓您 toocreate 因為允許使用您的帳戶會盡量目錄。 hello 的下列程式碼會建立名為子目錄**sampledir** hello 根目錄下。

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a>刪除目錄
刪除目錄是相當簡單的工作，不過請注意您無法刪除仍然包含檔案或其他目錄的目錄。

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>列舉 Azure 檔案共用的檔案和目錄
取得共用內檔案和目錄的清單很容易，只要在 CloudFileDirectory 參考上呼叫 **listFilesAndDirectories** 即可。 hello 方法會傳回您可以在逐一查看 ListFileItem 物件的清單。 例如，hello 下列程式碼會列出檔案和目錄內 hello 根目錄。

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>上傳檔案
Azure 檔案共用，其中包含在 hello 非常少，檔案可以所在的根目錄。 在本節中，您將學習如何 tooupload 檔案從本機儲存體 hello 到根目錄的共用。

hello 中上傳檔案的第一個步驟是 tooobtain 它所在的位置參考 toohello 目錄。 您可以呼叫 hello **getRootDirectoryReference** hello 共用物件的方法。

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

有參考 toohello 根目錄的 hello 共用之後，您可以上傳檔案到它使用下列程式碼的 hello。

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>下載檔案
Hello 更頻繁的作業，您將會執行對 Azure 檔案儲存體的其中一個是 toodownload 檔案。 在下列範例的 hello，下載 SampleFile.txt hello 程式碼，並顯示其內容。

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a>刪除檔案
另一個常見的 Azure 檔案儲存體作業是刪除檔案。 hello 下列程式碼會刪除名為 SampleFile.txt 儲存目錄內名為**sampledir**。

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a>後續步驟
如果您想要深入了解其他 Azure 儲存體 Api toolearn，請遵循這些連結。

* [Java 開發人員中心](http://azure.microsoft.com/develop/java/)
* [Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
* [Azure Storage SDK for Android](https://github.com/azure/azure-storage-android)
* [Azure 儲存體用戶端 SDK 參考](http://dl.windowsazure.com/storage/javadoc/)
* [Azure 儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)
* [使用 AzCopy 命令列公用程式的 hello 傳輸資料](storage-use-azcopy.md)
