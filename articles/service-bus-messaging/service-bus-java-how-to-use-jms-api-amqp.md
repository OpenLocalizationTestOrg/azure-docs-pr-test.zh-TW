---
title: "如何使用 AMQP 1.0 與 Java 服務匯流排 API 搭配 | Microsoft Docs"
description: "如何搭配 Azure 服務匯流排和 Advanced Message Queuing Protodol (AMQP) 1.0 使用 Java Message Service (JMS)。"
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="366a1-103">如何搭配使用 Java 訊息服務 (JMS) API 與服務匯流排和 AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="366a1-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="366a1-104">進階訊息佇列通訊協定 (AMQP) 1.0 是一個有效率且可靠的有線等級訊息通訊協定，可以用來建置強大的跨平台訊息應用程式。</span><span class="sxs-lookup"><span data-stu-id="366a1-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="366a1-105">在服務匯流排中支援 AMQP 1.0 代表您現在能夠從一組平台中使用有效率的二進位通訊協定，來運用佇列與發佈/訂閱代理傳訊功能。</span><span class="sxs-lookup"><span data-stu-id="366a1-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="366a1-106">此外，您還可以建置使用混合語言、架構及作業系統所建置之元件所組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="366a1-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="366a1-107">本文說明如何利用常用的 Java 訊息服務 (JMS) API 標準，從 Java 應用程式使用服務匯流排傳訊功能 (佇列和發佈/訂閱主題)。</span><span class="sxs-lookup"><span data-stu-id="366a1-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="366a1-108">這是說明如何使用服務匯流排 .NET API 達到相同效用的[附屬文章](service-bus-amqp-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="366a1-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="366a1-109">您可以同時使用這兩個指南了解使用 AMQP 1.0 的跨平台訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="366a1-110">開始使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="366a1-110">Get started with Service Bus</span></span>
<span data-ttu-id="366a1-111">本指南假設您已經有服務匯流排命名空間，其中包含名稱為 **queue1** 的佇列。</span><span class="sxs-lookup"><span data-stu-id="366a1-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="366a1-112">如果沒有，您可以使用 [Azure 入口網站](service-bus-create-namespace-portal.md)建立[命名空間和佇列](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="366a1-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="366a1-113">如需有關如何建立服務匯流排命名空間和佇列的相關詳細資訊，請參閱[開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="366a1-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="366a1-114">分割的佇列和主題也支援 AMQP。</span><span class="sxs-lookup"><span data-stu-id="366a1-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="366a1-115">如需詳細資訊，請參閱[分割傳訊實體](service-bus-partitioning.md)及[服務匯流排分割佇列和主題的 AMQP 1.0 支援](service-bus-partitioned-queues-and-topics-amqp-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="366a1-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="366a1-116">下載 AMQP 1.0 JMS 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="366a1-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="366a1-117">如需可從哪裡下載最新版 Apache Qpid JMS AMQP 1.0 用戶端程式庫的相關資訊，請造訪 [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html)。</span><span class="sxs-lookup"><span data-stu-id="366a1-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="366a1-118">您使用服務匯流排建立和執行 JMS 應用程式時，必須從 Apache Qpid JMS AMQP 1.0 散發封裝將下列 4 個 JAR 檔加入 Java CLASSPATH：</span><span class="sxs-lookup"><span data-stu-id="366a1-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="366a1-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="366a1-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="366a1-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="366a1-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="366a1-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="366a1-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="366a1-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="366a1-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="366a1-123">編寫 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="366a1-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="366a1-124">Java 命名及目錄介面 (JNDI)</span><span class="sxs-lookup"><span data-stu-id="366a1-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="366a1-125">JMS 使用 Java 命名及目錄介面 (JNDI) 建立邏輯名稱與實際名稱之間的區別。</span><span class="sxs-lookup"><span data-stu-id="366a1-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="366a1-126">使用 JNDI 可以解析兩種 JMS 物件：ConnectionFactory 和 Destination。</span><span class="sxs-lookup"><span data-stu-id="366a1-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="366a1-127">JNDI 使用提供者模型，您可以在其中插入不同的目錄服務處理名稱解析作業。</span><span class="sxs-lookup"><span data-stu-id="366a1-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="366a1-128">Apache Qpid JMS AMQP 1.0 程式庫提供使用下列格式的內容檔案設定的簡單內容檔案型 JNDI 提供者：</span><span class="sxs-lookup"><span data-stu-id="366a1-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="366a1-129">設定 ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="366a1-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="366a1-130">在 Qpid 屬性檔案 JNDI 提供者中用來定義 **ConnectionFactory** 的項目使用下列格式：</span><span class="sxs-lookup"><span data-stu-id="366a1-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="366a1-131">其中 **[jndi_name]** 及 **[ConnectionURL]** 具有下列意義：</span><span class="sxs-lookup"><span data-stu-id="366a1-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="366a1-132">**[jndi_name]**：ConnectionFactory 的邏輯名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="366a1-133">這是使用 JNDI IntialContext.lookup() 方法在 Java 應用程式中解析的名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="366a1-134">**[ConnectionURL]**：將包含所需資訊的 JMS 程式庫提供給 AMQP 訊息代理程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="366a1-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="366a1-135">**ConnectionURL** 的格式如下：</span><span class="sxs-lookup"><span data-stu-id="366a1-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="366a1-136">其中 **[namespace]**、**[SASPolicyName]** 和 **[SASPolicyKey]** 具有下列意義：</span><span class="sxs-lookup"><span data-stu-id="366a1-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="366a1-137">**[namespace]**：服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="366a1-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="366a1-138">**[SASPolicyName]**：佇列共用存取簽章原則名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="366a1-139">**[SASPolicyKey]**：佇列共用存取簽章原則金鑰。</span><span class="sxs-lookup"><span data-stu-id="366a1-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="366a1-140">您必須手動使用 URL 將密碼編碼。</span><span class="sxs-lookup"><span data-stu-id="366a1-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="366a1-141">[http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp) 中提供實用的 URL 編碼公用程式。</span><span class="sxs-lookup"><span data-stu-id="366a1-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="366a1-142">設定目的地</span><span class="sxs-lookup"><span data-stu-id="366a1-142">Configure destinations</span></span>
<span data-ttu-id="366a1-143">在 Qpid 屬性檔案 JNDI 提供者中用來定義目的地的項目使用下列格式：</span><span class="sxs-lookup"><span data-stu-id="366a1-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="366a1-144">或</span><span class="sxs-lookup"><span data-stu-id="366a1-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="366a1-145">其中 **[jndi\_name]** 及 **[physical\_name]** 具有下列意義：</span><span class="sxs-lookup"><span data-stu-id="366a1-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="366a1-146">**[jndi_name]**：目的地的邏輯名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="366a1-147">這是使用 JNDI IntialContext.lookup() 方法在 Java 應用程式中解析的名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="366a1-148">**[physical_name]**：應用程式傳送或接收訊息的服務匯流排實體名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="366a1-149">從服務匯流排主題訂用帳戶收到在 JNDI 中指定的實體名稱應該是主題的名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="366a1-150">以 JMS 應用程式程式碼建立持續性訂用帳戶時，將建立訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="366a1-151">[服務匯流排 AMQP 1.0 開發人員指南](service-bus-amqp-dotnet.md)提供處理 JMS 服務匯流排主題的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="366a1-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="366a1-152">撰寫 JMS 應用程式</span><span class="sxs-lookup"><span data-stu-id="366a1-152">Write the JMS application</span></span>
<span data-ttu-id="366a1-153">對於服務匯流排使用 JMS 時，不需要特別 API 或選項。</span><span class="sxs-lookup"><span data-stu-id="366a1-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="366a1-154">不過，後續將說明一些限制。</span><span class="sxs-lookup"><span data-stu-id="366a1-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="366a1-155">和任何 JMS 應用程式一樣，首先需要設定 JNDI 環境，才能夠解析 **ConnectionFactory** 和目的地。</span><span class="sxs-lookup"><span data-stu-id="366a1-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="366a1-156">設定 JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="366a1-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="366a1-157">將組態資訊的雜湊表傳遞到 javax.naming.InitialContext 類別的建構函式，將設定 JNDI 環境。</span><span class="sxs-lookup"><span data-stu-id="366a1-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="366a1-158">雜湊表中的兩個所需項目是 Initial Context Factory 和 Provider URL 的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="366a1-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="366a1-159">下列程式碼顯示如何使用名稱為 **servicebus.properties** 的內容檔案，設定 JNDI 環境使用 Qpid 內容檔案型 JNDI 提供者。</span><span class="sxs-lookup"><span data-stu-id="366a1-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="366a1-160">使用服務匯流排佇列的簡單 JMS 應用程式</span><span class="sxs-lookup"><span data-stu-id="366a1-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="366a1-161">下列範例程式將 JMS TextMessages 傳送到 JNDI 邏輯名稱為 QUEUE 的服務匯流排佇列，並收到傳回的訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="366a1-162">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="366a1-162">Run the application</span></span>
<span data-ttu-id="366a1-163">執行應用程式將產生表單的輸出：</span><span class="sxs-lookup"><span data-stu-id="366a1-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="366a1-164">JMS 與 .NET 之間的跨平台訊息</span><span class="sxs-lookup"><span data-stu-id="366a1-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="366a1-165">本指南說明使用 JMS 傳送和接收服務匯流排的訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="366a1-166">不過，AMQP 1.0 的其中一個主要優點是能夠從不同語言撰寫的元件建立應用程式，並確實完整交換訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="366a1-167">使用上述的範例 JMS 應用程式和取自隨附文章[搭配使用 .NET 的服務匯流排與 AMQP 1.0](service-bus-amqp-dotnet.md) 的類似 .NET 應用程式，即可交換 .NET 與 Java 之間的訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="366a1-168">如需使用服務匯流排與 AMQP 1.0 傳送跨平台訊息的詳細資訊，請參閱本文。</span><span class="sxs-lookup"><span data-stu-id="366a1-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="366a1-169">JMS 到 .NET</span><span class="sxs-lookup"><span data-stu-id="366a1-169">JMS to .NET</span></span>
<span data-ttu-id="366a1-170">示範 JMS 到 .NET 的訊息：</span><span class="sxs-lookup"><span data-stu-id="366a1-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="366a1-171">不使用任何命令列引數啟動 .NET 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="366a1-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="366a1-172">使用「sendonly」命令列引數啟動 Java 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="366a1-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="366a1-173">在此模式中，應用程式將不會接收來自佇列的訊息，它只會傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="366a1-174">在 Java 應用程式主控台多次按下 **Enter** 鍵，這將傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="366a1-175">這些訊息將由 .NET 應用程式所接收。</span><span class="sxs-lookup"><span data-stu-id="366a1-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="366a1-176">JMS 應用程式的輸出</span><span class="sxs-lookup"><span data-stu-id="366a1-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="366a1-177">.NET 應用程式的輸出</span><span class="sxs-lookup"><span data-stu-id="366a1-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="366a1-178">.NET 到 JMS</span><span class="sxs-lookup"><span data-stu-id="366a1-178">.NET to JMS</span></span>
<span data-ttu-id="366a1-179">示範從 .NET 到 JMS 的傳訊操作：</span><span class="sxs-lookup"><span data-stu-id="366a1-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="366a1-180">使用「sendonly」命令列引數啟動 .NET 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="366a1-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="366a1-181">在此模式中，應用程式將不會接收來自佇列的訊息，它只會傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="366a1-182">不使用任何命令列引數啟動 Java 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="366a1-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="366a1-183">在 .NET 應用程式主控台多次按下 **Enter** 鍵，這將傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="366a1-184">這些訊息將由 Java 應用程式所接收。</span><span class="sxs-lookup"><span data-stu-id="366a1-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="366a1-185">.NET 應用程式的輸出</span><span class="sxs-lookup"><span data-stu-id="366a1-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="366a1-186">JMS 應用程式的輸出</span><span class="sxs-lookup"><span data-stu-id="366a1-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="366a1-187">不支援的功能和限制</span><span class="sxs-lookup"><span data-stu-id="366a1-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="366a1-188">對於服務匯流排使用 JMS 而不使用 AMQP 1.0 會有下列限制：</span><span class="sxs-lookup"><span data-stu-id="366a1-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="366a1-189">對於各個**工作階段**僅允許一個 **MessageProducer** 或 **MessageConsumer**。</span><span class="sxs-lookup"><span data-stu-id="366a1-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="366a1-190">如果您需要在應用程式中建立多個 **MessageProducers** 或 **MessageConsumers**，請分別建立專用的**工作階段**。</span><span class="sxs-lookup"><span data-stu-id="366a1-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="366a1-191">目前不支援可變更的主題訂閱。</span><span class="sxs-lookup"><span data-stu-id="366a1-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="366a1-192">目前不支援 **MessageSelectors**。</span><span class="sxs-lookup"><span data-stu-id="366a1-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="366a1-193">目前不支援 **TemporaryQueue** 和 **TemporaryTopic** 這些暫時目的地，也不支援用到這些目的地的 **QueueRequestor** 和 **TopicRequestor** API。</span><span class="sxs-lookup"><span data-stu-id="366a1-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="366a1-194">不支援交易式工作階段和分散式交易。</span><span class="sxs-lookup"><span data-stu-id="366a1-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="366a1-195">摘要</span><span class="sxs-lookup"><span data-stu-id="366a1-195">Summary</span></span>
<span data-ttu-id="366a1-196">本作法指南說明如何以常用的 JMS API 和 AMQP 1.0 從 Java 使用服務匯流排代理訊息功能 (佇列和發佈/訂閱主題)。</span><span class="sxs-lookup"><span data-stu-id="366a1-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="366a1-197">您也可以使用包括 .NET、C、Python 和 PHP 在內的其他語言所撰寫的 Service Bus AMQP 1.0。</span><span class="sxs-lookup"><span data-stu-id="366a1-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="366a1-198">使用這些不同的語言撰寫的元件可使用服務匯流排中的 AMQP 1.0 支援確實完整交換訊息。</span><span class="sxs-lookup"><span data-stu-id="366a1-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="366a1-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="366a1-199">Next steps</span></span>
* [<span data-ttu-id="366a1-200">Azure 服務匯流排中的 AMQP 1.0 支援</span><span class="sxs-lookup"><span data-stu-id="366a1-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="366a1-201">如何透過服務匯流排 .NET API 使用 AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="366a1-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="366a1-202">服務匯流排 AMQP 1.0 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="366a1-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="366a1-203">開始使用服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="366a1-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="366a1-204">Java 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="366a1-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

