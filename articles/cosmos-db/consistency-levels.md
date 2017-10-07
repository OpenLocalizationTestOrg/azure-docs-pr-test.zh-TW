---
title: "在 Azure Cosmos DB aaaConsistency 層級 |Microsoft 文件"
description: "Azure Cosmos DB 有五個一致性層級 toohelp 平衡最終一致性、 可用性和延遲取捨。"
keywords: "最終一致性, azure cosmos db, azure, Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Azure Cosmos DB 中的 Tunable 資料一致性層級
Hello 地面與全域發佈記住每個資料模型被設計 azure Cosmos DB。 它是設計的 toooffer 可預測的低延遲保證 99.99%可用性 SLA，並妥善定義的多個放寬一致性模型。 Azure Cosmos DB 目前提供五種一致性層級：強式、限定過期、工作階段、一致的前置和最終。 

除了**強式**和**最終一致性**模型通常是由分散式資料庫所提供，Azure Cosmos DB 還提供其他三個已仔細編碼且可運作的一致性模型，並已根據真實世界的使用案例驗證過它們的實用性。 這些是 hello**繫結失效**，**工作階段**，和**一致的前置詞**一致性層級。 共同這五個一致性層級可讓您 toomake 良好事物之間的利弊得失一致性、 可用性和延遲。 

## <a name="distributed-databases-and-consistency"></a>分散式資料庫和一致性
商業散發資料庫分為兩類：完全不會提供完善且可證明之一致性選擇的資料庫，以及提供兩個極端的可程式性選擇 (強式與最終一致性) 的資料庫。 

