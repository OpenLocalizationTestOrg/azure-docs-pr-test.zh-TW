---
title: "Azure Service Fabric 中度量的重組 | Microsoft Docs"
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
ms.openlocfilehash: b253cc07066092aa82d218c9c82c8aac502245a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="e6259-103">度量的重組和 Service Fabric 中的負載</span><span class="sxs-lookup"><span data-stu-id="e6259-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="e6259-104">Service Fabric 叢集資源管理員對於管理叢集中負載計量的預設策略是分散負載。</span><span class="sxs-lookup"><span data-stu-id="e6259-104">The Service Fabric Cluster Resource Manager's default strategy for managing load metrics in the cluster is to distribute the load.</span></span> <span data-ttu-id="e6259-105">確保平均使用節點，以避免忙碌和閒置位置，導致爭用和浪費的資源。</span><span class="sxs-lookup"><span data-stu-id="e6259-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead to both contention and wasted resources.</span></span> <span data-ttu-id="e6259-106">就故障情況下幸存而言，分散工作負載是最安全的，因為這可確保不會因為故障而使指定的工作負載損失慘重。</span><span class="sxs-lookup"><span data-stu-id="e6259-106">Distributing workloads in the cluster is also the safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> 

<span data-ttu-id="e6259-107">Service Fabric 叢集資源管理員支援管理負載的不同策略，也就是重組。</span><span class="sxs-lookup"><span data-stu-id="e6259-107">The Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span></span> <span data-ttu-id="e6259-108">重組表示合併計量，而不是嘗試將計量的使用量分散到叢集中。</span><span class="sxs-lookup"><span data-stu-id="e6259-108">Defragmentation means that instead of trying to distribute the utilization of a metric across the cluster, it is consolidated.</span></span> <span data-ttu-id="e6259-109">合併完全逆轉預設平衡策略 – 叢集資源管理員嘗試增加偏差，而不是將計量負載的平均標準偏差最小化。</span><span class="sxs-lookup"><span data-stu-id="e6259-109">Consolidation is just an inversion of the default balancing strategy – instead of minimizing the average standard deviation of metric load, the Cluster Resource Manager tries to increase it.</span></span>

## <a name="when-to-use-defragmentation"></a><span data-ttu-id="e6259-110">使用重組的時機</span><span class="sxs-lookup"><span data-stu-id="e6259-110">When to use defragmentation</span></span>
<span data-ttu-id="e6259-111">分散叢集中的負載，會耗用每個節點上的一些資源。</span><span class="sxs-lookup"><span data-stu-id="e6259-111">Distributing load in the cluster consumes some of the resources on each node.</span></span> <span data-ttu-id="e6259-112">某些工作負載會建立極龐大且耗用大部分或所有節點的服務。</span><span class="sxs-lookup"><span data-stu-id="e6259-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span></span> <span data-ttu-id="e6259-113">在這些情況下，有可能在建立大型工作負載時，任何節點上都沒有可以執行的足夠空間。</span><span class="sxs-lookup"><span data-stu-id="e6259-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node to run them.</span></span> <span data-ttu-id="e6259-114">大型工作負載在 Service Fabric 中並不是問題；在這些情況下，叢集資源管理員會決定需要重組叢集，以騰出空間給這個大型工作負載。</span><span class="sxs-lookup"><span data-stu-id="e6259-114">Large workloads aren't a problem in Service Fabric; in these cases the Cluster Resource Manager determines that it needs to reorganize the cluster to make room for this large workload.</span></span> <span data-ttu-id="e6259-115">不過，同時此工作負載必須等待在叢集中排程。</span><span class="sxs-lookup"><span data-stu-id="e6259-115">However, in the meantime that workload has to wait to be scheduled in the cluster.</span></span>

<span data-ttu-id="e6259-116">如果要通過許多服務和狀態，則大型工作負載會經過很常的時間才放入叢集中。</span><span class="sxs-lookup"><span data-stu-id="e6259-116">If there are many services and state to move around, then it could take a long time for the large workload to be placed in the cluster.</span></span> <span data-ttu-id="e6259-117">如果叢集中的其他工作負載也很大，因而移動時間很久，可能就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="e6259-117">This is more likely if other workloads in the cluster are also large and so take longer to reorganize.</span></span> <span data-ttu-id="e6259-118">Service Fabric 小組是模擬此案例來測量建立時間。</span><span class="sxs-lookup"><span data-stu-id="e6259-118">The Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="e6259-119">我們發現，只要叢集使用率超過 30% 到 50% 之間，建立大型服務所花費的時間就會更久。</span><span class="sxs-lookup"><span data-stu-id="e6259-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span></span> <span data-ttu-id="e6259-120">為了解決這種情況，我們引進重組當作平衡策略。</span><span class="sxs-lookup"><span data-stu-id="e6259-120">To handle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="e6259-121">我們發現，對於大型工作負載，特別是建立時間很重要的工作負載，重組確實有助於將新的工作負載放入叢集中排程。</span><span class="sxs-lookup"><span data-stu-id="e6259-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in the cluster.</span></span>

