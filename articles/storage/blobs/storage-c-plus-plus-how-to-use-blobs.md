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
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>如何 toouse 從 c + + 的 Blob 儲存體
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀
Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。 Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 Blob 儲存體也是參考的 tooas 物件儲存體。

本指南將示範如何使用 tooperform 常見案例 hello Azure Blob 儲存體服務。 hello 範例以 c + + 撰寫，並使用 hello [c + + 的 Azure 儲存體用戶端程式庫](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)。 hello 涵蓋案例包括**上載**，**列出**，**下載**，和**刪除**blob。  

> [!NOTE]
> 此指南的目標 hello Azure 儲存體用戶端程式庫，c + + 1.0.0 版和更新版本。 hello 建議版本是儲存體用戶端程式庫 2.2.0，也就是可透過使用[NuGet](http://www.nuget.org/packages/wastorage)或[GitHub](https://github.com/Azure/azure-storage-cpp)。
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>建立 C++ 應用程式
在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。  

toodo 因此，您將需要 tooinstall hello for c + + 的 Azure 儲存體用戶端程式庫，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。   

tooinstall hello Azure 儲存體用戶端程式庫的 c + +，，您可以使用下列方法的 hello:

* **Linux:**遵循 hello 所提供的 hello 指示[for c + + 讀我檔案的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)頁面。  
* **Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。 型別 hello 下列命令到 hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)按**ENTER**。  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>設定您的應用程式 tooaccess Blob 儲存體
加入 hello 下列包含您想要 toouse hello Azure 儲存體 Api tooaccess blob hello c + + 檔案的陳述式 toohello 頂端：  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。 用戶端應用程式中執行時，您必須提供 hello 遵循格式，並透過儲存體帳戶和 hello 儲存體存取金鑰的 hello 名稱 hello hello 中所列的儲存體帳戶中的 hello 儲存體連接字串[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。 如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。 此範例顯示如何宣告靜態欄位 toohold hello 連接字串：  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest 您的應用程式在本機的 Windows 電腦，您可以使用 Microsoft Azure 的 hello[儲存體模擬器](../storage-use-emulator.md)會隨 hello [Azure SDK](https://azure.microsoft.com/downloads/)。 hello 儲存體模擬器是模擬 hello Blob、 佇列和表格服務在本機開發電腦上可用在 Azure 中的公用程式。 hello 下列範例顯示如何宣告靜態欄位 toohold hello 連接字串 tooyour 本機儲存體模擬器：

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure 儲存體模擬器中，選取 hello**啟動**按鈕或按 hello **Windows**索引鍵。 開始輸入**Azure 儲存體模擬器**，然後選取**Microsoft Azure 儲存體模擬器**hello 清單中的應用程式。  

hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。  

## <a name="retrieve-your-connection-string"></a>擷取連接字串
您可以使用 hello**驗證 cloud_storage_account**類別 toorepresent 儲存體帳戶資訊。 tooretrieve 您的儲存體帳戶資訊 hello 儲存體連接字串，您可以使用 hello**剖析**方法。  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

接下來，取得參考 tooa **cloud_blob_client**類別，如它可讓您表示容器和 blob 儲存在 Blob 儲存體服務的 hello tooretrieve 物件。 hello 下列程式碼會建立**cloud_blob_client**使用 hello 我們擷取上述的儲存體帳戶物件的物件：  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>作法：建立容器
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

這個範例會示範如何 toocreate 如果不存在的容器：  

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

根據預設，hello 新容器是 private，而且您必須指定您的儲存體存取金鑰 toodownload blob，從這個容器。 如果您要設定 hello 容器可用 tooeveryone toomake hello 檔案 (blob)，您可以設定 hello 容器 toobe 公用使用下列程式碼的 hello:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Hello 網際網路上的任何人可以看到公用容器中的 blob，但您可以修改或刪除它們，只有當您擁有 hello 適當的存取金鑰。  

## <a name="how-to-upload-a-blob-into-a-container"></a>作法：將 Blob 上傳到容器中
Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。 Hello 大部分的情況下，在區塊 blob 會是建議的型別 toouse hello。  

tooupload 檔案 tooa 區塊 blob，取得容器的參考，並將它 tooget 區塊 blob 參考。 Blob 參考之後，您可以上傳任何資料流的資料 tooit 呼叫 hello **upload_from_stream**方法。 如果先前沒有存在，或覆寫它存在的話，這項作業將會建立 hello blob。 下列範例會示範如何 hello tooupload blob 容器，並假設已建立該 hello 容器。  

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

或者，您可以使用 hello **upload_from_file**方法 tooupload 檔案 tooa 區塊 blob。

## <a name="how-to-list-hello-blobs-in-a-container"></a>如何： 列出容器中的 hello blob
toolist hello blob 容器中的第一次取得容器的參考。 然後，您可以使用 hello 容器**list_blobs**方法 tooretrieve hello blob 及/或目錄內。 tooaccess hello 豐富的屬性和方法傳回**list_blob_item**，您必須呼叫 hello **list_blob_item.as_blob**方法 tooget **cloud_blob**物件，或 hello **list_blob.as_directory**方法 tooget cloud_blob_directory 物件。 hello 下列程式碼示範如何 tooretrieve 和輸出 hello hello 中每個項目的 URI**我範例容器**容器：

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

如需列出作業的詳細資訊，請參閱 [以 C++ 列出 Azure 儲存體資源](../storage-c-plus-plus-enumeration.md)。

## <a name="how-to-download-blobs"></a>作法：下載 Blob
toodownload blob，先擷取 blob 的參考，然後再呼叫 hello **download_to_stream**方法。 hello 下列範例會使用 hello **download_to_stream**方法 tootransfer hello blob 內容 tooa 資料流物件，您可以再保存 tooa 本機檔案。  

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

或者，您可以使用 hello **download_to_file**方法 toodownload hello blob tooa 檔案的內容。
此外，您也可以使用 hello **download_text**方法 toodownload hello 內容為文字字串的 blob。  

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

## <a name="how-to-delete-blobs"></a>作法：刪除 Blob
toodelete blob，先取得 blob 的參考，然後再呼叫 hello **delete_blob**方法。  

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

## <a name="next-steps"></a>後續步驟
現在，您學到的 blob 儲存體的 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure 儲存體。  

* [如何 toouse 佇列儲存體從 c + +](../storage-c-plus-plus-how-to-use-queues.md)
* [如何 toouse 從 c + + 的資料表儲存體](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [以 C++ 列出 Azure 儲存體資源](../storage-c-plus-plus-enumeration.md)
* [Storage Client Library for C++ 參考資料](http://azure.github.io/azure-storage-cpp)
* [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)
* [使用 hello AzCopy 命令列公用程式傳輸資料](../storage-use-azcopy.md)

