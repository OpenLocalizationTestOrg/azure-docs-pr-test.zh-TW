---
title: "Service Fabric 服務的 aaaScalability |Microsoft 文件"
description: "描述如何 tooscale Service Fabric 服務"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Service Fabric 中的縮放比例
Azure Service Fabric 可讓您輕鬆 toobuild 可擴充的應用程式透過管理 hello 服務、 資料分割，以及 hello 的叢集節點上的複本。 執行許多工作負載的 hello 相同的硬體可讓最大資源使用量，但也會提供彈性的選擇方式 tooscale 您的工作負載。 

Service Fabric 的縮放比例會以數種不同的方式來完成：

1. 透過建立或移除無狀態服務執行個體進行縮放比例
2. 透過建立或移除新的具名服務進行縮放比例
3. 透過建立或移除新的具名應用程式執行個體進行縮放比例
4. 使用分割區的服務進行縮放比例
5. 調整所新增和移除從 hello 叢集中的節點 
6. 使用叢集 Resource Manager 計量進行縮放比例

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>透過建立或移除無狀態服務執行個體進行縮放比例
其中一個內 Service Fabric hello 最簡單方式 tooscale 適用於無狀態服務。 當您建立無狀態服務時，您會取得可能發生 toodefine `InstanceCount`。 `InstanceCount`定義 hello 服務啟動時，會建立多少份執行該服務的程式碼。 比方說，比方說，hello 叢集中有 100 個節點。 另外再假設建立服務時，`InstanceCount` 為 10。 在執行階段，這些 10 個執行中複本的 hello 程式碼可能全部會變得太忙碌 （或可能不是足夠忙碌）。 其中一種方式 tooscale 該工作負載是 toochange hello 的執行個體的數目。 例如，監視或管理的程式碼某些部分可以變更的執行個體 too50 或 too5 hello 現有數目、 根據 hello 工作負載是否需要 in 或 out 根據 hello tooscale 載入。 

C#：

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

PowerShell：

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>使用動態執行個體計數
無狀態服務，專用的 Service Fabric 會提供自動的方式 toochange hello 執行個體計數。 這可讓 hello 服務 tooscale 動態地 hello 可用的節點數目。 此行為的 hello 方式 tooopt 是 tooset hello 執行個體計數 =-1。 InstanceCount =-1 會指示 tooService 網狀架構，指出 「 每個節點上執行此無狀態服務 」。 如果節點的 hello 數目變更時，Service Fabric 會自動變更 hello 執行個體計數 toomatch，確保 hello 服務正在執行有效的所有節點上。 

C#：

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell：

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>透過建立或移除新的具名服務進行縮放比例
指定的服務執行個體是特定的執行個體的服務型別 (請參閱[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)) 中某些 hello 叢集中的具名的應用程式執行個體。 

可以在服務的忙碌程度提高或降低時，建立 (或移除) 新的具名服務執行個體。 這可讓要求 toobe 分散到多個服務執行個體，通常允許現有的服務 toodecrease 負載。 建立服務，hello Service Fabric 叢集資源管理員會在分散式方式 hello 叢集中放在 hello 服務。 hello 確切決策都受到 hello[度量](service-fabric-cluster-resource-manager-metrics.md)hello 叢集和其他定位規則中。 服務可以建立數個不同的方式，但 hello 最常透過系統管理動作，如某人呼叫[ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps)，或藉由程式碼呼叫[ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet)。 `CreateServiceAsync`可以甚至從內呼叫 hello 叢集中執行的其他服務。

各種情節中皆可使用動態建立服務，且是常見的模式。 例如，假設有一個可代表特定工作流程的具狀態服務。 代表工作的呼叫將 tooshow toothis 服務，而這個服務進行 tooexecute hello 步驟 toothat 工作流程和記錄進度。 

您會如何對此特定的服務規模？hello 服務可以某種形式的多租用戶和接受的呼叫，並且在相同開始步驟的 hello 許多不同的執行個體一次工作流程。 不過，，可讓 hello 程式碼更複雜，因為它有許多不同的執行個體 hello 有關 tooworry 現在相同的工作流程，所有的不同階段，以及來自不同客戶。 此外，處理多個工作流程在同一時間不能解決的 hello hello 標尺問題。 這是因為此服務會在某個時間點耗用太多資源 toofit 特定電腦上。 未建立 hello 第一個位置在此模式的許多服務也會遇到困難到期 toosome 固有的瓶頸或速度變慢標定程式碼中。 這類問題會造成 hello 服務不 toowork 以及它會追蹤並行的工作流程的 hello 數目變大時。  

