---
title: "如何使用 PHP 的 Blob 儲存體 (物件儲存體) | Microsoft Docs"
description: "使用 Azure Blob 儲存體 (物件儲存體) 在雲端中儲存非結構化資料。"
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
ms.openlocfilehash: 2c356d7faafa8ef4591087b5b1f949b9374732be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="3ee53-103">如何使用 PHP 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="3ee53-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="3ee53-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3ee53-104">Overview</span></span>
<span data-ttu-id="3ee53-105">Azure Blob 儲存體是可將非結構化的資料儲存在雲端作為物件/blob 的服務。</span><span class="sxs-lookup"><span data-stu-id="3ee53-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="3ee53-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="3ee53-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="3ee53-107">Blob 儲存體也稱為物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="3ee53-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="3ee53-108">本指南會示範如何使用 Azure Blob 服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="3ee53-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="3ee53-109">這些範例均是以 PHP 撰寫，並使用 [Azure SDK for PHP][download]。</span><span class="sxs-lookup"><span data-stu-id="3ee53-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="3ee53-110">所涵蓋的案例包括**上傳**、**列出**、**下載**及**刪除** Blob。</span><span class="sxs-lookup"><span data-stu-id="3ee53-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="3ee53-111">如需 Blob 的詳細資訊，請參閱 [後續步驟](#next-steps) 一節。</span><span class="sxs-lookup"><span data-stu-id="3ee53-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="3ee53-112">建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="3ee53-112">Create a PHP application</span></span>
<span data-ttu-id="3ee53-113">若要建立 PHP 應用程式並使其存取 Azure Blob 服務，唯一要求就是在您的程式碼中參考 Azure SDK for PHP 中的類別。</span><span class="sxs-lookup"><span data-stu-id="3ee53-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="3ee53-114">您可以使用任何開發工具來建立應用程式 (包括 [記事本])。</span><span class="sxs-lookup"><span data-stu-id="3ee53-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="3ee53-115">在本指南中，您會使用可從 PHP 應用程式內本機呼叫的服務功能，或可在 Azure Web 角色、背景工作角色或網站內執行的程式碼中呼叫的服務功能。</span><span class="sxs-lookup"><span data-stu-id="3ee53-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="3ee53-116">取得 Azure 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="3ee53-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="3ee53-117">設定您的應用程式以存取 Blob 服務</span><span class="sxs-lookup"><span data-stu-id="3ee53-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="3ee53-118">若要使用 Azure Blob 服務 API，您必須：</span><span class="sxs-lookup"><span data-stu-id="3ee53-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="3ee53-119">參考使用 [require_once] 陳述式的自動載入器檔案，以及</span><span class="sxs-lookup"><span data-stu-id="3ee53-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="3ee53-120">參考任何您可能使用的類別。</span><span class="sxs-lookup"><span data-stu-id="3ee53-120">Reference any classes you might use.</span></span>

<span data-ttu-id="3ee53-121">下列範例顯示如何納入自動載入器檔案及參考 **ServicesBuilder** 類別。</span><span class="sxs-lookup"><span data-stu-id="3ee53-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="3ee53-122">本文中的範例假設您已透過 Composer 安裝 PHP Client Libraries for Azure。</span><span class="sxs-lookup"><span data-stu-id="3ee53-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="3ee53-123">如果您是以手動方式安裝程式庫，則必須參考 `WindowsAzure.php` 自動載入器檔案。</span><span class="sxs-lookup"><span data-stu-id="3ee53-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="3ee53-124">在下列各範例中，一律會顯示 `require_once` 陳述式，但只會參考要執行之範例所需的類別。</span><span class="sxs-lookup"><span data-stu-id="3ee53-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="3ee53-125">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="3ee53-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="3ee53-126">若要具現化 Azure Blob 服務用戶端，您必須具備有效的連接字串。</span><span class="sxs-lookup"><span data-stu-id="3ee53-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="3ee53-127">Blob 服務的連接字串格式為：</span><span class="sxs-lookup"><span data-stu-id="3ee53-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="3ee53-128">用於存取即時服務：</span><span class="sxs-lookup"><span data-stu-id="3ee53-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="3ee53-129">用於存取儲存體模擬器：</span><span class="sxs-lookup"><span data-stu-id="3ee53-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="3ee53-130">若要建立任何 Azure 服務用戶端，您必須使用 **ServicesBuilder** 類別。</span><span class="sxs-lookup"><span data-stu-id="3ee53-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="3ee53-131">您可以：</span><span class="sxs-lookup"><span data-stu-id="3ee53-131">You can:</span></span>

* <span data-ttu-id="3ee53-132">直接將連接字串傳遞給它，或</span><span class="sxs-lookup"><span data-stu-id="3ee53-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="3ee53-133">使用 **CloudConfigurationManager (CCM)** 到多種外部來源檢查連接字串：</span><span class="sxs-lookup"><span data-stu-id="3ee53-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="3ee53-134">預設已支援一種外部來源，即環境變數</span><span class="sxs-lookup"><span data-stu-id="3ee53-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="3ee53-135">您可以擴充 **ConnectionStringSource** 類別以加入新來源。</span><span class="sxs-lookup"><span data-stu-id="3ee53-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="3ee53-136">在本文的各範例中，將會直接傳遞連接字串。</span><span class="sxs-lookup"><span data-stu-id="3ee53-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="3ee53-137">建立容器</span><span class="sxs-lookup"><span data-stu-id="3ee53-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="3ee53-138">**BlobRestProxy** 物件可讓您使用 **createContainer** 方法建立 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="3ee53-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="3ee53-139">建立容器時，您可以在容器上設定選項，但這並非必要動作。</span><span class="sxs-lookup"><span data-stu-id="3ee53-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="3ee53-140">(下列範例顯示如何設定容器存取控制清單 (ACL) 和容器中繼資料)。</span><span class="sxs-lookup"><span data-stu-id="3ee53-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
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

