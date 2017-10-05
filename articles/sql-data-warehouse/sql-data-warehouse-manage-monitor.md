---
title: "使用 DMV 監視工作負載 | Microsoft Docs"
description: "了解如何使用 DMV 監視工作負載。"
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
ms.openlocfilehash: 7ce6c2cdf1e28852da536414533ccdcdaeb437e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="eff43-103">使用 DMV 監視工作負載</span><span class="sxs-lookup"><span data-stu-id="eff43-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="eff43-104">本文說明如何使用動態管理檢視 (DMV)，在 Azure SQL 資料倉儲中監視工作負載及調查查詢執行。</span><span class="sxs-lookup"><span data-stu-id="eff43-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="eff43-105">權限</span><span class="sxs-lookup"><span data-stu-id="eff43-105">Permissions</span></span>
<span data-ttu-id="eff43-106">若要查詢此文章中的 DMV，您需要「檢視資料庫狀態」或「控制」權限。</span><span class="sxs-lookup"><span data-stu-id="eff43-106">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="eff43-107">通常授與「檢視資料庫狀態」是慣用的權限，因為它較具限制性。</span><span class="sxs-lookup"><span data-stu-id="eff43-107">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE TO myuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="eff43-108">監視連接</span><span class="sxs-lookup"><span data-stu-id="eff43-108">Monitor connections</span></span>
<span data-ttu-id="eff43-109">所有針對 SQL 資料倉儲的登入都會記錄到 [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions]。</span><span class="sxs-lookup"><span data-stu-id="eff43-109">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="eff43-110">這個 DMV 會包含最後 10,000 筆登入。</span><span class="sxs-lookup"><span data-stu-id="eff43-110">This DMV contains the last 10,000 logins.</span></span>  <span data-ttu-id="eff43-111">Session_id 是主索引鍵，並依序指派給每個新的登入。</span><span class="sxs-lookup"><span data-stu-id="eff43-111">The session_id is the primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="eff43-112">監視查詢執行</span><span class="sxs-lookup"><span data-stu-id="eff43-112">Monitor query execution</span></span>
<span data-ttu-id="eff43-113">SQL 資料倉儲上所執行的所有查詢會都記錄到 [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests]。</span><span class="sxs-lookup"><span data-stu-id="eff43-113">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="eff43-114">這個 DMV 會包含最後 10,000 筆執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="eff43-114">This DMV contains the last 10,000 queries executed.</span></span>  <span data-ttu-id="eff43-115">Request_id 可唯一識別每筆查詢，而且是此 DMV 的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="eff43-115">The request_id uniquely identifies each query and is the primary key for this DMV.</span></span>  <span data-ttu-id="eff43-116">Request_id 會依序指派給每筆新查詢，並加上 QID 代表查詢識別碼。</span><span class="sxs-lookup"><span data-stu-id="eff43-116">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="eff43-117">查詢此 DMV 來尋找指定的 session_id，即會顯示指定登入的所有查詢。</span><span class="sxs-lookup"><span data-stu-id="eff43-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="eff43-118">預存程序會使用多個要求 ID。</span><span class="sxs-lookup"><span data-stu-id="eff43-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="eff43-119">要求 ID 是依序指派。</span><span class="sxs-lookup"><span data-stu-id="eff43-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="eff43-120">請遵循以下步驟來調查特定查詢的查詢執行計畫和時間。</span><span class="sxs-lookup"><span data-stu-id="eff43-120">Here are steps to follow to investigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-the-query-you-wish-to-investigate"></a><span data-ttu-id="eff43-121">步驟 1︰識別您想要調查的查詢</span><span class="sxs-lookup"><span data-stu-id="eff43-121">STEP 1: Identify the query you wish to investigate</span></span>
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

-- Find a query with the Label 'My Query'
-- Use brackets when querying the label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="eff43-122">從前述的查詢結果中，記下您想要調查之查詢的 **要求 ID** 。</span><span class="sxs-lookup"><span data-stu-id="eff43-122">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span></span>