<span data-ttu-id="e6259-122">您可以設定重組計量，讓叢集資源管理員主動嘗試將服務的負載壓縮至較少的節點。</span><span class="sxs-lookup"><span data-stu-id="e6259-122">You can configure defragmentation metrics to have the Cluster Resource Manager to proactively try to condense the load of the services into fewer nodes.</span></span> <span data-ttu-id="e6259-123">這有助於確保幾乎永遠有空間容納更大型的服務，而不需要重新組織叢集。</span><span class="sxs-lookup"><span data-stu-id="e6259-123">This helps ensure that there is almost always room for large services without reorganizing the cluster.</span></span> <span data-ttu-id="e6259-124">不需要重新組織叢集可以讓建立大型工作負載更快速。</span><span class="sxs-lookup"><span data-stu-id="e6259-124">Not having to reorganize the cluster allows creating large workloads quickly.</span></span>

<span data-ttu-id="e6259-125">大部分的人不需要重組。</span><span class="sxs-lookup"><span data-stu-id="e6259-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="e6259-126">服務通常很小，因此在叢集中不難找到空間給它們。</span><span class="sxs-lookup"><span data-stu-id="e6259-126">Services are usually be small, so it’s not hard to find room for them in the cluster.</span></span> <span data-ttu-id="e6259-127">重新組織可行時，同樣地可以快速執行，因為大部分服務很小，而且可以快速且平行地移動。</span><span class="sxs-lookup"><span data-stu-id="e6259-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span></span> <span data-ttu-id="e6259-128">不過，如果您有大型的服務且需要儘速建立，則重組策略就適合您。</span><span class="sxs-lookup"><span data-stu-id="e6259-128">However, if you have large services and need them created quickly then the defragmentation strategy is for you.</span></span> <span data-ttu-id="e6259-129">我們接下來將討論使用重組的權衡取捨。</span><span class="sxs-lookup"><span data-stu-id="e6259-129">We'll discuss the tradeoffs of using defragmentation next.</span></span> 

## <a name="defragmentation-tradeoffs"></a><span data-ttu-id="e6259-130">重組權衡取捨</span><span class="sxs-lookup"><span data-stu-id="e6259-130">Defragmentation tradeoffs</span></span>
<span data-ttu-id="e6259-131">重組會放大故障的影響力，因為在故障節點上執行的服務更多。</span><span class="sxs-lookup"><span data-stu-id="e6259-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span></span> <span data-ttu-id="e6259-132">重組也會增加成本，因為叢集中的資源必須保留，等候大型工作負載的建立。</span><span class="sxs-lookup"><span data-stu-id="e6259-132">Defragmentation can also increase costs, since resources in the cluster must be held in reserve, waiting for the creation of large workloads.</span></span>

<span data-ttu-id="e6259-133">下圖提供兩個叢集的視覺表示法，其中一個已重組，另一個未重組。</span><span class="sxs-lookup"><span data-stu-id="e6259-133">The following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span></span> 

