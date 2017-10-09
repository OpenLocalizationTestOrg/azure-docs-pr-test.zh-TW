---
title: "當在 SQL 資料倉儲中選取 (CTAS) aaaCreate 資料表 |Microsoft 文件"
description: "使用 hello 撰寫程式碼的秘訣建立資料表，當在 Azure SQL 資料倉儲中選取 (CTAS) 陳述式，來開發方案。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>在 SQL 資料倉儲中的 Create Table As Select (CTAS)
建立為選取的資料表或`CTAS`是 hello 的其中一個最重要的 T-SQL 功能可用。 這是建立新的資料表根據 hello SELECT 陳述式的輸出完全平行化的作業。 `CTAS`是 hello 最簡單且最快方式 toocreate 資料表的副本。 本文件提供 `CTAS`的範例和最佳做法。

## <a name="selectinto-vs-ctas"></a>比較 SELECT..INTO 與CTAS
您可以將 `CTAS` 視為加強版的 `SELECT..INTO`。

以下範例是簡單的 `SELECT..INTO` 陳述式：

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

在上面的 hello 範例`[dbo].[FactInternetSales_new]`會為 ROUND_ROBIN 分散式資料表具有叢集資料行存放區索引在其上建立，因為這些是 Azure SQL 資料倉儲中的 hello 資料表預設值。

`SELECT..INTO`但是不允許您 toochange 任一 hello 發佈方法或 hello 索引輸入 hello 作業的一部分。 此時便適合使用 `CTAS`。

tooconvert 太 hello 上方`CTAS`是相當簡單：

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

與`CTAS`都能 toochange 兩者 hello 發佈的 hello 資料表資料，以及 hello 資料表類型。 

> [!NOTE]
> 如果您只想 toochange hello 索引中的您`CTAS`作業和 hello 來源資料表是分散式的雜湊則`CTAS`作業將會執行在您所維護的最佳 hello 相同的散發資料行和資料類型。 這樣會更有效率的 hello 作業期間，這樣可避免跨發佈資料移動。
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>使用 CTAS toocopy 資料表
可能是其中一個最常見的 hello 使用的`CTAS`，因此您可以變更 hello DDL 會建立一份資料表。 如果您最初建立做為資料表，例如`ROUND_ROBIN`和資料行，現在想將它變更分散式 tooa 資料表`CTAS`是如何變更 hello 散發資料行。 `CTAS`也可以使用的 toochange 資料分割、 索引或資料行的類型。

假設您建立使用 hello 預設散發類型這個資料表`ROUND_ROBIN`分散式由於沒有散發資料行指定在 hello `CREATE TABLE`。

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

現在您想 toocreate 此資料表具有叢集資料行存放區索引的新副本，以便您可以利用 hello 資料表效能的叢集資料行存放區。 您也想 toodistribute 此資料表在 ProductKey 因為您會預期這個資料行上的聯結，而且想 tooavoid 資料移動期間 ProductKey 上聯結。 最後您也想 tooadd 上的分割區 OrderDateKey 以便卸除舊的資料分割，您可以快速地刪除舊的資料。 以下是會將舊資料表複製到新的資料表 hello CTAS 陳述式。

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

最後，您可以在新的資料表重新命名資料表 tooswap，且再卸除舊的資料表。

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> Azure 資料倉儲尚未支援自動建立或自動更新統計資料。  在順序 tooget hello 達到最佳效能從您的查詢，請務必在所有資料表的所有資料行上建立統計資料，hello 第一次載入之後或 hello 資料會發生任何大量變更。  統計資料的詳細說明，請參閱 hello[統計資料][ Statistics] hello 開發一組主題中的主題。
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>使用 CTAS toowork 周圍不支援的功能
`CTAS`也可以使用的 toowork 使用數種下面所列的 hello 不支援的功能。 這可以通常證明 toobe win/win 情況下不只將您的程式碼會相容，但它會經常執行的速度 SQL 資料倉儲。 這是完全平行化設計的結果。 可以使用 CTAS 解決的案例包括：

* ANSI JOINS on UPDATEs
* ANSI JOINs on DELETEs
* MERGE 陳述式

> [!NOTE]
> 再試一次 toothink"CTAS 第一次 」。 如果您認為您可以解決問題，使用`CTAS`，通常是最佳方式 tooapproach hello，即使您要撰寫更多資料，因此。
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>update 陳述式的 ANSI 聯結取代
您可能會發現有複雜聯結兩個以上的資料表一起使用 ANSI 聯結語法 tooperform hello 更新或刪除的更新。

假設此資料表具有 tooupdate:

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

hello 原始查詢可能會有看起來像下面這樣：

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

