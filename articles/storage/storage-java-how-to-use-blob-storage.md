---
title: "如何從 Java 使用 Azure Blob 儲存體 (物件儲存體) | Microsoft Docs"
description: "使用 Azure Blob 儲存體 (物件儲存體) 在雲端中儲存非結構化資料。"
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
ms.openlocfilehash: b8a4eca600b458802a7a23851bb80ea4da2664ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-java"></a><span data-ttu-id="e482e-103">如何使用 Java 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e482e-103">How to use Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="e482e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e482e-104">Overview</span></span>
<span data-ttu-id="e482e-105">Azure Blob 儲存體是可將非結構化的資料儲存在雲端作為物件/blob 的服務。</span><span class="sxs-lookup"><span data-stu-id="e482e-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="e482e-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="e482e-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="e482e-107">Blob 儲存體也稱為物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="e482e-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="e482e-108">本文將示範如何使用 Microsoft Azure Blob 儲存體執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="e482e-108">This article will show you how to perform common scenarios using the Microsoft Azure Blob storage.</span></span> <span data-ttu-id="e482e-109">相關範例是以 Java 撰寫並使用 [Azure Storage SDK for Java][Azure Storage SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="e482e-109">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="e482e-110">所涵蓋的案例包括**上傳**、**列出**、**下載**及**刪除** Blob。</span><span class="sxs-lookup"><span data-stu-id="e482e-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="e482e-111">如需 Blob 的詳細資訊，請參閱[後續步驟](#Next-Steps)一節。</span><span class="sxs-lookup"><span data-stu-id="e482e-111">For more information on blobs, see the [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="e482e-112">有一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="e482e-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="e482e-113">如需詳細資訊，請參閱 [Azure Storage SDK for Android][Azure Storage SDK for Android]。</span><span class="sxs-lookup"><span data-stu-id="e482e-113">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="e482e-114">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="e482e-114">Create a Java application</span></span>
<span data-ttu-id="e482e-115">在本文中，您將使用儲存體功能，這些功能可執行於本機的 Java 應用程式內，也可執行於在 Azure 中之 Web 角色或背景工作角色內執行的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="e482e-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="e482e-116">若要這樣做，您需要安裝 Java Development Kit (JDK)，並在 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e482e-116">To do so, you will need to install the Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="e482e-117">完成此動作之後，您需要驗證開發系統符合 GitHub 上的 [Azure Storage SDK for Java][Azure Storage SDK for Java] 儲存機制中所列出的最低需求和相依性。</span><span class="sxs-lookup"><span data-stu-id="e482e-117">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="e482e-118">如果系統符合這些需求，則您可以依照指示，從該儲存機制中下載 Azure Storage Libraries for Java 並安裝在系統上。</span><span class="sxs-lookup"><span data-stu-id="e482e-118">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="e482e-119">完成這些工作之後，您就能夠利用本文中的範例來建立 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e482e-119">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="e482e-120">設定您的應用程式以存取 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e482e-120">Configure your application to access Blob storage</span></span>
<span data-ttu-id="e482e-121">在您要使用 Azure 儲存體 API 來存取 Blob 的 Java 檔案頂端，新增下列 import 陳述式。</span><span class="sxs-lookup"><span data-stu-id="e482e-121">Add the following import statements to the top of the Java file where you want to use the Azure Storage APIs to access blobs.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e482e-122">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="e482e-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="e482e-123">Azure 儲存體用戶端會使用儲存體連接字串來儲存存取資料管理服務時所用的端點與認證。</span><span class="sxs-lookup"><span data-stu-id="e482e-123">An Azure Storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="e482e-124">在用戶端應用程式中執行時，您必須以下列格式提供儲存體連接字串 (其中的 AccountName 和 AccountKey 值要使用您儲存體帳戶的名稱，以及在 [Azure 入口網站](https://portal.azure.com)中針對該儲存體帳戶而列出的主要存取金鑰)。</span><span class="sxs-lookup"><span data-stu-id="e482e-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="e482e-125">下列範例將示範如何宣告靜態欄位來存放連接字串。</span><span class="sxs-lookup"><span data-stu-id="e482e-125">The following example shows how you can declare a static field to hold the connection string.</span></span>

```java
// Define the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="e482e-126">在 Microsoft Azure 的角色內執行的應用程式中，此字串可以儲存在服務組態檔 *ServiceConfiguration.cscfg* 裡，且可以藉由呼叫 **RoleEnvironment.getConfigurationSettings** 方法來存取。</span><span class="sxs-lookup"><span data-stu-id="e482e-126">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="e482e-127">以下是從服務組態檔中名為 StorageConnectionString 的 **Setting** 元素取得連接字串的範例。</span><span class="sxs-lookup"><span data-stu-id="e482e-127">The following example gets the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="e482e-128">下列範例假設您已經使用這兩個方法之一來取得儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="e482e-128">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="e482e-129">建立容器</span><span class="sxs-lookup"><span data-stu-id="e482e-129">Create a container</span></span>
<span data-ttu-id="e482e-130">**CloudBlobClient** 物件可讓您取得容器和 Blob 的參考物件。</span><span class="sxs-lookup"><span data-stu-id="e482e-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="e482e-131">下列程式碼將建立 **CloudBlobClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="e482e-131">The following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="e482e-132">還有其他方法可建立 **CloudStorageAccount** 物件。如需詳細資訊，請參閱 [CloudBlobContainer.listBlobs]中的 **CloudStorageAccount**。</span><span class="sxs-lookup"><span data-stu-id="e482e-132">There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="e482e-133">使用 **CloudBlobClient** 物件來取得想要使用容器的參考。</span><span class="sxs-lookup"><span data-stu-id="e482e-133">Use the **CloudBlobClient** object to get a reference to the container you want to use.</span></span> <span data-ttu-id="e482e-134">如果容器不存在，可以使用 **createIfNotExists** 方法建立，如果存在，此方法則會傳回現有的容器。</span><span class="sxs-lookup"><span data-stu-id="e482e-134">You can create the container if it doesn't exist with the **createIfNotExists** method, which will otherwise return the existing container.</span></span> <span data-ttu-id="e482e-135">根據預設，新容器屬私人性質，您必須指定儲存體存取金鑰 (如先前所做) 才能從此容器下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="e482e-135">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference to a container.
    // The container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create the container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="e482e-136">選擇性步驟：設定公用存取的容器</span><span class="sxs-lookup"><span data-stu-id="e482e-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="e482e-137">依預設會將容器的權限設定為私人存取，但針對網際網路上的所有使用者，您可以輕鬆地將容器的權限設定為公用、唯讀存取：</span><span class="sxs-lookup"><span data-stu-id="e482e-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions to allow public, read-only access for all users on the Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in the permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set the permissions on the container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="e482e-138">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="e482e-138">Upload a blob into a container</span></span>
<span data-ttu-id="e482e-139">若要將檔案上傳至 Blob，請取得容器參考，並使用該參考來取得 Blob 參考。</span><span class="sxs-lookup"><span data-stu-id="e482e-139">To upload a file to a blob, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="e482e-140">擁有 Blob 參考後，即可在 Blob 參考上呼叫 upload，上傳任何資料流。</span><span class="sxs-lookup"><span data-stu-id="e482e-140">Once you have a blob reference, you can upload any stream by calling upload on the blob reference.</span></span> <span data-ttu-id="e482e-141">如果 Blob 不存在，此作業將予以建立，若已存在，則予以覆寫。</span><span class="sxs-lookup"><span data-stu-id="e482e-141">This operation will create the blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="e482e-142">下列程式碼範例顯示此點，並假設已經建立好容器。</span><span class="sxs-lookup"><span data-stu-id="e482e-142">The following code sample shows this, and assumes that the container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define the path to a local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite the "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="e482e-143">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="e482e-143">List the blobs in a container</span></span>
<span data-ttu-id="e482e-144">若要列出容器中的 Blob，請先取得容器參考，就像上傳 Blob 那樣。</span><span class="sxs-lookup"><span data-stu-id="e482e-144">To list the blobs in a container, first get a container reference like you did to upload a blob.</span></span> <span data-ttu-id="e482e-145">您可以使用容器的 **listBlobs** 方法搭配 **for** 迴圈。</span><span class="sxs-lookup"><span data-stu-id="e482e-145">You can use the container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="e482e-146">下列程式碼將容器中每個 Blob 的 URI 輸出到主控台。</span><span class="sxs-lookup"><span data-stu-id="e482e-146">The following code outputs the Uri of each blob in a container to the console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within the container and output the URI to each of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="e482e-147">請注意，為 Blob 命名時，您可以在其名稱中包含路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="e482e-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="e482e-148">這會建立虛擬目錄結構，讓您能夠組織及周遊，就像使用傳統檔案系統一樣。</span><span class="sxs-lookup"><span data-stu-id="e482e-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="e482e-149">請注意，目錄結構僅限虛擬目錄結構 - Blog 儲存體中唯一可用的資源為容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="e482e-149">Note that the directory structure is virtual only - the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="e482e-150">但是，用戶端程式庫提供 **CloudBlobDirectory** 物件來參照虛擬目錄，以及簡化透過此方式組織之 Blob 的使用程序。</span><span class="sxs-lookup"><span data-stu-id="e482e-150">However, the client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="e482e-151">例如，您可能有名為 "photos" 的容器，當中您可能上傳名為 "rootphoto1"、"2010/photo1"、"2010/photo2" 和 "2011/photo1" 的 Blob。</span><span class="sxs-lookup"><span data-stu-id="e482e-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="e482e-152">這會在 "photos" 容器內建立虛擬目錄 "2010" 和 "2011"。</span><span class="sxs-lookup"><span data-stu-id="e482e-152">This would create the virtual directories "2010" and "2011" within the "photos" container.</span></span> <span data-ttu-id="e482e-153">當您在 "photos" 容器上呼叫 **ListBlobs** 時，傳回的集合將包含 **CloudBlobDirectory** 和 **CloudBlob** 物件，其分別代表最上層所包含的目錄和 Blob。</span><span class="sxs-lookup"><span data-stu-id="e482e-153">When you call **listBlobs** on the "photos" container, the collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="e482e-154">在此情況下，系統會傳回目錄 "2010" 和 "2011"，以及照片 "rootphoto1"。</span><span class="sxs-lookup"><span data-stu-id="e482e-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="e482e-155">您可以使用 **instanceof** 運算子來區別這些物件。</span><span class="sxs-lookup"><span data-stu-id="e482e-155">You can use the **instanceof** operator to distinguish these objects.</span></span>

<span data-ttu-id="e482e-156">您可以選擇性地將參數傳入 **listBlobs** 方法，將 **useFlatBlobListing** 參數設為 true。</span><span class="sxs-lookup"><span data-stu-id="e482e-156">Optionally, you can pass in parameters to the **listBlobs** method with the **useFlatBlobListing** parameter set to true.</span></span> <span data-ttu-id="e482e-157">如此會導致不論目錄為何，都會傳回每個 Blob。</span><span class="sxs-lookup"><span data-stu-id="e482e-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="e482e-158">如需詳細資訊，請參閱 **Azure 儲存體用戶端 SDK 參考** 中的 [CloudBlobContainer.listBlobs]。</span><span class="sxs-lookup"><span data-stu-id="e482e-158">For more information, see **CloudBlobContainer.listBlobs** in the [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="e482e-159">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="e482e-159">Download a blob</span></span>
<span data-ttu-id="e482e-160">若要下載 Blob，請遵循與上傳 Blob 相同的步驟，以取得 Blob 參考。</span><span class="sxs-lookup"><span data-stu-id="e482e-160">To download blobs, follow the same steps as you did for uploading a blob in order to get a blob reference.</span></span> <span data-ttu-id="e482e-161">在上傳範例中，您對 blob 物件呼叫了 upload。</span><span class="sxs-lookup"><span data-stu-id="e482e-161">In the uploading example, you called upload on the blob object.</span></span> <span data-ttu-id="e482e-162">在下列範例中，呼叫 download 將 Blob 內容傳到串流物件，例如 **FileOutputStream**，您可以用串流物件來將 Blob 永久儲存到本機檔案。</span><span class="sxs-lookup"><span data-stu-id="e482e-162">In the following example, call download to transfer the blob contents to a stream object such as a **FileOutputStream** that you can use to persist the blob to a local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in the container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If the item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download the item and save it to a file with the same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="e482e-163">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="e482e-163">Delete a blob</span></span>
<span data-ttu-id="e482e-164">若要刪除 Blob，請取得 Blob 參考，然後呼叫 **deleteIfExists**。</span><span class="sxs-lookup"><span data-stu-id="e482e-164">To delete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference to a blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete the blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="e482e-165">刪除 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="e482e-165">Delete a blob container</span></span>
<span data-ttu-id="e482e-166">最後，若要刪除 Blob 容器，請取得 Blob 容器的參考，然後呼叫 **deleteIfExists**。</span><span class="sxs-lookup"><span data-stu-id="e482e-166">Finally, to delete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete the blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="e482e-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e482e-167">Next steps</span></span>
<span data-ttu-id="e482e-168">了解 Blob 儲存體的基礎概念之後，請參考下列連結以了解有關更複雜的儲存工作。</span><span class="sxs-lookup"><span data-stu-id="e482e-168">Now that you've learned the basics of Blob storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="e482e-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="e482e-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="e482e-170">[Azure 儲存體用戶端 SDK 參考][CloudBlobContainer.listBlobs]</span><span class="sxs-lookup"><span data-stu-id="e482e-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="e482e-171">[Azure 儲存體 REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="e482e-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="e482e-172">[Azure 儲存體團隊部落格][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="e482e-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="e482e-173">如需詳細資訊，也請參閱 [Java 開發人員中心](/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="e482e-173">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="e482e-174">[CloudBlobContainer.listBlobs]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="e482e-174">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
