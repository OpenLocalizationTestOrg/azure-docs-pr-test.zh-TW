---
title: "In-Memory OLTP 可改善 SQL 交易效能 | Microsoft Docs"
description: "採用記憶體內部 OLTP 來改善現有 SQL Database 的交易效能。"
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
ms.openlocfilehash: 50eed9aed417778bd497f55e20c8e732fdae9cf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a><span data-ttu-id="0775b-103">使用記憶體內部 OLTP 改善 SQL Database 中的應用程式效能</span><span class="sxs-lookup"><span data-stu-id="0775b-103">Use In-Memory OLTP to improve your application performance in SQL Database</span></span>
<span data-ttu-id="0775b-104">[記憶體內部 OLTP](sql-database-in-memory.md) 可用來改善交易處理、資料擷取和暫時性資料的效能，在[高階](sql-database-service-tiers.md) Azure SQL Database 而無須增加定價層。</span><span class="sxs-lookup"><span data-stu-id="0775b-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="0775b-105">[了解仲裁如何透過 SQL Database 讓重要資料庫的工作負載加倍，同時降低 70% 的 DTU](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="0775b-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="0775b-106">請依照下列步驟，在您現有的資料庫中採用 In-Memory OLTP。</span><span class="sxs-lookup"><span data-stu-id="0775b-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="0775b-107">步驟 1︰請確定您使用高階資料庫</span><span class="sxs-lookup"><span data-stu-id="0775b-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="0775b-108">只有高階資料庫支援記憶體內部 OLTP。</span><span class="sxs-lookup"><span data-stu-id="0775b-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="0775b-109">如果傳回的結果為 1 (不是 0)，則支援 In-Memory：</span><span class="sxs-lookup"><span data-stu-id="0775b-109">In-Memory is supported if the returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="0775b-110">*XTP* 代表*極端交易處理 (Extreme Transaction Processing)*</span><span class="sxs-lookup"><span data-stu-id="0775b-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a><span data-ttu-id="0775b-111">步驟 2：識別要移轉至 In-Memory OLTP 的物件</span><span class="sxs-lookup"><span data-stu-id="0775b-111">Step 2: Identify objects to migrate to In-Memory OLTP</span></span>
<span data-ttu-id="0775b-112">SSMS 包含您可以對具有作用中工作負載的資料庫執行的 [交易效能分析概觀]  報告。</span><span class="sxs-lookup"><span data-stu-id="0775b-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="0775b-113">此報告會識別要移轉至 In-Memory OLTP 的候選資料表和預存程序。</span><span class="sxs-lookup"><span data-stu-id="0775b-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span></span>

<span data-ttu-id="0775b-114">在 SSMS 中，若要產生報告︰</span><span class="sxs-lookup"><span data-stu-id="0775b-114">In SSMS, to generate the report:</span></span>

* <span data-ttu-id="0775b-115">在 [物件總管] 中，以滑鼠右鍵按一下您的資料庫節點。</span><span class="sxs-lookup"><span data-stu-id="0775b-115">In the **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="0775b-116">按一下 [報表] > [標準報表] > [交易效能分析概觀]。</span><span class="sxs-lookup"><span data-stu-id="0775b-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="0775b-117">如需詳細資訊，請參閱 [判斷資料表或預存程序是否應該移植到 In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0775b-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="0775b-118">步驟 3：建立可比較的測試資料庫</span><span class="sxs-lookup"><span data-stu-id="0775b-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="0775b-119">假設報告指出您的資料庫的某個資料表若轉換成記憶體最佳化的資料表將會有好處。</span><span class="sxs-lookup"><span data-stu-id="0775b-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span></span> <span data-ttu-id="0775b-120">我們建議您先測試以確認這項指示。</span><span class="sxs-lookup"><span data-stu-id="0775b-120">We recommend that you first test to confirm the indication by testing.</span></span>

