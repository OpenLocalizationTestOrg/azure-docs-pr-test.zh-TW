---
title: "使用 Java 的 Azure 事件中心 aaaReceive 事件 |Microsoft 文件"
description: "開始使用 Java 從事件中樞接收事件"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="68b49-103">使用 Java 從 Azure 事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="68b49-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="68b49-104">簡介</span><span class="sxs-lookup"><span data-stu-id="68b49-104">Introduction</span></span>
<span data-ttu-id="68b49-105">事件中心是可高度擴充擷取系統可以內嵌包含數百萬個事件每秒，讓應用程式 tooprocess 及分析 hello 連接的裝置和應用程式所產生的資料量很大。</span><span class="sxs-lookup"><span data-stu-id="68b49-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="68b49-106">收集到事件中樞後，您可以使用任何即時分析提供者或儲存體叢集轉換和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="68b49-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="68b49-107">如需詳細資訊，請參閱 hello[事件中心概觀][Event Hubs overview]。</span><span class="sxs-lookup"><span data-stu-id="68b49-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="68b49-108">本教學課程示範如何 tooreceive 事件到事件中心使用以 Java 撰寫的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="68b49-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68b49-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="68b49-109">Prerequisites</span></span>

<span data-ttu-id="68b49-110">在順序 toocomplete 本教學課程中，您需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="68b49-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="68b49-111">Java 開發環境。</span><span class="sxs-lookup"><span data-stu-id="68b49-111">A Java development environment.</span></span> <span data-ttu-id="68b49-112">針對本教學課程，我們採用 [Eclipse](https://www.eclipse.org/)。</span><span class="sxs-lookup"><span data-stu-id="68b49-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="68b49-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="68b49-113">An active Azure account.</span></span> <br/><span data-ttu-id="68b49-114">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="68b49-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="68b49-115">如需詳細資料，請參閱 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 免費試用</a>。</span><span class="sxs-lookup"><span data-stu-id="68b49-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="68b49-116">在 Java 中使用 EventProcessorHost 接收訊息</span><span class="sxs-lookup"><span data-stu-id="68b49-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="68b49-117">**EventProcessorHost** 是一個 Java 類別，透過管理持續檢查點以及來自事件中樞的平行接收，簡化來自事件中樞之事件的接收作業。</span><span class="sxs-lookup"><span data-stu-id="68b49-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="68b49-118">使用 EventProcessorHost，您可以將事件分割到多個接收者，即使裝載於不同的節點時也是一樣。</span><span class="sxs-lookup"><span data-stu-id="68b49-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="68b49-119">這個範例會示範如何為單一接收者 toouse EventProcessorHost。</span><span class="sxs-lookup"><span data-stu-id="68b49-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="68b49-120">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="68b49-120">Create a storage account</span></span>
<span data-ttu-id="68b49-121">您必須擁有 toouse EventProcessorHost， [Azure 儲存體帳戶][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="68b49-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="68b49-122">登入 toohello [Azure 入口網站][Azure portal]，然後按一下**+ 新增**左側 hello 囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="68b49-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="68b49-123">按一下 [儲存體]，然後按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="68b49-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="68b49-124">在 hello**建立儲存體帳戶**刀鋒視窗中，輸入 hello 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="68b49-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="68b49-125">完成 hello 其餘 hello 欄位，選取您想要的地區，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="68b49-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="68b49-126">按一下 hello 新建立的儲存體帳戶，然後再按一下**管理存取金鑰**:</span><span class="sxs-lookup"><span data-stu-id="68b49-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="68b49-127">將複製 hello 主要存取金鑰 tooa 暫存位置，toouse 稍後在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="68b49-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="68b49-128">建立 Java 專案使用 hello EventProcessor 主機</span><span class="sxs-lookup"><span data-stu-id="68b49-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="68b49-129">hello 事件中心的 Java 用戶端程式庫是可用於從 hello Maven 專案[Maven 中央儲存機制][Maven Package]，而且可以在 hello 內的相依性宣告之後參考您Maven 專案檔：</span><span class="sxs-lookup"><span data-stu-id="68b49-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="68b49-130">對於不同類型的建置環境，您可以明確地取得最新發行的 hello JAR 檔案從 hello [Maven 中央儲存機制][ Maven Package]或從[hello 發行發佈點上GitHub](https://github.com/Azure/azure-event-hubs/releases)。</span><span class="sxs-lookup"><span data-stu-id="68b49-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="68b49-131">Hello 遵循範例，先在您最愛的 Java 開發環境中建立新 Maven 專案主控台/shell 應用程式。</span><span class="sxs-lookup"><span data-stu-id="68b49-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="68b49-132">hello 類別稱為`ErrorNotificationHandler`。</span><span class="sxs-lookup"><span data-stu-id="68b49-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="68b49-133">使用 hello 下列程式碼會呼叫新的類別 toocreate `EventProcessor`。</span><span class="sxs-lookup"><span data-stu-id="68b49-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="68b49-134">建立一個更多的類別，稱為`EventProcessorSample`，並使用下列程式碼 hello。</span><span class="sxs-lookup"><span data-stu-id="68b49-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter toostop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="68b49-135">取代 hello 具備 hello 值建立 hello 事件中樞和儲存體帳戶時，使用下列欄位。</span><span class="sxs-lookup"><span data-stu-id="68b49-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="68b49-136">本教學課程使用單一 EventProcessorHost 執行個體。</span><span class="sxs-lookup"><span data-stu-id="68b49-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="68b49-137">tooincrease 輸送量，建議您執行多個執行個體的 EventProcessorHost，最好是在不同電腦上。</span><span class="sxs-lookup"><span data-stu-id="68b49-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="68b49-138">這麼做也會提供備援性。</span><span class="sxs-lookup"><span data-stu-id="68b49-138">This provides redundancy as well.</span></span> <span data-ttu-id="68b49-139">在這些情況下，不同執行個體自動彼此以協調順序 tooload 平衡 hello hello 接收到事件。</span><span class="sxs-lookup"><span data-stu-id="68b49-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="68b49-140">如果您想要多個接收者 tooeach 程序*所有*hello 事件，您必須使用 hello **ConsumerGroup**概念。</span><span class="sxs-lookup"><span data-stu-id="68b49-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="68b49-141">當從不同的電腦收到事件時，它可能有用 toospecify EventProcessorHost hello 機器 （或角色） 為基礎的執行個體名稱中所部署。</span><span class="sxs-lookup"><span data-stu-id="68b49-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="68b49-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68b49-142">Next steps</span></span>
<span data-ttu-id="68b49-143">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="68b49-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="68b49-144">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="68b49-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="68b49-145">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="68b49-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="68b49-146">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="68b49-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