<span data-ttu-id="3ee53-141">呼叫 **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** 可讓容器和 Blob 資料開放透過匿名要求來存取。</span><span class="sxs-lookup"><span data-stu-id="3ee53-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="3ee53-142">呼叫 **setPublicAccess(PublicAccessType::BLOBS_ONLY)** 可讓 Blob 資料開放透過匿名要求來存取。</span><span class="sxs-lookup"><span data-stu-id="3ee53-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="3ee53-143">如需容器 ACL 的詳細資訊，請參閱[設定容器 ACL (REST API)][container-acl]。</span><span class="sxs-lookup"><span data-stu-id="3ee53-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="3ee53-144">如需 Blob 服務錯誤碼的詳細資訊，請參閱 [Blob 服務錯誤碼][error-codes]。</span><span class="sxs-lookup"><span data-stu-id="3ee53-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="3ee53-145">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="3ee53-145">Upload a blob into a container</span></span>
<span data-ttu-id="3ee53-146">若要將檔案當作 Blob 上傳，請使用 **BlobRestProxy->createBlockBlob** 方法。</span><span class="sxs-lookup"><span data-stu-id="3ee53-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="3ee53-147">如果 Blob 不存在，此作業會予以建立，若已存在，則予以覆寫。</span><span class="sxs-lookup"><span data-stu-id="3ee53-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="3ee53-148">下列程式碼範例假設已建立容器，並使用 [fopen][fopen] 將檔案當作串流開啟。</span><span class="sxs-lookup"><span data-stu-id="3ee53-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

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

<span data-ttu-id="3ee53-149">請注意，前述範例會以串流方式上傳 Blob。</span><span class="sxs-lookup"><span data-stu-id="3ee53-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="3ee53-150">不過，也可以使用 [file\_get\_contents][file_get_contents] 之類的函式將 Blob 當作字串上傳。</span><span class="sxs-lookup"><span data-stu-id="3ee53-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="3ee53-151">若要使用前述範例執行這項操作，請將 `$content = fopen("c:\myfile.txt", "r");` 變更為 `$content = file_get_contents("c:\myfile.txt");`。</span><span class="sxs-lookup"><span data-stu-id="3ee53-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="3ee53-152">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="3ee53-152">List the blobs in a container</span></span>
<span data-ttu-id="3ee53-153">若要列出容器中的 Blob，請搭配使用 **BlobRestProxy->listBlobs** 方法與 **foreach** 迴圈，對結果進行迴圈。</span><span class="sxs-lookup"><span data-stu-id="3ee53-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="3ee53-154">下列程式碼會將容器中每個 Blob 的名稱作為輸出顯示，並將 URI 顯示於瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="3ee53-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="3ee53-155">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="3ee53-155">Download a blob</span></span>
<span data-ttu-id="3ee53-156">若要下載 Blob，請呼叫 **BlobRestProxy->getBlob** 方法，然後在結果產生的 **GetBlobResult** 物件上呼叫 **getContentStream** 方法。</span><span class="sxs-lookup"><span data-stu-id="3ee53-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="3ee53-157">請注意，以上範例會以串流資源形式 (預設行為) 取得 Blob。</span><span class="sxs-lookup"><span data-stu-id="3ee53-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="3ee53-158">不過，您可以使用 [stream\_get\_contents][stream-get-contents] 函式將傳回的串流轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="3ee53-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="3ee53-159">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="3ee53-159">Delete a blob</span></span>
<span data-ttu-id="3ee53-160">若要刪除 Blob，請將容器名稱和 Blob 名稱傳遞至 **BlobRestProxy->deleteBlob**。</span><span class="sxs-lookup"><span data-stu-id="3ee53-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="3ee53-161">刪除 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="3ee53-161">Delete a blob container</span></span>
<span data-ttu-id="3ee53-162">最後，若要刪除 Blob 容器，請將容器名稱傳遞至 **BlobRestProxy->deleteContainer**。</span><span class="sxs-lookup"><span data-stu-id="3ee53-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3ee53-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ee53-163">Next steps</span></span>
<span data-ttu-id="3ee53-164">了解 Azure Blob 服務的基礎概念之後，請參考下列連結以深入了解更複雜的儲存工作。</span><span class="sxs-lookup"><span data-stu-id="3ee53-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="3ee53-165">造訪 [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="3ee53-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="3ee53-166">請參閱 [PHP 區塊 Blob 範例](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php)。</span><span class="sxs-lookup"><span data-stu-id="3ee53-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="3ee53-167">請參閱 [PHP 分頁 Blob 範例](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php)。</span><span class="sxs-lookup"><span data-stu-id="3ee53-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="3ee53-168">使用 AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="3ee53-168">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="3ee53-169">如需詳細資訊，另請參閱 [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="3ee53-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
<span data-ttu-id="3ee53-170">[require_once]: http://php.net/require_once</span><span class="sxs-lookup"><span data-stu-id="3ee53-170">[require_once]: http://php.net/require_once</span></span>
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
