---
title: "如何從 C++ 使用 Blob 儲存體 (物件儲存體) | Microsoft Docs"
description: "使用 Azure Blob 儲存體 (物件儲存體) 在雲端中儲存非結構化資料。"
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
ms.openlocfilehash: 3f28fbee4e267ab6962e2f73af5af6461cc16448
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="b6563-103">如何使用 C++ 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b6563-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="b6563-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b6563-104">Overview</span></span>
<span data-ttu-id="b6563-105">Azure Blob 儲存體是可將非結構化的資料儲存在雲端作為物件/blob 的服務。</span><span class="sxs-lookup"><span data-stu-id="b6563-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="b6563-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="b6563-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="b6563-107">Blob 儲存體也稱為物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="b6563-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="b6563-108">本指南將示範如何使用 Azure Blob 儲存體服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="b6563-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="b6563-109">這些範例均以 C++ 撰寫，並使用 [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="b6563-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="b6563-110">所涵蓋的案例包括**上傳**、**列出**、**下載**及**刪除** Blob。</span><span class="sxs-lookup"><span data-stu-id="b6563-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="b6563-111">本指南以 Azure Storage Client Library for C++ 1.0.0 版和更新版本為對象。</span><span class="sxs-lookup"><span data-stu-id="b6563-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="b6563-112">建議的版本是 Storage Client Library 2.2.0，可透過 [NuGet](http://www.nuget.org/packages/wastorage) 或 [GitHub](https://github.com/Azure/azure-storage-cpp) 取得。</span><span class="sxs-lookup"><span data-stu-id="b6563-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="b6563-113">建立 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="b6563-113">Create a C++ application</span></span>
<span data-ttu-id="b6563-114">在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="b6563-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="b6563-115">若要這樣做，您需要安裝 Azure Storage Client Library for C++，並在 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6563-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="b6563-116">若要安裝 Azure Storage Client Library for C++，您可以使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="b6563-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="b6563-117">**Linux：** 遵循 [Azure Storage Client Library for C++ 讀我檔案](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 頁面中提供的指示進行。</span><span class="sxs-lookup"><span data-stu-id="b6563-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="b6563-118">**Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="b6563-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="b6563-119">在 [NuGet 套件管理員主控台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 中輸入下列命令，然後按下 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="b6563-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="b6563-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="b6563-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="b6563-121">設定您的應用程式以存取 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="b6563-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="b6563-122">在您要使用 Azure 儲存體 API 來存取 Blob 的 C++ 檔案頂端，加入下列 include 陳述式：</span><span class="sxs-lookup"><span data-stu-id="b6563-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="b6563-123">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="b6563-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="b6563-124">Azure 儲存體用戶端會使用儲存體連接字串來儲存存取資料管理服務時所用的端點與認證。</span><span class="sxs-lookup"><span data-stu-id="b6563-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="b6563-125">在用戶端應用程式中執行時，您必須以下列格式提供儲存體連接字串 (其中的 *AccountName* 和 *AccountKey* 值要使用您儲存體帳戶的名稱，以及在 [Azure 入口網站](https://portal.azure.com)中針對該儲存體帳戶而列出的儲存體存取金鑰)。</span><span class="sxs-lookup"><span data-stu-id="b6563-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="b6563-126">如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="b6563-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="b6563-127">本範例將示範如何宣告靜態欄位來存放連接字串：</span><span class="sxs-lookup"><span data-stu-id="b6563-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="b6563-128">若要在本機 Windows 電腦中測試您的應用程式，可以使用隨 [Azure SDK](https://azure.microsoft.com/downloads/) 一起安裝的 Microsoft Azure [儲存體模擬器](storage-use-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="b6563-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="b6563-129">儲存體模擬器是一個公用程式，可在本機開發電腦上模擬 Azure 提供的 Blob、佇列和表格服務。</span><span class="sxs-lookup"><span data-stu-id="b6563-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="b6563-130">下列範例示範如何宣告靜態欄位以便將連接字串存放到本機儲存體模擬器中：</span><span class="sxs-lookup"><span data-stu-id="b6563-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="b6563-131">若要啟動 Azure 儲存體模擬器，選取 [開始] 按鈕或按下 [Windows] 鍵。</span><span class="sxs-lookup"><span data-stu-id="b6563-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="b6563-132">開始輸入 **Azure 儲存體模擬器**，然後從應用程式清單選取 [Microsoft Azure 儲存體模擬器]。</span><span class="sxs-lookup"><span data-stu-id="b6563-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="b6563-133">下列範例假設您已經使用這兩個方法之一來取得儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="b6563-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="b6563-134">擷取連接字串</span><span class="sxs-lookup"><span data-stu-id="b6563-134">Retrieve your connection string</span></span>
<span data-ttu-id="b6563-135">您可以使用 **cloud_storage_account** 類別來代表儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b6563-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="b6563-136">若要從儲存體連接字串擷取儲存體帳戶資訊，您可以使用 **parse** 方法。</span><span class="sxs-lookup"><span data-stu-id="b6563-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="b6563-137">接著，取得 **cloud_blob_client** 類別的參考，因為這可讓您擷取代表 Blob 儲存體服務中儲存的容器和 Blob 的物件。</span><span class="sxs-lookup"><span data-stu-id="b6563-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="b6563-138">下列程式碼會使用我們在前面擷取的儲存體帳戶物件，建立 **cloud_blob_client** 物件：</span><span class="sxs-lookup"><span data-stu-id="b6563-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="b6563-139">作法：建立容器</span><span class="sxs-lookup"><span data-stu-id="b6563-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="b6563-140">此範例說明如何建立尚不存在的容器：</span><span class="sxs-lookup"><span data-stu-id="b6563-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="b6563-141">根據預設，新容器屬私人性質，您必須指定儲存體存取金鑰才能從此容器下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="b6563-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="b6563-142">若要讓所有人都能使用容器中的檔案 (Blob)，您可以使用下列程式碼將容器設定為公用容器：</span><span class="sxs-lookup"><span data-stu-id="b6563-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="b6563-143">網際網路上的任何人都可以看到公用容器中的 Blob，但要有適當的存取金鑰，才能修改或刪除這些 Blob。</span><span class="sxs-lookup"><span data-stu-id="b6563-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="b6563-144">作法：將 Blob 上傳到容器中</span><span class="sxs-lookup"><span data-stu-id="b6563-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="b6563-145">Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="b6563-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="b6563-146">在大多數情況下，建議使用區塊 Blob 的類型。</span><span class="sxs-lookup"><span data-stu-id="b6563-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="b6563-147">若要將檔案上傳至區塊 Blob，請取得容器參照，並使用該參照來取得區塊 Blob 參照。</span><span class="sxs-lookup"><span data-stu-id="b6563-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="b6563-148">取得 Blob 參考後，即可藉由呼叫 **upload_from_stream** 方法，將任何資料流上傳至 Blob。</span><span class="sxs-lookup"><span data-stu-id="b6563-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="b6563-149">此操作會建立 Blob (如果其並不存在) 或覆寫 Blob (如果其已存在)。</span><span class="sxs-lookup"><span data-stu-id="b6563-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="b6563-150">下列範例顯示如何將 Blob 上傳到容器，並假設已建立該容器。</span><span class="sxs-lookup"><span data-stu-id="b6563-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="b6563-151">或者，您可以使用 **upload_from_file** 方法，將檔案上傳至區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="b6563-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="b6563-152">作法：列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="b6563-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="b6563-153">若要列出容器中的 Blob，請先取得容器參照。</span><span class="sxs-lookup"><span data-stu-id="b6563-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="b6563-154">然後，您可以使用容器的 **list_blobs** 方法來擷取 blob 和 (或) 其中的目錄。</span><span class="sxs-lookup"><span data-stu-id="b6563-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="b6563-155">若要存取傳回的 **list_blob_item** 中豐富的屬性和方法，您必須呼叫 **list_blob_item.as_blob** 方法來取得 **cloud_blob** 物件，或呼叫 **list_blob.as_directory** 方法來取得 cloud_blob_directory 物件。</span><span class="sxs-lookup"><span data-stu-id="b6563-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="b6563-156">下列程式碼示範如何擷取和輸出 **my-sample-container** 容器中每個項目的 URI：</span><span class="sxs-lookup"><span data-stu-id="b6563-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
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

<span data-ttu-id="b6563-157">如需列出作業的詳細資訊，請參閱 [以 C++ 列出 Azure 儲存體資源](storage-c-plus-plus-enumeration.md)。</span><span class="sxs-lookup"><span data-stu-id="b6563-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="b6563-158">作法：下載 Blob</span><span class="sxs-lookup"><span data-stu-id="b6563-158">How to: Download blobs</span></span>
<span data-ttu-id="b6563-159">若要下載 Blob，請先擷取 Blob 參考，然後呼叫 **download_to_stream** 方法。</span><span class="sxs-lookup"><span data-stu-id="b6563-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="b6563-160">下列範例使用 **download_to_stream** 方法將 Blob 內容傳送給資料流物件，您接著可將該物件永久儲存成本機檔案。</span><span class="sxs-lookup"><span data-stu-id="b6563-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="b6563-161">或者，您可以使用 **download_to_file** 方法，將 Blob 的內容下載到檔案。</span><span class="sxs-lookup"><span data-stu-id="b6563-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="b6563-162">此外，您也可以使用 **download_text** 方法，將 Blob 的內容當成文字字串下載。</span><span class="sxs-lookup"><span data-stu-id="b6563-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="b6563-163">作法：刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="b6563-163">How to: Delete blobs</span></span>
<span data-ttu-id="b6563-164">若要刪除 Blob，請先取得 Blob 參考，然後針對該參考呼叫 **delete_blob** 方法。</span><span class="sxs-lookup"><span data-stu-id="b6563-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="b6563-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6563-165">Next steps</span></span>
<span data-ttu-id="b6563-166">了解 Blob 儲存體的基礎概念之後，請依照下列連結深入了解 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b6563-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="b6563-167">如何使用 C++ 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="b6563-167">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="b6563-168">如何使用 C++ 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="b6563-168">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="b6563-169">以 C++ 列出 Azure 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="b6563-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="b6563-170">Storage Client Library for C++ 參考資料</span><span class="sxs-lookup"><span data-stu-id="b6563-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="b6563-171">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="b6563-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="b6563-172">使用 AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="b6563-172">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)

