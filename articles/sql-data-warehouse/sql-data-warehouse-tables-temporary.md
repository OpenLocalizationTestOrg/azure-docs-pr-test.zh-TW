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
# <a name="temporary-tables-in-sql-data-warehouse"></a>SQL 資料倉儲中的暫存資料表
> [!div class="op_single_selector"]
> * [概觀][Overview]
> * [資料類型][Data Types]
> * [散發][Distribute]
> * [索引][Index]
> * [資料分割][Partition]
> * [統計資料][Statistics]
> * [暫存][Temporary]
> 
> 

特別是在其中 hello 中繼結果是暫時性的轉換期間處理資料集時，暫存資料表會相當實用。 SQL 資料倉儲中暫存資料表會存在於 hello 工作階段層級。  它們是只有可見 toohello 工作階段中所建立的人員，以及該工作階段登出時，會自動卸除。  暫存資料表會提供效能優勢，因為其結果會寫入 toolocal，而不是遠端存放裝置。  暫存資料表是稍有不同 Azure SQL 資料倉儲中 Azure SQL Database，因為它們可以存取從任何地方 hello 工作階段，包括內部和外部預存程序內。

這篇文章包含有關使用暫存資料表的基本指導，並反白顯示 hello 原則的工作階段層級的暫存資料表。 使用本文章中的 hello 資訊可協助您模組化您的程式碼中，然後再提升重複使用性和您的程式碼維護的方便性。

## <a name="create-a-temporary-table"></a>建立暫存資料表
建立暫存資料表時只是在資料表名稱前面加上 `#`。  例如：

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

暫存資料表也可以建立與`CTAS`完全使用 hello 相同的方法：

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
> `CTAS`是非常強大的命令，並且 hello 加入優點是其交易記錄空間的使用中非常有效率。 
> 
> 

## <a name="dropping-temporary-tables"></a>捨棄暫存資料表
建立新的工作階段時，不應該存在任何暫存資料表。  相同但是 hello 如果您將會呼叫預存程序，會建立暫存 hello 與相同的名稱、 tooensure，您`CREATE TABLE`陳述式都能成功與簡單的預先存在檢查`DROP`可以用於如下列範例中的 hello 所示：

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

撰寫程式碼的一致性，對於良好練習 toouse 此模式的資料表和暫存資料表。  它也是個不錯的主意 toouse`DROP TABLE`當您在程式碼中完成與其 tooremove 暫存資料表。  在預存程序開發是相當常見 toosee hello drop 命令配套在一起的程序 tooensure hello 結尾這些物件會被清除。

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a>模組化程式碼
因為暫存資料表可以出現在使用者工作階段的任何位置，這可以是被入侵的 toohelp 您模組化您的應用程式程式碼。  例如，hello 下列預存程序結合了 hello 建議作法 corresponding toogenerate DDL 這將會更新 hello 資料庫中的所有統計資料的統計資料名稱。

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

在這個階段 hello 唯一發生的動作才會是 hello 建立預存程序，將只會產生暫存資料表時，#stats_ddl，DDL 陳述式。  這個預存程序將會卸除 #stats_ddl，如果已經存在的 tooensure 失敗如果在工作階段中，執行一次以上。  不過，因為沒有任何`DROP TABLE`在 hello hello 預存程序結尾，hello 預存程序完成時，它將保留 hello 建立資料表，使它能夠讀取 hello 預存程序之外。  在 SQL 資料倉儲中，不同於其他 SQL Server 資料庫，它是建立它的 hello 程序之外可能 toouse hello 暫存資料表。  可以使用 SQL 資料倉儲的暫存資料表**隨處**hello 工作階段內。 這可能會導致 toomore 模組化而且更容易管理的程式碼如下列範例中的 hello 所示：

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

## <a name="temporary-table-limitations"></a>暫存資料表限制
SQL 資料倉儲在實作暫存資料表時的確有一些限制。  目前，僅支援工作階段範圍內的暫存資料表。  不支援全域暫存資料表。  此外，無法在暫存資料表上建立檢視。

## <a name="next-steps"></a>後續步驟
toolearn 詳細資訊，請參閱 hello 文件上[資料表概觀][Overview]，[資料表資料類型][Data Types]，[散發資料表][ Distribute]，[的資料表建立索引][Index]，[分割資料表][ Partition]和[維護資料表統計資料][Statistics]。  若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。

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
