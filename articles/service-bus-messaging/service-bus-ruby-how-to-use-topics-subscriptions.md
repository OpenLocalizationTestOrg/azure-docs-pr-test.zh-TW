---
title: "aaaHow toouse Service Bus 主題 (Ruby) |Microsoft 文件"
description: "深入了解如何 toouse Service Bus 主題和訂用帳戶在 Azure 中的。 程式碼範例專為 Ruby 應用程式撰寫。"
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>如何 toouse Service Bus 主題和訂閱與 Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

本文說明如何 toouse Service Bus 主題和訂閱從 Ruby 應用程式。 hello 涵蓋案例包括**建立主題和訂用帳戶，來建立訂用帳戶篩選，將訊息傳送**tooa 主題**從訂閱接收訊息**，和**主題和訂用帳戶刪除**。 如需有關主題和訂閱的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>建立主題
hello **Azure::ServiceBusService**物件可讓您 toowork 與主題。 hello 下列程式碼會建立**Azure::ServiceBusService**物件。 toocreate 主題，使用 hello`create_topic()`方法。 下列範例中的 hello 建立主題，或如果有的話，會列印出 hello 錯誤。

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

您也可以傳遞**Azure::ServiceBus::Topic**其他選項，可讓您 toooverride 預設主題設定，例如訊息時間 toolive 或最大佇列大小的物件。 hello 下列範例所示設定 hello 最大佇列大小 too5 GB 和時間 toolive too1 分鐘：

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>建立訂用帳戶
主題訂用帳戶也會建立以 hello **Azure::ServiceBusService**物件。 訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。

訂閱是持續性，而且將會繼續 tooexist 直到任一它們，或 hello 主題它們相關聯，則會被刪除。 如果您的應用程式包含邏輯 toocreate 訂用帳戶，它應該先檢查 hello 訂用帳戶已經有使用 hello getSubscription 方法。

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>建立訂用帳戶與 hello 預設 (MatchAll) 篩選器
hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。 當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題置於 hello 訂用帳戶的虛擬佇列。 hello 下列範例會建立名為"all messages"訂用帳戶，並使用 hello 預設**MatchAll**篩選器。

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>使用篩選器建立訂用帳戶
您也可以定義可讓您 toospecify tooa 主題應該會顯示特定的訂用帳戶內傳送的訊息篩選器。

hello 最有彈性的訂用帳戶支援的篩選器的類型為 hello **Azure::ServiceBus::SqlFilter**，它會實作 SQL92 的子集。 SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。 如需有關可以搭配 SQL 篩選的 hello 運算式的詳細資訊，請檢閱 hello [SqlFilter](service-bus-messaging-sql-filter.md)語法。

您可以加入篩選 tooa 訂用帳戶使用 hello`create_rule()`方法 hello **Azure::ServiceBusService**物件。 這個方法可讓您 tooadd 新篩選 tooan 現有訂用帳戶。

因為 hello 預設篩選器會自動套用 tooall 新訂用帳戶，您必須先移除 hello 預設篩選器，或 hello **MatchAll**將會覆寫任何其他您可以指定的篩選器。 您可以藉由使用 hello 移除 hello 預設規則`delete_rule()`方法上 hello **Azure::ServiceBusService**物件。

hello 下列範例會建立名為 「 高訊息 」 的訂閱**Azure::ServiceBus::SqlFilter**只選取自訂的訊息`message_number`大於 3 的屬性：

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

同樣地，hello 下列範例會建立名為訂用帳戶`low-messages`與**Azure::ServiceBus::SqlFilter**只選取有訊息`message_number`屬性小於或等於 too3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

