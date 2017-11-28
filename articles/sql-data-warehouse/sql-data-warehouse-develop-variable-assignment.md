---
title: "在 SQL 資料倉儲中指派變數 |Microsoft Docs"
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
ms.openlocfilehash: 045d5148cd3f12dac63c961ccf7c953d355ed725
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="81259-103">在 SQL 資料倉儲中指派變數</span><span class="sxs-lookup"><span data-stu-id="81259-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="81259-104">SQL 資料倉儲中的變數是使用 `DECLARE` 陳述式或 `SET` 陳述式進行設定的。</span><span class="sxs-lookup"><span data-stu-id="81259-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span></span>

<span data-ttu-id="81259-105">下列各項是設定變數值的完全有效方式：</span><span class="sxs-lookup"><span data-stu-id="81259-105">All of the following are perfectly valid ways to set a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="81259-106">使用 DECLARE 設定宣告</span><span class="sxs-lookup"><span data-stu-id="81259-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="81259-107">使用 DECLARE 初始化變數是在 SQL 資料倉儲中設定變數值的其中一種最具彈性的方式。</span><span class="sxs-lookup"><span data-stu-id="81259-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="81259-108">您也可以使用 DECLARE，一次設定一個以上的變數。</span><span class="sxs-lookup"><span data-stu-id="81259-108">You can also use DECLARE to set more than one variable at a time.</span></span> <span data-ttu-id="81259-109">您可以使用 `SELECT` 或 `UPDATE` 來執行此作業：</span><span class="sxs-lookup"><span data-stu-id="81259-109">You cannot use `SELECT` or `UPDATE` to do this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="81259-110">您無法在相同的 DECLARE 陳述式中初始化並使用變數。</span><span class="sxs-lookup"><span data-stu-id="81259-110">You cannot initialise and use a variable in the same DECLARE statement.</span></span> <span data-ttu-id="81259-111">為了說明這點，**不**允許以下範例，因為 @p1 已在相同的 DECLARE 陳述式中初始化和使用。</span><span class="sxs-lookup"><span data-stu-id="81259-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span></span> <span data-ttu-id="81259-112">這會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="81259-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="81259-113">使用 SET 設定值</span><span class="sxs-lookup"><span data-stu-id="81259-113">Setting values with SET</span></span>
<span data-ttu-id="81259-114">SET 是設定單一變數時很常見的方法。</span><span class="sxs-lookup"><span data-stu-id="81259-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="81259-115">下列所有範例都是使用 SET 設定變數的有效方式：</span><span class="sxs-lookup"><span data-stu-id="81259-115">All of the examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="81259-116">您一次只能使用 SET 設定一個變數。</span><span class="sxs-lookup"><span data-stu-id="81259-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="81259-117">不過，如上所示，可允許複合運算子。</span><span class="sxs-lookup"><span data-stu-id="81259-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="81259-118">限制</span><span class="sxs-lookup"><span data-stu-id="81259-118">Limitations</span></span>
<span data-ttu-id="81259-119">您無法使用 SELECT 或 UPDATE 進行變數指派。</span><span class="sxs-lookup"><span data-stu-id="81259-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81259-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81259-120">Next steps</span></span>
<span data-ttu-id="81259-121">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="81259-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
