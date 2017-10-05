---
title: "在 SQL 資料倉儲中的 Create table as select (CTAS) | Microsoft Docs"
description: "在 Azure SQL 資料倉儲中利用 create table as select (CTAS) 陳述式撰寫程式碼做為開發解決方案的提示。"
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
ms.openlocfilehash: cb08313726e8135feaa9b413937c2197ea397f4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="cab69-103">在 SQL 資料倉儲中的 Create Table As Select (CTAS)</span><span class="sxs-lookup"><span data-stu-id="cab69-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="cab69-104">Create table as select 或 `CTAS` 是最重要的可用 T-SQL 功能之一。</span><span class="sxs-lookup"><span data-stu-id="cab69-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span></span> <span data-ttu-id="cab69-105">該作業與根據 SELECT 陳述式的輸出來建立新資料表的作業完全平行。</span><span class="sxs-lookup"><span data-stu-id="cab69-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="cab69-106">`CTAS` 是建立資料表複本的最簡單且最快速方式。</span><span class="sxs-lookup"><span data-stu-id="cab69-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span></span> <span data-ttu-id="cab69-107">本文件提供 `CTAS`的範例和最佳做法。</span><span class="sxs-lookup"><span data-stu-id="cab69-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="cab69-108">比較 SELECT..INTO 與CTAS</span><span class="sxs-lookup"><span data-stu-id="cab69-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="cab69-109">您可以將 `CTAS` 視為加強版的 `SELECT..INTO`。</span><span class="sxs-lookup"><span data-stu-id="cab69-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="cab69-110">以下範例是簡單的 `SELECT..INTO` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="cab69-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="cab69-111">在上述範例中，`[dbo].[FactInternetSales_new]` 會建立為包含 CLUSTERED COLUMNSTORE INDEX 的 ROUND_ROBIN 分散式資料表，因為這是 Azure SQL 資料倉儲的資料表預設值。</span><span class="sxs-lookup"><span data-stu-id="cab69-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="cab69-112">但是 `SELECT..INTO` 不允許在作業期間變更分散方法或索引類型。</span><span class="sxs-lookup"><span data-stu-id="cab69-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="cab69-113">此時便適合使用 `CTAS`。</span><span class="sxs-lookup"><span data-stu-id="cab69-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="cab69-114">而將上述範例轉換到 `CTAS` 的方式相當簡單：</span><span class="sxs-lookup"><span data-stu-id="cab69-114">To convert the above to `CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="cab69-115">您可以使用 `CTAS`，變更資料表資料的分散方法，以及資料表類型。</span><span class="sxs-lookup"><span data-stu-id="cab69-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="cab69-116">如果您嘗試在 `CTAS` 作業中變更索引，且來源資料表是雜湊分散，則維持相同的分散資料行和資料類型會使 `CTAS` 作業有最佳效能。</span><span class="sxs-lookup"><span data-stu-id="cab69-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="cab69-117">這樣可避免在作業期間有跨越分散資料移動，所以會有較佳效能。</span><span class="sxs-lookup"><span data-stu-id="cab69-117">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="cab69-118">使用 CTAS 複製資料表</span><span class="sxs-lookup"><span data-stu-id="cab69-118">Using CTAS to copy a table</span></span>
<span data-ttu-id="cab69-119">`CTAS` 最常見的用途之一，就是建立資料表複本，讓您可以變更 DDL。</span><span class="sxs-lookup"><span data-stu-id="cab69-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="cab69-120">例如，您原本將資料表建立為 `ROUND_ROBIN`，而現在想變更為在資料行上散發的資料表，`CTAS` 就是您將變更散發資料行的方式。</span><span class="sxs-lookup"><span data-stu-id="cab69-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="cab69-121">`CTAS` 也可以用來變更分割、索引或資料行類型。</span><span class="sxs-lookup"><span data-stu-id="cab69-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="cab69-122">假設您因為在 `ROUND_ROBIN` 中沒有指定散發資料行，而使用 `CREATE TABLE` 散發的預設散發類型建立資料表。</span><span class="sxs-lookup"><span data-stu-id="cab69-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

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

