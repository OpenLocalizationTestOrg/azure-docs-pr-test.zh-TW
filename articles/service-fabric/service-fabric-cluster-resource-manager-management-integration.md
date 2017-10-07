---
title: "aaaService 網狀架構叢集資源管理員的管理整合 |Microsoft 文件"
description: "Hello 整合點之間 hello 叢集資源管理員和服務網狀架構管理的概觀。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>叢集資源管理員與 Service Fabric 叢集管理整合
hello Service Fabric 叢集資源管理員不中的磁碟機升級服務的網狀架構，但它與。 hello hello 叢集資源管理員可協助管理是由追蹤 hello 的第一種方法所需的 hello 叢集和內文中的 hello 服務狀態。 它不能放 hello 所需的組態中的 hello 叢集時，健全狀況報表會傳送 hello 叢集資源管理員。 例如，如果沒有足夠容量 hello 叢集資源管理員會送出健全狀況警告和指出 hello 發生問題的錯誤。 整合的其他片段都有 toodo 與升級的運作方式。 hello 叢集資源管理員會在升級期間稍微變更其行為。  

## <a name="health-integration"></a>健康狀態整合
hello 叢集資源管理員經常會追蹤 hello 規則中所定義的放置您的服務。 它也會追蹤 hello 剩餘整體容量 hello 節點 hello 叢集中，以及上 hello 叢集中的每個度量。 如果無法滿足這些規則，或容量不足，則會發出健康情況警告和錯誤。 例如，如果節點是透過容量和 hello 叢集資源管理員會嘗試 toofix hello 情況移動服務。 如果它不能更正 hello 情況發出健全狀況警告指出哪一個節點透過容量，以及哪些度量。

Hello 資源管理員的健全狀況警告的另一個範例是放置條件約束違規。 例如，如果您已定義位置條件約束 (例如`“NodeColor == Blue”`) 和 hello 資源管理員偵測到該條件約束的違規情形，請發出健全狀況警告。 這是自訂的條件約束和 hello 預設條件約束 （例如 hello 容錯網域和升級網域的條件約束），則為 true。

以下是這類健康狀態報告的範例。 在此情況下，hello 健全狀況報表是一個 hello 系統服務的資料分割。 hello 健全狀況訊息會指出的 hello 該分割的複本會暫時封裝為太少的 「 升級 」 網域。

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

以下是此健康狀態訊息要告訴我們的事情︰

1. 所有的 hello 複本本身都是狀況良好： 每個都有 AggregatedHealthState: [確定]
2. 目前違反 hello 升級網域散發條件約束。 這表示特定升級網域擁有這個磁碟的過多分割複本。
3. 哪些節點包含 hello 複本導致 hello 違規。 在此情況下是 hello 名稱"Node.8"hello 節點
4. 無論此分割區是否正在升級 (「Currently Upgrading -- false」)
5. hello 散發原則針對此服務: 「 發佈原則--封裝 」。 這由 hello `RequireDomainDistribution` [位置原則](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing)。 「封裝」表示在此情況下_不_需要 DomainDistribution，因此可知道並未替該服務指定放置原則。 
6. Hello 報表何時發生-2015 年 8 月 10 日下午 7:13:02

資訊在實際執行 toolet 您知道某項目有任何錯誤，而且也會引發用 toodetect 這次方警示等停止不正確的升級。 在此情況下，我們可能會想 toosee，如果我們可以找出 hello 資源管理員必須 toopack hello 複本到 hello 升級網域的原因。 通常封裝是暫時性的因為在 hello hello 節點其他升級網域已關閉，例如。

假設 hello 叢集資源管理員正在嘗試 tooplace 某些服務，但是沒有任何工作的解決方案。 當服務不放時，通常是其中一個 hello 下列原因：

1. 某些暫時性的狀況，變成無法 tooplace 此服務執行個體或複本正確
2. hello 服務位置需求是 unsatisfiable。

在這些情況下，從 hello 叢集資源管理員的健康情況報告協助您判斷為什麼無法放置 hello 服務。 我們會呼叫此處理序 hello 條件約束刪除順序。 期間，hello 系統會查核透過影響 hello 服務和記錄它們不需要設定 hello 條件約束。 如此一來，當服務不能 toobe 用來放置，您可以看到也消除了哪些節點和原因。

## <a name="constraint-types"></a>條件約束類型
我們要討論每一個 hello 這些健康情況報告中的不同條件約束。 當複本不能放時，您會看到健全狀況的訊息相關的 toothese 條件約束。

