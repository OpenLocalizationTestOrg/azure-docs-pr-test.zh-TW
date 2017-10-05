---
title: "Service Fabric 叢集 Resource Manager - 管理整合 | Microsoft Docs"
description: "叢集資源管理員和 Service Fabric 管理之間的整合點概觀。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9601e758e1033b4e2f86c2c230d4f49479fe6f45
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a><span data-ttu-id="8d755-103">叢集資源管理員與 Service Fabric 叢集管理整合</span><span class="sxs-lookup"><span data-stu-id="8d755-103">Cluster resource manager integration with Service Fabric cluster management</span></span>
<span data-ttu-id="8d755-104">Service Fabric 叢集資源管理員不會促使 Service Fabric 升級，但有所關聯。</span><span class="sxs-lookup"><span data-stu-id="8d755-104">The Service Fabric Cluster Resource Manager doesn't drive upgrades in Service Fabric, but it is involved.</span></span> <span data-ttu-id="8d755-105">叢集資源管理員協助管理的第一種方法是追蹤所需的叢集狀態及其內部的服務。</span><span class="sxs-lookup"><span data-stu-id="8d755-105">The first way that the Cluster Resource Manager helps with management is by tracking the desired state of the cluster and the services inside it.</span></span> <span data-ttu-id="8d755-106">當叢集資源管理員無法讓叢集處於所需的設定時，它會送出健全狀況報告。</span><span class="sxs-lookup"><span data-stu-id="8d755-106">The Cluster Resource Manager sends out health reports when it cannot put the cluster into the desired configuration.</span></span> <span data-ttu-id="8d755-107">例如，如果容量不足，叢集資源管理員會發出健康情況警告和錯誤，指出問題所在。</span><span class="sxs-lookup"><span data-stu-id="8d755-107">For example, if there is insufficient capacity the Cluster Resource Manager sends out health warnings and errors indicating the problem.</span></span> <span data-ttu-id="8d755-108">整合的另一方面必定與升級方式有關。</span><span class="sxs-lookup"><span data-stu-id="8d755-108">Another piece of integration has to do with how upgrades work.</span></span> <span data-ttu-id="8d755-109">在升級期間，叢集資源管理員會稍微改變其行為。</span><span class="sxs-lookup"><span data-stu-id="8d755-109">The Cluster Resource Manager alters its behavior slightly during upgrades.</span></span>  

## <a name="health-integration"></a><span data-ttu-id="8d755-110">健康狀態整合</span><span class="sxs-lookup"><span data-stu-id="8d755-110">Health integration</span></span>
<span data-ttu-id="8d755-111">叢集資源管理員會持續追蹤您為服務定義的規則。</span><span class="sxs-lookup"><span data-stu-id="8d755-111">The Cluster Resource Manager constantly tracks the rules you have defined for placing your services.</span></span> <span data-ttu-id="8d755-112">對於節點上和叢集中的每個計量，以及整個叢集中的每個計量，其也會追蹤剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="8d755-112">It also tracks the remaining capacity for each metric on the nodes and in the cluster and in the cluster as a whole.</span></span> <span data-ttu-id="8d755-113">如果無法滿足這些規則，或容量不足，則會發出健康情況警告和錯誤。</span><span class="sxs-lookup"><span data-stu-id="8d755-113">If it can't satisfy those rules or if there is insufficient capacity, health warnings and errors are emitted.</span></span> <span data-ttu-id="8d755-114">例如，若節點超出容量，叢集資源管理員會移動服務來嘗試解決情況。</span><span class="sxs-lookup"><span data-stu-id="8d755-114">For example, if a node is over capacity and the Cluster Resource Manager will try to fix the situation by moving services.</span></span> <span data-ttu-id="8d755-115">如果無法解決情況，則會發出健全狀況警告，指出哪一個節點超出容量和涉及哪些計量。</span><span class="sxs-lookup"><span data-stu-id="8d755-115">If it can't correct the situation it emits a health warning indicating which node is over capacity, and for which metrics.</span></span>

<span data-ttu-id="8d755-116">Resource Manager 健全狀況警告的另一個例子是違反放置條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-116">Another example of the Resource Manager's health warnings is violations of placement constraints.</span></span> <span data-ttu-id="8d755-117">例如，若您已定義放置條件約束 (例如 `“NodeColor == Blue”`)，而資源管理員偵測到該條件約束的違規情形時，會發出健康情況警告。</span><span class="sxs-lookup"><span data-stu-id="8d755-117">For example, if you have defined a placement constraint (such as `“NodeColor == Blue”`) and the Resource Manager detects a violation of that constraint, it emits a health warning.</span></span> <span data-ttu-id="8d755-118">這適用於自訂條件約束和預設條件約束 (例如容錯網域和升級網域條件約束)。</span><span class="sxs-lookup"><span data-stu-id="8d755-118">This is true for custom constraints and the default constraints (like the Fault Domain and Upgrade Domain constraints).</span></span>

