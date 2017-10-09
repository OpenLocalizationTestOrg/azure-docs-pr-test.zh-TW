---
title: "aaaMigrate 您資料倉儲的 SQL 程式碼 tooSQL |Microsoft 文件"
description: "移轉您的 SQL 程式碼 tooAzure SQL 資料倉儲來開發方案的提示。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>移轉您的 SQL 程式碼 tooSQL 資料倉儲
這篇文章會說明程式碼變更時，您可能需要 toomake 從另一個資料庫 tooSQL 資料倉儲移轉您的程式碼。 某些 SQL 資料倉儲功能可大幅提升效能，因為它們是設計的 toowork 分散式方式。 不過，toomaintain 效能和小數位數，部分功能也無法使用。

## <a name="common-t-sql-limitations"></a>常見 T-SQL 限制
hello 下列清單摘要說明 hello SQL 資料倉儲不支援的最常見功能。 hello 連結會帶領您 tooworkarounds hello 不支援的功能：

* [更新時的 ANSI 聯結][ANSI joins on updates]
* [刪除時的 ANSI 聯結][ANSI joins on deletes]
* [merge 陳述式][merge statement]
* 跨資料庫聯結
* [資料指標][cursors]
* <seg>
  [INSERT..EXEC][INSERT..EXEC]</seg>
* output 子句
* 內嵌使用者定義函數
* 多重陳述式函式
* [通用資料表運算式](#Common-table-expressions)
* [遞迴通用資料表運算式 (CTE)](#Recursive-common-table-expressions-(CTE)
* CLR 函式和程序
* $partition 函式
* 資料表變數
* 資料表值參數
* 分散式交易
* 認可/回復工作
* 儲存交易
* 執行內容 (EXECUTE AS)
* [group by 子句搭配 rollup / cube / grouping sets 選項][group by clause with rollup / cube / grouping sets options]
* [巢狀層級超過 8][nesting levels beyond 8]
* [透過檢視表更新][updating through views]
* [使用 select 進行變數指派][use of select for variable assignment]
* [動態 SQL 字串沒有 MAX 資料類型][no MAX data type for dynamic SQL strings]

幸好這些限制大部分都可以克服。 上述的 hello 相關開發文件中提供說明。

## <a name="supported-cte-features"></a>支援的 CTE 功能
SQL 資料倉儲針對通用資料表運算式 (CTE) 提供部分支援。  目前支援下列 CTE 功能 hello:

* CTE 可以指定於 SELECT 陳述式中。
* CTE 可以指定於 CREATE VIEW 陳述式中。
* CTE 可以指定於 CREATE TABLE AS SELECT (CTAS) 陳述式中。
* CTE 可以指定於 CREATE REMOTE TABLE AS SELECT (CRTAS) 陳述式中。
* CTE 可以指定於 CREATE EXTERNAL TABLE AS SELECT (CETAS) 陳述式中。
* 遠端資料表可以參考自 CTE。
* 外部資料表可以參考自 CTE。
* CTE 中可以定義多個 CTE 查詢定義。

## <a name="cte-limitations"></a>CTE 限制
通用資料表運算式在 SQL 資料倉儲中有某些限制，包含：

* CTE 後面必須接著單一 SELECT 陳述式。 INSERT、UPDATE、DELETE 和 MERGE 陳述式不受支援。
* 不支援通用資料表運算式，其中包含參考 tooitself （遞迴通用資料表運算式） （請參閱下一節）。
* 不允許在 CTE 中指定多個 WITH 子句。 例如，如果 CTE_query_definition 包含子查詢，這個子查詢就不能包含定義另一個 CTE 的巢狀 WITH 子句。
* ORDER BY 子句不能在 hello 個 CTE_query_definition，除了指定 TOP 子句。
* CTE 陳述式中，批次的一部分使用時之前它, hello 陳述式必須後面跟著分號。
* Cte sp_prepare 備妥的陳述式中使用時，將行為 hello 與 PDW 中其他 SELECT 陳述式相同的方式。 不過，如果使用 Cte CETAS sp_prepare 備妥的一部分，hello 行為可以延遲從 SQL Server 和其他 PDW 陳述式由於繫結，則實作 sp_prepare hello 方式。 如果參考 CTE 使用錯誤的資料行不存在於 CTE，hello sp_prepare 將卻未偵測 hello 錯誤可傳遞，但 hello 錯誤會改為擲回 sp_execute 期間選取。

## <a name="recursive-ctes"></a>遞迴 CTE
SQL 資料倉儲並不支援遞迴 CTE。  遞迴 CTE 的 hello 移轉可能會稍微複雜，但 hello 最佳程序 toobreak 到多個步驟。 通常，您可以使用迴圈，並填入的暫存資料表，當您逐一查看 hello 遞迴暫時查詢。 Hello 暫存資料表填入之後您就可以傳回 hello 資料做為單一結果集。 類似的方法已經使用的 toosolve`GROUP BY WITH CUBE`在 hello[分組子句的彙總] / [cube] / [群組集選項][ group by clause with rollup / cube / grouping sets options]發行項。

## <a name="unsupported-system-functions"></a>不支援的系統函式
另外還有一些不支援的系統函式。 Hello 主要的您覺得通常用於資料倉儲中的部分包括：

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE()

這些問題中有部分可以解決。

## <a name="rowcount-workaround"></a>@@ROWCOUNT 因應措施
不支援 @ 周圍 toowork@ROWCOUNT，建立的預存程序會擷取 sys.dm_pdw_request_steps hello 最後一個資料列計數，然後執行`EXEC LastRowCount`DML 陳述式之後。

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a>後續步驟
如需所有所支援 T-SQL 陳述式的完整清單，請參閱 [Transact-SQL 主題][Transact-SQL topics]。

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
