---
title: "SQL 資料倉儲中的資料表上的 aaaManaging 統計資料 |Microsoft 文件"
description: "開始使用 Azure SQL 資料倉儲中的資料表的統計資料。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="fdb3c-103">管理 SQL 資料倉儲中的資料表的統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="fdb3c-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="fdb3c-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="fdb3c-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="fdb3c-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-107">[Index][Index]</span></span>
> * <span data-ttu-id="fdb3c-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="fdb3c-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="fdb3c-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="fdb3c-111">hello 詳細的 SQL 資料倉儲知道您的資料，hello 速度它可以針對執行查詢您的資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="fdb3c-112">SQL 資料倉儲告訴您資料的 hello 方式就是收集資料的相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="fdb3c-113">在您的資料具有統計資料是其中一個 hello 最重要的是您可以執行 toooptimize 您的查詢。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="fdb3c-114">統計資料可協助建立 hello 最佳查詢計劃的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="fdb3c-115">這是因為 hello SQL 資料倉儲查詢最佳化工具是以成本為基礎最佳化工具。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="fdb3c-116">也就是說，它會比較 hello 成本的各種查詢計劃，並再選擇 hello 計劃與 hello 最低成本，也應該將執行 hello 最快的 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="fdb3c-117">您可以根據單一資料行、多個資料行或資料表的索引來建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="fdb3c-118">統計資料會儲存在長條圖，這會擷取 hello 範圍和選擇性的值。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="fdb3c-119">時，這特別感興趣的 hello 最佳化工具需要 tooevaluate 聯結、 GROUP BY、 HAVING 和 WHERE 子句，在查詢中的。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="fdb3c-120">例如，如果 hello 最佳化工具估計，您要篩選查詢中的 hello 日期將會傳回 1 個資料列，它可能會選擇非常不同計劃比如果它評估這些日期您已選取會傳回 1 百萬個資料列。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="fdb3c-121">建立統計資料是相當重要，同樣很重要的統計資料*精確地*反映 hello hello 資料表目前狀態。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="fdb3c-122">具有最新的統計資料，可確保好的計畫 hello 最佳化工具所選取。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="fdb3c-123">hello 最佳化工具所建立的 hello 計劃，才適合您資料的 hello 統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="fdb3c-124">hello 的建立和更新統計資料的程序目前是手動程序，但 toodo 的非常簡單。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="fdb3c-125">這不同於 SQL Server 根據單一資料行和索引來自動建立和更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="fdb3c-126">使用下列的 hello 資訊，您可以大幅自動化 hello hello 統計資料的管理對您的資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="fdb3c-127">開始使用統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-127">Getting started with statistics</span></span>
 <span data-ttu-id="fdb3c-128">每個資料行上建立取樣的統計資料是簡單的方式 tooget 入門統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="fdb3c-129">保守的作法是同樣重要 tookeep 統計資料保持最新狀態，因為可能會 tooupdate 統計資料每日或每次載入之後。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="fdb3c-130">總是會有效能與 hello 成本 toocreate 和更新統計資料之間的取捨。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="fdb3c-131">如果您發現所需花費太長 toomaintain 所有統計資料，您可能想 tootry toobe 更具選擇性有關哪些資料行具有統計資料或資料行需要頻繁的更新。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="fdb3c-132">比方說，您可能會想 tooupdate 日期資料行，每日，可能會加入新的值而不是每個載入之後。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="fdb3c-133">同樣地，您將可以 hello 最大效益，具有統計資料中的資料行所涉及聯結、 GROUP BY、 HAVING 和 WHERE 子句。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="fdb3c-134">如果您有大量的資料表 hello 中只使用資料行的 SELECT 子句、 這些資料行統計資料可能無法幫助，並花一些更多的精力 tooidentify 只有 hello 資料行，其中的統計資料會幫助，可以降低 hello 時間 toomaintain 統計資料.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="fdb3c-135">多重資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-135">Multi-column statistics</span></span>
