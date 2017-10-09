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
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a><span data-ttu-id="4aff7-103">使用 Transact-SQL 為 Azure SQL Database 起始計劃性或非計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="4aff7-103">Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL</span></span>

<span data-ttu-id="4aff7-104">本文章將示範如何 tooinitiate 容錯移轉 tooa 使用 TRANSACT-SQL 的次要 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4aff7-104">This article shows you how tooinitiate failover tooa secondary SQL Database using Transact-SQL.</span></span> <span data-ttu-id="4aff7-105">tooconfigure 異地複寫，請參閱[for Azure SQL Database 設定異地複寫](sql-database-geo-replication-transact-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="4aff7-105">tooconfigure geo-replication, see [Configure geo-replication for Azure SQL Database](sql-database-geo-replication-transact-sql.md).</span></span>

<span data-ttu-id="4aff7-106">tooinitiate 容錯移轉時，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4aff7-106">tooinitiate failover, you need hello following:</span></span>

* <span data-ttu-id="4aff7-107">為 DBManager hello 主要的登入</span><span class="sxs-lookup"><span data-stu-id="4aff7-107">A login that is DBManager on hello primary</span></span>
* <span data-ttu-id="4aff7-108">具有 db_ownership hello 本機資料庫，您會進行異地複寫</span><span class="sxs-lookup"><span data-stu-id="4aff7-108">Have db_ownership of hello local database that you will geo-replicate</span></span>
* <span data-ttu-id="4aff7-109">DBManager 位於 hello 夥伴伺服器 toowhich 您將設定異地複寫</span><span class="sxs-lookup"><span data-stu-id="4aff7-109">Be DBManager on hello partner server(s) toowhich you will configure geo-replication</span></span>
* <span data-ttu-id="4aff7-110">最新版的 SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="4aff7-110">Newest version of SQL Server Management Studio (SSMS)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4aff7-111">建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4aff7-111">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="4aff7-112">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4aff7-112">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a><span data-ttu-id="4aff7-113">初始化規劃的容錯移轉升級的次要資料庫 toobecome hello 新主要複本</span><span class="sxs-lookup"><span data-stu-id="4aff7-113">Initiate a planned failover promoting a secondary database toobecome hello new primary</span></span>
<span data-ttu-id="4aff7-114">您可以使用 hello **ALTER DATABASE**陳述式 toopromote 次要資料庫 toobecome hello 新主要複本在計劃的方式，降級 hello 現有主要 toobecome 次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="4aff7-114">You can use hello **ALTER DATABASE** statement toopromote a secondary database toobecome hello new primary database in a planned fashion, demoting hello existing primary toobecome a secondary.</span></span> <span data-ttu-id="4aff7-115">Hello master 資料庫中的 hello 所在地理區域複寫的次要資料庫正在升級的 hello Azure SQL Database 邏輯伺服器上執行此陳述式。</span><span class="sxs-lookup"><span data-stu-id="4aff7-115">This statement is executed on hello master database on hello Azure SQL Database logical server in which hello geo-replicated secondary database that is being promoted resides.</span></span> <span data-ttu-id="4aff7-116">這項功能規劃的容錯移轉，例如設計期間 hello DR 鑽研，而且需要該 hello 主要資料庫可以使用。</span><span class="sxs-lookup"><span data-stu-id="4aff7-116">This functionality is designed for planned failover, such as during hello DR drills, and requires that hello primary database be available.</span></span>

<span data-ttu-id="4aff7-117">hello 命令會執行下列工作流程的 hello:</span><span class="sxs-lookup"><span data-stu-id="4aff7-117">hello command performs hello following workflow:</span></span>

1. <span data-ttu-id="4aff7-118">交換器複寫 toosynchronous 模式，導致所有未完成的交易 toobe 暫時排清 toohello 次要資料庫，封鎖所有新的交易。</span><span class="sxs-lookup"><span data-stu-id="4aff7-118">Temporarily switches replication toosynchronous mode, causing all outstanding transactions toobe flushed toohello secondary and blocking all new transactions;</span></span>
2. <span data-ttu-id="4aff7-119">交換器 hello hello hello 地理複寫合作關係中的兩個資料庫的角色。</span><span class="sxs-lookup"><span data-stu-id="4aff7-119">Switches hello roles of hello two databases in hello geo-replication partnership.</span></span>  

<span data-ttu-id="4aff7-120">此順序可保證該 hello hello 角色切換，因此會發生資料不會遺失之前，同步處理兩個資料庫。</span><span class="sxs-lookup"><span data-stu-id="4aff7-120">This sequence guarantees that hello two databases are synchronized before hello roles switch and therefore no data loss will occur.</span></span> <span data-ttu-id="4aff7-121">沒有在短期間這兩個資料庫是無法使用 （在 0 too25 秒 hello 順序） 而 hello 角色切換。</span><span class="sxs-lookup"><span data-stu-id="4aff7-121">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="4aff7-122">如果 hello 主要資料庫中有多個次要資料庫、 hello 命令將會自動重新設定 hello 其他次要 tooconnect toohello 新主要複本。</span><span class="sxs-lookup"><span data-stu-id="4aff7-122">If hello primary database has multiple secondary databases, hello command will automatically reconfigure hello other secondaries tooconnect toohello new primary.</span></span>  <span data-ttu-id="4aff7-123">hello 整個作業花費時間小於一分鐘 toocomplete 在一般情況下。</span><span class="sxs-lookup"><span data-stu-id="4aff7-123">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> <span data-ttu-id="4aff7-124">如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="4aff7-124">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>

