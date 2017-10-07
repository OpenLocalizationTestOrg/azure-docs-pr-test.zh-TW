---
title: "Azure SQL 資料倉儲中執行迴圈的 aaaLeverage T-SQL |Microsoft 文件"
description: "在 Azure SQL 資料倉儲中使用 Transact-SQL 迴圈及取代資料指標以開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a>SQL 資料倉儲中的迴圈
SQL 資料倉儲支援 hello[時][時]迴圈重複執行陳述式區塊。 這將會持續 hello 程式碼，只要 hello 指定條件為 true，或直到特別終止 hello 迴圈使用 hello`BREAK`關鍵字。 迴圈特別適用於取代 SQL 程式碼中定義的資料指標。 幸運的是，幾乎所有的資料指標中的 SQL 程式碼所撰寫的 hello 快速轉寄、 讀取只各種不同。 因此[時]迴圈是絕佳的替代方案，如果您發現自己需要 tooreplace 其中一個。

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>運用迴圈和取代 SQL 資料倉儲中的資料指標
但是之前先深入標頭, 應該詢問自己下列問題 hello: 「 這個資料指標可以重新撰寫 toouse 集基礎的作業嗎？ 」。 在許多情況下 hello 回應會是 [是]，且通常 hello 最好的方法。 集合型作業的執行速度通常會比反覆的逐列方法還要快。

向前快轉唯讀資料指標可以輕鬆地以迴圈建構取代。 以下是簡單的範例： 這個程式碼範例會更新每個資料庫資料表中 hello hello 統計資料。 藉由我們反覆 hello 迴圈中的 hello 資料表所能 tooexecute 序列中的每個命令。

首先，建立暫存資料表，其中包含唯一的資料列數字使用的 tooidentify hello 個別陳述式：

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

第二，初始化 hello 變數需要的 tooperform hello 迴圈：

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

現在每次對一個陳數式執行一次迴圈：

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

最後卸除 hello hello 第一個步驟中建立的暫存資料表

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[時]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
