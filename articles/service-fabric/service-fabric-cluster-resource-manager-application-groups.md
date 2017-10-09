---
title: "aaaService 網狀架構叢集資源管理員的應用程式群組 |Microsoft 文件"
description: "Hello hello Service Fabric 叢集資源管理員中的應用程式群組功能的概觀"
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
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="d9cb2-103">簡介 tooApplication 群組</span><span class="sxs-lookup"><span data-stu-id="d9cb2-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="d9cb2-104">透過將 hello 負載分散到 Service Fabric 叢集資源管理員通常管理的叢集資源 (透過下列方式表示[度量](service-fabric-cluster-resource-manager-metrics.md)) 平均分散整個 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="d9cb2-105">Service Fabric 管理透過整個 hello 叢集和叢集 hello hello 節點 hello 容量[容量](service-fabric-cluster-resource-manager-cluster-description.md)。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="d9cb2-106">計量和容量很適用於許多工作負載，但過度使用不同 Service Fabric 應用程式執行個體的模式，有時會引起其他需求。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="d9cb2-107">例如，您可能想要：</span><span class="sxs-lookup"><span data-stu-id="d9cb2-107">For example you may want to:</span></span>

- <span data-ttu-id="d9cb2-108">保留某些具名的應用程式執行個體中的 hello 服務 hello hello 叢集中節點上某些容量</span><span class="sxs-lookup"><span data-stu-id="d9cb2-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="d9cb2-109">限制具名的應用程式執行個體中的 hello 服務執行 （而不是散佈它們 hello 整個叢集） 的節點 hello 的總數</span><span class="sxs-lookup"><span data-stu-id="d9cb2-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="d9cb2-110">定義本身 hello 具名的應用程式執行個體上的內文中的 hello 服務的服務或總共資源耗用量 toolimit hello 數目的容量</span><span class="sxs-lookup"><span data-stu-id="d9cb2-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="d9cb2-111">toomeet 這些需求，hello Service Fabric 叢集資源管理員支援稱為應用程式群組的功能。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="d9cb2-112">限制 hello 的節點數上限</span><span class="sxs-lookup"><span data-stu-id="d9cb2-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="d9cb2-113">應用程式容量 hello 簡單使用案例是當應用程式執行個體需要 toobe 有限 tooa 特定節點的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="d9cb2-114">這會將該應用程式執行個體中的所有服務合併到固定數目的機器上。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="d9cb2-115">彙總時，您在繼續努力 toopredict 或限制該具名的應用程式執行個體中的 hello 服務在實體資源使用。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="d9cb2-116">hello 下列影像顯示應用程式執行個體逾時或無定義的節點數目上限：</span><span class="sxs-lookup"><span data-stu-id="d9cb2-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="d9cb2-117"><center>
![定義節點數目上限的應用程式執行個體][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="d9cb2-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="d9cb2-118">在 hello 左範例中，hello 應用程式沒有定義的節點數目上限，它有三種服務。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="d9cb2-119">hello 叢集資源管理員具有所有複本都擴展到六個可用的節點 tooachieve hello 最佳平衡 hello 叢集中 （hello 預設行為）。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="d9cb2-120">在 hello 右範例中，我們看到 hello 相同的應用程式限制 toothree 節點。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="d9cb2-121">hello 參數，可控制這個行為稱為 MaximumNodes。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="d9cb2-122">您可以在應用程式建立期間設定這個參數，也可以針對執行中的應用程式執行個體更新這個參數。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="d9cb2-123">Powershell</span><span class="sxs-lookup"><span data-stu-id="d9cb2-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="d9cb2-124">C#</span><span class="sxs-lookup"><span data-stu-id="d9cb2-124">C#</span></span>

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

<span data-ttu-id="d9cb2-125">Hello 集中的節點，hello 叢集資源管理員並不保證哪一個服務物件取得放置在一起，或使用哪些節點取得。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="d9cb2-126">應用程式度量、負載和容量</span><span class="sxs-lookup"><span data-stu-id="d9cb2-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="d9cb2-127">應用程式群組也可讓您指定具名的應用程式執行個體和該應用程式執行個體的容量的這些度量資訊與相關聯的 toodefine 標準。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="d9cb2-128">應用程式計量可讓您 tootrack、 保留，並限制 hello 服務該應用程式執行個體中的 hello 資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="d9cb2-129">每一個應用程式計量可以設定兩個值︰</span><span class="sxs-lookup"><span data-stu-id="d9cb2-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="d9cb2-130">**應用程式容量總計**– 這項設定代表 hello 的特定度量的 hello 應用程式的總容量。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="d9cb2-131">hello 叢集資源管理員不允許任何新的服務會導致此值總負載 tooexceed 這個應用程式執行個體中的 hello 的建立。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="d9cb2-132">例如，假設 hello 應用程式執行個體具有 10 個的容量，並已經有五個的負載。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="d9cb2-133">會允許服務與 10 的總預設負載 hello 建立。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="d9cb2-134">**最大節點容量**– 此設定可指定 hello 的最大總載入 hello 應用程式的單一節點上。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="d9cb2-135">如果負載是經過這個容量，hello 叢集資源管理員會移動複本 tooother 節點，使 hello 負載降低。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="d9cb2-136">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="d9cb2-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="d9cb2-137">C#：</span><span class="sxs-lookup"><span data-stu-id="d9cb2-137">C#:</span></span>

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

## <a name="reserving-capacity"></a><span data-ttu-id="d9cb2-138">保留容量</span><span class="sxs-lookup"><span data-stu-id="d9cb2-138">Reserving Capacity</span></span>
<span data-ttu-id="d9cb2-139">應用程式群組的另一個常見用途是 tooensure 內資源 hello 叢集保留給指定的應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="d9cb2-140">建立 hello 應用程式執行個體時，一定會保留 hello 空格。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="d9cb2-141">保留 hello 叢集中的空間，如 hello 應用程式事件會立即發生，即使：</span><span class="sxs-lookup"><span data-stu-id="d9cb2-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="d9cb2-142">hello 應用程式執行個體建立，但沒有任何服務中</span><span class="sxs-lookup"><span data-stu-id="d9cb2-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="d9cb2-143">每次變更服務 hello 應用程式執行個體中的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="d9cb2-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="d9cb2-144">hello 服務存在但不耗用 hello 資源</span><span class="sxs-lookup"><span data-stu-id="d9cb2-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="d9cb2-145">保留應用程式執行個體的資源，需要指定兩個額外參數：*MinimumNodes* 和 *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="d9cb2-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="d9cb2-146">**MinimumNodes** -定義 hello 最小數目的 hello 應用程式的節點執行個體應該在上執行。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="d9cb2-147">**NodeReservationCapacity** -此設定是每個計量 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="d9cb2-148">hello 值為 hello 數量保留給 hello 應用程式，其中的 hello 服務執行該應用程式中的任何節點上的度量。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="d9cb2-149">結合**MinimumNodes**和**NodeReservationCapacity**保證 hello hello 叢集內的應用程式的最小的負載保留項目。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="d9cb2-150">如果有較少的剩餘容量 hello 叢集比 hello 所需的總保留時，建立 hello 應用程式失敗。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="d9cb2-151">讓我們看看容量保留的範例︰</span><span class="sxs-lookup"><span data-stu-id="d9cb2-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="d9cb2-152"><center>
![定義保留容量的應用程式執行個體][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="d9cb2-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="d9cb2-153">在 hello 左範例中，應用程式沒有定義任何應用程式容量。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="d9cb2-154">hello 叢集資源管理員之間取得平衡，根據 toonormal 規則的所有項目。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="d9cb2-155">在右 hello 上 hello 範例中，假設 Application1 已建立以 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="d9cb2-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="d9cb2-156">MinimumNodes 設定 tootwo</span><span class="sxs-lookup"><span data-stu-id="d9cb2-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="d9cb2-157">應用程式計量定義下列值</span><span class="sxs-lookup"><span data-stu-id="d9cb2-157">An application Metric defined with</span></span>
  - <span data-ttu-id="d9cb2-158">NodeReservationCapacity 為 20</span><span class="sxs-lookup"><span data-stu-id="d9cb2-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="d9cb2-159">Powershell</span><span class="sxs-lookup"><span data-stu-id="d9cb2-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="d9cb2-160">C#</span><span class="sxs-lookup"><span data-stu-id="d9cb2-160">C#</span></span>

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

<span data-ttu-id="d9cb2-161">Service Fabric Application1，保留兩個節點上的容量，並不允許從 Application2 tooconsume 服務該容量即使沒有任何負載所耗用的 hello 服務內 Application1 hello 次。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="d9cb2-162">這個保留的應用程式的功能會被視為耗用，而且不利於 hello 剩餘容量該節點上並 hello 叢集內。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="d9cb2-163">hello 保留扣除 hello 立即剩餘叢集容量，只有在至少一個服務物件置於其上時，不過 hello 保留要耗用量扣除從特定節點的 hello 容量。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="d9cb2-164">這後來的保留做法能夠更有彈性和更充分利用資源，因為只有在需要時才於節點上保留資源。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="d9cb2-165">取得 hello 應用程式載入資訊</span><span class="sxs-lookup"><span data-stu-id="d9cb2-165">Obtaining hello application load information</span></span>
<span data-ttu-id="d9cb2-166">每個應用程式具有一個或多個度量定義應用程式容量，您可以取得 hello hello 彙總載入複本的服務所報告的資訊。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="d9cb2-167">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="d9cb2-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="d9cb2-168">C#</span><span class="sxs-lookup"><span data-stu-id="d9cb2-168">C#</span></span>

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

<span data-ttu-id="d9cb2-169">hello ApplicationLoad 查詢會傳回有關 hello 應用程式所指定的應用程式容量的 hello 基本資訊。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="d9cb2-170">此資訊包括 hello 節點最小值和最大節點資訊，以及目前佔用 hello 應用程式的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="d9cb2-171">也包含每個應用程式負載計量的相關資訊，包括︰</span><span class="sxs-lookup"><span data-stu-id="d9cb2-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="d9cb2-172">度量的名稱： Hello 度量的名稱。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="d9cb2-173">此應用程式保留 hello 叢集中的保留容量： 叢集容量。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="d9cb2-174">應用程式負載︰此應用程式的子複本的總負載。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="d9cb2-175">應用程式容量︰許可的應用程式負載值上限。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="d9cb2-176">移除應用程式容量</span><span class="sxs-lookup"><span data-stu-id="d9cb2-176">Removing Application Capacity</span></span>
<span data-ttu-id="d9cb2-177">一旦應用程式設定 hello 應用程式容量參數之後，他們可以使用更新應用程式的 Api 或 PowerShell 指令程式來移除。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="d9cb2-178">例如：</span><span class="sxs-lookup"><span data-stu-id="d9cb2-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="d9cb2-179">此命令會移除 hello 應用程式執行個體中的所有應用程式容量管理參數。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="d9cb2-180">這包括 MinimumNodes、 MaximumNodes 和 hello 應用程式的度量，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="d9cb2-181">hello 影響 hello 命令是即時的。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="d9cb2-182">此命令完成之後，hello 叢集資源管理員會管理應用程式使用 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="d9cb2-183">您可以透過 `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()` 再次指定「應用程式容量」參數。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="d9cb2-184">應用程式容量的限制</span><span class="sxs-lookup"><span data-stu-id="d9cb2-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="d9cb2-185">應用程式容量參數有數個限制必須遵守。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="d9cb2-186">如果發生驗證錯誤，則不會進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="d9cb2-187">所有整數參數必須為非負數。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="d9cb2-188">MinimumNodes 不能大於 MaximumNodes。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="d9cb2-189">如果已定義負載度量的容量，則它們必須遵守下列規則︰</span><span class="sxs-lookup"><span data-stu-id="d9cb2-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="d9cb2-190">節點保留容量不能大於節點容量上限。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="d9cb2-191">例如，您無法限制 hello 度量"CPU"hello 節點 tootwo 單元上的 hello 容量，然後再次嘗試 tooreserve 三個單位，每個節點上。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="d9cb2-192">如果指定 MaximumNodes，然後 MaximumNodes 和最大節點容量 hello 產品不能大於應用程式容量總計。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="d9cb2-193">例如，假設 hello，"CPU"設定 tooeight 負載度量的最大節點容量。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="d9cb2-194">我們也假設您設定最大節點 too10 hello。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="d9cb2-195">在此情況下，此負載計量的「應用程式容量總計」必須大於 80。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="d9cb2-196">同時在應用程式建立及更新期間，都會強制執行 hello 限制。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="d9cb2-197">如何 toouse 應用程式容量</span><span class="sxs-lookup"><span data-stu-id="d9cb2-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="d9cb2-198">請勿嘗試 toouse hello 應用程式群組功能 tooconstrain hello 應用程式 tooa_特定_節點的子集。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="d9cb2-199">換句話說，您可以指定 hello 應用程式執行最多五個節點上，但不是哪些特定五個叢集中的節點 hello。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="d9cb2-200">限制應用程式 toospecific 節點可以達成服務的使用位置條件約束。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="d9cb2-201">請勿嘗試 toouse hello 應用程式容量 tooensure hello 置於相同的應用程式從兩個服務 hello 相同節點。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="d9cb2-202">請改用[親和性](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)或[放置條件約束](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9cb2-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9cb2-203">Next steps</span></span>
- <span data-ttu-id="d9cb2-204">如需服務設定的詳細資訊，請[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="d9cb2-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="d9cb2-205">toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="d9cb2-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="d9cb2-206">Hello 從頭開始並[取得簡介 toohello Service Fabric 叢集資源管理員](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="d9cb2-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="d9cb2-207">如需度量通常如何運作的詳細資訊，請繼續閱讀 [Service Fabric 負載度量](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="d9cb2-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="d9cb2-208">hello 叢集資源管理員有許多選擇可用來描述 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="d9cb2-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="d9cb2-209">toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="d9cb2-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
