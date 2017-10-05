---
title: "監視 Azure SQL Database 中的資料庫效能 | Microsoft Docs"
description: "了解使用 Azure 工具和動態管理檢視來監視您的資料庫的選項。"
keywords: "資料庫監視, 雲端資料庫效能"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: e11ed3275413b428523eef78a5a89b537f6a4afc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a><span data-ttu-id="7efb3-104">監視 Azure SQL Database 中的資料庫效能</span><span class="sxs-lookup"><span data-stu-id="7efb3-104">Monitoring database performance in Azure SQL Database</span></span>
<span data-ttu-id="7efb3-105">在 Azure 中監視 SQL Database 的效能，必須從監視您選擇之資料庫效能等級相關的資源使用率開始。</span><span class="sxs-lookup"><span data-stu-id="7efb3-105">Monitoring the performance of a SQL database in Azure starts with monitoring the resource utilization relative to the level of database performance you choose.</span></span> <span data-ttu-id="7efb3-106">監視可協助您判斷您的資料庫是否有超量的容量或因為資源超量而發生問題，然後判斷是否開始調整您資料庫的效能等級和[服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="7efb3-106">Monitoring helps you  determine whether your database has excess capacity or is having trouble because resources are maxed out, and then decide whether it's time to adjust the performance level and [service tier](sql-database-service-tiers.md) of your database.</span></span> <span data-ttu-id="7efb3-107">您可以使用 [Azure 入口網站](https://portal.azure.com)中的圖形化工具或使用 SQL [動態管理檢視](https://msdn.microsoft.com/library/ms188754.aspx)，監視您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7efb3-107">You can monitor your database using graphical tools in the [Azure portal](https://portal.azure.com) or using SQL [dynamic management views](https://msdn.microsoft.com/library/ms188754.aspx).</span></span>

## <a name="monitor-databases-using-the-azure-portal"></a><span data-ttu-id="7efb3-108">使用 Azure 入口網站監視資料庫</span><span class="sxs-lookup"><span data-stu-id="7efb3-108">Monitor databases using the Azure portal</span></span>
<span data-ttu-id="7efb3-109">在 [Azure 入口網站](https://portal.azure.com/)中，您可以透過選取資料庫，並按一下 [監視] 圖表，監視單一資料庫的使用率。</span><span class="sxs-lookup"><span data-stu-id="7efb3-109">In the [Azure portal](https://portal.azure.com/), you can monitor a single database’s utilization by selecting your database and clicking the **Monitoring** chart.</span></span> <span data-ttu-id="7efb3-110">如此會帶出您可變更的 [度量] 視窗，只要按一下 [編輯圖表] 按鈕即可。</span><span class="sxs-lookup"><span data-stu-id="7efb3-110">This brings up a **Metric** window that you can change by clicking the **Edit chart** button.</span></span> <span data-ttu-id="7efb3-111">新增下列度量：</span><span class="sxs-lookup"><span data-stu-id="7efb3-111">Add the following metrics:</span></span>

* <span data-ttu-id="7efb3-112">CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="7efb3-112">CPU percentage</span></span>
* <span data-ttu-id="7efb3-113">DTU 百分比</span><span class="sxs-lookup"><span data-stu-id="7efb3-113">DTU percentage</span></span>
* <span data-ttu-id="7efb3-114">資料 IO 百分比</span><span class="sxs-lookup"><span data-stu-id="7efb3-114">Data IO percentage</span></span>
* <span data-ttu-id="7efb3-115">資料庫大小百分比</span><span class="sxs-lookup"><span data-stu-id="7efb3-115">Database size percentage</span></span>

<span data-ttu-id="7efb3-116">新增這些度量之後，您可以在 [度量] 視窗中，在含有詳細資料的 [監視] 圖表中繼續檢視它們。</span><span class="sxs-lookup"><span data-stu-id="7efb3-116">Once you’ve added these metrics, you can continue to view them in the **Monitoring** chart with more details on the **Metric** window.</span></span> <span data-ttu-id="7efb3-117">這四個度量都會顯示與資料庫 **DTU** 相對的平均使用率百分比。</span><span class="sxs-lookup"><span data-stu-id="7efb3-117">All four metrics show the average utilization percentage relative to the **DTU** of your database.</span></span> <span data-ttu-id="7efb3-118">如需 DTU 的詳細資訊，請參閱 [服務層](sql-database-service-tiers.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="7efb3-118">See the [service tiers](sql-database-service-tiers.md) article for details about DTUs.</span></span>

![資料庫效能的服務層監視。](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

<span data-ttu-id="7efb3-120">您也可以在效能度量中設定警示。</span><span class="sxs-lookup"><span data-stu-id="7efb3-120">You can also configure alerts on the performance metrics.</span></span> <span data-ttu-id="7efb3-121">按一下 [度量] 視窗中的 [新增警示] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7efb3-121">Click the **Add alert** button in the **Metric** window.</span></span> <span data-ttu-id="7efb3-122">遵循精靈的指示以設定警示。</span><span class="sxs-lookup"><span data-stu-id="7efb3-122">Follow the wizard to configure your alert.</span></span> <span data-ttu-id="7efb3-123">您可以選擇在度量超出或低於特定臨界值時發出警示。</span><span class="sxs-lookup"><span data-stu-id="7efb3-123">You have the option to alert if the metrics exceed a certain threshold or if the metric falls below a certain threshold.</span></span>

<span data-ttu-id="7efb3-124">例如，如果您預期資料庫中的工作負載會成長，可以選擇設定電子郵件警示，以便在資料庫的任何效能度量達到 80% 時收到警示。</span><span class="sxs-lookup"><span data-stu-id="7efb3-124">For example, if you expect the workload on your database to grow, you can choose to configure an email alert whenever your database reaches 80% on any of the performance metrics.</span></span> <span data-ttu-id="7efb3-125">您可以使用此警示做為早期警告，協助您判斷何時需要切換至更高的效能層級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-125">You can use this as an early warning to figure out when you might have to switch to the next higher performance level.</span></span>

<span data-ttu-id="7efb3-126">效能度量也可協助您判斷您是否能夠降級至較低的效能層級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-126">The performance metrics can also help you determine if you are able to downgrade to a lower performance level.</span></span> <span data-ttu-id="7efb3-127">假設您使用標準 S2 資料庫，且所有效能度量皆顯示在指定時間內，資料庫平均使用率沒有超過 10%。</span><span class="sxs-lookup"><span data-stu-id="7efb3-127">Assume you are using a Standard S2 database and all performance metrics show that the database on average does not use more than 10% at any given time.</span></span> <span data-ttu-id="7efb3-128">則該資料庫可能在標準 S1 中會運作得不錯。</span><span class="sxs-lookup"><span data-stu-id="7efb3-128">It is likely that the database will work well in Standard S1.</span></span> <span data-ttu-id="7efb3-129">不過，在您決定將資料庫移至較低效能層級前，請先注意暴增或大幅變動的工作負載。</span><span class="sxs-lookup"><span data-stu-id="7efb3-129">However, be aware of workloads that spike or fluctuate before making the decision to move to a lower performance level.</span></span>

## <a name="monitor-databases-using-dmvs"></a><span data-ttu-id="7efb3-130">使用 DMV 監視資料庫</span><span class="sxs-lookup"><span data-stu-id="7efb3-130">Monitor databases using DMVs</span></span>
<span data-ttu-id="7efb3-131">您也可以透過下列系統檢視取得公開在入口網站中的相同度量：伺服器的邏輯 **master** 資料庫中的 [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)，以及使用者資料庫中的 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7efb3-131">The same metrics that are exposed in the portal are also available through system views: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) in the logical **master** database of your server, and [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) in the user database.</span></span> <span data-ttu-id="7efb3-132">如果您需要在一段長時間內監視較不細微的資料，請使用 **sys.resource_stats**。</span><span class="sxs-lookup"><span data-stu-id="7efb3-132">Use **sys.resource_stats** if you need to monitor less granular data across a longer period of time.</span></span> <span data-ttu-id="7efb3-133">如果您需要在較小的時間範圍內監視較細微的資料，請使用 **sys.dm_db_resource_stats**。</span><span class="sxs-lookup"><span data-stu-id="7efb3-133">Use **sys.dm_db_resource_stats** if you need to monitor more granular data within a smaller time frame.</span></span> <span data-ttu-id="7efb3-134">如需詳細資訊，請參閱 [Azure SQL Database 效能指引](sql-database-single-database-monitor.md#monitor-resource-use)。</span><span class="sxs-lookup"><span data-stu-id="7efb3-134">For more information, see [Azure SQL Database Performance Guidance](sql-database-single-database-monitor.md#monitor-resource-use).</span></span>

> [!NOTE]
> <span data-ttu-id="7efb3-135">使用於 Web 和 Business Edition 資料庫 (已淘汰) 時，**sys.dm_db_resource_stats** 會傳回空的結果集。</span><span class="sxs-lookup"><span data-stu-id="7efb3-135">**sys.dm_db_resource_stats** returns an empty result set when used in Web and Business edition databases, which are retired.</span></span>
>
>

### <a name="monitor-resource-use"></a><span data-ttu-id="7efb3-136">監視資源使用量</span><span class="sxs-lookup"><span data-stu-id="7efb3-136">Monitor resource use</span></span>

<span data-ttu-id="7efb3-137">您可以使用 [SQL Database 查詢效能深入解析](sql-database-query-performance.md)和[查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx)來監視資源用量。</span><span class="sxs-lookup"><span data-stu-id="7efb3-137">You can monitor resource usage using [SQL Database Query Performance Insight](sql-database-query-performance.md) and [Query Store](https://msdn.microsoft.com/library/dn817826.aspx).</span></span>

<span data-ttu-id="7efb3-138">您也可以使用以下兩種檢視來監視用量：</span><span class="sxs-lookup"><span data-stu-id="7efb3-138">You can also monitor usage using these two views:</span></span>

* [<span data-ttu-id="7efb3-139">sys.dm_db_resource_stats</span><span class="sxs-lookup"><span data-stu-id="7efb3-139">sys.dm_db_resource_stats</span></span>](https://msdn.microsoft.com/library/dn800981.aspx)
* [<span data-ttu-id="7efb3-140">sys.resource_stats</span><span class="sxs-lookup"><span data-stu-id="7efb3-140">sys.resource_stats</span></span>](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a><span data-ttu-id="7efb3-141">sys.dm_db_resource_stats</span><span class="sxs-lookup"><span data-stu-id="7efb3-141">sys.dm_db_resource_stats</span></span>
<span data-ttu-id="7efb3-142">您可以在每一個 SQL Database 中使用 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)檢視。</span><span class="sxs-lookup"><span data-stu-id="7efb3-142">You can use the [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) view in every SQL database.</span></span> <span data-ttu-id="7efb3-143">**sys.dm_db_resource_stats** 檢視可顯示相對於服務層的最新資源使用量資料。</span><span class="sxs-lookup"><span data-stu-id="7efb3-143">The **sys.dm_db_resource_stats** view shows recent resource use data relative to the service tier.</span></span> <span data-ttu-id="7efb3-144">每隔 15 秒鐘就會記錄一次 CPU、資料 I/O、記錄檔寫入和記憶體的平均百分比，並且會維持 1 小時。</span><span class="sxs-lookup"><span data-stu-id="7efb3-144">Average percentages for CPU, data I/O, log writes, and memory are recorded every 15 seconds and are maintained for 1 hour.</span></span>

<span data-ttu-id="7efb3-145">因為此檢視會提供更細微的資源使用量資訊，請先使用 **sys.dm_db_resource_stats** 來進行任何現狀分析或疑難排解。</span><span class="sxs-lookup"><span data-stu-id="7efb3-145">Because this view provides a more granular look at resource use, use **sys.dm_db_resource_stats** first for any current-state analysis or troubleshooting.</span></span> <span data-ttu-id="7efb3-146">例如，下列查詢會顯示目前的資料庫在過去一小時的平均和最大資源使用量：</span><span class="sxs-lookup"><span data-stu-id="7efb3-146">For example, this query shows the average and maximum resource use for the current database over the past hour:</span></span>

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

<span data-ttu-id="7efb3-147">如需其他查詢的資訊，請參閱 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) 中的範例。</span><span class="sxs-lookup"><span data-stu-id="7efb3-147">For other queries, see the examples in [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).</span></span>

#### <a name="sysresourcestats"></a><span data-ttu-id="7efb3-148">sys.resource_stats</span><span class="sxs-lookup"><span data-stu-id="7efb3-148">sys.resource_stats</span></span>
<span data-ttu-id="7efb3-149">**master** 資料庫中的 [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) 檢視有其他資訊可協助您監視 SQL Database 在其特定服務層和效能等級的效能。</span><span class="sxs-lookup"><span data-stu-id="7efb3-149">The [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) view in the **master** database has additional information that can help you monitor the performance of your SQL database at its specific service tier and performance level.</span></span> <span data-ttu-id="7efb3-150">這項資料每隔 5 分鐘就會收集一次，並且會維持大約 35 天。</span><span class="sxs-lookup"><span data-stu-id="7efb3-150">The data is collected every 5 minutes and is maintained for approximately 35 days.</span></span> <span data-ttu-id="7efb3-151">這個檢視適合用於進行 SQL Database 如何使用資源的長期歷史分析。</span><span class="sxs-lookup"><span data-stu-id="7efb3-151">This view is useful for a longer-term historical analysis of how your SQL database uses resources.</span></span>

<span data-ttu-id="7efb3-152">下圖顯示在一週中 P2 效能等級之高階資料庫每小時的 CPU 資源使用量。</span><span class="sxs-lookup"><span data-stu-id="7efb3-152">The following graph shows the CPU resource use for a Premium database with the P2 performance level for each hour in a week.</span></span> <span data-ttu-id="7efb3-153">此圖從星期一開始，顯示 5 個工作天，然後顯示較少發生在應用程式的週末。</span><span class="sxs-lookup"><span data-stu-id="7efb3-153">This graph starts on a Monday, shows 5 work days, and then shows a weekend, when much less happens on the application.</span></span>

![SQL Database 的資源使用量](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

<span data-ttu-id="7efb3-155">從資料中，這個資料庫目前相對於 P2 效能等級的尖峰 CPU 負載剛好超過 50% 的 CPU 使用量 (星期二中午)。</span><span class="sxs-lookup"><span data-stu-id="7efb3-155">From the data, this database currently has a peak CPU load of just over 50 percent CPU use relative to the P2 performance level (midday on Tuesday).</span></span> <span data-ttu-id="7efb3-156">如果 CPU 是應用程式的資源設定檔中的主要因素，您可能會決定 P2 是正確的效能等級，以確保永遠符合工作負載。</span><span class="sxs-lookup"><span data-stu-id="7efb3-156">If CPU is the dominant factor in the application’s resource profile, then you might decide that P2 is the right performance level to guarantee that the workload always fits.</span></span> <span data-ttu-id="7efb3-157">如果您預期應用程式會隨著時間成長，最好預留額外的資源緩衝，讓應用程式永遠不會達到效能等級限制。</span><span class="sxs-lookup"><span data-stu-id="7efb3-157">If you expect an application to grow over time, it's a good idea to have an extra resource buffer so that the application doesn't ever reach the performance-level limit.</span></span> <span data-ttu-id="7efb3-158">如果您提升效能等級，則可協助避免資料庫沒有足夠能力來有效處理要求時可能發生的客戶可見錯誤，尤其是在延遲敏感的環境中。</span><span class="sxs-lookup"><span data-stu-id="7efb3-158">If you increase the performance level, you can help avoid customer-visible errors that might occur when a database doesn't have enough power to process requests effectively, especially in latency-sensitive environments.</span></span> <span data-ttu-id="7efb3-159">其中一例便是支援可根據資料庫呼叫結果繪製網頁之應用程式的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7efb3-159">An example is a database that supports an application that paints webpages based on the results of database calls.</span></span>

<span data-ttu-id="7efb3-160">其他應用程式類型可能會以不同方式解譯相同的圖形。</span><span class="sxs-lookup"><span data-stu-id="7efb3-160">Other application types might interpret the same graph differently.</span></span> <span data-ttu-id="7efb3-161">例如，如果應用程式嘗試每天處理薪資資料而且具有同一張圖表，這種「批次作業」模型可能會在 P1 效能等級中正常執行。</span><span class="sxs-lookup"><span data-stu-id="7efb3-161">For example, if an application tries to process payroll data each day and has the same chart, this kind of "batch job" model might do fine at a P1 performance level.</span></span> <span data-ttu-id="7efb3-162">相較於 P2 效能等級的 200 個 DTU，P1 效能等級有 100 個 DTU。</span><span class="sxs-lookup"><span data-stu-id="7efb3-162">The P1 performance level has 100 DTUs compared to 200 DTUs at the P2 performance level.</span></span> <span data-ttu-id="7efb3-163">P1 效能等級提供的效能是 P2 效能等級的一半。</span><span class="sxs-lookup"><span data-stu-id="7efb3-163">The P1 performance level provides half the performance of the P2 performance level.</span></span> <span data-ttu-id="7efb3-164">因此，P2 中 50% 的 CPU 使用量等於 P1 中 100% 的 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="7efb3-164">So, 50 percent of CPU use in P2 equals 100 percent CPU use in P1.</span></span> <span data-ttu-id="7efb3-165">如果應用程式沒有逾時，就算作業花了 2 個小時或 2.5 個小時才能完成也沒關係，只要它在今天內完成即可。</span><span class="sxs-lookup"><span data-stu-id="7efb3-165">If the application does not have timeouts, it might not matter if a job takes 2 hours or 2.5 hours to finish, if it gets done today.</span></span> <span data-ttu-id="7efb3-166">這個類別中的應用程式或許可以使用 P1 效能等級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-166">An application in this category probably can use a P1 performance level.</span></span> <span data-ttu-id="7efb3-167">一天中有好幾個時段的資源使用量較低，您可以善用這個事實，讓任何「巨量尖峰」可以溢出到當天稍後的一個低谷。</span><span class="sxs-lookup"><span data-stu-id="7efb3-167">You can take advantage of the fact that there are periods of time during the day when resource use is lower, so that any "big peak" might spill over into one of the troughs later in the day.</span></span> <span data-ttu-id="7efb3-168">只要作業可以每天及時完成，P1 效能等級可能就很適合這類應用程式 (並節省經費)。</span><span class="sxs-lookup"><span data-stu-id="7efb3-168">The P1 performance level might be good for that kind of application (and save money), as long as the jobs can finish on time each day.</span></span>

<span data-ttu-id="7efb3-169">Azure SQL Database 會在每個伺服器 **master** 資料庫的 **sys.resource_stats** 檢視中公開每個作用中資料庫的耗用資源資訊。</span><span class="sxs-lookup"><span data-stu-id="7efb3-169">Azure SQL Database exposes consumed resource information for each active database in the **sys.resource_stats** view of the **master** database in each server.</span></span> <span data-ttu-id="7efb3-170">資料表中的資料會以 5 分鐘的間隔彙總。</span><span class="sxs-lookup"><span data-stu-id="7efb3-170">The data in the table is aggregated for 5-minute intervals.</span></span> <span data-ttu-id="7efb3-171">利用基本、標準和進階服務層，資料可能要花 5 分鐘以上的時間才會出現在資料表中，因此這項資料比較適合進行歷程記錄分析而不是近乎即時的分析。</span><span class="sxs-lookup"><span data-stu-id="7efb3-171">With the Basic, Standard, and Premium service tiers, the data can take more than 5 minutes to appear in the table, so this data is more useful for historical analysis rather than near-real-time analysis.</span></span> <span data-ttu-id="7efb3-172">查詢 **sys.resource_stats** 檢視可查看資料庫的近期歷程記錄，並驗證所選的保留是否會在必要時提供所需的效能。</span><span class="sxs-lookup"><span data-stu-id="7efb3-172">Query the **sys.resource_stats** view to see the recent history of a database and to validate whether the reservation you chose delivered the performance you want when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="7efb3-173">您必須連接到邏輯 SQL Database 伺服器的 **master** 資料庫才能在下列範例中查詢 **sys.resource_stats**。</span><span class="sxs-lookup"><span data-stu-id="7efb3-173">You must be connected to the **master** database of your logical SQL database server to query **sys.resource_stats** in the following examples.</span></span>
> 
> 

<span data-ttu-id="7efb3-174">下列範例會示範如何公開此檢視中的資料：</span><span class="sxs-lookup"><span data-stu-id="7efb3-174">This example shows you how the data in this view is exposed:</span></span>

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![sys.resource_stats 目錄檢視](./media/sql-database-performance-guidance/sys_resource_stats.png)

<span data-ttu-id="7efb3-176">下列範例示範不同方式，以供您用來使用 **sys.resource_stats** 目錄檢視取得有關 SQL Database 如何使用資源的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="7efb3-176">The next example shows you different ways that you can use the **sys.resource_stats** catalog view to get information about how your SQL database uses resources:</span></span>

1. <span data-ttu-id="7efb3-177">若要查看 userdb1 資料庫在過去一週的資源使用量，您可以執行下列查詢：</span><span class="sxs-lookup"><span data-stu-id="7efb3-177">To look at the past week’s resource use for the database userdb1, you can run this query:</span></span>
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. <span data-ttu-id="7efb3-178">若要評估您的工作負載與效能等級的符合程度，您必須鑽研資源度量的每個層面：CPU、讀取、寫入、背景工作角色數目和工作階段數目。</span><span class="sxs-lookup"><span data-stu-id="7efb3-178">To evaluate how well your workload fits the performance level, you need to drill down into each aspect of the resource metrics: CPU, reads, writes, number of workers, and number of sessions.</span></span> <span data-ttu-id="7efb3-179">以下是使用 **sys.resource_stats** 修訂過的查詢，可報告這些資源度量的平均值和最大值：</span><span class="sxs-lookup"><span data-stu-id="7efb3-179">Here's a revised query using **sys.resource_stats** to report the average and maximum values of these resource metrics:</span></span>
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. <span data-ttu-id="7efb3-180">利用這項有關各資源度量平均值和最大值的資訊，您可以評估您的工作負載與您所選之效能等級的符合程度。</span><span class="sxs-lookup"><span data-stu-id="7efb3-180">With this information about the average and maximum values of each resource metric, you can assess how well your workload fits into the performance level you chose.</span></span> <span data-ttu-id="7efb3-181">通常，來自 **sys.resource_stats** 的平均值可提供您對目標大小所使用的理想基準。</span><span class="sxs-lookup"><span data-stu-id="7efb3-181">Usually, average values from **sys.resource_stats** give you a good baseline to use against the target size.</span></span> <span data-ttu-id="7efb3-182">它應該是您主要的量尺。</span><span class="sxs-lookup"><span data-stu-id="7efb3-182">It should be your primary measurement stick.</span></span> <span data-ttu-id="7efb3-183">例如，您可能使用標準服務層搭配 S2 效能等級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-183">For an example, you might be using the Standard service tier with S2 performance level.</span></span> <span data-ttu-id="7efb3-184">CPU 以及 I/O 讀取和寫入的平均使用量百分比低於 40%，背景工作角色平均數目低於 50，而且工作階段平均數目低於 200。</span><span class="sxs-lookup"><span data-stu-id="7efb3-184">The average use percentages for CPU and I/O reads and writes are below 40 percent, the average number of workers is below 50, and the average number of sessions is below 200.</span></span> <span data-ttu-id="7efb3-185">您的工作負載可能符合 S1 效能等級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-185">Your workload might fit into the S1 performance level.</span></span> <span data-ttu-id="7efb3-186">要看到您的資料庫是否符合背景工作和工作階段限制範圍內非常容易。</span><span class="sxs-lookup"><span data-stu-id="7efb3-186">It's easy to see whether your database fits in the worker and session limits.</span></span> <span data-ttu-id="7efb3-187">若要查看資料庫在 CPU、讀取和寫入方面是否符合較低的效能等級，請將較低效能等級的 DTU 數目除以目前效能等級的 DTU 數目，然後將結果乘以 100：</span><span class="sxs-lookup"><span data-stu-id="7efb3-187">To see whether a database fits into a lower performance level with regards to CPU, reads, and writes, divide the DTU number of the lower performance level by the DTU number of your current performance level, and then multiply the result by 100:</span></span>
   
    <span data-ttu-id="7efb3-188">**S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**</span><span class="sxs-lookup"><span data-stu-id="7efb3-188">**S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**</span></span>
   
    <span data-ttu-id="7efb3-189">此結果是以百分比表示之兩個效能等級的相對效能差異。</span><span class="sxs-lookup"><span data-stu-id="7efb3-189">The result is the relative performance difference between the two performance levels in percentage.</span></span> <span data-ttu-id="7efb3-190">如果您的資源使用量未超過這個數量，您的工作負載可能符合較低的效能等級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-190">If your resource use doesn't exceed this amount, your workload might fit into the lower performance level.</span></span> <span data-ttu-id="7efb3-191">不過，您需要查看所有範圍的資源使用量值，並以百分比判斷資料庫工作負載符合較低效能等級的頻率。</span><span class="sxs-lookup"><span data-stu-id="7efb3-191">However, you need to look at all ranges of resource use values, and determine, by percentage, how often your database workload would fit into the lower performance level.</span></span> <span data-ttu-id="7efb3-192">下列查詢會根據我們在此範例中計算的 40% 臨界值，輸出每個資源維度的相符百分比：</span><span class="sxs-lookup"><span data-stu-id="7efb3-192">The following query outputs the fit percentage per resource dimension, based on the threshold of 40 percent that we calculated in this example:</span></span>
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    <span data-ttu-id="7efb3-193">根據您的資料庫服務等級目標 (SLO)，您可以決定您的工作負載是否符合較低的效能等級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-193">Based on your database service level objective (SLO), you can decide whether your workload fits into the lower performance level.</span></span> <span data-ttu-id="7efb3-194">如果您的資料庫工作負載 SLO 是 99.9%，且上述查詢針對三個資源維度傳回的值都大於 99.9，您的工作負載可能會符合較低的效能等級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-194">If your database workload SLO is 99.9 percent and the preceding query returns values greater than 99.9 percent for all three resource dimensions, your workload likely fits into the lower performance level.</span></span>
   
    <span data-ttu-id="7efb3-195">查看相符百分比也可讓您深入了解是否必須移到下一個較高的效能等級來滿足您的 SLO。</span><span class="sxs-lookup"><span data-stu-id="7efb3-195">Looking at the fit percentage also gives you insight into whether you should move to the next higher performance level to meet your SLO.</span></span> <span data-ttu-id="7efb3-196">例如，userdb1 會顯示過去一週的下列 CPU 使用量：</span><span class="sxs-lookup"><span data-stu-id="7efb3-196">For example, userdb1 shows the following CPU use for the past week:</span></span>
   
   | <span data-ttu-id="7efb3-197">平均 CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="7efb3-197">Average CPU percent</span></span> | <span data-ttu-id="7efb3-198">最大 CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="7efb3-198">Maximum CPU percent</span></span> |
   | --- | --- |
   | <span data-ttu-id="7efb3-199">24.5</span><span class="sxs-lookup"><span data-stu-id="7efb3-199">24.5</span></span> |<span data-ttu-id="7efb3-200">100.00</span><span class="sxs-lookup"><span data-stu-id="7efb3-200">100.00</span></span> |
   
    <span data-ttu-id="7efb3-201">平均 CPU 大約是效能等級限制的四分之一，完全符合資料庫的效能等級。</span><span class="sxs-lookup"><span data-stu-id="7efb3-201">The average CPU is about a quarter of the limit of the performance level, which would fit well into the performance level of the database.</span></span> <span data-ttu-id="7efb3-202">不過，此最大值會顯示資料庫達到效能等級的限制。</span><span class="sxs-lookup"><span data-stu-id="7efb3-202">But, the maximum value shows that the database reaches the limit of the performance level.</span></span> <span data-ttu-id="7efb3-203">您需要移至下一個較高的效能等級嗎？</span><span class="sxs-lookup"><span data-stu-id="7efb3-203">Do you need to move to the next higher performance level?</span></span> <span data-ttu-id="7efb3-204">請查看工作負載達到 100% 的次數，然後將其與您的資料庫工作負載 SLO 做比較。</span><span class="sxs-lookup"><span data-stu-id="7efb3-204">Look at how many times your workload reaches 100 percent, and then compare it to your database workload SLO.</span></span>
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    <span data-ttu-id="7efb3-205">如果此查詢針對三個資源維度傳回的值小於 99.9%，請考慮移到下一個較高的效能等級或使用應用程式微調技術減少 SQL Database 的負載。</span><span class="sxs-lookup"><span data-stu-id="7efb3-205">If this query returns a value less than 99.9 percent for any of the three resource dimensions, consider either moving to the next higher performance level or use application-tuning techniques to reduce the load on the SQL database.</span></span>
4. <span data-ttu-id="7efb3-206">此練習也會考慮您預計的未來工作負載增加量。</span><span class="sxs-lookup"><span data-stu-id="7efb3-206">This exercise also considers your projected workload increase in the future.</span></span>

<span data-ttu-id="7efb3-207">若為彈性集區，您可以監視其中的個別資料庫，技巧如本節所述。</span><span class="sxs-lookup"><span data-stu-id="7efb3-207">For elastic pools, you can monitor individual databases in the pool with the techniques described in this section.</span></span> <span data-ttu-id="7efb3-208">但您也可以監視集區整體。</span><span class="sxs-lookup"><span data-stu-id="7efb3-208">But you can also monitor the pool as a whole.</span></span> <span data-ttu-id="7efb3-209">如需詳細資訊，請參閱 [監視和管理彈性集區](sql-database-elastic-pool-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7efb3-209">For information, see [Monitor and manage an elastic pool](sql-database-elastic-pool-manage-portal.md).</span></span>


### <a name="maximum-concurrent-requests"></a><span data-ttu-id="7efb3-210">並行要求數上限</span><span class="sxs-lookup"><span data-stu-id="7efb3-210">Maximum concurrent requests</span></span>
<span data-ttu-id="7efb3-211">若要查看並行要求數目，請在 SQL Database 上執行下列 Transact-SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="7efb3-211">To see the number of concurrent requests, run this Transact-SQL query on your SQL database:</span></span>

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

<span data-ttu-id="7efb3-212">若要分析內部部署 SQL Server 資料庫的工作負載，請修改此查詢來篩選您要分析的特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="7efb3-212">To analyze the workload of an on-premises SQL Server database, modify this query to filter on the specific database you want to analyze.</span></span> <span data-ttu-id="7efb3-213">比方說，如果您擁有名為 MyDatabase 的內部部署資料庫，則下列 Transact-SQL 查詢會傳回該資料庫中並行要求的計數：</span><span class="sxs-lookup"><span data-stu-id="7efb3-213">For example, if you have an on-premises database named MyDatabase, this Transact-SQL query returns the count of concurrent requests in that database:</span></span>

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

<span data-ttu-id="7efb3-214">這只是單一時間點的快照。</span><span class="sxs-lookup"><span data-stu-id="7efb3-214">This is just a snapshot at a single point in time.</span></span> <span data-ttu-id="7efb3-215">若要進一步了解您的工作負載和並行要求需求，您必須收集一段時間內的許多範例。</span><span class="sxs-lookup"><span data-stu-id="7efb3-215">To get a better understanding of your workload and concurrent request requirements, you'll need to collect many samples over time.</span></span>

### <a name="maximum-concurrent-logins"></a><span data-ttu-id="7efb3-216">並行登入數上限</span><span class="sxs-lookup"><span data-stu-id="7efb3-216">Maximum concurrent logins</span></span>
<span data-ttu-id="7efb3-217">您可以分析您的使用者和應用程式模式以了解登入頻率。</span><span class="sxs-lookup"><span data-stu-id="7efb3-217">You can analyze your user and application patterns to get an idea of the frequency of logins.</span></span> <span data-ttu-id="7efb3-218">您也可以在測試環境中執行真實世界的負載，藉此確定您不會達到我們在本文中討論的這項限制或其他限制。</span><span class="sxs-lookup"><span data-stu-id="7efb3-218">You also can run real-world loads in a test environment to make sure that you're not hitting this or other limits we discuss in this article.</span></span> <span data-ttu-id="7efb3-219">沒有任何單一查詢或動態管理檢視 (DMV) 可以向您顯示並行登入計數或歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="7efb3-219">There isn’t a single query or dynamic management view (DMV) that can show you concurrent login counts or history.</span></span>

<span data-ttu-id="7efb3-220">如果這些用戶端使用相同的連接字串，服務仍會驗證每一個登入。</span><span class="sxs-lookup"><span data-stu-id="7efb3-220">If multiple clients use the same connection string, the service authenticates each login.</span></span> <span data-ttu-id="7efb3-221">如果有 10 位使用者同時以相同的使用者名稱和密碼連接到資料庫，將會有 10 個並行登入。</span><span class="sxs-lookup"><span data-stu-id="7efb3-221">If 10 users simultaneously connect to a database by using the same username and password, there would be 10 concurrent logins.</span></span> <span data-ttu-id="7efb3-222">這項限制只適用於登入和驗證期間。</span><span class="sxs-lookup"><span data-stu-id="7efb3-222">This limit applies only to the duration of the login and authentication.</span></span> <span data-ttu-id="7efb3-223">如果相同的 10 位使用者依序連接到資料庫，並行登入數目絕對不會大於 1。</span><span class="sxs-lookup"><span data-stu-id="7efb3-223">If the same 10 users connect to the database sequentially, the number of concurrent logins would never be greater than 1.</span></span>

> [!NOTE]
> <span data-ttu-id="7efb3-224">這項限制目前不適用於彈性集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7efb3-224">Currently, this limit does not apply to databases in elastic pools.</span></span>
> 
> 

### <a name="maximum-sessions"></a><span data-ttu-id="7efb3-225">工作階段數上限</span><span class="sxs-lookup"><span data-stu-id="7efb3-225">Maximum sessions</span></span>
<span data-ttu-id="7efb3-226">若要查看目前的作用中工作階段數目，請在 SQL Database 上執行下列 Transact-SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="7efb3-226">To see the number of current active sessions, run this Transact-SQL query on your SQL database:</span></span>

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

<span data-ttu-id="7efb3-227">如果您要分析內部部署 SQL Server 的工作負載，請修改查詢以專注於特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="7efb3-227">If you're analyzing an on-premises SQL Server workload, modify the query to focus on a specific database.</span></span> <span data-ttu-id="7efb3-228">如果您考慮將資料庫移至 Azure SQL Database，此查詢可協助您判斷該資料庫可能的工作階段需求。</span><span class="sxs-lookup"><span data-stu-id="7efb3-228">This query helps you determine possible session needs for the database if you are considering moving it to Azure SQL Database.</span></span>

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

<span data-ttu-id="7efb3-229">同樣地，這些查詢傳回的是某一時間點的計數。</span><span class="sxs-lookup"><span data-stu-id="7efb3-229">Again, these queries return a point-in-time count.</span></span> <span data-ttu-id="7efb3-230">如果您收集一段時間內的多個範例，您就可以充分了解您的工作階段使用量。</span><span class="sxs-lookup"><span data-stu-id="7efb3-230">If you collect multiple samples over time, you’ll have the best understanding of your session use.</span></span>

<span data-ttu-id="7efb3-231">若要進行 SQL Database 分析，您可以查詢 [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)檢視，並檢閱 **active_session_count** 資料行，以取得工作階段的歷史統計資料。</span><span class="sxs-lookup"><span data-stu-id="7efb3-231">For SQL Database analysis, you can get historical statistics on sessions by querying the [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) view and reviewing the **active_session_count** column.</span></span> 
