---
title: "aaaAzure Service Fabric 災害復原 |Microsoft 文件"
description: "Azure Service Fabric 提供 hello 功能所需 toodeal 用於所有類型的損毀。 這篇文章描述 hello 類型可能會發生的嚴重損壞情況以及如何與其 toodeal。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Azure Service Fabric 中的災害復原
提供高可用性的關鍵在於確保服務能夠承受所有不同類型的故障。 這對於預料之外且無法控制的故障而言特別重要。 本文說明一些常見的故障模式，如果沒有未正確建立模型和管理，可能會造成嚴重損壞。 它也會探討緩和措施和動作 tootake 如果仍發生損毀。 hello 目標是 toolimit，或在發生失敗，已規劃或否則會發生時，排除 hello 的停機時間或資料遺失的風險。

## <a name="avoiding-disaster"></a>避免災害
Service Fabric 的主要目標是 toohelp 您的環境和您服務的方式，常見的失敗類型不是您的嚴重損壞時，您建立的模型。 

一般情況下，災害/故障情節有兩種情況：

1. 硬體或軟體錯誤
2. 操作錯誤

### <a name="hardware-and-software-faults"></a>硬體和軟體錯誤
硬體和軟體錯誤是無法預期的。 最簡單方式 toosurvive 錯誤 hello 執行更多份跨越硬體或軟體錯誤界限 hello 服務。 比方說，如果只有一個特定的機器上執行您的服務，然後 hello 確定一部電腦失敗是該服務損毀。 hello 簡單的方式 tooavoid 此嚴重損壞是指 tooensure hello 服務實際執行多部電腦上。 測試是另一部電腦的必要 tooensure hello 失敗不會中斷執行服務的 hello。 容量規劃，可確保替代執行個體可由其他位置並減少容量不會多載 hello 剩餘服務。 hello 相同的模式運作，不論您正在嘗試的項目 tooavoid hello 失敗。 例如， 如果您擔心 SAN hello 失敗，您會執行跨多個 San。 如果您擔心伺服器機架的 hello 遺失，您會跨多個機架上執行。 如果您擔心 hello 遺失的資料中心，您的服務應執行分散到多個 Azure 區域或資料中心。 

這種類型的合併模式中執行時，您還是同時失敗，但單一和多個失敗的特定類型的主體 toosome 類型 (例如： 單一的 VM 或網路連結失敗) 會自動處理 （並因此不會再 「 災害 」）。 Service Fabric 提供許多擴充 hello 叢集，並處理重新將失敗的節點和服務的機制。 服務網狀架構也可讓您的服務的許多執行個體從執行中順序 tooavoid 這些類型的未預期的失敗開啟到真正的災害。

可能有透過失敗執行部署夠大的 toospan 為何不可行的原因。 例如，可能需要更多硬體資源比您不願意 toopay 的相對 toohello 有故障的機會。 處理分散式應用程式時，可能是跨地理位置距離的其他通訊躍點或狀態複寫成本造成無法接受的延遲。 每個應用程式繪製的此線條有所不同。 軟體錯誤具體來說，hello 錯誤可能是 hello 服務嘗試 tooscale。 在此情況下更多的複製，不會造成 hello 損毀，因為 hello 失敗狀況會跨所有 hello 執行個體相互關聯。

### <a name="operational-faults"></a>操作錯誤
即使您的服務跨越 hello 地球與許多多餘項目，它仍可能會遇到而言事件。 例如，如果有人不小心重新設定 hello hello 服務的 dns 名稱或將它完全刪除。 舉例來說，假設您的 Service Fabric 具狀態服務，而有人不小心刪除了該服務。 除非有其他風險降低，該服務所有 hello 狀態，請立即消失。 這些類型的操作災害 (「糟糕」情況) 恢復所需的緩解和步驟與一般未預期故障不同。 

hello 最佳方式 tooavoid 這些類型的操作錯誤為
1. 限制作業存取 toohello 環境
2. 嚴格稽核危險的作業
3. 強制執行自動化，避免手動或移出頻外變更，而且之前制定這些驗證針對 hello 實際環境的特定變更
4. 確認破壞性操作是否為「軟性」。 軟性操作不會立即生效，或是可以在一段時間內復原

服務網狀架構會提供一些機制 tooprevent 操作錯誤，例如提供[以角色為基礎](service-fabric-cluster-security-roles.md)存取控制針對叢集操作。 不過，大部分的操作錯誤需要投入組織化的心力以及其他系統。 Service Fabric 提供一些機制以因應操作錯誤，最值得注意的是具狀態服務的備份與還原。

