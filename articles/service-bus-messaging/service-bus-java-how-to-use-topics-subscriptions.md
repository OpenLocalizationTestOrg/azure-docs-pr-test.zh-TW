---
title: "使用 Java aaaHow toouse Azure 服務匯流排主題 |Microsoft 文件"
description: "使用 Azure 中的服務匯流排主題和訂用帳戶。"
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>如何 toouse Service Bus 主題和訂閱與 Java

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

本指南說明如何 toouse Service Bus 主題和訂閱。 hello 範例以 Java 撰寫，並使用 hello [Azure SDK for Java][Azure SDK for Java]。 hello 涵蓋案例包括**建立主題和訂閱**，**建立訂用帳戶篩選**，**傳送訊息 tooa 主題**，**接收從訂用帳戶的郵件**，和**主題和訂用帳戶刪除**。

## <a name="what-are-service-bus-topics-and-subscriptions"></a>什麼是服務匯流排主題和訂用帳戶？
服務匯流排主題和訂用帳戶支援「發佈/訂閱」  訊息通訊模型。 使用主題和訂用帳戶時，分散式應用程式的元件彼此不直接通訊，相反的，他們會透過扮演中繼角色的主題來交換訊息。

![主題概念](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

有別於服務匯流排佇列，服務匯流排佇列中的每個訊息只會由單一取用者處理，主題和訂用帳戶採用發佈/訂用帳戶模式，提供一對多的通訊形式。 就可以註冊多個訂用帳戶 tooa 主題。 當訊息傳送 tooa 主題時，它就可使用可用 tooeach 訂用帳戶 toohandle/處理序分開。

訂用帳戶 tooa 主題類似於虛擬佇列，可接收 toohello 主題傳送 hello 訊息複本。 您可以選擇性地註冊主題以每個訂用帳戶為基礎，可讓您 toofilter/限制哪些主題訂用帳戶所收到的訊息 tooa 主題上的篩選規則。

服務匯流排主題和訂用帳戶可讓您 tooscale tooprocess 非常大量的訊息在非常大量的使用者和應用程式。

## <a name="create-a-service-namespace"></a>建立服務命名空間
toobegin 使用服務匯流排主題和訂用帳戶在 Azure 中，您必須先建立的命名空間提供範圍的容器應用程式中的服務匯流排資源定址。

toocreate 命名空間：

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>設定您的應用程式 toouse 服務匯流排
請確定您已安裝 hello [Azure SDK for Java] [ Azure SDK for Java]之前建置此範例。 如果您使用 Eclipse，您可以安裝 hello [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse]包含 hello Azure SDK for Java。 然後，您可以加入 hello **Microsoft Azure Libraries for Java** tooyour 專案：

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

新增下列 hello `import` hello Java 檔案的陳述式 toohello 頂端：

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

新增 hello Azure Libraries for Java tooyour 建置路徑，並將它加入您的專案部署組件中。

## <a name="create-a-topic"></a>建立主題
服務匯流排主題的管理作業可透過 **ServiceBusContract** 類別來執行。 A **ServiceBusContract**物件建構適當的設定封裝的權限 toomanage SAS 權杖，且 hello **ServiceBusContract**類別是 hello 唯一點使用 Azure 進行通訊。

hello **ServiceBusService**類別會提供方法 toocreate、 列舉和刪除的主題。 下列範例會示範如何 hello **ServiceBusService**物件可以用的 toocreate 主題名為`TestTopic`，與呼叫的命名空間`HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

上有方法**TopicInfo**可讓 hello 主題設定的屬性 (例如： tooset hello 預設存留時間 (TTL) 值套用 toobe toomessages 傳送 toohello 主題)。 hello 下列範例示範如何 toocreate 主題命名`TestTopic`5 GB 的大小上限：

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

請注意，您可以使用 hello **listTopics**方法**ServiceBusContract**物件 toocheck，如果在服務命名空間已經存在具有指定名稱的主題。

## <a name="create-subscriptions"></a>建立訂用帳戶
訂用帳戶 tootopics 也會建立以 hello **ServiceBusService**類別。 訂用帳戶命名，而且可以有選擇性篩選器，以限制 hello 組傳遞 toohello 訂用帳戶的虛擬佇列的訊息。

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>建立訂用帳戶與 hello 預設 (MatchAll) 篩選器
hello **MatchAll**是 hello 預設篩選器時所用新的訂用帳戶建立時指定任何篩選條件。 當 hello **MatchAll**篩選時，所有的訊息已發行的 toohello 主題會放在訂用帳戶的虛擬佇列。 hello 下列範例會建立名為"AllMessages 」 訂用帳戶，並使用 hello 預設**MatchAll**篩選器。

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>使用篩選器建立訂用帳戶
您也可以建立可讓您篩選器 tooscope tooa 主題應該會顯示特定主題的訂用帳戶內傳送的訊息。

hello 最有彈性的訂用帳戶支援的篩選器的類型是[SqlFilter][SqlFilter]，它會實作 SQL92 的子集。 SQL 篩選操作的已發行的 toohello 主題 hello 訊息 hello 屬性。 如需有關可以搭配 SQL 篩選的 hello 運算式的詳細資訊，請檢閱 hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression]語法。

hello 下列範例會建立名為訂用帳戶`HighMessages`與[SqlFilter] [ SqlFilter]物件只會選取自訂的訊息， **MessageNumber**大於 3 的內容：

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

同樣地，hello 下列範例會建立名為訂用帳戶`LowMessages`與[SqlFilter] [ SqlFilter]物件，以只選取有訊息**MessageNumber**屬性小於或等於 too3:

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

當訊息現在是否傳送太`TestTopic`，它會一律傳送訂閱的 tooreceivers toohello`AllMessages`訂用帳戶，並選擇性地傳遞的 tooreceivers 訂閱 toohello`HighMessages`和`LowMessages`訂用帳戶 (根據訊息內容）。

## <a name="send-messages-tooa-topic"></a>傳送訊息 tooa 主題
toosend 訊息 tooa Service Bus 主題，您的應用程式會取得**ServiceBusContract**物件。 hello 下列程式碼示範如何 toosend hello 訊息`TestTopic`hello 內先前建立的主題`HowToSample`命名空間：

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

傳送 tooService 匯流排主題的訊息是的執行個體[BrokeredMessage] [ BrokeredMessage]類別。 [BrokeredMessage][BrokeredMessage]* 物件具有一組標準方法 (例如**setLabel**和**TimeToLive**)，是使用的 toohold 自訂字典應用程式特定的屬性和任意應用程式資料的主體。 應用程式可以將任何可序列化的物件傳遞至 hello 建構函式設定 hello 訊息本文[BrokeredMessage][BrokeredMessage]，並適當 hello **DataContractSerializer**就會使用的 tooserialize hello 物件。 或者，也可以提供 **java.io.InputStream**。

hello 下列範例會示範如何 toosend 五個測試訊息 toothe `TestTopic` **MessageSender**我們取得 hello 上述程式碼片段中。
請注意如何 hello **MessageNumber** hello hello 迴圈反覆運算上的每個訊息的屬性值而有所不同 （這會決定哪些訂閱接收該）：

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

服務匯流排主題支援 hello 訊息大小上限為 256KB[標準層](service-bus-premium-messaging.md)和 1 MB 的 hello [Premium 層](service-bus-premium-messaging.md)。 hello 標頭，其中包括 hello 標準和自訂應用程式屬性，可以有 64 KB 的大小上限。 訊息保留在主題中的 hello 數目沒有限制，但 hello 主題所持有的 hello 訊息總大小沒有限制。 此主題大小會在建立時定義，上限是 5 GB。

## <a name="how-tooreceive-messages-from-a-subscription"></a>Tooreceive 從訂用帳戶的郵件
從訂用帳戶，tooreceive 訊息使用**ServiceBusContract**物件。 接收的訊息可在兩種不同的模式下運作：**ReceiveAndDelete** 和 **PeekLock**。

當使用 hello **ReceiveAndDelete**模式中，接收是單發式作業-也就是當服務匯流排接收訊息的讀取的要求時，它會標示為正在使用的 hello 訊息，就傳回該 toothe 應用程式。 **ReceiveAndDelete**模式 hello 簡單的模式，最適合用於應用程式可以容許不處理中失敗的 hello 事件訊息的案例。 toounderstand，假設在哪一個 hello 取用者問題 hello 接收要求，而後再處理它。 服務匯流排將已經標示為正在使用，然後當 hello 應用程式重新啟動並開始取用訊息一次訊息，因為它將會遺失已的 hello 訊息取用先前 toohello 損毀。

在**PeekLock**模式中，接收作業會變成兩個階段，使其不容許遺失訊息的可能 toosupport 應用程式。 服務匯流排收到要求時，它會尋找下一個訊息 toobe hello 耗用鎖定，tooprevent 其他消費者接收該，然後再將它傳 toohello 應用程式。 Hello 應用程式完成處理 hello 訊息 （或可靠地儲存以供未來處理後），它就會完成 hello hello 第二個階段藉由呼叫接收處理序**刪除**上收到 hello 訊息。 當服務匯流排會看見 hello**刪除**呼叫，它會將標示為正在使用的 hello 訊息，並移除 hello 主題。

hello 以下範例示範如何收到訊息的方式，以及處理使用**PeekLock**模式 （未 hello 預設模式）。 hello 下面範例會執行迴圈和處理 hello"HighMessages 」 訂用帳戶中的訊息，並結束作業沒有任何訊息時 （或者，它無法設定新郵件 toowait）。

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Toohandle 應用程式的當機，而且無法讀取訊息
服務匯流排提供的功能 toohelp 適宜地自行復原發生錯誤的應用程式或處理訊息的問題。 如果接收者應用程式無法 tooprocess hello 訊息基於某些原因，則它可以呼叫 hello **unlockMessage**收到 hello 訊息上的方法 (而不是 hello **deleteMessage**方法)。 這將導致 hello 主題內的服務匯流排 toounlock hello 訊息，並讓它使用 toobe 收到試一次，請藉由 hello 取用應用程式，或由另一個使用的應用程式相同。

也沒有逾時 > 主題內鎖定的訊息相關聯，而且如果 hello 應用程式失敗 tooprocess hello 訊息之前鎖定逾時 （例如，如果 hello 應用程式當機），然後服務匯流排會自動解除鎖定 hello 訊息並將其可用 toobe 再度接收。

在 hello hello 應用程式的事件損毀之後處理 hello 訊息，但之前 hello **deleteMessage**發出要求，則 hello 訊息將會是已重新傳遞的 toohello 應用程式，重新啟動時。 這通常稱為**至少一旦處理**，也就是將至少一次處理每則訊息，但可能在某些情況下 hello 傳遞相同的訊息。 如果 hello 案例無法容許重複處理，應用程式開發人員應該加入額外的邏輯 tootheir 應用程式 toohandle 重複的訊息傳遞。 這通常用來達成 hello **getMessageId** hello 訊息，將會維持所有傳遞嘗試的方法。

## <a name="delete-topics-and-subscriptions"></a>刪除主題和訂用帳戶
hello 主要方式 toodelete 主題和訂用帳戶是 toouse **ServiceBusContract**物件。 刪除的主題也會刪除任何訂用帳戶註冊的 hello 主題。 您也可以個別刪除訂用帳戶。

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>後續步驟
現在，您學到的服務匯流排佇列的 hello 基本概念，請參閱[服務匯流排佇列、 主題和訂用帳戶][ Service Bus queues, topics, and subscriptions]如需詳細資訊。

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
