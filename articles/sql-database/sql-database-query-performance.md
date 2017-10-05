---
title: "Azure SQL Database 的查詢效能深入解析 | Microsoft Docs"
description: "查詢效能監視可識別 Azure SQL Database 的大部分 CPU 取用的查詢。"
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
ms.openlocfilehash: 1925d4ff8f5b16a0df56de987f8653cfd8441c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="02034-103">Azure SQL Database 查詢效能深入解析</span><span class="sxs-lookup"><span data-stu-id="02034-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="02034-104">管理和調整關聯式資料庫效能是一項具挑戰性的工作，需要投入大量的專業知識和時間。</span><span class="sxs-lookup"><span data-stu-id="02034-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="02034-105">「查詢效能深入解析」提供了下列各項，讓您得以花費較少時間來對資料庫效能進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="02034-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span></span>

* <span data-ttu-id="02034-106">更深入的資料庫資源 (DTU) 取用分析。</span><span class="sxs-lookup"><span data-stu-id="02034-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="02034-107">依 CPU/持續時間/執行計數排名最前面的查詢，進行微調有可能會改善效能。</span><span class="sxs-lookup"><span data-stu-id="02034-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="02034-108">能夠向下鑽研查詢的詳細資料，以檢視其文字和資源使用量的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="02034-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="02034-109">效能微調註解，可顯示 [SQL Azure Database 建議程式](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="02034-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="02034-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="02034-110">Prerequisites</span></span>
* <span data-ttu-id="02034-111">「查詢效能深入解析」要求 [查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx) 在您的資料庫上為作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="02034-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="02034-112">如果查詢存放區不在執行中，則入口網站會提示您將它開啟。</span><span class="sxs-lookup"><span data-stu-id="02034-112">If Query Store is not running, the portal prompts you to turn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="02034-113">權限</span><span class="sxs-lookup"><span data-stu-id="02034-113">Permissions</span></span>
<span data-ttu-id="02034-114">需有下列 [角色型存取控制](../active-directory/role-based-access-control-what-is.md) 權限，才能使用「查詢效能深入解析」︰</span><span class="sxs-lookup"><span data-stu-id="02034-114">The following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required to use Query Performance Insight:</span></span> 

* <span data-ttu-id="02034-115">檢視排名最前面的資源取用查詢和圖表時，需具備**讀取器**、**擁有者**、**參與者**、**SQL DB 參與者** 或 **SQL Server 參與者** 權限。</span><span class="sxs-lookup"><span data-stu-id="02034-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="02034-116">檢視查詢文字時，需具備**擁有者**、**參與者**、**SQL DB 參與者**或 **SQL Server 參與者**權限。</span><span class="sxs-lookup"><span data-stu-id="02034-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="02034-117">使用查詢效能深入解析</span><span class="sxs-lookup"><span data-stu-id="02034-117">Using Query Performance Insight</span></span>
<span data-ttu-id="02034-118">「查詢效能深入解析」很容易使用︰</span><span class="sxs-lookup"><span data-stu-id="02034-118">Query Performance Insight is easy to use:</span></span>

