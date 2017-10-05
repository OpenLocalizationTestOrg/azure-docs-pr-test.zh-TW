---
title: "平衡 Azure Service Fabric 叢集 | Microsoft Docs"
description: "使用 Azure Service Fabric 叢集資源管理員平衡叢集的簡介。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="9cc45-103">平衡 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="9cc45-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="9cc45-104">「Service Fabric 叢集資源管理員」支援動態負載變更、因應節點或服務的新增或移除。</span><span class="sxs-lookup"><span data-stu-id="9cc45-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="9cc45-105">它也會自動修正條件約束違規，以及主動重新平衡叢集。</span><span class="sxs-lookup"><span data-stu-id="9cc45-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="9cc45-106">但是這些動作執行的頻率，以及觸發它們的項目是什麼？</span><span class="sxs-lookup"><span data-stu-id="9cc45-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="9cc45-107">叢集資源管理員所執行的工作有三個不同的類別。</span><span class="sxs-lookup"><span data-stu-id="9cc45-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="9cc45-108">如下：</span><span class="sxs-lookup"><span data-stu-id="9cc45-108">They are:</span></span>

1. <span data-ttu-id="9cc45-109">放置 - 這個階段涉及安置任何遺漏的具狀態複本或無狀態執行個體。</span><span class="sxs-lookup"><span data-stu-id="9cc45-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="9cc45-110">放置包含新服務，也包含處理已失敗的具狀態複本或無狀態執行個體。</span><span class="sxs-lookup"><span data-stu-id="9cc45-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="9cc45-111">刪除和捨棄複本或執行個體都是在這裡處理。</span><span class="sxs-lookup"><span data-stu-id="9cc45-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="9cc45-112">條件約束檢查 – 這個階段會檢查並更正系統內不同放置條件約束 (規則) 的違規情形。</span><span class="sxs-lookup"><span data-stu-id="9cc45-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="9cc45-113">規則範例包括像是確保節點不超出容量，以及符合服務的放置條件約束。</span><span class="sxs-lookup"><span data-stu-id="9cc45-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="9cc45-114">平衡 - 這個階段會根據為不同計量設定的所需平衡層級，查看是否有必要使用重新平衡。</span><span class="sxs-lookup"><span data-stu-id="9cc45-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="9cc45-115">如果有必要，就會嘗試在叢集中尋找更平衡的安排方式。</span><span class="sxs-lookup"><span data-stu-id="9cc45-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="9cc45-116">設定叢集資源管理員計時器</span><span class="sxs-lookup"><span data-stu-id="9cc45-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="9cc45-117">與平衡相關的第一組控制項是一組計時器。</span><span class="sxs-lookup"><span data-stu-id="9cc45-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="9cc45-118">這些計時器控管叢集資源管理員檢查叢集並且採取矯正措施的頻率。</span><span class="sxs-lookup"><span data-stu-id="9cc45-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="9cc45-119">「叢集資源管理員」可執行的每個不同類型修正，都是由控管其頻率的不同計時器所控制。</span><span class="sxs-lookup"><span data-stu-id="9cc45-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="9cc45-120">當每個計時器啟動時，便會排程工作。</span><span class="sxs-lookup"><span data-stu-id="9cc45-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="9cc45-121">根據預設，Resource Manager 會：</span><span class="sxs-lookup"><span data-stu-id="9cc45-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="9cc45-122">每 1/10 秒掃描一次其狀態並套用更新 (例如記錄某個節點已關閉)</span><span class="sxs-lookup"><span data-stu-id="9cc45-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="9cc45-123">設定放置檢查旗標</span><span class="sxs-lookup"><span data-stu-id="9cc45-123">sets the placement check flag</span></span> 
* <span data-ttu-id="9cc45-124">設定每秒條件約束檢查旗標</span><span class="sxs-lookup"><span data-stu-id="9cc45-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="9cc45-125">每 5 秒設定一次平衡旗標。</span><span class="sxs-lookup"><span data-stu-id="9cc45-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="9cc45-126">控管這些計時器的設定範例如下：</span><span class="sxs-lookup"><span data-stu-id="9cc45-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="9cc45-127">ClusterManifest.xml：</span><span class="sxs-lookup"><span data-stu-id="9cc45-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="9cc45-128">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="9cc45-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="9cc45-129">目前「叢集資源管理員」只會依序一次執行這些動作其中之一。</span><span class="sxs-lookup"><span data-stu-id="9cc45-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="9cc45-130">這就是為什麼我們將這些計時器稱為「最小間隔」，計時器關閉時所採取的動作稱為「設定旗標」。</span><span class="sxs-lookup"><span data-stu-id="9cc45-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="9cc45-131">例如，「叢集資源管理員」在平衡叢集之前，會先處理要建立服務的擱置中要求。</span><span class="sxs-lookup"><span data-stu-id="9cc45-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="9cc45-132">如您所見，「叢集資源管理員」會依據指定的預設時間間隔，掃描它需要經常執行的一切項目。</span><span class="sxs-lookup"><span data-stu-id="9cc45-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="9cc45-133">通常這表示在每個步驟所做的一組變更通常很小。</span><span class="sxs-lookup"><span data-stu-id="9cc45-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="9cc45-134">經常進行少量變更可讓「叢集資源管理員」快速因應叢集中發生的情況。</span><span class="sxs-lookup"><span data-stu-id="9cc45-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="9cc45-135">由於許多相同類型的事件易於同時發生，因此預設計時器提供一些批次處理。</span><span class="sxs-lookup"><span data-stu-id="9cc45-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="9cc45-136">例如，當節點失敗時，他們可以一次對整個容錯網域執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="9cc45-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="9cc45-137">所有失敗會在 *PLBRefreshGap* 之後的下一個狀態更新期間擷取。</span><span class="sxs-lookup"><span data-stu-id="9cc45-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="9cc45-138">更正會在下列位置、條件約束檢查以及平衡執行期間決定。</span><span class="sxs-lookup"><span data-stu-id="9cc45-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="9cc45-139">「叢集資源管理員」預設不會將叢集中數小時的變更整個掃描一遍，然後嘗試一次處理所有變更。</span><span class="sxs-lookup"><span data-stu-id="9cc45-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="9cc45-140">這麼做會導致變換量激增。</span><span class="sxs-lookup"><span data-stu-id="9cc45-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="9cc45-141">「叢集資源管理員」也需要一些其他資訊，才能判斷叢集是否處於不平衡的狀態。</span><span class="sxs-lookup"><span data-stu-id="9cc45-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="9cc45-142">因此，我們有其他兩個的設定︰「平衡臨界值」和「活動臨界值」。</span><span class="sxs-lookup"><span data-stu-id="9cc45-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="9cc45-143">平衡臨界值</span><span class="sxs-lookup"><span data-stu-id="9cc45-143">Balancing thresholds</span></span>
<span data-ttu-id="9cc45-144">平衡臨界值是觸發重新平衡的主要控制項。</span><span class="sxs-lookup"><span data-stu-id="9cc45-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="9cc45-145">計量的平衡臨界值是一個_比率_。</span><span class="sxs-lookup"><span data-stu-id="9cc45-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="9cc45-146">如果負載最多之節點的計量負載除以負載最少之節點的負載量超過該計量的*平衡臨界值*，此叢集就會被視為不平衡。</span><span class="sxs-lookup"><span data-stu-id="9cc45-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="9cc45-147">因此，下一次「叢集資源管理員」進行檢查時，就會觸發平衡作業。</span><span class="sxs-lookup"><span data-stu-id="9cc45-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="9cc45-148">MinLoadBalancingInterval 計時器會定義當需要重新平衡時，「叢集資源管理員」的檢查頻率。</span><span class="sxs-lookup"><span data-stu-id="9cc45-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="9cc45-149">檢查並不意謂著有發生任何事情。</span><span class="sxs-lookup"><span data-stu-id="9cc45-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="9cc45-150">平衡臨界值會根據每個度量定義為叢集定義的一部分。</span><span class="sxs-lookup"><span data-stu-id="9cc45-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="9cc45-151">如需有關計量的詳細資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="9cc45-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="9cc45-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="9cc45-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="9cc45-153">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="9cc45-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="9cc45-154"><center>
![平衡臨界值範例][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="9cc45-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="9cc45-155">在此範例中，每個服務皆取用一單位的某個計量。</span><span class="sxs-lookup"><span data-stu-id="9cc45-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="9cc45-156">在上半部的範例中，節點的負載上限為 5，而下限為 2。</span><span class="sxs-lookup"><span data-stu-id="9cc45-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="9cc45-157">假設此計量的平衡臨界值為 3。</span><span class="sxs-lookup"><span data-stu-id="9cc45-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="9cc45-158">由於叢集中的比率是 5/2 = 2.5，小於指定的平衡臨界值 3，因此叢集處於平衡狀態。</span><span class="sxs-lookup"><span data-stu-id="9cc45-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="9cc45-159">當「叢集資源管理員」進行檢查時，不會觸發任何平衡作業。</span><span class="sxs-lookup"><span data-stu-id="9cc45-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="9cc45-160">在下半部的範例中，節點的負載上限為 10，而下限為 2，所以比率為 5。</span><span class="sxs-lookup"><span data-stu-id="9cc45-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="9cc45-161">5 大於該計量的指定平衡臨界值 3。</span><span class="sxs-lookup"><span data-stu-id="9cc45-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="9cc45-162">因此，下一次引發平衡計時器時，便會排定執行重新平衡。</span><span class="sxs-lookup"><span data-stu-id="9cc45-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="9cc45-163">在類似這樣的情況中，有些負載通常會分散到 Node3。</span><span class="sxs-lookup"><span data-stu-id="9cc45-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="9cc45-164">由於「Service Fabric 叢集資源管理員」並不使用窮盡方法，因此有些負載也可能分散到 Node2。</span><span class="sxs-lookup"><span data-stu-id="9cc45-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="9cc45-165"><center>
![平衡臨界值範例動作][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="9cc45-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="9cc45-166">「平衡」會處理兩個不同的策略來管理叢集中的負載。</span><span class="sxs-lookup"><span data-stu-id="9cc45-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="9cc45-167">叢集資源管理員使用的預設策略是在叢集的節點之間分散負載。</span><span class="sxs-lookup"><span data-stu-id="9cc45-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="9cc45-168">其他的策略是[重組](service-fabric-cluster-resource-manager-defragmentation-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="9cc45-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="9cc45-169">重組是在相同平衡執行期間執行。</span><span class="sxs-lookup"><span data-stu-id="9cc45-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="9cc45-170">平衡和重組策略可以用於相同叢集中不同的計量。</span><span class="sxs-lookup"><span data-stu-id="9cc45-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="9cc45-171">服務可以同時有平衡和重組計量。</span><span class="sxs-lookup"><span data-stu-id="9cc45-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="9cc45-172">對於重組計量，當叢集中的負載比率_低於_平衡臨界值時，會觸發重新平衡。</span><span class="sxs-lookup"><span data-stu-id="9cc45-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="9cc45-173">使數據低於平衡臨界值並不是一個明確的目標。</span><span class="sxs-lookup"><span data-stu-id="9cc45-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="9cc45-174">平衡臨界值只是*觸發程序*。</span><span class="sxs-lookup"><span data-stu-id="9cc45-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="9cc45-175">當平衡執行時，叢集資源管理員會判斷可以進行哪些增強功能，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="9cc45-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="9cc45-176">因為平衡搜尋開始並不代表任何項目移動。</span><span class="sxs-lookup"><span data-stu-id="9cc45-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="9cc45-177">有時候叢集過於受到修正的限制而不平衡。</span><span class="sxs-lookup"><span data-stu-id="9cc45-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="9cc45-178">或者，改進需要的移動太[昂貴](service-fabric-cluster-resource-manager-movement-cost.md))。</span><span class="sxs-lookup"><span data-stu-id="9cc45-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="9cc45-179">活動臨界值</span><span class="sxs-lookup"><span data-stu-id="9cc45-179">Activity thresholds</span></span>
<span data-ttu-id="9cc45-180">有時候，雖然節點處於相對的不平衡狀態，但叢集中的負載「總量」  卻很低。</span><span class="sxs-lookup"><span data-stu-id="9cc45-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="9cc45-181">缺乏負載可能是暫時性的下跌情況，或是因為叢集是新的且才剛啟動而已。</span><span class="sxs-lookup"><span data-stu-id="9cc45-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="9cc45-182">不論是上述哪一種情況，您可能都不想花時間平衡叢集，因為能獲得的好處很少。</span><span class="sxs-lookup"><span data-stu-id="9cc45-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="9cc45-183">如果叢集進行平衡作業，您將需要花費網路和計算資源將東西四處移動，但卻不會產生任何大型的「絕對」差異。</span><span class="sxs-lookup"><span data-stu-id="9cc45-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="9cc45-184">為了避免不必要的移動，出現了另一種控制方式，稱為「活動臨界值」。</span><span class="sxs-lookup"><span data-stu-id="9cc45-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="9cc45-185">「活動臨界值」可讓您為活動指定某種絕對下限。</span><span class="sxs-lookup"><span data-stu-id="9cc45-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="9cc45-186">如果沒有任何節點超出此臨界值，則即使達到「平衡臨界值」，也不會觸發平衡作業。</span><span class="sxs-lookup"><span data-stu-id="9cc45-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="9cc45-187">假設我們為這個計量保留平衡臨界值 3。</span><span class="sxs-lookup"><span data-stu-id="9cc45-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="9cc45-188">同時假設我們有活動臨界值 1536。</span><span class="sxs-lookup"><span data-stu-id="9cc45-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="9cc45-189">在第一個案例中，根據「平衡臨界值」，叢集是處於不平衡狀態，但沒有任何節點達到「活動臨界值」，因此不會發生任何事情。</span><span class="sxs-lookup"><span data-stu-id="9cc45-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="9cc45-190">在下半部的範例中，Node1 超出「活動臨界值」。</span><span class="sxs-lookup"><span data-stu-id="9cc45-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="9cc45-191">由於同時超出該計量的「平衡臨界值」和「活動臨界值」，因此會排定平衡作業。</span><span class="sxs-lookup"><span data-stu-id="9cc45-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="9cc45-192">讓我們看看下圖的範例：</span><span class="sxs-lookup"><span data-stu-id="9cc45-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="9cc45-193"><center>
![活動臨界值範例][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="9cc45-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="9cc45-194">如同平衡臨界值，活動臨界值會透過叢集定義根據每個度量進行定義︰</span><span class="sxs-lookup"><span data-stu-id="9cc45-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="9cc45-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="9cc45-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="9cc45-196">透過 ClusterConfig.json (適用於獨立部署) 或 Template.json (適用於 Azure 裝載的叢集)：</span><span class="sxs-lookup"><span data-stu-id="9cc45-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="9cc45-197">平衡臨界值和活動臨界值都與特定計量繫結 - 只有同時超出同一計量的「平衡臨界值」和「活動臨界值」時，才會觸發平衡作業。</span><span class="sxs-lookup"><span data-stu-id="9cc45-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="9cc45-198">一起平衡服務</span><span class="sxs-lookup"><span data-stu-id="9cc45-198">Balancing services together</span></span>
<span data-ttu-id="9cc45-199">叢集是否不平衡牽涉到整個叢集的決策。</span><span class="sxs-lookup"><span data-stu-id="9cc45-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="9cc45-200">不過，我們修正此種情況的方法是將個別的服務複本和執行個體四處移動。</span><span class="sxs-lookup"><span data-stu-id="9cc45-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="9cc45-201">這很合理，對吧？</span><span class="sxs-lookup"><span data-stu-id="9cc45-201">This makes sense, right?</span></span> <span data-ttu-id="9cc45-202">如果記憶體堆疊在某一個節點上，可能是由多個複本或執行個體所造成。</span><span class="sxs-lookup"><span data-stu-id="9cc45-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="9cc45-203">若要修正不平衡的狀態，可能需要移動所有使用不平衡計量的具狀態複本或無狀態執行個體。</span><span class="sxs-lookup"><span data-stu-id="9cc45-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="9cc45-204">有時候本身並非不平衡的服務會被移動 (請記住稍早關於邏輯和全域加權的討論)。</span><span class="sxs-lookup"><span data-stu-id="9cc45-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="9cc45-205">為什麼當服務的計量平衡時服務會移動？</span><span class="sxs-lookup"><span data-stu-id="9cc45-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="9cc45-206">看看以下範例：</span><span class="sxs-lookup"><span data-stu-id="9cc45-206">Let’s see an example:</span></span>

- <span data-ttu-id="9cc45-207">假設有四個服務：Service1、Service2、Service3 及 Service4。</span><span class="sxs-lookup"><span data-stu-id="9cc45-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="9cc45-208">Service1 報告計量 Metric1 和 Metric2。</span><span class="sxs-lookup"><span data-stu-id="9cc45-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="9cc45-209">Service2 報告計量 Metric2 和 Metric3。</span><span class="sxs-lookup"><span data-stu-id="9cc45-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="9cc45-210">Service3 報告計量 Metric3 和 Metric4。</span><span class="sxs-lookup"><span data-stu-id="9cc45-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="9cc45-211">Service4 報告計量 Metric99。</span><span class="sxs-lookup"><span data-stu-id="9cc45-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="9cc45-212">您應該可以看出這個範例要表達什麼：有鏈結！</span><span class="sxs-lookup"><span data-stu-id="9cc45-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="9cc45-213">我們並非實際上擁有 4 個獨立的服務，而是有 3 個相關的服務，以及一個獨立的服務。</span><span class="sxs-lookup"><span data-stu-id="9cc45-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="9cc45-214"><center>
![將服務一起平衡][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="9cc45-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="9cc45-215">因為這個鏈結，所以計量 1-4 若發生不平衡，可能會導致屬於服務 1-3 的複本或執行個體四處移動。</span><span class="sxs-lookup"><span data-stu-id="9cc45-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="9cc45-216">我們也知道計量 1、2 或 3 若發生不平衡，並不會導致 Service4 中發生移動。</span><span class="sxs-lookup"><span data-stu-id="9cc45-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="9cc45-217">這麼做並沒有必要，因為將屬於 Service4 的複本或執行個體四處移動完全不會影響計量 1-3 的平衡。</span><span class="sxs-lookup"><span data-stu-id="9cc45-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="9cc45-218">叢集資源管理員會自動找出相關的服務。</span><span class="sxs-lookup"><span data-stu-id="9cc45-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="9cc45-219">新增、移除或變更服務的計量，可能會影響它們的關聯性。</span><span class="sxs-lookup"><span data-stu-id="9cc45-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="9cc45-220">例如，在兩次執行平衡作業之間，可能已經更新 Service2 來移除 Metric2。</span><span class="sxs-lookup"><span data-stu-id="9cc45-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="9cc45-221">這會中斷 Service1 和 Service2 之間的鏈結。</span><span class="sxs-lookup"><span data-stu-id="9cc45-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="9cc45-222">現在，您擁有的是三個相關服務群組，而非兩個︰</span><span class="sxs-lookup"><span data-stu-id="9cc45-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="9cc45-223"><center>
![將服務一起平衡][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="9cc45-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc45-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9cc45-224">Next steps</span></span>
* <span data-ttu-id="9cc45-225">度量是 Service Fabric 叢集資源管理員管理叢集中的耗用量和容量的方式。</span><span class="sxs-lookup"><span data-stu-id="9cc45-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="9cc45-226">若要深入了解計量及其設定方式，請查看[這篇文章](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="9cc45-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="9cc45-227">移動成本是向叢集資源管理員發出訊號，表示移動某些服務會比較貴的其中一種方式。</span><span class="sxs-lookup"><span data-stu-id="9cc45-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="9cc45-228">如需有關移動成本的詳細資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="9cc45-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="9cc45-229">叢集資源管理員有數個為減緩叢集的流失而可以設定的節流。</span><span class="sxs-lookup"><span data-stu-id="9cc45-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="9cc45-230">這些節流通常不是必要的，但若有需要，您可以參閱 [這裡](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="9cc45-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