<span data-ttu-id="8d755-119">以下是這類健康狀態報告的範例。</span><span class="sxs-lookup"><span data-stu-id="8d755-119">Here’s an example of one such health report.</span></span> <span data-ttu-id="8d755-120">在此情況下，健全狀況報告是針對系統服務的其中一個資料分割。</span><span class="sxs-lookup"><span data-stu-id="8d755-120">In this case, the health report is for one of the system service’s partitions.</span></span> <span data-ttu-id="8d755-121">健全狀況訊息指出該資料分割的複本暫時封裝至太少的升級網域。</span><span class="sxs-lookup"><span data-stu-id="8d755-121">The health message indicates the replicas of that partition are temporarily packed into too few Upgrade Domains.</span></span>

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating the Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="8d755-122">以下是此健康狀態訊息要告訴我們的事情︰</span><span class="sxs-lookup"><span data-stu-id="8d755-122">Here's what this health message is telling us is:</span></span>

1. <span data-ttu-id="8d755-123">所有複本本身均狀況良好：每個都有 AggregatedHealthState : Ok</span><span class="sxs-lookup"><span data-stu-id="8d755-123">All the replicas themselves are healthy: Each has AggregatedHealthState : Ok</span></span>
2. <span data-ttu-id="8d755-124">目前違反升級網域發佈條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-124">The Upgrade Domain distribution constraint is currently being violated.</span></span> <span data-ttu-id="8d755-125">這表示特定升級網域擁有這個磁碟的過多分割複本。</span><span class="sxs-lookup"><span data-stu-id="8d755-125">This means a particular Upgrade Domain has more replicas from this partition than it should.</span></span>
3. <span data-ttu-id="8d755-126">哪個節點包含造成違規的複本。</span><span class="sxs-lookup"><span data-stu-id="8d755-126">Which node contains the replica causing the violation.</span></span> <span data-ttu-id="8d755-127">在此案例中是名為「Node.8」的節點。</span><span class="sxs-lookup"><span data-stu-id="8d755-127">In this case it's the node with the name "Node.8"</span></span>
4. <span data-ttu-id="8d755-128">無論此分割區是否正在升級 (「Currently Upgrading -- false」)</span><span class="sxs-lookup"><span data-stu-id="8d755-128">Whether an upgrade is currently happening for this partition ("Currently Upgrading -- false")</span></span>
5. <span data-ttu-id="8d755-129">此服務的發佈原則：「Distribution Policy -- Packing」。</span><span class="sxs-lookup"><span data-stu-id="8d755-129">The distribution policy for this service: "Distribution Policy -- Packing".</span></span> <span data-ttu-id="8d755-130">這是由`RequireDomainDistribution`[放置原則](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing)控管。</span><span class="sxs-lookup"><span data-stu-id="8d755-130">This is governed by the `RequireDomainDistribution` [placement policy](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing).</span></span> <span data-ttu-id="8d755-131">「封裝」表示在此情況下_不_需要 DomainDistribution，因此可知道並未替該服務指定放置原則。</span><span class="sxs-lookup"><span data-stu-id="8d755-131">"Packing" indicates that in this case DomainDistribution was _not_ required, so we know that placement policy was not specified for this service.</span></span> 
6. <span data-ttu-id="8d755-132">報告時間 - 2015 年 8 月 10 日下午 7:13:02</span><span class="sxs-lookup"><span data-stu-id="8d755-132">When the report happened - 8/10/2015 7:13:02 PM</span></span>

<span data-ttu-id="8d755-133">這種資訊會引出在生產環境中出現的警示，讓您知道已發生問題，也會用來偵測和停止不正確的升級。</span><span class="sxs-lookup"><span data-stu-id="8d755-133">Information like this powers alerts that fire in production to let you know something has gone wrong and is also used to detect and halt bad upgrades.</span></span> <span data-ttu-id="8d755-134">在此情況下，我們需要查明 Resource Manager 為何一定要將複本封裝至升級網域。</span><span class="sxs-lookup"><span data-stu-id="8d755-134">In this case, we’d want to see if we can figure out why the Resource Manager had to pack the replicas into the Upgrade Domain.</span></span> <span data-ttu-id="8d755-135">例如，封裝是暫時性的，因為其他升級網域中的節點已關閉。</span><span class="sxs-lookup"><span data-stu-id="8d755-135">Usually packing is transient because the nodes in the other Upgrade Domains were down, for example.</span></span>

<span data-ttu-id="8d755-136">假設叢集資源管理員嘗試放置某些服務，但沒有任何可行的解決方案。</span><span class="sxs-lookup"><span data-stu-id="8d755-136">Let’s say the Cluster Resource Manager is trying to place some services, but there aren't any solutions that work.</span></span> <span data-ttu-id="8d755-137">無法放置服務時，通常是下列其中一個原因所致：</span><span class="sxs-lookup"><span data-stu-id="8d755-137">When services can't be placed, it is usually for one of the following reasons:</span></span>

1. <span data-ttu-id="8d755-138">某個暫時性情況導致無法正確地放置此服務執行個體或複本</span><span class="sxs-lookup"><span data-stu-id="8d755-138">Some transient condition has made it impossible to place this service instance or replica correctly</span></span>
2. <span data-ttu-id="8d755-139">未滿足服務的放置需求。</span><span class="sxs-lookup"><span data-stu-id="8d755-139">The service’s placement requirements are unsatisfiable.</span></span>

