---
title: "aaaAzure SQL 資料倉儲備份快照，異地備援 |Microsoft 文件"
description: "了解 SQL 資料倉儲內建的資料庫備份可讓您 toorestore Azure SQL 資料倉儲 tooa 還原點不同的地理區域。"
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a><span data-ttu-id="96b44-103">SQL 資料倉儲備份</span><span class="sxs-lookup"><span data-stu-id="96b44-103">SQL Data Warehouse backups</span></span>
<span data-ttu-id="96b44-104">SQL 資料倉儲備份提供本機和異地備份做為其資料倉儲備份功能的一部份。</span><span class="sxs-lookup"><span data-stu-id="96b44-104">SQL Data Warehouse offers both local and geographical backups as part of its data warehouse backup capabilities.</span></span> <span data-ttu-id="96b44-105">這些包括 Azure 儲存體 Blob 快照集和異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="96b44-105">These include Azure Storage Blob snapshots and geo-redundant storage.</span></span> <span data-ttu-id="96b44-106">使用資料倉儲備份 toorestore 資料倉儲 tooa 還原點在 hello 主要區域中，或還原 tooa 不同的地理區域。</span><span class="sxs-lookup"><span data-stu-id="96b44-106">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or restore tooa different geographical region.</span></span> <span data-ttu-id="96b44-107">本文說明 hello 細節 SQL 資料倉儲中的備份。</span><span class="sxs-lookup"><span data-stu-id="96b44-107">This article explains hello specifics of backups in SQL Data Warehouse.</span></span>

## <a name="what-is-a-data-warehouse-backup"></a><span data-ttu-id="96b44-108">什麼是資料倉儲備份？</span><span class="sxs-lookup"><span data-stu-id="96b44-108">What is a data warehouse backup?</span></span>
<span data-ttu-id="96b44-109">在資料倉儲備份，hello 資料，您可以使用 toorestore 資料倉儲 tooa 特定時間。</span><span class="sxs-lookup"><span data-stu-id="96b44-109">A data warehouse backup is hello data that you can use toorestore a data warehouse tooa specific time.</span></span>  <span data-ttu-id="96b44-110">由於 SQL 資料倉儲是一個分散式系統，所以一個資料倉儲備份是由儲存在 Azure Blob 中的許多檔案組成。</span><span class="sxs-lookup"><span data-stu-id="96b44-110">Since SQL Data Warehouse is a distributed system, a data warehouse backup consists of many files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="96b44-111">資料庫備份可保護資料免於意外損毀或刪除，是商務持續性和災害復原策略中不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="96b44-111">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span></span> <span data-ttu-id="96b44-112">如需詳細資訊，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="96b44-112">For more information, see [Business continuity overview](../sql-database/sql-database-business-continuity.md).</span></span>

## <a name="data-redundancy"></a><span data-ttu-id="96b44-113">資料備援</span><span class="sxs-lookup"><span data-stu-id="96b44-113">Data redundancy</span></span>
<span data-ttu-id="96b44-114">SQL 資料倉儲會透過將您的資料儲存在本地備援 (LRS) Azure 進階儲存體來保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="96b44-114">SQL Data Warehouse protects your data by storing your data in locally redundant (LRS) Azure Premium Storage.</span></span> <span data-ttu-id="96b44-115">此 Azure 儲存體功能會將多份同步 hello 資料儲存在 hello 本機資料中心 tooguarantee 透明資料保護中，如果當地語系化的失敗。</span><span class="sxs-lookup"><span data-stu-id="96b44-115">This Azure Storage feature stores multiple synchronous copies of hello data in hello local data center tooguarantee transparent data protection if there are localized failures.</span></span> <span data-ttu-id="96b44-116">資料備援可確保您的資料在發生基礎結構問題 (例如磁碟故障等) 時能夠存留。</span><span class="sxs-lookup"><span data-stu-id="96b44-116">Data redundancy ensures that your data can survive infrastructure issues such as disk failures.</span></span> <span data-ttu-id="96b44-117">資料備援可利用容錯和高可用性基礎結構來確保商務持續性。</span><span class="sxs-lookup"><span data-stu-id="96b44-117">Data redundancy ensures business continuity with a fault tolerant and highly available infrastructure.</span></span>

