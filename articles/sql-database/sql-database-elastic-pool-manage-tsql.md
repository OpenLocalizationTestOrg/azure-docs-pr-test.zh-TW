---
title: "T-SQL：管理 Azure SQL Database 彈性集區 | Microsoft Docs"
description: "使用 T-SQL toomanage Azure SQL Database 彈性集區。"
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>使用 Transact-SQL 監視和管理彈性集區
本主題說明如何 toomanage 可擴充[彈性集區](sql-database-elastic-pool.md)使用 Transact SQL。  您也可以建立和管理 Azure 的彈性集區 hello [Azure 入口網站](https://portal.azure.com/)， [PowerShell](sql-database-elastic-pool-manage-powershell.md)，hello REST API 或[C#](sql-database-elastic-pool-manage-csharp.md)。 您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。


使用 hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx)和[Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx)彈性集區進出命令 toocreate 和移動資料庫。 您可以使用這些命令之前，必須存在 hello 彈性集區。 這些命令只會影響資料庫。 建立新的集區及 hello 設定 （例如 min 和 max Edtu) 的集區屬性無法變更使用 T-SQL 命令。

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>在彈性集區中建立集區資料庫
使用 hello CREATE DATABASE 命令和 hello SERVICE_OBJECTIVE 選項。   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

彈性集區中的所有資料庫都會都繼承 hello 彈性集區 （Basic、 Standard、 Premium） 的 hello 服務層。 

## <a name="move-a-database-between-elastic-pools"></a>在彈性集區之間移動資料庫
以 hello 修改使用 hello ALTER DATABASE 命令，並設定服務\_目標選項設定為彈性\_集區。 設定 hello 名稱 toohello hello 目標集區的名稱。

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>將資料庫移入彈性集區
以 hello 修改使用 hello ALTER DATABASE 命令，並設定服務\_ELASTIC_POOL 為目標的選項。 設定 hello 名稱 toohello hello 目標集區的名稱。

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>將資料庫移出彈性集區
使用 hello ALTER DATABASE 命令，並設定 hello SERVICE_OBJECTIVE tooone hello 效能層級 （例如 S0 或 S1）。

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>列出彈性集區中的資料庫
使用 hello [log_reuse_wait_desc\_服務\_目標檢視](https://msdn.microsoft.com/library/mt712619)toolist 所有 hello 彈性集區中的資料庫。 登入 toohello master 資料庫 tooquery hello 檢視。

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>取得彈性集區的資源使用量資料
使用 hello [sys.elastic\_集區\_資源\_統計檢視](https://msdn.microsoft.com/library/mt280062.aspx)tooexamine hello 資源使用量統計資料的邏輯伺服器上彈性集區。 登入 toohello master 資料庫 tooquery hello 檢視。

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>取得集區資料庫的資源使用量
使用 hello [sys.dm\_ db\_資源\_統計檢視](https://msdn.microsoft.com/library/dn800981.aspx)或[sys.resource\_統計檢視](https://msdn.microsoft.com/library/dn269979.aspx)tooexamine hello 資源使用量統計資料的彈性集區中的資料庫。 此程序是單一資料庫的類似 tooquerying 資源使用量。

## <a name="next-steps"></a>後續步驟
在建立之後彈性集區，您可以藉由建立彈性的工作管理 hello 集區中的彈性資料庫。 彈性的作業有助於針對任意數目的 hello 集區中的資料庫執行 T-SQL 指令碼。 如需詳細資訊，請參閱 [彈性資料庫工作概觀](sql-database-elastic-jobs-overview.md)。 

請參閱[使用 Azure SQL Database 向外延展](sql-database-elastic-scale-introduction.md)： 使用彈性資料庫工具 tooscale 外的，移動資料、 查詢或建立的交易。

