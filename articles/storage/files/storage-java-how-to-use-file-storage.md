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
ms.openlocfilehash: be71a946604da8af0130f101f2eb6135c5e08abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="6937c-103">使用 Java 開發 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="6937c-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="6937c-104">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="6937c-104">About this tutorial</span></span>
<span data-ttu-id="6937c-105">本教學課程將示範 hello 使用 Java toodevelop 應用程式或服務使用 Azure 檔案儲存體 toostore 檔案資料的基本概念。</span><span class="sxs-lookup"><span data-stu-id="6937c-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="6937c-106">在本教學課程中，我們將建立簡單的主控台應用程式，並顯示如何使用 Java 和 Azure 檔案儲存體 tooperform 基本動作：</span><span class="sxs-lookup"><span data-stu-id="6937c-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="6937c-107">建立及刪除 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="6937c-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="6937c-108">建立及刪除目錄</span><span class="sxs-lookup"><span data-stu-id="6937c-108">Create and delete directories</span></span>
* <span data-ttu-id="6937c-109">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="6937c-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="6937c-110">上傳、下載及刪除檔案</span><span class="sxs-lookup"><span data-stu-id="6937c-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="6937c-111">因為可能透過 SMB 存取 Azure 檔案儲存體，所以可能 toowrite 簡單的應用程式存取 hello Azure 檔案共用使用 hello 標準的 Java I/O 類別。</span><span class="sxs-lookup"><span data-stu-id="6937c-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="6937c-112">本文將說明如何使用 toowrite 應用程式 hello Azure 儲存體 Java SDK，它會使用 hello [Azure 檔案儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 檔案存放裝置。</span><span class="sxs-lookup"><span data-stu-id="6937c-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="6937c-113">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="6937c-113">Create a Java application</span></span>
<span data-ttu-id="6937c-114">toobuild hello 範例，您將需要 hello Java Development Kit (JDK) 和 hello [Azure 儲存體 SDK for Java] []。</span><span class="sxs-lookup"><span data-stu-id="6937c-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="6937c-115">您也應該建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6937c-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="6937c-116">設定您的應用程式 toouse Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="6937c-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="6937c-117">toouse hello Azure 儲存體應用程式開發介面，加入下列陳述式 toohello 頂端 hello Java 檔案，但您想從 tooaccess hello 儲存體服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="6937c-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="6937c-118">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="6937c-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="6937c-119">toouse Azure 檔案儲存體，您需要 tooconnect tooyour Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6937c-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="6937c-120">hello 第一個步驟就是，我們將使用的連接字串 tooconfigure tooconnect tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6937c-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="6937c-121">讓我們來定義靜態變數 toodo 的。</span><span class="sxs-lookup"><span data-stu-id="6937c-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="6937c-122">Your_storage_account_name 和 your_storage_account_key 取代 hello 的儲存體帳戶的實際值。</span><span class="sxs-lookup"><span data-stu-id="6937c-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="6937c-123">連接 tooan Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6937c-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="6937c-124">tooconnect tooyour 儲存體帳戶，您需要 toouse hello **CloudStorageAccount**物件，傳遞連接字串 tooits**剖析**方法。</span><span class="sxs-lookup"><span data-stu-id="6937c-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="6937c-125">**CloudStorageAccount.parse**擲回 InvalidKeyException，因此您需要 tooput 內部 try/catch 區塊。</span><span class="sxs-lookup"><span data-stu-id="6937c-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="6937c-126">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="6937c-126">Create an Azure File share</span></span>
<span data-ttu-id="6937c-127">Azure 檔案儲存體中的所有檔案和目錄都位於名為 [共用] 的容器中。</span><span class="sxs-lookup"><span data-stu-id="6937c-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="6937c-128">您的儲存體帳戶可以有帳戶容量允許數量的共用。</span><span class="sxs-lookup"><span data-stu-id="6937c-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="6937c-129">tooobtain 存取 tooa 共用和其內容，您會需要 toouse Azure 檔案儲存體用戶端。</span><span class="sxs-lookup"><span data-stu-id="6937c-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="6937c-130">使用 hello Azure 檔案儲存體用戶端，您可以再取得參考 tooa 共用。</span><span class="sxs-lookup"><span data-stu-id="6937c-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="6937c-131">tooactually 建立 hello 共用，請使用 hello **createIfNotExists** hello CloudFileShare 物件的方法。</span><span class="sxs-lookup"><span data-stu-id="6937c-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="6937c-132">此時，**共用**保存參考 tooa 共用名為**sampleshare**。</span><span class="sxs-lookup"><span data-stu-id="6937c-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="6937c-133">刪除 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="6937c-133">Delete an Azure File share</span></span>
<span data-ttu-id="6937c-134">刪除共用由呼叫 hello **deleteIfExists** CloudFileShare 物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="6937c-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="6937c-135">以下是執行該作業的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="6937c-135">Here's sample code that does that.</span></span>

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

