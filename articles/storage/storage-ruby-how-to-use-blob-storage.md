---
title: "如何使用拼音的 Blob 儲存體 (物件儲存體) | Microsoft Docs"
description: "使用 Azure Blob 儲存體 (物件儲存體) 在雲端中儲存非結構化資料。"
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
ms.openlocfilehash: 7f7d0c52b2b50a360711477e8e0eafc07ddcf374
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="482d8-103">如何使用 Ruby 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="482d8-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="482d8-104">概觀</span><span class="sxs-lookup"><span data-stu-id="482d8-104">Overview</span></span>
<span data-ttu-id="482d8-105">Azure Blob 儲存體是可將非結構化的資料儲存在雲端作為物件/blob 的服務。</span><span class="sxs-lookup"><span data-stu-id="482d8-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="482d8-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="482d8-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="482d8-107">Blob 儲存體也稱為物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="482d8-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="482d8-108">本指南將示範如何使用 Blob 儲存體執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="482d8-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="482d8-109">這些範例使用 Ruby API 撰寫。</span><span class="sxs-lookup"><span data-stu-id="482d8-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="482d8-110">所涵蓋的案例包括「上傳、列出、下載」及「刪除」Blob。</span><span class="sxs-lookup"><span data-stu-id="482d8-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="482d8-111">建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="482d8-111">Create a Ruby application</span></span>
<span data-ttu-id="482d8-112">建立 Ruby 應用程式。</span><span class="sxs-lookup"><span data-stu-id="482d8-112">Create a Ruby application.</span></span> <span data-ttu-id="482d8-113">如需指示，請參閱 [Azure VM 上的 Ruby on Rails Web 應用程式](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="482d8-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="482d8-114">設定您的應用程式以存取儲存體</span><span class="sxs-lookup"><span data-stu-id="482d8-114">Configure your application to access Storage</span></span>
<span data-ttu-id="482d8-115">若要使用 Azure 儲存體，您需要下載並使用 Ruby azure 套件，這包含一組便利程式庫，能與儲存體 REST 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="482d8-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="482d8-116">使用 RubyGems 來取得套件</span><span class="sxs-lookup"><span data-stu-id="482d8-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="482d8-117">使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。</span><span class="sxs-lookup"><span data-stu-id="482d8-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="482d8-118">在命令視窗中鍵入 "gem install azure" 以安裝 Gem 和相依性。</span><span class="sxs-lookup"><span data-stu-id="482d8-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="482d8-119">匯入套件</span><span class="sxs-lookup"><span data-stu-id="482d8-119">Import the package</span></span>
<span data-ttu-id="482d8-120">使用您偏好的文字編輯器，將以下內容新增至您打算使用儲存體的 Ruby 檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="482d8-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="482d8-121">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="482d8-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="482d8-122">azure 模組會讀取環境變數 **AZURE\_STORAGE\_ACCOUNT** 及 **AZURE\_STORAGE\_ACCESS_KEY**，以取得連接 Azure 儲存體帳戶所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="482d8-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="482d8-123">如果尚未設定這些環境變數，您必須下列程式碼中使用 **Azure::Blob::BlobService** 前指定帳戶資訊：</span><span class="sxs-lookup"><span data-stu-id="482d8-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="482d8-124">若要從 Azure 入口網站中的傳統或 Resource Manager 儲存體帳戶取得這些值：</span><span class="sxs-lookup"><span data-stu-id="482d8-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="482d8-125">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="482d8-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="482d8-126">瀏覽到您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="482d8-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="482d8-127">在右邊的 [設定] 刀鋒視窗中，按一下 [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="482d8-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="482d8-128">[存取金鑰] 刀鋒視窗隨即顯示，您會看到存取金鑰 1 和存取金鑰 2。</span><span class="sxs-lookup"><span data-stu-id="482d8-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="482d8-129">您可以使用其中一個存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="482d8-129">You can use either of these.</span></span>
5. <span data-ttu-id="482d8-130">按一下複製圖示以將金鑰複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="482d8-130">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="482d8-131">若要從 Azure 入口網站的傳統儲存體帳戶取得這些值：</span><span class="sxs-lookup"><span data-stu-id="482d8-131">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="482d8-132">登入傳統 [Azure 入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="482d8-132">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="482d8-133">瀏覽到您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="482d8-133">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="482d8-134">按一下導覽窗格底部的 [管理存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="482d8-134">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="482d8-135">在快顯對話方塊中，您將會看到儲存體帳戶名稱、主要存取金鑰和次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="482d8-135">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="482d8-136">如需存取金鑰，您可以使用主要存取金鑰或次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="482d8-136">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="482d8-137">按一下複製圖示以將金鑰複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="482d8-137">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="482d8-138">建立容器</span><span class="sxs-lookup"><span data-stu-id="482d8-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="482d8-139">**Azure::Blob::BlobService** 物件可讓您運用容器及 Blob。</span><span class="sxs-lookup"><span data-stu-id="482d8-139">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="482d8-140">若要建立容器，請使用 **create\_container()** 方法。</span><span class="sxs-lookup"><span data-stu-id="482d8-140">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="482d8-141">下列程式碼範例會建立容器或列印錯誤訊息 (若有的話)。</span><span class="sxs-lookup"><span data-stu-id="482d8-141">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="482d8-142">如果您想讓容器中的檔案成為公用性質，可以設定容器的權限。</span><span class="sxs-lookup"><span data-stu-id="482d8-142">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="482d8-143">您可以只修改 <strong>create\_container()</strong> 呼叫以傳遞 **:public\_access\_level** 選項：</span><span class="sxs-lookup"><span data-stu-id="482d8-143">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="482d8-144">**:public\_access\_level** 選項的有效值包括：</span><span class="sxs-lookup"><span data-stu-id="482d8-144">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="482d8-145">**blob：** 指定 Blob 的公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="482d8-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="482d8-146">您可以透過匿名要求讀取此容器內的 Blob 資料，但您無法使用容器資料。</span><span class="sxs-lookup"><span data-stu-id="482d8-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="482d8-147">用戶端無法透過匿名要求列舉容器內的 Blob。</span><span class="sxs-lookup"><span data-stu-id="482d8-147">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="482d8-148">**container：**指定容器和 Blob 資料的完整公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="482d8-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="482d8-149">用戶端可以透過匿名要求列舉容器內的 Blob，但無法列舉儲存體帳戶內的容器。</span><span class="sxs-lookup"><span data-stu-id="482d8-149">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="482d8-150">或者，您可以使用 **set\_container\_acl()** 方法指定公用存取等級，藉此修改容器的公用存取等級。</span><span class="sxs-lookup"><span data-stu-id="482d8-150">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="482d8-151">下列程式碼範例會將公用存取等級變更為 **容器**：</span><span class="sxs-lookup"><span data-stu-id="482d8-151">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="482d8-152">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="482d8-152">Upload a blob into a container</span></span>
<span data-ttu-id="482d8-153">若要將內容上傳至 Blob，請使用 **create\_block\_blob()** 方法建立 Blob，使用檔案或字串作為 Blob 的內容。</span><span class="sxs-lookup"><span data-stu-id="482d8-153">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="482d8-154">下列程式碼將上傳檔案 **test.png** 做為容器中的新 Blob (名為 "image-blob")。</span><span class="sxs-lookup"><span data-stu-id="482d8-154">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="482d8-155">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="482d8-155">List the blobs in a container</span></span>
<span data-ttu-id="482d8-156">若要列出容器，請使用 **list_containers()** 方法。</span><span class="sxs-lookup"><span data-stu-id="482d8-156">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="482d8-157">若要列出容器內的 Blob，請使用 **list\_blobs()** 方法。</span><span class="sxs-lookup"><span data-stu-id="482d8-157">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="482d8-158">這會輸出該帳戶所有容器中所有 Blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="482d8-158">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="482d8-159">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="482d8-159">Download blobs</span></span>
<span data-ttu-id="482d8-160">若要下載 Blob，請使用 **get\_blob()** 方法以擷取內容。</span><span class="sxs-lookup"><span data-stu-id="482d8-160">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="482d8-161">下列程式碼範例示範使用 **get\_blob()** 來下載 "image-blob" 的內容，並將它寫入本機檔案。</span><span class="sxs-lookup"><span data-stu-id="482d8-161">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="482d8-162">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="482d8-162">Delete a Blob</span></span>
<span data-ttu-id="482d8-163">最後，若要刪除 Blob，請使用 **delete\_blob()** 方法。</span><span class="sxs-lookup"><span data-stu-id="482d8-163">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="482d8-164">下列程式碼範例示範如何刪除 Blob。</span><span class="sxs-lookup"><span data-stu-id="482d8-164">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="482d8-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="482d8-165">Next steps</span></span>
<span data-ttu-id="482d8-166">請遵循下列連結以深入了解更複雜的儲存體工作：</span><span class="sxs-lookup"><span data-stu-id="482d8-166">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="482d8-167">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="482d8-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="482d8-168">GitHub 上的 [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) 儲存機制</span><span class="sxs-lookup"><span data-stu-id="482d8-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="482d8-169">使用 AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="482d8-169">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

