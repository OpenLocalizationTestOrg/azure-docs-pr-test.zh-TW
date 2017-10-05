---
title: "分割 Service Fabric 服務 | Microsoft Docs"
description: "描述如何分割 Service Fabric 具狀態服務。 資料分割可讓資料儲存在本機電腦上，因此可以一起調整資料和計算。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 3c1e80305cb65f41a6981b99f69e8b87f89599ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="8b4c4-104">分割 Service Fabric 可靠服務</span><span class="sxs-lookup"><span data-stu-id="8b4c4-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="8b4c4-105">這篇文章介紹分割 Azure Service Fabric 可靠服務的基本概念。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-105">This article provides an introduction to the basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="8b4c4-106">[GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)上也提供本文中使用的原始碼。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-106">The source code used in the article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="8b4c4-107">分割</span><span class="sxs-lookup"><span data-stu-id="8b4c4-107">Partitioning</span></span>
<span data-ttu-id="8b4c4-108">分割不是 Service Fabric 所獨有。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-108">Partitioning is not unique to Service Fabric.</span></span> <span data-ttu-id="8b4c4-109">事實上，它是建置可調整服務的核心模式。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="8b4c4-110">廣義上，我們可以將分割視為將狀態 (資料) 和計算分成較小的可存取單位來改善延展性和效能。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units to improve scalability and performance.</span></span> <span data-ttu-id="8b4c4-111">[資料分割][wikipartition]是一種知名的分割形式，也稱為分區化。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="8b4c4-112">分割 Service Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="8b4c4-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="8b4c4-113">對於無狀態服務，您可以將資料分割視為邏輯單元，其中包含服務的一個或多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="8b4c4-114">圖 1 顯示無狀態服務有 5 個執行個體分散到使用一個資料分割的叢集。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![無狀態服務](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="8b4c4-116">實際上有兩種無狀態服務解決方案。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="8b4c4-117">第一種是將狀態保存在外部的服務，例如 Azure SQL 資料庫 (例如儲存工作階段資訊和資料的網站)。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-117">The first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores the session information and data).</span></span> <span data-ttu-id="8b4c4-118">第二種是僅限計算的服務 (例如計算機或影像縮圖)，不管理任何持續性狀態。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-118">The second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="8b4c4-119">在任一情況下，分割無狀態服務是很少見的情況，通常是藉由新增更多執行個體來達成延展性和可用性。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="8b4c4-120">當您必須符合特殊的路由要求時，才會想要考慮對無狀態服務執行個體使用多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-120">The only time you want to consider multiple partitions for stateless service instances is when you need to meet special routing requests.</span></span>

<span data-ttu-id="8b4c4-121">例如，試想有一個情況，其中識別碼在某個範圍內的使用者應只由特定的服務執行個體來服務。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="8b4c4-122">另一個您會分割無狀態服務的例子是當您有真正分割的後端時 (例如分區化 SQL 資料庫)，而且您想要控制哪一個服務執行個體應該寫入資料庫分區，或在需要有後端中使用的相同分割資訊的無狀態服務內執行其他準備工作。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want to control which service instance should write to the database shard--or perform other preparation work within the stateless service that requires the same partitioning information as is used in the backend.</span></span> <span data-ttu-id="8b4c4-123">這幾種情況也可以透過不同方式解決，不一定需要服務分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="8b4c4-124">本逐步解說的其餘部分著重於具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-124">The remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="8b4c4-125">分割 Service Fabric 具狀態服務</span><span class="sxs-lookup"><span data-stu-id="8b4c4-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="8b4c4-126">Service Fabric 提供一流的方法來分割狀態 (資料)，讓您輕鬆開發可調整的具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-126">Service Fabric makes it easy to develop scalable stateful services by offering a first-class way to partition state (data).</span></span> <span data-ttu-id="8b4c4-127">在概念上，您可以將具狀態服務視為一種縮放單位，透過叢集中節點之間分散和平衡的 [複本](service-fabric-availability-services.md) ，此縮放單位非常可靠。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across the nodes in a cluster.</span></span>

<span data-ttu-id="8b4c4-128">在提及 Service Fabric 具狀態服務時，分割過程是指決定特定的服務資料分割負責服務完整狀態的一部分 </span><span class="sxs-lookup"><span data-stu-id="8b4c4-128">Partitioning in the context of Service Fabric stateful services refers to the process of determining that a particular service partition is responsible for a portion of the complete state of the service.</span></span> <span data-ttu-id="8b4c4-129">(如前所述，資料分割是一組[複本](service-fabric-availability-services.md))。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="8b4c4-130">Service Fabric 最棒的一點是將資料分割放在不同節點上。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-130">A great thing about Service Fabric is that it places the partitions on different nodes.</span></span> <span data-ttu-id="8b4c4-131">這可讓它們在節點的資源限制內成長。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-131">This allows them to grow to a node's resource limit.</span></span> <span data-ttu-id="8b4c4-132">資料需求成長時，資料分割也會成長，Service Fabric 會重新平衡節點之間的資料分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-132">As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="8b4c4-133">這可確保持續有效率地使用硬體資源。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-133">This ensures the continued efficient use of hardware resources.</span></span>

<span data-ttu-id="8b4c4-134">舉例來說，假設您一開始叢集有 5 個節點、服務設定為有 10 個資料分割，以及目標為三個複本。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-134">To give you an example, say you start with a 5-node cluster and a service that is configured to have 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="8b4c4-135">在此情況下，Service Fabric 會將複本平衡並分散到叢集，最後每個節點會有 2 個主要 [複本](service-fabric-availability-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-135">In this case, Service Fabric would balance and distribute the replicas across the cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="8b4c4-136">如果您現在需要將我們的叢集相應放大到 10 個節點，Service Fabric 會在所有 10 個節點之間重新平衡主要 [複本](service-fabric-availability-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-136">If you now need to scale out the cluster to 10 nodes, Service Fabric would rebalance the primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="8b4c4-137">同樣地，如果調降為 5 個節點，Service Fabric 會在 5 個節點之間重新平衡所有複本。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-137">Likewise, if you scaled back to 5 nodes, Service Fabric would rebalance all the replicas across the 5 nodes.</span></span>  

<span data-ttu-id="8b4c4-138">圖 2 顯示調整叢集之前和之後 10 個資料分割的分佈。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-138">Figure 2 shows the distribution of 10 partitions before and after scaling the cluster.</span></span>

![具狀態服務](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="8b4c4-140">如此一來，因為來自用戶端要求會分散到各電腦而達成相應放大，應用程式的整體效能獲得改善，也減少競爭存取資料區塊的情況。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-140">As a result, the scale-out is achieved since requests from clients are distributed across computers, overall performance of the application is improved, and contention on access to chunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="8b4c4-141">規劃分割</span><span class="sxs-lookup"><span data-stu-id="8b4c4-141">Plan for partitioning</span></span>
<span data-ttu-id="8b4c4-142">實作服務之前，一定要考慮相應放大所需的分割策略。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-142">Before implementing a service, you should always consider the partitioning strategy that is required to scale out.</span></span> <span data-ttu-id="8b4c4-143">方法不同，但全部都著重於應用程式必須達到的目的。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-143">There are different ways, but all of them focus on what the application needs to achieve.</span></span> <span data-ttu-id="8b4c4-144">在這篇文章中，讓我們看一些更重要的層面。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-144">For the context of this article, let's consider some of the more important aspects.</span></span>

<span data-ttu-id="8b4c4-145">第一步先思考必須分割的狀態結構是個不錯的方法。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-145">A good approach is to think about the structure of the state that needs to be partitioned, as the first step.</span></span>

<span data-ttu-id="8b4c4-146">我們來看一個簡單的範例。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-146">Let's take a simple example.</span></span> <span data-ttu-id="8b4c4-147">如果您要為一次全國性選舉建置服務，您可以為該國的每個城市建立資料分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-147">If you were to build a service for a countywide poll, you could create a partition for each city in the county.</span></span> <span data-ttu-id="8b4c4-148">然後，您可以將城市中每一個人的投票存放在對應到該城市的資料分割中。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-148">Then, you could store the votes for every person in the city in the partition that corresponds to that city.</span></span> <span data-ttu-id="8b4c4-149">圖 3 說明一組人及其居住城市。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-149">Figure 3 illustrates a set of people and the city in which they reside.</span></span>

![簡單資料分割](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="8b4c4-151">由於城市人口差異極大，最後可能是某些資料分割包含大量資料 (例如西雅圖)，而另外一些資料分割只有極少狀態 (例如柯克蘭)。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-151">As the population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="8b4c4-152">狀態數量不平均的資料分割有什麼影響？</span><span class="sxs-lookup"><span data-stu-id="8b4c4-152">So what is the impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="8b4c4-153">如果您回顧一下範例，就會明白保存西雅圖投票的資料分割會比柯克蘭資料分割的流量更多。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-153">If you think about the example again, you can easily see that the partition that holds the votes for Seattle will get more traffic than the Kirkland one.</span></span> <span data-ttu-id="8b4c4-154">根據預設，Service Fabric 會確保每個節點上的主要和次要複本數目大約相同。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-154">By default, Service Fabric makes sure that there is about the same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="8b4c4-155">所以您最後可能是保存複本的一些節點處理有較多流量，而另外一些節點有較少流量。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-155">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="8b4c4-156">您可能想要避免叢集中發生像這樣的冷熱不均。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-156">You would preferably want to avoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="8b4c4-157">若要避免這種情況，您應該從分割觀點來做兩件事：</span><span class="sxs-lookup"><span data-stu-id="8b4c4-157">In order to avoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="8b4c4-158">試著分割狀態，使它平均分散到所有資料分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-158">Try to partition the state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="8b4c4-159">報告此服務每個複本的負載</span><span class="sxs-lookup"><span data-stu-id="8b4c4-159">Report load from each of the replicas for the service.</span></span> <span data-ttu-id="8b4c4-160">(如需有關如何進行的資訊，請參閱[度量和負載](service-fabric-cluster-resource-manager-metrics.md)上的這篇文章)。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-160">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="8b4c4-161">Service Fabric 能夠報告服務取用的負載，例如記憶體數量或記錄數量。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-161">Service Fabric provides the capability to report load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="8b4c4-162">根據報告的計量，Service Fabric 會偵測到某些資料分割處理的負載高於其他資料分割，然後將複本移至更適合的節點，以重新平衡叢集，使整體沒有節點多載。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-162">Based on the metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances the cluster by moving replicas to more suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="8b4c4-163">有時候您不知道給定的資料分割中有多少資料。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-163">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="8b4c4-164">所以一般是建議兩者都做，首先是採用分割策略將資料平均分散到資料分割，其次是報告負載。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-164">So a general recommendation is to do both--first, by adopting a partitioning strategy that spreads the data evenly across the partitions and second, by reporting load.</span></span>  <span data-ttu-id="8b4c4-165">第一種方法可避免投票範例中的情況，第二種方法有助於消除一段期間內短暫的存取或負載差異。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-165">The first method prevents situations described in the voting example, while the second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="8b4c4-166">分割規劃的另一方面是一開始選擇正確的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-166">Another aspect of partition planning is to choose the correct number of partitions to begin with.</span></span>
<span data-ttu-id="8b4c4-167">從 Service Fabric 的觀點來看，並不阻止您一開始就使用高於案例預期的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-167">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="8b4c4-168">事實上，假設資料分割的最大數目是有效的方法。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-168">In fact, assuming the maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="8b4c4-169">在少數情況下，最後需要的磁碟分割可能比一開始選擇的數目更多。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-169">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="8b4c4-170">因為您不能在事後變更資料分割計數，您需要套用一些進階的分割方法，例如建立相同服務類型的新服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-170">As you cannot change the partition count after the fact, you would need to apply some advanced partition approaches, such as creating a new service instance of the same service type.</span></span> <span data-ttu-id="8b4c4-171">您也需要實作一些用戶端邏輯，根據用戶端程式碼必須維護的用戶端知識，將要求路由傳送至正確的服務執行個體</span><span class="sxs-lookup"><span data-stu-id="8b4c4-171">You would also need to implement some client-side logic that routes the requests to the correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="8b4c4-172">分割規劃的另一項考量是可用的電腦資源。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-172">Another consideration for partitioning planning is the available computer resources.</span></span> <span data-ttu-id="8b4c4-173">因為狀態需要存取與儲存，您會受下列限制約束：</span><span class="sxs-lookup"><span data-stu-id="8b4c4-173">As the state needs to be accessed and stored, you are bound to follow:</span></span>

* <span data-ttu-id="8b4c4-174">網路頻寬限制</span><span class="sxs-lookup"><span data-stu-id="8b4c4-174">Network bandwidth limits</span></span>
* <span data-ttu-id="8b4c4-175">系統記憶體限制</span><span class="sxs-lookup"><span data-stu-id="8b4c4-175">System memory limits</span></span>
* <span data-ttu-id="8b4c4-176">磁碟儲存體限制</span><span class="sxs-lookup"><span data-stu-id="8b4c4-176">Disk storage limits</span></span>

<span data-ttu-id="8b4c4-177">如果在執行中的叢集遇到資源限制，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="8b4c4-177">So what happens if you run into resource constraints in a running cluster?</span></span> <span data-ttu-id="8b4c4-178">答案是您可以輕易地調相應放大群集來滿足新的需求。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-178">The answer is that you can simply scale out the cluster to accommodate the new requirements.</span></span>

<span data-ttu-id="8b4c4-179">[容量規劃指南](service-fabric-capacity-planning.md) 提供如何判斷叢集需要多少節點的指導方針。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-179">[The capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how to determine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="8b4c4-180">開始進行分割</span><span class="sxs-lookup"><span data-stu-id="8b4c4-180">Get started with partitioning</span></span>
<span data-ttu-id="8b4c4-181">本節描述如何開始分割您的服務。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-181">This section describes how to get started with partitioning your service.</span></span>

<span data-ttu-id="8b4c4-182">Service Fabric 有三個資料分割配置可選擇：</span><span class="sxs-lookup"><span data-stu-id="8b4c4-182">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="8b4c4-183">範圍分割 (亦稱為 UniformInt64Partition)。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-183">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="8b4c4-184">具名分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-184">Named partitioning.</span></span> <span data-ttu-id="8b4c4-185">採用此模型的應用程式通常是在有界限集合內有可分割為值區的資料。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-185">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="8b4c4-186">一些常見做為具名資料分割索引鍵的資料欄位範例包括區域、郵遞區號、客戶群組或其他商務界限。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-186">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="8b4c4-187">單一分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-187">Singleton partitioning.</span></span> <span data-ttu-id="8b4c4-188">服務不需要任何額外的路由時，通常會使用單一資料分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-188">Singleton partitions are typically used when the service does not require any additional routing.</span></span> <span data-ttu-id="8b4c4-189">例如，無狀態服務依預設使用此分割配置。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-189">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="8b4c4-190">具名和單一分割配置是特殊形式的範圍資料分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-190">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="8b4c4-191">根據預設，Visual Studio 的 Service Fabric 範本使用範圍分割，因為這是最常見和最有用的配置。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-191">By default, the Visual Studio templates for Service Fabric use ranged partitioning, as it is the most common and useful one.</span></span> <span data-ttu-id="8b4c4-192">這篇文章的其餘部分著重於範圍分割配置。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-192">The remainder of this article focuses on the ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="8b4c4-193">範圍分割配置</span><span class="sxs-lookup"><span data-stu-id="8b4c4-193">Ranged partitioning scheme</span></span>
<span data-ttu-id="8b4c4-194">此功能用來指定整數範圍 (透過低索引鍵和高索引鍵來識別) 和資料分割數目 (n)。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-194">This is used to specify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="8b4c4-195">它會建立 n 個資料分割，各負責處理整體資料分割索引鍵範圍的一個非重疊子範圍。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-195">It creates n partitions, each responsible for a non-overlapping subrange of the overall partition key range.</span></span> <span data-ttu-id="8b4c4-196">範例：具有低索引鍵 0、高索引鍵 99 及計數 4 的範圍分割配置，將會建立 4 個資料分割，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-196">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![定界分割](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="8b4c4-198">常見的方法是根據資料集內的唯一索引鍵建立雜湊。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-198">A common approach is to create a hash based on a unique key within the data set.</span></span> <span data-ttu-id="8b4c4-199">索引鍵的某些常見範例可能是汽車識別號碼 (VIN)、員工識別碼或唯一字串。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-199">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="8b4c4-200">接著，您可以使用此唯一索引鍵產生雜湊程式碼，經過索引鍵範圍的模數運算，做為您的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-200">By using this unique key, you would then generate a hash code, modulus the key range, to use as your key.</span></span> <span data-ttu-id="8b4c4-201">您可以指定可允許索引鍵範圍的上限和下限。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-201">You can specify the upper and lower bounds of the allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="8b4c4-202">選取雜湊演算法</span><span class="sxs-lookup"><span data-stu-id="8b4c4-202">Select a hash algorithm</span></span>
<span data-ttu-id="8b4c4-203">雜湊中的重要部分即為選取雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-203">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="8b4c4-204">無論目標是分組彼此靠近的類似索引鍵 (位置敏感雜湊)，或應該將活動廣泛分散到所有資料分割 (分散雜湊)，需要考量何者較常用。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-204">A consideration is whether the goal is to group similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="8b4c4-205">良好分散雜湊演算法的特性包括容易計算、衝突小且平均分佈索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-205">The characteristics of a good distribution hashing algorithm are that it is easy to compute, it has few collisions, and it distributes the keys evenly.</span></span> <span data-ttu-id="8b4c4-206">[FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) 雜湊演算法是高效率雜湊演算法的一個很好例子。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-206">A good example of an efficient hash algorithm is the [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="8b4c4-207">一般選擇雜湊程式碼演算法的絕佳資源是 [雜湊函數的維基百科頁面](http://en.wikipedia.org/wiki/Hash_function)。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-207">A good resource for general hash code algorithm choices is the [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="8b4c4-208">建置具有多個資料分割的具狀態服務</span><span class="sxs-lookup"><span data-stu-id="8b4c4-208">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="8b4c4-209">讓我們使用多個資料分割建立第一個可靠的具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-209">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="8b4c4-210">在本例中，您將建立一個非常簡單的應用程式，其中，您想要將所有以相同字母開頭的姓氏儲存在相同的資料分割中。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-210">In this example, you will build a very simple application where you want to store all last names that start with the same letter in the same partition.</span></span>

<span data-ttu-id="8b4c4-211">撰寫任何程式碼之前，您必須考慮資料分割和資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-211">Before you write any code, you need to think about the partitions and partition keys.</span></span> <span data-ttu-id="8b4c4-212">您需要 26 個資料分割，每個字母英文各一個資料分割，但如何處理低和高索引鍵？</span><span class="sxs-lookup"><span data-stu-id="8b4c4-212">You need 26 partitions (one for each letter in the alphabet), but what about the low and high keys?</span></span>
<span data-ttu-id="8b4c4-213">因為我們真的想要每個字母有一個資料分割，我們可以把 0 當做低索引鍵，25 當做高索引鍵，因為每個字母就是它自己的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-213">As we literally want to have one partition per letter, we can use 0 as the low key and 25 as the high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="8b4c4-214">這是簡化的案例，因為現實上分佈會不平均。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-214">This is a simplified scenario, as in reality the distribution would be uneven.</span></span> <span data-ttu-id="8b4c4-215">"S" 或 "M" 字母開頭的姓氏比 "X" 或 "Y" 開頭的姓氏更常見。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-215">Last names starting with the letters "S" or "M" are more common than the ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="8b4c4-216">開啟 [Visual Studio] > [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-216">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="8b4c4-217">在 [新增專案]  對話方塊中，選擇 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="8b4c4-217">In the **New Project** dialog box, choose the Service Fabric application.</span></span>
3. <span data-ttu-id="8b4c4-218">將專案命名為 "AlphabetPartitions"。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-218">Call the project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="8b4c4-219">在 [建立服務] 對話方塊中，選擇 [具狀態] 服務，命名為 "Alphabet.Processing"，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-219">In the **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in the image below.</span></span>
       <span data-ttu-id="8b4c4-220">![Visual Studio 中的新增服務對話方塊][1]</span><span class="sxs-lookup"><span data-stu-id="8b4c4-220">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="8b4c4-221">設定資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-221">Set the number of partitions.</span></span> <span data-ttu-id="8b4c4-222">開啟位於 AlphabetPartitions 專案的 ApplicationPackageRoot 資料夾中的 ApplicationManifest.xml 檔案，將參數 Processing_PartitionCount 更新為 26，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-222">Open the Applicationmanifest.xml file located in the ApplicationPackageRoot folder of the AlphabetPartitions project and update the parameter Processing_PartitionCount to 26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="8b4c4-223">您也需要在 ApplicationManifest.xml 中更新 StatefulService 元素的 LowKey 和 HighKey 屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-223">You also need to update the LowKey and HighKey properties of the StatefulService element in the ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="8b4c4-224">為了能夠存取服務，請在 Alphabet.Processing 服務的 ServiceManifest.xml (位於 PackageRoot 資料夾) 中加入 endpoint 元素，以便在連接埠上開啟端點，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8b4c4-224">For the service to be accessible, open up an endpoint on a port by adding the endpoint element of ServiceManifest.xml (located in the PackageRoot folder) for the Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="8b4c4-225">現在，服務已設定為接聽有 26 個資料分割的內部端點。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-225">Now the service is configured to listen to an internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="8b4c4-226">接下來，您必須覆寫 Processing 類別的 `CreateServiceReplicaListeners()` 方法。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-226">Next, you need to override the `CreateServiceReplicaListeners()` method of the Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8b4c4-227">在這個範例中，我們假設您使用簡單的 HttpCommunicationListener。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-227">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="8b4c4-228">如需可靠服務通訊的詳細資訊，請參閱 [Reliable Service 通訊模型](service-fabric-reliable-services-communication.md)。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-228">For more information on reliable service communication, see [The Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="8b4c4-229">關於複本接聽的 URL，建議的模式是下列格式： `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-229">A recommended pattern for the URL that a replica listens on is the following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="8b4c4-230">所以您可以設定通訊接聽程式接聽正確的端點並使用此模式。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-230">So you want to configure your communication listener to listen on the correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="8b4c4-231">相同電腦上可能裝載此服務的多個複本，因此複本的此位址必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-231">Multiple replicas of this service may be hosted on the same computer, so this address needs to be unique to the replica.</span></span> <span data-ttu-id="8b4c4-232">這就是為什麼我們在 URL 中有資料分割識別碼 + 複本識別碼。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-232">This is why   partition ID + replica ID are in the URL.</span></span> <span data-ttu-id="8b4c4-233">只要 URL 首碼是唯一的，HttpListener 就可以在相同連接埠上的多個位址接聽。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-233">HttpListener can listen on multiple addresses on the same port as long as the URL prefix    is unique.</span></span>
   
    <span data-ttu-id="8b4c4-234">在進階案例中，次要複本也會接聽唯讀要求，所以有額外 GUID。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-234">The extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="8b4c4-235">在這種情況下，從主要轉換到次要時，您想要確保使用新的唯一位址以強制用戶端重新解析位址。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-235">When that's the case, you want to make sure that a new unique address is used when transitioning from primary to secondary to force clients to re-resolve the address.</span></span> <span data-ttu-id="8b4c4-236">'+' 在此做為位址，因此複本會接聽所有可用的主機 (IP、FQDM、localhost 等等)。下列程式碼顯示範例。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-236">'+' is used as the address here so that the replica listens on all available hosts (IP, FQDM, localhost, etc.) The code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="8b4c4-237">另外值得注意的是，發佈的 URL 稍微不同於接聽 URL 首碼。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-237">It's also worth noting that the published URL is slightly different from the listening URL prefix.</span></span>
    <span data-ttu-id="8b4c4-238">接聽 URL 提供給 HttpListener。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-238">The listening URL is given to HttpListener.</span></span> <span data-ttu-id="8b4c4-239">發佈的 URL 是發佈給 Service Fabric 命名服務 (用於服務探索) 的 URL。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-239">The published URL is the URL that is published to the Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="8b4c4-240">用戶端會透過該探索服務來要求這個位址。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-240">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="8b4c4-241">用戶端取得的位址必須有節點的實際 IP 或 FQDN 才能連接。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-241">The address that clients get needs to have the actual IP or FQDN of the node in order to connect.</span></span> <span data-ttu-id="8b4c4-242">所以您必須以節點的 IP 或 FQDN 取代 '+'，如上所示。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-242">So you need to replace '+' with the node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="8b4c4-243">最後一個步驟是將處理邏輯加入至服務，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-243">The last step is to add the processing logic to the service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="8b4c4-244">`ProcessInternalRequest` 讀取用來呼叫資料分割的查詢字串參數的值，並呼叫 `AddUserAsync` 將 lastname 加入可靠的字典 `dictionary`。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-244">`ProcessInternalRequest` reads the values of the query string parameter used to call the partition and calls `AddUserAsync` to add the lastname to the reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="8b4c4-245">讓我們將無狀態服務加入至專案，瞭解如何呼叫特定的資料分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-245">Let's add a stateless service to the project to see how you can call a particular partition.</span></span>
    
    <span data-ttu-id="8b4c4-246">這項服務做為簡單的 Web 介面，將接受 lastname 做為查詢字串參數、決定資料分割索引鍵，然後將它傳送給 Alphabet.Processing 服務來處理。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-246">This service serves as a simple web interface that accepts the lastname as a query string parameter, determines the partition key, and sends it to the Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="8b4c4-247">在 [建立服務] 對話方塊中，選擇 [無狀態] 服務，命名為 "Alphabet.Web"，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-247">In the **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![無狀態服務螢幕擷取畫面](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="8b4c4-249">上也提供本文中使用的原始碼。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-249">.</span></span>
12. <span data-ttu-id="8b4c4-250">更新 Alphabet.WebApi 服務的 ServiceManifest.xml 中的端點資訊，以開啟連接埠，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-250">Update the endpoint information in the ServiceManifest.xml of the Alphabet.WebApi service to open up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="8b4c4-251">您需要傳回 Web 類別中 ServiceInstanceListeners 的集合。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-251">You need to return a collection of ServiceInstanceListeners in the class Web.</span></span> <span data-ttu-id="8b4c4-252">同樣地，您可以選擇實作簡單的 HttpCommunicationListener。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-252">Again, you can choose to implement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is the node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="8b4c4-253">現在您需要實作處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-253">Now you need to implement the processing logic.</span></span> <span data-ttu-id="8b4c4-254">有要求傳入時，HttpCommunicationListener 會呼叫 `ProcessInputRequest` 。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-254">The HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="8b4c4-255">讓我們繼續並加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-255">So let's go ahead and add the code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from the first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added to Partition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="8b4c4-256">讓我們帶您逐步了解。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-256">Let's walk through it step by step.</span></span> <span data-ttu-id="8b4c4-257">程式碼將查詢字串參數 `lastname` 的第一個字母讀取為字元。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-257">The code reads the first letter of the query string parameter `lastname` into a char.</span></span> <span data-ttu-id="8b4c4-258">並從姓氏第一個字母的十六進位值中擷取 `A` 的十六進位值，判斷此字母的分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-258">Then, it determines the partition key for this letter by subtracting the hexadecimal value of `A` from the hexadecimal value of the last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="8b4c4-259">請記得，在此範例中，我們使用 26 個資料分割，每個資料分割有一個資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-259">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="8b4c4-260">接下來，我們使用 `servicePartitionResolver` 物件的 `ResolveAsync` 方法，取得此索引鍵的服務資料分割 `partition`。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-260">Next, we obtain the service partition `partition` for this key by using the `ResolveAsync` method on the `servicePartitionResolver` object.</span></span> <span data-ttu-id="8b4c4-261">`servicePartitionResolver` 定義為</span><span class="sxs-lookup"><span data-stu-id="8b4c4-261">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="8b4c4-262">`ResolveAsync` 方法接受服務 URI、資料分割索引鍵和取消語 Token 做為參數。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-262">The `ResolveAsync` method takes the service URI, the partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="8b4c4-263">處理服務的服務 URI 是 `fabric:/AlphabetPartitions/Processing`。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-263">The service URI for the processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="8b4c4-264">接下來，我們會取得資料分割的端點。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-264">Next, we get the endpoint of the partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="8b4c4-265">最後，我們建置端點 URL 加上查詢字串，並呼叫處理服務。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-265">Finally, we build the endpoint URL plus the querystring and call the processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="8b4c4-266">處理完成後，我們就寫回輸出。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-266">Once the processing is done, we write the output back.</span></span>
15. <span data-ttu-id="8b4c4-267">最後一個步驟是測試服務。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-267">The last step is to test the service.</span></span> <span data-ttu-id="8b4c4-268">Visual Studio 會在本機和雲端部署中使用應用程式參數。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-268">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="8b4c4-269">若要在本機測試有 26 個資料分割的服務，您需要更新 AlphabetPartitions 專案的 ApplicationParameters 資料夾中的 `Local.xml` 檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8b4c4-269">To test the service with 26 partitions locally, you need to update the `Local.xml` file in the ApplicationParameters folder of the AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="8b4c4-270">完成部署之後，您可以在 Service Fabric 總管中檢查服務及其所有資料分割。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-270">Once you finish deployment, you can check the service and all of its partitions in the Service Fabric Explorer.</span></span>
    
    ![Service Fabric 總管螢幕擷取畫面](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="8b4c4-272">您可以在瀏覽器中輸入 `http://localhost:8081/?lastname=somename`來測試分割邏輯。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-272">In a browser, you can test the partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="8b4c4-273">您會看到以相同字母開頭的每個姓氏儲存在相同的資料分割中。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-273">You will see that each last name that starts with the same letter is being stored in the same partition.</span></span>
    
    ![瀏覽器螢幕擷取畫面](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="8b4c4-275">範例的完整原始程式碼位於 [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)。</span><span class="sxs-lookup"><span data-stu-id="8b4c4-275">The entire source code of the sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b4c4-276">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b4c4-276">Next steps</span></span>
<span data-ttu-id="8b4c4-277">如需 Service Fabric 概念的資訊，請參閱下列項目：</span><span class="sxs-lookup"><span data-stu-id="8b4c4-277">For information on Service Fabric concepts, see the following:</span></span>

* [<span data-ttu-id="8b4c4-278">Service Fabric 服務的可用性</span><span class="sxs-lookup"><span data-stu-id="8b4c4-278">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="8b4c4-279">Service Fabric 服務的延展性</span><span class="sxs-lookup"><span data-stu-id="8b4c4-279">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="8b4c4-280">Service Fabric 應用程式的容量規劃</span><span class="sxs-lookup"><span data-stu-id="8b4c4-280">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png