---
title: "監視和效能微調 - Azure SQL Database | Microsoft Docs"
description: "透過評估和改進來調整 Azure SQL Database 效能的秘訣。"
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: "sql 效能調整，資料庫效能調整，sql 效能調整秘訣，sql 資料庫效能調整"
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 7a2f1199a56e0bd32eafef9f420879c756673e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-and-performance-tuning"></a><span data-ttu-id="b44e8-104">監視和效能微調</span><span class="sxs-lookup"><span data-stu-id="b44e8-104">Monitoring and performance tuning</span></span>

<span data-ttu-id="b44e8-105">Azure SQL Database 是自動管理和彈性的資料服務，您可以輕鬆監視使用狀況、新增或移除資源 (CPU、資源、IO)、尋找可改善資料庫效能的建議，或讓資料庫調整您的工作負載並自動最佳化效能。</span><span class="sxs-lookup"><span data-stu-id="b44e8-105">Azure SQL Database is automatically managed and flexible data service where you can easily monitor usage, add or remove resources (CPU, memory, io), find recommendations that can improve performance of your database, or let database adapt to your workload and automatically optimize performance.</span></span>

<span data-ttu-id="b44e8-106">本文提供 Azure SQL Database 中可用的監視和效能微調選項概觀。</span><span class="sxs-lookup"><span data-stu-id="b44e8-106">This article provides overview of monitoring and performance tuning options that are available in Azure SQL Database.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a><span data-ttu-id="b44e8-107">針對資料庫效能進行監視和疑難排解</span><span class="sxs-lookup"><span data-stu-id="b44e8-107">Monitoring and troubleshooting database performance</span></span>

<span data-ttu-id="b44e8-108">Azure SQL Database 可讓您輕鬆地監視資料庫使用量並找出可能造成效能問題的查詢。</span><span class="sxs-lookup"><span data-stu-id="b44e8-108">Azure SQL Database enables you to easily monitor your database usage and identify queries that might cause the performance issues.</span></span> <span data-ttu-id="b44e8-109">您可以使用 Azure 入口網站或系統檢視來監視資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="b44e8-109">You can monitor database performance using Azure portal or system views.</span></span> <span data-ttu-id="b44e8-110">您有下列選項可以用來針對資料庫效能進行監視和疑難排解：</span><span class="sxs-lookup"><span data-stu-id="b44e8-110">You have the following options for monitoring and troubleshooting database performance:</span></span>

