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
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="f0287-103">使用 DMV 監視工作負載</span><span class="sxs-lookup"><span data-stu-id="f0287-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="f0287-104">本文說明如何 toouse 動態管理檢視 (Dmv) toomonitor 您的工作負載，並調查在 Azure SQL 資料倉儲中的查詢執行。</span><span class="sxs-lookup"><span data-stu-id="f0287-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="f0287-105">權限</span><span class="sxs-lookup"><span data-stu-id="f0287-105">Permissions</span></span>
<span data-ttu-id="f0287-106">tooquery hello Dmv 在本文中，您需要 VIEW DATABASE STATE 或 CONTROL 權限。</span><span class="sxs-lookup"><span data-stu-id="f0287-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="f0287-107">通常，授與的 VIEW DATABASE STATE 是慣用的 hello 權限，因為它是更具限制性。</span><span class="sxs-lookup"><span data-stu-id="f0287-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="f0287-108">監視連接</span><span class="sxs-lookup"><span data-stu-id="f0287-108">Monitor connections</span></span>
<span data-ttu-id="f0287-109">所有登入 tooSQL 資料倉儲會記錄太[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions]。</span><span class="sxs-lookup"><span data-stu-id="f0287-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="f0287-110">此 DMV 包含 hello 上次 10000 的登入。</span><span class="sxs-lookup"><span data-stu-id="f0287-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="f0287-111">hello session_id hello 主索引鍵，並依序指派給每個新的登入。</span><span class="sxs-lookup"><span data-stu-id="f0287-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="f0287-112">監視查詢執行</span><span class="sxs-lookup"><span data-stu-id="f0287-112">Monitor query execution</span></span>
<span data-ttu-id="f0287-113">SQL 資料倉儲上執行的所有查詢會都記錄太[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests]。</span><span class="sxs-lookup"><span data-stu-id="f0287-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="f0287-114">此 DMV 包含 hello 上次執行的查詢 10,000。</span><span class="sxs-lookup"><span data-stu-id="f0287-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="f0287-115">hello request_id 唯一識別每個查詢，而且 hello 針對這個 DMV 的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f0287-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="f0287-116">hello request_id 依序指派給每個新的查詢，並加上 //WWW.AMAZON.COM/APPLIED-MICROSOFT-SERVER-ANALYSIS-SERVICES/DP/0976635356/REF，代表查詢的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f0287-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="f0287-117">查詢此 DMV 來尋找指定的 session_id，即會顯示指定登入的所有查詢。</span><span class="sxs-lookup"><span data-stu-id="f0287-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="f0287-118">預存程序會使用多個要求 ID。</span><span class="sxs-lookup"><span data-stu-id="f0287-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="f0287-119">要求 ID 是依序指派。</span><span class="sxs-lookup"><span data-stu-id="f0287-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="f0287-120">以下是步驟 toofollow tooinvestigate 查詢執行計畫和特定查詢的時間。</span><span class="sxs-lookup"><span data-stu-id="f0287-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="f0287-121">步驟 1： 識別您想 tooinvestigate hello 查詢</span><span class="sxs-lookup"><span data-stu-id="f0287-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
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

