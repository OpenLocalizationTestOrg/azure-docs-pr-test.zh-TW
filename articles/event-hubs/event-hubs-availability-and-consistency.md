---
title: "aaaAvailability 和 Azure 事件中心的一致性 |Microsoft 文件"
description: "Tooprovide hello 最大數量可用性以及與 Azure 事件中心使用一致的分割區。"
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
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="9b05a-103">事件中樞的可用性和一致性</span><span class="sxs-lookup"><span data-stu-id="9b05a-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="9b05a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9b05a-104">Overview</span></span>
<span data-ttu-id="9b05a-105">Azure 事件中心採用[分割模型](event-hubs-features.md#partitions)tooimprove 可用性和平行處理單一事件中心內。</span><span class="sxs-lookup"><span data-stu-id="9b05a-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="9b05a-106">例如，如果事件中心有四個資料分割，而且這些資料分割的其中一個會從負載平衡作業中的一部伺服器 tooanother 移，您仍可以傳送及接收來自其他三個資料分割。</span><span class="sxs-lookup"><span data-stu-id="9b05a-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="9b05a-107">此外，讓多個資料分割可讓您 toohave 更多的並行讀取器處理您的資料，改善您的彙總輸送量。</span><span class="sxs-lookup"><span data-stu-id="9b05a-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="9b05a-108">了解的資料分割和排序分散式系統中的 hello 含意是解決方案設計的重要層面。</span><span class="sxs-lookup"><span data-stu-id="9b05a-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="9b05a-109">toohelp 說明 hello 排序與可用性之間的取捨，請參閱 hello [CAP 理論](https://en.wikipedia.org/wiki/CAP_theorem)，也稱為 Brewer 的理論。</span><span class="sxs-lookup"><span data-stu-id="9b05a-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="9b05a-110">此理論討論之間的一致性、 可用性和資料分割容錯的 hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="9b05a-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="9b05a-111">Brewer 的理論會定義一致性和可用性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9b05a-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="9b05a-112">分割容錯： hello 處理資料，即使在磁碟分割失敗，就會發生資料處理系統 toocontinue 的能力。</span><span class="sxs-lookup"><span data-stu-id="9b05a-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="9b05a-113">可用性：非失敗節點會在合理的時間 (不含錯誤或逾時) 內傳回合理的回應。</span><span class="sxs-lookup"><span data-stu-id="9b05a-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="9b05a-114">： 讀取保證一致性 tooreturn hello 最新的寫入給定的用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b05a-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="9b05a-115">分割區容錯</span><span class="sxs-lookup"><span data-stu-id="9b05a-115">Partition tolerance</span></span>
<span data-ttu-id="9b05a-116">「事件中樞」是建置在已分割的資料模型上。</span><span class="sxs-lookup"><span data-stu-id="9b05a-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="9b05a-117">您可以在安裝期間，在事件中樞設定 hello 資料分割數目，但是您之後無法變更此值。</span><span class="sxs-lookup"><span data-stu-id="9b05a-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="9b05a-118">由於您必須使用事件中心使用資料分割，您將 toomake 決策，以可用性和一致性應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b05a-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="9b05a-119">Availability</span><span class="sxs-lookup"><span data-stu-id="9b05a-119">Availability</span></span>
<span data-ttu-id="9b05a-120">hello 最簡單的方式 tooget 入門事件中心是 toouse hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="9b05a-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="9b05a-121">如果您建立新`EventHubClient`物件，並使用 hello`Send`方法，您的事件會自動發佈事件中樞中的資料分割之間。</span><span class="sxs-lookup"><span data-stu-id="9b05a-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="9b05a-122">此行為可讓您 hello 最大的時間。</span><span class="sxs-lookup"><span data-stu-id="9b05a-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="9b05a-123">需要 hello 最大執行時間的使用案例，此模型是慣用的。</span><span class="sxs-lookup"><span data-stu-id="9b05a-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="9b05a-124">一致性</span><span class="sxs-lookup"><span data-stu-id="9b05a-124">Consistency</span></span>
<span data-ttu-id="9b05a-125">在某些情況下，hello 的事件排序可能很重要。</span><span class="sxs-lookup"><span data-stu-id="9b05a-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="9b05a-126">例如，您可以您的後端系統 tooprocess update 命令之前刪除命令。</span><span class="sxs-lookup"><span data-stu-id="9b05a-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="9b05a-127">在本例中，您可以在事件上設定 hello 資料分割索引鍵，或使用`PartitionSender`物件 tooonly 傳送事件 tooa 特定資料分割。</span><span class="sxs-lookup"><span data-stu-id="9b05a-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="9b05a-128">這樣可以確保，當這些事件會讀取來自 hello 磁碟分割，它們會讀取順序。</span><span class="sxs-lookup"><span data-stu-id="9b05a-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="9b05a-129">此設定，請注意，如果您要傳送的 hello 特定資料分割 toowhich 無法使用時，您會收到錯誤回應。</span><span class="sxs-lookup"><span data-stu-id="9b05a-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="9b05a-130">為的比較點，如果您不需要同質 tooa 單一資料分割，hello 事件中心服務會傳送您事件 toohello 下一個可用的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="9b05a-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="9b05a-131">一個可能的解決方案 tooensure 排序，同時也執行時間，盡量將 tooaggregate 事件做為您的事件處理應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="9b05a-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="9b05a-132">這個 hello 最簡單的方式 tooaccomplish 是 toostamp 自訂的序號屬性與事件。</span><span class="sxs-lookup"><span data-stu-id="9b05a-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="9b05a-133">下列程式碼的 hello 顯示範例：</span><span class="sxs-lookup"><span data-stu-id="9b05a-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="9b05a-134">這個範例事件中樞，以傳送您的事件 tooone hello 可用的資料分割，並從您的應用程式設定 hello 對應序號。</span><span class="sxs-lookup"><span data-stu-id="9b05a-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="9b05a-135">此解決方案需要狀態 toobe 保持為您處理的應用程式，但可讓您的寄件者比較可能 toobe 可用的端點。</span><span class="sxs-lookup"><span data-stu-id="9b05a-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b05a-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b05a-136">Next steps</span></span>
<span data-ttu-id="9b05a-137">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="9b05a-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="9b05a-138">事件中樞服務概觀</span><span class="sxs-lookup"><span data-stu-id="9b05a-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="9b05a-139">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="9b05a-139">Create an event hub</span></span>](event-hubs-create.md)
