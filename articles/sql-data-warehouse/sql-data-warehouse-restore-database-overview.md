---
title: "還原 Azure 資料倉儲 - 本機與異地備援 | Microsoft Docs"
description: "復原 Azure SQL 資料倉儲中資料庫之資料庫還原選項的概觀。"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: ea42b7135d0695b66d569095e70bb3d9f8b9594b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="5bc8e-103">SQL 資料倉儲還原</span><span class="sxs-lookup"><span data-stu-id="5bc8e-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5bc8e-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="5bc8e-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="5bc8e-105">[入口網站][Portal]</span><span class="sxs-lookup"><span data-stu-id="5bc8e-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="5bc8e-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="5bc8e-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="5bc8e-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="5bc8e-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="5bc8e-108">「SQL 資料倉儲」提供本機和異地還原作為其資料倉儲災害復原功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="5bc8e-109">使用資料倉儲備份將您的資料倉儲還原至主要區域中的某個還原點，或使用異地備援備份來還原至不同的地理區域。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-109">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or use geo-redundant backups to restore to a different geographical region.</span></span> <span data-ttu-id="5bc8e-110">本文說明還原資料倉儲的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-110">This article explains the specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="5bc8e-111">什麼是資料倉儲還原？</span><span class="sxs-lookup"><span data-stu-id="5bc8e-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="5bc8e-112">資料倉儲還原係指從現有或已刪除之資料倉儲的備份建立的新資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="5bc8e-113">還原的資料倉儲會重新建立特定時間的已備份資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-113">The restored data warehouse re-creates the backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="5bc8e-114">由於「SQL 資料倉儲」是一個分散式系統，因此會從儲存在 Azure Blob 中的許多備份檔案建立一個資料倉儲還原。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="5bc8e-115">資料庫還原是所有商務持續性和災害復原策略中不可或缺的一部分，因為它可在您的資料發生意外損毀或刪除之後重新建立該資料。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="5bc8e-116">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5bc8e-116">For more information, see:</span></span>

