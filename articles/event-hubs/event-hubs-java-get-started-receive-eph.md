---
title: "使用 Java 從 Azure 事件中樞接收事件 | Microsoft Docs"
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
ms.openlocfilehash: 3c1b455e6298367dc50f0943b58f6cf1e7f1c5fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="ccee7-103">使用 Java 從 Azure 事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="ccee7-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="ccee7-104">簡介</span><span class="sxs-lookup"><span data-stu-id="ccee7-104">Introduction</span></span>
<span data-ttu-id="ccee7-105">事件中樞是高度可擴充的擷取系統，每秒可擷取數百萬個事件，讓應用程式能處理並分析已連線裝置與應用程式產生的大量資料。</span><span class="sxs-lookup"><span data-stu-id="ccee7-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="ccee7-106">收集到事件中樞後，您可以使用任何即時分析提供者或儲存體叢集轉換和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ccee7-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="ccee7-107">如需詳細資訊，請參閱 [事件中樞概觀][Event Hubs overview]。</span><span class="sxs-lookup"><span data-stu-id="ccee7-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="ccee7-108">本教學課程也會示範如何使用以 Java 撰寫的主控台應用程式，將事件接收到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ccee7-108">This tutorial shows how to receive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccee7-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="ccee7-109">Prerequisites</span></span>

<span data-ttu-id="ccee7-110">若要完成本教學課程，您需要下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="ccee7-110">In order to complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="ccee7-111">Java 開發環境。</span><span class="sxs-lookup"><span data-stu-id="ccee7-111">A Java development environment.</span></span> <span data-ttu-id="ccee7-112">針對本教學課程，我們採用 [Eclipse](https://www.eclipse.org/)。</span><span class="sxs-lookup"><span data-stu-id="ccee7-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="ccee7-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccee7-113">An active Azure account.</span></span> <br/><span data-ttu-id="ccee7-114">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccee7-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="ccee7-115">如需詳細資料，請參閱 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 免費試用</a>。</span><span class="sxs-lookup"><span data-stu-id="ccee7-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="ccee7-116">在 Java 中使用 EventProcessorHost 接收訊息</span><span class="sxs-lookup"><span data-stu-id="ccee7-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="ccee7-117">**EventProcessorHost** 是一個 Java 類別，透過管理持續檢查點以及來自事件中樞的平行接收，簡化來自事件中樞之事件的接收作業。</span><span class="sxs-lookup"><span data-stu-id="ccee7-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="ccee7-118">使用 EventProcessorHost，您可以將事件分割到多個接收者，即使裝載於不同的節點時也是一樣。</span><span class="sxs-lookup"><span data-stu-id="ccee7-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="ccee7-119">這個範例顯示單一接收者如何使用 EventProcessorHost。</span><span class="sxs-lookup"><span data-stu-id="ccee7-119">This example shows how to use EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="ccee7-120">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ccee7-120">Create a storage account</span></span>
<span data-ttu-id="ccee7-121">若要使用 EventProcessorHost，您必須擁有 [Azure 儲存體帳戶][Azure Storage account]：</span><span class="sxs-lookup"><span data-stu-id="ccee7-121">To use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="ccee7-122">登入 [Azure 入口網站][Azure portal]，然後按一下畫面左上方的 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="ccee7-122">Log on to the [Azure portal][Azure portal], and click **+ New** on the left-hand side of the screen.</span></span>
2. <span data-ttu-id="ccee7-123">按一下 [儲存體]，然後按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="ccee7-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="ccee7-124">在 [建立儲存體帳戶] 刀鋒視窗中，輸入儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ccee7-124">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="ccee7-125">完成其餘欄位，選取您想要的區域，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ccee7-125">Complete the rest of the fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="ccee7-126">按一下新建立的儲存體帳戶，然後按一下 [ **管理存取金鑰**]：</span><span class="sxs-lookup"><span data-stu-id="ccee7-126">Click the newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="ccee7-127">將主要存取金鑰複製到暫存位置，以便稍後在此教學課程中使用。</span><span class="sxs-lookup"><span data-stu-id="ccee7-127">Copy the primary access key to a temporary location, to use later in this tutorial.</span></span>

### <a name="create-a-java-project-using-the-eventprocessor-host"></a><span data-ttu-id="ccee7-128">使用 EventProcessor 主機建立 Java 專案</span><span class="sxs-lookup"><span data-stu-id="ccee7-128">Create a Java project using the EventProcessor Host</span></span>
<span data-ttu-id="ccee7-129">適用於事件中樞的 Java 用戶端程式庫可以在來自 [Maven 中央儲存機制][Maven Package]的 Maven 專案中使用，而且可在您的 Maven 專案檔內使用下列相依性宣告來參考：</span><span class="sxs-lookup"><span data-stu-id="ccee7-129">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

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

<span data-ttu-id="ccee7-130">對於不同類型的組建環境，您可以明確地從 [Maven 中央儲存機制][Maven Package]或 [GitHub 上的版本發佈點](https://github.com/Azure/azure-event-hubs/releases)取得最新發行的 JAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="ccee7-130">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="ccee7-131">針對下列範例，在您最喜愛的 Java 開發環境中，先為主控台/殼層應用程式建立新的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="ccee7-131">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="ccee7-132">類別稱為 `ErrorNotificationHandler`。</span><span class="sxs-lookup"><span data-stu-id="ccee7-132">The class is called `ErrorNotificationHandler`.</span></span>     
   
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
2. <span data-ttu-id="ccee7-133">使用下列程式碼，建立名為 `EventProcessor`的新類別。</span><span class="sxs-lookup"><span data-stu-id="ccee7-133">Use the following code to create a new class called `EventProcessor`.</span></span>
   
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
3. <span data-ttu-id="ccee7-134">使用下列程式碼，再建立一個名為 `EventProcessorSample` 的類別。</span><span class="sxs-lookup"><span data-stu-id="ccee7-134">Create one more class called `EventProcessorSample`, using the following code.</span></span>
   
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
   
            System.out.println("Press enter to stop");
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
4. <span data-ttu-id="ccee7-135">使用您建立事件中樞和儲存體帳戶時所用的值，取代下列欄位。</span><span class="sxs-lookup"><span data-stu-id="ccee7-135">Replace the following fields with the values used when you created the event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="ccee7-136">本教學課程使用單一 EventProcessorHost 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ccee7-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="ccee7-137">若要增加輸送量，建議您執行多個 EventProcessorHost 執行個體 (最好能在個別的機器上)。</span><span class="sxs-lookup"><span data-stu-id="ccee7-137">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="ccee7-138">這麼做也會提供備援性。</span><span class="sxs-lookup"><span data-stu-id="ccee7-138">This provides redundancy as well.</span></span> <span data-ttu-id="ccee7-139">在這些情況下，各種執行個體會自動彼此協調以對已接收的事件進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="ccee7-139">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span></span> <span data-ttu-id="ccee7-140">如果您想要多個接收者都處理 *所有* 事件，則必須使用 **ConsumerGroup** 概念。</span><span class="sxs-lookup"><span data-stu-id="ccee7-140">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="ccee7-141">收到來自不同電腦的事件時，根據在其中執行 EventProcessorHost 執行個體的電腦 (或角色) 來指定名稱可能十分有用。</span><span class="sxs-lookup"><span data-stu-id="ccee7-141">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ccee7-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccee7-142">Next steps</span></span>
<span data-ttu-id="ccee7-143">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="ccee7-143">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="ccee7-144">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="ccee7-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ccee7-145">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="ccee7-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ccee7-146">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="ccee7-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
