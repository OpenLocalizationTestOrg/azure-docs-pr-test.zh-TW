---
title: "全域與 Azure Cosmos DB aaaDistribute 資料 |Microsoft 文件"
description: "了解如何從 Azure Cosmos DB (全域散發的多模型資料庫服務)，使用全域資料庫進行全球規模的異地複寫、容錯移轉及資料復原。"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>如何與 Azure Cosmos DB 全域 toodistribute 資料
Azure 無所不在 - 跨 30 多個地理區域，遍佈全球並持續擴充中。 其全球存在，請使用 Azure 提供 tooits 開發人員的 hello 區分的功能的其中一個是 hello 能力 toobuild、 部署和管理全域散發的應用程式輕鬆地。 

[Azure Cosmos DB](../cosmos-db/introduction.md) 是 Microsoft 全域發佈的多模型資料庫服務，適用於任務關鍵性應用程式。 Azure 的 Cosmos DB 會提供周全的全域發佈[彈性調整的輸送量與儲存體](../cosmos-db/partition-data.md)hello 99th 百分位數 在全球、 單一位數毫秒延遲[五個妥善定義的一致性層級](consistency-levels.md)，而保證其高可用性，所有支援[領先業界的 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)。 Azure Cosmos DB[自動索引資料](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)而不需要使用結構描述與索引管理 toodeal。 它是多重模型，可支援文件、索引鍵/值、圖表和單欄式資料模型。 為雲端產生的服務，Azure Cosmos DB 仔細被工程與多租用戶和全域發佈從 hello 接地。

**分割並散發在多個 Azure 區域的單一 Azure Cosmos DB 集合**

![分割並散發在三個區域的 Azure Cosmos DB 集合](./media/distribute-data-globally/global-apps.png)

如我們在建置 Azure Cosmos DB 時所知，當務之急是新增全域散發功能，而不能只將它放在「單一網站」資料庫系統上。 所提供的全域散發資料庫的 hello 能力延伸到其他的傳統地理災害復原 (GEO-DR)，提供 「 單一站台 」 資料庫。 提供 Geo-DR 功能的單一網站資料庫是分散在世界各地的資料庫嚴格子集。 

