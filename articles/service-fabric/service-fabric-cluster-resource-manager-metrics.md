---
title: "使用度量 aaaManage Azure 的微服務負載 |Microsoft 文件"
description: "深入了解如何 Service Fabric toomanage tooconfigure 和使用計量服務資源耗用量。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>在 Service Fabric 中使用度量管理資源耗用量和負載
*度量*hello hello 叢集中的節點提供您服務在意和其中的 hello 資源。 度量是您想要在您的服務順序 tooimprove 或監視器 hello 效能 toomanage 的任何項目。 例如，您可能會監看記憶體耗用量 tooknow 如果您的服務多載。 另一個用途是 toofigure 出是否 hello 服務無法移動其中的記憶體是小於順序 tooget 較佳的效能受到限制的其他位置。

像記憶體、磁碟 及 CPU 使用率等項目都是計量的範例。 這些度量資訊是實體的度量，對應 toophysical hello 需要 toobe 受管理的節點上的資源的資源。 計量也可以是 (且通常是) 邏輯計量。 邏輯計量的範例是 “MyWorkQueueDepth”、"MessagesToProcess" 或 "TotalRecords" 之類的項目。 邏輯度量是應用程式定義並間接對應 toosome 實體資源耗用量。 邏輯度量資訊是常見的因為很難 toomeasure 和報表的每個服務為基礎的實體資源的耗用量。 hello 複雜度測量與報告自己實體度量也是為什麼 Service Fabric 提供某些預設度量資訊。

## <a name="default-metrics"></a>預設度量
假設您想 tooget 啟動撰寫和部署您的服務。 此時，您不知道它會取用哪些實體或邏輯資源。 沒關係！ hello Service Fabric 叢集資源管理員時指定其他度量資訊，請使用某些預設度量資訊。 如下：

  - PrimaryCount-hello 節點上的主要複本的計數 
  - ReplicaCount-hello 節點上可設定狀態的複本總數的計數
  - 計數-所有服務上的物件 （無狀態與可設定狀態） hello 節點計數

| 計量 | 無狀態執行個體負載 | 具狀態次要負載 | 具狀態主要負載 |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Count |1 |1 |1 |

針對基本的工作負載，hello 預設度量會提供工作 hello 叢集中的不錯分佈。 在下列範例的 hello，我們來看看當我們建立兩個服務，並依賴 hello 預設度量平衡時，會發生什麼事。 hello 第一個服務具有三個資料分割的可設定狀態服務，目標複本集大小的三個。 hello 第二個服務是無狀態服務具有一個資料分割和三個執行個體計數。

以下是您將看到的情況：

<center>
![使用預設計量的叢集配置][Image1]
</center>

某些事項 toonote:
  - Hello 可設定狀態服務的主要複本會分散到數個節點
  - Hello 不同節點是相同的資料分割的複本
  - hello 叢集中發佈的主要複本會與次要複本的 hello 總數
  - 平均每個節點上配置的服務物件的 hello 總數

很好！

hello 預設計量很大，是個起點。 不過，hello 預設計量將只執行您到目前為止。 例如： 中完全甚至使用率何謂 hello 可能性 hello 資料分割配置您挑選的結果的所有磁碟分割？ 何謂 hello 負載指定服務的 hello 機率經過一段時間，是常數，或甚至只 hello 相同跨多個分割區現在嗎？

您可以執行包含只 hello 預設度量。 不過，這樣通常表示叢集使用率較低，比您想要的更不平均。 這是因為 hello 預設計量不是自動調整，以及假設所有項目相當。 例如，忙線中的主要複本，另一個則不是這兩個參與"1"toohello PrimaryCount 度量。 Hello 最壞的情況下，使用 hello 預設度量也造成效能問題所導致的 overscheduled 節點。 如果您想要以取得 hello 大部分超出您的叢集，並避免效能問題，您需要 toouse 自訂計量與動態載入報表。

## <a name="custom-metrics"></a>自訂度量
度量資訊會在您要建立 hello 服務時，設定個別具名-服務-執行個體為基礎。

任何計量都有一些描述它的屬性：名稱、權數及預設負載。

