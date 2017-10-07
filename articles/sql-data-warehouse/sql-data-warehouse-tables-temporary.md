---
title: "SQL 資料倉儲中的 aaaTemporary 資料表 |Microsoft 文件"
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
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="042d7-103">SQL 資料倉儲中的暫存資料表</span><span class="sxs-lookup"><span data-stu-id="042d7-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="042d7-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="042d7-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="042d7-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="042d7-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="042d7-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="042d7-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="042d7-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="042d7-107">[Index][Index]</span></span>
> * <span data-ttu-id="042d7-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="042d7-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="042d7-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="042d7-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="042d7-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="042d7-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="042d7-111">特別是在其中 hello 中繼結果是暫時性的轉換期間處理資料集時，暫存資料表會相當實用。</span><span class="sxs-lookup"><span data-stu-id="042d7-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="042d7-112">SQL 資料倉儲中暫存資料表會存在於 hello 工作階段層級。</span><span class="sxs-lookup"><span data-stu-id="042d7-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="042d7-113">它們是只有可見 toohello 工作階段中所建立的人員，以及該工作階段登出時，會自動卸除。</span><span class="sxs-lookup"><span data-stu-id="042d7-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="042d7-114">暫存資料表會提供效能優勢，因為其結果會寫入 toolocal，而不是遠端存放裝置。</span><span class="sxs-lookup"><span data-stu-id="042d7-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="042d7-115">暫存資料表是稍有不同 Azure SQL 資料倉儲中 Azure SQL Database，因為它們可以存取從任何地方 hello 工作階段，包括內部和外部預存程序內。</span><span class="sxs-lookup"><span data-stu-id="042d7-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="042d7-116">這篇文章包含有關使用暫存資料表的基本指導，並反白顯示 hello 原則的工作階段層級的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="042d7-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="042d7-117">使用本文章中的 hello 資訊可協助您模組化您的程式碼中，然後再提升重複使用性和您的程式碼維護的方便性。</span><span class="sxs-lookup"><span data-stu-id="042d7-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="042d7-118">建立暫存資料表</span><span class="sxs-lookup"><span data-stu-id="042d7-118">Create a temporary table</span></span>
<span data-ttu-id="042d7-119">建立暫存資料表時只是在資料表名稱前面加上 `#`。</span><span class="sxs-lookup"><span data-stu-id="042d7-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="042d7-120">例如：</span><span class="sxs-lookup"><span data-stu-id="042d7-120">For example:</span></span>

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

<span data-ttu-id="042d7-121">暫存資料表也可以建立與`CTAS`完全使用 hello 相同的方法：</span><span class="sxs-lookup"><span data-stu-id="042d7-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

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
> <span data-ttu-id="042d7-122">`CTAS`是非常強大的命令，並且 hello 加入優點是其交易記錄空間的使用中非常有效率。</span><span class="sxs-lookup"><span data-stu-id="042d7-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="042d7-123">捨棄暫存資料表</span><span class="sxs-lookup"><span data-stu-id="042d7-123">Dropping temporary tables</span></span>
<span data-ttu-id="042d7-124">建立新的工作階段時，不應該存在任何暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="042d7-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="042d7-125">相同但是 hello 如果您將會呼叫預存程序，會建立暫存 hello 與相同的名稱、 tooensure，您`CREATE TABLE`陳述式都能成功與簡單的預先存在檢查`DROP`可以用於如下列範例中的 hello 所示：</span><span class="sxs-lookup"><span data-stu-id="042d7-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="042d7-126">撰寫程式碼的一致性，對於良好練習 toouse 此模式的資料表和暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="042d7-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="042d7-127">它也是個不錯的主意 toouse`DROP TABLE`當您在程式碼中完成與其 tooremove 暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="042d7-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="042d7-128">在預存程序開發是相當常見 toosee hello drop 命令配套在一起的程序 tooensure hello 結尾這些物件會被清除。</span><span class="sxs-lookup"><span data-stu-id="042d7-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="042d7-129">模組化程式碼</span><span class="sxs-lookup"><span data-stu-id="042d7-129">Modularizing code</span></span>
<span data-ttu-id="042d7-130">因為暫存資料表可以出現在使用者工作階段的任何位置，這可以是被入侵的 toohelp 您模組化您的應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="042d7-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="042d7-131">例如，hello 下列預存程序結合了 hello 建議作法 corresponding toogenerate DDL 這將會更新 hello 資料庫中的所有統計資料的統計資料名稱。</span><span class="sxs-lookup"><span data-stu-id="042d7-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

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

<span data-ttu-id="042d7-132">在這個階段 hello 唯一發生的動作才會是 hello 建立預存程序，將只會產生暫存資料表時，#stats_ddl，DDL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="042d7-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="042d7-133">這個預存程序將會卸除 #stats_ddl，如果已經存在的 tooensure 失敗如果在工作階段中，執行一次以上。</span><span class="sxs-lookup"><span data-stu-id="042d7-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="042d7-134">不過，因為沒有任何`DROP TABLE`在 hello hello 預存程序結尾，hello 預存程序完成時，它將保留 hello 建立資料表，使它能夠讀取 hello 預存程序之外。</span><span class="sxs-lookup"><span data-stu-id="042d7-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="042d7-135">在 SQL 資料倉儲中，不同於其他 SQL Server 資料庫，它是建立它的 hello 程序之外可能 toouse hello 暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="042d7-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="042d7-136">可以使用 SQL 資料倉儲的暫存資料表**隨處**hello 工作階段內。</span><span class="sxs-lookup"><span data-stu-id="042d7-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="042d7-137">這可能會導致 toomore 模組化而且更容易管理的程式碼如下列範例中的 hello 所示：</span><span class="sxs-lookup"><span data-stu-id="042d7-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="042d7-138">暫存資料表限制</span><span class="sxs-lookup"><span data-stu-id="042d7-138">Temporary table limitations</span></span>
<span data-ttu-id="042d7-139">SQL 資料倉儲在實作暫存資料表時的確有一些限制。</span><span class="sxs-lookup"><span data-stu-id="042d7-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="042d7-140">目前，僅支援工作階段範圍內的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="042d7-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="042d7-141">不支援全域暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="042d7-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="042d7-142">此外，無法在暫存資料表上建立檢視。</span><span class="sxs-lookup"><span data-stu-id="042d7-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="042d7-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="042d7-143">Next steps</span></span>
<span data-ttu-id="042d7-144">toolearn 詳細資訊，請參閱 hello 文件上[資料表概觀][Overview]，[資料表資料類型][Data Types]，[散發資料表][ Distribute]，[的資料表建立索引][Index]，[分割資料表][ Partition]和[維護資料表統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="042d7-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="042d7-145">若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="042d7-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