使用 Azure Cosmos DB 的通行全域發佈，開發人員就不需要 toobuild 自己複寫 scaffolding 採用任一 hello Lambda 模式 (例如， [AWS DynamoDB 複寫](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) 透過 hello 資料庫記錄檔或跨多個區域進行"double 寫入 」。 我們不建議這種方法，因為它是不可能 tooensure 正確性的這類方法，並提供聲音的 Sla。 

在本文中，我們提供 Azure Cosmos DB 的全域散發功能概觀。 我們也會說明 Azure Cosmos DB 的唯一方法 tooproviding 完整的 Sla。 

## <a id="EnableGlobalDistribution"></a>啟用周全的全域散發
Azure 的 Cosmos DB 會提供 hello 下列功能 tooenable 您 tooeasily 寫入地球調整應用程式。 這些功能可透過 hello Azure Cosmos DB 的資源提供者架構[REST Api](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)以及 hello Azure 入口網站。

### <a id="RegionalPresence"></a>遍及各區，無所不在 
Azure 透過不斷連上[新的地理區域](https://azure.microsoft.com/regions/)，而日益普及。 根據預設，新的 Azure 區域全部都可使用 Azure Cosmos DB。 這可讓您 tooassociate 包含您的 Azure Cosmos DB 資料庫帳戶的地理區域儘速 Azure 開啟 hello 商務新的區域。

**新的 Azure 區域預設全部都可使用 Azure Cosmos DB**

![新的 Azure 區域全部都可使用 Azure Cosmos DB](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>將數目不拘的區域與您的 Azure Cosmos DB 資料庫帳戶產生關聯
Azure Cosmos DB 可讓您 tooassociate 任意數目的 Azure 區域，以您的 Azure Cosmos DB 資料庫帳戶。 地理圍欄限制，例如中國 （德國） 之外有 hello 可以與您的 Azure Cosmos DB 資料庫帳戶相關聯的區域數目沒有限制。 hello 遵循圖會顯示資料庫帳戶設定 toospan 跨 25 的 Azure 區域。  

**橫跨 25 個 Azure 區域的租用戶 Azure Cosmos DB 資料庫帳戶**

![橫跨 25 個 Azure 區域的 Azure Cosmos DB 資料庫帳戶](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>原則式異地隔離限制
Azure 的 Cosmos DB 是設計的 toohave 以原則為基礎的地理範圍功能。 異地隔離是重要的元件 tooensure 資料監管和法務遵循限制，而且可能會造成將特定區域與您的帳戶產生關聯。 地理圍欄的範例包括 （但不限於），設定全域發佈 toohello 區域 （例如，中國及德國） 統領雲端內或政府課稅界限 （例如澳大利亞） 內的範圍。 hello 原則會控制使用您的 Azure 訂閱 hello 中繼資料。

### <a id="DynamicallyAddRegions"></a>動態新增和移除區域
Azure Cosmos DB 可讓您 tooadd （關聯） 或移除 （中斷） 區域 tooyour 資料庫帳戶 」，在任何時間點 (請參閱[上圖中](#UnlimitedRegionsPerAccount))。 透過平行的資料分割之間複寫資料，Azure Cosmos DB 可確保新的區域線上時，Azure Cosmos DB 可用 30 分鐘內任何位置中的總 too100 TBs 的 hello world。 

### <a id="FailoverPriorities"></a>容錯移轉優先順序
地區容錯移轉時的多地區中斷 Azure Cosmos DB 的 toocontrol 順序可讓您與 hello 資料庫帳戶相關聯的 tooassociate hello 優先順序 toovarious 區域 （請參閱下列圖 hello）。 Azure Cosmos DB 可確保 hello 自動容錯移轉順序，會發生您所指定的 hello 優先權順序。 如需有關區域性容錯移轉的詳細資訊，請參閱 [Azure Cosmos DB 中商務持續性的自動區域容錯移轉](regional-failover.md)。

**Azure Cosmos DB 的租用戶可以為資料庫帳戶相關聯的區域設定 hello 容錯移轉優先順序 （右窗格）**

![使用 Azure Cosmos DB 設定容錯移轉優先順序](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>讓區域動態「離線」
Azure Cosmos DB 可讓您 tootake 資料庫帳戶的特定區域中的 離線，並將其恢復上線之後。 標示為離線的區域不主動參與複寫，而且不 hello 容錯移轉順序的一部分。 這可讓您上次已知良好的資料庫映像中的 hello 其中一個推出具有潛在風險升級 tooyour 應用程式之前，請閱讀區域 toofreeze hello。

### <a id="ConsistencyLevels"></a>多個定義完善的一致性模型可供全球複寫資料庫使用
Azure Cosmos DB 會公開由 SLA 所支援的[多個定義完善的一致性層級](consistency-levels.md)。 您可以選擇根據 hello 工作負載情況下 （從 hello 可用選項的清單），將特定的一致性模型。 

### <a id="TunableConsistency"></a>可微調全球複寫資料庫不一致之處
Azure 的 Cosmos DB 可讓您 tooprogrammatically 覆寫，並且放寬 hello 預設一致性選擇針對每個要求，在執行階段。 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>可動態設定讀取和寫入區域
Azure Cosmos DB 可讓您 tooconfigure hello 區域 （hello 資料庫相關聯） 的 「 讀取 」、 「 寫入 」 或 「 讀取/寫入 」 區域。 

### <a id="ElasticallyScaleThroughput"></a>在 Azure 區域，來彈性調整的輸送量
您能以程式設計方式佈建輸送量，彈性地調整 Azure Cosmos DB 集合。 hello 輸送量為 hello 集合發佈於套用的 tooall hello 區域。

### <a id="GeoLocalReadsAndWrites"></a>異地本機讀取和寫入
hello 的全域散發資料庫的主要優點是 toooffer 低延遲存取 toohello 資料 hello 世界各地。 Azure Cosmos DB 可在 P99 進行各種資料庫作業時提供低延遲保證。 它可確保所有的讀取路由的 toohello 最接近本機讀取的區域。 則使用 tooserve 讀取要求，發出讀取 hello hello 仲裁本機 toohello 區域。hello 一樣 toohello 寫入。 只在複本的大部分內容經過永久認可 hello 寫入本機但不會在閘道上遠端複本 tooacknowledge hello 寫入之後，都會認可寫入。 將以不同的方式，Azure Cosmos DB hello 複寫通訊協定下的運作方式 hello 假設 hello 讀取及寫入仲裁永遠是本機 toohello 讀取和寫入區域，分別發出哪些 hello 要求。

### <a id="ManualFailover"></a>手動起始區域的容錯移轉
Azure Cosmos DB 可讓您 tootrigger hello 容錯移轉的 hello 資料庫帳戶 toovalidate hello*結束 tooend*可用性的 hello 整個應用程式 （除了 hello 資料庫） 的屬性。 因為同時 hello 安全且保證 hello 失敗偵測和領導者選擇 liveness 屬性，可保證 Azure Cosmos DB*零資料遺失*租用戶起始手動容錯移轉作業。

### <a id="AutomaticFailover"></a>自動容錯移轉
Azure Cosmos DB 支援在發生一或多個區域中斷時自動容錯移轉。 進行區域容錯移轉時，Azure Cosmos DB 會維持其讀取延遲、執行時間可用性、一致性及輸送量 SLA。 Azure Cosmos 資料庫提供自動容錯移轉作業 toocomplete hello 持續時間上限。 這是可能遺失資料的 hello 視窗在 hello 地區中斷。

### <a id="GranularFailover"></a>專為不同的容錯移轉資料粒度設計
目前 hello 自動和手動容錯移轉功能所公開的 hello 資料庫帳戶的 hello 資料粒度。 請注意，在內部 Azure Cosmos DB 會設計的 toooffer*自動*精細的資料庫、 集合或甚至的分割區 （擁有索引鍵範圍的集合） 的容錯移轉。 

### <a id="MultiHomingAPIs"></a>Azure Cosmos DB 中的多路連接 API
Azure Cosmos DB 可讓您 toointeract hello 資料庫使用與邏輯 （區域無從驗證） 或實體 （特定地區） 端點。 使用邏輯端點，可確保的 hello 應用程式以透明的方式可以多重主目錄，如果發生容錯移轉。 hello 後者、 實體端點，請提供更細微的控制 toohello 應用程式 tooredirect 讀取和寫入 toospecific 區域。

您可以找到有關 tooconfigure 讀取 hello 的喜好設定的方式[DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md)， [Graph API](../cosmos-db/tutorial-global-distribution-graph.md)，[表格 API](../cosmos-db/tutorial-global-distribution-table.md)，和[MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)中其各自連結文件。

### <a id="TransparentSchemaMigration"></a>透明且一致的資料庫結構描述與索引移轉 
Azure Cosmos DB 完全[無從驗證結構描述 (英文)](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)。 hello 其資料庫引擎的獨特的設計允許 tooautomatically，並以同步方式將它內嵌而不需要任何結構描述或從您的次要索引的 hello 資料的所有索引。 這可讓您 tooiterate 全域分散式的應用程式快速而不需要擔心資料庫結構描述與索引移轉或協調多階段的應用程式首度發行的結構描述變更。 Azure Cosmos DB 保證明確您所做的任何變更 tooindexing 原則不會造成的效能或可用性降低到。  

### <a id="ComprehensiveSLAs"></a>全方位 SLA (不光只有高可用性)
為全域分散式的資料庫服務，Azure Cosmos DB 會提供妥善定義的 SLA**資料遺失**，**可用性**，**延遲 P99**，**輸送量**和**一致性**hello 資料庫整體，無論 hello 與 hello 資料庫相關聯的區域數目。  

## <a id="LatencyGuarantees"></a>延遲保證
hello 像 Azure Cosmos DB 全域分散式的資料庫服務的主要優點是 toooffer 低延遲存取 tooyour 資料 hello 世界各地。 Azure Cosmos DB 可在 P99 進行各種資料庫作業時保證低延遲。 藉由運用 Azure Cosmos DB hello 複寫通訊協定可確保該 hello 資料庫作業 （理想情況下，讀取和寫入） hello 區域本機 toothat hello 用戶端一律會執行。 Azure Cosmos DB SLA 包含如 P99 hello 延遲讀取、 寫入 （同步） 索引和查詢不同要求和回應的大小。 寫入的 hello 延遲保證包括永久性多數仲裁認可 hello 本機資料中心內。

### <a id="LatencyAndConsistency"></a>延遲和一致性的關聯性 
全域分散式的服務 toooffer 強式一致性全域散發的安裝程式中，它需要 toosynchronously 複寫 hello 寫入同步或非同步執行跨地區讀取 – 淺色與 hello 廣域網路網路可靠性聽寫 hello 速度高延遲及低的可用性資料庫作業產生的強式一致性。 因此，順序 toooffer 保證在 P99 和 99.99 可用性的低延遲，在 hello 服務必須採用非同步複寫。 這會需要 hello 服務必須也提供[妥善定義、 鬆散一致性 choice(s)](consistency-levels.md) – 低於強式 （toooffer 低延遲和可用性保證） 和 「 最終 」 一致性 （較理想的情況下toooffer 直覺式的程式設計模型)。

Azure Cosmos DB 可確保讀取的作業不需要的 toocontact 複本跨多個區域 toodeliver hello 特定的一致性層級保證。 同樣地，它可確保，在寫入作業不會無法取得封鎖並同時 hello 資料已複寫到所有的 hello 區域 （也就是寫入會以非同步方式跨區域複寫）。 對於多重區域資料庫帳戶，可以提供多個寬鬆的一致性層級。 

### <a id="LatencyAndAvailability"></a>延遲和可用性的關聯性 
延遲和可用性是兩端 hello hello 相同的參考。 我們會討論在穩定狀態和可用性，hello 字體的失敗中的 hello 作業的延遲。 Hello 應用程式的觀點而言，很慢的執行資料庫作業會區別資料庫無法使用。 

從無法使用，Azure Cosmos DB toodistinguish 高延遲提供各種資料庫作業的延遲時間絕對上限。 如果超過 hello 上限 toocomplete hello 資料庫作業，Azure Cosmos DB 傳回逾時錯誤。 hello Azure Cosmos DB 可用性 SLA 可確保該 hello 逾時依據 hello 可用性 SLA 計算。 

### <a id="LatencyAndThroughput"></a>延遲和輸送量的關聯性
Azure Cosmos DB 不會要您在延遲和輸送量之間做出選擇。 它接受兩個延遲 P99 hello SLA，並傳遞您所佈建 hello 輸送量。 

## <a id="ConsistencyGuarantees"></a>一致性保證
Hello 時[強式一致性模型](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)hello 金級標準的可程式性，它也是高延遲時間 （處於穩定狀態） 的 hello 並不容易學習價格與可用性 （在 hello 朝的失敗）。 

Azure Cosmos 資料庫提供了完善的程式設計模型 tooyou tooreason 有關複寫的資料一致性。 在排序 tooenable 您 toobuild 多重主目錄應用程式，Azure Cosmos DB 所公開的 hello 一致性模型與設計的 toobe 地區無關，而不要依賴 hello 區域從提供 hello 讀取和寫入。 

Azure Cosmos DB 的一致性 SLA 會保證 100%的讀取要求將會符合 hello 一致性保證 hello 一致性層級 （hello 預設一致性層級上 hello 資料庫帳戶，或是覆寫的 hello 值 hello 要求您的要求). 如果已滿足所有 hello 一致性保證 hello 一致性層級相關聯，讀取的要求被視為符合 toohave hello 一致性 SLA。 hello 表擷取 hello 對應 toospecific Azure Cosmos DB 所提供的一致性層級的一致性保證。

**和 Azure Cosmos DB 中所指定一致性層級相關聯的一致性保證**

<table>
    <tr>
        <td><strong>一致性層級</strong></td>
        <td><strong>一致性特性</strong></td>
        <td><strong>SLA</strong></td>
    </tr>
    <tr>
        <td rowspan="3">工作階段</td>
        <td>讀取自己的寫入</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>單純讀取</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>一致的前置詞</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">界限-陳舊</td>
        <td>單純讀取 (區域內)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>一致的前置詞</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>過期限定 &lt; K、T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>一致的前置詞</td>
        <td>一致的前置詞</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>重要事項</td>
        <td>線性</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>一致性和可用性的關聯性
hello [impossibility 結果](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf)的 hello [CAP 理論](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf)證明，就不能確實 hello 系統 tooremain 可用和優惠 linearizable hello 朝失敗的一致性。 hello 資料庫服務，必須選擇 toobe CP 或 AP-CP 系統放棄可用性改用 linearizable 一致性時放棄 hello AP 系統[linearizable 一致性](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)改用可用性。 Azure Cosmos DB 永遠不會違反 hello 要求一致性層級，正式進行 CP 系統。 不過，實際上一致性不是全部或任何主張 – 有沿著 hello 一致性頻譜之間 linearizable 和最終一致性的多個定義完善的一致性模型。 在 Azure Cosmos DB 中，我們已嘗試 tooidentify 數個 hello 放寬真實世界適用性與直覺式的程式設計模型的一致性模型。 Azure Cosmos DB 巡覽 hello 一致性可用性權衡取捨的供應項目連同 99.99 可用性 SLA[多放寬尚未妥善定義的一致性層級](consistency-levels.md)。 

### <a id="ConsistencyAndAvailability"></a>一致性和延遲的關聯性
Daniel Abadi 教授提出更全面的 CAP 變化稱為 [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf)，也能解釋在穩定狀態下對延遲和一致性的權衡取捨。 它指出在穩定狀態，hello 資料庫系統必須選擇一致性和延遲。 （非同步複寫和本機讀取、 寫入仲裁所支援） 的多個鬆散的一致性模型，與 Azure Cosmos DB 可確保所有讀取和寫入目前本機 toohello 讀取，而分別撰寫區域。  這可讓 Azure Cosmos DB toooffer 低度延遲保證 hello 一致性層級的 hello 區域內。  

### <a id="ConsistencyAndThroughput"></a>一致性和輸送量的關聯性
因為特定的一致性模型的 hello 實作取決於 hello 選擇[仲裁類型](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)，hello 輸送量也取決 hello 所選擇的一致性。 比方說，在 Azure Cosmos DB hello 強式一致性的讀取輸送量是大約一半 toothat 的最終一致性的讀取。 
 
**Azure Cosmos DB 中特定一致性層級之讀取容量的關聯性**

![一致性和輸送量之間的關聯性](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>輸送量保證 
Azure Cosmos DB 可讓您 tooscale 輸送量 （以及，儲存體），彈性地跨越不同地區根據 hello 需求。 

**單一 Azure Cosmos DB 集合經過分割 (跨三個分區)，然後散發在三個 Azure 區域**

![Azure Cosmos DB 已散發並分割集合](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Azure Cosmos DB 集合可使用兩個維度來散發：在區域內，然後跨區域。 方式如下： 

* 在單一區域內，以資源分割區的方式相應放大 Azure Cosmos DB 集合。 藉由在一組複本間複寫狀態機器，每個資源資料分割都會管理一組索引鍵且極為一致並高度可用。 Azure Cosmos DB 是輸送量的完全管理的資源系統負責傳遞的系統資源配置 tooit hello 預算其共用資源分割區所在。 hello 調整 Azure Cosmos DB 集合是完全透明 – Azure Cosmos DB 管理 hello 資源資料分割和分割，並視需要將其合併。 
* 然後 hello 資源分割區的每個會發佈到多個區域。 資源擁有的分割區跨各種區域表單分割集 hello 同一組索引鍵 (請參閱[上圖中](#ThroughputGuarantees))。  資料分割集內的資源分割區是協調 hello 跨多個區域使用狀態機器複寫。 根據 hello 一致性層級設定，資料分割集內的 hello 資源分割區設定成使用不同的拓撲 （例如，星狀、 菊輪鍊、 樹狀目錄等），以動態方式。 

由於高回應性資料分割管理、 負載平衡和嚴格資源控管，Azure Cosmos DB 可讓您 tooelastically 標尺輸送量跨 Azure Cosmos DB 集合上的多個 Azure 區域。 在集合上的變更輸送量就像是使用 Azure Cosmos DB 保證 hello 絕對上限您要求 toochange hello 輸送量的延遲其他資料庫作業的 Azure Cosmos 資料庫-用於執行階段作業。 例如，hello 遵循圖會顯示彈性地佈建輸送量 （範圍從 1 M-10 M 要求數/秒跨兩個區域） 隨 hello 與客戶的集合。
 
**彈性地佈建輸送量的客戶集合 (每秒 1M-10M 個要求)**

![Azure Cosmos DB 可彈性佈建輸送量](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>輸送量和一致性的關聯性 
與[一致性和輸送量的關聯性](#ConsistencyAndThroughput)相同。

### <a id="ThroughputAndAvailability"></a>輸送量和可用性的關聯性
Azure Cosmos DB 時，會繼續 toomaintain 其可用性 hello 變更 toohello 輸送量。 Azure Cosmos DB 以透明的方式管理資料分割 （例如，分割、 合併、 複製作業），並確保該 hello 作業會降低效能或可用性，而 hello 應用程式彈性地增加或減少輸送量。 

## <a id="AvailabilityGuarantees"></a>可用性保證
Azure Cosmos 資料庫提供 99.99%執行時間可用性 SLA hello 的每個資料和控制平面作業。 如先前所述，Azure Cosmos DB 的可用性保證包含每個資料面和控制面作業的延遲絕對上限。 hello 可用性保證 steadfast 而且不會變更具有區域或區域之間的地理距離的 hello 數目。 可用性保證適用於手動以及自動容錯移轉。 Azure Cosmos DB 會提供透明多路連接的 Api，可以確保您的應用程式可以對邏輯的端點，並且可以明確地路由傳送 hello 要求 toohello 新的區域發生容錯移轉。 將以不同的方式，您的應用程式不需要在區域的容錯移轉時重新部署 toobe hello 可用性 Sla 維護及。

### <a id="AvailabilityAndConsistency"></a>可用性和一致性、延遲及輸送量的關聯性
可用性和一致性、延遲及輸送量的關聯性，如[一致性和可用性的關聯性](#ConsistencyAndAvailability)、[延遲和可用性的關聯性](#LatencyAndAvailability)及[輸送量和可用性的關聯性](#ThroughputAndAvailability)中所述。 

## <a id="GuaranteesAgainstDataLoss"></a>「資料遺失」的保證和系統行為
在 Azure Cosmos DB 中，每個分割區 (集合) 都有數個複本散佈在至少 10-20 個容錯網域，藉以提供高可用性。 所有寫入會以同步和永久都認可的複本的多數仲裁之前通知 toohello 用戶端。 協調分散在多個區域的資料分割，需要套用非同步複寫。 Azure Cosmos DB 保證租用戶起始的手動容錯移轉零資料遺失。 自動容錯移轉期間，Azure Cosmos DB 保證 hello 設定上限限定在 hello 資料遺失期間失效間隔做為其 SLA 的一部分。

## <a id="CustomerFacingSLAMetrics"></a>客戶面向 SLA 計量
Azure Cosmos DB 以透明的方式公開 hello 輸送量、 延遲、 一致性和可用性的度量。 這些計量都可存取，以程式設計方式及透過 hello Azure 入口網站 （請參閱下列圖）。 您也可以設定各種使用 Azure Application Insights 的臨界值警示。
 
**一致性、 延遲、 輸送量和可用性的度量資訊會以透明的方式使用 tooeach 租用戶**

![Azure Cosmos DB 客戶可見的 SLA 計量](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>接續步驟
* 在您 Azure Cosmos DB 帳戶使用 tooimplement 全域複寫 hello Azure 入口網站，請參閱[tooperform Azure Cosmos DB 全域資料庫複寫使用 hello Azure 入口網站如何](tutorial-global-distribution-documentdb.md)。
* 有關如何 toolearn tooimplement 多重主要架構，以 Azure Cosmos DB，請參閱[多重主要資料庫架構以 Azure Cosmos DB](multi-region-writers.md)。
* toolearn 深入了解如何自動和手動容錯移轉運作在 Azure Cosmos DB，請參閱[地區容錯移轉，在 Azure Cosmos DB](regional-failover.md)。

## <a id="References"></a>參考
1. Eric Brewer。 [面對健全的分散式系統 (英文)](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf)
2. Eric Brewer。 [CAP 十二年稍後 – hello 規則已變更的方式](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert、Lynch。 - [一致、可用、資料分割容錯 Web 服務的布魯爾推測和可行性](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) (英文)
4. Daniel Abadi。 [現代分散式資料庫系統設計的一致性取捨 (英文)](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf)
5. Martin Kleppmann。 [不要再以 CP 或 AP 來稱呼資料庫 (英文)](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html)
6. Peter Bailis et al。[實際部分仲裁的隨機限定過期 (PBS) (英文)](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
7. Naor 和 Wool。 [仲裁系統的負載、容量及可用性 (英文)](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf)
8. Herlihy 和 Wing。 [線性：並行物件的正確性條件 (英文)](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)
9. [Azure Cosmos DB SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
