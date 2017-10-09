---
title: "Azure Service Fabric 中標準的 aaaDefragmentation |Microsoft 文件"
description: "使用重組或封裝作為 Service Fabric 中度量策略的概觀"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="b8e76-103">度量的重組和 Service Fabric 中的負載</span><span class="sxs-lookup"><span data-stu-id="b8e76-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="b8e76-104">管理 hello 叢集中的負載度量 hello Service Fabric 叢集資源管理員的預設策略是 toodistribute hello 負載。</span><span class="sxs-lookup"><span data-stu-id="b8e76-104">hello Service Fabric Cluster Resource Manager's default strategy for managing load metrics in hello cluster is toodistribute hello load.</span></span> <span data-ttu-id="b8e76-105">確保節點平均並加以使用，可避免熱門和冷門導致 tooboth 爭用和浪費的資源的點。</span><span class="sxs-lookup"><span data-stu-id="b8e76-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead tooboth contention and wasted resources.</span></span> <span data-ttu-id="b8e76-106">散發 hello 叢集中的工作負載，也是最安全方面存活失敗，因為它可確保失敗不取出指定的工作負載大量百分比的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8e76-106">Distributing workloads in hello cluster is also hello safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> 

<span data-ttu-id="b8e76-107">hello Service Fabric 叢集資源管理員支援不同的策略來管理負載，也就是磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="b8e76-107">hello Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span></span> <span data-ttu-id="b8e76-108">磁碟重組表示，而不是整個 hello 叢集嘗試 toodistribute hello 使用量度量資訊，它會彙總。</span><span class="sxs-lookup"><span data-stu-id="b8e76-108">Defragmentation means that instead of trying toodistribute hello utilization of a metric across hello cluster, it is consolidated.</span></span> <span data-ttu-id="b8e76-109">彙總只逆轉 hello 預設平衡策略 – 而不是 hello 平均標準差的度量的負載降到最低，hello 叢集資源管理員會嘗試 tooincrease 它。</span><span class="sxs-lookup"><span data-stu-id="b8e76-109">Consolidation is just an inversion of hello default balancing strategy – instead of minimizing hello average standard deviation of metric load, hello Cluster Resource Manager tries tooincrease it.</span></span>

## <a name="when-toouse-defragmentation"></a><span data-ttu-id="b8e76-110">當 toouse 磁碟重組</span><span class="sxs-lookup"><span data-stu-id="b8e76-110">When toouse defragmentation</span></span>
<span data-ttu-id="b8e76-111">Hello 叢集中的負載，會消耗一些 hello 每個節點上的資源。</span><span class="sxs-lookup"><span data-stu-id="b8e76-111">Distributing load in hello cluster consumes some of hello resources on each node.</span></span> <span data-ttu-id="b8e76-112">某些工作負載會建立極龐大且耗用大部分或所有節點的服務。</span><span class="sxs-lookup"><span data-stu-id="b8e76-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span></span> <span data-ttu-id="b8e76-113">在這些情況下，可能會，當大型取得建立工作負載沒有足夠的空間上任何節點 toorun 它們。</span><span class="sxs-lookup"><span data-stu-id="b8e76-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node toorun them.</span></span> <span data-ttu-id="b8e76-114">大型工作負載不 Service Fabric; 中的問題在這些情況下 hello 叢集資源管理員會判斷它需要 tooreorganize hello 叢集 toomake 空間供這個大量的工作負載。</span><span class="sxs-lookup"><span data-stu-id="b8e76-114">Large workloads aren't a problem in Service Fabric; in these cases hello Cluster Resource Manager determines that it needs tooreorganize hello cluster toomake room for this large workload.</span></span> <span data-ttu-id="b8e76-115">不過，在 hello 同時工作負載有 toowait toobe 排程 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="b8e76-115">However, in hello meantime that workload has toowait toobe scheduled in hello cluster.</span></span>

<span data-ttu-id="b8e76-116">如果有許多的服務和狀態 toomove 周圍，它可能需要很長的時間 hello 大量的工作負載 toobe 放置 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="b8e76-116">If there are many services and state toomove around, then it could take a long time for hello large workload toobe placed in hello cluster.</span></span> <span data-ttu-id="b8e76-117">如果在 hello 叢集中的其他工作負載也很大，而且讓長 tooreorganize，這是更有可能。</span><span class="sxs-lookup"><span data-stu-id="b8e76-117">This is more likely if other workloads in hello cluster are also large and so take longer tooreorganize.</span></span> <span data-ttu-id="b8e76-118">hello Service Fabric 小組測量建立時間，在此案例的模擬。</span><span class="sxs-lookup"><span data-stu-id="b8e76-118">hello Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="b8e76-119">我們發現，只要叢集使用率超過 30% 到 50% 之間，建立大型服務所花費的時間就會更久。</span><span class="sxs-lookup"><span data-stu-id="b8e76-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span></span> <span data-ttu-id="b8e76-120">toohandle 此案例中，我們引進了做為平衡策略磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="b8e76-120">toohandle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="b8e76-121">我們發現，大型工作負載，特別是其中的建立時間為重要的是，磁碟重組真的協助這些新的工作負載已排入排程 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="b8e76-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in hello cluster.</span></span>