* 度量名稱： hello hello 度量名稱。 hello 衡量標準名稱是從 hello 資源管理員的觀點來看 hello 叢集內的 hello 度量的唯一識別碼。
* 加權： 重要性此計量會相對 toohello 衡量標準權數定義此服務的其他度量資訊。
* 預設值載入： hello 預設負載的表示方式會根據 hello 服務是無狀態或可設定狀態。
  * 就無狀態服務而言，每個計量都有名為 DefaultLoad 的單一屬性
  * 針對具狀態服務，您需定義：
    * 此服務使用時，它主要這個標準的 primaryDefaultLoad: hello 預設量
    * 此服務使用次要複本時此標準的 secondaryDefaultLoad: hello 預設數量

> [!NOTE]
> 如果您定義自訂的度量，而您想 too_also_ 使用 hello 預設度量，您需要 too_explicitly_ 新增 hello 預設計量備份，並為其定義加權和值。 這是因為您必須定義 hello hello 預設計量和自訂的度量之間的關聯性。 例如，也許您會在意 ConnectionCount 或 WorkQueueDepth 更甚於主要分配。 依預設 hello 權數的 hello PrimaryCount 度量是高，所以您想 tooreduce 它 tooMedium 時新增這些對應優先您其他度量 tooensure。
>

### <a name="defining-metrics-for-your-service---an-example"></a>為您的服務定義計量 - 範例
例如，假設您想 hello 下列組態：

  - 您的服務報告名為 "ConnectionCount” 的計量
  - 您也想 toouse hello 預設計量 
  - 您已經完成一些測量，而知道該服務的主要複本通常佔用 20 單位的 "ConnectionCount"。
  - 而次要複本則佔用 5 單位的 "ConnectionCount"
  - 您知道"ConnectionCount 」 是 hello 以管理此特定服務的 hello 效能最重要的度量
  - 但您仍然希望主要複本達到平衡。 無論如何，平衡主要複本通常是個不錯的主意。 這有助於防止 hello 遺失某些節點或容錯網域的影響以及它的主要複本的多數。 
  - 否則，hello 預設計量是正常

Hello 程式碼，您會撰寫 toocreate 服務與該度量的組態如下：

程式碼：

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> hello 上述範例與 hello 本文的其餘部分將描述管理度量上名為-針對服務。 它也是您在 hello 服務的服務可能 toodefine 度量_類型_層級。 這會透過在您的服務資訊清單中指定它們來完成。 不建議定義類型層級度量有幾個原因。 hello 第一個原因是，度量名稱要經常特定的環境。 除非就地確實的合約，就無法確定在一個環境中的 hello 度量"核心"不在其他"MiliCores 」 或 「 核心"。 如果您的度量定義資訊清單中您會需要 toocreate 每個環境的新資訊清單。 這讓 tooa 激增不同的資訊清單有只有些許差異，這可能會導致 toomanagement 困難。  
>
> 計量負載通常會為每個具名服務執行個體指派。 例如，假設您建立一個執行個體的 hello 服務人員計劃 toouse CustomerA 它根本很少。 同時假設您為 CustomerB 建立另一個執行個體，該客戶有更大的工作負載。 在此情況下，您可能會想 tootweak hello 預設載入這些服務。 如果您有度量，並定義資訊清單，然後透過載入想 toosupport 這種情況下，它可以針對每個客戶需要不同的應用程式和服務類型。 在服務建立時定義的 hello 值會覆寫在 hello 資訊清單中定義，因此您可以使用該 tooset hello 特定預設值。 不過，這樣會導致 hello hello 資訊清單 toonot 這些 hello 服務實際上會以執行的相符項目中所宣告的值。 這可能會導致 tooconfusion。 
>

提醒： 如果您只想 toouse hello 預設度量，不需要 tootouch hello 度量收集或建立您的服務時執行任何特殊的動作。 當沒有其他已定義時，取得會自動使用 hello 預設計量。 

現在，我們再逐行更詳細的這些設定，並討論有關它所影響的 hello 行為延伸模組。

## <a name="load"></a>載入
hello 定義度量的重點是 toorepresent 一些負荷。 「負載」係指特定節點上的某個服務執行個體或複本取用的特定計量數量。 隨時可以設定負載。 例如：

  - 建立服務時，可以定義負載。 這稱為_預設負載_。
  - 建立 hello 服務之後，可以更新服務載入 hello 度量資訊，包括預設值。 這稱為_更新服務_。 
  - hello 載入給定資料分割可以重設 toohello 預設值，該服務。 這稱為_重設資料分割負載_。
  - 負載可以每個服務物件為基礎，在執行階段以動態方式報告。 這稱為_報告負載_。 
  