<span data-ttu-id="cab69-123">現在您想建立此資料表的新複本搭配叢集的資料行存放區索引，讓您可以利用叢集的資料行存放區資料表的效能。</span><span class="sxs-lookup"><span data-stu-id="cab69-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="cab69-124">您也會想要在 ProductKey 上散發此資料表，因為您預期會聯結此資料行，並在聯結 ProductKey 期間避免資料移動。</span><span class="sxs-lookup"><span data-stu-id="cab69-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="cab69-125">最後您也會想在 OrderDateKey 上加入資料分割，如此就可以透過卸除舊的資料分割來快速刪除舊資料。</span><span class="sxs-lookup"><span data-stu-id="cab69-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="cab69-126">以下是 CTAS 陳述式，會將您的舊資料表複製到新資料表。</span><span class="sxs-lookup"><span data-stu-id="cab69-126">Here is the CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="cab69-127">最後可以重新命名您的資料表以切換到新的資料表，然後卸除舊資料表。</span><span class="sxs-lookup"><span data-stu-id="cab69-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="cab69-128">Azure 資料倉儲尚未支援自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="cab69-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="cab69-129">為了獲得查詢的最佳效能，在首次載入資料，或是資料中發生重大變更之後，建立所有資料表的所有資料行統計資料非常重要。</span><span class="sxs-lookup"><span data-stu-id="cab69-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="cab69-130">如需統計資料的詳細說明，請參閱「開發」主題群組中的[統計資料][Statistics]主題。</span><span class="sxs-lookup"><span data-stu-id="cab69-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="cab69-131">使用 CTAS 解決不支援的功能</span><span class="sxs-lookup"><span data-stu-id="cab69-131">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="cab69-132">`CTAS` 也可以用來暫時解決以下幾個不支援的功能。</span><span class="sxs-lookup"><span data-stu-id="cab69-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="cab69-133">這通常可以證明是雙贏的情況，因為您的程式碼不但能夠相容，而且通常可以在 SQL 資料倉儲上更快速執行。</span><span class="sxs-lookup"><span data-stu-id="cab69-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="cab69-134">這是完全平行化設計的結果。</span><span class="sxs-lookup"><span data-stu-id="cab69-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="cab69-135">可以使用 CTAS 解決的案例包括：</span><span class="sxs-lookup"><span data-stu-id="cab69-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="cab69-136">ANSI JOINS on UPDATEs</span><span class="sxs-lookup"><span data-stu-id="cab69-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="cab69-137">ANSI JOINs on DELETEs</span><span class="sxs-lookup"><span data-stu-id="cab69-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="cab69-138">MERGE 陳述式</span><span class="sxs-lookup"><span data-stu-id="cab69-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="cab69-139">嘗試考慮「CTAS 優先」。</span><span class="sxs-lookup"><span data-stu-id="cab69-139">Try to think "CTAS first".</span></span> <span data-ttu-id="cab69-140">如果您認為您可以使用 `CTAS` 解決問題，即使您正在撰寫更多資料做為結果，這通常是最佳的解決方法。</span><span class="sxs-lookup"><span data-stu-id="cab69-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="cab69-141">update 陳述式的 ANSI 聯結取代</span><span class="sxs-lookup"><span data-stu-id="cab69-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="cab69-142">您可能會發現有複雜的更新，使用 ANSI 聯結語法執行 UPDATE 或 DELETE 以將兩個以上的資料表聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="cab69-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="cab69-143">假設您必須更新此資料表：</span><span class="sxs-lookup"><span data-stu-id="cab69-143">Imagine you had to update this table:</span></span>

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

<span data-ttu-id="cab69-144">原始的查詢看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="cab69-144">The original query might have looked something like this:</span></span>

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

