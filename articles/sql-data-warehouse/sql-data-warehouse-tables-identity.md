---
title: "使用 IDENTITY 建立 Surrogate 索引鍵 |Microsoft Docs"
description: "了解如何使用 IDENTITY 在資料表上建立 Surrogate 索引鍵。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 3ab5d159e6eaeb830135fe134e108b0e4de4b7d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="45adc-103">使用 IDENTITY 建立 Surrogate 索引鍵</span><span class="sxs-lookup"><span data-stu-id="45adc-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="45adc-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="45adc-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="45adc-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="45adc-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="45adc-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="45adc-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="45adc-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="45adc-107">[Index][Index]</span></span>
> * <span data-ttu-id="45adc-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="45adc-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="45adc-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="45adc-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="45adc-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="45adc-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="45adc-111">[身分識別][Identity]</span><span class="sxs-lookup"><span data-stu-id="45adc-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="45adc-112">許多資料製造模型者在設計資料倉儲模型時，都喜歡在其資料表上建立 Surrogate 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="45adc-112">Many data modelers like to create surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="45adc-113">您可以使用 IDENTITY 屬性，在不影響載入效能的情況下，以簡單又有效的方式達成此目標。</span><span class="sxs-lookup"><span data-stu-id="45adc-113">You can use the IDENTITY property to achieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="45adc-114">開始使用 IDENTITY</span><span class="sxs-lookup"><span data-stu-id="45adc-114">Get started with IDENTITY</span></span>
<span data-ttu-id="45adc-115">您在初次建立資料表時，可以使用類似下列陳述式的語法，將資料表定義為具有 IDENTITY 屬性：</span><span class="sxs-lookup"><span data-stu-id="45adc-115">You can define a table as having the IDENTITY property when you first create the table by using syntax that is similar to the following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="45adc-116">然後，您可以使用 `INSERT..SELECT` 來填入資料表。</span><span class="sxs-lookup"><span data-stu-id="45adc-116">You can then use `INSERT..SELECT` to populate the table.</span></span>

