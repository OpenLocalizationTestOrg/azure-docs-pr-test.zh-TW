---
title: "規劃 Service Fabric 應用程式的 aaaCapacity |Microsoft 文件"
description: "描述如何 tooidentify hello 的 Service Fabric 應用程式所需的運算節點數目"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Service Fabric 應用程式的容量規劃
這份文件教您如何 tooestimate hello 數量的資源 （Cpu、 RAM、 磁碟儲存體） 您需要 toorun Azure Service Fabric 應用程式。 通常會為您的資源需求 toochange 經過一段時間。 開發/測試您的服務時通常需要少數資源，之後進入生產環境且您的應用程式受歡迎度增長時會需要更多資源。 當您設計您的應用程式時，思考 hello 長期的需求，並做出選擇，並允許您服務 tooscale toomeet 高的客戶需求。

 當您建立 Service Fabric 叢集時，您可以決定 hello 叢集進行的虛擬機器 (Vm) 的類型。 每個 VM 會具有有限的 Cpu （核心和速度）、 網路頻寬、 RAM 和磁碟儲存體 hello 形式的資源。 隨著您的服務增加一段時間，您可以升級 tooVMs 提供更高的資源和/或新增更多 Vm tooyour 叢集。 toodo hello 後者，您必須設計架構，您的服務一開始讓其能夠運用以動態方式加入 toohello 叢集的新 Vm。

部分服務管理 hello Vm 本身很少 toono 資料。 因此，這些服務應該主要著重在效能，這表示選取 hello 規劃容量適當 hello Vm 的 Cpu （核心和速度）。 此外，您應該考慮網路頻寬，包括發生網路傳輸的頻率特別以及要傳送的資料量。 如果您的服務需要 tooperform 以及服務使用量增加，您可以新增多個 Vm toohello 叢集及所有 hello Vm 之間進行負載平衡 hello 網路要求。

管理大量資料 hello Vm 上的服務，容量規劃應該主要著重在大小。 因此，您應該仔細考量 hello hello VM 的 RAM 和磁碟儲存體容量。 在 Windows 中的 hello 虛擬記憶體管理系統可讓 RAM tooapplication 程式碼看起來的磁碟空間。 此外，hello Service Fabric 執行階段提供 「 智慧型分頁處理，讓只有熱資料保留在記憶體和移動 hello 冷資料 toodisk。 因此，應用程式可以使用更多記憶體超出實際可用 hello VM 上。 需要更多 RAM 只會提高效能，因為 hello VM 可保留在 RAM 中的多個磁碟儲存體。 hello 您選取的 VM 應該 hello VM 您想要的磁碟夠大 toostore hello 資料。 同樣地，hello VM 應該有足夠的 RAM tooprovide 您與 hello 您想要的效能。 如果您的服務資料隨著時間而定，您可以加入更多 Vm toohello 叢集和磁碟分割 hello 資料跨所有 hello Vm。

## <a name="determine-how-many-nodes-you-need"></a>決定您需要多少個節點
資料分割您的服務可讓您 tooscale 出您的服務資料。 如需有關分割的詳細資訊，請參閱 [分割 Service Fabric](service-fabric-concepts-partitioning.md)。 必須將每個資料分割納入單一 VM，但是可以將多個 (小型) 資料分割放在單一 VM 上。 因此，如果有比較多的小型資料分割，比起有比較少的大型資料分割，可提供您更大的彈性。 hello 代價是，有很多分割區增加 Service Fabric 負擔，而且您無法跨磁碟分割執行的交易的作業數。 如果您的服務程式碼經常需要 tooaccess 存在於不同的資料分割的資料片段，也會產生更多潛在的網路流量。 在設計您的服務時，您應該仔細考量這些優缺點的 tooarrive 在有效的資料分割策略。

