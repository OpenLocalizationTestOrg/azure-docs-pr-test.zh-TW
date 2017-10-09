---
title: "aaaRestore Azure SQL database 備份 |Microsoft 文件"
description: "深入了解，可讓您 tooroll 後的時間點還原 Azure SQL Database tooa 前一個點的時間 （向上 too35 天為單位）。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a><span data-ttu-id="84778-103">使用自動資料庫備份復原 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="84778-103">Recover an Azure SQL database using automated database backups</span></span>
<span data-ttu-id="84778-104">SQL Database 針對使用[自動資料庫備份](sql-database-automated-backups.md)和[長期保留備份](sql-database-long-term-retention.md)進行資料庫復原，提供以下選項。</span><span class="sxs-lookup"><span data-stu-id="84778-104">SQL Database provides these options for database recovery using [automated database backups](sql-database-automated-backups.md) and [backups in long-term retention](sql-database-long-term-retention.md).</span></span> <span data-ttu-id="84778-105">您可從資料庫備份還原至︰</span><span class="sxs-lookup"><span data-stu-id="84778-105">You can restore from a database backup to:</span></span>

* <span data-ttu-id="84778-106">新的資料庫上相同的邏輯伺服器復原的 hello tooa 指定 hello 保留期限內的時間點。</span><span class="sxs-lookup"><span data-stu-id="84778-106">A new database on hello same logical server recovered tooa specified point in time within hello retention period.</span></span> 
* <span data-ttu-id="84778-107">A 上的資料庫 hello 相同邏輯伺服器復原已刪除的資料庫的 toohello 刪除時間。</span><span class="sxs-lookup"><span data-stu-id="84778-107">A database on hello same logical server recovered toohello deletion time for a deleted database.</span></span>
* <span data-ttu-id="84778-108">新的資料庫中的任何區域的任何邏輯伺服器上復原 toohello 點 hello 的最新每日備份在異地備援 blob 儲存體 (RA-GRS)。</span><span class="sxs-lookup"><span data-stu-id="84778-108">A new database on any logical server in any region recovered toohello point of hello most recent daily backups in geo-replicated blob storage (RA-GRS).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84778-109">在還原期間，您無法覆寫現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-109">You cannot overwrite an existing database during restore.</span></span>
>

<span data-ttu-id="84778-110">您也可以使用[自動化資料庫備份](sql-database-automated-backups.md)toocreate[資料庫複製](sql-database-copy.md)的任何區域中的任何邏輯伺服器上。</span><span class="sxs-lookup"><span data-stu-id="84778-110">You can also use [automated database backups](sql-database-automated-backups.md) toocreate a [database copy](sql-database-copy.md) on any logical server in any region.</span></span> 

## <a name="recovery-time"></a><span data-ttu-id="84778-111">復原時間</span><span class="sxs-lookup"><span data-stu-id="84778-111">Recovery time</span></span>
<span data-ttu-id="84778-112">hello 復原時間 toorestore 使用自動化的資料庫備份的資料庫由數個因素影響：</span><span class="sxs-lookup"><span data-stu-id="84778-112">hello recovery time toorestore a database using automated database backups is impacted by several factors:</span></span> 

