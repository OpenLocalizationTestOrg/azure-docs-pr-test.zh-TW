---
title: "aaaService 網狀架構叢集資源管理員的應用程式群組 |Microsoft 文件"
description: "Hello hello Service Fabric 叢集資源管理員中的應用程式群組功能的概觀"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>簡介 tooApplication 群組
透過將 hello 負載分散到 Service Fabric 叢集資源管理員通常管理的叢集資源 (透過下列方式表示[度量](service-fabric-cluster-resource-manager-metrics.md)) 平均分散整個 hello 叢集。 Service Fabric 管理透過整個 hello 叢集和叢集 hello hello 節點 hello 容量[容量](service-fabric-cluster-resource-manager-cluster-description.md)。 計量和容量很適用於許多工作負載，但過度使用不同 Service Fabric 應用程式執行個體的模式，有時會引起其他需求。 例如，您可能想要：

- 保留某些具名的應用程式執行個體中的 hello 服務 hello hello 叢集中節點上某些容量
- 限制具名的應用程式執行個體中的 hello 服務執行 （而不是散佈它們 hello 整個叢集） 的節點 hello 的總數
- 定義本身 hello 具名的應用程式執行個體上的內文中的 hello 服務的服務或總共資源耗用量 toolimit hello 數目的容量

toomeet 這些需求，hello Service Fabric 叢集資源管理員支援稱為應用程式群組的功能。

## <a name="limiting-hello-maximum-number-of-nodes"></a>限制 hello 的節點數上限
應用程式容量 hello 簡單使用案例是當應用程式執行個體需要 toobe 有限 tooa 特定節點的數目上限。 這會將該應用程式執行個體中的所有服務合併到固定數目的機器上。 彙總時，您在繼續努力 toopredict 或限制該具名的應用程式執行個體中的 hello 服務在實體資源使用。 

hello 下列影像顯示應用程式執行個體逾時或無定義的節點數目上限：

<center>
![定義節點數目上限的應用程式執行個體][Image1]
</center>

在 hello 左範例中，hello 應用程式沒有定義的節點數目上限，它有三種服務。 hello 叢集資源管理員具有所有複本都擴展到六個可用的節點 tooachieve hello 最佳平衡 hello 叢集中 （hello 預設行為）。 在 hello 右範例中，我們看到 hello 相同的應用程式限制 toothree 節點。

hello 參數，可控制這個行為稱為 MaximumNodes。 您可以在應用程式建立期間設定這個參數，也可以針對執行中的應用程式執行個體更新這個參數。

Powershell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

Hello 集中的節點，hello 叢集資源管理員並不保證哪一個服務物件取得放置在一起，或使用哪些節點取得。

## <a name="application-metrics-load-and-capacity"></a>應用程式度量、負載和容量
應用程式群組也可讓您指定具名的應用程式執行個體和該應用程式執行個體的容量的這些度量資訊與相關聯的 toodefine 標準。 應用程式計量可讓您 tootrack、 保留，並限制 hello 服務該應用程式執行個體中的 hello 資源耗用量。

每一個應用程式計量可以設定兩個值︰

- **應用程式容量總計**– 這項設定代表 hello 的特定度量的 hello 應用程式的總容量。 hello 叢集資源管理員不允許任何新的服務會導致此值總負載 tooexceed 這個應用程式執行個體中的 hello 的建立。 例如，假設 hello 應用程式執行個體具有 10 個的容量，並已經有五個的負載。 會允許服務與 10 的總預設負載 hello 建立。
- **最大節點容量**– 此設定可指定 hello 的最大總載入 hello 應用程式的單一節點上。 如果負載是經過這個容量，hello 叢集資源管理員會移動複本 tooother 節點，使 hello 負載降低。


PowerShell：

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C#：

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>保留容量
應用程式群組的另一個常見用途是 tooensure 內資源 hello 叢集保留給指定的應用程式執行個體。 建立 hello 應用程式執行個體時，一定會保留 hello 空格。

保留 hello 叢集中的空間，如 hello 應用程式事件會立即發生，即使：
- hello 應用程式執行個體建立，但沒有任何服務中
- 每次變更服務 hello 應用程式執行個體中的 hello 數目 
- hello 服務存在但不耗用 hello 資源 

保留應用程式執行個體的資源，需要指定兩個額外參數：*MinimumNodes* 和 *NodeReservationCapacity*

- **MinimumNodes** -定義 hello 最小數目的 hello 應用程式的節點執行個體應該在上執行。  
- **NodeReservationCapacity** -此設定是每個計量 hello 應用程式。 hello 值為 hello 數量保留給 hello 應用程式，其中的 hello 服務執行該應用程式中的任何節點上的度量。

