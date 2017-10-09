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
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a><span data-ttu-id="f134f-103">移轉您的 SQL 程式碼 tooSQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="f134f-103">Migrate your SQL code tooSQL Data Warehouse</span></span>
<span data-ttu-id="f134f-104">這篇文章會說明程式碼變更時，您可能需要 toomake 從另一個資料庫 tooSQL 資料倉儲移轉您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f134f-104">This article explains code changes you will probably need toomake when migrating your code from another database tooSQL Data Warehouse.</span></span> <span data-ttu-id="f134f-105">某些 SQL 資料倉儲功能可大幅提升效能，因為它們是設計的 toowork 分散式方式。</span><span class="sxs-lookup"><span data-stu-id="f134f-105">Some SQL Data Warehouse features can significantly improve performance as they are designed toowork in a distributed fashion.</span></span> <span data-ttu-id="f134f-106">不過，toomaintain 效能和小數位數，部分功能也無法使用。</span><span class="sxs-lookup"><span data-stu-id="f134f-106">However, toomaintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="f134f-107">常見 T-SQL 限制</span><span class="sxs-lookup"><span data-stu-id="f134f-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="f134f-108">hello 下列清單摘要說明 hello SQL 資料倉儲不支援的最常見功能。</span><span class="sxs-lookup"><span data-stu-id="f134f-108">hello following list summarizes hello most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="f134f-109">hello 連結會帶領您 tooworkarounds hello 不支援的功能：</span><span class="sxs-lookup"><span data-stu-id="f134f-109">hello links take you tooworkarounds for hello unsupported features:</span></span>

