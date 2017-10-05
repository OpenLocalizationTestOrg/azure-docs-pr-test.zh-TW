---
title: "使用 Python 開發 Azure 檔案儲存體 | Microsoft Docs"
description: "了解如何開發使用 Azure 檔案儲存體來儲存檔案資料的 Python 應用程式和服務。"
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
ms.openlocfilehash: a1a37266908277b54e7b42d85b9b4873af77e622
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="97e03-103">使用 Python 開發 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="97e03-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="97e03-104">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="97e03-104">About this tutorial</span></span>
<span data-ttu-id="97e03-105">本教學課程將示範使用 Python 來開發使用 Azure 檔案儲存體來儲存檔案資料的應用程式和服務之基本概念。</span><span class="sxs-lookup"><span data-stu-id="97e03-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="97e03-106">在本教學課程中，我們將建立簡單的主控台應用程式，並說明如何執行 Python 和 Azure 檔案儲存體的基本動作：</span><span class="sxs-lookup"><span data-stu-id="97e03-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="97e03-107">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="97e03-107">Create Azure File shares</span></span>
* <span data-ttu-id="97e03-108">建立目錄</span><span class="sxs-lookup"><span data-stu-id="97e03-108">Create directories</span></span>
* <span data-ttu-id="97e03-109">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="97e03-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="97e03-110">上傳、下載及刪除檔案</span><span class="sxs-lookup"><span data-stu-id="97e03-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="97e03-111">由於 Azure 檔案儲存體可透過 SMB 存取，因此便可使用標準 Python I/O 類別和函式撰寫簡單的應用程式以存取 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="97e03-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="97e03-112">本文將說明如何撰寫使用 Azure 儲存體 Python SDK 的應用程式，它會使用 [Azure 檔案儲存體 REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) 與 Azure 檔案儲存體通訊。</span><span class="sxs-lookup"><span data-stu-id="97e03-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="97e03-113">設定您的應用程式以使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="97e03-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="97e03-114">將下列內容新增至您想要在其中以程式設計方式存取 Azure 儲存體之任何 Python 來源檔案內的頂端附近。</span><span class="sxs-lookup"><span data-stu-id="97e03-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="97e03-115">設定連接至 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="97e03-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="97e03-116">`FileService` 物件可讓您使用共用、目錄和檔案。</span><span class="sxs-lookup"><span data-stu-id="97e03-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="97e03-117">下列程式碼會使用儲存體帳戶名稱和帳戶金鑰來建立 `FileService` 物件。</span><span class="sxs-lookup"><span data-stu-id="97e03-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="97e03-118">以您的帳戶名稱和金鑰取代 `<myaccount>` 和 `<mykey>`。</span><span class="sxs-lookup"><span data-stu-id="97e03-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="97e03-119">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="97e03-119">Create an Azure File share</span></span>
<span data-ttu-id="97e03-120">在下列的程式碼範例中，如果共用不存在，您可以使用 `FileService` 物件建立共用。</span><span class="sxs-lookup"><span data-stu-id="97e03-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="97e03-121">建立目錄</span><span class="sxs-lookup"><span data-stu-id="97e03-121">Create a directory</span></span>
<span data-ttu-id="97e03-122">您也可以組織儲存體，方法是將檔案放在子目錄中，而不是將所有檔案都放在根目錄中。</span><span class="sxs-lookup"><span data-stu-id="97e03-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="97e03-123">Azure 檔案儲存體可讓您建立您的帳戶允許數量的目錄。</span><span class="sxs-lookup"><span data-stu-id="97e03-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="97e03-124">下列程式碼會在根目錄底下建立名為 **sampledir** 的子目錄。</span><span class="sxs-lookup"><span data-stu-id="97e03-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="97e03-125">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="97e03-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="97e03-126">若要列出共用中的檔案和目錄，請使用 **list\_directories\_and\_files** 方法。</span><span class="sxs-lookup"><span data-stu-id="97e03-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="97e03-127">這個方法會傳回產生器。</span><span class="sxs-lookup"><span data-stu-id="97e03-127">This method returns a generator.</span></span> <span data-ttu-id="97e03-128">下列程式碼會將共用中每個檔案和目錄的 **name** 輸出到主控台。</span><span class="sxs-lookup"><span data-stu-id="97e03-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="97e03-129">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="97e03-129">Upload a file</span></span> 
<span data-ttu-id="97e03-130">Azure 檔案共用至少包含根目錄，檔案可以放置其中。</span><span class="sxs-lookup"><span data-stu-id="97e03-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="97e03-131">在本節中，您將學習如何從本機儲存體將檔案上傳至共用的根目錄。</span><span class="sxs-lookup"><span data-stu-id="97e03-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="97e03-132">若要建立檔案並上傳資料，請使用 `create_file_from_path`、`create_file_from_stream`、`create_file_from_bytes` 或 `create_file_from_text` 方法。</span><span class="sxs-lookup"><span data-stu-id="97e03-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="97e03-133">這些是高階方法，可在資料大小超過 64 MB 時執行必要的區塊化動作。</span><span class="sxs-lookup"><span data-stu-id="97e03-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="97e03-134">`create_file_from_path` 會從指定的路徑上傳檔案的內容，`create_file_from_stream` 會從已開啟的檔案/串流上傳內容。</span><span class="sxs-lookup"><span data-stu-id="97e03-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="97e03-135">`create_file_from_bytes` 會上傳位元組陣列，`create_file_from_text` 會使用指定的編碼 (預設為 UTF-8) 上傳指定的文字值。</span><span class="sxs-lookup"><span data-stu-id="97e03-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="97e03-136">下列範例會將 **sunset.png** 檔案的內容上傳至 **myfile** 檔案中。</span><span class="sxs-lookup"><span data-stu-id="97e03-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="97e03-137">下載檔案</span><span class="sxs-lookup"><span data-stu-id="97e03-137">Download a file</span></span>
<span data-ttu-id="97e03-138">若要從檔案下載資料，請使用 `get_file_to_path`、`get_file_to_stream`、`get_file_to_bytes` 或 `get_file_to_text`。</span><span class="sxs-lookup"><span data-stu-id="97e03-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="97e03-139">這些是高階方法，可在資料大小超過 64 MB 時執行必要的區塊化動作。</span><span class="sxs-lookup"><span data-stu-id="97e03-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="97e03-140">下列範例示範如何使用 `get_file_to_path` 下載 **myfile** 檔案的內容，並將其儲存至 **out-sunset.png** 檔案。</span><span class="sxs-lookup"><span data-stu-id="97e03-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="97e03-141">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="97e03-141">Delete a file</span></span>
<span data-ttu-id="97e03-142">最後，若要刪除檔案，請呼叫 `delete_file`。</span><span class="sxs-lookup"><span data-stu-id="97e03-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="97e03-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97e03-143">Next steps</span></span>
<span data-ttu-id="97e03-144">您現在已經學會如何使用 Python 操作 Azure 檔案儲存體，請遵循下列連結深入了解。</span><span class="sxs-lookup"><span data-stu-id="97e03-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="97e03-145">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="97e03-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="97e03-146">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="97e03-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="97e03-147">Microsoft Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="97e03-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)