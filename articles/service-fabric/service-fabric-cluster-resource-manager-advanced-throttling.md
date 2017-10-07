---
title: "在 hello Service Fabric 叢集資源管理員 aaaThrottling |Microsoft 文件"
description: "了解 tooconfigure hello 流速 hello Service Fabric 叢集資源管理員所提供。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a><span data-ttu-id="1111c-103">節流 hello Service Fabric 叢集資源管理員</span><span class="sxs-lookup"><span data-stu-id="1111c-103">Throttling hello Service Fabric Cluster Resource Manager</span></span>
<span data-ttu-id="1111c-104">即使您已正確設定 hello 叢集資源管理員，可以取得中斷 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1111c-104">Even if you’ve configured hello Cluster Resource Manager correctly, hello cluster can get disrupted.</span></span> <span data-ttu-id="1111c-105">例如，可能同時節點和容錯網域失敗-所發生的升級期間會發生什麼事？hello 叢集資源管理員一律會嘗試 toofix 一切耗用嘗試 tooreorganize 並修正 hello 叢集 hello 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="1111c-105">For example, there could be simultaneous node and fault domain failures - what would happen if that occurred during an upgrade? hello Cluster Resource Manager always tries toofix everything, consuming hello cluster's resources trying tooreorganize and fix hello cluster.</span></span> <span data-ttu-id="1111c-106">流速協助提供機制，讓 hello 叢集可以使用資源 toostabilize-hello 節點回來，hello 網路磁碟分割修復、 部署已更正的位元。</span><span class="sxs-lookup"><span data-stu-id="1111c-106">Throttles help provide a backstop so that hello cluster can use resources toostabilize - hello nodes come back, hello network partitions heal, corrected bits get deployed.</span></span>

<span data-ttu-id="1111c-107">toohelp 以這類情況下，hello Service Fabric 叢集資源管理員包含數個節流。</span><span class="sxs-lookup"><span data-stu-id="1111c-107">toohelp with these sorts of situations, hello Service Fabric Cluster Resource Manager includes several throttles.</span></span> <span data-ttu-id="1111c-108">這些節流功能個個都是強大無比的工具。</span><span class="sxs-lookup"><span data-stu-id="1111c-108">These throttles are all fairly large hammers.</span></span> <span data-ttu-id="1111c-109">一般來說，如果您沒有仔細規劃並測試，就請不要對其進行變更。</span><span class="sxs-lookup"><span data-stu-id="1111c-109">Generally they shouldn’t be changed without careful planning and testing.</span></span>

<span data-ttu-id="1111c-110">如果您變更 hello 叢集資源管理員的節流，您應該調整它們 tooyour 的預期實際負載。</span><span class="sxs-lookup"><span data-stu-id="1111c-110">If you change hello Cluster Resource Manager's throttles, you should tune them tooyour expected actual load.</span></span> <span data-ttu-id="1111c-111">您可決定您需要的 toohave 某些節流的位置，即使它表示 hello 叢集在某些情況下會較長的 toostabilize。</span><span class="sxs-lookup"><span data-stu-id="1111c-111">You may determine you need toohave some throttles in place, even if it means hello cluster takes longer toostabilize in some situations.</span></span> <span data-ttu-id="1111c-112">測試是節流的必要的 toodetermine hello 正確值。</span><span class="sxs-lookup"><span data-stu-id="1111c-112">Testing is required toodetermine hello correct values for throttles.</span></span> <span data-ttu-id="1111c-113">流速需要 toobe 夠高 tooallow hello 叢集 toorespond toochanges 在合理的時間，而且低足夠 tooactually 避免過多的資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="1111c-113">Throttles need toobe high enough tooallow hello cluster toorespond toochanges in a reasonable amount of time, and low enough tooactually prevent too much resource consumption.</span></span> 