## <a name="managing-failures"></a>管理故障
Service Fabric hello 目標幾乎都是自動管理的失敗。 不過，若要 toohandle 某些類型的錯誤，服務必須有額外的程式碼。 因為安全和營運永續性的考量，_不_應該自動解決其他類型的故障。 

### <a name="handling-single-failures"></a>處理單一故障
單一機器可能鑒於各種原因而故障。 其中一些是硬體因素，例如電源供應器和網路硬體故障。 其他是軟體故障， 這些包含失敗的實際作業系統 hello 和 hello 服務本身。 服務網狀架構會自動偵測這些失敗類型，包括萬一 hello 電腦無法與其他機器因為 toonetwork 問題隔離。

Hello 不論類型為何的服務，執行單一執行個體產生該服務的停機時間如果因為任何原因失敗 hello 程式碼的單一複本。 

在順序 toohandle 任何單一失敗，hello 最簡單的事，您可以是您的服務在一個以上的節點執行預設的 tooensure。 針對無狀態服務，這可藉由讓 `InstanceCount` 大於 1 來實現。 可設定狀態服務，hello 最小建議的做法是永遠`TargetReplicaSetSize`和`MinReplicaSetSize`為至少 3。 執行服務程式碼的多個複本可確保您的服務可自動處理任何單一失敗。 

### <a name="handling-coordinated-failures"></a>處理協調失敗
協調的失敗可能會發生因為 tooeither 計劃或非計劃的基礎結構失敗和變更，或是已規劃的軟體變更叢集中。 Service Fabric 會將發生協調失敗的基礎結構區域建立模型，做為「容錯網域」。 發生協調軟體變更的區域會建立模型做為「升級網域」。 關於容錯網域和升級網域的更多資訊，請參閱[此文件](service-fabric-cluster-resource-manager-cluster-description.md)，文中會說明叢集的拓撲和定義。

在規劃應在何處執行服務時，Service Fabric 依預設會考慮容錯網域和升級網域。 根據預設，Service Fabric 會嘗試 tooensure 規劃或未規劃的變更，就可能發生，如果您的服務仍可讓您的服務執行跨數個容錯網域和升級網域。 

例如，假設失敗的電力來源，同時會造成機器 toofail 機架。 使用中容錯網域失敗時所執行的許多機器 hello 遺失的 hello 服務的多個複本會轉換成只是另一個範例中的指定服務的單一失敗。 這就是為什麼管理的容錯網域是重大 tooensuring 高可用性，您的服務。 在 Azure 中執行 Service Fabric 時，會自動管理容錯網域。 在其他環境中可能不會自動管理。 如果您建置在內部部署叢集，可確定 toomap 並正確規劃您的容錯網域版面配置。

升級網域可用於模型化軟體正在發生 toobe 升級 hello 相同區域的時間。 因為這個緣故，升級 」 網域通常也會定義其中計劃升級期間停機軟體 hello 界限。 服務網狀架構和您的服務升級遵循 hello 相同的模型。 如需輪流升級，升級的網域和 hello 服務網狀架構健全狀況模型，可協助避免非預期的變更影響 hello 叢集與您的服務詳細資訊，請參閱這些文件：

 - [應用程式升級](service-fabric-application-upgrade.md)
 - [應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md)
 - [Service Fabric 健康情況模型](service-fabric-health-introduction.md)

您可以視覺化 hello 版面配置使用 hello 叢集對應中提供您叢集的[Service Fabric 總管](service-fabric-visualizing-your-cluster.md):

<center>
![節點散佈於 Service Fabric Explorer 中的各個容錯網域][sfx-cluster-map]
</center>

> [!NOTE]
> 模型失敗，輪流升級，執行您的服務程式碼和狀態的許多執行個體的區域放置規則 tooensure 跨容錯和升級網域，執行您的服務和內建的健全狀況監視只是**某些**的 helloService Fabric 順序 tookeep 正常操作問題並開啟到的嚴重損壞時從失敗中所提供的功能。 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>處理同時發生的硬體或軟體故障
上述探討的是單一故障。 如您所見，是無狀態與可設定狀態服務的簡單 toohandle 只會保留更多份 hello 程式碼 （和狀態） 跨過容錯和升級網域。 也可能發生多個同時的隨機失敗。 這些是更 toolead tooan 實際嚴重損壞。


