---
title: "Service Fabric 叢集 Resource Manager 中的節流 | Microsoft Docs"
description: "了解如何設定 Service Fabric 叢集 Resource Manager 提供的節流。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 1be0beaf2e199a9c384187efd80b33c7dab5e87c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="throttling-the-service-fabric-cluster-resource-manager"></a><span data-ttu-id="3d1d8-103">對 Service Fabric 叢集資源管理員進行節流</span><span class="sxs-lookup"><span data-stu-id="3d1d8-103">Throttling the Service Fabric Cluster Resource Manager</span></span>
<span data-ttu-id="3d1d8-104">即使您已經正確設定叢集資源管理員，也可以中斷叢集。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-104">Even if you’ve configured the Cluster Resource Manager correctly, the cluster can get disrupted.</span></span> <span data-ttu-id="3d1d8-105">例如，叢集可能會同時發生節點和容錯網域失敗，如果這些失敗是在升級時發生會造成什麼後果？</span><span class="sxs-lookup"><span data-stu-id="3d1d8-105">For example, there could be simultaneous node and fault domain failures - what would happen if that occurred during an upgrade?</span></span> <span data-ttu-id="3d1d8-106">叢集資源管理員會不斷嘗試讓一切恢復正常，耗用叢集的資源來試著重新組織並修正叢集。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-106">The Cluster Resource Manager always tries to fix everything, consuming the cluster's resources trying to reorganize and fix the cluster.</span></span> <span data-ttu-id="3d1d8-107">節流有助於提供最後防線，讓叢集利用資源來穩定系統，也就是讓節點恢復運作、修復網路磁碟分割，以及部署經過修正的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-107">Throttles help provide a backstop so that the cluster can use resources to stabilize - the nodes come back, the network partitions heal, corrected bits get deployed.</span></span>

<span data-ttu-id="3d1d8-108">為了協助達成這幾種情況，Service Fabric 叢集資源管理員包含幾種節流。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-108">To help with these sorts of situations, the Service Fabric Cluster Resource Manager includes several throttles.</span></span> <span data-ttu-id="3d1d8-109">這些節流功能個個都是強大無比的工具。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-109">These throttles are all fairly large hammers.</span></span> <span data-ttu-id="3d1d8-110">一般來說，如果您沒有仔細規劃並測試，就請不要對其進行變更。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-110">Generally they shouldn’t be changed without careful planning and testing.</span></span>

<span data-ttu-id="3d1d8-111">如果您變更叢集資源管理員的節流功能，請針對您預期的實際負載來調整它們。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-111">If you change the Cluster Resource Manager's throttles, you should tune them to your expected actual load.</span></span> <span data-ttu-id="3d1d8-112">您可能會認定，即使使用節流會在某些情況下導致叢集需要更長的時間才能穩定下來，但您還是需要備有節流功能。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-112">You may determine you need to have some throttles in place, even if it means the cluster takes longer to stabilize in some situations.</span></span> <span data-ttu-id="3d1d8-113">您必須進行測試才能決定正確的節流值。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-113">Testing is required to determine the correct values for throttles.</span></span> <span data-ttu-id="3d1d8-114">節流值必須夠高，才能讓叢集在合理的時間內對變更做出回應，但也要夠低，才能真正避免過度耗用資源。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-114">Throttles need to be high enough to allow the cluster to respond to changes in a reasonable amount of time, and low enough to actually prevent too much resource consumption.</span></span> 

<span data-ttu-id="3d1d8-115">由於客戶環境中的資源已經有限，因此我們發現他們大多會實施節流措施。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-115">Most of the time we’ve seen customers use throttles it has been because they were already in a resource constrained environment.</span></span> <span data-ttu-id="3d1d8-116">例如，限制個別節點的網路頻寬，或由於輸送量有限而不讓磁碟同時建置許多具狀態複本。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-116">Some examples would be limited network bandwidth for individual nodes, or disks that aren't able to build many stateful replicas in parallel due to throughput limitations.</span></span> <span data-ttu-id="3d1d8-117">若不實施節流措施，將會有大量作業爭用這些資源，從而導致作業失敗或速度變慢。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-117">Without throttles, operations could overwhelm these resources, causing operations to fail or be slow.</span></span> <span data-ttu-id="3d1d8-118">有鑑於此，客戶被迫實施了節流措施，卻也知道叢集需要更久的時間才能達到穩定狀態。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-118">In these situations customers used throttles and knew they were extending the amount of time it would take the cluster to reach a stable state.</span></span> <span data-ttu-id="3d1d8-119">客戶也了解進行節流時，最後可能會在整體可靠性降低的情況下運作。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-119">Customers also understood they could end up running at lower overall reliability while they were throttled.</span></span>


