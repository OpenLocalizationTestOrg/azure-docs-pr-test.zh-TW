---
title: "針對使用 Azure 備份伺服器的 SQL Server 工作負載的 aaaAzure 備份 |Microsoft 文件"
description: "使用 Azure 備份伺服器的 SQL Server 資料庫簡介 toobacking"
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
ms.openlocfilehash: 3a94338e8aca3f9d8611a72bcd223397ffb96f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-with-azure-backup-server"></a><span data-ttu-id="3ff1f-103">備份 SQL Server tooAzure 與 Azure 備份伺服器</span><span class="sxs-lookup"><span data-stu-id="3ff1f-103">Back up SQL Server tooAzure With Azure Backup Server</span></span>
<span data-ttu-id="3ff1f-104">這篇文章會引導您完成 hello 組態步驟，使用 Microsoft Azure 備份伺服器 (MABS) 的 SQL Server 資料庫的備份。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-104">This article leads you through hello configuration steps for backup of SQL Server databases using Microsoft Azure Backup Server (MABS).</span></span>

<span data-ttu-id="3ff1f-105">SQL Server 資料庫備份 tooAzure 和復原，從 Azure 的 hello 管理包含三個步驟：</span><span class="sxs-lookup"><span data-stu-id="3ff1f-105">hello management of SQL Server database backup tooAzure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="3ff1f-106">建立備份原則 tooprotect SQL Server 資料庫 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-106">Create a backup policy tooprotect SQL Server databases tooAzure.</span></span>
2. <span data-ttu-id="3ff1f-107">建立備份副本，視 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-107">Create on-demand backup copies tooAzure.</span></span>
3. <span data-ttu-id="3ff1f-108">從 Azure 復原 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-108">Recover hello database from Azure.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3ff1f-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="3ff1f-109">Before you start</span></span>
<span data-ttu-id="3ff1f-110">開始之前，請確定您有[安裝並準備好 Azure 備份伺服器 hello](backup-azure-microsoft-azure-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-110">Before you begin, ensure that you have [installed and prepared hello Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a><span data-ttu-id="3ff1f-111">建立備份原則 tooprotect SQL Server 資料庫 tooAzure</span><span class="sxs-lookup"><span data-stu-id="3ff1f-111">Create a backup policy tooprotect SQL Server databases tooAzure</span></span>
1. <span data-ttu-id="3ff1f-112">在 hello Azure 備份伺服器 UI 中，按一下 hello**保護**工作區。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-112">On hello Azure Backup Server UI, click hello **Protection** workspace.</span></span>
2. <span data-ttu-id="3ff1f-113">在 hello 工具功能區中，按一下 **新增**toocreate 新的保護群組。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-113">On hello tool ribbon, click **New** toocreate a new protection group.</span></span>

    ![建立保護群組](./media/backup-azure-backup-sql/protection-group.png)
3. <span data-ttu-id="3ff1f-115">MABS 顯示 hello 指南 hello [開始] 畫面上建立**保護群組**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-115">MABS shows hello start screen with hello guidance on creating a **Protection Group**.</span></span> <span data-ttu-id="3ff1f-116">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-116">Click **Next**.</span></span>
4. <span data-ttu-id="3ff1f-117">選取 [伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-117">Select **Servers**.</span></span>

    ![選取保護群組類型 - 伺服器](./media/backup-azure-backup-sql/pg-servers.png)
5. <span data-ttu-id="3ff1f-119">展開 hello 存在 hello 資料庫 toobe 備份所在的 SQL Server 電腦。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-119">Expand hello SQL Server machine where hello databases toobe backed up are present.</span></span> <span data-ttu-id="3ff1f-120">MABS 會顯示可從該伺服器備份的各種資料來源。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-120">MABS shows various data sources that can be backed up from that server.</span></span> <span data-ttu-id="3ff1f-121">展開 hello**所有 SQL 共用**選取 hello 選取的資料庫 （在此情況下我們 ReportServer$ MSDPM2012 和 ReportServer$ MSDPM2012TempDB） toobe 備份。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-121">Expand hello **All SQL Shares** and select hello databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) toobe backed up.</span></span> <span data-ttu-id="3ff1f-122">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-122">Click **Next**.</span></span>

    ![選取 SQL DB](./media/backup-azure-backup-sql/pg-databases.png)
6. <span data-ttu-id="3ff1f-124">提供 hello 保護群組的名稱，並選取 hello**我要執行線上保護**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-124">Provide a name for hello protection group and select hello **I want online Protection** checkbox.</span></span>

    ![資料保護方式 - 短期磁碟和線上 Azure](./media/backup-azure-backup-sql/pg-name.png)
7. <span data-ttu-id="3ff1f-126">在 hello**指定短期目標**畫面上，包括 hello 必要輸入 toocreate 備份點 toodisk。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-126">In hello **Specify Short-Term Goals** screen, include hello necessary inputs toocreate backup points toodisk.</span></span>

    <span data-ttu-id="3ff1f-127">我們在這裡看到的**保留範圍**設定得*5 天*，**同步處理頻率**tooonce 設定每個*15 分鐘*即 hello取得備份的頻率。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-127">Here we see that **Retention range** is set too*5 days*, **Synchronization frequency** is set tooonce every *15 minutes* which is hello frequency at which backup is taken.</span></span> <span data-ttu-id="3ff1f-128">**快速完整備份**設定得*8:00 P.M.*。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-128">**Express Full Backup** is set too*8:00 P.M*.</span></span>

    ![短期目標](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="3ff1f-130">下午 8:00 （依據 toohello 螢幕輸入） 備份點由每日傳送 hello hello 資料已修改的前一天的下午 8:00 備份點。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-130">At 8:00 PM (according toohello screen input) a backup point is created every day by transferring hello data that has been modified from hello previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="3ff1f-131">這個程序稱為 [快速完整備份] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-131">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="3ff1f-132">Hello 交易記錄檔會同步處理時，則會重新顯示 hello hello 記錄檔建立 hello 點，如果在下午 9:00 – 需要 toorecover hello 資料庫每隔 15 分鐘上一次快速完整備份點 (在此情況下的 8 pm)。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-132">While hello transaction logs are synchronized every 15 minutes, if there is a need toorecover hello database at 9:00 PM – then hello point is created by replaying hello logs from hello last express full backup point (8pm in this case).</span></span>
   >
   >

8. <span data-ttu-id="3ff1f-133">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="3ff1f-133">Click **Next**</span></span>

    <span data-ttu-id="3ff1f-134">MABS 顯示 hello 可用的整體儲存空間和 hello 潛在磁碟空間使用量。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-134">MABS shows hello overall storage space available and hello potential disk space utilization.</span></span>

    ![磁碟配置](./media/backup-azure-backup-sql/pg-storage.png)

    <span data-ttu-id="3ff1f-136">根據預設，MABS 會建立一個磁碟區，每個資料來源 （SQL Server 資料庫） 是用於 hello 初始備份複本。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-136">By default, MABS creates one volume per data source (SQL Server database) which is used for hello initial backup copy.</span></span> <span data-ttu-id="3ff1f-137">Hello 邏輯磁碟管理員 (LDM) 會使用這個方法，限制 MABS 保護 too300 資料來源 （SQL Server 資料庫）。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-137">Using this approach, hello Logical Disk Manager (LDM) limits MABS protection too300 data sources (SQL Server databases).</span></span> <span data-ttu-id="3ff1f-138">這項限制，選取 hello toowork **DPM 存放集區中的資料共置**，選項。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-138">toowork around this limitation, select hello **Co-locate data in DPM Storage Pool**, option.</span></span> <span data-ttu-id="3ff1f-139">如果您使用此選項，MABS 會使用單一磁碟區的多個資料來源，可讓 MABS tooprotect too2000 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-139">If you use this option, MABS uses a single volume for multiple data sources, which allows MABS tooprotect up too2000 SQL databases.</span></span>

    <span data-ttu-id="3ff1f-140">如果**自動擴大 hello 磁碟區**選取選項，則 hello 實際執行資料隨著 MABS 可以考量增加 hello 備份磁碟區。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-140">If **Automatically grow hello volumes** option is selected, MABS can account for hello increased backup volume as hello production data grows.</span></span> <span data-ttu-id="3ff1f-141">如果**自動擴大 hello 磁碟區**選項並未選取，MABS 限制 hello 備份儲存體使用 toohello hello 保護群組中的資料來源。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-141">If **Automatically grow hello volumes** option is not selected, MABS limits hello backup storage used toohello data sources in hello protection group.</span></span>
9. <span data-ttu-id="3ff1f-142">Hello 選擇的傳輸此初始備份以手動方式 （網路） 關閉 tooavoid 頻寬壅塞或 hello 網路時，會給予系統管理員。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-142">Administrators are given hello choice of transferring this initial backup manually (off network) tooavoid bandwidth congestion or over hello network.</span></span> <span data-ttu-id="3ff1f-143">他們也可以設定初始區域轉送，可以發生在哪一個 hello hello 時間。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-143">They can also configure hello time at which hello initial transfer can happen.</span></span> <span data-ttu-id="3ff1f-144">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-144">Click **Next**.</span></span>

    ![初始複寫方法](./media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="3ff1f-146">hello 初始備份複本需要從生產伺服器 （SQL Server 機器） tooMABS 傳送 hello 整個資料來源 （SQL Server 資料庫）。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-146">hello initial backup copy requires transfer of hello entire data source (SQL Server database) from production server (SQL Server machine) tooMABS.</span></span> <span data-ttu-id="3ff1f-147">這項資料可能會很大，並透過 hello 網路傳輸的 hello 資料可能會超出頻寬。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-147">This data might be large, and transferring hello data over hello network could exceed bandwidth.</span></span> <span data-ttu-id="3ff1f-148">基於這個理由，系統管理員可以選擇 tootransfer hello 初始備份：**手動**（使用卸除式媒體） tooavoid 頻寬壅塞或**自動透過網路 hello** （在指定時間）。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-148">For this reason, administrators can choose tootransfer hello initial backup: **Manually** (using removable media) tooavoid bandwidth congestion, or **Automatically over hello network** (at a specified time).</span></span>

    <span data-ttu-id="3ff1f-149">Hello 初始備份完成之後，請 hello rest 的 hello 備份是增量備份 hello 初始備份複本。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-149">Once hello initial backup is complete, hello rest of hello backups are incremental backups on hello initial backup copy.</span></span> <span data-ttu-id="3ff1f-150">增量備份通常 toobe 小，而且可輕鬆地轉移 hello 網路上。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-150">Incremental backups tend toobe small and are easily transferred across hello network.</span></span>
10. <span data-ttu-id="3ff1f-151">選擇當您想 hello 一致性檢查 toorun，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-151">Choose when you want hello consistency check toorun and click **Next**.</span></span>

    ![一致性檢查](./media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="3ff1f-153">MABS 可以執行一致性檢查 toocheck hello 的完整性 hello 備份點。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-153">MABS can perform a consistency check toocheck hello integrity of hello backup point.</span></span> <span data-ttu-id="3ff1f-154">它會計算 hello 備份檔案的 hello 實際執行伺服器 （在此案例中的 SQL Server 電腦） 和 hello 備份資料用於該檔案在 MABS hello 總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-154">It calculates hello checksum of hello backup file on hello production server (SQL Server machine in this scenario) and hello backed-up data for that file at MABS.</span></span> <span data-ttu-id="3ff1f-155">在發生衝突的 hello 情況下，它會假設該 hello 在 MABS 備份檔案已損毀。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-155">In hello case of a conflict, it is assumed that hello backed-up file at MABS is corrupt.</span></span> <span data-ttu-id="3ff1f-156">MABS 改正了 hello 備份資料，藉由傳送嗨區塊對應 toohello 總和檢查碼不符。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-156">MABS rectifies hello backed-up data by sending hello blocks corresponding toohello checksum mismatch.</span></span> <span data-ttu-id="3ff1f-157">因為 hello 一致性檢查的效能密集作業，管理員可以在 hello 選擇的排程 hello 一致性檢查或自動執行它。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-157">As hello consistency check is a performance-intensive operation, administrators have hello option of scheduling hello consistency check or running it automatically.</span></span>
11. <span data-ttu-id="3ff1f-158">toospecify hello 多數目的資料來源的線上保護，選取 hello 資料庫 toobe 受保護的 tooAzure 和按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-158">toospecify online protection of hello datasources, select hello databases toobe protected tooAzure and click **Next**.</span></span>

    ![選取資料來源](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. <span data-ttu-id="3ff1f-160">系統管理員可以選擇備份排程以及符合其組織原則的保留原則。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-160">Administrators can choose backup schedules and retention policies that suit their organization policies.</span></span>

    ![排程和保留](./media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="3ff1f-162">在此範例中，備份每天進行一次在下午 12:00 和下午 8 （囉 」 畫面中的下半部）</span><span class="sxs-lookup"><span data-stu-id="3ff1f-162">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of hello screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="3ff1f-163">它是很好的作法 toohave 少數的短期復原點，在磁碟上，以便快速復原。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-163">It’s a good practice toohave a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="3ff1f-164">這些復原點可用於「操作復原」。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-164">These recovery points are used for “operational recovery".</span></span> <span data-ttu-id="3ff1f-165">Azure 可做為具有較高 SLA 和保證可用性的良好離站位置。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-165">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="3ff1f-166">**最佳作法**： 請確定 Azure 備份已排定 hello 使用 DPM 的本機磁碟備份完成後。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-166">**Best Practice**: Make sure that Azure Backups are scheduled after hello completion of local disk backups using DPM.</span></span> <span data-ttu-id="3ff1f-167">這可讓最新磁碟複製備份 toobe tooAzure hello。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-167">This enables hello latest disk backup toobe copied tooAzure.</span></span>

13. <span data-ttu-id="3ff1f-168">選擇 hello 保留原則排程。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-168">Choose hello retention policy schedule.</span></span> <span data-ttu-id="3ff1f-169">在提供 hello hello 保留原則的運作方式的詳細資訊[使用 Azure Backup tooreplace 您磁帶基礎結構的文章](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-169">hello details on how hello retention policy works are provided at [Use Azure Backup tooreplace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![保留原則](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="3ff1f-171">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="3ff1f-171">In this example:</span></span>

    * <span data-ttu-id="3ff1f-172">備份在下午 12:00 和下午 8 （下半部囉 」 畫面） 是一天一次，並且會保留為 180 天。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-172">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of hello screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="3ff1f-173">星期六的下午 12:00 的 hello 備份</span><span class="sxs-lookup"><span data-stu-id="3ff1f-173">hello backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="3ff1f-174">會保留 104 週</span><span class="sxs-lookup"><span data-stu-id="3ff1f-174">is retained for 104 weeks</span></span>
    * <span data-ttu-id="3ff1f-175">最後一個星期六的下午 12:00 的 hello 備份</span><span class="sxs-lookup"><span data-stu-id="3ff1f-175">hello backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="3ff1f-176">會保留 60 週</span><span class="sxs-lookup"><span data-stu-id="3ff1f-176">is retained for 60 months</span></span>
    * <span data-ttu-id="3ff1f-177">在最後一個星期六的下午 12:00 的 3 月 hello 備份</span><span class="sxs-lookup"><span data-stu-id="3ff1f-177">hello backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="3ff1f-178">會保留 10 年</span><span class="sxs-lookup"><span data-stu-id="3ff1f-178">is retained for 10 years</span></span>
14. <span data-ttu-id="3ff1f-179">按一下**下一步**和選取 hello 傳送嗨初始備份複本 tooAzure 適當的選項。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-179">Click **Next** and select hello appropriate option for transferring hello initial backup copy tooAzure.</span></span> <span data-ttu-id="3ff1f-180">您可以選擇**自動透過網路 hello**或**離線備份**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-180">You can choose **Automatically over hello network** or **Offline Backup**.</span></span>

    * <span data-ttu-id="3ff1f-181">**自動透過網路 hello**傳輸 hello 依據 hello 排程備份選擇的備份資料 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-181">**Automatically over hello network** transfers hello backup data tooAzure as per hello schedule chosen for backup.</span></span>
    * <span data-ttu-id="3ff1f-182">[在 Azure 備份中離線備份工作流程](backup-azure-backup-import-export.md)說明 [離線備份] 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-182">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span></span>

    <span data-ttu-id="3ff1f-183">選擇 hello 相關傳輸機制 toosend hello 初始備份複本 tooAzure 按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-183">Choose hello relevant transfer mechanism toosend hello initial backup copy tooAzure and click **Next**.</span></span>
15. <span data-ttu-id="3ff1f-184">一旦您檢閱 hello 原則詳細資料，在 hello**摘要**畫面上，按一下 hello**建立群組**按鈕 toocomplete hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-184">Once you review hello policy details in hello **Summary** screen, click on hello **Create group** button toocomplete hello workflow.</span></span> <span data-ttu-id="3ff1f-185">您可以按一下 hello**關閉**在 [監視] 工作區的按鈕和監視器 hello 工作進度。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-185">You can click hello **Close** button and monitor hello job progress in Monitoring workspace.</span></span>

    ![保護群組的建立正在進行中](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="3ff1f-187">SQL Server 資料庫的隨選備份</span><span class="sxs-lookup"><span data-stu-id="3ff1f-187">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="3ff1f-188">當 hello 先前的步驟建立備份原則時，hello 第一次備份，就會發生時，才建立的復原點 」。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-188">While hello previous steps created a backup policy, a “recovery point” is created only when hello first backup occurs.</span></span> <span data-ttu-id="3ff1f-189">而不是等待中的 hello 排程器 tookick，hello 步驟觸發程序 hello 建立復原點以手動方式。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-189">Rather than waiting for hello scheduler tookick in, hello steps below trigger hello creation of a recovery point manually.</span></span>

1. <span data-ttu-id="3ff1f-190">等待 hello 保護群組狀態顯示**確定**hello 資料庫，再建立 hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-190">Wait until hello protection group status shows **OK** for hello database before creating hello recovery point.</span></span>

    ![保護群組成員](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="3ff1f-192">Hello 資料庫上按一下滑鼠右鍵，然後選取**建立復原點**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-192">Right-click on hello database and select **Create Recovery Point**.</span></span>

    ![建立線上復原點](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="3ff1f-194">選擇**線上保護**hello 下拉式選單中按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-194">Choose **Online Protection** in hello drop-down menu and click **OK**.</span></span> <span data-ttu-id="3ff1f-195">這是在 Azure 中啟動 hello 建立復原點。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-195">This starts hello creation of a recovery point in Azure.</span></span>

    ![建立復原點](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="3ff1f-197">您可以檢視 hello 工作進度中 hello**監視**工作區，您可以在其中找到正在進行中作業，像是 hello hello 下圖所示的其中一個。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-197">You can view hello job progress in hello **Monitoring** workspace where you'll find an in progress job like hello one depicted in hello next figure.</span></span>

    ![監視主控台](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="3ff1f-199">從 Azure 復原 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="3ff1f-199">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="3ff1f-200">hello 下列步驟是必要的 toorecover 從 Azure 的受保護實體 （SQL Server 資料庫）。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-200">hello following steps are required toorecover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="3ff1f-201">開啟 hello DPM 伺服器管理主控台。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-201">Open hello DPM server Management Console.</span></span> <span data-ttu-id="3ff1f-202">瀏覽過**復原**您可以在其中看到 hello 伺服器工作區由 DPM 備份。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-202">Navigate too**Recovery** workspace where you can see hello servers backed up by DPM.</span></span> <span data-ttu-id="3ff1f-203">瀏覽 hello 必要的資料庫 （在此案例 ReportServer$ MSDPM2012)。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-203">Browse hello required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="3ff1f-204">選取以 [線上] 結尾的 [復原自] 時間。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-204">Select a **Recovery from** time which ends with **Online**.</span></span>

    ![選取復原點](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="3ff1f-206">Hello 資料庫名稱上按一下滑鼠右鍵，然後按一下**復原**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-206">Right-click hello database name and click **Recover**.</span></span>

    ![從 Azure 復原](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="3ff1f-208">DPM 會顯示 hello hello 復原點詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-208">DPM shows hello details of hello recovery point.</span></span> <span data-ttu-id="3ff1f-209">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-209">Click **Next**.</span></span> <span data-ttu-id="3ff1f-210">toooverwrite hello 資料庫中，選取 hello 復原類型**復原 toooriginal SQL Server 執行個體**。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-210">toooverwrite hello database, select hello recovery type **Recover toooriginal instance of SQL Server**.</span></span> <span data-ttu-id="3ff1f-211">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-211">Click **Next**.</span></span>

    ![復原 tooOriginal 位置](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="3ff1f-213">在此範例中，DPM 可讓復原的 hello 資料庫 tooanother SQL Server 執行個體或 tooa 獨立網路 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-213">In this example, DPM allows recovery of hello database tooanother SQL Server instance or tooa standalone network folder.</span></span>
4. <span data-ttu-id="3ff1f-214">在 [hello**指定復原選項**] 畫面上，您可以選取 hello 復原選項，例如網路頻寬使用節流設定使用復原 toothrottle hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-214">In hello **Specify Recovery options** screen, you can select hello recovery options like Network bandwidth usage throttling toothrottle hello bandwidth used by recovery.</span></span> <span data-ttu-id="3ff1f-215">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-215">Click **Next**.</span></span>
5. <span data-ttu-id="3ff1f-216">在 hello**摘要**畫面上，看到所有的 hello 復原設定，提供到目前為止。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-216">In hello **Summary** screen, you see all hello recovery configurations provided so far.</span></span> <span data-ttu-id="3ff1f-217">按一下 [復原] 。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-217">Click **Recover**.</span></span>

    <span data-ttu-id="3ff1f-218">hello 復原狀態會顯示 hello 資料庫恢復中。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-218">hello Recovery status shows hello database being recovered.</span></span> <span data-ttu-id="3ff1f-219">您可以按一下**關閉**tooclose hello 精靈和檢視 hello 進度中 hello**監視**工作區。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-219">You can click **Close** tooclose hello wizard and view hello progress in hello **Monitoring** workspace.</span></span>

    ![起始復原程序](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="3ff1f-221">Hello 復原完成後，hello 還原資料庫是一致的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ff1f-221">Once hello recovery is completed, hello restored database is application consistent.</span></span>

### <a name="next-steps"></a><span data-ttu-id="3ff1f-222">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="3ff1f-222">Next Steps:</span></span>
<span data-ttu-id="3ff1f-223">•    [Azure 備份常見問題集](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3ff1f-223">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
