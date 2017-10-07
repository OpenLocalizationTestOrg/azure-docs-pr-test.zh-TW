---
title: "Azure SQL database aaaQuery 效能深入資訊 |Microsoft 文件"
description: "效能監視識別的 hello 大部分的 CPU 耗用查詢 Azure SQL database 的查詢。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="2c727-103">Azure SQL Database 查詢效能深入解析</span><span class="sxs-lookup"><span data-stu-id="2c727-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="2c727-104">管理和調整 hello 關聯式資料庫效能是富有挑戰性的工作需要重要的專業知識和需要投入時間。</span><span class="sxs-lookup"><span data-stu-id="2c727-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="2c727-105">查詢效能深入解析可讓您 toospend 藉由提供 hello 下列疑難排解資料庫效能較少的時間：</span><span class="sxs-lookup"><span data-stu-id="2c727-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="2c727-106">更深入的資料庫資源 (DTU) 取用分析。</span><span class="sxs-lookup"><span data-stu-id="2c727-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="2c727-107">hello 排名最前面查詢依 CPU/期間執行計數，可能會改善效能進行微調。</span><span class="sxs-lookup"><span data-stu-id="2c727-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="2c727-108">向下的能力 toodrill hello 到 hello 詳細資料的查詢、 檢視其文字和資源使用量的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="2c727-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="2c727-109">效能微調註解，可顯示 [SQL Azure Database 建議程式](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="2c727-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="2c727-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="2c727-110">Prerequisites</span></span>
* <span data-ttu-id="2c727-111">「查詢效能深入解析」要求 [查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx) 在您的資料庫上為作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="2c727-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="2c727-112">如果未執行查詢存放區，hello 入口網站會提示您 tooturn 其上。</span><span class="sxs-lookup"><span data-stu-id="2c727-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="2c727-113">權限</span><span class="sxs-lookup"><span data-stu-id="2c727-113">Permissions</span></span>
<span data-ttu-id="2c727-114">hello 下列[角色型存取控制](../active-directory/role-based-access-control-what-is.md)權限是必要的 toouse 查詢效能深入解析：</span><span class="sxs-lookup"><span data-stu-id="2c727-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="2c727-115">**讀取器**，**擁有者**，**參與者**， **SQL DB 參與者**，或**SQL Server 參與者**權限需要 tooview hello 熱門資源取用查詢和圖表。</span><span class="sxs-lookup"><span data-stu-id="2c727-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="2c727-116">**擁有者**，**參與者**， **SQL DB 參與者**，或**SQL Server 參與者**權限是必要的 tooview 查詢文字。</span><span class="sxs-lookup"><span data-stu-id="2c727-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="2c727-117">使用查詢效能深入解析</span><span class="sxs-lookup"><span data-stu-id="2c727-117">Using Query Performance Insight</span></span>
<span data-ttu-id="2c727-118">查詢效能深入解析為簡單 toouse:</span><span class="sxs-lookup"><span data-stu-id="2c727-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="2c727-119">開啟[Azure 入口網站](https://portal.azure.com/)和尋找您想 tooexamine 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="2c727-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="2c727-120">從左側功能表中，[支援和疑難排解] 下方，選取 [查詢效能深入解析]。</span><span class="sxs-lookup"><span data-stu-id="2c727-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="2c727-121">Hello 第一個索引標籤上，檢閱 熱門資源取用查詢的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="2c727-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="2c727-122">選取個別查詢 tooview 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2c727-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="2c727-123">開啟 [SQL Azure Database 建議程式](sql-database-advisor.md) ，並查看是否有任何可用的建議。</span><span class="sxs-lookup"><span data-stu-id="2c727-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="2c727-124">使用滑桿或縮放圖示 toochange 觀察到的間隔。</span><span class="sxs-lookup"><span data-stu-id="2c727-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![效能儀表板](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="2c727-126">幾個小時的資料需要 toobe 查詢存放區所擷取的 SQL Database tooprovide 查詢效能深入資訊。</span><span class="sxs-lookup"><span data-stu-id="2c727-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="2c727-127">如果 hello 資料庫有任何活動或查詢存放區期間，未作用一段時間，顯示該時間週期時，將為空白 hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="2c727-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="2c727-128">如果查詢存放區不在執行中，您可隨時加以啟用。</span><span class="sxs-lookup"><span data-stu-id="2c727-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="2c727-129">檢閱排名最前面的 CPU 取用查詢</span><span class="sxs-lookup"><span data-stu-id="2c727-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="2c727-130">在 hello[入口網站](http://portal.azure.com)不要遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="2c727-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="2c727-131">瀏覽 tooa SQL 資料庫，然後按一下 **所有設定** > **支援 + 疑難排解** > **查詢效能深入解析**。</span><span class="sxs-lookup"><span data-stu-id="2c727-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![查詢效能深入解析][1]
   
    <span data-ttu-id="2c727-133">hello 排名最前面查詢檢視隨即開啟，並列出 hello 前 CPU 取用查詢。</span><span class="sxs-lookup"><span data-stu-id="2c727-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="2c727-134">按一下 詳細資料的 hello 圖表周圍。</span><span class="sxs-lookup"><span data-stu-id="2c727-134">Click around hello chart for details.</span></span><br><span data-ttu-id="2c727-135">hello 第一行會顯示 hello 資料庫的整體 DTU %hello 橫條圖會顯示在 hello 選間隔期間 hello 選取查詢所使用的 CPU %時 (例如，如果**上週**選取每個橫條都代表一天)。</span><span class="sxs-lookup"><span data-stu-id="2c727-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![排名最前面的查詢][2]
   
    <span data-ttu-id="2c727-137">hello 下方的方格代表 hello 顯示查詢的彙總的資訊。</span><span class="sxs-lookup"><span data-stu-id="2c727-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="2c727-138">查詢識別碼 - 資料庫內部查詢的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="2c727-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="2c727-139">在可觀察時間間隔期間每個查詢的 CPU (取決於彙總函式)。</span><span class="sxs-lookup"><span data-stu-id="2c727-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="2c727-140">每個查詢的持續時間 (取決於彙總函式)。</span><span class="sxs-lookup"><span data-stu-id="2c727-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="2c727-141">特定查詢的總執行次數。</span><span class="sxs-lookup"><span data-stu-id="2c727-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="2c727-142">選取或清除個別查詢 tooinclude 或排除 hello 圖表使用核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2c727-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="2c727-143">如果您的資料就會成為過時，請按一下 hello**重新整理** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2c727-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="2c727-144">您可以使用滑桿和顯示比例按鈕 toochange 的觀測間隔，並調查尖峰：![設定](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="2c727-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="2c727-145">(選擇性) 如果您想要不同的檢視，您可以選取 [自訂]  索引標籤，然後設定：</span><span class="sxs-lookup"><span data-stu-id="2c727-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="2c727-146">度量 (CPU、持續時間、執行計數)</span><span class="sxs-lookup"><span data-stu-id="2c727-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="2c727-147">時間間隔 (過去 24 小時、過去一週、過去一個月)。</span><span class="sxs-lookup"><span data-stu-id="2c727-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="2c727-148">查詢數目。</span><span class="sxs-lookup"><span data-stu-id="2c727-148">Number of queries.</span></span>
   * <span data-ttu-id="2c727-149">彙總函式。</span><span class="sxs-lookup"><span data-stu-id="2c727-149">Aggregation function.</span></span>
     
     ![settings](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="2c727-151">檢視個別查詢詳細資料</span><span class="sxs-lookup"><span data-stu-id="2c727-151">Viewing individual query details</span></span>
<span data-ttu-id="2c727-152">tooview 查詢詳細資料：</span><span class="sxs-lookup"><span data-stu-id="2c727-152">tooview query details:</span></span>

1. <span data-ttu-id="2c727-153">按一下 hello 清單的最上層查詢中的任何查詢。</span><span class="sxs-lookup"><span data-stu-id="2c727-153">Click any query in hello list of top queries.</span></span>
   
    ![詳細資料](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="2c727-155">hello 詳細資料檢視會開啟，並 hello 查詢 CPU 耗用量/期間執行計數細分經過一段時間。</span><span class="sxs-lookup"><span data-stu-id="2c727-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="2c727-156">按一下 詳細資料的 hello 圖表周圍。</span><span class="sxs-lookup"><span data-stu-id="2c727-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="2c727-157">上方圖表可顯示行整體資料庫的 DTU %，而且 hello 列 hello 選取的查詢所耗用的 CPU %。</span><span class="sxs-lookup"><span data-stu-id="2c727-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="2c727-158">第二個圖表可顯示總持續時間由 hello 選取的查詢。</span><span class="sxs-lookup"><span data-stu-id="2c727-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="2c727-159">下方圖表可顯示 hello 選取查詢所執行的總次數。</span><span class="sxs-lookup"><span data-stu-id="2c727-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![查詢詳細資料][3]
4. <span data-ttu-id="2c727-161">（選擇性） 使用滑桿、 顯示比例按鈕或按**設定**toocustomize 查詢資料的顯示方式或 toopick 不同的時間期間。</span><span class="sxs-lookup"><span data-stu-id="2c727-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="2c727-162">針對每段持續時間檢閱排名最前面的查詢</span><span class="sxs-lookup"><span data-stu-id="2c727-162">Review top queries per duration</span></span>
<span data-ttu-id="2c727-163">在 hello 最近更新中的查詢效能深入解析，我們引進了兩個新的計量，可協助您找出潛在的瓶頸： 持續時間和執行計數。</span><span class="sxs-lookup"><span data-stu-id="2c727-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="2c727-164">長時間執行的查詢有 hello 的鎖定較長的資源、 封鎖其他使用者，以及限制延展性的最大可能性。</span><span class="sxs-lookup"><span data-stu-id="2c727-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="2c727-165">它們也是 hello 最佳化的最佳候選項目。</span><span class="sxs-lookup"><span data-stu-id="2c727-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="2c727-166">tooidentify 長時間執行的查詢：</span><span class="sxs-lookup"><span data-stu-id="2c727-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="2c727-167">針對選取的資料庫，在 [查詢效能深入解析] 中開啟 [自訂]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="2c727-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="2c727-168">變更計量 toobe**持續時間**</span><span class="sxs-lookup"><span data-stu-id="2c727-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="2c727-169">選取查詢數目和觀測間隔</span><span class="sxs-lookup"><span data-stu-id="2c727-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="2c727-170">選取彙總函式</span><span class="sxs-lookup"><span data-stu-id="2c727-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="2c727-171">**Sum** 會加總整個觀測間隔內的所有查詢執行時間。</span><span class="sxs-lookup"><span data-stu-id="2c727-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="2c727-172">**Max** 會尋找在整個觀測間隔內執行時間最大的查詢。</span><span class="sxs-lookup"><span data-stu-id="2c727-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="2c727-173">**Avg**平均執行時間，所有的查詢執行並顯示您會發現 hello 超出這些平均值的頂端。</span><span class="sxs-lookup"><span data-stu-id="2c727-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![查詢持續時間][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="2c727-175">針對每個執行計數檢閱排名最前面的查詢</span><span class="sxs-lookup"><span data-stu-id="2c727-175">Review top queries per execution count</span></span>
<span data-ttu-id="2c727-176">執行數目很高可能不會影響資料庫本身且資源使用量可能很低，但整體應用程式可能會變慢。</span><span class="sxs-lookup"><span data-stu-id="2c727-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="2c727-177">在某些情況下，極高的執行計數可能會導致 tooincrease 的網路往返。</span><span class="sxs-lookup"><span data-stu-id="2c727-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="2c727-178">往返次數會大幅影響效能。</span><span class="sxs-lookup"><span data-stu-id="2c727-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="2c727-179">它們是主體 toonetwork 延遲和 toodownstream 伺服器延遲。</span><span class="sxs-lookup"><span data-stu-id="2c727-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="2c727-180">比方說，許多資料導向網站經常存取 hello 資料庫針對每個使用者要求。</span><span class="sxs-lookup"><span data-stu-id="2c727-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="2c727-181">雖然連接共用有幫助，hello 增加網路流量和 hello 資料庫伺服器上的處理負載可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="2c727-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="2c727-182">一般建議是 tookeep round 往返 tooan 絕對最小值。</span><span class="sxs-lookup"><span data-stu-id="2c727-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="2c727-183">tooidentify 經常執行的查詢 （「 多對話 」） 的查詢：</span><span class="sxs-lookup"><span data-stu-id="2c727-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="2c727-184">針對選取的資料庫，在 [查詢效能深入解析] 中開啟 [自訂]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="2c727-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="2c727-185">變更計量 toobe**執行計數**</span><span class="sxs-lookup"><span data-stu-id="2c727-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="2c727-186">選取查詢數目和觀測間隔</span><span class="sxs-lookup"><span data-stu-id="2c727-186">Select number of queries and observation interval</span></span>
   
    ![查詢執行計數][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="2c727-188">了解效能微調註解</span><span class="sxs-lookup"><span data-stu-id="2c727-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="2c727-189">同時瀏覽您的工作負載中查詢效能深入解析，您可能會注意到具有垂直線 hello 圖表上方的圖示。</span><span class="sxs-lookup"><span data-stu-id="2c727-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="2c727-190">這些圖示是註解。它們代表 [SQL Azure Database 建議程式](sql-database-advisor.md)所執行會影響效能的動作。</span><span class="sxs-lookup"><span data-stu-id="2c727-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="2c727-191">由暫留註釋，您可以取得 hello 動作的基本資訊：</span><span class="sxs-lookup"><span data-stu-id="2c727-191">By hovering annotation, you get basic information about hello action:</span></span>

![查詢註解][6]

<span data-ttu-id="2c727-193">如果您想要更多的 tooknow，或將 advisor 建議，套用，請按一下 [hello] 圖示。</span><span class="sxs-lookup"><span data-stu-id="2c727-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="2c727-194">隨即會開啟動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2c727-194">It will open details of action.</span></span> <span data-ttu-id="2c727-195">如果是有效的建議，您就能使用命令立即套用動作。</span><span class="sxs-lookup"><span data-stu-id="2c727-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![查詢註解詳細資料][7]

### <a name="multiple-annotations"></a><span data-ttu-id="2c727-197">多個註解。</span><span class="sxs-lookup"><span data-stu-id="2c727-197">Multiple annotations.</span></span>
<span data-ttu-id="2c727-198">它是可能的縮放層級，因為會關閉 tooeach 其他的註釋，將取得摺疊成一個。</span><span class="sxs-lookup"><span data-stu-id="2c727-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="2c727-199">這將會利用特殊的圖示來表示，按一下該圖示就會開啟新的刀鋒視窗，其中顯示已分組的註解清單。</span><span class="sxs-lookup"><span data-stu-id="2c727-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="2c727-200">建立查詢和效能調整動作的關聯可協助 toobetter 了解您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="2c727-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="2c727-201">最佳化查詢效能深入解析的 hello 查詢存放區組態</span><span class="sxs-lookup"><span data-stu-id="2c727-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="2c727-202">在您使用的查詢效能深入解析，您可能會遇到 hello 遵循查詢存放區的訊息：</span><span class="sxs-lookup"><span data-stu-id="2c727-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="2c727-203">「此資料庫的查詢存放區未正確設定。</span><span class="sxs-lookup"><span data-stu-id="2c727-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="2c727-204">按一下這裡 toolearn 詳細。 」</span><span class="sxs-lookup"><span data-stu-id="2c727-204">Click here toolearn more."</span></span>
* <span data-ttu-id="2c727-205">「此資料庫的查詢存放區未正確設定。</span><span class="sxs-lookup"><span data-stu-id="2c727-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="2c727-206">按一下這裡 toochange 設定。 」</span><span class="sxs-lookup"><span data-stu-id="2c727-206">Click here toochange settings."</span></span> 

<span data-ttu-id="2c727-207">查詢存放區不能 toocollect 新資料時，通常會出現這些訊息。</span><span class="sxs-lookup"><span data-stu-id="2c727-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="2c727-208">當查詢存放區處於唯讀狀態且以最佳方式設定參數時，就會發生第一種狀況。</span><span class="sxs-lookup"><span data-stu-id="2c727-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="2c727-209">您可以藉由增加查詢存放區的大小，或清除查詢存放區來修正此問題。</span><span class="sxs-lookup"><span data-stu-id="2c727-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![qds 按鈕][8]

<span data-ttu-id="2c727-211">當查詢存放區已關閉或參數並不是以最佳方式所設定時，就會發生第二種狀況。</span><span class="sxs-lookup"><span data-stu-id="2c727-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="2c727-212">藉由執行下列命令，或直接從入口網站，您可以變更 hello 保留和擷取原則，並啟用查詢存放區：</span><span class="sxs-lookup"><span data-stu-id="2c727-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![qds 按鈕][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="2c727-214">建議使用的保留期和擷取原則</span><span class="sxs-lookup"><span data-stu-id="2c727-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="2c727-215">保留期原則有兩種：</span><span class="sxs-lookup"><span data-stu-id="2c727-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="2c727-216">大小基礎-如果已到達組 tooAUTO 它將會清除資料自動當接近大小上限。</span><span class="sxs-lookup"><span data-stu-id="2c727-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="2c727-217">以時間為基礎-根據預設，我們會將它設定 too30 天，也就是說，如果查詢存放區就會用完空間，將會刪除查詢超過 30 天的資訊</span><span class="sxs-lookup"><span data-stu-id="2c727-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="2c727-218">擷取原則可以設定為：</span><span class="sxs-lookup"><span data-stu-id="2c727-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="2c727-219">**All**：擷取所有的查詢。</span><span class="sxs-lookup"><span data-stu-id="2c727-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="2c727-220">**Auto**：會忽略不常執行的查詢，以及編譯和執行持續時間微不足道的查詢。</span><span class="sxs-lookup"><span data-stu-id="2c727-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="2c727-221">執行次數、編譯及執行階段持續時間的臨界值是由內部決定的。</span><span class="sxs-lookup"><span data-stu-id="2c727-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="2c727-222">這是 hello 預設選項。</span><span class="sxs-lookup"><span data-stu-id="2c727-222">This is hello default option.</span></span>
* <span data-ttu-id="2c727-223">**None**：「查詢存放區」會停止擷取新的查詢，不過仍然會收集已擷取查詢的執行階段統計資料。</span><span class="sxs-lookup"><span data-stu-id="2c727-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="2c727-224">我們建議您設定的所有原則 tooAUTO 和全新的原則 too30 天：</span><span class="sxs-lookup"><span data-stu-id="2c727-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="2c727-225">增加查詢存放區的大小，</span><span class="sxs-lookup"><span data-stu-id="2c727-225">Increase size of Query Store.</span></span> <span data-ttu-id="2c727-226">這可能是由連接 tooa 資料庫執行和發行下列查詢：</span><span class="sxs-lookup"><span data-stu-id="2c727-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="2c727-227">不過，如果您不想 toowait 您可以清除查詢存放區，套用這些設定會最後會讓收集新的查詢，查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="2c727-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="2c727-228">執行下列查詢將會刪除 hello 查詢存放區中的所有目前資訊。</span><span class="sxs-lookup"><span data-stu-id="2c727-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="2c727-229">摘要</span><span class="sxs-lookup"><span data-stu-id="2c727-229">Summary</span></span>
<span data-ttu-id="2c727-230">查詢效能深入解析，可協助您了解 hello 的查詢工作負載的影響，以及它與 toodatabase 資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="2c727-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="2c727-231">利用此功能，您將深入了解 hello 頂端取用查詢，並輕鬆地在問題之前就識別出 hello 的 toofix。</span><span class="sxs-lookup"><span data-stu-id="2c727-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c727-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c727-232">Next steps</span></span>
<span data-ttu-id="2c727-233">如需有關改善您的 SQL database 的 hello 效能的其他建議，請按一下[建議](sql-database-advisor.md)上 hello**查詢效能深入解析**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c727-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

![效能建議程式](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

