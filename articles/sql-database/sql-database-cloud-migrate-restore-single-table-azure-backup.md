---
title: "aaaRestore 單一資料表，從 Azure SQL Database 備份 |Microsoft 文件"
description: "了解如何 toorestore 單一資料表中 Azure SQL Database 備份。"
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
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="ebb73-103">如何 toorestore 單一資料表中的 Azure SQL Database 備份</span><span class="sxs-lookup"><span data-stu-id="ebb73-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="ebb73-104">您可能會遇到的情況中，您偶爾修改 SQL database 中的部分資料，而您想 toorecover hello 單一受影響的資料表。</span><span class="sxs-lookup"><span data-stu-id="ebb73-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="ebb73-105">本文說明如何 toorestore 單一資料表中將資料庫從一個 hello SQL Database[自動備份](sql-database-automated-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="ebb73-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="ebb73-106">準備步驟： hello 資料表重新命名，並還原 hello 資料庫的複本</span><span class="sxs-lookup"><span data-stu-id="ebb73-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="ebb73-107">識別您想與 hello 還原複本 tooreplace 您 Azure SQL database 中的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="ebb73-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="ebb73-108">使用 Microsoft SQL Management Studio toorename hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="ebb73-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="ebb73-109">例如，資料表重新命名 hello 為&lt;資料表名稱&gt;_old。</span><span class="sxs-lookup"><span data-stu-id="ebb73-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ebb73-110">tooavoid 被封鎖，請確定您要重新命名的 hello 資料表上執行任何活動。</span><span class="sxs-lookup"><span data-stu-id="ebb73-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="ebb73-111">如果您遇到問題，則請確定在維護期間執行此程序。</span><span class="sxs-lookup"><span data-stu-id="ebb73-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="ebb73-112">還原備份的資料庫 tooa 點時間中您想 toorecover toousing hello[點 In_Time 還原](sql-database-recovery-using-backups.md#point-in-time-restore)步驟。</span><span class="sxs-lookup"><span data-stu-id="ebb73-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ebb73-113">hello 的 hello 還原資料庫的名稱將會是 hello DBName + 時間戳記格式。例如， **Adventureworks2012_2016 01-01T22 12Z**。</span><span class="sxs-lookup"><span data-stu-id="ebb73-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="ebb73-114">這個步驟不會覆寫在 hello 伺服器 hello 現有資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="ebb73-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="ebb73-115">這是安全性量值，而且它能 tooallow tooverify hello 還原資料庫後再進行卸除其目前的資料庫，並重新命名用於實際執行環境的 hello 還原資料庫。</span><span class="sxs-lookup"><span data-stu-id="ebb73-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="ebb73-116">Hello 複製 hello 資料表使用 hello SQL Database 移轉工具還原資料庫</span><span class="sxs-lookup"><span data-stu-id="ebb73-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="ebb73-117">下載並安裝 hello [SQL Database 移轉精靈](https://sqlazuremw.codeplex.com)。</span><span class="sxs-lookup"><span data-stu-id="ebb73-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="ebb73-118">開啟 hello SQL Database 移轉精靈，在 hello**選取處理序**頁面上，選取**分析/移轉資料庫**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ebb73-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL Database 移轉精靈 - 選取程序](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="ebb73-120">在 hello**連接 tooServer**對話方塊方塊中，套用下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="ebb73-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="ebb73-121">伺服器名稱︰**您的 SQL 伺服器**</span><span class="sxs-lookup"><span data-stu-id="ebb73-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="ebb73-122">驗證：**SQL Server 驗證**</span><span class="sxs-lookup"><span data-stu-id="ebb73-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="ebb73-123">登入︰**您的登入**</span><span class="sxs-lookup"><span data-stu-id="ebb73-123">Login: **Your login**</span></span>
   * <span data-ttu-id="ebb73-124">密碼︰**您的密碼**</span><span class="sxs-lookup"><span data-stu-id="ebb73-124">Password: **Your password**</span></span>
   * <span data-ttu-id="ebb73-125">資料庫：**Master DB (列出所有資料庫)**</span><span class="sxs-lookup"><span data-stu-id="ebb73-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ebb73-126">根據預設 hello 精靈 」 會儲存您的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="ebb73-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="ebb73-127">如果您不希望它儲存，請選取 [忘記登入資訊] 。</span><span class="sxs-lookup"><span data-stu-id="ebb73-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL Database 移轉精靈 - 選取來源 - 步驟 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="ebb73-129">在 hello**選取來源**對話方塊中，選取 hello 還原的資料庫名稱從 hello**準備步驟**做為來源，區段，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ebb73-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL Database 移轉精靈 - 選取來源 - 步驟 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="ebb73-131">在 hello**選擇物件**對話方塊中，選取 hello**選取特定資料庫物件**選項，然後再選取您想 toomigrate toohello 目標伺服器 hello table(or tables)。</span><span class="sxs-lookup"><span data-stu-id="ebb73-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="ebb73-132">![SQL Database 移轉精靈 - 選取物件](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="ebb73-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="ebb73-133">在 hello**指令碼精靈摘要**頁面上，按一下**是**當系統提示您輸入有關您是否已準備好 toogenerate SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="ebb73-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="ebb73-134">您也可以 hello 選項 toosave hello TSQL 指令碼供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="ebb73-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="ebb73-135">![SQL Database 移轉精靈 - 指令碼精靈摘要](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="ebb73-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="ebb73-136">在 hello**結果摘要**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ebb73-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="ebb73-137">![SQL Database 移轉精靈 - 結果摘要](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="ebb73-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="ebb73-138">在 hello**設定目標伺服器連線**頁面上，按一下**連接 tooServer**，然後輸入 hello 詳細資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ebb73-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="ebb73-139">**伺服器名稱**：目標伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="ebb73-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="ebb73-140">**驗證**：**SQL Server 驗證**。</span><span class="sxs-lookup"><span data-stu-id="ebb73-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="ebb73-141">輸入您的登入認證。</span><span class="sxs-lookup"><span data-stu-id="ebb73-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="ebb73-142">**資料庫**：**Master DB (列出所有資料庫)**。</span><span class="sxs-lookup"><span data-stu-id="ebb73-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="ebb73-143">此選項會列出所有 hello hello 目標伺服器上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ebb73-143">This option lists all hello databases on hello target server.</span></span>
     
     ![SQL Database 移轉精靈 - 設定目標伺服器的連線](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="ebb73-145">按一下**連接**，選取 hello 目標資料庫，您想要 toomove hello 資料表，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="ebb73-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="ebb73-146">這應該執行 hello 先前產生的指令碼，來完成，您應該會看見 hello 剛移動資料表複製的 toohello 目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="ebb73-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="ebb73-147">驗證步驟</span><span class="sxs-lookup"><span data-stu-id="ebb73-147">Verification step</span></span>

- <span data-ttu-id="ebb73-148">查詢並測試新複製的 hello 資料表 toomake 確認 hello 的資料保持不變。</span><span class="sxs-lookup"><span data-stu-id="ebb73-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="ebb73-149">根據確認，您可以卸除 hello 重新命名資料表表單**準備步驟**> 一節。</span><span class="sxs-lookup"><span data-stu-id="ebb73-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="ebb73-150">(例如，&lt;資料表名稱&gt;_old)。</span><span class="sxs-lookup"><span data-stu-id="ebb73-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebb73-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebb73-151">Next steps</span></span>
[<span data-ttu-id="ebb73-152">SQL Database 自動備份</span><span class="sxs-lookup"><span data-stu-id="ebb73-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

