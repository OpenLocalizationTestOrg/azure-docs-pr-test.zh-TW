---
title: "使用 DPM 進行 SQL Server 工作負載的 Azure 備份 | Microsoft Docs"
description: "使用 Azure 備份服務來備份 SQL Server 資料庫的簡介"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli
editor: 
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: c9edc066ea2edc9cd4b8453047d5584a588174dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-sql-server-to-azure-as-a-dpm-workload"></a><span data-ttu-id="798ad-103">將 SQL Server 備份至 Azure 做為 DPM 工作負載</span><span class="sxs-lookup"><span data-stu-id="798ad-103">Back up SQL Server to Azure as a DPM workload</span></span>
<span data-ttu-id="798ad-104">本文將引導您完成使用 Azure 備份來備份 SQL Server 資料庫的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="798ad-104">This article leads you through the configuration steps for backup of SQL Server databases using Azure Backup.</span></span>

<span data-ttu-id="798ad-105">若要將 SQL Server 資料庫備份至 Azure，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="798ad-105">To back up SQL Server databases to Azure, you need an Azure account.</span></span> <span data-ttu-id="798ad-106">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="798ad-106">If you don’t have an account, you can create a free trial account in just couple of minutes.</span></span> <span data-ttu-id="798ad-107">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="798ad-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="798ad-108">將 SQL Server 資料庫備份至 Azure 及從 Azure 復原的管理作業包含三個步驟：</span><span class="sxs-lookup"><span data-stu-id="798ad-108">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="798ad-109">建立備份原則以在 Azure 保護 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="798ad-109">Create a backup policy to protect SQL Server databases to Azure.</span></span>
2. <span data-ttu-id="798ad-110">在 Azure 建立隨選備份複本。</span><span class="sxs-lookup"><span data-stu-id="798ad-110">Create on-demand backup copies to Azure.</span></span>
3. <span data-ttu-id="798ad-111">從 Azure 復原資料庫。</span><span class="sxs-lookup"><span data-stu-id="798ad-111">Recover the database from Azure.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="798ad-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="798ad-112">Before you start</span></span>
<span data-ttu-id="798ad-113">開始之前，請確定符合使用 Microsoft Azure 備份保護工作負載的所有 [必要條件](backup-azure-dpm-introduction.md#prerequisites) 。</span><span class="sxs-lookup"><span data-stu-id="798ad-113">Before you begin, ensure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="798ad-114">必要條件涵蓋下列類似工作：建立備份保存庫、下載保存庫認證、安裝 Azure Backup Agent，以及向保存庫註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="798ad-114">The prerequisites cover tasks such as: creating a backup vault, downloading vault credentials, installing the Azure Backup Agent, and registering the server with the vault.</span></span>

## <a name="create-a-backup-policy-to-protect-sql-server-databases-to-azure"></a><span data-ttu-id="798ad-115">建立備份原則以在 Azure 保護 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="798ad-115">Create a backup policy to protect SQL Server databases to Azure</span></span>
1. <span data-ttu-id="798ad-116">在 DPM 伺服器上，按一下 [保護]  工作區。</span><span class="sxs-lookup"><span data-stu-id="798ad-116">On the DPM server, click the **Protection** workspace.</span></span>
2. <span data-ttu-id="798ad-117">在工具功能區中，按一下 [新增]  以建立新的保護群組。</span><span class="sxs-lookup"><span data-stu-id="798ad-117">On the tool ribbon, click **New** to create a new protection group.</span></span>

    ![建立保護群組](./media/backup-azure-backup-sql/protection-group.png)
3. <span data-ttu-id="798ad-119">DPM 會顯示開始畫面，其中包含建立 **保護群組**的指引。</span><span class="sxs-lookup"><span data-stu-id="798ad-119">DPM shows the start screen with the guidance on creating a **Protection Group**.</span></span> <span data-ttu-id="798ad-120">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-120">Click **Next**.</span></span>
4. <span data-ttu-id="798ad-121">選取 [伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-121">Select **Servers**.</span></span>

    ![選取保護群組類型 - 伺服器](./media/backup-azure-backup-sql/pg-servers.png)
5. <span data-ttu-id="798ad-123">展開要備份之資料庫所在的 SQL Server 電腦。</span><span class="sxs-lookup"><span data-stu-id="798ad-123">Expand the SQL Server machine where the databases to be backed up are present.</span></span> <span data-ttu-id="798ad-124">DPM 顯示可從該伺服器備份的各種資料來源。</span><span class="sxs-lookup"><span data-stu-id="798ad-124">DPM shows various data sources that can be backed up from that server.</span></span> <span data-ttu-id="798ad-125">展開 [所有 SQL 共用]  並選取要備份的資料庫 (在本例中我們選取 ReportServer$MSDPM2012 和 ReportServer$MSDPM2012TempDB)。</span><span class="sxs-lookup"><span data-stu-id="798ad-125">Expand the **All SQL Shares** and select the databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) to be backed up.</span></span> <span data-ttu-id="798ad-126">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-126">Click **Next**.</span></span>

    ![選取 SQL DB](./media/backup-azure-backup-sql/pg-databases.png)
6. <span data-ttu-id="798ad-128">提供保護群組的名稱，然後選取 [我想要線上保護]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="798ad-128">Provide a name for the protection group and select the **I want online Protection** checkbox.</span></span>

    ![資料保護方式 - 短期磁碟和線上 Azure](./media/backup-azure-backup-sql/pg-name.png)
7. <span data-ttu-id="798ad-130">在 [指定短期目標]  畫面中，包含建立磁碟備份點所需的輸入。</span><span class="sxs-lookup"><span data-stu-id="798ad-130">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk.</span></span>

    <span data-ttu-id="798ad-131">我們在此看到 [保留範圍] 設定為 [5 天]，[同步處理頻率] 設定為每隔 [15 分鐘]，這就是執行備份的頻率。</span><span class="sxs-lookup"><span data-stu-id="798ad-131">Here we see that **Retention range** is set to *5 days*, **Synchronization frequency** is set to once every *15 minutes* which is the frequency at which backup is taken.</span></span> <span data-ttu-id="798ad-132">[快速完整備份] 設定為 [下午 8:00]。</span><span class="sxs-lookup"><span data-stu-id="798ad-132">**Express Full Backup** is set to *8:00 P.M*.</span></span>

    ![短期目標](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="798ad-134">傳輸從前一天下午 8:00 備份點後修改的資料，即可在每天下午 8:00 PM (根據畫面輸入) 建立備份點。</span><span class="sxs-lookup"><span data-stu-id="798ad-134">At 8:00 PM (according to the screen input) a backup point is created every day by transferring the data that has been modified from the previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="798ad-135">這個程序稱為 [快速完整備份] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-135">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="798ad-136">雖然交易記錄檔每隔 15 分鐘同步處理一次，但如果有需要在下午 9:00 復原資料庫，則此點可藉由重新執行最後一個快速完整備份點 (在本例中為下午 8:00) 的記錄檔來建立。</span><span class="sxs-lookup"><span data-stu-id="798ad-136">While the transaction logs are synchronized every 15 minutes, if there is a need to recover the database at 9:00 PM – then the point is created by replaying the logs from the last express full backup point (8pm in this case).</span></span>
   >
   >

8. <span data-ttu-id="798ad-137">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="798ad-137">Click **Next**</span></span>

    <span data-ttu-id="798ad-138">DPM 會顯示可用的整體儲存空間和潛在的磁碟空間使用量。</span><span class="sxs-lookup"><span data-stu-id="798ad-138">DPM shows the overall storage space available and the potential disk space utilization.</span></span>

    ![磁碟配置](./media/backup-azure-backup-sql/pg-storage.png)

    <span data-ttu-id="798ad-140">依預設，DPM 會為每個資料來源 (SQL Server 資料庫) 建立一個磁碟區，以供初始備份複本之用。</span><span class="sxs-lookup"><span data-stu-id="798ad-140">By default, DPM creates one volume per data source (SQL Server database) which is used for the initial backup copy.</span></span> <span data-ttu-id="798ad-141">透過這個方法，邏輯磁碟管理員 (LDM) 會將 DPM 保護限制為 300 個資料來源 (SQL Server 資料庫)。</span><span class="sxs-lookup"><span data-stu-id="798ad-141">Using this approach, the Logical Disk Manager (LDM) limits DPM protection to 300 data sources (SQL Server databases).</span></span> <span data-ttu-id="798ad-142">若要因應這項限制，請選取 [將資料共置在 DPM 存放集區中] 選項。</span><span class="sxs-lookup"><span data-stu-id="798ad-142">To work around this limitation, select the **Co-locate data in DPM Storage Pool**, option.</span></span> <span data-ttu-id="798ad-143">如果您使用這個選項，DPM 會使用單一磁碟區來存放多個資料來源，讓 DPM 得以保護多達 2000 個 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="798ad-143">If you use this option, DPM uses a single volume for multiple data sources, which allows DPM to protect up to 2000 SQL databases.</span></span>

    <span data-ttu-id="798ad-144">如果您選取 [自動擴大磁碟區] 選項，DPM 將會負責隨著生產資料成長而增加備份磁碟區。</span><span class="sxs-lookup"><span data-stu-id="798ad-144">If **Automatically grow the volumes** option is selected, DPM can account for the increased backup volume as the production data grows.</span></span> <span data-ttu-id="798ad-145">如果您未選取 [自動擴大磁碟區]，DPM 會限制用於保護群組中資料來源的備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="798ad-145">If **Automatically grow the volumes** option is not selected, DPM limits the backup storage used to the data sources in the protection group.</span></span>
9. <span data-ttu-id="798ad-146">系統管理員可選擇手動 (關閉網路) 傳輸此初始備份，以避免頻寬壅塞或透過網路。</span><span class="sxs-lookup"><span data-stu-id="798ad-146">Administrators are given the choice of transferring this initial backup manually (off network) to avoid bandwidth congestion or over the network.</span></span> <span data-ttu-id="798ad-147">他們也可以設定可發生初始傳輸的時間。</span><span class="sxs-lookup"><span data-stu-id="798ad-147">They can also configure the time at which the initial transfer can happen.</span></span> <span data-ttu-id="798ad-148">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-148">Click **Next**.</span></span>

    ![初始複寫方法](./media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="798ad-150">初始備份複本要求將整個資料來源 (SQL Server 資料庫) 從生產伺服器 (SQL Server 電腦) 傳輸到 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="798ad-150">The initial backup copy requires transfer of the entire data source (SQL Server database) from production server (SQL Server machine) to the DPM server.</span></span> <span data-ttu-id="798ad-151">這些資料可能會很大，因此透過網路傳輸資料可能會超出頻寬。</span><span class="sxs-lookup"><span data-stu-id="798ad-151">This data might be large, and transferring the data over the network could exceed bandwidth.</span></span> <span data-ttu-id="798ad-152">基於這個理由，系統管理員可以選擇傳送初始備份的方式︰**手動** (使用卸除式媒體，可避免頻寬壅塞) 或**自動透過網路** (在指定時間)。</span><span class="sxs-lookup"><span data-stu-id="798ad-152">For this reason, administrators can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span></span>

    <span data-ttu-id="798ad-153">一旦完成初始備份，其餘的備份會是初始備份複本的增量備份。</span><span class="sxs-lookup"><span data-stu-id="798ad-153">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span></span> <span data-ttu-id="798ad-154">增量備份通常都非常小，因此有利於透過網路傳輸。</span><span class="sxs-lookup"><span data-stu-id="798ad-154">Incremental backups tend to be small and are easily transferred across the network.</span></span>
10. <span data-ttu-id="798ad-155">選擇是否想要執行一致性檢查，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-155">Choose when you want the consistency check to run and click **Next**.</span></span>

    ![一致性檢查](./media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="798ad-157">DPM 可以執行一致性檢查來檢查備份點的完整性。</span><span class="sxs-lookup"><span data-stu-id="798ad-157">DPM can perform a consistency check to check the integrity of the backup point.</span></span> <span data-ttu-id="798ad-158">它會計算生產伺服器 (在此案例中為 SQL Server 電腦) 上備份檔案的總和檢查碼以及 DPM 上該檔案的已備份資料。</span><span class="sxs-lookup"><span data-stu-id="798ad-158">It calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file at DPM.</span></span> <span data-ttu-id="798ad-159">在衝突的情況下，假設 DPM 上的備份檔案已損毀。</span><span class="sxs-lookup"><span data-stu-id="798ad-159">In the case of a conflict, it is assumed that the backed-up file at DPM is corrupt.</span></span> <span data-ttu-id="798ad-160">DPM 藉由傳送對應至總和檢查碼不符的區塊，改正已備份的資料。</span><span class="sxs-lookup"><span data-stu-id="798ad-160">DPM rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span></span> <span data-ttu-id="798ad-161">由於一致性檢查是效能密集作業，所以系統管理員可選擇排程一致性檢查或自動執行此作業。</span><span class="sxs-lookup"><span data-stu-id="798ad-161">As the consistency check is a performance-intensive operation, administrators have the option of scheduling the consistency check or running it automatically.</span></span>
11. <span data-ttu-id="798ad-162">若要指定資料來源的線上保護，請選取要送至 Azure 保護的資料庫，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-162">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span></span>

    ![選取資料來源](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. <span data-ttu-id="798ad-164">系統管理員可以選擇備份排程以及符合其組織原則的保留原則。</span><span class="sxs-lookup"><span data-stu-id="798ad-164">Administrators can choose backup schedules and retention policies that suit their organization policies.</span></span>

    ![排程和保留](./media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="798ad-166">在此範例中，每天下午 12:00 和下午 8:00 會進行一次備份 (螢幕的下半部)</span><span class="sxs-lookup"><span data-stu-id="798ad-166">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="798ad-167">建議您在磁碟上保留幾個短期復原點，以便快速復原。</span><span class="sxs-lookup"><span data-stu-id="798ad-167">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="798ad-168">這些復原點可用於「操作復原」。</span><span class="sxs-lookup"><span data-stu-id="798ad-168">These recovery points are used for “operational recovery".</span></span> <span data-ttu-id="798ad-169">Azure 可做為具有較高 SLA 和保證可用性的良好離站位置。</span><span class="sxs-lookup"><span data-stu-id="798ad-169">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="798ad-170">**最佳作法**︰請確定 Azure 備份已排在使用 DPM 完成本機磁碟備份之後。</span><span class="sxs-lookup"><span data-stu-id="798ad-170">**Best Practice**: Make sure that Azure Backups are scheduled after the completion of local disk backups using DPM.</span></span> <span data-ttu-id="798ad-171">這可讓您將最新的磁碟備份複製到 Azure。</span><span class="sxs-lookup"><span data-stu-id="798ad-171">This enables the latest disk backup to be copied to Azure.</span></span>

13. <span data-ttu-id="798ad-172">選擇保留原則排程。</span><span class="sxs-lookup"><span data-stu-id="798ad-172">Choose the retention policy schedule.</span></span> <span data-ttu-id="798ad-173">如需保留原則運作方式的詳細資訊，請參閱 [使用 Azure 備份來取代您的磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)一文。</span><span class="sxs-lookup"><span data-stu-id="798ad-173">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![保留原則](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="798ad-175">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="798ad-175">In this example:</span></span>

    * <span data-ttu-id="798ad-176">每天下午 12:00 和下午 8:00 會進行一次備份 (螢幕的下半部) 並保留 180 天。</span><span class="sxs-lookup"><span data-stu-id="798ad-176">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="798ad-177">星期六下午 12:00 的備份</span><span class="sxs-lookup"><span data-stu-id="798ad-177">The backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="798ad-178">會保留 104 週</span><span class="sxs-lookup"><span data-stu-id="798ad-178">is retained for 104 weeks</span></span>
    * <span data-ttu-id="798ad-179">上星期六下午 12:00 的備份</span><span class="sxs-lookup"><span data-stu-id="798ad-179">The backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="798ad-180">會保留 60 週</span><span class="sxs-lookup"><span data-stu-id="798ad-180">is retained for 60 months</span></span>
    * <span data-ttu-id="798ad-181">三月份最後一個星期六下午 12:00 的備份</span><span class="sxs-lookup"><span data-stu-id="798ad-181">The backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="798ad-182">會保留 10 年</span><span class="sxs-lookup"><span data-stu-id="798ad-182">is retained for 10 years</span></span>
14. <span data-ttu-id="798ad-183">按一下 [下一步]  並選取適當的選項，以便將初始備份複本傳輸至 Azure。</span><span class="sxs-lookup"><span data-stu-id="798ad-183">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span></span> <span data-ttu-id="798ad-184">您可以選擇 [自動透過網路] 或 [離線備份]。</span><span class="sxs-lookup"><span data-stu-id="798ad-184">You can choose **Automatically over the network** or **Offline Backup**.</span></span>

    * <span data-ttu-id="798ad-185">**自動透過網路** 會依據選擇的備份排程，將備份資料傳輸至 Azure。</span><span class="sxs-lookup"><span data-stu-id="798ad-185">**Automatically over the network** transfers the backup data to Azure as per the schedule chosen for backup.</span></span>
    * <span data-ttu-id="798ad-186">[在 Azure 備份中離線備份工作流程](backup-azure-backup-import-export.md)說明 [離線備份] 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="798ad-186">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span></span>

    <span data-ttu-id="798ad-187">選擇相關的傳輸機制以將初始備份複本傳送至 Azure，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-187">Choose the relevant transfer mechanism to send the initial backup copy to Azure and click **Next**.</span></span>
15. <span data-ttu-id="798ad-188">在 [摘要] 畫面中檢閱原則詳細資料後，按一下 [建立群組] 按鈕以完成工作流程。</span><span class="sxs-lookup"><span data-stu-id="798ad-188">Once you review the policy details in the **Summary** screen, click on the **Create group** button to complete the workflow.</span></span> <span data-ttu-id="798ad-189">您可以按一下 [關閉]  按鈕並在 [監視] 工作區中監視工作進度。</span><span class="sxs-lookup"><span data-stu-id="798ad-189">You can click the **Close** button and monitor the job progress in Monitoring workspace.</span></span>

    ![保護群組的建立正在進行中](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="798ad-191">SQL Server 資料庫的隨選備份</span><span class="sxs-lookup"><span data-stu-id="798ad-191">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="798ad-192">雖然先前的步驟建立了備份原則，但只有在第一次備份發生時，才會建立「復原點」。</span><span class="sxs-lookup"><span data-stu-id="798ad-192">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span></span> <span data-ttu-id="798ad-193">不需等待排程器開始作用，下列步驟會手動觸發復原點的建立。</span><span class="sxs-lookup"><span data-stu-id="798ad-193">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span></span>

1. <span data-ttu-id="798ad-194">建立復原點之前，請等到資料庫的保護群組狀態顯示 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="798ad-194">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span></span>

    ![保護群組成員](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="798ad-196">以滑鼠右鍵按一下資料庫，然後選取 [建立復原點] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-196">Right-click on the database and select **Create Recovery Point**.</span></span>

    ![建立線上復原點](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="798ad-198">選擇下拉式功能表中的 [線上保護]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="798ad-198">Choose **Online Protection** in the drop-down menu and click **OK**.</span></span> <span data-ttu-id="798ad-199">這會在 Azure 中開始建立復原點。</span><span class="sxs-lookup"><span data-stu-id="798ad-199">This starts the creation of a recovery point in Azure.</span></span>

    ![建立復原點](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="798ad-201">您可以在 [監視]  工作區中檢視作業進度，您可以在其中尋找進行中的作業 (如下圖中所描繪的作業)。</span><span class="sxs-lookup"><span data-stu-id="798ad-201">You can view the job progress in the **Monitoring** workspace where you'll find an in progress job like the one depicted in the next figure.</span></span>

    ![監視主控台](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="798ad-203">從 Azure 復原 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="798ad-203">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="798ad-204">以下是從 Azure 復原受保護的實體 (SQL Server 資料庫) 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="798ad-204">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="798ad-205">開啟 [DPM 伺服器管理主控台]。</span><span class="sxs-lookup"><span data-stu-id="798ad-205">Open the DPM server Management Console.</span></span> <span data-ttu-id="798ad-206">巡覽至 [復原]  工作區，您可以在此處查看 DPM 所備份的伺服器。</span><span class="sxs-lookup"><span data-stu-id="798ad-206">Navigate to **Recovery** workspace where you can see the servers backed up by DPM.</span></span> <span data-ttu-id="798ad-207">瀏覽所需的資料庫 (在此例中為 ReportServer$MSDPM2012)。</span><span class="sxs-lookup"><span data-stu-id="798ad-207">Browse the required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="798ad-208">選取以 [線上] 結尾的 [復原自] 時間。</span><span class="sxs-lookup"><span data-stu-id="798ad-208">Select a **Recovery from** time which ends with **Online**.</span></span>

    ![選取復原點](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="798ad-210">以滑鼠右鍵按一下資料庫名稱，然後按一下 [復原]。</span><span class="sxs-lookup"><span data-stu-id="798ad-210">Right-click the database name and click **Recover**.</span></span>

    ![從 Azure 復原](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="798ad-212">DPM 會顯示復原點的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="798ad-212">DPM shows the details of the recovery point.</span></span> <span data-ttu-id="798ad-213">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-213">Click **Next**.</span></span> <span data-ttu-id="798ad-214">若要覆寫資料庫，請選取復原類型 [復原到原始的 SQL Server 執行個體] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-214">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span></span> <span data-ttu-id="798ad-215">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-215">Click **Next**.</span></span>

    ![復原到原始位置](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="798ad-217">在本例中，DPM 可讓資料庫復原至另一個 SQL server 執行個體或獨立的網路資料夾。</span><span class="sxs-lookup"><span data-stu-id="798ad-217">In this example, DPM allows recovery of the database to another SQL Server instance or to a standalone network folder.</span></span>
4. <span data-ttu-id="798ad-218">在 [指定復原選項]  畫面上，您可以選取 [網路頻寬使用節流設定] 等復原選項來進行復原所用頻寬的節流。</span><span class="sxs-lookup"><span data-stu-id="798ad-218">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span></span> <span data-ttu-id="798ad-219">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-219">Click **Next**.</span></span>
5. <span data-ttu-id="798ad-220">在 [摘要]  畫面中，您會看到目前為止提供的所有復原組態。</span><span class="sxs-lookup"><span data-stu-id="798ad-220">In the **Summary** screen, you see all the recovery configurations provided so far.</span></span> <span data-ttu-id="798ad-221">按一下 [復原] 。</span><span class="sxs-lookup"><span data-stu-id="798ad-221">Click **Recover**.</span></span>

    <span data-ttu-id="798ad-222">[復原狀態] 會顯示正在復原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="798ad-222">The Recovery status shows the database being recovered.</span></span> <span data-ttu-id="798ad-223">您可以按一下 [關閉] 關閉精靈，並在 [監視] 工作區中檢視進度。</span><span class="sxs-lookup"><span data-stu-id="798ad-223">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span></span>

    ![起始復原程序](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="798ad-225">一旦完成復原，還原的資料庫會是應用程式一致複本。</span><span class="sxs-lookup"><span data-stu-id="798ad-225">Once the recovery is completed, the restored database is application consistent.</span></span>

### <a name="next-steps"></a><span data-ttu-id="798ad-226">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="798ad-226">Next Steps:</span></span>
<span data-ttu-id="798ad-227">•    [Azure 備份常見問題集](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="798ad-227">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