<span data-ttu-id="e6259-134"><center>
![比較平衡和重組叢集][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="e6259-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

<span data-ttu-id="e6259-135">在平衡情況下，請注意放置其中一個最大服務物件所需的移動次數。</span><span class="sxs-lookup"><span data-stu-id="e6259-135">In the balanced case, consider the number of movements that would be necessary to place one of the largest service objects.</span></span> <span data-ttu-id="e6259-136">在重組的叢集中，大型工作負載可以放置於四或五個節點，而不需要等待其他服務移動。</span><span class="sxs-lookup"><span data-stu-id="e6259-136">In the defragmented cluster, the large workload could be placed on nodes four or five without having to wait for any other services to move.</span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="e6259-137">重組的優缺點</span><span class="sxs-lookup"><span data-stu-id="e6259-137">Defragmentation pros and cons</span></span>
<span data-ttu-id="e6259-138">因此，有哪些其他概念性的代價？</span><span class="sxs-lookup"><span data-stu-id="e6259-138">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="e6259-139">以下是要考慮事項的一覽表︰</span><span class="sxs-lookup"><span data-stu-id="e6259-139">Here’s a quick table of things to think about:</span></span>

| <span data-ttu-id="e6259-140">重組優點</span><span class="sxs-lookup"><span data-stu-id="e6259-140">Defragmentation Pros</span></span> | <span data-ttu-id="e6259-141">重組缺點</span><span class="sxs-lookup"><span data-stu-id="e6259-141">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="e6259-142">能夠更快速建立大型服務</span><span class="sxs-lookup"><span data-stu-id="e6259-142">Allows faster creation of large services</span></span> |<span data-ttu-id="e6259-143">將負載集中到較少數的節點，提高爭用</span><span class="sxs-lookup"><span data-stu-id="e6259-143">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="e6259-144">在建立期間啟用較低的資料移動</span><span class="sxs-lookup"><span data-stu-id="e6259-144">Enables lower data movement during creation</span></span> |<span data-ttu-id="e6259-145">失敗會影響更多服務，並導致更多流失</span><span class="sxs-lookup"><span data-stu-id="e6259-145">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="e6259-146">能夠豐富描述需求和空間的回收</span><span class="sxs-lookup"><span data-stu-id="e6259-146">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="e6259-147">較複雜的整體資源管理組態</span><span class="sxs-lookup"><span data-stu-id="e6259-147">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="e6259-148">您可以在相同叢集中混用重組計量和一般計量。</span><span class="sxs-lookup"><span data-stu-id="e6259-148">You can mix defragmented and normal metrics in the same cluster.</span></span> <span data-ttu-id="e6259-149">叢集資源管理員會嘗試儘可能合併重組計量，而分散其他計量。</span><span class="sxs-lookup"><span data-stu-id="e6259-149">The Cluster Resource Manager tries to consolidate the defragmentation metrics as much as possible while spreading out the others.</span></span> <span data-ttu-id="e6259-150">混合重組和平衡策略的結果取決於許多因素，包括：</span><span class="sxs-lookup"><span data-stu-id="e6259-150">The results of mixing defragmentation and balancing strategies depends on several factors, including:</span></span>
  - <span data-ttu-id="e6259-151">平衡計量數目與重組計量數目</span><span class="sxs-lookup"><span data-stu-id="e6259-151">the number of balancing metrics vs. the number of defragmentation metrics</span></span>
  - <span data-ttu-id="e6259-152">是否有任何服務同時使用兩種類型的計量</span><span class="sxs-lookup"><span data-stu-id="e6259-152">Whether any service uses both types of metrics</span></span> 
  - <span data-ttu-id="e6259-153">計量權數</span><span class="sxs-lookup"><span data-stu-id="e6259-153">the metric weights</span></span>
  - <span data-ttu-id="e6259-154">目前的計量負載</span><span class="sxs-lookup"><span data-stu-id="e6259-154">current metric loads</span></span>
  
<span data-ttu-id="e6259-155">需要實驗來判斷所需的確切組態。</span><span class="sxs-lookup"><span data-stu-id="e6259-155">Experimentation is required to determine the exact configuration necessary.</span></span> <span data-ttu-id="e6259-156">我們建議先徹底測量您的工作負載，然後再於生產中啟用重組計量。</span><span class="sxs-lookup"><span data-stu-id="e6259-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span></span> <span data-ttu-id="e6259-157">在相同服務中混合重組和平衡計量時，更是如此。</span><span class="sxs-lookup"><span data-stu-id="e6259-157">This is especially true when mixing defragmentation and balanced metrics within the same service.</span></span> 

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="e6259-158">設定重組度量</span><span class="sxs-lookup"><span data-stu-id="e6259-158">Configuring defragmentation metrics</span></span>
<span data-ttu-id="e6259-159">設定重組計量是叢集中的全域決策，而您可以選取個別的計量進行重組。</span><span class="sxs-lookup"><span data-stu-id="e6259-159">Configuring defragmentation metrics is a global decision in the cluster, and individual metrics can be selected for defragmentation.</span></span> <span data-ttu-id="e6259-160">下列設定程式碼片段示範如何設定重組的計量。</span><span class="sxs-lookup"><span data-stu-id="e6259-160">The following config snippets show how to configure metrics for defragmentation.</span></span> <span data-ttu-id="e6259-161">在此情況下，"Metric1" 設定為重組計量，"Metric2" 則繼續進行一般平衡。</span><span class="sxs-lookup"><span data-stu-id="e6259-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue to be balanced normally.</span></span> 

<span data-ttu-id="e6259-162">ClusterManifest.xml：</span><span class="sxs-lookup"><span data-stu-id="e6259-162">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

<span data-ttu-id="e6259-163">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="e6259-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="e6259-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6259-164">Next steps</span></span>
- <span data-ttu-id="e6259-165">叢集資源管理員有許多描述叢集的選項。</span><span class="sxs-lookup"><span data-stu-id="e6259-165">The Cluster Resource Manager has man options for describing the cluster.</span></span> <span data-ttu-id="e6259-166">若要深入了解這些選項，請參閱關於[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)一文</span><span class="sxs-lookup"><span data-stu-id="e6259-166">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="e6259-167">度量是 Service Fabric 叢集資源管理員管理叢集中的耗用量和容量的方式。</span><span class="sxs-lookup"><span data-stu-id="e6259-167">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="e6259-168">若要深入了解計量及其設定方式，請查看[這篇文章](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="e6259-168">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
