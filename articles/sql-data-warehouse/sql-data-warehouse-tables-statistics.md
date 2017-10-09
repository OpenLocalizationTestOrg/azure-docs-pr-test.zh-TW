---
title: "SQL 資料倉儲中的資料表上的 aaaManaging 統計資料 |Microsoft 文件"
description: "開始使用 Azure SQL 資料倉儲中的資料表的統計資料。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>管理 SQL 資料倉儲中的資料表的統計資料
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

hello 詳細的 SQL 資料倉儲知道您的資料，hello 速度它可以針對執行查詢您的資料。  SQL 資料倉儲告訴您資料的 hello 方式就是收集資料的相關統計資料。  在您的資料具有統計資料是其中一個 hello 最重要的是您可以執行 toooptimize 您的查詢。  統計資料可協助建立 hello 最佳查詢計劃的 SQL 資料倉儲。  這是因為 hello SQL 資料倉儲查詢最佳化工具是以成本為基礎最佳化工具。  也就是說，它會比較 hello 成本的各種查詢計劃，並再選擇 hello 計劃與 hello 最低成本，也應該將執行 hello 最快的 hello 計劃。

您可以根據單一資料行、多個資料行或資料表的索引來建立統計資料。  統計資料會儲存在長條圖，這會擷取 hello 範圍和選擇性的值。  時，這特別感興趣的 hello 最佳化工具需要 tooevaluate 聯結、 GROUP BY、 HAVING 和 WHERE 子句，在查詢中的。  例如，如果 hello 最佳化工具估計，您要篩選查詢中的 hello 日期將會傳回 1 個資料列，它可能會選擇非常不同計劃比如果它評估這些日期您已選取會傳回 1 百萬個資料列。  建立統計資料是相當重要，同樣很重要的統計資料*精確地*反映 hello hello 資料表目前狀態。  具有最新的統計資料，可確保好的計畫 hello 最佳化工具所選取。  hello 最佳化工具所建立的 hello 計劃，才適合您資料的 hello 統計資料。

hello 的建立和更新統計資料的程序目前是手動程序，但 toodo 的非常簡單。  這不同於 SQL Server 根據單一資料行和索引來自動建立和更新統計資料。  使用下列的 hello 資訊，您可以大幅自動化 hello hello 統計資料的管理對您的資料。 

## <a name="getting-started-with-statistics"></a>開始使用統計資料
 每個資料行上建立取樣的統計資料是簡單的方式 tooget 入門統計資料。  保守的作法是同樣重要 tookeep 統計資料保持最新狀態，因為可能會 tooupdate 統計資料每日或每次載入之後。 總是會有效能與 hello 成本 toocreate 和更新統計資料之間的取捨。  如果您發現所需花費太長 toomaintain 所有統計資料，您可能想 tootry toobe 更具選擇性有關哪些資料行具有統計資料或資料行需要頻繁的更新。  比方說，您可能會想 tooupdate 日期資料行，每日，可能會加入新的值而不是每個載入之後。 同樣地，您將可以 hello 最大效益，具有統計資料中的資料行所涉及聯結、 GROUP BY、 HAVING 和 WHERE 子句。  如果您有大量的資料表 hello 中只使用資料行的 SELECT 子句、 這些資料行統計資料可能無法幫助，並花一些更多的精力 tooidentify 只有 hello 資料行，其中的統計資料會幫助，可以降低 hello 時間 toomaintain 統計資料.

## <a name="multi-column-statistics"></a>多重資料行統計資料
除了針對單一資料行 toocreating 統計資料，您可能會發現，您的查詢將受益於多個資料行統計資料。  多重資料行統計資料是對一份資料行清單建立的統計資料。  它們包含在 hello 清單中的 hello 第一個資料行的單一資料行統計資料加上一些跨資料行相互關聯資訊呼叫密度。  例如，如果您有兩個資料行聯結 tooanother 的資料表，您可能會發現 SQL 資料倉儲能夠更為最佳化 hello 計劃是否其了解 hello 兩個資料行之間的關聯性。   多重資料行統計資料可以改善某些作業 (例如複合聯結和分組分式) 的查詢效能。

## <a name="updating-statistics"></a>更新統計資料
在資料庫管理例行工作中，更新統計資料很重要。  當 hello 發佈 hello 資料庫中的資料變更時，統計資料需要 toobe 更新。  過期的統計資料會導致 toosub 達到最佳查詢效能。