<span data-ttu-id="eff43-123"> 狀態的查詢會因為並行限制而進入佇列。</span><span class="sxs-lookup"><span data-stu-id="eff43-123">Queries in the **Suspended** state are being queued due to concurrency limits.</span></span> <span data-ttu-id="eff43-124">這些查詢也會顯示在 sys.dm_pdw_waits 等候查詢中，類型為 UserConcurrencyResourceType。</span><span class="sxs-lookup"><span data-stu-id="eff43-124">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="eff43-125">如需並行限制的詳細資料，請參閱[並行和工作負載管理][Concurrency and workload management]。</span><span class="sxs-lookup"><span data-stu-id="eff43-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="eff43-126">查詢也會因其他原因 (例如物件鎖定) 而等候。</span><span class="sxs-lookup"><span data-stu-id="eff43-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="eff43-127">如果您的查詢正在等候資源，請參閱本文稍後的[檢查正在等候資源的查詢][Investigating queries waiting for resources]。</span><span class="sxs-lookup"><span data-stu-id="eff43-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="eff43-128">若要簡化在 sys.dm_pdw_exec_requests 資料表中查閱查詢的方式，請使用 [LABEL][LABEL] 來將可在 sys.dm_pdw_exec_requests 檢視中查閱的註解指派給您的查詢。</span><span class="sxs-lookup"><span data-stu-id="eff43-128">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-the-query-plan"></a><span data-ttu-id="eff43-129">步驟 2︰ 調查查詢計劃</span><span class="sxs-lookup"><span data-stu-id="eff43-129">STEP 2: Investigate the query plan</span></span>
<span data-ttu-id="eff43-130">使用要求識別碼，從 [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps] 擷取查詢的分散式 SQL (DSQL) 計畫。</span><span class="sxs-lookup"><span data-stu-id="eff43-130">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find the distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="eff43-131">當 DSQL 計劃所花的時間超出預期時，有可能是含有許多 DSQL 步驟的複雜計劃所導致，或只是某個步驟需要長時間處理。</span><span class="sxs-lookup"><span data-stu-id="eff43-131">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="eff43-132">如果計劃是含有數個移動作業的許多步驟，請考慮最佳化您的資料表散發以減少資料移動。</span><span class="sxs-lookup"><span data-stu-id="eff43-132">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span></span> <span data-ttu-id="eff43-133">[資料表散發][Table distribution]一文說明為何需要移動資料才能解決查詢，並說明最小化資料移動的一些散發策略。</span><span class="sxs-lookup"><span data-stu-id="eff43-133">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span></span>

<span data-ttu-id="eff43-134">進一步調查單一步驟 (長時間執行查詢步驟的 *operation_type* 資料行) 的詳細資料，並且記下**步驟索引**：</span><span class="sxs-lookup"><span data-stu-id="eff43-134">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span></span>

* <span data-ttu-id="eff43-135">針對下列 **SQL 作業**繼續執行步驟 3a：OnOperation、RemoteOperation、ReturnOperation。</span><span class="sxs-lookup"><span data-stu-id="eff43-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="eff43-136">針對下列 **資料移動作業**繼續執行步驟 3b：ShuffleMoveOperation、BroadcastMoveOperation、TrimMoveOperation、PartitionMoveOperation、MoveOperation、CopyOperation。</span><span class="sxs-lookup"><span data-stu-id="eff43-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-the-distributed-databases"></a><span data-ttu-id="eff43-137">步驟 3a︰調查分散式資料庫上的 SQL</span><span class="sxs-lookup"><span data-stu-id="eff43-137">STEP 3a: Investigate SQL on the distributed databases</span></span>
<span data-ttu-id="eff43-138">使用要求識別碼及步驟索引，從 [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests] 擷取詳細資料，其中包含所有分散式資料庫上查詢步驟的執行資訊。</span><span class="sxs-lookup"><span data-stu-id="eff43-138">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span></span>

```sql
-- Find the distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="eff43-139">當查詢步驟正在執行時，可以使用 [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] 針對正在特定散發上執行的步驟，從 SQL Server 計畫快取擷取 SQL Server 預估計畫。</span><span class="sxs-lookup"><span data-stu-id="eff43-139">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span></span>

```sql
-- Find the SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-the-distributed-databases"></a><span data-ttu-id="eff43-140">步驟 3b︰調查分散式資料庫的資料移動</span><span class="sxs-lookup"><span data-stu-id="eff43-140">STEP 3b: Investigate data movement on the distributed databases</span></span>
<span data-ttu-id="eff43-141">使用要求識別碼和步驟索引，從 [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers] 擷取在每個散發上執行之資料移動步驟的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="eff43-141">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find the information about all the workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="eff43-142">檢查 *total_elapsed_time* 資料行，查看是否有特定散發，在資料移動上比其他散發用了更多時間。</span><span class="sxs-lookup"><span data-stu-id="eff43-142">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="eff43-143">如果是長時間執行的散發，請檢查 *rows_processed* 資料行，查看從該散發移動的資料列數是否遠多過其他散發。</span><span class="sxs-lookup"><span data-stu-id="eff43-143">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="eff43-144">若是如此，這可能表示基礎資料的扭曲。</span><span class="sxs-lookup"><span data-stu-id="eff43-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="eff43-145">如果查詢正在執行，可以使用 [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN]，針對特定散發內目前正在執行的 SQL 步驟，從 SQL Server 計畫快取擷取 SQL Server 預估計畫。</span><span class="sxs-lookup"><span data-stu-id="eff43-145">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find the SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="eff43-146">監視等候中的查詢</span><span class="sxs-lookup"><span data-stu-id="eff43-146">Monitor waiting queries</span></span>
<span data-ttu-id="eff43-147">如果您發現您的查詢因為正在等候資源而沒有進度，以下查詢可顯示查詢正在等候的所有資源。</span><span class="sxs-lookup"><span data-stu-id="eff43-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span></span>

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

