---
title: "針對效能問題進行疑難排解並將資料庫最佳化 | Microsoft Docs"
description: "對 SQL Database 套用效能建議以及了解如何獲得對資料庫執行之查詢效能的深入解析"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: f9ae96cdc80c347593f229cb2fce3f2d4d8e7caf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="46b0e-103">針對效能問題進行疑難排解並將資料庫最佳化</span><span class="sxs-lookup"><span data-stu-id="46b0e-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="46b0e-104">遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。</span><span class="sxs-lookup"><span data-stu-id="46b0e-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="46b0e-105">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="46b0e-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="46b0e-106">檢閱、套用和還原效能改進建議</span><span class="sxs-lookup"><span data-stu-id="46b0e-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="46b0e-107">尋找具有高資源使用率的查詢</span><span class="sxs-lookup"><span data-stu-id="46b0e-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="46b0e-108">尋找長時間執行的查詢</span><span class="sxs-lookup"><span data-stu-id="46b0e-108">Find long running queries</span></span>

> <span data-ttu-id="46b0e-109">您必須對發生效能問題 (例如，遺漏索引) 的資料庫進行連續的工作負載，才能獲得建議。</span><span class="sxs-lookup"><span data-stu-id="46b0e-109">You need a continuous workload on a database with performance issues – missing an index for example to receive a recommendation.</span></span>
>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="46b0e-110">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="46b0e-110">Log in to the Azure portal</span></span>

<span data-ttu-id="46b0e-111">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="46b0e-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="46b0e-112">檢閱並套用建議</span><span class="sxs-lookup"><span data-stu-id="46b0e-112">Review and apply a recommendation</span></span>

<span data-ttu-id="46b0e-113">遵循下列步驟來套用系統對資料庫所提出的建議︰</span><span class="sxs-lookup"><span data-stu-id="46b0e-113">Follow these steps to apply a recommendation from the system for your database:</span></span>

1. <span data-ttu-id="46b0e-114">按一下資料庫刀鋒視窗中的 [效能建議] 功能表。</span><span class="sxs-lookup"><span data-stu-id="46b0e-114">Click the **Performance recommendations** menu in the database blade.</span></span>

    ![效能建議](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="46b0e-116">從建議清單中，選取作用中的建議。</span><span class="sxs-lookup"><span data-stu-id="46b0e-116">From the list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="46b0e-117">在此範例中是「建立索引」。</span><span class="sxs-lookup"><span data-stu-id="46b0e-117">In this example, Create Index.</span></span>

    ![選取建議](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="46b0e-119">按一下 [套用] 按鈕來套用建議。</span><span class="sxs-lookup"><span data-stu-id="46b0e-119">Apply the recommendation by clicking the **Apply** button.</span></span> <span data-ttu-id="46b0e-120">(選擇性) 檢閱建議的詳細資料，然後按一下 [檢視指令碼] 按鈕來查看要執行的 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="46b0e-120">Optionally, review the recommendation details and see the T-SQL script to  be executed by clicking on **View Script** button.</span></span>

    ![套用建議](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="46b0e-122">[選擇性] 啟用自動調整以讓系統自動套用建議。</span><span class="sxs-lookup"><span data-stu-id="46b0e-122">[Optional] Enable automatic tuning for recommendations to be applied automatically.</span></span>

    ![自動調整](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="46b0e-124">還原建議</span><span class="sxs-lookup"><span data-stu-id="46b0e-124">Revert a recommendation</span></span>

<span data-ttu-id="46b0e-125">Database Advisor 會監視系統所實作的每項建議。</span><span class="sxs-lookup"><span data-stu-id="46b0e-125">The Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="46b0e-126">如果某項建議無法改善工作負載，系統就會自動將該項建議還原。</span><span class="sxs-lookup"><span data-stu-id="46b0e-126">If a recommendation doesn't improve the workload it will be automatically reverted.</span></span> <span data-ttu-id="46b0e-127">您可以手動還原建議，但大部分情況下並不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="46b0e-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="46b0e-128">若要還原建議：</span><span class="sxs-lookup"><span data-stu-id="46b0e-128">To revert a recommendation:</span></span>

1. <span data-ttu-id="46b0e-129">移至效能建議功能表，然後選取其中一項已套用的建議。</span><span class="sxs-lookup"><span data-stu-id="46b0e-129">Go to the performance recommendations menu and select one of the applied recommendations.</span></span>

    ![選取建議](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="46b0e-131">在詳細資料檢視中，按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="46b0e-131">In the details view, click **Revert**.</span></span>

    ![還原建議](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-the-query-that-consumes-the-most-resources"></a><span data-ttu-id="46b0e-133">尋找耗用最多資源的查詢</span><span class="sxs-lookup"><span data-stu-id="46b0e-133">Find the query that consumes the most resources</span></span>

<span data-ttu-id="46b0e-134">請遵循下列步驟來尋找耗用最多資源的查詢︰</span><span class="sxs-lookup"><span data-stu-id="46b0e-134">Follow these steps to find the query consuming the most resources:</span></span>

1. <span data-ttu-id="46b0e-135">按一下資料庫刀鋒視窗中的 [查詢效能深入解析] 功能表。</span><span class="sxs-lookup"><span data-stu-id="46b0e-135">Click on the **Query Performance Insight** menu in the database blade.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="46b0e-137">選取資源類型。</span><span class="sxs-lookup"><span data-stu-id="46b0e-137">Select a resource type.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="46b0e-139">選取資料表中的第一個查詢。</span><span class="sxs-lookup"><span data-stu-id="46b0e-139">Select the first query in the table.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="46b0e-141">檢閱查詢詳細資料。</span><span class="sxs-lookup"><span data-stu-id="46b0e-141">Review the query details.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-the-longest-running-query"></a><span data-ttu-id="46b0e-143">尋找執行最久的查詢</span><span class="sxs-lookup"><span data-stu-id="46b0e-143">Find the longest running query</span></span>

1. <span data-ttu-id="46b0e-144">移至 [查詢效能深入解析]，然後選取 [長時間執行的查詢] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="46b0e-144">Go to Query Performance Insight and select the **Long running queries** tab.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="46b0e-146">選取資料表中的第一個查詢。</span><span class="sxs-lookup"><span data-stu-id="46b0e-146">Select the first query in the table.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="46b0e-148">檢閱查詢詳細資料。</span><span class="sxs-lookup"><span data-stu-id="46b0e-148">Review the query details.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="46b0e-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46b0e-150">Next steps</span></span> 
<span data-ttu-id="46b0e-151">遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。</span><span class="sxs-lookup"><span data-stu-id="46b0e-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="46b0e-152">在本教學課程中，您已了解：</span><span class="sxs-lookup"><span data-stu-id="46b0e-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="46b0e-153">檢閱、套用和還原效能改進建議</span><span class="sxs-lookup"><span data-stu-id="46b0e-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="46b0e-154">尋找具有高資源使用率的查詢</span><span class="sxs-lookup"><span data-stu-id="46b0e-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="46b0e-155">尋找長時間執行的查詢</span><span class="sxs-lookup"><span data-stu-id="46b0e-155">Find long running queries</span></span>

[<span data-ttu-id="46b0e-156">SQL Database 效能調整秘訣</span><span class="sxs-lookup"><span data-stu-id="46b0e-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
