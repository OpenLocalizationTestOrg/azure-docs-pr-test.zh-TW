---
title: "Azure 服務匯流排進階和標準傳訊定價層概觀 | Microsoft Docs"
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
ms.openlocfilehash: 3fe666da149085d14c3839a64b50765eea483e05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a><span data-ttu-id="928bb-103">服務匯流排進階和標準傳訊層級</span><span class="sxs-lookup"><span data-stu-id="928bb-103">Service Bus Premium and Standard messaging tiers</span></span>

<span data-ttu-id="928bb-104">服務匯流排傳訊 (包含佇列和主題等實體) 結合雲端級別的企業傳訊功能與豐富的發佈-訂閱語意。</span><span class="sxs-lookup"><span data-stu-id="928bb-104">Service Bus Messaging, which includes entities such as queues and topics, combines enterprise messaging capabilities with rich publish-subscribe semantics at cloud scale.</span></span> <span data-ttu-id="928bb-105">服務匯流排傳訊作為許多縝密雲端解決方案的通訊骨幹。</span><span class="sxs-lookup"><span data-stu-id="928bb-105">Service Bus Messaging is used as the communication backbone for many sophisticated cloud solutions.</span></span>

<span data-ttu-id="928bb-106">服務匯流排傳訊的「進階」層級可滿足一般客戶對於關鍵任務應用程式的規模、效能和可用性要求。</span><span class="sxs-lookup"><span data-stu-id="928bb-106">The *Premium* tier of Service Bus Messaging addresses common customer requests around scale, performance, and availability for mission-critical applications.</span></span> <span data-ttu-id="928bb-107">雖然功能組幾乎完全相同，但這兩層級的服務匯流排傳訊設計用來服務不同的使用案例。</span><span class="sxs-lookup"><span data-stu-id="928bb-107">Although the feature sets are nearly identical, these two tiers of Service Bus Messaging are designed to serve different use cases.</span></span>

<span data-ttu-id="928bb-108">下表強調大致的一些差異。</span><span class="sxs-lookup"><span data-stu-id="928bb-108">Some high-level differences are highlighted in the following table.</span></span>

| <span data-ttu-id="928bb-109">高級</span><span class="sxs-lookup"><span data-stu-id="928bb-109">Premium</span></span> | <span data-ttu-id="928bb-110">標準</span><span class="sxs-lookup"><span data-stu-id="928bb-110">Standard</span></span> |
| --- | --- |
| <span data-ttu-id="928bb-111">高輸送量</span><span class="sxs-lookup"><span data-stu-id="928bb-111">High throughput</span></span> |<span data-ttu-id="928bb-112">變動輸送量</span><span class="sxs-lookup"><span data-stu-id="928bb-112">Variable throughput</span></span> |
| <span data-ttu-id="928bb-113">可預測的效能</span><span class="sxs-lookup"><span data-stu-id="928bb-113">Predictable performance</span></span> |<span data-ttu-id="928bb-114">變動延遲</span><span class="sxs-lookup"><span data-stu-id="928bb-114">Variable latency</span></span> |
| <span data-ttu-id="928bb-115">固定價格</span><span class="sxs-lookup"><span data-stu-id="928bb-115">Fixed pricing</span></span> |<span data-ttu-id="928bb-116">隨用隨付變動價格</span><span class="sxs-lookup"><span data-stu-id="928bb-116">Pay as you go variable pricing</span></span> |
| <span data-ttu-id="928bb-117">相應增加和相應減少工作負載的能力</span><span class="sxs-lookup"><span data-stu-id="928bb-117">Ability to scale workload up and down</span></span> |<span data-ttu-id="928bb-118">N/A</span><span class="sxs-lookup"><span data-stu-id="928bb-118">N/A</span></span> |
| <span data-ttu-id="928bb-119">訊息大小上限為 1 MB</span><span class="sxs-lookup"><span data-stu-id="928bb-119">Message size up to 1 MB</span></span> |<span data-ttu-id="928bb-120">訊息大小上限為 256 KB</span><span class="sxs-lookup"><span data-stu-id="928bb-120">Message size up to 256 KB</span></span> |

