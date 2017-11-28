---
title: "監視並改善效能 - Azure SQL Database | Microsoft Docs"
description: "Azure SQL Database 會提供可協助您找出可改善目前查詢效能區域的效能工具。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 522b932ab055978c52f085dbaa36095bb6b77962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="14590-103">監視並改善效能</span><span class="sxs-lookup"><span data-stu-id="14590-103">Monitor and improve performance</span></span>
<span data-ttu-id="14590-104">Azure SQL Database 可找出資料庫中的潛在問題，並透過提供智慧型微調動作和建議來建議可以改善工作負載效能的動作。</span><span class="sxs-lookup"><span data-stu-id="14590-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="14590-105">若要檢閱您的資料庫效能，請使用 [概觀] 頁面上的 [效能] 圖格，或往下瀏覽到 [支援 + 疑難排解] 區段：</span><span class="sxs-lookup"><span data-stu-id="14590-105">To review your database performance, use the **Performance** tile on the Overview page, or navigate down to "Support + troubleshooting" section:</span></span>

   ![檢視效能](./media/sql-database-performance/entries.png)

<span data-ttu-id="14590-107">在 [支援 + 疑難排解] 區段中，您可以使用下列頁面：</span><span class="sxs-lookup"><span data-stu-id="14590-107">In the "Support + troubleshooting" section, you can use the following pages:</span></span>


