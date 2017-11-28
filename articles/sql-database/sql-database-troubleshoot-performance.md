---
title: "aaaMonitoring （& s) 效能調整-Azure SQL Database |Microsoft 文件"
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
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a><span data-ttu-id="92b82-104">監視和效能微調</span><span class="sxs-lookup"><span data-stu-id="92b82-104">Monitoring and performance tuning</span></span>

<span data-ttu-id="92b82-105">Azure SQL Database 自動管理，而且有彈性的資料服務，您可以輕鬆地監視使用量、 新增或移除資源 （CPU、 記憶體、 io），尋找可以改善效能，您的資料庫，或讓資料庫調整 tooyour 工作負載的建議和自動讓效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="92b82-105">Azure SQL Database is automatically managed and flexible data service where you can easily monitor usage, add or remove resources (CPU, memory, io), find recommendations that can improve performance of your database, or let database adapt tooyour workload and automatically optimize performance.</span></span>

<span data-ttu-id="92b82-106">本文提供 Azure SQL Database 中可用的監視和效能微調選項概觀。</span><span class="sxs-lookup"><span data-stu-id="92b82-106">This article provides overview of monitoring and performance tuning options that are available in Azure SQL Database.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a><span data-ttu-id="92b82-107">針對資料庫效能進行監視和疑難排解</span><span class="sxs-lookup"><span data-stu-id="92b82-107">Monitoring and troubleshooting database performance</span></span>

<span data-ttu-id="92b82-108">Azure SQL Database 可讓您 tooeasily 監視資料庫的使用量，以及識別可能造成 hello 效能問題的查詢。</span><span class="sxs-lookup"><span data-stu-id="92b82-108">Azure SQL Database enables you tooeasily monitor your database usage and identify queries that might cause hello performance issues.</span></span> <span data-ttu-id="92b82-109">您可以使用 Azure 入口網站或系統檢視來監視資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="92b82-109">You can monitor database performance using Azure portal or system views.</span></span> <span data-ttu-id="92b82-110">您有下列選項來監視和疑難排解資料庫效能的 hello:</span><span class="sxs-lookup"><span data-stu-id="92b82-110">You have hello following options for monitoring and troubleshooting database performance:</span></span>

