---
title: "aaaHow toouse blob 儲存體 （物件儲存體） 從 c + + |Microsoft 文件"
description: "使用 Azure Blob 儲存體 （物件儲存體） 的 hello 雲端中儲存非結構化的資料。"
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="b5c90-103">如何 toouse 從 c + + 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b5c90-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="b5c90-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b5c90-104">Overview</span></span>
<span data-ttu-id="b5c90-105">Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。</span><span class="sxs-lookup"><span data-stu-id="b5c90-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="b5c90-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="b5c90-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="b5c90-107">Blob 儲存體也是參考的 tooas 物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="b5c90-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="b5c90-108">本指南將示範如何使用 tooperform 常見案例 hello Azure Blob 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="b5c90-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="b5c90-109">hello 範例以 c + + 撰寫，並使用 hello [c + + 的 Azure 儲存體用戶端程式庫](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="b5c90-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="b5c90-110">hello 涵蓋案例包括**上載**，**列出**，**下載**，和**刪除**blob。</span><span class="sxs-lookup"><span data-stu-id="b5c90-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="b5c90-111">此指南的目標 hello Azure 儲存體用戶端程式庫，c + + 1.0.0 版和更新版本。</span><span class="sxs-lookup"><span data-stu-id="b5c90-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="b5c90-112">hello 建議版本是儲存體用戶端程式庫 2.2.0，也就是可透過使用[NuGet](http://www.nuget.org/packages/wastorage)或[GitHub](https://github.com/Azure/azure-storage-cpp)。</span><span class="sxs-lookup"><span data-stu-id="b5c90-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="b5c90-113">建立 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="b5c90-113">Create a C++ application</span></span>
<span data-ttu-id="b5c90-114">在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="b5c90-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="b5c90-115">toodo 因此，您將需要 tooinstall hello for c + + 的 Azure 儲存體用戶端程式庫，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b5c90-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="b5c90-116">tooinstall hello Azure 儲存體用戶端程式庫的 c + +，，您可以使用下列方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5c90-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="b5c90-117">**Linux:**遵循 hello 所提供的 hello 指示[for c + + 讀我檔案的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="b5c90-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="b5c90-118">**Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="b5c90-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="b5c90-119">型別 hello 下列命令到 hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="b5c90-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="b5c90-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="b5c90-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="b5c90-121">設定您的應用程式 tooaccess Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b5c90-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="b5c90-122">加入 hello 下列包含您想要 toouse hello Azure 儲存體 Api tooaccess blob hello c + + 檔案的陳述式 toohello 頂端：</span><span class="sxs-lookup"><span data-stu-id="b5c90-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="b5c90-123">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="b5c90-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="b5c90-124">Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。</span><span class="sxs-lookup"><span data-stu-id="b5c90-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="b5c90-125">用戶端應用程式中執行時，您必須提供 hello 遵循格式，並透過儲存體帳戶和 hello 儲存體存取金鑰的 hello 名稱 hello hello 中所列的儲存體帳戶中的 hello 儲存體連接字串[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。</span><span class="sxs-lookup"><span data-stu-id="b5c90-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="b5c90-126">如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="b5c90-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="b5c90-127">此範例顯示如何宣告靜態欄位 toohold hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="b5c90-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="b5c90-128">tootest 您的應用程式在本機的 Windows 電腦，您可以使用 Microsoft Azure 的 hello[儲存體模擬器](storage-use-emulator.md)會隨 hello [Azure SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="b5c90-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="b5c90-129">hello 儲存體模擬器是模擬 hello Blob、 佇列和表格服務在本機開發電腦上可用在 Azure 中的公用程式。</span><span class="sxs-lookup"><span data-stu-id="b5c90-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="b5c90-130">hello 下列範例顯示如何宣告靜態欄位 toohold hello 連接字串 tooyour 本機儲存體模擬器：</span><span class="sxs-lookup"><span data-stu-id="b5c90-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="b5c90-131">toostart hello Azure 儲存體模擬器中，選取 hello**啟動**按鈕或按 hello **Windows**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b5c90-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="b5c90-132">開始輸入**Azure 儲存體模擬器**，然後選取**Microsoft Azure 儲存體模擬器**hello 清單中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5c90-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="b5c90-133">hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。</span><span class="sxs-lookup"><span data-stu-id="b5c90-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="b5c90-134">擷取連接字串</span><span class="sxs-lookup"><span data-stu-id="b5c90-134">Retrieve your connection string</span></span>
<span data-ttu-id="b5c90-135">您可以使用 hello**驗證 cloud_storage_account**類別 toorepresent 儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b5c90-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="b5c90-136">tooretrieve 您的儲存體帳戶資訊 hello 儲存體連接字串，您可以使用 hello**剖析**方法。</span><span class="sxs-lookup"><span data-stu-id="b5c90-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="b5c90-137">接下來，取得參考 tooa **cloud_blob_client**類別，如它可讓您表示容器和 blob 儲存在 Blob 儲存體服務的 hello tooretrieve 物件。</span><span class="sxs-lookup"><span data-stu-id="b5c90-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="b5c90-138">hello 下列程式碼會建立**cloud_blob_client**使用 hello 我們擷取上述的儲存體帳戶物件的物件：</span><span class="sxs-lookup"><span data-stu-id="b5c90-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="b5c90-139">作法：建立容器</span><span class="sxs-lookup"><span data-stu-id="b5c90-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="b5c90-140">這個範例會示範如何 toocreate 如果不存在的容器：</span><span class="sxs-lookup"><span data-stu-id="b5c90-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="b5c90-141">根據預設，hello 新容器是 private，而且您必須指定您的儲存體存取金鑰 toodownload blob，從這個容器。</span><span class="sxs-lookup"><span data-stu-id="b5c90-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="b5c90-142">如果您要設定 hello 容器可用 tooeveryone toomake hello 檔案 (blob)，您可以設定 hello 容器 toobe 公用使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5c90-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="b5c90-143">Hello 網際網路上的任何人可以看到公用容器中的 blob，但您可以修改或刪除它們，只有當您擁有 hello 適當的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b5c90-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="b5c90-144">作法：將 Blob 上傳到容器中</span><span class="sxs-lookup"><span data-stu-id="b5c90-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="b5c90-145">Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="b5c90-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="b5c90-146">Hello 大部分的情況下，在區塊 blob 會是建議的型別 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="b5c90-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="b5c90-147">tooupload 檔案 tooa 區塊 blob，取得容器的參考，並將它 tooget 區塊 blob 參考。</span><span class="sxs-lookup"><span data-stu-id="b5c90-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="b5c90-148">Blob 參考之後，您可以上傳任何資料流的資料 tooit 呼叫 hello **upload_from_stream**方法。</span><span class="sxs-lookup"><span data-stu-id="b5c90-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="b5c90-149">如果先前沒有存在，或覆寫它存在的話，這項作業將會建立 hello blob。</span><span class="sxs-lookup"><span data-stu-id="b5c90-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="b5c90-150">下列範例會示範如何 hello tooupload blob 容器，並假設已建立該 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="b5c90-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="b5c90-151">或者，您可以使用 hello **upload_from_file**方法 tooupload 檔案 tooa 區塊 blob。</span><span class="sxs-lookup"><span data-stu-id="b5c90-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="b5c90-152">如何： 列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="b5c90-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="b5c90-153">toolist hello blob 容器中的第一次取得容器的參考。</span><span class="sxs-lookup"><span data-stu-id="b5c90-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="b5c90-154">然後，您可以使用 hello 容器**list_blobs**方法 tooretrieve hello blob 及/或目錄內。</span><span class="sxs-lookup"><span data-stu-id="b5c90-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="b5c90-155">tooaccess hello 豐富的屬性和方法傳回**list_blob_item**，您必須呼叫 hello **list_blob_item.as_blob**方法 tooget **cloud_blob**物件，或 hello **list_blob.as_directory**方法 tooget cloud_blob_directory 物件。</span><span class="sxs-lookup"><span data-stu-id="b5c90-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="b5c90-156">hello 下列程式碼示範如何 tooretrieve 和輸出 hello hello 中每個項目的 URI**我範例容器**容器：</span><span class="sxs-lookup"><span data-stu-id="b5c90-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="b5c90-157">如需列出作業的詳細資訊，請參閱 [以 C++ 列出 Azure 儲存體資源](storage-c-plus-plus-enumeration.md)。</span><span class="sxs-lookup"><span data-stu-id="b5c90-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="b5c90-158">作法：下載 Blob</span><span class="sxs-lookup"><span data-stu-id="b5c90-158">How to: Download blobs</span></span>
<span data-ttu-id="b5c90-159">toodownload blob，先擷取 blob 的參考，然後再呼叫 hello **download_to_stream**方法。</span><span class="sxs-lookup"><span data-stu-id="b5c90-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="b5c90-160">hello 下列範例會使用 hello **download_to_stream**方法 tootransfer hello blob 內容 tooa 資料流物件，您可以再保存 tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="b5c90-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="b5c90-161">或者，您可以使用 hello **download_to_file**方法 toodownload hello blob tooa 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="b5c90-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="b5c90-162">此外，您也可以使用 hello **download_text**方法 toodownload hello 內容為文字字串的 blob。</span><span class="sxs-lookup"><span data-stu-id="b5c90-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="b5c90-163">作法：刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="b5c90-163">How to: Delete blobs</span></span>
<span data-ttu-id="b5c90-164">toodelete blob，先取得 blob 的參考，然後再呼叫 hello **delete_blob**方法。</span><span class="sxs-lookup"><span data-stu-id="b5c90-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="b5c90-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5c90-165">Next steps</span></span>
<span data-ttu-id="b5c90-166">現在，您學到的 blob 儲存體的 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b5c90-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="b5c90-167">如何 toouse 佇列儲存體從 c + +</span><span class="sxs-lookup"><span data-stu-id="b5c90-167">How toouse Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="b5c90-168">如何 toouse 從 c + + 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="b5c90-168">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="b5c90-169">以 C++ 列出 Azure 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="b5c90-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="b5c90-170">Storage Client Library for C++ 參考資料</span><span class="sxs-lookup"><span data-stu-id="b5c90-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="b5c90-171">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="b5c90-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="b5c90-172">使用 hello AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="b5c90-172">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

