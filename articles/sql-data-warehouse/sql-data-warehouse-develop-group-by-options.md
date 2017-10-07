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
# <a name="group-by-options-in-sql-data-warehouse"></a>根據 SQL 資料倉儲中的選項分組
hello [GROUP BY] [ GROUP BY]子句用 tooaggregate 資料 tooa 摘要資料列集。 它也有一些克服 Azure SQL 資料倉儲不直接支援該需求 toobe 擴充其功能的選項。

可用選項包括

* GROUP BY 搭配 ROLLUP
* GROUPING SETS
* GROUP BY 搭配 CUBE

## <a name="rollup-and-grouping-sets-options"></a>Rollup 和 grouping sets 選項
hello 最簡單的選項是 toouse`UNION ALL`改為 tooperform hello 彙總套件，而不是依賴 hello 明確的語法。 hello 結果完全 hello 相同

以下是範例的 group by 陳述式使用 hello`ROLLUP`選項：

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

使用彙總我們要求要有下列彙總的 hello:

* 國家及區域
* 國家 (地區)
* 總計

tooreplace 此您將需要 toouse `UNION ALL`; 指定所需明確的 hello 彙總是 tooreturn hello 相同的結果：

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

我們對於我們只需要 toodo 是採用 GROUPING SETS hello 主體相同，但僅建立彙總層級 hello 的 UNION ALL 區段想 toosee

## <a name="cube-options"></a>Cube 選項
它是可能 toocreate GROUP BY WITH CUBE 使用 hello UNION ALL 方法。 hello 問題是，hello 程式碼可能很快就會相當繁雜而不便。 toomitigate 此您可以使用這個更進階的方法。

我們將使用上述的 hello 範例。

hello 第一個步驟為 toodefine hello 'cube' 可定義所有彙總我們想要 toocreate hello 層級。 Hello 兩個衍生資料表的交叉聯結的 hello 重要 tootake 記下它。 這會產生所有 hello 層級給我們。 hello 其餘的 hello 程式碼真的有格式化。

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

hello hello 結果 CTAS 可以看到如下：

![][1]

hello 第二個步驟是的 toospecify 目標資料表 toostore 暫時結果：

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

hello 第三個步驟是 tooloop 針對我們的資料行執行 hello 彙總的 cube。 hello 查詢將 hello #Cube 暫存資料表中每個資料列執行一次，而且 hello 結果儲存在 hello #Results 暫存資料表

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

最後我們可以傳回的只讀取 hello #Results 暫存資料表中的 hello 結果

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Hello 程式碼分成區段，並產生迴圈建構 hello 程式碼變得更容易管理而且更容易維護。

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
