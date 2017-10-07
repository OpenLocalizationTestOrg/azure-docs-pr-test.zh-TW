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
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="b18bd-103">如何 toouse blob 來自 PHP 的儲存體</span><span class="sxs-lookup"><span data-stu-id="b18bd-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="b18bd-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b18bd-104">Overview</span></span>
<span data-ttu-id="b18bd-105">Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。</span><span class="sxs-lookup"><span data-stu-id="b18bd-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="b18bd-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="b18bd-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="b18bd-107">Blob 儲存體也是參考的 tooas 物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="b18bd-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="b18bd-108">本指南也說明如何 tooperform 常見的案例，使用 hello Azure blob 服務。</span><span class="sxs-lookup"><span data-stu-id="b18bd-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="b18bd-109">hello 範例以 PHP 撰寫和使用 hello [Azure SDK for PHP][download]。</span><span class="sxs-lookup"><span data-stu-id="b18bd-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="b18bd-110">hello 涵蓋案例包括**上載**，**列出**，**下載**，和**刪除**blob。</span><span class="sxs-lookup"><span data-stu-id="b18bd-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="b18bd-111">如需有關 blob 的詳細資訊，請參閱 hello[後續步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="b18bd-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="b18bd-112">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="b18bd-112">Create a PHP application</span></span>
<span data-ttu-id="b18bd-113">只有建立 PHP 應用程式存取 hello Azure blob 服務的需求為 hello hello 參考 hello Azure SDK 中的類別從 PHP 的程式碼內。</span><span class="sxs-lookup"><span data-stu-id="b18bd-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="b18bd-114">您可以使用任何開發工具 toocreate 您的應用程式，包括 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="b18bd-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="b18bd-115">在本指南中，您會使用可從 PHP 應用程式內本機呼叫的服務功能，或可在 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的服務功能。</span><span class="sxs-lookup"><span data-stu-id="b18bd-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="b18bd-116">取得 hello Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="b18bd-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="b18bd-117">設定您的應用程式 tooaccess hello 的 blob 服務</span><span class="sxs-lookup"><span data-stu-id="b18bd-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="b18bd-118">您需要 toouse hello Azure blob 服務 Api:</span><span class="sxs-lookup"><span data-stu-id="b18bd-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="b18bd-119">參考 hello 自動換片器檔案使用 hello [require_once]陳述式，並</span><span class="sxs-lookup"><span data-stu-id="b18bd-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="b18bd-120">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="b18bd-120">Reference any classes you might use.</span></span>

<span data-ttu-id="b18bd-121">hello 下列範例示範如何 tooinclude hello 自動換片器檔案和參考 hello **ServicesBuilder**類別。</span><span class="sxs-lookup"><span data-stu-id="b18bd-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="b18bd-122">本文中的 hello 範例假設您已安裝 hello Azure 透過編輯器的 PHP 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="b18bd-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="b18bd-123">如果您手動安裝 hello 程式庫，您需要 tooreference hello`WindowsAzure.php`自動換片器檔案。</span><span class="sxs-lookup"><span data-stu-id="b18bd-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="b18bd-124">在以下範例 hello，hello`require_once`陳述式會一律，不會顯示，但所需的 hello 範例 tooexecute 只有 hello 類別所參考。</span><span class="sxs-lookup"><span data-stu-id="b18bd-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="b18bd-125">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="b18bd-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="b18bd-126">tooinstantiate Azure blob 服務用戶端，您必須先取得有效的連接字串。</span><span class="sxs-lookup"><span data-stu-id="b18bd-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="b18bd-127">hello hello blob 服務的連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="b18bd-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="b18bd-128">用於存取即時服務：</span><span class="sxs-lookup"><span data-stu-id="b18bd-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="b18bd-129">用於存取 hello 儲存體模擬器：</span><span class="sxs-lookup"><span data-stu-id="b18bd-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="b18bd-130">toocreate 任何 Azure 服務用戶端，您需要 toouse hello **ServicesBuilder**類別。</span><span class="sxs-lookup"><span data-stu-id="b18bd-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="b18bd-131">您可以：</span><span class="sxs-lookup"><span data-stu-id="b18bd-131">You can:</span></span>

* <span data-ttu-id="b18bd-132">傳送嗨連接字串直接 tooit 或</span><span class="sxs-lookup"><span data-stu-id="b18bd-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="b18bd-133">使用 hello **CloudConfigurationManager (CCM)** toocheck hello 連接字串的多個外部來源：</span><span class="sxs-lookup"><span data-stu-id="b18bd-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="b18bd-134">預設已支援一種外部來源，即環境變數</span><span class="sxs-lookup"><span data-stu-id="b18bd-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="b18bd-135">您可以新增新的來源延伸 hello **ConnectionStringSource**類別。</span><span class="sxs-lookup"><span data-stu-id="b18bd-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="b18bd-136">如需此處所述的 hello 範例，將直接傳遞 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="b18bd-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="b18bd-137">建立容器</span><span class="sxs-lookup"><span data-stu-id="b18bd-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="b18bd-138">A **BlobRestProxy**物件可讓您建立 blob 容器以 hello **createContainer**方法。</span><span class="sxs-lookup"><span data-stu-id="b18bd-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="b18bd-139">建立容器時，您可以設定 hello 容器上的選項，但這麼做是不需要。</span><span class="sxs-lookup"><span data-stu-id="b18bd-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="b18bd-140">（hello 下面範例示範如何 tooset hello 容器存取控制清單 (ACL) 和容器中繼資料）。</span><span class="sxs-lookup"><span data-stu-id="b18bd-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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

