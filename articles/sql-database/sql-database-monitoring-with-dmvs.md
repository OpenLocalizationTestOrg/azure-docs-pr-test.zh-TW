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
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="ca075-103">使用動態管理檢視監視 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ca075-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="ca075-104">Microsoft Azure SQL Database 可讓子集的動態管理檢視 toodiagnose 效能問題可能已封鎖或長時間執行的查詢、 資源瓶頸、 不佳的查詢計畫等所造成。</span><span class="sxs-lookup"><span data-stu-id="ca075-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="ca075-105">此主題提供有關如何使用動態管理檢視 toodetect 常見效能問題。</span><span class="sxs-lookup"><span data-stu-id="ca075-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="ca075-106">SQL Database 部分支援動態管理檢視的三個類別目錄：</span><span class="sxs-lookup"><span data-stu-id="ca075-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="ca075-107">資料庫相關的動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="ca075-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="ca075-108">執行相關的動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="ca075-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="ca075-109">交易相關的動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="ca075-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="ca075-110">如需動態管理檢視的詳細資訊，請參閱《SQL Server 線上叢書》中的 [動態管理檢視和函數 (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ca075-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="ca075-111">權限</span><span class="sxs-lookup"><span data-stu-id="ca075-111">Permissions</span></span>
<span data-ttu-id="ca075-112">在 SQL Database 中，查詢動態管理檢視需要 **VIEW DATABASE STATE** 權限。</span><span class="sxs-lookup"><span data-stu-id="ca075-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="ca075-113">hello **VIEW DATABASE STATE**權限傳回 hello 目前資料庫中所有物件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ca075-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="ca075-114">toogrant hello **VIEW DATABASE STATE**權限 tooa 特定資料庫使用者，執行下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca075-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="ca075-115">在內部部署 SQL Server 的執行個體中，動態管理檢視會傳回伺服器狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="ca075-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="ca075-116">在 SQL Database 中，僅會傳回與您目前的邏輯資料庫相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="ca075-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="ca075-117">正在計算資料庫大小</span><span class="sxs-lookup"><span data-stu-id="ca075-117">Calculating database size</span></span>
<span data-ttu-id="ca075-118">hello 下列查詢會傳回 hello 您的資料庫大小 （以 mb 為單位）：</span><span class="sxs-lookup"><span data-stu-id="ca075-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="ca075-119">hello 下列查詢會傳回 hello 大小 （以 mb 為單位） 的個別物件的資料庫中：</span><span class="sxs-lookup"><span data-stu-id="ca075-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="ca075-120">監視連線</span><span class="sxs-lookup"><span data-stu-id="ca075-120">Monitoring connections</span></span>
<span data-ttu-id="ca075-121">您可以使用 hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx)檢視 tooretrieve hello 所建立的連線 tooa 特定 Azure SQL Database 伺服器和每個連接 hello 詳細資料資訊。</span><span class="sxs-lookup"><span data-stu-id="ca075-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="ca075-122">此外，hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx)檢視擷取所有作用中使用者連接和內部工作的相關資訊時非常有用。</span><span class="sxs-lookup"><span data-stu-id="ca075-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="ca075-123">hello 下列查詢會擷取 hello 目前連接的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="ca075-123">hello following query retrieves information on hello current connection:</span></span>

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
> <span data-ttu-id="ca075-124">當執行 hello **sys.dm_exec_requests**和**sys.dm_exec_sessions 檢視**，如果您有**VIEW DATABASE STATE**權限在 hello 資料庫，您會看到所有執行hello 資料庫上的工作階段否則，您看到只有 hello 目前工作階段。</span><span class="sxs-lookup"><span data-stu-id="ca075-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="ca075-125">監視查詢效能</span><span class="sxs-lookup"><span data-stu-id="ca075-125">Monitoring query performance</span></span>
<span data-ttu-id="ca075-126">速度慢或長時間執行的查詢可能會耗用大量系統資源。</span><span class="sxs-lookup"><span data-stu-id="ca075-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="ca075-127">本節示範如何 toouse 動態管理檢視表 toodetect 幾個常見的查詢效能問題。</span><span class="sxs-lookup"><span data-stu-id="ca075-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="ca075-128">如需疑難排解，較舊的但仍有幫助參考為 hello[效能問題的疑難排解 SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) Microsoft TechNet 上的發行項。</span><span class="sxs-lookup"><span data-stu-id="ca075-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="ca075-129">尋找前 N 個查詢</span><span class="sxs-lookup"><span data-stu-id="ca075-129">Finding top N queries</span></span>
<span data-ttu-id="ca075-130">hello 下列範例會傳回 hello 之前五項查詢的平均 CPU 時間的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ca075-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="ca075-131">這個範例會彙總根據查詢雜湊，tootheir hello 查詢，以便依據累計資源耗用量分組邏輯對等查詢。</span><span class="sxs-lookup"><span data-stu-id="ca075-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="ca075-132">監視封鎖的查詢</span><span class="sxs-lookup"><span data-stu-id="ca075-132">Monitoring blocked queries</span></span>
<span data-ttu-id="ca075-133">較慢或長時間執行的查詢可以參與 tooexcessive 資源耗用量，和會封鎖查詢的 hello 後果。</span><span class="sxs-lookup"><span data-stu-id="ca075-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="ca075-134">hello 封鎖的 hello 原因可能是應用程式設計不良，錯誤 hello 缺少有用的索引，查詢計劃，等等。</span><span class="sxs-lookup"><span data-stu-id="ca075-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="ca075-135">在您的 Azure SQL Database 中，您可以使用 hello sys.dm_tran_locks 檢視 tooget hello 目前鎖定活動資訊。</span><span class="sxs-lookup"><span data-stu-id="ca075-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="ca075-136">如需範例程式碼，請參閱《SQL Server 線上叢書》中的 [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ca075-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="ca075-137">監視查詢計畫</span><span class="sxs-lookup"><span data-stu-id="ca075-137">Monitoring query plans</span></span>
<span data-ttu-id="ca075-138">效率不佳的查詢計畫也可能會增加 CPU 耗用量。</span><span class="sxs-lookup"><span data-stu-id="ca075-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="ca075-139">hello 下列範例會使用 hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx)檢視的 toodetermine 哪一個查詢使用 hello 最多的累計 CPU。</span><span class="sxs-lookup"><span data-stu-id="ca075-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="ca075-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ca075-140">See also</span></span>
[<span data-ttu-id="ca075-141">簡介 tooSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="ca075-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