<span data-ttu-id="cab69-145">由於 SQL 資料倉儲不支援在 `UPDATE` 陳述式的 `FROM` 子句中使用 ANSI 聯結，因此您無法在毫不變更此程式碼的情況下將它複製過去。</span><span class="sxs-lookup"><span data-stu-id="cab69-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="cab69-146">您可以使用 `CTAS` 和隱含聯結的組合來取代此程式碼：</span><span class="sxs-lookup"><span data-stu-id="cab69-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

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

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="cab69-147">delete 陳述式的 ANSI 聯結取代</span><span class="sxs-lookup"><span data-stu-id="cab69-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="cab69-148">有時候刪除資料的最佳方法是使用 `CTAS`。</span><span class="sxs-lookup"><span data-stu-id="cab69-148">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="cab69-149">除了刪除資料以外，可以只選取您想要保留的資料。</span><span class="sxs-lookup"><span data-stu-id="cab69-149">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="cab69-150">這對於使用 ANSI 聯結語法的 `DELETE` 陳述式尤其適用，因為 SQL 資料倉儲不支援在 `DELETE` 陳述式的 `FROM` 子句中使用 ANSI 聯結。</span><span class="sxs-lookup"><span data-stu-id="cab69-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="cab69-151">已轉換之 DELETE 陳述式的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="cab69-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="cab69-152">取代 merge 陳述式</span><span class="sxs-lookup"><span data-stu-id="cab69-152">Replace merge statements</span></span>
<span data-ttu-id="cab69-153">Merge 陳述式可以取代，至少有部分可使用 `CTAS`取代。</span><span class="sxs-lookup"><span data-stu-id="cab69-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="cab69-154">您可以將 `INSERT` 和 `UPDATE` 合併成單一陳述式。</span><span class="sxs-lookup"><span data-stu-id="cab69-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span></span> <span data-ttu-id="cab69-155">任何已刪除的記錄都必須在第二個陳述式中關閉。</span><span class="sxs-lookup"><span data-stu-id="cab69-155">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="cab69-156">`UPSERT` 的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="cab69-156">An example of an `UPSERT` is available below:</span></span>

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

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="cab69-157">CTAS 建議：明確陳述資料類型和輸出可為 null</span><span class="sxs-lookup"><span data-stu-id="cab69-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="cab69-158">移轉程式碼時，您可能會發現自己正在跨這種類型的程式碼撰寫模式執行：</span><span class="sxs-lookup"><span data-stu-id="cab69-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="cab69-159">您可能會自動認為您應該將此程式碼移轉到 CTAS，就會是正確的。</span><span class="sxs-lookup"><span data-stu-id="cab69-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="cab69-160">不過，還是會有隱藏的問題。</span><span class="sxs-lookup"><span data-stu-id="cab69-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="cab69-161">下列程式碼不會產生相同的結果：</span><span class="sxs-lookup"><span data-stu-id="cab69-161">The following code does NOT yield the same result:</span></span>

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

<span data-ttu-id="cab69-162">請注意，資料行 "result" 沿用運算式的資料類型和可為 null 值。</span><span class="sxs-lookup"><span data-stu-id="cab69-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="cab69-163">如果不小心處理，這可能會導致細微差異值。</span><span class="sxs-lookup"><span data-stu-id="cab69-163">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="cab69-164">請嘗試下列內容做為範例：</span><span class="sxs-lookup"><span data-stu-id="cab69-164">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="cab69-165">儲存的結果值是不同的。</span><span class="sxs-lookup"><span data-stu-id="cab69-165">The value stored for result is different.</span></span> <span data-ttu-id="cab69-166">因為結果資料行中保留的值用於其他運算式，錯誤變得更加顯著。</span><span class="sxs-lookup"><span data-stu-id="cab69-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="cab69-167">這對資料移轉特別重要。</span><span class="sxs-lookup"><span data-stu-id="cab69-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="cab69-168">即使第二個查詢已經更精確，仍然有一個問題。</span><span class="sxs-lookup"><span data-stu-id="cab69-168">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="cab69-169">相較於來源系統，此資料有所不同，這會在移轉中產生完整性的問題。</span><span class="sxs-lookup"><span data-stu-id="cab69-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="cab69-170">這是「錯誤」答案其實是正確答案的少數原因之一！</span><span class="sxs-lookup"><span data-stu-id="cab69-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="cab69-171">我們會看到這兩個結果之間有差異，追根究柢的原因是隱含的類型轉型。</span><span class="sxs-lookup"><span data-stu-id="cab69-171">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="cab69-172">在第一個範例中，資料表會定義資料行。</span><span class="sxs-lookup"><span data-stu-id="cab69-172">In the first example the table defines the column definition.</span></span> <span data-ttu-id="cab69-173">插入資料列時，就會發生隱含類型轉換。</span><span class="sxs-lookup"><span data-stu-id="cab69-173">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="cab69-174">在第二個範例中，沒有隱含類型轉換，因為此運算式會定義資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="cab69-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="cab69-175">請注意，第二個範例中的資料行已定義為可為 Null 的資料行，而在第一個範例中還沒有定義。</span><span class="sxs-lookup"><span data-stu-id="cab69-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="cab69-176">在第一個範例中建立資料表時，尚未明確定義資料行可為 null。</span><span class="sxs-lookup"><span data-stu-id="cab69-176">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="cab69-177">在第二個範例中，它只留給了運算式，根據預設，這會導致 NULL 定義。</span><span class="sxs-lookup"><span data-stu-id="cab69-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="cab69-178">若要解決這些問題，您必須在 `CTAS` 陳述式的 `SELECT` 部分中明確設定類型轉換和可為 null 屬性。</span><span class="sxs-lookup"><span data-stu-id="cab69-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span></span> <span data-ttu-id="cab69-179">您無法在建立資料表的部分中設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="cab69-179">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="cab69-180">下列範例示範如何修正程式碼：</span><span class="sxs-lookup"><span data-stu-id="cab69-180">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="cab69-181">請注意：</span><span class="sxs-lookup"><span data-stu-id="cab69-181">Note the following:</span></span>