<span data-ttu-id="b18bd-141">呼叫**setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOB)**讓 hello 可透過匿名要求存取的容器和 blob 資料。</span><span class="sxs-lookup"><span data-stu-id="b18bd-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="b18bd-142">呼叫 **setPublicAccess(PublicAccessType::BLOBS_ONLY)** 可讓 Blob 資料開放透過匿名要求來存取。</span><span class="sxs-lookup"><span data-stu-id="b18bd-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="b18bd-143">如需容器 ACL 的詳細資訊，請參閱[設定容器 ACL (REST API)][container-acl]。</span><span class="sxs-lookup"><span data-stu-id="b18bd-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="b18bd-144">如需 Blob 服務錯誤碼的詳細資訊，請參閱 [Blob 服務錯誤碼][error-codes]。</span><span class="sxs-lookup"><span data-stu-id="b18bd-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="b18bd-145">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="b18bd-145">Upload a blob into a container</span></span>
<span data-ttu-id="b18bd-146">將檔案當做 blob 時，使用 hello tooupload **BlobRestProxy]-> [createBlockBlob**方法。</span><span class="sxs-lookup"><span data-stu-id="b18bd-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="b18bd-147">如果它不存在，或覆寫它，如果是的話，這項作業會建立 hello blob。</span><span class="sxs-lookup"><span data-stu-id="b18bd-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="b18bd-148">hello 下列程式碼範例假設已經建立，並使用該 hello 容器[fopen] [ fopen] tooopen hello 檔案資料流的形式。</span><span class="sxs-lookup"><span data-stu-id="b18bd-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="b18bd-149">請注意，hello 前一個範例會將 blob 上傳做為資料流。</span><span class="sxs-lookup"><span data-stu-id="b18bd-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="b18bd-150">不過，blob 可以也可上傳為字串，例如，使用 hello[檔案\_取得\_內容][ file_get_contents]函式。</span><span class="sxs-lookup"><span data-stu-id="b18bd-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="b18bd-151">toodo 此使用 hello 先前的範例，變更`$content = fopen("c:\myfile.txt", "r");`太`$content = file_get_contents("c:\myfile.txt");`。</span><span class="sxs-lookup"><span data-stu-id="b18bd-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="b18bd-152">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="b18bd-152">List hello blobs in a container</span></span>
<span data-ttu-id="b18bd-153">toolist hello blob 容器中的使用 hello **BlobRestProxy]-> [listBlobs**方法**foreach**迴圈 tooloop 透過 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="b18bd-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="b18bd-154">hello 下列程式碼顯示的每個 blob 的 hello 名稱做為容器中的輸出並顯示其 URI toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="b18bd-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="b18bd-155">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="b18bd-155">Download a blob</span></span>
<span data-ttu-id="b18bd-156">toodownload blob，呼叫 hello **BlobRestProxy]-> [getBlob**方法，則呼叫 hello **getContentStream**方法 hello 產生**GetBlobResult**物件。</span><span class="sxs-lookup"><span data-stu-id="b18bd-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="b18bd-157">請注意，上述的 hello 範例取得 blob 做為資料流資源 （hello 預設行為）。</span><span class="sxs-lookup"><span data-stu-id="b18bd-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="b18bd-158">不過，您可以使用 hello[資料流\_取得\_內容][ stream-get-contents]函式 tooconvert hello 傳回資料流 tooa 字串。</span><span class="sxs-lookup"><span data-stu-id="b18bd-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="b18bd-159">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="b18bd-159">Delete a blob</span></span>
<span data-ttu-id="b18bd-160">toodelete blob，可傳遞 hello 容器名稱和 blob 名稱太**BlobRestProxy]-> [deleteBlob**。</span><span class="sxs-lookup"><span data-stu-id="b18bd-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="b18bd-161">刪除 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="b18bd-161">Delete a blob container</span></span>
<span data-ttu-id="b18bd-162">最後，toodelete blob 容器、 傳遞 hello 容器名稱太**BlobRestProxy]-> [deleteContainer**。</span><span class="sxs-lookup"><span data-stu-id="b18bd-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b18bd-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b18bd-163">Next steps</span></span>
<span data-ttu-id="b18bd-164">既然您已經學會 hello 的 hello Azure blob 服務的基本概念，請遵循這些連結 toolearn，更複雜的存放工作相關。</span><span class="sxs-lookup"><span data-stu-id="b18bd-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="b18bd-165">請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="b18bd-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="b18bd-166">請參閱 hello [PHP 區塊 blob 範例](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php)。</span><span class="sxs-lookup"><span data-stu-id="b18bd-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="b18bd-167">請參閱 hello [PHP 頁面 blob 範例](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php)。</span><span class="sxs-lookup"><span data-stu-id="b18bd-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="b18bd-168">使用 AzCopy 命令列公用程式的 hello 傳輸資料</span><span class="sxs-lookup"><span data-stu-id="b18bd-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="b18bd-169">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="b18bd-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
