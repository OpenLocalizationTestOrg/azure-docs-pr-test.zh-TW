---
title: "aaaService 網狀架構叢集資源管理員的位置原則 |Microsoft 文件"
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
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="f6df1-103">Service Fabric 服務的放置原則</span><span class="sxs-lookup"><span data-stu-id="f6df1-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="f6df1-104">位置原則是可以在某些特定的較不常見的情況下使用的 toogovern 服務位置的其他規則。</span><span class="sxs-lookup"><span data-stu-id="f6df1-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="f6df1-105">這些情況的一些例子如下︰</span><span class="sxs-lookup"><span data-stu-id="f6df1-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="f6df1-106">您的 Service Fabric 叢集跨越一段地理距離 (例如多個內部部署資料中心) 或跨越多個 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="f6df1-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="f6df1-107">您的環境跨越多個區域的地緣政治或法律控制項或某些其他您擁有其原則界限的情況下需要 tooenforce</span><span class="sxs-lookup"><span data-stu-id="f6df1-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="f6df1-108">有到期 toolarge 距離或使用速度較慢或較不可靠的網路連結的通訊延遲或效能考量</span><span class="sxs-lookup"><span data-stu-id="f6df1-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="f6df1-109">您需要特定工作負載共置，以做為最佳效果，與其他工作負載，或在鄰近 toocustomers tookeep</span><span class="sxs-lookup"><span data-stu-id="f6df1-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="f6df1-110">大部分的這些需求對齊 hello 實體配置 hello 叢集中，表示，如 hello hello 叢集的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f6df1-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="f6df1-111">hello 進階的放置原則可協助解決這些案例包括：</span><span class="sxs-lookup"><span data-stu-id="f6df1-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="f6df1-112">無效的網域</span><span class="sxs-lookup"><span data-stu-id="f6df1-112">Invalid domains</span></span>
2. <span data-ttu-id="f6df1-113">所需的網域</span><span class="sxs-lookup"><span data-stu-id="f6df1-113">Required domains</span></span>
3. <span data-ttu-id="f6df1-114">慣用的網域</span><span class="sxs-lookup"><span data-stu-id="f6df1-114">Preferred domains</span></span>
4. <span data-ttu-id="f6df1-115">不允許封裝複本</span><span class="sxs-lookup"><span data-stu-id="f6df1-115">Disallowing replica packing</span></span>

