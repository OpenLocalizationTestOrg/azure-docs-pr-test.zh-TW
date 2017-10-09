---
title: "aaaBalance Azure Service Fabric 叢集 |Microsoft 文件"
description: "簡介 toobalancing hello Service Fabric 叢集資源管理員與您的叢集。"
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
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="44a86-103">平衡 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="44a86-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="44a86-104">hello Service Fabric 叢集資源管理員支援動態負載變更，對回應 tooadditions 或移除的節點或服務。</span><span class="sxs-lookup"><span data-stu-id="44a86-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="44a86-105">它也會自動更正條件約束違規，並主動重新平衡 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="44a86-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="44a86-106">但是這些動作執行的頻率，以及觸發它們的項目是什麼？</span><span class="sxs-lookup"><span data-stu-id="44a86-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="44a86-107">叢集資源管理員會執行該 hello 有三種不同的工作。</span><span class="sxs-lookup"><span data-stu-id="44a86-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="44a86-108">如下：</span><span class="sxs-lookup"><span data-stu-id="44a86-108">They are:</span></span>

1. <span data-ttu-id="44a86-109">放置 - 這個階段涉及安置任何遺漏的具狀態複本或無狀態執行個體。</span><span class="sxs-lookup"><span data-stu-id="44a86-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="44a86-110">放置包含新服務，也包含處理已失敗的具狀態複本或無狀態執行個體。</span><span class="sxs-lookup"><span data-stu-id="44a86-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="44a86-111">刪除和捨棄複本或執行個體都是在這裡處理。</span><span class="sxs-lookup"><span data-stu-id="44a86-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="44a86-112">條件約束檢查 – 此階段進行檢查並修正 hello 系統中的 hello 不同的位置限制 （規則） 的違規情形。</span><span class="sxs-lookup"><span data-stu-id="44a86-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="44a86-113">規則範例包括像是確保節點不超出容量，以及符合服務的放置條件約束。</span><span class="sxs-lookup"><span data-stu-id="44a86-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="44a86-114">平衡-這個階段會檢查 toosee 重新平衡有必要時根據 hello 設定需要不同的度量資訊的餘額的層級。</span><span class="sxs-lookup"><span data-stu-id="44a86-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="44a86-115">如果是它會嘗試的 toofind hello 中的排列方式也就是叢集多個平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="44a86-116">設定叢集資源管理員計時器</span><span class="sxs-lookup"><span data-stu-id="44a86-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="44a86-117">hello 第一組控制項周圍平衡是一組的計時器。</span><span class="sxs-lookup"><span data-stu-id="44a86-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="44a86-118">頻率 hello 叢集資源管理員會檢查 hello 叢集，並採取修正動作，這些計時器控管。</span><span class="sxs-lookup"><span data-stu-id="44a86-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="44a86-119">這兩種不同類型的叢集資源管理員可更正 hello 受到控管其頻率的不同計時器。</span><span class="sxs-lookup"><span data-stu-id="44a86-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="44a86-120">當每個計時器啟動時，會排程 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="44a86-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="44a86-121">根據預設 hello 資源管理員：</span><span class="sxs-lookup"><span data-stu-id="44a86-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="44a86-122">每 1/10 秒掃描一次其狀態並套用更新 (例如記錄某個節點已關閉)</span><span class="sxs-lookup"><span data-stu-id="44a86-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="44a86-123">設定 hello 放置核取旗標</span><span class="sxs-lookup"><span data-stu-id="44a86-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="44a86-124">每秒設定 hello 條件約束檢查旗標</span><span class="sxs-lookup"><span data-stu-id="44a86-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="44a86-125">設定 hello 平衡每五秒的旗標。</span><span class="sxs-lookup"><span data-stu-id="44a86-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="44a86-126">控管這些計時器 hello 組態的範例如下：</span><span class="sxs-lookup"><span data-stu-id="44a86-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="44a86-127">ClusterManifest.xml：</span><span class="sxs-lookup"><span data-stu-id="44a86-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="44a86-128">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="44a86-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="44a86-129">現今 hello 叢集資源管理員只會執行其中一個動作一次，以循序方式。</span><span class="sxs-lookup"><span data-stu-id="44a86-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="44a86-130">這就是為什麼我們 toothese 計時器，為 「 最小間隔 」，請參閱和 hello hello 計時器與 [設定旗標] 當取得採取的動作。</span><span class="sxs-lookup"><span data-stu-id="44a86-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="44a86-131">例如，叢集資源管理員會負責的擱置中的 hello 要求 toocreate 服務之前平衡 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="44a86-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="44a86-132">您可以看到所指定的 hello 預設時間間隔，hello 叢集資源管理員會掃描的任何項目它需求 toodo 常見問題。</span><span class="sxs-lookup"><span data-stu-id="44a86-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="44a86-133">通常這表示每個步驟期間所做的變更的 hello 集很小。</span><span class="sxs-lookup"><span data-stu-id="44a86-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="44a86-134">經常進行小變更可讓叢集資源管理員 toobe hello 回應 hello 叢集中所發生的事項時。</span><span class="sxs-lookup"><span data-stu-id="44a86-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="44a86-135">hello 預設計時器提供某些批次處理後 hello 的許多相同的事件類型傾向 toooccur 同時。</span><span class="sxs-lookup"><span data-stu-id="44a86-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="44a86-136">例如，當節點失敗時，他們可以一次對整個容錯網域執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="44a86-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="44a86-137">所有這些失敗會擷取期間 hello 下一個狀態更新之後 hello *PLBRefreshGap*。</span><span class="sxs-lookup"><span data-stu-id="44a86-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="44a86-138">hello 更正是在 hello 遵循條件約束檢查的位置，並平衡執行期間決定的。</span><span class="sxs-lookup"><span data-stu-id="44a86-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="44a86-139">依預設 hello 叢集資源管理員不是透過小時 hello 叢集中變更的掃描，然後再 tooaddress 所有變更一次。</span><span class="sxs-lookup"><span data-stu-id="44a86-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="44a86-140">這樣會導致 toobursts 的變換。</span><span class="sxs-lookup"><span data-stu-id="44a86-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="44a86-141">hello 叢集資源管理員也需要一些其他資訊 toodetermine 如果 hello 叢集不平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="44a86-142">因此，我們有其他兩個的設定︰「平衡臨界值」和「活動臨界值」。</span><span class="sxs-lookup"><span data-stu-id="44a86-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="44a86-143">平衡臨界值</span><span class="sxs-lookup"><span data-stu-id="44a86-143">Balancing thresholds</span></span>
<span data-ttu-id="44a86-144">平衡臨界值為 hello 主控制項，用於觸發重新平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="44a86-145">hello 平衡臨界值標準是_比率_。</span><span class="sxs-lookup"><span data-stu-id="44a86-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="44a86-146">節點上 hello 標準 hello 負載最載入除以 hello 負載量 hello 至少載入的節點是否超過該度量*BalancingThreshold*，然後 hello 叢集不平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="44a86-147">如此一來平衡為觸發的 hello 叢集資源管理員會檢查下一個時間 hello。</span><span class="sxs-lookup"><span data-stu-id="44a86-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="44a86-148">hello *MinLoadBalancingInterval*計時器定義 hello 叢集資源管理員應檢查的頻率如果需要重新平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="44a86-149">檢查並不意謂著有發生任何事情。</span><span class="sxs-lookup"><span data-stu-id="44a86-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="44a86-150">每個標準為基礎 hello 叢集中定義的一部分定義平衡臨界值。</span><span class="sxs-lookup"><span data-stu-id="44a86-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="44a86-151">如需有關計量的詳細資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="44a86-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="44a86-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="44a86-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="44a86-153">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="44a86-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="44a86-154"><center>
![平衡臨界值範例][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="44a86-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="44a86-155">在此範例中，每個服務皆取用一單位的某個計量。</span><span class="sxs-lookup"><span data-stu-id="44a86-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="44a86-156">在 hello 上方範例中，hello 節點上的最大負載為 5，hello 最小值為二。</span><span class="sxs-lookup"><span data-stu-id="44a86-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="44a86-157">例如，假設該 hello 平衡這個標準的臨界值為 3。</span><span class="sxs-lookup"><span data-stu-id="44a86-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="44a86-158">因為 hello 叢集中的 hello 比例是 5/2 = 2.5，也就是少於 hello 指定平衡臨界值的三個 hello 叢集平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="44a86-159">無平衡 hello 叢集資源管理員會檢查時觸發。</span><span class="sxs-lookup"><span data-stu-id="44a86-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="44a86-160">Hello 下方範例中，在 hello 節點上的最大載入時 hello 最小值是 2，產生五個比例是 10。</span><span class="sxs-lookup"><span data-stu-id="44a86-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="44a86-161">五個大於 hello 指定平衡臨界值的三個該標準。</span><span class="sxs-lookup"><span data-stu-id="44a86-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="44a86-162">如此一來，重新平衡執行將會排定平衡計時器引發的下一個時間 hello。</span><span class="sxs-lookup"><span data-stu-id="44a86-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="44a86-163">在此情況下某些負載會是通常分散式的 tooNode3。</span><span class="sxs-lookup"><span data-stu-id="44a86-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="44a86-164">Hello Service Fabric 叢集資源管理員不會使用窮盡方法，因為某些負載也可能是分散式的 tooNode2。</span><span class="sxs-lookup"><span data-stu-id="44a86-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="44a86-165"><center>
![平衡臨界值範例動作][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="44a86-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="44a86-166">「平衡」會處理兩個不同的策略來管理叢集中的負載。</span><span class="sxs-lookup"><span data-stu-id="44a86-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="44a86-167">hello hello 叢集資源管理員使用的預設策略 hello hello 叢集中的節點都 toodistribute 負載。</span><span class="sxs-lookup"><span data-stu-id="44a86-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="44a86-168">hello 其他策略是[重組](service-fabric-cluster-resource-manager-defragmentation-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="44a86-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="44a86-169">執行磁碟重組 hello 期間執行的相同平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="44a86-170">hello 平衡和重組策略可以用不同度量 hello 內相同的叢集。</span><span class="sxs-lookup"><span data-stu-id="44a86-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="44a86-171">服務可以同時有平衡和重組計量。</span><span class="sxs-lookup"><span data-stu-id="44a86-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="44a86-172">磁碟重組度量，hello hello 比例載入 hello 叢集觸發程序時重新平衡_下方_hello 平衡臨界值。</span><span class="sxs-lookup"><span data-stu-id="44a86-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="44a86-173">取得以下 hello 平衡臨界值不是明確的目標。</span><span class="sxs-lookup"><span data-stu-id="44a86-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="44a86-174">平衡臨界值只是*觸發程序*。</span><span class="sxs-lookup"><span data-stu-id="44a86-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="44a86-175">平衡執行、 當 hello 叢集資源管理員會決定哪些增強功能，它可以進行，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="44a86-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="44a86-176">因為平衡搜尋開始並不代表任何項目移動。</span><span class="sxs-lookup"><span data-stu-id="44a86-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="44a86-177">有時 hello 叢集是 toocorrect 不平衡，但太受條件約束。</span><span class="sxs-lookup"><span data-stu-id="44a86-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="44a86-178">或者，hello 改良需要移動，也都是[昂貴](service-fabric-cluster-resource-manager-movement-cost.md))。</span><span class="sxs-lookup"><span data-stu-id="44a86-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="44a86-179">活動臨界值</span><span class="sxs-lookup"><span data-stu-id="44a86-179">Activity thresholds</span></span>
<span data-ttu-id="44a86-180">有時候，節點是相對較不平衡，雖然 hello*總*的 hello 叢集中的負載量很低。</span><span class="sxs-lookup"><span data-stu-id="44a86-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="44a86-181">hello 缺乏負載可能是暫時性的 dip，或因為 hello 叢集是新的和取得只需啟動載入。</span><span class="sxs-lookup"><span data-stu-id="44a86-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="44a86-182">在任一情況下，您可能不想平衡 hello 叢集，因為沒有獲得小 toobe toospend 時間。</span><span class="sxs-lookup"><span data-stu-id="44a86-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="44a86-183">如果 hello 叢集經歷了平衡，您會花在網路中，計算資源 toomove 項目，而不進行任何大型*絕對*差異。</span><span class="sxs-lookup"><span data-stu-id="44a86-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="44a86-184">不必要的 tooavoid 移動時，會有另一個控制又稱為活動臨界值。</span><span class="sxs-lookup"><span data-stu-id="44a86-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="44a86-185">活動臨界值可讓您 toospecify 某些絕對下限 」 活動。</span><span class="sxs-lookup"><span data-stu-id="44a86-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="44a86-186">如果沒有節點超過此閾值，平衡未觸發，即使 hello 平衡臨界值到達。</span><span class="sxs-lookup"><span data-stu-id="44a86-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="44a86-187">假設我們為這個計量保留平衡臨界值 3。</span><span class="sxs-lookup"><span data-stu-id="44a86-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="44a86-188">同時假設我們有活動臨界值 1536。</span><span class="sxs-lookup"><span data-stu-id="44a86-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="44a86-189">在 hello 第一種情況下，平衡每 hello hello 叢集時平衡臨界值那里沒有節點符合該活動臨界值，因此不會發生。</span><span class="sxs-lookup"><span data-stu-id="44a86-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="44a86-190">在 hello 下方範例中，Node1 位於 hello 活動臨界值。</span><span class="sxs-lookup"><span data-stu-id="44a86-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="44a86-191">由於同時 hello 平衡臨界值，而且超過 hello 標準 hello 活動臨界值時，將排程平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="44a86-192">例如，讓我們看看下列圖表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="44a86-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="44a86-193"><center>
![活動臨界值範例][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="44a86-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="44a86-194">平衡臨界值，就像活動臨界值會定義每個-度量透過 hello 叢集定義：</span><span class="sxs-lookup"><span data-stu-id="44a86-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="44a86-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="44a86-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="44a86-196">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="44a86-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="44a86-197">平衡及活動的臨界值都同時 hello 平衡臨界值和 hello 超過活動臨界值時，才可以觸發繫結的 tooa 特定度量的平衡相同的度量。</span><span class="sxs-lookup"><span data-stu-id="44a86-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="44a86-198">一起平衡服務</span><span class="sxs-lookup"><span data-stu-id="44a86-198">Balancing services together</span></span>
<span data-ttu-id="44a86-199">Hello 叢集是否不平衡是整個叢集的決策。</span><span class="sxs-lookup"><span data-stu-id="44a86-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="44a86-200">不過，我們要予以修正 hello 方式移動個別的服務複本和需要的執行個體。</span><span class="sxs-lookup"><span data-stu-id="44a86-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="44a86-201">這很合理，對吧？</span><span class="sxs-lookup"><span data-stu-id="44a86-201">This makes sense, right?</span></span> <span data-ttu-id="44a86-202">如果其中一個節點上堆疊記憶體，多個複本或執行個體可能導致 tooit。</span><span class="sxs-lookup"><span data-stu-id="44a86-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="44a86-203">修正 hello 不平衡，可能需要移動任何 hello 可設定狀態的複本或無狀態的執行個體使用 hello 平衡度量資訊。</span><span class="sxs-lookup"><span data-stu-id="44a86-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="44a86-204">偶爾但未本身不平衡的服務取得移動 （請記住 hello 討論的本機和全域加權稍早）。</span><span class="sxs-lookup"><span data-stu-id="44a86-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="44a86-205">為什麼當服務的計量平衡時服務會移動？</span><span class="sxs-lookup"><span data-stu-id="44a86-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="44a86-206">看看以下範例：</span><span class="sxs-lookup"><span data-stu-id="44a86-206">Let’s see an example:</span></span>

- <span data-ttu-id="44a86-207">假設有四個服務：Service1、Service2、Service3 及 Service4。</span><span class="sxs-lookup"><span data-stu-id="44a86-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="44a86-208">Service1 報告計量 Metric1 和 Metric2。</span><span class="sxs-lookup"><span data-stu-id="44a86-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="44a86-209">Service2 報告計量 Metric2 和 Metric3。</span><span class="sxs-lookup"><span data-stu-id="44a86-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="44a86-210">Service3 報告計量 Metric3 和 Metric4。</span><span class="sxs-lookup"><span data-stu-id="44a86-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="44a86-211">Service4 報告計量 Metric99。</span><span class="sxs-lookup"><span data-stu-id="44a86-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="44a86-212">您應該可以看出這個範例要表達什麼：有鏈結！</span><span class="sxs-lookup"><span data-stu-id="44a86-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="44a86-213">我們並非實際上擁有 4 個獨立的服務，而是有 3 個相關的服務，以及一個獨立的服務。</span><span class="sxs-lookup"><span data-stu-id="44a86-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="44a86-214"><center>
![將服務一起平衡][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="44a86-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="44a86-215">因為此鏈結中，很可能，在 1-4 的度量不平衡可能會導致複本或執行個體屬於 tooservices 周圍的 1-3 toomove。</span><span class="sxs-lookup"><span data-stu-id="44a86-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="44a86-216">我們也知道計量 1、2 或 3 若發生不平衡，並不會導致 Service4 中發生移動。</span><span class="sxs-lookup"><span data-stu-id="44a86-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="44a86-217">因為移動 hello 複本會有任何點或執行個體屬於 tooService4 周圍可以不絕對度量 1-3 tooimpact hello 之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="44a86-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="44a86-218">hello 叢集資源管理員會自動找出相關的服務。</span><span class="sxs-lookup"><span data-stu-id="44a86-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="44a86-219">新增、 移除或變更服務的 hello 度量可能會影響它們的關聯性。</span><span class="sxs-lookup"><span data-stu-id="44a86-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="44a86-220">例如，之間的平衡 Service2 的兩個回合可能已更新的 tooremove Metric2。</span><span class="sxs-lookup"><span data-stu-id="44a86-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="44a86-221">這會中斷 Service1 和 Service2 之間的 hello 鏈結。</span><span class="sxs-lookup"><span data-stu-id="44a86-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="44a86-222">現在，您擁有的是三個相關服務群組，而非兩個︰</span><span class="sxs-lookup"><span data-stu-id="44a86-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="44a86-223"><center>
![將服務一起平衡][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="44a86-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="44a86-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44a86-224">Next steps</span></span>
* <span data-ttu-id="44a86-225">度量資訊是如何 hello Service Fabric 叢集資源管理員管理耗用量和 hello 叢集中的容量。</span><span class="sxs-lookup"><span data-stu-id="44a86-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="44a86-226">toolearn 更多關於度量和如何 tooconfigure 它們，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="44a86-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="44a86-227">移動成本是訊號某些服務會比其他更耗費資源 toomove toohello 叢集資源管理員的一種方式。</span><span class="sxs-lookup"><span data-stu-id="44a86-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="44a86-228">如需有關移動成本的詳細資訊，請參閱太[這篇文章](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="44a86-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="44a86-229">hello 叢集資源管理員有數個節流，您可以設定下變換 tooslow hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="44a86-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="44a86-230">這些節流通常不是必要的，但若有需要，您可以參閱 [這裡](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="44a86-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
