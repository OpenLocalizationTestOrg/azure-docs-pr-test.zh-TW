---
title: "使用 Python Azure 檔案儲存的 aaaDevelop |Microsoft 文件"
description: "了解 toodevelop Python 應用程式和服務使用 Azure 檔案儲存體 toostore 檔案資料。"
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="53bd8-103">使用 Python 開發 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="53bd8-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="53bd8-104">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="53bd8-104">About this tutorial</span></span>
<span data-ttu-id="53bd8-105">本教學課程將示範 hello 使用 Python toodevelop 應用程式或服務使用 Azure 檔案儲存體 toostore 檔案資料的基本概念。</span><span class="sxs-lookup"><span data-stu-id="53bd8-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="53bd8-106">在本教學課程中，我們將建立簡單的主控台應用程式，並顯示如何使用 Python 和 Azure 檔案儲存體 tooperform 基本動作：</span><span class="sxs-lookup"><span data-stu-id="53bd8-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="53bd8-107">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="53bd8-107">Create Azure File shares</span></span>
* <span data-ttu-id="53bd8-108">建立目錄</span><span class="sxs-lookup"><span data-stu-id="53bd8-108">Create directories</span></span>
* <span data-ttu-id="53bd8-109">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="53bd8-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="53bd8-110">上傳、下載及刪除檔案</span><span class="sxs-lookup"><span data-stu-id="53bd8-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="53bd8-111">因為可能透過 SMB 存取 Azure 檔案儲存體，所以可能 toowrite 簡單的應用程式存取 hello Azure 檔案共用使用 hello 標準 Python I/O 類別和函式。</span><span class="sxs-lookup"><span data-stu-id="53bd8-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="53bd8-112">本文將說明如何使用 toowrite 應用程式 hello Azure 儲存體 Python SDK，它會使用 hello [Azure 檔案儲存體 REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 檔案存放裝置。</span><span class="sxs-lookup"><span data-stu-id="53bd8-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="53bd8-113">設定您的應用程式 toouse Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="53bd8-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="53bd8-114">將任何您想在其中 tooprogrammatically 存取 Azure 儲存體的 Python 原始程式檔的 hello 頂端附近的 hello 面一行加入。</span><span class="sxs-lookup"><span data-stu-id="53bd8-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="53bd8-115">設定連線 tooAzure 檔案存放裝置</span><span class="sxs-lookup"><span data-stu-id="53bd8-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="53bd8-116">hello`FileService`物件可讓您使用共用、 目錄和檔案。</span><span class="sxs-lookup"><span data-stu-id="53bd8-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="53bd8-117">hello 下列程式碼會建立`FileService`使用 hello 儲存體帳戶名稱和帳戶金鑰的物件。</span><span class="sxs-lookup"><span data-stu-id="53bd8-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="53bd8-118">以您的帳戶名稱和金鑰取代 `<myaccount>` 和 `<mykey>`。</span><span class="sxs-lookup"><span data-stu-id="53bd8-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="53bd8-119">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="53bd8-119">Create an Azure File share</span></span>
<span data-ttu-id="53bd8-120">在下列程式碼範例的 hello，您可以使用`FileService`物件 toocreate hello 共用如果不存在。</span><span class="sxs-lookup"><span data-stu-id="53bd8-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="53bd8-121">建立目錄</span><span class="sxs-lookup"><span data-stu-id="53bd8-121">Create a directory</span></span>
<span data-ttu-id="53bd8-122">您也可以管理儲存體放而不需要全部都在 hello 根目錄的子目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="53bd8-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="53bd8-123">Azure 檔案儲存體可讓您 toocreate 因為允許使用您的帳戶會當做多個目錄。</span><span class="sxs-lookup"><span data-stu-id="53bd8-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="53bd8-124">hello 的下列程式碼會建立名為子目錄**sampledir** hello 根目錄下。</span><span class="sxs-lookup"><span data-stu-id="53bd8-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="53bd8-125">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="53bd8-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="53bd8-126">toolist hello 檔案和目錄在共用，使用 hello**清單\_目錄\_和\_檔案**方法。</span><span class="sxs-lookup"><span data-stu-id="53bd8-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="53bd8-127">這個方法會傳回產生器。</span><span class="sxs-lookup"><span data-stu-id="53bd8-127">This method returns a generator.</span></span> <span data-ttu-id="53bd8-128">hello 下列程式碼輸出 hello**名稱**的每個檔案和目錄在共用 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="53bd8-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="53bd8-129">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="53bd8-129">Upload a file</span></span> 
<span data-ttu-id="53bd8-130">Azure 共用包含在 hello 非常少的檔案，檔案可以所在的根目錄。</span><span class="sxs-lookup"><span data-stu-id="53bd8-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="53bd8-131">在本節中，您將學習如何 tooupload 檔案從本機儲存體 hello 到根目錄的共用。</span><span class="sxs-lookup"><span data-stu-id="53bd8-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="53bd8-132">toocreate 檔案和上傳資料，使用 hello `create_file_from_path`， `create_file_from_stream`，`create_file_from_bytes`或`create_file_from_text`方法。</span><span class="sxs-lookup"><span data-stu-id="53bd8-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="53bd8-133">它們是執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時的高層級方法。</span><span class="sxs-lookup"><span data-stu-id="53bd8-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="53bd8-134">`create_file_from_path`上傳 hello 從 hello 指定的路徑、 檔案的內容和`create_file_from_stream`上傳 hello 從已開啟的檔案/資料流的內容。</span><span class="sxs-lookup"><span data-stu-id="53bd8-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="53bd8-135">`create_file_from_bytes`上傳的位元組陣列和`create_file_from_text`使用 hello 文字值會指定編碼 (預設值 tooUTF-8) 時，指定上傳 hello。</span><span class="sxs-lookup"><span data-stu-id="53bd8-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="53bd8-136">hello 下列範例會將上傳的 hello hello 內容**sunset.png**檔案 hello **myfile**檔案。</span><span class="sxs-lookup"><span data-stu-id="53bd8-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="53bd8-137">下載檔案</span><span class="sxs-lookup"><span data-stu-id="53bd8-137">Download a file</span></span>
<span data-ttu-id="53bd8-138">從檔案、 toodownload 資料使用`get_file_to_path`， `get_file_to_stream`， `get_file_to_bytes`，或`get_file_to_text`。</span><span class="sxs-lookup"><span data-stu-id="53bd8-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="53bd8-139">它們是執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時的高層級方法。</span><span class="sxs-lookup"><span data-stu-id="53bd8-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="53bd8-140">hello 下列範例示範如何使用`get_file_to_path`hello toodownload hello 內容**myfile**檔案，並將它儲存 toohello **out sunset.png**檔案。</span><span class="sxs-lookup"><span data-stu-id="53bd8-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="53bd8-141">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="53bd8-141">Delete a file</span></span>
<span data-ttu-id="53bd8-142">最後，toodelete 檔案，呼叫`delete_file`。</span><span class="sxs-lookup"><span data-stu-id="53bd8-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="53bd8-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53bd8-143">Next steps</span></span>
<span data-ttu-id="53bd8-144">既然您已經學會如何 toomanipulate Azure 檔案儲存體使用 Python，依照這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="53bd8-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="53bd8-145">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="53bd8-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="53bd8-146">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="53bd8-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="53bd8-147">Microsoft Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="53bd8-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)