<span data-ttu-id="f6df1-116">無法透過節點屬性及位置條件約束，設定大部分的 hello 控制項，但有些是更複雜。</span><span class="sxs-lookup"><span data-stu-id="f6df1-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="f6df1-117">toomake 方面更簡單，hello Service Fabric 叢集資源管理員會提供這些額外的位置原則。</span><span class="sxs-lookup"><span data-stu-id="f6df1-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="f6df1-118">放置原則可以依個別具名服務執行個體來設定，</span><span class="sxs-lookup"><span data-stu-id="f6df1-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="f6df1-119">還可以動態更新。</span><span class="sxs-lookup"><span data-stu-id="f6df1-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="f6df1-120">指定無效的網域</span><span class="sxs-lookup"><span data-stu-id="f6df1-120">Specifying invalid domains</span></span>
<span data-ttu-id="f6df1-121">hello **InvalidDomain**位置原則可讓您 toospecify 特定容錯網域是無效的特定服務。</span><span class="sxs-lookup"><span data-stu-id="f6df1-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="f6df1-122">此原則可確保特定的服務絕對不會在特定的區域中執行，例如，基於地緣政治或公司政策的緣故。</span><span class="sxs-lookup"><span data-stu-id="f6df1-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="f6df1-123">您可以透過個別原則指定多個無效的網域。</span><span class="sxs-lookup"><span data-stu-id="f6df1-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="f6df1-124"><center>
![無效的網域範例][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="f6df1-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="f6df1-125">程式碼：</span><span class="sxs-lookup"><span data-stu-id="f6df1-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="f6df1-126">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="f6df1-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="f6df1-127">指定所需的網域</span><span class="sxs-lookup"><span data-stu-id="f6df1-127">Specifying required domains</span></span>
<span data-ttu-id="f6df1-128">hello 需要網域位置原則需要 hello 服務只能在 hello 指定網域中。</span><span class="sxs-lookup"><span data-stu-id="f6df1-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="f6df1-129">您可以透過個別原則指定多個所需的網域。</span><span class="sxs-lookup"><span data-stu-id="f6df1-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="f6df1-130"><center>
![所需的網域範例][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="f6df1-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="f6df1-131">程式碼：</span><span class="sxs-lookup"><span data-stu-id="f6df1-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="f6df1-132">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="f6df1-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="f6df1-133">指定的可設定狀態服務的 hello 主要複本的慣用的網域</span><span class="sxs-lookup"><span data-stu-id="f6df1-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="f6df1-134">hello 慣用的主要網域指定 hello 容錯網域 tooplace hello Primary in。</span><span class="sxs-lookup"><span data-stu-id="f6df1-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="f6df1-135">hello 主要最後會在這個網域中的所有項目為狀況良好時。</span><span class="sxs-lookup"><span data-stu-id="f6df1-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="f6df1-136">如果 hello 網域或 hello 主要複本失敗，或關閉，主要 hello 移動 toosome 其他位置，最好是在 hello 相同的網域。</span><span class="sxs-lookup"><span data-stu-id="f6df1-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="f6df1-137">如果這個新的位置不在 hello 慣用的網域，hello 叢集資源管理員移回儘速 toohello 慣用的網域。</span><span class="sxs-lookup"><span data-stu-id="f6df1-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="f6df1-138">當然，此設定僅適用於具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="f6df1-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="f6df1-139">如果叢集跨越 Azure 區域或多個資料中心，但具有選擇放置在特定位置的服務，此原則最有用。</span><span class="sxs-lookup"><span data-stu-id="f6df1-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="f6df1-140">讓主要複本會關閉 tootheir 使用者或其他有助於提供較低的延遲時間，特別是針對讀取，會由主要複本會根據預設的服務。</span><span class="sxs-lookup"><span data-stu-id="f6df1-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="f6df1-141"><center>
![慣用的主要網域和容錯移轉][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="f6df1-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="f6df1-142">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="f6df1-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="f6df1-143">要求複本散佈，且不允許封裝</span><span class="sxs-lookup"><span data-stu-id="f6df1-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="f6df1-144">複本是_通常_分散容錯和升級網域，當 hello 叢集狀況良好。</span><span class="sxs-lookup"><span data-stu-id="f6df1-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="f6df1-145">不過，指定資料分割的多個複本有時會暫時封裝到單一網域。</span><span class="sxs-lookup"><span data-stu-id="f6df1-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="f6df1-146">例如，假設該 hello 叢集有九個節點中三個容錯網域，fd: / 0，fd: / 1 和 fd: / 2。</span><span class="sxs-lookup"><span data-stu-id="f6df1-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="f6df1-147">假設您的服務有三個複本。</span><span class="sxs-lookup"><span data-stu-id="f6df1-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="f6df1-148">讓我們假設該 hello 節點已使用那些中的複本 fd: / 1 和 fd: / 2 停擺。</span><span class="sxs-lookup"><span data-stu-id="f6df1-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="f6df1-149">通常 hello 叢集資源管理員想使用這些相同的容錯網域中的其他節點。</span><span class="sxs-lookup"><span data-stu-id="f6df1-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="f6df1-150">在此情況下，我們假設因為 toocapacity 問題無 hello 的這些網域中的其他節點都有效。</span><span class="sxs-lookup"><span data-stu-id="f6df1-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="f6df1-151">如果 hello 叢集資源管理員建置取代這些複本，它就會有 toochoose 節點在 fd: / 0。</span><span class="sxs-lookup"><span data-stu-id="f6df1-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="f6df1-152">不過，執行_，_建立代表違反 hello 容錯網域條件約束的情況。</span><span class="sxs-lookup"><span data-stu-id="f6df1-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="f6df1-153">壓縮複本會增加 hello 整個複本集的 hello 機率無法向下或遺失。</span><span class="sxs-lookup"><span data-stu-id="f6df1-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="f6df1-154">如需一般情況下條件約束和條件約束優先順序的詳細資訊，請參閱[本主題](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities)。</span><span class="sxs-lookup"><span data-stu-id="f6df1-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="f6df1-155">如果您曾看過類似「`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`」的健康狀態訊息，表示您已遇到此狀況或類似的情況。</span><span class="sxs-lookup"><span data-stu-id="f6df1-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="f6df1-156">通常只有一或兩個複本會暫時封裝在一起。</span><span class="sxs-lookup"><span data-stu-id="f6df1-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="f6df1-157">只要少於指定網域中複本的法定數目，就是安全的。</span><span class="sxs-lookup"><span data-stu-id="f6df1-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="f6df1-158">封裝很少見，但還是有可能發生，並且這些情況通常是暫時性因為 hello 節點回來。</span><span class="sxs-lookup"><span data-stu-id="f6df1-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="f6df1-159">如果 hello 節點執行保持關閉且 hello 叢集資源管理員需要 toobuild 取代項目時，通常有可用的其他節點 hello 理想的容錯網域中。</span><span class="sxs-lookup"><span data-stu-id="f6df1-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="f6df1-160">某些工作負載偏好一律擁有 hello 目標數目複本，即使它們會封裝為更少的定義域。</span><span class="sxs-lookup"><span data-stu-id="f6df1-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="f6df1-161">這些工作負載打賭會同時全面發生永久性網域故障，通常可以復原本機狀態。</span><span class="sxs-lookup"><span data-stu-id="f6df1-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="f6df1-162">其他工作負載而需要花 hello 停機時間早於風險正確性或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="f6df1-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="f6df1-163">大部分生產工作負載執行時會使用三個以上的複本、三個以上的容錯網域，以及每個容錯網域的許多有效節點。</span><span class="sxs-lookup"><span data-stu-id="f6df1-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="f6df1-164">因為這個緣故，hello 預設行為的預設值，讓網域封裝。</span><span class="sxs-lookup"><span data-stu-id="f6df1-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="f6df1-165">hello 預設行為可讓一般平衡和容錯移轉 toohandle 這些極端的情況下，即使這表示暫存網域封裝。</span><span class="sxs-lookup"><span data-stu-id="f6df1-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="f6df1-166">如果您想 toodisable 這類特定工作負載的封裝，您可以指定 hello `RequireDomainDistribution` hello 服務上的原則。</span><span class="sxs-lookup"><span data-stu-id="f6df1-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="f6df1-167">當此原則設定時，hello 叢集資源管理員可確保從 hello hello 相同錯誤，或升級網域中執行相同的資料分割沒有兩個複本。</span><span class="sxs-lookup"><span data-stu-id="f6df1-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="f6df1-168">程式碼：</span><span class="sxs-lookup"><span data-stu-id="f6df1-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="f6df1-169">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="f6df1-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="f6df1-170">現在，它會是可能 toouse 服務合併不地理位置的叢集中的這些設定嗎？</span><span class="sxs-lookup"><span data-stu-id="f6df1-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="f6df1-171">可以，但也沒有充分的理由。</span><span class="sxs-lookup"><span data-stu-id="f6df1-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="f6df1-172">hello 必要、 不正確，及慣用網域組態應該避免除非 hello 案例需要這些項目。</span><span class="sxs-lookup"><span data-stu-id="f6df1-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="f6df1-173">它不讓任何有意義 tootry tooforce 給定工作負載 toorun 在單一機架或 tooprefer 某個線段的透過另一個本機叢集。</span><span class="sxs-lookup"><span data-stu-id="f6df1-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="f6df1-174">不同的硬體設定應該分散至容錯網域，並透過一般放置條件約束和節點屬性來處理。</span><span class="sxs-lookup"><span data-stu-id="f6df1-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6df1-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6df1-175">Next steps</span></span>
- <span data-ttu-id="f6df1-176">如需服務設定的詳細資訊，請[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="f6df1-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
