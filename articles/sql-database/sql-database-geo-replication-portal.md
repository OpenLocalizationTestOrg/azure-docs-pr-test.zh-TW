---
title: "Azure 入口網站︰SQL Database 異地複寫 | Microsoft Docs"
description: "在 Azure 入口網站中為 Azure SQL Database 設定異地複寫，並起始容錯移轉"
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
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="d940c-103">在 Azure 入口網站中為 Azure SQL Database 設定主動式異地複寫，並起始容錯移轉</span><span class="sxs-lookup"><span data-stu-id="d940c-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="d940c-104">本文說明如何在 [Azure 入口網站](http://portal.azure.com)中為 SQL Database 設定主動式異地複寫，並起始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d940c-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="d940c-105">若要使用 Azure 入口網站起始容錯移轉，請參閱 [使用 Azure 入口網站為 Azure SQL Database 起始計劃性或非計劃性容錯移轉](sql-database-geo-replication-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d940c-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="d940c-106">若要使用 Azure 入口網站來設定作用中異地複寫，您需要下列資源：</span><span class="sxs-lookup"><span data-stu-id="d940c-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="d940c-107">Azure SQL Database：您想要複寫到不同地理區域的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="d940c-108">主動式異地複寫必須是在相同訂用帳戶內的資料庫之間進行。</span><span class="sxs-lookup"><span data-stu-id="d940c-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="d940c-109">新增次要資料庫</span><span class="sxs-lookup"><span data-stu-id="d940c-109">Add a secondary database</span></span>
<span data-ttu-id="d940c-110">下列步驟會在異地複寫合作關係中建立新的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="d940c-111">若要新增次要資料庫，您必須是訂用帳戶擁有者或共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="d940c-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="d940c-112">次要資料庫的名稱會與主要資料庫相同，並且預設會具有相同的服務層級。</span><span class="sxs-lookup"><span data-stu-id="d940c-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="d940c-113">次要資料庫可以是單一資料庫或彈性集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="d940c-114">如需詳細資訊，請參閱 [服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="d940c-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="d940c-115">建立並植入次要複本之後，就會開始從主要資料庫將資料複寫到新的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="d940c-116">如果夥伴資料庫已經存在 (例如，因終止先前的「異地複寫」關聯性所導致)，命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="d940c-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="d940c-117">在 [Azure 入口網站](http://portal.azure.com)中，瀏覽至您想要為「異地複寫」設定的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="d940c-118">在 SQL Database 頁面上，選取 [異地複寫]，然後選取要建立次要資料庫的區域。</span><span class="sxs-lookup"><span data-stu-id="d940c-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="d940c-119">您可以選取裝載主要資料庫之區域以外的任何區域，但我們建議您選取[配對區域](../best-practices-availability-paired-regions.md)。</span><span class="sxs-lookup"><span data-stu-id="d940c-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![設定異地複寫](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="d940c-121">選取或設定伺服器及次要資料庫的定價層。</span><span class="sxs-lookup"><span data-stu-id="d940c-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![設定次要資料庫](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="d940c-123">(選擇性) 您可以將次要資料庫新增至彈性集區。</span><span class="sxs-lookup"><span data-stu-id="d940c-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="d940c-124">若要在集區中建立次要資料庫，請按一下 [彈性集區]，然後選取目標伺服器上的集區。</span><span class="sxs-lookup"><span data-stu-id="d940c-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="d940c-125">集區必須已存在目標伺服器上。</span><span class="sxs-lookup"><span data-stu-id="d940c-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="d940c-126">此工作流程不會建立集區。</span><span class="sxs-lookup"><span data-stu-id="d940c-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="d940c-127">按一下 [建立]  以加入次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="d940c-128">將會建立次要資料庫並開始植入程序。</span><span class="sxs-lookup"><span data-stu-id="d940c-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![設定次要資料庫](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="d940c-130">當植入程序完成時，次要資料庫會顯示其狀態。</span><span class="sxs-lookup"><span data-stu-id="d940c-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![植入完成](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="d940c-132">起始容錯移轉</span><span class="sxs-lookup"><span data-stu-id="d940c-132">Initiate a failover</span></span>

<span data-ttu-id="d940c-133">次要資料庫可被切換成為主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="d940c-134">在 [Azure 入口網站](http://portal.azure.com) 中，瀏覽至「異地複寫」合作關係中的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="d940c-135">在 [SQL Database] 刀鋒視窗上，選取 [所有設定] > [異地複寫]。</span><span class="sxs-lookup"><span data-stu-id="d940c-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="d940c-136">在 [次要] 清單中，選取要做為新主要資料庫的資料庫，然後按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="d940c-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![容錯移轉](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="d940c-138">按一下 [是]  即可開始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d940c-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="d940c-139">命令會立即將次要資料庫切換為主要角色。</span><span class="sxs-lookup"><span data-stu-id="d940c-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="d940c-140">切換角色時，會有一小段時間無法使用這兩個資料庫 (大約為 0 到 25 秒)。</span><span class="sxs-lookup"><span data-stu-id="d940c-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="d940c-141">如果主要資料庫有多個次要資料庫，此命令會自動重新設定其他次要複本以連接至新的主要複本。</span><span class="sxs-lookup"><span data-stu-id="d940c-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="d940c-142">在正常情況下，完成整個作業所需的時間應該少於一分鐘。</span><span class="sxs-lookup"><span data-stu-id="d940c-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="d940c-143">此命令的設計目的是要快速復原發生中斷的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="d940c-144">它會觸發容錯移轉但不進行資料同步 (強制性容錯移轉)。</span><span class="sxs-lookup"><span data-stu-id="d940c-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="d940c-145">發出命令時，如果主要複本處於線上並且正在認可交易，可能會發生部分資料遺失。</span><span class="sxs-lookup"><span data-stu-id="d940c-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="d940c-146">移除次要資料庫</span><span class="sxs-lookup"><span data-stu-id="d940c-146">Remove secondary database</span></span>
<span data-ttu-id="d940c-147">此作業會永久終止對次要資料庫的複寫，並將次要資料庫的角色變更為一般讀寫資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="d940c-148">如果與次要資料庫的連線中斷，命令將會成功，但次要資料庫必須等到連線恢復後才會變成讀寫資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="d940c-149">在 [Azure 入口網站](http://portal.azure.com) 中，瀏覽至「異地複寫」合作關係中的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="d940c-150">在 SQL Database 頁面上，選取 [異地複寫]。</span><span class="sxs-lookup"><span data-stu-id="d940c-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="d940c-151">在 [次要] 清單中，選取您想要從「異地複寫」合作關係中移除的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="d940c-152">按一下 [ **停止複寫**]。</span><span class="sxs-lookup"><span data-stu-id="d940c-152">Click **Stop Replication**.</span></span>
   
    ![移除次要](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="d940c-154">隨即開啟確認視窗。</span><span class="sxs-lookup"><span data-stu-id="d940c-154">A confirmation window opens.</span></span> <span data-ttu-id="d940c-155">按一下 [是] 以從異地複寫合作關係中移除資料庫。</span><span class="sxs-lookup"><span data-stu-id="d940c-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="d940c-156">(將它設定為讀寫資料庫不屬於任何複寫的一部分。)</span><span class="sxs-lookup"><span data-stu-id="d940c-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d940c-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d940c-157">Next steps</span></span>
* <span data-ttu-id="d940c-158">若要深入了解作用中異地複寫，請參閱[作用中異地複寫](sql-database-geo-replication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d940c-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="d940c-159">如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)。</span><span class="sxs-lookup"><span data-stu-id="d940c-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