加入新的日期時，一個最佳作法將是 tooupdate 日期資料行統計資料每一天。  每次新的資料列載入至 hello 資料倉儲，新負載交易日期或加入。 這些變更 hello 資料發佈，以進行 hello 統計資料已過時。 相反地，customer 資料表中的國家/地區資料行的統計資料可能永遠不需要 toobe 更新，因為通常不會變更 hello 值分佈。 假設 hello 發佈常數的客戶，加入新的資料列 toohello 資料表變數不會為 toochange hello 資料分佈。 不過，如果您的資料倉儲只包含一個國家/地區，並從新的國家/地區匯入資料，導致資料從多個國家 （地區） 儲存，然後您確實需要 tooupdate hello 國家/地區資料行的統計資料。

其中一個 hello 第一個問題 tooask 當疑難排解查詢時，「 是 hello 統計資料保持最新狀態？ 」

這個問題的答案不是其中 hello 資料的 hello 存留期可以回答。 最新的 toodate 統計資料物件可能已基礎資料沒有變更材料 toohello 的非常舊。 當 hello 的資料列的數目已大幅變更，或者沒有 hello 特定資料行的值分佈的材料變更*然後*是時間 tooupdate 統計資料。  

如需參考， **SQL Server** (非 SQL 資料倉儲) 會針對下列情況自動更新統計資料：

* 如果有零個資料列在 hello 資料表中，當您將加入資料列，就會自動更新統計資料
* 當您將加入開頭為少於 500 個資料列超過 500 個資料列 tooa 資料表 （例如在開始您有 499 然後再新增 500 列 tooa 共 999 個資料列），就會自動更新 
* 一旦您已超過 500 個資料列就 tooadd 500 個其他資料列 + hello hello 資料表大小的 20%之前，您會看到 自動更新在 hello 統計資料

因為沒有任何 DMV toodetermine 如果自從 hello 時間統計資料上次更新 hello 資料表中的資料已經變更，了解 hello 存留期統計資料可以提供您與 hello 圖片的一部分。  您可以使用下列查詢 toodetermine hello 上次統計資料的 hello 其中每個資料表上更新。  

> [!NOTE]
> 請記住，是否沒有 hello 特定資料行的值分佈的實質性變更，您應該更新統計資料，不論 hello 它們已更新的上次。  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

例如，資料倉儲中的日期資料行通常需要經常更新統計資料。 每次新的資料列載入至 hello 資料倉儲，新負載交易日期或加入。 這些變更 hello 資料發佈，以進行 hello 統計資料已過時。  相反地，在 customer 資料表在性別資料行的統計資料可能永遠不需要 toobe 更新。 假設 hello 發佈常數的客戶，加入新的資料列 toohello 資料表變數不會為 toochange hello 資料分佈。 不過，如果您的資料倉儲僅包含一個性別和新的需求結果，在多個性別明確先然後 tooupdate hello 性別資料行的統計資料。

如需進一步說明，請參閱 MSDN 上的[統計資料][Statistics]。

## <a name="implementing-statistics-management"></a>實作統計資料管理
它通常是個不錯的主意 tooextend 資料載入會在更新統計資料的程序 tooensure hello hello 載入結束。 hello 資料載入時，資料表經常會變更其大小和/或其值的分佈。 因此，這是邏輯上 tooimplement 某些管理處理程序。

有些指導原則如下所示為 hello 載入程序期間更新統計資料：

* 確保每個載入的資料表至少都更新一個統計資料物件。 此更新 hello hello 統計資料更新的大小 （資料列計數與頁面計數） 資訊的資料表。
* 將焦點放在參與 JOIN、GROUP BY、ORDER BY 和 DISTINCT 子句的資料行。
* 請考慮更新 「 遞增索引鍵 」 的交易之類的資料行日期將不會在 hello 統計資料長條圖中包含這些值更頻繁。
* 考慮較不常更新靜態散發資料行。
* 請記得，每個統計資料物件會依序更新。 僅只實作 `UPDATE STATISTICS <TABLE_NAME>` 可能不太理想 - 尤其是對具有許多統計資料物件的寬型資料表而言。

> [!NOTE]
> 如需詳細資訊 [遞增索引鍵] 請參閱 SQL Server 2014 toohello 基數估計模型技術白皮書。
> 
> 

如需進一步說明，請參閱 MSDN 上的[基數估計][Cardinality Estimation]。

## <a name="examples-create-statistics"></a>範例：建立統計資料
下列範例將示範如何 toouse 建立統計資料的各種選項。 您使用每個資料行的 hello 選項取決於資料的 hello 特性以及 hello 資料行在查詢中的使用方式。

