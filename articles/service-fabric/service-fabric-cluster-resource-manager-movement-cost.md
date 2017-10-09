---
title: "Service Fabric 叢集 Resource Manager：移動成本 | Microsoft Docs"
description: "Service Fabric 服務的移動成本概觀"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a>服務移動成本
嘗試 toodetermine 何種變更 toomake tooa 叢集 hello 成本，這些變更時，會將視為 hello Service Fabric 叢集資源管理員的因素。 "cost"hello 概念是針對可以提升多少 hello 叢集買賣關閉。 成本在移動服務進行平衡、重組和其他需求時納入考量因素。 hello 的目標是在 hello toomeet hello 需求最低干擾或昂貴的方法。 

移動服務會花費最少的 CPU 時間和網路頻寬。 可設定狀態服務，它需要複製 hello 這些服務，因而會耗用額外的記憶體和磁碟的狀態。 Azure Service Fabric 叢集資源管理員出現該 hello 降到最低 hello 成本的解決方案，可協助確保 hello 叢集資源不不必要地花費。 不過，您也不想 tooignore 解決方案，將會大幅改善 hello hello 叢集中的資源配置。

hello 叢集資源管理員有兩種運算成本，以及它會嘗試 toomanage hello 叢集時，限制他們的方式。 hello 第一種機制只要計算它會使每次移動。 如果這兩個方案會產生與 hello 相同平衡 （分數），然後 hello 叢集資源管理員慣用一個 hello 以 hello 最低成本 （總數會移動）。

此策略效果不錯。 但是若使用預設或靜態負載時，不太可能在任何複雜的系統中所有的移動都相等。 有些可能 toobe 昂貴。

## <a name="setting-move-costs"></a>設定移動成本 
在建立時，您可以指定服務的 hello 預設移動成本：

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C#： 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

您也可以指定或 MoveCost 動態更新服務的 hello 服務已經建立完成之後： 

PowerShell： 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C#：

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>以動態方式指定每個複本的移動成本

hello 上述程式碼片段是否所有指定 MoveCost 外部 hello 服務本身一次的整個服務。 不過，移動成本是最有用時，透過其使用期限的 hello 移動成本，特定服務物件的變更。 由於 hello 服務本身或許 hello 最好了解如何昂貴它們是 toomove 給定的時間，沒有服務 tooreport 自己個別移動成本在執行階段 API。 

C#：

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>移動成本的影響
MoveCost 有四個層級：零、低、中和高。 MoveCosts 是相對 tooeach 其他，除了零。 零移動成本表示移動是免費的而且不應該列入 hello hello 解決方案的分數。 設定移動成本 tooHigh 沒有*不*保證該 hello 複本保持在同一個地方。

<center>
![移動成本作為選取要移動之複本的因素][Image1]
</center>

MoveCost 可協助您尋找 hello 解決方案原因整體 hello 最少中斷和是最簡單的 tooachieve 時仍抵達相等的平衡。 服務概念，可以是成本的相對 toomany 項目。 hello 最常見的因素計算移動成本是：

- 狀態或資料 hello 服務有 toomove hello 數量。
- 中斷連線的用戶端 hello 成本。 移動主要複本會通常比 hello 成本，將次要複本。
- 中斷執行中作業的 hello 成本。 某些作業在 hello 資料儲存區層級或回應 tooa 用戶端呼叫中執行的作業成本很高。 在特定時間點之後, 您不想 toostop 如果您不需要它們。 因此 hello 作業正在進行的作業，而您會增加移動此服務物件 tooreduce hello 可能性 hello 移動成本。 當 hello 作業完成時，您會設定 hello 成本後 toonormal。

## <a name="enabling-move-cost-in-your-cluster"></a>在您的叢集中啟用移動成本
為了讓 hello 更細微的 MoveCosts toobe 列入考量，MoveCost 必須啟用您的叢集中。 這項設定，計算移 hello 預設模式用來計算 MoveCost，而不會忽略 MoveCost 報告。


ClusterManifest.xml：

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a>後續步驟
- Service Fabric 叢集資源管理員會在 hello 叢集中使用度量 toomanage 耗用量和容量。 toolearn 更多關於度量和如何 tooconfigure 它們，請參閱[管理資源耗用和服務網狀架構中的負載度量與](service-fabric-cluster-resource-manager-metrics.md)。
- toolearn 如何 hello 叢集資源管理員管理和 hello 叢集中的負載平衡，請參閱[平衡 Service Fabric 叢集](service-fabric-cluster-resource-manager-balancing.md)。

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
