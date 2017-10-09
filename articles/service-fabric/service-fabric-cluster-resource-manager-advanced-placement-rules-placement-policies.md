---
title: "aaaService 網狀架構叢集資源管理員的位置原則 |Microsoft 文件"
description: "Service Fabric 服務的其他放置原則和規則的概觀"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a>Service Fabric 服務的放置原則
位置原則是可以在某些特定的較不常見的情況下使用的 toogovern 服務位置的其他規則。 這些情況的一些例子如下︰

- 您的 Service Fabric 叢集跨越一段地理距離 (例如多個內部部署資料中心) 或跨越多個 Azure 區域
- 您的環境跨越多個區域的地緣政治或法律控制項或某些其他您擁有其原則界限的情況下需要 tooenforce
- 有到期 toolarge 距離或使用速度較慢或較不可靠的網路連結的通訊延遲或效能考量
- 您需要特定工作負載共置，以做為最佳效果，與其他工作負載，或在鄰近 toocustomers tookeep

大部分的這些需求對齊 hello 實體配置 hello 叢集中，表示，如 hello hello 叢集的容錯網域。 

hello 進階的放置原則可協助解決這些案例包括：

1. 無效的網域
2. 所需的網域
3. 慣用的網域
4. 不允許封裝複本

無法透過節點屬性及位置條件約束，設定大部分的 hello 控制項，但有些是更複雜。 toomake 方面更簡單，hello Service Fabric 叢集資源管理員會提供這些額外的位置原則。 放置原則可以依個別具名服務執行個體來設定， 還可以動態更新。

## <a name="specifying-invalid-domains"></a>指定無效的網域
hello **InvalidDomain**位置原則可讓您 toospecify 特定容錯網域是無效的特定服務。 此原則可確保特定的服務絕對不會在特定的區域中執行，例如，基於地緣政治或公司政策的緣故。 您可以透過個別原則指定多個無效的網域。

<center>
![無效的網域範例][Image1]
</center>

程式碼：

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>指定所需的網域
hello 需要網域位置原則需要 hello 服務只能在 hello 指定網域中。 您可以透過個別原則指定多個所需的網域。

<center>
![所需的網域範例][Image2]
</center>

程式碼：

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>指定的可設定狀態服務的 hello 主要複本的慣用的網域
hello 慣用的主要網域指定 hello 容錯網域 tooplace hello Primary in。 hello 主要最後會在這個網域中的所有項目為狀況良好時。 如果 hello 網域或 hello 主要複本失敗，或關閉，主要 hello 移動 toosome 其他位置，最好是在 hello 相同的網域。 如果這個新的位置不在 hello 慣用的網域，hello 叢集資源管理員移回儘速 toohello 慣用的網域。 當然，此設定僅適用於具狀態服務。 如果叢集跨越 Azure 區域或多個資料中心，但具有選擇放置在特定位置的服務，此原則最有用。 讓主要複本會關閉 tootheir 使用者或其他有助於提供較低的延遲時間，特別是針對讀取，會由主要複本會根據預設的服務。

<center>
![慣用的主要網域和容錯移轉][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>要求複本散佈，且不允許封裝
複本是_通常_分散容錯和升級網域，當 hello 叢集狀況良好。 不過，指定資料分割的多個複本有時會暫時封裝到單一網域。 例如，假設該 hello 叢集有九個節點中三個容錯網域，fd: / 0，fd: / 1 和 fd: / 2。 假設您的服務有三個複本。 讓我們假設該 hello 節點已使用那些中的複本 fd: / 1 和 fd: / 2 停擺。 通常 hello 叢集資源管理員想使用這些相同的容錯網域中的其他節點。 在此情況下，我們假設因為 toocapacity 問題無 hello 的這些網域中的其他節點都有效。 如果 hello 叢集資源管理員建置取代這些複本，它就會有 toochoose 節點在 fd: / 0。 不過，執行_，_建立代表違反 hello 容錯網域條件約束的情況。 壓縮複本會增加 hello 整個複本集的 hello 機率無法向下或遺失。 

> [!NOTE]
> 如需一般情況下條件約束和條件約束優先順序的詳細資訊，請參閱[本主題](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities)。
>

如果您曾看過類似「`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`」的健康狀態訊息，表示您已遇到此狀況或類似的情況。 通常只有一或兩個複本會暫時封裝在一起。 只要少於指定網域中複本的法定數目，就是安全的。 封裝很少見，但還是有可能發生，並且這些情況通常是暫時性因為 hello 節點回來。 如果 hello 節點執行保持關閉且 hello 叢集資源管理員需要 toobuild 取代項目時，通常有可用的其他節點 hello 理想的容錯網域中。

某些工作負載偏好一律擁有 hello 目標數目複本，即使它們會封裝為更少的定義域。 這些工作負載打賭會同時全面發生永久性網域故障，通常可以復原本機狀態。 其他工作負載而需要花 hello 停機時間早於風險正確性或資料遺失。 大部分生產工作負載執行時會使用三個以上的複本、三個以上的容錯網域，以及每個容錯網域的許多有效節點。 因為這個緣故，hello 預設行為的預設值，讓網域封裝。 hello 預設行為可讓一般平衡和容錯移轉 toohandle 這些極端的情況下，即使這表示暫存網域封裝。

如果您想 toodisable 這類特定工作負載的封裝，您可以指定 hello `RequireDomainDistribution` hello 服務上的原則。 當此原則設定時，hello 叢集資源管理員可確保從 hello hello 相同錯誤，或升級網域中執行相同的資料分割沒有兩個複本。

程式碼：

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

現在，它會是可能 toouse 服務合併不地理位置的叢集中的這些設定嗎？ 可以，但也沒有充分的理由。 hello 必要、 不正確，及慣用網域組態應該避免除非 hello 案例需要這些項目。 它不讓任何有意義 tootry tooforce 給定工作負載 toorun 在單一機架或 tooprefer 某個線段的透過另一個本機叢集。 不同的硬體設定應該分散至容錯網域，並透過一般放置條件約束和節點屬性來處理。

## <a name="next-steps"></a>後續步驟
- 如需服務設定的詳細資訊，請[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
