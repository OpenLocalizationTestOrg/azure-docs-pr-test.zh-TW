---
title: "aaaPlanning hello Service Fabric 叢集容量 |Microsoft 文件"
description: "Service Fabric 叢集容量規劃考量。 Nodetypes、持久性和可靠性層級"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>Service Fabric 叢集容量規劃考量
對於任何生產部署而言，容量規劃都是一個很重要的步驟。 以下是一些您在該程序的一部分有 tooconsider hello 項目。

* hello 數目節點類型出與您叢集的需求 toostart
* 每個節點型別 （大小、 主要伺服器上，網際網路對向 Vm 等） 的 hello 內容
* hello 可靠性和持久性 hello 叢集特性

讓我們簡短地檢閱各個項目。

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>hello 數目節點類型出與您叢集的需求 toostart
首先，您需要出您要建立何種 hello 叢集即將用於 toobe 和規劃的應用程式種類 toofigure toodeploy 到此叢集中。 如果您不是 hello 目的 hello 叢集上的 清除，您最有可能尚未就緒 tooenter hello 容量規劃程序。

建立您的叢集需要與 out toostart 的節點類型的 hello 數目。  每個節點類型會對應的 tooa 虛擬機器擴展集。 然後每個節點類型可以獨立相應增加或相應減少，可以開啟不同組的連接埠，並可以有不同的容量度量。 因此 hello 決策 hello 數種節點類型的基本上這時候您就要 toohello 下列考量：