結合**MinimumNodes**和**NodeReservationCapacity**保證 hello hello 叢集內的應用程式的最小的負載保留項目。 如果有較少的剩餘容量 hello 叢集比 hello 所需的總保留時，建立 hello 應用程式失敗。 

讓我們看看容量保留的範例︰

<center>
![定義保留容量的應用程式執行個體][Image2]
</center>

在 hello 左範例中，應用程式沒有定義任何應用程式容量。 hello 叢集資源管理員之間取得平衡，根據 toonormal 規則的所有項目。

在右 hello 上 hello 範例中，假設 Application1 已建立以 hello 下列設定：

- MinimumNodes 設定 tootwo
- 應用程式計量定義下列值
  - NodeReservationCapacity 為 20

Powershell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Service Fabric Application1，保留兩個節點上的容量，並不允許從 Application2 tooconsume 服務該容量即使沒有任何負載所耗用的 hello 服務內 Application1 hello 次。 這個保留的應用程式的功能會被視為耗用，而且不利於 hello 剩餘容量該節點上並 hello 叢集內。  hello 保留扣除 hello 立即剩餘叢集容量，只有在至少一個服務物件置於其上時，不過 hello 保留要耗用量扣除從特定節點的 hello 容量。 這後來的保留做法能夠更有彈性和更充分利用資源，因為只有在需要時才於節點上保留資源。

## <a name="obtaining-hello-application-load-information"></a>取得 hello 應用程式載入資訊
每個應用程式具有一個或多個度量定義應用程式容量，您可以取得 hello hello 彙總載入複本的服務所報告的資訊。

PowerShell：

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

hello ApplicationLoad 查詢會傳回有關 hello 應用程式所指定的應用程式容量的 hello 基本資訊。 此資訊包括 hello 節點最小值和最大節點資訊，以及目前佔用 hello 應用程式的 hello 數目。 也包含每個應用程式負載計量的相關資訊，包括︰

* 度量的名稱： Hello 度量的名稱。
* 此應用程式保留 hello 叢集中的保留容量： 叢集容量。
* 應用程式負載︰此應用程式的子複本的總負載。
* 應用程式容量︰許可的應用程式負載值上限。

## <a name="removing-application-capacity"></a>移除應用程式容量
一旦應用程式設定 hello 應用程式容量參數之後，他們可以使用更新應用程式的 Api 或 PowerShell 指令程式來移除。 例如：

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

此命令會移除 hello 應用程式執行個體中的所有應用程式容量管理參數。 這包括 MinimumNodes、 MaximumNodes 和 hello 應用程式的度量，如果有的話。 hello 影響 hello 命令是即時的。 此命令完成之後，hello 叢集資源管理員會管理應用程式使用 hello 預設行為。 您可以透過 `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()` 再次指定「應用程式容量」參數。

### <a name="restrictions-on-application-capacity"></a>應用程式容量的限制
應用程式容量參數有數個限制必須遵守。 如果發生驗證錯誤，則不會進行任何變更。

- 所有整數參數必須為非負數。
- MinimumNodes 不能大於 MaximumNodes。
- 如果已定義負載度量的容量，則它們必須遵守下列規則︰
  - 節點保留容量不能大於節點容量上限。 例如，您無法限制 hello 度量"CPU"hello 節點 tootwo 單元上的 hello 容量，然後再次嘗試 tooreserve 三個單位，每個節點上。
  - 如果指定 MaximumNodes，然後 MaximumNodes 和最大節點容量 hello 產品不能大於應用程式容量總計。 例如，假設 hello，"CPU"設定 tooeight 負載度量的最大節點容量。 我們也假設您設定最大節點 too10 hello。 在此情況下，此負載計量的「應用程式容量總計」必須大於 80。

同時在應用程式建立及更新期間，都會強制執行 hello 限制。

## <a name="how-not-toouse-application-capacity"></a>如何 toouse 應用程式容量
- 請勿嘗試 toouse hello 應用程式群組功能 tooconstrain hello 應用程式 tooa_特定_節點的子集。 換句話說，您可以指定 hello 應用程式執行最多五個節點上，但不是哪些特定五個叢集中的節點 hello。 限制應用程式 toospecific 節點可以達成服務的使用位置條件約束。
- 請勿嘗試 toouse hello 應用程式容量 tooensure hello 置於相同的應用程式從兩個服務 hello 相同節點。 請改用[親和性](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)或[放置條件約束](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)。

## <a name="next-steps"></a>後續步驟
- 如需服務設定的詳細資訊，請[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)
- toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)
- Hello 從頭開始並[取得簡介 toohello Service Fabric 叢集資源管理員](service-fabric-cluster-resource-manager-introduction.md)
- 如需度量通常如何運作的詳細資訊，請繼續閱讀 [Service Fabric 負載度量](service-fabric-cluster-resource-manager-metrics.md)
- hello 叢集資源管理員有許多選擇可用來描述 hello 叢集。 toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