例如，假設您的應用程式已有您在一年中預期 toogrow tooDB_Size GB 的存放區大小的單一可設定狀態服務。 您在多個應用程式 （和資料分割） 成是願意 tooadd 遇到超出該年度的成長。  hello 複寫因數 (RF)，決定服務影響 hello 總 DB_Size hello 複本數目。 在所有複本上的總 DB_Size 為 hello 複寫因數乘以 DB_Size hello。  Node_Size 代表 hello 磁碟空間/RAM 每個節點要 toouse 為您的服務。 為了達到最佳效能，hello DB_Size 應該跨 hello 叢集與周圍的 hello 應該選擇 VM 的 RAM hello Node_Size 放入記憶體中。 藉由配置大於 hello RAM 容量 Node_Size，您依賴在 hello Service Fabric 執行階段所提供的 hello 分頁。 因此，您可能無法達到最佳效能如果整個資料被視為 toobe 熱 （從然後 hello 資料分頁/out)。 不過，對於許多服務，其中只有一小部份 hello 資料是作用，它是更符合成本效益。

節點所需的最大效能的 hello 數目的計算方式，如下所示：

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>考慮成長
您可能想要的節點 toocompute hello 數目根據 hello DB_Size 此外如預期，您服務 toogrow toohello DB_Size 您開始使用。 然後，成長 hello 節點數目，您的服務成長時，讓您要不過度佈建 hello 節點數目。 但是資料分割的 hello 數目應該依據 hello 當您執行您的服務在最大成長時所需的節點數目。

它是好 toohave 一些額外的電腦可用在任何時間，如此可以處理任何非預期的尖峰或失敗 （例如，如果一些 Vm 都當機）。  使用您預期的尖峰，應該判斷 hello 額外容量，而的起始點是 tooreserve 幾個額外的 Vm (5-10%額外)。

hello 上述假設單一的可設定狀態服務。 如果您有多個可設定狀態服務，您會有 tooadd hello 與相關聯的 DB_Size hello hello 方程式到其他服務。 或者，您可以計算 hello 分別為每個可設定狀態服務的節點數目。  您的服務的複本或資料分割可能不平衡。 請記住，有些資料分割的資料可能比其他資料分割還多。 如需有關分割的詳細資訊，請參閱 [最佳作法的分割文章](service-fabric-concepts-partitioning.md)。 不過，hello 上述公式是資料分割和複本無關，因為 Service Fabric 可確保，hello 複本會散佈在 hello 節點之間以最佳方式。

## <a name="use-a-spreadsheet-for-cost-calculation"></a>使用試算表進行成本計算
現在讓我們將某些實際數字放在 hello 公式。 [範例試算表](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx)示範如何 tooplan hello 的應用程式包含三種類型的資料物件的容量。 針對每個物件，我們的近似大小，我們預期 toohave 的物件數目。 我們也選取對每個物件類型我們想要的複本數。 hello 試算表計算記憶體 toobe hello 叢集中儲存的 hello 總數。

然後，我們輸入 VM 大小和每月成本。 根據 hello VM 大小，hello 試算表會告知 hello 您必須使用符合資料 toophysically toosplit hello 節點的資料分割的最小數目。 您可能想要更大量的資料分割 tooaccommodate 需要您的應用程式特定的計算和網路流量。 hello 試算表會顯示 hello 管理 hello 使用者設定檔物件的資料分割數目已從一個 toosix 增加。

現在，根據這項資訊，hello 試算表會顯示您實際上可以取得所有 hello 資料與預期的 hello 資料分割和複本 26 雙節點叢集上。 不過，此叢集會是緊密壓縮的因此您可能需要一些額外的節點 tooaccommodate 節點失敗和升級。 hello 試算表也會顯示，具有多個 57 節點提供任何其他值，因為您會有空白節點。 同樣地，您可能想 toogo 57 節點上方還是 tooaccommodate 節點失敗和升級。 您可以調整 hello 試算表 toomatch 應用程式的特定需求。   

![成本計算的試算表][Image1]

## <a name="next-steps"></a>後續步驟
簽出[分割 Service Fabric 服務][ 10] toolearn 深入了解您的服務資料分割。

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