因為 SQL 資料倉儲不支援 ANSI 聯結在 hello`FROM`子句`UPDATE`陳述式中，無法複製透過此程式碼，而不需要稍微變更它。

您可以使用多種`CTAS`和隱含聯結 tooreplace 這段程式碼：

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a>delete 陳述式的 ANSI 聯結取代
有時候 hello 刪除資料的最佳方法是 toouse `CTAS`。 而不刪除 hello 資料只選取您想要 tookeep hello 資料。 這尤其適合`DELETE`使用 ansi 聯結語法，因為 SQL 資料倉儲不支援在 hello ANSI 聯結陳述式`FROM`子句`DELETE`陳述式。

已轉換之 DELETE 陳述式的範例如下所示：

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a>取代 merge 陳述式
Merge 陳述式可以取代，至少有部分可使用 `CTAS`取代。 您可以合併 hello`INSERT`和 hello`UPDATE`為單一陳述式。 已刪除的記錄需要 toobe 關閉第二個陳述式中。

`UPSERT` 的範例如下所示：

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>CTAS 建議：明確陳述資料類型和輸出可為 null
移轉程式碼時，您可能會發現自己正在跨這種類型的程式碼撰寫模式執行：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Instinctively 您可能會認為您應該將這個程式碼 tooa CTAS 移轉，而系統會將正確。 不過，還是會有隱藏的問題。

hello 下列程式碼不會產生 hello 相同的結果：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

請注意 hello 資料行"result"向前帶有 hello 資料類型和 null 屬性值的 hello 運算式。 如果您不小心，這會導致 toosubtle 差異值。

請嘗試 hello 舉例如下：

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

儲存結果的 hello 值不相同。 當 hello 保存的 hello 結果資料行中的值用在其他運算式 hello 錯誤變得更重要。

![][1]

這對資料移轉特別重要。 即使 hello 第二個查詢是更精確的說是有問題。 hello 資料會是不同的比較的 toohello 來源系統，並可會 tooquestions 的完整性在 hello 移轉。 這是罕見情況下，其中 hello 「 錯誤 」 的答案都是實際 hello 右移一個 ！

hello 我們會看到這個 hello 兩個結果之間差異的原因已關閉 tooimplicit 類型轉換。 在 hello hello 資料表第一個範例會定義 hello 資料行定義。 Hello 資料列插入時，就會發生隱含類型轉換。 Hello 第二個範例中沒有任何隱含類型轉換為 hello 運算式定義 hello 資料行資料類型。 請注意該 hello 第二個範例中的 hello 資料行也已經定義為 Null 的資料行而 hello 第一個範例中還沒有。 Hello 資料表在建立時已明確定義 hello 第一個範例資料行 null 屬性。 在第二個範例中 hello 它已保留 toohello 運算式和預設這會導致 NULL 定義。  

這些問題的 tooresolve 必須明確設定 hello 型別轉換和 null 屬性在 hello`SELECT`部分 hello`CTAS`陳述式。 您無法設定這些屬性在 hello 建立資料表的一部分。

下列的 hello 範例示範如何 toofix hello 程式碼：

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

請注意 hello 下列：

* 可能已經使用 CAST 或 CONVERT
* ISNULL 是使用的 tooforce 不 COALESCE 的 null 屬性
* ISNULL 是 hello 最外層的函式
* hello ISNULL hello 第二部分是常數，也就是 0

> [!NOTE]
> Hello null 屬性 toobe 正確設定是很重要的 toouse`ISNULL`而非`COALESCE`。 `COALESCE`不具決定性的函式，並因此 hello hello 運算式結果將會永遠是可為 Null。 `ISNULL` 不同。 它是具決定性的。 因此當 hello 第二個部分 hello`ISNULL`函式是常數或常值，則 hello 產生值將會是 NOT NULL。
> 
> 

這個提示不只適合用於確保您的計算 hello 完整性。 它對資料表分割切換也很重要。 假設您根據事實定義此資料表：

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

不過，hello 值欄位是計算的運算式，它不是 hello 來源資料的一部分。

toocreate 您可能要 toodo 此分割資料集：

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

hello 查詢就會執行可行的。 hello 問題在於當您嘗試 tooperform hello 資料分割切換。 hello 資料表定義不相符。 toomake hello 資料表定義符合的 hello CTAS 需要 toobe 修改。

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

因此，您可以查看類型一致性，且維護 CTAS 上的可為 null 屬性是很好的工程最佳作法。 它可協助您的計算 toomaintain 完整性，並也可確保資料分割切換，就可能。

如需使用詳細資訊，請參閱 tooMSDN [CTAS][CTAS]。 它是其中一個 Azure SQL 資料倉儲中的 hello 最重要陳述式。 請確定您已徹底了解。

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
