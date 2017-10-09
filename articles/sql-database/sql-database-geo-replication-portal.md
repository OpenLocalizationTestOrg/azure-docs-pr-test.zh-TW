---
title: "Azure 入口網站︰SQL Database 異地複寫 | Microsoft Docs"
description: "針對 Azure SQL Database 設定地理複寫 hello Azure 入口網站和起始容錯移轉"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="bcea9-103">在 hello Azure 入口網站和起始容錯移轉中，設定 Azure SQL database 的作用中地理複寫</span><span class="sxs-lookup"><span data-stu-id="bcea9-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="bcea9-104">本文章將示範如何 tooconfigure 作用中地理複寫 SQL database 中 hello [Azure 入口網站](http://portal.azure.com)和 tooinitiate 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="bcea9-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="bcea9-105">tooinitiate 容錯移轉以 hello Azure 入口網站，請參閱[for Azure SQL Database 起始計劃性或非計劃性容錯移轉以 hello Azure 入口網站](sql-database-geo-replication-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="bcea9-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="bcea9-106">tooconfigure 作用中地理複寫使用 hello Azure 入口網站，您需要下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="bcea9-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="bcea9-107">Azure SQL database: hello 的 tooreplicate tooa 不同的地理區域的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="bcea9-108">作用中地理複寫必須是資料庫在 hello 之間相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bcea9-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="bcea9-109">新增次要資料庫</span><span class="sxs-lookup"><span data-stu-id="bcea9-109">Add a secondary database</span></span>
<span data-ttu-id="bcea9-110">hello 下列步驟會建立新的次要資料庫以進行異地複寫合作關係。</span><span class="sxs-lookup"><span data-stu-id="bcea9-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="bcea9-111">tooadd 次要資料庫，您必須是 hello 訂用帳戶擁有者或共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="bcea9-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="bcea9-112">hello 次要資料庫名稱為 hello 主要資料庫相同的 hello 且具有，根據預設，hello 相同服務層級。</span><span class="sxs-lookup"><span data-stu-id="bcea9-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="bcea9-113">hello 次要資料庫可以是單一資料庫或彈性集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="bcea9-114">如需詳細資訊，請參閱 [服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="bcea9-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="bcea9-115">建立並植入次要 hello 後，資料就會開始從 hello 主要資料庫 toohello 新的次要資料庫複寫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="bcea9-116">如果 hello 夥伴資料庫已經存在 （例如，由於結束先前的地理複寫關聯性） hello 命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="bcea9-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="bcea9-117">在 hello [Azure 入口網站](http://portal.azure.com)，瀏覽您要進行地理複寫 tooset toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="bcea9-118">在 hello SQL 資料庫 頁面上，選取 **地理複寫**，然後選取 hello 區域 toocreate hello 次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="bcea9-119">您可以選取任何區域以外 hello 區域裝載 hello 主要資料庫，但我們建議 hello[配對的區域](../best-practices-availability-paired-regions.md)。</span><span class="sxs-lookup"><span data-stu-id="bcea9-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![設定異地複寫](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="bcea9-121">選取或設定伺服器 hello 和 hello 次要資料庫的定價層。</span><span class="sxs-lookup"><span data-stu-id="bcea9-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![設定次要資料庫](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="bcea9-123">（選擇性） 您可以新增次要資料庫的 tooan 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="bcea9-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="bcea9-124">toocreate hello 次要資料庫在資料庫中，按一下**彈性集區**選取 hello 目標伺服器上的集區。</span><span class="sxs-lookup"><span data-stu-id="bcea9-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="bcea9-125">集區必須已經存在 hello 目標伺服器上。</span><span class="sxs-lookup"><span data-stu-id="bcea9-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="bcea9-126">此工作流程不會建立集區。</span><span class="sxs-lookup"><span data-stu-id="bcea9-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="bcea9-127">按一下**建立**tooadd hello 次要。</span><span class="sxs-lookup"><span data-stu-id="bcea9-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="bcea9-128">hello 次要資料庫會建立而且 hello 植入處理程序開始。</span><span class="sxs-lookup"><span data-stu-id="bcea9-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![設定次要資料庫](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="bcea9-130">Hello 植入處理程序完成時，hello 次要資料庫就會顯示其狀態。</span><span class="sxs-lookup"><span data-stu-id="bcea9-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![植入完成](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="bcea9-132">起始容錯移轉</span><span class="sxs-lookup"><span data-stu-id="bcea9-132">Initiate a failover</span></span>

<span data-ttu-id="bcea9-133">hello 次要資料庫可以是主要的交換的 toobecome hello。</span><span class="sxs-lookup"><span data-stu-id="bcea9-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="bcea9-134">在 hello [Azure 入口網站](http://portal.azure.com)，瀏覽 toohello hello 地理複寫合作關係中的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="bcea9-135">在 hello SQL 資料庫刀鋒視窗中，選取 **所有設定** > **地理複寫**。</span><span class="sxs-lookup"><span data-stu-id="bcea9-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="bcea9-136">在 hello**次要**清單時，要產生 toobecome 選取 hello 資料庫 hello 新主要複本，然後按一下**容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="bcea9-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![容錯移轉](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="bcea9-138">按一下**是**toobegin hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="bcea9-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="bcea9-139">hello 命令立即會切換成主要角色的 hello hello 次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="bcea9-140">沒有在短期間這兩個資料庫是無法使用 （在 0 too25 秒 hello 順序） 而 hello 角色切換。</span><span class="sxs-lookup"><span data-stu-id="bcea9-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="bcea9-141">如果 hello 主要資料庫中有多個次要資料庫、 hello 命令自動檔重新設定 hello 其他次要 tooconnect toohello 新主要複本。</span><span class="sxs-lookup"><span data-stu-id="bcea9-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="bcea9-142">hello 整個作業花費時間小於一分鐘 toocomplete 在一般情況下。</span><span class="sxs-lookup"><span data-stu-id="bcea9-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="bcea9-143">此命令可供快速地復原 hello 資料庫發生中斷。</span><span class="sxs-lookup"><span data-stu-id="bcea9-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="bcea9-144">它會觸發容錯移轉但不進行資料同步 (強制性容錯移轉)。</span><span class="sxs-lookup"><span data-stu-id="bcea9-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="bcea9-145">如果主要 hello 在線上而且 hello 命令發出部分資料遺失時認可交易可能會發生。</span><span class="sxs-lookup"><span data-stu-id="bcea9-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="bcea9-146">移除次要資料庫</span><span class="sxs-lookup"><span data-stu-id="bcea9-146">Remove secondary database</span></span>
<span data-ttu-id="bcea9-147">這項作業永久終止 hello 複寫 toohello 次要資料庫，並變更 hello hello 次要 tooa 規則讀寫資料庫的角色。</span><span class="sxs-lookup"><span data-stu-id="bcea9-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="bcea9-148">如果 hello 連線 toohello 次要資料庫已損毀，hello 命令成功，但連線恢復後 hello 次要並不會變成讀寫之前。</span><span class="sxs-lookup"><span data-stu-id="bcea9-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="bcea9-149">在 hello [Azure 入口網站](http://portal.azure.com)，瀏覽 toohello hello 地理複寫合作關係中的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="bcea9-150">在 hello SQL 資料庫 頁面上，選取 **地理複寫**。</span><span class="sxs-lookup"><span data-stu-id="bcea9-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="bcea9-151">在 hello**次要**清單中，您想要從 hello 地理複寫合作關係 tooremove 選取 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="bcea9-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="bcea9-152">按一下 [ **停止複寫**]。</span><span class="sxs-lookup"><span data-stu-id="bcea9-152">Click **Stop Replication**.</span></span>
   
    ![移除次要](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="bcea9-154">隨即開啟確認視窗。</span><span class="sxs-lookup"><span data-stu-id="bcea9-154">A confirmation window opens.</span></span> <span data-ttu-id="bcea9-155">按一下**是**tooremove hello 資料庫從 hello 地理複寫合作關係。</span><span class="sxs-lookup"><span data-stu-id="bcea9-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="bcea9-156">（設定它 tooa 讀寫資料庫不屬於任何複寫的一部分）。</span><span class="sxs-lookup"><span data-stu-id="bcea9-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcea9-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcea9-157">Next steps</span></span>
* <span data-ttu-id="bcea9-158">toolearn 進一步了解作用中的地理複寫，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bcea9-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="bcea9-159">如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="bcea9-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

