---
title: "將您的結構描述移轉至 SQL 資料倉儲 | Microsoft Docs"
description: "將您的結構描述移轉至 Azure SQL 資料倉儲來開發解決方案的秘訣。"
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
ms.openlocfilehash: 07ca2321852e276502187e768177e7e82bdfd080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-schemas-to-sql-data-warehouse"></a><span data-ttu-id="59a52-103">將您的結構描述移轉至 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="59a52-103">Migrate your schemas to SQL Data Warehouse</span></span>
<span data-ttu-id="59a52-104">將您的 SQL 結構描述移轉至 SQL 資料倉儲的指引。</span><span class="sxs-lookup"><span data-stu-id="59a52-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="59a52-105">規劃結構描述移轉</span><span class="sxs-lookup"><span data-stu-id="59a52-105">Plan your schema migration</span></span>

<span data-ttu-id="59a52-106">規劃結構描述移轉時，請參閱[資料表概觀][table overview]以熟悉各種資料表設計考量，例如統計資料、發佈、分割及編製索引。</span><span class="sxs-lookup"><span data-stu-id="59a52-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="59a52-107">它也會列出一些[不支援的資料表功能][unsupported table features]和其因應措施。</span><span class="sxs-lookup"><span data-stu-id="59a52-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-to-consolidate-databases"></a><span data-ttu-id="59a52-108">使用使用者定義的結構描述來合併資料庫</span><span class="sxs-lookup"><span data-stu-id="59a52-108">Use user-defined schemas to consolidate databases</span></span>

<span data-ttu-id="59a52-109">您現有的工作負載可能有多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="59a52-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="59a52-110">例如，SQL Server 資料倉儲可能包含臨時資料庫、資料倉儲資料庫和某些資料超市資料庫。</span><span class="sxs-lookup"><span data-stu-id="59a52-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="59a52-111">在此拓撲中，每個資料庫都會搭配個別的安全性原則，以個別工作負載的形式執行。</span><span class="sxs-lookup"><span data-stu-id="59a52-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="59a52-112">相反地，SQL 資料倉儲會在某個資料庫中執行整個資料倉儲工作負載。</span><span class="sxs-lookup"><span data-stu-id="59a52-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="59a52-113">不允許跨資料庫聯結。</span><span class="sxs-lookup"><span data-stu-id="59a52-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="59a52-114">因此，SQL 資料倉儲預期由資料倉儲使用的所有資料表都會儲存在單一資料庫內。</span><span class="sxs-lookup"><span data-stu-id="59a52-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span></span>

<span data-ttu-id="59a52-115">建議您透過使用者定義的結構描述，將現有的工作負載合併成單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="59a52-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span></span> <span data-ttu-id="59a52-116">如需範例，請參閱[使用者定義的結構描述](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="59a52-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="59a52-117">使用相容的資料類型</span><span class="sxs-lookup"><span data-stu-id="59a52-117">Use compatible data types</span></span>
<span data-ttu-id="59a52-118">修改資料類型以與 SQL 資料倉儲相容。</span><span class="sxs-lookup"><span data-stu-id="59a52-118">Modify your data types to be compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="59a52-119">如需所有支援和不支援資料類型的清單，請參閱[資料類型][data types]。</span><span class="sxs-lookup"><span data-stu-id="59a52-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="59a52-120">該主題提供不支援類型的因應措施。</span><span class="sxs-lookup"><span data-stu-id="59a52-120">That topic gives workarounds for the unsupported types.</span></span> <span data-ttu-id="59a52-121">它也會提供查詢來識別 SQL 資料倉儲中不支援的現有類型。</span><span class="sxs-lookup"><span data-stu-id="59a52-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="59a52-122">將資料列大小最小化</span><span class="sxs-lookup"><span data-stu-id="59a52-122">Minimize row size</span></span>
<span data-ttu-id="59a52-123">若要達到最佳效能，請將資料表的資料列長度最小化。</span><span class="sxs-lookup"><span data-stu-id="59a52-123">For best performance, minimize the row length of your tables.</span></span> <span data-ttu-id="59a52-124">由於較短的資料列長度會有更好的效能，因此請使用適合您資料的最小資料類型。</span><span class="sxs-lookup"><span data-stu-id="59a52-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span></span> 