所有這些策略可用於其存留期相同服務的 hello。 

## <a name="default-load"></a>預設負載
*預設負載*多少 hello 度量取用此服務每個服務物件 （無狀態的執行個體或可設定狀態的複本）。 hello 叢集資源管理員會使用這個數字 hello 服務物件的 hello 負載，直到其接收到的其他資訊，例如動態載入報表。 針對簡單服務，hello 預設負載會是靜態的定義。 hello 預設載入不會再更新，並用於 hello hello 服務存留期間。 預設值載入簡單的容量規劃特定資源數量是專用的 toodifferent 工作負載，而不會變更的效果很好。

> [!NOTE]
> 如需有關容量管理和叢集中定義 hello 節點容量的詳細資訊，請參閱[本文](service-fabric-cluster-resource-manager-cluster-description.md#capacity)。
> 

hello 叢集資源管理員可讓您可設定狀態服務 toospecify 不同的預設載入其主要複本會與次要資料庫。 無狀態服務只能指定一個適用於 tooall 執行個體的值。 可設定狀態服務，主要和次要複本的 hello 預設負載是工作的通常不同，因為複本執行不同類型的每個角色中。 例如，主要複本會通常讀取和寫入，而處理大部分的 hello 計算負擔，但不需要次要資料庫。 通常是主要複本的 hello 預設負載高於 hello 預設負載的次要複本。 hello 實際數字應該取決於您自己的量值。

## <a name="dynamic-load"></a>動態負載
假設您已經執行服務達一段時間。 藉由一些監視，您已注意到：

1. 所指定服務的某些資料分割或執行個體比其他資料分割或執行個體耗用更多資源
2. 某些服務的負載會隨著時間改變。

有很多原因可能造成這些類型的負載變動。 例如，不同的服務或資料分割會與具有不同需求的不同客戶相關聯。 由於工作 hello 服務的 hello 數量並隨著 hello 課程 hello 每日，也可以變更負載。 不論 hello 原因，所以通常沒有您可以使用預設的單一數字。 特別是如果您想 tooget hello 移出 hello 叢集的大部分使用率。 您挑選為預設負載錯誤 hello 時間部分的任何值。 不正確的預設載入 hello 叢集資源管理員透過或下配置資源中的結果。 如此一來，您有高於或低於利用即使 hello 叢集資源管理員認為平衡 hello 叢集的節點。 由於預設負載提供初始放置的某些資訊，因此它們仍有其實用性，但是它們並無法反映實際工作負載的完整面貌。 tooaccurately 擷取變更的資源需求，hello 叢集資源管理員可在執行階段期間每個服務物件 tooupdate 它自己的負載。 這稱為動態負載報告功能。

動態負載報告允許複本或執行個體 tooadjust 其配置/報告負載度量的超過存留期。 閒置且未執行任何工作的服務複本或執行個體通常會回報使用少量的指定計量。 忙碌的複本或執行個體則會回報使用較多的資源。

報告每個複本或執行個體的負載可讓叢集資源管理員 tooreorganize hello hello 個別的服務物件 hello 叢集中。 重新組織 hello 服務，可協助確保他們取得所需要的 hello 資源。 服務忙碌中有效地取得太"回收 」 從其他的複本或正在冷或執行較少工作的執行個體的資源。

在可靠的服務，hello 程式碼 tooreport 載入以動態方式看起來像這樣：

程式碼：

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

服務可以報告在任何在建立時定義為它的 hello 計量。 如果服務報表，而不是為度量設定負載 toouse，Service Fabric 會忽略該報表。 如果有其他度量報告在 hello 相同有效，這些報告所接受的時間。 服務程式碼可以測量並報告所有 hello 的度量它知道如何使用，而且運算子可以指定 hello 度量組態 toouse 而不需要 toochange hello 服務程式碼。 

### <a name="updating-a-services-metric-configuration"></a>更新服務的計量設定
與 hello 服務相關聯的度量的 hello 清單和即時 hello 服務時的這些度量的 hello 屬性也可以動態更新。 這樣可以進行實驗並具有彈性。 非常有用的某些範例為：

  - 針對特定服務停用具有錯誤報告的計量
  - 重新設定 hello 加權度量根據想要的行為
  - hello 程式碼已經部署並透過其他機制進行驗證時，才可以啟用新的度量
  - 變更服務，根據觀察到的行為和耗用量的 hello 預設負載

hello 主應用程式開發介面變更度量的組態是`FabricClient.ServiceManagementClient.UpdateServiceAsync`在 C# 和`Update-ServiceFabricService`在 PowerShell 中。 您指定使用這些 Api 的任何資訊會立即取代 hello 現有度量 hello 服務資訊。 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>混用預設負載值和動態負載報告
預設負載及動態負載可以用於 hello 相同的服務。 當服務利用預設負載和動態負載報告時，預設負載會作為預估值，直到動態報告出現為止。 預設負載適合，因為它讓 hello 叢集資源管理員項目與 toowork。 hello 預設負載在建立時，允許 hello 叢集資源管理員 tooplace hello 良好的位置中的服務物件。 如果未提供任何預設負載資訊，就會以隨機方式有效率地放置服務。 載入報表稍後到達時 hello 初始的隨機位置通常是錯誤且 hello 叢集資源管理員 toomove 服務。

讓我們採用先前的範例，看看當我們加入一些自訂負載和動態負載報告功能時會發生什麼狀況。 在此範例中，我們使用 “MemoryInMb” 作為範例計量。

> [!NOTE]
> 記憶體是其中一個 hello 系統度量，Service Fabric 可以[資源控管](service-fabric-resource-governance.md)，並報告它是通常很困難。 我們不實際期待您 tooreport 記憶體耗用量。使用的記憶體為 hello hello 叢集資源管理員功能的相關協助 toolearning。
>

讓我們假設為我們一開始建立 hello 具狀態服務以 hello 下列命令：

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

提醒您，此語法是 ("MetricName, MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad")。

讓我們看看可能的叢集配置看起來如何︰

<center>
![使用預設和自訂計量平衡的叢集][Image2]
</center>

有幾件事值得一提：

* 資料分割內的次要複本可以有自己的負載
* 整體 hello 度量尋找平衡。 記憶體 hello hello 最大值之間的比率，且最小的負載 1.75 (hello 節點以 hello 大部分負載 N3，hello 至少是 N2 和 28/16 = 1.75)。

我們仍需要 tooexplain 事項錯誤：

* 何者決定 1.75 的比率是否合理？ 如何 hello 叢集資源管理員知道，是否夠好，或者如果沒有更多工作 toodo？
* 何時發生平衡？
* 記憶體的權數「很高」是什麼意思？

## <a name="metric-weights"></a>度量權數
追蹤 hello 相同度量資訊，在不同的服務是很重要。 全域檢視是允許 hello hello 叢集中的叢集資源管理員 tootrack 耗用量，節點平均分配耗用量，並確認節點不超過容量。 不過，服務可能會有不同的檢視為 toohello 重要性的 hello 相同的度量。 此外，在具有許多計量和許多服務的叢集中，可能並非所有計量都有完美平衡的解決方案。 Hello 叢集資源管理員如何處理這些情況？

衡量標準權數允許 hello 叢集資源管理員 toodecide toobalance hello 叢集化不完整的回應時。 衡量標準權數也可讓叢集資源管理員 toobalance hello 特定服務以不同的方式。 度量可以有四個不同的權數層級︰零、低、中和高。 在考量項目是否平衡時，權數為「零」的計量並沒有任何貢獻。 不過，其負載仍參與 toocapacity 管理。 具有「零」權數的計量仍然相當有用，並且經常作為服務行為和效能監視的一部分。 [這篇文章](service-fabric-diagnostics-event-generation-infra.md)提供的監視度量的 hello 使用與您的服務診斷的詳細資訊。 

hello 的不同度量的加權 hello 叢集中的實際影響是該 hello 叢集資源管理員會產生不同的解決方案。 衡量標準權數告訴 hello 叢集資源管理員，某些度量資訊會比其他更重要。 當沒有任何完美的解決方案 hello 時，叢集資源管理員可以偏好平衡 hello 高加權的度量更好的解決方案。 如果服務認為特定計量不重要，它可能會發現對該計量的使用不平衡。 這可讓另一個服務 tooget 某些度量資訊會是重要的 tooit 平均分配。

讓我們看看一些負載報告和不同的度量的範例加權 hello 叢集中不同的配置中的結果。 在此範例中，我們看到，切換 hello hello 度量相對權數會使叢集資源管理員 toocreate hello 的服務不同的排列方式。

<center>
![計量權數範例及其對平衡解決方案的影響][Image3]
</center>

在此範例中，有四個不同的服務，它們都針對兩個不同計量 (MetricA 和 MetricB) 報告不同值。 在其中一個案例中，所有的 hello 服務定義 MetricA 為 hello 最重要的 (加權 = 高) 和 MetricB 做並不重要 (加權 = 低)。 如此一來，我們會看到該 hello 叢集資源管理員會將 hello 服務以便 MetricA 就是進一步比 MetricB 平衡。 「更加平衡」表示 MetricA 具有比 MetricB 較低的標準差。 在 hello 第二個案例中，我們會反轉 hello 衡量標準權數。 如此一來，hello 叢集資源管理員交換服務 A 和 B toocome 向上其中 MetricB 是更好比 MetricA 平衡配置。

> [!NOTE]
> 衡量標準權數判斷如何應平衡 hello 叢集資源管理員，但不是時平衡應該發生。 如需有關平衡的詳細資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-balancing.md)
>