* <span data-ttu-id="cab69-182">可能已經使用 CAST 或 CONVERT</span><span class="sxs-lookup"><span data-stu-id="cab69-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="cab69-183">ISNULL 是用來強制 NULLability，而非 COALESCE</span><span class="sxs-lookup"><span data-stu-id="cab69-183">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="cab69-184">ISNULL 是最外層的函式</span><span class="sxs-lookup"><span data-stu-id="cab69-184">ISNULL is the outermost function</span></span>
* <span data-ttu-id="cab69-185">ISNULL 的第二個部分是常數，也就是 0</span><span class="sxs-lookup"><span data-stu-id="cab69-185">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="cab69-186">若要正確地設定可為 null 屬性，必須使用 `ISNULL` 而不是 `COALESCE`。</span><span class="sxs-lookup"><span data-stu-id="cab69-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="cab69-187">`COALESCE` 不是具決定性的函數，因此運算式的結果一律可為 Null。</span><span class="sxs-lookup"><span data-stu-id="cab69-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="cab69-188">`ISNULL` 不同。</span><span class="sxs-lookup"><span data-stu-id="cab69-188">`ISNULL` is different.</span></span> <span data-ttu-id="cab69-189">它是具決定性的。</span><span class="sxs-lookup"><span data-stu-id="cab69-189">It is deterministic.</span></span> <span data-ttu-id="cab69-190">因此當 `ISNULL` 函數的第二個部分是常數或常值，則結果值將會是 NOT NULL。</span><span class="sxs-lookup"><span data-stu-id="cab69-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="cab69-191">本秘訣不只適用於確保計算的完整性。</span><span class="sxs-lookup"><span data-stu-id="cab69-191">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="cab69-192">它對資料表分割切換也很重要。</span><span class="sxs-lookup"><span data-stu-id="cab69-192">It is also important for table partition switching.</span></span> <span data-ttu-id="cab69-193">假設您根據事實定義此資料表：</span><span class="sxs-lookup"><span data-stu-id="cab69-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="cab69-194">不過，[值] 欄位是已計算的運算式，它不是來源資料的一部分。</span><span class="sxs-lookup"><span data-stu-id="cab69-194">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="cab69-195">若要建立資料分割資料集，您可能會想要這麼做：</span><span class="sxs-lookup"><span data-stu-id="cab69-195">To create your partitioned dataset you might want to do this:</span></span>

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

<span data-ttu-id="cab69-196">執行最適合的查詢。</span><span class="sxs-lookup"><span data-stu-id="cab69-196">The query would run perfectly fine.</span></span> <span data-ttu-id="cab69-197">當您嘗試執行資料分割切換時會出現問題。</span><span class="sxs-lookup"><span data-stu-id="cab69-197">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="cab69-198">資料表定義不相符。</span><span class="sxs-lookup"><span data-stu-id="cab69-198">The table definitions do not match.</span></span> <span data-ttu-id="cab69-199">若要讓資料表定義相符，必須修改 CTAS。</span><span class="sxs-lookup"><span data-stu-id="cab69-199">To make the table definitions match the CTAS needs to be modified.</span></span>

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

<span data-ttu-id="cab69-200">因此，您可以查看類型一致性，且維護 CTAS 上的可為 null 屬性是很好的工程最佳作法。</span><span class="sxs-lookup"><span data-stu-id="cab69-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="cab69-201">它有助於維護計算的完整性，並且也可確保資料分割切換的可能性。</span><span class="sxs-lookup"><span data-stu-id="cab69-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="cab69-202">如需使用 [CTAS][CTAS] 的詳細資訊，請參閱 MSDN。</span><span class="sxs-lookup"><span data-stu-id="cab69-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="cab69-203">它是 Azure SQL 資料倉儲中最重要的陳述式之一。</span><span class="sxs-lookup"><span data-stu-id="cab69-203">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="cab69-204">請確定您已徹底了解。</span><span class="sxs-lookup"><span data-stu-id="cab69-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cab69-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cab69-205">Next steps</span></span>
<span data-ttu-id="cab69-206">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="cab69-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