## <a name="behavior"></a><span data-ttu-id="45adc-117">行為</span><span class="sxs-lookup"><span data-stu-id="45adc-117">Behavior</span></span>
<span data-ttu-id="45adc-118">IDENTITY 屬性的設計，可在不影響載入效能的情況下，於資料倉儲的所有發佈上進行相應放大。</span><span class="sxs-lookup"><span data-stu-id="45adc-118">The IDENTITY property is designed to scale out across all the distributions in the data warehouse without affecting load performance.</span></span> <span data-ttu-id="45adc-119">因此，IDENTITY 的實作便是為了達成這些目標。</span><span class="sxs-lookup"><span data-stu-id="45adc-119">Therefore, the implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="45adc-120">本節會重點說明此實作的細節，以協助您更全面地了解它們。</span><span class="sxs-lookup"><span data-stu-id="45adc-120">This section highlights the nuances of the implementation to help you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="45adc-121">值的配置</span><span class="sxs-lookup"><span data-stu-id="45adc-121">Allocation of values</span></span>
<span data-ttu-id="45adc-122">IDENTITY 屬性並不會保證 Surrogate 值的配置順序，這會反映出 SQL Server 和 Azure SQL Database 行為。</span><span class="sxs-lookup"><span data-stu-id="45adc-122">The IDENTITY property doesn't guarantee the order in which the surrogate values are allocated, which reflects the behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="45adc-123">不過，在 Azure SQL 資料倉儲中，此保證的不存在則更為明顯。</span><span class="sxs-lookup"><span data-stu-id="45adc-123">However, in Azure SQL Data Warehouse, the absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="45adc-124">下列範例將做出說明：</span><span class="sxs-lookup"><span data-stu-id="45adc-124">The following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="45adc-125">在上述範例中，有兩個資料列落在發佈 1 中。</span><span class="sxs-lookup"><span data-stu-id="45adc-125">In the preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="45adc-126">第一個資料列在資料行 `C1` 中具有 1 的 Surrogate 值，而第二個資料列則具有 61 的 Surrogate 值。</span><span class="sxs-lookup"><span data-stu-id="45adc-126">The first row has the surrogate value of 1 in column `C1`, and the second row has the surrogate value of 61.</span></span> <span data-ttu-id="45adc-127">這兩個值都是由 IDENTITY 屬性所產生。</span><span class="sxs-lookup"><span data-stu-id="45adc-127">Both of these values were generated by the IDENTITY property.</span></span> <span data-ttu-id="45adc-128">不過，值的配置並不是連續的。</span><span class="sxs-lookup"><span data-stu-id="45adc-128">However, the allocation of the values is not contiguous.</span></span> <span data-ttu-id="45adc-129">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="45adc-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="45adc-130">偏斜資料</span><span class="sxs-lookup"><span data-stu-id="45adc-130">Skewed data</span></span> 
<span data-ttu-id="45adc-131">資料類型的值範圍會平均分散於發佈上。</span><span class="sxs-lookup"><span data-stu-id="45adc-131">The range of values for the data type are spread evenly across the distributions.</span></span> <span data-ttu-id="45adc-132">如果分散式資料表受到偏斜資料的影響，則可供資料類型使用的值範圍可能會提前耗盡。</span><span class="sxs-lookup"><span data-stu-id="45adc-132">If a distributed table suffers from skewed data, then the range of values available to the datatype can be exhausted prematurely.</span></span> <span data-ttu-id="45adc-133">例如，如果所有資料最後都位於單一發佈中，則該資料表實際上將只能存取該資料類型六十分之一的值。</span><span class="sxs-lookup"><span data-stu-id="45adc-133">For example, if all the data ends up in a single distribution, then effectively the table has access to only one-sixtieth of the values of the data type.</span></span> <span data-ttu-id="45adc-134">因此，IDENTITY 屬性僅限用於 `INT` 和 `BIGINT` 資料類型。</span><span class="sxs-lookup"><span data-stu-id="45adc-134">For this reason, the IDENTITY property is limited to `INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="45adc-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="45adc-135">SELECT..INTO</span></span>
<span data-ttu-id="45adc-136">將現有的 IDENTITY 資料行選取至新的資料表時，新的資料行會繼承 IDENTITY 屬性，除非下列其中一項條件成立：</span><span class="sxs-lookup"><span data-stu-id="45adc-136">When an existing IDENTITY column is selected into a new table, the new column inherits the IDENTITY property, unless one of the following conditions is true:</span></span>
- <span data-ttu-id="45adc-137">SELECT 陳述式包含聯結。</span><span class="sxs-lookup"><span data-stu-id="45adc-137">The SELECT statement contains a join.</span></span>
- <span data-ttu-id="45adc-138">多個 SELECT 陳述式使用 UNION 進行聯結。</span><span class="sxs-lookup"><span data-stu-id="45adc-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="45adc-139">IDENTITY 資料行在 SELECT 清單中列出多次。</span><span class="sxs-lookup"><span data-stu-id="45adc-139">The IDENTITY column is listed more than one time in the SELECT list.</span></span>
- <span data-ttu-id="45adc-140">IDENTITY 資料行是運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="45adc-140">The IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="45adc-141">如果這些條件的其中之一成立，資料行會建立為「非 NULL」，而不是繼承 IDENTITY 屬性。</span><span class="sxs-lookup"><span data-stu-id="45adc-141">If any one of these conditions is true, the column is created NOT NULL instead of inheriting the IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="45adc-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="45adc-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="45adc-143">CREATE TABLE AS SELECT (CTAS) 會遵循針對 SELECT..INTO 記錄的相同 SQL Server 行為。</span><span class="sxs-lookup"><span data-stu-id="45adc-143">CREATE TABLE AS SELECT (CTAS) follows the same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="45adc-144">不過，您無法在陳述式 `CREATE TABLE` 部分的資料行定義中指定 IDENTITY 屬性。</span><span class="sxs-lookup"><span data-stu-id="45adc-144">However, you can't specify an IDENTITY property in the column definition of the `CREATE TABLE` part of the statement.</span></span> <span data-ttu-id="45adc-145">您也無法在 CTAS 的 `SELECT` 部分使用 IDENTITY 函式。</span><span class="sxs-lookup"><span data-stu-id="45adc-145">You also can't use the IDENTITY function in the `SELECT` part of the CTAS.</span></span> <span data-ttu-id="45adc-146">若要填入資料表，您必須使用 `CREATE TABLE` 來定義資料表，接著使用 `INSERT..SELECT` 來填入它。</span><span class="sxs-lookup"><span data-stu-id="45adc-146">To populate a table, you need to use `CREATE TABLE` to define the table followed by `INSERT..SELECT` to populate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="45adc-147">明確地將值插入 IDENTITY 資料行</span><span class="sxs-lookup"><span data-stu-id="45adc-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="45adc-148">SQL 資料倉儲支援 `SET IDENTITY_INSERT <your table> ON|OFF` 語法。</span><span class="sxs-lookup"><span data-stu-id="45adc-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="45adc-149">您可以使用此語法來明確地將值插入 IDENTITY 資料行。</span><span class="sxs-lookup"><span data-stu-id="45adc-149">You can use this syntax to explicitly insert values into the IDENTITY column.</span></span>

<span data-ttu-id="45adc-150">許多資料製造模型者喜歡在其維度的特定資料列中使用預先定義的負數值。</span><span class="sxs-lookup"><span data-stu-id="45adc-150">Many data modelers like to use predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="45adc-151">其中一個範例為 -1 或「未知的成員」資料列。</span><span class="sxs-lookup"><span data-stu-id="45adc-151">An example is the -1 or "unknown member" row.</span></span> 

<span data-ttu-id="45adc-152">下一個指令碼會示範如何使用 SET IDENTITY_INSERT 明確地加入此資料列：</span><span class="sxs-lookup"><span data-stu-id="45adc-152">The next script shows how to explicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="45adc-153">使用 IDENTITY 將資料載入資料表</span><span class="sxs-lookup"><span data-stu-id="45adc-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="45adc-154">IDENTITY 屬性的存在會對您的資料載入程式碼造成一些影響。</span><span class="sxs-lookup"><span data-stu-id="45adc-154">The presence of the IDENTITY property has some implications to your data-loading code.</span></span> <span data-ttu-id="45adc-155">本節會重點說明使用 IDENTITY 將資料載入資料表的一些基本模式。</span><span class="sxs-lookup"><span data-stu-id="45adc-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="45adc-156">使用 PolyBase 載入資料</span><span class="sxs-lookup"><span data-stu-id="45adc-156">Load data with PolyBase</span></span>
<span data-ttu-id="45adc-157">若要使用 IDENTITY 將資料載入資料表並產生 Surrogate 索引鍵，請建立資料表，然後使用 INSERT..SELECT 或 INSERT..VALUES 來執行載入。</span><span class="sxs-lookup"><span data-stu-id="45adc-157">To load data into a table and generate a surrogate key by using IDENTITY, create the table and then use INSERT..SELECT or INSERT..VALUES to perform the load.</span></span>

<span data-ttu-id="45adc-158">下列範例會重點說明基本模式：</span><span class="sxs-lookup"><span data-stu-id="45adc-158">The following example highlights the basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT to populate the table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="45adc-159">目前在使用 IDENTITY 資料行將資料載入資料表時，並無法使用 `CREATE TABLE AS SELECT`。</span><span class="sxs-lookup"><span data-stu-id="45adc-159">It's not possible to use `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="45adc-160">如需使用大量複製程式 (BCP) 工具載入資料的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="45adc-160">For more information on loading data by using the bulk copy program (BCP) tool, see the following articles:</span></span>

