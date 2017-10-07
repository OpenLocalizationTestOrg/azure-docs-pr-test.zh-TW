---
title: "aaaTroubleshoot 效能問題，並最佳化您的資料庫 |Microsoft 文件"
description: "適用於效能建議 tooyour SQL 資料庫，以及上清除 toogain 深入了解如何 hello hello 查詢您的資料庫上執行的效能。"
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
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="12c3b-103">針對效能問題進行疑難排解並將資料庫最佳化</span><span class="sxs-lookup"><span data-stu-id="12c3b-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="12c3b-104">遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。</span><span class="sxs-lookup"><span data-stu-id="12c3b-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="12c3b-105">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="12c3b-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="12c3b-106">檢閱、套用和還原效能改進建議</span><span class="sxs-lookup"><span data-stu-id="12c3b-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="12c3b-107">尋找具有高資源使用率的查詢</span><span class="sxs-lookup"><span data-stu-id="12c3b-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="12c3b-108">尋找長時間執行的查詢</span><span class="sxs-lookup"><span data-stu-id="12c3b-108">Find long running queries</span></span>

> <span data-ttu-id="12c3b-109">您需要連續的工作負載效能問題 – 遺漏索引，例如 tooreceive 建議使用的資料庫上。</span><span class="sxs-lookup"><span data-stu-id="12c3b-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="12c3b-110">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="12c3b-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="12c3b-111">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="12c3b-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="12c3b-112">檢閱並套用建議</span><span class="sxs-lookup"><span data-stu-id="12c3b-112">Review and apply a recommendation</span></span>

<span data-ttu-id="12c3b-113">從 hello 系統為您的資料庫，請遵循這些步驟 tooapply 建議：</span><span class="sxs-lookup"><span data-stu-id="12c3b-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="12c3b-114">按一下 hello**效能建議**hello 資料庫刀鋒視窗中的功能表。</span><span class="sxs-lookup"><span data-stu-id="12c3b-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![效能建議](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="12c3b-116">從 hello 的建議清單，選取 使用中的建議。</span><span class="sxs-lookup"><span data-stu-id="12c3b-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="12c3b-117">在此範例中是「建立索引」。</span><span class="sxs-lookup"><span data-stu-id="12c3b-117">In this example, Create Index.</span></span>

    ![選取建議](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="12c3b-119">按一下 hello 套用 hello 建議**套用** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12c3b-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="12c3b-120">（選擇性） 檢閱 hello 建議詳細資料，並查看 hello T-SQL 指令碼太執行上的 [**檢視指令碼**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12c3b-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![套用建議](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="12c3b-122">[選用]啟用自動微調建議 toobe 自動套用。</span><span class="sxs-lookup"><span data-stu-id="12c3b-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![自動調整](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="12c3b-124">還原建議</span><span class="sxs-lookup"><span data-stu-id="12c3b-124">Revert a recommendation</span></span>

<span data-ttu-id="12c3b-125">hello Database Advisor 監視實作的每個建議。</span><span class="sxs-lookup"><span data-stu-id="12c3b-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="12c3b-126">如果建議未能改善 hello 工作負載將會自動還原。</span><span class="sxs-lookup"><span data-stu-id="12c3b-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="12c3b-127">您可以手動還原建議，但大部分情況下並不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="12c3b-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="12c3b-128">toorevert 建議：</span><span class="sxs-lookup"><span data-stu-id="12c3b-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="12c3b-129">移 toohello 效能建議功能表，然後選取其中一個 hello 套用建議事項。</span><span class="sxs-lookup"><span data-stu-id="12c3b-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![選取建議](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="12c3b-131">在 hello 詳細資料檢視中，按一下  **Revert**。</span><span class="sxs-lookup"><span data-stu-id="12c3b-131">In hello details view, click **Revert**.</span></span>

    ![還原建議](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="12c3b-133">尋找取用 hello hello 查詢最多資源</span><span class="sxs-lookup"><span data-stu-id="12c3b-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="12c3b-134">請依照下列耗用 hello 這些步驟 toofind hello 查詢最多資源：</span><span class="sxs-lookup"><span data-stu-id="12c3b-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="12c3b-135">按一下 hello**查詢效能深入解析**hello 資料庫刀鋒視窗中的功能表。</span><span class="sxs-lookup"><span data-stu-id="12c3b-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="12c3b-137">選取資源類型。</span><span class="sxs-lookup"><span data-stu-id="12c3b-137">Select a resource type.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="12c3b-139">選取 hello hello 資料表中的第一個查詢。</span><span class="sxs-lookup"><span data-stu-id="12c3b-139">Select hello first query in hello table.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="12c3b-141">檢閱 hello 查詢詳細資料。</span><span class="sxs-lookup"><span data-stu-id="12c3b-141">Review hello query details.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="12c3b-143">尋找 hello 最長執行的查詢</span><span class="sxs-lookup"><span data-stu-id="12c3b-143">Find hello longest running query</span></span>

1. <span data-ttu-id="12c3b-144">移 tooQuery 效能深入解析，然後選取 hello**長時間執行的查詢** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="12c3b-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="12c3b-146">選取 hello hello 資料表中的第一個查詢。</span><span class="sxs-lookup"><span data-stu-id="12c3b-146">Select hello first query in hello table.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="12c3b-148">檢閱 hello 查詢詳細資料。</span><span class="sxs-lookup"><span data-stu-id="12c3b-148">Review hello query details.</span></span>

    ![查詢深入解析](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="12c3b-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12c3b-150">Next steps</span></span> 
<span data-ttu-id="12c3b-151">遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。</span><span class="sxs-lookup"><span data-stu-id="12c3b-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="12c3b-152">在本教學課程中，您已了解：</span><span class="sxs-lookup"><span data-stu-id="12c3b-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="12c3b-153">檢閱、套用和還原效能改進建議</span><span class="sxs-lookup"><span data-stu-id="12c3b-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="12c3b-154">尋找具有高資源使用率的查詢</span><span class="sxs-lookup"><span data-stu-id="12c3b-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="12c3b-155">尋找長時間執行的查詢</span><span class="sxs-lookup"><span data-stu-id="12c3b-155">Find long running queries</span></span>

[<span data-ttu-id="12c3b-156">SQL Database 效能調整秘訣</span><span class="sxs-lookup"><span data-stu-id="12c3b-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
