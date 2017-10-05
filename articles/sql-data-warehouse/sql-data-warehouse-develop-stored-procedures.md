---
title: "SQL 資料倉儲中的預存程序 | Microsoft Docs"
description: "在 Azure SQL 資料倉儲中實作預存程序以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: e42d80f0ca35f3fbb67389c66d072bc40d8a8d2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="8c77e-103">SQL 資料倉儲中的預存程序</span><span class="sxs-lookup"><span data-stu-id="8c77e-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="8c77e-104">SQL 資料倉儲支援許多 SQL Server 中具備的 TRANSACT-SQL 功能。</span><span class="sxs-lookup"><span data-stu-id="8c77e-104">SQL Data Warehouse supports many of the Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="8c77e-105">更重要的是，我們會想要運用相應放大特定功能，將解決方案的效能最大化。</span><span class="sxs-lookup"><span data-stu-id="8c77e-105">More importantly there are scale out specific features that we will want to leverage to maximize the performance of your solution.</span></span>

<span data-ttu-id="8c77e-106">不過，為了維護 SQL 資料倉儲的規模和效能，還有一些具有行為差異的功能以及其他不支援的功能。</span><span class="sxs-lookup"><span data-stu-id="8c77e-106">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="8c77e-107">本文說明如何實作 SQL 資料倉儲中的預存程序。</span><span class="sxs-lookup"><span data-stu-id="8c77e-107">This article explains how to implement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="8c77e-108">預存程序簡介</span><span class="sxs-lookup"><span data-stu-id="8c77e-108">Introducing stored procedures</span></span>
<span data-ttu-id="8c77e-109">預存程序很適合用來封裝您的 SQL 程式碼；將它儲存在資料倉儲中您的資料附近。</span><span class="sxs-lookup"><span data-stu-id="8c77e-109">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span></span> <span data-ttu-id="8c77e-110">藉由將程式碼封裝成可管理的單位，預存程序協助開發人員將其解決方案模組化；促使程式碼有更大的可重複使用性。</span><span class="sxs-lookup"><span data-stu-id="8c77e-110">By encapsulating the code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="8c77e-111">每個預存程序也可接受參數，使其更具彈性。</span><span class="sxs-lookup"><span data-stu-id="8c77e-111">Each stored procedure can also accept parameters to make them even more flexible.</span></span>

<span data-ttu-id="8c77e-112">SQL 資料倉儲提供簡化且更簡化的預存程序實作。</span><span class="sxs-lookup"><span data-stu-id="8c77e-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="8c77e-113">相較於 SQL Server，最大差異是預存程序不是預先編譯的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8c77e-113">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="8c77e-114">在資料倉儲中，我們通常比較不在乎編譯時間。</span><span class="sxs-lookup"><span data-stu-id="8c77e-114">In data warehouses we are generally less concerned with the compilation time.</span></span> <span data-ttu-id="8c77e-115">比較重要的是在對大型資料磁碟區操作時，正確地最佳化預存程序程式碼。</span><span class="sxs-lookup"><span data-stu-id="8c77e-115">It is more important that the stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="8c77e-116">目標是要節省時數、分鐘數和秒數，而不是毫秒數。</span><span class="sxs-lookup"><span data-stu-id="8c77e-116">The goal is to save hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="8c77e-117">因此，將預存程序視為 SQL 邏輯的容器更有幫助。</span><span class="sxs-lookup"><span data-stu-id="8c77e-117">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="8c77e-118">當 SQL 資料倉儲執行預存程序時，SQL 陳述式會在執行階段進行剖析、轉譯和最佳化。</span><span class="sxs-lookup"><span data-stu-id="8c77e-118">When SQL Data Warehouse executes your stored procedure the SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="8c77e-119">在此過程中，每個陳述式都會轉換為分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="8c77e-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="8c77e-120">實際針對資料執行的 SQL 程式碼與提交的查詢不同。</span><span class="sxs-lookup"><span data-stu-id="8c77e-120">The SQL code that is actually executed against the data is different to the query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="8c77e-121">巢狀預存程序</span><span class="sxs-lookup"><span data-stu-id="8c77e-121">Nesting stored procedures</span></span>
<span data-ttu-id="8c77e-122">當預存程序呼叫其他預存程序或執行動態 sql 時，內部預存程序或程式碼叫用據稱就是巢狀。</span><span class="sxs-lookup"><span data-stu-id="8c77e-122">When stored procedures call other stored procedures or execute dynamic sql then the inner stored procedure or code invocation is said to be nested.</span></span>

<span data-ttu-id="8c77e-123">SQL 資料倉儲最多支援 8 個巢狀層級。</span><span class="sxs-lookup"><span data-stu-id="8c77e-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="8c77e-124">這與 SQL Server 稍有不同。</span><span class="sxs-lookup"><span data-stu-id="8c77e-124">This is slightly different to SQL Server.</span></span> <span data-ttu-id="8c77e-125">SQL Server 中的巢狀層級為 32。</span><span class="sxs-lookup"><span data-stu-id="8c77e-125">The nest level in SQL Server is 32.</span></span>

