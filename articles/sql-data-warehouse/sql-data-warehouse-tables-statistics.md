---
title: "管理 SQL 資料倉儲中的資料表的統計資料 | Microsoft Docs"
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
ms.openlocfilehash: 1d5ded69e394643ddfc3de0c6d30dbd30c8e848f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="38d78-103">管理 SQL 資料倉儲中的資料表的統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="38d78-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="38d78-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="38d78-105">[資料類型][Data Types]</span><span class="sxs-lookup"><span data-stu-id="38d78-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="38d78-106">[散發][Distribute]</span><span class="sxs-lookup"><span data-stu-id="38d78-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="38d78-107">[索引][Index]</span><span class="sxs-lookup"><span data-stu-id="38d78-107">[Index][Index]</span></span>
> * <span data-ttu-id="38d78-108">[資料分割][Partition]</span><span class="sxs-lookup"><span data-stu-id="38d78-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="38d78-109">[統計資料][Statistics]</span><span class="sxs-lookup"><span data-stu-id="38d78-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="38d78-110">[暫存][Temporary]</span><span class="sxs-lookup"><span data-stu-id="38d78-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="38d78-111">SQL 資料倉儲越了解您的資料，查詢資料的速度就越快。</span><span class="sxs-lookup"><span data-stu-id="38d78-111">The more SQL Data Warehouse knows about your data, the faster it can execute queries against your data.</span></span>  <span data-ttu-id="38d78-112">您藉由收集資料的統計資料，讓 SQL 資料倉儲了解您的資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-112">The way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="38d78-113">從資料中取得統計資料是將查詢最佳化最重要的工作之一。</span><span class="sxs-lookup"><span data-stu-id="38d78-113">Having statistics on your data is one of the most important things you can do to optimize your queries.</span></span>  <span data-ttu-id="38d78-114">統計資料可協助 SQL 資料倉儲為您的查詢建立最佳計畫。</span><span class="sxs-lookup"><span data-stu-id="38d78-114">Statistics help SQL Data Warehouse create the most optimal plan for your queries.</span></span>  <span data-ttu-id="38d78-115">這是因為 SQL 資料倉儲查詢最佳化工具是一種以成本為考量的最佳化工具。</span><span class="sxs-lookup"><span data-stu-id="38d78-115">This is because the SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="38d78-116">也就是說，它會比較各種查詢計畫的成本，然後選擇成本最低的計畫，也就是執行速度最快的計畫。</span><span class="sxs-lookup"><span data-stu-id="38d78-116">That is, it compares the cost of various query plans and then chooses the plan with the lowest cost, which should also be the plan that will execute the fastest.</span></span>

<span data-ttu-id="38d78-117">您可以根據單一資料行、多個資料行或資料表的索引來建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="38d78-118">統計資料儲存在長條圖中，可擷取值的範圍和選擇性。</span><span class="sxs-lookup"><span data-stu-id="38d78-118">Statistics are stored in a histogram which captures the range and selectivity of values.</span></span>  <span data-ttu-id="38d78-119">當最佳化工具需要評估查詢中的 JOIN、GROUP BY、HAVING 和 WHERE 子句時，這是特別有用。</span><span class="sxs-lookup"><span data-stu-id="38d78-119">This is of particular interest when the optimizer needs to evaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="38d78-120">例如，如果最佳化工具估計您在查詢中篩選的日期會傳回 1 個資料列，一旦它估計您選取的日期會傳回 1 百萬個資料列，它可能會選擇非常不同的計畫。</span><span class="sxs-lookup"><span data-stu-id="38d78-120">For example, if the optimizer estimates that the date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="38d78-121">建立統計資料非常重要，同樣重要的是統計資料要能「準確」  反映資料表的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="38d78-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect the current state of the table.</span></span>  <span data-ttu-id="38d78-122">取得最新統計資料可確保最佳化工具選取良好的計畫。</span><span class="sxs-lookup"><span data-stu-id="38d78-122">Having up-to-date statistics ensures that a good plan is selected by the optimizer.</span></span>  <span data-ttu-id="38d78-123">最佳化工具建立的計畫是否良好，完全取決於資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-123">The plans created by the optimizer are only as good as the statistics on your data.</span></span>