1. <span data-ttu-id="92b82-111">在 hello [Azure 入口網站](https://portal.azure.com)，按一下  **SQL 資料庫**選取 hello 資料庫，然後使用 hello 監視圖表 toolook 接近其最大的資源。</span><span class="sxs-lookup"><span data-stu-id="92b82-111">In hello [Azure portal](https://portal.azure.com), click **SQL databases**, select hello database, and then use hello Monitoring chart toolook for resources approaching their maximum.</span></span> <span data-ttu-id="92b82-112">預設會顯示 DTU 耗用量。</span><span class="sxs-lookup"><span data-stu-id="92b82-112">DTU consumption is shown by default.</span></span> <span data-ttu-id="92b82-113">按一下**編輯**toochange hello 時間範圍和顯示的值。</span><span class="sxs-lookup"><span data-stu-id="92b82-113">Click **Edit** toochange hello time range and values shown.</span></span>
2. <span data-ttu-id="92b82-114">使用[查詢效能深入解析](sql-database-query-performance.md)tooidentify hello 查詢花費的最 hello 的資源。</span><span class="sxs-lookup"><span data-stu-id="92b82-114">Use [Query Performance Insight](sql-database-query-performance.md) tooidentify hello queries that spend hello most of resources.</span></span>
3. <span data-ttu-id="92b82-115">您可以使用動態管理檢視 (Dmv)，擴充的事件 (`XEvents`)，和 hello 即時 SSMS tooget 效能參數中的查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="92b82-115">You can use dynamic management views (DMVs), Extended Events (`XEvents`), and hello Query Store in SSMS tooget performance parameters in real time.</span></span>

<span data-ttu-id="92b82-116">請參閱 hello[效能指引主題](sql-database-performance-guidance.md)toofind 技術，您就可以使用 Azure SQL Database 的 tooimprove 效能，如果您找出使用這些報表或檢視表的一些問題。</span><span class="sxs-lookup"><span data-stu-id="92b82-116">See hello [performance guidance topic](sql-database-performance-guidance.md) toofind techniques that you can use tooimprove performance of Azure SQL Database if you identify some issue using these reports or views.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="92b82-117">建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="92b82-117">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="92b82-118">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="92b82-118">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
>

## <a name="optimize-database-tooimprove-performance"></a><span data-ttu-id="92b82-119">最佳化資料庫 tooimprove 效能</span><span class="sxs-lookup"><span data-stu-id="92b82-119">Optimize database tooimprove performance</span></span>

<span data-ttu-id="92b82-120">Azure SQL Database 可讓您 tooidentify 機會 tooimprove 和最佳化查詢效能，而不變更資源，藉由檢閱[效能微調建議](sql-database-advisor.md)。</span><span class="sxs-lookup"><span data-stu-id="92b82-120">Azure SQL Database enables you tooidentify opportunities tooimprove and optimize query performance without changing resources by reviewing [performance tuning recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="92b82-121">遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。</span><span class="sxs-lookup"><span data-stu-id="92b82-121">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="92b82-122">您可以套用您的工作負載這些微調建議 tooimprove 效能。</span><span class="sxs-lookup"><span data-stu-id="92b82-122">You can apply these tuning recommendations tooimprove performance of your workload.</span></span>
<span data-ttu-id="92b82-123">您也可以讓的 Azure SQL database 太[自動最佳化查詢效能](sql-database-automatic-tuning.md)藉由套用所有識別的建議，並確認它們改善資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="92b82-123">You can also let Azure SQL database too[automatically optimize performance of your queries](sql-database-automatic-tuning.md) by applying all identified recommendations and verifying that they improve database performance.</span></span> <span data-ttu-id="92b82-124">您可以使用下列選項 tooimprove 對資料庫效能的 hello:</span><span class="sxs-lookup"><span data-stu-id="92b82-124">You can use hello following options tooimprove performance of your database:</span></span>

1. <span data-ttu-id="92b82-125">使用[SQL Database Advisor](sql-database-advisor-portal.md) tooview 建立和卸除索引、 參數化查詢，以及修正結構描述問題的建議。</span><span class="sxs-lookup"><span data-stu-id="92b82-125">Use [SQL Database Advisor](sql-database-advisor-portal.md) tooview recommendations for creating and dropping indexes, parameterizing queries, and fixing schema issues.</span></span>
2. <span data-ttu-id="92b82-126">[啟用自動調整](sql-database-automatic-tuning-enable.md)並讓 Azure SQL Database 自動修正發現的效能問題。</span><span class="sxs-lookup"><span data-stu-id="92b82-126">[Enable automatic tuning](sql-database-automatic-tuning-enable.md) and let Azure SQL database automatically fix identified performance issues.</span></span>

## <a name="improving-database-performance-with-more-resources"></a><span data-ttu-id="92b82-127">使用更多資源提升資料庫效能</span><span class="sxs-lookup"><span data-stu-id="92b82-127">Improving database performance with more resources</span></span>

<span data-ttu-id="92b82-128">最後，如果沒有可採取動作的項目，可以改善您資料庫的效能，您可以變更 hello Azure SQL Database 中可用的資源數量。</span><span class="sxs-lookup"><span data-stu-id="92b82-128">Finally, if there are no actionable items that can improve performance of your database, you can change hello amount of resources available in Azure SQL Database.</span></span> <span data-ttu-id="92b82-129">您可以指派更多資源，藉由變更 hello[服務層](sql-database-service-tiers.md)獨立的資料庫，或在任何時間增加彈性集區的 edtu 數 （hello）。</span><span class="sxs-lookup"><span data-stu-id="92b82-129">You can assign more resources by changing hello [service tier](sql-database-service-tiers.md) of a standalone database or increase hello eDTUs of an elastic pool at any time.</span></span>
1. <span data-ttu-id="92b82-130">您可以為獨立資料庫[來變更服務層](sql-database-service-tiers.md)隨 tooimprove 資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="92b82-130">For standalone databases, you can [change service tiers](sql-database-service-tiers.md) on-demand tooimprove database performance.</span></span>
2. <span data-ttu-id="92b82-131">針對多個資料庫，請考慮使用[彈性集區](sql-database-elastic-pool-guidance.md)tooscale 資源自動。</span><span class="sxs-lookup"><span data-stu-id="92b82-131">For multiple databases, consider using [elastic pools](sql-database-elastic-pool-guidance.md) tooscale resources automatically.</span></span>

## <a name="tune-and-refactor-application-or-database-code"></a><span data-ttu-id="92b82-132">調整和重構應用程式或資料庫程式碼</span><span class="sxs-lookup"><span data-stu-id="92b82-132">Tune and refactor application or database code</span></span>

<span data-ttu-id="92b82-133">您可以變更應用程式程式碼 toomore 最佳的方式使用 hello 資料庫、 變更索引、 強制執行計劃，或使用 toomanually 調整 hello 資料庫 tooyour 工作負載的提示。</span><span class="sxs-lookup"><span data-stu-id="92b82-133">You can change application code toomore optimally use hello database, change indexes, force plans, or use hints toomanually adapt hello database tooyour workload.</span></span> <span data-ttu-id="92b82-134">尋找一些指導方針和秘訣手動調整或重寫 hello hello 碼[效能指引主題](sql-database-performance-guidance.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="92b82-134">Find some guidance and tips for manual tuning and rewriting hello code in hello [performance guidance topic](sql-database-performance-guidance.md) article.</span></span>


## <a name="next-steps"></a><span data-ttu-id="92b82-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92b82-135">Next steps</span></span>

- <span data-ttu-id="92b82-136">自動調整 Azure SQL Database，然後讓自動 tooenable 完全微調功能管理您的工作負載，請參閱[啟用自動調整](sql-database-automatic-tuning-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="92b82-136">tooenable automatic tuning in Azure SQL Database and let automatic tuning feature fully manage your workload, see [Enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>
- <span data-ttu-id="92b82-137">toouse 手動微調，您可以檢閱[微調建議，在 Azure 入口網站中的](sql-database-advisor-portal.md)並手動套用 hello 改善查詢效能的項目。</span><span class="sxs-lookup"><span data-stu-id="92b82-137">toouse manual tuning, you can review [Tuning recommendations in Azure portal](sql-database-advisor-portal.md) and manually apply hello ones that improve performance of your queries.</span></span>
- <span data-ttu-id="92b82-138">變更 [Azure SQL Database 服務層](sql-database-performance-guidance.md)來變更資料庫中可用的資源</span><span class="sxs-lookup"><span data-stu-id="92b82-138">Change resources that are available in your database by changing [Azure SQL Database service tiers](sql-database-performance-guidance.md)</span></span>