<span data-ttu-id="8c77e-126">最上層預存程序呼叫等同於巢狀層級 1</span><span class="sxs-lookup"><span data-stu-id="8c77e-126">The top level stored procedure call equates to nest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="8c77e-127">如果預存程序也會進行另一個 EXEC 呼叫，則這會將巢狀層級提高到 2</span><span class="sxs-lookup"><span data-stu-id="8c77e-127">If the stored procedure also makes another EXEC call then this will increase the nest level to 2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="8c77e-128">如果第二個程序接著會執行一些動態 SQL，則這會將巢狀層級提高到 3</span><span class="sxs-lookup"><span data-stu-id="8c77e-128">If the second procedure then executes some dynamic sql then this will increase the nest level to 3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="8c77e-129">請注意，SQL 資料倉儲目前不支援 @@NESTLEVEL。</span><span class="sxs-lookup"><span data-stu-id="8c77e-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="8c77e-130">您必須自行追蹤您的巢狀層級。</span><span class="sxs-lookup"><span data-stu-id="8c77e-130">You will need to keep a track of your nest level yourself.</span></span> <span data-ttu-id="8c77e-131">您不太可能會達到 8 個巢狀層級的限制，但如果達到，您必須重新處理您的程式碼並將其「壓平合併」，使其符合這項限制。</span><span class="sxs-lookup"><span data-stu-id="8c77e-131">It is unlikely you will hit the 8 nest level limit but if you do you will need to re-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="8c77e-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="8c77e-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="8c77e-133">SQL 資料倉儲不允許您透過 INSERT 陳述式取用預存程序的結果集。</span><span class="sxs-lookup"><span data-stu-id="8c77e-133">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="8c77e-134">不過，您可以使用另一個方法。</span><span class="sxs-lookup"><span data-stu-id="8c77e-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="8c77e-135">如需如何這麼做的範例，請參閱有關 [暫存資料表] 的文章。</span><span class="sxs-lookup"><span data-stu-id="8c77e-135">Please refer to the following article on [temporary tables] for an example on how to do this.</span></span>

## <a name="limitations"></a><span data-ttu-id="8c77e-136">限制</span><span class="sxs-lookup"><span data-stu-id="8c77e-136">Limitations</span></span>
<span data-ttu-id="8c77e-137">在 SQL 資料倉儲中不會實作 TRANSACT-SQL 預存程序的有些層面。</span><span class="sxs-lookup"><span data-stu-id="8c77e-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="8c77e-138">如下：</span><span class="sxs-lookup"><span data-stu-id="8c77e-138">They are:</span></span>

* <span data-ttu-id="8c77e-139">暫存預存程序</span><span class="sxs-lookup"><span data-stu-id="8c77e-139">temporary stored procedures</span></span>
* <span data-ttu-id="8c77e-140">編號預存程序</span><span class="sxs-lookup"><span data-stu-id="8c77e-140">numbered stored procedures</span></span>
* <span data-ttu-id="8c77e-141">擴充預存程序</span><span class="sxs-lookup"><span data-stu-id="8c77e-141">extended stored procedures</span></span>
* <span data-ttu-id="8c77e-142">CLR 預存程序</span><span class="sxs-lookup"><span data-stu-id="8c77e-142">CLR stored procedures</span></span>
* <span data-ttu-id="8c77e-143">加密選項</span><span class="sxs-lookup"><span data-stu-id="8c77e-143">encryption option</span></span>
* <span data-ttu-id="8c77e-144">複寫選項</span><span class="sxs-lookup"><span data-stu-id="8c77e-144">replication option</span></span>
* <span data-ttu-id="8c77e-145">資料表值參數</span><span class="sxs-lookup"><span data-stu-id="8c77e-145">table-valued parameters</span></span>
* <span data-ttu-id="8c77e-146">唯讀參數</span><span class="sxs-lookup"><span data-stu-id="8c77e-146">read-only parameters</span></span>
* <span data-ttu-id="8c77e-147">預設參數</span><span class="sxs-lookup"><span data-stu-id="8c77e-147">default parameters</span></span>
* <span data-ttu-id="8c77e-148">執行內容</span><span class="sxs-lookup"><span data-stu-id="8c77e-148">execution contexts</span></span>
* <span data-ttu-id="8c77e-149">return 陳述式</span><span class="sxs-lookup"><span data-stu-id="8c77e-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c77e-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c77e-150">Next steps</span></span>
<span data-ttu-id="8c77e-151">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="8c77e-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
<span data-ttu-id="8c77e-152">[暫存資料表]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span><span class="sxs-lookup"><span data-stu-id="8c77e-152">[temporary tables]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span></span>
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