1. <span data-ttu-id="b44e8-111">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [SQL Database]、選取資料庫，然後使用監視圖表尋找接近其上限的資源。</span><span class="sxs-lookup"><span data-stu-id="b44e8-111">In the [Azure portal](https://portal.azure.com), click **SQL databases**, select the database, and then use the Monitoring chart to look for resources approaching their maximum.</span></span> <span data-ttu-id="b44e8-112">預設會顯示 DTU 耗用量。</span><span class="sxs-lookup"><span data-stu-id="b44e8-112">DTU consumption is shown by default.</span></span> <span data-ttu-id="b44e8-113">按一下 [編輯]  來變更所顯示的時間範圍和值。</span><span class="sxs-lookup"><span data-stu-id="b44e8-113">Click **Edit** to change the time range and values shown.</span></span>
2. <span data-ttu-id="b44e8-114">使用[查詢效能深入解析](sql-database-query-performance.md)來找出花費最多資源的查詢。</span><span class="sxs-lookup"><span data-stu-id="b44e8-114">Use [Query Performance Insight](sql-database-query-performance.md) to identify the queries that spend the most of resources.</span></span>
3. <span data-ttu-id="b44e8-115">您可以使用動態管理檢視 (DMV)、擴充的事件 (`XEvents`) 和 SSMS 中的查詢存放區即時取得效能參數。</span><span class="sxs-lookup"><span data-stu-id="b44e8-115">You can use dynamic management views (DMVs), Extended Events (`XEvents`), and the Query Store in SSMS to get performance parameters in real time.</span></span>

<span data-ttu-id="b44e8-116">如果您使用這些報告或檢視發現某些問題，請參閱[效能指引主題](sql-database-performance-guidance.md)來尋找可用來改善 Azure SQL Database 效能的技巧。</span><span class="sxs-lookup"><span data-stu-id="b44e8-116">See the [performance guidance topic](sql-database-performance-guidance.md) to find techniques that you can use to improve performance of Azure SQL Database if you identify some issue using these reports or views.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b44e8-117">建議您一律使用最新版本的 Management Studio 保持與 Microsoft Azure 及 SQL Database 更新同步。</span><span class="sxs-lookup"><span data-stu-id="b44e8-117">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="b44e8-118">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b44e8-118">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
>

## <a name="optimize-database-to-improve-performance"></a><span data-ttu-id="b44e8-119">最佳化要改進效能的資料庫</span><span class="sxs-lookup"><span data-stu-id="b44e8-119">Optimize database to improve performance</span></span>

<span data-ttu-id="b44e8-120">Azure SQL Database 可讓您檢閱[效能微調建議](sql-database-advisor.md)，找出不必變更資源卻能改善和最佳化查詢效能的機會。</span><span class="sxs-lookup"><span data-stu-id="b44e8-120">Azure SQL Database enables you to identify opportunities to improve and optimize query performance without changing resources by reviewing [performance tuning recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="b44e8-121">遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。</span><span class="sxs-lookup"><span data-stu-id="b44e8-121">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b44e8-122">您可以套用這些調整建議來改善工作負載的效能。</span><span class="sxs-lookup"><span data-stu-id="b44e8-122">You can apply these tuning recommendations to improve performance of your workload.</span></span>
<span data-ttu-id="b44e8-123">您也可以套用所有發現的建議並驗證能否改善資料庫效能，讓 Azure SQL Database [自動最佳化查詢](sql-database-automatic-tuning.md)。</span><span class="sxs-lookup"><span data-stu-id="b44e8-123">You can also let Azure SQL database to [automatically optimize performance of your queries](sql-database-automatic-tuning.md) by applying all identified recommendations and verifying that they improve database performance.</span></span> <span data-ttu-id="b44e8-124">您可以使用下列選項來改善資料庫效能：</span><span class="sxs-lookup"><span data-stu-id="b44e8-124">You can use the following options to improve performance of your database:</span></span>

1. <span data-ttu-id="b44e8-125">使用 [SQL Database Advisor](sql-database-advisor-portal.md) 來檢視建立和卸除索引、參數化查詢，以及修正結構描述問題的建議。</span><span class="sxs-lookup"><span data-stu-id="b44e8-125">Use [SQL Database Advisor](sql-database-advisor-portal.md) to view recommendations for creating and dropping indexes, parameterizing queries, and fixing schema issues.</span></span>
2. <span data-ttu-id="b44e8-126">[啟用自動調整](sql-database-automatic-tuning-enable.md)並讓 Azure SQL Database 自動修正發現的效能問題。</span><span class="sxs-lookup"><span data-stu-id="b44e8-126">[Enable automatic tuning](sql-database-automatic-tuning-enable.md) and let Azure SQL database automatically fix identified performance issues.</span></span>

## <a name="improving-database-performance-with-more-resources"></a><span data-ttu-id="b44e8-127">使用更多資源提升資料庫效能</span><span class="sxs-lookup"><span data-stu-id="b44e8-127">Improving database performance with more resources</span></span>

<span data-ttu-id="b44e8-128">最後，如果沒有可改善資料庫效能的可操作項目，您可以變更 Azure SQL Database 中可用的資源數量。</span><span class="sxs-lookup"><span data-stu-id="b44e8-128">Finally, if there are no actionable items that can improve performance of your database, you can change the amount of resources available in Azure SQL Database.</span></span> <span data-ttu-id="b44e8-129">您可以隨時變更獨立資料庫的[服務層](sql-database-service-tiers.md)或增加彈性集區的 eDTU。</span><span class="sxs-lookup"><span data-stu-id="b44e8-129">You can assign more resources by changing the [service tier](sql-database-service-tiers.md) of a standalone database or increase the eDTUs of an elastic pool at any time.</span></span>
1. <span data-ttu-id="b44e8-130">若是獨立資料庫，您可以視需要[變更服務層級](sql-database-service-tiers.md)以提升資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="b44e8-130">For standalone databases, you can [change service tiers](sql-database-service-tiers.md) on-demand to improve database performance.</span></span>
2. <span data-ttu-id="b44e8-131">若是多個資料庫，請考慮使用[彈性集區](sql-database-elastic-pool-guidance.md)來自動調整資源。</span><span class="sxs-lookup"><span data-stu-id="b44e8-131">For multiple databases, consider using [elastic pools](sql-database-elastic-pool-guidance.md) to scale resources automatically.</span></span>

## <a name="tune-and-refactor-application-or-database-code"></a><span data-ttu-id="b44e8-132">調整和重構應用程式或資料庫程式碼</span><span class="sxs-lookup"><span data-stu-id="b44e8-132">Tune and refactor application or database code</span></span>

<span data-ttu-id="b44e8-133">您可以變更應用程式程式碼，針對工作負載以最佳方式使用資料庫、變更索引、強制執行計劃，或使用提示來手動調整資料庫。</span><span class="sxs-lookup"><span data-stu-id="b44e8-133">You can change application code to more optimally use the database, change indexes, force plans, or use hints to manually adapt the database to your workload.</span></span> <span data-ttu-id="b44e8-134">在[效能指引主題](sql-database-performance-guidance.md)文章中可找到手動調整或重寫程式碼的一些方針和秘訣。</span><span class="sxs-lookup"><span data-stu-id="b44e8-134">Find some guidance and tips for manual tuning and rewriting the code in the [performance guidance topic](sql-database-performance-guidance.md) article.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b44e8-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b44e8-135">Next steps</span></span>

- <span data-ttu-id="b44e8-136">若要在 Azure SQL Database 中啟用自動調整，並讓自動調整功能完全管理您的工作負載，請參閱[啟用自動調整](sql-database-automatic-tuning-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="b44e8-136">To enable automatic tuning in Azure SQL Database and let automatic tuning feature fully manage your workload, see [Enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>
- <span data-ttu-id="b44e8-137">若要使用手動調整，您可以檢閱 [Azure 入口網站中的調整建議](sql-database-advisor-portal.md)並手動套用可改善查詢效能的建議。</span><span class="sxs-lookup"><span data-stu-id="b44e8-137">To use manual tuning, you can review [Tuning recommendations in Azure portal](sql-database-advisor-portal.md) and manually apply the ones that improve performance of your queries.</span></span>
- <span data-ttu-id="b44e8-138">變更 [Azure SQL Database 服務層](sql-database-performance-guidance.md)來變更資料庫中可用的資源</span><span class="sxs-lookup"><span data-stu-id="b44e8-138">Change resources that are available in your database by changing [Azure SQL Database service tiers](sql-database-performance-guidance.md)</span></span>