1. <span data-ttu-id="14590-108">[效能概觀](#performance-overview)可以監視資料庫的效能。</span><span class="sxs-lookup"><span data-stu-id="14590-108">[Performance overview](#performance-overview) to monitor performance of your database.</span></span> 
2. <span data-ttu-id="14590-109">[效能建議](#performance-recommendations)可以找到能改善工作負載效能的效能建議。</span><span class="sxs-lookup"><span data-stu-id="14590-109">[Performance recommendations](#performance-recommendations) to find performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="14590-110">[查詢效能深入解析](#query-performance-insight)可以找到排名最前面的資源取用查詢。</span><span class="sxs-lookup"><span data-stu-id="14590-110">[Query Performance Insight](#query-performance-insight) to find top resource consuming queries.</span></span>
4. <span data-ttu-id="14590-111">[自動調整](#automatic-tuning)可以讓 Azure SQL Database 自動將資料庫最佳化。</span><span class="sxs-lookup"><span data-stu-id="14590-111">[Automatic tuning](#automatic-tuning) to let Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="14590-112">效能概觀</span><span class="sxs-lookup"><span data-stu-id="14590-112">Performance Overview</span></span>
<span data-ttu-id="14590-113">此檢視會提供您的資料庫效能的摘要，並可協助您進行效能調整和疑難排解。</span><span class="sxs-lookup"><span data-stu-id="14590-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![效能](./media/sql-database-performance/performance.png)

* <span data-ttu-id="14590-115">[建議] 圖格會提供適用於資料庫的微調建議分解 (如果有多個建議，則會顯示前三個)。</span><span class="sxs-lookup"><span data-stu-id="14590-115">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="14590-116">按一下此圖格，即會帶您前往 [[效能建議](#performance-recommendations)]。</span><span class="sxs-lookup"><span data-stu-id="14590-116">Clicking this tile takes you to **[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="14590-117">[微調活動]  圖格會提供資料庫進行中和已完成微調動作的摘要，讓您快速檢視調整活動的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="14590-117">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="14590-118">按一下此圖格會帶您前往您的資料庫的完整微調記錄檢視。</span><span class="sxs-lookup"><span data-stu-id="14590-118">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="14590-119">[自動調整] 圖格會顯示資料庫的[自動調整設定](sql-database-automatic-tuning-enable.md) (自動套用至資料庫的微調選項)。</span><span class="sxs-lookup"><span data-stu-id="14590-119">The **Auto-tuning** tile shows the [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied to your database).</span></span> <span data-ttu-id="14590-120">按一下此圖格會開啟 [自動化組態] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="14590-120">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="14590-121">[資料庫查詢] 圖格會顯示資料庫的查詢效能摘要 (整體 DTU 使用量和排名最前面的資源取用查詢)。</span><span class="sxs-lookup"><span data-stu-id="14590-121">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="14590-122">按一下此圖格，即會帶您前往 [[查詢效能深入解析](#query-performance-insight)]。</span><span class="sxs-lookup"><span data-stu-id="14590-122">Clicking this tile takes you to **[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="14590-123">效能建議</span><span class="sxs-lookup"><span data-stu-id="14590-123">Performance recommendations</span></span>
<span data-ttu-id="14590-124">此頁面提供可改善資料庫效能的智慧型[微調建議](sql-database-advisor.md)。</span><span class="sxs-lookup"><span data-stu-id="14590-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="14590-125">此頁面上顯示的建議類型如下：</span><span class="sxs-lookup"><span data-stu-id="14590-125">The following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="14590-126">要建立或卸除哪些索引的建議。</span><span class="sxs-lookup"><span data-stu-id="14590-126">Recommendations on which indexes to create or drop.</span></span>
* <span data-ttu-id="14590-127">在資料庫中發現結構描述問題時的建議。</span><span class="sxs-lookup"><span data-stu-id="14590-127">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="14590-128">當查詢可以受益於參數化查詢時的建議。</span><span class="sxs-lookup"><span data-stu-id="14590-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![效能](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="14590-130">您也可以找到過去所套用微調動作的完整歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="14590-130">You can also find complete history of tuning actions that were applied in the past.</span></span>

<span data-ttu-id="14590-131">在[尋找和套用效能建議](sql-database-advisor-portal.md)文章中，了解如何找到和套用效能建議。</span><span class="sxs-lookup"><span data-stu-id="14590-131">Learn how to find an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="14590-132">自動微調</span><span class="sxs-lookup"><span data-stu-id="14590-132">Automatic tuning</span></span>
<span data-ttu-id="14590-133">Azure SQL Databases 能透過套用[效能建議](sql-database-advisor.md)來自動微調資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="14590-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="14590-134">若要深入了解，請參閱[自動調整文章](sql-database-automatic-tuning.md)。</span><span class="sxs-lookup"><span data-stu-id="14590-134">To learn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="14590-135">若要啟用它，請參閱[如何啟用自動調整](sql-database-automatic-tuning-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="14590-135">To enable it, read [how to enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="14590-136">查詢效能深入解析</span><span class="sxs-lookup"><span data-stu-id="14590-136">Query Performance Insight</span></span>
<span data-ttu-id="14590-137">[查詢效能深入解析](sql-database-query-performance.md) 提供了下列各項，讓您得以花費較少的時間來針對資料庫效能進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="14590-137">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="14590-138">更深入的資料庫資源 (DTU) 取用分析。</span><span class="sxs-lookup"><span data-stu-id="14590-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="14590-139">排名最前面的 CPU 取用查詢，進行微調有可能會改善效能。</span><span class="sxs-lookup"><span data-stu-id="14590-139">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="14590-140">向下鑽研查詢詳細資料的功能。</span><span class="sxs-lookup"><span data-stu-id="14590-140">The ability to drill down into the details of a query.</span></span> 

  ![效能儀表板](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="14590-142">如需此頁面的詳細資訊，可在**[如何使用查詢效能深入解析](sql-database-query-performance.md)**一文中找到。</span><span class="sxs-lookup"><span data-stu-id="14590-142">Find more information about this page in the article **[How to use Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14590-143">其他資源</span><span class="sxs-lookup"><span data-stu-id="14590-143">Additional resources</span></span>
* [<span data-ttu-id="14590-144">單一資料庫的 Azure SQL Database 效能指引</span><span class="sxs-lookup"><span data-stu-id="14590-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="14590-145">何時使用彈性集區？</span><span class="sxs-lookup"><span data-stu-id="14590-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

