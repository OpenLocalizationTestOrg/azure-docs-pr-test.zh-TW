---
title: "Azure SQL Database 中的 aaaMonitoring 資料庫效能 |Microsoft 文件"
description: "深入了解 hello 選項來監視您的 Azure 工具和動態管理檢視的資料庫。"
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
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a><span data-ttu-id="82177-104">監視 Azure SQL Database 中的資料庫效能</span><span class="sxs-lookup"><span data-stu-id="82177-104">Monitoring database performance in Azure SQL Database</span></span>
<span data-ttu-id="82177-105">監視 Azure 中的 SQL 資料庫的效能，hello 開頭監視 hello 資源使用率相對 toohello 等級您選擇的資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="82177-105">Monitoring hello performance of a SQL database in Azure starts with monitoring hello resource utilization relative toohello level of database performance you choose.</span></span> <span data-ttu-id="82177-106">監視可協助您判斷您的資料庫具有過多的容量或時發生問題，因為已超過資源，並決定是否時間 tooadjust hello 效能層級和[服務層](sql-database-service-tiers.md)您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="82177-106">Monitoring helps you  determine whether your database has excess capacity or is having trouble because resources are maxed out, and then decide whether it's time tooadjust hello performance level and [service tier](sql-database-service-tiers.md) of your database.</span></span> <span data-ttu-id="82177-107">您可以監視您的資料庫使用圖形化工具中 hello [Azure 入口網站](https://portal.azure.com)或使用 SQL[動態管理檢視](https://msdn.microsoft.com/library/ms188754.aspx)。</span><span class="sxs-lookup"><span data-stu-id="82177-107">You can monitor your database using graphical tools in hello [Azure portal](https://portal.azure.com) or using SQL [dynamic management views](https://msdn.microsoft.com/library/ms188754.aspx).</span></span>

