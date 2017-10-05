---
title: "Azure 服務匯流排的訊息處理架構 | Microsoft Docs"
description: "描述 Azure 服務匯流排的訊息處理架構。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 83456d775c5ff2a2476ba46e9c78a8dc1bb482e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="service-bus-architecture"></a><span data-ttu-id="be716-103">服務匯流排架構</span><span class="sxs-lookup"><span data-stu-id="be716-103">Service Bus architecture</span></span>
<span data-ttu-id="be716-104">本文章描述 Azure 服務匯流排的訊息處理架構。</span><span class="sxs-lookup"><span data-stu-id="be716-104">This article describes the message processing architecture of Azure Service Bus.</span></span>

## <a name="service-bus-scale-units"></a><span data-ttu-id="be716-105">服務匯流排縮放單位</span><span class="sxs-lookup"><span data-stu-id="be716-105">Service Bus scale units</span></span>
<span data-ttu-id="be716-106">服務匯流排依 *縮放單位*組織。</span><span class="sxs-lookup"><span data-stu-id="be716-106">Service Bus is organized by *scale units*.</span></span> <span data-ttu-id="be716-107">縮放單位是部署單位，並包含執行服務所需的所有元件。</span><span class="sxs-lookup"><span data-stu-id="be716-107">A scale unit is a unit of deployment and contains all components required run the service.</span></span> <span data-ttu-id="be716-108">每個區域都會部署一或多個服務匯流排縮放單位。</span><span class="sxs-lookup"><span data-stu-id="be716-108">Each region deploys one or more Service Bus scale units.</span></span>

<span data-ttu-id="be716-109">服務匯流排命名空間會對應到一個縮放單位。</span><span class="sxs-lookup"><span data-stu-id="be716-109">A Service Bus namespace is mapped to a scale unit.</span></span> <span data-ttu-id="be716-110">縮放單位會處理所有類型的服務匯流排實體 (佇列、主題、訂用帳戶)。</span><span class="sxs-lookup"><span data-stu-id="be716-110">The scale unit handles all types of Service Bus entities (queues, topics, subscriptions).</span></span> <span data-ttu-id="be716-111">服務匯流排縮放單位是由下列元件所組成：</span><span class="sxs-lookup"><span data-stu-id="be716-111">A Service Bus scale unit consists of the following components:</span></span>

* <span data-ttu-id="be716-112">**一組閘道器節點。**</span><span class="sxs-lookup"><span data-stu-id="be716-112">**A set of gateway nodes.**</span></span> <span data-ttu-id="be716-113">閘道節點會驗證傳入要求。</span><span class="sxs-lookup"><span data-stu-id="be716-113">Gateway nodes authenticate incoming requests.</span></span> <span data-ttu-id="be716-114">每個閘道器節點都有一個公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="be716-114">Each gateway node has a public IP address.</span></span>
* <span data-ttu-id="be716-115">**一組訊息代理程式節點。**</span><span class="sxs-lookup"><span data-stu-id="be716-115">**A set of messaging broker nodes.**</span></span> <span data-ttu-id="be716-116">訊息代理程式節點會處理關於訊息實體的要求。</span><span class="sxs-lookup"><span data-stu-id="be716-116">Messaging broker nodes process requests concerning messaging entities.</span></span>
* <span data-ttu-id="be716-117">**一個閘道器存放區。**</span><span class="sxs-lookup"><span data-stu-id="be716-117">**One gateway store.**</span></span> <span data-ttu-id="be716-118">閘道器存放區會保存此縮放單位中定義的每個實體的資料。</span><span class="sxs-lookup"><span data-stu-id="be716-118">The gateway store holds the data for every entity that is defined in this scale unit.</span></span> <span data-ttu-id="be716-119">閘道器存放區是在 SQL Azure 資料庫上實作。</span><span class="sxs-lookup"><span data-stu-id="be716-119">The gateway store is implemented on top of a SQL Azure database.</span></span>
* <span data-ttu-id="be716-120">**多個訊息存放區。**</span><span class="sxs-lookup"><span data-stu-id="be716-120">**Multiple messaging stores.**</span></span> <span data-ttu-id="be716-121">訊息存放區會保存此縮放單位中定義的所有佇列、主題和訂用帳戶的訊息。</span><span class="sxs-lookup"><span data-stu-id="be716-121">Messaging stores hold the messages of all queues, topics and subscriptions that are defined in this scale unit.</span></span> <span data-ttu-id="be716-122">它也包含所有訂用帳戶資料。</span><span class="sxs-lookup"><span data-stu-id="be716-122">It also contains all subscription data.</span></span> <span data-ttu-id="be716-123">除非啟用了[分割傳訊實體](service-bus-partitioning.md)，佇列或主題才會對應至一個傳訊存放區。</span><span class="sxs-lookup"><span data-stu-id="be716-123">Unless [partitioning messaging entities](service-bus-partitioning.md) is enabled, a queue or topic is mapped to one messaging store.</span></span> <span data-ttu-id="be716-124">訂用帳戶是儲存在與父項主題相同的訊息存放區。</span><span class="sxs-lookup"><span data-stu-id="be716-124">Subscriptions are stored in the same messaging store as their parent topic.</span></span> <span data-ttu-id="be716-125">除了服務匯流排[進階傳訊](service-bus-premium-messaging.md)以外，訊息存放區會在 SQL Azure 資料庫之上實作。</span><span class="sxs-lookup"><span data-stu-id="be716-125">Except for Service Bus [Premium Messaging](service-bus-premium-messaging.md), the messaging stores are implemented on top of SQL Azure databases.</span></span>