hello 先前負擔其中其複寫通訊協定的應用程式開發人員，並預期這些 toomake 難以取捨一致性、 可用性、 延遲和輸送量。 hello，後者會將不足的壓力 toochoose hello 兩個極端的其中一個。 Hello 豐富的研究和 50 個以上的一致性模型的提案，儘管 hello 分散式的資料庫社群不是強式與最終一致性除了能 toocommercialize 一致性層級。 Cosmos DB 可讓開發人員 toochoose 沿著 hello 一致性頻譜 – 強，五個妥善定義的一致性模型之間的繫結失效，[工作階段](http://dl.acm.org/citation.cfm?id=383631)，一致的前置詞，以及最終。 

![Azure Cosmos 資料庫提供了多個正確定義 （寬鬆的方式） 的一致性模型 toochoose 從](./media/consistency-levels/five-consistency-levels.png)

hello 下表說明每個一致性層級提供的 hello 特定保證。
 
**一致性層級和保證**

| 一致性層級 | 保證 |
| --- | --- |
| 強式 | 線性化能力 |
| 限定過期 | 一致前置詞。 讀取落後寫入 (k 前置詞或 t 間隔) |
| 工作階段   | 一致前置詞。 單純讀取、單純寫入、讀取您的寫入、讀取後接寫入 |
| 一致前置詞 | 傳回的更新是某些前置詞的所有 hello 更新，不可有間隔 |
| 最終  | 次序錯誤讀取 |

您可以 Cosmos DB 帳戶上設定 hello 預設一致性層級 （和更新版本覆寫在特定的讀取要求的 hello 一致性）。 就內部而言，hello 預設一致性層級套用 toodata hello 資料分割集可能會跨越區域內。 大約 73% 的租用戶使用工作階段一致性，而 20% 的租用戶則偏好限定過期。 我們發現，大約有 3% 的客戶在一開始試驗不同的一致性層級，然後才決定應用程式的特定一致性選擇。 我們也發現只有 2% 的租用戶在個別要求基礎上覆寫一致性層級。 

在 Cosmos DB 中，在工作階段、一致前置詞和最終一致性提供服務的讀取，比起使用強式或限定過期一致性的讀取，其成本便宜兩倍。 Cosmos DB 有領先業界的完整 99.99% SLA，包括一致性保證以及可用性、輸送量和延遲。 我們採用[linearizability 檢查](http://dl.acm.org/citation.cfm?id=1806634)，其中我們服務遙測上持續運作，並公開報告任何一致性違規 tooyou。 針對繫結失效，我們監視以及報表所需的任何違規，t 界限。 所有五個的鬆散的一致性層級，我們也會報告 hello[機率的繫結的失效度量](http://dl.acm.org/citation.cfm?id=2212359)直接 tooyou。  

## <a name="scope-of-consistency"></a>一致性的範圍
hello 資料粒度是一致性的已設定領域的 tooa 單一使用者要求。 寫入的要求可能對應 tooan 插入、 取代、 更新插入，或刪除交易。 如同寫入、 讀取/查詢交易也是已設定領域的 tooa 單一使用者要求。 hello 使用者可能需要的 toopaginate 透過大型結果集、 跨越多個資料分割，但每個讀取的交易範圍的 tooa 單一頁面，並由單一資料分割內。

## <a name="consistency-levels"></a>一致性層級
您可以設定在您套用 tooall 集合 （和資料庫） 的資料庫帳戶的預設一致性層級 Cosmos DB 帳戶下。 根據預設，所有的讀取和針對 hello 發出查詢使用者定義的資源使用 hello 資料庫帳戶上指定的 hello 預設一致性層級。 您可能會放寬 hello 一致性層級的特定讀取/查詢要求中每個 hello 使用支援的 Api。 有五種類型的一致性層級 hello Azure Cosmos DB 複寫通訊協定所支援，提供清楚的取捨專屬一致性保證和效能，如本節所述。

**重要事項**： 

* 提供強式一致性[linearizability](https://aphyr.com/posts/313-strong-consistency-models)以 hello 保證讀取保證的 tooreturn hello 最新版本的項目。 
* 強式一致性可確保它由複本的 hello 多數仲裁內容經過永久認可之後才看得到寫入。 寫入時是以同步方式內容經過永久認可 hello 主要和次要資料庫，hello 仲裁或中止。 讀取永遠都會認可由 hello 多數讀取仲裁，用戶端可以永遠不會看到未認可或部分的寫入，而且一律保證 tooread hello 最新認可的寫入。 
* Azure 會設定的 toouse 強式一致性的 Cosmos DB 帳戶無法建立與 Azure Cosmos DB 帳戶關聯多個 Azure 區域。 
* hello 讀取作業的成本 (的[要求單位](request-units.md)耗用) 具有強式一致性高於工作階段且最終的但是相同 hello 做為繫結失效。

**限定過期**： 

* 已繫結的過期一致性可確保，hello 讀取可能會落後寫入最多*K*版本或前置詞的項目或*t*時間間隔。 
* 因此，當選擇繫結失效，hello 「 過時 」 可以設定兩種方式： 版本的數字*K* hello 項目，藉以 hello 讀取落後輸入 hello 寫入，hello 時間間隔的*t* 
* 繫結失效優惠全域訂單總數以外內 hello 「 過時視窗 」。 hello 單調函式讀取保證存在區內內部和外部 hello 「 過時視窗 」。 
* 限定過期可提供比工作階段或最終一致性還要強大的一致性保證。 對於全域散發的應用程式，我們建議您用於當您會想 toohave 強式一致性，但也會想 99.99%可用性和低延遲案例已繫結的失效。 
* 使用限定過期一致性設定的 Azure Cosmos DB 帳戶可以將任意數目的 Azure 區域關聯至它們的 Azure Cosmos DB 區域。 
* hello （依據耗用 RUs) 讀取作業的成本與繫結的失效高於工作階段和最終一致性，但為強式一致性 hello 相同。

**工作階段**： 

* 不像 hello 全域一致性模型提供強式和已繫結失效的一致性層級，工作階段一致性是已設定領域的 tooa 用戶端工作階段。 
* 工作階段一致性適用於所有牽涉到裝置或使用者工作階段的案例，因為它保證單純讀取、單純寫入和讀取您自己的寫入 (RYW) 保證。 
* 工作階段一致性工作階段，提供可預測的一致性和最大讀取輸送量時 hello 最低延遲寫入與讀取供應項目。 
* 使用工作階段一致性設定的 Azure Cosmos DB 帳戶可以將任意數目的 Azure 區域關聯至它們的 Azure Cosmos DB 區域。 
* hello 與工作階段一致性層級是小於強式和已繫結失效，但多個最終一致性的讀取作業 （依據耗用 RUs) 的成本

<a id="consistent-prefix"></a>
**一致前置詞**： 

* 一致的前置詞可保證，沒有任何其他寫入的情況下，hello 群組中的 hello 複本最後聚合。 
* 一致前置詞保證讀取永遠不會看到沒有順序的寫入。 如果寫入執行 hello 順序的`A, B, C`，則用戶端會看到  `A`， `A,B`，或`A,B,C`，但永遠不會失序像`A,C`或`B,A,C`。
* 使用一致前置詞一致性設定的 Azure Cosmos DB 帳戶可以將任意數目的 Azure 區域關聯至它們的 Azure Cosmos DB 區域。 

**最終**： 

* 最終一致性可確保，在沒有任何其他寫入的情況下，hello 群組中的 hello 複本最後聚合。 
* 最終一致性是 hello 一致性最弱形式，其中用戶端可能會收到 hello 值早於它之前看過的 hello 的。
* 最終一致性提供 hello 最薄弱的讀取一致性，但提供的讀取和寫入 hello 最低延遲。
* 使用最終一致性設定的 Azure Cosmos DB 帳戶可以將任意數目的 Azure 區域關聯至它們的 Azure Cosmos DB 區域。 
* hello （依據耗用 RUs) 讀取作業的成本與 hello 最終一致性層級為所有 hello Azure Cosmos DB 一致性層級的最低的 hello。

