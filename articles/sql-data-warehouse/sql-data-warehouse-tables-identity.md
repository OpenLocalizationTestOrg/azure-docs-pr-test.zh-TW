---
title: "aaaCreate surrogate 索引鍵使用的識別 |Microsoft 文件"
description: "了解 toouse 識別 toocreate 代理程式資料表上的索引鍵。"
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
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="7730c-103">使用 IDENTITY 建立 Surrogate 索引鍵</span><span class="sxs-lookup"><span data-stu-id="7730c-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7730c-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="7730c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="7730c-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="7730c-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="7730c-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="7730c-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="7730c-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="7730c-107">[Index][Index]</span></span>
> * <span data-ttu-id="7730c-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="7730c-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="7730c-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="7730c-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="7730c-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="7730c-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="7730c-111">[身分識別][Identity]</span><span class="sxs-lookup"><span data-stu-id="7730c-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="7730c-112">它們在設計資料倉儲模型時，許多資料建模者喜歡 toocreate surrogate 索引鍵，其資料表上。</span><span class="sxs-lookup"><span data-stu-id="7730c-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="7730c-113">您可以使用 hello 識別屬性 tooachieve 此目標只是和有效率的方法而不會影響載入效能。</span><span class="sxs-lookup"><span data-stu-id="7730c-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="7730c-114">開始使用 IDENTITY</span><span class="sxs-lookup"><span data-stu-id="7730c-114">Get started with IDENTITY</span></span>
<span data-ttu-id="7730c-115">您可以將資料表定義為具有 hello IDENTITY 屬性，當您初次建立 hello 資料表使用 「 類似 toohello 後面的陳述式的語法：</span><span class="sxs-lookup"><span data-stu-id="7730c-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

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

<span data-ttu-id="7730c-116">然後您可以使用`INSERT..SELECT`toopopulate hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="7730c-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="7730c-117">行為</span><span class="sxs-lookup"><span data-stu-id="7730c-117">Behavior</span></span>
<span data-ttu-id="7730c-118">hello 識別屬性是設計出 tooscale 跨所有 hello 分佈，而不會影響載入效能 hello 資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="7730c-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="7730c-119">因此，身分識別的 hello 實作會導向達成這些目標。</span><span class="sxs-lookup"><span data-stu-id="7730c-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="7730c-120">本章節強調 hello 細節的 hello 實作 toohelp 您瞭解這些更完整。</span><span class="sxs-lookup"><span data-stu-id="7730c-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="7730c-121">值的配置</span><span class="sxs-lookup"><span data-stu-id="7730c-121">Allocation of values</span></span>
<span data-ttu-id="7730c-122">hello IDENTITY 屬性並不保證 hello 順序中的 hello 配置 surrogate 值，其會反映的 SQL Server 和 Azure SQL Database 的 hello 行為。</span><span class="sxs-lookup"><span data-stu-id="7730c-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="7730c-123">不過，在 Azure SQL 資料倉儲中，更唸成 hello 缺乏保證。</span><span class="sxs-lookup"><span data-stu-id="7730c-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="7730c-124">hello 下列範例會示範：</span><span class="sxs-lookup"><span data-stu-id="7730c-124">hello following example is an illustration:</span></span>

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

