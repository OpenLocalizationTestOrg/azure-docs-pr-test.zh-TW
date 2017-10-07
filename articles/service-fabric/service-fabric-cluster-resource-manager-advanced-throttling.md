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
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>節流 hello Service Fabric 叢集資源管理員
即使您已正確設定 hello 叢集資源管理員，可以取得中斷 hello 叢集。 例如，可能同時節點和容錯網域失敗-所發生的升級期間會發生什麼事？hello 叢集資源管理員一律會嘗試 toofix 一切耗用嘗試 tooreorganize 並修正 hello 叢集 hello 叢集資源。 流速協助提供機制，讓 hello 叢集可以使用資源 toostabilize-hello 節點回來，hello 網路磁碟分割修復、 部署已更正的位元。

toohelp 以這類情況下，hello Service Fabric 叢集資源管理員包含數個節流。 這些節流功能個個都是強大無比的工具。 一般來說，如果您沒有仔細規劃並測試，就請不要對其進行變更。

如果您變更 hello 叢集資源管理員的節流，您應該調整它們 tooyour 的預期實際負載。 您可決定您需要的 toohave 某些節流的位置，即使它表示 hello 叢集在某些情況下會較長的 toostabilize。 測試是節流的必要的 toodetermine hello 正確值。 流速需要 toobe 夠高 tooallow hello 叢集 toorespond toochanges 在合理的時間，而且低足夠 tooactually 避免過多的資源耗用量。 

大部分的 hello 時間，我們已看到客戶使用已因為它們已在資源的限制環境的節流。 某些範例可能是有限的網路頻寬的個別節點或不能 toobuild 中的許多可設定狀態之複本的磁碟平行到期 toothroughput 限制。 沒有流速作業無法不勝負荷這些資源，導致作業 toofail 或會變慢。 在這些情況下使用節流閥的客戶，而且知道它們所擴充 hello 一段時間會花費 hello 叢集 tooreach 穩定的狀態。 客戶也了解進行節流時，最後可能會在整體可靠性降低的情況下運作。


## <a name="configuring-hello-throttles"></a>設定 hello 節流

Service Fabric 有兩種節流 hello 複本移動數目的機制。 服務網狀架構 5.7 之前就存在的 hello 預設機制代表節流設定為絕對數字之允許的移動。 但這種方式不適用於所有規模的叢集。 特別是，大型叢集 hello 預設值可以是太小，大幅降低平衡甚至會在必要時，同時不有任何作用中較小的群集。 這個先前機制已被取代的百分比為基礎的節流，其規模會更好的動態叢集服務的 hello 數字而定期變更節點。

hello 節流根據 hello hello 叢集中的複本數目的百分比表示。 基礎 Percetage 流速啟用表達 hello 規則: 「 不會移動超過 10%的複本以 10 分鐘間隔 」，例如。

hello 百分比為基礎的節流組態設定是：

  - GlobalMovementThrottleThresholdPercentage-移動，也可以隨時在叢集中允許的最大數目以 hello 叢集中的複本總數的百分比表示。 0 表示沒有限制。 hello 預設值為 0。 如果未指定此設定 」 和 「 GlobalMovementThrottleThreshold，然後 hello 更保守的限制會使用。
  - GlobalMovementThrottleThresholdPercentageForPlacement-允許在 hello 放置階段中，以在 hello 叢集中的複本總數的百分比表示移動的最大數目。 0 表示沒有限制。 hello 預設值為 0。 如果未指定此設定 」 和 「 GlobalMovementThrottleThresholdForPlacement，然後 hello 更保守的限制會使用。
  - GlobalMovementThrottleThresholdPercentageForBalancing-移動期間 hello 平衡階段中，以在 hello 叢集中的複本總數的百分比表示，允許的最大數目。 0 表示沒有限制。 hello 預設值為 0。 如果未指定此設定 」 和 「 GlobalMovementThrottleThresholdForBalancing，然後 hello 更保守的限制會使用。

當指定 hello 節流的百分比，就必須指定為 0.05 的 5%。 這些節流會控管的 hello 間隔為 hello GlobalMovementThrottleCountingInterval，指定以秒為單位。


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：

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

### <a name="default-count-based-throttles"></a>預設計數型節流
我們提供了這項資訊，以免您還有較舊的叢集或是仍在已升級的叢集中保有這些組態。 一般情況下，建議您使用這些取代上述 hello 百分比架構節流。 以百分比為基礎的節流預設為停用，因為這些節流時停用並取代 hello 百分比為基礎的節流之前，就會維持叢集 hello 預設節流。 

  - GlobalMovementThrottleThreshold – 此設定控制移動 hello 叢集中的 hello 總數透過一些時間。 以秒為單位為 hello GlobalMovementThrottleCountingInterval 指定 hello 量的時間。 hello GlobalMovementThrottleThreshold hello 預設值為 1000年，hello GlobalMovementThrottleCountingInterval hello 預設值為 600。
  - MovementPerPartitionThrottleThreshold – 此設定控制任何服務資料分割的移動 hello 的總數透過一些時間。 以秒為單位為 hello MovementPerPartitionThrottleCountingInterval 指定 hello 量的時間。 hello MovementPerPartitionThrottleThreshold hello 預設值為 50，而且 hello MovementPerPartitionThrottleCountingInterval hello 預設值為 600。

這些相同模式為節流 hello 百分比為基礎的節流如下所示 hello hello 組態。

## <a name="next-steps"></a>後續步驟
- toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)
- hello 叢集資源管理員有許多選擇可用來描述 hello 叢集。 toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)
