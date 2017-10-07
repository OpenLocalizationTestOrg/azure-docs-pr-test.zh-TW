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
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="ed5d9-103">如何 toouse Ruby 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ed5d9-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="ed5d9-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ed5d9-104">Overview</span></span>
<span data-ttu-id="ed5d9-105">Azure Blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="ed5d9-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="ed5d9-107">Blob 儲存體也是參考的 tooas 物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="ed5d9-108">本指南說明您如何使用 Blob 儲存體 tooperform 常見案例。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="ed5d9-109">使用 hello Ruby 應用程式開發介面撰寫 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="ed5d9-110">hello 涵蓋案例包括**上傳、 列出、 下載**和**刪除**blob。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="ed5d9-111">建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="ed5d9-111">Create a Ruby application</span></span>
<span data-ttu-id="ed5d9-112">建立 Ruby 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-112">Create a Ruby application.</span></span> <span data-ttu-id="ed5d9-113">如需指示，請參閱 [Azure VM 上的 Ruby on Rails Web 應用程式](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="ed5d9-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="ed5d9-114">設定您的應用程式 tooaccess 儲存體</span><span class="sxs-lookup"><span data-stu-id="ed5d9-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="ed5d9-115">toouse Azure 儲存體，您需要 toodownload 和使用 hello 拼音 azure 的封裝，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="ed5d9-116">使用 RubyGems tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="ed5d9-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="ed5d9-117">使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="ed5d9-118">輸入健身安裝 azure 」 在 hello 命令視窗 tooinstall hello 健身和相依性。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="ed5d9-119">匯入 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="ed5d9-119">Import hello package</span></span>
<span data-ttu-id="ed5d9-120">使用慣用的文字編輯器，加入下列 toohello hello 拼音想 toouse 儲存體的檔案頂端的 hello:</span><span class="sxs-lookup"><span data-stu-id="ed5d9-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="ed5d9-121">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="ed5d9-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="ed5d9-122">hello azure 模組會讀取 hello 環境變數**AZURE\_儲存體\_帳戶**和**AZURE\_儲存體\_ACCESS_KEY**的tooconnect tooyour Azure 儲存體帳戶所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="ed5d9-123">如果未設定這些環境變數，您必須指定 hello 帳戶資訊，才能使用**Azure::Blob::BlobService**以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ed5d9-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="ed5d9-124">tooobtain hello Azure 入口網站中的帳戶從傳統或資源管理員儲存這些值：</span><span class="sxs-lookup"><span data-stu-id="ed5d9-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="ed5d9-125">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ed5d9-126">瀏覽您想 toouse toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="ed5d9-127">在 hello 設定 刀鋒視窗上 hello 右邊，按一下 **便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="ed5d9-128">在 hello 存取金鑰刀鋒視窗中出現，您會看到 hello 便捷鍵 1 和 2 的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="ed5d9-129">您可以使用其中一個存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-129">You can use either of these.</span></span>
5. <span data-ttu-id="ed5d9-130">按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="ed5d9-131">建立容器</span><span class="sxs-lookup"><span data-stu-id="ed5d9-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="ed5d9-132">hello **Azure::Blob::BlobService**物件可讓您使用容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-132">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="ed5d9-133">toocreate 容器，使用 hello**建立\_container()**方法。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-133">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="ed5d9-134">hello 下列程式碼範例會建立容器，或列印 hello 錯誤如果有的話。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-134">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="ed5d9-135">如果您想 toomake hello 容器中的 hello 檔案公用，您可以設定 hello 容器的權限。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-135">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="ed5d9-136">您可以只修改 hello<strong>建立\_container()</strong>呼叫 toopass hello **： 公用\_存取\_層級**選項：</span><span class="sxs-lookup"><span data-stu-id="ed5d9-136">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="ed5d9-137">有效的值為 hello **： 公用\_存取\_層級**選項：</span><span class="sxs-lookup"><span data-stu-id="ed5d9-137">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="ed5d9-138">**blob：** 指定 Blob 的公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="ed5d9-139">您可以透過匿名要求讀取此容器內的 Blob 資料，但您無法使用容器資料。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="ed5d9-140">用戶端無法列舉 hello 透過匿名要求的容器中的 blob。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-140">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="ed5d9-141">**container：**指定容器和 Blob 資料的完整公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="ed5d9-142">用戶端透過匿名要求，hello 容器內的 blob，但無法列舉 hello 儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-142">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="ed5d9-143">或者，您可以修改容器的 hello 公用存取層級使用**設定\_容器\_acl()**方法 toospecify hello 公用存取層級。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-143">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="ed5d9-144">下列程式碼範例變更太 hello 公用存取層級的 hello**容器**:</span><span class="sxs-lookup"><span data-stu-id="ed5d9-144">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ed5d9-145">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="ed5d9-145">Upload a blob into a container</span></span>
<span data-ttu-id="ed5d9-146">tooupload 內容 tooa blob、 使用 hello**建立\_區塊\_blob()**方法 toocreate hello blob，使用檔案或字串做為 hello 的 hello blob 的內容。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-146">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="ed5d9-147">hello 下列程式碼檔案上傳 hello **test.png**為名為 「 映像的 blob"hello 容器中的新 blob。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-147">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="ed5d9-148">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="ed5d9-148">List hello blobs in a container</span></span>
<span data-ttu-id="ed5d9-149">toolist hello 容器，使用**list_containers()**方法。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-149">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="ed5d9-150">toolist hello blob 容器內使用**清單\_blobs()**方法。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-150">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="ed5d9-151">這會輸出所有 hello blob hello 帳戶所有 hello 容器中的 hello url。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-151">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="ed5d9-152">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="ed5d9-152">Download blobs</span></span>
<span data-ttu-id="ed5d9-153">toodownload blob 使用 hello**取得\_blob()**方法 tooretrieve hello 內容。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-153">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="ed5d9-154">hello 下列程式碼範例示範如何使用**取得\_blob()** toodownload hello 」 映像 blob"的內容，並將它寫入 tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-154">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="ed5d9-155">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="ed5d9-155">Delete a Blob</span></span>
<span data-ttu-id="ed5d9-156">最後，toodelete blob，使用 hello**刪除\_blob()**方法。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-156">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="ed5d9-157">hello 下列程式碼範例示範如何 toodelete blob。</span><span class="sxs-lookup"><span data-stu-id="ed5d9-157">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="ed5d9-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed5d9-158">Next steps</span></span>
<span data-ttu-id="ed5d9-159">更複雜的存放工作需 toolearn 請追蹤下列連結：</span><span class="sxs-lookup"><span data-stu-id="ed5d9-159">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="ed5d9-160">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="ed5d9-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="ed5d9-161">GitHub 上的 [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) 儲存機制</span><span class="sxs-lookup"><span data-stu-id="ed5d9-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="ed5d9-162">使用 AzCopy 命令列公用程式的 hello 傳輸資料</span><span class="sxs-lookup"><span data-stu-id="ed5d9-162">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