* **ReplicaExclusionStatic**和**ReplicaExclusionDynamic**： 這些條件約束表示方案遭到拒絕，因為兩個服務物件，從 hello 相同的資料分割會有 toobe 置於 hello 相同節點。 不允許這麼做是因為該節點的失敗會過度影響該分割區。 ReplicaExclusionStatic 和 ReplicaExclusionDynamic 是幾乎相同的規則和 hello 差異無關緊要的 hello。 如果您會看到包含任一 hello ReplicaExclusionStatic 或 ReplicaExclusionDynamic 條件約束，hello 叢集資源管理員條件約束刪除順序認為沒有足夠的節點。 這需要剩餘解決方案 toouse 這些無效的位置，這不被允許。 hello hello 序列中的其他條件約束通常告訴為什麼節點會被排除在 hello 第一個位置。
* **PlacementConstraint**： 如果您看到此訊息，表示我們刪除某些節點，因為它們不符合 hello 服務位置條件約束。 我們目前設定的 hello 位置條件約束時追蹤此訊息的一部分。 如果您已定義放置條件約束，則這是正常情形。 不過，如果位置條件約束不正確造成太多節點 toobe 消除這是如何您會注意到。
* **NodeCapacity**： 這個條件約束表示叢集資源管理員無法將 hello 複本放在該 hello hello 指示節點，因為，會將它們放低於產能。
* **同質**： 這個條件約束表示我們無法 hello 複本放在受影響的 hello 節點上因為它會導致 hello 親和性條件約束違規。 如需同質性的詳細資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
* **FaultDomain**和**UpgradeDomain**： 這個條件約束排除節點，如果在 hello 放 hello 複本指示節點會造成特定的錯誤或升級網域中的封裝。 討論這個條件約束的數個範例會出現在 hello 主題[容錯和升級網域條件約束和產生的行為](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**： 通常不應該看到從 hello 方案移除節點，因為最佳化預設會執行這個條件約束。 hello 慣用位置限制式也會出現在升級期間。 在升級期間是使用的 toomove 服務後 toowhere hello 升級啟動。

## <a name="blocklisting-nodes"></a>封鎖節點
另一個健全狀況訊息 hello 叢集資源管理員報告時，節點是 blocklisted。 您可以將封鎖視為自動套用的暫時性條件約束。 啟動該服務類型的執行個體時，發生重複失敗的節點會遭封鎖。 節點是依照服務類型來封鎖。 某個服務類型的節點可能會被封鎖，另一個服務類型的節點則未被封鎖。 

您會看到 blocklisting 通常在開發期間啟用： 在啟動時導致您的服務主機 toocrash 的一些錯誤。 Service Fabric toocreate hello 服務主機嘗試幾次，並 hello 失敗持續發生。 在少數的嘗試後 hello 節點取得 blocklisted，及 hello 叢集資源管理員會嘗試其他地方 toocreate hello 服務。 如果該失敗情況持續發生多個節點上，很可能所有 hello 有效節點在 hello 叢集最後會封鎖。 Blocklisting 也可以移除，不足，所以無法成功啟動 hello 服務 toomeet hello 預期規模太多節點。 您通常會看到其他錯誤或警告 hello hello 服務低於 hello 的複本或執行個體計數，以及健全狀況的訊息，指出哪一個 hello 失敗表示叢集資源管理員時，會導致 toohelloblocklisting hello 第一個位置中。

封鎖不是永久情況。 請稍候幾分鐘 hello 節點移除 hello 封鎖清單和服務網狀架構可能會重新啟動該節點上的 hello 服務。 如果服務繼續 toofail，hello 節點再次成為 blocklisted 該服務類型。 

### <a name="constraint-priorities"></a>條件約束優先順序

> [!WARNING]
> 不建議變更條件約束優先順序，因為可能對叢集造成顯著的負面影響。 hello 以下資訊供參考的 hello 預設條件約束的優先權，且其行為。 
>

所有這些條件約束，您可能有已考慮"Hi – 我認為容錯網域條件約束是 hello 最重要的是，我的系統中。 在訂單 tooensure hello 容錯網域違反條件約束不是，我願意 tooviolate 其他條件約束。 」

可以使用不同的優先順序等級來設定條件約束。 它們是：

   - 「硬性」(0)
   - 「彈性」(1)
   - 「最佳化」(2)
   - 「關閉」(-1)。 
   
根據預設，大部分的 hello 條件約束會設定為硬式條件約束。

變更 hello 優先順序條件約束是常見的。 有好幾次 toochange，通常是其他 bug 或已影響 hello 環境的行為周圍 toowork 優先順序條件約束所需。 通常 hello hello 條件約束優先順序的基礎結構的彈性，曾很好，但通常不需要。 大部分的 hello 時間的所有項目會位於其預設優先權。 

hello 優先權等級不表示指定的條件約束_將_違反，也不一定會符合。 條件約束優先順序會定義強制執行條件約束的順序。 優先權會定義 hello 權衡取捨時，它不可能 toosatisfy 所有條件約束。 通常除非沒有其他進行 hello 環境中的項目，可以滿足所有 hello 條件約束。 就會導致 tooconstraint 違規案例的一些範例包括衝突的條件約束，或大量的並行失敗。

在進階的情況下，您可以變更 hello 的優先順序條件約束。 例如，假設您想要 tooensure 必要 toosolve 節點容量發出時，一律會違反親和性。 tooachieve，您無法設定 hello hello 親和性條件約束太 「 軟性 」 (1) 的優先順序和離開 hello 容量限制設定太 「 硬式 」 (0)。

hello hello 不同的條件約束的預設優先權值會指定 hello 下列組態：

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>容錯網域和升級網域的條件約束
hello 叢集資源管理員會希望 tookeep 遍佈容錯和升級網域的服務。 它的模型做為條件約束 hello 叢集資源管理員的引擎內。 如需使用方式的詳細資訊和其特定的行為，請參閱 hello 發行項上[叢集設定](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior)。

hello 叢集資源管理員可能需要 toopack 一些複本至中順序 toodeal 與升級、 失敗或其他條件約束違規的升級網域。 通常壓縮成錯誤或升級網域，會發生時，才有一些失敗或其他變換導致無法正確放置 hello 系統中。 如果您想 tooprevent 壓縮，即使在這些情況下，您可以利用 hello `RequireDomainDistribution` [位置原則](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing)。 請注意，這可能會產生影響服務可用性和可靠性的副作用，請審慎考慮。

Hello 環境已正確設定，如果所有條件約束必須確實遵守，即使在升級期間。 hello 的重點為叢集資源管理員，會為您的條件約束觀賞該 hello。 偵測到違規時，它立即將它報告，並嘗試 toocorrect hello 問題。

## <a name="hello-preferred-location-constraint"></a>hello 慣用的位置限制式
hello PreferredLocation 條件約束是有點不同，它有兩個不同的用途。 這個條件約束的其中一種用法是在應用程式升級期間。 hello 叢集資源管理員會在升級期間，自動管理這個條件約束。 它是使用的 tooensure，當升級已完成複本傳回 tootheir 初始位置。 hello hello PreferredLocation 條件約束的其他用途為 hello [ `PreferredPrimaryDomain`位置原則](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)。 這兩種最佳化，而且因此 hello PreferredLocation 條件約束，是設定得 hello 唯一條件約束是預設的 「 最佳化 」。

## <a name="upgrades"></a>升級
hello 叢集資源管理員也可協助應用程式和其兩個工作的叢集升級期間：

* 確保不會影響 hello 叢集的 hello 規則
* 順暢地嘗試 toohelp hello 升級到

### <a name="keep-enforcing-hello-rules"></a>保留強制 hello 規則
hello 留意的重點 toobe 是 hello 規則 – hello 嚴格的條件約束類似放置條件約束和容量-仍會在升級期間強制執行。 放置條件約束可確保工作負載只在允許的位置執行，即在升級期間也一樣。 服務受到極大的條件約束時，升級可能需要較長的時間。 Hello 服務或 hello 節點執行時是關閉，可能會有幾個選項，它可用的更新。

### <a name="smart-replacements"></a>聰明取代
升級啟動時，資源管理員 hello 的快照 hello 叢集的 hello 目前的排列方式。 每個升級網域完成時，它會嘗試 tooreturn hello 服務，該升級網域 tootheir 原始排列方式。 這種方式有最多兩個轉換服務 hello 升級期間。 有一個移出受影響的 hello 節點，而且其中一個向後移。 傳回 hello 叢集或服務 toohow hello 升級也可確保 hello 升級之前不會影響 hello 叢集的 hello 版面配置。 

### <a name="reduced-churn"></a>減少流失
在升級期間，會發生情況的另一項為叢集資源管理員會關閉平衡該 hello。 防止平衡可避免不必要的反應 toohello 升級本身，例如將服務移到清空 hello 升級的節點。 如果有問題的 hello 升級叢集升級，然後 hello 整個叢集不平衡 hello 升級期間。 條件約束檢查會持續作用，只有移動根據 hello 主動平衡的計量已停用。

### <a name="buffered-capacity--upgrade"></a>緩衝處理的容量和升級
通常您希望 hello 升級 toocomplete 即使 hello 叢集條件約束或關閉 toofull。 Hello 叢集的 hello 容量的管理會更重要在升級期間比平常。 根據 hello 必須為 hello 升級彙透過 hello 叢集移轉介於 5 到 20%的容量的升級網域數目。 該工作有 toogo 的某處。 這是其中 hello 概念[緩衝處理容量](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity)很有用。 在正常作業期間，系統會採用緩衝處理的容量。 hello 叢集資源管理員可能會在必要時升級期間，填滿向上 tootheir 總容量 （使用 hello 緩衝區） 的節點。

## <a name="next-steps"></a>後續步驟
* Hello 從頭開始並[取得簡介 toohello Service Fabric 叢集資源管理員](service-fabric-cluster-resource-manager-introduction.md)