* <span data-ttu-id="f134f-110">[更新時的 ANSI 聯結][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="f134f-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="f134f-111">[刪除時的 ANSI 聯結][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="f134f-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="f134f-112">[merge 陳述式][merge statement]</span><span class="sxs-lookup"><span data-stu-id="f134f-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="f134f-113">跨資料庫聯結</span><span class="sxs-lookup"><span data-stu-id="f134f-113">cross-database joins</span></span>
* <span data-ttu-id="f134f-114">[資料指標][cursors]</span><span class="sxs-lookup"><span data-stu-id="f134f-114">[cursors][cursors]</span></span>
* <span data-ttu-id="f134f-115"><seg>
  [INSERT..EXEC][INSERT..EXEC]</seg></span><span class="sxs-lookup"><span data-stu-id="f134f-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="f134f-116">output 子句</span><span class="sxs-lookup"><span data-stu-id="f134f-116">output clause</span></span>
* <span data-ttu-id="f134f-117">內嵌使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="f134f-117">inline user-defined functions</span></span>
* <span data-ttu-id="f134f-118">多重陳述式函式</span><span class="sxs-lookup"><span data-stu-id="f134f-118">multi-statement functions</span></span>
* [<span data-ttu-id="f134f-119">通用資料表運算式</span><span class="sxs-lookup"><span data-stu-id="f134f-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="f134f-120">[遞迴通用資料表運算式 (CTE)](#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="f134f-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="f134f-121">CLR 函式和程序</span><span class="sxs-lookup"><span data-stu-id="f134f-121">CLR functions and procedures</span></span>
* <span data-ttu-id="f134f-122">$partition 函式</span><span class="sxs-lookup"><span data-stu-id="f134f-122">$partition function</span></span>
* <span data-ttu-id="f134f-123">資料表變數</span><span class="sxs-lookup"><span data-stu-id="f134f-123">table variables</span></span>
* <span data-ttu-id="f134f-124">資料表值參數</span><span class="sxs-lookup"><span data-stu-id="f134f-124">table value parameters</span></span>
* <span data-ttu-id="f134f-125">分散式交易</span><span class="sxs-lookup"><span data-stu-id="f134f-125">distributed transactions</span></span>
* <span data-ttu-id="f134f-126">認可/回復工作</span><span class="sxs-lookup"><span data-stu-id="f134f-126">commit / rollback work</span></span>
* <span data-ttu-id="f134f-127">儲存交易</span><span class="sxs-lookup"><span data-stu-id="f134f-127">save transaction</span></span>
* <span data-ttu-id="f134f-128">執行內容 (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="f134f-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="f134f-129">[group by 子句搭配 rollup / cube / grouping sets 選項][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="f134f-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="f134f-130">[巢狀層級超過 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="f134f-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="f134f-131">[透過檢視表更新][updating through views]</span><span class="sxs-lookup"><span data-stu-id="f134f-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="f134f-132">[使用 select 進行變數指派][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="f134f-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="f134f-133">[動態 SQL 字串沒有 MAX 資料類型][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="f134f-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="f134f-134">幸好這些限制大部分都可以克服。</span><span class="sxs-lookup"><span data-stu-id="f134f-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="f134f-135">上述的 hello 相關開發文件中提供說明。</span><span class="sxs-lookup"><span data-stu-id="f134f-135">Explanations are provided in hello relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="f134f-136">支援的 CTE 功能</span><span class="sxs-lookup"><span data-stu-id="f134f-136">Supported CTE features</span></span>
<span data-ttu-id="f134f-137">SQL 資料倉儲針對通用資料表運算式 (CTE) 提供部分支援。</span><span class="sxs-lookup"><span data-stu-id="f134f-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="f134f-138">目前支援下列 CTE 功能 hello:</span><span class="sxs-lookup"><span data-stu-id="f134f-138">hello following CTE features are currently supported:</span></span>

* <span data-ttu-id="f134f-139">CTE 可以指定於 SELECT 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="f134f-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="f134f-140">CTE 可以指定於 CREATE VIEW 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="f134f-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="f134f-141">CTE 可以指定於 CREATE TABLE AS SELECT (CTAS) 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="f134f-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="f134f-142">CTE 可以指定於 CREATE REMOTE TABLE AS SELECT (CRTAS) 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="f134f-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="f134f-143">CTE 可以指定於 CREATE EXTERNAL TABLE AS SELECT (CETAS) 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="f134f-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="f134f-144">遠端資料表可以參考自 CTE。</span><span class="sxs-lookup"><span data-stu-id="f134f-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="f134f-145">外部資料表可以參考自 CTE。</span><span class="sxs-lookup"><span data-stu-id="f134f-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="f134f-146">CTE 中可以定義多個 CTE 查詢定義。</span><span class="sxs-lookup"><span data-stu-id="f134f-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="f134f-147">CTE 限制</span><span class="sxs-lookup"><span data-stu-id="f134f-147">CTE Limitations</span></span>
<span data-ttu-id="f134f-148">通用資料表運算式在 SQL 資料倉儲中有某些限制，包含：</span><span class="sxs-lookup"><span data-stu-id="f134f-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="f134f-149">CTE 後面必須接著單一 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="f134f-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="f134f-150">INSERT、UPDATE、DELETE 和 MERGE 陳述式不受支援。</span><span class="sxs-lookup"><span data-stu-id="f134f-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="f134f-151">不支援通用資料表運算式，其中包含參考 tooitself （遞迴通用資料表運算式） （請參閱下一節）。</span><span class="sxs-lookup"><span data-stu-id="f134f-151">A common table expression that includes references tooitself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="f134f-152">不允許在 CTE 中指定多個 WITH 子句。</span><span class="sxs-lookup"><span data-stu-id="f134f-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="f134f-153">例如，如果 CTE_query_definition 包含子查詢，這個子查詢就不能包含定義另一個 CTE 的巢狀 WITH 子句。</span><span class="sxs-lookup"><span data-stu-id="f134f-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="f134f-154">ORDER BY 子句不能在 hello 個 CTE_query_definition，除了指定 TOP 子句。</span><span class="sxs-lookup"><span data-stu-id="f134f-154">An ORDER BY clause cannot be used in hello CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="f134f-155">CTE 陳述式中，批次的一部分使用時之前它, hello 陳述式必須後面跟著分號。</span><span class="sxs-lookup"><span data-stu-id="f134f-155">When a CTE is used in a statement that is part of a batch, hello statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="f134f-156">Cte sp_prepare 備妥的陳述式中使用時，將行為 hello 與 PDW 中其他 SELECT 陳述式相同的方式。</span><span class="sxs-lookup"><span data-stu-id="f134f-156">When used in statements prepared by sp_prepare, CTEs will behave hello same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="f134f-157">不過，如果使用 Cte CETAS sp_prepare 備妥的一部分，hello 行為可以延遲從 SQL Server 和其他 PDW 陳述式由於繫結，則實作 sp_prepare hello 方式。</span><span class="sxs-lookup"><span data-stu-id="f134f-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, hello behavior can defer from SQL Server and other PDW statements because of hello way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="f134f-158">如果參考 CTE 使用錯誤的資料行不存在於 CTE，hello sp_prepare 將卻未偵測 hello 錯誤可傳遞，但 hello 錯誤會改為擲回 sp_execute 期間選取。</span><span class="sxs-lookup"><span data-stu-id="f134f-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, hello sp_prepare will pass without detecting hello error, but hello error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="f134f-159">遞迴 CTE</span><span class="sxs-lookup"><span data-stu-id="f134f-159">Recursive CTEs</span></span>
<span data-ttu-id="f134f-160">SQL 資料倉儲並不支援遞迴 CTE。</span><span class="sxs-lookup"><span data-stu-id="f134f-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="f134f-161">遞迴 CTE 的 hello 移轉可能會稍微複雜，但 hello 最佳程序 toobreak 到多個步驟。</span><span class="sxs-lookup"><span data-stu-id="f134f-161">hello migration of recursive CTE can be somewhat complex and hello best process is toobreak it into multiple steps.</span></span> <span data-ttu-id="f134f-162">通常，您可以使用迴圈，並填入的暫存資料表，當您逐一查看 hello 遞迴暫時查詢。</span><span class="sxs-lookup"><span data-stu-id="f134f-162">You can typically use a loop and populate a temporary table as you iterate over hello recursive interim queries.</span></span> <span data-ttu-id="f134f-163">Hello 暫存資料表填入之後您就可以傳回 hello 資料做為單一結果集。</span><span class="sxs-lookup"><span data-stu-id="f134f-163">Once hello temporary table is populated you can then return hello data as a single result set.</span></span> <span data-ttu-id="f134f-164">類似的方法已經使用的 toosolve`GROUP BY WITH CUBE`在 hello[分組子句的彙總] / [cube] / [群組集選項][ group by clause with rollup / cube / grouping sets options]發行項。</span><span class="sxs-lookup"><span data-stu-id="f134f-164">A similar approach has been used toosolve `GROUP BY WITH CUBE` in hello [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="f134f-165">不支援的系統函式</span><span class="sxs-lookup"><span data-stu-id="f134f-165">Unsupported system functions</span></span>
<span data-ttu-id="f134f-166">另外還有一些不支援的系統函式。</span><span class="sxs-lookup"><span data-stu-id="f134f-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="f134f-167">Hello 主要的您覺得通常用於資料倉儲中的部分包括：</span><span class="sxs-lookup"><span data-stu-id="f134f-167">Some of hello main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="f134f-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="f134f-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="f134f-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="f134f-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="f134f-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="f134f-170">@@IDENTITY()</span></span>
* <span data-ttu-id="f134f-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="f134f-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="f134f-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="f134f-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="f134f-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="f134f-173">ERROR_LINE()</span></span>

<span data-ttu-id="f134f-174">這些問題中有部分可以解決。</span><span class="sxs-lookup"><span data-stu-id="f134f-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="f134f-175">@@ROWCOUNT 因應措施</span><span class="sxs-lookup"><span data-stu-id="f134f-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="f134f-176">不支援 @ 周圍 toowork@ROWCOUNT，建立的預存程序會擷取 sys.dm_pdw_request_steps hello 最後一個資料列計數，然後執行`EXEC LastRowCount`DML 陳述式之後。</span><span class="sxs-lookup"><span data-stu-id="f134f-176">toowork around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve hello last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f134f-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f134f-177">Next steps</span></span>
<span data-ttu-id="f134f-178">如需所有所支援 T-SQL 陳述式的完整清單，請參閱 [Transact-SQL 主題][Transact-SQL topics]。</span><span class="sxs-lookup"><span data-stu-id="f134f-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

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
