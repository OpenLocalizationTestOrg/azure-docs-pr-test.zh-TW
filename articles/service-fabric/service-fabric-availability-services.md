---
title: "Service Fabric 服務的 aaaAvailability |Microsoft 文件"
description: "描述錯誤偵測、容錯移轉與服務復原"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a><span data-ttu-id="95941-103">Service Fabric 服務的可用性</span><span class="sxs-lookup"><span data-stu-id="95941-103">Availability of Service Fabric services</span></span>
<span data-ttu-id="95941-104">本文章概述 Service Fabric 如何維護服務的可用性。</span><span class="sxs-lookup"><span data-stu-id="95941-104">This article gives an overview of how Service Fabric maintains availability of a service.</span></span>

## <a name="availability-of-service-fabric-stateless-services"></a><span data-ttu-id="95941-105">Service Fabric 無狀態服務的可用性</span><span class="sxs-lookup"><span data-stu-id="95941-105">Availability of Service Fabric stateless services</span></span>
<span data-ttu-id="95941-106">Azure Service Fabric 服務可能是具狀態或無狀態。</span><span class="sxs-lookup"><span data-stu-id="95941-106">Azure Service Fabric services can be either stateful or stateless.</span></span> <span data-ttu-id="95941-107">無狀態服務是沒有任何應用程式服務[本機狀態](service-fabric-concepts-state.md)需要 toobe 高度可用或可靠。</span><span class="sxs-lookup"><span data-stu-id="95941-107">A stateless service is an application service that does not have any [local state](service-fabric-concepts-state.md) that needs toobe highly available or reliable.</span></span>

<span data-ttu-id="95941-108">建立無狀態服務需要定義 `InstanceCount`。</span><span class="sxs-lookup"><span data-stu-id="95941-108">Creating a stateless service requires defining an `InstanceCount`.</span></span> <span data-ttu-id="95941-109">hello 執行個體計數定義 hello hello 無狀態服務的應用程式邏輯，應該在 hello 叢集中執行的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="95941-109">hello instance count defines hello number of instances of hello stateless service's application logic that should be running in hello cluster.</span></span> <span data-ttu-id="95941-110">執行個體的 hello 數目增加為 hello 建議的向外延展無狀態服務的方式。</span><span class="sxs-lookup"><span data-stu-id="95941-110">Increasing hello number of instances is hello recommended way of scaling out a stateless service.</span></span>

<span data-ttu-id="95941-111">無狀態的名為 service 執行個體失敗時，某些合格 hello 叢集中節點上建立的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="95941-111">When an instance of a stateless named service fails, a new instance is created on some eligible node in hello cluster.</span></span> <span data-ttu-id="95941-112">例如，無狀態服務執行個體可能會在 Node1 上失敗並在 Node5 上重新建立。</span><span class="sxs-lookup"><span data-stu-id="95941-112">For example, a stateless service instance might fail on Node1 and be recreated on Node5.</span></span>

## <a name="availability-of-service-fabric-stateful-services"></a><span data-ttu-id="95941-113">Service Fabric 可設定狀態服務的可用性</span><span class="sxs-lookup"><span data-stu-id="95941-113">Availability of Service Fabric stateful services</span></span>
<span data-ttu-id="95941-114">具狀態服務具有某些與其相關聯的狀態。</span><span class="sxs-lookup"><span data-stu-id="95941-114">A stateful service has some state associated with it.</span></span> <span data-ttu-id="95941-115">在 Service Fabric 中，可設定狀態服務會模型化為複本集。</span><span class="sxs-lookup"><span data-stu-id="95941-115">In Service Fabric, a stateful service is modeled as a set of replicas.</span></span> <span data-ttu-id="95941-116">每個複本是 hello hello 服務也有一份該服務的 hello 狀態碼的執行個體。</span><span class="sxs-lookup"><span data-stu-id="95941-116">Each replica is a running instance of hello code of hello service that also has a copy of hello state for that service.</span></span> <span data-ttu-id="95941-117">讀取和寫入作業會執行一個複本 （稱為 hello 主要）。</span><span class="sxs-lookup"><span data-stu-id="95941-117">Read and write operations are performed at one replica (called hello Primary).</span></span> <span data-ttu-id="95941-118">會從寫入作業變更 toostate*複寫*toohello hello 複本設定 （稱為作用中次要資料庫） 中的其他複本及套用。</span><span class="sxs-lookup"><span data-stu-id="95941-118">Changes toostate from write operations are *replicated* toohello other replicas in hello replica set (called Active Secondaries) and applied.</span></span> 