* <span data-ttu-id="02034-119">開啟 [Azure 入口網站](https://portal.azure.com/) ，然後尋找您想要檢查的資料庫。</span><span class="sxs-lookup"><span data-stu-id="02034-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span></span> 
  * <span data-ttu-id="02034-120">從左側功能表中，[支援和疑難排解] 下方，選取 [查詢效能深入解析]。</span><span class="sxs-lookup"><span data-stu-id="02034-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="02034-121">在第一個索引標籤上，檢閱排名最前面的資源取用查詢清單。</span><span class="sxs-lookup"><span data-stu-id="02034-121">On the first tab, review the list of top resource-consuming queries.</span></span>
* <span data-ttu-id="02034-122">選取個別的查詢來檢視其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02034-122">Select an individual query to view its details.</span></span>
* <span data-ttu-id="02034-123">開啟 [SQL Azure Database 建議程式](sql-database-advisor.md) ，並查看是否有任何可用的建議。</span><span class="sxs-lookup"><span data-stu-id="02034-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="02034-124">使用滑桿或縮放圖示來變更所觀測的間隔。</span><span class="sxs-lookup"><span data-stu-id="02034-124">Use sliders or zoom icons to change observed interval.</span></span>
  
    ![效能儀表板](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="02034-126">SQL Database 的查詢存放區需要擷取數個小時的資料，才能提供查詢效能深入解析。</span><span class="sxs-lookup"><span data-stu-id="02034-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span></span> <span data-ttu-id="02034-127">如果在某段時間內資料庫沒有任何作用中的活動或查詢存放區，則在顯示該期間時圖表會是空的。</span><span class="sxs-lookup"><span data-stu-id="02034-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span></span> <span data-ttu-id="02034-128">如果查詢存放區不在執行中，您可隨時加以啟用。</span><span class="sxs-lookup"><span data-stu-id="02034-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="02034-129">檢閱排名最前面的 CPU 取用查詢</span><span class="sxs-lookup"><span data-stu-id="02034-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="02034-130">在 [入口網站](http://portal.azure.com) 中執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="02034-130">In the [portal](http://portal.azure.com) do the following:</span></span>

1. <span data-ttu-id="02034-131">瀏覽至 SQL Database，然後按一下 [所有設定]  >  [支援 + 疑難排解]  >  [查詢效能深入解析]。</span><span class="sxs-lookup"><span data-stu-id="02034-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![查詢效能深入解析][1]
   
    <span data-ttu-id="02034-133">排名最前面的查詢檢視會隨即開啟，並列出排名最前面的 CPU 取用查詢。</span><span class="sxs-lookup"><span data-stu-id="02034-133">The top queries view opens and the top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="02034-134">按一下圖表周圍以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02034-134">Click around the chart for details.</span></span><br><span data-ttu-id="02034-135">最上面的線條顯示資料庫的整體 DTU %，而長條則顯示已選取查詢在所選間隔內 (例如，如果已選取 [過去一週]，則每個長條代表一天) 所取用的 CPU %。</span><span class="sxs-lookup"><span data-stu-id="02034-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![排名最前面的查詢][2]
   
    <span data-ttu-id="02034-137">底部格線則代表可見查詢的彙總資訊。</span><span class="sxs-lookup"><span data-stu-id="02034-137">The bottom grid represents aggregated information for the visible queries.</span></span>
   
   * <span data-ttu-id="02034-138">查詢識別碼 - 資料庫內部查詢的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="02034-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="02034-139">在可觀察時間間隔期間每個查詢的 CPU (取決於彙總函式)。</span><span class="sxs-lookup"><span data-stu-id="02034-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="02034-140">每個查詢的持續時間 (取決於彙總函式)。</span><span class="sxs-lookup"><span data-stu-id="02034-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="02034-141">特定查詢的總執行次數。</span><span class="sxs-lookup"><span data-stu-id="02034-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="02034-142">使用核取方塊，選取或清除圖表要包含或排除的個別查詢。</span><span class="sxs-lookup"><span data-stu-id="02034-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span></span>
3. <span data-ttu-id="02034-143">如果您的資料過期了，請按一下 [重新整理]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="02034-143">If your data becomes stale, click the **Refresh** button.</span></span>
4. <span data-ttu-id="02034-144">您可以使用滑桿和縮放按鈕來變更觀測間隔，並調查尖峰︰![設定](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="02034-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="02034-145">(選擇性) 如果您想要不同的檢視，您可以選取 [自訂]  索引標籤，然後設定：</span><span class="sxs-lookup"><span data-stu-id="02034-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="02034-146">度量 (CPU、持續時間、執行計數)</span><span class="sxs-lookup"><span data-stu-id="02034-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="02034-147">時間間隔 (過去 24 小時、過去一週、過去一個月)。</span><span class="sxs-lookup"><span data-stu-id="02034-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="02034-148">查詢數目。</span><span class="sxs-lookup"><span data-stu-id="02034-148">Number of queries.</span></span>
   * <span data-ttu-id="02034-149">彙總函式。</span><span class="sxs-lookup"><span data-stu-id="02034-149">Aggregation function.</span></span>
     
     ![settings](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="02034-151">檢視個別查詢詳細資料</span><span class="sxs-lookup"><span data-stu-id="02034-151">Viewing individual query details</span></span>
<span data-ttu-id="02034-152">若要檢視查詢詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="02034-152">To view query details:</span></span>

1. <span data-ttu-id="02034-153">按一下排名最前面的查詢清單中的任何查詢。</span><span class="sxs-lookup"><span data-stu-id="02034-153">Click any query in the list of top queries.</span></span>
   
    ![詳細資料](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="02034-155">詳細資料檢視隨即開啟，而查詢的 CPU 取用量/持續時間/執行計數會根據時間來細分。</span><span class="sxs-lookup"><span data-stu-id="02034-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="02034-156">按一下圖表周圍以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02034-156">Click around the chart for details.</span></span>
   
   * <span data-ttu-id="02034-157">最上層圖表顯示一條含有整體資料庫 DTU % 的線條，而長條是已選取查詢所耗用的 CPU %。</span><span class="sxs-lookup"><span data-stu-id="02034-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span></span>
   * <span data-ttu-id="02034-158">第二個圖表顯示已選取查詢的總持續時間。</span><span class="sxs-lookup"><span data-stu-id="02034-158">Second chart shows total duration by the selected query.</span></span>
   * <span data-ttu-id="02034-159">底層圖表則顯示已選取查詢的執行總數。</span><span class="sxs-lookup"><span data-stu-id="02034-159">Bottom chart shows total number of executions by the selected query.</span></span>
     
     ![查詢詳細資料][3]
4. <span data-ttu-id="02034-161">(選擇性) 使用滑桿、縮放按鈕或按一下 [設定]  ，來自訂查詢資料的顯示方式或挑選不同的期間。</span><span class="sxs-lookup"><span data-stu-id="02034-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="02034-162">針對每段持續時間檢閱排名最前面的查詢</span><span class="sxs-lookup"><span data-stu-id="02034-162">Review top queries per duration</span></span>
<span data-ttu-id="02034-163">在「查詢效能深入解析」的最新查詢中，我們引進了兩個新的度量，可協助您識別潛在的瓶頸︰持續時間和執行計數。</span><span class="sxs-lookup"><span data-stu-id="02034-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="02034-164">長時間執行的查詢最有可能會鎖定資源較長的時間、封鎖其他使用者，以及限制擴充性。</span><span class="sxs-lookup"><span data-stu-id="02034-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="02034-165">它們也是最適合進行最佳化的項目。</span><span class="sxs-lookup"><span data-stu-id="02034-165">They are also the best candidates for optimization.</span></span><br>

<span data-ttu-id="02034-166">識別長時間執行的查詢：</span><span class="sxs-lookup"><span data-stu-id="02034-166">To identify long running queries:</span></span>

1. <span data-ttu-id="02034-167">針對選取的資料庫，在 [查詢效能深入解析] 中開啟 [自訂]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="02034-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="02034-168">將度量變更為 [持續時間] </span><span class="sxs-lookup"><span data-stu-id="02034-168">Change metrics to be **duration**</span></span>
3. <span data-ttu-id="02034-169">選取查詢數目和觀測間隔</span><span class="sxs-lookup"><span data-stu-id="02034-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="02034-170">選取彙總函式</span><span class="sxs-lookup"><span data-stu-id="02034-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="02034-171">**Sum** 會加總整個觀測間隔內的所有查詢執行時間。</span><span class="sxs-lookup"><span data-stu-id="02034-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="02034-172">**Max** 會尋找在整個觀測間隔內執行時間最大的查詢。</span><span class="sxs-lookup"><span data-stu-id="02034-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="02034-173">**Avg** 會尋找所有查詢執行的平均執行時間，並顯示這些平均值中排名最高者。</span><span class="sxs-lookup"><span data-stu-id="02034-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span></span> 
     
     ![查詢持續時間][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="02034-175">針對每個執行計數檢閱排名最前面的查詢</span><span class="sxs-lookup"><span data-stu-id="02034-175">Review top queries per execution count</span></span>
<span data-ttu-id="02034-176">執行數目很高可能不會影響資料庫本身且資源使用量可能很低，但整體應用程式可能會變慢。</span><span class="sxs-lookup"><span data-stu-id="02034-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="02034-177">在某些情況下，極高的執行計數可能會導致網路往返次數增加。</span><span class="sxs-lookup"><span data-stu-id="02034-177">In some cases, very high execution count may lead to increase of network round trips.</span></span> <span data-ttu-id="02034-178">往返次數會大幅影響效能。</span><span class="sxs-lookup"><span data-stu-id="02034-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="02034-179">它們會受限於網路延遲和下游伺服器延遲。</span><span class="sxs-lookup"><span data-stu-id="02034-179">They are subject to network latency and to downstream server latency.</span></span> 

<span data-ttu-id="02034-180">例如，許多資料導向的網站會針對每個使用者要求大量存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="02034-180">For example, many data-driven Web sites heavily access the database for every user request.</span></span> <span data-ttu-id="02034-181">儘管有連線集區的協助，但是資料庫伺服器上增加的網路流量和處理負載可能會對效能產生不利的影響。</span><span class="sxs-lookup"><span data-stu-id="02034-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span></span>  <span data-ttu-id="02034-182">通常會建議您將往返次數維持在絕對最小值。</span><span class="sxs-lookup"><span data-stu-id="02034-182">General advice is to keep round trips to an absolute minimum.</span></span>

<span data-ttu-id="02034-183">識別經常執行查詢 (「多對話」) 的查詢：</span><span class="sxs-lookup"><span data-stu-id="02034-183">To identify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="02034-184">針對選取的資料庫，在 [查詢效能深入解析] 中開啟 [自訂]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="02034-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="02034-185">將度量變更為 [執行計數] </span><span class="sxs-lookup"><span data-stu-id="02034-185">Change metrics to be **execution count**</span></span>
3. <span data-ttu-id="02034-186">選取查詢數目和觀測間隔</span><span class="sxs-lookup"><span data-stu-id="02034-186">Select number of queries and observation interval</span></span>
   
    ![查詢執行計數][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="02034-188">了解效能微調註解</span><span class="sxs-lookup"><span data-stu-id="02034-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="02034-189">在「查詢效能深入解析」中瀏覽您的工作負載時，您可能會注意到圖表最上方含有垂直線的圖示。</span><span class="sxs-lookup"><span data-stu-id="02034-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span></span><br>

<span data-ttu-id="02034-190">這些圖示是註解。它們代表 [SQL Azure Database 建議程式](sql-database-advisor.md)所執行會影響效能的動作。</span><span class="sxs-lookup"><span data-stu-id="02034-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="02034-191">您可以藉由停留在註解上方來取得與動作有關的基本資訊：</span><span class="sxs-lookup"><span data-stu-id="02034-191">By hovering annotation, you get basic information about the action:</span></span>

![查詢註解][6]

<span data-ttu-id="02034-193">如果您想要深入了解或套用建議程式的建議，請按一下圖示。</span><span class="sxs-lookup"><span data-stu-id="02034-193">If you want to know more or apply advisor recommendation, click the icon.</span></span> <span data-ttu-id="02034-194">隨即會開啟動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02034-194">It will open details of action.</span></span> <span data-ttu-id="02034-195">如果是有效的建議，您就能使用命令立即套用動作。</span><span class="sxs-lookup"><span data-stu-id="02034-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![查詢註解詳細資料][7]

### <a name="multiple-annotations"></a><span data-ttu-id="02034-197">多個註解。</span><span class="sxs-lookup"><span data-stu-id="02034-197">Multiple annotations.</span></span>
<span data-ttu-id="02034-198">這是可能的，由於縮放等級的緣故，使得彼此相近的註解將會摺疊成一個。</span><span class="sxs-lookup"><span data-stu-id="02034-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span></span> <span data-ttu-id="02034-199">這將會利用特殊的圖示來表示，按一下該圖示就會開啟新的刀鋒視窗，其中顯示已分組的註解清單。</span><span class="sxs-lookup"><span data-stu-id="02034-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="02034-200">使查詢和效能調整動作相互關聯，有助於深入了解您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="02034-200">Correlating queries and performance tuning actions can help to better understand your workload.</span></span> 

## <a name="optimizing-the-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="02034-201">針對查詢效能深入解析來讓查詢存放區組態最佳化</span><span class="sxs-lookup"><span data-stu-id="02034-201">Optimizing the Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="02034-202">您在使用查詢效能深入解析的期間，可能會看到下列查詢存放區訊息：</span><span class="sxs-lookup"><span data-stu-id="02034-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span></span>

* <span data-ttu-id="02034-203">「此資料庫的查詢存放區未正確設定。</span><span class="sxs-lookup"><span data-stu-id="02034-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="02034-204">請按一下這裡深入了解。」</span><span class="sxs-lookup"><span data-stu-id="02034-204">Click here to learn more."</span></span>
* <span data-ttu-id="02034-205">「此資料庫的查詢存放區未正確設定。</span><span class="sxs-lookup"><span data-stu-id="02034-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="02034-206">請按一下這裡變更設定。」</span><span class="sxs-lookup"><span data-stu-id="02034-206">Click here to change settings."</span></span> 

<span data-ttu-id="02034-207">這些訊息通常會在查詢存放區無法收集新資料時出現。</span><span class="sxs-lookup"><span data-stu-id="02034-207">These messages usually appear when Query Store is not able to collect new data.</span></span> 

<span data-ttu-id="02034-208">當查詢存放區處於唯讀狀態且以最佳方式設定參數時，就會發生第一種狀況。</span><span class="sxs-lookup"><span data-stu-id="02034-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="02034-209">您可以藉由增加查詢存放區的大小，或清除查詢存放區來修正此問題。</span><span class="sxs-lookup"><span data-stu-id="02034-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![qds 按鈕][8]

<span data-ttu-id="02034-211">當查詢存放區已關閉或參數並不是以最佳方式所設定時，就會發生第二種狀況。</span><span class="sxs-lookup"><span data-stu-id="02034-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="02034-212">您可以執行下列命令或直接從入口網站，變更保留期和擷取原則並啟用查詢存放區：</span><span class="sxs-lookup"><span data-stu-id="02034-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![qds 按鈕][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="02034-214">建議使用的保留期和擷取原則</span><span class="sxs-lookup"><span data-stu-id="02034-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="02034-215">保留期原則有兩種：</span><span class="sxs-lookup"><span data-stu-id="02034-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="02034-216">容量大小式：設定為 [AUTO] 時，該原則會在收集的資料量接近容量上限時，自動清除資料。</span><span class="sxs-lookup"><span data-stu-id="02034-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="02034-217">時間式：預設設定為 30 天，這代表當查詢存放區的空間用完時，就會刪除 30 天之前的查詢資訊</span><span class="sxs-lookup"><span data-stu-id="02034-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="02034-218">擷取原則可以設定為：</span><span class="sxs-lookup"><span data-stu-id="02034-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="02034-219">**All**：擷取所有的查詢。</span><span class="sxs-lookup"><span data-stu-id="02034-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="02034-220">**Auto**：會忽略不常執行的查詢，以及編譯和執行持續時間微不足道的查詢。</span><span class="sxs-lookup"><span data-stu-id="02034-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="02034-221">執行次數、編譯及執行階段持續時間的臨界值是由內部決定的。</span><span class="sxs-lookup"><span data-stu-id="02034-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="02034-222">這是預設選項。</span><span class="sxs-lookup"><span data-stu-id="02034-222">This is the default option.</span></span>
* <span data-ttu-id="02034-223">**None**：「查詢存放區」會停止擷取新的查詢，不過仍然會收集已擷取查詢的執行階段統計資料。</span><span class="sxs-lookup"><span data-stu-id="02034-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="02034-224">我們建議您將所有原則設定為 [AUTO]，並將清除原則設定為 30 天：</span><span class="sxs-lookup"><span data-stu-id="02034-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="02034-225">增加查詢存放區的大小，</span><span class="sxs-lookup"><span data-stu-id="02034-225">Increase size of Query Store.</span></span> <span data-ttu-id="02034-226">方法是連線至資料庫，然後發出下列查詢：</span><span class="sxs-lookup"><span data-stu-id="02034-226">This could be performed by connecting to a database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="02034-227">套用這些設定，最終會使查詢存放區收集新的查詢，不過，如果您不想等待，可以清除查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="02034-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="02034-228">執行下列查詢將會刪除查詢存放區中所有目前的資訊。</span><span class="sxs-lookup"><span data-stu-id="02034-228">Executing following query will delete all current information in the Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="02034-229">摘要</span><span class="sxs-lookup"><span data-stu-id="02034-229">Summary</span></span>
<span data-ttu-id="02034-230">「查詢效能深入解析」可協助您了解您的查詢工作負載的影響，以及其與資料庫資源取用量的關係。</span><span class="sxs-lookup"><span data-stu-id="02034-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span></span> <span data-ttu-id="02034-231">使用此功能，您將了解排名最前面的取用查詢，並且在發生問題前輕鬆地找出要修正的項目。</span><span class="sxs-lookup"><span data-stu-id="02034-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02034-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02034-232">Next steps</span></span>
<span data-ttu-id="02034-233">如需有關改善 SQL Database 效能的其他建議，請按一下 [查詢效能深入解析] 刀鋒視窗上的 [建議](sql-database-advisor.md)。</span><span class="sxs-lookup"><span data-stu-id="02034-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span></span>

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

