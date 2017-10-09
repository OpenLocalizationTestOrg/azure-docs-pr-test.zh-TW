---
title: "以 hello Java 服務匯流排 API aaaHow toouse AMQP 1.0 |Microsoft 文件"
description: "如何 toouse hello Java 訊息服務 (JMS) 與 Azure 服務匯流排和進階訊息佇列 Protodol (AMQP) 1.0。"
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>如何 toouse hello Java 訊息服務 (JMS) API 服務匯流排與 AMQP 1.0
hello 進階訊息佇列通訊協定 (AMQP) 1.0 是一種有效率、 可靠、 有線等級訊息通訊協定，您可以使用 toobuild 強固且能跨平台訊息應用程式。

表示您可以使用 hello 佇列和發佈/訂閱代理傳訊功能從某個範圍的平台使用有效率的二進位通訊協定的服務匯流排 AMQP 1.0 支援。 此外，您還可以建置使用混合語言、架構及作業系統所建置之元件所組成的應用程式。

本文說明如何 toouse 服務匯流排傳訊功能 （佇列和發佈/訂閱主題） 使用的 Java 應用程式從 hello 熱門 Java 訊息服務 (JMS) API 的標準。 沒有[同系列文章](service-bus-amqp-dotnet.md)，說明如何 toodo hello 相同使用 hello 服務匯流排.NET API。 您可以使用下列兩個指南一起 toolearn 關於跨平台訊息使用 AMQP 1.0。

