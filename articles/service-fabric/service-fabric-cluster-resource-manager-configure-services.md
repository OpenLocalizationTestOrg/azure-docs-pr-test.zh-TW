---
title: "在 Azure microservices aaaSpecify 度量和放置設定 |Microsoft 文件"
description: "藉由指定計量、放置條件約束及其他放置原則來描述 Service Fabric 服務。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>設定 Service Fabric 服務的叢集資源管理員設定
hello Service Fabric 叢集資源管理員可讓您管理每個個別命名服務的 hello 規則更細微的控制。 每個指定的服務可以指定規則應該會將它配置 hello 叢集中的方式。 每個指定的服務也可以定義 hello 組，它想 tooreport，包括它們所 toothat 服務重要的度量。 設定服務可細分成三個不同的工作︰

1. 設定放置條件約束
2. 設定計量
3. 設定進階放置原則及其他規則 (較不常見)

## <a name="placement-constraints"></a>放置條件約束
位置條件約束是使用的 toocontrol hello 叢集中的節點可實際執行服務。 通常在特定命名服務執行個體或指定的型別限制 toorun 特定類型的節點上的所有服務。 放置條件約束是可擴充的。 您可以依據節點類型定義任何屬性集，然後在建立服務時為它們選取條件約束。 您也可以變更執行中的服務放置條件約束。 這可讓您 toorespond toochanges hello 叢集或 hello hello 服務需求。 指定節點的 hello 屬性也可以進行更新動態 hello 叢集中。 上放置條件約束和如何 tooconfigure 它們可以在找到更多資訊[這篇文章](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>度量
度量資訊是 hello 組指定的具名的服務需要的資源。 服務的計量組態包括該服務的每個具狀態複本或無狀態執行個體對該資源的預設耗用量。 度量也會包含表示重要性平衡該度量 toothat 服務以防缺點是必要的加權。

## <a name="advanced-placement-rules"></a>進階放置規則
在較少見的情況中，有其他類型的配置規則可使用。 部分範例如下：
- 對於依地理位置的分散式叢集有助益的條件約束
- 特定應用程式架構

其他放置規則是透過「相互關聯」或「原則」來設定。

## <a name="next-steps"></a>後續步驟
- 度量資訊是如何 hello Service Fabric 叢集資源管理員管理耗用量和 hello 叢集中的容量。 toolearn 更多關於度量和如何 tooconfigure 它們，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)
- 親和性是您可以針對服務設定的一種模式。 它並不常見，但如果您需要，可以參閱 [這裡](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- 有許多不同的位置規則可以設定服務 toohandle 的其他案例。 您可以在 [這裡](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Hello 從頭開始並[取得簡介 toohello Service Fabric 叢集資源管理員](service-fabric-cluster-resource-manager-introduction.md)
- toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)
- hello 叢集資源管理員有許多選擇可用來描述 hello 叢集。 toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)
