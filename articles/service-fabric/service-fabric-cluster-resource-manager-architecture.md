---
title: "aaaResource Manager 架構 |Microsoft 文件"
description: "Service Fabric 叢集資源管理員的架構概觀。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a><span data-ttu-id="90e8d-103">叢集資源管理員架構概觀</span><span class="sxs-lookup"><span data-stu-id="90e8d-103">Cluster resource manager architecture overview</span></span>
<span data-ttu-id="90e8d-104">hello Service Fabric 叢集資源管理員會提供集中的服務執行於 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="90e8d-104">hello Service Fabric Cluster Resource Manager is a central service that runs in hello cluster.</span></span> <span data-ttu-id="90e8d-105">它會管理在 hello 叢集中，特別是使用尊重 tooresource 耗用量和任何放置規則的 hello 服務 hello 預期狀態。</span><span class="sxs-lookup"><span data-stu-id="90e8d-105">It manages hello desired state of hello services in hello cluster, particularly with respect tooresource consumption and any placement rules.</span></span> 

<span data-ttu-id="90e8d-106">在叢集中的 toomanage hello 資源，hello Service Fabric 叢集資源管理員都必須有數個資訊片段：</span><span class="sxs-lookup"><span data-stu-id="90e8d-106">toomanage hello resources in your cluster, hello Service Fabric Cluster Resource Manager must have several pieces of information:</span></span>

- <span data-ttu-id="90e8d-107">目前有哪些服務</span><span class="sxs-lookup"><span data-stu-id="90e8d-107">Which services currently exist</span></span>
- <span data-ttu-id="90e8d-108">每個服務的目前 (或預設) 資源耗用量</span><span class="sxs-lookup"><span data-stu-id="90e8d-108">Each service's current (or default) resource consumption</span></span> 
- <span data-ttu-id="90e8d-109">hello 剩餘叢集容量</span><span class="sxs-lookup"><span data-stu-id="90e8d-109">hello remaining cluster capacity</span></span> 
- <span data-ttu-id="90e8d-110">hello 叢集中的節點 hello hello 產能</span><span class="sxs-lookup"><span data-stu-id="90e8d-110">hello capacity of hello nodes in hello cluster</span></span> 
- <span data-ttu-id="90e8d-111">每個節點上所耗用的資源的 hello 數量</span><span class="sxs-lookup"><span data-stu-id="90e8d-111">hello amount of resources consumed on each node</span></span>

<span data-ttu-id="90e8d-112">經過一段時間，可以變更的特定服務的 hello 資源耗用量，服務通常很重視多個資源類型。</span><span class="sxs-lookup"><span data-stu-id="90e8d-112">hello resource consumption of a given service can change over time, and services usually care about more than one type of resource.</span></span> <span data-ttu-id="90e8d-113">在不同的服務之間，可能會同時測量真正實物和實體資源。</span><span class="sxs-lookup"><span data-stu-id="90e8d-113">Across different services, there may be both real physical and physical resources being measured.</span></span> <span data-ttu-id="90e8d-114">服務可能追蹤實體計量，例如記憶體和磁碟耗用量。</span><span class="sxs-lookup"><span data-stu-id="90e8d-114">Services may track physical metrics like memory and disk consumption.</span></span> <span data-ttu-id="90e8d-115">服務可能較關心邏輯計量，例如 "WorkQueueDepth" 或 "TotalRequests"。</span><span class="sxs-lookup"><span data-stu-id="90e8d-115">More commonly, services may care about logical metrics - things like "WorkQueueDepth" or "TotalRequests".</span></span> <span data-ttu-id="90e8d-116">邏輯與實體度量可在 hello 相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="90e8d-116">Both logical and physical metrics can be used in hello same cluster.</span></span> <span data-ttu-id="90e8d-117">度量可以橫跨多個服務或特定 tooa 特定服務。</span><span class="sxs-lookup"><span data-stu-id="90e8d-117">Metrics can be shared across many services or be specific tooa particular service.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="90e8d-118">其他考量</span><span class="sxs-lookup"><span data-stu-id="90e8d-118">Other considerations</span></span>
<span data-ttu-id="90e8d-119">hello 的擁有者和運算子的 hello 叢集可以不同於 hello 服務和應用程式的作者，或在最小值為 hello 相同穿不同 hats 的人員。</span><span class="sxs-lookup"><span data-stu-id="90e8d-119">hello owners and operators of hello cluster can be different from hello service and application authors, or at a minimum are hello same people wearing different hats.</span></span> <span data-ttu-id="90e8d-120">當您開發應用程式時，您知道它所需的一些事項。</span><span class="sxs-lookup"><span data-stu-id="90e8d-120">When you develop your application you know a few things about what it requires.</span></span> <span data-ttu-id="90e8d-121">您必須估計的 hello 便會取用的資源和不同的服務應部署。</span><span class="sxs-lookup"><span data-stu-id="90e8d-121">You have an estimate of hello resources it will consume and how different services should be deployed.</span></span> <span data-ttu-id="90e8d-122">比方說，hello web 層都需要 toorun 節點公開 toohello 網際網路上的時不應該 hello 資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="90e8d-122">For example, hello web tier needs toorun on nodes exposed toohello Internet, while hello database services should not.</span></span> <span data-ttu-id="90e8d-123">另舉一例，hello web 服務可能會限制 CPU 和網路，同時 hello 資料層服務在意更多記憶體和磁碟的耗用量。</span><span class="sxs-lookup"><span data-stu-id="90e8d-123">As another example, hello web services are probably constrained by CPU and network, while hello data tier services care more about memory and disk consumption.</span></span> <span data-ttu-id="90e8d-124">不過，處理實際執行環境，該服務的網站即時事件或使用者管理升級 toohello 服務的 hello 人有不同的工作 toodo，而且需要不同的工具。</span><span class="sxs-lookup"><span data-stu-id="90e8d-124">However, hello person handling a live-site incident for that service in production, or who is managing an upgrade toohello service has a different job toodo, and requires different tools.</span></span> 

