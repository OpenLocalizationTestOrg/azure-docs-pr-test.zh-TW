---
title: "還原 Azure SQL 資料倉儲 (Azure 入口網站) | Microsoft Docs"
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
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="eee1a-103">還原 Azure SQL 資料倉儲 (入口網站)</span><span class="sxs-lookup"><span data-stu-id="eee1a-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="eee1a-104">[概觀][Overview]</span><span class="sxs-lookup"><span data-stu-id="eee1a-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="eee1a-105">[入口網站][Portal]</span><span class="sxs-lookup"><span data-stu-id="eee1a-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="eee1a-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="eee1a-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="eee1a-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="eee1a-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="eee1a-108">在本文中，您將了解如何使用 Azure 入口網站來還原 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="eee1a-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eee1a-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="eee1a-109">Before you begin</span></span>
<span data-ttu-id="eee1a-110">**請驗證您的 DTU 容量。**</span><span class="sxs-lookup"><span data-stu-id="eee1a-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="eee1a-111">SQL 資料倉儲的每個執行個體均由具有預設資料配額單位 (DTU) 的 SQL Database 裝載 (例如，myserver.database.windows.net)。</span><span class="sxs-lookup"><span data-stu-id="eee1a-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="eee1a-112">在您還原 SQL 資料倉儲之前，請確認您的 SQL 伺服器有足夠的剩餘 DTU 配額可供要還原的資料庫使用。</span><span class="sxs-lookup"><span data-stu-id="eee1a-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="eee1a-113">若要了解如何計算所需 DTU 配額或要求更多 DTU，請參閱 [要求 DTU 配額變更][Request a DTU quota change]。</span><span class="sxs-lookup"><span data-stu-id="eee1a-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="eee1a-114">還原作用中或已暫停的資料庫</span><span class="sxs-lookup"><span data-stu-id="eee1a-114">Restore an active or paused database</span></span>
<span data-ttu-id="eee1a-115">還原資料庫：</span><span class="sxs-lookup"><span data-stu-id="eee1a-115">To restore a database:</span></span>

1. <span data-ttu-id="eee1a-116">登入 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="eee1a-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="eee1a-117">在左窗格中，選取 [瀏覽]，然後選取 [SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="eee1a-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![選取 [瀏覽] > [SQL Server]](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="eee1a-119">尋找您的伺服器，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="eee1a-119">Find your server, and then select it.</span></span>

    ![選取您的伺服器](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="eee1a-121">尋找您想要還原的 SQL 資料倉儲的執行個體，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="eee1a-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![選取要還原的 SQL 資料倉儲的執行個體](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="eee1a-123">在 [資料倉儲] 刀鋒視窗頂端，選取 [還原]。</span><span class="sxs-lookup"><span data-stu-id="eee1a-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![選取 [還原]](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="eee1a-125">指定新的 **資料庫名稱**。</span><span class="sxs-lookup"><span data-stu-id="eee1a-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="eee1a-126">選取最新的 **還原點**。</span><span class="sxs-lookup"><span data-stu-id="eee1a-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="eee1a-127">確定您選擇了最新的還原點。</span><span class="sxs-lookup"><span data-stu-id="eee1a-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="eee1a-128">還原點會以國際標準時間 (UTC) 顯示，因此預設選項可能不是最新的還原點。</span><span class="sxs-lookup"><span data-stu-id="eee1a-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![選取還原點](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="eee1a-130">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eee1a-130">Select **OK**.</span></span>
9. <span data-ttu-id="eee1a-131">資料庫還原程序將會開始，您可以使用 [通知] 來監視此程序。</span><span class="sxs-lookup"><span data-stu-id="eee1a-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="eee1a-132">還原完成後，您可以遵循 [在復原之後設定資料庫][Configure your database after recovery]來設定復原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="eee1a-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="eee1a-133">還原已刪除的資料庫</span><span class="sxs-lookup"><span data-stu-id="eee1a-133">Restore a deleted database</span></span>
<span data-ttu-id="eee1a-134">還原已刪除的資料庫：</span><span class="sxs-lookup"><span data-stu-id="eee1a-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="eee1a-135">登入 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="eee1a-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="eee1a-136">在左窗格中，選取 [瀏覽]，然後選取 [SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="eee1a-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![選取 [瀏覽] > [SQL Server]](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="eee1a-138">尋找您的伺服器，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="eee1a-138">Find your server, and then select it.</span></span>

    ![選取您的伺服器](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="eee1a-140">在伺服器的刀鋒視窗上捲動至 [作業] 區段。</span><span class="sxs-lookup"><span data-stu-id="eee1a-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="eee1a-141">選取 [已刪除的資料庫] 圖格。</span><span class="sxs-lookup"><span data-stu-id="eee1a-141">Select the **Deleted databases** tile.</span></span>

    ![選取 [已刪除的資料庫] 圖格](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="eee1a-143">選取您想要還原的已刪除資料庫。</span><span class="sxs-lookup"><span data-stu-id="eee1a-143">Select the deleted database that you want to restore.</span></span>

    ![選取要還原的資料庫](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="eee1a-145">指定新的 **資料庫名稱**。</span><span class="sxs-lookup"><span data-stu-id="eee1a-145">Specify a new **Database name**.</span></span>

    ![新增資料庫的名稱](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="eee1a-147">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eee1a-147">Select **OK**.</span></span>
9. <span data-ttu-id="eee1a-148">資料庫還原程序將會開始，您可以使用 [通知] 來監視此程序。</span><span class="sxs-lookup"><span data-stu-id="eee1a-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="eee1a-149">若要在還原完成之後設定資料庫，請參閱 [在復原之後設定資料庫][Configure your database after recovery]。</span><span class="sxs-lookup"><span data-stu-id="eee1a-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="eee1a-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eee1a-150">Next steps</span></span>
<span data-ttu-id="eee1a-151">若要深入了解 Azure SQL Database 版本的商務持續性功能，請閱讀 [Azure SQL Database 商務持續性概觀][Azure SQL Database business continuity overview]。</span><span class="sxs-lookup"><span data-stu-id="eee1a-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
