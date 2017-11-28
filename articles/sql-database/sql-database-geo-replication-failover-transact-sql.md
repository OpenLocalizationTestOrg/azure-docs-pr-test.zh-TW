---
title: "TSQL：起始 Azure SQL Database 的容錯移轉 | Microsoft Docs"
description: "使用 Transact-SQL 為 Azure SQL Database 起始計劃性或非計劃性容錯移轉"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 459941d2c82e5d4ef62beab4ccf775ab8f5efce4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a><span data-ttu-id="99291-103">使用 Transact-SQL 為 Azure SQL Database 起始計劃性或非計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="99291-103">Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL</span></span>

<span data-ttu-id="99291-104">本文說明如何使用 Transact-SQL 起始容錯移轉至次要 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="99291-104">This article shows you how to initiate failover to a secondary SQL Database using Transact-SQL.</span></span> <span data-ttu-id="99291-105">若要設定異地複寫，請參閱[為 Azure SQL Database 設定異地複寫](sql-database-geo-replication-transact-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="99291-105">To configure geo-replication, see [Configure geo-replication for Azure SQL Database](sql-database-geo-replication-transact-sql.md).</span></span>

<span data-ttu-id="99291-106">若要起始容錯移轉，您需要下列各項︰</span><span class="sxs-lookup"><span data-stu-id="99291-106">To initiate failover, you need the following:</span></span>

* <span data-ttu-id="99291-107">主要資料庫上的 DBManager 登入</span><span class="sxs-lookup"><span data-stu-id="99291-107">A login that is DBManager on the primary</span></span>
* <span data-ttu-id="99291-108">擁有您要異地複寫之本機資料庫的 db_ownership</span><span class="sxs-lookup"><span data-stu-id="99291-108">Have db_ownership of the local database that you will geo-replicate</span></span>
* <span data-ttu-id="99291-109">成為您為異地複寫所設定之夥伴伺服器上的 DBManager</span><span class="sxs-lookup"><span data-stu-id="99291-109">Be DBManager on the partner server(s) to which you will configure geo-replication</span></span>
* <span data-ttu-id="99291-110">最新版的 SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="99291-110">Newest version of SQL Server Management Studio (SSMS)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99291-111">建議您一律使用最新版本的 Management Studio 保持與 Microsoft Azure 及 SQL Database 更新同步。</span><span class="sxs-lookup"><span data-stu-id="99291-111">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="99291-112">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99291-112">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-to-become-the-new-primary"></a><span data-ttu-id="99291-113">起始規劃的容錯移轉，將次要資料庫升級成為新主要複本</span><span class="sxs-lookup"><span data-stu-id="99291-113">Initiate a planned failover promoting a secondary database to become the new primary</span></span>
<span data-ttu-id="99291-114">您可以使用 **ALTER DATABASE** 陳述式，來升級次要資料庫，使它成為規劃的方式中的新主要資料庫，將現有主要降級成為次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="99291-114">You can use the **ALTER DATABASE** statement to promote a secondary database to become the new primary database in a planned fashion, demoting the existing primary to become a secondary.</span></span> <span data-ttu-id="99291-115">此陳述式是在要升級的異地複寫次要資料庫所在的 Azure SQL Database 邏輯伺服器上的 master 資料庫上執行。</span><span class="sxs-lookup"><span data-stu-id="99291-115">This statement is executed on the master database on the Azure SQL Database logical server in which the geo-replicated secondary database that is being promoted resides.</span></span> <span data-ttu-id="99291-116">這項功能是為了規劃的容錯移轉 (例如 DR 鑽研期間) 設計，並且需要主要資料庫可供使用。</span><span class="sxs-lookup"><span data-stu-id="99291-116">This functionality is designed for planned failover, such as during the DR drills, and requires that the primary database be available.</span></span>

<span data-ttu-id="99291-117">此命令會執行下列工作流程：</span><span class="sxs-lookup"><span data-stu-id="99291-117">The command performs the following workflow:</span></span>

1. <span data-ttu-id="99291-118">暫時切換複寫為同步模式，造成所有未完成的交易被排清至次要複本並封鎖所有新交易；</span><span class="sxs-lookup"><span data-stu-id="99291-118">Temporarily switches replication to synchronous mode, causing all outstanding transactions to be flushed to the secondary and blocking all new transactions;</span></span>
2. <span data-ttu-id="99291-119">切換異地複寫合作關係中兩個資料庫的角色。</span><span class="sxs-lookup"><span data-stu-id="99291-119">Switches the roles of the two databases in the geo-replication partnership.</span></span>  

<span data-ttu-id="99291-120">此順序可保證在角色切換之前兩個資料庫經過同步處理，因此不會發生資料遺失。</span><span class="sxs-lookup"><span data-stu-id="99291-120">This sequence guarantees that the two databases are synchronized before the roles switch and therefore no data loss will occur.</span></span> <span data-ttu-id="99291-121">切換角色時，會有一小段時間無法使用這兩個資料庫 (大約為 0 到 25 秒)。</span><span class="sxs-lookup"><span data-stu-id="99291-121">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="99291-122">如果主要資料庫有多個次要資料庫，此命令會自動重新設定其他次要複本以連接至新的主要複本。</span><span class="sxs-lookup"><span data-stu-id="99291-122">If the primary database has multiple secondary databases, the command will automatically reconfigure the other secondaries to connect to the new primary.</span></span>  <span data-ttu-id="99291-123">在正常情況下，完成整個作業所需的時間應該少於一分鐘。</span><span class="sxs-lookup"><span data-stu-id="99291-123">The entire operation should take less than a minute to complete under normal circumstances.</span></span> <span data-ttu-id="99291-124">如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="99291-124">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>

<span data-ttu-id="99291-125">使用下列步驟來起始規劃的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="99291-125">Use the following steps to initiate a planned failover.</span></span>

1. <span data-ttu-id="99291-126">在 Management Studio 中，連接到異地複寫次要資料庫所在的 Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="99291-126">In Management Studio, connect to the Azure SQL Database logical server in which a geo-replicated secondary database resides.</span></span>
2. <span data-ttu-id="99291-127">開啟 Databases 資料夾、展開 [System Databases] 資料夾、在 [master] 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="99291-127">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="99291-128">使用下列 **ALTER DATABASE** 陳述式，將次要資料庫切換為主要角色。</span><span class="sxs-lookup"><span data-stu-id="99291-128">Use the following **ALTER DATABASE** statement to switch the secondary database to the primary role.</span></span>
   
        ALTER DATABASE <MyDB> FAILOVER;
4. <span data-ttu-id="99291-129">按一下 [執行]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="99291-129">Click **Execute** to run the query.</span></span>

> [!NOTE]
> <span data-ttu-id="99291-130">在少數情況下，作業會無法完成並且可能會出現停滯。</span><span class="sxs-lookup"><span data-stu-id="99291-130">In rare cases, it is possible that the operation cannot complete and may appear stuck.</span></span> <span data-ttu-id="99291-131">在此情況下，使用者可以執行強制容錯移轉命令並接受資料遺失。</span><span class="sxs-lookup"><span data-stu-id="99291-131">In this case, the user can execute the force failover command and accept data loss.</span></span>
> 
> 

## <a name="initiate-an-unplanned-failover-from-the-primary-database-to-the-secondary-database"></a><span data-ttu-id="99291-132">起始從主要資料庫到次要資料庫的未規劃的容錯移轉</span><span class="sxs-lookup"><span data-stu-id="99291-132">Initiate an unplanned failover from the primary database to the secondary database</span></span>
<span data-ttu-id="99291-133">您可以使用 **ALTER DATABASE** 陳述式，來升級次要資料庫，使它成為未規劃的方式中的新主要資料庫，每當主要資料庫無法使用時，一次強制將現有主要降級成為次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="99291-133">You can use the **ALTER DATABASE** statement to promote a secondary database to become the new primary database in an unplanned fashion, forcing the demotion of the existing primary to become a secondary at a time when the primary database is no longer available.</span></span> <span data-ttu-id="99291-134">此陳述式是在要升級的異地複寫次要資料庫所在的 Azure SQL Database 邏輯伺服器上的 master 資料庫上執行。</span><span class="sxs-lookup"><span data-stu-id="99291-134">This statement is executed on the master database on the Azure SQL Database logical server in which the geo-replicated secondary database that is being promoted resides.</span></span>

<span data-ttu-id="99291-135">這項功能是針對還原資料庫的可用性非常重要而且部分資料遺失是可接受時的災害復原所設計。</span><span class="sxs-lookup"><span data-stu-id="99291-135">This functionality is designed for disaster recovery when restoring availability of the database is critical and some data loss is acceptable.</span></span> <span data-ttu-id="99291-136">叫用強制容錯移轉時，指定的次要資料庫立即成為主要資料庫，並開始接受寫入交易。</span><span class="sxs-lookup"><span data-stu-id="99291-136">When forced failover is invoked, the specified secondary database immediately becomes the primary database and begins accepting write transactions.</span></span> <span data-ttu-id="99291-137">原始主要資料庫能夠與這個新的主要資料庫重新連線時，會在原始主要資料庫執行增量備份，而舊的主要資料庫會變成新主要資料庫的次要資料庫；之後就只是新的主要資料庫的複本。</span><span class="sxs-lookup"><span data-stu-id="99291-137">As soon as the original primary database is able to reconnect with this new primary database, an incremental backup is taken on the original primary database and the old primary database is made into a secondary database for the new primary database; subsequently, it is merely a synchronizing replica of the new primary.</span></span>

<span data-ttu-id="99291-138">不過，因為次要資料庫上不支援還原時間點，發生強制容錯移轉之前，如果使用者想要復原已認可到舊主要資料庫但尚未複寫到新主要資料庫的資料，使用者應該接洽支援人員復源遺失的資料。</span><span class="sxs-lookup"><span data-stu-id="99291-138">However, because Point In Time Restore is not supported on the secondary databases, if the user wishes to recover data committed to the old primary database that had not been replicated to the new primary database before the forced failover occurred, the user will need to engage support to recover this lost data.</span></span>

<span data-ttu-id="99291-139">如果主要資料庫有多個次要資料庫，此命令會自動重新設定其他次要複本以連接至新的主要複本。</span><span class="sxs-lookup"><span data-stu-id="99291-139">If the primary database has multiple secondary databases, the command will automatically reconfigure the other secondaries to connect to the new primary.</span></span>

<span data-ttu-id="99291-140">使用下列步驟來起始非計劃性的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="99291-140">Use the following steps to initiate an unplanned failover.</span></span>

1. <span data-ttu-id="99291-141">在 Management Studio 中，連接到異地複寫次要資料庫所在的 Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="99291-141">In Management Studio, connect to the Azure SQL Database logical server in which a geo-replicated secondary database resides.</span></span>
2. <span data-ttu-id="99291-142">開啟 Databases 資料夾、展開 [System Databases] 資料夾、在 [master] 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="99291-142">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="99291-143">使用下列 **ALTER DATABASE** 陳述式，將次要資料庫切換為主要角色。</span><span class="sxs-lookup"><span data-stu-id="99291-143">Use the following **ALTER DATABASE** statement to switch the secondary database to the primary role.</span></span>
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. <span data-ttu-id="99291-144">按一下 [執行]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="99291-144">Click **Execute** to run the query.</span></span>

> [!NOTE]
> <span data-ttu-id="99291-145">如果在主要資料庫和次要資料庫上線時發出此命令，舊的主要會立即變成新的次要資料庫，而不會進行資料同步處理。</span><span class="sxs-lookup"><span data-stu-id="99291-145">If the command is issued when both primary and secondary are online the old primary will become the new secondary immediately without data synchronization.</span></span> <span data-ttu-id="99291-146">發出命令時，如果主要複本正在認可交易，可能會發生部分資料遺失。</span><span class="sxs-lookup"><span data-stu-id="99291-146">If the primary is committing transactions when the command is issued some data loss may occur.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="99291-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99291-147">Next steps</span></span>
* <span data-ttu-id="99291-148">容錯移轉之後，請確認已在新的主要資料庫上設定伺服器和資料庫的驗證需求。</span><span class="sxs-lookup"><span data-stu-id="99291-148">After failover, ensure the authentication requirements for your server and database are configured on the new primary.</span></span> <span data-ttu-id="99291-149">如需詳細資訊，請參閱 [災害復原後的 SQL Database 安全性](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="99291-149">For details, see [SQL Database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>
* <span data-ttu-id="99291-150">若要了解如何使用主動式異地複寫在災害之後進行復原，包括復原前和復原後步驟，以及執行災害復原演練，請參閱[災害復原](sql-database-disaster-recovery.md)</span><span class="sxs-lookup"><span data-stu-id="99291-150">To learn recovering after a disaster using active geo-replication, including pre-recovery and post-recovery steps and performing a disaster recovery drill, see [Disaster Recovery](sql-database-disaster-recovery.md)</span></span>
* <span data-ttu-id="99291-151">如需 Sasha Nosov 有關主動式異地複寫的部落格文章，請參閱[新異地複寫功能要點](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)</span><span class="sxs-lookup"><span data-stu-id="99291-151">For a Sasha Nosov blog post about active geo-replication, see [Spotlight on new geo-replication capabilities](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)</span></span>
* <span data-ttu-id="99291-152">如需如何設計雲端應用程式使用主動式異地複寫的相關資訊，請參閱[使用異地複寫設計商務持續性的雲端應用程式](sql-database-designing-cloud-solutions-for-disaster-recovery.md)</span><span class="sxs-lookup"><span data-stu-id="99291-152">For information about designing cloud applications to use active geo-replication, see [Designing cloud applications for business continuity using geo-replication](sql-database-designing-cloud-solutions-for-disaster-recovery.md)</span></span>
* <span data-ttu-id="99291-153">如需使用主動式異地複寫與彈性集區的相關資訊，請參閱[彈性集區災害復原策略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="99291-153">For information about using active geo-replication with elastic pools, see [Elastic Pool disaster recovery strategies](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).</span></span>
* <span data-ttu-id="99291-154">如需商務持續性的概觀，請參閱[商務持續性概觀](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="99291-154">For an overview of business continuity, see [Business Continuity Overview](sql-database-business-continuity.md)</span></span>

