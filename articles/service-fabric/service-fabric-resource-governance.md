---
title: "適用於容器和服務的 Azure Service Fabric 資源管理 | Microsoft Docs"
description: "Azure Service Fabric 可讓您針對在容器內部或外部執行的服務指定資源限制。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88d44953ad83f9e7401fd087a39842e4a3790124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="resource-governance"></a><span data-ttu-id="c5a7d-103">資源管理</span><span class="sxs-lookup"><span data-stu-id="c5a7d-103">Resource governance</span></span> 

<span data-ttu-id="c5a7d-104">在相同的節點或叢集上執行多個服務時，有可能發生一個服務取用較多資源而導致其他服務無資源可用的情況。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-104">When running multiple services on the same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="c5a7d-105">此問題稱為擾鄰問題。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-105">This problem is referred to as the noisy-neighbor problem.</span></span> <span data-ttu-id="c5a7d-106">Service Fabric 可讓開發人員指定每一服務的保留和限制，以確保有資源可用並且也限制其資源使用量。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-106">Service Fabric allows the developer to specify reservations and limits per service to guarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="c5a7d-107">資源管理計量</span><span class="sxs-lookup"><span data-stu-id="c5a7d-107">Resource governance metrics</span></span> 

<span data-ttu-id="c5a7d-108">Service Fabric 可依每一[服務套件](service-fabric-application-model.md)支援資源管理。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="c5a7d-109">指派給「服務套件」的資源可以進一步在程式碼套件之間分配。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-109">The resources that are assigned to Service Package can be further divided between code packages.</span></span> <span data-ttu-id="c5a7d-110">指定的資源限制也意謂著資源的保留。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-110">The resource limits specified also mean the reservation of the resources.</span></span> <span data-ttu-id="c5a7d-111">Service Fabric 支援使用兩個內建的[計量](service-fabric-cluster-resource-manager-metrics.md)來指定每一服務套件的 CPU 和記憶體：</span><span class="sxs-lookup"><span data-stu-id="c5a7d-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="c5a7d-112">CPU (計量名稱 `ServiceFabric:/_CpuCores`)：核心係指主機電腦上可用的邏輯核心，所有節點上所有核心的權數都相同。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on the host machine, and all cores across all nodes are weighted the same.</span></span>
* <span data-ttu-id="c5a7d-113">記憶體 (計量名稱 `ServiceFabric:/_MemoryInMB`)：記憶體的單位為 MB，它會與電腦上可用的實體記憶體對應。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps to physical memory that is available on the machine.</span></span>

<span data-ttu-id="c5a7d-114">僅提供彈性保留保證 - 如果超出可用的資源數，執行階段就會拒絕開啟新的服務套件。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-114">Only soft reservation guarantees are provided - the runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="c5a7d-115">不過，如在節點上放置另一個可執行檔或容器，可能就會違反原先的保留保證。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-115">However, if another executable or container is placed on the node, that may violate the original reservation guarantees.</span></span>

