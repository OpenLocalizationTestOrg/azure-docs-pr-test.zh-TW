---
title: "從 Azure SQL Database 備份還原單一資料表 | Microsoft Docs"
description: "了解如何從 Azure SQL Database 備份還原單一資料表。"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 8c750c503d10ea63b9665958b96db2dfea3d9a3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-restore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="a699e-103">如何從 Azure SQL Database 備份還原單一資料表</span><span class="sxs-lookup"><span data-stu-id="a699e-103">How to restore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="a699e-104">您可能不小心修改了 SQL 資料庫中的某些資料，而想要還原受影響的單一資料表。</span><span class="sxs-lookup"><span data-stu-id="a699e-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want to recover the single affected table.</span></span> <span data-ttu-id="a699e-105">本文說明如何從其中一個 SQL Database [自動備份](sql-database-automated-backups.md)還原資料庫中的單一資料表。</span><span class="sxs-lookup"><span data-stu-id="a699e-105">This article describes how to restore a single table in a database from one of the SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-the-table-and-restore-a-copy-of-the-database"></a><span data-ttu-id="a699e-106">準備步驟︰重新命名資料表，並還原資料庫的複本</span><span class="sxs-lookup"><span data-stu-id="a699e-106">Preparation steps: Rename the table and restore a copy of the database</span></span>
1. <span data-ttu-id="a699e-107">識別出 Azure SQL Database 中您想要以還原複本取代的資料表。</span><span class="sxs-lookup"><span data-stu-id="a699e-107">Identify the table in your Azure SQL database that you want to replace with the restored copy.</span></span> <span data-ttu-id="a699e-108">使用 Microsoft SQL Management Studio 來重新命名資料表。</span><span class="sxs-lookup"><span data-stu-id="a699e-108">Use Microsoft SQL Management Studio to rename the table.</span></span> <span data-ttu-id="a699e-109">例如，將資料表重新命名為 &lt;資料表名稱&gt;_old。</span><span class="sxs-lookup"><span data-stu-id="a699e-109">For example, rename the table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a699e-110">為了避免被阻斷，請確定您要重新命名的資料表上沒有正在執行的活動。</span><span class="sxs-lookup"><span data-stu-id="a699e-110">To avoid being blocked, make sure that there's no activity running on the table that you are renaming.</span></span> <span data-ttu-id="a699e-111">如果您遇到問題，則請確定在維護期間執行此程序。</span><span class="sxs-lookup"><span data-stu-id="a699e-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="a699e-112">使用[還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)步驟，將資料庫備份還原至您想要復原的時間點。</span><span class="sxs-lookup"><span data-stu-id="a699e-112">Restore a backup of your database to a point in time that you want to recover to using the [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a699e-113">還原之資料庫的名稱會是「資料庫名稱+時間戳記」的格式；例如，**Adventureworks2012_2016-01-01T22-12Z**。</span><span class="sxs-lookup"><span data-stu-id="a699e-113">The name of the restored database will be in the DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="a699e-114">此步驟不會覆寫伺服器上現有的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="a699e-114">This step doesn't overwrite the existing database name on the server.</span></span> <span data-ttu-id="a699e-115">這是一項安全措施，其目的是要讓您在卸除目前的資料庫並重新命名還原的資料庫以供生產環境使用之前，先確認還原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a699e-115">This is a safety measure, and it's intended to allow you to verify the restored database before they drop their current database and rename the restored database for production use.</span></span>
   
## <a name="copying-the-table-from-the-restored-database-by-using-the-sql-database-migration-tool"></a><span data-ttu-id="a699e-116">使用 SQL Database 移轉工具，從還原的資料庫複製資料表</span><span class="sxs-lookup"><span data-stu-id="a699e-116">Copying the table from the restored database by using the SQL Database Migration tool</span></span>

1. <span data-ttu-id="a699e-117">下載並安裝 [SQL Database 移轉精靈](https://sqlazuremw.codeplex.com)。</span><span class="sxs-lookup"><span data-stu-id="a699e-117">Download and install the [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="a699e-118">開啟 SQL Database 移轉精靈，並在 [選取程序] 頁面，選取 [分析/移轉] 底下的 [資料庫]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a699e-118">Open the SQL Database Migration Wizard, on the **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL Database 移轉精靈 - 選取程序](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="a699e-120">在 [連接至伺服器]  對話方塊中，套用下列設定：</span><span class="sxs-lookup"><span data-stu-id="a699e-120">In the **Connect to Server** dialog box, apply the following settings:</span></span>

   * <span data-ttu-id="a699e-121">伺服器名稱︰**您的 SQL 伺服器**</span><span class="sxs-lookup"><span data-stu-id="a699e-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="a699e-122">驗證：**SQL Server 驗證**</span><span class="sxs-lookup"><span data-stu-id="a699e-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="a699e-123">登入︰**您的登入**</span><span class="sxs-lookup"><span data-stu-id="a699e-123">Login: **Your login**</span></span>
   * <span data-ttu-id="a699e-124">密碼︰**您的密碼**</span><span class="sxs-lookup"><span data-stu-id="a699e-124">Password: **Your password**</span></span>
   * <span data-ttu-id="a699e-125">資料庫：**Master DB (列出所有資料庫)**</span><span class="sxs-lookup"><span data-stu-id="a699e-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a699e-126">根據預設，精靈會儲存您的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="a699e-126">By default the wizard saves your login information.</span></span> <span data-ttu-id="a699e-127">如果您不希望它儲存，請選取 [忘記登入資訊] 。</span><span class="sxs-lookup"><span data-stu-id="a699e-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL Database 移轉精靈 - 選取來源 - 步驟 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="a699e-129">在 [選取來源] 對話方塊中，從 [準備步驟] 區段選取還原之資料庫的名稱以做為來源，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a699e-129">In the **Select Source** dialog box, select the restored database name from the **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL Database 移轉精靈 - 選取來源 - 步驟 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="a699e-131">在 [選擇物件] 對話方塊中，選取 [選取特定的資料庫物件] 選項，然後選取您要移轉到目標伺服器的資料表 (可選取多個)。</span><span class="sxs-lookup"><span data-stu-id="a699e-131">In the **Choose Objects** dialog box, select the **Select specific database objects** option, and then select the table(or tables) that you want to migrate to the target server.</span></span>
   <span data-ttu-id="a699e-132">![SQL Database 移轉精靈 - 選取物件](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="a699e-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="a699e-133">在 [指令碼精靈摘要] 頁面中，當系統提示您是否準備好要產生 SQL 指令碼時，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="a699e-133">On the **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready to generate a SQL script.</span></span> <span data-ttu-id="a699e-134">也有可儲存 TSQL 指令碼的選項以供您稍後使用。</span><span class="sxs-lookup"><span data-stu-id="a699e-134">You also have the option to save the TSQL Script for later use.</span></span>
   <span data-ttu-id="a699e-135">![SQL Database 移轉精靈 - 指令碼精靈摘要](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="a699e-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="a699e-136">在 [結果摘要] 頁面中，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a699e-136">On the **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="a699e-137">![SQL Database 移轉精靈 - 結果摘要](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="a699e-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="a699e-138">在 [設定目標伺服器的連線] 頁面中，按一下 [連接至伺服器]，然後輸入詳細資訊如下：</span><span class="sxs-lookup"><span data-stu-id="a699e-138">On the **Setup Target Server Connection** page, click **Connect to Server**, and then enter the details as follows:</span></span>
   
   * <span data-ttu-id="a699e-139">**伺服器名稱**：目標伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="a699e-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="a699e-140">**驗證**：**SQL Server 驗證**。</span><span class="sxs-lookup"><span data-stu-id="a699e-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="a699e-141">輸入您的登入認證。</span><span class="sxs-lookup"><span data-stu-id="a699e-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="a699e-142">**資料庫**：**Master DB (列出所有資料庫)**。</span><span class="sxs-lookup"><span data-stu-id="a699e-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="a699e-143">此選項會列出目標伺服器上的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="a699e-143">This option lists all the databases on the target server.</span></span>
     
     ![SQL Database 移轉精靈 - 設定目標伺服器的連線](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="a699e-145">按一下 [連接]，選取資料表要移動至的目標資料庫，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a699e-145">Click **Connect**, select the target database that you want to move the table to, and then click **Next**.</span></span> <span data-ttu-id="a699e-146">先前產生的指令碼應該會完成執行，且您應該會看到剛才移動的資料表已複製到目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="a699e-146">This should finish running the previously generated script, and you should see the newly moved table copied to the target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="a699e-147">驗證步驟</span><span class="sxs-lookup"><span data-stu-id="a699e-147">Verification step</span></span>

- <span data-ttu-id="a699e-148">查詢並測試剛才複製的資料表，以確認資料完整。</span><span class="sxs-lookup"><span data-stu-id="a699e-148">Query and test the newly copied table to make sure that the data is intact.</span></span> <span data-ttu-id="a699e-149">經過確認之後，您就可以從 [準備步驟]  區段卸除已重新命名的資料表。</span><span class="sxs-lookup"><span data-stu-id="a699e-149">Upon confirmation, you can drop the renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="a699e-150">(例如，&lt;資料表名稱&gt;_old)。</span><span class="sxs-lookup"><span data-stu-id="a699e-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a699e-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a699e-151">Next steps</span></span>
[<span data-ttu-id="a699e-152">SQL Database 自動備份</span><span class="sxs-lookup"><span data-stu-id="a699e-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

