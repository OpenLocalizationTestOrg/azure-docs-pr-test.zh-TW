---
title: "Azure SQL Database 使用動態管理檢視 aaaMonitoring |Microsoft 文件"
description: "深入了解如何 toodetect 及診斷使用動態管理檢視 toomonitor Microsoft Azure SQL Database 的常見效能問題。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>使用動態管理檢視監視 Azure SQL Database
Microsoft Azure SQL Database 可讓子集的動態管理檢視 toodiagnose 效能問題可能已封鎖或長時間執行的查詢、 資源瓶頸、 不佳的查詢計畫等所造成。 此主題提供有關如何使用動態管理檢視 toodetect 常見效能問題。

SQL Database 部分支援動態管理檢視的三個類別目錄：

* 資料庫相關的動態管理檢視。
* 執行相關的動態管理檢視。
* 交易相關的動態管理檢視。

如需動態管理檢視的詳細資訊，請參閱《SQL Server 線上叢書》中的 [動態管理檢視和函數 (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) 。

## <a name="permissions"></a>權限
在 SQL Database 中，查詢動態管理檢視需要 **VIEW DATABASE STATE** 權限。 hello **VIEW DATABASE STATE**權限傳回 hello 目前資料庫中所有物件的相關資訊。
toogrant hello **VIEW DATABASE STATE**權限 tooa 特定資料庫使用者，執行下列查詢的 hello:

```GRANT VIEW DATABASE STATE toodatabase_user; ```

在內部部署 SQL Server 的執行個體中，動態管理檢視會傳回伺服器狀態資訊。 在 SQL Database 中，僅會傳回與您目前的邏輯資料庫相關的資訊。

## <a name="calculating-database-size"></a>正在計算資料庫大小
hello 下列查詢會傳回 hello 您的資料庫大小 （以 mb 為單位）：

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

hello 下列查詢會傳回 hello 大小 （以 mb 為單位） 的個別物件的資料庫中：

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>監視連線
您可以使用 hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx)檢視 tooretrieve hello 所建立的連線 tooa 特定 Azure SQL Database 伺服器和每個連接 hello 詳細資料資訊。 此外，hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx)檢視擷取所有作用中使用者連接和內部工作的相關資訊時非常有用。
hello 下列查詢會擷取 hello 目前連接的詳細資訊：

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> 當執行 hello **sys.dm_exec_requests**和**sys.dm_exec_sessions 檢視**，如果您有**VIEW DATABASE STATE**權限在 hello 資料庫，您會看到所有執行hello 資料庫上的工作階段否則，您看到只有 hello 目前工作階段。
> 
> 

## <a name="monitoring-query-performance"></a>監視查詢效能
速度慢或長時間執行的查詢可能會耗用大量系統資源。 本節示範如何 toouse 動態管理檢視表 toodetect 幾個常見的查詢效能問題。 如需疑難排解，較舊的但仍有幫助參考為 hello[效能問題的疑難排解 SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) Microsoft TechNet 上的發行項。

### <a name="finding-top-n-queries"></a>尋找前 N 個查詢
hello 下列範例會傳回 hello 之前五項查詢的平均 CPU 時間的相關資訊。 這個範例會彙總根據查詢雜湊，tootheir hello 查詢，以便依據累計資源耗用量分組邏輯對等查詢。

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a>監視封鎖的查詢
較慢或長時間執行的查詢可以參與 tooexcessive 資源耗用量，和會封鎖查詢的 hello 後果。 hello 封鎖的 hello 原因可能是應用程式設計不良，錯誤 hello 缺少有用的索引，查詢計劃，等等。 在您的 Azure SQL Database 中，您可以使用 hello sys.dm_tran_locks 檢視 tooget hello 目前鎖定活動資訊。 如需範例程式碼，請參閱《SQL Server 線上叢書》中的 [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx)。

### <a name="monitoring-query-plans"></a>監視查詢計畫
效率不佳的查詢計畫也可能會增加 CPU 耗用量。 hello 下列範例會使用 hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx)檢視的 toodetermine 哪一個查詢使用 hello 最多的累計 CPU。

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a>另請參閱
[簡介 tooSQL 資料庫](sql-database-technical-overview.md)

