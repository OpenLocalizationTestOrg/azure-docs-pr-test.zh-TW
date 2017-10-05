---
title: "根據 SQL 資料倉儲中的選項分組 | Microsoft Docs"
description: "根據 Azure SQL 資料倉儲中的選項實作群組以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: da71cb834c13da5d0f5690f471efc6c696163f30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="a1cb6-103">根據 SQL 資料倉儲中的選項分組</span><span class="sxs-lookup"><span data-stu-id="a1cb6-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="a1cb6-104">[GROUP BY][GROUP BY] 子句是用來將資料彙總至摘要的一組資料列。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="a1cb6-105">它也具有一些擴充其功能的選項，這些選項都需要克服，因為 Azure SQL 資料倉儲並不直接支援這些選項。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="a1cb6-106">可用選項包括</span><span class="sxs-lookup"><span data-stu-id="a1cb6-106">These options are</span></span>

* <span data-ttu-id="a1cb6-107">GROUP BY 搭配 ROLLUP</span><span class="sxs-lookup"><span data-stu-id="a1cb6-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="a1cb6-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="a1cb6-108">GROUPING SETS</span></span>
* <span data-ttu-id="a1cb6-109">GROUP BY 搭配 CUBE</span><span class="sxs-lookup"><span data-stu-id="a1cb6-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="a1cb6-110">Rollup 和 grouping sets 選項</span><span class="sxs-lookup"><span data-stu-id="a1cb6-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="a1cb6-111">此處最簡單的選項是改為使用 `UNION ALL` 來執行彙總，而不是依賴明確的語法。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="a1cb6-112">應該會出現幾乎相同的結果</span><span class="sxs-lookup"><span data-stu-id="a1cb6-112">The result is exactly the same</span></span>

<span data-ttu-id="a1cb6-113">以下是使用 `ROLLUP` 選項的 group by 陳述式範例：</span><span class="sxs-lookup"><span data-stu-id="a1cb6-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="a1cb6-114">藉由使用 ROLLUP，我們要求下列彙總：</span><span class="sxs-lookup"><span data-stu-id="a1cb6-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="a1cb6-115">國家及區域</span><span class="sxs-lookup"><span data-stu-id="a1cb6-115">Country and Region</span></span>
* <span data-ttu-id="a1cb6-116">國家 (地區)</span><span class="sxs-lookup"><span data-stu-id="a1cb6-116">Country</span></span>
* <span data-ttu-id="a1cb6-117">總計</span><span class="sxs-lookup"><span data-stu-id="a1cb6-117">Grand Total</span></span>

<span data-ttu-id="a1cb6-118">若要將其取代，您必須使用 `UNION ALL`；指定彙總明確需要傳回相同的結果：</span><span class="sxs-lookup"><span data-stu-id="a1cb6-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="a1cb6-119">對於 GROUPING SETS，我們必須做的是採用相同的主體，並且只建立我們想要查看之彙總層級的 UNION ALL 區段</span><span class="sxs-lookup"><span data-stu-id="a1cb6-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="a1cb6-120">Cube 選項</span><span class="sxs-lookup"><span data-stu-id="a1cb6-120">Cube options</span></span>
<span data-ttu-id="a1cb6-121">可以使用 UNION ALL 方法建立 GROUP BY WITH CUBE。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="a1cb6-122">問題是程式碼可能很快就會很麻煩且不易處理。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="a1cb6-123">若要避免此情形，您可以使用這項更進階的方法。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="a1cb6-124">使用上述範例。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-124">Let's use the example above.</span></span>

<span data-ttu-id="a1cb6-125">第一個步驟是定義 'cube'，其定義我們想要建立的所有彙總層級。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="a1cb6-126">請務必記下兩個衍生資料表的交叉聯結。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="a1cb6-127">這樣可以為我們產生所有層級。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-127">This generates all the levels for us.</span></span> <span data-ttu-id="a1cb6-128">其餘程式碼真的有格式化。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-128">The rest of the code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="a1cb6-129">CTAS 的結果如下所示：</span><span class="sxs-lookup"><span data-stu-id="a1cb6-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="a1cb6-130">第二個步驟是指定目標資料表來儲存過渡結果：</span><span class="sxs-lookup"><span data-stu-id="a1cb6-130">The second step is to specify a target table to store interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="a1cb6-131">第三個步驟是對執行彙總的資料行 cube 執行迴圈。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="a1cb6-132">查詢會為 #Cube 暫存資料表中的每個資料列執行一次，並將結果儲存在 #Results 暫存資料表中</span><span class="sxs-lookup"><span data-stu-id="a1cb6-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="a1cb6-133">最後，我們只需要從 #Results 暫存資料表讀取，就可以傳回結果</span><span class="sxs-lookup"><span data-stu-id="a1cb6-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="a1cb6-134">將程式碼分成區段，並產生迴圈建構，程式碼就會變得更容易管理及維護。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1cb6-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1cb6-135">Next steps</span></span>
<span data-ttu-id="a1cb6-136">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="a1cb6-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