<span data-ttu-id="7730c-125">在上述範例中的 hello，兩個資料列處於發佈 1。</span><span class="sxs-lookup"><span data-stu-id="7730c-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="7730c-126">hello 第一個資料列資料行有 hello surrogate 值為 1 `C1`，而且 hello 第二個資料列 61 hello surrogate 值。</span><span class="sxs-lookup"><span data-stu-id="7730c-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="7730c-127">兩個這些值所產生的 hello IDENTITY 屬性。</span><span class="sxs-lookup"><span data-stu-id="7730c-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="7730c-128">不過，不是連續的 hello 值 hello 配置。</span><span class="sxs-lookup"><span data-stu-id="7730c-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="7730c-129">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="7730c-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="7730c-130">偏斜資料</span><span class="sxs-lookup"><span data-stu-id="7730c-130">Skewed data</span></span> 
<span data-ttu-id="7730c-131">hello hello 資料類型的值範圍會平均分散 hello 分佈。</span><span class="sxs-lookup"><span data-stu-id="7730c-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="7730c-132">如果資料的誤用因分散式的資料表，然後 hello 可用 toohello 資料型別可能會耗盡不當的值範圍。</span><span class="sxs-lookup"><span data-stu-id="7730c-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="7730c-133">比方說，如果所有的 hello 資料最後會在單一通訊中，然後有效 hello 資料表有存取 tooonly 一個 sixtieth hello hello 資料類型值。</span><span class="sxs-lookup"><span data-stu-id="7730c-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="7730c-134">基於這個理由，hello IDENTITY 屬性太有限`INT`和`BIGINT`資料型別。</span><span class="sxs-lookup"><span data-stu-id="7730c-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="7730c-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="7730c-135">SELECT..INTO</span></span>
<span data-ttu-id="7730c-136">到新的資料表選取現有的身分識別資料行時，hello 新資料行就會繼承 hello IDENTITY 屬性，除非其中一個 hello 下列條件成立：</span><span class="sxs-lookup"><span data-stu-id="7730c-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="7730c-137">hello SELECT 陳述式包含聯結。</span><span class="sxs-lookup"><span data-stu-id="7730c-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="7730c-138">多個 SELECT 陳述式使用 UNION 進行聯結。</span><span class="sxs-lookup"><span data-stu-id="7730c-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="7730c-139">hello 身分識別資料行被列一次以上 hello 選取清單中。</span><span class="sxs-lookup"><span data-stu-id="7730c-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="7730c-140">hello 身分識別資料行是運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="7730c-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="7730c-141">如果任何一個條件為 true，hello 資料行建立成 NOT NULL 而非繼承 hello IDENTITY 屬性。</span><span class="sxs-lookup"><span data-stu-id="7730c-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="7730c-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="7730c-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="7730c-143">建立資料表 AS 選取 (CTAS) 如下所示 hello 相同的 SQL Server 行為，以便進行 SELECT 記錄...到。</span><span class="sxs-lookup"><span data-stu-id="7730c-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="7730c-144">不過，您無法 hello hello 資料行定義中指定的 IDENTITY 屬性`CREATE TABLE`hello 陳述式的一部分。</span><span class="sxs-lookup"><span data-stu-id="7730c-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="7730c-145">您也無法使用 hello IDENTITY 函數在 hello `SELECT` hello CTAS 的一部分。</span><span class="sxs-lookup"><span data-stu-id="7730c-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="7730c-146">toopopulate 資料表，您需要 toouse `CREATE TABLE` toodefine hello 表格後面`INSERT..SELECT`toopopulate 它。</span><span class="sxs-lookup"><span data-stu-id="7730c-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="7730c-147">明確地將值插入 IDENTITY 資料行</span><span class="sxs-lookup"><span data-stu-id="7730c-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="7730c-148">SQL 資料倉儲支援 `SET IDENTITY_INSERT <your table> ON|OFF` 語法。</span><span class="sxs-lookup"><span data-stu-id="7730c-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="7730c-149">您可以使用此語法 tooexplicitly 插入值到 hello 識別資料行。</span><span class="sxs-lookup"><span data-stu-id="7730c-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="7730c-150">許多資料建模者像 toouse 預先定義的負值特定值維度中的資料列。</span><span class="sxs-lookup"><span data-stu-id="7730c-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="7730c-151">例如，-1 hello 或 「 未知的成員 」 資料列。</span><span class="sxs-lookup"><span data-stu-id="7730c-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="7730c-152">hello 下一個指令碼會示範 tooexplicitly 利用 SET IDENTITY_INSERT 所新增的這個資料列：</span><span class="sxs-lookup"><span data-stu-id="7730c-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

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

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="7730c-153">使用 IDENTITY 將資料載入資料表</span><span class="sxs-lookup"><span data-stu-id="7730c-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="7730c-154">hello 的 hello IDENTITY 屬性的目前狀態有某些含意 tooyour 資料載入程式碼。</span><span class="sxs-lookup"><span data-stu-id="7730c-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="7730c-155">本節會重點說明使用 IDENTITY 將資料載入資料表的一些基本模式。</span><span class="sxs-lookup"><span data-stu-id="7730c-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="7730c-156">使用 PolyBase 載入資料</span><span class="sxs-lookup"><span data-stu-id="7730c-156">Load data with PolyBase</span></span>
<span data-ttu-id="7730c-157">tooload 資料到資料表和產生 surrogate 索引鍵使用的識別、 建立 hello 資料表，然後使用 INSERT...SELECT 或 INSERT...值 tooperform hello 負載。</span><span class="sxs-lookup"><span data-stu-id="7730c-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="7730c-158">hello 下列範例會反白顯示 hello 基本模式：</span><span class="sxs-lookup"><span data-stu-id="7730c-158">hello following example highlights hello basic pattern:</span></span>
 
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

