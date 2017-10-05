---
title: "Azure SQL 資料倉儲備份 - 快照集、異地備援 | Microsoft Docs"
description: "了解 SQL 資料倉儲內建資料庫備份，它可以讓您將 Azure SQL 資料倉儲還原到還原點或不同的地理區域。"
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
ms.openlocfilehash: 54c0149a769e654139bbdf709802d49127f041ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="sql-data-warehouse-backups"></a><span data-ttu-id="748aa-103">SQL 資料倉儲備份</span><span class="sxs-lookup"><span data-stu-id="748aa-103">SQL Data Warehouse backups</span></span>
<span data-ttu-id="748aa-104">SQL 資料倉儲備份提供本機和異地備份做為其資料倉儲備份功能的一部份。</span><span class="sxs-lookup"><span data-stu-id="748aa-104">SQL Data Warehouse offers both local and geographical backups as part of its data warehouse backup capabilities.</span></span> <span data-ttu-id="748aa-105">這些包括 Azure 儲存體 Blob 快照集和異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="748aa-105">These include Azure Storage Blob snapshots and geo-redundant storage.</span></span> <span data-ttu-id="748aa-106">使用資料倉儲備份來將您的資料倉儲還原至主要區域中的某一個還原點，或還原至不同的地理區域。</span><span class="sxs-lookup"><span data-stu-id="748aa-106">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or restore to a different geographical region.</span></span> <span data-ttu-id="748aa-107">本文說明 SQL 資料倉儲中備份的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="748aa-107">This article explains the specifics of backups in SQL Data Warehouse.</span></span>

## <a name="what-is-a-data-warehouse-backup"></a><span data-ttu-id="748aa-108">什麼是資料倉儲備份？</span><span class="sxs-lookup"><span data-stu-id="748aa-108">What is a data warehouse backup?</span></span>
<span data-ttu-id="748aa-109">資料倉儲備份是您可以用來將資料倉儲還原至某一特定時間點的資料。</span><span class="sxs-lookup"><span data-stu-id="748aa-109">A data warehouse backup is the data that you can use to restore a data warehouse to a specific time.</span></span>  <span data-ttu-id="748aa-110">由於 SQL 資料倉儲是一個分散式系統，所以一個資料倉儲備份是由儲存在 Azure Blob 中的許多檔案組成。</span><span class="sxs-lookup"><span data-stu-id="748aa-110">Since SQL Data Warehouse is a distributed system, a data warehouse backup consists of many files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="748aa-111">資料庫備份可保護資料免於意外損毀或刪除，是商務持續性和災害復原策略中不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="748aa-111">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span></span> <span data-ttu-id="748aa-112">如需詳細資訊，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="748aa-112">For more information, see [Business continuity overview](../sql-database/sql-database-business-continuity.md).</span></span>

## <a name="data-redundancy"></a><span data-ttu-id="748aa-113">資料備援</span><span class="sxs-lookup"><span data-stu-id="748aa-113">Data redundancy</span></span>
<span data-ttu-id="748aa-114">SQL 資料倉儲會透過將您的資料儲存在本地備援 (LRS) Azure 進階儲存體來保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="748aa-114">SQL Data Warehouse protects your data by storing your data in locally redundant (LRS) Azure Premium Storage.</span></span> <span data-ttu-id="748aa-115">這項 Azure 儲存體功能可將資料的多個同步複本儲存在當地的資料中心，以確保當地語系化失敗時能夠提供透明的資料保護。</span><span class="sxs-lookup"><span data-stu-id="748aa-115">This Azure Storage feature stores multiple synchronous copies of the data in the local data center to guarantee transparent data protection if there are localized failures.</span></span> <span data-ttu-id="748aa-116">資料備援可確保您的資料在發生基礎結構問題 (例如磁碟故障等) 時能夠存留。</span><span class="sxs-lookup"><span data-stu-id="748aa-116">Data redundancy ensures that your data can survive infrastructure issues such as disk failures.</span></span> <span data-ttu-id="748aa-117">資料備援可利用容錯和高可用性基礎結構來確保商務持續性。</span><span class="sxs-lookup"><span data-stu-id="748aa-117">Data redundancy ensures business continuity with a fault tolerant and highly available infrastructure.</span></span>