## <a name="configuring-hello-default-consistency-level"></a>設定 hello 預設一致性層級
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，在 hello Jumpbar 中按一下**Azure Cosmos DB**。
2. 在 hello **Azure Cosmos DB**刀鋒視窗中，選取 hello 資料庫帳戶 toomodify。
3. 在 hello 帳戶刀鋒視窗中，按一下 **預設一致性**。
4. 在 hello**預設一致性**刀鋒視窗中，選取 hello 新一致性層級，然後按一下 **儲存**。
   
    ![Hello 設定圖示和預設一致性項目反白顯示的螢幕擷取畫面](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>查詢的一致性層級
根據預設，使用者定義的資源，hello 一致性層級為查詢 hello 相同 hello 一致性層級的讀取。 根據預設，hello 索引會以同步方式在每個插入、 取代或刪除的項目 toohello Cosmos DB 容器上更新。 這樣做可讓 hello 查詢 toohonor hello 相同一致性層級的點讀取。 雖然 Azure Cosmos DB 有防寫最佳化，並支援持續性磁碟區的寫入同步索引維護，提供一致的查詢，您可以設定特定集合 tooupdate 其索引延遲的方式。 延遲索引進一步提升 hello 寫入效能，而且適用於大量擷取案例主要是大量讀取工作負載時。  

| 索引模式 | 讀取 | 查詢 |
| --- | --- | --- |
| 一致 (預設) |從強式、限定過期、工作階段、一致前置詞或最終等選項中選取 |從強式、限定過期、工作階段或最終等選項中選取 |
| 緩慢 |從強式、限定過期、工作階段、一致前置詞或最終等選項中選取 |最終 |
| None |從強式、限定過期、工作階段、一致前置詞或最終等選項中選取 |不適用 |

做為與讀取的要求，您可以降低特定的查詢要求每個應用程式開發介面中的 hello 一致性層級。

## <a name="next-steps"></a>後續步驟
如果您想要 toodo 更需一致性層級和權衡取捨完全讀取，我們建議 hello 下列資源：

* Doug Terry。 透過棒球來解說複寫的資料一致性 (影片)。   
  [https://www.youtube.com/watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Doug Terry。 透過棒球來解說複寫的資料一致性。   
  [http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Doug Terry。 弱式一致複寫資料的工作階段保證。   
  [http://dl.acm.org/citation.cfm?id=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi。 在現代的分散式資料庫系統設計一致性權衡取捨完全： CAP 只是一部分的 hello 劇本 」。   
  [http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis、Shivaram Venkataraman、Michael J. Franklin、Joseph M. Hellerstein、Ion Stoica。 實際部分仲裁的機率界限-陳舊 (PBS)。   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels。 再論最終一致。    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.html](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* Moni Naor、 Avishai 毛、 hello 負載、 容量和可用性的仲裁系統中，運算、 v.27 n.2、 p.423 447，年 4 月 1998 SIAM 日誌。
  [http://epubs.siam.org/doi/abs/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt、 Chris Dern、 Macanal Musuvathi，伊 Tan、 將： 完整且自動 linearizability 棋子，程式設計語言設計與實作中，年 6 月 05-10，2010，多倫多適用當地法律，hello 2010 ACM SIGPLAN 會議的訴訟加拿大 [doi > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peter Bailis、 Shivaram 卡塔拉曼、 Michael J.林、 約瑟夫 M.Hellerstein Ionic Stoica 都可能繫結失效的實用部分仲裁、 hello VLDB Endowment，v.5 n.8、 p.776 787，2012 年 4 月的訴訟[http://dl.acm.org/citation.cfm?id=2212359](http://dl.acm.org/citation.cfm?id=2212359)