<span data-ttu-id="c5a7d-116">針對這兩個計量，[叢集資源管理員](service-fabric-cluster-resource-manager-cluster-description.md)會追蹤叢集總容量、叢集中每個節點上的負載，以及叢集中剩餘的資源數。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-116">For these two metrics, the [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, the load on each node in the cluster, and, remaining resources in the cluster.</span></span> <span data-ttu-id="c5a7d-117">這兩個計量等同於任何其他使用者或自訂計量，而且所有現有的功能都可以與它們搭配使用：</span><span class="sxs-lookup"><span data-stu-id="c5a7d-117">These two metrics are equivalent to any other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="c5a7d-118">叢集可以根據這兩個計量 (預設行為) 來進行[平衡](service-fabric-cluster-resource-manager-balancing.md)。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according to these two metrics (default behavior).</span></span>
* <span data-ttu-id="c5a7d-119">叢集可以根據這兩個計量來進行[重組](service-fabric-cluster-resource-manager-defragmentation-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according to these two metrics.</span></span>
* <span data-ttu-id="c5a7d-120">在[描述叢集](service-fabric-cluster-resource-manager-cluster-description.md)時，可以為這兩個計量設定緩衝處理的容量。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="c5a7d-121">這些計量不支援[動態負載報告](service-fabric-cluster-resource-manager-metrics.md)，而這些計量的負載則是在建立時定義。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="c5a7d-122">設定叢集以啟用資源管理</span><span class="sxs-lookup"><span data-stu-id="c5a7d-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="c5a7d-123">您應該依下列方式，在叢集的每個節點中手動定義容量：</span><span class="sxs-lookup"><span data-stu-id="c5a7d-123">Capacity should be defined manually in each node type in the cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="c5a7d-124">只有在使用者服務上才允許進行資源管理，在任何系統服務上則都不允許。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="c5a7d-125">指定容量時，必須保留部分核心和記憶體不進行配置，以供系統服務使用。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="c5a7d-126">為了獲得最佳效能，在叢集資訊清單中應該也開啟下列設定：</span><span class="sxs-lookup"><span data-stu-id="c5a7d-126">For optimal performance, the following setting should also be turned on in the cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="c5a7d-127">指定資源管理</span><span class="sxs-lookup"><span data-stu-id="c5a7d-127">Specifying resource governance</span></span> 

<span data-ttu-id="c5a7d-128">指定資源管理限制時，是在應用程式資訊清單 (ServiceManifestImport 區段) 中指定，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="c5a7d-128">Resource governance limits are specified in the application manifest (ServiceManifestImport section) as shown in the following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has the number of CPU cores defined, but doesn't have the MemoryInMB defined.
  In this case, Service Fabric will sum the limits on code packages and uses the sum as 
  the overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
<span data-ttu-id="c5a7d-129">在此範例中，服務套件 ServicePackageA 在其所在的節點上獲得一個核心。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-129">In this example, service package ServicePackageA gets one core on the nodes where it is placed.</span></span> <span data-ttu-id="c5a7d-130">此服務套件包含兩個程式碼套件 (CodeA1 和 CodeA2)，且兩者皆指定 `CpuShares` 參數。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify the `CpuShares` parameter.</span></span> <span data-ttu-id="c5a7d-131">CpuShares 的比例 512:256 會將核心在這兩個程式碼套件做分配。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-131">The proportion of CpuShares 512:256  divides the core across the two code packages.</span></span> <span data-ttu-id="c5a7d-132">因此，在此範例中，CodeA1 會獲得 2/3 的核心，CodeA2 則獲得 1/3 的核心 (並具有同樣的彈性保證保留)。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="c5a7d-133">如果未針對程式碼套件指定 CpuShares，Service Fabric 就會在它們之間平均分配核心。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-133">In case when CpuShares are not specified for code packages, Service Fabric divides the cores equally among them.</span></span>

<span data-ttu-id="c5a7d-134">記憶體限制是絕對的，因此這兩個程式碼套件都限制為 1024 MB 的記憶體 (並具有同樣的彈性保證保留)。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-134">Memory limits are absolute, so both code packages are limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="c5a7d-135">程式碼套件 (容器或處理序) 無法配置超過此限制的記憶體，如果嘗試這麼做，將會導致發生記憶體不足的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-135">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="c5a7d-136">若要讓資源限制強制能夠運作，應該為服務套件內的所有程式碼套件都指定記憶體限制。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-136">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c5a7d-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5a7d-137">Next steps</span></span>
* <span data-ttu-id="c5a7d-138">若要深入了解「叢集資源管理員」，請參閱這篇[文章](service-fabric-cluster-resource-manager-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-138">To learn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="c5a7d-139">若要深入了解應用程式模型、服務套件、程式碼套件，以及複本如何與它們對應，請參閱這篇[文章](service-fabric-application-model.md)。</span><span class="sxs-lookup"><span data-stu-id="c5a7d-139">To learn more about application model, service packages, code packages and how replicas map to them read this [article](service-fabric-application-model.md).</span></span>
