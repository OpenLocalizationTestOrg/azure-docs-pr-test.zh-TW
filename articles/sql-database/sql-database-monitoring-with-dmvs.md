---
title: "使用動態管理檢視監視 Azure SQL Database | Microsoft Docs"
description: "了解如何使用動態管理檢視監視 Microsoft Azure SQL Database 來偵測和診斷常見的效能問題。"
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
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="ad7ca-103">使用動態管理檢視監視 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ad7ca-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="ad7ca-104">Microsoft Azure SQL Database 可使用動態管理檢視的子集來診斷可能因為封鎖或長時間執行的查詢、資源瓶頸、不佳的查詢計畫等等所造成的效能問題。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="ad7ca-105">本主題提供有關如何使用動態管理檢視來偵測常見效能問題的資訊。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="ad7ca-106">SQL Database 部分支援動態管理檢視的三個類別目錄：</span><span class="sxs-lookup"><span data-stu-id="ad7ca-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="ad7ca-107">資料庫相關的動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="ad7ca-108">執行相關的動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="ad7ca-109">交易相關的動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="ad7ca-110">如需動態管理檢視的詳細資訊，請參閱《SQL Server 線上叢書》中的 [動態管理檢視和函數 (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="ad7ca-111">權限</span><span class="sxs-lookup"><span data-stu-id="ad7ca-111">Permissions</span></span>
<span data-ttu-id="ad7ca-112">在 SQL Database 中，查詢動態管理檢視需要 **VIEW DATABASE STATE** 權限。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="ad7ca-113">**VIEW DATABASE STATE** 權限會傳回目前資料庫中所有物件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="ad7ca-114">若要授與 **VIEW DATABASE STATE** 權限給特定的資料庫使用者，請執行下列查詢：</span><span class="sxs-lookup"><span data-stu-id="ad7ca-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="ad7ca-115">在內部部署 SQL Server 的執行個體中，動態管理檢視會傳回伺服器狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="ad7ca-116">在 SQL Database 中，僅會傳回與您目前的邏輯資料庫相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="ad7ca-117">正在計算資料庫大小</span><span class="sxs-lookup"><span data-stu-id="ad7ca-117">Calculating database size</span></span>
<span data-ttu-id="ad7ca-118">下列查詢會傳回資料庫的大小 (以 MB 為單位)：</span><span class="sxs-lookup"><span data-stu-id="ad7ca-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="ad7ca-119">下列查詢會傳回您資料庫中個別物件的大小 (以 MB 為單位)：</span><span class="sxs-lookup"><span data-stu-id="ad7ca-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="ad7ca-120">監視連線</span><span class="sxs-lookup"><span data-stu-id="ad7ca-120">Monitoring connections</span></span>
<span data-ttu-id="ad7ca-121">您可以使用 [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) 檢視，擷取與特定 Azure SQL Database 伺服器建立之連接和每個連接之詳細資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="ad7ca-122">此外，[sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) 檢視有助於擷取所有作用中使用者的連接資訊和內部工作。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="ad7ca-123">下列查詢可擷取目前的連接資訊：</span><span class="sxs-lookup"><span data-stu-id="ad7ca-123">The following query retrieves information on the current connection:</span></span>

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
> <span data-ttu-id="ad7ca-124">執行 **sys.dm_exec_requests** 和 **sys.dm_exec_sessions views** 時，如果您具備資料庫的 **VIEW DATABASE STATE** 權限，您就會看到該資料庫上所有正在執行的工作階段；否則您只會看到目前的工作階段。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="ad7ca-125">監視查詢效能</span><span class="sxs-lookup"><span data-stu-id="ad7ca-125">Monitoring query performance</span></span>
<span data-ttu-id="ad7ca-126">速度慢或長時間執行的查詢可能會耗用大量系統資源。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="ad7ca-127">本節示範如何使用動態管理檢視偵測幾個常見的查詢效能問題。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="ad7ca-128">在 Microsoft TechNet 上的文章 [疑難排解 SQL Server 2008 的效能問題](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) 雖然較舊，但仍是針對疑難排解相當有用的參考資料。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="ad7ca-129">尋找前 N 個查詢</span><span class="sxs-lookup"><span data-stu-id="ad7ca-129">Finding top N queries</span></span>
<span data-ttu-id="ad7ca-130">下列範例會傳回以平均 CPU 時間排名的前五個查詢的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="ad7ca-131">此範例會根據查詢雜湊來彙總查詢，使在邏輯上等同的查詢依其累積資源耗用量進行分組。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="ad7ca-132">監視封鎖的查詢</span><span class="sxs-lookup"><span data-stu-id="ad7ca-132">Monitoring blocked queries</span></span>
<span data-ttu-id="ad7ca-133">速度慢或長時間執行的查詢會造成過度的資源耗用，並且會導致封鎖查詢的後果。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="ad7ca-134">導致封鎖的原因可能是不佳的應用程式設計、不良的查詢計畫、缺乏有用的索引等等。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="ad7ca-135">您可以使用 sys.dm_tran_locks 檢視，取得在您的 Azure SQL Database 中目前正鎖定之活動的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="ad7ca-136">如需範例程式碼，請參閱《SQL Server 線上叢書》中的 [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="ad7ca-137">監視查詢計畫</span><span class="sxs-lookup"><span data-stu-id="ad7ca-137">Monitoring query plans</span></span>
<span data-ttu-id="ad7ca-138">效率不佳的查詢計畫也可能會增加 CPU 耗用量。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="ad7ca-139">下列範例使用 [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) 檢視來判斷哪一個查詢使用最多的累計 CPU。</span><span class="sxs-lookup"><span data-stu-id="ad7ca-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="ad7ca-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ad7ca-140">See also</span></span>
[<span data-ttu-id="ad7ca-141">SQL Database 簡介</span><span class="sxs-lookup"><span data-stu-id="ad7ca-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