## <a name="get-started-with-service-bus"></a>開始使用服務匯流排
本指南假設您已經有服務匯流排命名空間，其中包含名稱為 **queue1** 的佇列。 如果您不這麼做，則您可以[建立 hello 命名空間與佇列](service-bus-create-namespace-portal.md)使用 hello [Azure 入口網站](https://portal.azure.com)。 如需有關如何 toocreate 服務匯流排命名空間和佇列，請參閱[開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)。

> [!NOTE]
> 分割的佇列和主題也支援 AMQP。 如需詳細資訊，請參閱[分割傳訊實體](service-bus-partitioning.md)及[服務匯流排分割佇列和主題的 AMQP 1.0 支援](service-bus-partitioned-queues-and-topics-amqp-overview.md)。
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>下載 hello AMQP 1.0 JMS 用戶端程式庫
其中 toodownload hello hello Apache Qpid JMS AMQP 1.0 用戶端程式庫的最新版本的相關資訊，請瀏覽[https://qpid.apache.org/download.html](https://qpid.apache.org/download.html)。

您必須新增 hello hello Apache Qpid JMS AMQP 1.0 發佈封存 toohello Java CLASSPATH 中的下列四個 JAR 檔案，建置和執行 JMS 應用程式與服務匯流排時：

* geronimo-jms\_1.1\_spec-1.0.jar
* qpid-amqp-1-0-client-[version].jar
* qpid-amqp-1-0-client-jms-[version].jar
* qpid-amqp-1-0-common-[version].jar

## <a name="coding-java-applications"></a>編寫 Java 應用程式
### <a name="java-naming-and-directory-interface-jndi"></a>Java 命名及目錄介面 (JNDI)
JMS 使用 hello Java Naming and Directory Interface (JNDI) toocreate 的區隔邏輯名稱和實體名稱。 使用 JNDI 可以解析兩種 JMS 物件：ConnectionFactory 和 Destination。 JNDI 使用提供者模型，您可以在其中插入不同的目錄服務 toohandle 名稱解析責任。 hello Apache Qpid JMS AMQP 1.0 程式庫隨附一個以簡單屬性以檔案為基礎 JNDI 提供者所設定使用內容檔的 hello 下列格式：

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a>設定 hello ConnectionFactory
hello 用項目的 toodefine **ConnectionFactory**在 hello Qpid 屬性檔 JNDI 提供者是下列格式的 hello:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

其中**[jndi_name]**和**[ConnectionURL]**具有下列意義 hello:

* **[jndi_name]**: hello 的 hello ConnectionFactory 的邏輯名稱。 這是將解決 hello 使用 hello JNDI Intialcontext.lookup （） 方法的 Java 應用程式中的 hello 名稱。
* **[ConnectionURL]**: Hello 的相關資訊提供給 hello JMS 程式庫的 URL 需要 toohello AMQP 代理人。

hello hello 格式**ConnectionURL**如下所示：

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
其中**[命名空間]**， **[SASPolicyName]**和**[SASPolicyKey]**具有下列意義 hello:

* **[命名空間]**: hello 服務匯流排命名空間。
* **[SASPolicyName]**: hello 佇列共用存取簽章原則名稱。
* **[SASPolicyKey]**: hello 佇列共用存取簽章原則機碼。

> [!NOTE]
> 您必須手動進行 URL 編碼 hello 密碼。 [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp) 中提供實用的 URL 編碼公用程式。
> 
> 

#### <a name="configure-destinations"></a>設定目的地
使用的 toodefine hello Qpid 屬性檔 JNDI 提供者中的目的地是下列格式的 hello hello 項目：

```
queue.[jndi_name] = [physical_name]
```

或

```
topic.[jndi_name] = [physical_name]
```

其中**[jndi\_名稱]**和**[實體\_名稱]**具有下列意義 hello:

* **[jndi_name]**: hello 的 hello 目的地的邏輯名稱。 這是將解決 hello 使用 hello JNDI Intialcontext.lookup （） 方法的 Java 應用程式中的 hello 名稱。
* **[physical_name]**: hello 名稱 hello 服務匯流排實體 toowhich hello 應用程式傳送或接收訊息。

> [!NOTE]
> 接收來自服務匯流排主題訂用帳戶，在 JNDI 中指定的 hello 實體名稱應該 hello hello 主題名稱。 hello JMS 應用程式程式碼中建立 hello 持久的訂用帳戶時，會提供 hello 訂用帳戶名稱。 hello[服務匯流排 AMQP 1.0 開發人員手冊 》](service-bus-amqp-dotnet.md)上使用來自 JMS 的服務匯流排主題提供更多詳細資料。
> 
> 

### <a name="write-hello-jms-application"></a>撰寫 hello JMS 應用程式
對於服務匯流排使用 JMS 時，不需要特別 API 或選項。 不過，後續將說明一些限制。 任何 JMS 應用程式中，首先需要 hello 是 hello JNDI 環境 toobe 無法 tooresolve 組態**ConnectionFactory**和目的地。

#### <a name="configure-hello-jndi-initialcontext"></a>設定 hello JNDI InitialContext
hello JNDI 環境設定將雜湊表的組態資訊傳遞至 hello javax.naming.InitialContext 類別 hello 建構函式。 hello 兩個必要的元素 hello 雜湊表中為 hello hello 初始內容 Factory 類別名稱和 hello 提供者 URL。 hello 下列程式碼會示範 tooconfigure hello JNDI 環境 toouse hello Qpid 屬性檔名為的內容檔案與所基礎的 JNDI 提供者**servicebus.properties**。

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>使用服務匯流排佇列的簡單 JMS 應用程式
hello 下列範例程式傳送 hello JNDI 邏輯佇列的名稱，與 JMS TextMessages tooa Service Bus 佇列和接收回 hello 訊息。

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a>執行 hello 應用程式
執行 hello 應用程式會產生 hello 形式的輸出：

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a>JMS 與 .NET 之間的跨平台訊息
本指南示範了如何 toosend 和從 Service Bus 使用 JMS 接收訊息 tooand。 不過，其中一個 hello 的 AMQP 1.0 的主要優點是它可讓應用程式 toobe 從不同語言撰寫，與訊息交換穩定且完整不失真的元件所建立。

使用上面所述的 hello 範例 JMS 應用程式和類似.NET 應用程式的相關文章，從[使用服務匯流排與 AMQP 1.0.net](service-bus-amqp-dotnet.md)，您可以交換.NET 和 Java 之間的訊息。 閱讀本文如需有關 hello 詳細資料的跨平台訊息使用服務匯流排與 AMQP 1.0。

### <a name="jms-toonet"></a>JMS too.NET
toodemonstrate JMS too.NET 傳訊：

* 啟動 hello.NET 範例應用程式沒有任何命令列引數。
* Hello Java 範例應用程式的開頭 hello"sendonly 」 命令列引數。 在此模式中，hello 應用程式不會從 hello 佇列接收訊息則才會傳送。
* 按**Enter**幾次在 hello Java 應用程式主控台中，這將會導致訊息 toobe 傳送。
* Hello.NET 應用程式接收這些訊息。

#### <a name="output-from-jms-application"></a>JMS 應用程式的輸出
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>.NET 應用程式的輸出
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>.NET tooJMS
toodemonstrate.NET tooJMS 傳訊：

* Hello.NET 範例應用程式的開頭 hello"sendonly 」 命令列引數。 在此模式中，hello 應用程式不會從 hello 佇列接收訊息則才會傳送。
* 啟動 hello Java 範例應用程式沒有任何命令列引數。
* 按**Enter**幾次在 hello.NET 應用程式主控台中，這將會導致訊息 toobe 傳送。
* Hello Java 應用程式接收這些訊息。

#### <a name="output-from-net-application"></a>.NET 應用程式的輸出
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>JMS 應用程式的輸出
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>不支援的功能和限制
也就使用服務匯流排與 AMQP 1.0 JMS 時，就會存在 hello 下列限制：

* 對於各個**工作階段**僅允許一個 **MessageProducer** 或 **MessageConsumer**。 如果您需要 toocreate 多個**MessageProducers**或**MessageConsumers**應用程式中，建立專用**工作階段**針對每一項。
* 目前不支援可變更的主題訂閱。
* 目前不支援 **MessageSelectors**。
* 暫時目的地;例如， **TemporaryQueue**， **TemporaryTopic**目前不支援，以及 hello **QueueRequestor**和**TopicRequestor**應用程式開發介面中使用它們。
* 不支援交易式工作階段和分散式交易。

## <a name="summary"></a>摘要
此方式 tooguide 示範了如何 toouse Service Bus 代理訊息功能 （佇列和發佈/訂閱主題） 從 Java 使用 hello 受歡迎的 JMS API 和 AMQP 1.0。

您也可以使用包括 .NET、C、Python 和 PHP 在內的其他語言所撰寫的 Service Bus AMQP 1.0。 使用這些不同的語言所建置的元件可以交換訊息，能夠可靠且完整不失真地使用服務匯流排中的 hello AMQP 1.0 支援。

## <a name="next-steps"></a>後續步驟
* [Azure 服務匯流排中的 AMQP 1.0 支援](service-bus-amqp-overview.md)
* [如何使用 toouse AMQP 1.0 hello 服務匯流排.NET API](service-bus-dotnet-advanced-message-queuing.md)
* [服務匯流排 AMQP 1.0 開發人員指南](service-bus-amqp-dotnet.md)
* [開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)
* [Java 開發人員中心](https://azure.microsoft.com/develop/java/)