### <a name="random-failures-leading-tooservice-failures"></a>隨機失敗導致 tooservice 失敗
假設 hello 服務有`InstanceCount`5 和數個節點執行這些執行個體的所有失敗 hello 在相同的時間。 Service Fabric 會藉由在其他節點上自動建立取代執行個體來回應。 它會繼續建立取代項目，直到 hello 服務回 tooits 預期執行個體計數。 另舉一例，假設有無狀態服務與`InstanceCount`-1，這表示在 hello 叢集中的所有有效的節點上執行。 比方說有些這些執行個體是 toofail。 在此情況下，Service Fabric 通知 hello 服務不在其所需的狀態，而且會嘗試 toocreate hello 執行個體，但已遺失的 hello 節點上。 

可設定狀態服務的 hello 情況取決於是否 hello 服務已保存狀態或不。 它也取決於有多少複本 hello 服務和多少失敗。 判斷具狀態服務是否發生災害，並進行管理，如下三個階段：

1. 判斷是否有仲裁遺失
 - 仲裁遺失是可設定狀態服務的 hello 複本的大部分都可以向下 hello 任何時間相同的時間，包括主要 hello。
2. 判斷 hello 仲裁遺失是否為永久
 - 大部分的 hello 時間是暫時性失敗。 處理程序會重新啟動，節點會重新啟動，VM 會重新啟動，網路磁碟分割會修復。 不過有時候失敗是永久性的。 
    - 對於非持續狀態的服務，單一仲裁或多個複本的失敗會_立即_導致永久性的仲裁遺失。 當 Service Fabric 偵測到遺失仲裁，可設定狀態的非持續性服務中時，便會立即繼續 dataloss toostep 3 藉由宣告 （可能）。 因為 Service Fabric 知道沒有點中等候 hello 複本 toocome 後，即使它們都已復原它們會是空白，再繼續 toodataloss 才有意義。
    - 對於可設定狀態的持續性服務，仲裁或多個複本的失敗會造成 Service Fabric toostart 等候 hello 複本 toocome 備份和還原仲裁。 這會導致服務中斷的任何_寫入_toohello 影響 hello 服務磁碟分割 （或 「 複本集 」）。 不過，仍可能在降低一致性保證的情況下進行讀取。 hello 預設的 Service Fabric 等候仲裁 toobe 還原量是時間的無限的因為繼續 （可能） 的 dataloss 事件，而且附帶其他風險。 覆寫 hello 預設`QuorumLossWaitDuration`值可能會但不是建議使用。 改為在此階段中，所有投入時間應該會向複本 toorestore hello。 這需要攜帶 hello 的節點下一步，並確保它們可以重新掛接 hello 它們用來儲存 hello 本機永續性狀態的磁碟機。 如果 hello 仲裁遺失因為處理序失敗，Service Fabric 自動嘗試 toorecreate hello 處理程序，並重新啟動那些 hello 複本。 如果此作業失敗，Service Fabric 會報告健康情況錯誤。 如果這些都無法解析然後 hello 複本通常回來。 有時候，不過，hello 複本將無法處於回。 比方說，hello 磁碟機可能所有已失敗，或由於某種原因而 hello 機器實際終結。 在這些情況下，我們現在有一個永久性的仲裁遺失事件。 等候複本 toocome，叢集系統管理員向 hello tootell Service Fabric toostop 必須判斷哪些資料分割，其中，服務會受到影響，呼叫 hello`Repair-ServiceFabricPartition -PartitionId`或` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)`應用程式開發介面。  此 API 可讓您指定的從 QuorumLoss 移至潛在 dataloss hello 分割 toomove hello ID。

> [!NOTE]
> 它是_從未_安全 toouse 此應用程式開發介面以外的目標方式，針對特定的資料分割中。 
>

