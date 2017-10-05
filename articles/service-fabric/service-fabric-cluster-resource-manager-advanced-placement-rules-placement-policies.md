---
title: "Service Fabric 叢集 Resource Manager - 放置原則 | Microsoft Docs"
description: "Service Fabric 服務的其他放置原則和規則的概觀"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 6c11d49d5fdb3148b0534c9448f815358fa8cab3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="47826-103">Service Fabric 服務的放置原則</span><span class="sxs-lookup"><span data-stu-id="47826-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="47826-104">放置原則是在一些較罕見的特定情況下可用來掌管服務放置的額外規則。</span><span class="sxs-lookup"><span data-stu-id="47826-104">Placement policies are additional rules that can be used to govern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="47826-105">這些情況的一些例子如下︰</span><span class="sxs-lookup"><span data-stu-id="47826-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="47826-106">您的 Service Fabric 叢集跨越一段地理距離 (例如多個內部部署資料中心) 或跨越多個 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="47826-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="47826-107">您的環境跨越多個地緣政治或法定管制區，或是在其他一些情況下，您有需要強制執行的政策界限</span><span class="sxs-lookup"><span data-stu-id="47826-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need to enforce</span></span>
- <span data-ttu-id="47826-108">由於距離很大，或是使用較慢或較不可靠的網路連結，而有通訊效能或延遲考量</span><span class="sxs-lookup"><span data-stu-id="47826-108">There are communication performance or latency considerations due to large distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="47826-109">您需要盡最大努力確保特定工作負載與其他工作負載共置，或放置在客戶附近</span><span class="sxs-lookup"><span data-stu-id="47826-109">You need to keep certain workloads collocated as a best effort, either with other workloads or in proximity to customers</span></span>

<span data-ttu-id="47826-110">上述大部分需求會與叢集的實體配置 (以叢集的容錯網域表示) 一致。</span><span class="sxs-lookup"><span data-stu-id="47826-110">Most of these requirements align with the physical layout of the cluster, represented as the fault domains of the cluster.</span></span> 

<span data-ttu-id="47826-111">可協助解決這些情況的進階放置原則包括：</span><span class="sxs-lookup"><span data-stu-id="47826-111">The advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="47826-112">無效的網域</span><span class="sxs-lookup"><span data-stu-id="47826-112">Invalid domains</span></span>
2. <span data-ttu-id="47826-113">所需的網域</span><span class="sxs-lookup"><span data-stu-id="47826-113">Required domains</span></span>
3. <span data-ttu-id="47826-114">慣用的網域</span><span class="sxs-lookup"><span data-stu-id="47826-114">Preferred domains</span></span>
4. <span data-ttu-id="47826-115">不允許封裝複本</span><span class="sxs-lookup"><span data-stu-id="47826-115">Disallowing replica packing</span></span>