<span data-ttu-id="90e8d-125">Hello 叢集和服務是動態的：</span><span class="sxs-lookup"><span data-stu-id="90e8d-125">Both hello cluster and services are dynamic:</span></span>

- <span data-ttu-id="90e8d-126">hello hello 叢集中的節點數目可以擴增和縮減</span><span class="sxs-lookup"><span data-stu-id="90e8d-126">hello number of nodes in hello cluster can grow and shrink</span></span>
- <span data-ttu-id="90e8d-127">不同大小和類型的節點可能轉瞬即逝</span><span class="sxs-lookup"><span data-stu-id="90e8d-127">Nodes of different sizes and types can come and go</span></span>
- <span data-ttu-id="90e8d-128">服務可能建立、移除和變更所需的資源配置和放置規則</span><span class="sxs-lookup"><span data-stu-id="90e8d-128">Services can be created, removed, and change their desired resource allocations and placement rules</span></span>
- <span data-ttu-id="90e8d-129">升級或其他管理作業無法回復透過 hello 應用程式在 hello 叢集基礎結構層級</span><span class="sxs-lookup"><span data-stu-id="90e8d-129">Upgrades or other management operations can roll through hello cluster at hello application on infrastructure levels</span></span>
- <span data-ttu-id="90e8d-130">隨時都可能發生問題。</span><span class="sxs-lookup"><span data-stu-id="90e8d-130">Failures can happen at any time.</span></span>

## <a name="cluster-resource-manager-components-and-data-flow"></a><span data-ttu-id="90e8d-131">叢集資源管理員元件和資料流程</span><span class="sxs-lookup"><span data-stu-id="90e8d-131">Cluster resource manager components and data flow</span></span>
<span data-ttu-id="90e8d-132">hello 叢集資源管理員會在這些服務每個服務物件有 tootrack hello 需求的每個服務和 hello 消耗的資源。</span><span class="sxs-lookup"><span data-stu-id="90e8d-132">hello Cluster Resource Manager has tootrack hello requirements of each service and hello consumption of resources by each service object within those services.</span></span> <span data-ttu-id="90e8d-133">hello 叢集資源管理員有兩個概念的部分： 在每個節點和容錯的服務執行的代理程式。</span><span class="sxs-lookup"><span data-stu-id="90e8d-133">hello Cluster Resource Manager has two conceptual parts: agents that run on each node and a fault-tolerant service.</span></span> <span data-ttu-id="90e8d-134">hello 上每個節點追蹤載入的代理程式從報表服務，彙總，並定期回報。</span><span class="sxs-lookup"><span data-stu-id="90e8d-134">hello agents on each node track load reports from services, aggregate them, and periodically report them.</span></span> <span data-ttu-id="90e8d-135">hello 叢集資源管理員服務彙總所有 hello 資訊從 hello 本機代理程式，並根據其目前組態的回應。</span><span class="sxs-lookup"><span data-stu-id="90e8d-135">hello Cluster Resource Manager service aggregates all hello information from hello local agents and reacts based on its current configuration.</span></span>

<span data-ttu-id="90e8d-136">讓我們看看下列圖表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="90e8d-136">Let’s look at hello following diagram:</span></span>

