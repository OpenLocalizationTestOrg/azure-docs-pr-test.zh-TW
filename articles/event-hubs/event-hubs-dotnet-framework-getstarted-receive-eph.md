---
title: "從 Azure 事件中心使用 aaaReceive 事件 hello.NET Framework |Microsoft 文件"
description: "從 Azure 事件中心使用 hello.NET Framework，請遵循此教學課程 tooreceive 事件。"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="e4bf6-103">從使用.NET Framework hello Azure 事件中心接收事件</span><span class="sxs-lookup"><span data-stu-id="e4bf6-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="e4bf6-104">簡介</span><span class="sxs-lookup"><span data-stu-id="e4bf6-104">Introduction</span></span>

<span data-ttu-id="e4bf6-105">「事件中樞」是一種服務，可處理來自連接裝置和應用程式的大量事件資料 (遙測)。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="e4bf6-106">資料收集到事件中心之後，您可以使用存放裝置叢集的 hello 資料儲存或轉換使用即時分析提供者。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="e4bf6-107">此大規模事件收集和處理功能是索引鍵的現代應用程式架構，包括 hello 物聯網 (IoT) 元件。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="e4bf6-108">本教學課程示範如何 toowrite.NET Framework 主控台應用程式會接收來自事件中心使用 hello 訊息**[事件處理器主機][EventProcessorHost]**。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="e4bf6-109">使用.NET Framework hello toosend 事件，請參閱 「 hello[傳送事件 tooAzure 事件中心使用.NET Framework hello](event-hubs-dotnet-framework-getstarted-send.md)文章，或按一下 hello 適當傳送的語言 hello 左側資料表的內容中。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="e4bf6-110">hello[事件處理器主機][ EventProcessorHost]是管理永續性的檢查點，藉以簡化從事件中心接收事件的.NET 類別和平行方式接收這些事件中心。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="e4bf6-111">使用 hello[事件處理器主機][Event Processor Host]，您可以跨多個接收者，分割事件，即使裝載於不同的節點。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="e4bf6-112">這個範例會示範如何 toouse hello[事件處理器主機][ EventProcessorHost]單一收件者。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="e4bf6-113">hello[擴充的事件處理][ Scale out Event Processing with Event Hubs]範例將示範如何 toouse hello[事件處理器主機][ EventProcessorHost]與多個接收者。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4bf6-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="e4bf6-114">Prerequisites</span></span>

<span data-ttu-id="e4bf6-115">toocomplete 本教學課程中，您需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="e4bf6-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="e4bf6-116">[Microsoft Visual Studio 2015 或更高版本](http://visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="e4bf6-117">在此教學課程中的 hello 螢幕擷取畫面會使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="e4bf6-118">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-118">An active Azure account.</span></span> <span data-ttu-id="e4bf6-119">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="e4bf6-120">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="e4bf6-121">建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="e4bf6-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="e4bf6-122">hello 第一個步驟是 toouse hello [Azure 入口網站](https://portal.azure.com)toocreate 的命名空間的輸入事件中心，並取得 hello 應用程式需要 toocommunicate 與 hello 事件中心的管理認證。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="e4bf6-123">toocreate 命名空間和事件中心，請依照下列中的 hello 程序[本文](event-hubs-create.md)，然後繼續進行下列步驟，在此教學課程中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="e4bf6-124">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e4bf6-124">Create an Azure Storage account</span></span>

