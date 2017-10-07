---
title: "aaaHow toouse Ruby 從佇列儲存體 |Microsoft 文件"
description: "了解 toouse hello Azure 佇列服務 toocreate 和刪除佇列，以及插入、 取得，並刪除訊息。 範例以 Ruby 撰寫。"
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c8eacac058442419cb9e8fe62cb69ad7ef1e2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="647f6-104">如何 toouse Ruby 從佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="647f6-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="647f6-105">概觀</span><span class="sxs-lookup"><span data-stu-id="647f6-105">Overview</span></span>
<span data-ttu-id="647f6-106">本指南也說明如何使用 tooperform 常見案例 hello Microsoft Azure 佇列儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="647f6-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="647f6-107">使用 hello Ruby Azure 應用程式開發介面撰寫 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="647f6-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="647f6-108">hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立及刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="647f6-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="647f6-109">建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="647f6-109">Create a Ruby Application</span></span>
<span data-ttu-id="647f6-110">建立 Ruby 應用程式。</span><span class="sxs-lookup"><span data-stu-id="647f6-110">Create a Ruby application.</span></span> <span data-ttu-id="647f6-111">如需指示，請參閱 [Azure VM 上的 Ruby on Rails Web 應用程式](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="647f6-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="647f6-112">設定您的應用程式 tooAccess 儲存體</span><span class="sxs-lookup"><span data-stu-id="647f6-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="647f6-113">toouse Azure 儲存體，您需要 toodownload 和使用 hello 拼音 azure 的封裝，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。</span><span class="sxs-lookup"><span data-stu-id="647f6-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="647f6-114">使用 RubyGems tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="647f6-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="647f6-115">使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。</span><span class="sxs-lookup"><span data-stu-id="647f6-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="647f6-116">輸入健身安裝 azure 」 在 hello 命令視窗 tooinstall hello 健身和相依性。</span><span class="sxs-lookup"><span data-stu-id="647f6-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="647f6-117">匯入 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="647f6-117">Import hello package</span></span>
<span data-ttu-id="647f6-118">使用您慣用的文字編輯器，請新增下列 toohello hello 拼音想 toouse 儲存體的檔案頂端的 hello:</span><span class="sxs-lookup"><span data-stu-id="647f6-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="647f6-119">設定 Azure 儲存體連接</span><span class="sxs-lookup"><span data-stu-id="647f6-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="647f6-120">hello azure 模組會讀取 hello 環境變數**AZURE\_儲存體\_帳戶**和**AZURE\_儲存體\_ACCESS_KEY**的tooconnect tooyour Azure 儲存體帳戶所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="647f6-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="647f6-121">如果未設定這些環境變數，您必須指定 hello 帳戶資訊，才能使用**Azure::QueueService**以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="647f6-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="647f6-122">tooobtain hello Azure 入口網站中的帳戶從傳統或資源管理員儲存這些值：</span><span class="sxs-lookup"><span data-stu-id="647f6-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="647f6-123">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="647f6-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="647f6-124">瀏覽您想 toouse toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="647f6-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="647f6-125">在 hello 設定 刀鋒視窗上 hello 右邊，按一下 **便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="647f6-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="647f6-126">在 hello 存取金鑰刀鋒視窗中出現，您會看到 hello 便捷鍵 1 和 2 的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="647f6-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="647f6-127">您可以使用其中一個存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="647f6-127">You can use either of these.</span></span> 
5. <span data-ttu-id="647f6-128">按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="647f6-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

## <a name="how-to-create-a-queue"></a><span data-ttu-id="647f6-129">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="647f6-129">How To: Create a Queue</span></span>
<span data-ttu-id="647f6-130">hello 下列程式碼會建立**Azure::QueueService**物件，可讓您與佇列搭配 toowork。</span><span class="sxs-lookup"><span data-stu-id="647f6-130">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="647f6-131">使用 hello **create_queue()**方法 toocreate hello 的佇列指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="647f6-131">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="647f6-132">作法：將訊息插入佇列中</span><span class="sxs-lookup"><span data-stu-id="647f6-132">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="647f6-133">將訊息插入佇列中，使用 hello tooinsert **create_message()**方法 toocreate 新訊息並將它加入 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="647f6-133">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="647f6-134">如何： 檢視 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="647f6-134">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="647f6-135">您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello**查看\_messages()**方法。</span><span class="sxs-lookup"><span data-stu-id="647f6-135">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="647f6-136">**peek\_messages()** 預設會查看單一訊息。</span><span class="sxs-lookup"><span data-stu-id="647f6-136">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="647f6-137">您也可以指定多少訊息想 toopeek。</span><span class="sxs-lookup"><span data-stu-id="647f6-137">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="647f6-138">如何： 清除佇列 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="647f6-138">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="647f6-139">您可以使用兩個步驟將訊息從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="647f6-139">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="647f6-140">當您呼叫**清單\_messages()**，預設會取得 hello 下一個訊息佇列中。</span><span class="sxs-lookup"><span data-stu-id="647f6-140">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="647f6-141">您也可以指定多少訊息想 tooget。</span><span class="sxs-lookup"><span data-stu-id="647f6-141">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="647f6-142">hello 訊息從傳回**清單\_messages()**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="647f6-142">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="647f6-143">以秒為單位，做為參數傳入 hello 可見度逾時。</span><span class="sxs-lookup"><span data-stu-id="647f6-143">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="647f6-144">toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**delete_message()**。</span><span class="sxs-lookup"><span data-stu-id="647f6-144">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="647f6-145">這兩個步驟的程序中移除訊息可確保當訊息因為 toohardware 或軟體失敗，另一個執行個體的程式碼可以取得您的程式碼失敗 tooprocess 可 hello 相同訊息，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="647f6-145">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="647f6-146">您的程式碼呼叫**刪除\_message()**處理 hello 訊息之後，以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="647f6-146">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="647f6-147">如何： 變更 hello 排入佇列的訊息內容</span><span class="sxs-lookup"><span data-stu-id="647f6-147">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="647f6-148">您可以變更訊息就地 hello 佇列中的 hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="647f6-148">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="647f6-149">下列程式碼 hello 使用 hello **update_message()**方法 tooupdate 訊息。</span><span class="sxs-lookup"><span data-stu-id="647f6-149">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="647f6-150">hello 方法會傳回 tuple，其中包含的 hello 佇列訊息的 pop receipt hello 和代表 hello 訊息會顯示 hello 佇列時的 UTC 日期時間值。</span><span class="sxs-lookup"><span data-stu-id="647f6-150">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="647f6-151">作法：清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="647f6-151">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="647f6-152">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="647f6-152">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="647f6-153">您可以取得一批訊息。</span><span class="sxs-lookup"><span data-stu-id="647f6-153">You can get a batch of message.</span></span>
2. <span data-ttu-id="647f6-154">您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="647f6-154">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="647f6-155">hello 下列程式碼範例會使用 hello**清單\_messages()**方法 tooget 15 訊息在單一呼叫中的。</span><span class="sxs-lookup"><span data-stu-id="647f6-155">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="647f6-156">接著，它會列出每個訊息，並加以刪除。</span><span class="sxs-lookup"><span data-stu-id="647f6-156">Then it prints and deletes each message.</span></span> <span data-ttu-id="647f6-157">它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。</span><span class="sxs-lookup"><span data-stu-id="647f6-157">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="647f6-158">如何： 取得 hello 佇列長度</span><span class="sxs-lookup"><span data-stu-id="647f6-158">How To: Get hello Queue Length</span></span>
<span data-ttu-id="647f6-159">您可以在 hello 佇列中取得估計的 hello 訊息數目。</span><span class="sxs-lookup"><span data-stu-id="647f6-159">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="647f6-160">hello**取得\_佇列\_metadata()**方法 hello 佇列的相關要求 hello 佇列服務 tooreturn hello 大約的訊息計數和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="647f6-160">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="647f6-161">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="647f6-161">How To: Delete a Queue</span></span>
<span data-ttu-id="647f6-162">toodelete 佇列和所有 hello 訊息包含在它呼叫 hello**刪除\_queue （)** hello 佇列物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="647f6-162">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="647f6-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="647f6-163">Next Steps</span></span>
<span data-ttu-id="647f6-164">現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn。</span><span class="sxs-lookup"><span data-stu-id="647f6-164">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="647f6-165">請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="647f6-165">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="647f6-166">請瀏覽 hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) GitHub 上的儲存機制</span><span class="sxs-lookup"><span data-stu-id="647f6-166">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="647f6-167">之間的比較為 hello Azure 佇列服務，此發行項與 hello 所述的 Azure 服務匯流排佇列中討論[如何 toouse Service Bus 佇列](/develop/ruby/how-to-guides/service-bus-queues/)發行項，請參閱[Azure 佇列和服務匯流排佇列-比較和對比](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="647f6-167">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
