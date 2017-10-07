---
title: "aaaSQL Server 資料庫移轉 tooAzure SQL 資料庫 |Microsoft 文件"
description: "了解如何 SQL Server 資料庫移轉 tooAzure hello 雲端中的 SQL 資料庫。 使用資料庫移轉工具 tootest 相容性先前 toodatabase 移轉。"
keywords: "database migration,sql server database migration,database migration tools,migrate database,migrate sql database,資料庫移轉,sql server 資料庫移轉,資料庫移轉工具,移轉資料庫,移轉 sql database"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>SQL Server 資料庫移轉 tooSQL hello 雲端中的資料庫
在本文中，您了解 hello 移轉 SQL Server 2005 或更新版本資料庫 tooAzure SQL 資料庫的兩種主要方法。 hello 第一種方法比較簡單，但是需要部分，可能是大，hello 移轉期間的停機時間。 hello 第二個方法更為複雜，但大幅消除 hello 移轉期間的停機時間。

在這兩種情況下，您需要 tooensure hello 來源資料庫是與 Azure SQL Database 使用 hello 相容[資料移轉小幫手 (DMA)](https://www.microsoft.com/download/details.aspx?id=53595)。 SQL Database V12 已接近[功能同位檢查](sql-database-features.md)與問題相關的 tooserver 層級和跨資料庫作業以外的 SQL Server。 資料庫和應用程式依賴[部分支援或不支援函式](sql-database-transact-sql-information.md)需要某些[重新工程 toofix 這些不相容狀況](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues)hello SQL Server 之前可以移轉資料庫。

> [!NOTE]
> toomigrate 非 SQL Server 資料庫，包括 Microsoft Access、 Sybase、 MySQL Oracle 和 DB2 tooAzure SQL Database，請參閱[SQL Server 移轉小幫手](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/)。
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Hello 移轉期間的方法 1： 移轉停機時間

 如果您可以經得起一些停機時間，或者您在執行生產資料庫的測試移轉，以便稍後進行移轉，請使用此方法。 如需教學課程，請參閱[移轉 SQL Server Database](sql-database-migrate-your-sql-server-database.md)。

hello 下列清單包含 hello SQL Server 資料庫移轉使用此方法的一般工作流程。

  ![VSSSDT 移轉圖表](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. 評估使用 hello 最新版本的相容性的 hello 資料庫[資料移轉小幫手 (DMA)](https://www.microsoft.com/download/details.aspx?id=53595)。
2. 準備 Transact-SQL 指令碼形式的任何必要修正。
3. 製作 hello 來源資料庫的交易一致性複本移轉-並確定沒有進一步進行的變更 toohello 來源資料庫 （或 hello 移轉完成之後，您可以手動套用任何這類變更）。 有許多方法 tooquiesce 資料庫，無法停用用戶端連線 toocreating[資料庫快照集](https://msdn.microsoft.com/library/ms175876.aspx)。
4. 部署 hello Transact SQL 指令碼 tooapply hello 修正 toohello 資料庫副本。
5. [匯出](sql-database-export.md)hello 資料庫複製 tooa。在本機磁碟機的 BACPAC 檔案。
6. [匯入](sql-database-import.md)hello。使用數個 BACPAC 的任何新的 Azure SQL database 當做 BACPAC 檔案匯入工具，SQLPackage.exe 正在 hello 建議為了達到最佳效能的工具。

### <a name="optimizing-data-transfer-performance-during-migration"></a>將移轉期間的資料傳輸效能最佳化 

下列清單中的 hello 包含 hello 匯入程序的最佳效能的建議。

* 選擇最高服務等級 hello 和效能層預算允許 toomaximize hello 傳輸效能。 Toosave money hello 移轉後，您可以向下進行調整。 
* Hello 之間的距離降至最低您。BACPAC 檔案和 hello 目的地的資料中心。
* 在移轉期間停用自動統計資料
* 分割資料表和索引
* 捨棄索引檢視表，然後於移轉完成後重新建立
* 移除查詢很少的歷程記錄資料 tooanother 資料庫，並移轉此歷程記錄資料 tooa 個別 Azure SQL 資料庫。 您接著可以使用[彈性查詢](sql-database-elastic-query-overview.md)查詢此歷程記錄資料。

### <a name="optimize-performance-after-hello-migration-completes"></a>Hello 移轉完成之後，將效能最佳化

[更新統計資料](https://msdn.microsoft.com/library/ms187348.aspx)與 hello 移轉完成之後進行完整掃描。

## <a name="method-2-use-transactional-replication"></a>方法 2：使用異動複寫

當無法承受 tooremove SQL Server 資料庫從生產 hello 移轉發生時，您可以使用 SQL Server 異動複寫，做為移轉解決方案。 toouse 這種方法，hello 來源資料庫必須符合 hello[異動複寫的需求](https://msdn.microsoft.com/library/mt589530.aspx)而相容的 Azure SQL Database。 如需使用 AlwaysOn 的 SQL 複寫相關資訊，請參閱[設定 AlwaysOn 可用性群組 (SQL Server) 的複寫](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server)。

toouse 此解決方案中，您設定您的 Azure SQL Database 為您想 toomigrate 的訂閱者 toohello SQL Server 執行個體。 hello 異動複寫散發者 」 同步處理 hello 資料庫 toobe 同步處理 （hello 發行者） 的資料時新的交易仍能繼續進行。 

使用異動複寫，所有變更 tooyour 資料或結構描述都顯示在您的 Azure SQL Database。 一旦 hello 同步作業已完成並準備好 toomigrate，變更您的應用程式 toopoint hello 連接字串它們 tooyour Azure SQL Database。 異動複寫會清空保留任何變更之後來源資料庫和所有應用程式上點 tooAzure DB 中，您可以解除安裝異動複寫。 您的 Azure SQL Database 現在已是您的生產環境系統。

 ![SeedCloudTR 圖表](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> 您也可以使用異動複寫 toomigrate 來源資料庫的子集。 您複寫 tooAzure SQL Database 的 hello 發行集可以是有限的 tooa hello 正在進行複寫的資料庫中的 hello 資料表子集。 每個資料表進行複寫，您可以限制 hello 資料 tooa hello 資料列的子集和/或 hello 資料行的子集。
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>移轉 tooSQL 資料庫使用的交易複寫工作流程

> [!IMPORTANT]
> Azure 和 SQL Database 更新 tooMicrosoft 與同步處理使用的 SQL Server Management Studio tooremain hello 最新版本。 舊版 SQL Server Management Studio 無法將 SQL Database 設定為訂閱者。 [更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。
> 

1. 設定散發套件
   -  [使用 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [使用 Transact-SQL](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. 建立發佈
   -  [使用 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [使用 Transact-SQL](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. 建立訂用帳戶
   -  [使用 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [使用 Transact-SQL](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>一些秘訣和移轉差異 tooSQL 資料庫

1. 使用本機散發者 
   - 這會造成 hello 伺服器效能造成影響。 
   - 如果無法接受 hello 效能影響，您可以使用另一部伺服器，但同時管理中增加了複雜性。
2. 選取的快照集資料夾，讓您選取確定 hello 資料夾是夠大 toohold 每個資料表的 BCP 想 tooreplicate。 
3. 快照集建立鎖定 hello 相關聯的資料表，直到它已完成，因此適當地排程快照集。 
4. Azure SQL Database 僅支援推送訂用帳戶。 您只能新增 「 訂閱者 」 從 hello 來源資料庫。

## <a name="resolving-database-migration-compatibility-issues"></a>解決資料庫移轉相容性問題
有各種不同的相容性可能會遇到的問題，同時在 hello 版本的 SQL Server 上根據 hello 來源資料庫和 hello 複雜性 hello 您要移轉的資料庫。 舊版 SQL Server 有更多的相容性問題。 使用下列資源的 hello，此外 tooa 目標使用的選項的搜尋引擎的網際網路搜尋：

* [Azure SQL Database 中不支援的 SQL Server 資料庫功能](sql-database-transact-sql-information.md)
* [SQL Server 2016 中已終止的資料庫引擎功能](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [SQL Server 2014 中已終止的資料庫引擎功能](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [SQL Server 2012 中已終止的資料庫引擎功能](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [SQL Server 2008 R2 中已終止的資料庫引擎功能](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [SQL Server 2005 中已終止的資料庫引擎功能](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

此外 toosearching hello 網際網路，並使用這些資源，請使用 hello [MSDN SQL Server 社群論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver)或[StackOverflow](http://stackoverflow.com/)。

## <a name="next-steps"></a>後續步驟
* 也使用 hello Azure SQL EMEA 工程師部落格上的 hello 指令碼[移轉過程監視 tempdb 使用量](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/)。
* 也使用 hello Azure SQL EMEA 工程師部落格上的 hello 指令碼[進行移轉時，監視資料庫的 hello 交易記錄空間](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0)。
* SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。
* 如需有關使用 UTC 時間，在移轉之後，請參閱[修改 hello 預設時區的當地時區](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/)。
* 移轉之後變更 hello 資料庫預設語言的相關資訊，請參閱[toochange hello Azure SQL Database 的預設語言的方式](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/)。


