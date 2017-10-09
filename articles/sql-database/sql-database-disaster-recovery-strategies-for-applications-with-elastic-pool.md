---
title: "aaaDesign 災害復原解決方案 Azure SQL Database |Microsoft 文件"
description: "深入了解如何 toodesign 選擇 hello 右容錯移轉模式的嚴重損壞修復您的雲端方案。"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>使用 SQL Database 彈性集區之應用程式的災害復原策略
Hello 年來，我們已經學會，雲端服務不容易發生災難事件。 這些事件發生時，SQL Database 會提供數個功能 tooprovide hello 商務持續性的應用程式。 [彈性集區](sql-database-elastic-pool.md)單一資料庫支援 hello 和相同類型的災害復原功能。 本文說明利用這些 SQL Database 商務持續性功能之彈性集區的數種 DR 策略。

這篇文章會使用下列標準 SaaS ISV 應用程式模式中的 hello:

<i>現代化雲端架構 web 應用程式佈建一個 SQL database 每位使用者。hello ISV 中有許多客戶，因此會使用許多資料庫，也就是租用戶資料庫的資料庫。因為 hello 租用戶資料庫通常會有無法預期的活動模式、 hello ISV 使用彈性集區 toomake hello 資料庫成本非常可預測一段很長的時間。當 hello 使用者活動升高 hello 彈性集區也可以簡化 hello 效能管理。此外 toohello 租用戶資料庫 hello 應用程式也會使用多個資料庫 toomanage 使用者設定檔安全性、 收集使用量模式等等。Hello 個別租用戶的可用性不會影響整體 hello 應用程式的可用性。不過，hello 管理資料庫的可用性與效能至關重要 hello 應用程式的函式，而如果 hello 管理資料庫會離線 hello 整個應用程式已離線。</i>  

這篇文章討論涵蓋範圍的案例，從成本機密啟動應用程式 tooones 具有嚴格的可用性需求的 DR 策略。

## <a name="scenario-1-cost-sensitive-startup"></a>案例 1. 成本導向創業
<i>我想要創業，而且成本極為有限。我想 toosimplify 部署及管理的 hello 應用程式，而且可以個別客戶有有限的 SLA。但是，我想 tooensure hello 應用程式，因為整個絕不會是離線。</i>

toosatisfy hello 簡化需求，將所有租用戶資料庫部署到 hello 您選擇的 Azure 區域中的一個彈性集區，並部署管理資料庫進行地理複寫單一資料庫。 租用戶的 hello 災害復原，使用 「 地理還原，會出現在無需額外成本。 tooensure hello 可用性 hello 管理資料庫，地理複寫它們 tooanother 區域，使用自動容錯移轉群組 （在預覽） （步驟 1）。 在此案例中的 hello 災害復原設定 hello 持續成本為等於 toohello hello 的次要資料庫的總成本。 在 hello 下圖說明此組態。

