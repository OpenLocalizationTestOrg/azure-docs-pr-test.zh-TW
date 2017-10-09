---
title: "aaaMonitor 並改善效能-Azure SQL Database |Microsoft 文件"
description: "hello Azure SQL Database 提供效能工具 toohelp 識別可改善目前的查詢效能的區域。"
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
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="95d85-103">監視並改善效能</span><span class="sxs-lookup"><span data-stu-id="95d85-103">Monitor and improve performance</span></span>
<span data-ttu-id="95d85-104">Azure SQL Database 可找出資料庫中的潛在問題，並透過提供智慧型微調動作和建議來建議可以改善工作負載效能的動作。</span><span class="sxs-lookup"><span data-stu-id="95d85-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="95d85-105">tooreview 您的資料庫效能、 使用 hello**效能**hello 概觀 頁面上的磚或向下巡覽太"支援 + 疑難排解 」 一節：</span><span class="sxs-lookup"><span data-stu-id="95d85-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![檢視效能](./media/sql-database-performance/entries.png)

<span data-ttu-id="95d85-107">在 hello"支援 + 疑難排解"區段中，您可以使用 hello 下列頁面：</span><span class="sxs-lookup"><span data-stu-id="95d85-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="95d85-108">[效能概觀](#performance-overview)toomonitor 對資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="95d85-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="95d85-109">[效能建議](#performance-recommendations)toofind 效能的建議可改善您的工作負載的效能。</span><span class="sxs-lookup"><span data-stu-id="95d85-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="95d85-110">[查詢效能深入解析](#query-performance-insight)toofind 熱門資源取用查詢。</span><span class="sxs-lookup"><span data-stu-id="95d85-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="95d85-111">[自動調整](#automatic-tuning)toolet Azure SQL Database 會自動最佳化您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="95d85-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="95d85-112">效能概觀</span><span class="sxs-lookup"><span data-stu-id="95d85-112">Performance Overview</span></span>
<span data-ttu-id="95d85-113">此檢視會提供您的資料庫效能的摘要，並可協助您進行效能調整和疑難排解。</span><span class="sxs-lookup"><span data-stu-id="95d85-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![效能](./media/sql-database-performance/performance.png)

* <span data-ttu-id="95d85-115">hello**建議**磚提供的微調建議，以您的資料庫分析 （前三個建議會顯示是否有更多）。</span><span class="sxs-lookup"><span data-stu-id="95d85-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="95d85-116">按一下此磚會帶您太**[效能建議](#performance-recommendations)**。</span><span class="sxs-lookup"><span data-stu-id="95d85-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="95d85-117">hello**微調活動**磚提供 hello 持續和已完成微調您資料庫的動作，讓您快速檢視的微調活動 hello 歷程記錄的摘要。</span><span class="sxs-lookup"><span data-stu-id="95d85-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="95d85-118">按一下此磚會帶您 toohello 完整微調您資料庫的歷程記錄檢視。</span><span class="sxs-lookup"><span data-stu-id="95d85-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="95d85-119">hello**自動調整**磚會顯示 hello[自動調整設定](sql-database-automatic-tuning-enable.md)資料庫 （微調選項會自動套用的 tooyour 資料庫）。</span><span class="sxs-lookup"><span data-stu-id="95d85-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="95d85-120">按一下此磚會開啟 hello 自動化組態對話方塊。</span><span class="sxs-lookup"><span data-stu-id="95d85-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="95d85-121">hello**資料庫查詢**磚會顯示 hello hello 查詢效能，為您的資料庫 （整體 DTU 使用量和 top 的資源取用查詢） 的摘要。</span><span class="sxs-lookup"><span data-stu-id="95d85-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="95d85-122">按一下此磚會帶您太**[查詢效能深入解析](#query-performance-insight)**。</span><span class="sxs-lookup"><span data-stu-id="95d85-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="95d85-123">效能建議</span><span class="sxs-lookup"><span data-stu-id="95d85-123">Performance recommendations</span></span>
<span data-ttu-id="95d85-124">此頁面提供可改善資料庫效能的智慧型[微調建議](sql-database-advisor.md)。</span><span class="sxs-lookup"><span data-stu-id="95d85-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="95d85-125">hello 下列類型的建議會顯示此頁面上：</span><span class="sxs-lookup"><span data-stu-id="95d85-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="95d85-126">建議的索引 toocreate 或卸除。</span><span class="sxs-lookup"><span data-stu-id="95d85-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="95d85-127">當 hello 資料庫中所識別的結構描述問題的建議。</span><span class="sxs-lookup"><span data-stu-id="95d85-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="95d85-128">當查詢可以受益於參數化查詢時的建議。</span><span class="sxs-lookup"><span data-stu-id="95d85-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![效能](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="95d85-130">您也可以找到完整的歷程記錄的微調 hello 過去在已套用的動作。</span><span class="sxs-lookup"><span data-stu-id="95d85-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="95d85-131">深入了解如何 toofind apply 效能建議[尋找並套用效能建議](sql-database-advisor-portal.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="95d85-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="95d85-132">自動微調</span><span class="sxs-lookup"><span data-stu-id="95d85-132">Automatic tuning</span></span>
<span data-ttu-id="95d85-133">Azure SQL Databases 能透過套用[效能建議](sql-database-advisor.md)來自動微調資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="95d85-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="95d85-134">詳細資訊，讀取 toolearn[自動調整的發行項](sql-database-automatic-tuning.md)。</span><span class="sxs-lookup"><span data-stu-id="95d85-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="95d85-135">讀取 tooenable[如何 tooenable 自動微調](sql-database-automatic-tuning-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="95d85-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="95d85-136">查詢效能深入解析</span><span class="sxs-lookup"><span data-stu-id="95d85-136">Query Performance Insight</span></span>
<span data-ttu-id="95d85-137">[查詢效能深入解析](sql-database-query-performance.md)可讓您 toospend 疑難排解資料庫效能所提供的時間：</span><span class="sxs-lookup"><span data-stu-id="95d85-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="95d85-138">更深入的資料庫資源 (DTU) 取用分析。</span><span class="sxs-lookup"><span data-stu-id="95d85-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="95d85-139">hello cpu 使用量最大可能會改善效能進行微調的查詢。</span><span class="sxs-lookup"><span data-stu-id="95d85-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="95d85-140">向下的能力 toodrill hello 到 hello 詳細資料的查詢中。</span><span class="sxs-lookup"><span data-stu-id="95d85-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![效能儀表板](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="95d85-142">Hello 文件中找到此頁面的詳細資訊**[如何 toouse 查詢效能深入解析](sql-database-query-performance.md)**。</span><span class="sxs-lookup"><span data-stu-id="95d85-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="95d85-143">其他資源</span><span class="sxs-lookup"><span data-stu-id="95d85-143">Additional resources</span></span>
* [<span data-ttu-id="95d85-144">單一資料庫的 Azure SQL Database 效能指引</span><span class="sxs-lookup"><span data-stu-id="95d85-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="95d85-145">何時使用彈性集區？</span><span class="sxs-lookup"><span data-stu-id="95d85-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