## <a name="containers"></a><span data-ttu-id="be716-126">容器</span><span class="sxs-lookup"><span data-stu-id="be716-126">Containers</span></span>
<span data-ttu-id="be716-127">每個訊息實體都會指派給特定的容器。</span><span class="sxs-lookup"><span data-stu-id="be716-127">Each messaging entity is assigned a specific container.</span></span> <span data-ttu-id="be716-128">容器是一種邏輯建構，僅使用一個訊息存放區來儲存此容器所有相關資料。</span><span class="sxs-lookup"><span data-stu-id="be716-128">A container is a logical construct that uses exactly one messaging store to store all relevant data for this container.</span></span> <span data-ttu-id="be716-129">每個容器都會被指派至訊息代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="be716-129">Each container is assigned to a messaging broker node.</span></span> <span data-ttu-id="be716-130">通常，容器較訊息代理程式節點多。</span><span class="sxs-lookup"><span data-stu-id="be716-130">Typically, there are more containers than messaging broker nodes.</span></span> <span data-ttu-id="be716-131">因此，每個訊息代理程式節點會載入多個容器。</span><span class="sxs-lookup"><span data-stu-id="be716-131">Therefore, each messaging broker node loads multiple containers.</span></span> <span data-ttu-id="be716-132">訊息代理程式節點的容器分配會經過組織，使得平均地載入所有的訊息代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="be716-132">The distribution of containers to a messaging broker node is organized such that all messaging broker nodes are equally loaded.</span></span> <span data-ttu-id="be716-133">如果載入模式變更 (例如其中一個容器變得十分忙碌)，或訊息代理程式節點會變成暫時無法使用，容器會在訊息代理程式節點間重新分配。</span><span class="sxs-lookup"><span data-stu-id="be716-133">If the load pattern changes (for example, one of the containers gets very busy), or if a messaging broker node becomes temporarily unavailable, the containers are redistributed among the messaging broker nodes.</span></span>

## <a name="processing-of-incoming-messaging-requests"></a><span data-ttu-id="be716-134">處理內送訊息要求</span><span class="sxs-lookup"><span data-stu-id="be716-134">Processing of incoming messaging requests</span></span>
<span data-ttu-id="be716-135">當用戶端傳送要求至服務匯流排時，Azure 負載平衡器會將其路由到任何一個閘道器節點。</span><span class="sxs-lookup"><span data-stu-id="be716-135">When a client sends a request to Service Bus, the Azure load balancer routes it to any of the gateway nodes.</span></span> <span data-ttu-id="be716-136">閘道器節點會授權要求。</span><span class="sxs-lookup"><span data-stu-id="be716-136">The gateway node authorizes the request.</span></span> <span data-ttu-id="be716-137">如果要求考量訊息實體 (佇列、主題、訂用帳戶)，則閘道器節點會在閘道器存放區中在尋找實體，並判斷實體位在哪個訊息存放區。</span><span class="sxs-lookup"><span data-stu-id="be716-137">If the request concerns a messaging entity (queue, topic, subscription), the gateway node looks up the entity in the gateway store and determines in which messaging store the entity is located.</span></span> <span data-ttu-id="be716-138">它接著會查詢哪些訊息代理程式節點目前正在服務此容器，並將要求傳送至該訊息代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="be716-138">It then looks up which messaging broker node is currently servicing this container, and sends the request to that messaging broker node.</span></span> <span data-ttu-id="be716-139">訊息代理程式節點會處理要求並更新容器存放區中的實體狀態。</span><span class="sxs-lookup"><span data-stu-id="be716-139">The messaging broker node processes the request and updates the entity state in the container store.</span></span> <span data-ttu-id="be716-140">訊息代理程式節點接著會傳送回應給閘道器節點，閘道器節點會傳送適當的回應給發出原始要求的用戶端。</span><span class="sxs-lookup"><span data-stu-id="be716-140">The messaging broker node then sends the response back to the gateway node, which sends an appropriate response back to the client that issued the original request.</span></span>

![處理內送訊息要求](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a><span data-ttu-id="be716-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be716-142">Next steps</span></span>
<span data-ttu-id="be716-143">既然您已閱讀服務匯流排架構的概觀，請參閱下列連結取得詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="be716-143">Now that you've read an overview of Service Bus architecture, visit the following links for more information:</span></span>

* [<span data-ttu-id="be716-144">服務匯流排訊息概觀</span><span class="sxs-lookup"><span data-stu-id="be716-144">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="be716-145">服務匯流排基本概念</span><span class="sxs-lookup"><span data-stu-id="be716-145">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="be716-146">使用服務匯流排佇列的佇列訊息解決方案</span><span class="sxs-lookup"><span data-stu-id="be716-146">A queued messaging solution using Service Bus queues</span></span>](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


