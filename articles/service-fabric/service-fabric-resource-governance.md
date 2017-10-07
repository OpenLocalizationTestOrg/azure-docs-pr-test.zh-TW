---
title: "aaaAzure 服務網狀架構資源管理針對容器和服務 |Microsoft 文件"
description: "Azure 服務網狀架構可讓您執行內部或外部的容器服務 toospecify 資源限制。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a>資源管理 

當上執行多個服務 hello 相同節點或叢集時，很可能在一個服務可能會耗用更多資源匱乏資源的其他服務。 這個問題是參照的 tooas hello 雜訊芳鄰的問題。 Service Fabric 可讓 hello 開發人員 toospecify 保留項目和每個服務 tooguarantee 資源限制，以及也會限制其資源使用量。 

## <a name="resource-governance-metrics"></a>資源管理計量 

Service Fabric 可依每一[服務套件](service-fabric-application-model.md)支援資源管理。 指派 tooService 套件 hello 資源可以進一步劃分的程式碼封裝。 指定的 hello 資源限制也表示 hello 資源 hello 保留項的目。 Service Fabric 支援使用兩個內建的[計量](service-fabric-cluster-resource-manager-metrics.md)來指定每一服務套件的 CPU 和記憶體：

* CPU (衡量標準名稱`ServiceFabric:/_CpuCores`): 一個核心 hello 主機電腦，可以使用的邏輯核心跨越所有節點的所有核心會都評估而且 hello 相同。
* 記憶體 (衡量標準名稱`ServiceFabric:/_MemoryInMB`): 表示記憶體以 mb 為單位，而且它會對應 toophysical hello 電腦可以使用的記憶體。

僅彈性保留保證就會提供-hello 執行階段會拒絕開啟新的服務封裝可用的資源超過。 不過，如果另一個可執行檔或容器放置在 hello 節點時，可能違反 hello 原始保留保證。

這些兩個度量，hello[叢集資源管理員](service-fabric-cluster-resource-manager-cluster-description.md)追蹤總叢集容量，hello hello 叢集中的每個節點上的負載，和剩餘的 hello 叢集中的資源。 這些兩個度量資訊會相當 tooany，其他使用者或自訂的度量和所有現有的功能可以搭配它們：
* 可以是叢集[平衡](service-fabric-cluster-resource-manager-balancing.md)根據 toothese 兩個度量 （預設行為）。
* 可以是叢集[重組](service-fabric-cluster-resource-manager-defragmentation-metrics.md)根據 toothese 兩個度量。
* 在[描述叢集](service-fabric-cluster-resource-manager-cluster-description.md)時，可以為這兩個計量設定緩衝處理的容量。

這些計量不支援[動態負載報告](service-fabric-cluster-resource-manager-metrics.md)，而這些計量的負載則是在建立時定義。

## <a name="cluster-set-up-for-enabling-resource-governance"></a>設定叢集以啟用資源管理

容量應定義為以手動方式在 hello 叢集中的每個節點類型，如下所示：

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
只有在使用者服務上才允許進行資源管理，在任何系統服務上則都不允許。 指定容量時，必須保留部分核心和記憶體不進行配置，以供系統服務使用。 為了達到最佳效能，下列設定的 hello 應該也開啟 hello 叢集資訊清單中： 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>指定資源管理 

資源控管限制 hello 應用程式資訊清單 （ServiceManifestImport 區段） 中指定 hello 下列範例所示：

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
在此範例中，服務封裝 ServicePackageA 取得 hello 節點放置的位置上的其中一個核心。 此服務封裝包含兩個程式碼封裝 （CodeA1 和 CodeA2），並同時指定 hello`CpuShares`參數。 CpuShares 512:256 hello 比例將在兩個程式碼封裝 hello 之間分割 hello 核心。 因此，在此範例中，CodeA1 取得三分之二的核心，CodeA2 取得三分之一的核心 （並的軟體保證保留 hello 相同）。 如果當 CpuShares 不會指定程式碼封裝，Service Fabric 會將它們之間平均 hello 核心。

記憶體限制是絕對的因此這兩個程式碼封裝的有限的 too1024 MB 的記憶體 （和 hello 相同的軟體保證保留）。 程式碼封裝 （容器或處理程序） 不能 tooallocate 記憶體超過此限制，而嘗試 toodo 因此會導致記憶體不足例外狀況。 資源限制強制 toowork，所有的程式碼封裝在服務封裝內必須有指定記憶體限制。


## <a name="next-steps"></a>後續步驟
* toolearn 更多有關叢集資源管理員，請閱讀本[文章](service-fabric-cluster-resource-manager-introduction.md)。
* 深入了解應用程式模型中，服務套件、 程式碼封裝和複本如何對應 toothem toolearn 讀取這[文章](service-fabric-application-model.md)。