<span data-ttu-id="1111c-114">大部分的 hello 時間，我們已看到客戶使用已因為它們已在資源的限制環境的節流。</span><span class="sxs-lookup"><span data-stu-id="1111c-114">Most of hello time we’ve seen customers use throttles it has been because they were already in a resource constrained environment.</span></span> <span data-ttu-id="1111c-115">某些範例可能是有限的網路頻寬的個別節點或不能 toobuild 中的許多可設定狀態之複本的磁碟平行到期 toothroughput 限制。</span><span class="sxs-lookup"><span data-stu-id="1111c-115">Some examples would be limited network bandwidth for individual nodes, or disks that aren't able toobuild many stateful replicas in parallel due toothroughput limitations.</span></span> <span data-ttu-id="1111c-116">沒有流速作業無法不勝負荷這些資源，導致作業 toofail 或會變慢。</span><span class="sxs-lookup"><span data-stu-id="1111c-116">Without throttles, operations could overwhelm these resources, causing operations toofail or be slow.</span></span> <span data-ttu-id="1111c-117">在這些情況下使用節流閥的客戶，而且知道它們所擴充 hello 一段時間會花費 hello 叢集 tooreach 穩定的狀態。</span><span class="sxs-lookup"><span data-stu-id="1111c-117">In these situations customers used throttles and knew they were extending hello amount of time it would take hello cluster tooreach a stable state.</span></span> <span data-ttu-id="1111c-118">客戶也了解進行節流時，最後可能會在整體可靠性降低的情況下運作。</span><span class="sxs-lookup"><span data-stu-id="1111c-118">Customers also understood they could end up running at lower overall reliability while they were throttled.</span></span>


## <a name="configuring-hello-throttles"></a><span data-ttu-id="1111c-119">設定 hello 節流</span><span class="sxs-lookup"><span data-stu-id="1111c-119">Configuring hello throttles</span></span>

<span data-ttu-id="1111c-120">Service Fabric 有兩種節流 hello 複本移動數目的機制。</span><span class="sxs-lookup"><span data-stu-id="1111c-120">Service Fabric has two mechanisms for throttling hello number of replica movements.</span></span> <span data-ttu-id="1111c-121">服務網狀架構 5.7 之前就存在的 hello 預設機制代表節流設定為絕對數字之允許的移動。</span><span class="sxs-lookup"><span data-stu-id="1111c-121">hello default mechanism that existed before Service Fabric 5.7 represents throttling as an absolute number of moves allowed.</span></span> <span data-ttu-id="1111c-122">但這種方式不適用於所有規模的叢集。</span><span class="sxs-lookup"><span data-stu-id="1111c-122">This does not work for clusters of all sizes.</span></span> <span data-ttu-id="1111c-123">特別是，大型叢集 hello 預設值可以是太小，大幅降低平衡甚至會在必要時，同時不有任何作用中較小的群集。</span><span class="sxs-lookup"><span data-stu-id="1111c-123">In particular, for large clusters hello default value can be too small, significantly slowing down balancing even when it is necessary, while having no effect in smaller clusters.</span></span> <span data-ttu-id="1111c-124">這個先前機制已被取代的百分比為基礎的節流，其規模會更好的動態叢集服務的 hello 數字而定期變更節點。</span><span class="sxs-lookup"><span data-stu-id="1111c-124">This prior mechanism has been superseded by percentage-based throttling, which scales better with dynamic clusters in which hello number of services and nodes change regularly.</span></span>

<span data-ttu-id="1111c-125">hello 節流根據 hello hello 叢集中的複本數目的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="1111c-125">hello throttles are based on a percentage of hello number of replicas in hello clusters.</span></span> <span data-ttu-id="1111c-126">基礎 Percetage 流速啟用表達 hello 規則: 「 不會移動超過 10%的複本以 10 分鐘間隔 」，例如。</span><span class="sxs-lookup"><span data-stu-id="1111c-126">Percetage based throttles enable expressing hello rule: "do not move more than 10% of replicas in a 10 minute interval", for example.</span></span>

