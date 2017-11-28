---
title: "Azure 資料倉儲中的本機和異地備援 aaaRestore |Microsoft 文件"
description: "復原資料庫，以在 Azure SQL 資料倉儲中的 hello 資料庫還原選項的概觀。"
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
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="95a47-103">SQL 資料倉儲還原</span><span class="sxs-lookup"><span data-stu-id="95a47-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="95a47-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="95a47-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="95a47-105">[入口網站][Portal]</span><span class="sxs-lookup"><span data-stu-id="95a47-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="95a47-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="95a47-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="95a47-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="95a47-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="95a47-108">「SQL 資料倉儲」提供本機和異地還原作為其資料倉儲災害復原功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="95a47-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="95a47-109">使用資料倉儲備份 toorestore 資料倉儲 tooa 還原點在 hello 主要區域中，或使用異地備援備份 toorestore tooa 不同的地理區域。</span><span class="sxs-lookup"><span data-stu-id="95a47-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="95a47-110">本文說明還原資料倉儲的 hello 的細節。</span><span class="sxs-lookup"><span data-stu-id="95a47-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="95a47-111">什麼是資料倉儲還原？</span><span class="sxs-lookup"><span data-stu-id="95a47-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="95a47-112">資料倉儲還原係指從現有或已刪除之資料倉儲的備份建立的新資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="95a47-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="95a47-113">hello 還原的資料倉儲重新建立在特定時間的 hello 備份資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="95a47-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="95a47-114">由於「SQL 資料倉儲」是一個分散式系統，因此會從儲存在 Azure Blob 中的許多備份檔案建立一個資料倉儲還原。</span><span class="sxs-lookup"><span data-stu-id="95a47-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="95a47-115">資料庫還原是所有商務持續性和災害復原策略中不可或缺的一部分，因為它可在您的資料發生意外損毀或刪除之後重新建立該資料。</span><span class="sxs-lookup"><span data-stu-id="95a47-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="95a47-116">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="95a47-116">For more information, see:</span></span>

* [<span data-ttu-id="95a47-117">SQL 資料倉儲備份</span><span class="sxs-lookup"><span data-stu-id="95a47-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="95a47-118">商務持續性概觀</span><span class="sxs-lookup"><span data-stu-id="95a47-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="95a47-119">資料倉儲還原點</span><span class="sxs-lookup"><span data-stu-id="95a47-119">Data warehouse restore points</span></span>
<span data-ttu-id="95a47-120">使用 Azure 高階儲存體的優點，作為 SQL 資料倉儲會使用 Azure 儲存體 Blob 快照集 toobackup hello 主要資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="95a47-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="95a47-121">每個快照集具有代表 hello 時間的還原點啟動 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="95a47-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="95a47-122">toorestore 資料倉儲，您選擇還原點，然後發出 restore 命令。</span><span class="sxs-lookup"><span data-stu-id="95a47-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="95a47-123">SQL 資料倉儲一律會還原 hello 備份 tooa 新的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="95a47-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="95a47-124">您可以保留 hello 還原的資料倉儲和 hello 目前一個，或刪除其中一個。</span><span class="sxs-lookup"><span data-stu-id="95a47-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="95a47-125">如果您想 tooreplace hello 目前資料倉儲以 hello 還原資料倉儲，您可以重新命名。</span><span class="sxs-lookup"><span data-stu-id="95a47-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="95a47-126">如果您需要 toorestore 已刪除或已暫停資料倉儲時，您可以[建立支援票證](sql-data-warehouse-get-started-create-support-ticket.md)。</span><span class="sxs-lookup"><span data-stu-id="95a47-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="95a47-127">異地備援還原</span><span class="sxs-lookup"><span data-stu-id="95a47-127">Geo-redundant restore</span></span>
<span data-ttu-id="95a47-128">您可以還原您支援您所選擇的效能層級的 Azure SQL 資料倉儲的資料倉儲 tooany 區域。</span><span class="sxs-lookup"><span data-stu-id="95a47-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="95a47-129">請注意，9000 和 18000 DWU 不支援在所有區域 hello 預覽期間。</span><span class="sxs-lookup"><span data-stu-id="95a47-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="95a47-130">您必須不選擇用這項功能的地理備援 tooperform 還原。</span><span class="sxs-lookup"><span data-stu-id="95a47-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="95a47-131">還原時間軸</span><span class="sxs-lookup"><span data-stu-id="95a47-131">Restore timeline</span></span>
<span data-ttu-id="95a47-132">您可以還原過去七天內 hello 的資料庫 tooany 可用還原時間點。</span><span class="sxs-lookup"><span data-stu-id="95a47-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="95a47-133">快照集開始每四個 tooeight 小時，且有七天。</span><span class="sxs-lookup"><span data-stu-id="95a47-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="95a47-134">當快照集存在時間超過七天，它就會過期，而且無法再使用其還原點。</span><span class="sxs-lookup"><span data-stu-id="95a47-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="95a47-135">還原成本</span><span class="sxs-lookup"><span data-stu-id="95a47-135">Restore costs</span></span>
<span data-ttu-id="95a47-136">hello hello 還原的資料倉儲儲存體費用是 hello Azure 高階儲存體費率計費。</span><span class="sxs-lookup"><span data-stu-id="95a47-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="95a47-137">如果您暫停還原的資料倉儲時，您將支付儲存體費率 hello Azure 高階儲存體。</span><span class="sxs-lookup"><span data-stu-id="95a47-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="95a47-138">暫停 hello 優點是您不需付費的 hello DWU 運算資源。</span><span class="sxs-lookup"><span data-stu-id="95a47-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="95a47-139">如需 SQL 資料倉儲價格的相關詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。</span><span class="sxs-lookup"><span data-stu-id="95a47-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="95a47-140">還原的用途</span><span class="sxs-lookup"><span data-stu-id="95a47-140">Uses for restore</span></span>
<span data-ttu-id="95a47-141">hello 主要用於資料倉儲還原資料意外遺失或損毀之後 toorecover 資料。</span><span class="sxs-lookup"><span data-stu-id="95a47-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="95a47-142">您也可以使用資料倉儲還原 tooretain 備份的時間超過七天。</span><span class="sxs-lookup"><span data-stu-id="95a47-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="95a47-143">Hello 備份還原之後，您會擁有 hello 資料倉儲線上的連線，並且可以暫停它無限期 toosave 計算成本。</span><span class="sxs-lookup"><span data-stu-id="95a47-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="95a47-144">hello 已暫停的資料庫會產生 hello Azure 高階儲存體費率的儲存體費用。</span><span class="sxs-lookup"><span data-stu-id="95a47-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="95a47-145">相關主題</span><span class="sxs-lookup"><span data-stu-id="95a47-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="95a47-146">案例</span><span class="sxs-lookup"><span data-stu-id="95a47-146">Scenarios</span></span>
* <span data-ttu-id="95a47-147">如需商務持續性概觀，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="95a47-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="95a47-148">資料倉儲 tooperform 還原，請使用還原：</span><span class="sxs-lookup"><span data-stu-id="95a47-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="95a47-149">Azure 入口網站，請參閱[還原資料倉儲使用 hello Azure 入口網站](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="95a47-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="95a47-150">PowerShell Cmdlet - 請參閱[使用 PowerShell Cmdlet 來還原資料倉儲](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="95a47-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="95a47-151">REST Api，請參閱[還原使用 hello REST Api 的資料倉儲](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="95a47-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

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