- <span data-ttu-id="45adc-161">[使用 PolyBase 載入][]</span><span class="sxs-lookup"><span data-stu-id="45adc-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="45adc-162">[PolyBase 最佳做法][]</span><span class="sxs-lookup"><span data-stu-id="45adc-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="45adc-163">使用 BCP 載入資料</span><span class="sxs-lookup"><span data-stu-id="45adc-163">Load data with BCP</span></span>
<span data-ttu-id="45adc-164">BCP 是一種命令列工具，您可以用來將資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="45adc-164">BCP is a command-line tool that you can use to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="45adc-165">它的其中一個參數 (-E) 可控制使用 IDENTITY 資料行將資料載入資料表時的 BCP 行為。</span><span class="sxs-lookup"><span data-stu-id="45adc-165">One of its parameters (-E) controls the behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="45adc-166">指定 -E 時，保留在具 IDENTITY 之資料行的輸入檔案中的值將會被保留下來。</span><span class="sxs-lookup"><span data-stu-id="45adc-166">When -E is specified, the values held in the input file for the column with IDENTITY are retained.</span></span> <span data-ttu-id="45adc-167">如果「未」指定 -E，系統會忽略此資料行中的值。</span><span class="sxs-lookup"><span data-stu-id="45adc-167">If -E is *not* specified, then the values in this column are ignored.</span></span> <span data-ttu-id="45adc-168">如果沒有包含 IDENTITY 資料行，則會以正常方式載入資料。</span><span class="sxs-lookup"><span data-stu-id="45adc-168">If the identity column is not included, then the data is loaded as normal.</span></span> <span data-ttu-id="45adc-169">值會根據屬性的增量和種子原則產生。</span><span class="sxs-lookup"><span data-stu-id="45adc-169">The values are generated according to the increment and seed policy of the property.</span></span>

