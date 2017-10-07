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
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>如何 toouse Ruby 從佇列儲存體
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>概觀
本指南也說明如何使用 tooperform 常見案例 hello Microsoft Azure 佇列儲存體服務。 使用 hello Ruby Azure 應用程式開發介面撰寫 hello 範例。
hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立及刪除佇列**。

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>建立 Ruby 應用程式
建立 Ruby 應用程式。 如需指示，請參閱 [Azure VM 上的 Ruby on Rails Web 應用程式](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)。

## <a name="configure-your-application-tooaccess-storage"></a>設定您的應用程式 tooAccess 儲存體
toouse Azure 儲存體，您需要 toodownload 和使用 hello 拼音 azure 的封裝，其中包含一組與 hello 儲存體服務 REST 服務通訊的便利性程式庫。

### <a name="use-rubygems-tooobtain-hello-package"></a>使用 RubyGems tooobtain hello 套件
1. 使用命令列介面，例如 **PowerShell** (Windows)、**Terminal** (Mac) 或 **Bash** (Unix)。
2. 輸入健身安裝 azure 」 在 hello 命令視窗 tooinstall hello 健身和相依性。

### <a name="import-hello-package"></a>匯入 hello 封裝
使用您慣用的文字編輯器，請新增下列 toohello hello 拼音想 toouse 儲存體的檔案頂端的 hello:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>設定 Azure 儲存體連接
hello azure 模組會讀取 hello 環境變數**AZURE\_儲存體\_帳戶**和**AZURE\_儲存體\_ACCESS_KEY**的tooconnect tooyour Azure 儲存體帳戶所需的資訊。 如果未設定這些環境變數，您必須指定 hello 帳戶資訊，才能使用**Azure::QueueService**以下列程式碼的 hello:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain hello Azure 入口網站中的帳戶從傳統或資源管理員儲存這些值：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 瀏覽您想 toouse toohello 儲存體帳戶。
3. 在 hello 設定 刀鋒視窗上 hello 右邊，按一下 **便捷鍵**。
4. 在 hello 存取金鑰刀鋒視窗中出現，您會看到 hello 便捷鍵 1 和 2 的存取金鑰。 您可以使用其中一個存取金鑰。 
5. 按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。 

tooobtain hello 傳統 Azure 入口網站中的這些值從傳統儲存體帳戶：

1. 登入 toohello[傳統 Azure 入口網站](https://manage.windowsazure.com)。
2. 瀏覽您想 toouse toohello 儲存體帳戶。
3. 按一下**管理存取金鑰**在 hello hello 瀏覽窗格的底部。
4. 在 hello 顯對話方塊中，您會看到 hello 儲存體帳戶名稱、 主要存取金鑰和次要存取金鑰。 針對存取金鑰，您可以使用 hello 主要或次要的一個 hello。 
5. 按一下 hello 複製圖示 toocopy hello 金鑰 toohello 剪貼簿。

## <a name="how-to-create-a-queue"></a>作法：建立佇列
hello 下列程式碼會建立**Azure::QueueService**物件，可讓您與佇列搭配 toowork。

```ruby
azure_queue_service = Azure::QueueService.new
```

使用 hello **create_queue()**方法 toocreate hello 的佇列指定的名稱。

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>作法：將訊息插入佇列中
將訊息插入佇列中，使用 hello tooinsert **create_message()**方法 toocreate 新訊息並將它加入 toohello 佇列。

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>如何： 檢視 hello 下一個訊息
您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello**查看\_messages()**方法。 **peek\_messages()** 預設會查看單一訊息。 您也可以指定多少訊息想 toopeek。

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>如何： 清除佇列 hello 下一個訊息
您可以使用兩個步驟將訊息從佇列中移除。

1. 當您呼叫**清單\_messages()**，預設會取得 hello 下一個訊息佇列中。 您也可以指定多少訊息想 tooget。 hello 訊息從傳回**清單\_messages()**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。 以秒為單位，做為參數傳入 hello 可見度逾時。
2. toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**delete_message()**。

這兩個步驟的程序中移除訊息可確保當訊息因為 toohardware 或軟體失敗，另一個執行個體的程式碼可以取得您的程式碼失敗 tooprocess 可 hello 相同訊息，然後再試一次。 您的程式碼呼叫**刪除\_message()**處理 hello 訊息之後，以滑鼠右鍵。

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>如何： 變更 hello 排入佇列的訊息內容
您可以變更訊息就地 hello 佇列中的 hello 的內容。 下列程式碼 hello 使用 hello **update_message()**方法 tooupdate 訊息。 hello 方法會傳回 tuple，其中包含的 hello 佇列訊息的 pop receipt hello 和代表 hello 訊息會顯示 hello 佇列時的 UTC 日期時間值。

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>作法：清除佇列訊息的其他選項
自訂從佇列中擷取訊息的方法有兩種。

1. 您可以取得一批訊息。
2. 您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。

hello 下列程式碼範例會使用 hello**清單\_messages()**方法 tooget 15 訊息在單一呼叫中的。 接著，它會列出每個訊息，並加以刪除。 它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>如何： 取得 hello 佇列長度
您可以在 hello 佇列中取得估計的 hello 訊息數目。 hello**取得\_佇列\_metadata()**方法 hello 佇列的相關要求 hello 佇列服務 tooreturn hello 大約的訊息計數和中繼資料。

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>作法：刪除佇列
toodelete 佇列和所有 hello 訊息包含在它呼叫 hello**刪除\_queue （)** hello 佇列物件上的方法。

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>後續步驟
現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn。

* 請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)
* 請瀏覽 hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) GitHub 上的儲存機制

之間的比較為 hello Azure 佇列服務，此發行項與 hello 所述的 Azure 服務匯流排佇列中討論[如何 toouse Service Bus 佇列](/develop/ruby/how-to-guides/service-bus-queues/)發行項，請參閱[Azure 佇列和服務匯流排佇列-比較和對比](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