* <span data-ttu-id="84778-113">hello hello 資料庫大小</span><span class="sxs-lookup"><span data-stu-id="84778-113">hello size of hello database</span></span>
* <span data-ttu-id="84778-114">hello hello 資料庫效能層級</span><span class="sxs-lookup"><span data-stu-id="84778-114">hello performance level of hello database</span></span>
* <span data-ttu-id="84778-115">交易記錄所涉及的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="84778-115">hello number of transaction logs involved</span></span>
* <span data-ttu-id="84778-116">hello 數量需要 toobe 活動重新執行 toorecover toohello 還原點</span><span class="sxs-lookup"><span data-stu-id="84778-116">hello amount of activity that needs toobe replayed toorecover toohello restore point</span></span>
* <span data-ttu-id="84778-117">hello 網路頻寬 hello 還原 tooa 不同的區域</span><span class="sxs-lookup"><span data-stu-id="84778-117">hello network bandwidth if hello restore is tooa different region</span></span> 
* <span data-ttu-id="84778-118">hello hello 目標區域中所處理的並行的還原要求數目。</span><span class="sxs-lookup"><span data-stu-id="84778-118">hello number of concurrent restore requests being processed in hello target region.</span></span> 
  
  <span data-ttu-id="84778-119">對於非常大型和/或作用中的資料庫，hello 還原可能需要數小時。</span><span class="sxs-lookup"><span data-stu-id="84778-119">For a very large and/or active database, hello restore may take several hours.</span></span> <span data-ttu-id="84778-120">如果某區域中的中斷延長，其他區域可能要處理大量的異地還原要求。</span><span class="sxs-lookup"><span data-stu-id="84778-120">If there is prolonged outage in a region, it is possible that there are large numbers of geo-restore requests being processed by other regions.</span></span> <span data-ttu-id="84778-121">當有許多要求時，hello 復原時間可能會增加該區域中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-121">When there are many requests, hello recovery time may increase for databases in that region.</span></span> <span data-ttu-id="84778-122">大多數資料庫還原會在 12 小時內完成。</span><span class="sxs-lookup"><span data-stu-id="84778-122">Most database restores complete within 12 hours.</span></span>
  
<span data-ttu-id="84778-123">沒有任何內建功能 toodo 大量還原。</span><span class="sxs-lookup"><span data-stu-id="84778-123">There is no built-in functionality toodo bulk restore.</span></span> <span data-ttu-id="84778-124">hello [Azure SQL Database： 完整伺服器復原](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666)指令碼是一種完成這項工作的範例。</span><span class="sxs-lookup"><span data-stu-id="84778-124">hello [Azure SQL Database: Full Server Recovery](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) script is an example of one way of accomplishing this task.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84778-125">toorecover 使用自動化備份，您必須是 hello hello 訂用帳戶中的 SQL Server 參與者角色的成員，或者是 hello 訂用帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="84778-125">toorecover using automated backups, you must be a member of hello SQL Server Contributor role in hello subscription or be hello subscription owner.</span></span> <span data-ttu-id="84778-126">您可以使用 hello Azure 入口網站、 PowerShell 或 REST API hello 進行復原。</span><span class="sxs-lookup"><span data-stu-id="84778-126">You can recover using hello Azure portal, PowerShell, or hello REST API.</span></span> <span data-ttu-id="84778-127">您無法使用 Transact-SQL。</span><span class="sxs-lookup"><span data-stu-id="84778-127">You cannot use Transact-SQL.</span></span> 
> 

## <a name="point-in-time-restore"></a><span data-ttu-id="84778-128">還原時間點</span><span class="sxs-lookup"><span data-stu-id="84778-128">Point-In-Time Restore</span></span>