<span data-ttu-id="95941-119">只能有一個「主要複本」，但可以有多個「作用中次要複本」。</span><span class="sxs-lookup"><span data-stu-id="95941-119">There can be only one Primary replica, but there can be multiple Active Secondary replicas.</span></span> <span data-ttu-id="95941-120">作用中次要複本的 hello 數目可設定，而有較多的複本可容許更多並行的軟體和硬體故障。</span><span class="sxs-lookup"><span data-stu-id="95941-120">hello number of Active Secondary replicas is configurable, and a higher number of replicas can tolerate a greater number of concurrent software and hardware failures.</span></span>

<span data-ttu-id="95941-121">如果 hello 主要複本已關閉時，Service Fabric，使其中一個 hello 作用中次要複本 hello 新的主要複本。</span><span class="sxs-lookup"><span data-stu-id="95941-121">If hello Primary replica goes down, Service Fabric makes one of hello Active Secondary replicas hello new Primary replica.</span></span> <span data-ttu-id="95941-122">這個作用中次要複本已有更新的 hello 版本 hello 狀態 (透過*複寫*)，以及它可以繼續處理其他的讀取和寫入作業。</span><span class="sxs-lookup"><span data-stu-id="95941-122">This Active Secondary replica already has hello updated version of hello state (via *replication*), and it can continue processing further read and write operations.</span></span>

<span data-ttu-id="95941-123">主要或作用中次要複本的這個概念，稱為 hello 複本角色。</span><span class="sxs-lookup"><span data-stu-id="95941-123">This concept, of a replica being either a Primary or Active Secondary, is known as hello Replica Role.</span></span>

### <a name="replica-roles"></a><span data-ttu-id="95941-124">複本角色</span><span class="sxs-lookup"><span data-stu-id="95941-124">Replica roles</span></span>
<span data-ttu-id="95941-125">hello 複本的角色是狀態的使用的 toomanage hello 生命週期的 hello 受該複本。</span><span class="sxs-lookup"><span data-stu-id="95941-125">hello role of a replica is used toomanage hello life cycle of hello state being managed by that replica.</span></span> <span data-ttu-id="95941-126">扮演「主要」角色的複本會為讀取要求提供服務。</span><span class="sxs-lookup"><span data-stu-id="95941-126">A replica whose role is Primary services read requests.</span></span> <span data-ttu-id="95941-127">hello 主要也可以更新其狀態，並複寫 hello 變更處理所有寫入要求。</span><span class="sxs-lookup"><span data-stu-id="95941-127">hello Primary also handles all write requests by updating its state and replicating hello changes.</span></span> <span data-ttu-id="95941-128">這些變更會套用的 toohello hello 複本集中作用中次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="95941-128">These changes are applied toohello Active Secondaries in hello replica set.</span></span> <span data-ttu-id="95941-129">作用中次要的 hello 作業是 tooreceive hello 主要複本的狀態變更已複寫，並更新其 hello 狀態的檢視。</span><span class="sxs-lookup"><span data-stu-id="95941-129">hello job of an Active Secondary is tooreceive state changes that hello Primary replica has replicated and update its view of hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="95941-130">較高層級的程式設計模型例如[Reliable Actors](service-fabric-reliable-actors-introduction.md)和[可靠服務](service-fabric-reliable-services-introduction.md)隱藏 hello 概念 hello 位開發人員的複本角色。</span><span class="sxs-lookup"><span data-stu-id="95941-130">Higher-level programming models such as [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) hide hello concept of replica role from hello developer.</span></span> <span data-ttu-id="95941-131">動作項目，在 hello 概念的角色中不需要，同時它主要簡化在大部分情況下的服務。</span><span class="sxs-lookup"><span data-stu-id="95941-131">In Actors, hello notion of role is unnecessary, while in Services it is largely simplified for most scenarios.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="95941-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95941-132">Next steps</span></span>
<span data-ttu-id="95941-133">如需有關 Service Fabric 概念的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="95941-133">For more information on Service Fabric concepts, see hello following articles:</span></span>

- [<span data-ttu-id="95941-134">調整 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="95941-134">Scaling Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
- [<span data-ttu-id="95941-135">分割 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="95941-135">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
- [<span data-ttu-id="95941-136">定義和管理狀態</span><span class="sxs-lookup"><span data-stu-id="95941-136">Defining and managing state</span></span>](service-fabric-concepts-state.md)
- [<span data-ttu-id="95941-137">Reliable Services</span><span class="sxs-lookup"><span data-stu-id="95941-137">Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