<span data-ttu-id="0775b-121">您需要實際執行資料庫的測試複本。</span><span class="sxs-lookup"><span data-stu-id="0775b-121">You need a test copy of your production database.</span></span> <span data-ttu-id="0775b-122">測試資料庫需位於與實際執行資料庫相同的服務層級。</span><span class="sxs-lookup"><span data-stu-id="0775b-122">The test database should be at the same service tier level as your production database.</span></span>

<span data-ttu-id="0775b-123">為了簡化測試，請依照下列方式調整測試資料庫：</span><span class="sxs-lookup"><span data-stu-id="0775b-123">To ease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="0775b-124">使用 SSMS 連接到測試資料庫。</span><span class="sxs-lookup"><span data-stu-id="0775b-124">Connect to the test database by using SSMS.</span></span>
2. <span data-ttu-id="0775b-125">若要避免在查詢中用到 WITH (SNAPSHOT) 選項，請依照下列 T-SQL 陳述式中所示設定資料庫選項：</span><span class="sxs-lookup"><span data-stu-id="0775b-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="0775b-126">步驟 4：移轉資料表</span><span class="sxs-lookup"><span data-stu-id="0775b-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="0775b-127">您必須建立並填入您想要測試之資料表的記憶體最佳化複本。</span><span class="sxs-lookup"><span data-stu-id="0775b-127">You must create and populate a memory-optimized copy of the table you want to test.</span></span> <span data-ttu-id="0775b-128">您可以使用下列其中一種方式加以建立：</span><span class="sxs-lookup"><span data-stu-id="0775b-128">You can create it by using either:</span></span>

* <span data-ttu-id="0775b-129">SSMS 中好用的記憶體最佳化精靈。</span><span class="sxs-lookup"><span data-stu-id="0775b-129">The handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="0775b-130">手動 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="0775b-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="0775b-131">SSMS 中的記憶體最佳化精靈</span><span class="sxs-lookup"><span data-stu-id="0775b-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="0775b-132">若要使用此移轉選項：</span><span class="sxs-lookup"><span data-stu-id="0775b-132">To use this migration option:</span></span>