<span data-ttu-id="928bb-121">**服務匯流排進階傳訊**提供 CPU 和記憶體層級的資源隔離，讓每個客戶工作負載能隔離執行。</span><span class="sxs-lookup"><span data-stu-id="928bb-121">**Service Bus Premium Messaging** provides resource isolation at the CPU and memory level so that each customer workload runs in isolation.</span></span> <span data-ttu-id="928bb-122">此資源容器稱為「傳訊單位」 。</span><span class="sxs-lookup"><span data-stu-id="928bb-122">This resource container is called a *messaging unit*.</span></span> <span data-ttu-id="928bb-123">每個進階命名空間都會被配置至少一個傳訊單位。</span><span class="sxs-lookup"><span data-stu-id="928bb-123">Each premium namespace is allocated at least one messaging unit.</span></span> <span data-ttu-id="928bb-124">您可以為每個服務匯流排進階命名空間購買 1、2 或 4 個傳訊單位。</span><span class="sxs-lookup"><span data-stu-id="928bb-124">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span></span> <span data-ttu-id="928bb-125">單一工作負載或實體可以跨越多個傳訊單位，而傳訊單位數目可以隨意變更，雖然計費是依 24 小時或每日費率收費。</span><span class="sxs-lookup"><span data-stu-id="928bb-125">A single workload or entity can span multiple messaging units and the number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span></span> <span data-ttu-id="928bb-126">結果是您的服務匯流排方案的效能可預測並可重複。</span><span class="sxs-lookup"><span data-stu-id="928bb-126">The result is predictable and repeatable performance for your Service Bus-based solution.</span></span>

<span data-ttu-id="928bb-127">此效能不僅更可預測並可取得，而且還更快速。</span><span class="sxs-lookup"><span data-stu-id="928bb-127">Not only is this performance more predictable and available, but it is also faster.</span></span> <span data-ttu-id="928bb-128">服務匯流排進階傳訊是以 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)中引進的儲存引擎為建置基礎。</span><span class="sxs-lookup"><span data-stu-id="928bb-128">Service Bus Premium Messaging builds on the storage engine introduced in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span> <span data-ttu-id="928bb-129">使用進階訊息，尖峰效能的速度比標準層級的速度快很多。</span><span class="sxs-lookup"><span data-stu-id="928bb-129">With Premium Messaging, peak performance is much faster than with the Standard tier.</span></span>

## <a name="premium-messaging-technical-differences"></a><span data-ttu-id="928bb-130">進階傳訊技術差異</span><span class="sxs-lookup"><span data-stu-id="928bb-130">Premium Messaging technical differences</span></span>

<span data-ttu-id="928bb-131">下列各節討論進階與標準傳訊層之間的一些差異。</span><span class="sxs-lookup"><span data-stu-id="928bb-131">The following sections discuss a few differences between Premium and Standard messaging tiers.</span></span>

### <a name="partitioned-queues-and-topics"></a><span data-ttu-id="928bb-132">分割的佇列和主題</span><span class="sxs-lookup"><span data-stu-id="928bb-132">Partitioned queues and topics</span></span>

<span data-ttu-id="928bb-133">進階傳訊支援分割的佇列和主題；事實上這些實體一律會進行分割 (且無法停用)。</span><span class="sxs-lookup"><span data-stu-id="928bb-133">Partitioned queues and topics are supported in Premium Messaging; in fact these entities are always partitioned (and cannot be disabled).</span></span> <span data-ttu-id="928bb-134">不過，進階分割的佇列和主題在服務匯流排傳訊的標準和基本層中的運作方式不同。</span><span class="sxs-lookup"><span data-stu-id="928bb-134">However, Premium partitioned queues and topics do not function the same way as in the Standard and Basic tiers of Service Bus messaging.</span></span> <span data-ttu-id="928bb-135">進階傳訊不會使用 SQL 做為資料存放區，而且不可能再有與共用平台相關聯的資源競爭。</span><span class="sxs-lookup"><span data-stu-id="928bb-135">Premium messaging does not use SQL as a data store and no longer has the possible resource competition associated with a shared platform.</span></span> <span data-ttu-id="928bb-136">因此，資料分割不一定能夠改善效能。</span><span class="sxs-lookup"><span data-stu-id="928bb-136">As a result, partitioning is not necessary to improve performance.</span></span> <span data-ttu-id="928bb-137">此外，資料分割計數已從標準傳訊中的 16 個資料分割變更為進階傳訊中的 2 個資料分割。</span><span class="sxs-lookup"><span data-stu-id="928bb-137">Additionally, the partition count has been changed from 16 partitions in Standard Messaging to 2 partitions in Premium.</span></span> <span data-ttu-id="928bb-138">擁有 2 個資料分割可確保可用性，而且是比較適合進階執行階段環境的數字。</span><span class="sxs-lookup"><span data-stu-id="928bb-138">Having two partitions ensures availability and is a more appropriate number for the Premium runtime environment.</span></span> 