<span data-ttu-id="eff43-148">如果查詢正在主動等候另一個查詢的資源，則狀態會是 **AcquireResources**。</span><span class="sxs-lookup"><span data-stu-id="eff43-148">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span></span>  <span data-ttu-id="eff43-149">如果查詢具有全部的所需資源，則狀態會是 **Granted**。</span><span class="sxs-lookup"><span data-stu-id="eff43-149">If the query has all the required resources, then the state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="eff43-150">監視 tempdb</span><span class="sxs-lookup"><span data-stu-id="eff43-150">Monitor tempdb</span></span>
<span data-ttu-id="eff43-151">高 tempdb 使用量是效能緩慢及記憶體不足問題的根本原因。</span><span class="sxs-lookup"><span data-stu-id="eff43-151">High tempdb utilization can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="eff43-152">請先檢查是否有資料扭曲或品質低落的資料列群組，並採取適當的動作。</span><span class="sxs-lookup"><span data-stu-id="eff43-152">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="eff43-153">如果您在查詢執行期間發現 tempdb 達到其上限，請考慮調整您的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="eff43-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="eff43-154">以下描述如何識別每個節點上每個查詢的 tempdb 使用量。</span><span class="sxs-lookup"><span data-stu-id="eff43-154">The following describes how to identify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="eff43-155">建立下列檢視，以針對 sys.dm_pdw_sql_requests 建立適當節點識別碼的關聯。</span><span class="sxs-lookup"><span data-stu-id="eff43-155">Create the following view to associate the appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="eff43-156">這可讓您運用其他傳遞 DMV，並將這些資料表與 sys.dm_pdw_sql_requests 聯結。</span><span class="sxs-lookup"><span data-stu-id="eff43-156">This will enable you to leverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with the correct node id
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
<span data-ttu-id="eff43-157">執行下列查詢可監視 tempdb：</span><span class="sxs-lookup"><span data-stu-id="eff43-157">Run the following query to monitor tempdb:</span></span>

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
## <a name="monitor-memory"></a><span data-ttu-id="eff43-158">監視記憶體</span><span class="sxs-lookup"><span data-stu-id="eff43-158">Monitor memory</span></span>

<span data-ttu-id="eff43-159">記憶體是效能緩慢及記憶體不足問題的根本原因。</span><span class="sxs-lookup"><span data-stu-id="eff43-159">Memory can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="eff43-160">請先檢查是否有資料扭曲或品質低落的資料列群組，並採取適當的動作。</span><span class="sxs-lookup"><span data-stu-id="eff43-160">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="eff43-161">如果您在查詢執行期間發現 SQL Server 記憶體使用量達到其上限，請考慮調整您的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="eff43-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="eff43-162">下列查詢會傳回每個節點的 SQL Server 記憶體使用量和記憶體不足壓力：</span><span class="sxs-lookup"><span data-stu-id="eff43-162">The following query returns SQL Server memory usage and memory pressure per node:</span></span>   
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
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="eff43-163">監視交易記錄大小</span><span class="sxs-lookup"><span data-stu-id="eff43-163">Monitor transaction log size</span></span>
<span data-ttu-id="eff43-164">下列查詢會傳回每個發佈上的交易記錄大小。</span><span class="sxs-lookup"><span data-stu-id="eff43-164">The following query returns the transaction log size on each distribution.</span></span> <span data-ttu-id="eff43-165">請檢查是否有資料扭曲或品質低落的資料列群組，並採取適當的動作。</span><span class="sxs-lookup"><span data-stu-id="eff43-165">Please check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="eff43-166">如果其中一個記錄檔達到 160 GB，您應該考慮將您的執行個體相應放大或限制您交易的大小。</span><span class="sxs-lookup"><span data-stu-id="eff43-166">If one of the log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
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
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="eff43-167">監視交易記錄復原</span><span class="sxs-lookup"><span data-stu-id="eff43-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="eff43-168">如果您的查詢失敗或需要長時間才能繼續，您可以檢查及監視是否有任何交易復原。</span><span class="sxs-lookup"><span data-stu-id="eff43-168">If your queries are failing or taking a long time to proceed, you can check and monitor if you have any transactions rolling back.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="eff43-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eff43-169">Next steps</span></span>
<span data-ttu-id="eff43-170">請參閱[系統檢視][System views]以取得 DMV 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="eff43-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="eff43-171">請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse best practices]以取得最佳做法的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="eff43-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

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
