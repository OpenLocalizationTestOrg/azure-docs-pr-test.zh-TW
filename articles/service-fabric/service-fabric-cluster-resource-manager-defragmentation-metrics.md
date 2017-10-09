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
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>度量的重組和 Service Fabric 中的負載
管理 hello 叢集中的負載度量 hello Service Fabric 叢集資源管理員的預設策略是 toodistribute hello 負載。 確保節點平均並加以使用，可避免熱門和冷門導致 tooboth 爭用和浪費的資源的點。 散發 hello 叢集中的工作負載，也是最安全方面存活失敗，因為它可確保失敗不取出指定的工作負載大量百分比的 hello。 

hello Service Fabric 叢集資源管理員支援不同的策略來管理負載，也就是磁碟重組。 磁碟重組表示，而不是整個 hello 叢集嘗試 toodistribute hello 使用量度量資訊，它會彙總。 彙總只逆轉 hello 預設平衡策略 – 而不是 hello 平均標準差的度量的負載降到最低，hello 叢集資源管理員會嘗試 tooincrease 它。

## <a name="when-toouse-defragmentation"></a>當 toouse 磁碟重組
Hello 叢集中的負載，會消耗一些 hello 每個節點上的資源。 某些工作負載會建立極龐大且耗用大部分或所有節點的服務。 在這些情況下，可能會，當大型取得建立工作負載沒有足夠的空間上任何節點 toorun 它們。 大型工作負載不 Service Fabric; 中的問題在這些情況下 hello 叢集資源管理員會判斷它需要 tooreorganize hello 叢集 toomake 空間供這個大量的工作負載。 不過，在 hello 同時工作負載有 toowait toobe 排程 hello 叢集中。

如果有許多的服務和狀態 toomove 周圍，它可能需要很長的時間 hello 大量的工作負載 toobe 放置 hello 叢集中。 如果在 hello 叢集中的其他工作負載也很大，而且讓長 tooreorganize，這是更有可能。 hello Service Fabric 小組測量建立時間，在此案例的模擬。 我們發現，只要叢集使用率超過 30% 到 50% 之間，建立大型服務所花費的時間就會更久。 toohandle 此案例中，我們引進了做為平衡策略磁碟重組。 我們發現，大型工作負載，特別是其中的建立時間為重要的是，磁碟重組真的協助這些新的工作負載已排入排程 hello 叢集中。

您可以設定磁碟重組度量 toohave hello hello 服務的叢集資源管理員 tooproactively 再試一次 toocondense hello 負載成較少的節點。 這有助於確保沒有幾乎大型的服務，而不需重新組織 hello 叢集中的空間。 沒有 tooreorganize hello 叢集可讓快速建立大型工作負載。

大部分的人不需要重組。 因此並不難 toofind 空間它們 hello 叢集中，服務會通常很小。 重新組織可行時，同樣地可以快速執行，因為大部分服務很小，而且可以快速且平行地移動。 不過，如果您有大型的服務，並需要快速地建立然後 hello 磁碟重組策略就是您。 我們將討論使用磁碟重組，接下來的 hello 權衡取捨。 

## <a name="defragmentation-tradeoffs"></a>重組權衡取捨
重組會放大故障的影響力，因為在故障節點上執行的服務更多。 磁碟重組也可以增加成本，因為 hello 叢集中的資源必須持有保留，等候 hello 建立大型工作負載。

hello 下列圖表提供兩個叢集的視覺表示法，已重組，一個不是。 

<center>
![比較平衡和重組叢集][Image1]
</center>

在 hello 平衡案例中，請考慮 hello 數目就是必要的 tooplace hello 最大的服務物件的移動。 在 hello 重組叢集中，hello 大量的工作負載無法置於四或五個節點而不需要的任何其他服務 toomove toowait。

## <a name="defragmentation-pros-and-cons"></a>重組的優缺點
因此，有哪些其他概念性的代價？ 以下是有關的事項 toothink 的快速資料表：

| 重組優點 | 重組缺點 |
| --- | --- |
| 能夠更快速建立大型服務 |將負載集中到較少數的節點，提高爭用 |
| 在建立期間啟用較低的資料移動 |失敗會影響更多服務，並導致更多流失 |
| 能夠豐富描述需求和空間的回收 |較複雜的整體資源管理組態 |

您可以混合重組和一般計量 hello 相同叢集中。 hello 叢集資源管理員會嘗試 tooconsolidate hello 重組度量盡可能時分配 hello 其他人。 hello 結果的混合磁碟重組和平衡策略取決於許多因素，包括：
  - hello 數目的平衡與 hello 的幾個磁碟重組度量的度量
  - 是否有任何服務同時使用兩種類型的計量 
  - hello 衡量標準權數
  - 目前的計量負載
  
試驗是必要的 toodetermine hello 確切必要組態。 我們建議先徹底測量您的工作負載，然後再於生產中啟用重組計量。 特別是當磁碟重組和平衡的度量 hello 中混用相同的服務。 

## <a name="configuring-defragmentation-metrics"></a>設定重組度量
設定磁碟重組度量資訊是全域的決策，在 hello 叢集中，並選取個別的度量來進行磁碟重組。 下列組態程式碼片段的 hello 顯示 tooconfigure 度量的磁碟重組。 在此情況下，"Metric1 」 設定為磁碟重組度量，"Metric2 」 將會繼續正常平衡 toobe 時。 

ClusterManifest.xml：

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：

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


## <a name="next-steps"></a>後續步驟
- hello 叢集資源管理員具有 man 選項描述 hello 叢集。 toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)
- 度量資訊是如何 hello Service Fabric 叢集資源管理員管理耗用量和 hello 叢集中的容量。 toolearn 更多關於度量和如何 tooconfigure 它們，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
