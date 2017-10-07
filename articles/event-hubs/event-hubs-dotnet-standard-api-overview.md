---
title: "hello Azure 事件中心.NET 標準 Api 的 aaaOverview |Microsoft 文件"
description: ".NET Standard API 概觀"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="6bbca-103">事件中樞 .NET Standard API 概觀</span><span class="sxs-lookup"><span data-stu-id="6bbca-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="6bbca-104">本文摘要說明一些 hello 金鑰事件中心標準.NET 用戶端應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6bbca-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="6bbca-105">目前有兩個 .NET Standard 用戶端程式庫︰</span><span class="sxs-lookup"><span data-stu-id="6bbca-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="6bbca-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="6bbca-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="6bbca-107">此程式庫提供所有基本的執行階段作業。</span><span class="sxs-lookup"><span data-stu-id="6bbca-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="6bbca-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="6bbca-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="6bbca-109">此程式庫新增額外的功能，允許追蹤的處理過的事件，而且是 hello 最簡單方式 tooread 自事件中心。</span><span class="sxs-lookup"><span data-stu-id="6bbca-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="6bbca-110">事件中樞用戶端</span><span class="sxs-lookup"><span data-stu-id="6bbca-110">Event Hubs client</span></span>
<span data-ttu-id="6bbca-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient)是 hello 使用 toosend 事件的主要物件建立的接收者和 tooget 執行階段資訊。</span><span class="sxs-lookup"><span data-stu-id="6bbca-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="6bbca-112">此用戶端連結的 tooa 特定事件中心，並且建立新的連接 toohello 事件中樞端點。</span><span class="sxs-lookup"><span data-stu-id="6bbca-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="6bbca-113">建立事件中樞用戶端</span><span class="sxs-lookup"><span data-stu-id="6bbca-113">Create an Event Hubs client</span></span>
<span data-ttu-id="6bbca-114">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) 物件是從連接字串建立。</span><span class="sxs-lookup"><span data-stu-id="6bbca-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="6bbca-115">最簡單方式 tooinstantiate hello 新的用戶端以 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6bbca-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="6bbca-116">tooprogrammatically 編輯 hello 連接字串，您可以使用 hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder)類別，並將 hello 連接字串當做參數傳遞太[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="6bbca-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="6bbca-117">傳送事件</span><span class="sxs-lookup"><span data-stu-id="6bbca-117">Send events</span></span>
<span data-ttu-id="6bbca-118">toosend 事件 tooan 事件中心使用 hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata)類別。</span><span class="sxs-lookup"><span data-stu-id="6bbca-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="6bbca-119">hello 主體必須是`byte`陣列，或`byte`陣列區段。</span><span class="sxs-lookup"><span data-stu-id="6bbca-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="6bbca-120">接收事件</span><span class="sxs-lookup"><span data-stu-id="6bbca-120">Receive events</span></span>
<span data-ttu-id="6bbca-121">建議的方式 tooreceive 事件從事件中樞的 hello 使用 hello[事件處理器主機](#event-processor-host-apis)，提供功能 tooautomatically 追蹤的位移，並將資料分割資訊。</span><span class="sxs-lookup"><span data-stu-id="6bbca-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="6bbca-122">不過，有某些情況的下，您可能想 toouse hello 彈性的 hello 核心事件中心程式庫 tooreceive 事件。</span><span class="sxs-lookup"><span data-stu-id="6bbca-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="6bbca-123">建立接收者</span><span class="sxs-lookup"><span data-stu-id="6bbca-123">Create a receiver</span></span>
<span data-ttu-id="6bbca-124">接收器是繫結的 toospecific 資料分割，因此在排序 tooreceive 所有的事件事件中心，您將需要 toocreate 多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="6bbca-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="6bbca-125">通常來說，它是很好的作法 tooget hello 磁碟分割資訊以程式設計的方式，而不是硬式編碼 hello 資料分割識別碼。</span><span class="sxs-lookup"><span data-stu-id="6bbca-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="6bbca-126">在排序 toodo 操作，您可以使用 hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync)方法。</span><span class="sxs-lookup"><span data-stu-id="6bbca-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

<span data-ttu-id="6bbca-127">由於事件會永遠不會從事件中心 （並僅到期），您必須 toospecify hello 適當起點。</span><span class="sxs-lookup"><span data-stu-id="6bbca-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="6bbca-128">hello 下列範例示範可能的組合。</span><span class="sxs-lookup"><span data-stu-id="6bbca-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="6bbca-129">使用事件</span><span class="sxs-lookup"><span data-stu-id="6bbca-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="6bbca-130">Event Processor Host API</span><span class="sxs-lookup"><span data-stu-id="6bbca-130">Event Processor Host APIs</span></span>
<span data-ttu-id="6bbca-131">這些 Api 提供恢復功能 tooworker 的處理程序可能會變成無法使用，可用的背景工作之間分散資料分割。</span><span class="sxs-lookup"><span data-stu-id="6bbca-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="6bbca-132">hello 以下是範例實作 hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor)。</span><span class="sxs-lookup"><span data-stu-id="6bbca-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="6bbca-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bbca-133">Next steps</span></span>
<span data-ttu-id="6bbca-134">toolearn 有關事件中心案例的詳細資訊，請前往下列連結：</span><span class="sxs-lookup"><span data-stu-id="6bbca-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="6bbca-135">Azure 事件中樞是什麼？</span><span class="sxs-lookup"><span data-stu-id="6bbca-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6bbca-136">可用的事件中樞 API</span><span class="sxs-lookup"><span data-stu-id="6bbca-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="6bbca-137">以下是 hello.NET API 參考：</span><span class="sxs-lookup"><span data-stu-id="6bbca-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="6bbca-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="6bbca-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="6bbca-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="6bbca-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)