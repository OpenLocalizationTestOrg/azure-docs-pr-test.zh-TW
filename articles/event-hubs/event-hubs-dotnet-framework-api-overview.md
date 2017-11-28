---
title: "hello Azure 事件中心.NET Framework Api 的 aaaOverview |Microsoft 文件"
description: "一些重要事件中心.NET Framework 用戶端 hello Api 的摘要。"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b0e12e43f91b025d7aa4ca03e664b9ff31b04097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="a6449-103">事件中樞 .NET Framework API 概觀</span><span class="sxs-lookup"><span data-stu-id="a6449-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="a6449-104">本文摘要說明一些 hello 金鑰事件中心.NET Framework 用戶端應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a6449-104">This article summarizes some of hello key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="a6449-105">分為兩種類別：管理和執行階段 API。</span><span class="sxs-lookup"><span data-stu-id="a6449-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="a6449-106">執行階段 Api 包含的所有作業所需 toosend 和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="a6449-106">Run-time APIs consist of all operations needed toosend and receive a message.</span></span> <span data-ttu-id="a6449-107">管理作業可讓您 toomanage 事件中心實體狀態，包括建立、 更新和刪除實體。</span><span class="sxs-lookup"><span data-stu-id="a6449-107">Management operations enable you toomanage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="a6449-108">監視案例跨越管理和執行階段。</span><span class="sxs-lookup"><span data-stu-id="a6449-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="a6449-109">如需 hello.NET Api 的詳細的參考文件，請參閱 hello[服務匯流排.NET](/dotnet/api/microsoft.servicebus.messaging)和[EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor)參考。</span><span class="sxs-lookup"><span data-stu-id="a6449-109">For detailed reference documentation on hello .NET APIs, see hello [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="a6449-110">管理 API</span><span class="sxs-lookup"><span data-stu-id="a6449-110">Management APIs</span></span>
<span data-ttu-id="a6449-111">tooperform hello 下列管理作業，您必須具有**管理**hello 事件中樞命名空間的權限：</span><span class="sxs-lookup"><span data-stu-id="a6449-111">tooperform hello following management operations, you must have **Manage** permissions on hello Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="a6449-112">建立</span><span class="sxs-lookup"><span data-stu-id="a6449-112">Create</span></span>
```csharp
// Create hello event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="a6449-113">更新</span><span class="sxs-lookup"><span data-stu-id="a6449-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="a6449-114">刪除</span><span class="sxs-lookup"><span data-stu-id="a6449-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="a6449-115">執行階段 API</span><span class="sxs-lookup"><span data-stu-id="a6449-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="a6449-116">建立發佈者</span><span class="sxs-lookup"><span data-stu-id="a6449-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="a6449-117">發佈訊息</span><span class="sxs-lookup"><span data-stu-id="a6449-117">Publish message</span></span>
```csharp
// Create hello device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="a6449-118">建立取用者</span><span class="sxs-lookup"><span data-stu-id="a6449-118">Create consumer</span></span>
```csharp
// Create hello Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get hello default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="a6449-119">取用訊息</span><span class="sxs-lookup"><span data-stu-id="a6449-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="a6449-120">Event Processor Host API</span><span class="sxs-lookup"><span data-stu-id="a6449-120">Event Processor Host APIs</span></span>
<span data-ttu-id="a6449-121">這些 Api 提供恢復功能 tooworker 的處理程序可能會變成無法使用，可用的背景工作之間分散資料分割。</span><span class="sxs-lookup"><span data-stu-id="a6449-121">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use hello EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// tooclose
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="a6449-122">hello [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor)介面的定義如下：</span><span class="sxs-lookup"><span data-stu-id="a6449-122">hello [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="a6449-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6449-123">Next steps</span></span>
<span data-ttu-id="a6449-124">toolearn 有關事件中心案例的詳細資訊，請前往下列連結：</span><span class="sxs-lookup"><span data-stu-id="a6449-124">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="a6449-125">Azure 事件中樞是什麼？</span><span class="sxs-lookup"><span data-stu-id="a6449-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a6449-126">事件中樞程式設計指南</span><span class="sxs-lookup"><span data-stu-id="a6449-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="a6449-127">以下是 hello.NET API 參考：</span><span class="sxs-lookup"><span data-stu-id="a6449-127">hello .NET API references are here:</span></span>

* [<span data-ttu-id="a6449-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="a6449-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="a6449-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="a6449-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)