### <a name="global-metric-weights"></a>全域度量權數
讓我們假設 Services 定義 MetricA 加權高，因為並 ServiceB 設定 hello 加權 MetricA tooLow 則為零。 Hello 最後會取得使用的實際權數是什麼？

針對每個計量都會追蹤多個權數。 hello 第一個寬度為 hello 建立 hello 服務時，為 hello 度量定義一個。 hello 其他加權值是全域的加權，自動計算。 hello 叢集資源管理員評分解決方案時，會使用這些的加權。 將這兩個權數列入考量很重要。 這可讓叢集資源管理員 toobalance hello 相應 tooits 擁有優先權，並為整個正確已配置，此外也請確認該 hello 叢集中每個服務。

如果 hello 叢集資源管理員不在意全域和本機的平衡，會發生什麼事？ 這就是輕鬆 tooconstruct 解決方案的全域平衡，但這會導致不佳的資源平衡個別服務。 在下列範例的 hello，讓我們看一下剛才 hello 預設計量，以設定服務，並查看 當被視為只有全域平衡時，會發生什麼情況：

<center>
![hello 只有全域方案的影響][Image4]
</center>

在 hello 上方範例中只會根據通用的平衡，確實平衡 hello 為整個叢集。 所有節點都有相同的主要複本會計算並 hello 相同的 hello 數字的複本總數。 不過，如果您看一下這個配置的 hello 實際影響它不是很理想： hello 遺失的任何節點將會影響特定工作負載不適當，因為它會接受所有其主要複本會。 比方說，如果 hello 第一個節點失敗 hello hello 三個不同資料分割的 hello 圓形服務的三個主要複本會將所有會遺失。 相反地，hello 三角形及六邊形服務有遺失的複本及其資料分割。 這會導致以外具有 toorecover hello 向複本的任何干擾。

