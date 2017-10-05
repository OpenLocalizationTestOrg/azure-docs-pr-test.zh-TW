---
title: "如何檢視 Azure Service Fabric 實體的彙總健康情況 | Microsoft Docs"
description: "說明如何透過健康情況查詢和一般查詢，來查詢、檢視和評估 Azure Service Fabric 實體的彙總健康情況。"
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: b97972b1bdc28a17fb9c3a0e997738f5bd0b5d15
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="e7d65-103">檢視 Service Fabric 健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="e7d65-103">View Service Fabric health reports</span></span>
<span data-ttu-id="e7d65-104">Azure Service Fabric 導入了由健康情況實體組成的[健康情況模型](service-fabric-health-introduction.md)，系統元件和看門狗可以在其上回報所監視的本機情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="e7d65-105">[健康情況存放區](service-fabric-health-introduction.md#health-store) 會彙總所有健康情況資料，以判斷實體是否狀況良好。</span><span class="sxs-lookup"><span data-stu-id="e7d65-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="e7d65-106">叢集會自動填入系統元件所傳送的健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="e7d65-106">The cluster is automatically populated with health reports sent by the system components.</span></span> <span data-ttu-id="e7d65-107">請參閱 [使用系統健康狀態報告進行疑難排解](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="e7d65-108">Service Fabric 會提供多種方式，以取得實體的彙總健康情況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="e7d65-109">[Service Fabric 總管](service-fabric-visualizing-your-cluster.md) 或其他視覺效果工具</span><span class="sxs-lookup"><span data-stu-id="e7d65-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="e7d65-110">健康情況查詢 (透過 PowerShell、API 或 REST)</span><span class="sxs-lookup"><span data-stu-id="e7d65-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="e7d65-111">一般查詢會傳回一份實體清單，這些實體的其中一個屬性即為健康情況 (透過 PowerShell、API 或 REST)</span><span class="sxs-lookup"><span data-stu-id="e7d65-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="e7d65-112">為了示範這些選項，我們會使用具有五個節點和 [fabric:/WordCount 應用程式](http://aka.ms/servicefabric-wordcountapp) 的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="e7d65-113">**fabric:/WordCount** 應用程式包含兩項預設服務︰`WordCountServiceType` 類型的具狀態服務，以及 `WordCountWebServiceType` 類型的無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="e7d65-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="e7d65-114">我變更了 `ApplicationManifest.xml`，以要求具狀態服務的七個目標複本和一個磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="e7d65-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span></span> <span data-ttu-id="e7d65-115">因為叢集中只有五個節點，所以系統元件會回報服務磁碟分割的警告，因為它低於目標計數。</span><span class="sxs-lookup"><span data-stu-id="e7d65-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="e7d65-116">Service Fabric 總管中的健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="e7d65-117">Service Fabric 總管提供叢集的視覺化檢視。</span><span class="sxs-lookup"><span data-stu-id="e7d65-117">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="e7d65-118">在下圖中，您可以看到：</span><span class="sxs-lookup"><span data-stu-id="e7d65-118">In the image below, you can see that:</span></span>

* <span data-ttu-id="e7d65-119">應用程式 **fabric:/WordCount** 是紅色 (錯誤)，因為它具有 **MyWatchdog** 針對屬性 **Availability** 所回報的錯誤事件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="e7d65-120">應用程式的其中一個服務 **fabric:/WordCount/WordCountService** 是黃色 (警告)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="e7d65-121">服務已設有七個複本，但叢集只有五個節點，所以有兩個複本無法安置。</span><span class="sxs-lookup"><span data-stu-id="e7d65-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="e7d65-122">雖然這裡沒有顯示，但因為來自 `System.FM` 的系統報告顯示 `Partition is below target replica or instance count`，所以服務磁碟分割為黃色。</span><span class="sxs-lookup"><span data-stu-id="e7d65-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="e7d65-123">黃色分割區觸發了黃色服務。</span><span class="sxs-lookup"><span data-stu-id="e7d65-123">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="e7d65-124">因為應用程式是紅色，所以叢集為紅色。</span><span class="sxs-lookup"><span data-stu-id="e7d65-124">The cluster is red because of the red application.</span></span>

<span data-ttu-id="e7d65-125">評估使用叢集資訊清單和應用程式資訊清單的預設原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-125">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="e7d65-126">它們是嚴格的原則，不容許任何失敗。</span><span class="sxs-lookup"><span data-stu-id="e7d65-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="e7d65-127">使用 Service Fabric 總管檢視叢集：</span><span class="sxs-lookup"><span data-stu-id="e7d65-127">View of the cluster with Service Fabric Explorer:</span></span>

![使用 Service Fabric 總管檢視叢集。][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="e7d65-129">深入了解 [Service Fabric 總管](service-fabric-visualizing-your-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="e7d65-130">健康情況查詢</span><span class="sxs-lookup"><span data-stu-id="e7d65-130">Health queries</span></span>
<span data-ttu-id="e7d65-131">Service Fabric 會針對每種支援的 [實體類型](service-fabric-health-introduction.md#health-entities-and-hierarchy)公開健康情況查詢。</span><span class="sxs-lookup"><span data-stu-id="e7d65-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="e7d65-132">您可透過 API (在 [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet) 上使用方法)、PowerShell Cmdlet 和 REST 來存取查詢。</span><span class="sxs-lookup"><span data-stu-id="e7d65-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="e7d65-133">這些查詢會傳回實體的完整健康情況資訊：彙總健康情況、實體健康事件、子系健康情況 (如果適用)、狀況不佳評估 (當實體狀況不佳時)，以及子系健康情況統計資料 (如果適用)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="e7d65-134">當健康狀態存放區中完全填滿一個健全狀況實體時，將會傳回此健全狀況實體。</span><span class="sxs-lookup"><span data-stu-id="e7d65-134">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="e7d65-135">實體必須是作用中 (未刪除)，並且具有系統報告。</span><span class="sxs-lookup"><span data-stu-id="e7d65-135">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="e7d65-136">階層鏈結上其父實體也必須有系統報告。</span><span class="sxs-lookup"><span data-stu-id="e7d65-136">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="e7d65-137">如果無法達成上述任何條件，健康情況查詢會傳回具有 [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` 的 [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception)，以顯示為何不傳回實體。</span><span class="sxs-lookup"><span data-stu-id="e7d65-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="e7d65-138">健康情況查詢需要傳入實體識別碼，識別碼會視實體類型而定。</span><span class="sxs-lookup"><span data-stu-id="e7d65-138">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="e7d65-139">查詢會接受選擇性的健康情況原則參數。</span><span class="sxs-lookup"><span data-stu-id="e7d65-139">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="e7d65-140">如果未指定健康狀態原則，則會使用叢集或應用程式資訊清單的 [健康狀態原則](service-fabric-health-introduction.md#health-policies) 進行評估。</span><span class="sxs-lookup"><span data-stu-id="e7d65-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="e7d65-141">如果資訊清單不包含的健康狀態原則的定義，則預設健康情況原則會用於評估。</span><span class="sxs-lookup"><span data-stu-id="e7d65-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span></span> <span data-ttu-id="e7d65-142">預設健康情況原則不容許任何失敗。</span><span class="sxs-lookup"><span data-stu-id="e7d65-142">The default health policies do not tolerate any failures.</span></span> <span data-ttu-id="e7d65-143">查詢也接受只傳回部分事件或子事件的篩選，這些事件與所指定的篩選相符。</span><span class="sxs-lookup"><span data-stu-id="e7d65-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span> <span data-ttu-id="e7d65-144">另一個篩選條件允許排除子系統計資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-144">Another filter allows excluding the children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="e7d65-145">輸出篩選會套用在伺服器端，所以訊息回覆的大小會減少。</span><span class="sxs-lookup"><span data-stu-id="e7d65-145">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="e7d65-146">建議使用輸出篩選來限制傳回的資料，而不是在用戶端上套用篩選。</span><span class="sxs-lookup"><span data-stu-id="e7d65-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="e7d65-147">實體的健康狀態包含︰</span><span class="sxs-lookup"><span data-stu-id="e7d65-147">An entity's health contains:</span></span>

* <span data-ttu-id="e7d65-148">實體的彙總健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-148">The aggregated health state of the entity.</span></span> <span data-ttu-id="e7d65-149">健康狀態資料存放區根據實體健康狀態報告、子健全狀況狀態 (如果適用) 和健康狀態原則所判斷的結果。</span><span class="sxs-lookup"><span data-stu-id="e7d65-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="e7d65-150">深入了解 [實體健康情況評估](service-fabric-health-introduction.md#health-evaluation)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="e7d65-151">實體上的健康情況事件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-151">The health events on the entity.</span></span>
* <span data-ttu-id="e7d65-152">針對可以有子系的實體，提供所有子系的健康情況狀態集合。</span><span class="sxs-lookup"><span data-stu-id="e7d65-152">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="e7d65-153">健康情況狀態包含實體識別碼和彙總健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-153">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="e7d65-154">若要取得子系的完整健康情況，請傳入子系識別碼，呼叫子實體類型的查詢健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="e7d65-155">如果實體的狀況不佳，則健康情況不佳的評估會指向觸發實體狀態的報告。</span><span class="sxs-lookup"><span data-stu-id="e7d65-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span> <span data-ttu-id="e7d65-156">評估是遞迴式的，其中包含觸發目前健康情況的子系健康情況評估。</span><span class="sxs-lookup"><span data-stu-id="e7d65-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span></span> <span data-ttu-id="e7d65-157">例如，看門狗回報了複本錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7d65-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="e7d65-158">應用程式健康情況會顯示狀況不良服務所致的狀況不良評估；服務因為磁碟分割發生錯誤而處於健康情況不良狀態；磁碟分割因為複本發生錯誤而處於健康情況不良狀態；複本因為看門狗錯誤健康情況報告而處於健康情況不良狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span></span>
* <span data-ttu-id="e7d65-159">具有子系之實體的所有子系類型的健康情況統計資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-159">The health statistics for all children types of the entities that have children.</span></span> <span data-ttu-id="e7d65-160">例如，叢集健康情況可顯示叢集中的應用程式、服務、磁碟分割、複本，以及已部署實體總數。</span><span class="sxs-lookup"><span data-stu-id="e7d65-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span></span> <span data-ttu-id="e7d65-161">服務健康情況會顯示指定的服務之下的磁碟分割和複本總數。</span><span class="sxs-lookup"><span data-stu-id="e7d65-161">Service health shows the total number of partitions and replicas under the specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="e7d65-162">取得叢集健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-162">Get cluster health</span></span>
<span data-ttu-id="e7d65-163">傳回叢集實體的健全狀況，並且包含應用程式和節點 (叢集的子系) 的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="e7d65-164">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-164">Input:</span></span>

* <span data-ttu-id="e7d65-165">[選擇性] 用來評估節點和叢集事件的叢集健康狀態原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="e7d65-166">[選擇性] 應用程式健康情況原則對應，加上用來覆寫應用程式資訊清單原則的健康情況原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="e7d65-167">[選擇性] 事件、節點和應用程式的篩選，指定對那些項目感到興趣，並且應該在結果中傳回 (例如，僅限錯誤、或警告和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="e7d65-168">所有事件、節點及應用程式都會用來評估實體彙總健全狀況，不論篩選器為何。</span><span class="sxs-lookup"><span data-stu-id="e7d65-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="e7d65-169">[選用] 用於排除健康情況統計資料的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-169">[Optional] Filter to exclude health statistics.</span></span>
* <span data-ttu-id="e7d65-170">[選用] 用於在健康情況統計資料中包含 fabric:/系統健康情況統計資料的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span></span> <span data-ttu-id="e7d65-171">僅適用於未排除健康情況統計資料時。</span><span class="sxs-lookup"><span data-stu-id="e7d65-171">Only applicable when the health statistics are not excluded.</span></span> <span data-ttu-id="e7d65-172">根據預設，健康情況統計資料只包含使用者應用程式的統計資料，而不包含系統應用程式的統計資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-172">By default, the health statistics include only statistics for user applications and not the System application.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-173">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-173">API</span></span>
<span data-ttu-id="e7d65-174">若要取得叢集健康情況，請建立 `FabricClient` ，並在其 [HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) 上呼叫 **GetClusterHealthAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="e7d65-175">下列呼叫會取得叢集健全狀況︰</span><span class="sxs-lookup"><span data-stu-id="e7d65-175">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="e7d65-176">以下程式碼使用自訂的叢集健全狀況原則和針對節點與應用程式的篩選，取得叢集健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="e7d65-177">其指定健康情況統計資料包含 fabric:/系統統計資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-177">It specifies that the health statistics include the fabric:/System statistics.</span></span> <span data-ttu-id="e7d65-178">這會建立包含輸入資訊的 [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="e7d65-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-179">PowerShell</span></span>
<span data-ttu-id="e7d65-180">取得叢集健康情況的 Cmdlet 是 [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="e7d65-181">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e7d65-182">叢集的狀態是五個節點、系統應用程式和依所述設定的 fabric:/WordCount。</span><span class="sxs-lookup"><span data-stu-id="e7d65-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="e7d65-183">以下 Cmdlet 會使用預設的健康情況原則，取得叢集健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-183">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="e7d65-184">彙總健康情況為警告，因為 fabric:/WordCount 應用程式處於警告狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="e7d65-185">請注意健康情況不佳的評估，會如何提供觸發彙總健康情況的條件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="e7d65-186">以下 Powershell Cmdlet 會使用自訂的應用程式原則，取得叢集的健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="e7d65-187">它會篩選結果，只取得發生錯誤或警告的應用程式和節點。</span><span class="sxs-lookup"><span data-stu-id="e7d65-187">It filters results to get only applications and nodes in error or warning.</span></span> <span data-ttu-id="e7d65-188">因此不會傳回任何節點，因為全部都狀況良好。</span><span class="sxs-lookup"><span data-stu-id="e7d65-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="e7d65-189">只有 fabric:/WordCount 應用程式符合應用程式篩選。</span><span class="sxs-lookup"><span data-stu-id="e7d65-189">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="e7d65-190">由於自訂原則針對 fabric:/WordCount 應用程式，指定將警告視為錯誤，因此應用程式以及叢集，均被評估為錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7d65-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="e7d65-191">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-191">REST</span></span>
<span data-ttu-id="e7d65-192">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) (含有其本文中所述的健康狀態原則) 取得叢集健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="e7d65-193">取得節點的健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-193">Get node health</span></span>
<span data-ttu-id="e7d65-194">傳回節點實體的健全狀況，並且包含節點上報告的健康狀態事件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-194">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="e7d65-195">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-195">Input:</span></span>

* <span data-ttu-id="e7d65-196">[必要] 可識別節點的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="e7d65-196">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="e7d65-197">[選擇性] 用來評估健康情況的叢集健康情況原則設定。</span><span class="sxs-lookup"><span data-stu-id="e7d65-197">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="e7d65-198">[選擇性] 事件的篩選，指定對那些項目感到興趣，並且應該在結果中傳回 (例如，僅限錯誤、或警告和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="e7d65-199">所有事件都會用來評估實體彙總健全狀況，不論篩選器為何。</span><span class="sxs-lookup"><span data-stu-id="e7d65-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-200">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-200">API</span></span>
<span data-ttu-id="e7d65-201">若要透過 API 取得節點健全狀況，請建立 `FabricClient` ，並在其 HealthManager 上呼叫 [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) 方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="e7d65-202">以下程式碼會取得指定節點名稱的節點健全狀況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-202">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="e7d65-203">以下程式碼會透過 [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription)傳入事件篩選和自訂原則，取得指定節點名稱的節點健全狀況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="e7d65-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-204">PowerShell</span></span>
<span data-ttu-id="e7d65-205">取得節點健全狀況的 Cmdlet 是 [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="e7d65-206">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="e7d65-207">以下 Cmdlet 會使用預設的健康情況原則，取得節點健康情況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-207">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="e7d65-208">以下 Cmdlet 會取得叢集中所有節點的健康情況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-208">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="e7d65-209">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-209">REST</span></span>
<span data-ttu-id="e7d65-210">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) (含有其本文中所述的健康狀態原則) 取得節點健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="e7d65-211">取得應用程式健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-211">Get application health</span></span>
<span data-ttu-id="e7d65-212">傳回應用程式實體的健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-212">Returns the health of an application entity.</span></span> <span data-ttu-id="e7d65-213">包含已部署應用程式和服務子系的健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-213">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="e7d65-214">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-214">Input:</span></span>

* <span data-ttu-id="e7d65-215">[必要] 可識別應用程式的應用程式名稱 (URI)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-215">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="e7d65-216">[選擇性] 用來覆寫應用程式資訊清單原則的應用程式健康情況原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-216">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="e7d65-217">[選擇性] 事件、服務和已部署應用程式的篩選，指定對那些項目感到興趣，並且應該在結果中傳回 (例如，僅限錯誤、或警告和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="e7d65-218">所有事件、服務及已部署應用程式都會用來評估實體彙總健全狀況，不論篩選器為何。</span><span class="sxs-lookup"><span data-stu-id="e7d65-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="e7d65-219">[選用] 用於排除健康情況統計資料的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-219">[Optional] Filter to exclude the health statistics.</span></span> <span data-ttu-id="e7d65-220">如果未指定，健康情況統計資料包含所有應用程式子系的 OK、警告和錯誤計數：服務、磁碟分割、複本、已部署的應用程式及已部署的服務套件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-221">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-221">API</span></span>
<span data-ttu-id="e7d65-222">若要取得應用程式健全狀況，請建立 `FabricClient` ，並在其 HealthManager 上呼叫 [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) 方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="e7d65-223">以下程式碼會取得指定應用程式名稱 (URI) 的應用程式健全狀況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-223">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="e7d65-224">以下程式碼會透過 [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription)指定篩選和自訂原則，取得指定應用程式名稱 (URI) 的應用程式健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="e7d65-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-225">PowerShell</span></span>
<span data-ttu-id="e7d65-226">取得應用程式健全狀況的 Cmdlet 是 [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="e7d65-227">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e7d65-228">以下 Cmdlet 會傳回 **fabric:/WordCount** 應用程式的健全狀況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="e7d65-229">以下 PowerShell Cmdlet 會傳入自訂原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-229">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="e7d65-230">它也會篩選子系和事件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="e7d65-231">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-231">REST</span></span>
<span data-ttu-id="e7d65-232">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) (含有其本文中所述的健康狀態原則) 取得應用程式健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="e7d65-233">取得服務健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-233">Get service health</span></span>
<span data-ttu-id="e7d65-234">傳回服務實體的健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-234">Returns the health of a service entity.</span></span> <span data-ttu-id="e7d65-235">包含分割區的健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-235">It contains the partition health states.</span></span> <span data-ttu-id="e7d65-236">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-236">Input:</span></span>

* <span data-ttu-id="e7d65-237">[必要] 可識別服務的服務名稱 (URI)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-237">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="e7d65-238">[選擇性] 用來覆寫應用程式資訊清單原則的應用程式健康情況原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-238">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="e7d65-239">[選擇性] 事件和分割區的篩選，指定對那些項目感到興趣，並且應該在結果中傳回 (例如，僅限錯誤、或警告和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="e7d65-240">所有事件和分割區都會用來評估實體彙總健全狀況，不論篩選器為何。</span><span class="sxs-lookup"><span data-stu-id="e7d65-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="e7d65-241">[選用] 用於排除健康情況統計資料的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-241">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="e7d65-242">如果未指定，健康情況統計資料會顯示服務的所有磁碟分割和複本之 OK、警告和錯誤計數。</span><span class="sxs-lookup"><span data-stu-id="e7d65-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-243">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-243">API</span></span>
<span data-ttu-id="e7d65-244">若要透過 API 取得服務健全狀況，請建立 `FabricClient` ，並在其 HealthManager 上呼叫 [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) 方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="e7d65-245">以下範例會使用指定的服務名稱 (URI)，取得服務的健康情況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-245">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="e7d65-246">以下程式碼會透過 [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription)指定篩選和自訂原則，取得指定服務名稱 (URI) 的服務健全狀況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="e7d65-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-247">PowerShell</span></span>
<span data-ttu-id="e7d65-248">取得服務健全狀況的 Cmdlet 是 [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="e7d65-249">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e7d65-250">以下 Cmdlet 會使用預設的健康情況原則，取得服務健康情況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-250">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="e7d65-251">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-251">REST</span></span>
<span data-ttu-id="e7d65-252">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) (含有其本文中所述的健康狀態原則) 取得服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="e7d65-253">取得分割區健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-253">Get partition health</span></span>
<span data-ttu-id="e7d65-254">傳回分割區實體的健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-254">Returns the health of a partition entity.</span></span> <span data-ttu-id="e7d65-255">包含複本的健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-255">It contains the replica health states.</span></span> <span data-ttu-id="e7d65-256">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-256">Input:</span></span>

* <span data-ttu-id="e7d65-257">[必要] 可識別分割區的分割識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-257">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="e7d65-258">[選擇性] 用來覆寫應用程式資訊清單原則的應用程式健康情況原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-258">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="e7d65-259">[選擇性] 事件和複本的篩選，指定對那些項目感到興趣，並且應該在結果中傳回 (例如，僅限錯誤、或警告和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="e7d65-260">所有事件和複本都會用來評估實體彙總健全狀況，不論篩選器為何。</span><span class="sxs-lookup"><span data-stu-id="e7d65-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="e7d65-261">[選用] 用於排除健康情況統計資料的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-261">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="e7d65-262">如果未指定，健康情況統計資料會顯示處於 OK、警告和錯誤狀態的複本數目。</span><span class="sxs-lookup"><span data-stu-id="e7d65-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-263">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-263">API</span></span>
<span data-ttu-id="e7d65-264">若要透過 API 取得分割區健全狀況，請建立 `FabricClient` ，並在其 HealthManager 上呼叫 [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) 方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="e7d65-265">若要指定選擇性參數，請建立 [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="e7d65-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-266">PowerShell</span></span>
<span data-ttu-id="e7d65-267">取得分割區健全狀況的 Cmdlet 是 [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="e7d65-268">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e7d65-269">以下 Cmdlet 會取得 **fabric:/WordCount/WordCountService** 服務之所有磁碟分割的健康情況，並篩選掉複本健康情況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="e7d65-270">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-270">REST</span></span>
<span data-ttu-id="e7d65-271">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) (含有其本文中所述的健康狀態原則) 取得分割區健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="e7d65-272">取得複本健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-272">Get replica health</span></span>
<span data-ttu-id="e7d65-273">傳回可設定具狀態服務複本或無狀態服務執行個體的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-273">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="e7d65-274">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-274">Input:</span></span>

* <span data-ttu-id="e7d65-275">[必要] 可識別複本的分割區識別碼 (GUID) 和複本識別碼。</span><span class="sxs-lookup"><span data-stu-id="e7d65-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="e7d65-276">[選擇性] 用來覆寫應用程式資訊清單原則的應用程式健康情況原則參數。</span><span class="sxs-lookup"><span data-stu-id="e7d65-276">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="e7d65-277">[選擇性] 事件的篩選，指定對那些項目感到興趣，並且應該在結果中傳回 (例如，僅限錯誤、或警告和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="e7d65-278">所有事件都會用來評估實體彙總健全狀況，不論篩選器為何。</span><span class="sxs-lookup"><span data-stu-id="e7d65-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-279">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-279">API</span></span>
<span data-ttu-id="e7d65-280">若要透過 API 取得複本健全狀況，請建立 `FabricClient` ，並在其 HealthManager 上呼叫 [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) 方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="e7d65-281">若要指定進階參數，請使用 [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="e7d65-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-282">PowerShell</span></span>
<span data-ttu-id="e7d65-283">取得複本健全狀況的 Cmdlet 是 [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="e7d65-284">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e7d65-285">以下 Cmdlet 會針對服務的所有分割區取得主要複本健康情況：</span><span class="sxs-lookup"><span data-stu-id="e7d65-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="e7d65-286">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-286">REST</span></span>
<span data-ttu-id="e7d65-287">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) (含有其本文中所述的健康狀態原則) 取得複本健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="e7d65-288">取得已部署應用程式的健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-288">Get deployed application health</span></span>
<span data-ttu-id="e7d65-289">傳回部署在節點實體上的應用程式健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-289">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="e7d65-290">包含已部署的服務封裝健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-290">It contains the deployed service package health states.</span></span> <span data-ttu-id="e7d65-291">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-291">Input:</span></span>

* <span data-ttu-id="e7d65-292">[必要] 可識別已部署應用程式的應用程式名稱 (URI) 和節點名稱 (字串)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="e7d65-293">[選擇性] 用來覆寫應用程式資訊清單原則的應用程式健康情況原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-293">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="e7d65-294">[選擇性] 事件和已部署服務封裝的篩選，指定對那些項目感到興趣，並且應該在結果中傳回 (例如，僅限錯誤、或警告和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="e7d65-295">所有事件和已部署服務封裝都會用來評估實體彙總健全狀況，不論篩選器為何。</span><span class="sxs-lookup"><span data-stu-id="e7d65-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="e7d65-296">[選用] 用於排除健康情況統計資料的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-296">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="e7d65-297">如果未指定，健康情況統計資料會顯示處於 OK、警告和錯誤健康狀態的已部署服務套件數目。</span><span class="sxs-lookup"><span data-stu-id="e7d65-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-298">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-298">API</span></span>
<span data-ttu-id="e7d65-299">若要透過 API 取得部署在節點上之應用程式的健全狀況，請建立 `FabricClient` 並在其 HealthManager 上呼叫 [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) 方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="e7d65-300">若要指定選擇性參數，請使用 [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="e7d65-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-301">PowerShell</span></span>
<span data-ttu-id="e7d65-302">取得已部署應用程式健全狀況的 Cmdlet 是 [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="e7d65-303">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="e7d65-304">若要找出應用程式的部署位置，請執行 [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ，並查看部署的應用程式子系。</span><span class="sxs-lookup"><span data-stu-id="e7d65-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span></span>

<span data-ttu-id="e7d65-305">以下 Cmdlet 會取得部署在 **_Node_2** 節點上的 **fabric:/WordCount** 應用程式健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="e7d65-306">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-306">REST</span></span>
<span data-ttu-id="e7d65-307">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) (含有其本文中所述的健康狀態原則) 取得已部署應用程式健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="e7d65-308">取得已部署服務封裝的健康情況</span><span class="sxs-lookup"><span data-stu-id="e7d65-308">Get deployed service package health</span></span>
<span data-ttu-id="e7d65-309">傳回已部署服務封裝實體的健康情況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-309">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="e7d65-310">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-310">Input:</span></span>

* <span data-ttu-id="e7d65-311">[必要] 可識別已部署服務封裝的應用程式名稱 (URI)、節點名稱 (字串) 及服務資訊清單名稱 (字串)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="e7d65-312">[選擇性] 用來覆寫應用程式資訊清單原則的應用程式健康情況原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-312">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="e7d65-313">[選擇性] 事件的篩選，指定對那些項目感到興趣，並且應該在結果中傳回 (例如，僅限錯誤、或警告和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="e7d65-314">所有事件都會用來評估實體彙總健全狀況，不論篩選器為何。</span><span class="sxs-lookup"><span data-stu-id="e7d65-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-315">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-315">API</span></span>
<span data-ttu-id="e7d65-316">若要透過 API 取得已部署服務套件的健全狀況，請建立 `FabricClient` ，並在其 HealthManager 上呼叫 [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) 方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="e7d65-317">若要指定選擇性參數，請使用 [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="e7d65-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-318">PowerShell</span></span>
<span data-ttu-id="e7d65-319">取得已部署服務套件健全狀況的 Cmdlet 是 [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="e7d65-320">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="e7d65-321">若要查看應用程式的部署位置，請執行 [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ，並查看部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7d65-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span></span> <span data-ttu-id="e7d65-322">若要查看應用程式中的服務封裝件為何，請檢視 [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) 輸出中已部署服務封裝的子系。</span><span class="sxs-lookup"><span data-stu-id="e7d65-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="e7d65-323">以下 Cmdlet 會取得部署在 **_Node_2** 節點上 **fabric:/WordCount** 應用程式的 **WordCountServicePkg** 服務套件健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="e7d65-324">此實體的 **System.Hosting** 報告具有成功的服務封裝和進入點啟用，以及成功的服務類型註冊。</span><span class="sxs-lookup"><span data-stu-id="e7d65-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="e7d65-325">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-325">REST</span></span>
<span data-ttu-id="e7d65-326">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) (含有其本文中所述的健康狀態原則) 取得已部署服務封裝的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="e7d65-327">健全狀況區塊查詢</span><span class="sxs-lookup"><span data-stu-id="e7d65-327">Health chunk queries</span></span>
<span data-ttu-id="e7d65-328">健全狀況區塊查詢可以傳回每個輸入篩選器的多層級叢集子系 (以遞迴方式)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="e7d65-329">它支援的進階篩選條件允許在選擇要傳回的子系時有很大的彈性。</span><span class="sxs-lookup"><span data-stu-id="e7d65-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span></span> <span data-ttu-id="e7d65-330">篩選條件可以依照唯一識別碼或依照其他群組識別碼和/或健康情況來指定子系。</span><span class="sxs-lookup"><span data-stu-id="e7d65-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="e7d65-331">根據預設，沒有子系包含在內，不同於永遠包含第一個層級子系的健全狀況命令。</span><span class="sxs-lookup"><span data-stu-id="e7d65-331">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="e7d65-332">[健全狀況查詢](service-fabric-view-entities-aggregated-health.md#health-queries) 只會傳回每個必要篩選器之指定實體的第一個層級子系。</span><span class="sxs-lookup"><span data-stu-id="e7d65-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="e7d65-333">若要取得子系的子系，您必須呼叫每個相關實體的其他健全狀況 API。</span><span class="sxs-lookup"><span data-stu-id="e7d65-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="e7d65-334">同樣地，若要取得特定實體的健全狀況，您必須呼叫每個所需實體的一個健全狀況 API。</span><span class="sxs-lookup"><span data-stu-id="e7d65-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="e7d65-335">區塊查詢進階篩選可讓您在一個查詢中要求多個相關項目，將訊息大小和訊息數目降至最低。</span><span class="sxs-lookup"><span data-stu-id="e7d65-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="e7d65-336">區塊查詢的值是您可以在一個呼叫中取得多個叢集實體 (可能是在必要的根開始的所有叢集實體) 的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="e7d65-337">您可以如下表示複雜的健全狀況查詢︰</span><span class="sxs-lookup"><span data-stu-id="e7d65-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="e7d65-338">只傳回發生錯誤的應用程式，以及針對這些應用程式，包含所有發生警告或錯誤的服務。</span><span class="sxs-lookup"><span data-stu-id="e7d65-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="e7d65-339">針對傳回的服務，包含所有分割。</span><span class="sxs-lookup"><span data-stu-id="e7d65-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="e7d65-340">只傳回 4 個應用程式的健康情況，由其名稱指定。</span><span class="sxs-lookup"><span data-stu-id="e7d65-340">Return only the health of four applications, specified by their names.</span></span>
* <span data-ttu-id="e7d65-341">只傳回所需應用程式類型的應用程式健全狀況。</span><span class="sxs-lookup"><span data-stu-id="e7d65-341">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="e7d65-342">傳回單一節點上所有已部署的實體。</span><span class="sxs-lookup"><span data-stu-id="e7d65-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="e7d65-343">傳回所有應用程式，單一指定節點上所有已部署的應用程式，與該節點上所有已部署的服務封裝。</span><span class="sxs-lookup"><span data-stu-id="e7d65-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="e7d65-344">傳回所有發生錯誤的複本。</span><span class="sxs-lookup"><span data-stu-id="e7d65-344">Return all replicas in error.</span></span> <span data-ttu-id="e7d65-345">傳回所有應用程式、服務、磁碟分割，以及只傳回發生錯誤的複本。</span><span class="sxs-lookup"><span data-stu-id="e7d65-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="e7d65-346">傳回所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7d65-346">Return all applications.</span></span> <span data-ttu-id="e7d65-347">針對指定的服務，包含所有分割。</span><span class="sxs-lookup"><span data-stu-id="e7d65-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="e7d65-348">目前的健全狀況區塊查詢僅對叢集實體公開。</span><span class="sxs-lookup"><span data-stu-id="e7d65-348">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="e7d65-349">它會傳回叢集健全狀況區塊，其中包含︰</span><span class="sxs-lookup"><span data-stu-id="e7d65-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="e7d65-350">叢集彙總健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-350">The cluster aggregated health state.</span></span>
* <span data-ttu-id="e7d65-351">採用輸入篩選器的節點健康狀態區塊清單。</span><span class="sxs-lookup"><span data-stu-id="e7d65-351">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="e7d65-352">採用輸入篩選器的應用程式健康狀態區塊清單。</span><span class="sxs-lookup"><span data-stu-id="e7d65-352">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="e7d65-353">每個應用程式健康狀態區塊都包含下列兩個區塊清單，具備所有採用輸入篩選器之服務的區塊清單，以及具備所有採用篩選器之部署應用程式的區塊清單。</span><span class="sxs-lookup"><span data-stu-id="e7d65-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="e7d65-354">對於服務和已部署應用程式的子系亦然。</span><span class="sxs-lookup"><span data-stu-id="e7d65-354">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="e7d65-355">如此一來，叢集中的所有實體都有可能在要求時以階層的形式傳回。</span><span class="sxs-lookup"><span data-stu-id="e7d65-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="e7d65-356">叢集健全狀況區塊查詢</span><span class="sxs-lookup"><span data-stu-id="e7d65-356">Cluster health chunk query</span></span>
<span data-ttu-id="e7d65-357">傳回叢集實體的健全狀況，並包含必要子系的階層健康狀態區塊。</span><span class="sxs-lookup"><span data-stu-id="e7d65-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="e7d65-358">輸入：</span><span class="sxs-lookup"><span data-stu-id="e7d65-358">Input:</span></span>

* <span data-ttu-id="e7d65-359">[選擇性] 用來評估節點和叢集事件的叢集健康狀態原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="e7d65-360">[選擇性] 應用程式健康情況原則對應，加上用來覆寫應用程式資訊清單原則的健康情況原則。</span><span class="sxs-lookup"><span data-stu-id="e7d65-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="e7d65-361">[選擇性] 節點和應用程式的篩選器，指定對那些項目感到興趣，並且應該在結果中傳回。</span><span class="sxs-lookup"><span data-stu-id="e7d65-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="e7d65-362">篩選器專屬於實體的實體/群組，或適用於該層級的所有實體。</span><span class="sxs-lookup"><span data-stu-id="e7d65-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="e7d65-363">篩選器清單可包含一個一般篩選器及/或由查詢傳回之細微實體的特定識別碼篩選器。</span><span class="sxs-lookup"><span data-stu-id="e7d65-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="e7d65-364">如果子系是空的，依預設不會傳回子系。</span><span class="sxs-lookup"><span data-stu-id="e7d65-364">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="e7d65-365">如需深入了解篩選器，請參閱 [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) 和 [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="e7d65-366">應用程式篩選器可以遞迴方式指定進階的篩選器給子系。</span><span class="sxs-lookup"><span data-stu-id="e7d65-366">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="e7d65-367">區塊結果包含採用篩選器的子系。</span><span class="sxs-lookup"><span data-stu-id="e7d65-367">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="e7d65-368">區塊查詢目前不會傳回狀況不良的評估或實體事件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="e7d65-369">該額外資訊可使用現有的叢集健全狀況查詢取得。</span><span class="sxs-lookup"><span data-stu-id="e7d65-369">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="e7d65-370">API</span><span class="sxs-lookup"><span data-stu-id="e7d65-370">API</span></span>
<span data-ttu-id="e7d65-371">若要取得叢集健康區塊，請建立 `FabricClient` ，並在其 [HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) 上呼叫 **GetClusterHealthChunkAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="e7d65-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="e7d65-372">您可以傳入 [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) 來描述健全狀況原則和進階篩選器。</span><span class="sxs-lookup"><span data-stu-id="e7d65-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="e7d65-373">下列程式碼使用進階篩選器取得叢集健全狀況區塊。</span><span class="sxs-lookup"><span data-stu-id="e7d65-373">The following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except the ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="e7d65-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7d65-374">PowerShell</span></span>
<span data-ttu-id="e7d65-375">取得叢集健全狀況的 Cmdlet 是 [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="e7d65-376">首先會使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e7d65-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e7d65-377">下列程式碼只有在錯誤時才會取得節點，只有一個特定節點例外，應該一律將其傳回。</span><span class="sxs-lookup"><span data-stu-id="e7d65-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="e7d65-378">下列 Cmdlet 會利用應用程式篩選器取得叢集區塊。</span><span class="sxs-lookup"><span data-stu-id="e7d65-378">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="e7d65-379">下列 Cmdlet 會傳回單一節點上所有的已部署實體。</span><span class="sxs-lookup"><span data-stu-id="e7d65-379">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="e7d65-380">REST</span><span class="sxs-lookup"><span data-stu-id="e7d65-380">REST</span></span>
<span data-ttu-id="e7d65-381">您可以使用 [GET 要求](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks)或 [POST 要求](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) (含有其本文中所述的健康狀態原則和進階篩選) 取得叢集健全狀況區塊。</span><span class="sxs-lookup"><span data-stu-id="e7d65-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="e7d65-382">一般查詢</span><span class="sxs-lookup"><span data-stu-id="e7d65-382">General queries</span></span>
<span data-ttu-id="e7d65-383">一般查詢會傳回指定類型的 Service Fabric 實體清單。</span><span class="sxs-lookup"><span data-stu-id="e7d65-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="e7d65-384">這些查詢會透過 API (透過 **FabricClient.QueryManager**上的方法)、Powershell Cmdlet 和 REST 來公開。</span><span class="sxs-lookup"><span data-stu-id="e7d65-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="e7d65-385">這些查詢會從多個元件彙總子查詢。</span><span class="sxs-lookup"><span data-stu-id="e7d65-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="e7d65-386">其中一個元件是 [健康狀態資料存放區](service-fabric-health-introduction.md#health-store)，它會針對每個查詢結果填入彙總健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="e7d65-387">一般查詢會傳回實體的彙總健康情況狀態，但不包含豐富的健康情況資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="e7d65-388">如果實體狀況不佳，您可以使用健康情況查詢加以追蹤，以取得所有的健康情況資訊，包括事件、子系健康情況狀態和健康情況不佳的評估。</span><span class="sxs-lookup"><span data-stu-id="e7d65-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="e7d65-389">如果一般查詢傳回不明的實體健康狀態，則可能是健康狀態存放區中沒有實體的完整資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="e7d65-390">此外，也可能是健康狀態存放區的子查詢未成功 (例如，發生通訊錯誤，或已節流處理健康狀態存放區)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="e7d65-391">請針對實體使用健康情況查詢加以追蹤。</span><span class="sxs-lookup"><span data-stu-id="e7d65-391">Follow up with a health query for the entity.</span></span> <span data-ttu-id="e7d65-392">如果子查詢發生暫時性錯誤，例如網路問題，此待處理的查詢可能會成功。</span><span class="sxs-lookup"><span data-stu-id="e7d65-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="e7d65-393">它也可以從健康狀態存放區提供關於為何實體不公開的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-393">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="e7d65-394">包含實體 **HealthState** 的查詢為：</span><span class="sxs-lookup"><span data-stu-id="e7d65-394">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="e7d65-395">節點清單：傳回叢集中的節點清單 (已分頁)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-395">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="e7d65-396">API： [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="e7d65-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="e7d65-397">PowerShell：Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e7d65-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="e7d65-398">應用程式清單：傳回叢集中的應用程式清單 (已分頁)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-398">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="e7d65-399">API： [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="e7d65-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="e7d65-400">PowerShell：Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="e7d65-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="e7d65-401">服務清單：傳回應用程式中的服務清單 (已分頁)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-401">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="e7d65-402">API： [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="e7d65-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="e7d65-403">PowerShell：Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="e7d65-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="e7d65-404">分割區清單：傳回服務中的分割區清單 (已分頁)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-404">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="e7d65-405">API： [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="e7d65-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="e7d65-406">PowerShell：Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="e7d65-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="e7d65-407">複本清單：傳回分割區中的複本清單 (已分頁)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-407">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="e7d65-408">API： [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="e7d65-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="e7d65-409">PowerShell：Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="e7d65-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="e7d65-410">已部署應用程式清單：傳回節點上已部署應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e7d65-410">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="e7d65-411">API： [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="e7d65-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="e7d65-412">PowerShell：Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="e7d65-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="e7d65-413">已部署服務封裝清單：傳回已部署應用程式中的服務封裝清單。</span><span class="sxs-lookup"><span data-stu-id="e7d65-413">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="e7d65-414">API： [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="e7d65-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="e7d65-415">PowerShell：Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="e7d65-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="e7d65-416">有些查詢會傳回已分頁的結果。</span><span class="sxs-lookup"><span data-stu-id="e7d65-416">Some of the queries return paged results.</span></span> <span data-ttu-id="e7d65-417">這些查詢的傳回內容是衍生自 [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1) 的清單。</span><span class="sxs-lookup"><span data-stu-id="e7d65-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="e7d65-418">如果結果不符合訊息，只會傳回頁面，且 ContinuationToken 會追蹤列舉停止之處。</span><span class="sxs-lookup"><span data-stu-id="e7d65-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="e7d65-419">繼續呼叫相同的查詢，並從先前的查詢傳入接續權杖以取得後續結果。</span><span class="sxs-lookup"><span data-stu-id="e7d65-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="e7d65-420">範例</span><span class="sxs-lookup"><span data-stu-id="e7d65-420">Examples</span></span>
<span data-ttu-id="e7d65-421">以下程式碼會取得叢集中健全狀況不佳的應用程式：</span><span class="sxs-lookup"><span data-stu-id="e7d65-421">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="e7d65-422">以下 Cmdlet 會取得 fabric:/WordCount 應用程式的應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="e7d65-423">請注意，健康情況狀態為警告。</span><span class="sxs-lookup"><span data-stu-id="e7d65-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="e7d65-424">以下 Cmdlet 會取得健康情況為錯誤的服務：</span><span class="sxs-lookup"><span data-stu-id="e7d65-424">The following cmdlet gets the services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="e7d65-425">叢集和應用程式升級</span><span class="sxs-lookup"><span data-stu-id="e7d65-425">Cluster and application upgrades</span></span>
<span data-ttu-id="e7d65-426">叢集與應用程式的受監視升級期間，Service Fabric 會檢查健康情況，以確保一切都能維持在健康情況良好的狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="e7d65-427">如果實體藉由使用已設定的健康狀況原則評估為狀況不良，升級會套用升級特定原則來決定下一個動作。</span><span class="sxs-lookup"><span data-stu-id="e7d65-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="e7d65-428">升級可能會暫停，以允許使用者互動 (例如修正錯誤條件或變更原則)，或是它會自動回復成先前的良好版本。</span><span class="sxs-lookup"><span data-stu-id="e7d65-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="e7d65-429">在叢集  升級期間，您可以取得叢集升級狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="e7d65-430">升級狀態包括狀況不良的評估，指向叢集中狀況不良的項目。</span><span class="sxs-lookup"><span data-stu-id="e7d65-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="e7d65-431">如果因為健全狀況問題導致升級回復，升級狀態會記住最後的狀況不良原因。</span><span class="sxs-lookup"><span data-stu-id="e7d65-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="e7d65-432">升級回復或停止之後，這項資訊可協助系統管理員調查問題出在哪裡。</span><span class="sxs-lookup"><span data-stu-id="e7d65-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="e7d65-433">同樣地，在應用程式  升級期間，應用程式升級狀態也會包含任何狀況不良的評估。</span><span class="sxs-lookup"><span data-stu-id="e7d65-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="e7d65-434">以下顯示修改後的 fabric:/WordCount 應用程式的應用程式升級狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="e7d65-435">監視程式回報了它其中一個複本的錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7d65-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="e7d65-436">因為健康情況檢查未通過，所以會將升級回復。</span><span class="sxs-lookup"><span data-stu-id="e7d65-436">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="e7d65-437">深入了解 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="e7d65-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="e7d65-438">使用健康狀況評估以進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e7d65-438">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="e7d65-439">叢集或應用程式中發生問題時，查看叢集或應用程式的健康情況，可以找出發生問題的原因。</span><span class="sxs-lookup"><span data-stu-id="e7d65-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="e7d65-440">健全狀況不佳的評估會提供觸發目前狀況不佳狀態的原因的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7d65-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="e7d65-441">如果需要，您可以向下鑽研至狀況不良的子實體，以識別根本原因。</span><span class="sxs-lookup"><span data-stu-id="e7d65-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

<span data-ttu-id="e7d65-442">例如，將應用程式視為健康情況不良，因為有其中一個複本的錯誤報告。</span><span class="sxs-lookup"><span data-stu-id="e7d65-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="e7d65-443">下列 Powershell Cmdlet 可顯示健康情況不良的評估：</span><span class="sxs-lookup"><span data-stu-id="e7d65-443">The following Powershell cmdlet shows the unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="e7d65-444">您可以查看複本，以取得詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="e7d65-444">You can look at the replica to get more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="e7d65-445">狀況不良的評估顯示實體的第一個原因評估為目前的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="e7d65-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="e7d65-446">可能有多個其他事件觸發此狀態，但是評估中不會反映這些事件。</span><span class="sxs-lookup"><span data-stu-id="e7d65-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="e7d65-447">如需詳細資訊，請向下鑽研健全狀況實體，以找出叢集中所有狀況不良的報告。</span><span class="sxs-lookup"><span data-stu-id="e7d65-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="e7d65-448">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7d65-448">Next steps</span></span>
[<span data-ttu-id="e7d65-449">使用系統健康狀態報告進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e7d65-449">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="e7d65-450">新增自訂 Service Fabric 健康狀態報告</span><span class="sxs-lookup"><span data-stu-id="e7d65-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="e7d65-451">如何回報和檢查服務健全狀況</span><span class="sxs-lookup"><span data-stu-id="e7d65-451">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="e7d65-452">在本機上監視及診斷服務</span><span class="sxs-lookup"><span data-stu-id="e7d65-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="e7d65-453">Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="e7d65-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