### <a name="a-create-single-column-statistics-with-default-options"></a>A. 使用預設選項建立單一資料行統計資料
toocreate 統計資料資料行，只要提供 hello 統計資料物件的名稱與 hello hello 資料行名稱。

此語法會使用所有 hello 預設選項。 根據預設，SQL 資料倉儲取樣 20%的 hello 資料表建立統計資料時。

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

例如：

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. 檢查每個資料列以建立單一資料行統計資料
hello 預設的 20%的取樣率已足以應付大多數情況。 不過，您可以調整 hello 取樣率。

toosample hello 完整資料表中，使用下列語法：

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

例如：

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. 藉由指定 hello 取樣大小建立單一資料行統計資料
或者，您可以指定 hello 取樣大小，以百分比表示：

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. 建立只對某些 hello 資料列的單一資料行統計資料
另一個選項，您可以建立統計資料部分 hello 資料列在資料表中。 這稱為篩選的統計資料。

比方說，您可以使用篩選的統計資料，當您計劃 tooquery 大型的資料分割資料表的特定分割區。 藉由只 hello 上磁碟分割值建立統計資料，hello hello 統計資料的精確度會改善，並因而改善查詢效能。

這個範例會建立某個值範圍的統計資料。 hello 值就可以輕鬆在定義資料分割中 toomatch hello 範圍的值。

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Hello 查詢最佳化工具 tooconsider 使用篩選的統計資料，則會選擇 hello 分散式的查詢計劃時，針對 hello 查詢必須配合 hello hello 統計資料物件定義。 使用 hello 上述範例中，hello 查詢子句中需要 2000101 之間 20001231 toospecify col1 值。
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. 與所有 hello 選項建立單一資料行統計資料
您當然可以一起結合 hello 選項。 下列的 hello 範例會建立篩選的統計資料物件，以自訂的取樣大小：

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

如需 hello 完整參考，請參閱[CREATE STATISTICS] [ CREATE STATISTICS] MSDN 上。

### <a name="f-create-multi-column-statistics"></a>F. 建立多重資料行統計資料
toocreate 多重資料行的統計資料，只需使用 hello 上述範例中，但指定多個資料行。

> [!NOTE]
> hello 長條圖，會使用 tooestimate hello 查詢結果中的資料列數只適用於 hello hello 統計資料物件定義中所列的第一個資料行。
> 
> 

在此範例中，hello 長條圖位於*產品\_類別*。 跨資料行統計資料會依據 product\_category 和 product\_sub_c\ategory 計算：

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

因為沒有之間的相互關聯*產品\_類別*和*產品\_sub\_類別*，多重資料行狀態就非常適合在存取這些資料行在 hello 相同的時間。

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>G. 在資料表中的所有 hello 資料行上建立統計資料
其中一種方式 toocreate 統計資料，則 tooissues CREATE STATISTICS 命令建立 hello 表格之後。

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>H. 資料庫中的所有資料行上使用預存程序 toocreate 統計資料
SQL 資料倉儲不太需要系統預存程序對等項目 [SQL Server 中的 [sp_create_stats]]。 這個預存程序上還沒有統計資料的 hello 資料庫的每個資料行建立單一資料行統計資料物件。

這會協助您開始進行資料庫設計。 感覺可用 tooadapt 它 tooyour 需要。

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

toocreate hello 這個程序中，資料表中的所有資料行的統計資料，只需呼叫 hello 程序。

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>範例：更新統計資料
tooupdate 統計資料，您可以：

1. 更新一個統計資料物件。 指定統計資料物件想 tooupdate hello hello 的名稱。
2. 更新資料表上的所有統計資料物件。 指定 hello hello 資料表，而不是一個特定的統計資料物件名稱。

### <a name="a-update-one-specific-statistics-object"></a>A. 更新一個特定統計資料物件
使用下列語法 tooupdate 特定統計資料物件的 hello:

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

例如：

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

藉由更新特定統計資料物件，您可以減少 hello 時間和資源所需的 toomanage 統計資料。 這需要一些以為，不過，toochoose hello 最佳統計資料物件 tooupdate。

### <a name="b-update-all-statistics-on-a-table"></a>B. 更新資料表上的所有統計資料。
這會顯示更新的資料表上的所有 hello 統計資料物件的簡單方法。

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

例如：

```sql
UPDATE STATISTICS dbo.table1;
```