1. <span data-ttu-id="0775b-133">使用 SSMS 連接到測試資料庫。</span><span class="sxs-lookup"><span data-stu-id="0775b-133">Connect to the test database with SSMS.</span></span>
2. <span data-ttu-id="0775b-134">在 [物件總管] 中，以滑鼠右鍵按一下資料表，然後按一下 [記憶體最佳化建議程式]。</span><span class="sxs-lookup"><span data-stu-id="0775b-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="0775b-135">[資料表記憶體最佳化建議程式]  精靈隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="0775b-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="0775b-136">在此精靈中按一下 [移轉驗證] \(或 [下一步] 按鈕)，以查看資料表是否有任何在記憶體最佳化資料表中不受支援的功能。</span><span class="sxs-lookup"><span data-stu-id="0775b-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="0775b-137">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="0775b-137">For more information, see:</span></span>
   
   * <span data-ttu-id="0775b-138">*記憶體最佳化建議程式* 中的 [記憶體最佳化檢查清單](http://msdn.microsoft.com/library/dn284308.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0775b-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="0775b-139">[In-Memory OLTP 不支援的 Transact-SQL 建構](http://msdn.microsoft.com/library/dn246937.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0775b-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="0775b-140">[移轉至 In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0775b-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="0775b-141">如果資料表沒有不受支援的功能，建議程式可以為您執行實際的結構描述和資料移轉。</span><span class="sxs-lookup"><span data-stu-id="0775b-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="0775b-142">手動 T-SQL</span><span class="sxs-lookup"><span data-stu-id="0775b-142">Manual T-SQL</span></span>
<span data-ttu-id="0775b-143">若要使用此移轉選項：</span><span class="sxs-lookup"><span data-stu-id="0775b-143">To use this migration option:</span></span>

1. <span data-ttu-id="0775b-144">使用 SSMS (或類似的公用程式) 連接到您的測試資料庫。</span><span class="sxs-lookup"><span data-stu-id="0775b-144">Connect to your test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="0775b-145">為您的資料表及其索引取得完整 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0775b-145">Obtain the complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="0775b-146">在 SSMS 中，以滑鼠右鍵按一下資料表節點。</span><span class="sxs-lookup"><span data-stu-id="0775b-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="0775b-147">按一下 [產生資料表的指令碼為] > [建立] > [新增查詢視窗]。</span><span class="sxs-lookup"><span data-stu-id="0775b-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="0775b-148">在指令碼視窗中，將 WITH (MEMORY_OPTIMIZED = ON) 新增至 CREATE TABLE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="0775b-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span></span>
4. <span data-ttu-id="0775b-149">如果有 CLUSTERED 索引，請將其變更為 NONCLUSTERED。</span><span class="sxs-lookup"><span data-stu-id="0775b-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span></span>
5. <span data-ttu-id="0775b-150">使用 SP_RENAME 重新命名現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="0775b-150">Rename the existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="0775b-151">執行您已編輯的 CREATE TABLE 指令碼，以建立新的記憶體最佳化資料表複本。</span><span class="sxs-lookup"><span data-stu-id="0775b-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="0775b-152">使用 INSERT...SELECT * INTO，將資料複製到您的記憶體最佳化資料表：</span><span class="sxs-lookup"><span data-stu-id="0775b-152">Copy the data to your memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="0775b-153">步驟 5 (選擇性)：移轉預存程序</span><span class="sxs-lookup"><span data-stu-id="0775b-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="0775b-154">In-Memory 功能也可以修改預存程序，以改善效能。</span><span class="sxs-lookup"><span data-stu-id="0775b-154">The In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="0775b-155">原生編譯預存程序的考量</span><span class="sxs-lookup"><span data-stu-id="0775b-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="0775b-156">原生編譯預存程序的 T-SQL WITH 子句必須具有下列選項：</span><span class="sxs-lookup"><span data-stu-id="0775b-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="0775b-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="0775b-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="0775b-158">SCHEMABINDING：表示除非您捨棄預存程序，否則無法由預存程序以任何會影響到預存程序的方式變更其資料行定義的資料表。</span><span class="sxs-lookup"><span data-stu-id="0775b-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span></span>

<span data-ttu-id="0775b-159">原生模組必須使用一個大型 [ATOMIC 區塊](http://msdn.microsoft.com/library/dn452281.aspx) 進行交易管理。</span><span class="sxs-lookup"><span data-stu-id="0775b-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="0775b-160">沒有明確 BEGIN TRANSACTION 或 ROLLBACK TRANSACTION 的角色。</span><span class="sxs-lookup"><span data-stu-id="0775b-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="0775b-161">如果您的程式碼偵測到違反商務規則，它可以利用 [THROW](http://msdn.microsoft.com/library/ee677615.aspx) 陳述式終止不可部分完成的區塊。</span><span class="sxs-lookup"><span data-stu-id="0775b-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="0775b-162">原生編譯的一般 CREATE PROCEDURE</span><span class="sxs-lookup"><span data-stu-id="0775b-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="0775b-163">建立原生編譯預存程序的 T-SQL 通常會類似於下列範本：</span><span class="sxs-lookup"><span data-stu-id="0775b-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span></span>

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

* <span data-ttu-id="0775b-164">就 TRANSACTION_ISOLATION_LEVEL 而言，SNAPSHOT 是原生編譯預存程序最常用的值。</span><span class="sxs-lookup"><span data-stu-id="0775b-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span></span> <span data-ttu-id="0775b-165">不過，也支援其他值的子集：</span><span class="sxs-lookup"><span data-stu-id="0775b-165">However,  a subset of the other values are also supported:</span></span>
  
  * <span data-ttu-id="0775b-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="0775b-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="0775b-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="0775b-167">SERIALIZABLE</span></span>
* <span data-ttu-id="0775b-168">sys.languages 檢視中必須有 LANGUAGE 值存在。</span><span class="sxs-lookup"><span data-stu-id="0775b-168">The LANGUAGE value must be present in the sys.languages view.</span></span>

### <a name="how-to-migrate-a-stored-procedure"></a><span data-ttu-id="0775b-169">如何移轉預存程序</span><span class="sxs-lookup"><span data-stu-id="0775b-169">How to migrate a stored procedure</span></span>
<span data-ttu-id="0775b-170">移轉步驟如下：</span><span class="sxs-lookup"><span data-stu-id="0775b-170">The migration steps are:</span></span>

1. <span data-ttu-id="0775b-171">取得規則解譯之預存程序的 CREATE PROCEDURE 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0775b-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="0775b-172">請重寫其標頭，以符合先前的範本。</span><span class="sxs-lookup"><span data-stu-id="0775b-172">Rewrite its header to match the previous template.</span></span>
3. <span data-ttu-id="0775b-173">確認預存程序 T-SQL 程式碼是否使用任何不支援原生編譯預存程序的功能。</span><span class="sxs-lookup"><span data-stu-id="0775b-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="0775b-174">視需要實作因應措施。</span><span class="sxs-lookup"><span data-stu-id="0775b-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="0775b-175">如需詳細資訊，請參閱 [原生編譯預存程序的移轉問題](http://msdn.microsoft.com/library/dn296678.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0775b-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="0775b-176">使用 SP_RENAME 重新命名舊的預存程序。</span><span class="sxs-lookup"><span data-stu-id="0775b-176">Rename the old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="0775b-177">或直接加以捨棄。</span><span class="sxs-lookup"><span data-stu-id="0775b-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="0775b-178">執行已編輯的 CREATE PROCEDURE T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0775b-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="0775b-179">步驟 6：在測試環境中執行您的工作負載</span><span class="sxs-lookup"><span data-stu-id="0775b-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="0775b-180">在測試資料庫中，執行與您在實際執行資料庫中執行的工作負載類似的工作負載。</span><span class="sxs-lookup"><span data-stu-id="0775b-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span></span> <span data-ttu-id="0775b-181">如此，將 In-Memory 功能用於資料表和預存程序所達到的效能改善應可顯現出來。</span><span class="sxs-lookup"><span data-stu-id="0775b-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="0775b-182">工作負載的主要屬性包括：</span><span class="sxs-lookup"><span data-stu-id="0775b-182">Major attributes of the workload are:</span></span>

* <span data-ttu-id="0775b-183">並行連線數目。</span><span class="sxs-lookup"><span data-stu-id="0775b-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="0775b-184">讀取/寫入比率。</span><span class="sxs-lookup"><span data-stu-id="0775b-184">Read/write ratio.</span></span>

<span data-ttu-id="0775b-185">若要修改並執行測試工作負載，請考慮使用方便的 ostress.exe 工具，如 [這裡](sql-database-in-memory.md)所說明。</span><span class="sxs-lookup"><span data-stu-id="0775b-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="0775b-186">為了盡可能減少網路延遲，請在資料庫所在的相同 Azure 地理區域中執行您的測試。</span><span class="sxs-lookup"><span data-stu-id="0775b-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="0775b-187">步驟 7：實作後的監視</span><span class="sxs-lookup"><span data-stu-id="0775b-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="0775b-188">請考慮監視您在實際執行環境中實作 In-Memory 的效能影響：</span><span class="sxs-lookup"><span data-stu-id="0775b-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="0775b-189">[監視記憶體內部儲存體](sql-database-in-memory-oltp-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="0775b-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="0775b-190">使用動態管理檢視監視 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0775b-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="0775b-191">相關連結</span><span class="sxs-lookup"><span data-stu-id="0775b-191">Related links</span></span>
* [<span data-ttu-id="0775b-192">In-Memory OLTP (In-Memory Optimization)</span><span class="sxs-lookup"><span data-stu-id="0775b-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="0775b-193">原生編譯預存程序簡介</span><span class="sxs-lookup"><span data-stu-id="0775b-193">Introduction to Natively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="0775b-194">記憶體最佳化建議程式</span><span class="sxs-lookup"><span data-stu-id="0775b-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

