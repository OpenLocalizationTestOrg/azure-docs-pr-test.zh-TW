---
title: "aaaWhat 是彈性集區嗎？ 管理多個 SQL Database - Azure | Microsoft Docs"
description: "管理及調整多個 SQL Database - 成百上千 - 使用彈性集區。 可視需要散發的資源只有一個價格。"
keywords: "多個資料庫, 資料庫資源, 資料庫效能"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>彈性集區可協助您管理及調整多個 SQL Database

SQL Database 彈性集區是簡單、符合成本效益的解決方案，可用來管理及調整使用需求變化不定且無法預測的多個資料庫。 彈性集區中的 hello 資料庫在單一的 Azure SQL Database 伺服器上，共用的資源 ([彈性資料庫交易單位](sql-database-what-is-a-dtu.md)(Edtu)) 組的價格。 在 Azure SQL Database 的彈性集區啟用 SaaS 開發人員 toooptimize hello 價格效能群組的資料庫符合規定的預算同時提供每個資料庫的效能彈性。   

> [!NOTE]
> 彈性集區已在所有 Azure 區域中正式運作 (GA)，但印度西部除外，此區域目前提供預覽版。  我們將儘速在此區域提供彈性集區的 GA。
>

## <a name="what-are-sql-elastic-pools"></a>SQL 彈性集區是什麼？ 

SaaS 開發人員會在由多個資料庫組成的大規模資料層上建置應用程式。 常見的應用程式模式是 tooprovision 單一資料庫針對每個客戶。 不同的客戶通常會有不同及無法預期的使用模式，但很難 toopredict hello 資源需求的每個個別的資料庫使用者。 您通常有兩個選項： 

- 根據尖峰使用量額外佈建資源並額外付款，或是
- 置中佈建 toosave 成本，在尖峰期間的效能和客戶滿意度的 hello 費用。 