在 hello 下方範例中，hello 叢集資源管理員卻散發 hello 複本根據這兩個 hello 全域和每個服務的平衡。 計算 hello 分數的 hello 方案時它會提供大部分的 hello 加權 toohello 全域方案，以及 （設定） 的部分 tooindividual 服務。 全域平衡標準是根據每個服務的 hello 衡量標準權數的 hello 平均計算。 每個服務平衡相應 tooits 自己定義衡量標準權數。 這可確保 hello 服務的平衡本身根據 tootheir 自己的需求。 如此一來，如果 hello 相同的第一個節點失敗 hello 失敗，都會分散到所有服務的所有資料分割中。 hello 影響 tooeach 是 hello 相同。

## <a name="next-steps"></a>後續步驟
- 如需有關設定服務的詳細資訊，請參閱[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- 定義磁碟重組度量資訊是其中一種方式 tooconsolidate 負載，而不是分配的節點上。toolearn 如何 tooconfigure 磁碟重組，請參閱太[這篇文章](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)
- Hello 從頭開始並[取得簡介 toohello Service Fabric 叢集資源管理員](service-fabric-cluster-resource-manager-introduction.md)
- 移動成本是訊號某些服務會比其他更耗費資源 toomove toohello 叢集資源管理員的一種方式。 深入了解移動成本 toolearn 參照太[這篇文章](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