<span data-ttu-id="59a52-125">針對資料表的資料列寬度，PolyBase 具有 1 MB 的限制。</span><span class="sxs-lookup"><span data-stu-id="59a52-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="59a52-126">如果您打算使用 PolyBase 將資料載入 SQL 資料倉儲，請更新您的資料表以使最大資料列寬度小於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="59a52-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but the largest possible size of the row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and the defined row width is less than one MB. When loading rows, PolyBase allocates the full length of the variable-length data. The full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-the-distribution-option"></a><span data-ttu-id="59a52-127">指定發佈選項</span><span class="sxs-lookup"><span data-stu-id="59a52-127">Specify the distribution option</span></span>
<span data-ttu-id="59a52-128">SQL 資料倉儲是一種分散式資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="59a52-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="59a52-129">每個資料表都會分散或複寫至多個計算節點。</span><span class="sxs-lookup"><span data-stu-id="59a52-129">Each table is distributed or replicated across the Compute nodes.</span></span> <span data-ttu-id="59a52-130">有一個資料表選項，可讓您指定散發資料的方式。</span><span class="sxs-lookup"><span data-stu-id="59a52-130">There's a table option that lets you specify how to distribute the data.</span></span> <span data-ttu-id="59a52-131">選擇包括循環配置資源、複寫或雜湊分散。</span><span class="sxs-lookup"><span data-stu-id="59a52-131">The choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="59a52-132">各有其優缺點。</span><span class="sxs-lookup"><span data-stu-id="59a52-132">Each has pros and cons.</span></span> <span data-ttu-id="59a52-133">如果您未指定發佈選項，SQL 資料倉儲預設會使用循環配置資源。</span><span class="sxs-lookup"><span data-stu-id="59a52-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span></span>

- <span data-ttu-id="59a52-134">預設值為循環配置資源。</span><span class="sxs-lookup"><span data-stu-id="59a52-134">Round-robin is the default.</span></span> <span data-ttu-id="59a52-135">它的使用方式很簡單，並能以最快的速度載入資料，但聯結作業將會需要移動資料，因而會使查詢效能變慢。</span><span class="sxs-lookup"><span data-stu-id="59a52-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="59a52-136">複寫會在每個計算節點上儲存資料表的複本。</span><span class="sxs-lookup"><span data-stu-id="59a52-136">Replicated stores a copy of the table on each Compute node.</span></span> <span data-ttu-id="59a52-137">由於複寫資料表的聯結和彙總作業並不需要移動資料，所以很有效率。</span><span class="sxs-lookup"><span data-stu-id="59a52-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="59a52-138">相對的，它們需要額外的儲存體，因此比較適合較小的資料表使用。</span><span class="sxs-lookup"><span data-stu-id="59a52-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="59a52-139">雜湊分散會透過雜湊函式將資料列散發至所有節點上。</span><span class="sxs-lookup"><span data-stu-id="59a52-139">Hash distributed distributes the rows across all the nodes via a hash function.</span></span> <span data-ttu-id="59a52-140">雜湊分散式資料表是 SQL 資料倉儲的核心，因為它們是針對在大型資料表上提供高度的查詢效能所設計。</span><span class="sxs-lookup"><span data-stu-id="59a52-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span></span> <span data-ttu-id="59a52-141">此選項需要稍加規劃，以選出最適合在其上方散發資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="59a52-141">This option requires some planning to select the best column on which to distribute the data.</span></span> <span data-ttu-id="59a52-142">不過，如果一開始並沒有選擇最適合的資料行，您可以輕鬆地在不同的資料行上重新散發資料。</span><span class="sxs-lookup"><span data-stu-id="59a52-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span></span> 

<span data-ttu-id="59a52-143">若要針對每個資料表選擇最佳發佈選項，請參閱[分散式資料表](sql-data-warehouse-tables-distribute.md)。</span><span class="sxs-lookup"><span data-stu-id="59a52-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="59a52-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59a52-144">Next steps</span></span>
<span data-ttu-id="59a52-145">將資料庫結構描述成功移轉到「SQL 資料倉儲」之後，您就可以繼續閱讀下列其中一篇文章：</span><span class="sxs-lookup"><span data-stu-id="59a52-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="59a52-146">[移轉資料][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="59a52-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="59a52-147">[移轉程式碼][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="59a52-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="59a52-148">若要深入了解 SQL 資料倉儲最佳做法，請參閱[最佳做法][best practices]一文。</span><span class="sxs-lookup"><span data-stu-id="59a52-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

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