當訊息現在是否傳送太`test-topic`，它會一律為訂閱的傳遞的 tooreceivers toohello`all-messages`主題訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello`high-messages`和`low-messages`主題訂用帳戶 (視 hello 訊息內容）。

## <a name="send-messages-tooa-topic"></a>傳送訊息 tooa 主題
toosend 訊息 tooa Service Bus 主題，您的應用程式必須使用 hello`send_topic_message()`方法上 hello **Azure::ServiceBusService**物件。 TooService 匯流排主題是 hello 的執行個體傳送訊息**Azure::ServiceBus::BrokeredMessage**物件。 **Azure::ServiceBus::BrokeredMessage**物件具有一組標準屬性 (例如`label`和`time_to_live`) 的字典，其中使用的 toohold 自訂應用程式特定屬性，和字串資料的主體。 應用程式可以藉由傳遞字串值 toohello 設定 hello hello 訊息本文`send_topic_message()`方法和任何所需標準屬性將會填入預設值。

hello 下列範例會示範如何 toosend 五個測試訊息太`test-topic`。 請注意該 hello `message_number` hello hello 迴圈反覆運算上的每個訊息的自訂屬性值而有所不同 （這會決定哪一個訂閱能收到它）：

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。 hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。 訊息保留在主題中的 hello 數目沒有限制，但是在 hello hello 訊息主題所持有的大小總計沒有端點。 此主題大小會在建立時定義，上限是 5 GB。

## <a name="receive-messages-from-a-subscription"></a>自訂用帳戶接收訊息
訊息會從訂用帳戶使用 hello 接收`receive_subscription_message()`方法上 hello **Azure::ServiceBusService**物件。 根據預設，訊息會 read(peak)，但不會刪除從 hello 訂用帳戶已鎖定。 您可以讀取並刪除 hello 訂用帳戶中的 hello 訊息，所設定的 hello`peek_lock`太選項**false**。

hello 預設行為可讓 hello 讀取和刪除兩階段作業，也使其不容許遺失訊息的可能 toosupport 應用程式。 服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。 Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序`delete_subscription_message()`方法並提供 hello 訊息 toobe 刪除做為參數。 hello`delete_subscription_message()`方法會標示為正在使用的 hello 訊息，並移除從 hello 訂用帳戶。

如果 hello`:peek_lock`參數設定太**false**，讀取和刪除 hello 訊息會變成 hello 最簡單的模型，並且適合用於應用程式可以容許不處理訊息的 hello 事件中的案例失敗。 toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。 服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。

hello 下列範例示範如何可以接收和處理使用`receive_subscription_message()`。 hello 範例先接收並刪除 hello 訊息`low-messages`訂用帳戶使用`:peek_lock`設定得**false**，然後在另一則訊息收到 hello `high-messages` ，然後刪除 hello 訊息使用`delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 應用程式的當機，而且無法讀取訊息
服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。 如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlock_subscription_message()`方法上 hello **Azure::ServiceBusService**物件。 這樣會導致服務匯流排 toounlock hello 訊息 hello 訂用帳戶內，並將其可用 toobe 接收一次，可能是藉由 hello 取用應用程式，或由另一個使用的應用程式相同。

另外還有 hello 訂閱內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），然後服務匯流排會解除鎖定 hello 訊息自動，並將其可用 toobe 再度接收。

在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`delete_subscription_message()`呼叫方法時，則 hello 訊息時，已重新傳遞的 toohello 應用程式會在重新啟動。 這通常稱為*至少一旦處理*; 也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。 如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。 這個邏輯通常用來達成 hello `message_id` hello 訊息，將會維持所有傳遞嘗試的屬性。

## <a name="delete-topics-and-subscriptions"></a>刪除主題和訂用帳戶
主題和訂閱持續性，而且必須明確刪除透過 hello [Azure 入口網站][ Azure portal]或以程式設計的方式。 下列的 hello 範例示範如何命名 toodelete hello 主題`test-topic`。

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

刪除的主題也會刪除任何訂用帳戶註冊的 hello 主題。 您也可以個別刪除訂用帳戶。 hello 下列程式碼示範如何 toodelete hello 訂用帳戶命名`high-messages`從 hello`test-topic`主題：

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>後續步驟
現在，您學到的 Service Bus 主題 hello 基本概念，請遵循這些連結 toolearn 更多。

* 請參閱[佇列、主題和訂用帳戶](service-bus-queues-topics-subscriptions.md)。
* [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter) 的 API 參考資料。
* 請瀏覽 hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) GitHub 上的儲存機制。

[Azure portal]: https://portal.azure.com