<span data-ttu-id="8d755-140">在這些案例中，叢集資源管理員的健康情況報告有助於判斷為什麼無法放置服務。</span><span class="sxs-lookup"><span data-stu-id="8d755-140">In these cases, health reports from the Cluster Resource Manager help you determine why the service can’t be placed.</span></span> <span data-ttu-id="8d755-141">我們將此程序稱為「條件約束消除序列」。</span><span class="sxs-lookup"><span data-stu-id="8d755-141">We call this process the constraint elimination sequence.</span></span> <span data-ttu-id="8d755-142">在此期間，系統會逐步解說會影響服務與記錄的已設定條件約束，以及它們所消除的項目。</span><span class="sxs-lookup"><span data-stu-id="8d755-142">During it, the system walks through the configured constraints affecting the service and records what they eliminate.</span></span> <span data-ttu-id="8d755-143">如此一來，當項目無法放置時，您可以看到哪些節點已經消除及消除原因。</span><span class="sxs-lookup"><span data-stu-id="8d755-143">This way when services aren’t able to be placed, you can see which nodes were eliminated and why.</span></span>

## <a name="constraint-types"></a><span data-ttu-id="8d755-144">條件約束類型</span><span class="sxs-lookup"><span data-stu-id="8d755-144">Constraint types</span></span>
<span data-ttu-id="8d755-145">讓我們討論這些健康情況報告中每個不同的條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-145">Let’s talk about each of the different constraints in these health reports.</span></span> <span data-ttu-id="8d755-146">無法放置複本時，會看到與這些條件約束有關的健康情況訊息。</span><span class="sxs-lookup"><span data-stu-id="8d755-146">You will see health messages related to these constraints when replicas can't be placed.</span></span>