<span data-ttu-id="748aa-118">若要深入了解：</span><span class="sxs-lookup"><span data-stu-id="748aa-118">To learn more about:</span></span>

* <span data-ttu-id="748aa-119">Azure 進階儲存體，請參閱 [Azure 進階儲存體簡介](../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="748aa-119">Azure Premium storage, see [Introduction to Azure Premium Storage](../storage/common/storage-premium-storage.md).</span></span>
* <span data-ttu-id="748aa-120">本地備援儲存體，請參閱 [Azure 儲存體複寫](../storage/common/storage-redundancy.md#locally-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="748aa-120">Locally Redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md#locally-redundant-storage).</span></span>

## <a name="azure-storage-blob-snapshots"></a><span data-ttu-id="748aa-121">Azure 儲存體 Blob 快照集</span><span class="sxs-lookup"><span data-stu-id="748aa-121">Azure Storage Blob snapshots</span></span>
<span data-ttu-id="748aa-122">使用 Azure 進階儲存體的一項優點是，SQL 資料倉儲會使用 Azure 儲存體 Blob 快照集來將資料倉儲備份在本地位置。</span><span class="sxs-lookup"><span data-stu-id="748aa-122">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the data warehouse locally.</span></span> <span data-ttu-id="748aa-123">您可以將資料倉儲還原至快照集還原點。</span><span class="sxs-lookup"><span data-stu-id="748aa-123">You can restore a data warehouse to a snapshot restore point.</span></span> <span data-ttu-id="748aa-124">快照集至少每八個小時會啟動，並且可供使用七天。</span><span class="sxs-lookup"><span data-stu-id="748aa-124">Snapshots start a minimum of every eight hours and are available for seven days.</span></span>  

<span data-ttu-id="748aa-125">若要深入了解：</span><span class="sxs-lookup"><span data-stu-id="748aa-125">To learn more about:</span></span>

* <span data-ttu-id="748aa-126">Azure Blob 快照集，請參閱[建立 Blob 快照集](../storage/blobs/storage-blob-snapshots.md)。</span><span class="sxs-lookup"><span data-stu-id="748aa-126">Azure blob snapshots, see [Create a blob snapshot](../storage/blobs/storage-blob-snapshots.md).</span></span>

## <a name="geo-redundant-backups"></a><span data-ttu-id="748aa-127">異地備援備份</span><span class="sxs-lookup"><span data-stu-id="748aa-127">Geo-redundant backups</span></span>
<span data-ttu-id="748aa-128">每 24 個小時，SQL 資料倉儲就會在標準儲存體中儲存完整資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="748aa-128">Every 24 hours, SQL Data Warehouse stores the full data warehouse in Standard storage.</span></span> <span data-ttu-id="748aa-129">完整資料倉儲的建立時間會與上一個快照集的時間相符。</span><span class="sxs-lookup"><span data-stu-id="748aa-129">The full data warehouse is created to match the time of the last snapshot.</span></span> <span data-ttu-id="748aa-130">標準儲存體屬於具備讀取權限的異地備援儲存體帳戶 (RA-GRS)。</span><span class="sxs-lookup"><span data-stu-id="748aa-130">The standard storage belongs to a geo-redundant storage account with read access (RA-GRS).</span></span> <span data-ttu-id="748aa-131">Azure 儲存體 RA-GRS 功能會將備份檔案複寫到 [配對的資料中心](../best-practices-availability-paired-regions.md)。</span><span class="sxs-lookup"><span data-stu-id="748aa-131">The Azure Storage RA-GRS feature replicates the backup files to a [paired data center](../best-practices-availability-paired-regions.md).</span></span> <span data-ttu-id="748aa-132">萬一您無法存取主要地區中的快照集，此異地複寫可確保您能夠還原資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="748aa-132">This geo-replication ensures you can restore data warehouse in case you cannot access the snapshots in your primary region.</span></span> 

<span data-ttu-id="748aa-133">這項功能為預設開啟。</span><span class="sxs-lookup"><span data-stu-id="748aa-133">This feature is on by default.</span></span> <span data-ttu-id="748aa-134">如果您不想要使用異地備援備份，您可以 [退出] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn)。</span><span class="sxs-lookup"><span data-stu-id="748aa-134">If you don't want to use geo-redundant backups, you can [opt out] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span></span> 

> [!NOTE]
> <span data-ttu-id="748aa-135">在 Azure 儲存體中，「複寫」一詞指的是將檔案從某個位置複製到另一個位置。</span><span class="sxs-lookup"><span data-stu-id="748aa-135">In Azure storage, the term *replication* refers to copying files from one location to another.</span></span> <span data-ttu-id="748aa-136">SQL 的「資料庫複寫」  指的是保持多個次要資料庫與主要資料庫同步。</span><span class="sxs-lookup"><span data-stu-id="748aa-136">SQL's *database replication* refers to keeping to multiple secondary databases synchronized with a primary database.</span></span> 
> 
> 

> [!NOTE]
> <span data-ttu-id="748aa-137">您無法選擇退出 DWU 9000 和 DWU 18000 的異地備援備份。</span><span class="sxs-lookup"><span data-stu-id="748aa-137">You cannot opt out of geo-redundant backups with DWU 9000 and DWU 18000.</span></span> 
>
> 

<span data-ttu-id="748aa-138">若要深入了解：</span><span class="sxs-lookup"><span data-stu-id="748aa-138">To learn more about:</span></span>

* <span data-ttu-id="748aa-139">異地備援儲存體，請參閱 [Azure 儲存體複寫](../storage/common/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="748aa-139">Geo-redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md).</span></span>
* <span data-ttu-id="748aa-140">RA-GRS 儲存體：請參閱 [讀取權限異地備援儲存體](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)。</span><span class="sxs-lookup"><span data-stu-id="748aa-140">RA-GRS storage, see [Read-access geo-redundant storage](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).</span></span>

## <a name="data-warehouse-backup-schedule-and-retention-period"></a><span data-ttu-id="748aa-141">資料倉儲備份排程與保留期限</span><span class="sxs-lookup"><span data-stu-id="748aa-141">Data warehouse backup schedule and retention period</span></span>
<span data-ttu-id="748aa-142">SQL 資料倉儲每四到八小時就會在您的線上資料倉儲上建立快照集，並將每個快照集保留七天。</span><span class="sxs-lookup"><span data-stu-id="748aa-142">SQL Data Warehouse creates snapshots on your online data warehouses every four to eight hours and keeps each snapshot for seven days.</span></span> <span data-ttu-id="748aa-143">您可以將線上資料庫還原至過去七天內的其中一個還原點。</span><span class="sxs-lookup"><span data-stu-id="748aa-143">You can restore your online database to one of the restore points in the past seven days.</span></span> 

<span data-ttu-id="748aa-144">若要查看上一個快照集的開始時間，請在您的線上 SQL 資料倉儲上執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="748aa-144">To see when the last snapshot started, run this query on your online SQL Data Warehouse.</span></span> 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

<span data-ttu-id="748aa-145">如果您需要將快照集保留超過七天，您可以將還原點還原至新的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="748aa-145">If you need to retain a snapshot for longer than seven days, you can restore a restore point to a new data warehouse.</span></span> <span data-ttu-id="748aa-146">完成還原之後，SQL 資料倉儲就會開始在新的資料倉儲上建立快照集。</span><span class="sxs-lookup"><span data-stu-id="748aa-146">After the restore is finished, SQL Data Warehouse starts creating snapshots on the new data warehouse.</span></span> <span data-ttu-id="748aa-147">如果您沒有變更新的資料倉儲，快照集就會保持空白，因此快照集成本會降到最低。</span><span class="sxs-lookup"><span data-stu-id="748aa-147">If you don't make changes to the new data warehouse, the snapshots stay empty and therefore the snapshot cost is minimal.</span></span> <span data-ttu-id="748aa-148">您也可以暫停資料庫來避免 SQL 資料倉儲建立快照集。</span><span class="sxs-lookup"><span data-stu-id="748aa-148">You could also pause the database to keep SQL Data Warehouse from creating snapshots.</span></span>

### <a name="what-happens-to-my-backup-retention-while-my-data-warehouse-is-paused"></a><span data-ttu-id="748aa-149">當我的資料倉儲暫停時，我的備份保留期會發生什麼狀況？</span><span class="sxs-lookup"><span data-stu-id="748aa-149">What happens to my backup retention while my data warehouse is paused?</span></span>
<span data-ttu-id="748aa-150">暫停資料倉儲時，SQL 資料倉儲不會建立快照集，快照集也不會過期。</span><span class="sxs-lookup"><span data-stu-id="748aa-150">SQL Data Warehouse does not create snapshots and does not expire snapshots while a data warehouse is paused.</span></span> <span data-ttu-id="748aa-151">暫停資料倉儲時，快照集存在時間不會改變。</span><span class="sxs-lookup"><span data-stu-id="748aa-151">The snapshot age does not change while the data warehouse is paused.</span></span> <span data-ttu-id="748aa-152">快照集保留期是以資料倉儲上線的天數為依據，而不是以行事曆天數為依據。</span><span class="sxs-lookup"><span data-stu-id="748aa-152">Snapshot retention is based on the number of days the data warehouse is online, not calendar days.</span></span>

<span data-ttu-id="748aa-153">例如，如果快照集是在 10 月 1 日下午 4 點開始，資料倉儲是在 10 月 3 日下午 4 點暫停，快照的存在時間為 2 天。</span><span class="sxs-lookup"><span data-stu-id="748aa-153">For example, if a snapshot starts October 1 at 4 pm and the data warehouse is paused October 3 at 4 pm, the snapshot is two days old.</span></span> <span data-ttu-id="748aa-154">無論資料倉儲何時恢復上線，快照集的存在時間都是 2 天。</span><span class="sxs-lookup"><span data-stu-id="748aa-154">Whenever the data warehouse comes back online the snapshot is two days old.</span></span> <span data-ttu-id="748aa-155">如果資料倉儲在 10 月 5 日下午 4 點恢復上線，快照集的存在時間為 2 天，並會繼續保留 5 天。</span><span class="sxs-lookup"><span data-stu-id="748aa-155">If the data warehouse comes online October 5 at 4 pm, the snapshot is two days old and remains for five more days.</span></span>

<span data-ttu-id="748aa-156">當資料倉儲恢復上線時，SQL 資料倉儲會繼續建立新的快照集，並在快照集包含超過 7 天的資料時讓快照集過期。</span><span class="sxs-lookup"><span data-stu-id="748aa-156">When the data warehouse comes back online, SQL Data Warehouse resumes new snapshots and expires snapshots when they have more than seven days of data.</span></span>

### <a name="how-long-is-the-retention-period-for-a-dropped-data-warehouse"></a><span data-ttu-id="748aa-157">已卸除資料倉儲的保留期限有多久？</span><span class="sxs-lookup"><span data-stu-id="748aa-157">How long is the retention period for a dropped data warehouse?</span></span>
<span data-ttu-id="748aa-158">當資料倉儲被卸除時，資料倉儲和快照集會儲存 7 天，然後就會被移除。</span><span class="sxs-lookup"><span data-stu-id="748aa-158">When a data warehouse is dropped, the data warehouse and the snapshots are saved for seven days and then removed.</span></span> <span data-ttu-id="748aa-159">您可以將資料倉儲還原至任何一個已儲存的還原點。</span><span class="sxs-lookup"><span data-stu-id="748aa-159">You can restore the data warehouse to any of the saved restore points.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="748aa-160">如果您刪除邏輯 SQL Server 執行個體，所有屬於該執行個體的資料庫也會一併刪除，且無法復原。</span><span class="sxs-lookup"><span data-stu-id="748aa-160">If you delete a logical SQL server instance, all databases that belong to the instance are also deleted and cannot be recovered.</span></span> <span data-ttu-id="748aa-161">您無法還原已刪除的伺服器。</span><span class="sxs-lookup"><span data-stu-id="748aa-161">You cannot restore a deleted server.</span></span>
> 
> 

## <a name="data-warehouse-backup-costs"></a><span data-ttu-id="748aa-162">資料倉儲備份成本</span><span class="sxs-lookup"><span data-stu-id="748aa-162">Data warehouse backup costs</span></span>
<span data-ttu-id="748aa-163">您主要資料倉儲和 7 天 Azure Blob 快照集的總成本會四捨五入到最接近的 TB。</span><span class="sxs-lookup"><span data-stu-id="748aa-163">The total cost for your primary data warehouse and seven days of Azure Blob snapshots is rounded to the nearest TB.</span></span> <span data-ttu-id="748aa-164">例如，如果您的資料倉儲為 1.5 TB，且快照集使用 100 GB，就會以 Azure 進階儲存體費率向您收取 2 TB 資料費用。</span><span class="sxs-lookup"><span data-stu-id="748aa-164">For example, if your data warehouse is 1.5 TB and the snapshots use 100 GB, you are billed for 2 TB of data at Azure Premium Storage rates.</span></span> 

> [!NOTE]
> <span data-ttu-id="748aa-165">每個快照集一開始都是空白的，然後會隨著您變更主要資料倉儲而成長。</span><span class="sxs-lookup"><span data-stu-id="748aa-165">Each snapshot is empty initially and grows as you make changes to the primary data warehouse.</span></span> <span data-ttu-id="748aa-166">所有快照集的大小都會隨著資料倉儲變更而增加。</span><span class="sxs-lookup"><span data-stu-id="748aa-166">All snapshots increase in size as the data warehouse changes.</span></span> <span data-ttu-id="748aa-167">因此快照集的儲存體成本也會依據變更的速度而增加。</span><span class="sxs-lookup"><span data-stu-id="748aa-167">Therefore, the storage costs for snapshots grow according to the rate of change.</span></span>
> 
> 

<span data-ttu-id="748aa-168">如果您正在使用異地備援儲存體，您會收到個別的儲存體收費項目。</span><span class="sxs-lookup"><span data-stu-id="748aa-168">If you are using geo-redundant storage, you receive a separate storage charge.</span></span> <span data-ttu-id="748aa-169">異地備援儲存體是依據標準讀取權限異地備援儲存體 (RA-GRS) 費率收費。</span><span class="sxs-lookup"><span data-stu-id="748aa-169">The geo-redundant storage is billed at the standard Read-Access Geographically Redundant Storage (RA-GRS) rate.</span></span>

<span data-ttu-id="748aa-170">如需 SQL 資料倉儲價格的相關詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。</span><span class="sxs-lookup"><span data-stu-id="748aa-170">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="using-database-backups"></a><span data-ttu-id="748aa-171">使用資料庫備份</span><span class="sxs-lookup"><span data-stu-id="748aa-171">Using database backups</span></span>
<span data-ttu-id="748aa-172">SQL 資料倉儲備份的主要用途，是用來將資料倉儲還原至保留期限內的其中一個還原點。</span><span class="sxs-lookup"><span data-stu-id="748aa-172">The primary use for SQL data warehouse backups is to restore the data warehouse to one of the restore points within the retention period.</span></span>  

* <span data-ttu-id="748aa-173">若要還原 SQL 資料倉儲，請參閱[還原 SQL 資料倉儲](sql-data-warehouse-restore-database-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="748aa-173">To restore a SQL data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="748aa-174">相關主題</span><span class="sxs-lookup"><span data-stu-id="748aa-174">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="748aa-175">案例</span><span class="sxs-lookup"><span data-stu-id="748aa-175">Scenarios</span></span>
* <span data-ttu-id="748aa-176">如需商務持續性概觀，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="748aa-176">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

* <span data-ttu-id="748aa-177">若要還原資料倉儲，請參閱[還原 SQL 資料倉儲](sql-data-warehouse-restore-database-overview.md)</span><span class="sxs-lookup"><span data-stu-id="748aa-177">To restore a data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md)</span></span>

<!-- ### Tutorials -->