--Use INSERT..SELECT toopopulate hello table from an external table
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
> <span data-ttu-id="7730c-159">不可能 toouse`CREATE TABLE AS SELECT`目前時將資料載入資料表之 IDENTITY 資料行。</span><span class="sxs-lookup"><span data-stu-id="7730c-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="7730c-160">如需有關使用 hello 大量複製程式 (BCP) 工具來載入資料的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="7730c-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="7730c-161">[使用 PolyBase 載入][]</span><span class="sxs-lookup"><span data-stu-id="7730c-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="7730c-162">[PolyBase 最佳做法][]</span><span class="sxs-lookup"><span data-stu-id="7730c-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="7730c-163">使用 BCP 載入資料</span><span class="sxs-lookup"><span data-stu-id="7730c-163">Load data with BCP</span></span>
<span data-ttu-id="7730c-164">BCP 就會是命令列工具，您可以使用 tooload 資料到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="7730c-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="7730c-165">其中一個參數 (-E) 將資料載入資料表之 IDENTITY 資料行時，控制項 hello BCP 的行為。</span><span class="sxs-lookup"><span data-stu-id="7730c-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="7730c-166">指定-E 時，識別持有 hello hello 資料行的輸入檔中的 hello 值都會保留下來。</span><span class="sxs-lookup"><span data-stu-id="7730c-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="7730c-167">如果-E 是*不*指定，則會忽略此資料行中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="7730c-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="7730c-168">如果不包含 hello 識別資料行，則 hello 資料被載入以正常的。</span><span class="sxs-lookup"><span data-stu-id="7730c-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="7730c-169">hello 值會產生根據 toohello 遞增和種子原則 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="7730c-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="7730c-170">如需有關使用 BCP 來載入資料的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="7730c-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="7730c-171">[使用 BCP 載入][]</span><span class="sxs-lookup"><span data-stu-id="7730c-171">[Load with BCP][]</span></span>
- <span data-ttu-id="7730c-172">[MSDN 中的 BCP][]</span><span class="sxs-lookup"><span data-stu-id="7730c-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="7730c-173">目錄檢視</span><span class="sxs-lookup"><span data-stu-id="7730c-173">Catalog views</span></span>
<span data-ttu-id="7730c-174">SQL 資料倉儲支援 hello`sys.identity_columns`目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="7730c-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="7730c-175">這個檢視可以使用的 tooidentify 具有 hello IDENTITY 屬性的資料行。</span><span class="sxs-lookup"><span data-stu-id="7730c-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="7730c-176">toohelp 深入了解 hello 資料庫結構描述，這個範例會示範如何 toointegrate`sys.identity_columns`與其他系統目錄檢視：</span><span class="sxs-lookup"><span data-stu-id="7730c-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

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

## <a name="limitations"></a><span data-ttu-id="7730c-177">限制</span><span class="sxs-lookup"><span data-stu-id="7730c-177">Limitations</span></span>
<span data-ttu-id="7730c-178">hello 識別屬性不能在下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="7730c-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="7730c-179">其中 hello 資料行資料類型不是 INT 或 BIGINT</span><span class="sxs-lookup"><span data-stu-id="7730c-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="7730c-180">其中 hello 資料行也是 hello 散發索引鍵</span><span class="sxs-lookup"><span data-stu-id="7730c-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="7730c-181">Hello 資料表所在的外部資料表</span><span class="sxs-lookup"><span data-stu-id="7730c-181">Where hello table is an external table</span></span> 

<span data-ttu-id="7730c-182">SQL 資料倉儲中不支援下列相關函式的 hello:</span><span class="sxs-lookup"><span data-stu-id="7730c-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="7730c-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="7730c-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="7730c-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="7730c-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="7730c-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="7730c-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="7730c-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="7730c-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="7730c-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="7730c-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="7730c-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="7730c-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="7730c-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="7730c-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="7730c-190">工作</span><span class="sxs-lookup"><span data-stu-id="7730c-190">Tasks</span></span>

<span data-ttu-id="7730c-191">本節提供範例程式碼，當您使用識別欄位時，您可以使用 tooperform 一般工作。</span><span class="sxs-lookup"><span data-stu-id="7730c-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="7730c-192">資料行 C1 是在下列工作的所有 hello hello 身分識別。</span><span class="sxs-lookup"><span data-stu-id="7730c-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="7730c-193">找到資料表的配置 hello 最高值</span><span class="sxs-lookup"><span data-stu-id="7730c-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="7730c-194">使用 hello`MAX()`函式的分散式資料表配置 toodetermine hello 最大值：</span><span class="sxs-lookup"><span data-stu-id="7730c-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="7730c-195">尋找 hello 種子和遞增值 hello IDENTITY 屬性</span><span class="sxs-lookup"><span data-stu-id="7730c-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="7730c-196">您可以使用 hello 目錄檢視 toodiscover hello 識別遞增和種子組態值的資料表使用下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="7730c-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="7730c-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7730c-197">Next steps</span></span>

* <span data-ttu-id="7730c-198">toolearn 進一步了解開發資料表，請參閱[資料表概觀][Overview]，[資料表的資料型別][Data Types]，[散發資料表][ Distribute]，[索引資料表][Index]，[分割資料表][Partition]，和[暫存資料表][Temporary]。</span><span class="sxs-lookup"><span data-stu-id="7730c-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="7730c-199">如需最佳做法的詳細資訊，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="7730c-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

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

[使用 bcp 載入]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[使用 PolyBase 載入]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[PolyBase 最佳做法]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[MSDN 中的 bcp]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