## <a name="configuring-the-throttles"></a><span data-ttu-id="3d1d8-120">設定節流</span><span class="sxs-lookup"><span data-stu-id="3d1d8-120">Configuring the throttles</span></span>

<span data-ttu-id="3d1d8-121">Service Fabric 有兩種機制可供節制移動的複本數目。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-121">Service Fabric has two mechanisms for throttling the number of replica movements.</span></span> <span data-ttu-id="3d1d8-122">Service Fabric 5.7 之前就存在的預設機制是以允許移動的數量固定不變的方式來進行節流。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-122">The default mechanism that existed before Service Fabric 5.7 represents throttling as an absolute number of moves allowed.</span></span> <span data-ttu-id="3d1d8-123">但這種方式不適用於所有規模的叢集。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-123">This does not work for clusters of all sizes.</span></span> <span data-ttu-id="3d1d8-124">對於大型叢集來說尤其如此，這種機制的預設值可能會太小，而導致即使這樣的值有其必要的情況下大幅降低平衡速度，然而這種機制對於較小的叢集來說卻沒有效果。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-124">In particular, for large clusters the default value can be too small, significantly slowing down balancing even when it is necessary, while having no effect in smaller clusters.</span></span> <span data-ttu-id="3d1d8-125">這個舊機制已由百分比式的節流所取代，後者對於服務和節點數目經常變更的動態叢集會有較好的調整效果。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-125">This prior mechanism has been superseded by percentage-based throttling, which scales better with dynamic clusters in which the number of services and nodes change regularly.</span></span>

<span data-ttu-id="3d1d8-126">這些節流值是以叢集中複本數目的百分比作為根據。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-126">The throttles are based on a percentage of the number of replicas in the clusters.</span></span> <span data-ttu-id="3d1d8-127">百分比式的節流能夠表達這樣的規則：「不要在為期 10 分鐘的間隔內移動超過 10% 的複本」(舉例)。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-127">Percetage based throttles enable expressing the rule: "do not move more than 10% of replicas in a 10 minute interval", for example.</span></span>

<span data-ttu-id="3d1d8-128">百分比式節流的組態設定如下：</span><span class="sxs-lookup"><span data-stu-id="3d1d8-128">The configuration settings for percentage-based throttling are:</span></span>

  - <span data-ttu-id="3d1d8-129">GlobalMovementThrottleThresholdPercentage - 叢集中隨時允許移動的數目上限，以「叢集中複本總數的百分比」來表示。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-129">GlobalMovementThrottleThresholdPercentage - Maximum number of movements allowed in cluster at any time, expressed as percentage of total number of replicas in the cluster.</span></span> <span data-ttu-id="3d1d8-130">0 表示沒有限制。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-130">0 indicates no limit.</span></span> <span data-ttu-id="3d1d8-131">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-131">The default value is 0.</span></span> <span data-ttu-id="3d1d8-132">如果您同時指定此設定和 GlobalMovementThrottleThreshold，則系統會使用更保守的限制。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-132">If both this setting and GlobalMovementThrottleThreshold are specified, then the more conservative limit is used.</span></span>
  - <span data-ttu-id="3d1d8-133">GlobalMovementThrottleThresholdPercentageForPlacement - 放置階段允許移動的數目上限，以「叢集中複本總數的百分比」來表示。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-133">GlobalMovementThrottleThresholdPercentageForPlacement - Maximum number of movements allowed during the placement phase, expressed as percentage of total number of replicas in the cluster.</span></span> <span data-ttu-id="3d1d8-134">0 表示沒有限制。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-134">0 indicates no limit.</span></span> <span data-ttu-id="3d1d8-135">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-135">The default value is 0.</span></span> <span data-ttu-id="3d1d8-136">如果您同時指定此設定和 GlobalMovementThrottleThresholdForPlacement，則系統會使用更保守的限制。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-136">If both this setting and GlobalMovementThrottleThresholdForPlacement are specified, then the more conservative limit is used.</span></span>
  - <span data-ttu-id="3d1d8-137">GlobalMovementThrottleThresholdPercentageForBalancing - 平衡階段允許移動的數目上限，以「叢集中複本總數的百分比」來表示。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-137">GlobalMovementThrottleThresholdPercentageForBalancing - Maximum number of movements allowed during the balancing phase, expressed as percentage of total number of replicas in the cluster.</span></span> <span data-ttu-id="3d1d8-138">0 表示沒有限制。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-138">0 indicates no limit.</span></span> <span data-ttu-id="3d1d8-139">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-139">The default value is 0.</span></span> <span data-ttu-id="3d1d8-140">如果您同時指定此設定和 GlobalMovementThrottleThresholdForBalancing，則系統會使用更保守的限制。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-140">If both this setting and GlobalMovementThrottleThresholdForBalancing are specified, then the more conservative limit is used.</span></span>