<span data-ttu-id="38d78-124">建立和更新統計資料的程序目前是手動程序，但做起來很簡單。</span><span class="sxs-lookup"><span data-stu-id="38d78-124">The process of creating and updating statistics is currently a manual process, but is very simple to do.</span></span>  <span data-ttu-id="38d78-125">這不同於 SQL Server 根據單一資料行和索引來自動建立和更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="38d78-126">下列資訊可讓您在管理資料的統計資料時，發揮更高的自動化程度。</span><span class="sxs-lookup"><span data-stu-id="38d78-126">By using the information below, you can greatly automate the management of the statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="38d78-127">開始使用統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-127">Getting started with statistics</span></span>
 <span data-ttu-id="38d78-128">建立每個資料行的範本統計資料是開始使用統計資料的簡單方式。</span><span class="sxs-lookup"><span data-stu-id="38d78-128">Creating sampled statistics on every column is an easy way to get started with statistics.</span></span>  <span data-ttu-id="38d78-129">因為隨時更新統計資料也同樣重要，保守的作法可能是每天或每次載入之後更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-129">Since it is equally important to keep statistics up-to-date, a conservative approach may be to update your statistics daily or after each load.</span></span> <span data-ttu-id="38d78-130">建立和更新統計資料的效能與成本之間總有一些取捨。</span><span class="sxs-lookup"><span data-stu-id="38d78-130">There are always trade-offs between performance and the cost to create and update statistics.</span></span>  <span data-ttu-id="38d78-131">如果您發現維護所有統計資料所需時間太長，可能要更謹慎選擇哪些資料行要加以統計資料、哪些資料行需要頻繁更新。</span><span class="sxs-lookup"><span data-stu-id="38d78-131">If you find it is taking too long to maintain all of your statistics, you may want to try to be more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="38d78-132">例如，由於可能有新的值加入，您可能想要每天更新日期資料行，而不是在每次載入之後才更新。</span><span class="sxs-lookup"><span data-stu-id="38d78-132">For example, you might want to update date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="38d78-133">同樣地，根據涉入 JOIN、GROUP BY、HAVING 和 WHERE 子句的資料行建立統計資料，將可享受最大的好處。</span><span class="sxs-lookup"><span data-stu-id="38d78-133">Again, you will gain the most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="38d78-134">如果資料表有許多資料行，但都只用在 SELECT 子句中，則這些資料行的統計資料沒有多大幫助，多花一些心思找出統計資料有所幫助的資料行，將可縮短統計資料的維護時間。</span><span class="sxs-lookup"><span data-stu-id="38d78-134">If you have a table with a lot of columns which are only used in the SELECT clause, statistics on these columns may not help, and spending a little more effort to identify only the columns where statistics will help, can reduce the time to maintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="38d78-135">多重資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-135">Multi-column statistics</span></span>
<span data-ttu-id="38d78-136">除了根據單一資料行建立統計資料，您可能會發現查詢也能受益於多重資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-136">In addition to creating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="38d78-137">多重資料行統計資料是對一份資料行清單建立的統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="38d78-138">其中包含清單中第一個資料行的單一資料行統計資料，再加上一些跨資料行關聯性資訊 (稱為密度)。</span><span class="sxs-lookup"><span data-stu-id="38d78-138">They include single column statistics on the first column in the list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="38d78-139">例如，如果一個資料表根據兩個資料行而聯結另一個資料表，您可能會發現只要 SQL 資料倉儲了解兩個資料行之間的關聯性，就可以進一步最佳化計畫。</span><span class="sxs-lookup"><span data-stu-id="38d78-139">For example, if you have a table that joins to another on two columns, you may find that SQL Data Warehouse can better optimize the plan if it understands the relationship between two columns.</span></span>   <span data-ttu-id="38d78-140">多重資料行統計資料可以改善某些作業 (例如複合聯結和分組分式) 的查詢效能。</span><span class="sxs-lookup"><span data-stu-id="38d78-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="38d78-141">更新統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-141">Updating statistics</span></span>
<span data-ttu-id="38d78-142">在資料庫管理例行工作中，更新統計資料很重要。</span><span class="sxs-lookup"><span data-stu-id="38d78-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="38d78-143">資料庫中的資料散發情況改變時，就需要更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-143">When the distribution of data in the database changes, statistics need to be updated.</span></span>  <span data-ttu-id="38d78-144">過期的統計資料將會導致查詢效能欠佳。</span><span class="sxs-lookup"><span data-stu-id="38d78-144">Out-of-date statistics will lead to sub-optimal query performance.</span></span>

<span data-ttu-id="38d78-145">其中一個最佳做法，是隨著新增新的日期，每天在日期資料行上更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-145">One best practice is to update statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="38d78-146">每次有新資料列載入資料倉儲時，就會加入新的載入日期或交易日期。</span><span class="sxs-lookup"><span data-stu-id="38d78-146">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="38d78-147">這些會改變資料散發情況並使統計資料過時。</span><span class="sxs-lookup"><span data-stu-id="38d78-147">These change the data distribution and make the statistics out-of-date.</span></span> <span data-ttu-id="38d78-148">相反地，客戶資料表中國家/地區資料行上的統計資料，可能永遠不需要更新，因為值散發通常不會變更。</span><span class="sxs-lookup"><span data-stu-id="38d78-148">Conversely, statistics on a country column in a customer table might never need to be updated, as the distribution of values doesn’t generally change.</span></span> <span data-ttu-id="38d78-149">假設客戶間的散發固定不變，將新資料列加入至資料表變化並不會改變資料散發情況。</span><span class="sxs-lookup"><span data-stu-id="38d78-149">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="38d78-150">不過，如果您的資料倉儲原本只包含單一國家/地區，而您又帶入來自新國家/地區的資料，並導致資料倉儲儲存了來自多個國家/地區的資料，您便必須更新國家/地區資料行上的統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need to update statistics on the country column.</span></span>

