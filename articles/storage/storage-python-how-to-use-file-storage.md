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
# <a name="develop-for-azure-file-storage-with-python"></a>使用 Python 開發 Azure 檔案儲存體
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>關於本教學課程
本教學課程將示範 hello 使用 Python toodevelop 應用程式或服務使用 Azure 檔案儲存體 toostore 檔案資料的基本概念。 在本教學課程中，我們將建立簡單的主控台應用程式，並顯示如何使用 Python 和 Azure 檔案儲存體 tooperform 基本動作：

* 建立 Azure 檔案共用
* 建立目錄
* 列舉 Azure 檔案共用的檔案和目錄
* 上傳、下載及刪除檔案

> [!Note]  
> 因為可能透過 SMB 存取 Azure 檔案儲存體，所以可能 toowrite 簡單的應用程式存取 hello Azure 檔案共用使用 hello 標準 Python I/O 類別和函式。 本文將說明如何使用 toowrite 應用程式 hello Azure 儲存體 Python SDK，它會使用 hello [Azure 檔案儲存體 REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 檔案存放裝置。

### <a name="set-up-your-application-toouse-azure-file-storage"></a>設定您的應用程式 toouse Azure 檔案儲存體
將任何您想在其中 tooprogrammatically 存取 Azure 儲存體的 Python 原始程式檔的 hello 頂端附近的 hello 面一行加入。

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>設定連線 tooAzure 檔案存放裝置 
hello`FileService`物件可讓您使用共用、 目錄和檔案。 hello 下列程式碼會建立`FileService`使用 hello 儲存體帳戶名稱和帳戶金鑰的物件。 以您的帳戶名稱和金鑰取代 `<myaccount>` 和 `<mykey>`。

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>建立 Azure 檔案共用
在下列程式碼範例的 hello，您可以使用`FileService`物件 toocreate hello 共用如果不存在。

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>建立目錄
您也可以管理儲存體放而不需要全部都在 hello 根目錄的子目錄中的檔案。 Azure 檔案儲存體可讓您 toocreate 因為允許使用您的帳戶會當做多個目錄。 hello 的下列程式碼會建立名為子目錄**sampledir** hello 根目錄下。

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>列舉 Azure 檔案共用的檔案和目錄
toolist hello 檔案和目錄在共用，使用 hello**清單\_目錄\_和\_檔案**方法。 這個方法會傳回產生器。 hello 下列程式碼輸出 hello**名稱**的每個檔案和目錄在共用 toohello 主控台。

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>上傳檔案 
Azure 共用包含在 hello 非常少的檔案，檔案可以所在的根目錄。 在本節中，您將學習如何 tooupload 檔案從本機儲存體 hello 到根目錄的共用。

toocreate 檔案和上傳資料，使用 hello `create_file_from_path`， `create_file_from_stream`，`create_file_from_bytes`或`create_file_from_text`方法。 它們是執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時的高層級方法。

`create_file_from_path`上傳 hello 從 hello 指定的路徑、 檔案的內容和`create_file_from_stream`上傳 hello 從已開啟的檔案/資料流的內容。 `create_file_from_bytes`上傳的位元組陣列和`create_file_from_text`使用 hello 文字值會指定編碼 (預設值 tooUTF-8) 時，指定上傳 hello。

hello 下列範例會將上傳的 hello hello 內容**sunset.png**檔案 hello **myfile**檔案。

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>下載檔案
從檔案、 toodownload 資料使用`get_file_to_path`， `get_file_to_stream`， `get_file_to_bytes`，或`get_file_to_text`。 它們是執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時的高層級方法。

hello 下列範例示範如何使用`get_file_to_path`hello toodownload hello 內容**myfile**檔案，並將它儲存 toohello **out sunset.png**檔案。

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>刪除檔案
最後，toodelete 檔案，呼叫`delete_file`。

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>後續步驟
既然您已經學會如何 toomanipulate Azure 檔案儲存體使用 Python，依照這些連結 toolearn 更多。

* [Python 開發人員中心](/develop/python/)
* [Azure 儲存體服務 REST API](http://msdn.microsoft.com/library/azure/dd179355)
* [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python)