<span data-ttu-id="47826-116">以下大部分控制可透過節點屬性和放置條件約束來設定，但其中有一些比較複雜。</span><span class="sxs-lookup"><span data-stu-id="47826-116">Most of the following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="47826-117">為了簡化起見，Service Fabric 叢集資源管理員提供這些額外的放置原則。</span><span class="sxs-lookup"><span data-stu-id="47826-117">To make things simpler, the Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="47826-118">放置原則可以依個別具名服務執行個體來設定，</span><span class="sxs-lookup"><span data-stu-id="47826-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="47826-119">還可以動態更新。</span><span class="sxs-lookup"><span data-stu-id="47826-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="47826-120">指定無效的網域</span><span class="sxs-lookup"><span data-stu-id="47826-120">Specifying invalid domains</span></span>
<span data-ttu-id="47826-121">**InvalidDomain** 放置原則可讓您指定某個容錯網域對特定服務是無效的。</span><span class="sxs-lookup"><span data-stu-id="47826-121">The **InvalidDomain** placement policy allows you to specify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="47826-122">此原則可確保特定的服務絕對不會在特定的區域中執行，例如，基於地緣政治或公司政策的緣故。</span><span class="sxs-lookup"><span data-stu-id="47826-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="47826-123">您可以透過個別原則指定多個無效的網域。</span><span class="sxs-lookup"><span data-stu-id="47826-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="47826-124"><center>
![無效的網域範例][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="47826-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="47826-125">程式碼：</span><span class="sxs-lookup"><span data-stu-id="47826-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="47826-126">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="47826-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="47826-127">指定所需的網域</span><span class="sxs-lookup"><span data-stu-id="47826-127">Specifying required domains</span></span>
<span data-ttu-id="47826-128">所需的網域放置原則要求服務只能存在於指定的網域中。</span><span class="sxs-lookup"><span data-stu-id="47826-128">The required domain placement policy requires that the service is present only in the specified domain.</span></span> <span data-ttu-id="47826-129">您可以透過個別原則指定多個所需的網域。</span><span class="sxs-lookup"><span data-stu-id="47826-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="47826-130"><center>
![所需的網域範例][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="47826-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="47826-131">程式碼：</span><span class="sxs-lookup"><span data-stu-id="47826-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="47826-132">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="47826-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-the-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="47826-133">指定具狀態服務之主要複本的慣用網域</span><span class="sxs-lookup"><span data-stu-id="47826-133">Specifying a preferred domain for the primary replicas of a stateful service</span></span>
<span data-ttu-id="47826-134">「慣用的主要網域」會指定要放置「主要」複本的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="47826-134">The Preferred Primary Domain specifies the fault domain to place the Primary in.</span></span> <span data-ttu-id="47826-135">若一切狀況良好，「主要」複本最後會在這個網域中。</span><span class="sxs-lookup"><span data-stu-id="47826-135">The Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="47826-136">如果網域或「主要」複本失敗或關閉，則「主要」複本會移至某些其他位置，在理想狀況下會是相同的網域。</span><span class="sxs-lookup"><span data-stu-id="47826-136">If the domain or the Primary replica fails or shuts down, the Primary moves to some other location, ideally in the same domain.</span></span> <span data-ttu-id="47826-137">如果這個新的位置並非慣用的網域，叢集資源管理員會儘快將它移回慣用的網域。</span><span class="sxs-lookup"><span data-stu-id="47826-137">If this new location isn't in the preferred domain, the Cluster Resource Manager moves it back to the preferred domain as soon as possible.</span></span> <span data-ttu-id="47826-138">當然，此設定僅適用於具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="47826-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="47826-139">如果叢集跨越 Azure 區域或多個資料中心，但具有選擇放置在特定位置的服務，此原則最有用。</span><span class="sxs-lookup"><span data-stu-id="47826-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="47826-140">讓「主要」複本靠近其使用者或其他服務有助於縮短延遲，特別是針對「主要」複本預設所處理的讀取作業。</span><span class="sxs-lookup"><span data-stu-id="47826-140">Keeping Primaries close to their users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="47826-141"><center>
![慣用的主要網域和容錯移轉][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="47826-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="47826-142">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="47826-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="47826-143">要求複本散佈，且不允許封裝</span><span class="sxs-lookup"><span data-stu-id="47826-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="47826-144">叢集狀況良好時，複本「通常」會散佈在容錯和升級網域之間。</span><span class="sxs-lookup"><span data-stu-id="47826-144">Replicas are _normally_ distributed across fault and upgrade domains when the cluster is healthy.</span></span> <span data-ttu-id="47826-145">不過，指定資料分割的多個複本有時會暫時封裝到單一網域。</span><span class="sxs-lookup"><span data-stu-id="47826-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="47826-146">例如，假設叢集有九個節點在三個容錯網域中 (fd:/0、fd:/1 和 fd:/2)。</span><span class="sxs-lookup"><span data-stu-id="47826-146">For example, let's say that the cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="47826-147">假設您的服務有三個複本。</span><span class="sxs-lookup"><span data-stu-id="47826-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="47826-148">假設 fd:/1 和 fd:/2 中用於這些複本的節點停止運作。</span><span class="sxs-lookup"><span data-stu-id="47826-148">Let's say that the nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="47826-149">叢集資源管理員通常會選擇這些相同容錯網域中的其他節點。</span><span class="sxs-lookup"><span data-stu-id="47826-149">Normally the Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="47826-150">在此情況下，假設因為容量問題，這些網域中的其他節點都無效。</span><span class="sxs-lookup"><span data-stu-id="47826-150">In this case, let's say due to capacity issues none of the other nodes in those domains were valid.</span></span> <span data-ttu-id="47826-151">如果叢集資源管理員為這些複本建立替代項目，則必須選擇 fd:/0 中的節點。</span><span class="sxs-lookup"><span data-stu-id="47826-151">If the Cluster Resource Manager builds replacements for those replicas, it would have to choose nodes in fd:/0.</span></span> <span data-ttu-id="47826-152">不過，「這樣做」會導致違反容錯網域條件約束。</span><span class="sxs-lookup"><span data-stu-id="47826-152">However, doing _that_ creates a situation where the Fault Domain constraint is violated.</span></span> <span data-ttu-id="47826-153">封裝複本會增加整個複本集停止運作或遺失的可能性。</span><span class="sxs-lookup"><span data-stu-id="47826-153">Packing replicas increases the chance that the whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="47826-154">如需一般情況下條件約束和條件約束優先順序的詳細資訊，請參閱[本主題](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities)。</span><span class="sxs-lookup"><span data-stu-id="47826-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="47826-155">如果您曾看過類似「`The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain`」的健康狀態訊息，表示您已遇到此狀況或類似的情況。</span><span class="sxs-lookup"><span data-stu-id="47826-155">If you've ever seen a health message such as "`The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="47826-156">通常只有一或兩個複本會暫時封裝在一起。</span><span class="sxs-lookup"><span data-stu-id="47826-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="47826-157">只要少於指定網域中複本的法定數目，就是安全的。</span><span class="sxs-lookup"><span data-stu-id="47826-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="47826-158">封裝很罕見，但可能發生，這些情況通常是暫時性，因為節點會恢復。</span><span class="sxs-lookup"><span data-stu-id="47826-158">Packing is rare, but it can happen, and usually these situations are transient since the nodes come back.</span></span> <span data-ttu-id="47826-159">如果節點持續關閉，而且叢集資源管理員需要建置替代項目，理想的容錯網域中通常會有其他節點可用。</span><span class="sxs-lookup"><span data-stu-id="47826-159">If the nodes do stay down and the Cluster Resource Manager needs to build replacements, usually there are other nodes available in the ideal fault domains.</span></span>

<span data-ttu-id="47826-160">某些工作負載即使封裝至更少的網域，也一律都有達到目標數目的複本。</span><span class="sxs-lookup"><span data-stu-id="47826-160">Some workloads would prefer always having the target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="47826-161">這些工作負載打賭會同時全面發生永久性網域故障，通常可以復原本機狀態。</span><span class="sxs-lookup"><span data-stu-id="47826-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="47826-162">其他工作負載會提早停工，而不想冒著更正或遺失資料的風險。</span><span class="sxs-lookup"><span data-stu-id="47826-162">Other workloads would rather take the downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="47826-163">大部分生產工作負載執行時會使用三個以上的複本、三個以上的容錯網域，以及每個容錯網域的許多有效節點。</span><span class="sxs-lookup"><span data-stu-id="47826-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="47826-164">因此，預設行為預設會允許網域封裝。</span><span class="sxs-lookup"><span data-stu-id="47826-164">Because of this, the default behavior allows domain packing by default.</span></span> <span data-ttu-id="47826-165">預設行為允許一般平衡和容錯移轉處理這些極端情況，即使這表示暫時的網域封裝也一樣。</span><span class="sxs-lookup"><span data-stu-id="47826-165">The default behavior allows normal balancing and failover to handle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="47826-166">如果您想要對指定的工作負載停用這類封裝，您可以在服務上指定 `RequireDomainDistribution` 原則。</span><span class="sxs-lookup"><span data-stu-id="47826-166">If you want to disable such packing for a given workload, you can specify the `RequireDomainDistribution` policy on the service.</span></span> <span data-ttu-id="47826-167">設定此原則時，叢集資源管理員可確保來自相同資料分割的兩個複本不會在相同的容錯網域或升級網域中執行。</span><span class="sxs-lookup"><span data-stu-id="47826-167">When this policy is set, the Cluster Resource Manager ensures no two replicas from the same partition run in the same fault or upgrade domain.</span></span>

<span data-ttu-id="47826-168">程式碼：</span><span class="sxs-lookup"><span data-stu-id="47826-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="47826-169">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="47826-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="47826-170">現在，是否可針對未跨越地理區域的叢集中的服務使用這些組態？</span><span class="sxs-lookup"><span data-stu-id="47826-170">Now, would it be possible to use these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="47826-171">可以，但也沒有充分的理由。</span><span class="sxs-lookup"><span data-stu-id="47826-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="47826-172">除非情況要求，否則請避免所需、無效和慣用的網域設定。</span><span class="sxs-lookup"><span data-stu-id="47826-172">The required, invalid, and preferred domain configurations should be avoided unless the scenarios require them.</span></span> <span data-ttu-id="47826-173">如果試著強制在單一機架中執行指定的工作負載，或偏好本機叢集的某些區段而不是其他區段，這樣並沒有任何意義。</span><span class="sxs-lookup"><span data-stu-id="47826-173">It doesn't make any sense to try to force a given workload to run in a single rack, or to prefer some segment of your local cluster over another.</span></span> <span data-ttu-id="47826-174">不同的硬體設定應該分散至容錯網域，並透過一般放置條件約束和節點屬性來處理。</span><span class="sxs-lookup"><span data-stu-id="47826-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47826-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47826-175">Next steps</span></span>
- <span data-ttu-id="47826-176">如需服務設定的詳細資訊，請[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="47826-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