<span data-ttu-id="38d78-151">進行查詢疑難排解時，首先要詢問的問題之一就是「統計資料是最新的嗎？」</span><span class="sxs-lookup"><span data-stu-id="38d78-151">One of the first questions to ask when troubleshooting a query is, "Are the statistics up-to-date?"</span></span>

<span data-ttu-id="38d78-152">這個問題不是可依資料年齡回答的問題。</span><span class="sxs-lookup"><span data-stu-id="38d78-152">This question is not one that can be answered by the age of the data.</span></span> <span data-ttu-id="38d78-153">如果基礎資料並沒有任何實質變更，最新的統計資料物件可能會非常舊。</span><span class="sxs-lookup"><span data-stu-id="38d78-153">An up to date statistics object could be very old if there's been no material change to the underlying data.</span></span> <span data-ttu-id="38d78-154">當資料列數目已顯著變更，或特定資料行的值散發有實質變更時，就  應該更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-154">When the number of rows has changed substantially or there is a material change in the distribution of values for a given column *then* it's time to update statistics.</span></span>  

<span data-ttu-id="38d78-155">如需參考， **SQL Server** (非 SQL 資料倉儲) 會針對下列情況自動更新統計資料：</span><span class="sxs-lookup"><span data-stu-id="38d78-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="38d78-156">如果您的資料表中有零個資料列，當您新增資料列時，系統便會自動更新統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-156">If you have zero rows in the table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="38d78-157">當您將超過 500 個資料列新增到原本擁有少於 500 個資料列的資料表時 (例如，您一開始擁有 499 個資料列，然後新增 500 個資料列，變成一共有 999 個資料列)，系統便會自動更新統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-157">When you add more than 500 rows to a table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows to a total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="38d78-158">當您擁有超過 500 個資料列之後，您必須新增 500 個資料列 + 數目為資料表大小 20% 的額外資料列，系統才會針對統計資料進行自動更新</span><span class="sxs-lookup"><span data-stu-id="38d78-158">Once you’re over 500 rows you will have to add 500 additional rows + 20% of the size of the table before you’ll see an automatic update on the stats</span></span>

<span data-ttu-id="38d78-159">由於沒有 DMV 可以判斷資料表內的資料於上次更新統計資料後是否有變更，了解您統計資料的年齡將可以協助您做出判斷。</span><span class="sxs-lookup"><span data-stu-id="38d78-159">Since there is no DMV to determine if data within the table has changed since the last time statistics were updated, knowing the age of your statistics can provide you with part of the picture.</span></span>  <span data-ttu-id="38d78-160">您可以使用下列查詢來判斷每份資料表上次更新了哪些統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-160">You can use the following query to determine the last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="38d78-161">請記住，如果特定資料行的值散發有實質變更，無論統計資料上一次更新的時間為何，您都應該更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-161">Remember if there is a material change in the distribution of values for a given column, you should update statistics regardless of the last time they were updated.</span></span>  
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

<span data-ttu-id="38d78-162">例如，資料倉儲中的日期資料行通常需要經常更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="38d78-163">每次有新資料列載入資料倉儲時，就會加入新的載入日期或交易日期。</span><span class="sxs-lookup"><span data-stu-id="38d78-163">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="38d78-164">這些會改變資料散發情況並使統計資料過時。</span><span class="sxs-lookup"><span data-stu-id="38d78-164">These change the data distribution and make the statistics out-of-date.</span></span>  <span data-ttu-id="38d78-165">相反地，客戶資料表上性別資料行的統計資料可能永遠不需要更新。</span><span class="sxs-lookup"><span data-stu-id="38d78-165">Conversely, statistics on a gender column on a customer table might never need to be updated.</span></span> <span data-ttu-id="38d78-166">假設客戶間的散發固定不變，將新資料列加入至資料表變化並不會改變資料散發情況。</span><span class="sxs-lookup"><span data-stu-id="38d78-166">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="38d78-167">不過，如果資料倉儲只包含一種性別，而新的需求導致多種性別，您肯定需要更新性別資料行的統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need to update statistics on the gender column.</span></span>