<span data-ttu-id="b8e76-122">您可以設定磁碟重組度量 toohave hello hello 服務的叢集資源管理員 tooproactively 再試一次 toocondense hello 負載成較少的節點。</span><span class="sxs-lookup"><span data-stu-id="b8e76-122">You can configure defragmentation metrics toohave hello Cluster Resource Manager tooproactively try toocondense hello load of hello services into fewer nodes.</span></span> <span data-ttu-id="b8e76-123">這有助於確保沒有幾乎大型的服務，而不需重新組織 hello 叢集中的空間。</span><span class="sxs-lookup"><span data-stu-id="b8e76-123">This helps ensure that there is almost always room for large services without reorganizing hello cluster.</span></span> <span data-ttu-id="b8e76-124">沒有 tooreorganize hello 叢集可讓快速建立大型工作負載。</span><span class="sxs-lookup"><span data-stu-id="b8e76-124">Not having tooreorganize hello cluster allows creating large workloads quickly.</span></span>

<span data-ttu-id="b8e76-125">大部分的人不需要重組。</span><span class="sxs-lookup"><span data-stu-id="b8e76-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="b8e76-126">因此並不難 toofind 空間它們 hello 叢集中，服務會通常很小。</span><span class="sxs-lookup"><span data-stu-id="b8e76-126">Services are usually be small, so it’s not hard toofind room for them in hello cluster.</span></span> <span data-ttu-id="b8e76-127">重新組織可行時，同樣地可以快速執行，因為大部分服務很小，而且可以快速且平行地移動。</span><span class="sxs-lookup"><span data-stu-id="b8e76-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span></span> <span data-ttu-id="b8e76-128">不過，如果您有大型的服務，並需要快速地建立然後 hello 磁碟重組策略就是您。</span><span class="sxs-lookup"><span data-stu-id="b8e76-128">However, if you have large services and need them created quickly then hello defragmentation strategy is for you.</span></span> <span data-ttu-id="b8e76-129">我們將討論使用磁碟重組，接下來的 hello 權衡取捨。</span><span class="sxs-lookup"><span data-stu-id="b8e76-129">We'll discuss hello tradeoffs of using defragmentation next.</span></span> 

## <a name="defragmentation-tradeoffs"></a><span data-ttu-id="b8e76-130">重組權衡取捨</span><span class="sxs-lookup"><span data-stu-id="b8e76-130">Defragmentation tradeoffs</span></span>
<span data-ttu-id="b8e76-131">重組會放大故障的影響力，因為在故障節點上執行的服務更多。</span><span class="sxs-lookup"><span data-stu-id="b8e76-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span></span> <span data-ttu-id="b8e76-132">磁碟重組也可以增加成本，因為 hello 叢集中的資源必須持有保留，等候 hello 建立大型工作負載。</span><span class="sxs-lookup"><span data-stu-id="b8e76-132">Defragmentation can also increase costs, since resources in hello cluster must be held in reserve, waiting for hello creation of large workloads.</span></span>

<span data-ttu-id="b8e76-133">hello 下列圖表提供兩個叢集的視覺表示法，已重組，一個不是。</span><span class="sxs-lookup"><span data-stu-id="b8e76-133">hello following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span></span> 

