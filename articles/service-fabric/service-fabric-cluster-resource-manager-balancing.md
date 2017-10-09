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
# <a name="balancing-your-service-fabric-cluster"></a>平衡 Service Fabric 叢集
hello Service Fabric 叢集資源管理員支援動態負載變更，對回應 tooadditions 或移除的節點或服務。 它也會自動更正條件約束違規，並主動重新平衡 hello 叢集。 但是這些動作執行的頻率，以及觸發它們的項目是什麼？

叢集資源管理員會執行該 hello 有三種不同的工作。 如下：

1. 放置 - 這個階段涉及安置任何遺漏的具狀態複本或無狀態執行個體。 放置包含新服務，也包含處理已失敗的具狀態複本或無狀態執行個體。 刪除和捨棄複本或執行個體都是在這裡處理。
2. 條件約束檢查 – 此階段進行檢查並修正 hello 系統中的 hello 不同的位置限制 （規則） 的違規情形。 規則範例包括像是確保節點不超出容量，以及符合服務的放置條件約束。
3. 平衡-這個階段會檢查 toosee 重新平衡有必要時根據 hello 設定需要不同的度量資訊的餘額的層級。 如果是它會嘗試的 toofind hello 中的排列方式也就是叢集多個平衡。

## <a name="configuring-cluster-resource-manager-timers"></a>設定叢集資源管理員計時器
hello 第一組控制項周圍平衡是一組的計時器。 頻率 hello 叢集資源管理員會檢查 hello 叢集，並採取修正動作，這些計時器控管。

這兩種不同類型的叢集資源管理員可更正 hello 受到控管其頻率的不同計時器。 當每個計時器啟動時，會排程 hello 工作。 根據預設 hello 資源管理員：

* 每 1/10 秒掃描一次其狀態並套用更新 (例如記錄某個節點已關閉)
* 設定 hello 放置核取旗標 
* 每秒設定 hello 條件約束檢查旗標
* 設定 hello 平衡每五秒的旗標。

控管這些計時器 hello 組態的範例如下：

ClusterManifest.xml：

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：

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

現今 hello 叢集資源管理員只會執行其中一個動作一次，以循序方式。 這就是為什麼我們 toothese 計時器，為 「 最小間隔 」，請參閱和 hello hello 計時器與 [設定旗標] 當取得採取的動作。 例如，叢集資源管理員會負責的擱置中的 hello 要求 toocreate 服務之前平衡 hello 叢集。 您可以看到所指定的 hello 預設時間間隔，hello 叢集資源管理員會掃描的任何項目它需求 toodo 常見問題。 通常這表示每個步驟期間所做的變更的 hello 集很小。 經常進行小變更可讓叢集資源管理員 toobe hello 回應 hello 叢集中所發生的事項時。 hello 預設計時器提供某些批次處理後 hello 的許多相同的事件類型傾向 toooccur 同時。 

例如，當節點失敗時，他們可以一次對整個容錯網域執行這個動作。 所有這些失敗會擷取期間 hello 下一個狀態更新之後 hello *PLBRefreshGap*。 hello 更正是在 hello 遵循條件約束檢查的位置，並平衡執行期間決定的。 依預設 hello 叢集資源管理員不是透過小時 hello 叢集中變更的掃描，然後再 tooaddress 所有變更一次。 這樣會導致 toobursts 的變換。

hello 叢集資源管理員也需要一些其他資訊 toodetermine 如果 hello 叢集不平衡。 因此，我們有其他兩個的設定︰「平衡臨界值」和「活動臨界值」。

## <a name="balancing-thresholds"></a>平衡臨界值
平衡臨界值為 hello 主控制項，用於觸發重新平衡。 hello 平衡臨界值標準是_比率_。 節點上 hello 標準 hello 負載最載入除以 hello 負載量 hello 至少載入的節點是否超過該度量*BalancingThreshold*，然後 hello 叢集不平衡。 如此一來平衡為觸發的 hello 叢集資源管理員會檢查下一個時間 hello。 hello *MinLoadBalancingInterval*計時器定義 hello 叢集資源管理員應檢查的頻率如果需要重新平衡。 檢查並不意謂著有發生任何事情。 

每個標準為基礎 hello 叢集中定義的一部分定義平衡臨界值。 如需有關計量的詳細資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)。

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：

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

<center>
![平衡臨界值範例][Image1]
</center>

在此範例中，每個服務皆取用一單位的某個計量。 在 hello 上方範例中，hello 節點上的最大負載為 5，hello 最小值為二。 例如，假設該 hello 平衡這個標準的臨界值為 3。 因為 hello 叢集中的 hello 比例是 5/2 = 2.5，也就是少於 hello 指定平衡臨界值的三個 hello 叢集平衡。 無平衡 hello 叢集資源管理員會檢查時觸發。

Hello 下方範例中，在 hello 節點上的最大載入時 hello 最小值是 2，產生五個比例是 10。 五個大於 hello 指定平衡臨界值的三個該標準。 如此一來，重新平衡執行將會排定平衡計時器引發的下一個時間 hello。 在此情況下某些負載會是通常分散式的 tooNode3。 Hello Service Fabric 叢集資源管理員不會使用窮盡方法，因為某些負載也可能是分散式的 tooNode2。 

<center>
![平衡臨界值範例動作][Image2]
</center>