<span data-ttu-id="f0287-122">從上述查詢結果的 hello**注意 hello 要求識別碼**希望 tooinvestigate hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="f0287-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="f0287-123">查詢中 hello **Suspended**狀態因為 tooconcurrency 限制加入佇列。</span><span class="sxs-lookup"><span data-stu-id="f0287-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="f0287-124">這些查詢也會出現在類型為 UserConcurrencyResourceType hello sys.dm_pdw_waits 等候查詢。</span><span class="sxs-lookup"><span data-stu-id="f0287-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="f0287-125">如需並行限制的詳細資料，請參閱[並行和工作負載管理][Concurrency and workload management]。</span><span class="sxs-lookup"><span data-stu-id="f0287-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="f0287-126">查詢也會因其他原因 (例如物件鎖定) 而等候。</span><span class="sxs-lookup"><span data-stu-id="f0287-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="f0287-127">如果您的查詢正在等候資源，請參閱本文稍後的[檢查正在等候資源的查詢][Investigating queries waiting for resources]。</span><span class="sxs-lookup"><span data-stu-id="f0287-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="f0287-128">hello sys.dm_pdw_exec_requests 資料表，請使用中的查詢 toosimplify hello 查閱[標籤][ LABEL] tooassign 可以查閱 hello sys.dm_pdw_exec_requests 檢視中的註解 tooyour 查詢。</span><span class="sxs-lookup"><span data-stu-id="f0287-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="f0287-129">步驟 2： 調查 hello 查詢計劃</span><span class="sxs-lookup"><span data-stu-id="f0287-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="f0287-130">使用 hello 要求識別碼 tooretrieve hello 查詢的分散式的 SQL (DSQL) 計劃從[sys.dm_pdw_request_steps][sys.dm_pdw_request_steps]。</span><span class="sxs-lookup"><span data-stu-id="f0287-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="f0287-131">當 DSQL 計劃所花的時間超出預期時，hello 原因可能是複雜的計劃與許多 DSQL 步驟或只在一個步驟，花費的時間過長。</span><span class="sxs-lookup"><span data-stu-id="f0287-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="f0287-132">如果 hello 計劃使用數種移動作業的許多步驟，請考慮最佳化的資料表散發 tooreduce 資料移動。</span><span class="sxs-lookup"><span data-stu-id="f0287-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="f0287-133">hello[資料表散發][ Table distribution]篇文章說明為何必須是移動的 toosolve 查詢資料，並說明某些發佈策略 toominimize 資料移動。</span><span class="sxs-lookup"><span data-stu-id="f0287-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="f0287-134">tooinvestigate 取得進一步的詳細資料的單一步驟中，hello *operation_type*資料行的 hello 長時間執行的查詢步驟並注意 hello**步驟索引**:</span><span class="sxs-lookup"><span data-stu-id="f0287-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="f0287-135">針對下列 **SQL 作業**繼續執行步驟 3a：OnOperation、RemoteOperation、ReturnOperation。</span><span class="sxs-lookup"><span data-stu-id="f0287-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="f0287-136">針對下列 **資料移動作業**繼續執行步驟 3b：ShuffleMoveOperation、BroadcastMoveOperation、TrimMoveOperation、PartitionMoveOperation、MoveOperation、CopyOperation。</span><span class="sxs-lookup"><span data-stu-id="f0287-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="f0287-137">步驟 3a: hello 散發資料庫上調查 SQL</span><span class="sxs-lookup"><span data-stu-id="f0287-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="f0287-138">使用要求識別碼 hello 和 hello 步驟索引 tooretrieve 詳細資料，從[sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests]，其中包含所有 hello 的執行資訊 hello 查詢步驟的散發資料庫。</span><span class="sxs-lookup"><span data-stu-id="f0287-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="f0287-139">當執行 hello 查詢步驟時， [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN]可以是使用的 tooretrieve hello SQL Server 估計計劃的 hello hello 步驟執行在特定的 SQL Server 計畫快取發佈。</span><span class="sxs-lookup"><span data-stu-id="f0287-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="f0287-140">步驟 3b： 調查 hello 散發資料庫上的資料移動</span><span class="sxs-lookup"><span data-stu-id="f0287-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="f0287-141">使用要求識別碼 hello 和 hello 資料移動步驟，從每個通訊群組上執行的步驟索引 tooretrieve 資訊[sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers]。</span><span class="sxs-lookup"><span data-stu-id="f0287-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="f0287-142">檢查 hello *total_elapsed_time*資料行 toosee 如果特定的分佈耗費時間大幅多於移動資料的其他人。</span><span class="sxs-lookup"><span data-stu-id="f0287-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="f0287-143">Hello 長時間執行的散發，請檢查 hello *rows_processed*如果 hello 數目的資料列已從該發佈移遠比其他資料行 toosee。</span><span class="sxs-lookup"><span data-stu-id="f0287-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="f0287-144">若是如此，這可能表示基礎資料的扭曲。</span><span class="sxs-lookup"><span data-stu-id="f0287-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="f0287-145">如果 hello 查詢正在執行， [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN]可以是使用的 tooretrieve hello SQL Server 估計計劃的 hello hello 目前執行 SQL 步驟內特定的 SQL Server 計畫快取發佈。</span><span class="sxs-lookup"><span data-stu-id="f0287-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="f0287-146">監視等候中的查詢</span><span class="sxs-lookup"><span data-stu-id="f0287-146">Monitor waiting queries</span></span>
<span data-ttu-id="f0287-147">如果您發現您的查詢無法達成的進度因為它正在等待資源時，以下是查詢正在等候會顯示所有 hello 資源的查詢。</span><span class="sxs-lookup"><span data-stu-id="f0287-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

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

