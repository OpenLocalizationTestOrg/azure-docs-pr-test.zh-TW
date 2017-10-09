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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="0ca88-103">如何 toouse hello Java 訊息服務 (JMS) API 服務匯流排與 AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="0ca88-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="0ca88-104">hello 進階訊息佇列通訊協定 (AMQP) 1.0 是一種有效率、 可靠、 有線等級訊息通訊協定，您可以使用 toobuild 強固且能跨平台訊息應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ca88-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="0ca88-105">表示您可以使用 hello 佇列和發佈/訂閱代理傳訊功能從某個範圍的平台使用有效率的二進位通訊協定的服務匯流排 AMQP 1.0 支援。</span><span class="sxs-lookup"><span data-stu-id="0ca88-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="0ca88-106">此外，您還可以建置使用混合語言、架構及作業系統所建置之元件所組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ca88-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="0ca88-107">本文說明如何 toouse 服務匯流排傳訊功能 （佇列和發佈/訂閱主題） 使用的 Java 應用程式從 hello 熱門 Java 訊息服務 (JMS) API 的標準。</span><span class="sxs-lookup"><span data-stu-id="0ca88-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="0ca88-108">沒有[同系列文章](service-bus-amqp-dotnet.md)，說明如何 toodo hello 相同使用 hello 服務匯流排.NET API。</span><span class="sxs-lookup"><span data-stu-id="0ca88-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="0ca88-109">您可以使用下列兩個指南一起 toolearn 關於跨平台訊息使用 AMQP 1.0。</span><span class="sxs-lookup"><span data-stu-id="0ca88-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="0ca88-110">開始使用服務匯流排</span><span class="sxs-lookup"><span data-stu-id="0ca88-110">Get started with Service Bus</span></span>
<span data-ttu-id="0ca88-111">本指南假設您已經有服務匯流排命名空間，其中包含名稱為 **queue1** 的佇列。</span><span class="sxs-lookup"><span data-stu-id="0ca88-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="0ca88-112">如果您不這麼做，則您可以[建立 hello 命名空間與佇列](service-bus-create-namespace-portal.md)使用 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="0ca88-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0ca88-113">如需有關如何 toocreate 服務匯流排命名空間和佇列，請參閱[開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="0ca88-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0ca88-114">分割的佇列和主題也支援 AMQP。</span><span class="sxs-lookup"><span data-stu-id="0ca88-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="0ca88-115">如需詳細資訊，請參閱[分割傳訊實體](service-bus-partitioning.md)及[服務匯流排分割佇列和主題的 AMQP 1.0 支援](service-bus-partitioned-queues-and-topics-amqp-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0ca88-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="0ca88-116">下載 hello AMQP 1.0 JMS 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="0ca88-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="0ca88-117">其中 toodownload hello hello Apache Qpid JMS AMQP 1.0 用戶端程式庫的最新版本的相關資訊，請瀏覽[https://qpid.apache.org/download.html](https://qpid.apache.org/download.html)。</span><span class="sxs-lookup"><span data-stu-id="0ca88-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="0ca88-118">您必須新增 hello hello Apache Qpid JMS AMQP 1.0 發佈封存 toohello Java CLASSPATH 中的下列四個 JAR 檔案，建置和執行 JMS 應用程式與服務匯流排時：</span><span class="sxs-lookup"><span data-stu-id="0ca88-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="0ca88-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="0ca88-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="0ca88-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="0ca88-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="0ca88-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="0ca88-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="0ca88-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="0ca88-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="0ca88-123">編寫 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="0ca88-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="0ca88-124">Java 命名及目錄介面 (JNDI)</span><span class="sxs-lookup"><span data-stu-id="0ca88-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="0ca88-125">JMS 使用 hello Java Naming and Directory Interface (JNDI) toocreate 的區隔邏輯名稱和實體名稱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="0ca88-126">使用 JNDI 可以解析兩種 JMS 物件：ConnectionFactory 和 Destination。</span><span class="sxs-lookup"><span data-stu-id="0ca88-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="0ca88-127">JNDI 使用提供者模型，您可以在其中插入不同的目錄服務 toohandle 名稱解析責任。</span><span class="sxs-lookup"><span data-stu-id="0ca88-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="0ca88-128">hello Apache Qpid JMS AMQP 1.0 程式庫隨附一個以簡單屬性以檔案為基礎 JNDI 提供者所設定使用內容檔的 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="0ca88-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

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

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="0ca88-129">設定 hello ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="0ca88-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="0ca88-130">hello 用項目的 toodefine **ConnectionFactory**在 hello Qpid 屬性檔 JNDI 提供者是下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="0ca88-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="0ca88-131">其中**[jndi_name]**和**[ConnectionURL]**具有下列意義 hello:</span><span class="sxs-lookup"><span data-stu-id="0ca88-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="0ca88-132">**[jndi_name]**: hello 的 hello ConnectionFactory 的邏輯名稱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="0ca88-133">這是將解決 hello 使用 hello JNDI Intialcontext.lookup （） 方法的 Java 應用程式中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="0ca88-134">**[ConnectionURL]**: Hello 的相關資訊提供給 hello JMS 程式庫的 URL 需要 toohello AMQP 代理人。</span><span class="sxs-lookup"><span data-stu-id="0ca88-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="0ca88-135">hello hello 格式**ConnectionURL**如下所示：</span><span class="sxs-lookup"><span data-stu-id="0ca88-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="0ca88-136">其中**[命名空間]**， **[SASPolicyName]**和**[SASPolicyKey]**具有下列意義 hello:</span><span class="sxs-lookup"><span data-stu-id="0ca88-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="0ca88-137">**[命名空間]**: hello 服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="0ca88-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="0ca88-138">**[SASPolicyName]**: hello 佇列共用存取簽章原則名稱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="0ca88-139">**[SASPolicyKey]**: hello 佇列共用存取簽章原則機碼。</span><span class="sxs-lookup"><span data-stu-id="0ca88-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="0ca88-140">您必須手動進行 URL 編碼 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0ca88-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="0ca88-141">[http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp) 中提供實用的 URL 編碼公用程式。</span><span class="sxs-lookup"><span data-stu-id="0ca88-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="0ca88-142">設定目的地</span><span class="sxs-lookup"><span data-stu-id="0ca88-142">Configure destinations</span></span>
<span data-ttu-id="0ca88-143">使用的 toodefine hello Qpid 屬性檔 JNDI 提供者中的目的地是下列格式的 hello hello 項目：</span><span class="sxs-lookup"><span data-stu-id="0ca88-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="0ca88-144">或</span><span class="sxs-lookup"><span data-stu-id="0ca88-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="0ca88-145">其中**[jndi\_名稱]**和**[實體\_名稱]**具有下列意義 hello:</span><span class="sxs-lookup"><span data-stu-id="0ca88-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="0ca88-146">**[jndi_name]**: hello 的 hello 目的地的邏輯名稱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="0ca88-147">這是將解決 hello 使用 hello JNDI Intialcontext.lookup （） 方法的 Java 應用程式中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="0ca88-148">**[physical_name]**: hello 名稱 hello 服務匯流排實體 toowhich hello 應用程式傳送或接收訊息。</span><span class="sxs-lookup"><span data-stu-id="0ca88-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="0ca88-149">接收來自服務匯流排主題訂用帳戶，在 JNDI 中指定的 hello 實體名稱應該 hello hello 主題名稱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="0ca88-150">hello JMS 應用程式程式碼中建立 hello 持久的訂用帳戶時，會提供 hello 訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="0ca88-151">hello[服務匯流排 AMQP 1.0 開發人員手冊 》](service-bus-amqp-dotnet.md)上使用來自 JMS 的服務匯流排主題提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0ca88-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="0ca88-152">撰寫 hello JMS 應用程式</span><span class="sxs-lookup"><span data-stu-id="0ca88-152">Write hello JMS application</span></span>
<span data-ttu-id="0ca88-153">對於服務匯流排使用 JMS 時，不需要特別 API 或選項。</span><span class="sxs-lookup"><span data-stu-id="0ca88-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="0ca88-154">不過，後續將說明一些限制。</span><span class="sxs-lookup"><span data-stu-id="0ca88-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="0ca88-155">任何 JMS 應用程式中，首先需要 hello 是 hello JNDI 環境 toobe 無法 tooresolve 組態**ConnectionFactory**和目的地。</span><span class="sxs-lookup"><span data-stu-id="0ca88-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="0ca88-156">設定 hello JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="0ca88-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="0ca88-157">hello JNDI 環境設定將雜湊表的組態資訊傳遞至 hello javax.naming.InitialContext 類別 hello 建構函式。</span><span class="sxs-lookup"><span data-stu-id="0ca88-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="0ca88-158">hello 兩個必要的元素 hello 雜湊表中為 hello hello 初始內容 Factory 類別名稱和 hello 提供者 URL。</span><span class="sxs-lookup"><span data-stu-id="0ca88-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="0ca88-159">hello 下列程式碼會示範 tooconfigure hello JNDI 環境 toouse hello Qpid 屬性檔名為的內容檔案與所基礎的 JNDI 提供者**servicebus.properties**。</span><span class="sxs-lookup"><span data-stu-id="0ca88-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="0ca88-160">使用服務匯流排佇列的簡單 JMS 應用程式</span><span class="sxs-lookup"><span data-stu-id="0ca88-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="0ca88-161">hello 下列範例程式傳送 hello JNDI 邏輯佇列的名稱，與 JMS TextMessages tooa Service Bus 佇列和接收回 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="0ca88-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

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

### <a name="run-hello-application"></a><span data-ttu-id="0ca88-162">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0ca88-162">Run hello application</span></span>
<span data-ttu-id="0ca88-163">執行 hello 應用程式會產生 hello 形式的輸出：</span><span class="sxs-lookup"><span data-stu-id="0ca88-163">Running hello application produces output of hello form:</span></span>

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

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="0ca88-164">JMS 與 .NET 之間的跨平台訊息</span><span class="sxs-lookup"><span data-stu-id="0ca88-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="0ca88-165">本指南示範了如何 toosend 和從 Service Bus 使用 JMS 接收訊息 tooand。</span><span class="sxs-lookup"><span data-stu-id="0ca88-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="0ca88-166">不過，其中一個 hello 的 AMQP 1.0 的主要優點是它可讓應用程式 toobe 從不同語言撰寫，與訊息交換穩定且完整不失真的元件所建立。</span><span class="sxs-lookup"><span data-stu-id="0ca88-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="0ca88-167">使用上面所述的 hello 範例 JMS 應用程式和類似.NET 應用程式的相關文章，從[使用服務匯流排與 AMQP 1.0.net](service-bus-amqp-dotnet.md)，您可以交換.NET 和 Java 之間的訊息。</span><span class="sxs-lookup"><span data-stu-id="0ca88-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="0ca88-168">閱讀本文如需有關 hello 詳細資料的跨平台訊息使用服務匯流排與 AMQP 1.0。</span><span class="sxs-lookup"><span data-stu-id="0ca88-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="0ca88-169">JMS too.NET</span><span class="sxs-lookup"><span data-stu-id="0ca88-169">JMS too.NET</span></span>
<span data-ttu-id="0ca88-170">toodemonstrate JMS too.NET 傳訊：</span><span class="sxs-lookup"><span data-stu-id="0ca88-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="0ca88-171">啟動 hello.NET 範例應用程式沒有任何命令列引數。</span><span class="sxs-lookup"><span data-stu-id="0ca88-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="0ca88-172">Hello Java 範例應用程式的開頭 hello"sendonly 」 命令列引數。</span><span class="sxs-lookup"><span data-stu-id="0ca88-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="0ca88-173">在此模式中，hello 應用程式不會從 hello 佇列接收訊息則才會傳送。</span><span class="sxs-lookup"><span data-stu-id="0ca88-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="0ca88-174">按**Enter**幾次在 hello Java 應用程式主控台中，這將會導致訊息 toobe 傳送。</span><span class="sxs-lookup"><span data-stu-id="0ca88-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="0ca88-175">Hello.NET 應用程式接收這些訊息。</span><span class="sxs-lookup"><span data-stu-id="0ca88-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="0ca88-176">JMS 應用程式的輸出</span><span class="sxs-lookup"><span data-stu-id="0ca88-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="0ca88-177">.NET 應用程式的輸出</span><span class="sxs-lookup"><span data-stu-id="0ca88-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="0ca88-178">.NET tooJMS</span><span class="sxs-lookup"><span data-stu-id="0ca88-178">.NET tooJMS</span></span>
<span data-ttu-id="0ca88-179">toodemonstrate.NET tooJMS 傳訊：</span><span class="sxs-lookup"><span data-stu-id="0ca88-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="0ca88-180">Hello.NET 範例應用程式的開頭 hello"sendonly 」 命令列引數。</span><span class="sxs-lookup"><span data-stu-id="0ca88-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="0ca88-181">在此模式中，hello 應用程式不會從 hello 佇列接收訊息則才會傳送。</span><span class="sxs-lookup"><span data-stu-id="0ca88-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="0ca88-182">啟動 hello Java 範例應用程式沒有任何命令列引數。</span><span class="sxs-lookup"><span data-stu-id="0ca88-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="0ca88-183">按**Enter**幾次在 hello.NET 應用程式主控台中，這將會導致訊息 toobe 傳送。</span><span class="sxs-lookup"><span data-stu-id="0ca88-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="0ca88-184">Hello Java 應用程式接收這些訊息。</span><span class="sxs-lookup"><span data-stu-id="0ca88-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="0ca88-185">.NET 應用程式的輸出</span><span class="sxs-lookup"><span data-stu-id="0ca88-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="0ca88-186">JMS 應用程式的輸出</span><span class="sxs-lookup"><span data-stu-id="0ca88-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="0ca88-187">不支援的功能和限制</span><span class="sxs-lookup"><span data-stu-id="0ca88-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="0ca88-188">也就使用服務匯流排與 AMQP 1.0 JMS 時，就會存在 hello 下列限制：</span><span class="sxs-lookup"><span data-stu-id="0ca88-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="0ca88-189">對於各個**工作階段**僅允許一個 **MessageProducer** 或 **MessageConsumer**。</span><span class="sxs-lookup"><span data-stu-id="0ca88-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="0ca88-190">如果您需要 toocreate 多個**MessageProducers**或**MessageConsumers**應用程式中，建立專用**工作階段**針對每一項。</span><span class="sxs-lookup"><span data-stu-id="0ca88-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="0ca88-191">目前不支援可變更的主題訂閱。</span><span class="sxs-lookup"><span data-stu-id="0ca88-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="0ca88-192">目前不支援 **MessageSelectors**。</span><span class="sxs-lookup"><span data-stu-id="0ca88-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="0ca88-193">暫時目的地;例如， **TemporaryQueue**， **TemporaryTopic**目前不支援，以及 hello **QueueRequestor**和**TopicRequestor**應用程式開發介面中使用它們。</span><span class="sxs-lookup"><span data-stu-id="0ca88-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="0ca88-194">不支援交易式工作階段和分散式交易。</span><span class="sxs-lookup"><span data-stu-id="0ca88-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="0ca88-195">摘要</span><span class="sxs-lookup"><span data-stu-id="0ca88-195">Summary</span></span>
<span data-ttu-id="0ca88-196">此方式 tooguide 示範了如何 toouse Service Bus 代理訊息功能 （佇列和發佈/訂閱主題） 從 Java 使用 hello 受歡迎的 JMS API 和 AMQP 1.0。</span><span class="sxs-lookup"><span data-stu-id="0ca88-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="0ca88-197">您也可以使用包括 .NET、C、Python 和 PHP 在內的其他語言所撰寫的 Service Bus AMQP 1.0。</span><span class="sxs-lookup"><span data-stu-id="0ca88-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="0ca88-198">使用這些不同的語言所建置的元件可以交換訊息，能夠可靠且完整不失真地使用服務匯流排中的 hello AMQP 1.0 支援。</span><span class="sxs-lookup"><span data-stu-id="0ca88-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ca88-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ca88-199">Next steps</span></span>
* [<span data-ttu-id="0ca88-200">Azure 服務匯流排中的 AMQP 1.0 支援</span><span class="sxs-lookup"><span data-stu-id="0ca88-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="0ca88-201">如何使用 toouse AMQP 1.0 hello 服務匯流排.NET API</span><span class="sxs-lookup"><span data-stu-id="0ca88-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="0ca88-202">服務匯流排 AMQP 1.0 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="0ca88-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="0ca88-203">開始使用服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="0ca88-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="0ca88-204">Java 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="0ca88-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

