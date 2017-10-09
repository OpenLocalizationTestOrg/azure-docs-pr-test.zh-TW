---
title: "aaaGet 開始使用 Azure 堆疊儲存體程式開發工具"
description: "開始使用 Azure 堆疊儲存體程式開發工具的指引 tooget"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 7/21/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 0756ed1b9fad4aed0cca4cfd719ef3334dec6700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a>開始使用 Azure Stack 儲存體開發工具 

Microsoft Azure Stack 提供一組儲存體服務，包括 Azure Blob、資料表和佇列儲存體。

這篇文章提供如何快速指南 toostart 使用 Azure 堆疊儲存體程式開發工具。 Hello 對應 Azure 儲存體教學課程中，您可以找到更多詳細的資訊和範例程式碼。

Azure 儲存體和 Azure Stack 儲存體之間有一些已知的差異，包括每個平台的一些特定需求。 例如，Azure Stack 有特定的用戶端程式庫以及特定的端點尾碼需求。 如需詳細資訊，請參閱 [Azure Stack 儲存體：差異與注意事項](azure-stack-acs-differences.md)。

## <a name="azure-client-libraries"></a>Azure 用戶端程式庫
Azure 堆疊儲存體的 hello 支援 REST API 版本為 2015年-04-05。 沒有完整的同位檢查與 hello hello Azure 儲存體的 REST API 最新版本。 因此 hello 儲存體用戶端程式庫，您需要 toobe 留意 hello 版本相容的 REST API 2015-04-05。


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
>透過編輯器 tooinstall:
>1. 建立名為`composer.json`hello hello 與下列程式碼的專案根目錄中：<br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. 下載[composer.phar](http://getcomposer.org/composer.phar)至 hello 專案根目錄。
>3. 執行：`php composer.phar install`。
>


## <a name="endpoint-declaration"></a>端點宣告
Azure 堆疊端點包含兩個部分： hello 地區和 hello Azure 堆疊網域名稱。
在 hello Azure 堆疊開發套件，是 hello 預設端點**local.azurestack.external**。
如果不確定您的端點，請連絡您的雲端系統管理員。

## <a name="examples"></a>範例


### <a name="net"></a>.NET

針對 Azure 堆疊 hello 端點尾碼會指定在 hello app.config 檔案中：

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a>Java

針對 Azure 堆疊 hello 端點尾碼會指定在 hello 安裝程式的連接字串中：

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a>Node.js

針對 Azure 堆疊 hello 端點尾碼會指定在 hello 宣告執行個體：

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a>C++

針對 Azure 堆疊 hello 端點尾碼會指定在 hello 安裝程式的連接字串中：

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a>PHP

針對 Azure 堆疊 hello 端點尾碼會指定在 hello 安裝程式的連接字串中：

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a>Python

針對 Azure 堆疊 hello 端點尾碼會指定在 hello 宣告執行個體：

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a>Ruby

針對 Azure 堆疊 hello 端點尾碼會指定在 hello 安裝程式的連接字串中：

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a>Blob 儲存體

hello 下列 Azure Blob 儲存體教學課程，適用 tooAzure 堆疊。 請注意 hello 特定端點尾碼需求 hello 先前所述的 Azure 堆疊[範例](#examples)> 一節。

* [以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [如何從 Java 的 Blob 儲存體 toouse](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [如何 toouse Node.js 從 Blob 儲存體](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [如何 toouse 從 c + + 的 Blob 儲存體](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [如何 toouse 來自 PHP 的 Blob 儲存體](../storage/blobs/storage-php-how-to-use-blobs.md)
* [如何 toouse 來自 Python 的 Azure Blob 儲存體](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [如何 toouse Ruby 從 Blob 儲存體](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a>佇列儲存體

hello 下列 Azure 佇列儲存體教學課程，適用 tooAzure 堆疊。 請注意 hello 特定端點尾碼需求 hello 先前所述的 Azure 堆疊[範例](#examples)> 一節。

* [以 .NET 開始使用 Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [如何從 Java 佇列儲存體 toouse](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [如何 toouse 從 Node.js 佇列儲存體](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [如何 toouse 佇列儲存體從 c + +](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [如何 toouse 來自 PHP 的佇列儲存體](../storage/queues/storage-php-how-to-use-queues.md)
* [如何 toouse 來自 Python 的佇列儲存體](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [如何 toouse Ruby 從佇列儲存體](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a>表格儲存體

hello 下列 Azure 資料表儲存體教學課程，適用 tooAzure 堆疊。 請注意 hello 特定端點尾碼需求 hello 先前所述的 Azure 堆疊[範例](#examples)> 一節。

* [以 .NET 開始使用 Azure 表格儲存體](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [如何從 Java 資料表儲存體 toouse](../cosmos-db/table-storage-how-to-use-java.md)
* [如何 toouse 從 Node.js 的 Azure 資料表儲存體](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [如何 toouse 從 c + + 的資料表儲存體](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [如何 toouse 來自 PHP 的資料表儲存體](../cosmos-db/table-storage-how-to-use-php.md)
* [如何 toouse Python 的表格儲存體](../cosmos-db/table-storage-how-to-use-python.md)
* [如何 toouse Ruby 從資料表儲存體](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a>後續步驟

* [簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)
