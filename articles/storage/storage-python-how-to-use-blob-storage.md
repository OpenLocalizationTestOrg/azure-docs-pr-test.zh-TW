---
title: "aaaHow toouse 來自 Python 的 Azure Blob 儲存體 （物件儲存體） |Microsoft 文件"
description: "使用 Azure Blob 儲存體 （物件儲存體） 的 hello 雲端中儲存非結構化的資料。"
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
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="120ca-103">如何 toouse 來自 Python 的 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="120ca-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="120ca-104">概觀</span><span class="sxs-lookup"><span data-stu-id="120ca-104">Overview</span></span>
<span data-ttu-id="120ca-105">Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。</span><span class="sxs-lookup"><span data-stu-id="120ca-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="120ca-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="120ca-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="120ca-107">Blob 儲存體也是參考的 tooas 物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="120ca-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="120ca-108">這篇文章將示範如何使用 Blob 儲存體 tooperform 常見案例。</span><span class="sxs-lookup"><span data-stu-id="120ca-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="120ca-109">hello 範例撰寫的 Python 和使用 hello [Microsoft Azure 儲存體 SDK for Python]。</span><span class="sxs-lookup"><span data-stu-id="120ca-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="120ca-110">涵蓋的 hello 案例包括上傳、 列出、 下載和刪除 blob。</span><span class="sxs-lookup"><span data-stu-id="120ca-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="120ca-111">建立容器</span><span class="sxs-lookup"><span data-stu-id="120ca-111">Create a container</span></span>
<span data-ttu-id="120ca-112">根據 blob hello 類型您想要 toouse，建立**BlockBlobService**， **AppendBlobService**，或**PageBlobService**物件。</span><span class="sxs-lookup"><span data-stu-id="120ca-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="120ca-113">hello 下列程式碼使用**BlockBlobService**物件。</span><span class="sxs-lookup"><span data-stu-id="120ca-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="120ca-114">加入要在其中任何 Python 檔案 tooprogrammatically 存取 Azure 區塊 Blob 儲存體的 hello 頂端附近的 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="120ca-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="120ca-115">hello 下列程式碼會建立**BlockBlobService**使用 hello 儲存體帳戶名稱和帳戶金鑰的物件。</span><span class="sxs-lookup"><span data-stu-id="120ca-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="120ca-116">將 'myaccount' 和 'mykey' 取代為您的帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="120ca-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="120ca-117">在下列程式碼範例的 hello，您可以使用**BlockBlobService**物件 toocreate hello 容器如果不存在。</span><span class="sxs-lookup"><span data-stu-id="120ca-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="120ca-118">根據預設，hello 新容器是私人的所以您必須指定儲存體存取金鑰 （如先前般） toodownload 從這個容器的 blob。</span><span class="sxs-lookup"><span data-stu-id="120ca-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="120ca-119">如果您想在 hello 容器可用 tooeveryone toomake hello blob，您可以建立 hello 容器，並傳遞 hello 公用存取層級，使用下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="120ca-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="120ca-120">或者，您也可以使用下列程式碼的 hello 建立之後修改容器。</span><span class="sxs-lookup"><span data-stu-id="120ca-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="120ca-121">此變更後，hello 網際網路上的任何人可以看到公用容器中的 blob，但只有您可以修改或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="120ca-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="120ca-122">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="120ca-122">Upload a blob into a container</span></span>
<span data-ttu-id="120ca-123">toocreate 區塊 blob 和上傳資料，使用 hello**建立\_blob\_從\_路徑**，**建立\_blob\_從\_資料流**，**建立\_blob\_從\_位元組**或**建立\_blob\_從\_文字**方法。</span><span class="sxs-lookup"><span data-stu-id="120ca-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="120ca-124">它們是執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時的高層級方法。</span><span class="sxs-lookup"><span data-stu-id="120ca-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="120ca-125">**建立\_blob\_從\_路徑**上傳 hello 從 hello 指定的路徑、 檔案的內容和**建立\_blob\_從\_資料流**上傳 hello 從已開啟的檔案/資料流的內容。</span><span class="sxs-lookup"><span data-stu-id="120ca-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="120ca-126">**建立\_blob\_從\_位元組**上傳的位元組陣列和**建立\_blob\_從\_文字**會上傳指定的 hello使用 hello 文字值會指定編碼 (預設值 tooUTF-8)。</span><span class="sxs-lookup"><span data-stu-id="120ca-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="120ca-127">hello 下列範例會將上傳的 hello hello 內容**sunset.png**檔案 hello **myblob** blob。</span><span class="sxs-lookup"><span data-stu-id="120ca-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="120ca-128">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="120ca-128">List hello blobs in a container</span></span>
<span data-ttu-id="120ca-129">toolist hello blob 容器中的使用 hello**清單\_blob**方法。</span><span class="sxs-lookup"><span data-stu-id="120ca-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="120ca-130">這個方法會傳回產生器。</span><span class="sxs-lookup"><span data-stu-id="120ca-130">This method returns a generator.</span></span> <span data-ttu-id="120ca-131">hello 下列程式碼輸出 hello**名稱**容器 toohello 主控台中的每個 blob。</span><span class="sxs-lookup"><span data-stu-id="120ca-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="120ca-132">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="120ca-132">Download blobs</span></span>
<span data-ttu-id="120ca-133">從 blob，toodownload 資料使用**取得\_blob\_至\_路徑**，**取得\_blob\_至\_資料流**， **取得\_blob\_至\_位元組**，或**取得\_blob\_至\_文字**。</span><span class="sxs-lookup"><span data-stu-id="120ca-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="120ca-134">它們是執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時的高層級方法。</span><span class="sxs-lookup"><span data-stu-id="120ca-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="120ca-135">hello 下列範例示範如何使用**取得\_blob\_至\_路徑**hello toodownload hello 內容**myblob** blob，並將它儲存 toohello **out sunset.png**檔案。</span><span class="sxs-lookup"><span data-stu-id="120ca-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="120ca-136">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="120ca-136">Delete a blob</span></span>
<span data-ttu-id="120ca-137">最後，呼叫 toodelete blob， **delete_blob**。</span><span class="sxs-lookup"><span data-stu-id="120ca-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="120ca-138">寫入 tooan 附加 blob</span><span class="sxs-lookup"><span data-stu-id="120ca-138">Writing tooan append blob</span></span>
<span data-ttu-id="120ca-139">附加 Blob 已針對附加作業 (例如紀錄) 最佳化。</span><span class="sxs-lookup"><span data-stu-id="120ca-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="120ca-140">為區塊 blob，例如附加 blob 區塊組成，但當您新增新的區塊 tooan 附加 blob 時，它一律是附加的 toohello hello blob 結尾。</span><span class="sxs-lookup"><span data-stu-id="120ca-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="120ca-141">您無法更新或刪除附加 Blob 中的現有區塊。</span><span class="sxs-lookup"><span data-stu-id="120ca-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="120ca-142">因為它們是區塊 blob，不會公開附加 blob 的 hello 區塊識別碼。</span><span class="sxs-lookup"><span data-stu-id="120ca-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="120ca-143">每個區塊中附加 blob 可以是不同的大小，tooa 最大值為 4 MB，總而且附加 blob 不可包括最多 50,000 個區塊。</span><span class="sxs-lookup"><span data-stu-id="120ca-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="120ca-144">hello 附加 blob 的大小上限，因此是稍微大於 195 GB （4 MB X 50000 區塊）。</span><span class="sxs-lookup"><span data-stu-id="120ca-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="120ca-145">hello 下面範例會建立新的附加 blob，並將附加一些資料 tooit，模擬簡單的記錄作業。</span><span class="sxs-lookup"><span data-stu-id="120ca-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="120ca-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="120ca-146">Next steps</span></span>
<span data-ttu-id="120ca-147">現在，您學到的 Blob 儲存體的 hello 基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="120ca-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="120ca-148">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="120ca-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="120ca-149">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="120ca-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="120ca-150">[Azure 儲存體團隊部落格]</span><span class="sxs-lookup"><span data-stu-id="120ca-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="120ca-151">[Microsoft Azure 儲存體 SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="120ca-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure 儲存體團隊部落格]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure 儲存體 SDK for Python]: https://github.com/Azure/azure-storage-python
