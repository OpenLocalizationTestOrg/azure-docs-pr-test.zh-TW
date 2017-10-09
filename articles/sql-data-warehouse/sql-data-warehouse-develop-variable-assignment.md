---
title: "SQL 資料倉儲中的 aaaAssign 變數 |Microsoft 文件"
description: "在 Azure SQL 資料倉儲中指派 TRANSACT-SQL 變數以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="d0f8b-103">在 SQL 資料倉儲中指派變數</span><span class="sxs-lookup"><span data-stu-id="d0f8b-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="d0f8b-104">SQL 資料倉儲中的變數會設定使用 hello`DECLARE`陳述式或 hello`SET`陳述式。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="d0f8b-105">所有 hello 下列都是正常的方式 tooset 變數的值：</span><span class="sxs-lookup"><span data-stu-id="d0f8b-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="d0f8b-106">使用 DECLARE 設定宣告</span><span class="sxs-lookup"><span data-stu-id="d0f8b-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="d0f8b-107">初始化與宣告的變數是其中一個最有彈性的方式 tooset hello SQL 資料倉儲中的變數值。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="d0f8b-108">您也可以使用 DECLARE tooset 多個變數一次。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="d0f8b-109">您無法使用`SELECT`或`UPDATE`toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="d0f8b-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="d0f8b-110">您無法初始化，並使用 hello 中的變數相同的 DECLARE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="d0f8b-111">tooillustrate hello 點 hello 下列範例是**不**允許做為@p1已初始化並 hello 中使用相同的 DECLARE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="d0f8b-112">這會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="d0f8b-113">使用 SET 設定值</span><span class="sxs-lookup"><span data-stu-id="d0f8b-113">Setting values with SET</span></span>
<span data-ttu-id="d0f8b-114">SET 是設定單一變數時很常見的方法。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="d0f8b-115">以下的 hello 範例均使用設定來設定變數的有效方法：</span><span class="sxs-lookup"><span data-stu-id="d0f8b-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="d0f8b-116">您一次只能使用 SET 設定一個變數。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="d0f8b-117">不過，如上所示，可允許複合運算子。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="d0f8b-118">限制</span><span class="sxs-lookup"><span data-stu-id="d0f8b-118">Limitations</span></span>
<span data-ttu-id="d0f8b-119">您無法使用 SELECT 或 UPDATE 進行變數指派。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0f8b-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0f8b-120">Next steps</span></span>
<span data-ttu-id="d0f8b-121">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="d0f8b-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