<span data-ttu-id="928bb-139">透過進階傳訊，當您使用 [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes) 指定實體的大小時，會將 2 個分割的大小平均分割，這不同於[標準分割的實體](service-bus-partitioning.md#standard)，其中總大小是 16 乘以指定的大小。</span><span class="sxs-lookup"><span data-stu-id="928bb-139">With Premium messaging, when you specify the size of an entity with [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), that size is split equally across the 2 partitions, unlike [Standard partitioned entities](service-bus-partitioning.md#standard) in which the total size is 16 times the specified size.</span></span> 

<span data-ttu-id="928bb-140">如需分割的詳細資訊，請參閱[分割的佇列和主題](service-bus-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="928bb-140">For more information about partitioning, see [Partitioned queues and topics](service-bus-partitioning.md).</span></span>

### <a name="express-entities"></a><span data-ttu-id="928bb-141">快速實體</span><span class="sxs-lookup"><span data-stu-id="928bb-141">Express entities</span></span>

<span data-ttu-id="928bb-142">因為進階傳訊是在完全隔離的執行階段環境中執行，所以在進階命名空間中並不支援快速實體。</span><span class="sxs-lookup"><span data-stu-id="928bb-142">Because Premium messaging runs in a completely isolated run-time environment, express entities are not supported in Premium namespaces.</span></span> <span data-ttu-id="928bb-143">如需快速功能的詳細資訊，請參閱 [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) 屬性。</span><span class="sxs-lookup"><span data-stu-id="928bb-143">For more information about the express feature, see the [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property.</span></span>

<span data-ttu-id="928bb-144">如果您的程式碼是在標準傳訊下執行，而您想要將它移植到高階層，請確定 [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) 屬性設為 **false** (預設值)。</span><span class="sxs-lookup"><span data-stu-id="928bb-144">If you have code running under Standard messaging and want to port it to the Premium tier, make sure the [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property is set to **false** (the default value).</span></span>

## <a name="get-started-with-premium-messaging"></a><span data-ttu-id="928bb-145">開始使用進階傳訊</span><span class="sxs-lookup"><span data-stu-id="928bb-145">Get started with Premium Messaging</span></span>

<span data-ttu-id="928bb-146">開始使用進階訊息非常簡單，其程序類似於標準傳訊。</span><span class="sxs-lookup"><span data-stu-id="928bb-146">Getting started with Premium Messaging is straightforward and the process is similar to that of Standard Messaging.</span></span> <span data-ttu-id="928bb-147">首先[建立命名空間](service-bus-create-namespace-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="928bb-147">Begin by [creating a namespace](service-bus-create-namespace-portal.md).</span></span> <span data-ttu-id="928bb-148">請務必選取 [定價層] 之下的 [進階]。</span><span class="sxs-lookup"><span data-stu-id="928bb-148">Make sure you select **Premium** under **Pricing tier**.</span></span>

![create-premium-namespace][create-premium-namespace]

<span data-ttu-id="928bb-150">您也可以[使用 Azure Resource Manager 範本建立進階命名空間](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/)。</span><span class="sxs-lookup"><span data-stu-id="928bb-150">You can also create [Premium namespaces using Azure Resource Manager templates](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).</span></span>


## <a name="next-steps"></a><span data-ttu-id="928bb-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="928bb-151">Next steps</span></span>

<span data-ttu-id="928bb-152">若要深入了解服務匯流排訊息，請參閱下列主題。</span><span class="sxs-lookup"><span data-stu-id="928bb-152">To learn more about Service Bus Messaging, see the following topics.</span></span>

* [<span data-ttu-id="928bb-153">Azure 服務匯流排進階傳訊簡介 (部落格文章)</span><span class="sxs-lookup"><span data-stu-id="928bb-153">Introducing Azure Service Bus Premium Messaging (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="928bb-154">Azure 服務匯流排進階傳訊簡介 (Channel9)</span><span class="sxs-lookup"><span data-stu-id="928bb-154">Introducing Azure Service Bus Premium Messaging (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="928bb-155">服務匯流排訊息概觀</span><span class="sxs-lookup"><span data-stu-id="928bb-155">Service Bus Messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="928bb-156">如何使用服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="928bb-156">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
