---
title: "aaaAzure 服務網狀架構資源管理針對容器和服務 |Microsoft 文件"
description: "Azure 服務網狀架構可讓您執行內部或外部的容器服務 toospecify 資源限制。"
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
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a><span data-ttu-id="a3ecb-103">資源管理</span><span class="sxs-lookup"><span data-stu-id="a3ecb-103">Resource governance</span></span> 

<span data-ttu-id="a3ecb-104">當上執行多個服務 hello 相同節點或叢集時，很可能在一個服務可能會耗用更多資源匱乏資源的其他服務。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="a3ecb-105">這個問題是參照的 tooas hello 雜訊芳鄰的問題。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="a3ecb-106">Service Fabric 可讓 hello 開發人員 toospecify 保留項目和每個服務 tooguarantee 資源限制，以及也會限制其資源使用量。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="a3ecb-107">資源管理計量</span><span class="sxs-lookup"><span data-stu-id="a3ecb-107">Resource governance metrics</span></span> 

<span data-ttu-id="a3ecb-108">Service Fabric 可依每一[服務套件](service-fabric-application-model.md)支援資源管理。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="a3ecb-109">指派 tooService 套件 hello 資源可以進一步劃分的程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="a3ecb-110">指定的 hello 資源限制也表示 hello 資源 hello 保留項的目。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="a3ecb-111">Service Fabric 支援使用兩個內建的[計量](service-fabric-cluster-resource-manager-metrics.md)來指定每一服務套件的 CPU 和記憶體：</span><span class="sxs-lookup"><span data-stu-id="a3ecb-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="a3ecb-112">CPU (衡量標準名稱`ServiceFabric:/_CpuCores`): 一個核心 hello 主機電腦，可以使用的邏輯核心跨越所有節點的所有核心會都評估而且 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="a3ecb-113">記憶體 (衡量標準名稱`ServiceFabric:/_MemoryInMB`): 表示記憶體以 mb 為單位，而且它會對應 toophysical hello 電腦可以使用的記憶體。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="a3ecb-114">僅彈性保留保證就會提供-hello 執行階段會拒絕開啟新的服務封裝可用的資源超過。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="a3ecb-115">不過，如果另一個可執行檔或容器放置在 hello 節點時，可能違反 hello 原始保留保證。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="a3ecb-116">這些兩個度量，hello[叢集資源管理員](service-fabric-cluster-resource-manager-cluster-description.md)追蹤總叢集容量，hello hello 叢集中的每個節點上的負載，和剩餘的 hello 叢集中的資源。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="a3ecb-117">這些兩個度量資訊會相當 tooany，其他使用者或自訂的度量和所有現有的功能可以搭配它們：</span><span class="sxs-lookup"><span data-stu-id="a3ecb-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="a3ecb-118">可以是叢集[平衡](service-fabric-cluster-resource-manager-balancing.md)根據 toothese 兩個度量 （預設行為）。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="a3ecb-119">可以是叢集[重組](service-fabric-cluster-resource-manager-defragmentation-metrics.md)根據 toothese 兩個度量。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="a3ecb-120">在[描述叢集](service-fabric-cluster-resource-manager-cluster-description.md)時，可以為這兩個計量設定緩衝處理的容量。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="a3ecb-121">這些計量不支援[動態負載報告](service-fabric-cluster-resource-manager-metrics.md)，而這些計量的負載則是在建立時定義。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="a3ecb-122">設定叢集以啟用資源管理</span><span class="sxs-lookup"><span data-stu-id="a3ecb-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="a3ecb-123">容量應定義為以手動方式在 hello 叢集中的每個節點類型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a3ecb-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="a3ecb-124">只有在使用者服務上才允許進行資源管理，在任何系統服務上則都不允許。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="a3ecb-125">指定容量時，必須保留部分核心和記憶體不進行配置，以供系統服務使用。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="a3ecb-126">為了達到最佳效能，下列設定的 hello 應該也開啟 hello 叢集資訊清單中：</span><span class="sxs-lookup"><span data-stu-id="a3ecb-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="a3ecb-127">指定資源管理</span><span class="sxs-lookup"><span data-stu-id="a3ecb-127">Specifying resource governance</span></span> 

<span data-ttu-id="a3ecb-128">資源控管限制 hello 應用程式資訊清單 （ServiceManifestImport 區段） 中指定 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="a3ecb-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
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
  
<span data-ttu-id="a3ecb-129">在此範例中，服務封裝 ServicePackageA 取得 hello 節點放置的位置上的其中一個核心。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="a3ecb-130">此服務封裝包含兩個程式碼封裝 （CodeA1 和 CodeA2），並同時指定 hello`CpuShares`參數。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="a3ecb-131">CpuShares 512:256 hello 比例將在兩個程式碼封裝 hello 之間分割 hello 核心。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="a3ecb-132">因此，在此範例中，CodeA1 取得三分之二的核心，CodeA2 取得三分之一的核心 （並的軟體保證保留 hello 相同）。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="a3ecb-133">如果當 CpuShares 不會指定程式碼封裝，Service Fabric 會將它們之間平均 hello 核心。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="a3ecb-134">記憶體限制是絕對的因此這兩個程式碼封裝的有限的 too1024 MB 的記憶體 （和 hello 相同的軟體保證保留）。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="a3ecb-135">程式碼封裝 （容器或處理程序） 不能 tooallocate 記憶體超過此限制，而嘗試 toodo 因此會導致記憶體不足例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="a3ecb-136">資源限制強制 toowork，所有的程式碼封裝在服務封裝內必須有指定記憶體限制。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a3ecb-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3ecb-137">Next steps</span></span>
* <span data-ttu-id="a3ecb-138">toolearn 更多有關叢集資源管理員，請閱讀本[文章](service-fabric-cluster-resource-manager-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="a3ecb-139">深入了解應用程式模型中，服務套件、 程式碼封裝和複本如何對應 toothem toolearn 讀取這[文章](service-fabric-application-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a3ecb-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
