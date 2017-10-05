---
title: "使用 Azure 備份伺服器進行 SQL Server 工作負載的 Azure 備份 | Microsoft Docs"
description: "使用 Azure 備份伺服器來備份 SQL Server 資料庫的簡介"
services: backup
documentationcenter: 
author: pvrk
manager: Shivamg
editor: 
ms.assetid: c8b1f7ec-26b1-4ef0-a3f2-91aec959daea
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 2af9ebaa8f52690ed63406cbd85b77544d2d900d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-sql-server-to-azure-with-azure-backup-server"></a><span data-ttu-id="6f12a-103">使用 Azure 備份伺服器將 SQL Server 備份至 Azure</span><span class="sxs-lookup"><span data-stu-id="6f12a-103">Back up SQL Server to Azure With Azure Backup Server</span></span>
<span data-ttu-id="6f12a-104">本文將引導您逐步完成使用 Microsoft Azure 備份伺服器 (MABS) 來備份 SQL Server 資料庫的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="6f12a-104">This article leads you through the configuration steps for backup of SQL Server databases using Microsoft Azure Backup Server (MABS).</span></span>

<span data-ttu-id="6f12a-105">將 SQL Server 資料庫備份至 Azure 及從 Azure 復原的管理作業包含三個步驟：</span><span class="sxs-lookup"><span data-stu-id="6f12a-105">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="6f12a-106">建立備份原則以在 Azure 保護 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f12a-106">Create a backup policy to protect SQL Server databases to Azure.</span></span>
2. <span data-ttu-id="6f12a-107">在 Azure 建立隨選備份複本。</span><span class="sxs-lookup"><span data-stu-id="6f12a-107">Create on-demand backup copies to Azure.</span></span>
3. <span data-ttu-id="6f12a-108">從 Azure 復原資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f12a-108">Recover the database from Azure.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6f12a-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="6f12a-109">Before you start</span></span>
<span data-ttu-id="6f12a-110">開始之前，請確定您已[安裝並備妥 Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="6f12a-110">Before you begin, ensure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="create-a-backup-policy-to-protect-sql-server-databases-to-azure"></a><span data-ttu-id="6f12a-111">建立備份原則以在 Azure 保護 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="6f12a-111">Create a backup policy to protect SQL Server databases to Azure</span></span>
1. <span data-ttu-id="6f12a-112">在 Azure 備份伺服器 UI 上，按一下 [保護] 工作區。</span><span class="sxs-lookup"><span data-stu-id="6f12a-112">On the Azure Backup Server UI, click the **Protection** workspace.</span></span>
2. <span data-ttu-id="6f12a-113">在工具功能區中，按一下 [新增]  以建立新的保護群組。</span><span class="sxs-lookup"><span data-stu-id="6f12a-113">On the tool ribbon, click **New** to create a new protection group.</span></span>

    ![建立保護群組](./media/backup-azure-backup-sql/protection-group.png)
3. <span data-ttu-id="6f12a-115">MABS 會顯示開始畫面，其中包含建立**保護群組**的指引。</span><span class="sxs-lookup"><span data-stu-id="6f12a-115">MABS shows the start screen with the guidance on creating a **Protection Group**.</span></span> <span data-ttu-id="6f12a-116">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-116">Click **Next**.</span></span>
4. <span data-ttu-id="6f12a-117">選取 [伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-117">Select **Servers**.</span></span>

    ![選取保護群組類型 - 伺服器](./media/backup-azure-backup-sql/pg-servers.png)
5. <span data-ttu-id="6f12a-119">展開要備份之資料庫所在的 SQL Server 電腦。</span><span class="sxs-lookup"><span data-stu-id="6f12a-119">Expand the SQL Server machine where the databases to be backed up are present.</span></span> <span data-ttu-id="6f12a-120">MABS 會顯示可從該伺服器備份的各種資料來源。</span><span class="sxs-lookup"><span data-stu-id="6f12a-120">MABS shows various data sources that can be backed up from that server.</span></span> <span data-ttu-id="6f12a-121">展開 [所有 SQL 共用]  並選取要備份的資料庫 (在本例中我們選取 ReportServer$MSDPM2012 和 ReportServer$MSDPM2012TempDB)。</span><span class="sxs-lookup"><span data-stu-id="6f12a-121">Expand the **All SQL Shares** and select the databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) to be backed up.</span></span> <span data-ttu-id="6f12a-122">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-122">Click **Next**.</span></span>

    ![選取 SQL DB](./media/backup-azure-backup-sql/pg-databases.png)
6. <span data-ttu-id="6f12a-124">提供保護群組的名稱，然後選取 [我想要線上保護]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6f12a-124">Provide a name for the protection group and select the **I want online Protection** checkbox.</span></span>

    ![資料保護方式 - 短期磁碟和線上 Azure](./media/backup-azure-backup-sql/pg-name.png)
7. <span data-ttu-id="6f12a-126">在 [指定短期目標]  畫面中，包含建立磁碟備份點所需的輸入。</span><span class="sxs-lookup"><span data-stu-id="6f12a-126">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk.</span></span>

    <span data-ttu-id="6f12a-127">我們在此看到 [保留範圍] 設定為 [5 天]，[同步處理頻率] 設定為每隔 [15 分鐘]，這就是執行備份的頻率。</span><span class="sxs-lookup"><span data-stu-id="6f12a-127">Here we see that **Retention range** is set to *5 days*, **Synchronization frequency** is set to once every *15 minutes* which is the frequency at which backup is taken.</span></span> <span data-ttu-id="6f12a-128">[快速完整備份] 設定為 [下午 8:00]。</span><span class="sxs-lookup"><span data-stu-id="6f12a-128">**Express Full Backup** is set to *8:00 P.M*.</span></span>

    ![短期目標](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="6f12a-130">傳輸從前一天下午 8:00 備份點後修改的資料，即可在每天下午 8:00 PM (根據畫面輸入) 建立備份點。</span><span class="sxs-lookup"><span data-stu-id="6f12a-130">At 8:00 PM (according to the screen input) a backup point is created every day by transferring the data that has been modified from the previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="6f12a-131">這個程序稱為 [快速完整備份] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-131">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="6f12a-132">雖然交易記錄檔每隔 15 分鐘同步處理一次，但如果有需要在下午 9:00 復原資料庫，則此點可藉由重新執行最後一個快速完整備份點 (在本例中為下午 8:00) 的記錄檔來建立。</span><span class="sxs-lookup"><span data-stu-id="6f12a-132">While the transaction logs are synchronized every 15 minutes, if there is a need to recover the database at 9:00 PM – then the point is created by replaying the logs from the last express full backup point (8pm in this case).</span></span>
   >
   >

8. <span data-ttu-id="6f12a-133">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="6f12a-133">Click **Next**</span></span>

    <span data-ttu-id="6f12a-134">MABS 會顯示可用的整體儲存空間和潛在的磁碟空間使用量。</span><span class="sxs-lookup"><span data-stu-id="6f12a-134">MABS shows the overall storage space available and the potential disk space utilization.</span></span>

    ![磁碟配置](./media/backup-azure-backup-sql/pg-storage.png)

    <span data-ttu-id="6f12a-136">依預設，MABS 會為每個資料來源 (SQL Server 資料庫) 建立一個磁碟區，以供初始備份複本之用。</span><span class="sxs-lookup"><span data-stu-id="6f12a-136">By default, MABS creates one volume per data source (SQL Server database) which is used for the initial backup copy.</span></span> <span data-ttu-id="6f12a-137">透過這個方法，邏輯磁碟管理員 (LDM) 會將 MABS 保護限制為 300 個資料來源 (SQL Server 資料庫)。</span><span class="sxs-lookup"><span data-stu-id="6f12a-137">Using this approach, the Logical Disk Manager (LDM) limits MABS protection to 300 data sources (SQL Server databases).</span></span> <span data-ttu-id="6f12a-138">若要因應這項限制，請選取 [將資料共置在 DPM 存放集區中] 選項。</span><span class="sxs-lookup"><span data-stu-id="6f12a-138">To work around this limitation, select the **Co-locate data in DPM Storage Pool**, option.</span></span> <span data-ttu-id="6f12a-139">如果您使用這個選項，MABS 會使用單一磁碟區來存放多個資料來源，讓 MABS 得以保護多達 2000 個 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f12a-139">If you use this option, MABS uses a single volume for multiple data sources, which allows MABS to protect up to 2000 SQL databases.</span></span>

    <span data-ttu-id="6f12a-140">如果選取 [自動擴大磁碟區] 選項，MABS 將負責隨著生產資料成長而增加備份磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6f12a-140">If **Automatically grow the volumes** option is selected, MABS can account for the increased backup volume as the production data grows.</span></span> <span data-ttu-id="6f12a-141">如果未選取 [自動擴大磁碟區]，MABS 會限制用於保護群組中資料來源的備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="6f12a-141">If **Automatically grow the volumes** option is not selected, MABS limits the backup storage used to the data sources in the protection group.</span></span>
9. <span data-ttu-id="6f12a-142">系統管理員可選擇手動 (關閉網路) 傳輸此初始備份，以避免頻寬壅塞或透過網路。</span><span class="sxs-lookup"><span data-stu-id="6f12a-142">Administrators are given the choice of transferring this initial backup manually (off network) to avoid bandwidth congestion or over the network.</span></span> <span data-ttu-id="6f12a-143">他們也可以設定可發生初始傳輸的時間。</span><span class="sxs-lookup"><span data-stu-id="6f12a-143">They can also configure the time at which the initial transfer can happen.</span></span> <span data-ttu-id="6f12a-144">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-144">Click **Next**.</span></span>

    ![初始複寫方法](./media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="6f12a-146">初始備份複本要求將整個資料來源 (SQL Server 資料庫) 從生產伺服器 (SQL Server 機器) 傳輸到 MABS。</span><span class="sxs-lookup"><span data-stu-id="6f12a-146">The initial backup copy requires transfer of the entire data source (SQL Server database) from production server (SQL Server machine) to MABS.</span></span> <span data-ttu-id="6f12a-147">這些資料可能會很大，因此透過網路傳輸資料可能會超出頻寬。</span><span class="sxs-lookup"><span data-stu-id="6f12a-147">This data might be large, and transferring the data over the network could exceed bandwidth.</span></span> <span data-ttu-id="6f12a-148">基於這個理由，系統管理員可以選擇傳送初始備份的方式︰**手動** (使用卸除式媒體，可避免頻寬壅塞) 或**自動透過網路** (在指定時間)。</span><span class="sxs-lookup"><span data-stu-id="6f12a-148">For this reason, administrators can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span></span>

    <span data-ttu-id="6f12a-149">一旦完成初始備份，其餘的備份會是初始備份複本的增量備份。</span><span class="sxs-lookup"><span data-stu-id="6f12a-149">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span></span> <span data-ttu-id="6f12a-150">增量備份通常都非常小，因此有利於透過網路傳輸。</span><span class="sxs-lookup"><span data-stu-id="6f12a-150">Incremental backups tend to be small and are easily transferred across the network.</span></span>
10. <span data-ttu-id="6f12a-151">選擇是否想要執行一致性檢查，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-151">Choose when you want the consistency check to run and click **Next**.</span></span>

    ![一致性檢查](./media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="6f12a-153">MABS 可以執行一致性檢查來檢查備份點的完整性。</span><span class="sxs-lookup"><span data-stu-id="6f12a-153">MABS can perform a consistency check to check the integrity of the backup point.</span></span> <span data-ttu-id="6f12a-154">它會計算生產伺服器 (在此案例中為 SQL Server 機器) 上備份檔案的總和檢查碼以及 MABS 上該檔案的已備份資料。</span><span class="sxs-lookup"><span data-stu-id="6f12a-154">It calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file at MABS.</span></span> <span data-ttu-id="6f12a-155">在衝突的情況下，假設 MABS 上的備份檔案已損毀。</span><span class="sxs-lookup"><span data-stu-id="6f12a-155">In the case of a conflict, it is assumed that the backed-up file at MABS is corrupt.</span></span> <span data-ttu-id="6f12a-156">MABS 藉由傳送對應至總和檢查碼不符的區塊，改正已備份的資料。</span><span class="sxs-lookup"><span data-stu-id="6f12a-156">MABS rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span></span> <span data-ttu-id="6f12a-157">由於一致性檢查是效能密集作業，所以系統管理員可選擇排程一致性檢查或自動執行此作業。</span><span class="sxs-lookup"><span data-stu-id="6f12a-157">As the consistency check is a performance-intensive operation, administrators have the option of scheduling the consistency check or running it automatically.</span></span>
11. <span data-ttu-id="6f12a-158">若要指定資料來源的線上保護，請選取要送至 Azure 保護的資料庫，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-158">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span></span>

    ![選取資料來源](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. <span data-ttu-id="6f12a-160">系統管理員可以選擇備份排程以及符合其組織原則的保留原則。</span><span class="sxs-lookup"><span data-stu-id="6f12a-160">Administrators can choose backup schedules and retention policies that suit their organization policies.</span></span>

    ![排程和保留](./media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="6f12a-162">在此範例中，每天下午 12:00 和下午 8:00 會進行一次備份 (螢幕的下半部)</span><span class="sxs-lookup"><span data-stu-id="6f12a-162">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="6f12a-163">建議您在磁碟上保留幾個短期復原點，以便快速復原。</span><span class="sxs-lookup"><span data-stu-id="6f12a-163">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="6f12a-164">這些復原點可用於「操作復原」。</span><span class="sxs-lookup"><span data-stu-id="6f12a-164">These recovery points are used for “operational recovery".</span></span> <span data-ttu-id="6f12a-165">Azure 可做為具有較高 SLA 和保證可用性的良好離站位置。</span><span class="sxs-lookup"><span data-stu-id="6f12a-165">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="6f12a-166">**最佳作法**︰請確定 Azure 備份已排在使用 DPM 完成本機磁碟備份之後。</span><span class="sxs-lookup"><span data-stu-id="6f12a-166">**Best Practice**: Make sure that Azure Backups are scheduled after the completion of local disk backups using DPM.</span></span> <span data-ttu-id="6f12a-167">這可讓您將最新的磁碟備份複製到 Azure。</span><span class="sxs-lookup"><span data-stu-id="6f12a-167">This enables the latest disk backup to be copied to Azure.</span></span>

13. <span data-ttu-id="6f12a-168">選擇保留原則排程。</span><span class="sxs-lookup"><span data-stu-id="6f12a-168">Choose the retention policy schedule.</span></span> <span data-ttu-id="6f12a-169">如需保留原則運作方式的詳細資訊，請參閱 [使用 Azure 備份來取代您的磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)一文。</span><span class="sxs-lookup"><span data-stu-id="6f12a-169">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![保留原則](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="6f12a-171">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="6f12a-171">In this example:</span></span>

    * <span data-ttu-id="6f12a-172">每天下午 12:00 和下午 8:00 會進行一次備份 (螢幕的下半部) 並保留 180 天。</span><span class="sxs-lookup"><span data-stu-id="6f12a-172">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="6f12a-173">星期六下午 12:00 的備份</span><span class="sxs-lookup"><span data-stu-id="6f12a-173">The backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="6f12a-174">會保留 104 週</span><span class="sxs-lookup"><span data-stu-id="6f12a-174">is retained for 104 weeks</span></span>
    * <span data-ttu-id="6f12a-175">上星期六下午 12:00 的備份</span><span class="sxs-lookup"><span data-stu-id="6f12a-175">The backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="6f12a-176">會保留 60 週</span><span class="sxs-lookup"><span data-stu-id="6f12a-176">is retained for 60 months</span></span>
    * <span data-ttu-id="6f12a-177">三月份最後一個星期六下午 12:00 的備份</span><span class="sxs-lookup"><span data-stu-id="6f12a-177">The backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="6f12a-178">會保留 10 年</span><span class="sxs-lookup"><span data-stu-id="6f12a-178">is retained for 10 years</span></span>
14. <span data-ttu-id="6f12a-179">按一下 [下一步]  並選取適當的選項，以便將初始備份複本傳輸至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6f12a-179">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span></span> <span data-ttu-id="6f12a-180">您可以選擇 [自動透過網路] 或 [離線備份]。</span><span class="sxs-lookup"><span data-stu-id="6f12a-180">You can choose **Automatically over the network** or **Offline Backup**.</span></span>

    * <span data-ttu-id="6f12a-181">**自動透過網路** 會依據選擇的備份排程，將備份資料傳輸至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6f12a-181">**Automatically over the network** transfers the backup data to Azure as per the schedule chosen for backup.</span></span>
    * <span data-ttu-id="6f12a-182">[在 Azure 備份中離線備份工作流程](backup-azure-backup-import-export.md)說明 [離線備份] 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="6f12a-182">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span></span>

    <span data-ttu-id="6f12a-183">選擇相關的傳輸機制以將初始備份複本傳送至 Azure，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-183">Choose the relevant transfer mechanism to send the initial backup copy to Azure and click **Next**.</span></span>
15. <span data-ttu-id="6f12a-184">在 [摘要] 畫面中檢閱原則詳細資料後，按一下 [建立群組] 按鈕以完成工作流程。</span><span class="sxs-lookup"><span data-stu-id="6f12a-184">Once you review the policy details in the **Summary** screen, click on the **Create group** button to complete the workflow.</span></span> <span data-ttu-id="6f12a-185">您可以按一下 [關閉]  按鈕並在 [監視] 工作區中監視工作進度。</span><span class="sxs-lookup"><span data-stu-id="6f12a-185">You can click the **Close** button and monitor the job progress in Monitoring workspace.</span></span>

    ![保護群組的建立正在進行中](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="6f12a-187">SQL Server 資料庫的隨選備份</span><span class="sxs-lookup"><span data-stu-id="6f12a-187">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="6f12a-188">雖然先前的步驟建立了備份原則，但只有在第一次備份發生時，才會建立「復原點」。</span><span class="sxs-lookup"><span data-stu-id="6f12a-188">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span></span> <span data-ttu-id="6f12a-189">不需等待排程器開始作用，下列步驟會手動觸發復原點的建立。</span><span class="sxs-lookup"><span data-stu-id="6f12a-189">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span></span>

1. <span data-ttu-id="6f12a-190">建立復原點之前，請等到資料庫的保護群組狀態顯示 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="6f12a-190">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span></span>

    ![保護群組成員](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="6f12a-192">以滑鼠右鍵按一下資料庫，然後選取 [建立復原點] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-192">Right-click on the database and select **Create Recovery Point**.</span></span>

    ![建立線上復原點](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="6f12a-194">選擇下拉式功能表中的 [線上保護]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6f12a-194">Choose **Online Protection** in the drop-down menu and click **OK**.</span></span> <span data-ttu-id="6f12a-195">這會在 Azure 中開始建立復原點。</span><span class="sxs-lookup"><span data-stu-id="6f12a-195">This starts the creation of a recovery point in Azure.</span></span>

    ![建立復原點](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="6f12a-197">您可以在 [監視]  工作區中檢視作業進度，您可以在其中尋找進行中的作業 (如下圖中所描繪的作業)。</span><span class="sxs-lookup"><span data-stu-id="6f12a-197">You can view the job progress in the **Monitoring** workspace where you'll find an in progress job like the one depicted in the next figure.</span></span>

    ![監視主控台](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="6f12a-199">從 Azure 復原 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="6f12a-199">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="6f12a-200">以下是從 Azure 復原受保護的實體 (SQL Server 資料庫) 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="6f12a-200">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="6f12a-201">開啟 [DPM 伺服器管理主控台]。</span><span class="sxs-lookup"><span data-stu-id="6f12a-201">Open the DPM server Management Console.</span></span> <span data-ttu-id="6f12a-202">巡覽至 [復原]  工作區，您可以在此處查看 DPM 所備份的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6f12a-202">Navigate to **Recovery** workspace where you can see the servers backed up by DPM.</span></span> <span data-ttu-id="6f12a-203">瀏覽所需的資料庫 (在此例中為 ReportServer$MSDPM2012)。</span><span class="sxs-lookup"><span data-stu-id="6f12a-203">Browse the required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="6f12a-204">選取以 [線上] 結尾的 [復原自] 時間。</span><span class="sxs-lookup"><span data-stu-id="6f12a-204">Select a **Recovery from** time which ends with **Online**.</span></span>

    ![選取復原點](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="6f12a-206">以滑鼠右鍵按一下資料庫名稱，然後按一下 [復原]。</span><span class="sxs-lookup"><span data-stu-id="6f12a-206">Right-click the database name and click **Recover**.</span></span>

    ![從 Azure 復原](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="6f12a-208">DPM 會顯示復原點的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6f12a-208">DPM shows the details of the recovery point.</span></span> <span data-ttu-id="6f12a-209">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-209">Click **Next**.</span></span> <span data-ttu-id="6f12a-210">若要覆寫資料庫，請選取復原類型 [復原到原始的 SQL Server 執行個體] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-210">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span></span> <span data-ttu-id="6f12a-211">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-211">Click **Next**.</span></span>

    ![復原到原始位置](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="6f12a-213">在本例中，DPM 可讓資料庫復原至另一個 SQL server 執行個體或獨立的網路資料夾。</span><span class="sxs-lookup"><span data-stu-id="6f12a-213">In this example, DPM allows recovery of the database to another SQL Server instance or to a standalone network folder.</span></span>
4. <span data-ttu-id="6f12a-214">在 [指定復原選項]  畫面上，您可以選取 [網路頻寬使用節流設定] 等復原選項來進行復原所用頻寬的節流。</span><span class="sxs-lookup"><span data-stu-id="6f12a-214">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span></span> <span data-ttu-id="6f12a-215">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-215">Click **Next**.</span></span>
5. <span data-ttu-id="6f12a-216">在 [摘要]  畫面中，您會看到目前為止提供的所有復原組態。</span><span class="sxs-lookup"><span data-stu-id="6f12a-216">In the **Summary** screen, you see all the recovery configurations provided so far.</span></span> <span data-ttu-id="6f12a-217">按一下 [復原] 。</span><span class="sxs-lookup"><span data-stu-id="6f12a-217">Click **Recover**.</span></span>

    <span data-ttu-id="6f12a-218">[復原狀態] 會顯示正在復原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f12a-218">The Recovery status shows the database being recovered.</span></span> <span data-ttu-id="6f12a-219">您可以按一下 [關閉] 關閉精靈，並在 [監視] 工作區中檢視進度。</span><span class="sxs-lookup"><span data-stu-id="6f12a-219">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span></span>

    ![起始復原程序](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="6f12a-221">一旦完成復原，還原的資料庫會是應用程式一致複本。</span><span class="sxs-lookup"><span data-stu-id="6f12a-221">Once the recovery is completed, the restored database is application consistent.</span></span>

### <a name="next-steps"></a><span data-ttu-id="6f12a-222">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="6f12a-222">Next Steps:</span></span>
<span data-ttu-id="6f12a-223">•    [Azure 備份常見問題集](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6f12a-223">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
