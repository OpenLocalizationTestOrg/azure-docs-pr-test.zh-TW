---
title: "Azure 事件中樞的可用性和一致性 | Microsoft Docs"
description: "如何使用分割區，以便透過 Azure 事件中樞提供最大數量的可用性和一致性。"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 681a9d1636d547492f6f827461c6b2494b918778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="b1a69-103">事件中樞的可用性和一致性</span><span class="sxs-lookup"><span data-stu-id="b1a69-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="b1a69-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b1a69-104">Overview</span></span>
<span data-ttu-id="b1a69-105">「Azure 事件中樞」會使用[資料分割模型](event-hubs-features.md#partitions)，來提升單一事件中樞內的可用性與平行處理。</span><span class="sxs-lookup"><span data-stu-id="b1a69-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) to improve availability and parallelization within a single event hub.</span></span> <span data-ttu-id="b1a69-106">例如，如果事件中樞有四個分割區，而其中一個分割區在負載平衡作業中從一部伺服器移到另一部伺服器，則您仍可從其他三個分割區進行傳送及接收。</span><span class="sxs-lookup"><span data-stu-id="b1a69-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server to another in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="b1a69-107">此外，擁有更多分割區可讓您使用更多並行讀取器來處理資料，進而改善您的彙總輸送量。</span><span class="sxs-lookup"><span data-stu-id="b1a69-107">Additionally, having more partitions enables you to have more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="b1a69-108">了解分散式系統中分割和排序的含意是解決方案設計的重要層面。</span><span class="sxs-lookup"><span data-stu-id="b1a69-108">Understanding the implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="b1a69-109">為了協助說明排序和可用性之間的權衡取捨，請參閱 [CAP 理論](https://en.wikipedia.org/wiki/CAP_theorem) (英文)，也稱為 Brewer 的理論。</span><span class="sxs-lookup"><span data-stu-id="b1a69-109">To help explain the trade-off between ordering and availability, see the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="b1a69-110">這個理論討論一致性、可用性及分割區容錯之間的選擇。</span><span class="sxs-lookup"><span data-stu-id="b1a69-110">This theorem discusses the choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="b1a69-111">Brewer 的理論會定義一致性和可用性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b1a69-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="b1a69-112">分割區容錯：即使發生分割區失敗，資料處理系統還是能夠繼續處理資料。</span><span class="sxs-lookup"><span data-stu-id="b1a69-112">Partition tolerance: the ability of a data processing system to continue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="b1a69-113">可用性：非失敗節點會在合理的時間 (不含錯誤或逾時) 內傳回合理的回應。</span><span class="sxs-lookup"><span data-stu-id="b1a69-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="b1a69-114">一致性：保證讀取會傳回指定用戶端的最新寫入。</span><span class="sxs-lookup"><span data-stu-id="b1a69-114">Consistency: a read is guaranteed to return the most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="b1a69-115">分割區容錯</span><span class="sxs-lookup"><span data-stu-id="b1a69-115">Partition tolerance</span></span>
<span data-ttu-id="b1a69-116">「事件中樞」是建置在已分割的資料模型上。</span><span class="sxs-lookup"><span data-stu-id="b1a69-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="b1a69-117">您可以在安裝時設定事件中樞中的分割區數目，但之後即無法變更此值。</span><span class="sxs-lookup"><span data-stu-id="b1a69-117">You can configure the number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="b1a69-118">由於您必須將分割區與事件中樞搭配使用，因此必須決定應用程式相關的可用性和一致性。</span><span class="sxs-lookup"><span data-stu-id="b1a69-118">Since you must use partitions with Event Hubs, you have to make a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="b1a69-119">Availability</span><span class="sxs-lookup"><span data-stu-id="b1a69-119">Availability</span></span>
<span data-ttu-id="b1a69-120">開始使用事件中樞的最簡單方式是使用預設行為。</span><span class="sxs-lookup"><span data-stu-id="b1a69-120">The simplest way to get started with Event Hubs is to use the default behavior.</span></span> <span data-ttu-id="b1a69-121">如果您建立新的 `EventHubClient` 物件並使用 `Send` 方法，系統就會在事件中樞的分割區之間自動分配事件。</span><span class="sxs-lookup"><span data-stu-id="b1a69-121">If you create a new `EventHubClient` object and use the `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="b1a69-122">此行為可讓運作時間達到最長。</span><span class="sxs-lookup"><span data-stu-id="b1a69-122">This behavior allows for the greatest amount of up time.</span></span>

<span data-ttu-id="b1a69-123">針對需要最長運作時間的使用案例，建議使用此模型。</span><span class="sxs-lookup"><span data-stu-id="b1a69-123">For use cases that require the maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="b1a69-124">一致性</span><span class="sxs-lookup"><span data-stu-id="b1a69-124">Consistency</span></span>
<span data-ttu-id="b1a69-125">在某些案例中，事件的順序可能相當重要。</span><span class="sxs-lookup"><span data-stu-id="b1a69-125">In some scenarios, the ordering of events can be important.</span></span> <span data-ttu-id="b1a69-126">例如，您可能想要讓後端系統在刪除命令之前先處理更新命令。</span><span class="sxs-lookup"><span data-stu-id="b1a69-126">For example, you may want your back-end system to process an update command before a delete command.</span></span> <span data-ttu-id="b1a69-127">在此情況下，您可以在事件上設定分割區索引鍵，或使用 `PartitionSender` 物件只將事件傳送到特定的分割區。</span><span class="sxs-lookup"><span data-stu-id="b1a69-127">In this instance, you can either set the partition key on an event, or use a `PartitionSender` object to only send events to a certain partition.</span></span> <span data-ttu-id="b1a69-128">這麼做可確保在從分割區讀取這些事件時，會依序讀取它們。</span><span class="sxs-lookup"><span data-stu-id="b1a69-128">Doing so ensures that when these events are read from the partition, they are read in order.</span></span>

<span data-ttu-id="b1a69-129">使用這個組態時，請記住，如果作為您傳送目的地的特定分割區無法使用，您將會收到錯誤回應。</span><span class="sxs-lookup"><span data-stu-id="b1a69-129">With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="b1a69-130">相較之下，如果您不傾向使用單一分割區，「事件中樞」服務就會將事件傳送至下一個可用的分割區。</span><span class="sxs-lookup"><span data-stu-id="b1a69-130">As a point of comparison, if you do not have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.</span></span>

<span data-ttu-id="b1a69-131">有一個既可確保排序又可讓運作時間達到最長的可能解決方案，就是在您的事件處理應用程式中彙總事件。</span><span class="sxs-lookup"><span data-stu-id="b1a69-131">One possible solution to ensure ordering, while also maximizing up time, would be to aggregate events as part of your event processing application.</span></span> <span data-ttu-id="b1a69-132">達到此目的的最簡單方式，就是為您的事件標上自訂序號屬性戳記。</span><span class="sxs-lookup"><span data-stu-id="b1a69-132">The easiest way to accomplish this is to stamp your event with a custom sequence number property.</span></span> <span data-ttu-id="b1a69-133">下列程式碼顯示一個範例：</span><span class="sxs-lookup"><span data-stu-id="b1a69-133">The following code shows an example:</span></span>

```csharp
// Get the latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="b1a69-134">這個範例會將事件傳送到事件中樞的其中一個可用分割區，然後從您的應用程式設定對應的序號。</span><span class="sxs-lookup"><span data-stu-id="b1a69-134">This example sends your event to one of the available partitions in your event hub, and sets the corresponding sequence number from your application.</span></span> <span data-ttu-id="b1a69-135">這個解決方案會要求您的處理應用程式保留狀態，但會為您的傳送者提供一個更可能可供使用的端點。</span><span class="sxs-lookup"><span data-stu-id="b1a69-135">This solution requires state to be kept by your processing application, but gives your senders an endpoint that is more likely to be available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1a69-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1a69-136">Next steps</span></span>
<span data-ttu-id="b1a69-137">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="b1a69-137">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="b1a69-138">事件中樞服務概觀</span><span class="sxs-lookup"><span data-stu-id="b1a69-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="b1a69-139">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="b1a69-139">Create an event hub</span></span>](event-hubs-create.md)