<span data-ttu-id="45adc-170">如需使用 BCP 載入資料的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="45adc-170">For more information on loading data by using BCP, see the following articles:</span></span>

- <span data-ttu-id="45adc-171">[使用 BCP 載入][]</span><span class="sxs-lookup"><span data-stu-id="45adc-171">[Load with BCP][]</span></span>
- <span data-ttu-id="45adc-172">[MSDN 中的 BCP][]</span><span class="sxs-lookup"><span data-stu-id="45adc-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="45adc-173">目錄檢視</span><span class="sxs-lookup"><span data-stu-id="45adc-173">Catalog views</span></span>
<span data-ttu-id="45adc-174">SQL 資料倉儲支援 `sys.identity_columns` 目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="45adc-174">SQL Data Warehouse supports the `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="45adc-175">此檢視可以用來識別具有 IDENTITY 屬性的資料行。</span><span class="sxs-lookup"><span data-stu-id="45adc-175">This view can be used to identify a column that has the IDENTITY property.</span></span>

<span data-ttu-id="45adc-176">為了協助您深入了解資料庫結構描述，此範例示範如何整合 `sys.identity_columns` 與其他系統目錄檢視：</span><span class="sxs-lookup"><span data-stu-id="45adc-176">To help you better understand the database schema, this example shows how to integrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="45adc-177">限制</span><span class="sxs-lookup"><span data-stu-id="45adc-177">Limitations</span></span>
<span data-ttu-id="45adc-178">下列案例不能使用 IDENTITY 屬性：</span><span class="sxs-lookup"><span data-stu-id="45adc-178">The IDENTITY property can't be used in the following scenarios:</span></span>
- <span data-ttu-id="45adc-179">資料行資料類型不是 INT 或 BIGINT</span><span class="sxs-lookup"><span data-stu-id="45adc-179">Where the column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="45adc-180">資料行也是散發索引鍵</span><span class="sxs-lookup"><span data-stu-id="45adc-180">Where the column is also the distribution key</span></span>
- <span data-ttu-id="45adc-181">資料表為外部資料表</span><span class="sxs-lookup"><span data-stu-id="45adc-181">Where the table is an external table</span></span> 

<span data-ttu-id="45adc-182">SQL 資料倉儲中不支援下列相關函式：</span><span class="sxs-lookup"><span data-stu-id="45adc-182">The following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="45adc-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="45adc-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="45adc-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="45adc-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="45adc-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="45adc-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="45adc-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="45adc-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="45adc-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="45adc-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="45adc-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="45adc-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="45adc-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="45adc-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="45adc-190">工作</span><span class="sxs-lookup"><span data-stu-id="45adc-190">Tasks</span></span>

<span data-ttu-id="45adc-191">本節提供一些範例程式碼，可在您使用 IDENTITY 資料行時用來執行一般工作。</span><span class="sxs-lookup"><span data-stu-id="45adc-191">This section provides some sample code you can use to perform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="45adc-192">在下列所有工作中，資料行 C1 都會是 IDENTITY。</span><span class="sxs-lookup"><span data-stu-id="45adc-192">Column C1 is the IDENTITY in all the following tasks.</span></span>
> 
 
### <a name="find-the-highest-allocated-value-for-a-table"></a><span data-ttu-id="45adc-193">找出資料表的最大配置值</span><span class="sxs-lookup"><span data-stu-id="45adc-193">Find the highest allocated value for a table</span></span>
<span data-ttu-id="45adc-194">使用 `MAX()` 函式來判斷針對分散式資料表所配置的最大值：</span><span class="sxs-lookup"><span data-stu-id="45adc-194">Use the `MAX()` function to determine the highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-the-seed-and-increment-for-the-identity-property"></a><span data-ttu-id="45adc-195">找出 IDENTITY 屬性的種子和增量</span><span class="sxs-lookup"><span data-stu-id="45adc-195">Find the seed and increment for the IDENTITY property</span></span>
<span data-ttu-id="45adc-196">您可以透過下列查詢，來使用目錄檢視以探索資料表的識別值增量和種子設定值：</span><span class="sxs-lookup"><span data-stu-id="45adc-196">You can use the catalog views to discover the identity increment and seed configuration values for a table by using the following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="45adc-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45adc-197">Next steps</span></span>

* <span data-ttu-id="45adc-198">若要深入了解開發資料表，請參閱[資料表概觀][Overview]、[資料表的資料類型][Data Types]、[散發資料表][Distribute]、[編製資料表的索引][Index]、[分割資料表][Partition]和[暫存資料表][Temporary]。</span><span class="sxs-lookup"><span data-stu-id="45adc-198">To learn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="45adc-199">如需最佳做法的詳細資訊，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="45adc-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<span data-ttu-id="45adc-200">[使用 bcp 載入]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span><span class="sxs-lookup"><span data-stu-id="45adc-200">[Load with bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span></span>
<span data-ttu-id="45adc-201">[使用 PolyBase 載入]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span><span class="sxs-lookup"><span data-stu-id="45adc-201">[Load with PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span></span>
<span data-ttu-id="45adc-202">[PolyBase 最佳做法]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span><span class="sxs-lookup"><span data-stu-id="45adc-202">[PolyBase best practices]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span></span>


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
<span data-ttu-id="45adc-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span><span class="sxs-lookup"><span data-stu-id="45adc-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span></span>
<span data-ttu-id="45adc-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span><span class="sxs-lookup"><span data-stu-id="45adc-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span></span>
<span data-ttu-id="45adc-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span><span class="sxs-lookup"><span data-stu-id="45adc-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span></span>
<span data-ttu-id="45adc-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span><span class="sxs-lookup"><span data-stu-id="45adc-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span></span>
<span data-ttu-id="45adc-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span><span class="sxs-lookup"><span data-stu-id="45adc-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span></span>
<span data-ttu-id="45adc-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span><span class="sxs-lookup"><span data-stu-id="45adc-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span></span>
<span data-ttu-id="45adc-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span><span class="sxs-lookup"><span data-stu-id="45adc-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span></span>

<span data-ttu-id="45adc-210">[MSDN 中的 bcp]: https://msdn.microsoft.com/library/ms162802.aspx</span><span class="sxs-lookup"><span data-stu-id="45adc-210">[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span></span>
  

<!--Other Web references-->  
