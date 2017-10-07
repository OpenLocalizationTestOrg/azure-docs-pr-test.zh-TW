---
title: "SQL 資料倉儲中的 aaaStored 程序 |Microsoft 文件"
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
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="c2bd4-103">SQL 資料倉儲中的預存程序</span><span class="sxs-lookup"><span data-stu-id="c2bd4-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="c2bd4-104">SQL 資料倉儲可支援許多 SQL Server 中的 hello TRANSACT-SQL 功能。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="c2bd4-105">更重要的是有向外延展，我們將需要您的方案 tooleverage toomaximize hello 效能的特定功能。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="c2bd4-106">不過，toomaintain hello 規模和 SQL 資料倉儲的效能有還有一些功能和已有些許差異，以及其他不支援的功能。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="c2bd4-107">本文說明 tooimplement 儲存 SQL 資料倉儲內的程序的方式。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="c2bd4-108">預存程序簡介</span><span class="sxs-lookup"><span data-stu-id="c2bd4-108">Introducing stored procedures</span></span>
<span data-ttu-id="c2bd4-109">預存程序很適合用來封裝您的 SQL 程式碼;它關閉 tooyour 將資料儲存在 hello 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="c2bd4-110">藉由 hello 程式碼封裝成可管理單位預存程序協助開發人員模塊化其方案中。促進大於 re-usability 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="c2bd4-111">每個預存程序也可以接受參數 toomake 它們更有彈性。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="c2bd4-112">SQL 資料倉儲提供簡化且更簡化的預存程序實作。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="c2bd4-113">hello 最大差異比較的 tooSQL 伺服器 hello 預存程序，不是先行編譯的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="c2bd4-114">在資料倉儲我們關心通常較不 hello 編譯時間。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="c2bd4-115">來得更重要的是針對大型資料磁碟區時，正確 optimised hello 預存程序程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="c2bd4-116">hello 目標是 toosave 小時、 分鐘和秒鐘不毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="c2bd4-117">因此，是預存程序的更有幫助 toothink 做為 SQL 邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="c2bd4-118">當 SQL 資料倉儲執行預存程序 hello SQL 陳述式會剖析、 轉譯和最佳化在執行階段。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="c2bd4-119">在此過程中，每個陳述式都會轉換為分散式查詢。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="c2bd4-120">提交的不同 toohello 查詢 hello hello 資料對實際執行的 SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="c2bd4-121">巢狀預存程序</span><span class="sxs-lookup"><span data-stu-id="c2bd4-121">Nesting stored procedures</span></span>
<span data-ttu-id="c2bd4-122">當預存程序呼叫其他預存程序，或執行動態 sql，則 hello 內部預存程序或程式碼引動過程即稱為 toobe 巢狀。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="c2bd4-123">SQL 資料倉儲最多支援 8 個巢狀層級。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="c2bd4-124">這是稍有不同 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="c2bd4-125">SQL Server 中的 hello 巢狀層級為 32。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="c2bd4-126">hello 上方層級的預存程序呼叫等同 toonest 層級 1</span><span class="sxs-lookup"><span data-stu-id="c2bd4-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="c2bd4-127">如果 hello 預存程序也可以呼叫另一個 EXEC，則這會增加 hello 巢狀層級 too2</span><span class="sxs-lookup"><span data-stu-id="c2bd4-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="c2bd4-128">如果 hello 第二個程序，然後執行一些動態 sql 然後這樣會增加 hello 巢狀層級 too3</span><span class="sxs-lookup"><span data-stu-id="c2bd4-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="c2bd4-129">請注意，SQL 資料倉儲目前不支援 @@NESTLEVEL。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="c2bd4-130">您將自己需要 tookeep 您巢狀層級的追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="c2bd4-131">不太會叫用 hello 8 巢狀層級的限制，但如果您執行您將需要 toore 工作程式碼和 「 簡化 」 它，使其符合此限制內。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="c2bd4-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="c2bd4-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="c2bd4-133">SQL 資料倉儲不允許您 tooconsume hello 結果集的 INSERT 陳述式的預存程序。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="c2bd4-134">不過，您可以使用另一個方法。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="c2bd4-135">請參閱下列文章 toohello[暫存資料表]如何例如 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="c2bd4-136">限制</span><span class="sxs-lookup"><span data-stu-id="c2bd4-136">Limitations</span></span>
<span data-ttu-id="c2bd4-137">在 SQL 資料倉儲中不會實作 TRANSACT-SQL 預存程序的有些層面。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="c2bd4-138">如下：</span><span class="sxs-lookup"><span data-stu-id="c2bd4-138">They are:</span></span>

* <span data-ttu-id="c2bd4-139">暫存預存程序</span><span class="sxs-lookup"><span data-stu-id="c2bd4-139">temporary stored procedures</span></span>
* <span data-ttu-id="c2bd4-140">編號預存程序</span><span class="sxs-lookup"><span data-stu-id="c2bd4-140">numbered stored procedures</span></span>
* <span data-ttu-id="c2bd4-141">擴充預存程序</span><span class="sxs-lookup"><span data-stu-id="c2bd4-141">extended stored procedures</span></span>
* <span data-ttu-id="c2bd4-142">CLR 預存程序</span><span class="sxs-lookup"><span data-stu-id="c2bd4-142">CLR stored procedures</span></span>
* <span data-ttu-id="c2bd4-143">加密選項</span><span class="sxs-lookup"><span data-stu-id="c2bd4-143">encryption option</span></span>
* <span data-ttu-id="c2bd4-144">複寫選項</span><span class="sxs-lookup"><span data-stu-id="c2bd4-144">replication option</span></span>
* <span data-ttu-id="c2bd4-145">資料表值參數</span><span class="sxs-lookup"><span data-stu-id="c2bd4-145">table-valued parameters</span></span>
* <span data-ttu-id="c2bd4-146">唯讀參數</span><span class="sxs-lookup"><span data-stu-id="c2bd4-146">read-only parameters</span></span>
* <span data-ttu-id="c2bd4-147">預設參數</span><span class="sxs-lookup"><span data-stu-id="c2bd4-147">default parameters</span></span>
* <span data-ttu-id="c2bd4-148">執行內容</span><span class="sxs-lookup"><span data-stu-id="c2bd4-148">execution contexts</span></span>
* <span data-ttu-id="c2bd4-149">return 陳述式</span><span class="sxs-lookup"><span data-stu-id="c2bd4-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2bd4-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2bd4-150">Next steps</span></span>
<span data-ttu-id="c2bd4-151">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="c2bd4-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[暫存資料表]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
