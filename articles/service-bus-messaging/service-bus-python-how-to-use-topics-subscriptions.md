---
title: "使用 Python aaaHow toouse Azure 服務匯流排主題 |Microsoft 文件"
description: "深入了解如何 toouse Azure 服務匯流排主題和訂閱來自 Python。"
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>如何 toouse Service Bus 主題和訂閱使用 Python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

本文說明如何 toouse Service Bus 主題和訂閱。 hello 範例撰寫的 Python 和使用 hello [Azure Python SDK 封裝][Azure Python package]。 hello 涵蓋案例包括**建立主題和訂閱**，**建立訂用帳戶篩選**，**傳送訊息 tooa 主題**，**接收從訂用帳戶的郵件**，和**主題和訂用帳戶刪除**。 如需主題和訂閱的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> 如果您需要 tooinstall Python 或 hello [Azure Python 封裝][Azure Python package]，請參閱 hello [Python 安裝指南](../python-how-to-install.md)。

## <a name="create-a-topic"></a>建立主題
hello **ServiceBusService**物件可讓您 toowork 與主題。 加入要在其中任何 Python 檔案 tooprogrammatically 存取服務匯流排的 hello 頂端附近的 hello 下列：

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

hello 下列程式碼會建立**ServiceBusService**物件。 請使用真實的命名空間、共用存取簽章 (SAS) 金鑰名稱和金鑰值來取代 `mynamespace`、`sharedaccesskeyname` 和 `sharedaccesskey`。

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

您可以從 hello 取得 hello 值 hello SAS 金鑰名稱和值[Azure 入口網站][Azure portal]。

```python
bus_service.create_topic('mytopic')
```

hello`create_topic`方法也支援其他選項，可讓您 toooverride 預設主題設定，例如訊息時間 toolive 或最大主題大小。 hello 下列範例會設定 hello 最大主題大小 too5 GB，而時間 toolive (TTL) 值為 1 分鐘：

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>建立訂用帳戶
訂用帳戶 tootopics 也會建立以 hello **ServiceBusService**物件。 訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。

> [!NOTE]
> 訂閱是持續性，而且將會繼續 tooexist 直到任一它們，或 hello 主題 toowhich 它們所訂用，則會刪除。
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>建立訂用帳戶與 hello 預設 (MatchAll) 篩選器
hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。 當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題置於 hello 訂用帳戶的虛擬佇列。 hello 下列範例會建立名為訂用帳戶`AllMessages`和使用 hello 預設**MatchAll**篩選器。

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>使用篩選器建立訂用帳戶
您也可以定義可讓您 toospecify tooa 主題應該會顯示特定主題的訂用帳戶內傳送的訊息篩選器。

hello 最有彈性的訂用帳戶支援的篩選器的類型是**SqlFilter**，它會實作 SQL92 的子集。 SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。 如需可以搭配 SQL 篩選的 hello 運算式的詳細資訊，請參閱 hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression]語法。

您可以加入篩選 tooa 訂用帳戶使用 hello**建立\_規則**方法 hello **ServiceBusService**物件。 這個方法可讓您 tooadd 新篩選 tooan 現有訂用帳戶。

> [!NOTE]
> 因為 hello 預設篩選器會自動套用 tooall 新訂用帳戶，您必須先移除 hello 預設篩選器或 hello **MatchAll**將會覆寫任何其他您可以指定的篩選器。 您可以藉由使用 hello 移除 hello 預設規則`delete_rule`方法 hello **ServiceBusService**物件。
> 
> 

hello 下列範例會建立名為訂用帳戶`HighMessages`與**SqlFilter**只選取自訂的訊息`messagenumber`大於 3 的屬性：

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

同樣地，hello 下列範例會建立名為訂用帳戶`LowMessages`與**SqlFilter**只選取有訊息`messagenumber`屬性小於或等於 too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

現在，當訊息傳送太`mytopic`它永遠傳遞訂閱 tooreceivers toohello **AllMessages**主題訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello **HighMessages**和**LowMessages**主題訂用帳戶 （取決於 hello 訊息內容）。

## <a name="send-messages-tooa-topic"></a>傳送訊息 tooa 主題
toosend 訊息 tooa Service Bus 主題，您的應用程式必須使用 hello`send_topic_message`方法 hello **ServiceBusService**物件。

hello 下列範例會示範如何 toosend 五個測試訊息太`mytopic`。 請注意該 hello `messagenumber` hello hello 迴圈反覆運算上的每個訊息的屬性值而有所不同 （這會決定哪些訂閱接收該）：

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。 hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。 訊息保留在主題中的 hello 數目沒有限制，但是在 hello hello 訊息主題所持有的大小總計沒有端點。 此主題大小會在建立時定義，上限是 5 GB。 如需有關配額的詳細資訊，請參閱[服務匯流排配額][Service Bus quotas]。

## <a name="receive-messages-from-a-subscription"></a>自訂用帳戶接收訊息
訊息會從訂用帳戶使用 hello 接收`receive_subscription_message`方法上 hello **ServiceBusService**物件：

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

在讀取時從 hello 訂用帳戶刪除訊息 hello 參數`peek_lock`設定得**False**。 您可以讀取 （查看），並鎖定 hello 訊息，而不刪除它所設定的 hello 參數從 hello 佇列`peek_lock`太**True**。

hello 行為的讀取和刪除 hello 訊息，因為 hello 的一部分接收作業是 hello 最簡單的模型，並最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。 toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。 服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次的 hello 訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。

如果 hello`peek_lock`參數設定太**True**，hello 接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。 服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。 Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序`delete`方法上 hello**訊息**物件。 hello`delete`方法標示為正在使用的 hello 訊息，並移除 hello 訂用帳戶。

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 應用程式的當機，而且無法讀取訊息
服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。 如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello`unlock`方法上 hello**訊息**物件。 這將導致 hello 訂用帳戶內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。

另外還有 hello 訂閱內鎖定的訊息相關聯的逾時，如果 hello 應用程式失敗 tooprocess hello 訊息之前 hello 鎖定逾時到期 （例如，如果 hello 應用程式當機），然後服務匯流排解除鎖定 hello 訊息自動並使其成為可用 toobe 再度接收。

在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello`delete`呼叫方法時，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。 這通常稱為*至少一旦處理*，也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。 如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。 這通常用來達成 hello **MessageId** hello 訊息，將會維持所有傳遞嘗試的屬性。

## <a name="delete-topics-and-subscriptions"></a>刪除主題和訂用帳戶
主題和訂閱持續性，而且必須明確刪除透過 hello [Azure 入口網站][ Azure portal]或以程式設計的方式。 hello 下列範例顯示如何命名 toodelete hello 主題`mytopic`:

```python
bus_service.delete_topic('mytopic')
```

刪除的主題也會刪除任何訂用帳戶註冊的 hello 主題。 您也可以個別刪除訂用帳戶。 hello 下列程式碼會示範如何 toodelete 訂用帳戶命名`HighMessages`從 hello`mytopic`主題：

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>後續步驟
現在，您學到的 Service Bus 主題 hello 基本概念，請遵循這些連結 toolearn 更多。

* 請參閱[佇列、主題和訂用帳戶][Queues, topics, and subscriptions]。
* [SqlFilter.SqlExpression][SqlFilter.SqlExpression] 的參考資料。

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