<span data-ttu-id="fdb3c-136">除了針對單一資料行 toocreating 統計資料，您可能會發現，您的查詢將受益於多個資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="fdb3c-137">多重資料行統計資料是對一份資料行清單建立的統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="fdb3c-138">它們包含在 hello 清單中的 hello 第一個資料行的單一資料行統計資料加上一些跨資料行相互關聯資訊呼叫密度。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="fdb3c-139">例如，如果您有兩個資料行聯結 tooanother 的資料表，您可能會發現 SQL 資料倉儲能夠更為最佳化 hello 計劃是否其了解 hello 兩個資料行之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="fdb3c-140">多重資料行統計資料可以改善某些作業 (例如複合聯結和分組分式) 的查詢效能。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="fdb3c-141">更新統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-141">Updating statistics</span></span>
<span data-ttu-id="fdb3c-142">在資料庫管理例行工作中，更新統計資料很重要。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="fdb3c-143">當 hello 發佈 hello 資料庫中的資料變更時，統計資料需要 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="fdb3c-144">過期的統計資料會導致 toosub 達到最佳查詢效能。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="fdb3c-145">加入新的日期時，一個最佳作法將是 tooupdate 日期資料行統計資料每一天。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="fdb3c-146">每次新的資料列載入至 hello 資料倉儲，新負載交易日期或加入。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="fdb3c-147">這些變更 hello 資料發佈，以進行 hello 統計資料已過時。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="fdb3c-148">相反地，customer 資料表中的國家/地區資料行的統計資料可能永遠不需要 toobe 更新，因為通常不會變更 hello 值分佈。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="fdb3c-149">假設 hello 發佈常數的客戶，加入新的資料列 toohello 資料表變數不會為 toochange hello 資料分佈。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="fdb3c-150">不過，如果您的資料倉儲只包含一個國家/地區，並從新的國家/地區匯入資料，導致資料從多個國家 （地區） 儲存，然後您確實需要 tooupdate hello 國家/地區資料行的統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="fdb3c-151">其中一個 hello 第一個問題 tooask 當疑難排解查詢時，「 是 hello 統計資料保持最新狀態？ 」</span><span class="sxs-lookup"><span data-stu-id="fdb3c-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="fdb3c-152">這個問題的答案不是其中 hello 資料的 hello 存留期可以回答。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="fdb3c-153">最新的 toodate 統計資料物件可能已基礎資料沒有變更材料 toohello 的非常舊。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="fdb3c-154">當 hello 的資料列的數目已大幅變更，或者沒有 hello 特定資料行的值分佈的材料變更*然後*是時間 tooupdate 統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="fdb3c-155">如需參考， **SQL Server** (非 SQL 資料倉儲) 會針對下列情況自動更新統計資料：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="fdb3c-156">如果有零個資料列在 hello 資料表中，當您將加入資料列，就會自動更新統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="fdb3c-157">當您將加入開頭為少於 500 個資料列超過 500 個資料列 tooa 資料表 （例如在開始您有 499 然後再新增 500 列 tooa 共 999 個資料列），就會自動更新</span><span class="sxs-lookup"><span data-stu-id="fdb3c-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="fdb3c-158">一旦您已超過 500 個資料列就 tooadd 500 個其他資料列 + hello hello 資料表大小的 20%之前，您會看到 自動更新在 hello 統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="fdb3c-159">因為沒有任何 DMV toodetermine 如果自從 hello 時間統計資料上次更新 hello 資料表中的資料已經變更，了解 hello 存留期統計資料可以提供您與 hello 圖片的一部分。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="fdb3c-160">您可以使用下列查詢 toodetermine hello 上次統計資料的 hello 其中每個資料表上更新。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="fdb3c-161">請記住，是否沒有 hello 特定資料行的值分佈的實質性變更，您應該更新統計資料，不論 hello 它們已更新的上次。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