<span data-ttu-id="4aff7-125">使用下列步驟 tooinitiate 規劃的容錯移轉的 hello。</span><span class="sxs-lookup"><span data-stu-id="4aff7-125">Use hello following steps tooinitiate a planned failover.</span></span>

1. <span data-ttu-id="4aff7-126">在 Management Studio 中進行地理複寫的次要資料庫所在的 toohello Azure SQL Database 邏輯伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="4aff7-126">In Management Studio, connect toohello Azure SQL Database logical server in which a geo-replicated secondary database resides.</span></span>
2. <span data-ttu-id="4aff7-127">開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="4aff7-127">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="4aff7-128">使用下列 hello **ALTER DATABASE**陳述式 tooswitch hello 次要資料庫 toohello 主要角色。</span><span class="sxs-lookup"><span data-stu-id="4aff7-128">Use hello following **ALTER DATABASE** statement tooswitch hello secondary database toohello primary role.</span></span>
   
        ALTER DATABASE <MyDB> FAILOVER;
4. <span data-ttu-id="4aff7-129">按一下**Execute** toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4aff7-129">Click **Execute** toorun hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="4aff7-130">在極少數的情況下，很可能 hello 作業無法完成，而且可能會出現陷入不斷。</span><span class="sxs-lookup"><span data-stu-id="4aff7-130">In rare cases, it is possible that hello operation cannot complete and may appear stuck.</span></span> <span data-ttu-id="4aff7-131">在此情況下，hello 使用者可以執行 hello 強制容錯移轉命令，並接受資料遺失。</span><span class="sxs-lookup"><span data-stu-id="4aff7-131">In this case, hello user can execute hello force failover command and accept data loss.</span></span>
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a><span data-ttu-id="4aff7-132">初始化規劃的容錯移轉從 hello 主要資料庫 toohello 次要資料庫</span><span class="sxs-lookup"><span data-stu-id="4aff7-132">Initiate an unplanned failover from hello primary database toohello secondary database</span></span>
<span data-ttu-id="4aff7-133">您可以使用 hello **ALTER DATABASE**陳述式 toopromote 次要資料庫 toobecome hello 新的主要資料庫中未規劃的方式，強制 hello 現有主要 toobecome hello 降級次要一次當 hello主要資料庫已無法再使用。</span><span class="sxs-lookup"><span data-stu-id="4aff7-133">You can use hello **ALTER DATABASE** statement toopromote a secondary database toobecome hello new primary database in an unplanned fashion, forcing hello demotion of hello existing primary toobecome a secondary at a time when hello primary database is no longer available.</span></span> <span data-ttu-id="4aff7-134">Hello master 資料庫中的 hello 所在地理區域複寫的次要資料庫正在升級的 hello Azure SQL Database 邏輯伺服器上執行此陳述式。</span><span class="sxs-lookup"><span data-stu-id="4aff7-134">This statement is executed on hello master database on hello Azure SQL Database logical server in which hello geo-replicated secondary database that is being promoted resides.</span></span>

<span data-ttu-id="4aff7-135">當 hello 資料庫的還原可用性至關重要，而是可以接受的部分資料遺失時，這項功能可供災害復原。</span><span class="sxs-lookup"><span data-stu-id="4aff7-135">This functionality is designed for disaster recovery when restoring availability of hello database is critical and some data loss is acceptable.</span></span> <span data-ttu-id="4aff7-136">叫用強制容錯移轉時，次要資料庫立即成為 hello 的主要資料庫，以及開始接受寫入交易，也會指定 hello。</span><span class="sxs-lookup"><span data-stu-id="4aff7-136">When forced failover is invoked, hello specified secondary database immediately becomes hello primary database and begins accepting write transactions.</span></span> <span data-ttu-id="4aff7-137">Hello 原始的主要資料庫是無法 tooreconnect 與這個新的主要資料庫，因為在 hello 原始的主要資料庫會從增量備份和 hello 舊主要資料庫成為新主要資料庫 hello; 的次要資料庫接著，它是只 hello 新主要複本的同步處理複本。</span><span class="sxs-lookup"><span data-stu-id="4aff7-137">As soon as hello original primary database is able tooreconnect with this new primary database, an incremental backup is taken on hello original primary database and hello old primary database is made into a secondary database for hello new primary database; subsequently, it is merely a synchronizing replica of hello new primary.</span></span>

