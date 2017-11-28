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
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a><span data-ttu-id="ac06a-103">如何從 Java 的 Blob 儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="ac06a-103">How toouse Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="ac06a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ac06a-104">Overview</span></span>
<span data-ttu-id="ac06a-105">Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。</span><span class="sxs-lookup"><span data-stu-id="ac06a-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="ac06a-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="ac06a-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="ac06a-107">Blob 儲存體也是參考的 tooas 物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="ac06a-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="ac06a-108">本文將告訴您如何使用 tooperform 常見案例 hello Microsoft Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ac06a-108">This article will show you how tooperform common scenarios using hello Microsoft Azure Blob storage.</span></span> <span data-ttu-id="ac06a-109">hello 範例以 Java 撰寫，並使用 hello [for Java 的 Azure 儲存體 SDK][Azure Storage SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="ac06a-109">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="ac06a-110">hello 涵蓋案例包括**上載**，**列出**，**下載**，和**刪除**blob。</span><span class="sxs-lookup"><span data-stu-id="ac06a-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="ac06a-111">如需有關 blob 的詳細資訊，請參閱 hello[接下來的步驟](#Next-Steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="ac06a-111">For more information on blobs, see hello [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="ac06a-112">有一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="ac06a-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="ac06a-113">如需詳細資訊，請參閱 hello[適用於 Android 的 Azure 儲存體 SDK][Azure Storage SDK for Android]。</span><span class="sxs-lookup"><span data-stu-id="ac06a-113">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="ac06a-114">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac06a-114">Create a Java application</span></span>
<span data-ttu-id="ac06a-115">在本文中，您將使用儲存體功能，這些功能可執行於本機的 Java 應用程式內，也可執行於在 Azure 中之 Web 角色或背景工作角色內執行的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="ac06a-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="ac06a-116">toodo 因此，您將需要 tooinstall hello Java Development Kit (JDK)，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac06a-116">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="ac06a-117">一旦您這樣做，您必須開發系統符合 hello 最低需求和相依性的 hello 中所列的 tooverify [for Java 的 Azure 儲存體 SDK] [ Azure Storage SDK for Java] GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ac06a-117">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="ac06a-118">如果您的系統符合這些需求，您可以遵循下載並安裝在您從該儲存機制的系統上的 hello Azure 儲存體 Libraries for Java 的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="ac06a-118">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="ac06a-119">當您完成這些工作時，您就會無法 toocreate hello 範例會使用這份文件中的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac06a-119">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="ac06a-120">設定您的應用程式 tooaccess Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ac06a-120">Configure your application tooaccess Blob storage</span></span>
<span data-ttu-id="ac06a-121">新增下列匯入陳述式 toohello 想 toouse hello Azure 儲存體 Api tooaccess blob hello Java 檔案頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="ac06a-121">Add hello following import statements toohello top of hello Java file where you want toouse hello Azure Storage APIs tooaccess blobs.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="ac06a-122">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="ac06a-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="ac06a-123">Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。</span><span class="sxs-lookup"><span data-stu-id="ac06a-123">An Azure Storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="ac06a-124">用戶端應用程式中執行時，您必須提供 hello 遵循格式，請使用 hello 您的儲存體帳戶名稱中的 hello 儲存體連接字串和 hello hello hello 中所列的儲存體帳戶的主要存取金鑰[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。</span><span class="sxs-lookup"><span data-stu-id="ac06a-124">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="ac06a-125">hello 下列範例示範如何宣告靜態欄位 toohold hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="ac06a-125">hello following example shows how you can declare a static field toohold hello connection string.</span></span>

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="ac06a-126">在應用程式中執行 Microsoft Azure 中的角色，這個字串可以儲存在 hello 服務組態檔， *ServiceConfiguration.cscfg*，而且可以存取與呼叫 toohello **RoleEnvironment.getConfigurationSettings**方法。</span><span class="sxs-lookup"><span data-stu-id="ac06a-126">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="ac06a-127">hello 下列範例會取得連接字串 hello**設定**名*StorageConnectionString* hello 服務組態檔中。</span><span class="sxs-lookup"><span data-stu-id="ac06a-127">hello following example gets hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="ac06a-128">hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。</span><span class="sxs-lookup"><span data-stu-id="ac06a-128">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="ac06a-129">建立容器</span><span class="sxs-lookup"><span data-stu-id="ac06a-129">Create a container</span></span>
<span data-ttu-id="ac06a-130">**CloudBlobClient** 物件可讓您取得容器和 Blob 的參考物件。</span><span class="sxs-lookup"><span data-stu-id="ac06a-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="ac06a-131">hello 下列程式碼會建立**CloudBlobClient**物件。</span><span class="sxs-lookup"><span data-stu-id="ac06a-131">hello following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="ac06a-132">有其他方式 toocreate **CloudStorageAccount**物件; 如需詳細資訊，請參閱**CloudStorageAccount**在 hello [Azure 儲存體用戶端 SDK 參考]。</span><span class="sxs-lookup"><span data-stu-id="ac06a-132">There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="ac06a-133">使用 hello **CloudBlobClient** tooget 想 toouse 參考 toohello 容器的物件。</span><span class="sxs-lookup"><span data-stu-id="ac06a-133">Use hello **CloudBlobClient** object tooget a reference toohello container you want toouse.</span></span> <span data-ttu-id="ac06a-134">如果以 hello 不存在，您可以建立 hello 容器**createIfNotExists**方法，否則會傳回 hello 現有容器。</span><span class="sxs-lookup"><span data-stu-id="ac06a-134">You can create hello container if it doesn't exist with hello **createIfNotExists** method, which will otherwise return hello existing container.</span></span> <span data-ttu-id="ac06a-135">根據預設，hello 新容器是私人的所以您必須指定儲存體存取金鑰 （如先前般） toodownload 從這個容器的 blob。</span><span class="sxs-lookup"><span data-stu-id="ac06a-135">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span>

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

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="ac06a-136">選擇性步驟：設定公用存取的容器</span><span class="sxs-lookup"><span data-stu-id="ac06a-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="ac06a-137">根據預設，容器的權限設定為私用存取，但您可以輕鬆地在 hello 網際網路上設定容器的權限 tooallow 公用、 僅限讀取所有使用者的存取：</span><span class="sxs-lookup"><span data-stu-id="ac06a-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions tooallow public, read-only access for all users on hello Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ac06a-138">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="ac06a-138">Upload a blob into a container</span></span>
<span data-ttu-id="ac06a-139">tooupload 檔案 tooa blob 取得容器的參考，並將它 tooget blob 參考。</span><span class="sxs-lookup"><span data-stu-id="ac06a-139">tooupload a file tooa blob, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="ac06a-140">Blob 參考之後，您可以藉由呼叫 hello blob 參考上的上傳來上傳任何資料流。</span><span class="sxs-lookup"><span data-stu-id="ac06a-140">Once you have a blob reference, you can upload any stream by calling upload on hello blob reference.</span></span> <span data-ttu-id="ac06a-141">如果它不存在，或覆寫它，如果是的話，這項作業將會建立 hello blob。</span><span class="sxs-lookup"><span data-stu-id="ac06a-141">This operation will create hello blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="ac06a-142">hello，下列程式碼範例顯示，並假設已建立該 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="ac06a-142">hello following code sample shows this, and assumes that hello container has already been created.</span></span>

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

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="ac06a-143">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="ac06a-143">List hello blobs in a container</span></span>
<span data-ttu-id="ac06a-144">toolist hello blob 容器中的第一次取得容器的參考，像 tooupload blob。</span><span class="sxs-lookup"><span data-stu-id="ac06a-144">toolist hello blobs in a container, first get a container reference like you did tooupload a blob.</span></span> <span data-ttu-id="ac06a-145">您可以使用 hello 容器**listBlobs**方法**如**迴圈。</span><span class="sxs-lookup"><span data-stu-id="ac06a-145">You can use hello container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="ac06a-146">hello 下列程式碼輸出 hello 容器 toohello 主控台中每個 blob 的 Uri。</span><span class="sxs-lookup"><span data-stu-id="ac06a-146">hello following code outputs hello Uri of each blob in a container toohello console.</span></span>

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

<span data-ttu-id="ac06a-147">請注意，為 Blob 命名時，您可以在其名稱中包含路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="ac06a-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="ac06a-148">這會建立虛擬目錄結構，讓您能夠組織及周遊，就像使用傳統檔案系統一樣。</span><span class="sxs-lookup"><span data-stu-id="ac06a-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="ac06a-149">請注意，只是虛擬 hello 目錄結構-hello 只可用的資源在 Blob 儲存體不容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="ac06a-149">Note that hello directory structure is virtual only - hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="ac06a-150">不過，hello 用戶端程式庫提供**CloudBlobDirectory**物件 toorefer tooa 虛擬目錄，並簡化 hello 程序會以這種方式組織的 blob 使用。</span><span class="sxs-lookup"><span data-stu-id="ac06a-150">However, hello client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="ac06a-151">例如，您可能有名為 "photos" 的容器，當中您可能上傳名為 "rootphoto1"、"2010/photo1"、"2010/photo2" 和 "2011/photo1" 的 Blob。</span><span class="sxs-lookup"><span data-stu-id="ac06a-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="ac06a-152">這樣會建立 hello"2010"和"2011"hello"相片 」 容器內的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="ac06a-152">This would create hello virtual directories "2010" and "2011" within hello "photos" container.</span></span> <span data-ttu-id="ac06a-153">當您呼叫**listBlobs** hello 「 相片 」 容器，將會包含傳回 hello 集合**CloudBlobDirectory**和**CloudBlob**代表 hello 物件目錄和包含在 hello 最上層的 blob。</span><span class="sxs-lookup"><span data-stu-id="ac06a-153">When you call **listBlobs** on hello "photos" container, hello collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="ac06a-154">在此情況下，系統會傳回目錄 "2010" 和 "2011"，以及照片 "rootphoto1"。</span><span class="sxs-lookup"><span data-stu-id="ac06a-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="ac06a-155">您可以使用 hello **instanceof**運算子 toodistinguish 這些物件。</span><span class="sxs-lookup"><span data-stu-id="ac06a-155">You can use hello **instanceof** operator toodistinguish these objects.</span></span>

<span data-ttu-id="ac06a-156">（選擇性） 您可以傳入參數 toohello **listBlobs**方法以 hello **useFlatBlobListing**參數設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="ac06a-156">Optionally, you can pass in parameters toohello **listBlobs** method with hello **useFlatBlobListing** parameter set tootrue.</span></span> <span data-ttu-id="ac06a-157">如此會導致不論目錄為何，都會傳回每個 Blob。</span><span class="sxs-lookup"><span data-stu-id="ac06a-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="ac06a-158">如需詳細資訊，請參閱**CloudBlobContainer.listBlobs**在 hello [Azure 儲存體用戶端 SDK 參考]。</span><span class="sxs-lookup"><span data-stu-id="ac06a-158">For more information, see **CloudBlobContainer.listBlobs** in hello [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="ac06a-159">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="ac06a-159">Download a blob</span></span>
<span data-ttu-id="ac06a-160">toodownload blob，請遵循相同步驟與您上傳 blob 中的 blob 參考的順序 tooget hello。</span><span class="sxs-lookup"><span data-stu-id="ac06a-160">toodownload blobs, follow hello same steps as you did for uploading a blob in order tooget a blob reference.</span></span> <span data-ttu-id="ac06a-161">在上傳範例 hello，您會在 hello blob 物件上呼叫上傳。</span><span class="sxs-lookup"><span data-stu-id="ac06a-161">In hello uploading example, you called upload on hello blob object.</span></span> <span data-ttu-id="ac06a-162">在下列範例的 hello，呼叫下載 tootransfer hello blob 內容 tooa 資料流物件，例如**FileOutputStream**您可以使用 toopersist hello blob tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="ac06a-162">In hello following example, call download tootransfer hello blob contents tooa stream object such as a **FileOutputStream** that you can use toopersist hello blob tooa local file.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="ac06a-163">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="ac06a-163">Delete a blob</span></span>
<span data-ttu-id="ac06a-164">toodelete blob、 取得 blob 參考，並呼叫**deleteIfExists**。</span><span class="sxs-lookup"><span data-stu-id="ac06a-164">toodelete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="ac06a-165">刪除 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="ac06a-165">Delete a blob container</span></span>
<span data-ttu-id="ac06a-166">最後，toodelete blob 容器、 取得 blob 容器的參考，並呼叫**deleteIfExists**。</span><span class="sxs-lookup"><span data-stu-id="ac06a-166">Finally, toodelete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ac06a-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac06a-167">Next steps</span></span>
<span data-ttu-id="ac06a-168">現在，您學到的 Blob 儲存體的 hello 基本概念，請遵循這些連結 toolearn，更複雜的存放工作相關。</span><span class="sxs-lookup"><span data-stu-id="ac06a-168">Now that you've learned hello basics of Blob storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="ac06a-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="ac06a-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="ac06a-170">[Azure 儲存體用戶端 SDK 參考][Azure 儲存體用戶端 SDK 參考]</span><span class="sxs-lookup"><span data-stu-id="ac06a-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="ac06a-171">[Azure 儲存體 REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="ac06a-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="ac06a-172">[Azure 儲存體團隊部落格][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="ac06a-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="ac06a-173">如需詳細資訊，請參閱 hello [Java 開發人員中心](/develop/java/)。</span><span class="sxs-lookup"><span data-stu-id="ac06a-173">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 儲存體用戶端 SDK 參考]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
