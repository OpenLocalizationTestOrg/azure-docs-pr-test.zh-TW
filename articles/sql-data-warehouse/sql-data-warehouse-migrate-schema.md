---
title: "aaaMigrate 您結構描述 tooSQL 資料倉儲 |Microsoft 文件"
description: "移轉您的結構描述 tooAzure SQL 資料倉儲來開發方案的提示。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="2dab0-103">移轉您的結構描述 tooSQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="2dab0-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="2dab0-104">移轉您的 SQL 結構描述 tooSQL 資料倉儲的指引。</span><span class="sxs-lookup"><span data-stu-id="2dab0-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="2dab0-105">規劃結構描述移轉</span><span class="sxs-lookup"><span data-stu-id="2dab0-105">Plan your schema migration</span></span>

<span data-ttu-id="2dab0-106">當您規劃移轉時，請參閱 hello[資料表概觀][ table overview] toobecome 熟悉例如統計資料、 發佈、 分割和索引的資料表設計考量。</span><span class="sxs-lookup"><span data-stu-id="2dab0-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="2dab0-107">它也會列出一些[不支援的資料表功能][unsupported table features]和其因應措施。</span><span class="sxs-lookup"><span data-stu-id="2dab0-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="2dab0-108">使用使用者定義的結構描述 tooconsolidate 資料庫</span><span class="sxs-lookup"><span data-stu-id="2dab0-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="2dab0-109">您現有的工作負載可能有多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="2dab0-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="2dab0-110">例如，SQL Server 資料倉儲可能包含臨時資料庫、資料倉儲資料庫和某些資料超市資料庫。</span><span class="sxs-lookup"><span data-stu-id="2dab0-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="2dab0-111">在此拓撲中，每個資料庫都會搭配個別的安全性原則，以個別工作負載的形式執行。</span><span class="sxs-lookup"><span data-stu-id="2dab0-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="2dab0-112">相反地，SQL 資料倉儲執行某個資料庫中的 hello 整個資料倉儲工作負載。</span><span class="sxs-lookup"><span data-stu-id="2dab0-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="2dab0-113">不允許跨資料庫聯結。</span><span class="sxs-lookup"><span data-stu-id="2dab0-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="2dab0-114">因此，SQL 資料倉儲必須要有 hello hello 某個資料庫中儲存的資料倉儲 toobe 所使用的所有資料表。</span><span class="sxs-lookup"><span data-stu-id="2dab0-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="2dab0-115">我們建議使用使用者定義的結構描述 tooconsolidate 您現有的工作負載至一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="2dab0-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="2dab0-116">如需範例，請參閱[使用者定義的結構描述](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="2dab0-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="2dab0-117">使用相容的資料類型</span><span class="sxs-lookup"><span data-stu-id="2dab0-117">Use compatible data types</span></span>
<span data-ttu-id="2dab0-118">修改您與 SQL 資料倉儲相容的資料型別 toobe。</span><span class="sxs-lookup"><span data-stu-id="2dab0-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="2dab0-119">如需所有支援和不支援資料類型的清單，請參閱[資料類型][data types]。</span><span class="sxs-lookup"><span data-stu-id="2dab0-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="2dab0-120">該主題提供解決 hello 不支援的型別。</span><span class="sxs-lookup"><span data-stu-id="2dab0-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="2dab0-121">它也提供查詢 tooidentify 不支援在 SQL 資料倉儲中的現有類型。</span><span class="sxs-lookup"><span data-stu-id="2dab0-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="2dab0-122">將資料列大小最小化</span><span class="sxs-lookup"><span data-stu-id="2dab0-122">Minimize row size</span></span>
<span data-ttu-id="2dab0-123">為了達到最佳效能，最小化 hello 的資料表的資料列長度。</span><span class="sxs-lookup"><span data-stu-id="2dab0-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="2dab0-124">較短的資料列長度會導致 toobetter 效能，因為使用 hello 最小資料類型可為您的資料。</span><span class="sxs-lookup"><span data-stu-id="2dab0-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="2dab0-125">針對資料表的資料列寬度，PolyBase 具有 1 MB 的限制。</span><span class="sxs-lookup"><span data-stu-id="2dab0-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="2dab0-126">如果您打算 tooload 資料到含有 PolyBase 的 SQL 資料倉儲時，更新您的資料表 toohave 最大資料列的寬度小於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="2dab0-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="2dab0-127">指定 hello 散發選項</span><span class="sxs-lookup"><span data-stu-id="2dab0-127">Specify hello distribution option</span></span>
<span data-ttu-id="2dab0-128">SQL 資料倉儲是一種分散式資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="2dab0-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="2dab0-129">每個資料表散發，或在 hello 計算節點之間複寫。</span><span class="sxs-lookup"><span data-stu-id="2dab0-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="2dab0-130">沒有選項可讓您指定如何 toodistribute hello 資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="2dab0-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="2dab0-131">hello 選項包括循環複寫，或雜湊散發。</span><span class="sxs-lookup"><span data-stu-id="2dab0-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="2dab0-132">各有其優缺點。</span><span class="sxs-lookup"><span data-stu-id="2dab0-132">Each has pros and cons.</span></span> <span data-ttu-id="2dab0-133">如果您未指定 hello 散發選項，SQL 資料倉儲會使用循環配置資源為 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="2dab0-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="2dab0-134">Hello 預設循環配置資源。</span><span class="sxs-lookup"><span data-stu-id="2dab0-134">Round-robin is hello default.</span></span> <span data-ttu-id="2dab0-135">它是最簡單 toouse hello，並載入 hello 資料盡快，但聯結需要移動資料的查詢效能會變慢。</span><span class="sxs-lookup"><span data-stu-id="2dab0-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="2dab0-136">複寫的儲存每個計算節點上的 hello 資料表的副本。</span><span class="sxs-lookup"><span data-stu-id="2dab0-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="2dab0-137">由於複寫資料表的聯結和彙總作業並不需要移動資料，所以很有效率。</span><span class="sxs-lookup"><span data-stu-id="2dab0-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="2dab0-138">相對的，它們需要額外的儲存體，因此比較適合較小的資料表使用。</span><span class="sxs-lookup"><span data-stu-id="2dab0-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="2dab0-139">分散式的雜湊會將 hello 資料列分散到所有的 hello 節點，透過雜湊函式。</span><span class="sxs-lookup"><span data-stu-id="2dab0-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="2dab0-140">分散式的雜湊表是 hello 核心 SQL 資料倉儲的因為它們是大型資料表上的設計的 tooprovide 高的查詢效能。</span><span class="sxs-lookup"><span data-stu-id="2dab0-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="2dab0-141">此選項需要一些規劃 tooselect hello 最佳資料行其中 toodistribute hello 資料。</span><span class="sxs-lookup"><span data-stu-id="2dab0-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="2dab0-142">不過，如果您沒有選擇最佳資料行 hello hello 第一次，您可以輕鬆地重新散發 hello 另一個資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="2dab0-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="2dab0-143">toochoose hello 最佳散發選項針對每個資料表，請參閱[分散式資料表](sql-data-warehouse-tables-distribute.md)。</span><span class="sxs-lookup"><span data-stu-id="2dab0-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="2dab0-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2dab0-144">Next steps</span></span>
<span data-ttu-id="2dab0-145">一旦您已成功移轉您的資料庫結構描述 tooSQL 資料倉儲，請繼續進行 tooone 的 hello 下列文章：</span><span class="sxs-lookup"><span data-stu-id="2dab0-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="2dab0-146">[移轉資料][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="2dab0-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="2dab0-147">[移轉程式碼][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="2dab0-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="2dab0-148">如需有關 SQL 資料倉儲的最佳作法，請參閱 hello[最佳做法][ best practices]發行項。</span><span class="sxs-lookup"><span data-stu-id="2dab0-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
