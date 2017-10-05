---
title: "使用 Azure Data Lake Tools for Visual Studio 解決資料扭曲問題 | Microsoft Docs"
description: "使用 Azure Data Lake Tools for Visual Studio 針對資料扭曲問題的可能解決方案進行疑難排解。"
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 9b284ef33be4b935569fc368d81ddf040b2c2b7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="5cd90-103">使用 Azure Data Lake Tools for Visual Studio 解決資料扭曲問題</span><span class="sxs-lookup"><span data-stu-id="5cd90-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="5cd90-104">什麼是資料扭曲？</span><span class="sxs-lookup"><span data-stu-id="5cd90-104">What is data skew?</span></span>

<span data-ttu-id="5cd90-105">簡單來說，資料扭曲就是被過度代表的值。</span><span class="sxs-lookup"><span data-stu-id="5cd90-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="5cd90-106">設想您指派了 50 名稅務審查員來稽核納稅申報單，一名審查員負責美國的一個州。</span><span class="sxs-lookup"><span data-stu-id="5cd90-106">Imagine that you have assigned 50 tax examiners to audit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="5cd90-107">懷俄明州的審查員因為該州人口稀少，因此沒什麼工作量。</span><span class="sxs-lookup"><span data-stu-id="5cd90-107">The Wyoming examiner, because the population there is small, has little to do.</span></span> <span data-ttu-id="5cd90-108">但加州的審查員則因為該州人口眾多，因此一直都很忙碌。</span><span class="sxs-lookup"><span data-stu-id="5cd90-108">In California, however, the examiner is kept very busy because of the state's large population.</span></span>
    <span data-ttu-id="5cd90-109">![資料扭曲問題範例](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="5cd90-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="5cd90-110">在我們的案例中，所有稅務審查員所需處理的資料並非平均分配的，這表示某些審查員必須完成的工作會多過他人。</span><span class="sxs-lookup"><span data-stu-id="5cd90-110">In our scenario, the data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="5cd90-111">在您自己的作業中，您經常會遇到如這裡所說的稅務審查員範例的情況。</span><span class="sxs-lookup"><span data-stu-id="5cd90-111">In your own job, you frequently experience situations like the tax-examiner example here.</span></span> <span data-ttu-id="5cd90-112">更專業的說法是，會有一個人拿到比他的同事多很多的資料，在這種情況下，那個人的工作量會多過其他人，因此最終會拖累整個作業的進度。</span><span class="sxs-lookup"><span data-stu-id="5cd90-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes the vertex work more than the others and that eventually slows down an entire job.</span></span> <span data-ttu-id="5cd90-113">更糟糕的是，該項作業可能會失敗，因為舉例來說，那個人可能受到 5 小時執行階段和 6 GB 記憶體的限制。</span><span class="sxs-lookup"><span data-stu-id="5cd90-113">What's worse, the job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="5cd90-114">解決資料扭曲問題</span><span class="sxs-lookup"><span data-stu-id="5cd90-114">Resolving data-skew problems</span></span>

<span data-ttu-id="5cd90-115">Azure Data Lake Tools for Visual Studio 可協助偵測出您的作業是否有資料扭曲問題。</span><span class="sxs-lookup"><span data-stu-id="5cd90-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="5cd90-116">如果有此問題，您可以試試本節的解決方案來加以解決。</span><span class="sxs-lookup"><span data-stu-id="5cd90-116">If a problem exists, you can resolve it by trying the solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="5cd90-117">解決方案 1：改善資料表分割</span><span class="sxs-lookup"><span data-stu-id="5cd90-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-the-skewed-key-value-in-advance"></a><span data-ttu-id="5cd90-118">選項 1：事先篩選扭曲的索引鍵值</span><span class="sxs-lookup"><span data-stu-id="5cd90-118">Option 1: Filter the skewed key value in advance</span></span>

<span data-ttu-id="5cd90-119">如果篩選不會影響商務邏輯的話，您可以事先篩選具有較高頻率的值。</span><span class="sxs-lookup"><span data-stu-id="5cd90-119">If it does not affect your business logic, you can filter the higher-frequency values in advance.</span></span> <span data-ttu-id="5cd90-120">例如，如果 GUID 資料行中有大量 000-000-000，您可能不想彙總該值。</span><span class="sxs-lookup"><span data-stu-id="5cd90-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want to aggregate that value.</span></span> <span data-ttu-id="5cd90-121">在彙總之前，您可以撰寫 “WHERE GUID != “000-000-000”” 來篩選高頻率值。</span><span class="sxs-lookup"><span data-stu-id="5cd90-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” to filter the high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="5cd90-122">選項 2：選擇不同的分割區或散發索引鍵</span><span class="sxs-lookup"><span data-stu-id="5cd90-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="5cd90-123">在前面的範例中，如果您只想要檢查全國各地的稅務稽核工作量，您可以選取 ID 號碼做為索引鍵，以改善資料散發。</span><span class="sxs-lookup"><span data-stu-id="5cd90-123">In the preceding example, if you want only to check the tax-audit workload all over the country, you can improve the data distribution by selecting the ID number as your key.</span></span> <span data-ttu-id="5cd90-124">有時候，選擇不同的分割區或散發索引鍵可以更平均地散發資料，但您必須確保此舉不會影響商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="5cd90-124">Picking a different partition or distribution key can sometimes distribute the data more evenly, but you need to make sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="5cd90-125">比方說，為了計算各州的總稅額，您可以指定_州別_做為資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5cd90-125">For instance, to calculate the tax sum for each state, you might want to designate _State_ as the partition key.</span></span> <span data-ttu-id="5cd90-126">如果您仍然遇到這個問題，請嘗試使用選項 3。</span><span class="sxs-lookup"><span data-stu-id="5cd90-126">If you continue to experience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="5cd90-127">選項 3：新增更多分割區或散發索引鍵</span><span class="sxs-lookup"><span data-stu-id="5cd90-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="5cd90-128">您可以不只使用_州別_做為資料分割索引鍵，而使用多個資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5cd90-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="5cd90-129">例如，請考慮新增_郵遞區號_做為額外的資料分割索引鍵，以降低資料分割大小，讓資料更平均地分散。</span><span class="sxs-lookup"><span data-stu-id="5cd90-129">For example, consider adding _ZIP Code_ as an additional partition key to reduce data-partition sizes and distribute the data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="5cd90-130">選項 4：使用循環配置資源散發</span><span class="sxs-lookup"><span data-stu-id="5cd90-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="5cd90-131">如果您針對分割區和散發找不到適合的索引鍵，便可以嘗試使用循環配置資源散發。</span><span class="sxs-lookup"><span data-stu-id="5cd90-131">If you cannot find an appropriate key for partition and distribution, you can try to use round-robin distribution.</span></span> <span data-ttu-id="5cd90-132">循環配置資源散發會平等對待所有資料列，並將資料列隨機放到對應的貯體。</span><span class="sxs-lookup"><span data-stu-id="5cd90-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="5cd90-133">資料會平均地散發，但將會失去位置資訊，這項缺點也會減少部分作業的作業效能。</span><span class="sxs-lookup"><span data-stu-id="5cd90-133">The data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="5cd90-134">此外，如果您原本便打算針對扭曲索引鍵進行彙總，資料扭曲的問題會持續存在。</span><span class="sxs-lookup"><span data-stu-id="5cd90-134">Additionally, if you are doing aggregation for the skewed key anyway, the data-skew problem will persist.</span></span> <span data-ttu-id="5cd90-135">若要深入了解循環配置資源散發，請參閱[CREATE TABLE (U-SQL)：使用結構描述建立資料表](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch)中的＜U-SQL 資料表散發＞一節。</span><span class="sxs-lookup"><span data-stu-id="5cd90-135">To learn more about round-robin distribution, see the U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-the-query-plan"></a><span data-ttu-id="5cd90-136">解決方案 2︰改善查詢計劃</span><span class="sxs-lookup"><span data-stu-id="5cd90-136">Solution 2: Improve the query plan</span></span>

### <a name="option-1-use-the-create-statistics-statement"></a><span data-ttu-id="5cd90-137">選項 1︰使用 CREATE STATISTICS 陳述式</span><span class="sxs-lookup"><span data-stu-id="5cd90-137">Option 1: Use the CREATE STATISTICS statement</span></span>

<span data-ttu-id="5cd90-138">U-SQL 針對資料表提供 CREATE STATISTICS 陳述式。</span><span class="sxs-lookup"><span data-stu-id="5cd90-138">U-SQL provides the CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="5cd90-139">此陳述式可提供更多關於資料表中所儲存之資料特性 (例如值的散發) 的資訊給查詢最佳化工具。</span><span class="sxs-lookup"><span data-stu-id="5cd90-139">This statement gives more information to the query optimizer about the data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="5cd90-140">對於大部分查詢而言，查詢最佳化工具已為高品質的查詢計劃產生所需的統計資料。</span><span class="sxs-lookup"><span data-stu-id="5cd90-140">For most queries, the query optimizer already generates the necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="5cd90-141">但有時候您可能需要藉由使用 CREATE STATISTICS 建立其他統計資料或藉由修改查詢設計來改善查詢效能。</span><span class="sxs-lookup"><span data-stu-id="5cd90-141">Occasionally, you might need to improve query performance by creating additional statistics with CREATE STATISTICS or by modifying the query design.</span></span> <span data-ttu-id="5cd90-142">如需詳細資訊，請參閱 [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) 頁面。</span><span class="sxs-lookup"><span data-stu-id="5cd90-142">For more information, see the [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="5cd90-143">程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="5cd90-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="5cd90-144">統計資料的資訊不會自動更新。</span><span class="sxs-lookup"><span data-stu-id="5cd90-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="5cd90-145">如果您沒有重新建立統計資料就更新資料表中的資料，查詢效能可能會下滑。</span><span class="sxs-lookup"><span data-stu-id="5cd90-145">If you update the data in a table without re-creating the statistics, the query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="5cd90-146">選項 2：使用 SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="5cd90-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="5cd90-147">如果您想要加總各州的稅額，您必須使用 GROUP BY 狀態這種無法避免資料扭曲問題的方法。</span><span class="sxs-lookup"><span data-stu-id="5cd90-147">If you want to sum the tax for each state, you must use GROUP BY state, an approach that doesn't avoid the data-skew problem.</span></span> <span data-ttu-id="5cd90-148">不過，您可以在查詢中提供資料提示以識別索引鍵中的資料扭曲，讓最佳化工具能夠為您準備好執行計畫。</span><span class="sxs-lookup"><span data-stu-id="5cd90-148">However, you can provide a data hint in your query to identify data skew in keys so that the optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="5cd90-149">通常您可以將參數設定為 0.5 和 1，0.5 代表沒有太過扭曲，1 則代表嚴重扭曲。</span><span class="sxs-lookup"><span data-stu-id="5cd90-149">Usually, you can set the parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="5cd90-150">提示會影響目前陳述式及所有下游陳述式的執行計畫最佳化，因此請務必在執行可能的扭曲索引鍵彙總之前新增提示。</span><span class="sxs-lookup"><span data-stu-id="5cd90-150">Because the hint affects execution-plan optimization for the current statement and all downstream statements, be sure to add the hint before the potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that the given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="5cd90-151">程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="5cd90-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="5cd90-152">選項 3：使用 ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="5cd90-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="5cd90-153">除了 SKEWFACTOR，若為特定的扭曲索引鍵聯結案例，如果您知道其他的聯結資料列集很小，您可以在 U-SQL 陳述式的 JOIN 前面新增 ROWCOUNT 提示，以將此情形告知最佳化工具。</span><span class="sxs-lookup"><span data-stu-id="5cd90-153">In addition to SKEWFACTOR, for specific skewed-key join cases, if you know that the other joined row set is small, you can tell the optimizer by adding a ROWCOUNT hint in the U-SQL statement before JOIN.</span></span> <span data-ttu-id="5cd90-154">如此一來，最佳化工具就可以選擇廣播聯結策略來協助改善效能。</span><span class="sxs-lookup"><span data-stu-id="5cd90-154">This way, optimizer can choose a broadcast join strategy to help improve performance.</span></span> <span data-ttu-id="5cd90-155">請注意，ROWCOUNT 無法解決資料扭曲問題，但它可以提供一些額外的協助。</span><span class="sxs-lookup"><span data-stu-id="5cd90-155">Be aware that ROWCOUNT does not resolve the data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="5cd90-156">程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="5cd90-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information to determine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-the-user-defined-reducer-and-combiner"></a><span data-ttu-id="5cd90-157">解決方案 3：改善使用者定義的歸納器和結合器</span><span class="sxs-lookup"><span data-stu-id="5cd90-157">Solution 3: Improve the user-defined reducer and combiner</span></span>

<span data-ttu-id="5cd90-158">有時候，您可以撰寫使用者定義的運算子來處理複雜的程序邏輯，而撰寫良好的歸納器和結合器可能會在某些情況下降低資料扭曲問題。</span><span class="sxs-lookup"><span data-stu-id="5cd90-158">You can sometimes write a user-defined operator to deal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="5cd90-159">選項 1：在情況允許時使用遞迴歸納器</span><span class="sxs-lookup"><span data-stu-id="5cd90-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="5cd90-160">根據預設，使用者定義的歸納器會以非遞迴模式執行，這代表某個索引鍵所減少的工作會被散發至單一頂點。</span><span class="sxs-lookup"><span data-stu-id="5cd90-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="5cd90-161">但如果您的資料已扭曲，大型的資料集可能會在單一頂點中處理，並執行相當久的時間。</span><span class="sxs-lookup"><span data-stu-id="5cd90-161">But if your data is skewed, the huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="5cd90-162">若要改善效能，您可以在程式碼中新增屬性，將歸納器定義為以遞迴模式執行。</span><span class="sxs-lookup"><span data-stu-id="5cd90-162">To improve performance, you can add an attribute in your code to define reducer to run in recursive mode.</span></span> <span data-ttu-id="5cd90-163">然後，大量的資料集就可以散發到多個頂點並平行執行，以加快作業速度。</span><span class="sxs-lookup"><span data-stu-id="5cd90-163">Then, the huge data sets can be distributed to multiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="5cd90-164">若要將非遞迴歸納器變更為遞迴，您必須確保演算法為關聯性。</span><span class="sxs-lookup"><span data-stu-id="5cd90-164">To change a non-recursive reducer to recursive, you need to make sure that your algorithm is associative.</span></span> <span data-ttu-id="5cd90-165">例如，總和為關聯性，而中位數則不是。</span><span class="sxs-lookup"><span data-stu-id="5cd90-165">For example, the sum is associative, and the median is not.</span></span> <span data-ttu-id="5cd90-166">此外，您必須確保歸納器的輸入和輸出會保持相同的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5cd90-166">You also need to make sure that the input and output for reducer keep the same schema.</span></span>

<span data-ttu-id="5cd90-167">遞迴歸納器的屬性：</span><span class="sxs-lookup"><span data-stu-id="5cd90-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="5cd90-168">程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="5cd90-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="5cd90-169">選項 2：在情況允許時使用資料列層級結合器模式</span><span class="sxs-lookup"><span data-stu-id="5cd90-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="5cd90-170">結合器模式與針對特定扭曲索引鍵加入案例的 ROWCOUNT 提示類似，會嘗試將大型扭曲索引鍵值集散發到多個頂點，讓工作可以並行執行。</span><span class="sxs-lookup"><span data-stu-id="5cd90-170">Similar to the ROWCOUNT hint for specific skewed-key join cases, combiner mode tries to distribute huge skewed-key value sets to multiple vertices so that the work can be executed concurrently.</span></span> <span data-ttu-id="5cd90-171">結合器模式無法解決資料扭曲問題，但能夠為大型扭曲索引鍵值集提供一些額外的協助。</span><span class="sxs-lookup"><span data-stu-id="5cd90-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="5cd90-172">根據預設，結合器模式為 Full，這代表無法分開左資料列集和右資料列集。</span><span class="sxs-lookup"><span data-stu-id="5cd90-172">By default, the combiner mode is Full, which means that the left row set and right row set cannot be separated.</span></span> <span data-ttu-id="5cd90-173">將模式設為 Left/Right/Inner 則可進行資料列層級聯結。</span><span class="sxs-lookup"><span data-stu-id="5cd90-173">Setting the mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="5cd90-174">系統會將對應的資料列集分開，並將其分散到多個平行執行的頂點。</span><span class="sxs-lookup"><span data-stu-id="5cd90-174">The system separates the corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="5cd90-175">不過，在設定結合器模式之前，請務必確保對應的資料列集可以分開。</span><span class="sxs-lookup"><span data-stu-id="5cd90-175">However, before you configure the combiner mode, be careful to ensure that the corresponding row sets can be separated.</span></span>

<span data-ttu-id="5cd90-176">接下來的範例顯示分開的左資料列集。</span><span class="sxs-lookup"><span data-stu-id="5cd90-176">The example that follows shows a separated left row set.</span></span> <span data-ttu-id="5cd90-177">每個輸出資料列相依於左邊的單一輸入資料列，並可能相依於所有具有相同索引鍵值的右邊資料列。</span><span class="sxs-lookup"><span data-stu-id="5cd90-177">Each output row depends on a single input row from the left, and it potentially depends on all rows from the right with the same key value.</span></span> <span data-ttu-id="5cd90-178">如果您將結合器模式設定為 Left，系統會將大型的左資料列集分開成較小的資料列集，並將它們指派給多個頂點。</span><span class="sxs-lookup"><span data-stu-id="5cd90-178">If you set the combiner mode as left, the system separates the huge left-row set into small ones and assigns them to multiple vertices.</span></span>

![結合器模式圖例](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="5cd90-180">如果您設定了錯誤的結合器模式，其組合會較無效率，且結果可能會出錯。</span><span class="sxs-lookup"><span data-stu-id="5cd90-180">If you set the wrong combiner mode, the combination is less efficient, and the results might be wrong.</span></span>

<span data-ttu-id="5cd90-181">結合器模式的屬性︰</span><span class="sxs-lookup"><span data-stu-id="5cd90-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all the input rows from left and right with the same key value.

- <span data-ttu-id="5cd90-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left)：每個輸出資料列相依於左邊的單一輸入資料列 (並可能相依於所有具有相同索引鍵值的右邊資料列)。</span><span class="sxs-lookup"><span data-stu-id="5cd90-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from the left (and potentially all rows from the right with the same key value).</span></span>

- <span data-ttu-id="5cd90-183">qlUserDefinedCombiner(Mode=CombinerMode.Right)：每個輸出資料列相依於右邊的單一輸入資料列 (並可能相依於所有具有相同索引鍵值的左邊資料列)。</span><span class="sxs-lookup"><span data-stu-id="5cd90-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from the right (and potentially all rows from the left with the same key value).</span></span>

- <span data-ttu-id="5cd90-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner)：每個輸出資料列相依於左邊和右邊具有相同值的單一輸入資料列。</span><span class="sxs-lookup"><span data-stu-id="5cd90-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from the left and the right with the same value.</span></span>

<span data-ttu-id="5cd90-185">程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="5cd90-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