> [!NOTE]
> 「平衡」會處理兩個不同的策略來管理叢集中的負載。 hello hello 叢集資源管理員使用的預設策略 hello hello 叢集中的節點都 toodistribute 負載。 hello 其他策略是[重組](service-fabric-cluster-resource-manager-defragmentation-metrics.md)。 執行磁碟重組 hello 期間執行的相同平衡。 hello 平衡和重組策略可以用不同度量 hello 內相同的叢集。 服務可以同時有平衡和重組計量。 磁碟重組度量，hello hello 比例載入 hello 叢集觸發程序時重新平衡_下方_hello 平衡臨界值。 
>

取得以下 hello 平衡臨界值不是明確的目標。 平衡臨界值只是*觸發程序*。 平衡執行、 當 hello 叢集資源管理員會決定哪些增強功能，它可以進行，如果有的話。 因為平衡搜尋開始並不代表任何項目移動。 有時 hello 叢集是 toocorrect 不平衡，但太受條件約束。 或者，hello 改良需要移動，也都是[昂貴](service-fabric-cluster-resource-manager-movement-cost.md))。

## <a name="activity-thresholds"></a>活動臨界值
有時候，節點是相對較不平衡，雖然 hello*總*的 hello 叢集中的負載量很低。 hello 缺乏負載可能是暫時性的 dip，或因為 hello 叢集是新的和取得只需啟動載入。 在任一情況下，您可能不想平衡 hello 叢集，因為沒有獲得小 toobe toospend 時間。 如果 hello 叢集經歷了平衡，您會花在網路中，計算資源 toomove 項目，而不進行任何大型*絕對*差異。 不必要的 tooavoid 移動時，會有另一個控制又稱為活動臨界值。 活動臨界值可讓您 toospecify 某些絕對下限 」 活動。 如果沒有節點超過此閾值，平衡未觸發，即使 hello 平衡臨界值到達。

假設我們為這個計量保留平衡臨界值 3。 同時假設我們有活動臨界值 1536。 在 hello 第一種情況下，平衡每 hello hello 叢集時平衡臨界值那里沒有節點符合該活動臨界值，因此不會發生。 在 hello 下方範例中，Node1 位於 hello 活動臨界值。 由於同時 hello 平衡臨界值，而且超過 hello 標準 hello 活動臨界值時，將排程平衡。 例如，讓我們看看下列圖表中的 hello: 

<center>
![活動臨界值範例][Image3]
</center>

平衡臨界值，就像活動臨界值會定義每個-度量透過 hello 叢集定義：

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：

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

平衡及活動的臨界值都同時 hello 平衡臨界值和 hello 超過活動臨界值時，才可以觸發繫結的 tooa 特定度量的平衡相同的度量。

## <a name="balancing-services-together"></a>一起平衡服務
Hello 叢集是否不平衡是整個叢集的決策。 不過，我們要予以修正 hello 方式移動個別的服務複本和需要的執行個體。 這很合理，對吧？ 如果其中一個節點上堆疊記憶體，多個複本或執行個體可能導致 tooit。 修正 hello 不平衡，可能需要移動任何 hello 可設定狀態的複本或無狀態的執行個體使用 hello 平衡度量資訊。

偶爾但未本身不平衡的服務取得移動 （請記住 hello 討論的本機和全域加權稍早）。 為什麼當服務的計量平衡時服務會移動？ 看看以下範例：

- 假設有四個服務：Service1、Service2、Service3 及 Service4。 
- Service1 報告計量 Metric1 和 Metric2。 
- Service2 報告計量 Metric2 和 Metric3。 
- Service3 報告計量 Metric3 和 Metric4。
- Service4 報告計量 Metric99。 

您應該可以看出這個範例要表達什麼：有鏈結！ 我們並非實際上擁有 4 個獨立的服務，而是有 3 個相關的服務，以及一個獨立的服務。

<center>
![將服務一起平衡][Image4]
</center>

因為此鏈結中，很可能，在 1-4 的度量不平衡可能會導致複本或執行個體屬於 tooservices 周圍的 1-3 toomove。 我們也知道計量 1、2 或 3 若發生不平衡，並不會導致 Service4 中發生移動。 因為移動 hello 複本會有任何點或執行個體屬於 tooService4 周圍可以不絕對度量 1-3 tooimpact hello 之間取得平衡。

hello 叢集資源管理員會自動找出相關的服務。 新增、 移除或變更服務的 hello 度量可能會影響它們的關聯性。 例如，之間的平衡 Service2 的兩個回合可能已更新的 tooremove Metric2。 這會中斷 Service1 和 Service2 之間的 hello 鏈結。 現在，您擁有的是三個相關服務群組，而非兩個︰

<center>
![將服務一起平衡][Image5]
</center>

## <a name="next-steps"></a>後續步驟
* 度量資訊是如何 hello Service Fabric 叢集資源管理員管理耗用量和 hello 叢集中的容量。 toolearn 更多關於度量和如何 tooconfigure 它們，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)
* 移動成本是訊號某些服務會比其他更耗費資源 toomove toohello 叢集資源管理員的一種方式。 如需有關移動成本的詳細資訊，請參閱太[這篇文章](service-fabric-cluster-resource-manager-movement-cost.md)
* hello 叢集資源管理員有數個節流，您可以設定下變換 tooslow hello 叢集中。 這些節流通常不是必要的，但若有需要，您可以參閱 [這裡](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
