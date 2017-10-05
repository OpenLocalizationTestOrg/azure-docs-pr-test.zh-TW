---
title: "Azure 事件中樞 .NET Standard API 概觀 | Microsoft Docs"
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
ms.openlocfilehash: eea682c40cd415b383a8b2f0004a5f3648e2f01f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="afe6b-103">事件中樞 .NET Standard API 概觀</span><span class="sxs-lookup"><span data-stu-id="afe6b-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="afe6b-104">本文將摘要列出一些主要事件中樞 .NET Standard 用戶端 API。</span><span class="sxs-lookup"><span data-stu-id="afe6b-104">This article summarizes some of the key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="afe6b-105">目前有兩個 .NET Standard 用戶端程式庫︰</span><span class="sxs-lookup"><span data-stu-id="afe6b-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="afe6b-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="afe6b-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="afe6b-107">此程式庫提供所有基本的執行階段作業。</span><span class="sxs-lookup"><span data-stu-id="afe6b-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="afe6b-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="afe6b-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="afe6b-109">此程式庫新增可讓您記錄處理過之事件的額外功能，並且是從事件中樞讀取的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="afe6b-109">This library adds additional functionality that allows for keeping track of processed events, and is the easiest way to read from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="afe6b-110">事件中樞用戶端</span><span class="sxs-lookup"><span data-stu-id="afe6b-110">Event Hubs client</span></span>
<span data-ttu-id="afe6b-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) 是您用來傳送事件、建立接收者，以及取得執行階段資訊的主要物件。</span><span class="sxs-lookup"><span data-stu-id="afe6b-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is the primary object you use to send events, create receivers, and to get run-time information.</span></span> <span data-ttu-id="afe6b-112">此用戶端會連結到特定的事件中樞，並建立新的「事件中樞」端點連線。</span><span class="sxs-lookup"><span data-stu-id="afe6b-112">This client is linked to a particular event hub, and creates a new connection to the Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="afe6b-113">建立事件中樞用戶端</span><span class="sxs-lookup"><span data-stu-id="afe6b-113">Create an Event Hubs client</span></span>
<span data-ttu-id="afe6b-114">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) 物件是從連接字串建立。</span><span class="sxs-lookup"><span data-stu-id="afe6b-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="afe6b-115">具現化新用戶端的最簡單方式，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="afe6b-115">The simplest way to instantiate a new client is shown in the following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="afe6b-116">若要以程式設計方式編輯連接字串，您可以使用 [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) 類別，並將連接字串做為參數傳遞到 [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_)。</span><span class="sxs-lookup"><span data-stu-id="afe6b-116">To programmatically edit the connection string, you can use the [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass the connection string as a parameter to [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="afe6b-117">傳送事件</span><span class="sxs-lookup"><span data-stu-id="afe6b-117">Send events</span></span>
<span data-ttu-id="afe6b-118">若要將事件傳送到事件中樞，請使用 [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) 類別。</span><span class="sxs-lookup"><span data-stu-id="afe6b-118">To send events to an event hub, use the [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="afe6b-119">主體必須是 `byte` 陣列，或者 `byte` 陣列區段。</span><span class="sxs-lookup"><span data-stu-id="afe6b-119">The body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="afe6b-120">接收事件</span><span class="sxs-lookup"><span data-stu-id="afe6b-120">Receive events</span></span>
<span data-ttu-id="afe6b-121">從事件中樞接收事件的建議方式是使用[事件處理器主機](#event-processor-host-apis)，它提供了自動追蹤位移的功能，以及資料分割資訊。</span><span class="sxs-lookup"><span data-stu-id="afe6b-121">The recommended way to receive events from Event Hubs is using the [Event Processor Host](#event-processor-host-apis), which provides functionality to automatically keep track of offset, and partition information.</span></span> <span data-ttu-id="afe6b-122">不過，在某些情況中，您可能會想要使用核心事件中樞程式庫的彈性來接收事件。</span><span class="sxs-lookup"><span data-stu-id="afe6b-122">However, there are certain situations in which you may want to use the flexibility of the core Event Hubs library to receive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="afe6b-123">建立接收者</span><span class="sxs-lookup"><span data-stu-id="afe6b-123">Create a receiver</span></span>
<span data-ttu-id="afe6b-124">接收者會繫結至特定的資料分割，因此為了要接收事件中樞中的所有事件，您將必須建立多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="afe6b-124">Receivers are tied to specific partitions, so in order to receive all events in an event hub, you will need to create multiple instances.</span></span> <span data-ttu-id="afe6b-125">一般而言，最好以程式設計的方式取得資料分割資訊，而不是以硬式編碼資料分割識別碼的方式。</span><span class="sxs-lookup"><span data-stu-id="afe6b-125">Generally speaking, it is a good practice to get the partition information programatically, rather than hard-coding the partition ids.</span></span> <span data-ttu-id="afe6b-126">若要這樣做，您可以使用 [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) 方法。</span><span class="sxs-lookup"><span data-stu-id="afe6b-126">In order to do so, you can use the [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list to keep track of the receivers
var receivers = new List<PartitionReceiver>();
// Use the eventHubClient created above to get the runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over the resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create the receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add the receiver to the list
    receivers.Add(receiver);
}
```

<span data-ttu-id="afe6b-127">由於事件一律不會從事件中樞內移除 (只會過期)，因此您必須指定適當的起始點。</span><span class="sxs-lookup"><span data-stu-id="afe6b-127">Since events are never removed from an event hub (and only expire), you need to specify the proper starting point.</span></span> <span data-ttu-id="afe6b-128">下列範例顯示可能的組合。</span><span class="sxs-lookup"><span data-stu-id="afe6b-128">The following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed to come from GetRuntimeInformationAsync()

// Using the constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="afe6b-129">使用事件</span><span class="sxs-lookup"><span data-stu-id="afe6b-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call to ReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop to process
    foreach (var ehEvent in ehEvents)
    {
        // Decode the byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load the custom property that we set in the send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="afe6b-130">Event Processor Host API</span><span class="sxs-lookup"><span data-stu-id="afe6b-130">Event Processor Host APIs</span></span>
<span data-ttu-id="afe6b-131">這些 API 會透過在可用的背景工作之間散佈資料分割，提供恢復功能給可能會變成無法使用的背景工作角色處理序。</span><span class="sxs-lookup"><span data-stu-id="afe6b-131">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

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

// Disposes of the Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="afe6b-132">以下是 [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor) 的範例實作。</span><span class="sxs-lookup"><span data-stu-id="afe6b-132">The following is a sample implementation of the [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="afe6b-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afe6b-133">Next steps</span></span>
<span data-ttu-id="afe6b-134">若要深入了解事件中樞案例，請造訪下列連結：</span><span class="sxs-lookup"><span data-stu-id="afe6b-134">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="afe6b-135">Azure 事件中樞是什麼？</span><span class="sxs-lookup"><span data-stu-id="afe6b-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="afe6b-136">可用的事件中樞 API</span><span class="sxs-lookup"><span data-stu-id="afe6b-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="afe6b-137">.NET API 參考如下：</span><span class="sxs-lookup"><span data-stu-id="afe6b-137">The .NET API references are here:</span></span>

* [<span data-ttu-id="afe6b-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="afe6b-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="afe6b-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="afe6b-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)