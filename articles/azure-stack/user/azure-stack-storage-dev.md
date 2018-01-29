---
title: "開始使用 Azure Stack 儲存體開發工具"
description: "開始使用 Azure Stack 儲存體開發工具的指引"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 9/25/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 5b2898c64c0f1b5d804e63fa4e4e1218fa7a672c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a>開始使用 Azure Stack 儲存體開發工具

適用於：Azure Stack 整合系統和 Azure Stack 開發套件


Microsoft Azure Stack 提供一組儲存體服務，包括 Azure Blob、資料表和佇列儲存體。

本文提供如何開始使用 Azure Stack 儲存體開發工具的快速指引。 您可以在對應的 Azure 儲存體教學課程中，找到更詳細的資訊和範例程式碼。

Azure 儲存體和 Azure Stack 儲存體之間有一些已知的差異，包括每個平台的一些特定需求。 例如，Azure Stack 有特定的用戶端程式庫以及特定的端點尾碼需求。 如需詳細資訊，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。

## <a name="azure-client-libraries"></a>Azure 用戶端程式庫
支援的 Azure Stack 儲存體 REST API 版本為 2015-04-05。 此版本異於最新版的 Azure 儲存體 REST API。 因此，針對儲存體用戶端程式庫，您需要知道與 REST API 2015-04-05 相容的版本。


|用戶端程式庫|Azure Stack 支援的版本|連結|端點規格|
|---------|---------|---------|---------|
|.NET     |6.2.0|Nuget 套件：<br>[https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br>GitHub 版本：<br>[https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|app.config 檔案|
|Java|4.1.0|Maven 套件：<br>[http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br>GitHub 版本：<br> [https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|連接字串設定|
|Node.js     |1.1.0|NPM 連結：<br>[https://www.npmjs.com/package/azure-storage](https://www.npmjs.com/package/azure-storage)<br>(執行：`npm install azure-storage@1.1.0)`<br><br>GitHub 版本：<br>[https://github.com/Azure/azure-storage-node/releases/tag/1.1.0](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|服務執行個體宣告||C++|2.4.0|Nuget 套件：<br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>GitHub 版本：<br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|連接字串設定|
|C++|2.4.0|Nuget 套件：<br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>GitHub 版本：<br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|連接字串設定|
|PHP|0.15.0|GitHub 版本：<br>[https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br>透過編輯器安裝 (請參閱下面的詳細資料)|連接字串設定|
|Python     |0.30.0|PIP 套件：<br> [https://pypi.python.org/pypi/azure-storage/0.30.0](https://pypi.python.org/pypi/azure-storage/0.30.0)<br>(執行：`pip install -v azure-storage==0.30.0)`<br><br>GitHub 版本：<br> [https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|服務執行個體宣告|
|Ruby|0.12.1<br>預覽|RubyGems 套件：<br> [https://rubygems.org/gems/azure-storage/versions/0.12.1.preview](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br>GitHub 版本：<br> [https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|連接字串設定|

> [!NOTE]
> PHP 詳細資料<br><br>
>透過編輯器安裝：
>1. 在專案的根目錄中，使用下列程式碼建立一個名為 `composer.json` 的檔案：<br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. 將 [composer.phar](http://getcomposer.org/composer.phar) 下載到專案根目錄中。
>3. 執行：`php composer.phar install`。
>


## <a name="endpoint-declaration"></a>端點宣告
Azure Stack 端點包含兩個部分：區域的名稱和 Azure Stack 網域。
在 Azure Stack 開發套件中，預設端點是 **local.azurestack.external**。
如果不確定您的端點，請連絡您的雲端系統管理員。

## <a name="examples"></a>範例


### <a name="net"></a>.NET

若是 Azure Stack，在 app.config 檔案中會指定端點尾碼：

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a>Java

若是 Azure Stack，在連接字串設定中會指定端點尾碼：

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a>Node.js

若是 Azure Stack，在宣告執行個體中會指定端點尾碼：

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a>C++

若是 Azure Stack，在連接字串設定中會指定端點尾碼：

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a>PHP

若是 Azure Stack，在連接字串設定中會指定端點尾碼：

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a>Python

若是 Azure Stack，在宣告執行個體中會指定端點尾碼：

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a>Ruby

若是 Azure Stack，在連接字串設定中會指定端點尾碼：

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a>Blob 儲存體

下列 Azure Blob 儲存體教學課程適用於 Azure Stack。 請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。

* [以 .NET 開始使用 Azure Blob 儲存體](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [如何使用 Java 的 Blob 儲存體](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [如何從 Node.js 使用 Blob 儲存體]../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [如何使用 C++ 的 Blob 儲存體](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [如何使用 PHP 的 Blob 儲存體](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [如何從 Python 使用 Azure Blob 儲存體](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [如何使用 Ruby 的 Blob 儲存體](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a>佇列儲存體

下列 Azure 佇列儲存體教學課程適用於 Azure Stack。 請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。

* [以 .NET 開始使用 Azure 佇列儲存體](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [如何使用 Java 的佇列儲存體](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [如何使用 Node.js 的佇列儲存體](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [如何使用 C++ 的佇列儲存體](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [如何使用 PHP 的佇列儲存體](../../storage/queues/storage-php-how-to-use-queues.md)
* [如何使用 Python 的佇列儲存體](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [如何使用 Ruby 的佇列儲存體](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a>表格儲存體

下列 Azure 資料表儲存體教學課程適用於 Azure Stack。 請注意先前[範例](#examples)一節中所述的 Azure Stack 特定端點尾碼需求。

* [以 .NET 開始使用 Azure 表格儲存體](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [如何使用 Java 的表格儲存體](../../cosmos-db/table-storage-how-to-use-java.md)
* [如何從 Node.js 使用 Azure 資料表儲存體](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [如何從 C++ 使用資料表儲存體](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [如何使用 PHP 的表格儲存體](../../cosmos-db/table-storage-how-to-use-php.md)
* [如何在 Python 中使用資料表儲存體](../../cosmos-db/table-storage-how-to-use-python.md)
* [如何使用 Ruby 的表格儲存體](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a>後續步驟

* [Microsoft Azure 儲存體簡介](../../storage/common/storage-introduction.md)