---
title: "Service Fabric 叢集 Resource Manager：移動成本 | Microsoft Docs"
description: "Service Fabric 服務的移動成本概觀"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="bb0f7-103">服務移動成本</span><span class="sxs-lookup"><span data-stu-id="bb0f7-103">Service movement cost</span></span>
<span data-ttu-id="bb0f7-104">嘗試 toodetermine 何種變更 toomake tooa 叢集 hello 成本，這些變更時，會將視為 hello Service Fabric 叢集資源管理員的因素。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="bb0f7-105">"cost"hello 概念是針對可以提升多少 hello 叢集買賣關閉。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="bb0f7-106">成本在移動服務進行平衡、重組和其他需求時納入考量因素。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="bb0f7-107">hello 的目標是在 hello toomeet hello 需求最低干擾或昂貴的方法。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="bb0f7-108">移動服務會花費最少的 CPU 時間和網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="bb0f7-109">可設定狀態服務，它需要複製 hello 這些服務，因而會耗用額外的記憶體和磁碟的狀態。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="bb0f7-110">Azure Service Fabric 叢集資源管理員出現該 hello 降到最低 hello 成本的解決方案，可協助確保 hello 叢集資源不不必要地花費。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="bb0f7-111">不過，您也不想 tooignore 解決方案，將會大幅改善 hello hello 叢集中的資源配置。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="bb0f7-112">hello 叢集資源管理員有兩種運算成本，以及它會嘗試 toomanage hello 叢集時，限制他們的方式。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="bb0f7-113">hello 第一種機制只要計算它會使每次移動。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="bb0f7-114">如果這兩個方案會產生與 hello 相同平衡 （分數），然後 hello 叢集資源管理員慣用一個 hello 以 hello 最低成本 （總數會移動）。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="bb0f7-115">此策略效果不錯。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-115">This strategy works well.</span></span> <span data-ttu-id="bb0f7-116">但是若使用預設或靜態負載時，不太可能在任何複雜的系統中所有的移動都相等。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="bb0f7-117">有些可能 toobe 昂貴。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="bb0f7-118">設定移動成本</span><span class="sxs-lookup"><span data-stu-id="bb0f7-118">Setting Move Costs</span></span> 
<span data-ttu-id="bb0f7-119">在建立時，您可以指定服務的 hello 預設移動成本：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="bb0f7-120">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="bb0f7-121">C#：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="bb0f7-122">您也可以指定或 MoveCost 動態更新服務的 hello 服務已經建立完成之後：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="bb0f7-123">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="bb0f7-124">C#：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="bb0f7-125">以動態方式指定每個複本的移動成本</span><span class="sxs-lookup"><span data-stu-id="bb0f7-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="bb0f7-126">hello 上述程式碼片段是否所有指定 MoveCost 外部 hello 服務本身一次的整個服務。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="bb0f7-127">不過，移動成本是最有用時，透過其使用期限的 hello 移動成本，特定服務物件的變更。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="bb0f7-128">由於 hello 服務本身或許 hello 最好了解如何昂貴它們是 toomove 給定的時間，沒有服務 tooreport 自己個別移動成本在執行階段 API。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="bb0f7-129">C#：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="bb0f7-130">移動成本的影響</span><span class="sxs-lookup"><span data-stu-id="bb0f7-130">Impact of move cost</span></span>
<span data-ttu-id="bb0f7-131">MoveCost 有四個層級：零、低、中和高。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="bb0f7-132">MoveCosts 是相對 tooeach 其他，除了零。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="bb0f7-133">零移動成本表示移動是免費的而且不應該列入 hello hello 解決方案的分數。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="bb0f7-134">設定移動成本 tooHigh 沒有*不*保證該 hello 複本保持在同一個地方。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="bb0f7-135"><center>
![移動成本作為選取要移動之複本的因素][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="bb0f7-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="bb0f7-136">MoveCost 可協助您尋找 hello 解決方案原因整體 hello 最少中斷和是最簡單的 tooachieve 時仍抵達相等的平衡。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="bb0f7-137">服務概念，可以是成本的相對 toomany 項目。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="bb0f7-138">hello 最常見的因素計算移動成本是：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="bb0f7-139">狀態或資料 hello 服務有 toomove hello 數量。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="bb0f7-140">中斷連線的用戶端 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="bb0f7-141">移動主要複本會通常比 hello 成本，將次要複本。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="bb0f7-142">中斷執行中作業的 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="bb0f7-143">某些作業在 hello 資料儲存區層級或回應 tooa 用戶端呼叫中執行的作業成本很高。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="bb0f7-144">在特定時間點之後, 您不想 toostop 如果您不需要它們。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="bb0f7-145">因此 hello 作業正在進行的作業，而您會增加移動此服務物件 tooreduce hello 可能性 hello 移動成本。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="bb0f7-146">當 hello 作業完成時，您會設定 hello 成本後 toonormal。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="bb0f7-147">在您的叢集中啟用移動成本</span><span class="sxs-lookup"><span data-stu-id="bb0f7-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="bb0f7-148">為了讓 hello 更細微的 MoveCosts toobe 列入考量，MoveCost 必須啟用您的叢集中。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="bb0f7-149">這項設定，計算移 hello 預設模式用來計算 MoveCost，而不會忽略 MoveCost 報告。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="bb0f7-150">ClusterManifest.xml：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="bb0f7-151">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="bb0f7-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="bb0f7-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb0f7-152">Next steps</span></span>
- <span data-ttu-id="bb0f7-153">Service Fabric 叢集資源管理員會在 hello 叢集中使用度量 toomanage 耗用量和容量。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="bb0f7-154">toolearn 更多關於度量和如何 tooconfigure 它們，請參閱[管理資源耗用和服務網狀架構中的負載度量與](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="bb0f7-155">toolearn 如何 hello 叢集資源管理員管理和 hello 叢集中的負載平衡，請參閱[平衡 Service Fabric 叢集](service-fabric-cluster-resource-manager-balancing.md)。</span><span class="sxs-lookup"><span data-stu-id="bb0f7-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
