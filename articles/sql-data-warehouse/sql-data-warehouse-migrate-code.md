---
title: "將您的 SQL 程式碼移轉至 SQL 資料倉儲 | Microsoft Docs"
description: "將 SQL 程式碼移轉至 Azure SQL 資料倉儲來開發解決方案的秘訣。"
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
ms.openlocfilehash: c6e6b890f5e2d0e31b10bbb6803adad02bf60248
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-code-to-sql-data-warehouse"></a><span data-ttu-id="13547-103">將您的 SQL 程式碼移轉至 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="13547-103">Migrate your SQL code to SQL Data Warehouse</span></span>
<span data-ttu-id="13547-104">本文說明將您的程式碼從另一個資料庫移轉到 SQL 資料倉儲時，可能需要進行的程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="13547-104">This article explains code changes you will probably need to make when migrating your code from another database to SQL Data Warehouse.</span></span> <span data-ttu-id="13547-105">某些 SQL 資料倉儲功能設計為以分散式方式運作，可以大幅改善效能。</span><span class="sxs-lookup"><span data-stu-id="13547-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span></span> <span data-ttu-id="13547-106">不過，為了維持效能和延展性，某些功能也無法使用。</span><span class="sxs-lookup"><span data-stu-id="13547-106">However, to maintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="13547-107">常見 T-SQL 限制</span><span class="sxs-lookup"><span data-stu-id="13547-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="13547-108">下列清單摘要說明 SQL 資料倉儲不支援的最常見功能。</span><span class="sxs-lookup"><span data-stu-id="13547-108">The following list summarizes the most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="13547-109">此連結會帶您前往不支援功能的因應措施：</span><span class="sxs-lookup"><span data-stu-id="13547-109">The links take you to workarounds for the unsupported features:</span></span>

