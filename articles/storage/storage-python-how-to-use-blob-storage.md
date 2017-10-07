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
# <a name="how-toouse-azure-blob-storage-from-python"></a>如何 toouse 來自 Python 的 Azure Blob 儲存體
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀
Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。 Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 Blob 儲存體也是參考的 tooas 物件儲存體。

這篇文章將示範如何使用 Blob 儲存體 tooperform 常見案例。 hello 範例撰寫的 Python 和使用 hello [Microsoft Azure 儲存體 SDK for Python]。 涵蓋的 hello 案例包括上傳、 列出、 下載和刪除 blob。

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>建立容器
根據 blob hello 類型您想要 toouse，建立**BlockBlobService**， **AppendBlobService**，或**PageBlobService**物件。 hello 下列程式碼使用**BlockBlobService**物件。 加入要在其中任何 Python 檔案 tooprogrammatically 存取 Azure 區塊 Blob 儲存體的 hello 頂端附近的 hello 下列。

```python
from azure.storage.blob import BlockBlobService
```

hello 下列程式碼會建立**BlockBlobService**使用 hello 儲存體帳戶名稱和帳戶金鑰的物件。  將 'myaccount' 和 'mykey' 取代為您的帳戶名稱和金鑰。

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

在下列程式碼範例的 hello，您可以使用**BlockBlobService**物件 toocreate hello 容器如果不存在。

```python
block_blob_service.create_container('mycontainer')
```

根據預設，hello 新容器是私人的所以您必須指定儲存體存取金鑰 （如先前般） toodownload 從這個容器的 blob。 如果您想在 hello 容器可用 tooeveryone toomake hello blob，您可以建立 hello 容器，並傳遞 hello 公用存取層級，使用下列程式碼的 hello。

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

或者，您也可以使用下列程式碼的 hello 建立之後修改容器。

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

此變更後，hello 網際網路上的任何人可以看到公用容器中的 blob，但只有您可以修改或刪除它們。

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
toocreate 區塊 blob 和上傳資料，使用 hello**建立\_blob\_從\_路徑**，**建立\_blob\_從\_資料流**，**建立\_blob\_從\_位元組**或**建立\_blob\_從\_文字**方法。 它們是執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時的高層級方法。

**建立\_blob\_從\_路徑**上傳 hello 從 hello 指定的路徑、 檔案的內容和**建立\_blob\_從\_資料流**上傳 hello 從已開啟的檔案/資料流的內容。 **建立\_blob\_從\_位元組**上傳的位元組陣列和**建立\_blob\_從\_文字**會上傳指定的 hello使用 hello 文字值會指定編碼 (預設值 tooUTF-8)。

hello 下列範例會將上傳的 hello hello 內容**sunset.png**檔案 hello **myblob** blob。

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
toolist hello blob 容器中的使用 hello**清單\_blob**方法。 這個方法會傳回產生器。 hello 下列程式碼輸出 hello**名稱**容器 toohello 主控台中的每個 blob。

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>下載 Blob
從 blob，toodownload 資料使用**取得\_blob\_至\_路徑**，**取得\_blob\_至\_資料流**， **取得\_blob\_至\_位元組**，或**取得\_blob\_至\_文字**。 它們是執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時的高層級方法。

hello 下列範例示範如何使用**取得\_blob\_至\_路徑**hello toodownload hello 內容**myblob** blob，並將它儲存 toohello **out sunset.png**檔案。

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>刪除 Blob
最後，呼叫 toodelete blob， **delete_blob**。

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>寫入 tooan 附加 blob
附加 Blob 已針對附加作業 (例如紀錄) 最佳化。 為區塊 blob，例如附加 blob 區塊組成，但當您新增新的區塊 tooan 附加 blob 時，它一律是附加的 toohello hello blob 結尾。 您無法更新或刪除附加 Blob 中的現有區塊。 因為它們是區塊 blob，不會公開附加 blob 的 hello 區塊識別碼。

每個區塊中附加 blob 可以是不同的大小，tooa 最大值為 4 MB，總而且附加 blob 不可包括最多 50,000 個區塊。 hello 附加 blob 的大小上限，因此是稍微大於 195 GB （4 MB X 50000 區塊）。

hello 下面範例會建立新的附加 blob，並將附加一些資料 tooit，模擬簡單的記錄作業。

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

## <a name="next-steps"></a>後續步驟
現在，您學到的 Blob 儲存體的 hello 基本概念，請遵循這些連結 toolearn 更多。

* [Python 開發人員中心](https://azure.microsoft.com/develop/python/)
* [Azure 儲存體服務 REST API](http://msdn.microsoft.com/library/azure/dd179355)
* [Azure 儲存體團隊部落格]
* [Microsoft Azure 儲存體 SDK for Python]

[Azure 儲存體團隊部落格]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure 儲存體 SDK for Python]: https://github.com/Azure/azure-storage-python
