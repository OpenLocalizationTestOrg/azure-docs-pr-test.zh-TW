---
title: "如何使用 Python 中的 Azure Blob 儲存體 (物件儲存體) | Microsoft Docs"
description: "使用 Azure Blob 儲存體 (物件儲存體) 在雲端中儲存非結構化資料。"
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 968814db9496fd410162d482191592c8a56101f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="2422e-103">如何使用 Python 的 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="2422e-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="2422e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2422e-104">Overview</span></span>
<span data-ttu-id="2422e-105">Azure Blob 儲存體是可將非結構化的資料儲存在雲端作為物件/blob 的服務。</span><span class="sxs-lookup"><span data-stu-id="2422e-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="2422e-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="2422e-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="2422e-107">Blob 儲存體也稱為物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="2422e-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="2422e-108">本文將示範如何使用 Blob 儲存體執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="2422e-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="2422e-109">這些範例是以 Python 所撰寫，並使用 [Microsoft Azure Storage SDK for Python (適用於 Python 的 Microsoft Azure 儲存體 SDK)]。</span><span class="sxs-lookup"><span data-stu-id="2422e-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="2422e-110">所涵蓋的案例包括「上傳、列出、下載」及「刪除」Blob。</span><span class="sxs-lookup"><span data-stu-id="2422e-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="2422e-111">建立容器</span><span class="sxs-lookup"><span data-stu-id="2422e-111">Create a container</span></span>
<span data-ttu-id="2422e-112">根據您想要使用的 Blob 類型，建立 **BlockBlobService**、**AppendBlobService** 或 **PageBlobService** 物件。</span><span class="sxs-lookup"><span data-stu-id="2422e-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="2422e-113">下列程式碼會使用 **BlockBlobService** 物件。</span><span class="sxs-lookup"><span data-stu-id="2422e-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="2422e-114">將下列內容新增至您想要在其中以程式設計方式存取 Azure 區塊 Blob 儲存體之任何 Python 檔案內的頂端附近。</span><span class="sxs-lookup"><span data-stu-id="2422e-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="2422e-115">下列程式碼會使用儲存體帳戶名稱和帳戶金鑰來建立 **BlockBlobService** 物件。</span><span class="sxs-lookup"><span data-stu-id="2422e-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="2422e-116">將 'myaccount' 和 'mykey' 取代為您的帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="2422e-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="2422e-117">在下列的程式碼範例中，如果容器不存在，您可以使用 **BlockBlobService** 物件建立容器。</span><span class="sxs-lookup"><span data-stu-id="2422e-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="2422e-118">根據預設，新容器屬私人性質，您必須指定儲存體存取金鑰 (如先前所做) 才能從此容器下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="2422e-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="2422e-119">若要讓所有人都能使用容器中的 blob，您可以使用下列程式碼建立容器，並傳遞公用存取等級。</span><span class="sxs-lookup"><span data-stu-id="2422e-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="2422e-120">或者，您也可以在建立容器之後使用下列程式碼修改它。</span><span class="sxs-lookup"><span data-stu-id="2422e-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="2422e-121">做此變更之後，網際網路上的任何人都可以看到公用容器中的 Blob，但只有您能修改或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="2422e-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="2422e-122">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="2422e-122">Upload a blob into a container</span></span>
<span data-ttu-id="2422e-123">若要建立區塊 Blob 和上傳資料，請使用 **create\_blob\_from\_path**、**create\_blob\_from\_stream**、**create\_blob\_from\_bytes** 或 **create\_blob\_from\_text** 方法。</span><span class="sxs-lookup"><span data-stu-id="2422e-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="2422e-124">這些是高階方法，可在資料大小超過 64 MB 時執行必要的區塊化動作。</span><span class="sxs-lookup"><span data-stu-id="2422e-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="2422e-125">**create\_blob\_from\_path** 會從指定的路徑上傳檔案的內容，**create\_blob\_from\_stream** 會從已開啟的檔案/串流上傳內容。</span><span class="sxs-lookup"><span data-stu-id="2422e-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="2422e-126">**create\_blob\_from\_bytes** 會上傳位元組陣列，**create\_blob\_from\_text** 會使用指定的編碼 (預設為 UTF-8) 上傳指定的文字值。</span><span class="sxs-lookup"><span data-stu-id="2422e-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="2422e-127">下列範例會將 **sunset.png** 檔案的內容上傳至 **myblob** Blob 中。</span><span class="sxs-lookup"><span data-stu-id="2422e-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="2422e-128">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="2422e-128">List the blobs in a container</span></span>
<span data-ttu-id="2422e-129">若要列出容器中的 Blob，請使用 **list\_blobs** 方法。</span><span class="sxs-lookup"><span data-stu-id="2422e-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="2422e-130">這個方法會傳回產生器。</span><span class="sxs-lookup"><span data-stu-id="2422e-130">This method returns a generator.</span></span> <span data-ttu-id="2422e-131">下列程式碼會將容器中每個 blob 的 **name** 輸出到主控台。</span><span class="sxs-lookup"><span data-stu-id="2422e-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="2422e-132">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="2422e-132">Download blobs</span></span>
<span data-ttu-id="2422e-133">若要從 blob 下載資料，請使用 **get\_blob\_to\_path****get\_blob\_to\_stream**、**get\_blob\_to\_bytes** 或 **get\_blob\_to\_text**。</span><span class="sxs-lookup"><span data-stu-id="2422e-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="2422e-134">這些是高階方法，可在資料大小超過 64 MB 時執行必要的區塊化動作。</span><span class="sxs-lookup"><span data-stu-id="2422e-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="2422e-135">下列範例示範如何使用 **get\_blob\_to\_path** 下載 **myblob** Blob 的內容，並將其儲存至 **out-sunset.png** 檔案。</span><span class="sxs-lookup"><span data-stu-id="2422e-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="2422e-136">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="2422e-136">Delete a blob</span></span>
<span data-ttu-id="2422e-137">最後，若要刪除 Blob，請呼叫 **delete_blob**。</span><span class="sxs-lookup"><span data-stu-id="2422e-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="2422e-138">寫入附加 Blob</span><span class="sxs-lookup"><span data-stu-id="2422e-138">Writing to an append blob</span></span>
<span data-ttu-id="2422e-139">附加 Blob 已針對附加作業 (例如紀錄) 最佳化。</span><span class="sxs-lookup"><span data-stu-id="2422e-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="2422e-140">如同區塊 Blob，附加 Blob 亦由區塊組成，但當您將新區塊加入附加 Blob 時，它一律會附加到 Blob 結尾。</span><span class="sxs-lookup"><span data-stu-id="2422e-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="2422e-141">您無法更新或刪除附加 Blob 中的現有區塊。</span><span class="sxs-lookup"><span data-stu-id="2422e-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="2422e-142">附加 Blob 的區塊識別碼不會公開顯示，因為該識別碼適用於區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="2422e-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="2422e-143">附加 Blob 中的每個區塊大小都不同，最大為 4 MB，而附加 Blob 可包含高達 50,000 個區塊。</span><span class="sxs-lookup"><span data-stu-id="2422e-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="2422e-144">因此，附加 Blob 的大小上限稍高於 195 GB (4 MB X 50,000 個區塊)。</span><span class="sxs-lookup"><span data-stu-id="2422e-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="2422e-145">下列範例中建立了新的附加 Blob，並附加一些資料，以模擬簡單的記錄作業。</span><span class="sxs-lookup"><span data-stu-id="2422e-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="2422e-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2422e-146">Next steps</span></span>
<span data-ttu-id="2422e-147">了解 Blob 儲存體的基礎概念之後，請使用下列連結深入了解。</span><span class="sxs-lookup"><span data-stu-id="2422e-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="2422e-148">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="2422e-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="2422e-149">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="2422e-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="2422e-150">[Azure 儲存體團隊部落格]</span><span class="sxs-lookup"><span data-stu-id="2422e-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="2422e-151">[Microsoft Azure Storage SDK for Python (適用於 Python 的 Microsoft Azure 儲存體 SDK)]</span><span class="sxs-lookup"><span data-stu-id="2422e-151">[Microsoft Azure Storage SDK for Python]</span></span>

<span data-ttu-id="2422e-152">[Azure 儲存體團隊部落格]: http://blogs.msdn.com/b/windowsazurestorage/</span><span class="sxs-lookup"><span data-stu-id="2422e-152">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/</span></span>
<span data-ttu-id="2422e-153">[Microsoft Azure Storage SDK for Python (適用於 Python 的 Microsoft Azure 儲存體 SDK)]: https://github.com/Azure/azure-storage-python</span><span class="sxs-lookup"><span data-stu-id="2422e-153">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span></span>
