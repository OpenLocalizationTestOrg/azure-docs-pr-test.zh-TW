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
ms.openlocfilehash: 5de07c259d1d327d0211338c2911804445dd6b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="7bc10-103">服務移動成本</span><span class="sxs-lookup"><span data-stu-id="7bc10-103">Service movement cost</span></span>
<span data-ttu-id="7bc10-104">「Service Fabric 叢集資源管理員」在嘗試判斷要對叢集進行哪些變更時會考量一個因素，就是這些變更的成本。</span><span class="sxs-lookup"><span data-stu-id="7bc10-104">A factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the cost of those changes.</span></span> <span data-ttu-id="7bc10-105">「成本」的概念是針對叢集可以改善多少來做取捨。</span><span class="sxs-lookup"><span data-stu-id="7bc10-105">The notion of "cost" is traded off against how much the cluster can be improved.</span></span> <span data-ttu-id="7bc10-106">成本在移動服務進行平衡、重組和其他需求時納入考量因素。</span><span class="sxs-lookup"><span data-stu-id="7bc10-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="7bc10-107">目標是以最沒有干擾、最便宜的方式符合需求。</span><span class="sxs-lookup"><span data-stu-id="7bc10-107">The goal is to meet the requirements in the least disruptive or expensive way.</span></span> 

<span data-ttu-id="7bc10-108">移動服務會花費最少的 CPU 時間和網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="7bc10-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="7bc10-109">對於具狀態服務，需要複製這些服務的狀態、耗用額外記憶體和磁碟。</span><span class="sxs-lookup"><span data-stu-id="7bc10-109">For stateful services, it requires copying the state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="7bc10-110">將 Azure Service Fabric 叢集資源管理員帶來的解決方案成本降至最低，有助於確保不會花費不必要的叢集資源。</span><span class="sxs-lookup"><span data-stu-id="7bc10-110">Minimizing the cost of solutions that the Azure Service Fabric Cluster Resource Manager comes up with helps ensure that the cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="7bc10-111">然而，也不想忽略可大幅改善叢集中資源配置的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7bc10-111">However, you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span></span>

<span data-ttu-id="7bc10-112">「叢集資源管理員」有兩種計算及限制成本的方式，在它嘗試管理叢集時亦是如此。</span><span class="sxs-lookup"><span data-stu-id="7bc10-112">The Cluster Resource Manager has two ways of computing costs and limiting them while it tries to manage the cluster.</span></span> <span data-ttu-id="7bc10-113">第一種機制只會計算進行的每次移動。</span><span class="sxs-lookup"><span data-stu-id="7bc10-113">The first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="7bc10-114">如果產生兩個平衡值 (分數) 幾乎相同的解決方案，「叢集資源管理員」就會採用成本最低 (移動總數) 的那一個。</span><span class="sxs-lookup"><span data-stu-id="7bc10-114">If two solutions are generated with about the same balance (score), then the Cluster Resource Manager prefers the one with the lowest cost (total number of moves).</span></span>

<span data-ttu-id="7bc10-115">此策略效果不錯。</span><span class="sxs-lookup"><span data-stu-id="7bc10-115">This strategy works well.</span></span> <span data-ttu-id="7bc10-116">但是若使用預設或靜態負載時，不太可能在任何複雜的系統中所有的移動都相等。</span><span class="sxs-lookup"><span data-stu-id="7bc10-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="7bc10-117">有些可能會昂貴許多。</span><span class="sxs-lookup"><span data-stu-id="7bc10-117">Some are likely to be much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="7bc10-118">設定移動成本</span><span class="sxs-lookup"><span data-stu-id="7bc10-118">Setting Move Costs</span></span> 
<span data-ttu-id="7bc10-119">您可以在服務建立時指定其預設移動成本：</span><span class="sxs-lookup"><span data-stu-id="7bc10-119">You can specify the default move cost for a service when it is created:</span></span>

<span data-ttu-id="7bc10-120">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="7bc10-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="7bc10-121">C#：</span><span class="sxs-lookup"><span data-stu-id="7bc10-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up the rest of the ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="7bc10-122">您也可以在服務建立之後，指定其移動成本或動態更新 MoveCost：</span><span class="sxs-lookup"><span data-stu-id="7bc10-122">You can also specify or update MoveCost dynamically for a service after the service has been created:</span></span> 

<span data-ttu-id="7bc10-123">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="7bc10-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="7bc10-124">C#：</span><span class="sxs-lookup"><span data-stu-id="7bc10-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="7bc10-125">以動態方式指定每個複本的移動成本</span><span class="sxs-lookup"><span data-stu-id="7bc10-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="7bc10-126">上述程式碼片段可以從服務本身外部一次指定整個服務的 MoveCost。</span><span class="sxs-lookup"><span data-stu-id="7bc10-126">The preceding snippets are all for specifying MoveCost for a whole service at once from outside the service itself.</span></span> <span data-ttu-id="7bc10-127">不過，當特定服務物件的移動成本隨著其生命週期變更時，移動成本最有用。</span><span class="sxs-lookup"><span data-stu-id="7bc10-127">However, move cost is most useful is when the move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="7bc10-128">因為服務本身可能有在指定時間移動需要多少成本的最佳想法，所以有一個適用於服務的 API 可以報告執行階段期間的個別移動成本。</span><span class="sxs-lookup"><span data-stu-id="7bc10-128">Since the services themselves probably have the best idea of how costly they are to move a given time, there's an API for services to report their own individual move cost during runtime.</span></span> 