## <a name="create-a-directory"></a><span data-ttu-id="6937c-136">建立目錄</span><span class="sxs-lookup"><span data-stu-id="6937c-136">Create a directory</span></span>
<span data-ttu-id="6937c-137">您也可以管理儲存體放而不需要全部都在 hello 根目錄的子目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="6937c-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="6937c-138">Azure 檔案儲存體可讓您 toocreate 因為允許使用您的帳戶會盡量目錄。</span><span class="sxs-lookup"><span data-stu-id="6937c-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="6937c-139">hello 的下列程式碼會建立名為子目錄**sampledir** hello 根目錄下。</span><span class="sxs-lookup"><span data-stu-id="6937c-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

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

## <a name="delete-a-directory"></a><span data-ttu-id="6937c-140">刪除目錄</span><span class="sxs-lookup"><span data-stu-id="6937c-140">Delete a directory</span></span>
<span data-ttu-id="6937c-141">刪除目錄是相當簡單的工作，不過請注意您無法刪除仍然包含檔案或其他目錄的目錄。</span><span class="sxs-lookup"><span data-stu-id="6937c-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="6937c-142">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="6937c-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="6937c-143">取得共用內檔案和目錄的清單很容易，只要在 CloudFileDirectory 參考上呼叫 **listFilesAndDirectories** 即可。</span><span class="sxs-lookup"><span data-stu-id="6937c-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="6937c-144">hello 方法會傳回您可以在逐一查看 ListFileItem 物件的清單。</span><span class="sxs-lookup"><span data-stu-id="6937c-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="6937c-145">例如，hello 下列程式碼會列出檔案和目錄內 hello 根目錄。</span><span class="sxs-lookup"><span data-stu-id="6937c-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="6937c-146">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="6937c-146">Upload a file</span></span>
<span data-ttu-id="6937c-147">Azure 檔案共用，其中包含在 hello 非常少，檔案可以所在的根目錄。</span><span class="sxs-lookup"><span data-stu-id="6937c-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="6937c-148">在本節中，您將學習如何 tooupload 檔案從本機儲存體 hello 到根目錄的共用。</span><span class="sxs-lookup"><span data-stu-id="6937c-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="6937c-149">hello 中上傳檔案的第一個步驟是 tooobtain 它所在的位置參考 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="6937c-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="6937c-150">您可以呼叫 hello **getRootDirectoryReference** hello 共用物件的方法。</span><span class="sxs-lookup"><span data-stu-id="6937c-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="6937c-151">有參考 toohello 根目錄的 hello 共用之後，您可以上傳檔案到它使用下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="6937c-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="6937c-152">下載檔案</span><span class="sxs-lookup"><span data-stu-id="6937c-152">Download a file</span></span>
<span data-ttu-id="6937c-153">Hello 更頻繁的作業，您將會執行對 Azure 檔案儲存體的其中一個是 toodownload 檔案。</span><span class="sxs-lookup"><span data-stu-id="6937c-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="6937c-154">在下列範例的 hello，下載 SampleFile.txt hello 程式碼，並顯示其內容。</span><span class="sxs-lookup"><span data-stu-id="6937c-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="6937c-155">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="6937c-155">Delete a file</span></span>
<span data-ttu-id="6937c-156">另一個常見的 Azure 檔案儲存體作業是刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="6937c-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="6937c-157">hello 下列程式碼會刪除名為 SampleFile.txt 儲存目錄內名為**sampledir**。</span><span class="sxs-lookup"><span data-stu-id="6937c-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6937c-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6937c-158">Next steps</span></span>
<span data-ttu-id="6937c-159">如果您想要深入了解其他 Azure 儲存體 Api toolearn，請遵循這些連結。</span><span class="sxs-lookup"><span data-stu-id="6937c-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="6937c-160">[適用於 Java 開發人員的 Azure](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="6937c-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="6937c-161">Azure Storage SDK for Java</span><span class="sxs-lookup"><span data-stu-id="6937c-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="6937c-162">Azure Storage SDK for Android</span><span class="sxs-lookup"><span data-stu-id="6937c-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="6937c-163">Azure 儲存體用戶端 SDK 參考</span><span class="sxs-lookup"><span data-stu-id="6937c-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="6937c-164">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="6937c-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="6937c-165">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="6937c-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="6937c-166">[使用 AzCopy 命令列公用程式的 hello 傳輸資料](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="6937c-166">[Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>