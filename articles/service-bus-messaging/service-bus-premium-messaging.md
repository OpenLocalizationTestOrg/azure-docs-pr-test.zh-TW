---
title: "aaaAzure 服務匯流排 Premium 和 Standard 傳訊定價層概觀 |Microsoft 文件"
description: "服務匯流排進階和標準傳訊層級"
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a><span data-ttu-id="1708d-103">服務匯流排進階和標準傳訊層級</span><span class="sxs-lookup"><span data-stu-id="1708d-103">Service Bus Premium and Standard messaging tiers</span></span>

<span data-ttu-id="1708d-104">服務匯流排傳訊 (包含佇列和主題等實體) 結合雲端級別的企業傳訊功能與豐富的發佈-訂閱語意。</span><span class="sxs-lookup"><span data-stu-id="1708d-104">Service Bus Messaging, which includes entities such as queues and topics, combines enterprise messaging capabilities with rich publish-subscribe semantics at cloud scale.</span></span> <span data-ttu-id="1708d-105">Service Bus 訊息作為 hello 通訊骨幹許多複雜的雲端解決方案。</span><span class="sxs-lookup"><span data-stu-id="1708d-105">Service Bus Messaging is used as hello communication backbone for many sophisticated cloud solutions.</span></span>

<span data-ttu-id="1708d-106">hello *Premium*的 Service Bus 訊息層位址周圍小數位數、 效能和可用性的關鍵任務應用程式的一般客戶要求。</span><span class="sxs-lookup"><span data-stu-id="1708d-106">hello *Premium* tier of Service Bus Messaging addresses common customer requests around scale, performance, and availability for mission-critical applications.</span></span> <span data-ttu-id="1708d-107">雖然 hello 功能集幾乎完全相同，但這些兩個 Service Bus 訊息層是設計的 tooserve 不同使用案例。</span><span class="sxs-lookup"><span data-stu-id="1708d-107">Although hello feature sets are nearly identical, these two tiers of Service Bus Messaging are designed tooserve different use cases.</span></span>

<span data-ttu-id="1708d-108">高層級的一些差異會在下表中的 hello 反白顯示。</span><span class="sxs-lookup"><span data-stu-id="1708d-108">Some high-level differences are highlighted in hello following table.</span></span>

| <span data-ttu-id="1708d-109">進階</span><span class="sxs-lookup"><span data-stu-id="1708d-109">Premium</span></span> | <span data-ttu-id="1708d-110">標準</span><span class="sxs-lookup"><span data-stu-id="1708d-110">Standard</span></span> |
| --- | --- |
| <span data-ttu-id="1708d-111">高輸送量</span><span class="sxs-lookup"><span data-stu-id="1708d-111">High throughput</span></span> |<span data-ttu-id="1708d-112">變動輸送量</span><span class="sxs-lookup"><span data-stu-id="1708d-112">Variable throughput</span></span> |
| <span data-ttu-id="1708d-113">可預測的效能</span><span class="sxs-lookup"><span data-stu-id="1708d-113">Predictable performance</span></span> |<span data-ttu-id="1708d-114">變動延遲</span><span class="sxs-lookup"><span data-stu-id="1708d-114">Variable latency</span></span> |
| <span data-ttu-id="1708d-115">固定價格</span><span class="sxs-lookup"><span data-stu-id="1708d-115">Fixed pricing</span></span> |<span data-ttu-id="1708d-116">隨用隨付變動價格</span><span class="sxs-lookup"><span data-stu-id="1708d-116">Pay as you go variable pricing</span></span> |
| <span data-ttu-id="1708d-117">增加和減少的能力 tooscale 工作負載</span><span class="sxs-lookup"><span data-stu-id="1708d-117">Ability tooscale workload up and down</span></span> |<span data-ttu-id="1708d-118">N/A</span><span class="sxs-lookup"><span data-stu-id="1708d-118">N/A</span></span> |
| <span data-ttu-id="1708d-119">向上 too1 MB 的訊息大小</span><span class="sxs-lookup"><span data-stu-id="1708d-119">Message size up too1 MB</span></span> |<span data-ttu-id="1708d-120">向上 too256 KB 的訊息大小</span><span class="sxs-lookup"><span data-stu-id="1708d-120">Message size up too256 KB</span></span> |

