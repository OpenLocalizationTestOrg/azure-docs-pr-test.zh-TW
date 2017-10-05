---
title: "SQL 資料倉儲中的暫存資料表 | Microsoft Docs"
description: "開始使用 Azure SQL 資料倉儲中的暫存資料表。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: fd8c31a727dae3b011aa8294a81f005bad72a278
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="8e89c-103">SQL 資料倉儲中的暫存資料表</span><span class="sxs-lookup"><span data-stu-id="8e89c-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8e89c-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="8e89c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="8e89c-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="8e89c-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="8e89c-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="8e89c-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="8e89c-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="8e89c-107">[Index][Index]</span></span>
> * <span data-ttu-id="8e89c-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="8e89c-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="8e89c-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="8e89c-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="8e89c-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="8e89c-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="8e89c-111">暫存資料表在處理資料時非常有用 - 尤其是具有暫時性中繼結果的轉換期間。</span><span class="sxs-lookup"><span data-stu-id="8e89c-111">Temporary tables are very useful when processing data - especially during transformation where the intermediate results are transient.</span></span> <span data-ttu-id="8e89c-112">在 SQL 資料倉儲中，暫存資料表存在於工作階段層級。</span><span class="sxs-lookup"><span data-stu-id="8e89c-112">In SQL Data Warehouse temporary tables exist at the session level.</span></span>  <span data-ttu-id="8e89c-113">它們只出現在建立它們的工作階段中，工作階段登出時就會自動卸除它們。</span><span class="sxs-lookup"><span data-stu-id="8e89c-113">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="8e89c-114">暫存資料表的結果會寫入至本機，而不是遠端儲存體，這是它的效能優點。</span><span class="sxs-lookup"><span data-stu-id="8e89c-114">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span></span>  <span data-ttu-id="8e89c-115">Azure SQL 資料倉儲中的暫存資料表稍微不同於 Azure SQL Database，因為從工作階段內的任何地方都可存取它們，包括在預存程序的內部和外部。</span><span class="sxs-lookup"><span data-stu-id="8e89c-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="8e89c-116">本文包含使用暫存資料表的基本指引，並強調說明工作階段層級暫存資料表的原則。</span><span class="sxs-lookup"><span data-stu-id="8e89c-116">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span></span> <span data-ttu-id="8e89c-117">使用這份文件中的資訊可協助您將程式碼模組化，以提高程式碼的重複使用性，維護起來更簡單。</span><span class="sxs-lookup"><span data-stu-id="8e89c-117">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="8e89c-118">建立暫存資料表</span><span class="sxs-lookup"><span data-stu-id="8e89c-118">Create a temporary table</span></span>
<span data-ttu-id="8e89c-119">建立暫存資料表時只是在資料表名稱前面加上 `#`。</span><span class="sxs-lookup"><span data-stu-id="8e89c-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="8e89c-120">例如：</span><span class="sxs-lookup"><span data-stu-id="8e89c-120">For example:</span></span>

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