<span data-ttu-id="1111c-127">hello 百分比為基礎的節流組態設定是：</span><span class="sxs-lookup"><span data-stu-id="1111c-127">hello configuration settings for percentage-based throttling are:</span></span>

  - <span data-ttu-id="1111c-128">GlobalMovementThrottleThresholdPercentage-移動，也可以隨時在叢集中允許的最大數目以 hello 叢集中的複本總數的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="1111c-128">GlobalMovementThrottleThresholdPercentage - Maximum number of movements allowed in cluster at any time, expressed as percentage of total number of replicas in hello cluster.</span></span> <span data-ttu-id="1111c-129">0 表示沒有限制。</span><span class="sxs-lookup"><span data-stu-id="1111c-129">0 indicates no limit.</span></span> <span data-ttu-id="1111c-130">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="1111c-130">hello default value is 0.</span></span> <span data-ttu-id="1111c-131">如果未指定此設定 」 和 「 GlobalMovementThrottleThreshold，然後 hello 更保守的限制會使用。</span><span class="sxs-lookup"><span data-stu-id="1111c-131">If both this setting and GlobalMovementThrottleThreshold are specified, then hello more conservative limit is used.</span></span>
  - <span data-ttu-id="1111c-132">GlobalMovementThrottleThresholdPercentageForPlacement-允許在 hello 放置階段中，以在 hello 叢集中的複本總數的百分比表示移動的最大數目。</span><span class="sxs-lookup"><span data-stu-id="1111c-132">GlobalMovementThrottleThresholdPercentageForPlacement - Maximum number of movements allowed during hello placement phase, expressed as percentage of total number of replicas in hello cluster.</span></span> <span data-ttu-id="1111c-133">0 表示沒有限制。</span><span class="sxs-lookup"><span data-stu-id="1111c-133">0 indicates no limit.</span></span> <span data-ttu-id="1111c-134">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="1111c-134">hello default value is 0.</span></span> <span data-ttu-id="1111c-135">如果未指定此設定 」 和 「 GlobalMovementThrottleThresholdForPlacement，然後 hello 更保守的限制會使用。</span><span class="sxs-lookup"><span data-stu-id="1111c-135">If both this setting and GlobalMovementThrottleThresholdForPlacement are specified, then hello more conservative limit is used.</span></span>
  - <span data-ttu-id="1111c-136">GlobalMovementThrottleThresholdPercentageForBalancing-移動期間 hello 平衡階段中，以在 hello 叢集中的複本總數的百分比表示，允許的最大數目。</span><span class="sxs-lookup"><span data-stu-id="1111c-136">GlobalMovementThrottleThresholdPercentageForBalancing - Maximum number of movements allowed during hello balancing phase, expressed as percentage of total number of replicas in hello cluster.</span></span> <span data-ttu-id="1111c-137">0 表示沒有限制。</span><span class="sxs-lookup"><span data-stu-id="1111c-137">0 indicates no limit.</span></span> <span data-ttu-id="1111c-138">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="1111c-138">hello default value is 0.</span></span> <span data-ttu-id="1111c-139">如果未指定此設定 」 和 「 GlobalMovementThrottleThresholdForBalancing，然後 hello 更保守的限制會使用。</span><span class="sxs-lookup"><span data-stu-id="1111c-139">If both this setting and GlobalMovementThrottleThresholdForBalancing are specified, then hello more conservative limit is used.</span></span>

<span data-ttu-id="1111c-140">當指定 hello 節流的百分比，就必須指定為 0.05 的 5%。</span><span class="sxs-lookup"><span data-stu-id="1111c-140">When specifying hello throttle percentage, you'd specify 5% as 0.05.</span></span> <span data-ttu-id="1111c-141">這些節流會控管的 hello 間隔為 hello GlobalMovementThrottleCountingInterval，指定以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="1111c-141">hello interval on which these throttles are governed is hello GlobalMovementThrottleCountingInterval, which is specified in seconds.</span></span>


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