* 您的應用程式是否有多個服務，而且其中任何需要 toobe 公用或網際網路？ 應用程式通常會包含從用戶端，接收輸入前端的閘道服務與一或多個後端服務通訊的 hello 前端服務。 因此，在此情況下，您最終會有至少兩個節點類型。
* 您 (構成應用程式) 的服務是否有不同的基礎結構需求，例如，更多的 RAM 或更高的 CPU 週期？ 例如，讓我們假設您想 toodeploy 包含前端服務和後端服務的 hello 應用程式。 hello 前端服務可以執行具有開啟 toohello 連接埠的較小 Vm （例如 D2 的 VM 大小） 上網際網路。  hello 後端服務，不過，較大的 Vm (例如 D4，D6，D15 VM 大小） 不是網際網路上的計算需要大量和需求 toorun 遇到。
  
  在此範例中，雖然您可以決定 tooput 所有 hello 一個節點類型上的服務，我們建議您將它們在叢集中有兩種節點類型。  這可讓每個節點型別 toohave 相異屬性，例如網際網路連線或 VM 大小。 獨立，也可以調整 Vm 的 hello 數目。  
* 因為您無法預測未來 hello，請與您知道的事項，並決定節點型別，應用程式需要與 toostart 的 hello 數目。 您之後都可以新增或移除節點類型。 Service Fabric 叢集必須至少有一個節點類型。

## <a name="hello-properties-of-each-node-type"></a>類型的每個節點的 hello 屬性
hello**節點型別**可視為相等 tooroles 雲端服務中。 節點型別定義 hello VM 大小、 hello 的 Vm，以及它們的屬性。 在 Service Fabric 叢集中定義的每個節點類型都會安裝為不同的虛擬機器擴展集。 虛擬機器規模集是 Azure 計算資源，您可以使用 toodeploy 和管理的虛擬機器作為一組的集合。 如果定義為不同的虛擬機器擴展集，則每個節點類型都可以獨立相應增加或相應減少、可以開放不同組的連接埠，而且可以有不同的容量度量。

讀取[這份文件](service-fabric-cluster-nodetypes.md)Nodetypes toovirtual 機器規模集的 hello 關聯性的詳細資料，如何 tooRDP 合而為一的 hello 執行個體，開啟新連接埠等。

您的叢集可以有一個以上的節點類型，但 hello 主要節點類型 (hello hello 入口網站上定義的第一個) 必須至少五個叢集用於實際執行工作負載的 Vm （或至少三個測試叢集的 Vm）。 如果您要建立 hello 叢集使用的資源管理員範本，然後尋找**是主要**下 hello 節點型別定義的屬性。 hello 主要節點類型為 hello 節點型別放置 Service Fabric 系統服務。  

### <a name="primary-node-type"></a>主要節點類型
針對多個節點類型的叢集，您需要其中一個 toochoose toobe 主要。 以下是 hello 的主要節點類型的特性：

* hello **Vm 的大小下限**hello 主要節點類型會判定 hello**持久性層**您選擇。 hello 持久性層的 hello 預設值是青銅卡。 如需詳細資訊是何種 hello 持久性層，以及 hello 的值可能需要向下捲動。  
* hello **Vm 的最小數目**hello 主要節點類型會判定 hello**可靠性層**您選擇。 hello 可靠性層的 hello 預設值為銀級。 如需詳細資訊是何種 hello 可靠性層，以及 hello 的值可能需要向下捲動。 


* hello Service Fabric 系統服務 （例如，hello 叢集管理員服務或映像存放區服務） 會放在 hello 主要節點類型，因此 hello 可靠性和持久性的 hello 叢集由 hello 可靠性層的值與持久性層您選取 hello 主要節點類型的值。

![有兩個節點類型的叢集螢幕擷取畫面 ][SystemServices]

### <a name="non-primary-node-type"></a>非主要節點類型
針對多個節點類型的叢集，一個主要節點類型，而 hello 其餘的非主要。 以下是 hello 特性的非主要節點類型：

* hello 最小的 Vm 給這個節點類型取決於您選擇的 hello 持久性層。 hello 持久性層的 hello 預設值是青銅卡。 如需詳細資訊是何種 hello 持久性層，以及 hello 的值可能需要向下捲動。  
* hello 最小的 Vm 數目給這個節點類型可以是下列其中一個。 不過，您應該選擇這個數字，根據 hello hello 應用程式/服務希望 toorun 中這個節點類型的複本數目。 部署 hello 叢集之後，可以增加節點型別中的 Vm hello 數目。

## <a name="hello-durability-characteristics-of-hello-cluster"></a>hello 持久性 hello 叢集特性
hello 持久性層是使用的 tooindicate toohello 系統 hello Vm 具有的權限與 hello 基本 Azure 基礎結構。 在 hello 主要節點類型這個權限會讓 Service Fabric toopause hello 系統服務和可設定狀態服務的 hello 仲裁需求會影響任何 VM 層級的基礎結構要求 （例如 VM 重新開機，VM 重新安裝映像或移轉 VM）。 在 hello 非主要節點類型中，此權限可讓您可設定狀態的服務執行中的 hello 仲裁需求會影響任何 VM 層級的基礎結構要求像 VM 重新開機、 VM 重新安裝映像、 移轉 VM 等，Service Fabric toopause。

此權限是在 hello 下列值來表示：

* 金級-hello UD 每兩小時期間可以暫停工作的基礎結構。 Gold 持久性只能在完整節點 VM SKU (例如 D15_V2、G5 等) 上啟用。
* 銀級-hello 基礎結構工作可暫停一段 UD 每 10 分鐘，可在單一核心的和更新版本的所有標準 Vm 上。
* Bronze - 無權限。 這是 hello 預設值。 針對_僅_執行無狀態工作負載的節點類型，只能使用這個持久性等級。 

> [!WARNING]
> 執行 Bronze 持久性的節點類型_沒有權限_。 這表示不會停止或延遲對您的無狀態工作負載造成影響的基礎結構作業。 這類作業很可能仍會影響您的工作負載，導致停機時間或其他問題。 對於任何種類的生產工作負載，建議至少以 Silver 執行。 
> 

您可以取得 toochoose 持久性層級的每個節點類型。您可以選擇一個節點型別 toohave 金級持久性層級或銀級和其他 hello hello 中都有青銅卡相同的叢集。**必須維護 durability 金級 」 或 「 銀級的任何節點類型 5 個節點的最小計數**。 

**使用 Silver 或 Gold 持久性層級的優點**
 
1. 會減少所需的步驟，在標尺在作業中的 hello 數目 （亦即，節點停用和移除 ServiceFabricNodeState 會自動呼叫）
2. 可降低 hello 到期 tooa 客戶起始就地 VM SKU 變更作業或 Azure 基礎結構作業的資料遺失風險。
     
**使用 Silver 或 Gold 持久性層級的缺點**
 
1. 虛擬機器擴展集的部署 tooyour 和其他相關的 Azure 資源） 可能會因為延遲、 可以逾時，或完全由您的叢集或 hello 基礎結構層級的問題，可能會封鎖。 
2. 增加 hello 數目[複本生命週期事件](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle )（例如，主要交換） 因為 tooautomated 節點和停用 Azure 基礎結構作業期間。

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>建議何時 toouse 銀級或金級持久性層級

使用銀級或金級持久性的所有節點都類型都會該主機可設定狀態服務預期 tooscale 中 （降低 VM 執行個體計數） 通常，您希望部署作業會因為延遲，以利於簡化這些小數位數的作業。 （將 Vm 執行個體） 的 hello 向外延展案例不會播放到您所選擇的 hello 持久性層，唯一的小數位數中。

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>操作建議 hello 節點輸入您已設定 toosilver 或金級持久性層級。

1. 讓叢集和應用程式狀況良好在任何時候，並確定應用程式回應 tooall[服務複本生命週期事件](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle)（例如在組建中的複本是否陷入停滯） 能夠及時。
2. 採用更安全方式 toomake VM SKU 變更 （小數位數向上/向下）： 變更的 hello 的虛擬機器擴展集 VM SKU 原本就不安全的作業，因此應該儘可能避免。 以下是您可以依照 tooavoid 常見問題的 hello 程序。
    - **針對非主要 nodetypes:**建議您建立新虛擬機器擴展集、 修改 hello 服務位置限制式 tooinclude hello 新虛擬機器擴展集/節點類型及接著減少 hello 舊虛擬機器擴展集（這是確定移除 hello 節點不會影響 hello 叢集的 hello 可靠性 toomake） 一次一個節點執行個體計數 too0。
    - **如 hello 主要 nodetype:**我們建議您不要變更 VM SKU 的 hello 主要節點類型。 如果 hello 原因為 hello 新 SKU 容量，我們建議將加入多個執行個體，或可能的話，請建立新的叢集。 如果您沒有任何選擇，請修改 toohello 虛擬機器擴充集模型定義 tooreflect hello 新 SKU。 如果您的叢集有只有一個節點類型，請確認所有可設定狀態之應用程式回應 tooall[服務複本生命週期事件](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle)（例如在組建中的複本是否陷入停滯） 能夠及時以及服務複本重建持續時間是五分鐘內 （適用於銀級持久性層級）。 


> [!WARNING]
> 不建議變更 hello VM 未執行至少銀級耐久性的 VM 規模集 SKU 大小。 變更 VM SKU 大小是資料破壞性就地基礎結構作業。 沒有至少部分能力 toodelay 或監視這項變更，就可能 hello 作業可能會導致 dataloss 可設定狀態的服務，或導致其他未預期操作問題，甚至針對無狀態工作負載。 
> 
    
3. 針對所有啟用 MR 的虛擬機器擴展集維持至少五個節點
4. 請勿隨機刪除 VM 執行個體，而一律使用虛擬機器擴展集的相應減少功能。 hello 刪除隨機 VM 執行個體都有可能會在分佈於 UD 和 FD hello VM 執行個體中建立失衡。 此不平衡嚴重地影響 hello 系統能力 tooproperly 負載平衡堆 hello 服務/服務執行個體的複本。
6. 如果使用自動調整規模，然後設定 hello 規則 （移除的 VM 執行個體） 中的小數位數由一次只有一個節點。 一次相應減少超過一個執行個體並不安全。
7. 如果向下主要節點類型的擴充，您應該永遠不會它向下調整超過哪些 hello 可靠性層允許。


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>hello 可靠性 hello 叢集特性
hello 可靠性層會使用 tooset hello 數目 hello 系統服務，您想 toorun hello 主要節點類型這個叢集中的複本。 hello 複本的多個 hello 數目、 hello 更可靠的 hello 系統服務會在您的叢集。  

hello 可靠性層可以採用下列值的 hello:

* 白金級-9 的目標複本集計數執行 hello 系統服務
* 金級-執行 hello 系統服務與目標複本設定為 7 的計數
* 銀級-5 的目標複本集計數執行 hello 系統服務 
* 青銅卡-執行 hello 系統服務 3 的目標複本集計數

> [!NOTE]
> 您選擇的 hello 可靠性層會決定 hello 主要節點類型必須有的節點數目下限。 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Hello 可靠性層的建議。

 當您增加或減少叢集 (所有節點型別中的 VM 執行個體的 hello sum) hello 大小時，您必須更新您的叢集，從某一層 tooanother hello 可靠性。 執行此動作會觸發 hello 叢集升級所需的 toochange hello 系統服務複本集計數。 等候 hello 升級進度 toocomplete 中進行任何其他變更 toohello 叢集中，例如新增節點之前。  您可以監視的 hello 升級 Service Fabric 總管或藉由執行 hello 進度[Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

以下是選擇 hello 可靠性層 hello 建議。

| **叢集大小** | **可靠性層級** |
| --- | --- |
| 1 |未指定 hello 可靠性層參數，hello 系統會計算它 |
| 3 |Bronze |
| 5 或 6|Silver |
| 7 或 8 |Gold |
| 9 以上 |Platinum |




## <a name="primary-node-type---capacity-guidance"></a>主要節點類型 - 容量指引

以下是規劃 hello 主要節點類型容量 hello 指引

1. **VM 執行個體數目 toorun 在 Azure 中的任何生產工作負載：**您必須指定主要節點類型大小下限為 5。 
2. **VM 執行個體數目 toorun 在 Azure 中的測試工作負載**您可以指定最小的主要節點類型大小為 1 或 3。 hello 一個節點的叢集，執行具有特殊的設定，因此，不支援從該叢集移除的標尺。 hello 一個節點的叢集，有沒有可靠性且因此在資源管理員範本中，您必須指定該組態的 tooremove/not （如果未將 hello 組態值不是足夠）。 如果您設定 hello 一個節點的叢集設定透過入口網站，然後 hello 組態會自動處理。 1 和 3 個節點叢集不支援執行生產工作負載。 
3. **VM SKU:**主要節點類型會是 hello 系統服務執行的位置，讓您選擇，必須採取到帳戶 hello 整體尖峰載入您的 VM SKU hello 規劃 tooplace 到 hello 叢集中。 以下是什麼我是說這裡將 hello 主要節點類型視為您"Lungs"，它是什麼提供氧氣 tooyour 大腦，比喻 tooillustrate，因此如果 hello 大腦未得到足夠氧氣，您主體遇到問題。 

由於叢集的 hello 容量需求取決於工作負載您計劃 toorun hello 叢集中，我們目前無法提供您與您特定的工作負載的質化指導，不過此處為 hello 廣泛指導 toohelp 快速入門

生產工作負載 


- hello 建議 VM SKU 是標準 D3 或標準 D3_V2 或對等項目，並至少加裝 14 GB 的本機 SSD。
- 標準 D1 或標準 D1_V2 或對等項目，並至少加裝 14 GB 的本機 SSD hello 最小支援使用 VM SKU。 
- 局部核心 VM SKU 不支援生產工作負載，例如標準 A0。
- 基於效能理由，標準 A1 SKU 不支援生產工作負載。


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>非主要節點類型 - 具狀態工作負載的容量指引

本指南是針對使用 Service fabric 的可設定狀態工作負載[可靠的集合或 reliable Actors](service-fabric-choose-framework.md)您正在執行中 hello 非主要節點類型。


**VM 執行個體數目︰**對於具狀態生產工作負載，建議使用目標複本計數至少為 5 來執行工作負載。 這表示在穩定狀態下，最後每個容錯網域和升級網域中會有一個複本 (來自複本集)。 hello 主要節點類型的 hello 整個可靠性層概念是方式 toospecify 系統服務的設定。 因此 hello 相同考量適用於以及 tooyour 可設定狀態的服務。

因此對於生產工作負載，hello 最小建議非主要節點類型的大小是 5，如果您在其中執行可設定狀態工作負載。


**VM SKU:**這 hello 節點型別其中應用程式服務正在執行，所以 hello VM SKU 您選擇，必須考慮到帳戶 hello 尖峰負載您規劃 tooplace 到每個節點。 hello hello nodetype 的容量需求，取決於工作負載您計劃 toorun hello 叢集中，因此我們目前無法提供您的特定的工作負載，不過以下是您開始的 hello 廣泛指導 toohelp 質化指南

生產工作負載 

- hello 建議 VM SKU 是標準 D3 或標準 D3_V2 或對等項目，並至少加裝 14 GB 的本機 SSD。
- 標準 D1 或標準 D1_V2 或對等項目，並至少加裝 14 GB 的本機 SSD hello 最小支援使用 VM SKU。 
- 局部核心 VM SKU 不支援生產工作負載，例如標準 A0。
- 基於效能理由，標準 A1 SKU 確定不支援生產工作負載。


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>非主要節點類型 - 無狀態工作負載的容量指引

本指南的 hello 非主要節點類型執行的無狀態工作負載。

**VM 執行個體數目：**是無狀態的實際執行工作負載，hello 最小支援非主要節點類型的大小是 2。 這可讓您 toorun 您兩個無狀態執行個體的應用程式並允許服務 toosurvive hello 喪失 VM 執行個體。 

> [!NOTE]
> 如果您的叢集服務網狀架構版本早於 5.6 上執行，因為 hello tooa 異常執行階段 （5.6 中修正此問題），而縮小非主要節點類型 tooless 大於 5，導致開啟狀況不良，直到您呼叫的叢集健全狀況[移除 ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) hello 適當的節點名稱。 如需詳細資訊，請參閱[放大或縮小執行 Service Fabric 叢集](service-fabric-cluster-scale-up-down.md)
> 
>

**VM SKU:**這 hello 節點型別其中應用程式服務正在執行，所以 hello VM SKU 您選擇，必須考慮到帳戶 hello 尖峰負載您規劃 tooplace 到每個節點。 hello hello nodetype 的容量需求，取決於工作負載您計劃 toorun hello 叢集中，因此我們目前無法提供您的特定的工作負載，不過以下是您開始的 hello 廣泛指導 toohelp 質化指南

生產工作負載 


- hello 建議 VM SKU 是標準 D3 或標準 D3_V2 或同等權限。 
- hello 最小支援使用 VM SKU 是標準在 D1 或標準 D1_V2 或對等項目。 
- 局部核心 VM SKU 不支援生產工作負載，例如標準 A0。
- 基於效能理由，標準 A1 SKU 不支援生產工作負載。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>後續步驟
一旦您完成容量規劃，並設定叢集，請閱讀 hello 下列：

* [Service Fabric 叢集安全性](service-fabric-cluster-security.md)
* [Service Fabric 健康情況模型簡介](service-fabric-health-introduction.md)
* [Nodetypes tooVirtual 機器標尺的關聯性設定](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
