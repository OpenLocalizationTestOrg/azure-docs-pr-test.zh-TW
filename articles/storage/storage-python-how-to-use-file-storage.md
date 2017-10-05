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
# <a name="develop-for-azure-file-storage-with-python"></a>使用 Python 開發 Azure 檔案儲存體
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>關於本教學課程
本教學課程將示範使用 Python 來開發使用 Azure 檔案儲存體來儲存檔案資料的應用程式和服務之基本概念。 在本教學課程中，我們將建立簡單的主控台應用程式，並說明如何執行 Python 和 Azure 檔案儲存體的基本動作：

* 建立 Azure 檔案共用
* 建立目錄
* 列舉 Azure 檔案共用的檔案和目錄
* 上傳、下載及刪除檔案

> [!Note]  
> 由於 Azure 檔案儲存體可透過 SMB 存取，因此便可使用標準 Python I/O 類別和函式撰寫簡單的應用程式以存取 Azure 檔案共用。 本文將說明如何撰寫使用 Azure 儲存體 Python SDK 的應用程式，它會使用 [Azure 檔案儲存體 REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) 與 Azure 檔案儲存體通訊。

### <a name="set-up-your-application-to-use-azure-file-storage"></a>設定您的應用程式以使用 Azure 檔案儲存體
將下列內容新增至您想要在其中以程式設計方式存取 Azure 儲存體之任何 Python 來源檔案內的頂端附近。

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a>設定連接至 Azure 檔案儲存體 
`FileService` 物件可讓您使用共用、目錄和檔案。 下列程式碼會使用儲存體帳戶名稱和帳戶金鑰來建立 `FileService` 物件。 以您的帳戶名稱和金鑰取代 `<myaccount>` 和 `<mykey>`。

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>建立 Azure 檔案共用
在下列的程式碼範例中，如果共用不存在，您可以使用 `FileService` 物件建立共用。

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>建立目錄
您也可以組織儲存體，方法是將檔案放在子目錄中，而不是將所有檔案都放在根目錄中。 Azure 檔案儲存體可讓您建立您的帳戶允許數量的目錄。 下列程式碼會在根目錄底下建立名為 **sampledir** 的子目錄。

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>列舉 Azure 檔案共用的檔案和目錄
若要列出共用中的檔案和目錄，請使用 **list\_directories\_and\_files** 方法。 這個方法會傳回產生器。 下列程式碼會將共用中每個檔案和目錄的 **name** 輸出到主控台。

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>上傳檔案 
Azure 檔案共用至少包含根目錄，檔案可以放置其中。 在本節中，您將學習如何從本機儲存體將檔案上傳至共用的根目錄。

若要建立檔案並上傳資料，請使用 `create_file_from_path`、`create_file_from_stream`、`create_file_from_bytes` 或 `create_file_from_text` 方法。 這些是高階方法，可在資料大小超過 64 MB 時執行必要的區塊化動作。

`create_file_from_path` 會從指定的路徑上傳檔案的內容，`create_file_from_stream` 會從已開啟的檔案/串流上傳內容。 `create_file_from_bytes` 會上傳位元組陣列，`create_file_from_text` 會使用指定的編碼 (預設為 UTF-8) 上傳指定的文字值。

下列範例會將 **sunset.png** 檔案的內容上傳至 **myfile** 檔案中。

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>下載檔案
若要從檔案下載資料，請使用 `get_file_to_path`、`get_file_to_stream`、`get_file_to_bytes` 或 `get_file_to_text`。 這些是高階方法，可在資料大小超過 64 MB 時執行必要的區塊化動作。

下列範例示範如何使用 `get_file_to_path` 下載 **myfile** 檔案的內容，並將其儲存至 **out-sunset.png** 檔案。

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>刪除檔案
最後，若要刪除檔案，請呼叫 `delete_file`。

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>後續步驟
您現在已經學會如何使用 Python 操作 Azure 檔案儲存體，請遵循下列連結深入了解。

* [Python 開發人員中心](/develop/python/)
* [Azure 儲存體服務 REST API](http://msdn.microsoft.com/library/azure/dd179355)
* [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python)