<span data-ttu-id="1111c-142">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="1111c-142">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a><span data-ttu-id="1111c-143">預設計數型節流</span><span class="sxs-lookup"><span data-stu-id="1111c-143">Default count based throttles</span></span>
<span data-ttu-id="1111c-144">我們提供了這項資訊，以免您還有較舊的叢集或是仍在已升級的叢集中保有這些組態。</span><span class="sxs-lookup"><span data-stu-id="1111c-144">This information is provided in case you have older clusters or still retain these configurations in clusters that have since been upgraded.</span></span> <span data-ttu-id="1111c-145">一般情況下，建議您使用這些取代上述 hello 百分比架構節流。</span><span class="sxs-lookup"><span data-stu-id="1111c-145">In general, it is recommended that these are replaced with hello percentage-based throttles above.</span></span> <span data-ttu-id="1111c-146">以百分比為基礎的節流預設為停用，因為這些節流時停用並取代 hello 百分比為基礎的節流之前，就會維持叢集 hello 預設節流。</span><span class="sxs-lookup"><span data-stu-id="1111c-146">Since percentage-based throttling is disabled by default, these throttles remain hello default throttles for a cluster until they are disabled and replaced with hello percentage-based throttles.</span></span> 

  - <span data-ttu-id="1111c-147">GlobalMovementThrottleThreshold – 此設定控制移動 hello 叢集中的 hello 總數透過一些時間。</span><span class="sxs-lookup"><span data-stu-id="1111c-147">GlobalMovementThrottleThreshold – this setting controls hello total number of movements in hello cluster over some time.</span></span> <span data-ttu-id="1111c-148">以秒為單位為 hello GlobalMovementThrottleCountingInterval 指定 hello 量的時間。</span><span class="sxs-lookup"><span data-stu-id="1111c-148">hello amount of time is specified in seconds as hello GlobalMovementThrottleCountingInterval.</span></span> <span data-ttu-id="1111c-149">hello GlobalMovementThrottleThreshold hello 預設值為 1000年，hello GlobalMovementThrottleCountingInterval hello 預設值為 600。</span><span class="sxs-lookup"><span data-stu-id="1111c-149">hello default value for hello GlobalMovementThrottleThreshold is 1000 and hello default value for hello GlobalMovementThrottleCountingInterval is 600.</span></span>
  - <span data-ttu-id="1111c-150">MovementPerPartitionThrottleThreshold – 此設定控制任何服務資料分割的移動 hello 的總數透過一些時間。</span><span class="sxs-lookup"><span data-stu-id="1111c-150">MovementPerPartitionThrottleThreshold – this setting controls hello total number of movements for any service partition over some time.</span></span> <span data-ttu-id="1111c-151">以秒為單位為 hello MovementPerPartitionThrottleCountingInterval 指定 hello 量的時間。</span><span class="sxs-lookup"><span data-stu-id="1111c-151">hello amount of time is specified in seconds as hello MovementPerPartitionThrottleCountingInterval.</span></span> <span data-ttu-id="1111c-152">hello MovementPerPartitionThrottleThreshold hello 預設值為 50，而且 hello MovementPerPartitionThrottleCountingInterval hello 預設值為 600。</span><span class="sxs-lookup"><span data-stu-id="1111c-152">hello default value for hello MovementPerPartitionThrottleThreshold is 50 and hello default value for hello MovementPerPartitionThrottleCountingInterval is 600.</span></span>

<span data-ttu-id="1111c-153">這些相同模式為節流 hello 百分比為基礎的節流如下所示 hello hello 組態。</span><span class="sxs-lookup"><span data-stu-id="1111c-153">hello configuration for these throttles follows hello same pattern as hello percentage-based throttling.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1111c-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1111c-154">Next steps</span></span>
- <span data-ttu-id="1111c-155">toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="1111c-155">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="1111c-156">hello 叢集資源管理員有許多選擇可用來描述 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1111c-156">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="1111c-157">toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="1111c-157">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