* [<span data-ttu-id="5bc8e-117">SQL 資料倉儲備份</span><span class="sxs-lookup"><span data-stu-id="5bc8e-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="5bc8e-118">商務持續性概觀</span><span class="sxs-lookup"><span data-stu-id="5bc8e-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="5bc8e-119">資料倉儲還原點</span><span class="sxs-lookup"><span data-stu-id="5bc8e-119">Data warehouse restore points</span></span>
<span data-ttu-id="5bc8e-120">使用「Azure 進階儲存體」的一項優點是，「SQL 資料倉儲」會使用「Azure 儲存體」Blob 快照集來備份主要資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the primary data warehouse.</span></span> <span data-ttu-id="5bc8e-121">每個快照都有一個代表快照開始時間的還原點。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-121">Each snapshot has a restore point that represents the time the snapshot started.</span></span> <span data-ttu-id="5bc8e-122">若要還原資料倉儲，您需選擇一個還原點並發出還原命令。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-122">To restore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="5bc8e-123">「SQL 資料倉儲」一律是將備份還原到新的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-123">SQL Data Warehouse always restores the backup to a new data warehouse.</span></span> <span data-ttu-id="5bc8e-124">您可以保留已還原的資料倉儲和目前的資料倉儲，或是刪除它們其中之一。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-124">You can either keep the restored data warehouse and the current one, or delete one of them.</span></span> <span data-ttu-id="5bc8e-125">如果您想要以已還原的資料倉儲取代目前的資料倉儲，您可以將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-125">If you want to replace the current data warehouse with the restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="5bc8e-126">如果您需要還原已刪除或暫停的資料倉儲，您可以[建立支援票證](sql-data-warehouse-get-started-create-support-ticket.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-126">If you need to restore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore the last available restore point.

Yes, for the next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps the data warehouse and its snapshots for seven days just in case you need the data. After seven days, you won't be able to restore to any of the restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="5bc8e-127">異地備援還原</span><span class="sxs-lookup"><span data-stu-id="5bc8e-127">Geo-redundant restore</span></span>
<span data-ttu-id="5bc8e-128">您可以將資料倉儲還原到在您選擇的效能等級支援您 Azure SQL 資料倉儲的任何區域。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-128">You can restore your data warehouse to any region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="5bc8e-129">請注意，在預覽期間，並非所有區域均支援 9000 和 18000 DWU。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-129">Please note that 9000 and 18000 DWU are not supported in all regions during the preview.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc8e-130">若要執行異地備援還原，您不可選擇退出這項功能。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-130">To perform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="5bc8e-131">還原時間軸</span><span class="sxs-lookup"><span data-stu-id="5bc8e-131">Restore timeline</span></span>
<span data-ttu-id="5bc8e-132">您可以將資料庫還原到過去七天內的任何可用還原點。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-132">You can restore a database to any available restore point within the last seven days.</span></span> <span data-ttu-id="5bc8e-133">快照集每四到八個小時會啟動，並且可供使用七天。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-133">Snapshots start every four to eight hours and are available for seven days.</span></span> <span data-ttu-id="5bc8e-134">當快照集存在時間超過七天，它就會過期，而且無法再使用其還原點。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="5bc8e-135">還原成本</span><span class="sxs-lookup"><span data-stu-id="5bc8e-135">Restore costs</span></span>
<span data-ttu-id="5bc8e-136">所還原資料倉儲的儲存體收費方式是以「Azure 進階儲存體」費率計費。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-136">The storage charge for the restored data warehouse is billed at the Azure Premium Storage rate.</span></span> 

<span data-ttu-id="5bc8e-137">如果您將已還原的資料倉儲暫停，會依據 Azure 進階儲存體費率向您收取儲存體費用。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-137">If you pause a restored data warehouse, you are charged for storage at the Azure Premium Storage rate.</span></span> <span data-ttu-id="5bc8e-138">暫停的好處是不會向您收取 DWU 計算資源的費用。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-138">The advantage of pausing is you are not charged for the DWU computing resources.</span></span>

<span data-ttu-id="5bc8e-139">如需 SQL 資料倉儲價格的相關詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="5bc8e-140">還原的用途</span><span class="sxs-lookup"><span data-stu-id="5bc8e-140">Uses for restore</span></span>
<span data-ttu-id="5bc8e-141">資料倉儲還原的主要用途是在發生意外資料遺失或損毀之後復原資料。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-141">The primary use for data warehouse restore is to recover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="5bc8e-142">您也可以使用資料倉儲還原來保留超過七天的備份。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-142">You can also use data warehouse restore to retain a backup for longer than seven days.</span></span> <span data-ttu-id="5bc8e-143">還原備份之後，資料倉儲會上線，而您可以無限期地暫停它來節省計算成本。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-143">Once the backup is restored, you have the data warehouse online and can pause it indefinitely to save compute costs.</span></span> <span data-ttu-id="5bc8e-144">暫停的資料庫會產生儲存體費用，以「Azure 進階儲存體」費率計費。</span><span class="sxs-lookup"><span data-stu-id="5bc8e-144">The paused database incurs storage charges at the Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="5bc8e-145">相關主題</span><span class="sxs-lookup"><span data-stu-id="5bc8e-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="5bc8e-146">案例</span><span class="sxs-lookup"><span data-stu-id="5bc8e-146">Scenarios</span></span>
* <span data-ttu-id="5bc8e-147">如需商務持續性概觀，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="5bc8e-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="5bc8e-148">若要執行資料倉儲還原，請使用下列方式來進行還原：</span><span class="sxs-lookup"><span data-stu-id="5bc8e-148">To perform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="5bc8e-149">Azure 入口網站 - 請參閱[使用 Azure 入口網站來還原資料倉儲](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5bc8e-149">Azure portal, see [Restore a data warehouse using the Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="5bc8e-150">PowerShell Cmdlet - 請參閱[使用 PowerShell Cmdlet 來還原資料倉儲](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="5bc8e-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="5bc8e-151">REST API - 請參閱[使用 REST API 來還原資料倉儲](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="5bc8e-151">REST APIs, see [Restore a data warehouse using the REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