<span data-ttu-id="38d78-168">如需進一步說明，請參閱 MSDN 上的[統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="38d78-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="38d78-169">實作統計資料管理</span><span class="sxs-lookup"><span data-stu-id="38d78-169">Implementing statistics management</span></span>
<span data-ttu-id="38d78-170">擴充您的資料載入程序通常是個不錯的主意，可確保在載入結束時更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-170">It is often a good idea to extend your data loading process to ensure that statistics are updated at the end of the load.</span></span> <span data-ttu-id="38d78-171">當資料表變更其大小和/或其值散發時，資料載入最為頻繁。</span><span class="sxs-lookup"><span data-stu-id="38d78-171">The data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="38d78-172">因此，這是實作某些管理程序的合理位置。</span><span class="sxs-lookup"><span data-stu-id="38d78-172">Therefore, this is a logical place to implement some management processes.</span></span>

<span data-ttu-id="38d78-173">以下提供一些指導原則，以便在載入過程中更新您的統計資料：</span><span class="sxs-lookup"><span data-stu-id="38d78-173">Some guiding principles are provided below for updating your statistics during the load process:</span></span>

* <span data-ttu-id="38d78-174">確保每個載入的資料表至少都更新一個統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="38d78-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="38d78-175">這會在統計資料更新過程中更新資料表大小 (資料列計數和頁面計數) 資訊。</span><span class="sxs-lookup"><span data-stu-id="38d78-175">This updates the tables size (row count and page count) information as part of the stats update.</span></span>
* <span data-ttu-id="38d78-176">將焦點放在參與 JOIN、GROUP BY、ORDER BY 和 DISTINCT 子句的資料行。</span><span class="sxs-lookup"><span data-stu-id="38d78-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="38d78-177">考慮較頻繁更新「遞增索引鍵」資料行 (例如交易日期)，因為這些值不會包含在統計資料長條圖中。</span><span class="sxs-lookup"><span data-stu-id="38d78-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in the statistics histogram.</span></span>
* <span data-ttu-id="38d78-178">考慮較不常更新靜態散發資料行。</span><span class="sxs-lookup"><span data-stu-id="38d78-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="38d78-179">請記得，每個統計資料物件會依序更新。</span><span class="sxs-lookup"><span data-stu-id="38d78-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="38d78-180">僅只實作 `UPDATE STATISTICS <TABLE_NAME>` 可能不太理想 - 尤其是對具有許多統計資料物件的寬型資料表而言。</span><span class="sxs-lookup"><span data-stu-id="38d78-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="38d78-181">如需 [遞增索引鍵] 的詳細資訊，請參閱 SQL Server 2014 基數估計模型白皮書。</span><span class="sxs-lookup"><span data-stu-id="38d78-181">For more details on [ascending key] please refer to the SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="38d78-182">如需進一步說明，請參閱 MSDN 上的[基數估計][Cardinality Estimation]。</span><span class="sxs-lookup"><span data-stu-id="38d78-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="38d78-183">範例：建立統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-183">Examples: Create statistics</span></span>
<span data-ttu-id="38d78-184">下列範例顯示如何使用各種選項來建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-184">These examples show how to use various options for creating statistics.</span></span> <span data-ttu-id="38d78-185">您用於每個資料行的選項取決於您的資料特定以及在查詢中使用資料行的方式。</span><span class="sxs-lookup"><span data-stu-id="38d78-185">The options that you use for each column depend on the characteristics of your data and how the column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="38d78-186">A.</span><span class="sxs-lookup"><span data-stu-id="38d78-186">A.</span></span> <span data-ttu-id="38d78-187">使用預設選項建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="38d78-188">若要建立資料行的統計資料，只需提供統計資料物件的名稱和資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="38d78-188">To create statistics on a column, simply provide a name for the statistics object and the name of the column.</span></span>

<span data-ttu-id="38d78-189">此語法會使用所有預設選項。</span><span class="sxs-lookup"><span data-stu-id="38d78-189">This syntax uses all of the default options.</span></span> <span data-ttu-id="38d78-190">根據預設，SQL 資料倉儲在建立統計資料時會取樣 20% 的資料表。</span><span class="sxs-lookup"><span data-stu-id="38d78-190">By default, SQL Data Warehouse samples 20 percent of the table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="38d78-191">例如：</span><span class="sxs-lookup"><span data-stu-id="38d78-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="38d78-192">B.</span><span class="sxs-lookup"><span data-stu-id="38d78-192">B.</span></span> <span data-ttu-id="38d78-193">檢查每個資料列以建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="38d78-194">20% 的預設取樣率足以應付大部分的情況。</span><span class="sxs-lookup"><span data-stu-id="38d78-194">The default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="38d78-195">不過，您可以調整取樣率。</span><span class="sxs-lookup"><span data-stu-id="38d78-195">However, you can adjust the sampling rate.</span></span>

<span data-ttu-id="38d78-196">若要取樣整個資料表，請使用此語法：</span><span class="sxs-lookup"><span data-stu-id="38d78-196">To sample the full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="38d78-197">例如：</span><span class="sxs-lookup"><span data-stu-id="38d78-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-the-sample-size"></a><span data-ttu-id="38d78-198">C.</span><span class="sxs-lookup"><span data-stu-id="38d78-198">C.</span></span> <span data-ttu-id="38d78-199">指定取樣大小以建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-199">Create single-column statistics by specifying the sample size</span></span>
<span data-ttu-id="38d78-200">或者，您可以以百分比指定取樣大小：</span><span class="sxs-lookup"><span data-stu-id="38d78-200">Alternatively, you can specify the sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-the-rows"></a><span data-ttu-id="38d78-201">D.</span><span class="sxs-lookup"><span data-stu-id="38d78-201">D.</span></span> <span data-ttu-id="38d78-202">只對某些資料列建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-202">Create single-column statistics on only some of the rows</span></span>
<span data-ttu-id="38d78-203">另一個選項是，您可以對資料表中部分的資料列建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-203">Another option, you can create statistics on a portion of the rows in your table.</span></span> <span data-ttu-id="38d78-204">這稱為篩選的統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="38d78-205">例如，當您計劃查詢大型分割資料表的特定分割時，可以使用篩選的統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-205">For example, you could use filtered statistics when you plan to query a specific partition of a large partitioned table.</span></span> <span data-ttu-id="38d78-206">只對分割值建立統計資料，統計資料的精確度將會改善，並因而改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="38d78-206">By creating statistics on only the partition values, the accuracy of the statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="38d78-207">這個範例會建立某個值範圍的統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="38d78-208">您可以輕鬆地定義這些值以符合分割中的值範圍。</span><span class="sxs-lookup"><span data-stu-id="38d78-208">The values could easily be defined to match the range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="38d78-209">若要讓查詢最佳化工具在選擇分散式查詢計劃時考慮使用篩選的統計資料，查詢必須符合統計資料物件的定義。</span><span class="sxs-lookup"><span data-stu-id="38d78-209">For the query optimizer to consider using filtered statistics when it chooses the distributed query plan, the query must fit inside the definition of the statistics object.</span></span> <span data-ttu-id="38d78-210">使用上述範例，查詢的 where 子句需要指定介於 2000101 和 20001231 之間的 col1 值。</span><span class="sxs-lookup"><span data-stu-id="38d78-210">Using the previous example, the query's where clause needs to specify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-the-options"></a><span data-ttu-id="38d78-211">E.</span><span class="sxs-lookup"><span data-stu-id="38d78-211">E.</span></span> <span data-ttu-id="38d78-212">使用所有選項建立單一資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-212">Create single-column statistics with all the options</span></span>
<span data-ttu-id="38d78-213">您當然可以將選項合在一起。</span><span class="sxs-lookup"><span data-stu-id="38d78-213">You can, of course, combine the options together.</span></span> <span data-ttu-id="38d78-214">以下範例會使用自訂樣本大小建立篩選的統計資料物件：</span><span class="sxs-lookup"><span data-stu-id="38d78-214">The example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="38d78-215">如需完整參考，請參閱 MSDN 上的 [CREATE STATISTICS][CREATE STATISTICS]。</span><span class="sxs-lookup"><span data-stu-id="38d78-215">For the full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="38d78-216">F.</span><span class="sxs-lookup"><span data-stu-id="38d78-216">F.</span></span> <span data-ttu-id="38d78-217">建立多重資料行統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-217">Create multi-column statistics</span></span>
<span data-ttu-id="38d78-218">若要建立多重資料行統計資料，只需利用上述範例，但要指定更多資料行。</span><span class="sxs-lookup"><span data-stu-id="38d78-218">To create a multi-column statistics, simply use the previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="38d78-219">用來估計查詢結果中資料列數目的長條圖，只適用於統計資料物件定義中所列的第一個資料行。</span><span class="sxs-lookup"><span data-stu-id="38d78-219">The histogram, which is used to estimate number of rows in the query result, is only available for the first column listed in the statistics object definition.</span></span>
> 
> 

<span data-ttu-id="38d78-220">在此範例中，長條圖位於 *product\_category*。</span><span class="sxs-lookup"><span data-stu-id="38d78-220">In this example, the histogram is on *product\_category*.</span></span> <span data-ttu-id="38d78-221">跨資料行統計資料會依據 product\_category 和 product\_sub_c\ategory 計算：</span><span class="sxs-lookup"><span data-stu-id="38d78-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="38d78-222">因為 product\_category 和 product\_sub\_category 之間有關聯性，所以多重資料行統計資料在同時存取這些資料行時相當實用。</span><span class="sxs-lookup"><span data-stu-id="38d78-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at the same time.</span></span>

### <a name="g-create-statistics-on-all-the-columns-in-a-table"></a><span data-ttu-id="38d78-223">G.</span><span class="sxs-lookup"><span data-stu-id="38d78-223">G.</span></span> <span data-ttu-id="38d78-224">對資料表中的所有資料行建立統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-224">Create statistics on all the columns in a table</span></span>
<span data-ttu-id="38d78-225">建立統計資料的其中一個方法是在建立資料表後發出 CREATE STATISTICS 命令。</span><span class="sxs-lookup"><span data-stu-id="38d78-225">One way to create statistics is to issues CREATE STATISTICS commands after creating the table.</span></span>

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

### <a name="h-use-a-stored-procedure-to-create-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="38d78-226">H.</span><span class="sxs-lookup"><span data-stu-id="38d78-226">H.</span></span> <span data-ttu-id="38d78-227">使用預存程序對資料庫中的所有資料行建立統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-227">Use a stored procedure to create statistics on all columns in a database</span></span>
<span data-ttu-id="38d78-228">SQL 資料倉儲沒有相當於 SQL Server 中 [sp_create_stats][] 的系統預存程序。</span><span class="sxs-lookup"><span data-stu-id="38d78-228">SQL Data Warehouse does not have a system stored procedure equivalent to [sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="38d78-229">此預存程序會對資料庫中還沒有統計資料的每個資料行建立單一資料行統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="38d78-229">This stored procedure creates a single column statistics object on every column of the database that doesn't already have statistics.</span></span>

<span data-ttu-id="38d78-230">這會協助您開始進行資料庫設計。</span><span class="sxs-lookup"><span data-stu-id="38d78-230">This will help you get started with your database design.</span></span> <span data-ttu-id="38d78-231">請放心地依照您的需求進行調整。</span><span class="sxs-lookup"><span data-stu-id="38d78-231">Feel free to adapt it to your needs.</span></span>

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

<span data-ttu-id="38d78-232">若要利用此程序對資料表中的所有資料行建立統計資料，只需呼叫程序即可。</span><span class="sxs-lookup"><span data-stu-id="38d78-232">To create statistics on all columns in the table with this procedure, simply call the procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="38d78-233">範例：更新統計資料</span><span class="sxs-lookup"><span data-stu-id="38d78-233">Examples: update statistics</span></span>
<span data-ttu-id="38d78-234">若要更新統計資料，您可以：</span><span class="sxs-lookup"><span data-stu-id="38d78-234">To update statistics, you can:</span></span>

1. <span data-ttu-id="38d78-235">更新一個統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="38d78-235">Update one statistics object.</span></span> <span data-ttu-id="38d78-236">指定您要更新的統計資料物件名稱。</span><span class="sxs-lookup"><span data-stu-id="38d78-236">Specify the name of the statistics object you wish to update.</span></span>
2. <span data-ttu-id="38d78-237">更新資料表上的所有統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="38d78-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="38d78-238">指定資料表名稱，而不是一個特定統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="38d78-238">Specify the name of the table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="38d78-239">A.</span><span class="sxs-lookup"><span data-stu-id="38d78-239">A.</span></span> <span data-ttu-id="38d78-240">更新一個特定統計資料物件</span><span class="sxs-lookup"><span data-stu-id="38d78-240">Update one specific statistics object</span></span>
<span data-ttu-id="38d78-241">使用下列語法來更新特定統計資料物件：</span><span class="sxs-lookup"><span data-stu-id="38d78-241">Use the following syntax to update a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="38d78-242">例如：</span><span class="sxs-lookup"><span data-stu-id="38d78-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="38d78-243">藉由更新特定統計資料物件，即可減少管理統計資料所需的時間和資源。</span><span class="sxs-lookup"><span data-stu-id="38d78-243">By updating specific statistics objects, you can minimize the time and resources required to manage statistics.</span></span> <span data-ttu-id="38d78-244">這需要經過思考，才能選擇要更新的最佳統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="38d78-244">This requires some thought, though, to choose the best statistics objects to update.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="38d78-245">B.</span><span class="sxs-lookup"><span data-stu-id="38d78-245">B.</span></span> <span data-ttu-id="38d78-246">更新資料表上的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-246">Update all statistics on a table</span></span>
<span data-ttu-id="38d78-247">這顯示一個簡單的方法來更新資料表上的所有統計資料物件。</span><span class="sxs-lookup"><span data-stu-id="38d78-247">This shows a simple method for updating all the statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="38d78-248">例如：</span><span class="sxs-lookup"><span data-stu-id="38d78-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="38d78-249">此陳述式很容易使用。</span><span class="sxs-lookup"><span data-stu-id="38d78-249">This statement is easy to use.</span></span> <span data-ttu-id="38d78-250">只要記住這會更新資料表上的所有統計資料，因此可能會執行超出所需的更多工作。</span><span class="sxs-lookup"><span data-stu-id="38d78-250">Just remember this updates all statistics on the table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="38d78-251">如果效能不成問題，這絕對是保證擁有最新統計資料的最簡單且最完整的方式。</span><span class="sxs-lookup"><span data-stu-id="38d78-251">If the performance is not an issue, this is definitely the easiest and most complete way to guarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="38d78-252">更新資料表上的所有統計資料時，SQL 資料倉儲會進行掃描，以針對每個統計資料進行資料表取樣。</span><span class="sxs-lookup"><span data-stu-id="38d78-252">When updating all statistics on a table, SQL Data Warehouse does a scan to sample the table for each statistics.</span></span> <span data-ttu-id="38d78-253">如果資料表很大、有許多資料行以及許多統計資料，則根據需求來更新個別統計資料可能比較有效率。</span><span class="sxs-lookup"><span data-stu-id="38d78-253">If the table is large, has many columns, and many statistics, it might be more efficient to update individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="38d78-254">如需 `UPDATE STATISTICS` 程序的實作，請參閱[暫存資料表][Temporary]一文。</span><span class="sxs-lookup"><span data-stu-id="38d78-254">For an implementation of an `UPDATE STATISTICS` procedure please see the [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="38d78-255">實作方法與上述的 `CREATE STATISTICS` 程序有點不同，但最終結果相同。</span><span class="sxs-lookup"><span data-stu-id="38d78-255">The implementation method is slightly different to the `CREATE STATISTICS` procedure above but the end result is the same.</span></span>

<span data-ttu-id="38d78-256">如需完整語法，請參閱 MSDN 上的[更新統計資料][Update Statistics]。</span><span class="sxs-lookup"><span data-stu-id="38d78-256">For the full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="38d78-257">統計資料中繼資料</span><span class="sxs-lookup"><span data-stu-id="38d78-257">Statistics metadata</span></span>
<span data-ttu-id="38d78-258">您可利用數個系統檢視和函式來尋找統計資料相關資訊。</span><span class="sxs-lookup"><span data-stu-id="38d78-258">There are several system view and functions that you can use to find information about statistics.</span></span> <span data-ttu-id="38d78-259">例如，使用 stats-date 函式來查看最後建立或更新統計資料的時間，即可查看統計資料物件是否可能過期。</span><span class="sxs-lookup"><span data-stu-id="38d78-259">For example, you can see if a statistics object might be out-of-date by using the stats-date function to see when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="38d78-260">統計資料的目錄檢視</span><span class="sxs-lookup"><span data-stu-id="38d78-260">Catalog views for statistics</span></span>
<span data-ttu-id="38d78-261">這些系統檢視提供統計資料的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="38d78-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="38d78-262">目錄檢視</span><span class="sxs-lookup"><span data-stu-id="38d78-262">Catalog View</span></span> | <span data-ttu-id="38d78-263">說明</span><span class="sxs-lookup"><span data-stu-id="38d78-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="38d78-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="38d78-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="38d78-265">每個資料行有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="38d78-265">One row for each column.</span></span> |
| <span data-ttu-id="38d78-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="38d78-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="38d78-267">資料庫中每個物件有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="38d78-267">One row for each object in the database.</span></span> |
| <span data-ttu-id="38d78-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="38d78-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="38d78-269">資料庫中每個結構描述有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="38d78-269">One row for each schema in the database.</span></span> |
| <span data-ttu-id="38d78-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="38d78-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="38d78-271">每個統計資料物件有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="38d78-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="38d78-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="38d78-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="38d78-273">統計資料物件中每個資料行有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="38d78-273">One row for each column in the statistics object.</span></span> <span data-ttu-id="38d78-274">連結回到 sys.columns。</span><span class="sxs-lookup"><span data-stu-id="38d78-274">Links back to sys.columns.</span></span> |
| <span data-ttu-id="38d78-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="38d78-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="38d78-276">每個資料表 (包括外部資料表) 有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="38d78-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="38d78-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="38d78-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="38d78-278">每個資料類型有一個資料列。</span><span class="sxs-lookup"><span data-stu-id="38d78-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="38d78-279">統計資料的系統函式</span><span class="sxs-lookup"><span data-stu-id="38d78-279">System functions for statistics</span></span>
<span data-ttu-id="38d78-280">這些系統函式很適合用於處理統計資料：</span><span class="sxs-lookup"><span data-stu-id="38d78-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="38d78-281">系統函式</span><span class="sxs-lookup"><span data-stu-id="38d78-281">System Function</span></span> | <span data-ttu-id="38d78-282">說明</span><span class="sxs-lookup"><span data-stu-id="38d78-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="38d78-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="38d78-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="38d78-284">上次更新統計資料物件的日期。</span><span class="sxs-lookup"><span data-stu-id="38d78-284">Date the statistics object was last updated.</span></span> |
| <span data-ttu-id="38d78-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="38d78-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="38d78-286">提供有關統計資料物件所理解之值散發的摘要層級和詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="38d78-286">Provides summary level and detailed information about the distribution of values as understood by the statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="38d78-287">將統計資料資料行和函式結合成一個檢視</span><span class="sxs-lookup"><span data-stu-id="38d78-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="38d78-288">此檢視會一起顯示與統計資料相關的資料行，以及 [STATS_DATE()][] 函式的結果。</span><span class="sxs-lookup"><span data-stu-id="38d78-288">This view brings columns that relate to statistics, and results from the [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="38d78-289">DBCC SHOW_STATISTICS() 範例</span><span class="sxs-lookup"><span data-stu-id="38d78-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="38d78-290">DBCC SHOW_STATISTICS() 顯示統計資料物件中保存的資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-290">DBCC SHOW_STATISTICS() shows the data held within a statistics object.</span></span> <span data-ttu-id="38d78-291">此資料來自三個部分。</span><span class="sxs-lookup"><span data-stu-id="38d78-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="38d78-292">標頭</span><span class="sxs-lookup"><span data-stu-id="38d78-292">Header</span></span>
2. <span data-ttu-id="38d78-293">密度向量</span><span class="sxs-lookup"><span data-stu-id="38d78-293">Density Vector</span></span>
3. <span data-ttu-id="38d78-294">長條圖</span><span class="sxs-lookup"><span data-stu-id="38d78-294">Histogram</span></span>

<span data-ttu-id="38d78-295">有關統計資料的標頭中繼資料。</span><span class="sxs-lookup"><span data-stu-id="38d78-295">The header metadata about the statistics.</span></span> <span data-ttu-id="38d78-296">此長條圖會顯示統計資料物件的第一個索引鍵資料行中的值散發。</span><span class="sxs-lookup"><span data-stu-id="38d78-296">The histogram displays the distribution of values in the first key column of the statistics object.</span></span> <span data-ttu-id="38d78-297">密度向量可測量跨資料行關聯性。</span><span class="sxs-lookup"><span data-stu-id="38d78-297">The density vector measures cross-column correlation.</span></span> <span data-ttu-id="38d78-298">SQLDW 可使用統計資料物件中的任何資料來計算基數估計值。</span><span class="sxs-lookup"><span data-stu-id="38d78-298">SQLDW computes cardinality estimates with any of the data in the statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="38d78-299">顯示標頭、密度和長條圖</span><span class="sxs-lookup"><span data-stu-id="38d78-299">Show header, density, and histogram</span></span>
<span data-ttu-id="38d78-300">這個簡單範例顯示統計資料物件的所有三個部分。</span><span class="sxs-lookup"><span data-stu-id="38d78-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="38d78-301">例如：</span><span class="sxs-lookup"><span data-stu-id="38d78-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="38d78-302">顯示 DBCC SHOW_STATISTICS(); 的一或多個部分</span><span class="sxs-lookup"><span data-stu-id="38d78-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="38d78-303">如果您只想要檢視特定部分，請使用 `WITH` 子句並指定您要查看哪些部分：</span><span class="sxs-lookup"><span data-stu-id="38d78-303">If you are only interested in viewing specific parts, use the `WITH` clause and specify which parts you want to see:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="38d78-304">例如：</span><span class="sxs-lookup"><span data-stu-id="38d78-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="38d78-305">DBCC SHOW_STATISTICS() 差異</span><span class="sxs-lookup"><span data-stu-id="38d78-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="38d78-306">相較於 SQL Server，DBCC SHOW_STATISTICS() 在 SQL 資料倉儲中會更嚴格地實作。</span><span class="sxs-lookup"><span data-stu-id="38d78-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared to SQL Server.</span></span>

1. <span data-ttu-id="38d78-307">不支援未記載的功能</span><span class="sxs-lookup"><span data-stu-id="38d78-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="38d78-308">無法使用 Stats_stream</span><span class="sxs-lookup"><span data-stu-id="38d78-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="38d78-309">無法聯結特定統計資料子集的結果，例如 (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="38d78-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="38d78-310">無法針對訊息隱藏項目設定 NO_INFOMSGS</span><span class="sxs-lookup"><span data-stu-id="38d78-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="38d78-311">無法使用統計資料名稱前後的方括號</span><span class="sxs-lookup"><span data-stu-id="38d78-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="38d78-312">無法使用資料行名稱來識別統計資料物件</span><span class="sxs-lookup"><span data-stu-id="38d78-312">Cannot use column names to identify statistics objects</span></span>
7. <span data-ttu-id="38d78-313">不支援自訂錯誤 2767</span><span class="sxs-lookup"><span data-stu-id="38d78-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="38d78-314">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38d78-314">Next steps</span></span>
<span data-ttu-id="38d78-315">如需詳細資訊，請參閱 MSDN 上的 [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]。</span><span class="sxs-lookup"><span data-stu-id="38d78-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="38d78-316">若要深入了解，請參閱[資料表概觀][Overview]、[資料表的資料類型][Data Types]、[散發資料表][Distribute]、[編製資料表的索引][Index]、[分割資料表][Partition]和[暫存資料表][Temporary]等文章。</span><span class="sxs-lookup"><span data-stu-id="38d78-316">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="38d78-317">若要深入了解最佳作法，請參閱 [SQL Data 資料倉儲最佳作法][SQL Data Warehouse Best Practices]。</span><span class="sxs-lookup"><span data-stu-id="38d78-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
