---
title: "aaaHow toouse Ruby 從 Blob 儲存體 （物件儲存體） |Microsoft 文件"
description: "使用 Azure Blob 儲存體 （物件儲存體） 的 hello 雲端中儲存非結構化的資料。"
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>如何 toouse Ruby 從 Blob 儲存體
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀
Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。 Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 Blob 儲存體也是參考的 tooas 物件儲存體。

本指南說明您如何使用 Blob 儲存體 tooperform 常見案例。 使用 hello Ruby 應用程式開發介面撰寫 hello 範例。 hello 涵蓋案例包括**上傳、 列出、 下載**和**刪除**blob。

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>建立 Ruby 應用程式
建立 Ruby 應用程式。 如需指示，請參閱 [Azure VM 上的 Ruby on Rails Web 應用程式](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)

## <a name="configure-your-application-tooaccess-storage"></a>設定您的應用程式 tooaccess 儲存體
toouse Azure 儲存體，您需要 toodownload 和使用 hello 拼音 azure 的封裝，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。

### <a name="use-rubygems-tooobtain-hello-package"></a>使用 RubyGems tooobtain hello 套件
1. 使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。
2. 輸入健身安裝 azure 」 在 hello 命令視窗 tooinstall hello 健身和相依性。

### <a name="import-hello-package"></a>匯入 hello 封裝
使用慣用的文字編輯器，加入下列 toohello hello 拼音想 toouse 儲存體的檔案頂端的 hello:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>設定 Azure 儲存體連接
hello azure 模組會讀取 hello 環境變數**AZURE\_儲存體\_帳戶**和**AZURE\_儲存體\_ACCESS_KEY**的tooconnect tooyour Azure 儲存體帳戶所需的資訊。 如果未設定這些環境變數，您必須指定 hello 帳戶資訊，才能使用**Azure::Blob::BlobService**以下列程式碼的 hello:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain hello Azure 入口網站中的帳戶從傳統或資源管理員儲存這些值：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 瀏覽您想 toouse toohello 儲存體帳戶。
3. 在 hello 設定 刀鋒視窗上 hello 右邊，按一下 **便捷鍵**。
4. 在 hello 存取金鑰刀鋒視窗中出現，您會看到 hello 便捷鍵 1 和 2 的存取金鑰。 您可以使用其中一個存取金鑰。
5. 按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。

## <a name="create-a-container"></a>建立容器
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

hello **Azure::Blob::BlobService**物件可讓您使用容器和 blob。 toocreate 容器，使用 hello**建立\_container()**方法。

hello 下列程式碼範例會建立容器，或列印 hello 錯誤如果有的話。

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

如果您想 toomake hello 容器中的 hello 檔案公用，您可以設定 hello 容器的權限。

您可以只修改 hello<strong>建立\_container()</strong>呼叫 toopass hello **： 公用\_存取\_層級**選項：

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

有效的值為 hello **： 公用\_存取\_層級**選項：

* **blob：** 指定 Blob 的公用讀取權限。 您可以透過匿名要求讀取此容器內的 Blob 資料，但您無法使用容器資料。 用戶端無法列舉 hello 透過匿名要求的容器中的 blob。
* **container：**指定容器和 Blob 資料的完整公用讀取權限。 用戶端透過匿名要求，hello 容器內的 blob，但無法列舉 hello 儲存體帳戶中的容器。

或者，您可以修改容器的 hello 公用存取層級使用**設定\_容器\_acl()**方法 toospecify hello 公用存取層級。

下列程式碼範例變更太 hello 公用存取層級的 hello**容器**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
tooupload 內容 tooa blob、 使用 hello**建立\_區塊\_blob()**方法 toocreate hello blob，使用檔案或字串做為 hello 的 hello blob 的內容。

hello 下列程式碼檔案上傳 hello **test.png**為名為 「 映像的 blob"hello 容器中的新 blob。

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
toolist hello 容器，使用**list_containers()**方法。
toolist hello blob 容器內使用**清單\_blobs()**方法。

這會輸出所有 hello blob hello 帳戶所有 hello 容器中的 hello url。

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>下載 Blob
toodownload blob 使用 hello**取得\_blob()**方法 tooretrieve hello 內容。

hello 下列程式碼範例示範如何使用**取得\_blob()** toodownload hello 」 映像 blob"的內容，並將它寫入 tooa 本機檔案。

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>刪除 Blob
最後，toodelete blob，使用 hello**刪除\_blob()**方法。 hello 下列程式碼範例示範如何 toodelete blob。

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>後續步驟
更複雜的存放工作需 toolearn 請追蹤下列連結：

* [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)
* GitHub 上的 [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) 儲存機制
* [使用 AzCopy 命令列公用程式的 hello 傳輸資料](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