<span data-ttu-id="3d1d8-141">在指定節流百分比時，請以 0.05 來指定 5%。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-141">When specifying the throttle percentage, you'd specify 5% as 0.05.</span></span> <span data-ttu-id="3d1d8-142">用來控管這些節流的間隔是 GlobalMovementThrottleCountingInterval，此設定是以秒為單位來指定。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-142">The interval on which these throttles are governed is the GlobalMovementThrottleCountingInterval, which is specified in seconds.</span></span>


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

<span data-ttu-id="3d1d8-143">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="3d1d8-143">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a><span data-ttu-id="3d1d8-144">預設計數型節流</span><span class="sxs-lookup"><span data-stu-id="3d1d8-144">Default count based throttles</span></span>
<span data-ttu-id="3d1d8-145">我們提供了這項資訊，以免您還有較舊的叢集或是仍在已升級的叢集中保有這些組態。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-145">This information is provided in case you have older clusters or still retain these configurations in clusters that have since been upgraded.</span></span> <span data-ttu-id="3d1d8-146">一般情況下，建議您使用上述的百分比式節流來取代這些節流。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-146">In general, it is recommended that these are replaced with the percentage-based throttles above.</span></span> <span data-ttu-id="3d1d8-147">百分比式節流依預設會停用，因此這些節流仍舊會是叢集的預設節流，除非您將它們停用，並以百分比式的節流來加以取代。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-147">Since percentage-based throttling is disabled by default, these throttles remain the default throttles for a cluster until they are disabled and replaced with the percentage-based throttles.</span></span> 

  - <span data-ttu-id="3d1d8-148">GlobalMovementThrottleThreshold – 這項設定會控制叢集在一段時間內的移動總數。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-148">GlobalMovementThrottleThreshold – this setting controls the total number of movements in the cluster over some time.</span></span> <span data-ttu-id="3d1d8-149">這段時間的長度會以 GlobalMovementThrottleCountingInterval 來指定，單位為秒。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-149">The amount of time is specified in seconds as the GlobalMovementThrottleCountingInterval.</span></span> <span data-ttu-id="3d1d8-150">GlobalMovementThrottleThreshold 的預設值為 1000，GlobalMovementThrottleCountingInterval 的預設值則為 600。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-150">The default value for the GlobalMovementThrottleThreshold is 1000 and the default value for the GlobalMovementThrottleCountingInterval is 600.</span></span>
  - <span data-ttu-id="3d1d8-151">MovementPerPartitionThrottleThreshold – 這項設定會控制任何服務分割區在一段時間內的移動總數。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-151">MovementPerPartitionThrottleThreshold – this setting controls the total number of movements for any service partition over some time.</span></span> <span data-ttu-id="3d1d8-152">這段時間的長度會以 MovementPerPartitionThrottleCountingInterval 來指定，單位為秒。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-152">The amount of time is specified in seconds as the MovementPerPartitionThrottleCountingInterval.</span></span> <span data-ttu-id="3d1d8-153">MovementPerPartitionThrottleThreshold 的預設值為 50，MovementPerPartitionThrottleCountingInterval 的預設值則為 600。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-153">The default value for the MovementPerPartitionThrottleThreshold is 50 and the default value for the MovementPerPartitionThrottleCountingInterval is 600.</span></span>

<span data-ttu-id="3d1d8-154">這些節流的組態會遵循和百分比式節流相同的模式。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-154">The configuration for these throttles follows the same pattern as the percentage-based throttling.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d1d8-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d1d8-155">Next steps</span></span>
- <span data-ttu-id="3d1d8-156">若要了解叢集資源管理員如何管理並平衡叢集中的負載，請查看關於 [平衡負載](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="3d1d8-156">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="3d1d8-157">叢集資源管理員有許多描述叢集的選項。</span><span class="sxs-lookup"><span data-stu-id="3d1d8-157">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="3d1d8-158">若要深入了解這些選項，請參閱關於[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)一文</span><span class="sxs-lookup"><span data-stu-id="3d1d8-158">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
