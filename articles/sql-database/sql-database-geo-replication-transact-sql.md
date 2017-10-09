---
title: "aaaConfigure 地理複寫的 Azure SQL Database 使用 TRANSACT-SQL |Microsoft 文件"
description: "使用 Transact-SQL 為 Azure SQL Database 設定異地複寫"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>使用 Transact-SQL 為 Azure SQL Database 設定作用中異地複寫

本文章將示範如何 tooconfigure 的作用中地理複寫使用 Azure SQL Database TRANSACT-SQL。

tooinitiate 容錯移轉使用 TRANSACT-SQL，請參閱[起始已規劃或未規劃的容錯移轉 Azure SQL database 使用 TRANSACT-SQL](sql-database-geo-replication-failover-transact-sql.md)。

> [!NOTE]
> 當您使用災害復原的作用中地理複寫 （可讀取次要資料庫），您應該設定應用程式 tooenable 自動和透明容錯移轉的所有資料庫的容錯移轉群組。 這項功能處於預覽狀態。 如需詳細資訊，請參閱[自動容錯移轉群組和異地複寫](sql-database-geo-replication-overview.md)。
> 
> 

tooconfigure 作用中地理複寫使用 TRANSACT-SQL，您需要下列 hello:

* Azure 訂用帳戶
* Azure SQL Database 邏輯伺服器<MyLocalServer>和 SQL database <MyDB> -您想 tooreplicate hello 主要資料庫
* 一或多個邏輯 Azure SQL Database 伺服器 < MySecondaryServer(n) >-hello 邏輯將會是您要在其中建立次要資料庫的 hello 夥伴伺服器的伺服器
* 為 DBManager hello 主要的登入
* 具有 db_ownership hello 本機資料庫，您會進行異地複寫
* DBManager 位於 hello 夥伴伺服器 toowhich 您將設定異地複寫
* hello 最新版本的 SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> 建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。 [更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。
> 
> 

## <a name="add-secondary-database"></a>加入次要資料庫
您可以使用 hello **ALTER DATABASE**陳述式 toocreate 夥伴伺服器上，進行地理複寫的次要資料庫。 您的 hello 伺服器包含 hello 資料庫 toobe 複寫 hello master 資料庫上執行此陳述式。 hello 進行地理複寫資料庫 (hello 「 主要資料庫 」) 將會擁有相同的名稱，因為正在進行複寫的 hello 資料庫並將預設 hello hello 相同服務層級為 hello 主要資料庫。 hello 次要資料庫可以是可讀取或無法讀取，而且可以是單一資料庫或彈性集區中。 如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。
建立並植入 hello 次要資料庫之後，資料將會開始從主要資料庫的 hello 以非同步方式複寫。 hello 下列步驟說明如何 tooconfigure 地理複寫使用 Management Studio。 步驟 toocreate 非可讀取和可讀取次要資料庫，被提供做為單一資料庫或彈性集區中。

> [!NOTE]
> 如果以相同的名稱，作為主要的 hello hello hello 指定的夥伴伺服器上的資料庫存在資料庫 hello 命令會失敗。
> 

### <a name="add-readable-secondary-single-database"></a>加入可讀取次要複本 (單一資料庫)
使用下列步驟 toocreate 可讀取的次要複本做為單一資料庫的 hello。

1. 在 Management Studio 中連接 tooyour Azure SQL Database 邏輯伺服器。
2. 開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。
3. 使用下列 hello **ALTER DATABASE**陳述式 toomake 次要伺服器上的可讀取次要資料庫與異地備援主要的本機資料庫。
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. 按一下**Execute** toorun hello 查詢。

### <a name="add-readable-secondary-elastic-pool"></a>新增可讀取次要複本 (彈性集區)
使用下列步驟 toocreate 彈性集區中的可讀取次要複本的 hello。

1. 在 Management Studio 中連接 tooyour Azure SQL Database 邏輯伺服器。
2. 開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。
3. 使用下列 hello **ALTER DATABASE**陳述式 toomake 彈性集區中的次要伺服器上的可讀取次要資料庫與異地備援主要的本機資料庫。
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. 按一下**Execute** toorun hello 查詢。

## <a name="remove-secondary-database"></a>移除次要資料庫
您可以使用 hello **ALTER DATABASE**陳述式 toopermanently 終止 hello 與其主要與次要資料庫的複寫合作關係。 主要資料庫所在的 hello hello master 資料庫上執行此陳述式。 Hello 關聯性終止之後，hello 次要資料庫會變成一般的讀寫資料庫。 如果 hello 連線 toosecondary 資料庫已損毀 hello 命令會成功，但次要 hello 連線恢復後，將會變成讀寫。 如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。

使用地理複寫合作關係中的下列步驟 tooremove 異地備援的次要的 hello。

1. 在 Management Studio 中連接 tooyour Azure SQL Database 邏輯伺服器。
2. 開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。
3. 使用下列 hello **ALTER DATABASE**陳述式 tooremove 異地備援的次要資料庫。
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. 按一下**Execute** toorun hello 查詢。

## <a name="monitor-active-geo-replication-configuration-and-health"></a>監視主動式異地複寫組態和健康狀態

監視工作包括 hello 地理複寫組態的監視和監視資料複寫健全狀況。  您可以使用 hello **sys.dm_geo_replication_links** hello master 資料庫 tooreturn 資訊中的每個資料庫的所有現有複寫連結的相關 hello Azure SQL Database 邏輯伺服器上的動態管理檢視。 此檢視會包含一個資料列，每個主要與次要資料庫之間的 hello 複寫連結。 您可以使用 hello **sys.dm_replication_link_status**動態管理檢視 tooreturn 一個資料列的每個目前參與複寫的複寫連結的 Azure SQL Database。 這包括主要和次要資料庫。 如果在給定主要資料庫有一個以上的連續複寫連結，此資料表會包含 hello 關聯性的每個資料列。 在所有資料庫，包括 hello 邏輯 master 中建立 hello 檢視。 不過，查詢在 hello 邏輯 master 中的這個檢視會傳回空集合。 您可以使用 hello **sys.dm_operation_status**動態管理檢視 tooshow hello 狀態，進行所有資料庫作業包括 hello hello 複寫連結狀態。 如需詳細資訊，請參閱 [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx)、[sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) 和 [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx)。

使用下列步驟 toomonitor 作用中地理複寫合作關係的 hello。

1. 在 Management Studio 中連接 tooyour Azure SQL Database 邏輯伺服器。
2. 開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。
3. 使用下列陳述式 tooshow hello 所有資料庫的異地複寫連結。
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. 按一下**Execute** toorun hello 查詢。
5. 開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**MyDB**，然後按一下**新查詢**。
6. 下列陳述式 tooshow hello 複寫使用 hello 會延遲，和最後一個 MyDB 我次要資料庫的複寫的時間。
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. 按一下**Execute** toorun hello 查詢。
8. 使用下列陳述式 tooshow hello 最新地理複寫作業 MyDB 資料庫相關聯的 hello。
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. 按一下**Execute** toorun hello 查詢。

## <a name="next-steps"></a>後續步驟
* toolearn 深入了解容錯移轉群組和作用中的地理複寫，請參閱-[容錯移轉群組](sql-database-geo-replication-overview.md)
* 如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)

