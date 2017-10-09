---
title: "aaaHow toouse Azure 服務匯流排佇列與 Ruby |Microsoft 文件"
description: "了解如何 toouse Service Bus 佇列在 Azure 中。 程式碼範例以 Ruby 撰寫。"
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>服務匯流排 toouse 排入佇列以 Ruby

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

本指南說明如何 toouse 服務匯流排佇列。 hello 範例以 Ruby 所撰寫，並使用 hello Azure 健身。 hello 涵蓋案例包括**建立佇列，傳送和接收訊息**，和**刪除佇列**。 如需有關 Service Bus 佇列的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>如何 toocreate 佇列
hello **Azure::ServiceBusService**物件可讓您與佇列搭配 toowork。 toocreate 佇列中，使用 hello`create_queue()`方法。 hello 下列範例會建立佇列或列印出任何錯誤。

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

您也可以傳遞**Azure::ServiceBus::Queue**物件與其他選項，可讓您 toooverride hello 預設佇列設定中的，例如訊息時間 toolive 或最大佇列大小。 hello 下列範例顯示如何 tooset hello 最大佇列大小 too5 GB 和 toolive too1 分鐘的時間：

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>如何 toosend 訊息 tooa 佇列
toosend 訊息 tooa Service Bus 佇列，您的應用程式呼叫 hello`send_queue_message()`方法上 hello **Azure::ServiceBusService**物件。 訊息太傳送 （與從接收的資料） 的服務匯流排佇列是**Azure::ServiceBus::BrokeredMessage**物件，並有一組標準屬性 (例如`label`和`time_to_live`)，是使用的 toohold 字典自訂應用程式特有的屬性和任意應用程式資料的主體。 應用程式可以設定 hello hello 訊息本文藉由傳遞字串值為 hello 訊息和任何必要的標準屬性會填入預設值。

hello 下列範例會示範如何 toosend 測試訊息 toohello 佇列名為`test-queue`使用`send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

服務匯流排佇列支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。 hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。 訊息保留在佇列中的 hello 數目沒有限制，但是在 hello hello 訊息佇列所持有的大小總計沒有端點。 此佇列大小會在建立時定義，上限是 5 GB。

## <a name="how-tooreceive-messages-from-a-queue"></a>Tooreceive 從佇列的訊息
訊息會使用從佇列接收 hello`receive_queue_message()`方法上 hello **Azure::ServiceBusService**物件。 根據預設，會讀取及鎖定而不從 hello 佇列刪除訊息。 不過，您可以刪除訊息從 hello 佇列設定 hello 讀取`:peek_lock`太選項**false**。

hello 預設行為可讓 hello 讀取和刪除兩階段作業，也使其不容許遺失訊息的可能 toosupport 應用程式。 服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。 Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序`delete_queue_message()`方法並提供 hello 訊息 toobe 刪除做為參數。 hello`delete_queue_message()`方法會標示為正在使用的 hello 訊息，並從 hello 佇列中移除它。

如果 hello`:peek_lock`參數設定太**false**，讀取和刪除 hello 訊息會變成 hello 最簡單的模型，並且適合用於應用程式可以容許不處理訊息的 hello 事件中的案例失敗。 toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。 服務匯流排已標示為正在使用，當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。

hello 下列範例會示範如何 tooreceive 和處理序訊息使用`receive_queue_message()`。 hello 範例先接收並刪除訊息使用`:peek_lock`設定得**false**、 收到另一則訊息，然後再刪除 hello 訊息使用`delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 應用程式的當機，而且無法讀取訊息
服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。 如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlock_queue_message()`方法上 hello **Azure::ServiceBusService**物件。 服務匯流排 toounlock hello hello 佇列訊息，並將其可用 toobe 同樣地，收到此呼叫原因可能是藉由 hello 取用應用程式，或由另一個使用的應用程式相同。

另外還有 hello 佇列內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），然後服務匯流排解除鎖定 hello 訊息自動並使其成為可用 toobe 再度接收。

在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`delete_queue_message()`呼叫方法時，則 hello 訊息時，已重新傳遞的 toohello 應用程式會在重新啟動。 此程序通常稱為*至少一旦處理*; 也就是說，每個訊息會至少處理一次，但可能在某些情況下 hello 傳遞相同的訊息。 如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。 這通常用來達成 hello `message_id` hello 訊息，嘗試傳遞都維持不變的屬性。

## <a name="next-steps"></a>後續步驟
現在，您學到的服務匯流排佇列的 hello 基本概念，請遵循這些連結 toolearn 更多。

* [佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)概觀。
* 請瀏覽 hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) GitHub 上的儲存機制。

如需本文所討論的 hello Azure 服務匯流排佇列和 Azure 佇列中 hello 討論之間的比較[如何 toouse 佇列儲存體從 Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md)發行項，請參閱[Azure 佇列和 Azure Service Bus 佇列-比較和對比](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