3. 判斷是否已有實際資料遺失，並從備份還原
  - 當 Service Fabric 呼叫 hello`OnDataLossAsync`方法一律會因為_懷疑_dataloss。 服務網狀架構，可確保此呼叫會傳遞 toohello_最佳_其餘複本。 這是不論哪一個複本已進行 hello 大部分的進度。 hello 的原因，我們一律說_懷疑_dataloss 是，它可能該 hello 其餘複本確實具有相同的所有狀態 hello 主要它已關閉時一樣。 不過，如果該狀態 toocompare 沒有它，就不好的 Service Fabric 或運算子 tooknow 供確認。 此時，Service Fabric 也知道 hello 其他複本無法返回。 這是我們停止等待 hello 仲裁遺失 tooresolve 本身時所做的 hello 決策。 hello 最佳的 hello 服務動作通常是 toofreeze，等候特定的系統管理員操作。 項目也會跟著 hello 的一般實作`OnDataLossAsync`方法？
  - 首先，記錄 `OnDataLossAsync` 已觸發，並關閉任何必要的管理警示。
   - 通常這個時候 toopause，並等待進一步決策及採取手動動作 toobe。 這是因為即使備份可供使用，它們就可能需要 toobe 備妥。 例如，如果兩個不同的服務會協調資訊，這些備份可能需要 toobe 一旦 hello 還原發生的 hello 資訊的兩個服務關心是一致的順序 tooensure 中修改。 
  - 通常另外還有一些其他遙測或排氣從 hello 服務。 此中繼資料可能包含在其他服務或記錄中。 這項資訊可以使用所需的 toodetermine hello 備份或複寫 toothis 特定複本中沒有任何呼叫接收及處理在主要 hello 一樣。 這些可能需要 toobe 重新執行或者新增 toohello 備份還原才可行。  
   - Hello 剩餘複本的狀態 toothat 任何可用的備份中包含的比較。 如果使用 hello Service Fabric 可靠集合，則表示工具，處理供執行這項作業中所述[本文](service-fabric-reliable-services-backup-restore.md)。 hello 目標時 toosee hello 複本中的 hello 狀態即已足夠，或也 hello 備份可能已遺失。
  - 一次 hello 而做比較，如果完成必要的 hello 還原，hello 服務程式碼應該會傳回有任何狀態變更時，則為 true。 如果它已 hello 最佳可用的複本 hello 狀態，並不會變更，判斷出 hello 複本，則傳回 false。 True 表示任何_其他_剩餘複本現在可能與此複本不一致。 將會卸除這些複本，並從此複本重建。 False 表示未進行任何狀態變更，因此 hello 其他複本可以保留它們的有。 

在生產中部署服務之前，服務製作者在實踐潛在的資料遺失和失敗案例至關重要。 針對 dataloss hello 可能性 tooprotect，務必 tooperiodically[備份 hello 狀態](service-fabric-reliable-services-backup-restore.md)任何您可設定狀態服務 tooa 異地備援存放區。 您也必須確定您擁有 hello 能力 toorestore 它。 因為許多不同的服務備份在不同的時間，您需要在還原後您的服務具有一致的檢視彼此的 tooensure。 例如，假設一項服務產生數字和加以儲存，然後將它傳送 tooanother 服務，也會儲存的位置。 還原之後，您可能會發現 hello 第二個服務都有 hello 數字，但 hello 第一次不存在，因為它的備份不包含該作業。

如果您發現該 hello 剩餘複本不足 toocontinue 從在 dataloss 案例中，而且您無法建構從遙測或排氣服務狀態，您的備份的 hello 頻率會決定您最佳的可能復原點目標 (RPO). Service Fabric 會提供許多工具，以測試各種失敗情況，包括需要從備份還原的永久仲裁和資料遺失。 這些案例會包含 Service Fabric 可測試性工具，受 hello 錯誤 Analysis Service 的一部分。 這些工具和模式的詳細資訊，請見[這裡](service-fabric-testability-overview.md)。 

> [!NOTE]
> 系統服務也可能會遺失仲裁、 與 hello 影響因素是特定 toohello 服務有問題。 比方說，hello 命名服務中的仲裁遺失而仲裁遺失中 hello 容錯移轉管理員服務會封鎖新的服務建立和容錯移轉會影響名稱解析。 雖然 hello Service Fabric 系統服務會依照相同模式為您進行狀態管理服務的 hello，但不建議您應該嘗試 toomove 從仲裁遺失移至潛在 dataloss 它們。 hello 建議改用太[尋求支援](service-fabric-support.md)toodetermine 方案，目標 tooyour 特定情況。  通常它是比 toosimply 等候直到向複本傳回 hello。
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Hello Service Fabric 叢集的可用性
一般而言，hello Service Fabric 叢集本身是任何單一失敗點的高度分散的環境。 任何一個節點的失敗不會導致可用性或可靠性問題 hello 叢集，主要是因為 hello Service Fabric 系統服務會遵循相同的指導方針之前所提供的 hello： 它們永遠都可執行三個或多個複本的預設值，以及系統服務是無狀態的所有節點上執行。 完整散發 hello 基礎 Service Fabric 網路功能與失敗偵測層級。 大部分的系統服務從 hello 叢集中的中繼資料就可以重建，或者知道如何 tooresynchronize 其狀態的其他位置。 如果系統服務會進入仲裁遺失情況說明上述 hello hello 叢集可用性可能會變成洩露出去。 在這些情況下您可能不是能 tooperform 特定 hello 叢集上的作業，例如開始升級或部署新服務，但 hello 叢集本身仍在運作。 已在執行上的服務會保留在這些情況中執行，除非它們需要寫入 toohello 系統服務 toocontinue 運作。 比方說，如果 hello 容錯移轉管理員是在仲裁遺失所有的服務將繼續 toorun，但失敗的任何服務將無法 tooautomatically 無法重新啟動，因為它會要求 hello 參與 hello 容錯移轉管理員。 

