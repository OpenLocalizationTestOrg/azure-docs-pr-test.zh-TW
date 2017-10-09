---
title: "aaaMonitor 您的工作負載使用 Dmv |Microsoft 文件"
description: "深入了解如何 toomonitor 您使用 Dmv 的工作負載。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a>使用 DMV 監視工作負載
本文說明如何 toouse 動態管理檢視 (Dmv) toomonitor 您的工作負載，並調查在 Azure SQL 資料倉儲中的查詢執行。

## <a name="permissions"></a>權限
tooquery hello Dmv 在本文中，您需要 VIEW DATABASE STATE 或 CONTROL 權限。 通常，授與的 VIEW DATABASE STATE 是慣用的 hello 權限，因為它是更具限制性。

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a>監視連接
所有登入 tooSQL 資料倉儲會記錄太[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions]。  此 DMV 包含 hello 上次 10000 的登入。  hello session_id hello 主索引鍵，並依序指派給每個新的登入。

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a>監視查詢執行
SQL 資料倉儲上執行的所有查詢會都記錄太[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests]。  此 DMV 包含 hello 上次執行的查詢 10,000。  hello request_id 唯一識別每個查詢，而且 hello 針對這個 DMV 的主索引鍵。  hello request_id 依序指派給每個新的查詢，並加上 //WWW.AMAZON.COM/APPLIED-MICROSOFT-SERVER-ANALYSIS-SERVICES/DP/0976635356/REF，代表查詢的識別碼。  查詢此 DMV 來尋找指定的 session_id，即會顯示指定登入的所有查詢。

> [!NOTE]
> 預存程序會使用多個要求 ID。  要求 ID 是依序指派。 
> 
> 

以下是步驟 toofollow tooinvestigate 查詢執行計畫和特定查詢的時間。

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a>步驟 1： 識別您想 tooinvestigate hello 查詢
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

從上述查詢結果的 hello**注意 hello 要求識別碼**希望 tooinvestigate hello 查詢。

查詢中 hello **Suspended**狀態因為 tooconcurrency 限制加入佇列。 這些查詢也會出現在類型為 UserConcurrencyResourceType hello sys.dm_pdw_waits 等候查詢。 如需並行限制的詳細資料，請參閱[並行和工作負載管理][Concurrency and workload management]。 查詢也會因其他原因 (例如物件鎖定) 而等候。  如果您的查詢正在等候資源，請參閱本文稍後的[檢查正在等候資源的查詢][Investigating queries waiting for resources]。

hello sys.dm_pdw_exec_requests 資料表，請使用中的查詢 toosimplify hello 查閱[標籤][ LABEL] tooassign 可以查閱 hello sys.dm_pdw_exec_requests 檢視中的註解 tooyour 查詢。

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a>步驟 2： 調查 hello 查詢計劃
使用 hello 要求識別碼 tooretrieve hello 查詢的分散式的 SQL (DSQL) 計劃從[sys.dm_pdw_request_steps][sys.dm_pdw_request_steps]。

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

當 DSQL 計劃所花的時間超出預期時，hello 原因可能是複雜的計劃與許多 DSQL 步驟或只在一個步驟，花費的時間過長。  如果 hello 計劃使用數種移動作業的許多步驟，請考慮最佳化的資料表散發 tooreduce 資料移動。 hello[資料表散發][ Table distribution]篇文章說明為何必須是移動的 toosolve 查詢資料，並說明某些發佈策略 toominimize 資料移動。

tooinvestigate 取得進一步的詳細資料的單一步驟中，hello *operation_type*資料行的 hello 長時間執行的查詢步驟並注意 hello**步驟索引**:

* 針對下列 **SQL 作業**繼續執行步驟 3a：OnOperation、RemoteOperation、ReturnOperation。
* 針對下列 **資料移動作業**繼續執行步驟 3b：ShuffleMoveOperation、BroadcastMoveOperation、TrimMoveOperation、PartitionMoveOperation、MoveOperation、CopyOperation。

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a>步驟 3a: hello 散發資料庫上調查 SQL
使用要求識別碼 hello 和 hello 步驟索引 tooretrieve 詳細資料，從[sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests]，其中包含所有 hello 的執行資訊 hello 查詢步驟的散發資料庫。

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

當執行 hello 查詢步驟時， [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN]可以是使用的 tooretrieve hello SQL Server 估計計劃的 hello hello 步驟執行在特定的 SQL Server 計畫快取發佈。

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a>步驟 3b： 調查 hello 散發資料庫上的資料移動
使用要求識別碼 hello 和 hello 資料移動步驟，從每個通訊群組上執行的步驟索引 tooretrieve 資訊[sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers]。

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* 檢查 hello *total_elapsed_time*資料行 toosee 如果特定的分佈耗費時間大幅多於移動資料的其他人。
* Hello 長時間執行的散發，請檢查 hello *rows_processed*如果 hello 數目的資料列已從該發佈移遠比其他資料行 toosee。 若是如此，這可能表示基礎資料的扭曲。

如果 hello 查詢正在執行， [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN]可以是使用的 tooretrieve hello SQL Server 估計計劃的 hello hello 目前執行 SQL 步驟內特定的 SQL Server 計畫快取發佈。

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a>監視等候中的查詢
如果您發現您的查詢無法達成的進度因為它正在等待資源時，以下是查詢正在等候會顯示所有 hello 資源的查詢。

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

如果 hello 查詢正在等候資源的其他查詢，則將 hello 狀態**AcquireResources**。  如果 hello 查詢具有所有所需的 hello 資源，則將 hello 狀態**Granted**。

## <a name="monitor-tempdb"></a>監視 tempdb
高 tempdb 使用量可以 hello 效能變慢，記憶體不足問題根本原因。 請先檢查是否有資料扭曲或較差的品質的資料列群組以及採取 hello 適當的動作。 如果您在查詢執行期間發現 tempdb 達到其上限，請考慮調整您的資料倉儲。 hello 下列程式碼說明如何 tooidentify tempdb 使用量，每個查詢，每個節點上。 

建立下列的 sys.dm_pdw_sql_requests 檢視 tooassociate hello 適當的節點識別碼 hello。 這將會啟用您 tooleverage 其他傳遞 Dmv，並聯結這些資料表與 sys.dm_pdw_sql_requests。

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
執行下列查詢 toomonitor tempdb hello:

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a>監視記憶體

記憶體可能 hello 效能變慢，記憶體不足問題根本原因。 請先檢查是否有資料扭曲或較差的品質的資料列群組以及採取 hello 適當的動作。 如果您在查詢執行期間發現 SQL Server 記憶體使用量達到其上限，請考慮調整您的資料倉儲。

hello，下列查詢會傳回 SQL Server 記憶體使用量和記憶體不足的壓力每個節點： 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a>監視交易記錄大小
hello 下列查詢會傳回 hello 交易記錄大小在每個發佈。 請如果您有資料扭曲或較差的品質的資料列群組，並採取 hello 適當的動作，檢查。 如果其中一個 hello 記錄檔達到 160 GB，您應該考慮您的執行個體向上擴充或限制您交易的大小。 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a>監視交易記錄復原
如果您的查詢失敗，或花很長的時間 tooproceed，您可以檢查和監視您如有任何交易回復。
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a>後續步驟
請參閱[系統檢視][System views]以取得 DMV 的詳細資訊。
請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse best practices]以取得最佳做法的詳細資訊

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