<span data-ttu-id="e4bf6-125">toouse hello[事件處理器主機][EventProcessorHost]，您必須擁有[Azure 儲存體帳戶][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="e4bf6-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="e4bf6-126">登入 toohello [Azure 入口網站][Azure portal]，然後按一下**新增**hello 在左上方的囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="e4bf6-127">按一下 [儲存體]，然後按一下 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="e4bf6-128">在 hello**建立儲存體帳戶**刀鋒視窗中，輸入 hello 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="e4bf6-129">Toocreate hello 資源選擇 Azure 訂用帳戶、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="e4bf6-130">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="e4bf6-131">在 [hello] 清單中的儲存體帳戶，hello 新建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="e4bf6-132">在 hello 儲存體帳戶刀鋒視窗中，按一下 **存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="e4bf6-133">複製 hello 值**key1** toouse 稍後在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="e4bf6-134">建立接收者主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="e4bf6-134">Create a receiver console application</span></span>

1. <span data-ttu-id="e4bf6-135">在 Visual Studio 中，建立新的 Visual C# 桌面應用程式專案，使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="e4bf6-136">名稱 hello 專案**接收者**。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="e4bf6-137">在 [方案總管] 中，以滑鼠右鍵按一下 hello**接收者**專案，然後再按一下**管理方案的 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="e4bf6-138">按一下 hello**瀏覽**索引標籤，然後搜尋`Microsoft Azure Service Bus Event Hub - EventProcessorHost`。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="e4bf6-139">按一下**安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="e4bf6-140">Visual Studio 會下載、 安裝，並將參考 toohello [Azure 服務匯流排事件中樞 EventProcessorHost NuGet 封裝](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost)，所有相依性。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="e4bf6-141">以滑鼠右鍵按一下 hello**接收者**專案中，按一下 **新增**，然後按一下**類別**。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="e4bf6-142">Hello 新類別命名**SimpleEventProcessor**，然後按一下**新增**toocreate hello 類別。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="e4bf6-143">新增下列陳述式在 hello hello SimpleEventProcessor.cs 檔案最上方的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4bf6-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="e4bf6-144">然後，以取代下列程式碼 hello hello 類別主體中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4bf6-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  <span data-ttu-id="e4bf6-145">這個類別會呼叫 hello **EventProcessorHost** tooprocess 收到 hello 事件中心的事件。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="e4bf6-146">hello`SimpleEventProcessor`類別使用馬錶 tooperiodically 呼叫 hello 檢查點方法上 hello **EventProcessorHost**內容。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="e4bf6-147">這項處理可確保，如果 hello 收件者會重新啟動，就會失去不超過五分鐘的處理工作。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="e4bf6-148">在 hello**程式**類別中，加入下列 hello`using`在 hello hello 檔案最上方的陳述式：</span><span class="sxs-lookup"><span data-stu-id="e4bf6-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="e4bf6-149">然後，取代 hello`Main`方法在 hello`Program`類別以下列程式碼的 hello、 替代 hello 事件中樞的名稱和 hello 命名空間層級的連接字串之前儲存和 hello 儲存體帳戶和您在 hello 中複製的索引鍵上一節。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. <span data-ttu-id="e4bf6-150">執行 hello 程式，並確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="e4bf6-151">恭喜！</span><span class="sxs-lookup"><span data-stu-id="e4bf6-151">Congratulations!</span></span> <span data-ttu-id="e4bf6-152">您現在已從事件中心使用 hello 事件處理器主機收到訊息。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="e4bf6-153">本教學課程使用單一 [EventProcessorHost][EventProcessorHost] 執行個體。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="e4bf6-154">tooincrease 輸送量，建議您執行多個執行個體[EventProcessorHost][EventProcessorHost]hello [事件處理時調整] 所示，[事件處理出縮放] 範例。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="e4bf6-155">在這些情況下，hello 不同執行個體自動協調彼此 tooload 平衡 hello 接收到事件。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="e4bf6-156">如果您想要多個接收者 tooeach 程序*所有*hello 事件，您必須使用 hello **ConsumerGroup**概念。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="e4bf6-157">當從不同的電腦收到事件時，可能會很有用的 toospecify 名稱[EventProcessorHost] [ EventProcessorHost]執行個體根據 hello 機器 （或角色） 中所部署。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="e4bf6-158">如需有關這些主題的詳細資訊，請參閱 hello[事件中心概觀][ Event Hubs overview]和 hello[事件中心程式設計指南][ Event Hubs Programming Guide]主題。</span><span class="sxs-lookup"><span data-stu-id="e4bf6-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e4bf6-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4bf6-159">Next steps</span></span>

<span data-ttu-id="e4bf6-160">既然您已建立實用應用程式會建立事件中心並傳送和接收資料，您可以進一步瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="e4bf6-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="e4bf6-161">[事件處理器主機][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="e4bf6-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="e4bf6-162">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="e4bf6-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="e4bf6-163">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="e4bf6-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
