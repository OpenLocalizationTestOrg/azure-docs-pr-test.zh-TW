---
title: "aaaHow toouse blob 儲存體 （物件儲存體） 從 PHP |Microsoft 文件"
description: "使用 Azure Blob 儲存體 （物件儲存體） 的 hello 雲端中儲存非結構化的資料。"
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a>如何 toouse blob 來自 PHP 的儲存體
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀
Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。 Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 Blob 儲存體也是參考的 tooas 物件儲存體。

本指南也說明如何 tooperform 常見的案例，使用 hello Azure blob 服務。 hello 範例以 PHP 撰寫和使用 hello [Azure SDK for PHP][download]。 hello 涵蓋案例包括**上載**，**列出**，**下載**，和**刪除**blob。 如需有關 blob 的詳細資訊，請參閱 hello[後續步驟](#next-steps)> 一節。

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>建立 PHP 應用程式
只有建立 PHP 應用程式存取 hello Azure blob 服務的需求為 hello hello 參考 hello Azure SDK 中的類別從 PHP 的程式碼內。 您可以使用任何開發工具 toocreate 您的應用程式，包括 [記事本]。

在本指南中，您會使用可從 PHP 應用程式內本機呼叫的服務功能，或可在 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的服務功能。

## <a name="get-hello-azure-client-libraries"></a>取得 hello Azure 用戶端程式庫
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>設定您的應用程式 tooaccess hello 的 blob 服務
您需要 toouse hello Azure blob 服務 Api:

1. 參考 hello 自動換片器檔案使用 hello [require_once]陳述式，並
2. 參考任何您可能使用的類別。

hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello **ServicesBuilder**類別。

> [!NOTE]
> 本文中的 hello 範例假設您已安裝 hello Azure 透過編輯器的 PHP 用戶端程式庫。 如果您手動安裝 hello 程式庫，您需要 tooreference hello`WindowsAzure.php`自動換片器檔案。
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

在以下範例 hello，hello`require_once`陳述式會一律，不會顯示，但所需的 hello 範例 tooexecute 只有 hello 類別所參考。

## <a name="set-up-an-azure-storage-connection"></a>設定 Azure 儲存體連接
tooinstantiate Azure blob 服務用戶端，您必須先取得有效的連接字串。 hello hello blob 服務的連接字串的格式如下：

用於存取即時服務：

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

用於存取 hello 儲存體模擬器：

```php
UseDevelopmentStorage=true
```

toocreate 任何 Azure 服務用戶端，您需要 toouse hello **ServicesBuilder**類別。 您可以：

* 傳送嗨連接字串直接 tooit 或
* 使用 hello **CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：
  * 預設已支援一種外部來源，即環境變數
  * 您可以新增新的來源延伸 hello **ConnectionStringSource**類別。

如需此處所述的 hello 範例，將直接傳遞 hello 連接字串。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>建立容器
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

A **BlobRestProxy**物件可讓您建立 blob 容器以 hello **createContainer**方法。 建立容器時，您可以設定 hello 容器上的選項，但這麼做是不需要。 （hello 下面範例示範如何 tooset hello 容器存取控制清單 (ACL) 和容器中繼資料）。

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

呼叫**setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOB)**讓 hello 可透過匿名要求存取的容器和 blob 資料。 呼叫 **setPublicAccess(PublicAccessType::BLOBS_ONLY)** 可讓 Blob 資料開放透過匿名要求來存取。 如需容器 ACL 的詳細資訊，請參閱[設定容器 ACL (REST API)][container-acl]。

如需 Blob 服務錯誤碼的詳細資訊，請參閱 [Blob 服務錯誤碼][error-codes]。

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
將檔案當做 blob 時，使用 hello tooupload **BlobRestProxy]-> [createBlockBlob**方法。 如果它不存在，或覆寫它，如果是的話，這項作業會建立 hello blob。 hello 下列程式碼範例假設已經建立，並使用該 hello 容器[fopen] [ fopen] tooopen hello 檔案資料流的形式。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

請注意，hello 前一個範例會將 blob 上傳做為資料流。 不過，blob 可以也可上傳為字串，例如，使用 hello[檔案\_取得\_內容][ file_get_contents]函式。 toodo 此使用 hello 先前的範例，變更`$content = fopen("c:\myfile.txt", "r");`太`$content = file_get_contents("c:\myfile.txt");`。

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
toolist hello blob 容器中的使用 hello **BlobRestProxy]-> [listBlobs**方法**foreach**迴圈 tooloop 透過 hello 結果。 hello 下列程式碼顯示的每個 blob 的 hello 名稱做為容器中的輸出並顯示其 URI toohello 瀏覽器。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a>下載 Blob
toodownload blob，呼叫 hello **BlobRestProxy]-> [getBlob**方法，則呼叫 hello **getContentStream**方法 hello 產生**GetBlobResult**物件。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

請注意，上述的 hello 範例取得 blob 做為資料流資源 （hello 預設行為）。 不過，您可以使用 hello[資料流\_取得\_內容][ stream-get-contents]函式 tooconvert hello 傳回資料流 tooa 字串。

## <a name="delete-a-blob"></a>刪除 Blob
toodelete blob，可傳遞 hello 容器名稱和 blob 名稱太**BlobRestProxy]-> [deleteBlob**。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a>刪除 Blob 容器
最後，toodelete blob 容器、 傳遞 hello 容器名稱太**BlobRestProxy]-> [deleteContainer**。

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>後續步驟
既然您已經學會 hello 的 hello Azure blob 服務的基本概念，請遵循這些連結 toolearn，更複雜的存放工作相關。

* 請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)
* 請參閱 hello [PHP 區塊 blob 範例](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php)。
* 請參閱 hello [PHP 頁面 blob 範例](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php)。
* [使用 AzCopy 命令列公用程式的 hello 傳輸資料](storage-use-azcopy.md)

如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