![圖 1](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

如果發生中斷 hello 主要區域中，hello 復原步驟 toobring hello 下圖說明您的應用程式上線。

* hello 容錯移轉群組會起始自動容錯移轉的 hello 管理資料庫 toohello DR 區域。 hello 應用程式會自動重新連線的 toohello 新的主要和所有新帳戶和租用戶資料庫建立 hello DR 區域中。 hello 現有客戶會看到其資料暫時無法使用。
* 建立 hello 彈性集區以 hello hello 原始集區 (2) 相同的組態。
* 使用地理還原 toocreate 份 hello 租用戶資料庫 (3)。 您可以考慮觸發 hello 個別還原 hello 使用者連接，或使用某些其他應用程式特定優先順序的架構。


此時您的應用程式上線在 hello DR 區域中，但有些客戶存取其資料時，遇到延遲。

![圖 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

如果暫存 hello 中斷，很可能該 hello 主要地區會復原 Azure 之前 hello DR 區域中所有的 hello 資料庫還原已完成。 在此情況下，協調移動 hello 應用程式後 toohello 主要區域。 hello 程序需要 hello hello 下一個圖表上所述的步驟。

* 取消所有未處理的異地還原要求。   
* 容錯移轉 hello 管理資料庫 toohello 主要區域 (5)。 Hello 區域復原後，hello 舊主要複本會自動成為次要資料庫。 現在，它們會再次切換角色。 
* 變更 hello 應用程式的連接字串 toopoint 後 toohello 主要區域。 現在所有新帳戶和租用戶資料庫建立 hello 主要區域中。 部分現有客戶會發現其資料暫時無法使用。   
* 在 hello DR 集區僅 tooread tooensure hello DR 區域 (6) 中無法修改這些設定的所有資料庫。 
* Hello hello 復原之後已經變更的 DR 集區中每個資料庫，重新命名或刪除 hello hello 主要集區 (7) 中對應的資料庫。 
* 複製 hello 更新 hello DR 集區 toohello 主要集區 (8) 的資料庫。 
* 刪除 hello DR 集區 (9)

此時您的應用程式中所有租用戶資料庫可用 hello 主要集區中的 hello 主要區域為線上。

![圖 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

hello 金鑰**獲益**是此策略就是資料層備援性低進行中的成本。 Hello 與任何應用程式重寫並不需要額外成本，SQL Database 服務會自動執行備份。  還原 hello 彈性資料庫時，才造成 hello 成本。 hello**取捨**是 hello 完成資料庫復原的所有租用戶要花很長的時間。 hello 的時間長度取決於 hello 總數還原您起始 hello DR 的區域和租用戶資料庫 hello 的整體大小。 即使您設定一些租用戶還原優先順序透過其他人時，您就會競爭以所有 hello 起始其他還原 hello 相同的區域為 hello 服務 arbitrates 並節流 toominimize hello hello 現有客戶的資料庫的整體影響。 此外之前建立 hello 新彈性集區 hello DR 區域中的,，無法啟動 hello hello 租用戶資料庫復原。

## <a name="scenario-2-mature-application-with-tiered-service"></a>案例 2. 具有分層服務的成熟應用程式
<i>我已熟悉試用版客戶和付費客戶具有分層服務提供項目和不同 SLA 的 SaaS 應用程式。Hello 試用的客戶，我有成本盡可能 tooreduce hello。試用的客戶可以接受的停機時間，但我想 tooreduce 的可能性。Hello 付費客戶，任何停機時間是飛行風險。所以我想確定付費客戶一定都能 tooaccess toomake 其資料。</i> 

此案例中，個別 hello 試用租用戶從 toosupport 支付租用戶的將它們放入個別的彈性集區。 hello 試用的客戶會有較低的 eDTU，每個租用戶和較低的 SLA，較長的復原時間。 hello 付費客戶是每個租用戶和更高的 SLA 更高的 eDTU 與集區中。 tooguarantee hello 最低復原時間，hello 付費客戶的租用戶資料庫的地理複寫。 在 hello 下圖說明此組態。 

![圖 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

如同 hello 第一個案例中，因此您對它 (1) 使用單一的地理複寫資料庫，會相當啟用 hello 管理資料庫。 這可確保新的客戶訂用帳戶、 設定檔更新和其他管理操作 hello 可預測的效能。 hello hello 混雜的 hello 管理資料庫所在的區域是 hello 主要區域，而 hello 的 hello 管理資料庫的次要資料庫所在的 hello 區域是 hello DR 區域。

hello 付費客戶租用戶資料庫使用中的資料庫中有 「 付費 」 集區佈建 hello 主要區域中的 hello。 佈建第二個集區以相同的名稱，在 hello DR 區域中的 hello。 每個租用戶是地理複寫 toohello 次要集區 (2)。 這會使用容錯移轉來快速復原所有租用戶資料庫。 

如果發生中斷 hello 主要區域，hello 復原步驟 toobring 中您的應用程式上線 hello 下圖所示：

![圖 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* 立即容錯移轉 hello 管理資料庫 toohello DR 區域 (3)。
* 變更 hello 應用程式的連接字串 toopoint toohello DR 地區。 現在所有新帳戶和租用戶資料庫建立 hello DR 區域中。 hello 現有試用的客戶會看到其資料暫時無法使用。
* 容錯移轉 hello 付費 hello DR 區域 tooimmediately 中的租用戶資料庫 toohello 集區還原其可用性 (4)。 由於 hello 容錯移轉是快速的中繼資料的層級變更，請考慮的最佳化 hello 個別的容錯移轉，依需求觸發 hello 使用者連接。 
* 如果因為 hello 次要資料庫僅需要的 hello 容量 tooprocess hello 變更記錄時，它們是次要資料庫，立即增加 hello 集區容量低於主要 hello 您的第二個集區 eDTU 大小，而現在 tooaccommodate hello 完整所有租用戶 (5) 的工作負載。 
* 建立 hello 新彈性集區以相同的名稱和 hello 相同的 hello hello 試用客戶的資料庫 (6) 的 hello DR 區域中的組態。 
* Hello 試用客戶的集區建立之後，使用地理還原 toorestore hello 個別的試用版租用戶資料庫到 hello 新集區 (7)。 請考慮觸發 hello 個別還原 hello 使用者連接，或使用某些其他應用程式特定優先順序的架構。

此時您的應用程式在 hello DR 區域中已回復連線。 所有的付費客戶預設具有存取 tootheir 資料時 hello 試用的客戶時存取其資料時遇到延遲。

當復原 Azure hello 主要區域*之後*還原 hello hello DR 區域，您可以繼續執行在該區域中的 hello 應用程式中的應用程式，或者您可以決定 toofail 後 toohello 主要區域。 如果復原 hello 主要區域*之前*hello 容錯移轉程序完成，立即失敗後請考慮。 hello 容錯回復採用 hello hello 下圖中所述的步驟： 

![圖 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* 取消所有未處理的異地還原要求。   
* 容錯移轉 hello 管理資料庫 (8)。 Hello 區域復原後，hello 舊的主要自動成為次要 hello。 現在它會變成 hello 主要一次。  
* 容錯移轉 hello 付費的租用戶資料庫 (9)。 同樣地，hello 區域復原後，hello 舊主要複本會自動成為 hello 次要資料庫。 現在就會將 hello 主要複本會變成一次。 
* 設定 hello 還原試用 hello DR 區域僅 tooread (10) 中已變更的資料庫。
* Hello 試用的客戶 DR 的集區中變更過 hello 復原每個資料庫，重新命名或刪除 hello hello 試用的客戶主要集區 (11) 中對應的資料庫。 
* 複製 hello 更新 hello DR 集區 toohello 主要集區 (12) 的資料庫。 
* 刪除 hello DR 集區 (13) 

> [!NOTE]
> hello 容錯移轉作業是非同步。 toominimize hello 的復原時間很重要，您至少 20 個資料庫的批次執行 hello 租用戶資料庫的容錯移轉命令。 
> 
> 

hello 金鑰**獲益**是此策略，是它提供 hello 最高 SLA 的付費客戶 hello。 它也會保證 hello 新試用已解除封鎖，因為建立 hello 試用 DR 集區。 hello**取捨**此安裝程式會增加 hello 的總成本 hello 租用戶資料庫 hello 成本 hello 次要 DR 集區的付費客戶。 此外，如果 hello 次要集區有不同的大小，hello 付費客戶遇到較低的效能在容錯移轉之後 hello hello DR 區域中的集區升級直到完成為止。 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>案例 3. 具有分層服務的分散式應用程式
<i>我已有完善且提供分層服務的 SaaS 應用程式。我想 toooffer 非常主動的 SLA toomy 付費客戶，而且即使短暫中斷可能會造成客戶不滿，因為發生中斷時，將 hello 風險的影響降至最低。請務必付款客戶該 hello 永遠可以存取其資料。hello 試用可用而且 hello 試用期間，不提供 SLA。</i> 

toosupport 這種情況下，使用三個個別彈性集區。 佈建兩個相同大小集區中兩個不同的區域 toocontain hello 每個資料庫的高 Edtu 付費客戶的租用戶資料庫。 包含 hello 試用租用戶 hello 第三個集區可以有較低的 Edtu，每個資料庫，並佈建中的其中一個 hello 兩個區域。

tooguarantee hello 最低復原時間的中斷期間，hello 付費客戶的租用戶資料庫的 50%的 hello 主要資料庫中的 hello 兩個區域的每個地理複寫。 同樣地，每個區域有 50%的 hello 次要資料庫。 如此一來，如果區域已離線，只達 50%的 hello 付費客戶的資料庫受到影響，並對 toofail。 hello 其他資料庫仍維持不變。 在 hello 下列圖表說明此組態：

![圖 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

相當 active hello 管理資料庫是在 hello 前一個案例中，因此將其設定為單一地理區域複寫資料庫 (1)。 這可確保 hello hello 新客戶訂用帳戶、 設定檔更新和其他管理作業的可預測的效能。 區域 A 與 hello hello 管理資料庫的主要區域，並用 hello 管理資料庫的復原 hello 區域 B。

hello 付費客戶的租用戶資料庫也是地理複寫，但次要複本與主要複本會分割成區域 A 與區域 B (2)。 如此一來，受到 hello 中斷 hello 租用戶主要資料庫可以容錯移轉 toohello 其他區也可供使用。 hello 另一半 hello 租用戶資料庫都不會影響所有。 

hello 下圖說明 hello 復原步驟 tootake，如果發生中斷在區域 a

![圖 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* 立即容錯移轉 hello 管理資料庫 tooregion B (3)。
* 變更 hello 應用程式的連接字串 toopoint toohello 管理資料庫中區域 b 修改 hello 管理資料庫 toomake 確定 hello 新帳戶和租用戶資料庫會建立區域 B 中，而且會那里尋找 hello 現有的租用戶資料庫做為區域。 hello 現有試用的客戶會看到其資料暫時無法使用。
* 容錯移轉 hello 付費的租用戶資料庫 toopool 2 區域 B tooimmediately 還原其可用性 (4)。 由於 hello 容錯移轉是快速的中繼資料的層級變更，您可以考慮的最佳化 hello 個別的容錯移轉，依需求觸發 hello 使用者連接。 
* 由於集區 2 包含只有主要資料庫，現在 hello hello 的增加集區中的總工作負載，而且可以立即增加其 eDTU 大小 (5)。 
* 建立 hello 新彈性集區以相同的名稱和 hello 相同的 hello hello 區域 B 的 hello 試用客戶的資料庫 (6) 中的組態。 
* 一次 hello 建立集區使用 「 地理還原 toorestore hello 個別的試用版租用戶資料庫到 hello 集區 (7)。 您可以考慮觸發 hello 個別還原 hello 使用者連接，或使用某些其他應用程式特定優先順序的架構。

> [!NOTE]
> hello 容錯移轉作業是非同步。 toominimize hello 復原時間，請務必至少 20 個資料庫的批次執行 hello 租用戶資料庫的容錯移轉命令。 
> 

此時您的應用程式處於上線區域 b。所有的付費客戶預設具有存取 tootheir 資料時 hello 試用的客戶時存取其資料時遇到延遲。

如果要 toouse 區域 B 試用的客戶或錯誤後回復 toousing hello 試用的客戶集區在區域 a 區域 A 則在復原時需要 「 toodecide一個準則可能 hello %的試用版租用戶 hello 復原後修改的資料庫。 不論該決策，您需要兩個集區之間 toore 平衡 hello 付費的租用戶。 hello 下圖說明當 hello 試用版租用戶資料庫失敗後 tooregion A.hello 程序  

![圖 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* 取消所有未處理的 「 地理還原要求 tootrial DR 集區。   
* 容錯移轉 hello 管理資料庫 (8)。 Hello 區域復原後，hello 舊的主要自動變為 hello 次要版本。 現在它會變成 hello 主要一次。  
* 選取哪些付費的租用戶資料庫失敗後 toopool 1 到起始容錯移轉 tootheir 次要 (9)。 Hello 區域復原後，集區 1 中的所有資料庫會自動都變成次要資料庫。 現在，其中的 50% 會再次變成主要。 
* 減少 hello 大小集區 2 toohello 原始 eDTU (10)。
* 設定所有還原 hello 區域 B tooread 專用 (11) 中的試用版資料庫。
* Hello 試用 DR 的集區中變更過 hello 復原每個資料庫，重新命名或刪除 hello hello 試用主要集區 (12) 中對應的資料庫。 
* 複製 hello 更新 hello DR 集區 toohello 主要集區 (13) 的資料庫。 
* 刪除 hello DR 集區 (14) 

hello 金鑰**優點**的這項策略：

* 它支援 hello 最積極 SLA hello 付費客戶，因為它會確保中斷不會影響超過 50%的 hello 租用戶資料庫。 
* 它可以保證 hello 新試用已解除封鎖，因為 hello 復原期間建立 hello 軌跡 DR 集區。 
* 它可讓更有效率地使用 hello 集區容量為 50%的集區 1 中的次要資料庫，而且集區 2 會保證 toobe 少時比 hello 主要資料庫。

主要的 hello**取捨**是：

* hello CRUD 作業，針對 hello 管理資料庫有 hello 連線的終端使用者 tooregion A 比 hello 連線的終端使用者 tooregion B 的較低的延遲，針對 hello 主要 hello 管理資料庫的執行。
* 它需要更複雜的設計 hello 管理資料庫。 例如，每個租用戶記錄有位置標記需要 toobe 容錯移轉和容錯回復期間變更。  
* hello 付款客戶可能會遇到較低的效能比平常 hello 區域 B 的集區升級直到完成為止。 

## <a name="summary"></a>摘要
本文著重在 hello SaaS ISV 多租用戶應用程式所使用的資料庫層的 hello 嚴重損壞修復策略。 hello 您選擇的策略根據 hello 需求 hello 應用程式，例如 hello 的商務模型，hello SLA 您希望 toooffer tooyour 客戶、 預算限制等。每個描述策略外框 hello 優點和取捨讓您無法做出明智的決策。 此外，特定應用程式可能包含其他 Azure 元件。 讓您檢閱其業務續航力指引，以及協調 hello 與它們的資料庫層的 hello 復原。 進一步了解管理在 Azure 中，資料庫應用程式的復原 toolearn 參照太[設計災害復原的雲端解決方案](sql-database-designing-cloud-solutions-for-disaster-recovery.md)。  

## <a name="next-steps"></a>後續步驟
* toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)。
* 如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)。
* toolearn 有關使用自動的備份進行復原，請參閱[hello 服務起始的備份還原的資料庫](sql-database-recovery-using-backups.md)。
* toolearn 有關更快速的復原選項，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)。
* toolearn 有關用於自動的備份封存，請參閱[資料庫複製](sql-database-copy.md)。