彈性集區解決方法是確保資料庫取得在需要時，所需的 hello 效能資源的這個問題。 它們會在可預測的預算內提供簡單的資源配置機制。 toolearn 有關使用彈性集區，SaaS 應用程式的設計模式的詳細資訊請參閱[設計模式為多租用戶 SaaS 應用程式使用 Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

彈性集區可讓 hello 開發人員 toopurchase[彈性資料庫交易單位](sql-database-what-is-a-dtu.md)(Edtu) 的個別資料庫所共用的使用方式的多個資料庫 tooaccommodate 週期無法預期的集區。 hello 集區的 eDTU 需求取決於其資料庫的 hello 彙總使用率。 hello Edtu toohello 可用集區的數目是由 hello 開發人員預算控制。 hello 開發人員只是將資料庫 toohello 集區，設定 hello 最小值和最大的 hello 資料庫的 Edtu，然後設定 hello eDTU 根據預算投入 hello 集區。 開發人員可以使用集區 tooseamlessly 成長的 「 精實 」 啟動 tooa 成熟企業在其服務不斷增加小數位數。

Hello 集區內的個別資料庫會提供 hello 彈性 tooauto 間隔內設定參數。 負載過重時，資料庫可能會耗用更多的 Edtu toomeet 需求。 負載較輕的資料庫取用較少的 eDTU，而完全無負載的資料庫不會取用任何 eDTU。 佈建 hello 整個集區，而不是單一資料庫的資源，可簡化管理工作。 此外，您還可以用於 hello 集區的可預測的預算。 可加入其他 Edtu tooan 現有集區沒有資料庫停機的情況下，不同之處在於 hello 資料庫可能需要移動 toobe tooprovide hello 其他運算資源 hello 新 eDTU 保留項目。 同樣地，如果不再需要額外 eDTU，則隨時可以從現有集區中移除。 而且，您可以加入或減去資料庫 toohello 集區。 如果可以預測資料庫使用少量資源，則將它移出。

您可以建立和管理彈性集區使用 hello [Azure 入口網站](sql-database-elastic-pool-manage-portal.md)， [PowerShell](sql-database-elastic-pool-manage-powershell.md)， [TRANSACT-SQL](sql-database-elastic-pool-manage-tsql.md)， [C#](sql-database-elastic-pool-manage-csharp.md)，和 hello REST API。 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>何時該考慮使用 SQL Database 彈性集區？

集區很適合具備特定使用模式的大量資料庫。 針對指定的資料庫，此模式的特徵是低平均使用量與相對不頻繁的使用量高峰。

hello 多個資料庫可以加入 tooa 存款變得更大的集區 hello。 根據您應用程式使用量的模式，就只需要兩個 S3 資料庫可能 toosee 節省量。  

hello 下列章節幫助您了解如何 tooassess 如果特定集合的資料庫有利的集區中。 hello 範例會使用標準的集區但 hello 相同的原則也適用於 tooBasic 和 Premium 的集區。

### <a name="assessing-database-utilization-patterns"></a>評估資料庫使用量模式

hello 下圖顯示花費在閒置的時間，但也會定期升高與活動之資料庫的範例。 這是適合集區的使用量模式：

   ![適合某個集區的單一資料庫](./media/sql-database-elastic-pool/one-database.png)

Hello 五分鐘內所述，向上 too90 Dtu DB1 尖峰，但其整體平均使用量不超過五個 Dtu。 效能層級是 S3 需要 toorun 在單一資料庫中，此工作負載，但這會讓大部分的 hello 資源未使用在活動較少的期間。

集區可讓這些未使用的 Dtu toobe 橫跨多個資料庫，並因此可降低 hello Dtu 必要且整體成本。

建置 hello 上述範例中，假設有其他資料庫具有類似的使用量模式為 DB1。 Hello 接著下列兩個圖形，在 hello 的四個資料庫的使用率和 20 個資料庫則會置於相同的 hello 到圖形 tooillustrate hello 非重疊的性質的使用率隨著時間：

   ![使用量模式適合某個集區的 4 個資料庫](./media/sql-database-elastic-pool/four-databases.png)

  ![使用量模式適合某個集區的 20 個資料庫](./media/sql-database-elastic-pool/twenty-databases.png)

hello 前面圖中的 hello 黑色列說明 hello 彙總 DTU 使用率 20 的所有資料庫。 這會顯示 hello 彙總的 DTU 使用率永遠不會超過 100 Dtu，並指出 hello 20 個資料庫可以共用 100 Edtu，此時間週期內。 這會導致 20 x 減少 Dtu 和 13 x 價格比較減少 tooplacing 每個 S3 效能層級的單一資料庫中的 hello 資料庫。

這個範例適合 hello 下列原因：

* 每一資料庫之間的尖峰使用量和平均使用量有相當大的差異。  
* 每個資料庫的 hello 尖峰使用量就會發生不同時間點的時間。
* eDTU 會在許多資料庫之間共用。

集區的 hello 價格是 hello 的集區 edtu 數目的函式。 1.5 x 大於 hello 單一資料庫的 DTU 單價 hello 集區 eDTU 單價時**可由多個資料庫共用集區 edtu 數目以及需要較少的總 Edtu**。 價格和 eDTU 共用這些差異，是的集區可以提供的 hello 價格節省潛在的 hello 基礎。  

hello 下列法則相關 toodatabase 計數和資料庫使用量說明 tooensure，集區提供降低單一資料庫的成本比較 toousing 效能層級。

### <a name="minimum-number-of-databases"></a>資料庫的最小數目

如果多個 1.5 x hello 集區所需的 hello Edtu hello 總和 hello 的單一資料庫的效能層級的 Dtu，彈性集區是更符合成本效益的。 如需可用的大小，請參閱[彈性集區和彈性資料庫的 eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)。

***範例***<br>
在至少兩個 S3 資料庫或至少 15 S0 資料庫所需的 100 eDTU 集區 toobe 更符合成本效益比使用單一資料庫的效能層級。

### <a name="maximum-number-of-concurrently-peaking-databases"></a>並行尖峰資料庫的最大數目

共用 Edtu，並非所有的資料庫集區中可以同時使用向上 toohello 限制可用的 Edtu 時使用單一資料庫的效能層級。 hello 較少的資料庫，同時尖峰，hello 較低的 hello 集區 eDTU 可以集和多個符合成本效益的 hello 集區會變成的 hello。 一般情況下，不超過 2/3 （或 67%） 的 hello 集區中的 hello 資料庫應該同時尖峰 tootheir eDTU 限制。

***範例***<br>
200 的 eDTU 集區中的三個 S3 資料庫的 tooreduce 成本，最多兩個資料庫可以同時尖峰其使用情況。 否則，如果兩個以上的四個 S3 資料庫同時尖峰 hello 集區必須 toobe 大小 toomore 比 200 Edtu。 如果 hello 集區調整大小的 toomore 比 200 的 Edtu，需要更多的 S3 資料庫 toobe 加入 toohello 集區 tookeep 成本低於單一資料庫的效能層級。

請注意此範例不考慮 hello 集區中的其他資料庫的使用率。 如果所有資料庫都有一些使用率在任何給定時間點的時間，然後小於 2/3 （或 67%） 的 hello 資料庫可以尖峰同時。

### <a name="dtu-utilization-per-database"></a>每個資料庫的 DTU 使用量
Hello 尖峰與平均使用量資料庫之間具有大幅差異表示低使用率很長一的段短的使用率過高。 這個使用量模式非常適合在資料庫之間共用資源。 若資料庫的尖峰使用量為平均使用量的 1.5 倍大，就應該將該資料庫視為集區。

***範例***<br>
尖峰 too100 Dtu 和平均使用 67 Dtu 的 S3 資料庫或 less 共用集區的 edtu 數目是很好的候選項目。 或者，S1 尖峰 too20 dtu 數及資料庫的平均使用 13 Dtu 或 less 是適合做為集區。

## <a name="how-do-i-choose-hello-correct-pool-size"></a>如何選擇 hello 正確的集區大小？

hello 集區的最佳大小取決於 hello 彙總的 edtu 數目及 hello 集區中的所有資料庫所都需的儲存體資源。 這項作業包括決定 hello 較大的 hello 下列：

* 利用 hello 集區中的所有資料庫的 Dtu 最大值。
* 利用 hello 集區中的所有資料庫的最大儲存體位元組。

如需可用的大小，請參閱[彈性集區和彈性資料庫的 eDTU 和儲存體限制](#what-are-the-resource-limits-for-elastic-pools)。

SQL Database 會自動評估 hello 歷史資源使用量中現有的 SQL 資料庫伺服器的資料庫，並且建議 hello Azure 入口網站中的 hello 適當的集區組態。 在加法 toohello 建議事項，內建的體驗會預估 hello 自訂群組的 hello 伺服器上資料庫的 eDTU 使用量。 這可讓您 toodo 「 假設 」 分析以互動方式新增資料庫 toohello 集區移除這些 tooget 資源使用量分析，並藉以調整大小的建議，再認可變更。 如需相關作法，請參閱 [監視、管理和估算彈性集區大小](sql-database-elastic-pool-manage-portal.md)。

在您無法在此使用工具的情況下，hello 下列逐步可協助您評估集區是否比單一資料庫更符合成本效益：

1. 評估 hello Edtu 所需的 hello 集區，如下所示：

   最大值(<DB 總數 X 每個 DB 的平均 DTU 使用量>，<br>
   <並行尖峰 DB 的數目** X 每個 DB 的尖峰 DTU 使用量**)
2. 評估 hello 藉由加入 hello 集區中的所有 hello 資料庫所都需的位元組 hello 編號 hello 集區所都需的儲存空間。 然後判斷提供此儲存體數量的 hello eDTU 集區大小。 如需以 eDTU 集區大小為基礎的集區儲存體限制，請參閱 [彈性集區和彈性資料庫的 eDTU 和儲存體限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)。
3. 需要較大的 hello eDTU 評估 hello 從步驟 1 和步驟 2。
4. 請參閱 hello [SQL Database 定價頁面](https://azure.microsoft.com/pricing/details/sql-database/)和尋找 hello 最小 eDTU 集區大小大於 hello 估計值，從步驟 3。
5. 比較 hello 集區價格從步驟 5 toohello 價格的單一資料庫的使用 hello 適當的效能層級。

### <a name="changing-elastic-pool-resources"></a>變更彈性集區資源

您可以增加或減少 hello 資源可用 tooan 彈性集區根據資源需求。

* 變更每個資料庫或最大每個資料庫的 Edtu hello min Edtu 通常完成在 5 分鐘或更短。
* 變更每個集區 edtu 數 （hello） 取決於 hello hello 集區中的所有資料庫所使用的空間數量總計。 變更作業平均每 100 GB 會在 90 分鐘以內完成。 比方說，如果使用的總空間的 hello hello 集區中的所有資料庫都為 200 GB，則 hello 預期的變更 hello 每個集區的集區 eDTU 延遲都為 3 小時或更少。

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>彈性集區的 hello 資源限制有哪些？

hello 下表描述彈性集區的 hello 資源的限制。  請注意，一般而言 hello 資源限制，在彈性集區中的個別資料庫的同一個集區之外的單一資料庫為基礎的 dtu 數及 hello 服務層的 hello。  例如，hello 最大並行的工作者 S2 資料庫是 120 的背景工作。  因此，hello 最大並行的背景工作標準的集區中的資料庫也是 120 工作者是否 hello hello 集區中每個資料庫的最大 DTU 50 的 dtu 數 （這是對等 tooS2）。

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

如果使用所有的彈性集區 Dtu，hello 集區中的每個資料庫就會收到等量的資源 tooprocess 查詢。  hello SQL Database 服務提供資源共用確保相等運算時間配量的資料庫之間的公平性。 彈性集區資源共用公平性此外是資源的 tooany hello 每個資料庫的 DTU 最小值設定為 tooa 非零值時，否則保證 tooeach 資料庫數量。

### <a name="database-properties-for-pooled-databases"></a>集區資料庫的資料庫屬性

hello 下表描述用於管理的集區資料庫的 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 每資料庫的 eDTU 上限 |hello 的 hello 集區中的任何資料庫可以使用，如果可用，根據使用率 hello 集區中的其他資料庫的 Edtu 數目上限。  每個資料庫的 eDTU 數目上限不等於資料庫的資源保證。  這項設定是套用 tooall 資料庫 hello 集區中的全域設定。 在資料庫使用量中設定每個資料庫的最大 Edtu 夠高 toohandle 尖峰。 某種程度的過量使用卻因為 hello 集區通常會假設熱門和冷門習慣的資料庫所在的所有資料庫都不同時都所。 例如，假設每個資料庫的 hello 尖峰使用量是 20 Edtu 而 hello 集區中的 hello 100 資料庫的 20%是尖峰發生於 hello 相同的時間。  如果每個資料庫最大的 hello eDTU 設定 too20 Edtu，則合理 tooovercommit hello 集區 5 次，而每個集區 too400 組 hello Edtu。 |
| 每資料庫的 eDTU 下限 |hello 的保證 hello 集區中的任何資料庫的 Edtu 下限。  這項設定是套用 tooall 資料庫 hello 集區中的全域設定。 每個資料庫的 hello min eDTU 設定 too0，而且也 hello 預設值。 這個屬性是設定 tooanywhere 0 和 hello 平均 eDTU 使用量，每個資料庫之間。 hello hello hello 集區和 hello min Edtu，每個資料庫中的資料庫的數字的產品不能超過每個集區 edtu 數 （hello）。  例如，如果集區有 20 個資料庫，而且每個資料庫的 hello eDTU 最小設定 too10 Edtu，則每個集區 edtu 數 （hello） 必須至少為 200 的 edtu 數 （） 一樣大。 |
| 每個資料庫的資料儲存體上限 |hello 最大儲存體集區中的資料庫。 管理的集區的資料庫共用集區儲存體，因此資料庫儲存體是有限的 toohello 較小的剩餘的集區儲存體和每個資料庫的最大儲存體。 每個資料庫的最大儲存體是指 toohello hello 資料檔的大小上限，而且不包含記錄檔所使用的 hello 空間。 |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>搭配彈性集區使用其他的 SQL Database 功能

### <a name="elastic-jobs-and-elastic-pools"></a>彈性作業和彈性集區

使用集區，只要在**[彈性作業](sql-database-elastic-jobs-overview.md)**中執行指令碼，就能簡化管理工作。 彈性作業會消除與大量資料庫相關聯的冗長工作。 toobegin，請參閱[入門彈性作業](sql-database-elastic-jobs-getting-started.md)。

如需可供使用多個資料庫之其他資料庫工具的詳細資訊，請參閱[使用Azure SQL Database 向上調整](sql-database-elastic-scale-introduction.md)。

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>彈性集區之中的資料庫所適用的業務持續性選項
共用資料庫通常支援 hello 相同[業務續航力功能](sql-database-business-continuity.md)所提供的 toosingle 資料庫。

- **還原時間點**： 還原中的時間點會自動資料庫備份 toorecover 資料庫使用中的集區 tooa 特定點的時間。 請參閱 [還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)

- **「 地理還原**： 異地還原提供 hello 預設復原選項，當資料庫是無法使用，因為 hello hello 資料庫裝載的區域中的事件。 請參閱[還原次要的 Azure SQL Database 或容錯移轉 tooa](sql-database-disaster-recovery.md)

- **作用中異地複寫**：針對較異地還原需要更主動復原的應用程式，設定[作用中異地複寫](sql-database-geo-replication-overview.md)。

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>管理 SQL Database 彈性集區使用 hello Azure 入口網站

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>建立新的 SQL Database 彈性集區，並使用 hello Azure 入口網站

有兩種方式，您可以在 hello Azure 入口網站中建立彈性集區。 您可以進行從頭如果您知道 hello 集區設定，或啟動從 hello 服務建議。 SQL Database 已內建建議的彈性集區設定，如果更符合成本效益根據過去的資料庫使用遙測 hello 為您的智慧。 

建立從現有的彈性集區**伺服器**hello 入口網站中的分頁是 hello 最簡單方式 toomove 現有的資料庫至彈性集區。 您也可以建立彈性集區，藉由搜尋**SQL 彈性集區**在 hello **Marketplace** ，或按一下 [ **+ 加**在 hello **SQL 彈性集區**瀏覽] 刀鋒視窗。 您就可以 toospecify 新的或現有的伺服器，透過此集區佈建工作流程。

> [!NOTE]
> 您可以建立多個集區的伺服器上，但您無法將資料庫從不同的伺服器新增到 hello 相同的集區。
>  

hello 集區的定價層會決定 hello 功能可用 toohello elastics hello 集區，以及 hello 最大數目 (eDTU 最大值) 的 edtu 數目及儲存體 (Gb) 可用 tooeach 資料庫中。 如需詳細資訊，請參閱 [服務層](#edtu-and-storage-limits-for-elastic-pools)。

toochange hello 定價層級的 hello 集區中，按一下**定價層**，按一下 定價的層，然後再按一下 hello**選取**。

> [!IMPORTANT]
> 您選擇定價層的 hello，即可認可您的變更後，當**確定**在 hello 最後一個步驟中，您必須能夠 toochange hello 定價層的 hello 集區。 toochange hello 現有彈性集區的定價層、 建立 hello 所需的定價層中的彈性集區及移轉 hello 資料庫 toothis 新集區。
>

如果您正在使用的 hello 資料庫的歷程記錄使用量遙測資料不足，hello**估計 eDTU 與 GB 使用量**圖形和 hello**實際 eDTU 使用量**橫條圖更新 toohelp 進行設定決策。 此外，hello 服務可能會提供建議訊息 toohelp 您適當的大小 hello 集區。

hello SQL Database 服務會評估使用量記錄，並且更符合成本效益比使用單一資料庫時，建議一或多個集區。 每個建議設定是最佳的方式調整 hello 集區的 hello 伺服器資料庫的唯一子集。

![建議的集區](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

hello 集區建議包含：

- （Basic、 Standard、 Premium 或 Premium RS） 的 hello 集區的定價層
- 適當的 [集區 eDTU]  \(也稱為每一集區的最大 eDTU)
- hello **eDTU 最大**和**eDTU 下限**每個資料庫
- hello hello 集區的建議資料庫清單

> [!IMPORTANT]
> hello 服務會 hello 前 30 天的遙測考量時，建議您將集區。 彈性集區的候選項目會視為資料庫 toobe，它必須存在至少 7 天。 已在彈性集區中的資料庫不會被視為彈性集區建議候選項目。
>

hello 服務會評估資源需求和成本效益的移動 hello 單一資料庫中每個服務層到集區的 hello 相同階層。 例如，會評估伺服器上的所有 Standard 資料庫是否適合 Standard 彈性集區。 這表示 hello 服務不會跨階層的建議，例如標準資料庫移動到 Premium 資料庫。

新增後資料庫 toohello 集區，建議動態產生 hello hello 資料庫，您已選取的歷程記錄的使用量為基礎。 這些建議會出現在 hello eDTU 與 GB 使用量圖表，橫幅中的建議頂端的 hello hello**設定集區**刀鋒視窗。 這些建議是預定的 tooassist 建立彈性集區中適合您特定的資料庫。

![動態建議](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

### <a name="manage-and-monitor-an-elastic-pool"></a>管理及監視彈性集區

您可以在 hello Azure 入口網站，監視 hello 善用彈性集區和該集區中的 hello 資料庫。 您也會使一組變更 tooyour 彈性集區並送出所有在 hello 變更相同的時間。 這些變更包括新增或移除資料庫、變更您的彈性集區設定，或變更您的資料庫設定。

hello 下列圖形顯示範例彈性集區。 hello 檢視包括：

*  監視資源使用量的 hello 彈性集區和 hello 集區中所包含的 hello 資料庫圖表。
*  hello**設定**集區 按鈕 toomake 變更 toohello 彈性集區。
*  hello**建立資料庫**按鈕會建立資料庫，並將它加入 toohello 目前彈性集區。
*  彈性工作，可藉由對清單中的所有資料庫執行 Transact SQL 指令碼，協助您管理大量資料庫。

![集區檢視](./media/sql-database-elastic-pool-manage-portal/basic.png)

您可以移 tooa 特定集區 toosee 其資源使用量。 根據預設，hello 集區是已設定的 tooshow 儲存體和 eDTU 使用量 hello 過去一小時內。 hello 圖表可以設定的 tooshow 不同度量經由各種時間視窗。 按一下 hello**資源使用率**圖表下**彈性集區監視**tooshow hello 的詳細檢視透過 hello 指定的時段指定度量。

![彈性集區監視](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![[度量] 刀鋒視窗](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>toocustomize hello 圖表顯示

您可以編輯 hello 圖表和 hello 計量刀鋒伺服器 toodisplay 其他度量資訊，例如 CPU 百分比、 資料 IO 百分比及使用的記錄 IO 百分比。

![按一下 [編輯]。](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

在 hello**編輯圖表**表單中，您可以選取的時間範圍 （過去一小時，目前或上週），或按一下**自訂**tooselect 任何日期範圍 hello 過去兩週。 您可以選擇橫條或線條圖，，然後選取 hello 資源 toomonitor。

> [!Note]
> 只有以 hello hello 中可顯示相同的量值單位的度量圖表 hello 在相同的時間。 比方說，如果您選取 「 eDTU 百分比 」 然後您只能選取其他度量，以百分比為 hello 測量單位。
>

[按一下 [編輯]](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>管理及監視彈性集區中的資料庫

您也可以監視個別資料庫的潛在問題。 在 [彈性資料庫監視] 之下，有一個圖表可顯示五個資料庫的度量。 根據預設，hello 圖表會顯示 hello 前 5 資料庫 hello 集區中 hello 平均 eDTU 使用量過去一小時。 

![彈性集區監視](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

按一下 hello **hello 過去一小時的資料庫的 eDTU 使用量**下**彈性資料庫監視**。 這會開啟**資料庫資源使用量**和提供的 hello 集區中的 hello 資料庫使用量的詳細的檢視。 使用 hello hello 的 hello 刀鋒視窗的下半部的方格，您可以選取任何資料庫中 hello 集區 toodisplay hello 圖表 （向上 too5 資料庫） 中的其使用情形。 您也可以自訂 hello 度量和時間範圍顯示 hello 圖表中，依序按一下**編輯圖表**。

![資料庫資源使用率刀鋒視窗](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>toocustomize hello 檢視

您可以編輯 hello 圖表 tooselect （過去一小時或過去 24 小時） 的時間範圍，或按一下**自訂**tooselect 不同每天在過去 2 週 toodisplay hello。

![按一下編輯圖表](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![按一下自訂](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

您也可以按一下 hello**比較資料庫**下拉式 tooselect 不同度量 toouse 比較資料庫時。

![編輯 hello 圖表](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect 資料庫 toomonitor

在 hello 資料庫清單中 hello**資料庫資源使用量**刀鋒視窗中，您可以找到特定的資料庫，藉由查詢透過 hello 清單中的 hello 頁面或在 hello 的資料庫名稱中輸入。 使用 hello 核取方塊 tooselect hello 資料庫。

![搜尋資料庫 toomonitor](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>加入警示 tooan 彈性集區資源

您可以加入規則 tooan 彈性集區 hello 彈性集區達到您設定使用率閾值時傳送電子郵件 toopeople 或警示字串 tooURL 端點。

**tooadd 警示 tooany 資源：**

1. 按一下 hello**資源使用率**圖表 tooopen hello**度量**刀鋒視窗中，按一下 **新增警示**，然後填入 hello 中的 hello 資訊**加入警示規則**刀鋒視窗 (**資源**自動設定 toobe hello 集區正在使用)。
2. 輸入**名稱**和**描述**可識別 hello 警示 tooyou 和 hello 收件者。
3. 選擇**度量**想 tooalert 從 hello 清單。

    hello 圖表以動態方式顯示該度量 toohelp 資源使用情況選擇臨界值。

4. 選擇 [條件] \(大於、小於等等) 和 [臨界值]。
5. 選擇**期間**的 hello 度量的時間必須符合規則之前 hello 警示觸發程序。
6. 按一下 [確定] 。

如需詳細資訊，請參閱[在 Azure 入口網站中建立 SQL Database 警示](sql-database-insights-alerts-portal.md)。

### <a name="move-a-database-into-an-elastic-pool"></a>將資料庫移入彈性集區

您可以從現有的集區中新增或移除資料庫。 hello 資料庫可以位於其他集區。 不過，您只可以加入會在 hello 相同的資料庫邏輯伺服器。

 ![按一下 [設定集區]](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![按一下 新增 toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![選取資料庫 tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![擱置中的新增集區](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![按一下 [儲存]。](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>將資料庫移出彈性集區

![資料庫清單](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![資料庫清單](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![預覽新增和移除的資料庫](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![按一下 [Save] \(儲存)。](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>變更彈性集區的效能設定

當您監視 hello 彈性集區的資源使用情況，您會發現一些調整所需。 或許 hello 集區需要 hello 效能或存放裝置限制中的變更。 可能是您想 toochange hello hello 集區中的資料庫設定。 您可以變更在任何時間 tooget hello 最佳平衡效能及成本的 hello 集區的 hello 安裝程式。 如需詳細資訊，請參閱[何時應該使用彈性集區？](sql-database-elastic-pool.md)

toochange hello Edtu 或儲存體限制每個集區，以及每個資料庫的 edtu 數目：

![彈性集區資源使用量](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![更新彈性集區和新的每月成本](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>使用 PowerShell 管理 SQL Database 彈性集區

toocreate 及管理 SQL Database 彈性集區使用 Azure PowerShell，請使用下列 PowerShell 指令程式的 hello。 如果您需要 tooinstall 或升級 PowerShell 時，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。 toocreate 和管理資料庫、 伺服器和防火牆規則，請參閱[建立及管理 Azure SQL Database 伺服器和資料庫使用 PowerShell](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell)。 

> [!TIP]
> PowerShell 範例指令碼，請參閱[建立彈性集區與集區之間，以及從集區中使用 PowerShell，將資料庫移](scripts/sql-database-move-database-between-pools-powershell.md)和[使用 PowerShell toomonitor 和小數位數 SQL 彈性集區中 Azure SQL Database](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Cmdlet | 說明 |
| --- | --- |
|[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|在邏輯 SQL Server 建立彈性資料庫集區。|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|取得邏輯 SQL Server 上的彈性集區及其屬性值。|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|修改邏輯 SQL Server 上的彈性資料庫集區屬性。|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|刪除邏輯 SQL Server 上的彈性資料庫集區。|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|取得 hello 彈性集區的邏輯 SQL server 上的作業狀態。|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|在現有的集區建立新的資料庫，或建立新的資料庫做為單一資料庫。 |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|取得一或多個資料庫。|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|設定資料庫的屬性，或將現有資料庫移入彈性集區、移出彈性集區，或在彈性集區之間移動。|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|移除資料庫。|

> [!TIP]
> 建立的彈性集區中的許多資料庫可能需要完成使用 hello 入口網站或 PowerShell cmdlet，一次建立單一資料庫時的時間。 tooautomate 建立成彈性集區，請參閱[CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae)。
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>管理 SQL Database 彈性集區使用 Azure CLI hello

toocreate 及管理 SQL Database 彈性集區以 hello [Azure CLI](/cli/azure/overview)，使用 hello 下列[Azure CLI SQL Database](/cli/azure/sql/db)命令。 使用 hello[雲端殼層](/azure/cloud-shell/overview)toorun hello CLI，瀏覽或[安裝](/cli/azure/install-azure-cli)到 macOS、 Linux 或 Windows。 

> [!TIP]
> 針對 Azure CLI 範例指令碼，請參閱[使用 CLI toomove SQL 彈性集區中 Azure SQL database](scripts/sql-database-move-database-between-pools-cli.md)和[使用 Azure CLI tooscale SQL 彈性集區中 Azure SQL Database](scripts/sql-database-scale-pool-cli.md)。
>

| Cmdlet | 說明 |
| --- | --- |
|[az sql elastic-pool create](/cli/azure/sql/elastic-pool#create)|建立彈性集區。|
|[az sql elastic-pool list](/cli/azure/sql/elastic-pool#list)|傳回將伺服器中的彈性集區列出的清單。|
|[az sql elastic-pool list-dbs](/cli/azure/sql/elastic-pool#list-dbs)|傳回將彈性集區中的資料庫列出的清單。|
|[az sql elastic-pool list-editions](/cli/azure/sql/elastic-pool#list-editions)|也包含可用的集區 DTU 設定、儲存體限制，以及個別資料庫設定。 在訂單 tooreduce 詳細資訊，額外的存放裝置限制，每個資料庫設定會依預設隱藏。|
|[az sql elastic-pool update](/cli/azure/sql/elastic-pool#update)|更新彈性集區。|
|[az sql elastic-pool delete](/cli/azure/sql/elastic-pool#delete)|刪除 hello 彈性集區。|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>使用 Transact-SQL 管理 SQL Database 彈性集區

toocreate 和移動的資料庫中現有的彈性集區或 tooreturn 資訊使用 Transact SQL，SQL Database 彈性集區使用下列 T-SQL 命令 hello。 您可以發出這些命令使用 hello Azure 入口網站[SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio)， [Visual Studio Code](https://code.visualstudio.com/docs)，或是任何其他程式可以連接 tooan Azure SQL Database 伺服器，並傳遞 Transact SQL命令。 toocreate 和管理資料庫、 伺服器和防火牆規則，請參閱[建立及管理 Azure SQL Database 伺服器和資料庫使用 TRANSACT-SQL](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql)。

> [!IMPORTANT]
> 您無法使用 Transact-SQL 建立、更新或刪除 Azure SQL Database 彈性集區。 您可以新增或移除彈性集區中的資料庫，您可以使用 Dmv tooreturn 資訊有關現有彈性集區。
>

| 命令 | 說明 |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|在現有的集區建立新的資料庫，或建立新的資料庫做為單一資料庫。 您必須是連接的 toohello master 資料庫 toocreate 新的資料庫。|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |將資料庫移入彈性集區、將資料庫移出彈性集區，或在彈性集區之間移動資料庫。|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|刪除資料庫。|
|[sys.elastic_pool_resource_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|傳回所有 hello 彈性資料庫集區的資源使用量統計資料的邏輯伺服器中。 每個彈性資料庫集區，每 15 秒報告時間範圍會傳回一列 (每分鐘四列)。 這包括 CPU、 IO、 記錄、 存放裝置耗用量和並行的要求/工作階段使用量 hello 集區中的所有資料庫。|
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|傳回 hello edition （服務層）、 （定價層） 的服務目標和彈性集區名稱，如果有的話，Azure SQL database 或 Azure SQL 資料倉儲。 如果登入 toohello master 資料庫中的 Azure SQL Database 伺服器，傳回所有資料庫相關資訊。 Azure SQL 資料倉儲，您必須連接的 toohello master 資料庫。|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>管理 SQL Database 彈性集區使用 hello REST API

toocreate 和管理 SQL Database 彈性集區使用 hello REST API，請參閱[Azure SQL Database REST API](/rest/api/sql/)。

## <a name="next-steps"></a>後續步驟

* 若要觀賞影片，請參閱[有關 Azure SQL Database 彈性功能的 Microsoft Virtual Academy 視訊課程](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554)
* toolearn 有關使用彈性集區，SaaS 應用程式的設計模式的詳細資訊請參閱[設計模式為多租用戶 SaaS 應用程式使用 Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md)。
* 如需使用彈性集區 SaaS 教學課程，請參閱[簡介 toohello Wingtip SaaS 應用程式](sql-database-wtp-overview.md)。
