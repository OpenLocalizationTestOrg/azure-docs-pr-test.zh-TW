---
title: "Azure SQL Database 服務和效能層 | Microsoft Docs"
description: "比較單一資料庫的 SQL Database 服務層和效能等級，並且介紹 SQL 彈性集區"
keywords: "資料庫選項, 資料庫效能"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Azure SQL Database 可用的效能選項為何

[Azure SQL Database](sql-database-technical-overview.md) 提供針對單一和[集區](sql-database-elastic-pool.md)資料庫提供四個服務層。 這些服務層為：[基本]、[標準]、[進階] 和 [進階 RS]。 每個服務層內是多個效能層級 ([Dtu](sql-database-what-is-a-dtu.md)) 和儲存體選項 toohandle 不同的工作負載和資料大小。 較高的效能層級提供額外的計算和儲存體資源設計 toodeliver 愈來愈高輸送量和容量。 您可以動態變更服務層、效能等級和儲存體，而不需要停機。 
- [基本]、[標準] 和 [高階] 服務層都具備 99.99% 的執行時間 SLA、彈性的商務持續性選項、安全性功能，以及按小時計費。 
- hello **Premium RS**層提供 hello 同一個效能層級 hello Premium 層，以降低 SLA 因為它會比中的資料庫副本的較低數字以執行 hello 其他服務層。 因此，您也可以在 hello 事件中的服務失敗，您可能需要您的資料庫從備份與 tooa 5 分鐘延隔 toorecover。

> [!IMPORTANT]
> Azure SQL database 取得一組保證的資源和 hello 預期不會影響資料庫的效能特性在 Azure 中的任何其他資料庫。 

## <a name="choosing-a-service-tier"></a>選擇服務層
hello 下表提供適用於不同的應用程式工作負載的最佳 hello 層範例。

| 服務層 | 目標工作負載 |
| :--- | --- |
| **基本** | 最適合於小型資料庫，通常會在指定的時間內支援單一的作用中作業。 範例包括用於開發或測試，或者不常使用之小規模應用程式的資料庫。 |
| **標準** |hello go-toooption 低 toomedium IO 效能需求，支援多個並行查詢的雲端應用程式。 範例包括工作群組或 Web 應用程式。 |
| **高級** | 針對具有高 IO 效能需求的高交易量而設計，支援許多並行使用者。 範例包括支援任務關鍵性應用程式的資料庫。 |
| **進階 RS** | 針對不需要高可用性保證 hello 的 IO 密集工作負載所設計。 範例包括高效能工作負載或其中 hello 資料庫不是 hello 系統的記錄分析工作負載測試。 |
|||

您可以在具有特定[效能等級](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)的服務層內，建立具有專用資源的單一資料庫，也可以在 [SQL 彈性集區](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus)內建立資料庫。 SQL 彈性集區，在 hello 運算和儲存體資源會共用到單一邏輯伺服器內的多個資料庫。 

單一資料庫可用的資源會以資料庫交易單位 (DTU) 表示，而 SQL 彈性集區的資源則會以彈性資料庫交易單位 (eDTU) 表示。 如需 DTU 和 eDTU 的詳細資訊，請參閱[什麼是 DTU 和 eDTU？](sql-database-what-is-a-dtu.md)。

toodecide 上一個服務階層，先判斷您需要的 hello 最小的資料庫功能：

| **服務層功能** | **基本** | **標準** | **高級** | **進階 RS**|
| :-- | --: | --: | --: | --: |
| 單一資料庫大小上限 | 2 GB | 250 GB | 4 TB*  | 500 GB  |
| 彈性集區大小上限 | 156 GB | 2.9 TB | 4 TB* | 750 GB |
| 彈性集區中的資料庫大小上限 | 2 GB | 250 GB | 500 GB | 500 GB |
| 每個集區的資料庫數目上限 | 500  | 500 | 100 | 100 |
| 單一資料庫 DTU 上限 | 5 | 100 | 4000 | 1000 |
| 彈性集區中每個資料庫的 DTU 上限 | 5 | 3000 | 4000 | 1000 |
| 資料庫備份的保留期限 | 7 天 | 35 天 | 35 天 | 35 天 |
||||||