<span data-ttu-id="1708d-121">**Service Bus 高階訊息**提供資源隔離層級 hello CPU 和記憶體，以便在隔離狀態執行的每個客戶工作負載。</span><span class="sxs-lookup"><span data-stu-id="1708d-121">**Service Bus Premium Messaging** provides resource isolation at hello CPU and memory level so that each customer workload runs in isolation.</span></span> <span data-ttu-id="1708d-122">此資源容器稱為「傳訊單位」 。</span><span class="sxs-lookup"><span data-stu-id="1708d-122">This resource container is called a *messaging unit*.</span></span> <span data-ttu-id="1708d-123">每個進階命名空間都會被配置至少一個傳訊單位。</span><span class="sxs-lookup"><span data-stu-id="1708d-123">Each premium namespace is allocated at least one messaging unit.</span></span> <span data-ttu-id="1708d-124">您可以為每個服務匯流排進階命名空間購買 1、2 或 4 個傳訊單位。</span><span class="sxs-lookup"><span data-stu-id="1708d-124">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span></span> <span data-ttu-id="1708d-125">單一的工作負載或實體可以跨越多個傳訊單位，可在將變更 hello 傳訊單位數目，雖然計費是 24 小時或每日速率費用。</span><span class="sxs-lookup"><span data-stu-id="1708d-125">A single workload or entity can span multiple messaging units and hello number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span></span> <span data-ttu-id="1708d-126">hello 結果是您 Service Bus 為基礎的解決方案的效能可預測且可重複。</span><span class="sxs-lookup"><span data-stu-id="1708d-126">hello result is predictable and repeatable performance for your Service Bus-based solution.</span></span>