<span data-ttu-id="8e89c-121">`CTAS` 也可用來建立暫存資料表，方法完全相同：</span><span class="sxs-lookup"><span data-stu-id="8e89c-121">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span></span>

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> <span data-ttu-id="8e89c-122">`CTAS` 是一個非常強大的命令，非常有效率地使用交易記錄空間是它額外的好處。</span><span class="sxs-lookup"><span data-stu-id="8e89c-122">`CTAS` is a very powerful command and has the added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="8e89c-123">捨棄暫存資料表</span><span class="sxs-lookup"><span data-stu-id="8e89c-123">Dropping temporary tables</span></span>
<span data-ttu-id="8e89c-124">建立新的工作階段時，不應該存在任何暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="8e89c-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="8e89c-125">不過，如果您呼叫同一個預存程序來建立具有相同名稱的暫存資料表，為了確保 `CREATE TABLE` 陳述式成功執行，可使用 `DROP` 進行簡單的預先存在性檢查，如以下範例所示︰</span><span class="sxs-lookup"><span data-stu-id="8e89c-125">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="8e89c-126">為了維持編寫程式碼的一致性，資料表和暫存資料表最好都採用此模式。</span><span class="sxs-lookup"><span data-stu-id="8e89c-126">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="8e89c-127">當您在程式碼中完成使用暫存資料表之後，使用 `DROP TABLE` 加以移除也是一個很好的做法。</span><span class="sxs-lookup"><span data-stu-id="8e89c-127">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="8e89c-128">在預存程序開發期間，在程序結尾一併搭配 drop 命令以確保會清除這些物件，也是相當常見的做法。</span><span class="sxs-lookup"><span data-stu-id="8e89c-128">In stored procedure development it is quite common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="8e89c-129">模組化程式碼</span><span class="sxs-lookup"><span data-stu-id="8e89c-129">Modularizing code</span></span>
<span data-ttu-id="8e89c-130">因為在使用者工作階段中的任何位置均可看見暫存資料表，這可用於協助您將應用程式程式碼模組化。</span><span class="sxs-lookup"><span data-stu-id="8e89c-130">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span></span>  <span data-ttu-id="8e89c-131">例如，下列預存程序結合了上述建議的做法產生 DDL，將可依統計資料名稱更新資料庫中的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="8e89c-131">For example, the stored procedure below brings together the recommended practices from above to generate DDL which will update all statistics in the database by statistic name.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

<span data-ttu-id="8e89c-132">在這個階段中，唯一進行的動作是建立預存程序，只是以 DDL 陳述式產生暫存資料表 #stats_ddl。</span><span class="sxs-lookup"><span data-stu-id="8e89c-132">At this stage the only action that has occurred is the creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="8e89c-133">如果 #stats_ddl 已經存在，這個預存程序將會卸除它，以確保在工作階段中執行一次以上時不會失敗。</span><span class="sxs-lookup"><span data-stu-id="8e89c-133">This stored procedure will drop #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="8e89c-134">不過，因為預存程序結尾沒有任何 `DROP TABLE` ，當預存程序完成時，它將保留建立的資料表，以便能夠從預存程序之外讀取。</span><span class="sxs-lookup"><span data-stu-id="8e89c-134">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it will leave the created table so that it can be read outside of the stored procedure.</span></span>  <span data-ttu-id="8e89c-135">不同於其他 SQL Server 資料庫，在 SQL 資料倉儲中，從建立暫存資料表的程序之外能夠使用此暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="8e89c-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span></span>  <span data-ttu-id="8e89c-136">工作階段內的 **任何位置** 都可以使用 SQL 資料倉儲暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="8e89c-136">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span></span> <span data-ttu-id="8e89c-137">這可以產生更具模組化和更易於管理的程式碼，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8e89c-137">This can lead to more modular and manageable code as in the below example:</span></span>

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a><span data-ttu-id="8e89c-138">暫存資料表限制</span><span class="sxs-lookup"><span data-stu-id="8e89c-138">Temporary table limitations</span></span>
<span data-ttu-id="8e89c-139">SQL 資料倉儲在實作暫存資料表時的確有一些限制。</span><span class="sxs-lookup"><span data-stu-id="8e89c-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="8e89c-140">目前，僅支援工作階段範圍內的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="8e89c-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="8e89c-141">不支援全域暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="8e89c-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="8e89c-142">此外，無法在暫存資料表上建立檢視。</span><span class="sxs-lookup"><span data-stu-id="8e89c-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e89c-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e89c-143">Next steps</span></span>
<span data-ttu-id="8e89c-144">若要深入了解，請參閱[資料表概觀][Overview]、[資料表資料類型][Data Types]、[散發資料表][Distribute]、[編製資料表的索引][Index]、[分割資料表][Partition]及[維護資料表統計資料][Statistics]等文章。</span><span class="sxs-lookup"><span data-stu-id="8e89c-144">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="8e89c-145">若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="8e89c-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