<span data-ttu-id="4aff7-138">不過，因為點中還原時間上不支援 hello 次要資料庫，如果 hello 使用者想認可 toorecover 資料 toohello 舊主要資料庫中有尚未複寫 toohello 新的主要資料庫發生 hello 強制容錯移轉之前hello 使用者將需要 tooengage 支援 toorecover 這遺失資料。</span><span class="sxs-lookup"><span data-stu-id="4aff7-138">However, because Point In Time Restore is not supported on hello secondary databases, if hello user wishes toorecover data committed toohello old primary database that had not been replicated toohello new primary database before hello forced failover occurred, hello user will need tooengage support toorecover this lost data.</span></span>

<span data-ttu-id="4aff7-139">如果 hello 主要資料庫中有多個次要資料庫、 hello 命令將會自動重新設定 hello 其他次要 tooconnect toohello 新主要複本。</span><span class="sxs-lookup"><span data-stu-id="4aff7-139">If hello primary database has multiple secondary databases, hello command will automatically reconfigure hello other secondaries tooconnect toohello new primary.</span></span>

<span data-ttu-id="4aff7-140">使用下列步驟 tooinitiate 未規劃的容錯移轉的 hello。</span><span class="sxs-lookup"><span data-stu-id="4aff7-140">Use hello following steps tooinitiate an unplanned failover.</span></span>

1. <span data-ttu-id="4aff7-141">在 Management Studio 中進行地理複寫的次要資料庫所在的 toohello Azure SQL Database 邏輯伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="4aff7-141">In Management Studio, connect toohello Azure SQL Database logical server in which a geo-replicated secondary database resides.</span></span>
2. <span data-ttu-id="4aff7-142">開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="4aff7-142">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="4aff7-143">使用下列 hello **ALTER DATABASE**陳述式 tooswitch hello 次要資料庫 toohello 主要角色。</span><span class="sxs-lookup"><span data-stu-id="4aff7-143">Use hello following **ALTER DATABASE** statement tooswitch hello secondary database toohello primary role.</span></span>
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. <span data-ttu-id="4aff7-144">按一下**Execute** toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4aff7-144">Click **Execute** toorun hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="4aff7-145">如果主要和次要資料庫已上線時，會發出 hello 命令將會變成 hello 舊的主要 hello 立即不進行資料同步處理新的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="4aff7-145">If hello command is issued when both primary and secondary are online hello old primary will become hello new secondary immediately without data synchronization.</span></span> <span data-ttu-id="4aff7-146">如果是主要的 hello hello 命令發出部分資料遺失時認可的交易可能會發生。</span><span class="sxs-lookup"><span data-stu-id="4aff7-146">If hello primary is committing transactions when hello command is issued some data loss may occur.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4aff7-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4aff7-147">Next steps</span></span>
* <span data-ttu-id="4aff7-148">容錯移轉之後，確定已 hello 新主要複本上設定您的伺服器和資料庫的 hello 驗證需求。</span><span class="sxs-lookup"><span data-stu-id="4aff7-148">After failover, ensure hello authentication requirements for your server and database are configured on hello new primary.</span></span> <span data-ttu-id="4aff7-149">如需詳細資訊，請參閱 [災害復原後的 SQL Database 安全性](sql-database-geo-replication-security-config.md)。</span><span class="sxs-lookup"><span data-stu-id="4aff7-149">For details, see [SQL Database security after disaster recovery](sql-database-geo-replication-security-config.md).</span></span>
* <span data-ttu-id="4aff7-150">請參閱 toolearn 之後使用作用中地理複寫，包括前復原及復原後的步驟，以及執行災害復原訓練，災害復原[災害復原](sql-database-disaster-recovery.md)</span><span class="sxs-lookup"><span data-stu-id="4aff7-150">toolearn recovering after a disaster using active geo-replication, including pre-recovery and post-recovery steps and performing a disaster recovery drill, see [Disaster Recovery](sql-database-disaster-recovery.md)</span></span>
* <span data-ttu-id="4aff7-151">如需 Sasha Nosov 有關主動式異地複寫的部落格文章，請參閱[新異地複寫功能要點](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)</span><span class="sxs-lookup"><span data-stu-id="4aff7-151">For a Sasha Nosov blog post about active geo-replication, see [Spotlight on new geo-replication capabilities](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)</span></span>
* <span data-ttu-id="4aff7-152">設計雲端應用程式 toouse 作用中地理複寫的相關資訊，請參閱[設計雲端應用程式使用地理複寫的商務持續性](sql-database-designing-cloud-solutions-for-disaster-recovery.md)</span><span class="sxs-lookup"><span data-stu-id="4aff7-152">For information about designing cloud applications toouse active geo-replication, see [Designing cloud applications for business continuity using geo-replication](sql-database-designing-cloud-solutions-for-disaster-recovery.md)</span></span>
* <span data-ttu-id="4aff7-153">如需使用主動式異地複寫與彈性集區的相關資訊，請參閱[彈性集區災害復原策略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="4aff7-153">For information about using active geo-replication with elastic pools, see [Elastic Pool disaster recovery strategies](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).</span></span>
* <span data-ttu-id="4aff7-154">如需商務持續性的概觀，請參閱[商務持續性概觀](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="4aff7-154">For an overview of business continuity, see [Business Continuity Overview](sql-database-business-continuity.md)</span></span>