解決方案是 toocreate 執行個體要 tootrack 的這項服務來 hello 工作流程的每個不同的執行個體。 這是很好的模式，而且是否 hello 服務無狀態或可設定狀態的運作方式。 對於此模式 toowork，沒有通常是另一項服務，可做為 「 工作負載管理員服務 」。 此服務的 hello 作業是 tooreceive 要求和 tooroute 這些要求 tooother 服務。 hello 管理員可以在收到 hello 訊息時，動態建立 hello 工作負載服務的執行個體，，然後將要求 toothose 服務上。 指定的工作流程服務完成其工作時，hello 管理員服務可能也會收到回呼。 Hello 管理員收到這些回呼時它無法刪除 hello 工作流程服務，該執行個體，或將它保留，如果有多個呼叫。 

進階的版本，這種類型的管理員甚至可以建立 hello 服務它所管理集的區。 hello 集區，有助於確保在新的要求進入時它並未 hello 服務 toospin 的 toowait。 相反地，hello 管理員就可以挑選不是目前忙碌中來自 hello 集區中，工作流程服務或隨機路由。 保持服務可用的集區可處理新的要求速度，因為它比較不可能是該 hello 要求具有新的服務 toobe 調整大小的 toowait。 建立新的服務很快速，但並非免費或可瞬間完成。 hello 集區有助於降低 hello hello 要求有 toowait 之前所服務的時間量。 回應時間最重要 hello 時，您通常會看到此管理員和集區的模式。 佇列的 hello 要求並建立 hello 背景中的 hello 服務和_然後_在傳遞也是常用的管理員模式中，因為負責建立及刪除一些追蹤工作的 hello 數量的該服務目前的基礎服務。有暫止。 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>透過建立或移除新的具名應用程式執行個體進行縮放比例
建立和刪除整個應用程式執行個體是建立及刪除服務的類似 toohello 模式。 對於此模式中，為決策 hello 根據它所查看的內容的 hello 要求某些 manager 服務和 hello 資訊正在接收來自 hello hello 叢集內的其他服務。 

何時應該使用建立新的具名應用程式執行個體，而不是在某些現有的應用程式中建立新的具名服務執行個體？ 還有一些案例：

  * hello 新應用程式執行個體是客戶，其程式碼需要 toorun 下某些特定識別或安全性設定。
    * Service Fabric 可定義不同的程式碼封裝 toorun 以特定的身分識別。 在訂單 toolaunch hello 以不同的身分識別，hello 啟用相同的程式碼封裝需要 toooccur 中不同的應用程式執行個體。 試想一個案例，您已部署現有客戶的工作負載。 這些可能會執行以特定的身分識別，所以您可以監視及控制其存取 tooother 資源，例如遠端資料庫或其他系統。 在此情況下，當新客戶註冊，您可能不想 tooactivate hello 其程式碼相同的內容 （處理序空間）。 雖然您可以這使得您特定的身分識別的 hello 內容中的服務程式碼 tooact 不容易。 您通常必須有更高的安全性、隔離及身分識別管理程式碼。 而不是使用不同名為 service hello 相同的應用程式執行個體和因此 hello 相同處理序空間內的執行個體，您可以使用不同的具名的 Service Fabric 應用程式執行個體。 這可讓您更輕鬆 toodefine 不同的識別內容。
  * hello 新應用程式執行個體也可做為一種組態
    * 根據預設，所有服務的具名執行個體特定的服務類型的應用程式執行個體中的 hello 會執行的 hello 相同的處理序指定的節點中。 這表示，儘管您可以使用不同的方式設定每個服務執行個體，但這麼做會很複雜。 服務必須使用其 config 組態封裝內 toolook 某些語彙基元。 這通常是只有 hello 服務的名稱。 這可正常運作，但是涉入的 hello 個別具名的服務執行個體，該應用程式執行個體中的 hello 設定 toohello 名稱。 這可能會造成混淆，硬 toomanage 自組態通常是應用程式執行個體的特定值的設計階段成品。 一律建立更多服務表示多個應用程式升級 toochange hello 資訊內 hello 組態封裝或新的 toodeploy 因此 hello 新服務可以查閱其特定的資訊。 通常會更容易 toocreate 全新的具名的應用程式執行個體。 然後您可以使用 hello 應用程式參數 tooset hello 服務需要任何組態。 如此一來，所有的 hello 服務內，建立名為應用程式執行個體可以繼承的特定組態設定。 例如，單一設定檔與 hello 設定和自訂的每位客戶，例如機密或每個客戶資源限制，您擁有而不會改為不同的應用程式執行個體使用這些設定的每位客戶覆寫。 
  * hello 新應用程式做為升級的界限
    * 在 Service Fabric 內，不同的具名應用程式執行個體會作為升級的界限。 一個具名的應用程式執行個體的升級不會影響另一個具名的應用程式執行個體正在執行的 hello 程式碼。 hello 不同的應用程式，最後將會執行不同版本相同的程式碼的 hello hello 上相同的節點。 當您需要 toomake 縮放的決策，因為您可以選擇是否 hello 新程式碼應該依照 hello 相同升級為另一個服務或不可以的因素。 例如，假設呼叫抵達 hello 管理員服務負責建立或刪除服務動態調整特定客戶工作負載。 在此情況下，hello 呼叫其實與相關聯的工作負載_新_客戶。 大部分的客戶希望還不只是為了 hello 安全性和設定之前，列出能彼此隔離，但因為它提供更多的彈性，以執行特定版本的 hello 軟體，然後選擇當它們進行升級。 您也可以建立新的應用程式執行個體，並建立 hello 服務只要 toofurther 分割區那里 hello 量，您會修改任何一個升級的服務。 個別的應用程式執行個體能在進行應用程式升級時提供更大的細微度，還可進行 A/B 測試和藍色/綠色部署。 
  * hello 現有應用程式執行個體已滿
    * 在 Service Fabric[應用程式容量](service-fabric-cluster-resource-manager-application-groups.md)是您可以針對特定應用程式執行個體使用 toocontrol hello 數量的可用資源的概念。 例如，您可能會決定給定的服務需要 toohave 順序 tooscale 中建立的另一個執行個體。 不過，此應用程式執行個體已超出特定計量的容量。 如果此特定客戶或工作負載應該仍被授與更多資源，然後您可以增加 hello 該應用程式的現有容量或建立新的應用程式。 