### <a name="failures-of-a-datacenter-or-azure-region"></a>資料中心或 Azure 區域的失敗
在少數情況下，實體資料中心可能會因為暫時無法使用 tooloss 電源或網路連線能力。 在這些情況下，在資料中心或 Azure 區域中的 Service Fabric 叢集和服務將無法使用。 不過，_您的資料會保留下來_。 在 Azure 中執行的叢集，您可以檢視更新上關閉 hello [Azure 狀態 頁面][azure-status-dashboard]。 在 hello 終結不太可能在實體資料中心是部分或完整的事件，那里裝載任何 Service Fabric 叢集或其中 hello 服務可能會遺失。 這包括在該資料中心或區域外部未備份的任何狀態。

沒有兩個不同的策略來存活 hello 的單一資料中心或地區的永久或持續性失敗。 

1. 在多個此類區域中，執行不同的 Service Fabric 叢集，並在這些環境之間利用容錯移轉和容錯回復的一些機制。 這種多叢集的主動至主動或主動至被動模型需要其他管理和作業碼。 這也需要的備份，從一個資料中心或區域中的 hello 服務協調，讓它們可用於其他資料中心或區域時失敗。 
2. 執行跨越多個資料中心或區域的單一 Service Fabric 叢集。 hello 最低支援的設定這是三個資料中心或區域。 hello 建議的區域數目或資料中心為 5。 這需要更複雜的叢集拓撲。 不過，hello 這個模型的優點是，一個資料中心或地區的失敗從嚴重損毀轉換成一般失敗。 可由單一區域內的叢集 hello 機制可處理這些失敗。 容錯網域、升級網域，以及 Service Fabric 放置規則確保工作負載是分散的，以便容忍一般失敗。 如需有助於在此類叢集中操作服務之原則的詳細資訊，請參閱[放置原則](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)

### <a name="random-failures-leading-toocluster-failures"></a>隨機失敗導致 toocluster 失敗
Service Fabric 有 hello 概念的種子節點。 這些是維護 hello 可用性的 hello 基礎叢集的節點。 這些節點會協助 tooensure hello 叢集會維持總建立租用，與其他節點，以及作為 tiebreakers 期間特定種類的網路失敗。 如果隨機失敗 hello 叢集中移除大多數 hello 種子節點，它們不帶回 hello 叢集會自動關閉。 在 Azure 中，種子節點會自動管理： 它們透過 hello 提供容錯和升級的網域，散發，而且如果從 hello 叢集中移除單一種子節點將在其位置中建立另一個。 

獨立 Service Fabric 叢集和 Azure 中 hello 「 主要節點類型 」 是指執行 hello 種子 hello。 當定義主要節點類型，Service Fabric 會自動利用 hello 提供藉由建立 too9 種子節點和 9 hello 系統服務的每個複本的節點數目。 如果在一組隨機失敗出這些系統服務複本的多數同時，hello 系統服務會進入遺失仲裁、 如我們上面所述。 如果大多數 hello 種子節點遺失，hello 叢集會關閉後立即。

## <a name="next-steps"></a>後續步驟
- 深入了解如何 toosimulate 各種失敗情況使用 hello[可測試性架構](service-fabric-testability-overview.md)
- 閱讀其他災害復原和高可用性的資源。 Microsoft 已發佈大量有關這些主題的指引。 而這些文件的某些其他產品的使用 toospecific 技術，其中包含許多一般的最佳作法，您可以套用 hello Service Fabric 內容中：
  - [可用性檢查清單](../best-practices-availability-checklist.md)
  - [執行災害復原演練](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Azure 應用程式的災害復原和高可用性][dr-ha-guide]
- 了解 [Service Fabric 支援選項](service-fabric-support.md)

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