此陳述式很容易 toouse。 請記得這更新 hello 資料表上的所有統計資料，因此可能會執行比所需的更多工作。 如果 hello 效能不是問題，這絕對是 hello 最簡單且最完整的方式 tooguarantee 統計資料處於最新狀態。

> [!NOTE]
> 在更新的資料表上的所有統計資料時，SQL 資料倉儲會掃描 toosample hello 資料表的每個統計資料。 如果 hello 資料表很大，具有多資料行，以及許多統計資料，可能會更有效率 tooupdate 個別統計資料根據需求。
> 
> 

實作`UPDATE STATISTICS`程序，請參閱 hello[暫存資料表][ Temporary]發行項。 hello 實作方法是稍有不同的 toohello`CREATE STATISTICS`上述的程序，但 hello 最終結果是 hello 相同。

如需 hello 完整語法，請參閱[Update Statistics] [ Update Statistics] MSDN 上。

## <a name="statistics-metadata"></a>統計資料中繼資料
有數個系統檢視和函數，您可以使用 toofind 統計的相關資訊。 例如，您可以看到是否統計資料物件可能已過期時最後建立或更新統計資料，請使用 hello stats 日期函式 toosee。

### <a name="catalog-views-for-statistics"></a>統計資料的目錄檢視
這些系統檢視提供統計資料的相關資訊：

| 目錄檢視 | 說明 |
|:--- |:--- |
| [sys.columns][sys.columns] |每個資料行有一個資料列。 |
| [sys.objects][sys.objects] |Hello 資料庫中每個物件的一個資料列。 |
| [sys.schemas][sys.schemas] |每個結構描述 hello 資料庫中的一個資料列。 |
| [sys.stats][sys.stats] |每個統計資料物件有一個資料列。 |
| [sys.stats_columns][sys.stats_columns] |Hello 統計資料物件中每個資料行的一個資料列。 連結回 toosys.columns。 |
| [sys.tables][sys.tables] |每個資料表 (包括外部資料表) 有一個資料列。 |
| [sys.table_types][sys.table_types] |每個資料類型有一個資料列。 |

### <a name="system-functions-for-statistics"></a>統計資料的系統函式
這些系統函式很適合用於處理統計資料：

| 系統函式 | 說明 |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |上次更新日期 hello 統計資料物件。 |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Hello 統計資料物件所了解，請提供有關值分佈 hello 的摘要層級及詳細資訊。 |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>將統計資料資料行和函式結合成一個檢視
此檢視會一起從 hello [STATS_DATE()] [] 函式與 toostatistics 和結果的資料行。

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>DBCC SHOW_STATISTICS() 範例
DBCC SHOW_STATISTICS() 顯示儲存統計資料物件中的 hello 資料。 此資料來自三個部分。

1. 標頭
2. 密度向量
3. 長條圖

hello hello 統計資料的相關標頭中繼資料。 hello 長條圖會顯示 hello 散發值 hello 第一個索引鍵資料行中的 hello 統計資料物件。 hello 密度向量來測量跨資料行相互關聯。 SQLDW 計算與任何 hello 統計資料物件中的 hello 資料的基數估計值。

### <a name="show-header-density-and-histogram"></a>顯示標頭、密度和長條圖
這個簡單範例顯示統計資料物件的所有三個部分。

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

例如：

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>顯示 DBCC SHOW_STATISTICS(); 的一或多個部分
如果您只想要檢視特定部分，請使用 hello`WITH`子句，並指定哪些部分您想 toosee:

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

例如：

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>DBCC SHOW_STATISTICS() 差異
DBCC SHOW_STATISTICS() 更嚴格地是比較 SQL 資料倉儲 tooSQL 伺服器實作。

1. 不支援未記載的功能
2. 無法使用 Stats_stream
3. 無法聯結特定統計資料子集的結果，例如 (STAT_HEADER JOIN DENSITY_VECTOR)
4. 無法針對訊息隱藏項目設定 NO_INFOMSGS
5. 無法使用統計資料名稱前後的方括號
6. 無法使用資料行名稱 tooidentify 統計資料物件
7. 不支援自訂錯誤 2767

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 MSDN 上的 [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]。  toolearn 詳細資訊，請參閱 hello 文件上[資料表概觀][Overview]，[資料表資料類型][Data Types]，[散發資料表][ Distribute]，[的資料表建立索引][Index]，[分割資料表][ Partition]和[暫存資料表][Temporary]。  若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。  

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
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