* <span data-ttu-id="8d755-147">**ReplicaExclusionStatic** 和 **ReplicaExclusionDynamic**：這些條件約束指出解決方案遭拒，因為來自相同分割區的兩個服務物件必須放置在相同節點上。</span><span class="sxs-lookup"><span data-stu-id="8d755-147">**ReplicaExclusionStatic** and **ReplicaExclusionDynamic**: These constraints indicates that a solution was rejected because two service objects from the same partition would have to be placed on the same node.</span></span> <span data-ttu-id="8d755-148">不允許這麼做是因為該節點的失敗會過度影響該分割區。</span><span class="sxs-lookup"><span data-stu-id="8d755-148">This isn’t allowed because then failure of that node would overly impact that partition.</span></span> <span data-ttu-id="8d755-149">ReplicaExclusionStatic 和 ReplicaExclusionDynamic 幾乎是完全相同的規則，兩者之間的差異並無太大影響。</span><span class="sxs-lookup"><span data-stu-id="8d755-149">ReplicaExclusionStatic and ReplicaExclusionDynamic are almost the same rule and the differences don't really matter.</span></span> <span data-ttu-id="8d755-150">如果您看到的條件約束消除序列包含 ReplicaExclusionStatic 或 ReplicaExclusionDynamic 條件約束，則是叢集資源管理員認為節點不足。</span><span class="sxs-lookup"><span data-stu-id="8d755-150">If you are seeing a constraint elimination sequence containing either the ReplicaExclusionStatic or ReplicaExclusionDynamic constraint, the Cluster Resource Manager thinks that there aren’t enough nodes.</span></span> <span data-ttu-id="8d755-151">這需要其他解決方案使用這些不被允許的無效位置。</span><span class="sxs-lookup"><span data-stu-id="8d755-151">This requires remaining solutions to use these invalid placements which are disallowed.</span></span> <span data-ttu-id="8d755-152">序列中的其他條件約束通常會告訴我們為什麼要先消除節點。</span><span class="sxs-lookup"><span data-stu-id="8d755-152">The other constraints in the sequence will usually tell us why nodes are being eliminated in the first place.</span></span>
* <span data-ttu-id="8d755-153">**PlacementConstraint**︰如果您看到此訊息，就表示我們已消除一些節點，因為它們不符合服務的放置條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-153">**PlacementConstraint**: If you see this message, it means that we eliminated some nodes because they didn’t match the service’s placement constraints.</span></span> <span data-ttu-id="8d755-154">我們會在此此訊息中描繪出目前所設定的放置條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-154">We trace out the currently configured placement constraints as a part of this message.</span></span> <span data-ttu-id="8d755-155">如果您已定義放置條件約束，則這是正常情形。</span><span class="sxs-lookup"><span data-stu-id="8d755-155">This is normal if you have a placement constraint defined.</span></span> <span data-ttu-id="8d755-156">不過，如果放置條件約束錯誤，而造成過多節點遭消除，您就應該注意。</span><span class="sxs-lookup"><span data-stu-id="8d755-156">However, if placement constraint is incorrectly causing too many nodes to be eliminated this is how you would notice.</span></span>
* <span data-ttu-id="8d755-157">**NodeCapacity**︰這個條件約束表示叢集資源管理員無法將複本放在指出的節點上，因為這樣會導致這些節點超出容量。</span><span class="sxs-lookup"><span data-stu-id="8d755-157">**NodeCapacity**: This constraint means that the Cluster Resource Manager couldn’t place the replicas on the indicated nodes because that would put them over capacity.</span></span>
* <span data-ttu-id="8d755-158">**Affinity**︰這個條件約束表示我們無法將複本放在受影響的節點上，因為這會導致違反同質性條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-158">**Affinity**: This constraint indicates that we couldn’t place the replica on the affected nodes since it would cause a violation of the affinity constraint.</span></span> <span data-ttu-id="8d755-159">如需同質性的詳細資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)</span><span class="sxs-lookup"><span data-stu-id="8d755-159">More information on affinity is in [this article](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)</span></span>
* <span data-ttu-id="8d755-160">**FaultDomain** 和 **UpgradeDomain**︰如果將複本放在指出的節點上會導致複本封裝在特定的容錯網域或升級網域中，此條件約束就會消除節點。</span><span class="sxs-lookup"><span data-stu-id="8d755-160">**FaultDomain** and **UpgradeDomain**: This constraint eliminates nodes if placing the replica on the indicated nodes would cause packing in a particular fault or upgrade domain.</span></span> <span data-ttu-id="8d755-161">[容錯與升級網域條件約束及產生的行為](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="8d755-161">Several examples discussing this constraint are presented in the topic on [fault and upgrade domain constraints and resulting behavior](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
* <span data-ttu-id="8d755-162">**PreferredLocation**︰您通常不會看到這個條件約束導致從解決方案中移除節點，因為該條件約束預設僅限用於最佳化。</span><span class="sxs-lookup"><span data-stu-id="8d755-162">**PreferredLocation**: You shouldn’t normally see this constraint removing nodes from the solution since it runs as an optimization by default.</span></span> <span data-ttu-id="8d755-163">慣用的位置條件約束也會在升級期間出現。</span><span class="sxs-lookup"><span data-stu-id="8d755-163">The preferred location constraint is also present during upgrades.</span></span> <span data-ttu-id="8d755-164">在升級期間，它用於將服務移回它們在升級開始時所在的位置。</span><span class="sxs-lookup"><span data-stu-id="8d755-164">During upgrade it is used to move services back to where they were when the upgrade started.</span></span>

## <a name="blocklisting-nodes"></a><span data-ttu-id="8d755-165">封鎖節點</span><span class="sxs-lookup"><span data-stu-id="8d755-165">Blocklisting Nodes</span></span>
<span data-ttu-id="8d755-166">封鎖節點時，叢集資源管理員會報告另一個健康情況訊息。</span><span class="sxs-lookup"><span data-stu-id="8d755-166">Another health message the Cluster Resource Manager reports is when nodes are blocklisted.</span></span> <span data-ttu-id="8d755-167">您可以將封鎖視為自動套用的暫時性條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-167">You can think of blocklisting as a temporary constraint that is automatically applied for you.</span></span> <span data-ttu-id="8d755-168">啟動該服務類型的執行個體時，發生重複失敗的節點會遭封鎖。</span><span class="sxs-lookup"><span data-stu-id="8d755-168">Nodes get blocklisted when they experience repeated failures when launching instances of that service type.</span></span> <span data-ttu-id="8d755-169">節點是依照服務類型來封鎖。</span><span class="sxs-lookup"><span data-stu-id="8d755-169">Nodes are blocklisted on a per-service-type basis.</span></span> <span data-ttu-id="8d755-170">某個服務類型的節點可能會被封鎖，另一個服務類型的節點則未被封鎖。</span><span class="sxs-lookup"><span data-stu-id="8d755-170">A node may be blocklisted for one service type but not another.</span></span> 

<span data-ttu-id="8d755-171">通常會在開發期間發生封鎖：一些錯誤導致服務主機在啟動時當機，</span><span class="sxs-lookup"><span data-stu-id="8d755-171">You'll see blocklisting kick in often during development: some bug causes your service host to crash on startup.</span></span> <span data-ttu-id="8d755-172">Service Fabric 多次嘗試建立服務主機，但是持續失敗。</span><span class="sxs-lookup"><span data-stu-id="8d755-172">Service Fabric tries to create the service host a few times, and the failure keeps occurring.</span></span> <span data-ttu-id="8d755-173">經過多次嘗試後，節點被封鎖，而叢集資源管理員會嘗試在其他位置建立服務。</span><span class="sxs-lookup"><span data-stu-id="8d755-173">After a few attempts, the node gets blocklisted, and the Cluster Resource Manager will try to create the service elsewhere.</span></span> <span data-ttu-id="8d755-174">如果多個節點持續發生同樣的失敗，最終可能導致叢集中的所有有效節點被封鎖。</span><span class="sxs-lookup"><span data-stu-id="8d755-174">If that failure keeps happening on multiple nodes, it's possible that all of the valid nodes in the cluster end up blocked.</span></span> <span data-ttu-id="8d755-175">封鎖也會移除許多節點，導致數量不足以無法成功啟動服務來達到所需的級別。</span><span class="sxs-lookup"><span data-stu-id="8d755-175">Blocklisting cna also remove so many nodes that not enough can successfully launch the service to meet the desired scale.</span></span> <span data-ttu-id="8d755-176">您通常會看見叢集資源管理員出現其他錯誤或警告，顯示服務低於所需的複本或執行個體計數，也會看到健康情況訊息顯示出最先導致封鎖的失敗。</span><span class="sxs-lookup"><span data-stu-id="8d755-176">You'll typically see additional errors or warnings from the Cluster Resource Manager indicating that the service is below the desired replica or instance count, as well as health messages indicating what the failure is that's leading to the blocklisting in the first place.</span></span>

<span data-ttu-id="8d755-177">封鎖不是永久情況。</span><span class="sxs-lookup"><span data-stu-id="8d755-177">Blocklisting is not a permanent condition.</span></span> <span data-ttu-id="8d755-178">經過幾分鐘後，便會從封鎖清單中移除節點，且 Service Fabric 會再次啟動該節點上的服務。</span><span class="sxs-lookup"><span data-stu-id="8d755-178">After a few minutes, the node is removed from the blocklist and Service Fabric may activate the services on that node again.</span></span> <span data-ttu-id="8d755-179">如果服務持續失敗，會再次封鎖該服務類型的節點。</span><span class="sxs-lookup"><span data-stu-id="8d755-179">If services continue to fail, the node is blocklisted for that service type again.</span></span> 

### <a name="constraint-priorities"></a><span data-ttu-id="8d755-180">條件約束優先順序</span><span class="sxs-lookup"><span data-stu-id="8d755-180">Constraint priorities</span></span>

> [!WARNING]
> <span data-ttu-id="8d755-181">不建議變更條件約束優先順序，因為可能對叢集造成顯著的負面影響。</span><span class="sxs-lookup"><span data-stu-id="8d755-181">Changing constraint priorities is not recommended and may have significant adverse effects on your cluster.</span></span> <span data-ttu-id="8d755-182">下列提供預設條件約束優先順序及其行為的參考資訊。</span><span class="sxs-lookup"><span data-stu-id="8d755-182">The below information is provided for reference of the default constraint priorities and their behavior.</span></span> 
>

<span data-ttu-id="8d755-183">所有這些條件約束可能會讓您覺得：「嘿，對我的系統來說，預設網域條件約束是最重要的。</span><span class="sxs-lookup"><span data-stu-id="8d755-183">With all of these constraints, you may have been thinking “Hey – I think that fault domain constraints are the most important thing in my system.</span></span> <span data-ttu-id="8d755-184">為了確保不會違反預設網域條件約束，我願意違反其他條件約束。」</span><span class="sxs-lookup"><span data-stu-id="8d755-184">In order to ensure the fault domain constraint isn't violated, I’m willing to violate other constraints.”</span></span>

<span data-ttu-id="8d755-185">可以使用不同的優先順序等級來設定條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-185">Constraints can be configured with different priority levels.</span></span> <span data-ttu-id="8d755-186">它們是：</span><span class="sxs-lookup"><span data-stu-id="8d755-186">These are:</span></span>

   - <span data-ttu-id="8d755-187">「硬性」(0)</span><span class="sxs-lookup"><span data-stu-id="8d755-187">“hard” (0)</span></span>
   - <span data-ttu-id="8d755-188">「彈性」(1)</span><span class="sxs-lookup"><span data-stu-id="8d755-188">“soft” (1)</span></span>
   - <span data-ttu-id="8d755-189">「最佳化」(2)</span><span class="sxs-lookup"><span data-stu-id="8d755-189">“optimization” (2)</span></span>
   - <span data-ttu-id="8d755-190">「關閉」(-1)。</span><span class="sxs-lookup"><span data-stu-id="8d755-190">“off” (-1).</span></span> 
   
<span data-ttu-id="8d755-191">大部分的條件約束預設是設定為硬性條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-191">Most of the constraints are configured as hard constraints by default.</span></span>

<span data-ttu-id="8d755-192">通常不會變更條件約束的優先順序。</span><span class="sxs-lookup"><span data-stu-id="8d755-192">Changing the priority of constraints is uncommon.</span></span> <span data-ttu-id="8d755-193">有時候需要變更條件約束的優先順序，通常是為了解決影響環境的其他錯誤或行為。</span><span class="sxs-lookup"><span data-stu-id="8d755-193">There have been times where constraint priorities needed to change, usually to work around some other bug or behavior that was impacting the environment.</span></span> <span data-ttu-id="8d755-194">大致上，條件約束優先順序基礎結構的彈性可以運作的非常好，但不會經常需要用到。</span><span class="sxs-lookup"><span data-stu-id="8d755-194">Generally the flexibility of the constraint priority infrastructure has worked very well, but it isn't needed often.</span></span> <span data-ttu-id="8d755-195">在大部分情況下，一切都按照預設優先順序安排。</span><span class="sxs-lookup"><span data-stu-id="8d755-195">Most of the time everything sits at their default priorities.</span></span> 

<span data-ttu-id="8d755-196">優先順序等級不表示會_違反_指定的條件約束，也不表示會一律符合條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-196">The priority levels don't mean that a given constraint _will_ be violated, nor that it will always be met.</span></span> <span data-ttu-id="8d755-197">條件約束優先順序會定義強制執行條件約束的順序。</span><span class="sxs-lookup"><span data-stu-id="8d755-197">Constraint priorities define an order in which constraints are enforced.</span></span> <span data-ttu-id="8d755-198">無法滿足所有條件約束時，會以優先順序決定權衡取捨。</span><span class="sxs-lookup"><span data-stu-id="8d755-198">Priorities define the tradeoffs when it is impossible to satisfy all constraints.</span></span> <span data-ttu-id="8d755-199">除非環境中有其他正在進行的項目，否則通常可以滿足所有條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-199">Usually all the constraints can be satisfied unless there's something else going on in the environment.</span></span> <span data-ttu-id="8d755-200">導致違反條件約束的一些情節範例包括衝突的條件約束，或大量的並行失敗。</span><span class="sxs-lookup"><span data-stu-id="8d755-200">Some examples of scenarios that will lead to constraint violations are conflicting constraints, or large numbers of concurrent failures.</span></span>

<span data-ttu-id="8d755-201">在進階情況中，可以變更條件約束優先順序。</span><span class="sxs-lookup"><span data-stu-id="8d755-201">In advanced situations, you can change the constraint priorities.</span></span> <span data-ttu-id="8d755-202">例如，假設為了解決節點容量問題，而必須確保一律違反同質性。</span><span class="sxs-lookup"><span data-stu-id="8d755-202">For example, say you wanted to ensure that affinity would always be violated when necessary to solve node capacity issues.</span></span> <span data-ttu-id="8d755-203">為了達到此目的，您可以將同質性條件約束的優先順序設為「軟式」(1)，並將容量條件約束維持設為「硬式」(0)。</span><span class="sxs-lookup"><span data-stu-id="8d755-203">To achieve this, you could set the priority of the affinity constraint to “soft” (1) and leave the capacity constraint set to “hard” (0).</span></span>

<span data-ttu-id="8d755-204">下列組態檔中指定了不同條件約束的預設優先順序值：</span><span class="sxs-lookup"><span data-stu-id="8d755-204">The default priority values for the different constraints are specified in the following config:</span></span>

<span data-ttu-id="8d755-205">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="8d755-205">ClusterManifest.xml</span></span>

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

<span data-ttu-id="8d755-206">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="8d755-206">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a><span data-ttu-id="8d755-207">容錯網域和升級網域的條件約束</span><span class="sxs-lookup"><span data-stu-id="8d755-207">Fault domain and upgrade domain constraints</span></span>
<span data-ttu-id="8d755-208">叢集資源管理員想要保留遍佈於容錯網域和升級網域的服務。</span><span class="sxs-lookup"><span data-stu-id="8d755-208">The Cluster Resource Manager wants to keep services spread out among fault and upgrade domains.</span></span> <span data-ttu-id="8d755-209">它會將此設定為叢集資源管理員的引擎內的條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-209">It models this as a constraint inside the Cluster Resource Manager’s engine.</span></span> <span data-ttu-id="8d755-210">如需其使用方式及特定行為的詳細資訊，請參閱[叢集設定](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior)一文。</span><span class="sxs-lookup"><span data-stu-id="8d755-210">For more information on how they are used and their specific behavior, check out the article on [cluster configuration](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).</span></span>

<span data-ttu-id="8d755-211">叢集資源管理員可能需要將一些複本封裝至升級網域，以處理升級、失敗或其他條件約束違規情形。</span><span class="sxs-lookup"><span data-stu-id="8d755-211">The Cluster Resource Manager may need to pack a couple replicas into an upgrade domain in order to deal with upgrades, failures, or other constraint violations.</span></span> <span data-ttu-id="8d755-212">通常，只有當系統中發生許多失敗或其他問題，導致無法正確放置時，才會封裝到容錯網域或升級網域。</span><span class="sxs-lookup"><span data-stu-id="8d755-212">Packing into fault or upgrade domains normally happens only when there are several failures or other churn in the system preventing correct placement.</span></span> <span data-ttu-id="8d755-213">如果即使在這類情況下也想要避免進行封裝，可以利用`RequireDomainDistribution`[放置原則](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing)。</span><span class="sxs-lookup"><span data-stu-id="8d755-213">If you wish to prevent packing even during these situations, you can utilize the `RequireDomainDistribution` [placement policy](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing).</span></span> <span data-ttu-id="8d755-214">請注意，這可能會產生影響服務可用性和可靠性的副作用，請審慎考慮。</span><span class="sxs-lookup"><span data-stu-id="8d755-214">Note that this may affect service availability and reliability as a side effect, so consider it carefully.</span></span>

<span data-ttu-id="8d755-215">如果已正確設定環境，則會完全遵守所有條件約束，甚至在升級期間也是如此。</span><span class="sxs-lookup"><span data-stu-id="8d755-215">If the environment is configured correctly, all constraints are fully respected, even during upgrades.</span></span> <span data-ttu-id="8d755-216">關鍵在於叢集資源管理員會監看您的條件約束，</span><span class="sxs-lookup"><span data-stu-id="8d755-216">The key thing is that the Cluster Resource Manager is watching out for your constraints.</span></span> <span data-ttu-id="8d755-217">在偵測到違規時會立即回報，並嘗試更正問題。</span><span class="sxs-lookup"><span data-stu-id="8d755-217">When it detects a violation it immediately reports it and tries to correct the issue.</span></span>

## <a name="the-preferred-location-constraint"></a><span data-ttu-id="8d755-218">慣用的位置條件約束</span><span class="sxs-lookup"><span data-stu-id="8d755-218">The preferred location constraint</span></span>
<span data-ttu-id="8d755-219">PreferredLocation 條件約束稍有不同，因為它有兩種不同的用途。</span><span class="sxs-lookup"><span data-stu-id="8d755-219">The PreferredLocation constraint is a little different, as it has two different uses.</span></span> <span data-ttu-id="8d755-220">這個條件約束的其中一種用法是在應用程式升級期間。</span><span class="sxs-lookup"><span data-stu-id="8d755-220">One use of this constraint is during application upgrades.</span></span> <span data-ttu-id="8d755-221">叢集資源管理員會在升級期間自動管理這個條件約束，</span><span class="sxs-lookup"><span data-stu-id="8d755-221">The Cluster Resource Manager automatically manages this constraint during upgrades.</span></span> <span data-ttu-id="8d755-222">用來確定複本在升級完成時會傳回到初始位置。</span><span class="sxs-lookup"><span data-stu-id="8d755-222">It is used to ensure that when upgrades are complete that replicas return to their initial locations.</span></span> <span data-ttu-id="8d755-223">PreferredLocation 條件約束的另一種用法與[`PreferredPrimaryDomain`放置原則](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)有關。</span><span class="sxs-lookup"><span data-stu-id="8d755-223">The other use of the PreferredLocation constraint is for the [`PreferredPrimaryDomain` placement policy](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md).</span></span> <span data-ttu-id="8d755-224">兩者都屬於最佳化，因此 PreferredLocation 條件約束是唯一預設為「最佳化」的條件約束。</span><span class="sxs-lookup"><span data-stu-id="8d755-224">Both of these are optimizations, and hence the PreferredLocation constraint is the only constraint set to "Optimization" by default.</span></span>

## <a name="upgrades"></a><span data-ttu-id="8d755-225">升級</span><span class="sxs-lookup"><span data-stu-id="8d755-225">Upgrades</span></span>
<span data-ttu-id="8d755-226">在應用程式和叢集升級過程中，叢集資源管理員也有所幫助，它在這期間有兩項作業︰</span><span class="sxs-lookup"><span data-stu-id="8d755-226">The Cluster Resource Manager also helps during application and cluster upgrades, during which it has two jobs:</span></span>

* <span data-ttu-id="8d755-227">確保不影響叢集的規則</span><span class="sxs-lookup"><span data-stu-id="8d755-227">ensure that the rules of the cluster are not compromised</span></span>
* <span data-ttu-id="8d755-228">嘗試協助順利地進行升級</span><span class="sxs-lookup"><span data-stu-id="8d755-228">try to help the upgrade go smoothly</span></span>

### <a name="keep-enforcing-the-rules"></a><span data-ttu-id="8d755-229">繼續強制執行規則</span><span class="sxs-lookup"><span data-stu-id="8d755-229">Keep enforcing the rules</span></span>
<span data-ttu-id="8d755-230">規則是需要注意的重點 – 在升級期間仍會強制執行嚴格的條件約束 (如放置條件約束和容量)。</span><span class="sxs-lookup"><span data-stu-id="8d755-230">The main thing to be aware of is that the rules – the strict constraints like placement constraints and capacities - are still enforced during upgrades.</span></span> <span data-ttu-id="8d755-231">放置條件約束可確保工作負載只在允許的位置執行，即在升級期間也一樣。</span><span class="sxs-lookup"><span data-stu-id="8d755-231">Placement constraints ensure that your workloads only run where they are allowed to, even during upgrades.</span></span> <span data-ttu-id="8d755-232">服務受到極大的條件約束時，升級可能需要較長的時間。</span><span class="sxs-lookup"><span data-stu-id="8d755-232">When services are highly constrained, upgrades can take longer.</span></span> <span data-ttu-id="8d755-233">服務或執行服務的節點為了更新而關閉時，可能有少數幾個選項可供選擇。</span><span class="sxs-lookup"><span data-stu-id="8d755-233">When the service or the node it is running on is brought down for an update there may be few options for where it can go.</span></span>

### <a name="smart-replacements"></a><span data-ttu-id="8d755-234">聰明取代</span><span class="sxs-lookup"><span data-stu-id="8d755-234">Smart replacements</span></span>
<span data-ttu-id="8d755-235">升級開始時，Resource Manager 會取得叢集目前配置方式的快照集。</span><span class="sxs-lookup"><span data-stu-id="8d755-235">When an upgrade starts, the Resource Manager takes a snapshot of the current arrangement of the cluster.</span></span> <span data-ttu-id="8d755-236">每次升級網域完成時，會嘗試將該升級網域中的服務恢復為原始排列方式。</span><span class="sxs-lookup"><span data-stu-id="8d755-236">As each Upgrade Domain completes, it attempts to return the services that were in that Upgrade Domain to their original arrangement.</span></span> <span data-ttu-id="8d755-237">如此一來，在升級期間，服務最多會進行兩次轉換。</span><span class="sxs-lookup"><span data-stu-id="8d755-237">This way there are at most two transitions for a service during the upgrade.</span></span> <span data-ttu-id="8d755-238">一次是從受影響的節點移出服務，另一次是將服務移入。</span><span class="sxs-lookup"><span data-stu-id="8d755-238">There is one move out of the affected node and one move back in.</span></span> <span data-ttu-id="8d755-239">讓叢集或服務回到升級之前的狀態，也可確保升級不會影響叢集配置。</span><span class="sxs-lookup"><span data-stu-id="8d755-239">Returning the cluster or service to how it was before the upgrade also ensures the upgrade doesn’t impact the layout of the cluster.</span></span> 

### <a name="reduced-churn"></a><span data-ttu-id="8d755-240">減少流失</span><span class="sxs-lookup"><span data-stu-id="8d755-240">Reduced churn</span></span>
<span data-ttu-id="8d755-241">升級期間發生還會發生另一件事，就是叢集資源管理員關閉平衡作業。</span><span class="sxs-lookup"><span data-stu-id="8d755-241">Another thing that happens during upgrades is that the Cluster Resource Manager turns off balancing.</span></span> <span data-ttu-id="8d755-242">阻止平衡可避免對升級本身做出不必要的反應，例如將服務移入已清空而不必升級的節點。</span><span class="sxs-lookup"><span data-stu-id="8d755-242">Preventing balancing prevents unnecessary reactions to the upgrade itself, like moving services into nodes that were emptied for the upgrade.</span></span> <span data-ttu-id="8d755-243">如果此次升級是「叢集」升級，則整個叢集在升級期間不會處於平衡狀態。</span><span class="sxs-lookup"><span data-stu-id="8d755-243">If the upgrade in question is a Cluster upgrade, then the entire cluster is not balanced during the upgrade.</span></span> <span data-ttu-id="8d755-244">條件約束檢查會持續作用，只會將計量主動平衡類型的移動停用。</span><span class="sxs-lookup"><span data-stu-id="8d755-244">Constraint checks stay active, only movement based on the proactive balancing of metrics is disabled.</span></span>

### <a name="buffered-capacity--upgrade"></a><span data-ttu-id="8d755-245">緩衝處理的容量和升級</span><span class="sxs-lookup"><span data-stu-id="8d755-245">Buffered Capacity & Upgrade</span></span>
<span data-ttu-id="8d755-246">通常，即使叢集整體受條件約束或接近滿載，您也希望升級完成。</span><span class="sxs-lookup"><span data-stu-id="8d755-246">Generally you want the upgrade to complete even if the cluster is constrained or close to full.</span></span> <span data-ttu-id="8d755-247">在升級期間，叢集容量的管理比平常更重要。</span><span class="sxs-lookup"><span data-stu-id="8d755-247">Managing the capacity of the cluster is even more important during upgrades than usual.</span></span> <span data-ttu-id="8d755-248">根據升級網域的數目，叢集內展開升級時，5% 到 20% 的容量必須移轉。</span><span class="sxs-lookup"><span data-stu-id="8d755-248">Depending on the number of upgrade domains, between 5 and 20 percent of capacity must be migrated as the upgrade rolls through the cluster.</span></span> <span data-ttu-id="8d755-249">工作必須移至別處。</span><span class="sxs-lookup"><span data-stu-id="8d755-249">That work has to go somewhere.</span></span> <span data-ttu-id="8d755-250">[緩衝容量](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity)的概念在此真正派上用場。</span><span class="sxs-lookup"><span data-stu-id="8d755-250">This is where the notion of [buffered capacities](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) is useful.</span></span> <span data-ttu-id="8d755-251">在正常作業期間，系統會採用緩衝處理的容量。</span><span class="sxs-lookup"><span data-stu-id="8d755-251">Buffered capacity is respected during normal operation.</span></span> <span data-ttu-id="8d755-252">在升級期間，叢集資源管理員可能會視需要而使用到節點的所有容量 (消耗緩衝區)。</span><span class="sxs-lookup"><span data-stu-id="8d755-252">The Cluster Resource Manager may fill nodes up to their total capacity (consuming the buffer) during upgrades if necessary.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d755-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8d755-253">Next steps</span></span>
* <span data-ttu-id="8d755-254">從頭開始，並 [取得 Service Fabric 叢集資源管理員的簡介](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8d755-254">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
