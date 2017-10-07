---
title: "使用 c + + 的 Azure 檔案儲存的 aaaDevelop |Microsoft 文件"
description: "了解 toodevelop c + + 應用程式和服務使用 Azure 檔案儲存體 toostore 檔案資料。"
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 40c3aac94214a91121913e2ded315031aeed1c30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>使用 C++ 開發 Azure 檔案儲存體
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>關於本教學課程

在此教學課程中，您將學習如何 tooperform Azure 檔案儲存體的基本作業。 透過以 c + + 撰寫的範例，您將學習如何 toocreate 共用與目錄上傳、 列出，請刪除檔案。 如果您是新的 tooAzure 檔案存放裝置，透過 hello 以下各節中的 hello 概念將有助於了解 hello 範例。


* 建立及刪除 Azure 檔案共用
* 建立及刪除目錄
* 列舉 Azure 檔案共用的檔案和目錄
* 上傳、下載及刪除檔案
* 設定 Azure 檔案共用的 hello 配額 （最大大小）
* 建立使用共用的存取原則，定義 hello 共用上的檔案共用的存取簽章 （SAS 索引鍵）。

> [!Note]  
> 因為可能透過 SMB 存取 Azure 檔案儲存體，所以可能 toowrite 簡單的應用程式存取 hello Azure 檔案共用使用 hello 標準 c + + I/O 類別和函式。 本文將說明如何使用 toowrite 應用程式 hello Azure 儲存體 c + + SDK，它會使用 hello [Azure 檔案儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 檔案存放裝置。

## <a name="create-a-c-application"></a>建立 C++ 應用程式
toobuild hello 範例，您將需要 tooinstall hello Azure 儲存體用戶端程式庫 2.4.0 for c + +。 您也應該建立 Azure 儲存體帳戶。

tooinstall hello Azure 儲存體用戶端 2.4.0 for c + +，您可以使用其中一個 hello 下列方法：

* **Linux:**遵循 hello 所提供的 hello 指示[for c + + 讀我檔案的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)頁面。
* **Windows：**在 Visual Studio 中，按一下 [工具]&gt;[NuGet 套件管理員]&gt;[套件管理員主控台]。 型別 hello 下列命令到 hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)按**ENTER**。
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>設定您的應用程式 toouse Azure 檔案儲存體
加入 hello 下列包含陳述式 toohello 頂端 hello 想 toomanipulate Azure 檔案儲存體的 c + + 原始程式檔：

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
toouse 檔案存放裝置，您需要 tooconnect tooyour Azure 儲存體帳戶。 hello 第一個步驟就是連接字串，我們將使用 tooconfigure tooconnect tooyour 儲存體帳戶。 讓我們來定義靜態變數 toodo 的。

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>連接 tooan Azure 儲存體帳戶
您可以使用 hello**驗證 cloud_storage_account**類別 toorepresent 儲存體帳戶資訊。 tooretrieve 您的儲存體帳戶資訊 hello 儲存體連接字串，您可以使用 hello**剖析**方法。

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>建立 Azure 檔案共用
Azure 檔案儲存體中的所有檔案和目錄都位於名為 [共用] 的容器中。 您的儲存體帳戶可以有帳戶容量允許數量的共用。 tooobtain 存取 tooa 共用和其內容，您會需要 toouse Azure 檔案儲存體用戶端。

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

使用 hello Azure 檔案儲存體用戶端，您可以再取得參考 tooa 共用。

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

toocreate hello 共用，使用 hello **create_if_not_exists**方法 hello **cloud_file_share**物件。

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

此時，**共用**保存參考 tooa 共用名為**我範例共用**。

## <a name="delete-an-azure-file-share"></a>刪除 Azure 檔案共用
刪除共用由呼叫 hello **delete_if_exists** cloud_file_share 物件上的方法。 以下是執行該作業的範例程式碼。

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>建立目錄
您可以將儲存體放而不需要全部都在 hello 根目錄的子目錄中的檔案。 Azure 檔案儲存體可讓您 toocreate 因為允許使用您的帳戶會當做多個目錄。 hello 的下列程式碼會建立名為目錄**我範例目錄**hello 根目錄，以及命名的子目錄下**我範例子目錄**。

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>刪除目錄
刪除目錄是一項簡單的工作，不過請注意您無法刪除仍然包含檔案或其他目錄的目錄。

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>列舉 Azure 檔案共用的檔案和目錄
取得共用內檔案和目錄的清單很容易，只要在 **cloud_file_directory** 參考上呼叫 **list_files_and_directories** 即可。 tooaccess hello 豐富的屬性和方法傳回**list_file_and_directory_item**，您必須呼叫 hello **list_file_and_directory_item.as_file**方法 tooget **cloud_檔案**物件或 hello **list_file_and_directory_item.as_directory**方法 tooget **cloud_file_directory**物件。

下列程式碼的 hello 示範 tooretrieve 和輸出 hello hello 根目錄中的 hello 共用每個項目的 URI。

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a>上傳檔案
在 hello 很少，對 Azure 檔案共用會包含檔案可以所在的根目錄。 在本節中，您將學習如何 tooupload 檔案從本機儲存體 hello 到根目錄的共用。

hello 中上傳檔案的第一個步驟是 tooobtain 它所在的位置參考 toohello 目錄。 您可以呼叫 hello **get_root_directory_reference** hello 共用物件的方法。

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

有參考 toohello 根目錄的 hello 共用之後，您可以上傳至其本身的檔案。 此範例會從檔案、文字和串流進行上傳。

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a>下載檔案
toodownload 檔案第一次擷取的檔案參考，然後呼叫 hello **download_to_stream**方法 tootransfer hello 檔案內容 tooa 資料流物件，您可以保存 tooa 本機檔案。 或者，您可以使用 hello **download_to_file**方法 toodownload hello 檔案 tooa 本機檔案的內容。 您可以使用 hello **download_text**方法 toodownload hello 內容為文字字串的檔案。

hello 下列範例會使用 hello **download_to_stream**和**download_text**方法 toodemonstrate 下載 hello 檔案，在上一節中所建立。

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a>刪除檔案
另一個常見的 Azure 檔案儲存體作業是刪除檔案。 hello 下列程式碼會刪除名為 my-範例-檔案-3 儲存 hello 根目錄下的檔案。

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>設定 Azure 檔案共用的 hello 配額 （最大大小）
您可以設定檔案共用，以 gb 為單位的 hello 配額 （或最大值）。 您也可以檢查的 toosee 多少資料目前儲存在 hello 共用。

共用設定 hello 配額，您可以限制 hello 的 hello hello 共用上儲存的檔案大小總計。 如果 hello 的 hello 共用上的檔案大小總計超過 hello 配額設定為在 hello 共用，然後用戶端，將現有的檔案無法 tooincrease hello 大小或建立新的檔案，除非那些檔案是空的。

下列的 hello 範例示範如何 toocheck hello 共用所需的目前使用量以及如何 tooset hello hello 共用配額。

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>產生檔案或檔案共用的共用存取簽章
您可以為檔案共用或個別檔案產生共用存取簽章 (SAS)。 您也可以建立共用的存取原則在檔案共用 toomanage 共用存取簽章。 建立共用的存取原則被建議，因為它提供撤銷 hello SAS，如果它應該會受到危害的方法。

下列範例中的 hello 共用上，建立共用的存取原則，然後使用 原則 tooprovide hello 條件約束 SAS hello 中的檔案共用。

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a>後續步驟
進一步了解 Azure 儲存體，toolearn 瀏覽這些資源：

* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Azure 儲存體檔案服務的 C++ 範例] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure 儲存體總管](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)