<span data-ttu-id="90e8d-137"><center>
![資源平衡器架構][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="90e8d-137"><center>
![Resource Balancer Architecture][Image1]
</center></span></span>

<span data-ttu-id="90e8d-138">執行階段可能發生許多變化。</span><span class="sxs-lookup"><span data-stu-id="90e8d-138">During runtime, there are many changes that could happen.</span></span> <span data-ttu-id="90e8d-139">例如，假設 hello 量資源的某些服務取用的變更，某些服務失敗，以及一些節點結合與離開 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="90e8d-139">For example, let’s say hello amount of resources some services consume changes, some services fail, and some nodes join and leave hello cluster.</span></span> <span data-ttu-id="90e8d-140">在節點上的所有 hello 變更會彙總，並定期傳送 toohello 叢集資源管理員服務 (1，2) 它們會在此再次彙總、 分析，然後儲存。</span><span class="sxs-lookup"><span data-stu-id="90e8d-140">All hello changes on a node are aggregated and periodically sent toohello Cluster Resource Manager service (1,2) where they are aggregated again, analyzed, and stored.</span></span> <span data-ttu-id="90e8d-141">每隔幾秒，服務會查看 hello 變更，並判斷是否需要任何動作 (3)。</span><span class="sxs-lookup"><span data-stu-id="90e8d-141">Every few seconds that service looks at hello changes and determines if any actions are necessary (3).</span></span> <span data-ttu-id="90e8d-142">比方說，它無法發現一些空白節點，已加入 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="90e8d-142">For example, it could notice that some empty nodes have been added toohello cluster.</span></span> <span data-ttu-id="90e8d-143">如此一來，它決定 toomove 某些服務 toothose 節點。</span><span class="sxs-lookup"><span data-stu-id="90e8d-143">As a result, it decides toomove some services toothose nodes.</span></span> <span data-ttu-id="90e8d-144">hello 叢集資源管理員無法同時也請注意，特定的節點已多載，或特定服務已失敗或已刪除，釋放資源的其他位置。</span><span class="sxs-lookup"><span data-stu-id="90e8d-144">hello Cluster Resource Manager could also notice that a particular node is overloaded, or that certain services have failed or been deleted, freeing up resources elsewhere.</span></span>

<span data-ttu-id="90e8d-145">讓我們看看下列圖表中的 hello，請參閱接下來的情況。</span><span class="sxs-lookup"><span data-stu-id="90e8d-145">Let’s look at hello following diagram and see what happens next.</span></span> <span data-ttu-id="90e8d-146">讓我們假設該 hello 叢集資源管理員決定不需要變更。</span><span class="sxs-lookup"><span data-stu-id="90e8d-146">Let’s say that hello Cluster Resource Manager determines that changes are necessary.</span></span> <span data-ttu-id="90e8d-147">它會協調與其他系統服務 （在特定 hello 容錯移轉管理員) toomake hello 必要的變更。</span><span class="sxs-lookup"><span data-stu-id="90e8d-147">It coordinates with other system services (in particular hello Failover Manager) toomake hello necessary changes.</span></span> <span data-ttu-id="90e8d-148">然後會傳送 hello 必要命令 toohello 適當的節點 (4)。</span><span class="sxs-lookup"><span data-stu-id="90e8d-148">Then hello necessary commands are sent toohello appropriate nodes (4).</span></span> <span data-ttu-id="90e8d-149">例如，假設的 hello Node5 已多載，並因此決定 Node5 tooNode4 toomove 服務 B，注意到資源管理員。</span><span class="sxs-lookup"><span data-stu-id="90e8d-149">For example, let's say hello Resource Manager noticed that Node5 was overloaded, and so decided toomove service B from Node5 tooNode4.</span></span> <span data-ttu-id="90e8d-150">在 hello hello 重新設定 (5) 結尾，hello 叢集看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="90e8d-150">At hello end of hello reconfiguration (5), hello cluster looks like this:</span></span>

<span data-ttu-id="90e8d-151"><center>
![資源平衡器架構][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="90e8d-151"><center>
![Resource Balancer Architecture][Image2]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="90e8d-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90e8d-152">Next steps</span></span>
- <span data-ttu-id="90e8d-153">hello 叢集資源管理員有許多選擇可用來描述 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="90e8d-153">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="90e8d-154">toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](./service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="90e8d-154">toofind out more about them, check out this article on [describing a Service Fabric cluster](./service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="90e8d-155">重新平衡 hello 叢集 hello 叢集資源管理員的主要責任，強制執行放置規則。</span><span class="sxs-lookup"><span data-stu-id="90e8d-155">hello Cluster Resource Manager's primary duties are rebalancing hello cluster and enforcing placement rules.</span></span> <span data-ttu-id="90e8d-156">如需有關設定這些行為的詳細資訊，請參閱[平衡 Service Fabric 叢集](./service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="90e8d-156">For more information on configuring these behaviors, see [balancing your Service Fabric cluster](./service-fabric-cluster-resource-manager-balancing.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png