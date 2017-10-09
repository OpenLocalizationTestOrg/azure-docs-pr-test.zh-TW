---
title: "aaaIn 記憶體內部 OLTP 改善 SQL txn 效能 |Microsoft 文件"
description: "採用記憶體內部 OLTP tooimprove 交易式的效能在現有的 SQL 資料庫。"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="be620-103">使用記憶體中 OLTP tooimprove SQL Database 中的應用程式效能</span><span class="sxs-lookup"><span data-stu-id="be620-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="be620-104">[記憶體內部 OLTP](sql-database-in-memory.md)可以是交易處理、 資料擷取和暫時性資料案例中，使用的 tooimprove hello 效能[Premium](sql-database-service-tiers.md) Azure SQL Database，而不會增加 hello 定價層。</span><span class="sxs-lookup"><span data-stu-id="be620-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="be620-105">[了解仲裁如何透過 SQL Database 讓重要資料庫的工作負載加倍，同時降低 70% 的 DTU](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="be620-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="be620-106">請遵循這些步驟 tooadopt 記憶體中 OLTP 中現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="be620-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="be620-107">步驟 1︰請確定您使用高階資料庫</span><span class="sxs-lookup"><span data-stu-id="be620-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="be620-108">只有高階資料庫支援記憶體內部 OLTP。</span><span class="sxs-lookup"><span data-stu-id="be620-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="be620-109">如果 hello 傳回結果為 1，則支援記憶體中 (不是 0):</span><span class="sxs-lookup"><span data-stu-id="be620-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="be620-110">*XTP* 代表*極端交易處理 (Extreme Transaction Processing)*</span><span class="sxs-lookup"><span data-stu-id="be620-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="be620-111">步驟 2： 識別物件 toomigrate tooIn In-memory OLTP</span><span class="sxs-lookup"><span data-stu-id="be620-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="be620-112">SSMS 包含您可以對具有作用中工作負載的資料庫執行的 [交易效能分析概觀]  報告。</span><span class="sxs-lookup"><span data-stu-id="be620-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="be620-113">hello 報表會識別資料表和預存程序的移轉候選 tooIn 記憶體內部 OLTP。</span><span class="sxs-lookup"><span data-stu-id="be620-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="be620-114">在 SSMS 中，toogenerate hello 報表：</span><span class="sxs-lookup"><span data-stu-id="be620-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="be620-115">在 [hello**物件總管] 中**，以滑鼠右鍵按一下資料庫節點。</span><span class="sxs-lookup"><span data-stu-id="be620-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="be620-116">按一下 [報表] > [標準報表] > [交易效能分析概觀]。</span><span class="sxs-lookup"><span data-stu-id="be620-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="be620-117">如需詳細資訊，請參閱[判斷是否將資料表或預存程序應該匯出 tooIn 記憶體內部 OLTP](http://msdn.microsoft.com/library/dn205133.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be620-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="be620-118">步驟 3：建立可比較的測試資料庫</span><span class="sxs-lookup"><span data-stu-id="be620-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="be620-119">假設 hello 報表會指出您的資料庫資料表可從正在獲益的已轉換 tooa 記憶體最佳化資料表。</span><span class="sxs-lookup"><span data-stu-id="be620-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="be620-120">我們建議您先測試所測試 tooconfirm hello 指示。</span><span class="sxs-lookup"><span data-stu-id="be620-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="be620-121">您需要實際執行資料庫的測試複本。</span><span class="sxs-lookup"><span data-stu-id="be620-121">You need a test copy of your production database.</span></span> <span data-ttu-id="be620-122">hello 測試資料庫都應該在 hello 相同服務與您的生產資料庫層級。</span><span class="sxs-lookup"><span data-stu-id="be620-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="be620-123">tooease 測試時，會調整您的測試資料庫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="be620-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="be620-124">使用 SSMS 連接 toohello 測試資料庫。</span><span class="sxs-lookup"><span data-stu-id="be620-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="be620-125">tooavoid 需要 hello WITH (SNAPSHOT) 選項，在查詢中的，將 hello 資料庫選項的設定，如 hello 下列 T-SQL 陳述式中所示：</span><span class="sxs-lookup"><span data-stu-id="be620-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="be620-126">步驟 4：移轉資料表</span><span class="sxs-lookup"><span data-stu-id="be620-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="be620-127">您必須建立和擴展記憶體最佳化的複製要 tootest 的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="be620-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="be620-128">您可以使用下列其中一種方式加以建立：</span><span class="sxs-lookup"><span data-stu-id="be620-128">You can create it by using either:</span></span>

* <span data-ttu-id="be620-129">hello 方便在 SSMS 中的記憶體最佳化精靈 」。</span><span class="sxs-lookup"><span data-stu-id="be620-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="be620-130">手動 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="be620-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="be620-131">SSMS 中的記憶體最佳化精靈</span><span class="sxs-lookup"><span data-stu-id="be620-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="be620-132">toouse 此移轉選項：</span><span class="sxs-lookup"><span data-stu-id="be620-132">toouse this migration option:</span></span>

1. <span data-ttu-id="be620-133">使用 SSMS 連接 toohello 測試資料庫。</span><span class="sxs-lookup"><span data-stu-id="be620-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="be620-134">在 [hello**物件總管] 中**hello 資料表上按一下滑鼠右鍵，然後按**Memory Optimization Advisor**。</span><span class="sxs-lookup"><span data-stu-id="be620-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="be620-135">hello**資料表記憶體最佳化 Advisor**精靈隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="be620-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="be620-136">在 hello 精靈中，按一下 **移轉驗證**(或 hello**下一步**按鈕) toosee 如果 hello 資料表有任何不支援的記憶體最佳化資料表中不支援的功能。</span><span class="sxs-lookup"><span data-stu-id="be620-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="be620-137">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="be620-137">For more information, see:</span></span>
   
   * <span data-ttu-id="be620-138">hello*記憶體最佳化檢查清單*中[Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be620-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="be620-139">[In-Memory OLTP 不支援的 Transact-SQL 建構](http://msdn.microsoft.com/library/dn246937.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be620-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="be620-140">[移轉 tooIn 記憶體內部 OLTP](http://msdn.microsoft.com/library/dn247639.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be620-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="be620-141">如果 hello 資料表有不支援的功能，hello advisor 可以為您執行 hello 實際結構描述和資料移轉。</span><span class="sxs-lookup"><span data-stu-id="be620-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="be620-142">手動 T-SQL</span><span class="sxs-lookup"><span data-stu-id="be620-142">Manual T-SQL</span></span>
<span data-ttu-id="be620-143">toouse 此移轉選項：</span><span class="sxs-lookup"><span data-stu-id="be620-143">toouse this migration option:</span></span>

1. <span data-ttu-id="be620-144">使用 SSMS （或類似的公用程式），以連接 tooyour 測試資料庫。</span><span class="sxs-lookup"><span data-stu-id="be620-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="be620-145">取得 hello 完成 T-SQL 指令碼供您的資料表和其索引。</span><span class="sxs-lookup"><span data-stu-id="be620-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="be620-146">在 SSMS 中，以滑鼠右鍵按一下資料表節點。</span><span class="sxs-lookup"><span data-stu-id="be620-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="be620-147">按一下 [產生資料表的指令碼為] > [建立] > [新增查詢視窗]。</span><span class="sxs-lookup"><span data-stu-id="be620-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="be620-148">在 hello 指令碼視窗中，加入 WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="be620-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="be620-149">如果沒有叢集索引，請將它變更 tooNONCLUSTERED。</span><span class="sxs-lookup"><span data-stu-id="be620-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="be620-150">使用 SP_RENAME 來重新命名 hello 現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="be620-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="be620-151">執行已編輯的 CREATE TABLE 指令碼，以建立 hello 新記憶體最佳化資料表的副本 hello。</span><span class="sxs-lookup"><span data-stu-id="be620-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="be620-152">複製 hello tooyour 記憶體最佳化資料表使用 INSERT...選取 * 成：</span><span class="sxs-lookup"><span data-stu-id="be620-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="be620-153">步驟 5 (選擇性)：移轉預存程序</span><span class="sxs-lookup"><span data-stu-id="be620-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="be620-154">hello 記憶體中的功能也可以修改預存程序來改善效能。</span><span class="sxs-lookup"><span data-stu-id="be620-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="be620-155">原生編譯預存程序的考量</span><span class="sxs-lookup"><span data-stu-id="be620-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="be620-156">原生編譯的預存程序必須有下列選項，在其 T-SQL WITH 子句的 hello:</span><span class="sxs-lookup"><span data-stu-id="be620-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="be620-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="be620-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="be620-158">SCHEMABINDING: hello 預存程序的意義資料表不可具有其資料行的定義會影響 hello 預存程序中，任何方式變更，除非您卸除 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="be620-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="be620-159">原生模組必須使用一個大型 [ATOMIC 區塊](http://msdn.microsoft.com/library/dn452281.aspx) 進行交易管理。</span><span class="sxs-lookup"><span data-stu-id="be620-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="be620-160">沒有明確 BEGIN TRANSACTION 或 ROLLBACK TRANSACTION 的角色。</span><span class="sxs-lookup"><span data-stu-id="be620-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="be620-161">如果您的程式碼偵測到商務規則的違規情形，它可能會終止 hello 與不可部分完成的區塊[擲回](http://msdn.microsoft.com/library/ee677615.aspx)陳述式。</span><span class="sxs-lookup"><span data-stu-id="be620-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="be620-162">原生編譯的一般 CREATE PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="be620-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="be620-163">通常 hello T-SQL toocreate 原生編譯的預存程序是類似 toohello 下列範本：</span><span class="sxs-lookup"><span data-stu-id="be620-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="be620-164">Hello TRANSACTION_ISOLATION_LEVEL，快照集是 hello 最常見的值為 hello 原生編譯的預存程序。</span><span class="sxs-lookup"><span data-stu-id="be620-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="be620-165">不過，子集 hello 其他也支援值：</span><span class="sxs-lookup"><span data-stu-id="be620-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="be620-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="be620-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="be620-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="be620-167">SERIALIZABLE</span></span>
* <span data-ttu-id="be620-168">hello 語言值必須存在於 hello sys.languages 檢視。</span><span class="sxs-lookup"><span data-stu-id="be620-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="be620-169">如何 toomigrate 預存程序</span><span class="sxs-lookup"><span data-stu-id="be620-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="be620-170">hello 移轉步驟如下：</span><span class="sxs-lookup"><span data-stu-id="be620-170">hello migration steps are:</span></span>

1. <span data-ttu-id="be620-171">取得 hello CREATE PROCEDURE 指令碼 toohello 一般解譯預存程序。</span><span class="sxs-lookup"><span data-stu-id="be620-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="be620-172">請重寫其標頭 toomatch hello 先前的範本。</span><span class="sxs-lookup"><span data-stu-id="be620-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="be620-173">確定 hello 預存程序 T-SQL 程式碼是否使用任何原生編譯的預存程序不支援的功能。</span><span class="sxs-lookup"><span data-stu-id="be620-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="be620-174">視需要實作因應措施。</span><span class="sxs-lookup"><span data-stu-id="be620-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="be620-175">如需詳細資訊，請參閱 [原生編譯預存程序的移轉問題](http://msdn.microsoft.com/library/dn296678.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be620-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="be620-176">使用 SP_RENAME 來重新命名 hello 舊的預存程序。</span><span class="sxs-lookup"><span data-stu-id="be620-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="be620-177">或直接加以捨棄。</span><span class="sxs-lookup"><span data-stu-id="be620-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="be620-178">執行已編輯的 CREATE PROCEDURE T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="be620-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="be620-179">步驟 6：在測試環境中執行您的工作負載</span><span class="sxs-lookup"><span data-stu-id="be620-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="be620-180">您會在您的生產資料庫中執行類似 toohello 工作負載的測試資料庫中執行工作負載。</span><span class="sxs-lookup"><span data-stu-id="be620-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="be620-181">這應該會顯示 hello hello 記憶體中功能的使用資料表和預存程序來達成的效能改善。</span><span class="sxs-lookup"><span data-stu-id="be620-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="be620-182">Hello 工作負載的主要屬性如下：</span><span class="sxs-lookup"><span data-stu-id="be620-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="be620-183">並行連線數目。</span><span class="sxs-lookup"><span data-stu-id="be620-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="be620-184">讀取/寫入比率。</span><span class="sxs-lookup"><span data-stu-id="be620-184">Read/write ratio.</span></span>

<span data-ttu-id="be620-185">tootailor 和執行的 hello 測試工作負載，請考慮使用 hello 方便 ostress.exe 工具中所述[這裡](sql-database-in-memory.md)。</span><span class="sxs-lookup"><span data-stu-id="be620-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="be620-186">toominimize 網路延遲，hello 中執行測試 hello 資料庫所在的相同 Azure 的地理區域。</span><span class="sxs-lookup"><span data-stu-id="be620-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="be620-187">步驟 7：實作後的監視</span><span class="sxs-lookup"><span data-stu-id="be620-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="be620-188">監視您在生產環境中的記憶體中實作 hello 效能影響，請考慮：</span><span class="sxs-lookup"><span data-stu-id="be620-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="be620-189">[監視記憶體內部儲存體](sql-database-in-memory-oltp-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="be620-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="be620-190">使用動態管理檢視監視 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="be620-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="be620-191">相關連結</span><span class="sxs-lookup"><span data-stu-id="be620-191">Related links</span></span>
* [<span data-ttu-id="be620-192">記憶體內部 OLTP (記憶體內部最佳化)</span><span class="sxs-lookup"><span data-stu-id="be620-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="be620-193">簡介 tooNatively 編譯的預存程序</span><span class="sxs-lookup"><span data-stu-id="be620-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="be620-194">記憶體最佳化建議程式</span><span class="sxs-lookup"><span data-stu-id="be620-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