> [!IMPORTANT]
> 向上 too4 TB 的儲存體目前僅供 hello 下列區域： 美國 East2、 美國西部、 美國 Gov 維吉尼亞州、 西歐、 德國中央、 南東亞、 日本東部、 澳洲東部、 加拿大中央和加拿大東部。 請參閱[目前的 4 TB 限制](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

一旦您判定 hello 適當的服務層，您已準備好 toodetermine hello 效能層級 （hello Dtu 數目） 和 hello hello 資料庫的儲存體數量。 

- hello S2 和 S3 效能層級中 hello**標準**層通常是很好的起點。 
- 對於高的 CPU 或 IO 需求的資料庫，hello hello 效能層級**Premium**層是 hello 右邊的起點。 
- hello **Premium**層提供更多的 CPU 和 10 倍的更多 IO 啟動比較中 hello toohello 最高的效能等級**標準**層。
- hello **PremiumRS**層提供 hello 效能，為 hello **Premium**層較低的成本，但與減少的 SLA。

> [!IMPORTANT]
> 檢閱 hello [SQL 彈性集區](sql-database-elastic-pool.md)主題 hello 詳細資料群組的資料庫到 SQL 彈性集區 tooshare 運算和儲存體資源。 hello 本主題其餘部分著重於服務層和效能層級的單一資料庫。
>

## <a name="single-database-service-tiers-and-performance-levels"></a>單一資料庫服務層和效能等級
若為單一資料庫，每個服務層內會有多個效能等級和儲存體數量。 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>相應放大或相應縮小單一資料庫

一開始挑選服務層和效能層級後，您可以根據實際經驗，動態放大或縮小單一資料庫。  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

變更 hello 服務層或效能層級的資料庫在 hello 新效能層級建立 hello 原始資料庫的複本，並再將連接切換 toohello 複本。 此程序期間會遺失任何資料，但在 hello 當我們切換 toohello 複本簡短的時刻，toohello 資料庫的連接會停用，因此某些在途中可能會回復交易。 hello hello 切換的時間長度會有所不同，但通常是在 4 秒為小於 30 秒 99%的 hello 時間。 如果有大量的交易傳送 hello 時刻連線已停用，hello 的 hello 切換的時間長度可能是較長。  

hello 整個向上延展程序取決於這兩個 hello 大小和 hello 服務層資料庫之前和之後變更 hello hello 持續時間。 例如，在標準服務層內進行變更的 250 GB 資料庫應在 6 小時內完成。 Hello 的資料庫相同的大小變更效能層級內 hello Premium 服務層，它應該 3 小時內完成。

> [!TIP]
> toocheck hello 的調整大小作業進行中的 SQL 資料庫的狀態，您可以使用下列查詢的 hello: ```select * from sys.dm_operation_status```。
>

* 如果您要升級 tooa 高服務層或效能層級，除非您明確指定較大的最大大小，不會增加 hello 資料庫大小上限。
* toodowngrade 資料庫，hello 資料庫必須是小於 hello 的允許大小上限 hello 目標服務層。 
* 升級的資料庫時[地理複寫](sql-database-geo-replication-portal.md)啟用，然後再升級主要資料庫 （一般指引） hello 升級其次要資料庫 toohello 所需的效能層。 當升級 tooa 不同版本 ugrading hello 次要資料庫第一次是必要。 
* 降級的資料庫時[地理複寫](sql-database-geo-replication-portal.md)啟用，將其主要資料庫 toohello 所需的效能層降級後再降級 hello 次要資料庫 （一般指引）。 當降級 tooa 不同版本降級 hello 主要資料庫第一次是必要。 

* hello 還原服務供應項目都會有不同 hello 不同服務層。 如果降級 toohello**基本**層，您將會具有較低的備份保留期限-請參閱[Azure SQL Database 備份](sql-database-automated-backups.md)。
* hello 變更完成之前，不會套用 hello hello 資料庫的新屬性。


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>P11 和 P15 資料庫目前的大小上限為 4 TB

某些區域中支援的 P11 與 P15 資料庫大小上限為 4 TB (如先前所討論)。 hello 下列考量與限制適用於 tooP11 和 4 TB maxsize P15 資料庫：

- 如果您選擇 hello 4 TB maxsize 選項，建立資料庫 （使用 4 TB 或 4096 GB 的值） 時，hello 建立命令失敗，發生錯誤 hello 資料庫不支援的地區中佈建。
- 對於現有 P11 和 P15 資料庫位於其中一個支援的 hello 區域，您可以增加 hello maxsize 儲存體 too4 TB。 這可以使用 hello 來檢查[選取 DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx)或藉由檢查 hello hello Azure 入口網站中的資料庫大小。 升級現有的 P11 或 P15 資料庫只能執行由伺服器層級主體登入或 hello dbmanager 資料庫角色的成員。 
- 如果在執行升級作業就會立即更新支援的地區 hello 組態。 hello 資料庫仍在線上 hello 升級程序期間。 不過，您就不能使用完整的 hello 4 TB 的儲存體之前 hello 實際的資料庫檔案都已升級 toohello 新 maxsize。 hello 長度所需的時間取決於在 hello hello 正在升級的資料庫大小。  
- 建立或更新 P11 或 P15 資料庫時，您只能在 1TB 和 4TB 的大小上限之間選擇。 目前不支援中繼儲存體大小。 建立 P11/P15，1 TB 的 hello 預設儲存體選項時，預先選取。 對於資料庫位於其中一個支援的 hello 區域，您可以增加 hello 為新的或現有的單一資料庫儲存體最大 too4TB。 在其他所有區域中，無法將大小上限增加至 1 TB 以上。 當您選取 4 TB 的儲存體包含 hello 價格不會變更。
- hello 4 TB 資料庫的 maxsize 不得變更的 too1 TB 即使使用 hello 實際儲存區未達 1 TB。 因此，您無法降級 P11-4 TB/P15-4 TB tooa P11-1 TB/P15-1 TB 或較低的效能層，例如 tooP1 P6） 直到我們效能層級提供額外的存放裝置 hello hello 其餘的選項。 這項限制也適用於 toohello 還原和複製案例，包括時間點，異地還原長期-長期備份的保留，以及資料庫複本。 資料庫設定之後使用 hello 4 TB 的選項，必須執行所有的還原作業，此資料庫到 P11/P15 4 TB maxsize。
- 當建立或升級 P11/P15 中的資料庫不支援的地區，hello 建立或升級作業因下列錯誤訊息的 hello: **P11 和 P15 資料庫上的儲存體 too4TB 位於美國 East2、 美國西部、 美國 Gov 維吉尼亞西歐、 德國中央、 東南亞、 日本東部、 澳洲東部、 加拿大中部和加拿大東部。**
- 若是作用中異地複寫案例：
   - 設定異地複寫關聯性： 如果 P11 或 P15 hello 主要資料庫，hello secondary(ies) 必須也是 P11 或 P15;較低效能層會做為次要資料庫拒絕，因為它們並非能夠支援 4 TB。
   - 升級的 hello 主要資料庫中的地理複寫關聯性： hello maxsize too4 TB，主要資料庫上的變更會觸發的 hello hello 次要資料庫變更時相同。 這兩個升級必須在 hello 主要 tootake 效果 hello 變更成功。 區域 hello 4 TB 選項限制 （請參閱上面）。 如果次要 hello 處於不支援 4 TB 的區域，主要的 hello 不會升級。
- 不支援使用 hello 匯入/匯出服務載入 P11-4 TB/P15-4 TB 的資料庫。 也使用 SqlPackage.exe[匯入](sql-database-import.md)和[匯出](sql-database-export.md)資料。

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>管理單一資料庫服務層和效能層級使用 hello Azure 入口網站

tooset 或變更 hello 服務層、 效能層級或使用 hello Azure 入口網站開啟 hello 新的或現有 Azure SQL 資料庫的儲存體數量**設定效能**為您的資料庫，依序按一下視窗**定價層 （小數位數的 Dtu）** -hello 下列螢幕擷取畫面所示。 

- 設定或變更 hello 服務層，選取您的工作負載的 hello 服務層。 
- 設定或變更 hello 效能層級 (**Dtu**) 使用 hello 服務層內**DTU**滑桿。
- 設定或變更使用 hello hello 效能層級的 hello 儲存體數量**儲存體**滑桿。 

  ![設定服務層和效能等級](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> 選取 P11 或 P15 服務層時，檢閱[P11 和 P15 資料庫目前的大小上限為 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)。
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>使用 PowerShell 管理單一資料庫服務層和效能等級

tooset 或變更 Azure SQL 資料庫服務層、 效能層級，與儲存體數量使用 PowerShell，使用下列 PowerShell 指令程式的 hello。 如果您需要 tooinstall 或升級 PowerShell 時，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。 

| Cmdlet | 說明 |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|建立資料庫 |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|取得一或多個資料庫|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|設定資料庫的屬性，或將現有資料庫移到彈性集區中|


> [!TIP]
> 監視的資料庫中的 hello 效能標準的 PowerShell 範例指令碼縮放，使其 tooa 較高的效能層級和建立警示規則上其中一個 hello 效能度量資訊，請參閱[監視器和調整規模為單一的 SQL 資料庫PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md)。

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>管理單一資料庫服務層和效能層級使用 Azure CLI hello

tooset 或變更 Azure SQL 資料庫服務層、 效能層級及使用 Azure CLI hello 的儲存體數量使用 hello 下列[Azure CLI SQL Database](/cli/azure/sql/db)命令。 使用 hello[雲端殼層](/azure/cloud-shell/overview)toorun hello CLI，瀏覽或[安裝](/cli/azure/install-azure-cli)到 macOS、 Linux 或 Windows。 如需建立和管理 SQL 彈性集區，請參閱[彈性集區](sql-database-elastic-pool.md)。

| Cmdlet | 說明 |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |建立資料庫|
|[az sql db list](/cli/azure/sql/db#list)|列出伺服器中的所有資料庫和資料倉儲，或彈性集區中的所有資料庫|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|列出可用的服務目標與儲存體限制|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|傳回資料庫使用方式|
|[az sql db show](/cli/azure/sql/db#show)|取得資料庫或資料倉儲|
|[az sql db update](/cli/azure/sql/db#update)|更新資料庫|

> [!TIP]
> 縮放後查詢 hello hello 資料庫大小資訊的單一 Azure SQL database tooa 不同的效能層級的 Azure CLI 範例指令碼，請參閱[使用 CLI toomonitor 和小數位數單一的 SQL database](scripts/sql-database-monitor-and-scale-database-cli.md)。
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>使用 Transact-SQL 管理單一資料庫服務層和效能等級

tooset 或變更 Azure SQL 資料庫服務層、 效能層級，與儲存體數量與 TRANSACT-SQL，使用下列 T-SQL 命令 hello。 您可以發出這些命令使用 hello Azure 入口網站[SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio)， [Visual Studio Code](https://code.visualstudio.com/docs)，或是任何其他程式可以連接 tooan Azure SQL Database 伺服器，並傳遞 Transact SQL命令。 

| 命令 | 說明 |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|建立新的資料庫。 您必須是連接的 toohello master 資料庫 toocreate 新的資料庫。|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |修改 Azure SQL 資料庫。 |
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|傳回 hello edition （服務層）、 （定價層） 的服務目標和彈性集區名稱，如果有的話，Azure SQL database 或 Azure SQL 資料倉儲。 如果登入 toohello master 資料庫中的 Azure SQL Database 伺服器，傳回所有資料庫相關資訊。 Azure SQL 資料倉儲，您必須連接的 toohello master 資料庫。|
|[sys.database_usage (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|列出 hello 數目、 類型和持續時間，Azure SQL Database 伺服器上的資料庫。|

hello 下列範例顯示 hello maxsize 正在變更使用 hello ALTER DATABASE 命令：

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>管理單一資料庫時使用 hello REST API

tooset 或變更 Azure SQL 資料庫服務層、 效能層級，與儲存體數量使用 hello REST API，請參閱[Azure SQL Database REST API](/rest/api/sql/)。

## <a name="next-steps"></a>後續步驟

* 深入了解 [DTU](sql-database-what-is-a-dtu.md)。
* toolearn 有關監視 DTU 使用量，請參閱[監視和效能調整](sql-database-troubleshoot-performance.md)。