<span data-ttu-id="1708d-127">此效能不僅更可預測並可取得，而且還更快速。</span><span class="sxs-lookup"><span data-stu-id="1708d-127">Not only is this performance more predictable and available, but it is also faster.</span></span> <span data-ttu-id="1708d-128">服務匯流排進階傳訊基礎 hello 儲存引擎中導入[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="1708d-128">Service Bus Premium Messaging builds on hello storage engine introduced in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span> <span data-ttu-id="1708d-129">使用進階傳訊，尖峰效能的速度比具有 hello 標準層。</span><span class="sxs-lookup"><span data-stu-id="1708d-129">With Premium Messaging, peak performance is much faster than with hello Standard tier.</span></span>

## <a name="premium-messaging-technical-differences"></a><span data-ttu-id="1708d-130">進階傳訊技術差異</span><span class="sxs-lookup"><span data-stu-id="1708d-130">Premium Messaging technical differences</span></span>

<span data-ttu-id="1708d-131">hello 下列各節討論 Premium 和 Standard 傳訊層之間有一些差異。</span><span class="sxs-lookup"><span data-stu-id="1708d-131">hello following sections discuss a few differences between Premium and Standard messaging tiers.</span></span>

### <a name="partitioned-queues-and-topics"></a><span data-ttu-id="1708d-132">分割的佇列和主題</span><span class="sxs-lookup"><span data-stu-id="1708d-132">Partitioned queues and topics</span></span>

<span data-ttu-id="1708d-133">進階傳訊支援分割的佇列和主題；事實上這些實體一律會進行分割 (且無法停用)。</span><span class="sxs-lookup"><span data-stu-id="1708d-133">Partitioned queues and topics are supported in Premium Messaging; in fact these entities are always partitioned (and cannot be disabled).</span></span> <span data-ttu-id="1708d-134">不過，Premium 分割佇列和主題不會運作 hello 相同的方式為 hello 標準和基本層的服務匯流排傳訊。</span><span class="sxs-lookup"><span data-stu-id="1708d-134">However, Premium partitioned queues and topics do not function hello same way as in hello Standard and Basic tiers of Service Bus messaging.</span></span> <span data-ttu-id="1708d-135">進階訊息未使用 SQL 做為資料存放區，且不再具有 hello 與共用的平台相關聯的可能的資源競爭。</span><span class="sxs-lookup"><span data-stu-id="1708d-135">Premium messaging does not use SQL as a data store and no longer has hello possible resource competition associated with a shared platform.</span></span> <span data-ttu-id="1708d-136">如此一來，資料分割不是必要的 tooimprove 效能。</span><span class="sxs-lookup"><span data-stu-id="1708d-136">As a result, partitioning is not necessary tooimprove performance.</span></span> <span data-ttu-id="1708d-137">此外，已從標準傳訊 too2 資料分割在 Premium 中 16 個資料分割變更 hello 分割區計數。</span><span class="sxs-lookup"><span data-stu-id="1708d-137">Additionally, hello partition count has been changed from 16 partitions in Standard Messaging too2 partitions in Premium.</span></span> <span data-ttu-id="1708d-138">擁有兩個資料分割可確保可用性，並是更適當的數字的 hello Premium 執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="1708d-138">Having two partitions ensures availability and is a more appropriate number for hello Premium runtime environment.</span></span> 

<span data-ttu-id="1708d-139">使用進階傳訊，當您指定的實體與 hello 大小[MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes)，，大小被分割同樣 hello 2 的磁碟分割，不同於[標準分割實體](service-bus-partitioning.md#standard)中的 hello總大小是 16 hello 指定大小的時間。</span><span class="sxs-lookup"><span data-stu-id="1708d-139">With Premium messaging, when you specify hello size of an entity with [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), that size is split equally across hello 2 partitions, unlike [Standard partitioned entities](service-bus-partitioning.md#standard) in which hello total size is 16 times hello specified size.</span></span> 

<span data-ttu-id="1708d-140">如需分割的詳細資訊，請參閱[分割的佇列和主題](service-bus-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="1708d-140">For more information about partitioning, see [Partitioned queues and topics](service-bus-partitioning.md).</span></span>

### <a name="express-entities"></a><span data-ttu-id="1708d-141">快速實體</span><span class="sxs-lookup"><span data-stu-id="1708d-141">Express entities</span></span>

<span data-ttu-id="1708d-142">因為進階傳訊是在完全隔離的執行階段環境中執行，所以在進階命名空間中並不支援快速實體。</span><span class="sxs-lookup"><span data-stu-id="1708d-142">Because Premium messaging runs in a completely isolated run-time environment, express entities are not supported in Premium namespaces.</span></span> <span data-ttu-id="1708d-143">如需 hello express 功能的詳細資訊，請參閱 hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress)屬性。</span><span class="sxs-lookup"><span data-stu-id="1708d-143">For more information about hello express feature, see hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property.</span></span>

<span data-ttu-id="1708d-144">如果您有下執行標準的訊息，且想 tooport 它 toohello Premium 層的程式碼，請確定 hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress)屬性設定太**false** (hello 預設值)。</span><span class="sxs-lookup"><span data-stu-id="1708d-144">If you have code running under Standard messaging and want tooport it toohello Premium tier, make sure hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property is set too**false** (hello default value).</span></span>

## <a name="get-started-with-premium-messaging"></a><span data-ttu-id="1708d-145">開始使用進階傳訊</span><span class="sxs-lookup"><span data-stu-id="1708d-145">Get started with Premium Messaging</span></span>

<span data-ttu-id="1708d-146">開始使用進階傳訊相當簡單，但 hello 程序類似 toothat 的傳訊標準。</span><span class="sxs-lookup"><span data-stu-id="1708d-146">Getting started with Premium Messaging is straightforward and hello process is similar toothat of Standard Messaging.</span></span> <span data-ttu-id="1708d-147">首先[建立命名空間](service-bus-create-namespace-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1708d-147">Begin by [creating a namespace](service-bus-create-namespace-portal.md).</span></span> <span data-ttu-id="1708d-148">請務必選取 [定價層] 之下的 [進階]。</span><span class="sxs-lookup"><span data-stu-id="1708d-148">Make sure you select **Premium** under **Pricing tier**.</span></span>

![create-premium-namespace][create-premium-namespace]

<span data-ttu-id="1708d-150">您也可以[使用 Azure Resource Manager 範本建立進階命名空間](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/)。</span><span class="sxs-lookup"><span data-stu-id="1708d-150">You can also create [Premium namespaces using Azure Resource Manager templates](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).</span></span>


## <a name="next-steps"></a><span data-ttu-id="1708d-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1708d-151">Next steps</span></span>

<span data-ttu-id="1708d-152">toolearn 有關 Service Bus 訊息的詳細資訊，請參閱下列主題中的 hello。</span><span class="sxs-lookup"><span data-stu-id="1708d-152">toolearn more about Service Bus Messaging, see hello following topics.</span></span>

* [<span data-ttu-id="1708d-153">Azure 服務匯流排進階傳訊簡介 (部落格文章)</span><span class="sxs-lookup"><span data-stu-id="1708d-153">Introducing Azure Service Bus Premium Messaging (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="1708d-154">Azure 服務匯流排進階傳訊簡介 (Channel9)</span><span class="sxs-lookup"><span data-stu-id="1708d-154">Introducing Azure Service Bus Premium Messaging (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="1708d-155">服務匯流排訊息概觀</span><span class="sxs-lookup"><span data-stu-id="1708d-155">Service Bus Messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="1708d-156">如何 toouse 服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="1708d-156">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
