---
title: "Azure 入口網站：建立及管理 SQL Database 彈性集區 | Microsoft Docs"
description: "了解 toouse hello Azure 入口網站和 SQL Database 內建智慧 toomanage、 監視器和適當的大小可延展的彈性集區 toooptimize 資料庫效能和管理成本的方式。"
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>建立及管理彈性集區以 hello Azure 入口網站
本主題說明如何 toocreate 及管理可擴充[彈性集區](sql-database-elastic-pool.md)以 hello Azure 入口網站。 您也可以建立和管理 Azure 的彈性集區與[PowerShell](sql-database-elastic-pool-manage-powershell.md)，hello REST API 或[C#](sql-database-elastic-pool-manage-csharp.md)。 您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。

## <a name="create-an-elastic-pool"></a>建立彈性集區 

彈性集區的建立方式有兩種。 您可以進行從頭如果您知道 hello 集區設定，或啟動從 hello 服務建議。 SQL Database 已內建建議的彈性集區設定，如果更符合成本效益根據過去的資料庫使用遙測 hello 為您的智慧。

您可以建立多個集區的伺服器上，但您無法將資料庫從不同的伺服器新增到 hello 相同的集區。 

> [!NOTE]
> 彈性集區已在所有 Azure 區域中正式運作 (GA)，但印度西部除外，此區域目前提供預覽版。  我們將儘速在此區域提供彈性集區的 GA。
>

### <a name="step-1-create-an-elastic-pool"></a>步驟 1：建立彈性集區

建立從現有的彈性集區**伺服器**hello 入口網站中的分頁是 hello 最簡單方式 toomove 現有的資料庫至彈性集區。

> [!NOTE]
> 您也可以建立彈性集區，藉由搜尋**SQL 彈性集區**在 hello **Marketplace** ，或按一下 [ **+ 加**在 hello **SQL 彈性集區**瀏覽] 刀鋒視窗。 您就可以 toospecify 新的或現有的伺服器，透過此集區佈建工作流程。
>
>

1. 在 hello [Azure 入口網站](http://portal.azure.com/)，按一下**更多服務**  **>**  **SQL 伺服器**，然後按一下包含 hello hello 伺服器您想要 tooadd tooan 彈性集區的資料庫。
2. 按一下 [新增集區] 。

    ![加入集區 tooa 伺服器](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **-或-**

    您可能會看到訊息，指出那里建議使用 hello 伺服器的彈性集區。 按一下 hello 訊息 toosee hello 建議的集區根據歷程記錄資料庫使用量遙測，然後按一下 hello 層 toosee 更多詳細資料，來自訂 hello 集區。 請參閱[了解集區建議](#understand-elastic-pool-recommendations)本主題稍後的 hello 建議開放的方式。

    ![建議的集區](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. hello**彈性集區**刀鋒視窗隨即出現，這是用來指定 hello 設定集區。 如果您按下**新集區**hello 先前步驟中，在 hello 定價層是**標準**選取預設並沒有資料庫。 您可以建立空的集區，或指定一組現有的資料庫，從該伺服器 toomove 到 hello 的集區。 如果您要建立建議的集區，hello 建議定價層，效能設定的資料庫清單預先填入，但您還是可以變更它們。

    ![設定彈性集區](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. 指定 hello 彈性集區的名稱，或將它保留為 hello 預設值。

### <a name="step-2-choose-a-pricing-tier"></a>步驟 2：選擇定價層

hello 集區的定價層會決定 hello 功能可用 toohello elastics hello 集區，以及 hello 最大數目 (eDTU 最大值) 的 edtu 數目及儲存體 (Gb) 可用 tooeach 資料庫中。 如需詳細資訊，請參閱服務層。

toochange hello 定價層級的 hello 集區中，按一下**定價層**，按一下 定價的層，然後再按一下 hello**選取**。

> [!IMPORTANT]
> 您選擇定價層的 hello，即可認可您的變更後，當**確定**在 hello 最後一個步驟中，您必須能夠 toochange hello 定價層的 hello 集區。 toochange hello 現有彈性集區的定價層、 建立 hello 所需的定價層中的彈性集區及移轉 hello 資料庫 toothis 新集區。
>

![選取定價層](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>步驟 3： 設定 hello 集區

設定後 hello 定價層，請按一下設定集區，其中您加入資料庫、 設定集區 Edtu 與儲存體 (集區 Gb)，而且您設定 hello elastics 的 hello min 和 max Edtu hello 集區中。

1. 按一下 [設定集區] 
2. 選取您想要 tooadd toohello 集區的 hello 資料庫。 建立 hello 集區時，這個步驟是選擇性的。 建立 hello 集區之後，可以加入資料庫。
    按一下 tooadd 資料庫**將資料庫加入**，按一下您想 tooadd，，，然後按一下hello hello 資料庫**選取** 按鈕。

    ![新增資料庫](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    如果您正在使用的 hello 資料庫的歷程記錄使用量遙測資料不足，hello**估計 eDTU 與 GB 使用量**圖形和 hello**實際 eDTU 使用量**橫條圖更新 toohelp 進行設定決策。 此外，hello 服務可能會提供建議訊息 toohelp 您適當的大小 hello 集區。 請參閱 [動態建議](#understand-elastic-pool-recommendations)。

3. 使用 hello hello 控制項**設定集區**tooexplore 設定頁面上，並設定您的集區。 如需各服務層限制的詳細資訊，請參閱[彈性集區限制](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)；如需如何決定彈性集區適當大小的詳細指導方針，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)。 如需集區設定的詳細資訊，請參閱[彈性集區屬性](sql-database-elastic-pool.md#database-properties-for-pooled-databases)。

    ![設定彈性集區](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. 按一下**選取**在 hello**設定集區**刀鋒視窗中的變更設定之後。
5. 按一下**確定**toocreate hello 集區。

## <a name="understand-elastic-pool-recommendations"></a>了解彈性集區建議

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

## <a name="manage-and-monitor-an-elastic-pool"></a>管理及監視彈性集區

您可以使用 Azure 入口網站 toomonitor hello 和管理彈性集區和 hello hello 集區中的資料庫。 從 hello 入口網站，您可以監視 hello 善用彈性集區和該集區中的 hello 資料庫。 您也會使一組變更 tooyour 彈性集區並送出所有在 hello 變更相同的時間。 這些變更包括新增或移除資料庫、變更您的彈性集區設定，或變更您的資料庫設定。

hello 下列圖形顯示範例彈性集區。 hello 檢視包括：

*  監視資源使用量的 hello 彈性集區和 hello 集區中所包含的 hello 資料庫圖表。
*  hello**設定**集區 按鈕 toomake 變更 toohello 彈性集區。
*  hello**建立資料庫**按鈕會建立資料庫，並將它加入 toohello 目前彈性集區。
*  彈性工作，可藉由對清單中的所有資料庫執行 Transact SQL 指令碼，協助您管理大量資料庫。

![集區檢視][2]

您可以移 tooa 特定集區 toosee 其資源使用量。 根據預設，hello 集區是已設定的 tooshow 儲存體和 eDTU 使用量 hello 過去一小時內。 hello 圖表可以設定的 tooshow 不同度量經由各種時間視窗。

1. 選取與彈性集區 toowork。
2. [彈性集區監視] 之下的是標示為 [資源使用率] 的圖表。 按一下 hello 圖表。

    ![彈性集區監視][3]

    hello**度量**刀鋒視窗中開啟，顯示 hello 的詳細的檢視透過 hello 指定的時段指定度量。   

    ![[度量] 刀鋒視窗][9]

### <a name="toocustomize-hello-chart-display"></a>toocustomize hello 圖表顯示

您可以編輯 hello 圖表和 hello 計量刀鋒伺服器 toodisplay 其他度量資訊，例如 CPU 百分比、 資料 IO 百分比及使用的記錄 IO 百分比。

1. 在 hello 計量刀鋒伺服器上按一下**編輯**。

    ![按一下 [編輯]。][6]

2. 在 hello**編輯圖表**刀鋒視窗中，選取時間範圍 （過去一小時，目前或上週），或按一下**自訂**tooselect 任何日期範圍 hello 過去兩週。 選取 hello 圖表類型 （橫條或線條），然後選取 hello 資源 toomonitor。

   > [!Note]
   > 只有以 hello hello 中可顯示相同的量值單位的度量圖表 hello 在相同的時間。 比方說，如果您選取 「 eDTU 百分比 」 然後您只能選取其他度量，以百分比為 hello 測量單位。
   >

    ![按一下 [編輯]。](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. 然後按一下 [確定] 。

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>管理及監視彈性集區中的資料庫

您也可以監視個別資料庫的潛在問題。

1. 在 [彈性資料庫監視] 之下，有一個圖表可顯示五個資料庫的度量。 根據預設，hello 圖表會顯示 hello 前 5 資料庫 hello 集區中 hello 平均 eDTU 使用量過去一小時。 按一下 hello 圖表。

    ![彈性集區監視][4]

2. hello**資料庫資源使用量**刀鋒視窗隨即出現。 這提供 hello hello 集區中的資料庫使用方式的詳細的檢視。 使用 hello hello 的 hello 刀鋒視窗的下半部的方格，您可以選取任何資料庫中 hello 集區 toodisplay hello 圖表 （向上 too5 資料庫） 中的其使用情形。 您也可以自訂 hello 度量和時間範圍顯示 hello 圖表中，依序按一下**編輯圖表**。

    ![資料庫資源使用率刀鋒視窗][8]

### <a name="toocustomize-hello-view"></a>toocustomize hello 檢視

1. 在 hello**資料庫資源使用率**刀鋒視窗中，按一下 **編輯圖表**。

    ![按一下編輯圖表](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. 在 hello**編輯**圖表刀鋒視窗中，選取時間範圍 （過去一小時或過去 24 小時），或按一下**自訂**tooselect 不同每天在過去 2 週 toodisplay hello。

    ![按一下自訂](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. 按一下 hello**比較資料庫**下拉式 tooselect 不同度量 toouse 比較資料庫時。

    ![編輯 hello 圖表](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect 資料庫 toomonitor

在 hello 資料庫清單中 hello**資料庫資源使用量**刀鋒視窗中，您可以找到特定的資料庫，藉由查詢透過 hello 清單中的 hello 頁面或在 hello 的資料庫名稱中輸入。 使用 hello 核取方塊 tooselect hello 資料庫。

![搜尋資料庫 toomonitor][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>加入警示 tooan 彈性集區資源

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

## <a name="move-a-database-into-an-elastic-pool"></a>將資料庫移入彈性集區

您可以從現有的集區中新增或移除資料庫。 hello 資料庫可以位於其他集區。 不過，您只可以加入會在 hello 相同的資料庫邏輯伺服器。

1. 在 hello 刀鋒視窗中的 hello 集區，在**彈性資料庫**按一下**設定集區**。

    ![按一下 [設定集區]][1]

2. 在 hello**設定集區**刀鋒視窗中，按一下 **新增 toopool**。

    ![按一下 新增 toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. 在 hello**新增資料庫**刀鋒視窗中，選取 hello 資料庫或資料庫 tooadd toohello 集區。 然後按一下 [選取] 。

    ![選取資料庫 tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    hello**設定集區**現在清單 hello 選取 toobe 加太設定其狀態的資料庫刀鋒視窗**暫止**。

    ![擱置中的新增集區](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. 在 hello**設定集區 刀鋒視窗**，按一下 **儲存**。

    ![按一下 [Save] \(儲存)。](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>將資料庫移出彈性集區

1. 在 hello**設定集區**刀鋒視窗中，選取 hello 資料庫或資料庫 tooremove。

    ![資料庫清單](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. 按一下 [從集區移除] 。

    ![資料庫清單](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    hello**設定集區**刀鋒視窗中列出 hello 選取 toobe 其狀態太設定中移除的資料庫現在**暫止**。

    ![預覽新增和移除的資料庫](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. 在 hello**設定集區 刀鋒視窗**，按一下 **儲存**。

    ![按一下 [Save] \(儲存)。](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>變更彈性集區的效能設定

當您監視 hello 彈性集區的資源使用情況，您會發現一些調整所需。 或許 hello 集區需要 hello 效能或存放裝置限制中的變更。 可能是您想 toochange hello hello 集區中的資料庫設定。 您可以變更在任何時間 tooget hello 最佳平衡效能及成本的 hello 集區的 hello 安裝程式。 如需詳細資訊，請參閱[何時應該使用彈性集區？](sql-database-elastic-pool.md)

toochange hello Edtu 或儲存體限制每個集區，以及每個資料庫的 edtu 數目：

1. 開啟 hello**設定集區**刀鋒視窗。

    在下**彈性集區設定**，使用其中一個滑桿 toochange hello 集區設定。

    ![彈性集區資源使用量](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. 當 hello 設定變更時，hello 顯示 hello 每月的估計成本 hello 變更。

    ![更新彈性集區和新的每月成本](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>彈性集區的作業延遲
* 變更每個資料庫或最大每個資料庫的 Edtu hello min Edtu 通常完成在 5 分鐘或更短。
* 變更每個集區 edtu 數 （hello） 取決於 hello hello 集區中的所有資料庫所使用的空間數量總計。 變更作業平均每 100 GB 會在 90 分鐘以內完成。 比方說，如果使用的總空間的 hello hello 集區中的所有資料庫都為 200 GB，則 hello 預期的變更 hello 每個集區的集區 eDTU 延遲都為 3 小時或更少。

## <a name="next-steps"></a>後續步驟

- 何種彈性集區，請參閱的 toounderstand [SQL Database 彈性集區](sql-database-elastic-pool.md)。
- 如需使用彈性集區的相關指導方針，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)。
- toouse 彈性作業 toorun Transact SQL 指令碼針對任意數目的資料庫中 hello 集區，請參閱[彈性的工作概觀](sql-database-elastic-jobs-overview.md)。
- tooquery 跨任意數目的資料庫中 hello 集區，請參閱[彈性的查詢概觀](sql-database-elastic-query-overview.md)。
- 交易任意數目的資料庫中 hello 集區，請參閱[彈性交易](sql-database-elastic-transactions-overview.md)。


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