<span data-ttu-id="7bc10-129">C#：</span><span class="sxs-lookup"><span data-stu-id="7bc10-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="7bc10-130">移動成本的影響</span><span class="sxs-lookup"><span data-stu-id="7bc10-130">Impact of move cost</span></span>
<span data-ttu-id="7bc10-131">MoveCost 有四個層級：零、低、中和高。</span><span class="sxs-lookup"><span data-stu-id="7bc10-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="7bc10-132">除了零之外，MoveCosts 彼此具有相對性。</span><span class="sxs-lookup"><span data-stu-id="7bc10-132">MoveCosts are relative to each other, except for Zero.</span></span> <span data-ttu-id="7bc10-133">零移動成本表示移動是免費的，因此不應計入解決方案的分數。</span><span class="sxs-lookup"><span data-stu-id="7bc10-133">Zero move cost means that movement is free and should not count against the score of the solution.</span></span> <span data-ttu-id="7bc10-134">將移動成本設定為 [高]，並「不」保證複本會待在一個地方。</span><span class="sxs-lookup"><span data-stu-id="7bc10-134">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span></span>

<span data-ttu-id="7bc10-135"><center>
![移動成本作為選取要移動之複本的因素][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="7bc10-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="7bc10-136">MoveCost 可協助您在達成對等的平衡時，尋找整體導致最少中斷且最容易達成的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7bc10-136">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="7bc10-137">服務的成本概念可相對於許多事項。</span><span class="sxs-lookup"><span data-stu-id="7bc10-137">A service’s notion of cost can be relative to many things.</span></span> <span data-ttu-id="7bc10-138">計算您的移動成本時最常見的因素為：</span><span class="sxs-lookup"><span data-stu-id="7bc10-138">The most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="7bc10-139">服務必須移動的狀態或資料量。</span><span class="sxs-lookup"><span data-stu-id="7bc10-139">The amount of state or data that the service has to move.</span></span>
- <span data-ttu-id="7bc10-140">用戶端中斷連線的成本。</span><span class="sxs-lookup"><span data-stu-id="7bc10-140">The cost of disconnection of clients.</span></span> <span data-ttu-id="7bc10-141">移動主要複本的成本通常高於移動次要複本的成本。</span><span class="sxs-lookup"><span data-stu-id="7bc10-141">Moving a primary replica is usually more costly than the cost of moving a secondary replica.</span></span>
- <span data-ttu-id="7bc10-142">中斷執行中作業的成本。</span><span class="sxs-lookup"><span data-stu-id="7bc10-142">The cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="7bc10-143">某些資料存放區層級的作業，或是執行以回應用戶端呼叫的作業，它們的成本都很高。</span><span class="sxs-lookup"><span data-stu-id="7bc10-143">Some operations at the data store level or operations performed in response to a client call are costly.</span></span> <span data-ttu-id="7bc10-144">在某個特定點之後，除非必要否則您不會想要停止它們。</span><span class="sxs-lookup"><span data-stu-id="7bc10-144">After a certain point, you don’t want to stop them if you don’t have to.</span></span> <span data-ttu-id="7bc10-145">因此，在作業持續期間，您可以提高此服務物件的移動成本以降低其移動的可能性。</span><span class="sxs-lookup"><span data-stu-id="7bc10-145">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span></span> <span data-ttu-id="7bc10-146">當作業完成之後，您可以將成本設定回正常。</span><span class="sxs-lookup"><span data-stu-id="7bc10-146">When the operation is done, you set the cost back to normal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="7bc10-147">在您的叢集中啟用移動成本</span><span class="sxs-lookup"><span data-stu-id="7bc10-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="7bc10-148">為了將更細微的 MoveCosts 納入考量，必須在叢集中啟用 MoveCost。</span><span class="sxs-lookup"><span data-stu-id="7bc10-148">In order for the more granular MoveCosts to be taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="7bc10-149">如果沒有此設定，則會使用計算移動的預設模式來計算 MoveCost，並且忽略 MoveCost 報告。</span><span class="sxs-lookup"><span data-stu-id="7bc10-149">Without this setting, the default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="7bc10-150">ClusterManifest.xml：</span><span class="sxs-lookup"><span data-stu-id="7bc10-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="7bc10-151">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="7bc10-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7bc10-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7bc10-152">Next steps</span></span>
- <span data-ttu-id="7bc10-153">Service Fabric 叢集資源管理員會使用度量來管理叢集中的耗用量和容量。</span><span class="sxs-lookup"><span data-stu-id="7bc10-153">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span></span> <span data-ttu-id="7bc10-154">若要深入了解度量及設定度量的方式，請參閱 [在 Service Fabric 中使用度量管理資源耗用量和負載](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="7bc10-154">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="7bc10-155">若要深入了解叢集資源管理員如何在叢集中進行管理和負載平衡，請查看 [平衡 Service Fabric 叢集](service-fabric-cluster-resource-manager-balancing.md)。</span><span class="sxs-lookup"><span data-stu-id="7bc10-155">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