<span data-ttu-id="f0287-148">如果 hello 查詢正在等候資源的其他查詢，則將 hello 狀態**AcquireResources**。</span><span class="sxs-lookup"><span data-stu-id="f0287-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="f0287-149">如果 hello 查詢具有所有所需的 hello 資源，則將 hello 狀態**Granted**。</span><span class="sxs-lookup"><span data-stu-id="f0287-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="f0287-150">監視 tempdb</span><span class="sxs-lookup"><span data-stu-id="f0287-150">Monitor tempdb</span></span>
<span data-ttu-id="f0287-151">高 tempdb 使用量可以 hello 效能變慢，記憶體不足問題根本原因。</span><span class="sxs-lookup"><span data-stu-id="f0287-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="f0287-152">請先檢查是否有資料扭曲或較差的品質的資料列群組以及採取 hello 適當的動作。</span><span class="sxs-lookup"><span data-stu-id="f0287-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="f0287-153">如果您在查詢執行期間發現 tempdb 達到其上限，請考慮調整您的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="f0287-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="f0287-154">hello 下列程式碼說明如何 tooidentify tempdb 使用量，每個查詢，每個節點上。</span><span class="sxs-lookup"><span data-stu-id="f0287-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="f0287-155">建立下列的 sys.dm_pdw_sql_requests 檢視 tooassociate hello 適當的節點識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="f0287-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="f0287-156">這將會啟用您 tooleverage 其他傳遞 Dmv，並聯結這些資料表與 sys.dm_pdw_sql_requests。</span><span class="sxs-lookup"><span data-stu-id="f0287-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

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
<span data-ttu-id="f0287-157">執行下列查詢 toomonitor tempdb hello:</span><span class="sxs-lookup"><span data-stu-id="f0287-157">Run hello following query toomonitor tempdb:</span></span>

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
## <a name="monitor-memory"></a><span data-ttu-id="f0287-158">監視記憶體</span><span class="sxs-lookup"><span data-stu-id="f0287-158">Monitor memory</span></span>

<span data-ttu-id="f0287-159">記憶體可能 hello 效能變慢，記憶體不足問題根本原因。</span><span class="sxs-lookup"><span data-stu-id="f0287-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="f0287-160">請先檢查是否有資料扭曲或較差的品質的資料列群組以及採取 hello 適當的動作。</span><span class="sxs-lookup"><span data-stu-id="f0287-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="f0287-161">如果您在查詢執行期間發現 SQL Server 記憶體使用量達到其上限，請考慮調整您的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="f0287-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="f0287-162">hello，下列查詢會傳回 SQL Server 記憶體使用量和記憶體不足的壓力每個節點：</span><span class="sxs-lookup"><span data-stu-id="f0287-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
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
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="f0287-163">監視交易記錄大小</span><span class="sxs-lookup"><span data-stu-id="f0287-163">Monitor transaction log size</span></span>
<span data-ttu-id="f0287-164">hello 下列查詢會傳回 hello 交易記錄大小在每個發佈。</span><span class="sxs-lookup"><span data-stu-id="f0287-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="f0287-165">請如果您有資料扭曲或較差的品質的資料列群組，並採取 hello 適當的動作，檢查。</span><span class="sxs-lookup"><span data-stu-id="f0287-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="f0287-166">如果其中一個 hello 記錄檔達到 160 GB，您應該考慮您的執行個體向上擴充或限制您交易的大小。</span><span class="sxs-lookup"><span data-stu-id="f0287-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
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
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="f0287-167">監視交易記錄復原</span><span class="sxs-lookup"><span data-stu-id="f0287-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="f0287-168">如果您的查詢失敗，或花很長的時間 tooproceed，您可以檢查和監視您如有任何交易回復。</span><span class="sxs-lookup"><span data-stu-id="f0287-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="f0287-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0287-169">Next steps</span></span>
<span data-ttu-id="f0287-170">請參閱[系統檢視][System views]以取得 DMV 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f0287-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="f0287-171">請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse best practices]以取得最佳做法的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f0287-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

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
