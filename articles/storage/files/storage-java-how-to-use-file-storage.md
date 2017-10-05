---
title: "使用 Java 開發 Azure 檔案儲存體 | Microsoft Docs"
description: "了解如何開發使用 Azure 檔案儲存體來儲存檔案資料的 Java 應用程式和服務。"
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
ms.openlocfilehash: ce38944b9d5e663505c5808864ba61a5e2284f3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="bf7f0-103">使用 Java 開發 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="bf7f0-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="bf7f0-104">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="bf7f0-104">About this tutorial</span></span>
<span data-ttu-id="bf7f0-105">本教學課程將示範使用 Java 來開發使用 Azure 檔案儲存體來儲存檔案資料的應用程式和服務之基本概念。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="bf7f0-106">在本教學課程中，我們將建立簡單的主控台應用程式，並說明如何執行 Java 和 Azure 檔案儲存體的基本動作：</span><span class="sxs-lookup"><span data-stu-id="bf7f0-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="bf7f0-107">建立及刪除 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="bf7f0-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="bf7f0-108">建立及刪除目錄</span><span class="sxs-lookup"><span data-stu-id="bf7f0-108">Create and delete directories</span></span>
* <span data-ttu-id="bf7f0-109">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="bf7f0-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="bf7f0-110">上傳、下載及刪除檔案</span><span class="sxs-lookup"><span data-stu-id="bf7f0-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="bf7f0-111">由於 Azure 檔案儲存體可透過 SMB 存取，因此便可使用標準 Java I/O 類別撰寫簡單的應用程式以存取 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="bf7f0-112">本文將說明如何撰寫使用 Azure 儲存體 Java SDK 的應用程式，此應用程式將使用 [Azure 檔案儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) 與 Azure 檔案儲存體通訊。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="bf7f0-113">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="bf7f0-113">Create a Java application</span></span>
<span data-ttu-id="bf7f0-114">如要建置範例，您將需要 Java Development Kit (JDK) 和 適用於 Java 的 Azure 儲存體 SDK。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="bf7f0-115">您也應該建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="bf7f0-116">設定您的應用程式以使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="bf7f0-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="bf7f0-117">若要使用 Azure 儲存體 API，請將下列陳述式加入至您要從其存取儲存體服務的 Java 檔案頂端。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="bf7f0-118">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="bf7f0-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="bf7f0-119">若要使用 Azure 檔案儲存體，您必須連接到您的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="bf7f0-120">第一個步驟是設定連接字串，我們會用來連接到您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="bf7f0-121">讓我們定義靜態變數以便進行。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="bf7f0-122">將 your_storage_account_name 和 your_storage_account_key 取代為您的儲存體帳戶的實際值。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="bf7f0-123">連接到 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bf7f0-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="bf7f0-124">若要連接到您的儲存體帳戶，您必須使用 **CloudStorageAccount** 物件，將連接字串傳遞至其**剖析**方法。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="bf7f0-125">**CloudStorageAccount.parse** 會擲回 InvalidKeyException，因此您必須將其放在 try/catch 區塊內。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="bf7f0-126">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="bf7f0-126">Create an Azure File share</span></span>
<span data-ttu-id="bf7f0-127">Azure 檔案儲存體中的所有檔案和目錄都位於名為 [共用] 的容器中。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="bf7f0-128">您的儲存體帳戶可以有帳戶容量允許數量的共用。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="bf7f0-129">若要取得共用及其內容的存取權，您必須使用 Azure 檔案儲存體用戶端。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="bf7f0-130">使用 Azure 檔案儲存體用戶端，您可以取得共用的參考。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="bf7f0-131">若要實際建立共用，請使用 CloudFileShare 物件的 **createIfNotExists** 方法。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="bf7f0-132">目前，**共用**會將參考保留至名為 **sampleshare** 的共用。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="bf7f0-133">刪除 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="bf7f0-133">Delete an Azure File share</span></span>
<span data-ttu-id="bf7f0-134">刪除共用可以藉由在 CloudFileShare 物件呼叫 **deleteIfExists** 方法來完成。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="bf7f0-135">以下是執行該作業的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="bf7f0-136">建立目錄</span><span class="sxs-lookup"><span data-stu-id="bf7f0-136">Create a directory</span></span>
<span data-ttu-id="bf7f0-137">您也可以組織儲存體，方法是將檔案放在子目錄中，而不是將所有檔案都放在根目錄中。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="bf7f0-138">Azure 檔案儲存體可讓您建立您的帳戶允許數量的目錄。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="bf7f0-139">下列程式碼會在根目錄底下建立名為 **sampledir** 的子目錄。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="bf7f0-140">刪除目錄</span><span class="sxs-lookup"><span data-stu-id="bf7f0-140">Delete a directory</span></span>
<span data-ttu-id="bf7f0-141">刪除目錄是相當簡單的工作，不過請注意您無法刪除仍然包含檔案或其他目錄的目錄。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="bf7f0-142">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="bf7f0-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="bf7f0-143">取得共用內檔案和目錄的清單很容易，只要在 CloudFileDirectory 參考上呼叫 **listFilesAndDirectories** 即可。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="bf7f0-144">方法會傳回您可以逐一查看的 ListFileItem 物件清單。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="bf7f0-145">例如，下列程式碼會列出根目錄內的檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="bf7f0-146">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="bf7f0-146">Upload a file</span></span>
<span data-ttu-id="bf7f0-147">Azure 檔案共用至少包含根目錄，檔案可以放置其中。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="bf7f0-148">在本節中，您將學習如何從本機儲存體將檔案上傳至共用的根目錄。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="bf7f0-149">上傳檔案的第一個步驟是取得檔案所在之目錄的參考。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="bf7f0-150">您可以藉由呼叫共用物件的 **getRootDirectoryReference** 方法來完成。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="bf7f0-151">現在您具有共用之根目錄的參考，您可以使用下列程式碼上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="bf7f0-152">下載檔案</span><span class="sxs-lookup"><span data-stu-id="bf7f0-152">Download a file</span></span>
<span data-ttu-id="bf7f0-153">您針對 Azure 檔案儲存體執行的其中一個較頻繁作業是下載檔案。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="bf7f0-154">在下列範例中，程式碼會下載 SampleFile.txt，並顯示其內容。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="bf7f0-155">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="bf7f0-155">Delete a file</span></span>
<span data-ttu-id="bf7f0-156">另一個常見的 Azure 檔案儲存體作業是刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="bf7f0-157">下列程式碼會刪除儲存在名為 **sampledir**之目錄內名為 SampleFile.txt 的檔案。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="bf7f0-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf7f0-158">Next steps</span></span>
<span data-ttu-id="bf7f0-159">如果您想要深入了解其他 Azure 儲存體 API，請參考下列連結。</span><span class="sxs-lookup"><span data-stu-id="bf7f0-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="bf7f0-160">[適用於 Java 開發人員的 Azure](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="bf7f0-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="bf7f0-161">Azure Storage SDK for Java</span><span class="sxs-lookup"><span data-stu-id="bf7f0-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="bf7f0-162">Azure Storage SDK for Android</span><span class="sxs-lookup"><span data-stu-id="bf7f0-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="bf7f0-163">Azure 儲存體用戶端 SDK 參考</span><span class="sxs-lookup"><span data-stu-id="bf7f0-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="bf7f0-164">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="bf7f0-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="bf7f0-165">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="bf7f0-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="bf7f0-166">[使用 AzCopy 命令列公用程式傳輸資料](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="bf7f0-166">[Transfer data with the AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>