* <span data-ttu-id="13547-110">[更新時的 ANSI 聯結][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="13547-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="13547-111">[刪除時的 ANSI 聯結][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="13547-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="13547-112">[merge 陳述式][merge statement]</span><span class="sxs-lookup"><span data-stu-id="13547-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="13547-113">跨資料庫聯結</span><span class="sxs-lookup"><span data-stu-id="13547-113">cross-database joins</span></span>
* <span data-ttu-id="13547-114">[資料指標][cursors]</span><span class="sxs-lookup"><span data-stu-id="13547-114">[cursors][cursors]</span></span>
* <span data-ttu-id="13547-115"><seg>
  [INSERT..EXEC][INSERT..EXEC]</seg></span><span class="sxs-lookup"><span data-stu-id="13547-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="13547-116">output 子句</span><span class="sxs-lookup"><span data-stu-id="13547-116">output clause</span></span>
* <span data-ttu-id="13547-117">內嵌使用者定義函數</span><span class="sxs-lookup"><span data-stu-id="13547-117">inline user-defined functions</span></span>
* <span data-ttu-id="13547-118">多重陳述式函式</span><span class="sxs-lookup"><span data-stu-id="13547-118">multi-statement functions</span></span>
* [<span data-ttu-id="13547-119">通用資料表運算式</span><span class="sxs-lookup"><span data-stu-id="13547-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="13547-120">[遞迴通用資料表運算式 (CTE)](#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="13547-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="13547-121">CLR 函式和程序</span><span class="sxs-lookup"><span data-stu-id="13547-121">CLR functions and procedures</span></span>
* <span data-ttu-id="13547-122">$partition 函式</span><span class="sxs-lookup"><span data-stu-id="13547-122">$partition function</span></span>
* <span data-ttu-id="13547-123">資料表變數</span><span class="sxs-lookup"><span data-stu-id="13547-123">table variables</span></span>
* <span data-ttu-id="13547-124">資料表值參數</span><span class="sxs-lookup"><span data-stu-id="13547-124">table value parameters</span></span>
* <span data-ttu-id="13547-125">分散式交易</span><span class="sxs-lookup"><span data-stu-id="13547-125">distributed transactions</span></span>
* <span data-ttu-id="13547-126">認可/回復工作</span><span class="sxs-lookup"><span data-stu-id="13547-126">commit / rollback work</span></span>
* <span data-ttu-id="13547-127">儲存交易</span><span class="sxs-lookup"><span data-stu-id="13547-127">save transaction</span></span>
* <span data-ttu-id="13547-128">執行內容 (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="13547-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="13547-129">[group by 子句搭配 rollup / cube / grouping sets 選項][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="13547-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="13547-130">[巢狀層級超過 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="13547-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="13547-131">[透過檢視表更新][updating through views]</span><span class="sxs-lookup"><span data-stu-id="13547-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="13547-132">[使用 select 進行變數指派][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="13547-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="13547-133">[動態 SQL 字串沒有 MAX 資料類型][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="13547-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="13547-134">幸好這些限制大部分都可以克服。</span><span class="sxs-lookup"><span data-stu-id="13547-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="13547-135">上面提及的相關開發文章中已提供說明。</span><span class="sxs-lookup"><span data-stu-id="13547-135">Explanations are provided in the relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="13547-136">支援的 CTE 功能</span><span class="sxs-lookup"><span data-stu-id="13547-136">Supported CTE features</span></span>
<span data-ttu-id="13547-137">SQL 資料倉儲針對通用資料表運算式 (CTE) 提供部分支援。</span><span class="sxs-lookup"><span data-stu-id="13547-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="13547-138">目前支援下列 CTE 功能：</span><span class="sxs-lookup"><span data-stu-id="13547-138">The following CTE features are currently supported:</span></span>

* <span data-ttu-id="13547-139">CTE 可以指定於 SELECT 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="13547-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="13547-140">CTE 可以指定於 CREATE VIEW 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="13547-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="13547-141">CTE 可以指定於 CREATE TABLE AS SELECT (CTAS) 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="13547-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="13547-142">CTE 可以指定於 CREATE REMOTE TABLE AS SELECT (CRTAS) 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="13547-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="13547-143">CTE 可以指定於 CREATE EXTERNAL TABLE AS SELECT (CETAS) 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="13547-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="13547-144">遠端資料表可以參考自 CTE。</span><span class="sxs-lookup"><span data-stu-id="13547-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="13547-145">外部資料表可以參考自 CTE。</span><span class="sxs-lookup"><span data-stu-id="13547-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="13547-146">CTE 中可以定義多個 CTE 查詢定義。</span><span class="sxs-lookup"><span data-stu-id="13547-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="13547-147">CTE 限制</span><span class="sxs-lookup"><span data-stu-id="13547-147">CTE Limitations</span></span>
<span data-ttu-id="13547-148">通用資料表運算式在 SQL 資料倉儲中有某些限制，包含：</span><span class="sxs-lookup"><span data-stu-id="13547-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="13547-149">CTE 後面必須接著單一 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="13547-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="13547-150">INSERT、UPDATE、DELETE 和 MERGE 陳述式不受支援。</span><span class="sxs-lookup"><span data-stu-id="13547-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="13547-151">包含自身參考 (遞迴通用資料表運算式) 的通用資料表運算式不受支援 (請參閱下一節)。</span><span class="sxs-lookup"><span data-stu-id="13547-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="13547-152">不允許在 CTE 中指定多個 WITH 子句。</span><span class="sxs-lookup"><span data-stu-id="13547-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="13547-153">例如，如果 CTE_query_definition 包含子查詢，這個子查詢就不能包含定義另一個 CTE 的巢狀 WITH 子句。</span><span class="sxs-lookup"><span data-stu-id="13547-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="13547-154">ORDER BY 子句不能用於 CTE_query_definition 中，除非有指定 TOP 子句。</span><span class="sxs-lookup"><span data-stu-id="13547-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="13547-155">當某批次中的陳述式使用 CTE 時，它前面的陳述式後面必須接著分號。</span><span class="sxs-lookup"><span data-stu-id="13547-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="13547-156">在用於 sp_prepare 所準備的陳述式時，CTE 的行為會與 PDW 中的其他 SELECT 陳述式相同。</span><span class="sxs-lookup"><span data-stu-id="13547-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="13547-157">不過，如果 CTE 是做為 sp_prepare 所準備之 CETAS 中的一部分時，就會因為針對 sp_prepare 實作繫結的方式而導致其行為與 SQL Server 和其他 PDW 陳述式不同。</span><span class="sxs-lookup"><span data-stu-id="13547-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="13547-158">如果參考 CTE 的 SELECT 使用不存在於 CTE 的錯誤資料行，sp_prepare 將會通過而不會偵測到錯誤，但在 sp_execute 期間則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="13547-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="13547-159">遞迴 CTE</span><span class="sxs-lookup"><span data-stu-id="13547-159">Recursive CTEs</span></span>
<span data-ttu-id="13547-160">SQL 資料倉儲並不支援遞迴 CTE。</span><span class="sxs-lookup"><span data-stu-id="13547-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="13547-161">遞迴 CTE 的移轉可能會有點複雜，而最佳做法便是將它細分成多個步驟。</span><span class="sxs-lookup"><span data-stu-id="13547-161">The migration of recursive CTE can be somewhat complex and the best process is to break it into multiple steps.</span></span> <span data-ttu-id="13547-162">一般來說，您可以使用迴圈，並在逐一執行遞迴中間的查詢時填入暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="13547-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span></span> <span data-ttu-id="13547-163">一旦暫存資料表填完之後，您可以將資料傳回做為單一結果集。</span><span class="sxs-lookup"><span data-stu-id="13547-163">Once the temporary table is populated you can then return the data as a single result set.</span></span> <span data-ttu-id="13547-164">[group by 子句搭配 rollup / cube / grouping sets 選項][group by clause with rollup / cube / grouping sets options]一文中使用類似的方法來解決 `GROUP BY WITH CUBE`。</span><span class="sxs-lookup"><span data-stu-id="13547-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="13547-165">不支援的系統函式</span><span class="sxs-lookup"><span data-stu-id="13547-165">Unsupported system functions</span></span>
<span data-ttu-id="13547-166">另外還有一些不支援的系統函式。</span><span class="sxs-lookup"><span data-stu-id="13547-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="13547-167">您通常可能會發現資料倉儲中使用的主要函式包括：</span><span class="sxs-lookup"><span data-stu-id="13547-167">Some of the main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="13547-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="13547-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="13547-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="13547-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="13547-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="13547-170">@@IDENTITY()</span></span>
* <span data-ttu-id="13547-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="13547-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="13547-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="13547-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="13547-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="13547-173">ERROR_LINE()</span></span>

<span data-ttu-id="13547-174">這些問題中有部分可以解決。</span><span class="sxs-lookup"><span data-stu-id="13547-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="13547-175">@@ROWCOUNT 因應措施</span><span class="sxs-lookup"><span data-stu-id="13547-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="13547-176">若要解決缺乏 @@ROWCOUNT 支援的問題，請建立會從 sys.dm_pdw_request_steps 擷取最後一個資料列計數的預存程序，然後在 DML 陳述式之後執行 `EXEC LastRowCount`。</span><span class="sxs-lookup"><span data-stu-id="13547-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="13547-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13547-177">Next steps</span></span>
<span data-ttu-id="13547-178">如需所有所支援 T-SQL 陳述式的完整清單，請參閱 [Transact-SQL 主題][Transact-SQL topics]。</span><span class="sxs-lookup"><span data-stu-id="13547-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

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
