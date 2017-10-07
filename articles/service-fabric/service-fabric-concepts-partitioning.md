---
title: "aaaPartitioning Service Fabric 服務 |Microsoft 文件"
description: "描述如何 toopartition Service Fabric 可設定狀態服務。 資料分割可讓 hello 本機電腦上的資料存放區，因此可以一起調整資料和計算。"
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
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="8ebc2-104">分割 Service Fabric 可靠服務</span><span class="sxs-lookup"><span data-stu-id="8ebc2-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="8ebc2-105">本文章提供簡介 toohello Azure Service Fabric 可靠的服務資料分割基本的概念。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="8ebc2-106">hello hello 發行項中使用的原始碼也會提供在[GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="8ebc2-107">分割</span><span class="sxs-lookup"><span data-stu-id="8ebc2-107">Partitioning</span></span>
<span data-ttu-id="8ebc2-108">資料分割不是唯一 tooService 網狀架構。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="8ebc2-109">事實上，它是建置可調整服務的核心模式。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="8ebc2-110">更廣泛的意義而言，我們可以將資料分割除以狀態 （資料） 的概念來計算成較小的可存取的單位 tooimprove 延展性和效能。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="8ebc2-111">[資料分割][wikipartition]是一種知名的分割形式，也稱為分區化。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="8ebc2-112">分割 Service Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="8ebc2-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="8ebc2-113">對於無狀態服務，您可以將資料分割視為邏輯單元，其中包含服務的一個或多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="8ebc2-114">圖 1 顯示無狀態服務有 5 個執行個體分散到使用一個資料分割的叢集。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![無狀態服務](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="8ebc2-116">實際上有兩種無狀態服務解決方案。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="8ebc2-117">hello 第一次是一項服務，例如將外部而言，其狀態保存在 Azure SQL database （例如網站儲存 hello 工作階段資訊和資料）。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="8ebc2-118">hello 第二個是僅限計算服務 （例如計算機或影像縮圖） 不會管理任何持續性的狀態。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="8ebc2-119">在任一情況下，分割無狀態服務是很少見的情況，通常是藉由新增更多執行個體來達成延展性和可用性。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="8ebc2-120">hello 時，才想的 tooconsider 無狀態的服務執行個體的多個資料分割是當您需要 toomeet 特殊路由要求。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="8ebc2-121">例如，試想有一個情況，其中識別碼在某個範圍內的使用者應只由特定的服務執行個體來服務。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="8ebc2-122">當您可以分割為無狀態服務的另一個範例時，具有真正的分割區的後端 (例如分區化 SQL database)，而且您想的 toocontrol 哪個服務執行個體應該寫入 toohello 資料庫分區-，或執行其他準備工作hello 無狀態服務，會要求 hello 相同 hello 後端中使用時，分割區資訊。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="8ebc2-123">這幾種情況也可以透過不同方式解決，不一定需要服務分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="8ebc2-124">本逐步解說的 hello 其餘部分著重於可設定狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="8ebc2-125">分割 Service Fabric 具狀態服務</span><span class="sxs-lookup"><span data-stu-id="8ebc2-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="8ebc2-126">Service Fabric 就可以輕鬆 toodevelop 可延展的可設定狀態服務供應項目第一級方式 toopartition 狀態 （資料）。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="8ebc2-127">在概念上，您可以將有關資料分割的可設定狀態服務視為延展單位，是透過可靠[複本](service-fabric-availability-services.md)，散發並 hello 叢集中的節點之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="8ebc2-128">Service Fabric 可設定狀態服務 hello 內容中的資料分割是指 toohello 程序可決定特定服務資料分割負責 hello hello 服務完成狀態的一部分。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="8ebc2-129">(如前所述，資料分割是一組[複本](service-fabric-availability-services.md))。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="8ebc2-130">Service Fabric 最棒的一點是它會 hello 資料分割放在不同節點上。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="8ebc2-131">這可讓它們 toogrow tooa 節點的資源限制。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="8ebc2-132">Hello 資料需要成長，成長的資料分割，以及 Service Fabric 節點之間會重新平衡資料分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="8ebc2-133">這可確保 hello 繼續有效率地使用硬體資源。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="8ebc2-134">您需範例，您說 toogive 5 個節點叢集，而是已設定的 toohave 10 資料分割和三個複本的目標服務的啟動。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="8ebc2-135">在此情況下，Service Fabric 會平衡 hello 複本分散 hello 叢集和您最後會出現兩個主要[複本](service-fabric-availability-services.md)每個節點。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="8ebc2-136">如果您現在需要 tooscale hello 叢集 too10 節點時，Service Fabric 會重新平衡 hello 主要[複本](service-fabric-availability-services.md)10 的所有節點。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="8ebc2-137">同樣地，如果您調整反向 too5 節點時，Service Fabric 會重新平衡所有 hello 複本 hello 5 節點之間。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="8ebc2-138">圖 2 顯示 hello 發佈的 10 個資料分割之前和之後調整 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![具狀態服務](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="8ebc2-140">如此一來，向外延展 hello 是因為來自用戶端要求會分散在電腦、 hello 應用程式的整體效能已獲得改善，而且會減少競爭資料的存取 toochunks 來達成。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="8ebc2-141">規劃分割</span><span class="sxs-lookup"><span data-stu-id="8ebc2-141">Plan for partitioning</span></span>
<span data-ttu-id="8ebc2-142">之前實作的服務，您應該永遠考慮資料分割策略，是需要的 tooscale 出 hello。有不同的方式，但全部都著重於哪些 hello 應用程式需要 tooachieve。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="8ebc2-143">Hello 這篇文章的內容，讓我們考慮某些 hello 更重要的層面。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="8ebc2-144">一個好方法是 toothink hello 結構，需要進行資料分割，第一個步驟中 hello toobe hello 狀態的相關。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="8ebc2-145">我們來看一個簡單的範例。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-145">Let's take a simple example.</span></span> <span data-ttu-id="8ebc2-146">如果您 toobuild countywide 輪詢的服務，您可以建立 hello 郡中的每個城市的資料分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="8ebc2-147">然後，您可以儲存的每個人的 hello 投票中對應 toothat 縣 （市） 的 hello 資料分割中的 hello 縣 （市）。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="8ebc2-148">圖 3 說明一組的人員和 hello 所在的城市。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![簡單資料分割](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="8ebc2-150">因為 hello 母體擴展的城市變化很大，最後可能包含大量資料 （例如西雅圖） 的某些資料分割與極少的狀態 (例如 Kirkland) 與其他資料分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="8ebc2-151">那麼 hello 影響的分割區不平均金額是狀態的什麼？</span><span class="sxs-lookup"><span data-stu-id="8ebc2-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="8ebc2-152">如果您認為 hello 範例需一次，可以輕鬆地查看保存 hello 投票數以供西雅圖的 hello 分割區會比其中一個 hello Kirkland 更多流量。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="8ebc2-153">根據預設，Service Fabric 可確保沒有 hello 關於相同數目的每個節點上的主要和次要複本。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="8ebc2-154">所以您最後可能是保存複本的一些節點處理有較多流量，而另外一些節點有較少流量。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="8ebc2-155">您最好是想讓 tooavoid 熱，冷點以這種方式在叢集中。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="8ebc2-156">在順序 tooavoid，您應該執行兩件事，從資料分割的觀點：</span><span class="sxs-lookup"><span data-stu-id="8ebc2-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="8ebc2-157">如此會平均分散到所有的資料分割，再試一次 toopartition hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="8ebc2-158">報告負載從每個 hello 服務的 hello 複本。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="8ebc2-159">(如需有關如何進行的資訊，請參閱[度量和負載](service-fabric-cluster-resource-manager-metrics.md)上的這篇文章)。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="8ebc2-160">Service Fabric 提供服務，例如記憶體數量或記錄數目所耗用的 hello 功能 tooreport 負載。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="8ebc2-161">根據報告的 hello 度量，Service Fabric 會偵測到某些資料分割正在提供更高的負載，比其他 hello 移動複本 toomore 適合節點，叢集會重新平衡，讓整體沒有節點多載。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="8ebc2-162">有時候您不知道給定的資料分割中有多少資料。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="8ebc2-163">一般建議是 toodo 這兩個-首先，採用資料分割策略，會將分散 hello 資料平均到 hello 資料分割和第二個，所報告的負載。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="8ebc2-164">hello 第一種方法可避免述 hello 投票範例中，雖然 hello 第二個可協助存取或載入中暫存的差異變平滑經過一段時間的情況。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="8ebc2-165">規劃磁碟分割的另一個層面是 toochoose hello 正確數目的資料分割 toobegin 與。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="8ebc2-166">從 Service Fabric 的觀點來看，並不阻止您一開始就使用高於案例預期的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="8ebc2-167">事實上，假設 hello 資料分割數目上限是有效的方法。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="8ebc2-168">在少數情況下，最後需要的磁碟分割可能比一開始選擇的數目更多。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="8ebc2-169">當您無法變更 hello 資料分割計數 hello 事實之後，您將需要 tooapply 一些進階的資料分割方法，例如建立新的服務執行個體的 hello 相同服務類型。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="8ebc2-170">您也需要的 tooimplement 路由傳送嗨某些用戶端邏輯要求 toohello 正確的服務執行個體，根據您的用戶端程式碼必須維護的用戶端知識。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="8ebc2-171">規劃資料分割的另一個考量是 hello 可用的電腦資源。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="8ebc2-172">為需要存取和儲存 toobe hello 狀態，您會繫結的 toofollow:</span><span class="sxs-lookup"><span data-stu-id="8ebc2-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="8ebc2-173">網路頻寬限制</span><span class="sxs-lookup"><span data-stu-id="8ebc2-173">Network bandwidth limits</span></span>
* <span data-ttu-id="8ebc2-174">系統記憶體限制</span><span class="sxs-lookup"><span data-stu-id="8ebc2-174">System memory limits</span></span>
* <span data-ttu-id="8ebc2-175">磁碟儲存體限制</span><span class="sxs-lookup"><span data-stu-id="8ebc2-175">Disk storage limits</span></span>

<span data-ttu-id="8ebc2-176">因此怎樣若在執行中執行的叢集資源條件約束？hello 辦法就是，您可以直接向外延展 hello 叢集 tooaccommodate hello 新需求。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="8ebc2-177">[hello 容量規劃指南](service-fabric-capacity-planning.md)提供的指導 toodetermine 您的叢集需要多少的節點。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="8ebc2-178">開始進行分割</span><span class="sxs-lookup"><span data-stu-id="8ebc2-178">Get started with partitioning</span></span>
<span data-ttu-id="8ebc2-179">本章節描述 tooget 中的資料分割您的服務的啟動方式。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="8ebc2-180">Service Fabric 有三個資料分割配置可選擇：</span><span class="sxs-lookup"><span data-stu-id="8ebc2-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="8ebc2-181">範圍分割 (亦稱為 UniformInt64Partition)。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="8ebc2-182">具名分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-182">Named partitioning.</span></span> <span data-ttu-id="8ebc2-183">採用此模型的應用程式通常是在有界限集合內有可分割為值區的資料。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="8ebc2-184">一些常見做為具名資料分割索引鍵的資料欄位範例包括區域、郵遞區號、客戶群組或其他商務界限。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="8ebc2-185">單一分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-185">Singleton partitioning.</span></span> <span data-ttu-id="8ebc2-186">單一資料分割通常用在 hello 服務不需要任何額外的路由。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="8ebc2-187">例如，無狀態服務依預設使用此分割配置。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="8ebc2-188">具名和單一分割配置是特殊形式的範圍資料分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="8ebc2-189">根據預設，hello Visual Studio 範本，用於 Service Fabric 遠距資料分割，因為它是 hello 最常用與實用的一個。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="8ebc2-190">hello 本文其餘部分著重於 hello 遠距的資料分割配置。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="8ebc2-191">範圍分割配置</span><span class="sxs-lookup"><span data-stu-id="8ebc2-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="8ebc2-192">這是使用的 toospecify 整數 （由低索引鍵，高索引鍵識別） 的範圍與資料分割 (n) 數目。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="8ebc2-193">它會建立 n 個資料分割，分別負責非重疊子範圍的 hello 整體資料分割索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="8ebc2-194">範例：具有低索引鍵 0、高索引鍵 99 及計數 4 的範圍分割配置，將會建立 4 個資料分割，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![定界分割](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="8ebc2-196">常見的方法是 toocreate hello 資料集內的唯一索引鍵為基礎的雜湊。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="8ebc2-197">索引鍵的某些常見範例可能是汽車識別號碼 (VIN)、員工識別碼或唯一字串。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="8ebc2-198">藉由使用這個唯一索引鍵，您接著便會做為您的索引鍵產生雜湊程式碼、 模數 hello 索引鍵範圍、 toouse。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="8ebc2-199">您可以指定 hello 上限和下限 hello 允許索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="8ebc2-200">選取雜湊演算法</span><span class="sxs-lookup"><span data-stu-id="8ebc2-200">Select a hash algorithm</span></span>
<span data-ttu-id="8ebc2-201">雜湊中的重要部分即為選取雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="8ebc2-202">考量是 hello 目標是否 toogroup （區域性機密雜湊）-彼此的附近的類似金鑰，或如果活動應該廣為散發的所有資料分割 （發佈雜湊），這是較常見。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="8ebc2-203">hello 特性較佳分佈雜湊演算法是很容易 toocompute、 它有幾個衝突，和其平均發佈 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="8ebc2-204">有效率的雜湊演算法的理想範例為 hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function)雜湊演算法。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="8ebc2-205">如需一般的雜湊程式碼演算法的選擇是絕佳的資源為 hello[雜湊函式上的維基百科頁面](http://en.wikipedia.org/wiki/Hash_function)。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="8ebc2-206">建置具有多個資料分割的具狀態服務</span><span class="sxs-lookup"><span data-stu-id="8ebc2-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="8ebc2-207">讓我們使用多個資料分割建立第一個可靠的具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="8ebc2-208">在此範例中，您將建立非常簡單的應用程式，您想要 toostore 所有開頭之姓氏以字母 hello 中的相同的 hello 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="8ebc2-209">撰寫任何程式碼之前，您會需要 toothink 需 hello 資料分割和資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="8ebc2-210">您需要什麼但 26 （一個 hello 字母中的每個字母），資料分割相關 hello 低和高索引鍵嗎？</span><span class="sxs-lookup"><span data-stu-id="8ebc2-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="8ebc2-211">字面意義，我們想要 toohave 字母每一個資料分割，我們可以使用 0 作為 hello 低索引鍵和 25 hello 高索引鍵，因為每個字母是它自己的金鑰。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="8ebc2-212">這是一個簡化的實例，因為事實上 hello 散發會以不平均。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="8ebc2-213">最後一個名稱開頭為"S"或"M"會比 hello 的開頭為"X"更為常見 hello 字母或"Y"。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="8ebc2-214">開啟 [Visual Studio] > [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="8ebc2-215">在 hello**新專案**對話方塊方塊中，選擇 hello Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="8ebc2-216">呼叫 hello 專案 」 AlphabetPartitions"。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="8ebc2-217">在 hello**建立服務**對話方塊方塊中，選擇**可設定狀態**服務並呼叫 「 Alphabet.Processing"hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="8ebc2-218">![Visual Studio 中的新增服務對話方塊][1]</span><span class="sxs-lookup"><span data-stu-id="8ebc2-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="8ebc2-219">設定資料分割的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-219">Set hello number of partitions.</span></span> <span data-ttu-id="8ebc2-220">開啟 hello Applicationmanifest.xml 檔案位於 hello ApplicationPackageRoot 資料夾 hello AlphabetPartitions 專案和更新 hello 參數 Processing_PartitionCount too26 如下所示。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="8ebc2-221">您也需要 tooupdate hello LowKey 與 HighKey 項目的屬性 hello StatefulService 在 hello ApplicationManifest.xml 如下所示。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="8ebc2-222">Hello 服務 toobe 存取，如開啟連接埠端點加入 hello 端點項目 （位於 hello 目錄資料夾） 的 ServiceManifest.xml 的 hello Alphabet.Processing 服務，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8ebc2-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="8ebc2-223">現在 hello 服務是設定的 toolisten tooan 內部端點具有 26 資料分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="8ebc2-224">接下來，您必須 toooverride hello `CreateServiceReplicaListeners()` hello 處理類別的方法。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8ebc2-225">在這個範例中，我們假設您使用簡單的 HttpCommunicationListener。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="8ebc2-226">如需可靠的服務通訊的詳細資訊，請參閱[hello 可靠的服務通訊模型](service-fabric-reliable-services-communication.md)。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="8ebc2-227">複本在上接聽的 hello url 建議的模式為下列格式的 hello: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="8ebc2-228">因此您需要 tooconfigure 您通訊接聽程式 toolisten 在 hello 正確端點，並使用此模式。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="8ebc2-229">此服務的多個複本可能會裝載於 hello 同一部電腦，因此此位址必須 toobe 唯一 toohello 複本。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="8ebc2-230">這是為什麼分割區識別碼 + 複本識別碼是 hello URL 中。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="8ebc2-231">HttpListener 可以接聽相同通訊埠，只要 hello URL 前置詞是唯一的 hello 的多個地址。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="8ebc2-232">hello 進階案例，其中的次要複本也接聽的唯讀要求有額外的 GUID。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="8ebc2-233">Hello 案例時，您會想 toomake 確定當轉換從主要 toosecondary tooforce 用戶端 toore 解析 hello 位址時，會使用新的唯一位址。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="8ebc2-234">'+' hello 地址，以便 hello 複本在上接聽所有 IP、 FQDM、 localhost （等） 可用的主機 hello 下列程式碼範例示範當做。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
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
   
    <span data-ttu-id="8ebc2-235">另外值得注意的是該 hello 發行 URL 會稍有不同 hello 接聽的 URL 首碼。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="8ebc2-236">hello 接聽的 URL 會指定 tooHttpListener。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="8ebc2-237">已發行的 URL 是 hello URL 是已發行的 toohello Service Fabric 命名服務，可用於服務探索，hello。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="8ebc2-238">用戶端會透過該探索服務來要求這個位址。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="8ebc2-239">用戶端取得需求 toohave hello 實際 IP 或 FQDN hello 節點的順序 tooconnect hello 位址。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="8ebc2-240">因此您需要 tooreplace '+' 與 hello 節點的 IP 或 FQDN，示上述。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="8ebc2-241">hello 最後一個步驟是 tooadd hello 處理邏輯 toohello 服務，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
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
   
    <span data-ttu-id="8ebc2-242">`ProcessInternalRequest`讀取 hello hello 查詢字串參數使用 toocall hello 磁碟分割和呼叫值`AddUserAsync`tooadd hello lastname toohello 可靠字典`dictionary`。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="8ebc2-243">讓我們加入無狀態服務 toohello 專案 toosee 呼叫特定資料分割的方式。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="8ebc2-244">此服務可做為簡單的 web 介面，可接受 hello lastname 做為查詢字串參數，決定 hello 資料分割索引鍵，並將它傳送 toohello Alphabet.Processing 服務進行處理。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="8ebc2-245">在 hello**建立服務**對話方塊方塊中，選擇  **Stateless**服務並呼叫 「 Alphabet.Web"如下所示。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![無狀態服務螢幕擷取畫面](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="8ebc2-247">.</span><span class="sxs-lookup"><span data-stu-id="8ebc2-247">.</span></span>
12. <span data-ttu-id="8ebc2-248">更新 hello ServiceManifest.xml 中的 hello Alphabet.WebApi 服務 tooopen 埠，如下所示的 hello 端點資訊。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="8ebc2-249">您需要 tooreturn hello 類別 Web 中 ServiceInstanceListeners 的集合。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="8ebc2-250">同樣地，您可以選擇 tooimplement 簡單 HttpCommunicationListener。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="8ebc2-251">現在您需要 tooimplement hello 處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="8ebc2-252">hello HttpCommunicationListener 呼叫`ProcessInputRequest`當要求進入。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="8ebc2-253">因此讓我們繼續並加入下列程式碼 hello。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-253">So let's go ahead and add hello code below.</span></span>
    
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
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
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
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="8ebc2-254">讓我們帶您逐步了解。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-254">Let's walk through it step by step.</span></span> <span data-ttu-id="8ebc2-255">hello 程式碼會讀取 hello hello 查詢字串參數的第一個字母`lastname`成 char。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="8ebc2-256">然後，它會判斷此代號 hello 資料分割索引鍵中減去 hello 十六進位值`A`hello 十六進位值中的 hello 姓氏的第一個字母。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="8ebc2-257">請記得，在此範例中，我們使用 26 個資料分割，每個資料分割有一個資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="8ebc2-258">接下來，我們會取得 hello 服務資料分割`partition`此索引鍵使用 hello`ResolveAsync`方法上 hello`servicePartitionResolver`物件。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="8ebc2-259">`servicePartitionResolver` 定義為</span><span class="sxs-lookup"><span data-stu-id="8ebc2-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="8ebc2-260">hello`ResolveAsync`方法會採用 hello 服務 URI、 hello 資料分割索引鍵，以及取消語彙基元做為參數。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="8ebc2-261">為處理服務的 hello hello 服務 URI `fabric:/AlphabetPartitions/Processing`。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="8ebc2-262">接下來，我們取得 hello 資料分割的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="8ebc2-263">最後，我們會建置 hello 端點 URL 加上 hello querystring，並呼叫 hello 處理服務。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="8ebc2-264">一旦 hello 處理完成時，我們 hello 輸出回寫。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="8ebc2-265">hello 最後一個步驟是 tootest hello 服務。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="8ebc2-266">Visual Studio 會在本機和雲端部署中使用應用程式參數。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="8ebc2-267">tootest hello 26 本機分割區的服務，您需要 tooupdate hello `Local.xml` hello ApplicationParameters hello AlphabetPartitions 專案資料夾中檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8ebc2-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="8ebc2-268">完成部署之後，您可以檢查 hello 服務和所有其 hello Service Fabric 總管中的資料分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Service Fabric 總管螢幕擷取畫面](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="8ebc2-270">在瀏覽器中，您可以測試邏輯分割輸入 hello `http://localhost:8081/?lastname=somename`。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="8ebc2-271">您會看到，各個姓氏開頭的 hello 相同的字母儲存在 hello 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![瀏覽器螢幕擷取畫面](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="8ebc2-273">hello 範例 hello 整個原始程式碼位於[GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)。</span><span class="sxs-lookup"><span data-stu-id="8ebc2-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ebc2-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ebc2-274">Next steps</span></span>
<span data-ttu-id="8ebc2-275">如需 Service Fabric 概念資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="8ebc2-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="8ebc2-276">Service Fabric 服務的可用性</span><span class="sxs-lookup"><span data-stu-id="8ebc2-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="8ebc2-277">Service Fabric 服務的延展性</span><span class="sxs-lookup"><span data-stu-id="8ebc2-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="8ebc2-278">Service Fabric 應用程式的容量規劃</span><span class="sxs-lookup"><span data-stu-id="8ebc2-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png