<span data-ttu-id="b8e76-134"><center>
![比較平衡和重組叢集][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="b8e76-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

<span data-ttu-id="b8e76-135">在 hello 平衡案例中，請考慮 hello 數目就是必要的 tooplace hello 最大的服務物件的移動。</span><span class="sxs-lookup"><span data-stu-id="b8e76-135">In hello balanced case, consider hello number of movements that would be necessary tooplace one of hello largest service objects.</span></span> <span data-ttu-id="b8e76-136">在 hello 重組叢集中，hello 大量的工作負載無法置於四或五個節點而不需要的任何其他服務 toomove toowait。</span><span class="sxs-lookup"><span data-stu-id="b8e76-136">In hello defragmented cluster, hello large workload could be placed on nodes four or five without having toowait for any other services toomove.</span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="b8e76-137">重組的優缺點</span><span class="sxs-lookup"><span data-stu-id="b8e76-137">Defragmentation pros and cons</span></span>
<span data-ttu-id="b8e76-138">因此，有哪些其他概念性的代價？</span><span class="sxs-lookup"><span data-stu-id="b8e76-138">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="b8e76-139">以下是有關的事項 toothink 的快速資料表：</span><span class="sxs-lookup"><span data-stu-id="b8e76-139">Here’s a quick table of things toothink about:</span></span>

| <span data-ttu-id="b8e76-140">重組優點</span><span class="sxs-lookup"><span data-stu-id="b8e76-140">Defragmentation Pros</span></span> | <span data-ttu-id="b8e76-141">重組缺點</span><span class="sxs-lookup"><span data-stu-id="b8e76-141">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="b8e76-142">能夠更快速建立大型服務</span><span class="sxs-lookup"><span data-stu-id="b8e76-142">Allows faster creation of large services</span></span> |<span data-ttu-id="b8e76-143">將負載集中到較少數的節點，提高爭用</span><span class="sxs-lookup"><span data-stu-id="b8e76-143">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="b8e76-144">在建立期間啟用較低的資料移動</span><span class="sxs-lookup"><span data-stu-id="b8e76-144">Enables lower data movement during creation</span></span> |<span data-ttu-id="b8e76-145">失敗會影響更多服務，並導致更多流失</span><span class="sxs-lookup"><span data-stu-id="b8e76-145">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="b8e76-146">能夠豐富描述需求和空間的回收</span><span class="sxs-lookup"><span data-stu-id="b8e76-146">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="b8e76-147">較複雜的整體資源管理組態</span><span class="sxs-lookup"><span data-stu-id="b8e76-147">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="b8e76-148">您可以混合重組和一般計量 hello 相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="b8e76-148">You can mix defragmented and normal metrics in hello same cluster.</span></span> <span data-ttu-id="b8e76-149">hello 叢集資源管理員會嘗試 tooconsolidate hello 重組度量盡可能時分配 hello 其他人。</span><span class="sxs-lookup"><span data-stu-id="b8e76-149">hello Cluster Resource Manager tries tooconsolidate hello defragmentation metrics as much as possible while spreading out hello others.</span></span> <span data-ttu-id="b8e76-150">hello 結果的混合磁碟重組和平衡策略取決於許多因素，包括：</span><span class="sxs-lookup"><span data-stu-id="b8e76-150">hello results of mixing defragmentation and balancing strategies depends on several factors, including:</span></span>
  - <span data-ttu-id="b8e76-151">hello 數目的平衡與 hello 的幾個磁碟重組度量的度量</span><span class="sxs-lookup"><span data-stu-id="b8e76-151">hello number of balancing metrics vs. hello number of defragmentation metrics</span></span>
  - <span data-ttu-id="b8e76-152">是否有任何服務同時使用兩種類型的計量</span><span class="sxs-lookup"><span data-stu-id="b8e76-152">Whether any service uses both types of metrics</span></span> 
  - <span data-ttu-id="b8e76-153">hello 衡量標準權數</span><span class="sxs-lookup"><span data-stu-id="b8e76-153">hello metric weights</span></span>
  - <span data-ttu-id="b8e76-154">目前的計量負載</span><span class="sxs-lookup"><span data-stu-id="b8e76-154">current metric loads</span></span>
  
<span data-ttu-id="b8e76-155">試驗是必要的 toodetermine hello 確切必要組態。</span><span class="sxs-lookup"><span data-stu-id="b8e76-155">Experimentation is required toodetermine hello exact configuration necessary.</span></span> <span data-ttu-id="b8e76-156">我們建議先徹底測量您的工作負載，然後再於生產中啟用重組計量。</span><span class="sxs-lookup"><span data-stu-id="b8e76-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span></span> <span data-ttu-id="b8e76-157">特別是當磁碟重組和平衡的度量 hello 中混用相同的服務。</span><span class="sxs-lookup"><span data-stu-id="b8e76-157">This is especially true when mixing defragmentation and balanced metrics within hello same service.</span></span> 

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="b8e76-158">設定重組度量</span><span class="sxs-lookup"><span data-stu-id="b8e76-158">Configuring defragmentation metrics</span></span>
<span data-ttu-id="b8e76-159">設定磁碟重組度量資訊是全域的決策，在 hello 叢集中，並選取個別的度量來進行磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="b8e76-159">Configuring defragmentation metrics is a global decision in hello cluster, and individual metrics can be selected for defragmentation.</span></span> <span data-ttu-id="b8e76-160">下列組態程式碼片段的 hello 顯示 tooconfigure 度量的磁碟重組。</span><span class="sxs-lookup"><span data-stu-id="b8e76-160">hello following config snippets show how tooconfigure metrics for defragmentation.</span></span> <span data-ttu-id="b8e76-161">在此情況下，"Metric1 」 設定為磁碟重組度量，"Metric2 」 將會繼續正常平衡 toobe 時。</span><span class="sxs-lookup"><span data-stu-id="b8e76-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue toobe balanced normally.</span></span> 

<span data-ttu-id="b8e76-162">ClusterManifest.xml：</span><span class="sxs-lookup"><span data-stu-id="b8e76-162">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

<span data-ttu-id="b8e76-163">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="b8e76-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a><span data-ttu-id="b8e76-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8e76-164">Next steps</span></span>
- <span data-ttu-id="b8e76-165">hello 叢集資源管理員具有 man 選項描述 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b8e76-165">hello Cluster Resource Manager has man options for describing hello cluster.</span></span> <span data-ttu-id="b8e76-166">toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="b8e76-166">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="b8e76-167">度量資訊是如何 hello Service Fabric 叢集資源管理員管理耗用量和 hello 叢集中的容量。</span><span class="sxs-lookup"><span data-stu-id="b8e76-167">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="b8e76-168">toolearn 更多關於度量和如何 tooconfigure 它們，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="b8e76-168">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