## <a name="scaling-at-hello-partition-level"></a>調整在 hello 資料分割層級
Service Fabric 支援資料分割。 分割區會將服務分割成數個邏輯與實體區段，其中每一個都是獨立運作。 這適合用於可設定狀態的服務，因為沒有設定的複本有 toohandle hello 的所有呼叫次 hello 狀態的所有操作。 hello[分割概觀](service-fabric-concepts-partitioning.md)hello 類型支援的資料分割配置上提供的資訊。 每個資料分割的 hello 複本會散佈到 hello 叢集中的節點，該服務的負載，並確定整個都沒有 hello 服務或任何資料分割有單一失敗點。 

假設有一個使用範圍資料分割配置的服務，其中低索引鍵為 0、高索引鍵為 99、資料分割計數為 4。 在三個節點叢集中，hello 服務可能會配置與共用 hello 資源如下所示，每個節點上的四個複本：

<center>
![使用三個節點分割配置](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

如果您增加 hello 節點數目時，Service Fabric 會那里移動某些 hello 現有複本。 例如，假設 hello 節點數目會增加 toofour 並轉散發 hello 複本取得。 現在 hello 服務現在有三個複本的每個節點上執行，每個屬於 toodifferent 資料分割。 這可讓更好的資源使用率，因為 hello 新節點並不陌生。 通常，它也會改善效能因為各服務都有更多的資源可用 tooit。

<center>
![使用四個節點分割配置](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>調整使用 hello Service Fabric 叢集資源管理員和度量
[度量](service-fabric-cluster-resource-manager-metrics.md)是服務如何表達其資源耗用量 tooService 網狀架構。 使用度量會提供 hello 叢集資源管理員有機會 tooreorganize，並最佳化 hello hello 叢集配置。 比方說，可能會有足夠的 hello 叢集中的資源，但它們可能不配置目前正在執行工作的 toohello 服務。 使用計量可讓 hello 叢集資源管理員 tooreorganize 服務具有存取權的 hello 叢集 tooensure toohello 可用資源。 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>調整所新增和移除從 hello 叢集中的節點 
進行 Service Fabric 調整的另一個選項是 toochange hello hello 叢集大小。 變更 hello hello 叢集大小表示加入或移除 hello 叢集中的一個或多個 hello 節點類型的節點。 例如，試想一個情況，所有 hello hello 叢集中的節點會作用。 這表示 hello 叢集資源為幾乎所有取用。 在此情況下，加入更多節點 toohello 叢集是最佳方式 tooscale hello。 一旦 hello 新節點加入 hello 叢集 hello Service Fabric 叢集資源管理員移動服務 toothem 導致較少的總負載 hello 現有節點上。 針對執行個體計數 = -1 的無狀態服務，會自動建立多個服務執行個體。 這可讓某些呼叫 toomove，從 hello 現有節點 toohello 新節點。 

加入和移除節點 toohello 叢集即可透過 hello Service Fabric Azure 資源管理員 PowerShell 模組。

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>總整理
讓我們來看我們這裡所討論，並透過範例交談的所有 hello 意見。 請考慮下列服務的 hello： 您嘗試 toobuild 充當通訊錄 中，服務上 toonames 和連絡資訊。 

您有一大堆問題相關 tooscale 右最前面位置： 使用者數目會持續 toohave？ 每個使用者會儲存多少連絡人？ 嘗試 toofigure 這所有影片時您會一直 hello 服務第一次並不容易。 讓我們假設您要 toogo 具有單一靜態服務的特定分割區計數。 hello 的挑選 hello 錯誤分割區計數可能會導致您 toohave 標尺問題之後的結果。 同樣地，即使所有 hello 資訊都挑選 hello 正確的計數，您可能沒有您需要。 比方說，您也有 toodecide hello 大小的最前面的位置，hello 叢集都會佔用 hello 多節點和其大小。 它通常硬 toopredict 多少的資源服務正在 tooconsume 其存留期。 它也可以是永久 tooknow 前面 hello 服務實際上看到的時間 hello 流量模式。 比方說，或許是人員新增和在 hello 早上，首先只移除他們的連絡人或或許其分佈平均分散在 hello 課程 hello 一天。 根據您可能需要登出 tooscale 動態這個問題。 或許您可以了解 toopredict 當您將 tooneed tooscale out 與中，但無論如何您可能要 tooneed tooreact toochanging 資源耗用量由您的服務。 這可能涉及到變更順序 tooprovide 中的 hello 叢集 hello 大小更多資源時重新組織使用現有的資源不足。 

但為什麼即使嘗試 toopick 所有使用者的單一資料分割配置出嗎？ 為什麼侷限 tooone 服務和一個靜態叢集嗎？hello 真實的情況是通常更具動態。 

在建置小數位數，請考慮 hello 遵循動態的模式。 您可能需要 tooadapt 它 tooyour 情況：

1. 而不是嘗試 toopick 資料分割配置的最前面位置每個人，建置 「 管理員 」 服務 」。
2. hello 作業 hello manager 服務註冊您的服務時 toolook 客戶資訊。 然後根據該資訊 hello 管理員服務建立的執行個體您_實際_連絡人儲存體服務_只針對該客戶_。 如果他們需要特別的組態、 隔離或升級，您也可以針對此客戶決定 toospin 構成應用程式執行個體。 

此動態建立模式的多項優點：

  - 您不想 tooguess hello 正確的資料分割計數最前面位置的所有使用者，或建置是全部都在它自己可無限調整的單一服務。 
  - 不同的使用者沒有 toohave hello 相同資料分割計數、 複本計數、 安置限制、 度量、 預設載入、 服務名稱、 dns 設定，或任何 hello hello 服務在指定的其他屬性或應用程式層級。 
  - 您可以取得其他的資料區段。 每個客戶都有其自己的 hello 服務複本
    - 每個客戶服務可以有不同的設定方式並授與較多或較少資源，以預期的縮放作為基礎，視需要使用較多或較少的分割區或複本。
      - 例如，假設 hello 客戶支付 hello"Gold"層-它們可以取得更多的複本或更高的資料分割計數，並潛在的專用資源 tootheir 服務透過度量和應用程式的容量。
      - 或假設它們提供指示 hello 數目連絡人需要這些資訊是 「 小 」-它們會得到只有幾個資料分割，或甚至無法放入與其他客戶的共用的服務集區。
  - 您不在您等候的總客戶 tooshow 執行一連串的服務執行個體或複本
  - 如果客戶可離開，再移除其資訊從您的服務很簡單，只讓 hello 管理員刪除該服務或它所建立的應用程式。

## <a name="next-steps"></a>後續步驟
如需有關 Service Fabric 概念的詳細資訊，請參閱下列文章 hello:

* [Service Fabric 服務的可用性](service-fabric-availability-services.md)
* [分割 Service Fabric 服務](service-fabric-concepts-partitioning.md)
