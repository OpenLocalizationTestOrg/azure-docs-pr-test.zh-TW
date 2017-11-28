---
title: "Service Fabric 叢集 Resource Manager - 應用程式群組 | Microsoft Docs"
description: "Service Fabric 叢集 Resource Manager 中應用程式群組功能的概觀"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7fc61731c8df2a0c3dc5b77ae718b41c240f9233
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-application-groups"></a><span data-ttu-id="79922-103">應用程式群組簡介</span><span class="sxs-lookup"><span data-stu-id="79922-103">Introduction to Application Groups</span></span>
<span data-ttu-id="79922-104">Service Fabric 的叢集資源管理員通常會將負載平均分配到整個叢集 (透過[計量](service-fabric-cluster-resource-manager-metrics.md)表示)，以管理叢集資源。</span><span class="sxs-lookup"><span data-stu-id="79922-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading the load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout the cluster.</span></span> <span data-ttu-id="79922-105">Service Fabric 透過[容量](service-fabric-cluster-resource-manager-cluster-description.md)管理叢集的節點容量及整個叢集的容量。</span><span class="sxs-lookup"><span data-stu-id="79922-105">Service Fabric manages the capacity of the nodes in the cluster and the cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="79922-106">計量和容量很適用於許多工作負載，但過度使用不同 Service Fabric 應用程式執行個體的模式，有時會引起其他需求。</span><span class="sxs-lookup"><span data-stu-id="79922-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="79922-107">例如，您可能想要：</span><span class="sxs-lookup"><span data-stu-id="79922-107">For example you may want to:</span></span>

- <span data-ttu-id="79922-108">保留叢集節點上的一些容量，用於具名應用程式執行個體內的服務</span><span class="sxs-lookup"><span data-stu-id="79922-108">Reserve some capacity on the nodes in the cluster for the services within some named application instance</span></span>
- <span data-ttu-id="79922-109">限制具名應用程式執行個體內的服務執行的節點總數 (而不是將這些服務散佈到整個叢集)</span><span class="sxs-lookup"><span data-stu-id="79922-109">Limit the total number of nodes that the services within a named application instance run on (instead of spreading them out over the entire cluster)</span></span>
- <span data-ttu-id="79922-110">決定具名應用程式執行個體本身的容量，以限制服務數量或執行個體內服務的資源總耗用量</span><span class="sxs-lookup"><span data-stu-id="79922-110">Define capacities on the named application instance itself to limit the number of services or total resource consumption of the services inside it</span></span>

<span data-ttu-id="79922-111">為了符合這些需求，Service Fabric 叢集資源管理員可支援名為應用程式群組的功能。</span><span class="sxs-lookup"><span data-stu-id="79922-111">To meet these requirements, the Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-the-maximum-number-of-nodes"></a><span data-ttu-id="79922-112">限制節點數目上限</span><span class="sxs-lookup"><span data-stu-id="79922-112">Limiting the maximum number of nodes</span></span>
<span data-ttu-id="79922-113">應用程式容量的最簡單使用案例，是在需要將應用程式執行個體限制為特定的節點數目上限時。</span><span class="sxs-lookup"><span data-stu-id="79922-113">The simplest use case for Application capacity is when an application instance needs to be limited to a certain maximum number of nodes.</span></span> <span data-ttu-id="79922-114">這會將該應用程式執行個體中的所有服務合併到固定數目的機器上。</span><span class="sxs-lookup"><span data-stu-id="79922-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="79922-115">在嘗試預測或限制該具名應用程式執行個體中的服務所使用的實體資源時，適合使用合併。</span><span class="sxs-lookup"><span data-stu-id="79922-115">Consolidation is useful when you're trying to predict or cap physical resource use by the services within that named application instance.</span></span> 

