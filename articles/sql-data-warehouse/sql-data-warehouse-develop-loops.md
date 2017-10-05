---
title: "在 Azure SQL 資料倉儲中採用 T-SQL 迴圈 | Microsoft Docs"
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
ms.openlocfilehash: 40a872ff310f48bfd543ac184fe7301b85b50258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="398e7-103">SQL 資料倉儲中的迴圈</span><span class="sxs-lookup"><span data-stu-id="398e7-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="398e7-104">SQL 資料倉儲支援 [WHILE][WHILE] 迴圈重複執行陳述式區塊。</span><span class="sxs-lookup"><span data-stu-id="398e7-104">SQL Data Warehouse supports the [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="398e7-105">只要指定的條件都成立，或者在程式碼使用 `BREAK` 關鍵字特別終止迴圈之前，這個情況都會繼續下去。</span><span class="sxs-lookup"><span data-stu-id="398e7-105">This will continue for as long as the specified conditions are true or until the code specifically terminates the loop using the `BREAK` keyword.</span></span> <span data-ttu-id="398e7-106">迴圈特別適用於取代 SQL 程式碼中定義的資料指標。</span><span class="sxs-lookup"><span data-stu-id="398e7-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="398e7-107">幸運的是，幾乎所有以 SQL 程式碼撰寫的資料指標都是向前快轉，並且只讀取多樣性。</span><span class="sxs-lookup"><span data-stu-id="398e7-107">Fortunately, almost all cursors that are written in SQL code are of the fast forward, read only variety.</span></span> <span data-ttu-id="398e7-108">因此，如果您發現自己必須將其取代， [WHILE] 迴圈是絕佳的替代方案。</span><span class="sxs-lookup"><span data-stu-id="398e7-108">Therefore [WHILE] loops are a great alternative if you find yourself having to replace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="398e7-109">運用迴圈和取代 SQL 資料倉儲中的資料指標</span><span class="sxs-lookup"><span data-stu-id="398e7-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="398e7-110">不過，在深入說明之前，您應該先自問下列問題：「這個資料指標是否能重新撰寫以使用集合型作業？」。</span><span class="sxs-lookup"><span data-stu-id="398e7-110">However, before diving in head first you should ask yourself the following question: "Could this cursor be re-written to use set based operations?".</span></span> <span data-ttu-id="398e7-111">在許多狀況下答案是肯定的，通常也是最佳方案。</span><span class="sxs-lookup"><span data-stu-id="398e7-111">In many cases the answer will be yes and is often the best approach.</span></span> <span data-ttu-id="398e7-112">集合型作業的執行速度通常會比反覆的逐列方法還要快。</span><span class="sxs-lookup"><span data-stu-id="398e7-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="398e7-113">向前快轉唯讀資料指標可以輕鬆地以迴圈建構取代。</span><span class="sxs-lookup"><span data-stu-id="398e7-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="398e7-114">以下是簡單的範例：</span><span class="sxs-lookup"><span data-stu-id="398e7-114">Below is a simple example.</span></span> <span data-ttu-id="398e7-115">程式碼範例會更新資料庫中每個資料表的統計資料。</span><span class="sxs-lookup"><span data-stu-id="398e7-115">This code example updates the statistics for every table in the database.</span></span> <span data-ttu-id="398e7-116">藉由反覆迴圈中的資料表，我們就能夠依序執行每個命令。</span><span class="sxs-lookup"><span data-stu-id="398e7-116">By iterating over the tables in the loop we are able to execute each command in sequence.</span></span>

<span data-ttu-id="398e7-117">首先，建立暫存資料表，其中包含用來識別個別陳述式的唯一資料列數目：</span><span class="sxs-lookup"><span data-stu-id="398e7-117">First, create a temporary table containing a unique row number used to identify the individual statements:</span></span>

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

<span data-ttu-id="398e7-118">其次，初始化執行迴圈的必要變數：</span><span class="sxs-lookup"><span data-stu-id="398e7-118">Second, initialize the variables required to perform the loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="398e7-119">現在每次對一個陳數式執行一次迴圈：</span><span class="sxs-lookup"><span data-stu-id="398e7-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="398e7-120">最後，將第一個步驟中建立的暫存資料表卸除</span><span class="sxs-lookup"><span data-stu-id="398e7-120">Finally drop the temporary table created in the first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="398e7-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="398e7-121">Next steps</span></span>
<span data-ttu-id="398e7-122">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="398e7-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
<span data-ttu-id="398e7-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span><span class="sxs-lookup"><span data-stu-id="398e7-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span></span>


<!--Other Web references-->