<span data-ttu-id="fdb3c-162">例如，資料倉儲中的日期資料行通常需要經常更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="fdb3c-163">每次新的資料列載入至 hello 資料倉儲，新負載交易日期或加入。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="fdb3c-164">這些變更 hello 資料發佈，以進行 hello 統計資料已過時。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="fdb3c-165">相反地，在 customer 資料表在性別資料行的統計資料可能永遠不需要 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="fdb3c-166">假設 hello 發佈常數的客戶，加入新的資料列 toohello 資料表變數不會為 toochange hello 資料分佈。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="fdb3c-167">不過，如果您的資料倉儲僅包含一個性別和新的需求結果，在多個性別明確先然後 tooupdate hello 性別資料行的統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="fdb3c-168">如需進一步說明，請參閱 MSDN 上的[統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="fdb3c-169">實作統計資料管理</span><span class="sxs-lookup"><span data-stu-id="fdb3c-169">Implementing statistics management</span></span>
<span data-ttu-id="fdb3c-170">它通常是個不錯的主意 tooextend 資料載入會在更新統計資料的程序 tooensure hello hello 載入結束。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="fdb3c-171">hello 資料載入時，資料表經常會變更其大小和/或其值的分佈。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="fdb3c-172">因此，這是邏輯上 tooimplement 某些管理處理程序。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="fdb3c-173">有些指導原則如下所示為 hello 載入程序期間更新統計資料：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="fdb3c-174">確保每個載入的資料表至少都更新一個統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="fdb3c-175">此更新 hello hello 統計資料更新的大小 （資料列計數與頁面計數） 資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="fdb3c-176">將焦點放在參與 JOIN、GROUP BY、ORDER BY 和 DISTINCT 子句的資料行。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="fdb3c-177">請考慮更新 「 遞增索引鍵 」 的交易之類的資料行日期將不會在 hello 統計資料長條圖中包含這些值更頻繁。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="fdb3c-178">考慮較不常更新靜態散發資料行。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="fdb3c-179">請記得，每個統計資料物件會依序更新。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="fdb3c-180">僅只實作 `UPDATE STATISTICS <TABLE_NAME>` 可能不太理想 - 尤其是對具有許多統計資料物件的寬型資料表而言。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="fdb3c-181">如需詳細資訊 [遞增索引鍵] 請參閱 SQL Server 2014 toohello 基數估計模型技術白皮書。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="fdb3c-182">如需進一步說明，請參閱 MSDN 上的[基數估計][Cardinality Estimation]。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="fdb3c-183">範例：建立統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-183">Examples: Create statistics</span></span>
<span data-ttu-id="fdb3c-184">下列範例將示範如何 toouse 建立統計資料的各種選項。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="fdb3c-185">您使用每個資料行的 hello 選項取決於資料的 hello 特性以及 hello 資料行在查詢中的使用方式。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="fdb3c-186">A.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-186">A.</span></span> <span data-ttu-id="fdb3c-187">使用預設選項建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="fdb3c-188">toocreate 統計資料資料行，只要提供 hello 統計資料物件的名稱與 hello hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="fdb3c-189">此語法會使用所有 hello 預設選項。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="fdb3c-190">根據預設，SQL 資料倉儲取樣 20%的 hello 資料表建立統計資料時。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="fdb3c-191">例如：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="fdb3c-192">B.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-192">B.</span></span> <span data-ttu-id="fdb3c-193">檢查每個資料列以建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="fdb3c-194">hello 預設的 20%的取樣率已足以應付大多數情況。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="fdb3c-195">不過，您可以調整 hello 取樣率。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="fdb3c-196">toosample hello 完整資料表中，使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="fdb3c-197">例如：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="fdb3c-198">C.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-198">C.</span></span> <span data-ttu-id="fdb3c-199">藉由指定 hello 取樣大小建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="fdb3c-200">或者，您可以指定 hello 取樣大小，以百分比表示：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="fdb3c-201">D.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-201">D.</span></span> <span data-ttu-id="fdb3c-202">建立只對某些 hello 資料列的單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="fdb3c-203">另一個選項，您可以建立統計資料部分 hello 資料列在資料表中。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="fdb3c-204">這稱為篩選的統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="fdb3c-205">比方說，您可以使用篩選的統計資料，當您計劃 tooquery 大型的資料分割資料表的特定分割區。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="fdb3c-206">藉由只 hello 上磁碟分割值建立統計資料，hello hello 統計資料的精確度會改善，並因而改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="fdb3c-207">這個範例會建立某個值範圍的統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="fdb3c-208">hello 值就可以輕鬆在定義資料分割中 toomatch hello 範圍的值。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="fdb3c-209">Hello 查詢最佳化工具 tooconsider 使用篩選的統計資料，則會選擇 hello 分散式的查詢計劃時，針對 hello 查詢必須配合 hello hello 統計資料物件定義。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="fdb3c-210">使用 hello 上述範例中，hello 查詢子句中需要 2000101 之間 20001231 toospecify col1 值。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="fdb3c-211">E.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-211">E.</span></span> <span data-ttu-id="fdb3c-212">與所有 hello 選項建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="fdb3c-213">您當然可以一起結合 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="fdb3c-214">下列的 hello 範例會建立篩選的統計資料物件，以自訂的取樣大小：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="fdb3c-215">如需 hello 完整參考，請參閱[CREATE STATISTICS] [ CREATE STATISTICS] MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="fdb3c-216">F.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-216">F.</span></span> <span data-ttu-id="fdb3c-217">建立多重資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-217">Create multi-column statistics</span></span>
<span data-ttu-id="fdb3c-218">toocreate 多重資料行的統計資料，只需使用 hello 上述範例中，但指定多個資料行。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="fdb3c-219">hello 長條圖，會使用 tooestimate hello 查詢結果中的資料列數只適用於 hello hello 統計資料物件定義中所列的第一個資料行。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="fdb3c-220">在此範例中，hello 長條圖位於*產品\_類別*。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="fdb3c-221">跨資料行統計資料會依據 product\_category 和 product\_sub_c\ategory 計算：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="fdb3c-222">因為沒有之間的相互關聯*產品\_類別*和*產品\_sub\_類別*，多重資料行狀態就非常適合在存取這些資料行在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="fdb3c-223">G.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-223">G.</span></span> <span data-ttu-id="fdb3c-224">在資料表中的所有 hello 資料行上建立統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="fdb3c-225">其中一種方式 toocreate 統計資料，則 tooissues CREATE STATISTICS 命令建立 hello 表格之後。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="fdb3c-226">H.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-226">H.</span></span> <span data-ttu-id="fdb3c-227">資料庫中的所有資料行上使用預存程序 toocreate 統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="fdb3c-228">SQL 資料倉儲不太需要系統預存程序對等項目 [SQL Server 中的 [sp_create_stats]]。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="fdb3c-229">這個預存程序上還沒有統計資料的 hello 資料庫的每個資料行建立單一資料行統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="fdb3c-230">這會協助您開始進行資料庫設計。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-230">This will help you get started with your database design.</span></span> <span data-ttu-id="fdb3c-231">感覺可用 tooadapt 它 tooyour 需要。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-231">Feel free tooadapt it tooyour needs.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

<span data-ttu-id="fdb3c-232">toocreate hello 這個程序中，資料表中的所有資料行的統計資料，只需呼叫 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="fdb3c-233">範例：更新統計資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-233">Examples: update statistics</span></span>
<span data-ttu-id="fdb3c-234">tooupdate 統計資料，您可以：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="fdb3c-235">更新一個統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-235">Update one statistics object.</span></span> <span data-ttu-id="fdb3c-236">指定統計資料物件想 tooupdate hello hello 的名稱。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="fdb3c-237">更新資料表上的所有統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="fdb3c-238">指定 hello hello 資料表，而不是一個特定的統計資料物件名稱。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="fdb3c-239">A.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-239">A.</span></span> <span data-ttu-id="fdb3c-240">更新一個特定統計資料物件</span><span class="sxs-lookup"><span data-stu-id="fdb3c-240">Update one specific statistics object</span></span>
<span data-ttu-id="fdb3c-241">使用下列語法 tooupdate 特定統計資料物件的 hello:</span><span class="sxs-lookup"><span data-stu-id="fdb3c-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="fdb3c-242">例如：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="fdb3c-243">藉由更新特定統計資料物件，您可以減少 hello 時間和資源所需的 toomanage 統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="fdb3c-244">這需要一些以為，不過，toochoose hello 最佳統計資料物件 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="fdb3c-245">B.</span><span class="sxs-lookup"><span data-stu-id="fdb3c-245">B.</span></span> <span data-ttu-id="fdb3c-246">更新資料表上的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-246">Update all statistics on a table</span></span>
<span data-ttu-id="fdb3c-247">這會顯示更新的資料表上的所有 hello 統計資料物件的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="fdb3c-248">例如：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="fdb3c-249">此陳述式很容易 toouse。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-249">This statement is easy toouse.</span></span> <span data-ttu-id="fdb3c-250">請記得這更新 hello 資料表上的所有統計資料，因此可能會執行比所需的更多工作。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="fdb3c-251">如果 hello 效能不是問題，這絕對是 hello 最簡單且最完整的方式 tooguarantee 統計資料處於最新狀態。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="fdb3c-252">在更新的資料表上的所有統計資料時，SQL 資料倉儲會掃描 toosample hello 資料表的每個統計資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="fdb3c-253">如果 hello 資料表很大，具有多資料行，以及許多統計資料，可能會更有效率 tooupdate 個別統計資料根據需求。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="fdb3c-254">實作`UPDATE STATISTICS`程序，請參閱 hello[暫存資料表][ Temporary]發行項。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="fdb3c-255">hello 實作方法是稍有不同的 toohello`CREATE STATISTICS`上述的程序，但 hello 最終結果是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="fdb3c-256">如需 hello 完整語法，請參閱[Update Statistics] [ Update Statistics] MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="fdb3c-257">統計資料中繼資料</span><span class="sxs-lookup"><span data-stu-id="fdb3c-257">Statistics metadata</span></span>
<span data-ttu-id="fdb3c-258">有數個系統檢視和函數，您可以使用 toofind 統計的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="fdb3c-259">例如，您可以看到是否統計資料物件可能已過期時最後建立或更新統計資料，請使用 hello stats 日期函式 toosee。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="fdb3c-260">統計資料的目錄檢視</span><span class="sxs-lookup"><span data-stu-id="fdb3c-260">Catalog views for statistics</span></span>
<span data-ttu-id="fdb3c-261">這些系統檢視提供統計資料的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="fdb3c-262">目錄檢視</span><span class="sxs-lookup"><span data-stu-id="fdb3c-262">Catalog View</span></span> | <span data-ttu-id="fdb3c-263">說明</span><span class="sxs-lookup"><span data-stu-id="fdb3c-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fdb3c-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="fdb3c-265">每個資料行有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-265">One row for each column.</span></span> |
| <span data-ttu-id="fdb3c-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="fdb3c-267">Hello 資料庫中每個物件的一個資料列。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="fdb3c-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="fdb3c-269">每個結構描述 hello 資料庫中的一個資料列。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="fdb3c-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="fdb3c-271">每個統計資料物件有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="fdb3c-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="fdb3c-273">Hello 統計資料物件中每個資料行的一個資料列。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="fdb3c-274">連結回 toosys.columns。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="fdb3c-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="fdb3c-276">每個資料表 (包括外部資料表) 有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="fdb3c-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="fdb3c-278">每個資料類型有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="fdb3c-279">統計資料的系統函式</span><span class="sxs-lookup"><span data-stu-id="fdb3c-279">System functions for statistics</span></span>
<span data-ttu-id="fdb3c-280">這些系統函式很適合用於處理統計資料：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="fdb3c-281">系統函式</span><span class="sxs-lookup"><span data-stu-id="fdb3c-281">System Function</span></span> | <span data-ttu-id="fdb3c-282">說明</span><span class="sxs-lookup"><span data-stu-id="fdb3c-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fdb3c-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="fdb3c-284">上次更新日期 hello 統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="fdb3c-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="fdb3c-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="fdb3c-286">Hello 統計資料物件所了解，請提供有關值分佈 hello 的摘要層級及詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="fdb3c-287">將統計資料資料行和函式結合成一個檢視</span><span class="sxs-lookup"><span data-stu-id="fdb3c-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="fdb3c-288">此檢視會一起從 hello [STATS_DATE()] [] 函式與 toostatistics 和結果的資料行。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="fdb3c-289">DBCC SHOW_STATISTICS() 範例</span><span class="sxs-lookup"><span data-stu-id="fdb3c-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="fdb3c-290">DBCC SHOW_STATISTICS() 顯示儲存統計資料物件中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="fdb3c-291">此資料來自三個部分。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="fdb3c-292">標頭</span><span class="sxs-lookup"><span data-stu-id="fdb3c-292">Header</span></span>
2. <span data-ttu-id="fdb3c-293">密度向量</span><span class="sxs-lookup"><span data-stu-id="fdb3c-293">Density Vector</span></span>
3. <span data-ttu-id="fdb3c-294">長條圖</span><span class="sxs-lookup"><span data-stu-id="fdb3c-294">Histogram</span></span>

<span data-ttu-id="fdb3c-295">hello hello 統計資料的相關標頭中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="fdb3c-296">hello 長條圖會顯示 hello 散發值 hello 第一個索引鍵資料行中的 hello 統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="fdb3c-297">hello 密度向量來測量跨資料行相互關聯。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="fdb3c-298">SQLDW 計算與任何 hello 統計資料物件中的 hello 資料的基數估計值。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="fdb3c-299">顯示標頭、密度和長條圖</span><span class="sxs-lookup"><span data-stu-id="fdb3c-299">Show header, density, and histogram</span></span>
<span data-ttu-id="fdb3c-300">這個簡單範例顯示統計資料物件的所有三個部分。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="fdb3c-301">例如：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="fdb3c-302">顯示 DBCC SHOW_STATISTICS(); 的一或多個部分</span><span class="sxs-lookup"><span data-stu-id="fdb3c-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="fdb3c-303">如果您只想要檢視特定部分，請使用 hello`WITH`子句，並指定哪些部分您想 toosee:</span><span class="sxs-lookup"><span data-stu-id="fdb3c-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="fdb3c-304">例如：</span><span class="sxs-lookup"><span data-stu-id="fdb3c-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="fdb3c-305">DBCC SHOW_STATISTICS() 差異</span><span class="sxs-lookup"><span data-stu-id="fdb3c-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="fdb3c-306">DBCC SHOW_STATISTICS() 更嚴格地是比較 SQL 資料倉儲 tooSQL 伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="fdb3c-307">不支援未記載的功能</span><span class="sxs-lookup"><span data-stu-id="fdb3c-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="fdb3c-308">無法使用 Stats_stream</span><span class="sxs-lookup"><span data-stu-id="fdb3c-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="fdb3c-309">無法聯結特定統計資料子集的結果，例如 (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="fdb3c-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="fdb3c-310">無法針對訊息隱藏項目設定 NO_INFOMSGS</span><span class="sxs-lookup"><span data-stu-id="fdb3c-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="fdb3c-311">無法使用統計資料名稱前後的方括號</span><span class="sxs-lookup"><span data-stu-id="fdb3c-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="fdb3c-312">無法使用資料行名稱 tooidentify 統計資料物件</span><span class="sxs-lookup"><span data-stu-id="fdb3c-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="fdb3c-313">不支援自訂錯誤 2767</span><span class="sxs-lookup"><span data-stu-id="fdb3c-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdb3c-314">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fdb3c-314">Next steps</span></span>
<span data-ttu-id="fdb3c-315">如需詳細資訊，請參閱 MSDN 上的 [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="fdb3c-316">toolearn 詳細資訊，請參閱 hello 文件上[資料表概觀][Overview]，[資料表資料類型][Data Types]，[散發資料表][ Distribute]，[的資料表建立索引][Index]，[分割資料表][ Partition]和[暫存資料表][Temporary]。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="fdb3c-317">若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="fdb3c-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