<span data-ttu-id="79922-116">下圖顯示已定義和未定義節點數目上限的應用程式執行個體：</span><span class="sxs-lookup"><span data-stu-id="79922-116">The following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="79922-117"><center>
![定義節點數目上限的應用程式執行個體][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="79922-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="79922-118">在左邊的範例中，應用程式沒有定義的節點數目上限，且提供有三項服務。</span><span class="sxs-lookup"><span data-stu-id="79922-118">In the left example, the application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="79922-119">叢集資源管理員已將所有複本分散到六個可用的節點，在叢集中達到最佳平衡狀態 (預設行為)。</span><span class="sxs-lookup"><span data-stu-id="79922-119">The Cluster Resource Manager has spread out all replicas across six available nodes to achieve the best balance in the cluster (the default behavior).</span></span> <span data-ttu-id="79922-120">在右邊的範例中，我們看到相同的應用程式限制為三個節點。</span><span class="sxs-lookup"><span data-stu-id="79922-120">In the right example, we see the same application limited to three nodes.</span></span>

<span data-ttu-id="79922-121">控制此行為的參數稱為 MaximumNodes。</span><span class="sxs-lookup"><span data-stu-id="79922-121">The parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="79922-122">您可以在應用程式建立期間設定這個參數，也可以針對執行中的應用程式執行個體更新這個參數。</span><span class="sxs-lookup"><span data-stu-id="79922-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="79922-123">Powershell</span><span class="sxs-lookup"><span data-stu-id="79922-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="79922-124">C#</span><span class="sxs-lookup"><span data-stu-id="79922-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="79922-125">在節點集內，叢集資源管理員無法保證哪些服務物件會放置在一起，或會使用哪些節點。</span><span class="sxs-lookup"><span data-stu-id="79922-125">Within the set of nodes, the Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="79922-126">應用程式度量、負載和容量</span><span class="sxs-lookup"><span data-stu-id="79922-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="79922-127">應用程式群組也可讓您定義與特定具名應用程式執行個體相關聯的計量，以及應用程式執行個體在這些計量中的容量。</span><span class="sxs-lookup"><span data-stu-id="79922-127">Application Groups also allow you to define metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="79922-128">應用程式計量可讓您追蹤、保留及限制該應用程式執行個體內各項服務的資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="79922-128">Application metrics allow you to track, reserve, and limit the resource consumption of the services inside that application instance.</span></span>

<span data-ttu-id="79922-129">每一個應用程式計量可以設定兩個值︰</span><span class="sxs-lookup"><span data-stu-id="79922-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="79922-130">**應用程式容量總計** – 這項設定代表應用程式在特定計量中的容量總計。</span><span class="sxs-lookup"><span data-stu-id="79922-130">**Total Application Capacity** – This setting represents the total capacity of the application for a particular metric.</span></span> <span data-ttu-id="79922-131">如果在這個應用程式執行個體內建立任何新的服務會導致總負載超過此值，則叢集資源管理員不允許建立這些服務。</span><span class="sxs-lookup"><span data-stu-id="79922-131">The Cluster Resource Manager disallows the creation of any new services within this application instance that would cause total load to exceed this value.</span></span> <span data-ttu-id="79922-132">例如，假設應用程式執行個體的容量為 10，而且已有五個負載。</span><span class="sxs-lookup"><span data-stu-id="79922-132">For example, let's say the application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="79922-133">不允許建立預設負載總計為 10 的服務。</span><span class="sxs-lookup"><span data-stu-id="79922-133">The creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="79922-134">**節點容量上限** – 這項設定指定在單一節點上的應用程式負載總計上限。</span><span class="sxs-lookup"><span data-stu-id="79922-134">**Maximum Node Capacity** – This setting specifies the maximum total load for the application on a single node.</span></span> <span data-ttu-id="79922-135">如果負載超過這個容量，叢集資源管理員會將複本移動到其他節點，使負載降低。</span><span class="sxs-lookup"><span data-stu-id="79922-135">If load goes over this capacity, the Cluster Resource Manager moves replicas to other nodes so that the load decreases.</span></span>


<span data-ttu-id="79922-136">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="79922-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="79922-137">C#：</span><span class="sxs-lookup"><span data-stu-id="79922-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="79922-138">保留容量</span><span class="sxs-lookup"><span data-stu-id="79922-138">Reserving Capacity</span></span>
<span data-ttu-id="79922-139">應用程式群組的另一個常見用途是確保叢集內的資源保留給指定的應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="79922-139">Another common use for application groups is to ensure that resources within the cluster are reserved for a given application instance.</span></span> <span data-ttu-id="79922-140">建立應用程式執行個體時，一定會保留空間。</span><span class="sxs-lookup"><span data-stu-id="79922-140">The space is always reserved when the application instance is created.</span></span>

<span data-ttu-id="79922-141">即使發生下列情況，也會立即為應用程式保留叢集中的空間：</span><span class="sxs-lookup"><span data-stu-id="79922-141">Reserving space in the cluster for the application happens immediately even when:</span></span>
- <span data-ttu-id="79922-142">應用程式執行個體已建立，但是其中尚無任何服務</span><span class="sxs-lookup"><span data-stu-id="79922-142">the application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="79922-143">每當變更應用程式執行個體中的服務數量時</span><span class="sxs-lookup"><span data-stu-id="79922-143">the number of services within the application instance changes every time</span></span> 
- <span data-ttu-id="79922-144">服務存在，但是不耗用資源</span><span class="sxs-lookup"><span data-stu-id="79922-144">the services exist but aren't consuming the resources</span></span> 

<span data-ttu-id="79922-145">保留應用程式執行個體的資源，需要指定兩個額外參數：*MinimumNodes* 和 *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="79922-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="79922-146">**MinimumNodes** - 定義應執行應用程式執行個體的節點數目下限。</span><span class="sxs-lookup"><span data-stu-id="79922-146">**MinimumNodes** - Defines the minimum number of nodes that the application instance should run on.</span></span>  
- <span data-ttu-id="79922-147">**NodeReservationCapacity** - 此設定是針對應用程式的計量。</span><span class="sxs-lookup"><span data-stu-id="79922-147">**NodeReservationCapacity** - This setting is per metric for the application.</span></span> <span data-ttu-id="79922-148">該值是在該應用程式中的服務執行的任何節點上，為該應用程式保留的計量數量。</span><span class="sxs-lookup"><span data-stu-id="79922-148">The value is the amount of that metric reserved for the application on any node where that the services in that application run.</span></span>

<span data-ttu-id="79922-149">結合 **MinimumNodes** 和 **NodeReservationCapacity** 可保證叢集中的應用程式獲得最小的負載保留。</span><span class="sxs-lookup"><span data-stu-id="79922-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for the application within the cluster.</span></span> <span data-ttu-id="79922-150">如果叢集中的剩餘容量小於所需的保留總量，則無法建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="79922-150">If there's less remaining capacity in the cluster than the total reservation required, creation of the application fails.</span></span> 

<span data-ttu-id="79922-151">讓我們看看容量保留的範例︰</span><span class="sxs-lookup"><span data-stu-id="79922-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="79922-152"><center>
![定義保留容量的應用程式執行個體][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="79922-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="79922-153">在左邊的範例中，應用程式並沒有定義任何應用程式容量。</span><span class="sxs-lookup"><span data-stu-id="79922-153">In the left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="79922-154">叢集資源管理員會根據一般規則來平衡一切事物。</span><span class="sxs-lookup"><span data-stu-id="79922-154">The Cluster Resource Manager balances everything according to normal rules.</span></span>

<span data-ttu-id="79922-155">在右邊範例中，假設以下列設定建立 Application1：</span><span class="sxs-lookup"><span data-stu-id="79922-155">In the example on the right, let's say that Application1 was created with the following settings:</span></span>

- <span data-ttu-id="79922-156">MinimumNodes 設為二</span><span class="sxs-lookup"><span data-stu-id="79922-156">MinimumNodes set to two</span></span>
- <span data-ttu-id="79922-157">應用程式計量定義下列值</span><span class="sxs-lookup"><span data-stu-id="79922-157">An application Metric defined with</span></span>
  - <span data-ttu-id="79922-158">NodeReservationCapacity 為 20</span><span class="sxs-lookup"><span data-stu-id="79922-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="79922-159">Powershell</span><span class="sxs-lookup"><span data-stu-id="79922-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="79922-160">C#</span><span class="sxs-lookup"><span data-stu-id="79922-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="79922-161">Service Fabric 為 Application1 保留了兩個節點上的容量，而且即使 Application1 內的服務當時並未耗用容量，也不允許 Application2 的服務耗用該容量。</span><span class="sxs-lookup"><span data-stu-id="79922-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 to consume that capacity even if there are no load is being consumed by the services inside Application1 at the time.</span></span> <span data-ttu-id="79922-162">保留的應用程式容量會被視為已耗用，且是取自該節點上和叢集內的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="79922-162">This reserved application capacity is considered consumed  and counts against the remaining capacity on that node and within the cluster.</span></span>  <span data-ttu-id="79922-163">保留的容量會立即從剩餘的叢集容量中扣除，但只有在至少一個服務物件置於節點上的情況下，才會從特定節點的容量中扣除保留的耗用量。</span><span class="sxs-lookup"><span data-stu-id="79922-163">The reservation is deducted from the remaining cluster capacity immediately, however the reserved consumption is deducted from the capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="79922-164">這後來的保留做法能夠更有彈性和更充分利用資源，因為只有在需要時才於節點上保留資源。</span><span class="sxs-lookup"><span data-stu-id="79922-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-the-application-load-information"></a><span data-ttu-id="79922-165">取得應用程式負載資訊</span><span class="sxs-lookup"><span data-stu-id="79922-165">Obtaining the application load information</span></span>
<span data-ttu-id="79922-166">若應用程式的「應用程式容量」由一個或多個計量定義，您可以從服務複本報告中取得每一個應用程式的彙總負載之相關資訊。</span><span class="sxs-lookup"><span data-stu-id="79922-166">For each application that has an Application Capacity defined for one or more metrics you can obtain the information about the aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="79922-167">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="79922-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="79922-168">C#</span><span class="sxs-lookup"><span data-stu-id="79922-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="79922-169">ApplicationLoad 查詢會傳回應用程式指定之「應用程式容量」的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="79922-169">The ApplicationLoad query returns the basic information about Application Capacity that was specified for the application.</span></span> <span data-ttu-id="79922-170">這項資訊包含「節點下限」和「節點上限」資訊，以及應用程式目前佔用的數目。</span><span class="sxs-lookup"><span data-stu-id="79922-170">This information includes the Minimum Nodes and Maximum Nodes info, and the number that the application is currently occupying.</span></span> <span data-ttu-id="79922-171">也包含每個應用程式負載計量的相關資訊，包括︰</span><span class="sxs-lookup"><span data-stu-id="79922-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="79922-172">度量名稱：度量的名稱。</span><span class="sxs-lookup"><span data-stu-id="79922-172">Metric Name: Name of the metric.</span></span>
* <span data-ttu-id="79922-173">保留容量：針對此應用程式保留在叢集中的叢集容量。</span><span class="sxs-lookup"><span data-stu-id="79922-173">Reservation Capacity: Cluster Capacity that is reserved in the cluster for this Application.</span></span>
* <span data-ttu-id="79922-174">應用程式負載︰此應用程式的子複本的總負載。</span><span class="sxs-lookup"><span data-stu-id="79922-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="79922-175">應用程式容量︰許可的應用程式負載值上限。</span><span class="sxs-lookup"><span data-stu-id="79922-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="79922-176">移除應用程式容量</span><span class="sxs-lookup"><span data-stu-id="79922-176">Removing Application Capacity</span></span>
<span data-ttu-id="79922-177">一旦針對應用程式設定應用程式容量參數，它們可以使用更新的應用程式 API 或 PowerShell Cmdlet 來移除。</span><span class="sxs-lookup"><span data-stu-id="79922-177">Once the Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="79922-178">例如：</span><span class="sxs-lookup"><span data-stu-id="79922-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="79922-179">此命令會從應用程式執行個體中移除所有「應用程式容量管理」參數，</span><span class="sxs-lookup"><span data-stu-id="79922-179">This command removes all Application capacity management parameters from the application instance.</span></span> <span data-ttu-id="79922-180">包括 MinimumNodes、MaximumNodes 和應用程式的度量 (如果有)。</span><span class="sxs-lookup"><span data-stu-id="79922-180">This includes MinimumNodes, MaximumNodes, and the Application's metrics, if any.</span></span> <span data-ttu-id="79922-181">此命令會立即生效。</span><span class="sxs-lookup"><span data-stu-id="79922-181">The effect of the command is immediate.</span></span> <span data-ttu-id="79922-182">此命令完成後，叢集資源管理員會使用預設行為來管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="79922-182">After this command completes, the Cluster Resource Manager uses the default behavior for managing applications.</span></span> <span data-ttu-id="79922-183">您可以透過 `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()` 再次指定「應用程式容量」參數。</span><span class="sxs-lookup"><span data-stu-id="79922-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="79922-184">應用程式容量的限制</span><span class="sxs-lookup"><span data-stu-id="79922-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="79922-185">應用程式容量參數有數個限制必須遵守。</span><span class="sxs-lookup"><span data-stu-id="79922-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="79922-186">如果發生驗證錯誤，則不會進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="79922-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="79922-187">所有整數參數必須為非負數。</span><span class="sxs-lookup"><span data-stu-id="79922-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="79922-188">MinimumNodes 不能大於 MaximumNodes。</span><span class="sxs-lookup"><span data-stu-id="79922-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="79922-189">如果已定義負載度量的容量，則它們必須遵守下列規則︰</span><span class="sxs-lookup"><span data-stu-id="79922-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="79922-190">節點保留容量不能大於節點容量上限。</span><span class="sxs-lookup"><span data-stu-id="79922-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="79922-191">例如，您不能在節點上將 “CPU” 計量的容量限制為兩個單位，卻嘗試在每個節點上保留三個單位。</span><span class="sxs-lookup"><span data-stu-id="79922-191">For example, you cannot limit the capacity for the metric “CPU” on the node to two units and try to reserve three units on each node.</span></span>
  - <span data-ttu-id="79922-192">如果已指定 MaximumNodes，則 MaximumNodes 和節點容量上限的乘積不能大於應用程式容量總計。</span><span class="sxs-lookup"><span data-stu-id="79922-192">If MaximumNodes is specified, then the product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="79922-193">例如，假設負載計量 “CPU” 的「節點容量上限」設定為八。</span><span class="sxs-lookup"><span data-stu-id="79922-193">For example, let's say the Maximum Node Capacity for load metric “CPU” is set to eight.</span></span> <span data-ttu-id="79922-194">另外也假設您將「節點上限」設定為 10。</span><span class="sxs-lookup"><span data-stu-id="79922-194">Let's also say you set the Maximum Nodes to 10.</span></span> <span data-ttu-id="79922-195">在此情況下，此負載計量的「應用程式容量總計」必須大於 80。</span><span class="sxs-lookup"><span data-stu-id="79922-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="79922-196">在應用程式建立及更新期間，都會強制執行限制。</span><span class="sxs-lookup"><span data-stu-id="79922-196">The restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-to-use-application-capacity"></a><span data-ttu-id="79922-197">如何不使用應用程式容量</span><span class="sxs-lookup"><span data-stu-id="79922-197">How not to use Application Capacity</span></span>
- <span data-ttu-id="79922-198">請勿嘗試使用「應用程式群組」功能將應用程式限制到「特定」的節點子集。</span><span class="sxs-lookup"><span data-stu-id="79922-198">Do not try to use the Application Group features to constrain the application to a _specific_ subset of nodes.</span></span> <span data-ttu-id="79922-199">換句話說，您可以指定最多在五個節點上執行應用程式，但無法指定叢集中的哪五個特定節點。</span><span class="sxs-lookup"><span data-stu-id="79922-199">In other words, you can specify that the application runs on at most five nodes, but not which specific five nodes in the cluster.</span></span> <span data-ttu-id="79922-200">您可以使用服務的放置條件約束，將應用程式限制到特定節點。</span><span class="sxs-lookup"><span data-stu-id="79922-200">Constraining an application to specific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="79922-201">請勿使用「應用程式容量」來確保相同應用程式的兩個服務放在相同的節點上。</span><span class="sxs-lookup"><span data-stu-id="79922-201">Do not try to use the Application Capacity to ensure that two services from the same application are placed on the same nodes.</span></span> <span data-ttu-id="79922-202">請改用[親和性](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)或[放置條件約束](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)。</span><span class="sxs-lookup"><span data-stu-id="79922-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="79922-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="79922-203">Next steps</span></span>
- <span data-ttu-id="79922-204">如需服務設定的詳細資訊，請[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="79922-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="79922-205">若要了解叢集資源管理員如何管理並平衡叢集中的負載，請查看關於 [平衡負載](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="79922-205">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="79922-206">從頭開始，並 [取得 Service Fabric 叢集 Resource Manager 的簡介](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="79922-206">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="79922-207">如需度量通常如何運作的詳細資訊，請繼續閱讀 [Service Fabric 負載度量](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="79922-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="79922-208">叢集資源管理員有許多描述叢集的選項。</span><span class="sxs-lookup"><span data-stu-id="79922-208">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="79922-209">若要深入了解這些選項，請參閱關於[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)一文</span><span class="sxs-lookup"><span data-stu-id="79922-209">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