<span data-ttu-id="96b44-118">toolearn 程式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="96b44-118">toolearn more about:</span></span>

* <span data-ttu-id="96b44-119">Azure 高階儲存體，請參閱[簡介 tooAzure 高階儲存體](../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="96b44-119">Azure Premium storage, see [Introduction tooAzure Premium Storage](../storage/common/storage-premium-storage.md).</span></span>
* <span data-ttu-id="96b44-120">本地備援儲存體，請參閱 [Azure 儲存體複寫](../storage/common/storage-redundancy.md#locally-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="96b44-120">Locally Redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md#locally-redundant-storage).</span></span>

## <a name="azure-storage-blob-snapshots"></a><span data-ttu-id="96b44-121">Azure 儲存體 Blob 快照集</span><span class="sxs-lookup"><span data-stu-id="96b44-121">Azure Storage Blob snapshots</span></span>
<span data-ttu-id="96b44-122">使用 Azure 高階儲存體的優點，作為 SQL 資料倉儲會在本機使用 Azure 儲存體 Blob 快照集 toobackup hello 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96b44-122">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello data warehouse locally.</span></span> <span data-ttu-id="96b44-123">您可以還原資料倉儲 tooa 快照集還原點。</span><span class="sxs-lookup"><span data-stu-id="96b44-123">You can restore a data warehouse tooa snapshot restore point.</span></span> <span data-ttu-id="96b44-124">快照集至少每八個小時會啟動，並且可供使用七天。</span><span class="sxs-lookup"><span data-stu-id="96b44-124">Snapshots start a minimum of every eight hours and are available for seven days.</span></span>  

<span data-ttu-id="96b44-125">toolearn 程式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="96b44-125">toolearn more about:</span></span>

* <span data-ttu-id="96b44-126">Azure Blob 快照集，請參閱[建立 Blob 快照集](../storage/blobs/storage-blob-snapshots.md)。</span><span class="sxs-lookup"><span data-stu-id="96b44-126">Azure blob snapshots, see [Create a blob snapshot](../storage/blobs/storage-blob-snapshots.md).</span></span>

## <a name="geo-redundant-backups"></a><span data-ttu-id="96b44-127">異地備援備份</span><span class="sxs-lookup"><span data-stu-id="96b44-127">Geo-redundant backups</span></span>
<span data-ttu-id="96b44-128">每 24 小時，SQL 資料倉儲儲存在標準儲存體中的 hello 完整的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96b44-128">Every 24 hours, SQL Data Warehouse stores hello full data warehouse in Standard storage.</span></span> <span data-ttu-id="96b44-129">hello 完整的資料倉儲建立 toomatch hello hello 最後一個快照集。</span><span class="sxs-lookup"><span data-stu-id="96b44-129">hello full data warehouse is created toomatch hello time of hello last snapshot.</span></span> <span data-ttu-id="96b44-130">hello 標準儲存體所屬 tooa 地理備援儲存體帳戶，具有讀取存取權 (RA-GRS)。</span><span class="sxs-lookup"><span data-stu-id="96b44-130">hello standard storage belongs tooa geo-redundant storage account with read access (RA-GRS).</span></span> <span data-ttu-id="96b44-131">hello Azure 儲存體 RA-GRS 功能複寫 hello 備份檔案 tooa[成對的資料中心](../best-practices-availability-paired-regions.md)。</span><span class="sxs-lookup"><span data-stu-id="96b44-131">hello Azure Storage RA-GRS feature replicates hello backup files tooa [paired data center](../best-practices-availability-paired-regions.md).</span></span> <span data-ttu-id="96b44-132">此地理複寫可確保萬一您無法存取主要區域中的 hello 快照集，您可以還原資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96b44-132">This geo-replication ensures you can restore data warehouse in case you cannot access hello snapshots in your primary region.</span></span> 

<span data-ttu-id="96b44-133">這項功能為預設開啟。</span><span class="sxs-lookup"><span data-stu-id="96b44-133">This feature is on by default.</span></span> <span data-ttu-id="96b44-134">如果您不想 toouse 異地備援備份，您也可以 [退出] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn)。</span><span class="sxs-lookup"><span data-stu-id="96b44-134">If you don't want toouse geo-redundant backups, you can [opt out] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span></span> 

> [!NOTE]
> <span data-ttu-id="96b44-135">在 Azure 儲存體，hello 詞彙*複寫*參考從一個位置 tooanother toocopying 檔案。</span><span class="sxs-lookup"><span data-stu-id="96b44-135">In Azure storage, hello term *replication* refers toocopying files from one location tooanother.</span></span> <span data-ttu-id="96b44-136">SQL 的*資料庫複寫*參考 tookeeping toomultiple 次要資料庫與主要資料庫同步處理。</span><span class="sxs-lookup"><span data-stu-id="96b44-136">SQL's *database replication* refers tookeeping toomultiple secondary databases synchronized with a primary database.</span></span> 
> 
> 

> [!NOTE]
> <span data-ttu-id="96b44-137">您無法選擇退出 DWU 9000 和 DWU 18000 的異地備援備份。</span><span class="sxs-lookup"><span data-stu-id="96b44-137">You cannot opt out of geo-redundant backups with DWU 9000 and DWU 18000.</span></span> 
>
> 

<span data-ttu-id="96b44-138">toolearn 程式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="96b44-138">toolearn more about:</span></span>

* <span data-ttu-id="96b44-139">異地備援儲存體，請參閱 [Azure 儲存體複寫](../storage/common/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="96b44-139">Geo-redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md).</span></span>
* <span data-ttu-id="96b44-140">RA-GRS 儲存體：請參閱 [讀取權限異地備援儲存體](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="96b44-140">RA-GRS storage, see [Read-access geo-redundant storage](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).</span></span>

## <a name="data-warehouse-backup-schedule-and-retention-period"></a><span data-ttu-id="96b44-141">資料倉儲備份排程與保留期限</span><span class="sxs-lookup"><span data-stu-id="96b44-141">Data warehouse backup schedule and retention period</span></span>
<span data-ttu-id="96b44-142">SQL 資料倉儲線上資料倉儲上建立快照集，每隔四種 tooeight 小時和每一個快照集七天的保留。</span><span class="sxs-lookup"><span data-stu-id="96b44-142">SQL Data Warehouse creates snapshots on your online data warehouses every four tooeight hours and keeps each snapshot for seven days.</span></span> <span data-ttu-id="96b44-143">您可以還原您的線上資料庫 tooone hello 還原點 hello 在過去七天內。</span><span class="sxs-lookup"><span data-stu-id="96b44-143">You can restore your online database tooone of hello restore points in hello past seven days.</span></span> 

<span data-ttu-id="96b44-144">toosee hello 最後一個快照集啟動時，您的線上 SQL 資料倉儲上執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="96b44-144">toosee when hello last snapshot started, run this query on your online SQL Data Warehouse.</span></span> 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

<span data-ttu-id="96b44-145">如果您需要 tooretain 快照集的時間超過七天，您可以還原還原點 tooa 新的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96b44-145">If you need tooretain a snapshot for longer than seven days, you can restore a restore point tooa new data warehouse.</span></span> <span data-ttu-id="96b44-146">Hello 還原完成之後，SQL 資料倉儲會啟動 hello 新的資料倉儲上建立快照集。</span><span class="sxs-lookup"><span data-stu-id="96b44-146">After hello restore is finished, SQL Data Warehouse starts creating snapshots on hello new data warehouse.</span></span> <span data-ttu-id="96b44-147">如果您不要進行變更 toohello 新的資料倉儲，hello 快照集保持空白，因此 hello 快照成本最少。</span><span class="sxs-lookup"><span data-stu-id="96b44-147">If you don't make changes toohello new data warehouse, hello snapshots stay empty and therefore hello snapshot cost is minimal.</span></span> <span data-ttu-id="96b44-148">您也可以暫停 hello 資料庫 tookeep SQL 資料倉儲無法建立快照集。</span><span class="sxs-lookup"><span data-stu-id="96b44-148">You could also pause hello database tookeep SQL Data Warehouse from creating snapshots.</span></span>

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a><span data-ttu-id="96b44-149">發生什麼事 toomy 備份保留我的資料倉儲暫停時？</span><span class="sxs-lookup"><span data-stu-id="96b44-149">What happens toomy backup retention while my data warehouse is paused?</span></span>
<span data-ttu-id="96b44-150">暫停資料倉儲時，SQL 資料倉儲不會建立快照集，快照集也不會過期。</span><span class="sxs-lookup"><span data-stu-id="96b44-150">SQL Data Warehouse does not create snapshots and does not expire snapshots while a data warehouse is paused.</span></span> <span data-ttu-id="96b44-151">暫停 hello 資料倉儲時，不會變更 hello 快照集存在時間。</span><span class="sxs-lookup"><span data-stu-id="96b44-151">hello snapshot age does not change while hello data warehouse is paused.</span></span> <span data-ttu-id="96b44-152">快照集保留根據 hello 資料倉儲已上線，不是行事曆日期的 hello 天數。</span><span class="sxs-lookup"><span data-stu-id="96b44-152">Snapshot retention is based on hello number of days hello data warehouse is online, not calendar days.</span></span>

<span data-ttu-id="96b44-153">例如，如果快照集啟動月 1 日下午 4 點，且 hello 資料倉儲在下午 4 點暫停年 10 月 3 hello 快照就是兩天。</span><span class="sxs-lookup"><span data-stu-id="96b44-153">For example, if a snapshot starts October 1 at 4 pm and hello data warehouse is paused October 3 at 4 pm, hello snapshot is two days old.</span></span> <span data-ttu-id="96b44-154">每當 hello 資料倉儲上線 hello 快照集是兩天。</span><span class="sxs-lookup"><span data-stu-id="96b44-154">Whenever hello data warehouse comes back online hello snapshot is two days old.</span></span> <span data-ttu-id="96b44-155">如果 hello 資料倉儲上線年 10 月 5 日下午 4 點，hello 快照集就會是舊的兩天，而會保留 5 天。</span><span class="sxs-lookup"><span data-stu-id="96b44-155">If hello data warehouse comes online October 5 at 4 pm, hello snapshot is two days old and remains for five more days.</span></span>

<span data-ttu-id="96b44-156">Hello 資料倉儲回到線上時，SQL 資料倉儲繼續新的快照集，且他們皆已超過七天的資料過期的快照集。</span><span class="sxs-lookup"><span data-stu-id="96b44-156">When hello data warehouse comes back online, SQL Data Warehouse resumes new snapshots and expires snapshots when they have more than seven days of data.</span></span>

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a><span data-ttu-id="96b44-157">Hello 保留期限的已卸除的資料倉儲的時間？</span><span class="sxs-lookup"><span data-stu-id="96b44-157">How long is hello retention period for a dropped data warehouse?</span></span>
<span data-ttu-id="96b44-158">資料倉儲放置時，會儲存七天 hello 資料倉儲和 hello 快照集，然後移除。</span><span class="sxs-lookup"><span data-stu-id="96b44-158">When a data warehouse is dropped, hello data warehouse and hello snapshots are saved for seven days and then removed.</span></span> <span data-ttu-id="96b44-159">您可以還原 hello 資料倉儲 tooany hello 儲存還原點。</span><span class="sxs-lookup"><span data-stu-id="96b44-159">You can restore hello data warehouse tooany of hello saved restore points.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96b44-160">如果您刪除邏輯的 SQL server 執行個體，也會一併刪除屬於 toohello 執行個體的所有資料庫，且無法復原。</span><span class="sxs-lookup"><span data-stu-id="96b44-160">If you delete a logical SQL server instance, all databases that belong toohello instance are also deleted and cannot be recovered.</span></span> <span data-ttu-id="96b44-161">您無法還原已刪除的伺服器。</span><span class="sxs-lookup"><span data-stu-id="96b44-161">You cannot restore a deleted server.</span></span>
> 
> 

## <a name="data-warehouse-backup-costs"></a><span data-ttu-id="96b44-162">資料倉儲備份成本</span><span class="sxs-lookup"><span data-stu-id="96b44-162">Data warehouse backup costs</span></span>
<span data-ttu-id="96b44-163">hello 總成本的您的主要資料倉儲和七天的 Azure Blob 快照集是圓角的 toohello 最接近的 TB。</span><span class="sxs-lookup"><span data-stu-id="96b44-163">hello total cost for your primary data warehouse and seven days of Azure Blob snapshots is rounded toohello nearest TB.</span></span> <span data-ttu-id="96b44-164">例如，如果您的資料倉儲是 1.5 TB hello 快照使用 100 GB，您所要支付 2 TB 的資料至 Azure 高階儲存體費率。</span><span class="sxs-lookup"><span data-stu-id="96b44-164">For example, if your data warehouse is 1.5 TB and hello snapshots use 100 GB, you are billed for 2 TB of data at Azure Premium Storage rates.</span></span> 

> [!NOTE]
> <span data-ttu-id="96b44-165">每個快照集是空的一開始，而且會隨著您進行變更 toohello 主要資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="96b44-165">Each snapshot is empty initially and grows as you make changes toohello primary data warehouse.</span></span> <span data-ttu-id="96b44-166">所有快照集的大小增加為 hello 資料倉儲的變更。</span><span class="sxs-lookup"><span data-stu-id="96b44-166">All snapshots increase in size as hello data warehouse changes.</span></span> <span data-ttu-id="96b44-167">因此，快照集的 hello 儲存體成本成長變動的相應 toohello 率。</span><span class="sxs-lookup"><span data-stu-id="96b44-167">Therefore, hello storage costs for snapshots grow according toohello rate of change.</span></span>
> 
> 

<span data-ttu-id="96b44-168">如果您正在使用異地備援儲存體，您會收到個別的儲存體收費項目。</span><span class="sxs-lookup"><span data-stu-id="96b44-168">If you are using geo-redundant storage, you receive a separate storage charge.</span></span> <span data-ttu-id="96b44-169">hello 地理備援儲存體是費率支付費用 hello 標準讀取權限地理備援儲存體 (RA-GRS)。</span><span class="sxs-lookup"><span data-stu-id="96b44-169">hello geo-redundant storage is billed at hello standard Read-Access Geographically Redundant Storage (RA-GRS) rate.</span></span>

<span data-ttu-id="96b44-170">如需 SQL 資料倉儲價格的相關詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。</span><span class="sxs-lookup"><span data-stu-id="96b44-170">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="using-database-backups"></a><span data-ttu-id="96b44-171">使用資料庫備份</span><span class="sxs-lookup"><span data-stu-id="96b44-171">Using database backups</span></span>
<span data-ttu-id="96b44-172">hello 的 SQL 資料倉儲備份的主要用途是 toorestore hello 資料倉儲 tooone hello 還原點 hello 保留期限內。</span><span class="sxs-lookup"><span data-stu-id="96b44-172">hello primary use for SQL data warehouse backups is toorestore hello data warehouse tooone of hello restore points within hello retention period.</span></span>  

* <span data-ttu-id="96b44-173">toorestore SQL 資料倉儲，請參閱[還原 SQL 資料倉儲](sql-data-warehouse-restore-database-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="96b44-173">toorestore a SQL data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="96b44-174">相關主題</span><span class="sxs-lookup"><span data-stu-id="96b44-174">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="96b44-175">案例</span><span class="sxs-lookup"><span data-stu-id="96b44-175">Scenarios</span></span>
* <span data-ttu-id="96b44-176">如需商務持續性概觀，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="96b44-176">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

* <span data-ttu-id="96b44-177">toorestore 資料倉儲，請參閱[還原 SQL 資料倉儲](sql-data-warehouse-restore-database-overview.md)</span><span class="sxs-lookup"><span data-stu-id="96b44-177">toorestore a data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md)</span></span>

<!-- ### Tutorials -->

