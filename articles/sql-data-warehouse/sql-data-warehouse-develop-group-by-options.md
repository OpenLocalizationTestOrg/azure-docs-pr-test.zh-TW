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
# <a name="group-by-options-in-sql-data-warehouse"></a>根據 SQL 資料倉儲中的選項分組
[GROUP BY][GROUP BY] 子句是用來將資料彙總至摘要的一組資料列。 它也具有一些擴充其功能的選項，這些選項都需要克服，因為 Azure SQL 資料倉儲並不直接支援這些選項。

可用選項包括

* GROUP BY 搭配 ROLLUP
* GROUPING SETS
* GROUP BY 搭配 CUBE

## <a name="rollup-and-grouping-sets-options"></a>Rollup 和 grouping sets 選項
此處最簡單的選項是改為使用 `UNION ALL` 來執行彙總，而不是依賴明確的語法。 應該會出現幾乎相同的結果

以下是使用 `ROLLUP` 選項的 group by 陳述式範例：

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

藉由使用 ROLLUP，我們要求下列彙總：

* 國家及區域
* 國家 (地區)
* 總計

若要將其取代，您必須使用 `UNION ALL`；指定彙總明確需要傳回相同的結果：

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

對於 GROUPING SETS，我們必須做的是採用相同的主體，並且只建立我們想要查看之彙總層級的 UNION ALL 區段

## <a name="cube-options"></a>Cube 選項
可以使用 UNION ALL 方法建立 GROUP BY WITH CUBE。 問題是程式碼可能很快就會很麻煩且不易處理。 若要避免此情形，您可以使用這項更進階的方法。

使用上述範例。

第一個步驟是定義 'cube'，其定義我們想要建立的所有彙總層級。 請務必記下兩個衍生資料表的交叉聯結。 這樣可以為我們產生所有層級。 其餘程式碼真的有格式化。

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

CTAS 的結果如下所示：

![][1]

第二個步驟是指定目標資料表來儲存過渡結果：

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

第三個步驟是對執行彙總的資料行 cube 執行迴圈。 查詢會為 #Cube 暫存資料表中的每個資料列執行一次，並將結果儲存在 #Results 暫存資料表中

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

最後，我們只需要從 #Results 暫存資料表讀取，就可以傳回結果

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

將程式碼分成區段，並產生迴圈建構，程式碼就會變得更容易管理及維護。

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