<span data-ttu-id="84778-129">您可以還原現有的資料庫 tooan 稍早的時間點為新的資料庫上 hello 相同邏輯伺服器使用 hello Azure 入口網站[PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase)，或使用 hello [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx)。</span><span class="sxs-lookup"><span data-stu-id="84778-129">You can restore an existing database tooan earlier point in time as a new database on hello same logical server using hello Azure portal, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), or hello [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="84778-130">顯示如何 tooperform 時間點還原的資料庫，請參閱範例 PowerShell 指令碼[還原 SQL 資料庫使用 PowerShell](scripts/sql-database-restore-database-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="84778-130">For a sample PowerShell script showing how tooperform a point-in-time restore of a database, see [Restore a SQL database using PowerShell](scripts/sql-database-restore-database-powershell.md).</span></span>
>

<span data-ttu-id="84778-131">hello 資料庫可以在還原的 tooany 服務層或效能層級，以及做為單一資料庫或彈性集區。</span><span class="sxs-lookup"><span data-stu-id="84778-131">hello database can be restored tooany service tier or performance level, and as a single database or into an elastic pool.</span></span> <span data-ttu-id="84778-132">請確定 hello 邏輯伺服器上有足夠的資源，或在 hello 彈性集區 toowhich hello 資料庫會還原。</span><span class="sxs-lookup"><span data-stu-id="84778-132">Ensure you have sufficient resources on hello logical server or in hello elastic pool toowhich you are restoring hello database.</span></span> <span data-ttu-id="84778-133">完成後，hello 還原資料庫是正常、 完全可存取的線上資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-133">Once complete, hello restored database is a normal, fully accessible, online database.</span></span> <span data-ttu-id="84778-134">根據其服務層和效能層級的標準費率計費 hello 還原資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-134">hello restored database is charged at normal rates based on its service tier and performance level.</span></span> <span data-ttu-id="84778-135">Hello 資料庫還原完成之前不會產生費用。</span><span class="sxs-lookup"><span data-stu-id="84778-135">You do not incur charges until hello database restore is complete.</span></span>

<span data-ttu-id="84778-136">您通常會還原資料庫 tooan 稍早點進行復原。</span><span class="sxs-lookup"><span data-stu-id="84778-136">You generally restore a database tooan earlier point for recovery purposes.</span></span> <span data-ttu-id="84778-137">時這麼做，您可以將 hello 做為 hello 原始資料庫的替代還原資料庫，或使用它從 tooretrieve 資料並更新 hello 原始資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-137">When doing so, you can treat hello restored database as a replacement for hello original database or use it tooretrieve data from and then update hello original database.</span></span> 

* <span data-ttu-id="84778-138">***資料庫取代：***如果 hello 還原資料庫用來取代 hello 原始資料庫，您應該確認 hello 效能層級和 （或) 是適當的服務層，並視 hello 資料庫的延展。</span><span class="sxs-lookup"><span data-stu-id="84778-138">***Database replacement:*** If hello restored database is intended as a replacement for hello original database, you should verify hello performance level and/or service tier are appropriate and scale hello database if necessary.</span></span> <span data-ttu-id="84778-139">您可以重新命名 hello 原始資料庫，然後將 hello 還原資料庫 hello 原始名稱使用 T-SQL 中的 hello ALTER DATABASE 命令。</span><span class="sxs-lookup"><span data-stu-id="84778-139">You can rename hello original database and then give hello restored database hello original name using hello ALTER DATABASE command in T-SQL.</span></span> 
* <span data-ttu-id="84778-140">***資料復原：***如果您計劃 tooretrieve hello 還原資料庫 toorecover 從使用者或應用程式錯誤的資料，您需要 toowrite 並從 hello 還原資料庫 toohello 執行 hello 必要的資料復原指令碼 tooextract 資料原始的資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-140">***Data recovery:*** If you plan tooretrieve data from hello restored database toorecover from a user or application error, you need toowrite and execute hello necessary data recovery scripts tooextract data from hello restored database toohello original database.</span></span> <span data-ttu-id="84778-141">雖然 hello 還原作業可能要花很長的時間 toocomplete，hello 還原資料庫中會顯示 hello 整個 hello 還原程序的資料庫清單。</span><span class="sxs-lookup"><span data-stu-id="84778-141">Although hello restore operation may take a long time toocomplete, hello restoring database is visible in hello database list throughout hello restore process.</span></span> <span data-ttu-id="84778-142">如果您刪除 hello 資料庫 hello 還原期間，hello 還原作業會取消，且您不需付費 hello 未完成 hello 還原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-142">If you delete hello database during hello restore, hello restore operation is canceled and you are not charged for hello database that did not complete hello restore.</span></span> 

### <a name="azure-portal"></a><span data-ttu-id="84778-143">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="84778-143">Azure portal</span></span>

<span data-ttu-id="84778-144">在時間中使用 toorecover tooa 點 hello Azure 入口網站、 資料庫和按一下開啟 hello 頁面**還原**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="84778-144">toorecover tooa point in time using hello Azure portal, open hello page for your database and click **Restore** on hello toolbar.</span></span>

![point-in-time-restore](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a><span data-ttu-id="84778-146">還原已刪除的資料庫</span><span class="sxs-lookup"><span data-stu-id="84778-146">Deleted database restore</span></span>
<span data-ttu-id="84778-147">您可以還原已刪除的資料庫 toohello 刪除時間的 hello 上已刪除的資料庫使用相同的邏輯伺服器 hello Azure 入口網站[PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase)，或使用 hello [REST (createMode = 還原)](https://msdn.microsoft.com/library/azure/mt163685.aspx)。</span><span class="sxs-lookup"><span data-stu-id="84778-147">You can restore a deleted database toohello deletion time for a deleted database on hello same logical server using hello Azure portal, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), or hello [REST (createMode=Restore)](https://msdn.microsoft.com/library/azure/mt163685.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="84778-148">如需範例 PowerShell 指令碼的顯示如何 toorestore 已刪除的資料庫，請參閱[還原 SQL 資料庫使用 PowerShell](scripts/sql-database-restore-database-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="84778-148">For a sample PowerShell script showing how toorestore a deleted database, see [Restore a SQL database using PowerShell](scripts/sql-database-restore-database-powershell.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="84778-149">如果您刪除 Azure SQL Database 伺服器執行個體，其所有資料庫也會一併刪除且無法加以復原。</span><span class="sxs-lookup"><span data-stu-id="84778-149">If you delete an Azure SQL Database server instance, all its databases are also deleted and cannot be recovered.</span></span> <span data-ttu-id="84778-150">目前不支援還原已刪除的伺服器。</span><span class="sxs-lookup"><span data-stu-id="84778-150">There is currently no support for restoring a deleted server.</span></span>
> 

### <a name="azure-portal"></a><span data-ttu-id="84778-151">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="84778-151">Azure portal</span></span>

<span data-ttu-id="84778-152">已刪除的 toorecover 資料庫期間其[保留期限](sql-database-service-tiers.md)使用 hello Azure 入口網站開啟 hello 頁面為您的伺服器，並在 hello 作業區域中，按一下 **已刪除資料庫**。</span><span class="sxs-lookup"><span data-stu-id="84778-152">toorecover a deleted database during its [retention period](sql-database-service-tiers.md) using hello Azure portal, open hello page for your server and in hello Operations area, click **Deleted databases**.</span></span>

![deleted-database-restore-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![deleted-database-restore-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a><span data-ttu-id="84778-155">異地還原</span><span class="sxs-lookup"><span data-stu-id="84778-155">Geo-restore</span></span>
<span data-ttu-id="84778-156">您可以從 hello 最新地理複寫完整和差異備份來還原 SQL 資料庫的任何 Azure 區域中的任何伺服器上。</span><span class="sxs-lookup"><span data-stu-id="84778-156">You can restore a SQL database on any server in any Azure region from hello most recent geo-replicated full and differential backups.</span></span> <span data-ttu-id="84778-157">「 地理還原使用異地備援備份做為來源，而且可以是使用的 toorecover 即使 hello 資料庫或資料中心無法存取到期 tooan 中斷。</span><span class="sxs-lookup"><span data-stu-id="84778-157">Geo-restore uses a geo-redundant backup as its source and can be used toorecover a database even if hello database or datacenter is inaccessible due tooan outage.</span></span> 

<span data-ttu-id="84778-158">地理還原 」 hello 預設復原選項，您無法使用資料庫時由於 hello hello 資料庫裝載的區域中的事件。</span><span class="sxs-lookup"><span data-stu-id="84778-158">Geo-restore is hello default recovery option when your database is unavailable because of an incident in hello region where hello database is hosted.</span></span> <span data-ttu-id="84778-159">如果資料庫應用程式中無法使用區域結果中的大規模事件，您可以從任何其他區域中的 hello 異地備援備份 tooa 伺服器來還原資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-159">If a large-scale incident in a region results in unavailability of your database application, you can restore a database from hello geo-replicated backups tooa server in any other region.</span></span> <span data-ttu-id="84778-160">當執行差異備份時，與時進行地理複寫 tooan Azure 之間的延遲不同區域中的 blob。</span><span class="sxs-lookup"><span data-stu-id="84778-160">There is a delay between when a differential backup is taken and when it is geo-replicated tooan Azure blob in a different region.</span></span> <span data-ttu-id="84778-161">此類延遲可能會向上 tooan 小時，因此，如果發生損毀，有最長可能會 tooone 小時資料遺失。</span><span class="sxs-lookup"><span data-stu-id="84778-161">This delay can be up tooan hour, so, if a disaster occurs, there can be up tooone hour data loss.</span></span> <span data-ttu-id="84778-162">hello 下列圖例顯示 hello 最新可用的備份在另一個地區 hello 資料庫的還原。</span><span class="sxs-lookup"><span data-stu-id="84778-162">hello following illustration shows restore of hello database from hello last available backup in another region.</span></span>

![異地還原](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> <span data-ttu-id="84778-164">如需範例 PowerShell 指令碼的顯示如何 tooperform 異地還原，請參閱[還原 SQL 資料庫使用 PowerShell](scripts/sql-database-restore-database-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="84778-164">For a sample PowerShell script showing how tooperform a geo-restore, see [Restore a SQL database using PowerShell](scripts/sql-database-restore-database-powershell.md).</span></span>
> 

<span data-ttu-id="84778-165">目前不支援異地次要資料庫上的時間點復原。</span><span class="sxs-lookup"><span data-stu-id="84778-165">Point-in-time restore on a geo-secondary is not currently supported.</span></span> <span data-ttu-id="84778-166">只有在主要資料庫上才可進行時間點復原。</span><span class="sxs-lookup"><span data-stu-id="84778-166">Point-in-time restore can be done only on a primary database.</span></span> <span data-ttu-id="84778-167">如需使用 「 地理還原 toorecover 從中斷的詳細資訊，請參閱[從中斷復原](sql-database-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="84778-167">For detailed information about using geo-restore toorecover from an outage, see [Recover from an outage](sql-database-disaster-recovery.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84778-168">從備份復原為 hello 最基本的 hello 災害復原方案中使用 SQL Database 提供 hello 最長的 RPO 和預估復原時間 (ERT)。</span><span class="sxs-lookup"><span data-stu-id="84778-168">Recovery from backups is hello most basic of hello disaster recovery solutions available in SQL Database with hello longest RPO and Estimate Recovery Time (ERT).</span></span> <span data-ttu-id="84778-169">對於使用基本資料庫的解決方案，常見且合理的 DR 解決方案是異地還原，且這個解決方案具有 12 小時的 ERT。</span><span class="sxs-lookup"><span data-stu-id="84778-169">For solutions using Basic databases, geo-restore is frequently a reasonable DR solution with an ERT of 12 hours.</span></span> <span data-ttu-id="84778-170">對於使用較大型標準或進階資料庫的解決方案，如果其需要縮短復原時間，您應該考慮使用[主動式異地複寫](sql-database-geo-replication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="84778-170">For solutions using larger Standard or Premium databases that require shorter recovery times, you should consider using [active geo-replication](sql-database-geo-replication-overview.md).</span></span> <span data-ttu-id="84778-171">作用中地理複寫會提供以較低的 RPO 和 ERT 程式它只會要求您起始容錯移轉 tooa 連續複寫的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-171">Active geo-replication offers a much lower RPO and ERT as it only requires you initiate a failover tooa continuously replicated secondary.</span></span> <span data-ttu-id="84778-172">如需商務持續性選項的詳細資訊，請參閱[商務持續性概觀](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="84778-172">For more information on business contiuity choices, see [over of business continuity](sql-database-business-continuity.md).</span></span>
> 

### <a name="azure-portal"></a><span data-ttu-id="84778-173">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="84778-173">Azure portal</span></span>

<span data-ttu-id="84778-174">toogeo 還原資料庫時其[保留期限](sql-database-service-tiers.md)使用 hello Azure 入口網站，開啟 hello SQL Database 頁面，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="84778-174">toogeo-restore a database during its [retention period](sql-database-service-tiers.md) using hello Azure portal, open hello SQL Databases page and then click **Add**.</span></span> <span data-ttu-id="84778-175">在 [hello**選取來源**] 文字方塊中，選取**備份**。</span><span class="sxs-lookup"><span data-stu-id="84778-175">In hello **Select source** text box, select **Backup**.</span></span> <span data-ttu-id="84778-176">Hello 區域中，您所選擇的 hello 伺服器上，指定 hello tooperform hello 復原備份。</span><span class="sxs-lookup"><span data-stu-id="84778-176">Specify hello backup from which tooperform hello recovery in hello region and on hello server of your choice.</span></span> 

## <a name="programmatically-performing-recovery-using-automated-backups"></a><span data-ttu-id="84778-177">使用自動備份以程式設計方式執行復原</span><span class="sxs-lookup"><span data-stu-id="84778-177">Programmatically performing recovery using automated backups</span></span>
<span data-ttu-id="84778-178">如先前所討論，此外 toohello Azure 入口網站資料庫復原可以使用 Azure PowerShell 以程式設計方式執行或是 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="84778-178">As previously discussed, in addition toohello Azure portal, database recovery can be performed programmatically using Azure PowerShell or hello REST API.</span></span> <span data-ttu-id="84778-179">hello 下表描述可用的命令 hello 集。</span><span class="sxs-lookup"><span data-stu-id="84778-179">hello following tables describe hello set of commands available.</span></span>

### <a name="powershell"></a><span data-ttu-id="84778-180">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84778-180">PowerShell</span></span>
| <span data-ttu-id="84778-181">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="84778-181">Cmdlet</span></span> | <span data-ttu-id="84778-182">說明</span><span class="sxs-lookup"><span data-stu-id="84778-182">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="84778-183">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="84778-183">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase) |<span data-ttu-id="84778-184">取得一或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-184">Gets one or more databases.</span></span> |
| [<span data-ttu-id="84778-185">Get-AzureRMSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="84778-185">Get-AzureRMSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="84778-186">取得可還原的已刪除資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-186">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="84778-187">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="84778-187">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |<span data-ttu-id="84778-188">取得資料庫的異地備援備份。</span><span class="sxs-lookup"><span data-stu-id="84778-188">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="84778-189">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="84778-189">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |<span data-ttu-id="84778-190">還原 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="84778-190">Restores a SQL database.</span></span> |
|  | |

### <a name="rest-api"></a><span data-ttu-id="84778-191">REST API</span><span class="sxs-lookup"><span data-stu-id="84778-191">REST API</span></span>
| <span data-ttu-id="84778-192">API</span><span class="sxs-lookup"><span data-stu-id="84778-192">API</span></span> | <span data-ttu-id="84778-193">說明</span><span class="sxs-lookup"><span data-stu-id="84778-193">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="84778-194">REST (createMode=Recovery)</span><span class="sxs-lookup"><span data-stu-id="84778-194">REST (createMode=Recovery)</span></span>](https://msdn.microsoft.com/library/azure/mt163685.aspx) |<span data-ttu-id="84778-195">還原資料庫</span><span class="sxs-lookup"><span data-stu-id="84778-195">Restores a database</span></span> |
| [<span data-ttu-id="84778-196">取得建立或更新資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="84778-196">Get Create or Update Database Status</span></span>](https://msdn.microsoft.com/library/azure/mt643934.aspx) |<span data-ttu-id="84778-197">在還原作業期間傳回 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="84778-197">Returns hello status during a restore operation</span></span> |
|  | |

## <a name="summary"></a><span data-ttu-id="84778-198">摘要</span><span class="sxs-lookup"><span data-stu-id="84778-198">Summary</span></span>
<span data-ttu-id="84778-199">自動備份可在發生使用者和應用程式錯誤、意外刪除資料庫和長時間中斷時保護您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="84778-199">Automatic backups protect your databases from user and application errors, accidental database deletion, and prolonged outages.</span></span> <span data-ttu-id="84778-200">這項內建的功能適用於所有服務層和效能層級。</span><span class="sxs-lookup"><span data-stu-id="84778-200">This built-in capability is available for all service tiers and performance levels.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="84778-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84778-201">Next steps</span></span>
* <span data-ttu-id="84778-202">如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="84778-202">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="84778-203">toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="84778-203">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="84778-204">toolearn 有關長期備份的保留，請參閱[長期備份的保留](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="84778-204">toolearn about long-term backup retention, see [Long-term backup retention](sql-database-long-term-retention.md)</span></span>
* <span data-ttu-id="84778-205">tooconfigure，管理和還原的使用 hello Azure 復原服務保存庫中的自動備份的長期保存從 Azure 入口網站，請參閱[設定和使用長期備份保留](sql-database-long-term-backup-retention-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="84778-205">tooconfigure, manage, and restore from long-term retention of automated backups in an Azure Recovery Services vault using hello Azure portal, see [Configure and use long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span> 
* <span data-ttu-id="84778-206">toolearn 有關更快速的復原選項，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="84778-206">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