## <a name="monitor-databases-using-hello-azure-portal"></a><span data-ttu-id="82177-108">監視使用 hello Azure 入口網站的資料庫</span><span class="sxs-lookup"><span data-stu-id="82177-108">Monitor databases using hello Azure portal</span></span>
<span data-ttu-id="82177-109">在 hello [Azure 入口網站](https://portal.azure.com/)，您可以監視單一資料庫的使用率選取您的資料庫，然後按一下 hello**監視**圖表。</span><span class="sxs-lookup"><span data-stu-id="82177-109">In hello [Azure portal](https://portal.azure.com/), you can monitor a single database’s utilization by selecting your database and clicking hello **Monitoring** chart.</span></span> <span data-ttu-id="82177-110">這會開啟**度量**視窗中，您可以按一下 hello**編輯圖表** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82177-110">This brings up a **Metric** window that you can change by clicking hello **Edit chart** button.</span></span> <span data-ttu-id="82177-111">新增下列度量的 hello:</span><span class="sxs-lookup"><span data-stu-id="82177-111">Add hello following metrics:</span></span>

* <span data-ttu-id="82177-112">CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="82177-112">CPU percentage</span></span>
* <span data-ttu-id="82177-113">DTU 百分比</span><span class="sxs-lookup"><span data-stu-id="82177-113">DTU percentage</span></span>
* <span data-ttu-id="82177-114">資料 IO 百分比</span><span class="sxs-lookup"><span data-stu-id="82177-114">Data IO percentage</span></span>
* <span data-ttu-id="82177-115">資料庫大小百分比</span><span class="sxs-lookup"><span data-stu-id="82177-115">Database size percentage</span></span>

<span data-ttu-id="82177-116">一旦您已經新增這些度量，您可以繼續 tooview 中 hello**監視**hello 上更多詳細資料圖表**度量**視窗。</span><span class="sxs-lookup"><span data-stu-id="82177-116">Once you’ve added these metrics, you can continue tooview them in hello **Monitoring** chart with more details on hello **Metric** window.</span></span> <span data-ttu-id="82177-117">所有四個度量顯示 hello 平均使用率百分比相對 toohello **DTU**您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="82177-117">All four metrics show hello average utilization percentage relative toohello **DTU** of your database.</span></span> <span data-ttu-id="82177-118">請參閱 hello[服務層](sql-database-service-tiers.md)Dtu 的詳細資料的發行項。</span><span class="sxs-lookup"><span data-stu-id="82177-118">See hello [service tiers](sql-database-service-tiers.md) article for details about DTUs.</span></span>

![資料庫效能的服務層監視。](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

<span data-ttu-id="82177-120">您也可以在 hello 效能度量上設定警示。</span><span class="sxs-lookup"><span data-stu-id="82177-120">You can also configure alerts on hello performance metrics.</span></span> <span data-ttu-id="82177-121">按一下 hello**新增警示**按鈕在 hello**度量**視窗。</span><span class="sxs-lookup"><span data-stu-id="82177-121">Click hello **Add alert** button in hello **Metric** window.</span></span> <span data-ttu-id="82177-122">請遵循 hello 精靈 tooconfigure 您的警示。</span><span class="sxs-lookup"><span data-stu-id="82177-122">Follow hello wizard tooconfigure your alert.</span></span> <span data-ttu-id="82177-123">您擁有 hello 選項 tooalert hello 度量超出某個臨界值時，或 hello 低於特定臨界值。</span><span class="sxs-lookup"><span data-stu-id="82177-123">You have hello option tooalert if hello metrics exceed a certain threshold or if hello metric falls below a certain threshold.</span></span>

<span data-ttu-id="82177-124">例如，如果您預期資料庫 toogrow hello 工作負載，您可以選擇 tooconfigure 電子郵件警示每當資料庫達到 80%時任何 hello 效能計量。</span><span class="sxs-lookup"><span data-stu-id="82177-124">For example, if you expect hello workload on your database toogrow, you can choose tooconfigure an email alert whenever your database reaches 80% on any of hello performance metrics.</span></span> <span data-ttu-id="82177-125">您可以使用這個早期的警告 toofigure out 時，您可能必須 tooswitch toohello 下一個較高的效能層級。</span><span class="sxs-lookup"><span data-stu-id="82177-125">You can use this as an early warning toofigure out when you might have tooswitch toohello next higher performance level.</span></span>

<span data-ttu-id="82177-126">hello 效能度量也可協助您判斷您是否能 toodowngrade tooa 低效能層級。</span><span class="sxs-lookup"><span data-stu-id="82177-126">hello performance metrics can also help you determine if you are able toodowngrade tooa lower performance level.</span></span> <span data-ttu-id="82177-127">假設您使用標準 S2 」 資料庫，而平均 hello 資料庫的所有效能度量顯示不都使用任何給定的時間超過 10%。</span><span class="sxs-lookup"><span data-stu-id="82177-127">Assume you are using a Standard S2 database and all performance metrics show that hello database on average does not use more than 10% at any given time.</span></span> <span data-ttu-id="82177-128">很可能標準 S1 中的 hello 資料庫運作。</span><span class="sxs-lookup"><span data-stu-id="82177-128">It is likely that hello database will work well in Standard S1.</span></span> <span data-ttu-id="82177-129">不過，請注意暴增或波動之前 hello 決策 toomove tooa 低效能層級的工作負載。</span><span class="sxs-lookup"><span data-stu-id="82177-129">However, be aware of workloads that spike or fluctuate before making hello decision toomove tooa lower performance level.</span></span>

## <a name="monitor-databases-using-dmvs"></a><span data-ttu-id="82177-130">使用 DMV 監視資料庫</span><span class="sxs-lookup"><span data-stu-id="82177-130">Monitor databases using DMVs</span></span>
<span data-ttu-id="82177-131">hello hello 入口網站中公開的相同度量也會提供透過系統檢視表： [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) hello 邏輯中**主要**您伺服器的資料庫和[sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) hello 使用者資料庫中。</span><span class="sxs-lookup"><span data-stu-id="82177-131">hello same metrics that are exposed in hello portal are also available through system views: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) in hello logical **master** database of your server, and [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) in hello user database.</span></span> <span data-ttu-id="82177-132">使用**sys.resource_stats**如果您需要更精細的資料少 toomonitor 長的時間。</span><span class="sxs-lookup"><span data-stu-id="82177-132">Use **sys.resource_stats** if you need toomonitor less granular data across a longer period of time.</span></span> <span data-ttu-id="82177-133">使用**sys.dm_db_resource_stats**如果您需要 toomonitor 較精細的資料較小的時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="82177-133">Use **sys.dm_db_resource_stats** if you need toomonitor more granular data within a smaller time frame.</span></span> <span data-ttu-id="82177-134">如需詳細資訊，請參閱 [Azure SQL Database 效能指引](sql-database-single-database-monitor.md#monitor-resource-use)。</span><span class="sxs-lookup"><span data-stu-id="82177-134">For more information, see [Azure SQL Database Performance Guidance](sql-database-single-database-monitor.md#monitor-resource-use).</span></span>

> [!NOTE]
> <span data-ttu-id="82177-135">使用於 Web 和 Business Edition 資料庫 (已淘汰) 時，**sys.dm_db_resource_stats** 會傳回空的結果集。</span><span class="sxs-lookup"><span data-stu-id="82177-135">**sys.dm_db_resource_stats** returns an empty result set when used in Web and Business edition databases, which are retired.</span></span>
>
>

### <a name="monitor-resource-use"></a><span data-ttu-id="82177-136">監視資源使用量</span><span class="sxs-lookup"><span data-stu-id="82177-136">Monitor resource use</span></span>

<span data-ttu-id="82177-137">您可以使用 [SQL Database 查詢效能深入解析](sql-database-query-performance.md)和[查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx)來監視資源用量。</span><span class="sxs-lookup"><span data-stu-id="82177-137">You can monitor resource usage using [SQL Database Query Performance Insight](sql-database-query-performance.md) and [Query Store](https://msdn.microsoft.com/library/dn817826.aspx).</span></span>

<span data-ttu-id="82177-138">您也可以使用以下兩種檢視來監視用量：</span><span class="sxs-lookup"><span data-stu-id="82177-138">You can also monitor usage using these two views:</span></span>

* [<span data-ttu-id="82177-139">sys.dm_db_resource_stats</span><span class="sxs-lookup"><span data-stu-id="82177-139">sys.dm_db_resource_stats</span></span>](https://msdn.microsoft.com/library/dn800981.aspx)
* [<span data-ttu-id="82177-140">sys.resource_stats</span><span class="sxs-lookup"><span data-stu-id="82177-140">sys.resource_stats</span></span>](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a><span data-ttu-id="82177-141">sys.dm_db_resource_stats</span><span class="sxs-lookup"><span data-stu-id="82177-141">sys.dm_db_resource_stats</span></span>
<span data-ttu-id="82177-142">您可以使用 hello [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)每個 SQL database 中的檢視。</span><span class="sxs-lookup"><span data-stu-id="82177-142">You can use hello [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) view in every SQL database.</span></span> <span data-ttu-id="82177-143">hello **sys.dm_db_resource_stats**檢視會顯示最近資源使用資料相對 toohello 服務層。</span><span class="sxs-lookup"><span data-stu-id="82177-143">hello **sys.dm_db_resource_stats** view shows recent resource use data relative toohello service tier.</span></span> <span data-ttu-id="82177-144">每隔 15 秒鐘就會記錄一次 CPU、資料 I/O、記錄檔寫入和記憶體的平均百分比，並且會維持 1 小時。</span><span class="sxs-lookup"><span data-stu-id="82177-144">Average percentages for CPU, data I/O, log writes, and memory are recorded every 15 seconds and are maintained for 1 hour.</span></span>

<span data-ttu-id="82177-145">因為此檢視會提供更細微的資源使用量資訊，請先使用 **sys.dm_db_resource_stats** 來進行任何現狀分析或疑難排解。</span><span class="sxs-lookup"><span data-stu-id="82177-145">Because this view provides a more granular look at resource use, use **sys.dm_db_resource_stats** first for any current-state analysis or troubleshooting.</span></span> <span data-ttu-id="82177-146">比方說，此查詢會顯示 hello 平均值和最大資源用於 hello 目前資料庫上 hello 過去一小時：</span><span class="sxs-lookup"><span data-stu-id="82177-146">For example, this query shows hello average and maximum resource use for hello current database over hello past hour:</span></span>

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

<span data-ttu-id="82177-147">其他查詢，請參閱中的 hello 範例[sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)。</span><span class="sxs-lookup"><span data-stu-id="82177-147">For other queries, see hello examples in [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).</span></span>

#### <a name="sysresourcestats"></a><span data-ttu-id="82177-148">sys.resource_stats</span><span class="sxs-lookup"><span data-stu-id="82177-148">sys.resource_stats</span></span>
<span data-ttu-id="82177-149">hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)  檢視中 hello**主要**資料庫具有可協助您監視您的 SQL database 在其特定的服務層和效能層級的 hello 效能的其他資訊.</span><span class="sxs-lookup"><span data-stu-id="82177-149">hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) view in hello **master** database has additional information that can help you monitor hello performance of your SQL database at its specific service tier and performance level.</span></span> <span data-ttu-id="82177-150">hello 資料會收集每隔 5 分鐘，並維護的大約可返回 35 天。</span><span class="sxs-lookup"><span data-stu-id="82177-150">hello data is collected every 5 minutes and is maintained for approximately 35 days.</span></span> <span data-ttu-id="82177-151">這個檢視適合用於進行 SQL Database 如何使用資源的長期歷史分析。</span><span class="sxs-lookup"><span data-stu-id="82177-151">This view is useful for a longer-term historical analysis of how your SQL database uses resources.</span></span>

<span data-ttu-id="82177-152">hello 下圖顯示 hello CPU 資源的使用以 hello P2 效能層級的 Premium 資料庫的每個小時一週。</span><span class="sxs-lookup"><span data-stu-id="82177-152">hello following graph shows hello CPU resource use for a Premium database with hello P2 performance level for each hour in a week.</span></span> <span data-ttu-id="82177-153">下圖從星期一開始，顯示 5 個工作日，然後才顯示週末，當多小於 hello 應用程式上發生的狀況。</span><span class="sxs-lookup"><span data-stu-id="82177-153">This graph starts on a Monday, shows 5 work days, and then shows a weekend, when much less happens on hello application.</span></span>

![SQL Database 的資源使用量](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

<span data-ttu-id="82177-155">Hello 資料從這個資料庫目前的尖峰 CPU 負載剛好超過 50%的 CPU 使用相對 toohello P2 效能層級 （星期二中午）。</span><span class="sxs-lookup"><span data-stu-id="82177-155">From hello data, this database currently has a peak CPU load of just over 50 percent CPU use relative toohello P2 performance level (midday on Tuesday).</span></span> <span data-ttu-id="82177-156">如果 CPU 是 hello 應用程式的資源設定檔中的 hello 主控項因素，您可能決定 P2 是右邊一律 hello 工作負載的效能層級 tooguarantee 符合 hello。</span><span class="sxs-lookup"><span data-stu-id="82177-156">If CPU is hello dominant factor in hello application’s resource profile, then you might decide that P2 is hello right performance level tooguarantee that hello workload always fits.</span></span> <span data-ttu-id="82177-157">如果您預期應用程式 toogrow 經過一段時間，它是個不錯的主意 toohave 額外的資源緩衝，如此 hello 應用程式不會達到 hello 效能層級限制也一樣。</span><span class="sxs-lookup"><span data-stu-id="82177-157">If you expect an application toogrow over time, it's a good idea toohave an extra resource buffer so that hello application doesn't ever reach hello performance-level limit.</span></span> <span data-ttu-id="82177-158">如果您增加 hello 效能層級，您可以協助避免客戶可見錯誤時資料庫沒有足夠的電力 tooprocess 要求有效，尤其是在延遲的環境可能會發生。</span><span class="sxs-lookup"><span data-stu-id="82177-158">If you increase hello performance level, you can help avoid customer-visible errors that might occur when a database doesn't have enough power tooprocess requests effectively, especially in latency-sensitive environments.</span></span> <span data-ttu-id="82177-159">例如，資料庫可支援繪製根據資料庫呼叫 hello 結果的網頁應用程式。</span><span class="sxs-lookup"><span data-stu-id="82177-159">An example is a database that supports an application that paints webpages based on hello results of database calls.</span></span>

<span data-ttu-id="82177-160">其他應用程式類型可能解譯的 hello 相同圖形以不同的方式。</span><span class="sxs-lookup"><span data-stu-id="82177-160">Other application types might interpret hello same graph differently.</span></span> <span data-ttu-id="82177-161">例如，如果應用程式嘗試 tooprocess 薪資資料每一天，而且具有 hello 相同的圖表，這種 「 批次作業 」 模型可能會正常執行 P1 效能層級。</span><span class="sxs-lookup"><span data-stu-id="82177-161">For example, if an application tries tooprocess payroll data each day and has hello same chart, this kind of "batch job" model might do fine at a P1 performance level.</span></span> <span data-ttu-id="82177-162">hello P1 效能層級在 hello P2 效能層級有 100 Dtu 比較 too200 Dtu。</span><span class="sxs-lookup"><span data-stu-id="82177-162">hello P1 performance level has 100 DTUs compared too200 DTUs at hello P2 performance level.</span></span> <span data-ttu-id="82177-163">hello P1 效能層級提供 hello P2 效能層級的一半 hello 的效能。</span><span class="sxs-lookup"><span data-stu-id="82177-163">hello P1 performance level provides half hello performance of hello P2 performance level.</span></span> <span data-ttu-id="82177-164">因此，P2 中 50% 的 CPU 使用量等於 P1 中 100% 的 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="82177-164">So, 50 percent of CPU use in P2 equals 100 percent CPU use in P1.</span></span> <span data-ttu-id="82177-165">如果 hello 應用程式沒有逾時，它可能不重要如果作業需要 2 小時或 2.5 個小時 toofinish 如果今天。</span><span class="sxs-lookup"><span data-stu-id="82177-165">If hello application does not have timeouts, it might not matter if a job takes 2 hours or 2.5 hours toofinish, if it gets done today.</span></span> <span data-ttu-id="82177-166">這個類別中的應用程式或許可以使用 P1 效能等級。</span><span class="sxs-lookup"><span data-stu-id="82177-166">An application in this category probably can use a P1 performance level.</span></span> <span data-ttu-id="82177-167">您可以利用 hello 事實是 hello 天資源使用量較低，使任何 「 高尖峰 」 可能會 「 溢出 」 的一個低谷 hello hello 天中稍後的時段。</span><span class="sxs-lookup"><span data-stu-id="82177-167">You can take advantage of hello fact that there are periods of time during hello day when resource use is lower, so that any "big peak" might spill over into one of hello troughs later in hello day.</span></span> <span data-ttu-id="82177-168">只要 hello 作業可以在每日時間完成，可能適合使用該類型的應用程式，儲存金錢 hello P1 效能層級。</span><span class="sxs-lookup"><span data-stu-id="82177-168">hello P1 performance level might be good for that kind of application (and save money), as long as hello jobs can finish on time each day.</span></span>

<span data-ttu-id="82177-169">Azure SQL Database 會公開使用的資源資訊中每個作用中資料庫 hello **sys.resource_stats**檢視 hello**主要**每一部伺服器中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="82177-169">Azure SQL Database exposes consumed resource information for each active database in hello **sys.resource_stats** view of hello **master** database in each server.</span></span> <span data-ttu-id="82177-170">hello 資料表中的 hello 資料會彙總每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="82177-170">hello data in hello table is aggregated for 5-minute intervals.</span></span> <span data-ttu-id="82177-171">Hello Basic、 Standard 和 Premium 服務層時，hello 資料可能要花超過 5 分鐘 tooappear hello 資料表中，因此這項資料是歷程分析，而不是接近即時的分析更有用。</span><span class="sxs-lookup"><span data-stu-id="82177-171">With hello Basic, Standard, and Premium service tiers, hello data can take more than 5 minutes tooappear in hello table, so this data is more useful for historical analysis rather than near-real-time analysis.</span></span> <span data-ttu-id="82177-172">查詢 hello **sys.resource_stats** toosee hello 最近的資料庫和 toovalidate hello 保留您選擇傳送您想要在需要時 hello 效能歷程的檢視。</span><span class="sxs-lookup"><span data-stu-id="82177-172">Query hello **sys.resource_stats** view toosee hello recent history of a database and toovalidate whether hello reservation you chose delivered hello performance you want when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="82177-173">您必須是連接的 toohello**主要**資料庫的邏輯的 SQL 資料庫伺服器 tooquery **sys.resource_stats** hello 遵循範例中。</span><span class="sxs-lookup"><span data-stu-id="82177-173">You must be connected toohello **master** database of your logical SQL database server tooquery **sys.resource_stats** in hello following examples.</span></span>
> 
> 

<span data-ttu-id="82177-174">此範例將示範如何將這個檢視中的 hello 資料會公開：</span><span class="sxs-lookup"><span data-stu-id="82177-174">This example shows you how hello data in this view is exposed:</span></span>

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![hello sys.resource_stats 目錄檢視](./media/sql-database-performance-guidance/sys_resource_stats.png)

<span data-ttu-id="82177-176">hello 下一個範例將示範不同的方式，您可以使用 hello **sys.resource_stats**目錄檢視有關您的 SQL 資料庫使用資源的方式 tooget 資訊：</span><span class="sxs-lookup"><span data-stu-id="82177-176">hello next example shows you different ways that you can use hello **sys.resource_stats** catalog view tooget information about how your SQL database uses resources:</span></span>

1. <span data-ttu-id="82177-177">在過去一週的資源 hello toolook hello 資料庫 userdb1 使用，您可以執行這個查詢：</span><span class="sxs-lookup"><span data-stu-id="82177-177">toolook at hello past week’s resource use for hello database userdb1, you can run this query:</span></span>
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. <span data-ttu-id="82177-178">tooevaluate 方式以及您的工作負載符合 hello 效能層級，您需要 toodrill 向下到 hello 資源度量的每個層面： CPU、 讀取、 寫入、 背景工作數目和工作階段數目。</span><span class="sxs-lookup"><span data-stu-id="82177-178">tooevaluate how well your workload fits hello performance level, you need toodrill down into each aspect of hello resource metrics: CPU, reads, writes, number of workers, and number of sessions.</span></span> <span data-ttu-id="82177-179">以下是一個修訂過查詢使用**sys.resource_stats** tooreport hello 這些資源度量的平均值和最大值：</span><span class="sxs-lookup"><span data-stu-id="82177-179">Here's a revised query using **sys.resource_stats** tooreport hello average and maximum values of these resource metrics:</span></span>
   
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
3. <span data-ttu-id="82177-180">使用各項資源度量的這個 hello 平均值和最大值相關的資訊，您可以評估您的工作負載符合您選擇的 hello 效能層級的程度。</span><span class="sxs-lookup"><span data-stu-id="82177-180">With this information about hello average and maximum values of each resource metric, you can assess how well your workload fits into hello performance level you chose.</span></span> <span data-ttu-id="82177-181">通常，平均值從**sys.resource_stats**可讓您針對 hello 目標大小的理想基準 toouse。</span><span class="sxs-lookup"><span data-stu-id="82177-181">Usually, average values from **sys.resource_stats** give you a good baseline toouse against hello target size.</span></span> <span data-ttu-id="82177-182">它應該是您主要的量尺。</span><span class="sxs-lookup"><span data-stu-id="82177-182">It should be your primary measurement stick.</span></span> <span data-ttu-id="82177-183">如需範例，您可能使用 hello Standard 服務層搭配 S2 效能層級。</span><span class="sxs-lookup"><span data-stu-id="82177-183">For an example, you might be using hello Standard service tier with S2 performance level.</span></span> <span data-ttu-id="82177-184">hello 平均使用百分比的 CPU 和 I/O 讀取和寫入為 40%下方、 hello 平均背景工作數目低於 50，和 hello 平均工作階段數目低於 200。</span><span class="sxs-lookup"><span data-stu-id="82177-184">hello average use percentages for CPU and I/O reads and writes are below 40 percent, hello average number of workers is below 50, and hello average number of sessions is below 200.</span></span> <span data-ttu-id="82177-185">您的工作負載可能符合 S1 效能層級 hello。</span><span class="sxs-lookup"><span data-stu-id="82177-185">Your workload might fit into hello S1 performance level.</span></span> <span data-ttu-id="82177-186">是，並輕鬆 toosee hello 背景工作和工作階段限制納入您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="82177-186">It's easy toosee whether your database fits in hello worker and session limits.</span></span> <span data-ttu-id="82177-187">toosee tooCPU、 讀取和寫入時，資料庫是否符合較低的效能層級與目前 hello hello 較低效能層級的 DTU 數字除以 hello 目前的效能層級的 DTU 數目，然後再乘 100 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="82177-187">toosee whether a database fits into a lower performance level with regards tooCPU, reads, and writes, divide hello DTU number of hello lower performance level by hello DTU number of your current performance level, and then multiply hello result by 100:</span></span>
   
    <span data-ttu-id="82177-188">**S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**</span><span class="sxs-lookup"><span data-stu-id="82177-188">**S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**</span></span>
   
    <span data-ttu-id="82177-189">hello 結果為 hello hello 兩個效能層級之間以百分比為單位的相對效能差異。</span><span class="sxs-lookup"><span data-stu-id="82177-189">hello result is hello relative performance difference between hello two performance levels in percentage.</span></span> <span data-ttu-id="82177-190">如果資源使用不超過此數量時，您的工作負載可能符合較低效能層級 hello。</span><span class="sxs-lookup"><span data-stu-id="82177-190">If your resource use doesn't exceed this amount, your workload might fit into hello lower performance level.</span></span> <span data-ttu-id="82177-191">不過，您需要的資源使用的值，所有範圍 toolook，並判斷您的資料庫工作負載會放入 hello 低效能層級的頻率，請依百分比。</span><span class="sxs-lookup"><span data-stu-id="82177-191">However, you need toolook at all ranges of resource use values, and determine, by percentage, how often your database workload would fit into hello lower performance level.</span></span> <span data-ttu-id="82177-192">hello 下列查詢會輸出 hello 適合每一資源維度，根據我們在此範例中計算出的 40%的 hello 臨界值百分比：</span><span class="sxs-lookup"><span data-stu-id="82177-192">hello following query outputs hello fit percentage per resource dimension, based on hello threshold of 40 percent that we calculated in this example:</span></span>
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    <span data-ttu-id="82177-193">根據您的資料庫服務等級目標 (SLO)，您可以決定 hello 較低效能層級是否符合您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="82177-193">Based on your database service level objective (SLO), you can decide whether your workload fits into hello lower performance level.</span></span> <span data-ttu-id="82177-194">如果您的資料庫工作負載 SLO 是 99.9 %hello 上述查詢會傳回值大於 99.9%的所有三個資源維度，您的工作負載可能會納入 hello 低效能層級。</span><span class="sxs-lookup"><span data-stu-id="82177-194">If your database workload SLO is 99.9 percent and hello preceding query returns values greater than 99.9 percent for all three resource dimensions, your workload likely fits into hello lower performance level.</span></span>
   
    <span data-ttu-id="82177-195">查看符合 hello 百分比也可讓您深入了解是否應該一併移動 toohello 下一個較高的效能層級 toomeet 您的 SLO。</span><span class="sxs-lookup"><span data-stu-id="82177-195">Looking at hello fit percentage also gives you insight into whether you should move toohello next higher performance level toomeet your SLO.</span></span> <span data-ttu-id="82177-196">例如，userdb1 顯示 hello 下列過去一週的 CPU 使用量 hello:</span><span class="sxs-lookup"><span data-stu-id="82177-196">For example, userdb1 shows hello following CPU use for hello past week:</span></span>
   
   | <span data-ttu-id="82177-197">平均 CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="82177-197">Average CPU percent</span></span> | <span data-ttu-id="82177-198">最大 CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="82177-198">Maximum CPU percent</span></span> |
   | --- | --- |
   | <span data-ttu-id="82177-199">24.5</span><span class="sxs-lookup"><span data-stu-id="82177-199">24.5</span></span> |<span data-ttu-id="82177-200">100.00</span><span class="sxs-lookup"><span data-stu-id="82177-200">100.00</span></span> |
   
    <span data-ttu-id="82177-201">hello 平均 CPU 大約是一季的 hello 限制 hello 效能層級，它也會納入 hello hello 資料庫效能層級。</span><span class="sxs-lookup"><span data-stu-id="82177-201">hello average CPU is about a quarter of hello limit of hello performance level, which would fit well into hello performance level of hello database.</span></span> <span data-ttu-id="82177-202">但是，hello 最大值會顯示該 hello 資料庫到達 hello hello 效能層級上限。</span><span class="sxs-lookup"><span data-stu-id="82177-202">But, hello maximum value shows that hello database reaches hello limit of hello performance level.</span></span> <span data-ttu-id="82177-203">您需要 toomove toohello 下一個較高的效能層級嗎？</span><span class="sxs-lookup"><span data-stu-id="82177-203">Do you need toomove toohello next higher performance level?</span></span> <span data-ttu-id="82177-204">查看如何多次工作負載達到 100%，然後比較 tooyour 資料庫工作負載 SLO。</span><span class="sxs-lookup"><span data-stu-id="82177-204">Look at how many times your workload reaches 100 percent, and then compare it tooyour database workload SLO.</span></span>
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    <span data-ttu-id="82177-205">如果此查詢傳回的值小於 99.9%的任何 hello 三個資源維度，請考慮可能是移動 toohello 下一個效能層級，或 hello SQL 資料庫上使用應用程式微調技術 tooreduce hello 負載。</span><span class="sxs-lookup"><span data-stu-id="82177-205">If this query returns a value less than 99.9 percent for any of hello three resource dimensions, consider either moving toohello next higher performance level or use application-tuning techniques tooreduce hello load on hello SQL database.</span></span>
4. <span data-ttu-id="82177-206">這個練習中也會考慮 hello 您預計的工作負載增加未來。</span><span class="sxs-lookup"><span data-stu-id="82177-206">This exercise also considers your projected workload increase in hello future.</span></span>

<span data-ttu-id="82177-207">彈性集區，您可以使用本節中所述的 hello 技巧監視 hello 集區中的個別資料庫。</span><span class="sxs-lookup"><span data-stu-id="82177-207">For elastic pools, you can monitor individual databases in hello pool with hello techniques described in this section.</span></span> <span data-ttu-id="82177-208">但是，您也可以監視整體的 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="82177-208">But you can also monitor hello pool as a whole.</span></span> <span data-ttu-id="82177-209">如需詳細資訊，請參閱 [監視和管理彈性集區](sql-database-elastic-pool-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="82177-209">For information, see [Monitor and manage an elastic pool](sql-database-elastic-pool-manage-portal.md).</span></span>


### <a name="maximum-concurrent-requests"></a><span data-ttu-id="82177-210">並行要求數上限</span><span class="sxs-lookup"><span data-stu-id="82177-210">Maximum concurrent requests</span></span>
<span data-ttu-id="82177-211">toosee hello 並行要求數量，您的 SQL 資料庫上執行此 TRANSACT-SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="82177-211">toosee hello number of concurrent requests, run this Transact-SQL query on your SQL database:</span></span>

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

<span data-ttu-id="82177-212">tooanalyze hello 工作負載，在內部部署 SQL Server 資料庫，修改此查詢 toofilter 想 tooanalyze hello 特定資料庫上。</span><span class="sxs-lookup"><span data-stu-id="82177-212">tooanalyze hello workload of an on-premises SQL Server database, modify this query toofilter on hello specific database you want tooanalyze.</span></span> <span data-ttu-id="82177-213">比方說，如果您擁有名為 MyDatabase 在內部部署資料庫時，此 Transact SQL 查詢會傳回 hello 計數的並行要求該資料庫中：</span><span class="sxs-lookup"><span data-stu-id="82177-213">For example, if you have an on-premises database named MyDatabase, this Transact-SQL query returns hello count of concurrent requests in that database:</span></span>

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

<span data-ttu-id="82177-214">這只是單一時間點的快照。</span><span class="sxs-lookup"><span data-stu-id="82177-214">This is just a snapshot at a single point in time.</span></span> <span data-ttu-id="82177-215">tooget 進一步了解您的工作負載和並行要求的需求，您將需要 toocollect 經過一段時間的許多範例。</span><span class="sxs-lookup"><span data-stu-id="82177-215">tooget a better understanding of your workload and concurrent request requirements, you'll need toocollect many samples over time.</span></span>

### <a name="maximum-concurrent-logins"></a><span data-ttu-id="82177-216">並行登入數上限</span><span class="sxs-lookup"><span data-stu-id="82177-216">Maximum concurrent logins</span></span>
<span data-ttu-id="82177-217">您可以分析您使用者和應用程式模式 tooget hello 頻率的登入的了解。</span><span class="sxs-lookup"><span data-stu-id="82177-217">You can analyze your user and application patterns tooget an idea of hello frequency of logins.</span></span> <span data-ttu-id="82177-218">您也可以執行實際負載測試環境 toomake 確定您在不遇到這個或其他限制，我們在本文中討論。</span><span class="sxs-lookup"><span data-stu-id="82177-218">You also can run real-world loads in a test environment toomake sure that you're not hitting this or other limits we discuss in this article.</span></span> <span data-ttu-id="82177-219">沒有任何單一查詢或動態管理檢視 (DMV) 可以向您顯示並行登入計數或歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="82177-219">There isn’t a single query or dynamic management view (DMV) that can show you concurrent login counts or history.</span></span>

<span data-ttu-id="82177-220">如果使用多個用戶端 hello 相同的連接字串 hello 服務會驗證每個登入。</span><span class="sxs-lookup"><span data-stu-id="82177-220">If multiple clients use hello same connection string, hello service authenticates each login.</span></span> <span data-ttu-id="82177-221">如果 10 個使用者同時連接使用 tooa 資料庫 hello 相同使用者名稱和密碼，會有 10 個並行登入。</span><span class="sxs-lookup"><span data-stu-id="82177-221">If 10 users simultaneously connect tooa database by using hello same username and password, there would be 10 concurrent logins.</span></span> <span data-ttu-id="82177-222">這項限制適用於僅 hello 登入與驗證 toohello 持續時間。</span><span class="sxs-lookup"><span data-stu-id="82177-222">This limit applies only toohello duration of hello login and authentication.</span></span> <span data-ttu-id="82177-223">如果 hello 相同 10 使用者依序連接 toohello 資料庫，並行登入的 hello 數目會絕對不大於 1。</span><span class="sxs-lookup"><span data-stu-id="82177-223">If hello same 10 users connect toohello database sequentially, hello number of concurrent logins would never be greater than 1.</span></span>

> [!NOTE]
> <span data-ttu-id="82177-224">目前，這項限制不適用 toodatabases 彈性集區中。</span><span class="sxs-lookup"><span data-stu-id="82177-224">Currently, this limit does not apply toodatabases in elastic pools.</span></span>
> 
> 

### <a name="maximum-sessions"></a><span data-ttu-id="82177-225">工作階段數上限</span><span class="sxs-lookup"><span data-stu-id="82177-225">Maximum sessions</span></span>
<span data-ttu-id="82177-226">toosee hello 目前作用中工作階段數目，您的 SQL 資料庫上執行此 TRANSACT-SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="82177-226">toosee hello number of current active sessions, run this Transact-SQL query on your SQL database:</span></span>

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

<span data-ttu-id="82177-227">如果您正在分析之內部部署 SQL Server 工作負載，修改 hello 查詢 toofocus 上特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="82177-227">If you're analyzing an on-premises SQL Server workload, modify hello query toofocus on a specific database.</span></span> <span data-ttu-id="82177-228">此查詢可協助您判斷可能的工作階段需求 hello 資料庫，如果您考慮將它移 tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="82177-228">This query helps you determine possible session needs for hello database if you are considering moving it tooAzure SQL Database.</span></span>

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

<span data-ttu-id="82177-229">同樣地，這些查詢傳回的是某一時間點的計數。</span><span class="sxs-lookup"><span data-stu-id="82177-229">Again, these queries return a point-in-time count.</span></span> <span data-ttu-id="82177-230">如果您收集一段時間的多個範例，您就必須 hello 充分瞭解您的工作階段使用。</span><span class="sxs-lookup"><span data-stu-id="82177-230">If you collect multiple samples over time, you’ll have hello best understanding of your session use.</span></span>

<span data-ttu-id="82177-231">SQL Database 的分析，您可以取得歷程記錄統計資料工作階段藉由查詢 hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)檢視和檢閱 hello **active_session_count**資料行。</span><span class="sxs-lookup"><span data-stu-id="82177-231">For SQL Database analysis, you can get historical statistics on sessions by querying hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) view and reviewing hello **active_session_count** column.</span></span> 
