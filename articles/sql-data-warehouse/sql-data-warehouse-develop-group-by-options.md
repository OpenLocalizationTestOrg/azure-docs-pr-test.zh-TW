---
title: "SQL 資料倉儲中的選項所 aaaGroup |Microsoft 文件"
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
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="52edd-103">根據 SQL 資料倉儲中的選項分組</span><span class="sxs-lookup"><span data-stu-id="52edd-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="52edd-104">hello [GROUP BY] [ GROUP BY]子句用 tooaggregate 資料 tooa 摘要資料列集。</span><span class="sxs-lookup"><span data-stu-id="52edd-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="52edd-105">它也有一些克服 Azure SQL 資料倉儲不直接支援該需求 toobe 擴充其功能的選項。</span><span class="sxs-lookup"><span data-stu-id="52edd-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="52edd-106">可用選項包括</span><span class="sxs-lookup"><span data-stu-id="52edd-106">These options are</span></span>

* <span data-ttu-id="52edd-107">GROUP BY 搭配 ROLLUP</span><span class="sxs-lookup"><span data-stu-id="52edd-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="52edd-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="52edd-108">GROUPING SETS</span></span>
* <span data-ttu-id="52edd-109">GROUP BY 搭配 CUBE</span><span class="sxs-lookup"><span data-stu-id="52edd-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="52edd-110">Rollup 和 grouping sets 選項</span><span class="sxs-lookup"><span data-stu-id="52edd-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="52edd-111">hello 最簡單的選項是 toouse`UNION ALL`改為 tooperform hello 彙總套件，而不是依賴 hello 明確的語法。</span><span class="sxs-lookup"><span data-stu-id="52edd-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="52edd-112">hello 結果完全 hello 相同</span><span class="sxs-lookup"><span data-stu-id="52edd-112">hello result is exactly hello same</span></span>

<span data-ttu-id="52edd-113">以下是範例的 group by 陳述式使用 hello`ROLLUP`選項：</span><span class="sxs-lookup"><span data-stu-id="52edd-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

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

<span data-ttu-id="52edd-114">使用彙總我們要求要有下列彙總的 hello:</span><span class="sxs-lookup"><span data-stu-id="52edd-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="52edd-115">國家及區域</span><span class="sxs-lookup"><span data-stu-id="52edd-115">Country and Region</span></span>
* <span data-ttu-id="52edd-116">國家 (地區)</span><span class="sxs-lookup"><span data-stu-id="52edd-116">Country</span></span>
* <span data-ttu-id="52edd-117">總計</span><span class="sxs-lookup"><span data-stu-id="52edd-117">Grand Total</span></span>

<span data-ttu-id="52edd-118">tooreplace 此您將需要 toouse `UNION ALL`; 指定所需明確的 hello 彙總是 tooreturn hello 相同的結果：</span><span class="sxs-lookup"><span data-stu-id="52edd-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

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

<span data-ttu-id="52edd-119">我們對於我們只需要 toodo 是採用 GROUPING SETS hello 主體相同，但僅建立彙總層級 hello 的 UNION ALL 區段想 toosee</span><span class="sxs-lookup"><span data-stu-id="52edd-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="52edd-120">Cube 選項</span><span class="sxs-lookup"><span data-stu-id="52edd-120">Cube options</span></span>
<span data-ttu-id="52edd-121">它是可能 toocreate GROUP BY WITH CUBE 使用 hello UNION ALL 方法。</span><span class="sxs-lookup"><span data-stu-id="52edd-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="52edd-122">hello 問題是，hello 程式碼可能很快就會相當繁雜而不便。</span><span class="sxs-lookup"><span data-stu-id="52edd-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="52edd-123">toomitigate 此您可以使用這個更進階的方法。</span><span class="sxs-lookup"><span data-stu-id="52edd-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="52edd-124">我們將使用上述的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="52edd-124">Let's use hello example above.</span></span>

<span data-ttu-id="52edd-125">hello 第一個步驟為 toodefine hello 'cube' 可定義所有彙總我們想要 toocreate hello 層級。</span><span class="sxs-lookup"><span data-stu-id="52edd-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="52edd-126">Hello 兩個衍生資料表的交叉聯結的 hello 重要 tootake 記下它。</span><span class="sxs-lookup"><span data-stu-id="52edd-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="52edd-127">這會產生所有 hello 層級給我們。</span><span class="sxs-lookup"><span data-stu-id="52edd-127">This generates all hello levels for us.</span></span> <span data-ttu-id="52edd-128">hello 其餘的 hello 程式碼真的有格式化。</span><span class="sxs-lookup"><span data-stu-id="52edd-128">hello rest of hello code is really there for formatting.</span></span>

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

<span data-ttu-id="52edd-129">hello hello 結果 CTAS 可以看到如下：</span><span class="sxs-lookup"><span data-stu-id="52edd-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="52edd-130">hello 第二個步驟是的 toospecify 目標資料表 toostore 暫時結果：</span><span class="sxs-lookup"><span data-stu-id="52edd-130">hello second step is toospecify a target table toostore interim results:</span></span>

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

<span data-ttu-id="52edd-131">hello 第三個步驟是 tooloop 針對我們的資料行執行 hello 彙總的 cube。</span><span class="sxs-lookup"><span data-stu-id="52edd-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="52edd-132">hello 查詢將 hello #Cube 暫存資料表中每個資料列執行一次，而且 hello 結果儲存在 hello #Results 暫存資料表</span><span class="sxs-lookup"><span data-stu-id="52edd-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

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

<span data-ttu-id="52edd-133">最後我們可以傳回的只讀取 hello #Results 暫存資料表中的 hello 結果</span><span class="sxs-lookup"><span data-stu-id="52edd-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="52edd-134">Hello 程式碼分成區段，並產生迴圈建構 hello 程式碼變得更容易管理而且更容易維護。</span><span class="sxs-lookup"><span data-stu-id="52edd-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52edd-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52edd-135">Next steps</span></span>
<span data-ttu-id="52edd-136">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="52edd-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
