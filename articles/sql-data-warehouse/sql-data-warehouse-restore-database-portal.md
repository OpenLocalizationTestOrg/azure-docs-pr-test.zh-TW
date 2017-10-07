---
title: "aaaRestore Azure SQL 資料倉儲 （Azure 入口網站） |Microsoft 文件"
description: "還原 Azure SQL 資料倉儲的 Azure 入口網站工作。"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="35594-103">還原 Azure SQL 資料倉儲 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="35594-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="35594-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="35594-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="35594-105">[入口網站][Portal]</span><span class="sxs-lookup"><span data-stu-id="35594-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="35594-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="35594-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="35594-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="35594-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="35594-108">在本文中，您將學習如何使用的 Azure SQL 資料倉儲 toorestore hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="35594-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="35594-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="35594-109">Before you begin</span></span>
<span data-ttu-id="35594-110">**請驗證您的 DTU 容量。**</span><span class="sxs-lookup"><span data-stu-id="35594-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="35594-111">SQL 資料倉儲的每個執行個體均由具有預設資料配額單位 (DTU) 的 SQL Database 裝載 (例如，myserver.database.windows.net)。</span><span class="sxs-lookup"><span data-stu-id="35594-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="35594-112">您可以還原 SQL 資料倉儲之前，請確認您的 SQL server 有足夠的剩餘 hello 資料庫的還原目的地的 DTU 配額。</span><span class="sxs-lookup"><span data-stu-id="35594-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="35594-113">toolearn 如何 toocalculate DTU 配額或 toorequest 更多 Dtu，請參閱[要求 DTU 配額變更][Request a DTU quota change]。</span><span class="sxs-lookup"><span data-stu-id="35594-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="35594-114">還原作用中或已暫停的資料庫</span><span class="sxs-lookup"><span data-stu-id="35594-114">Restore an active or paused database</span></span>
<span data-ttu-id="35594-115">toorestore 資料庫：</span><span class="sxs-lookup"><span data-stu-id="35594-115">toorestore a database:</span></span>

1. <span data-ttu-id="35594-116">登入 toohello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="35594-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="35594-117">Hello 左窗格中，選取**瀏覽**，然後選取**SQL 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="35594-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![選取 [瀏覽] > [SQL Server]](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="35594-119">尋找您的伺服器，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="35594-119">Find your server, and then select it.</span></span>

    ![選取您的伺服器](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="35594-121">您想要從，toorestore，，然後選取它，請尋找 hello SQL 資料倉儲執行個體。</span><span class="sxs-lookup"><span data-stu-id="35594-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![選取 SQL 資料倉儲 toorestore hello 執行個體](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="35594-123">在 [hello hello 資料倉儲] 刀鋒視窗頂端，選取**還原**。</span><span class="sxs-lookup"><span data-stu-id="35594-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![選取 [還原]](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="35594-125">指定新的 **資料庫名稱**。</span><span class="sxs-lookup"><span data-stu-id="35594-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="35594-126">最新的選取 hello**還原點**。</span><span class="sxs-lookup"><span data-stu-id="35594-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="35594-127">請確定您選擇 hello 最新的還原點。</span><span class="sxs-lookup"><span data-stu-id="35594-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="35594-128">以國際標準時間 (UTC) 顯示還原點，因為 hello 預設選項，可能無法 hello 最新的還原點。</span><span class="sxs-lookup"><span data-stu-id="35594-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![選取還原點](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="35594-130">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="35594-130">Select **OK**.</span></span>
9. <span data-ttu-id="35594-131">hello 資料庫還原程序會開始，而且您可以使用**通知**toomonitor hello 程序。</span><span class="sxs-lookup"><span data-stu-id="35594-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="35594-132">Hello 還原完成後，您可以依照下列設定復原的資料庫[設定您的資料庫復原後][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="35594-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="35594-133">還原已刪除的資料庫</span><span class="sxs-lookup"><span data-stu-id="35594-133">Restore a deleted database</span></span>
<span data-ttu-id="35594-134">toorestore 已刪除的資料庫：</span><span class="sxs-lookup"><span data-stu-id="35594-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="35594-135">登入 toohello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="35594-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="35594-136">Hello 左窗格中，選取**瀏覽**，然後選取**SQL 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="35594-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![選取 [瀏覽] > [SQL Server]](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="35594-138">尋找您的伺服器，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="35594-138">Find your server, and then select it.</span></span>

    ![選取您的伺服器](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="35594-140">捲動 toohello**作業**> 一節，在您的伺服器 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="35594-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="35594-141">選取 hello**已刪除資料庫**磚。</span><span class="sxs-lookup"><span data-stu-id="35594-141">Select hello **Deleted databases** tile.</span></span>

    ![選取 hello 已刪除資料庫並排顯示](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="35594-143">選取您想 toorestore hello 刪除資料庫。</span><span class="sxs-lookup"><span data-stu-id="35594-143">Select hello deleted database that you want toorestore.</span></span>

    ![選取資料庫 toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="35594-145">指定新的 **資料庫名稱**。</span><span class="sxs-lookup"><span data-stu-id="35594-145">Specify a new **Database name**.</span></span>

    ![新增 hello 資料庫的名稱](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="35594-147">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="35594-147">Select **OK**.</span></span>
9. <span data-ttu-id="35594-148">hello 資料庫還原程序會開始，而且您可以使用**通知**toomonitor hello 程序。</span><span class="sxs-lookup"><span data-stu-id="35594-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="35594-149">tooconfigure 資料庫 hello 還原完成之後，請參閱[設定您的資料庫復原後][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="35594-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="35594-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35594-150">Next steps</span></span>
<span data-ttu-id="35594-151">關於 hello 業務續航力功能的 Azure SQL Database 版本中，讀取 hello toolearn [Azure SQL Database 業務持續性概觀][Azure SQL Database business continuity overview]。</span><span class="sxs-lookup"><span data-stu-id="35594-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
